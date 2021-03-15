```c++
#include <iostream>
#include <sstream>
#include <string>
#include <array>
#include <boost/asio.hpp>

constexpr short multicast_port = 30001;

class messenger
{
public:
    messenger(boost::asio::io_context& io_context,
        const boost::asio::ip::address& listen_address,
        const boost::asio::ip::address& multicast_address)
        : transmit_endpoint_(multicast_address, multicast_port),
        receive_endpoint_(listen_address, multicast_port),
        transmit_socket_(io_context, transmit_endpoint_.protocol()),
        receive_socket_(io_context),
        nickname_("noname")
    {
        // Set a nickname
        std::cout << "Welcome! Please input your nickname: ";
        std::getline(std::cin, nickname_);

        // Create the socket so that multiple may be bound to the same address.
        receive_socket_.open(receive_endpoint_.protocol());
        receive_socket_.set_option(boost::asio::ip::udp::socket::reuse_address(true));
        receive_socket_.bind(receive_endpoint_);

        // Join the multicast group.
        receive_socket_.set_option(
            boost::asio::ip::multicast::join_group(multicast_address));

        do_receive();
    }

    void do_send(std::string line)
    {
        message_ = line;
        do_transmit();
    }

private:
    void do_transmit()
    {
        std::ostringstream os;

        os << nickname_ << ": " << message_;
        message_ = os.str();

        transmit_socket_.async_send_to(
            boost::asio::buffer(message_), transmit_endpoint_,
            [this](boost::system::error_code ec, std::size_t /*length*/)
            {
                // pass
            });
    }

    void do_receive()
    {
        receive_socket_.async_receive_from(
            boost::asio::buffer(data_), receive_endpoint_,
            [this](boost::system::error_code ec, std::size_t length)
            {
                if (!ec)
                {
                    std::cout.write(data_.data(), length);
                    std::cout << std::endl;

                    do_receive();
                }
            });
    }

private:
    boost::asio::ip::udp::endpoint transmit_endpoint_;
    boost::asio::ip::udp::endpoint receive_endpoint_;
    boost::asio::ip::udp::socket transmit_socket_;
    boost::asio::ip::udp::socket receive_socket_;
    std::string nickname_;
    std::string message_;
    std::array<char, 1024> data_;
};


int main(int argc, char* argv[])
{
    try
    {
        boost::asio::io_context io_context;
        std::string listen_address_raw = "0.0.0.0";
        std::string multicast_address_raw = "239.255.0.1";

        messenger s(io_context,
            boost::asio::ip::make_address(listen_address_raw),
            boost::asio::ip::make_address(multicast_address_raw));

        std::thread t([&io_context]() { io_context.run(); });

        std::string line;
        while (std::getline(std::cin, line))
        {
            s.do_send(line);
        }

        t.join();
    }
    catch (std::exception& e)
    {
        std::cerr << "Exception: " << e.what() << "\n";
    }

    return 0;
}
```
