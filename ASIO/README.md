[Boost.Asio](https://www.boost.org/doc/libs/1_75_0/doc/html/boost_asio.html) is a C++ library for network and low-level I/O programming.

One of its [official examples](https://www.boost.org/doc/libs/1_75_0/doc/html/boost_asio/examples/cpp11_examples.html) shows the use of multicast to transmit packets to a group of subscribers.
This official multicast example includes two programs: 
[receiver.cpp](https://www.boost.org/doc/libs/1_75_0/doc/html/boost_asio/example/cpp11/multicast/receiver.cpp) 
and [sender.cpp](https://www.boost.org/doc/libs/1_75_0/doc/html/boost_asio/example/cpp11/multicast/sender.cpp)
.

The following Multicast Messenger program is inspired by the official multicast example.
It works as a transceiver which integrates the functionalities of transmitting and receiving packets.
Given a multicast address, this messenger program provides a local chat room without relying a specific server.

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
        std::cout << "Hello " << nickname_ << "! You can chat now!" << std::endl;

        // Create the socket so that multiple may be bound to the same address.
        receive_socket_.open(receive_endpoint_.protocol());
        receive_socket_.set_option(boost::asio::ip::udp::socket::reuse_address(true));
        receive_socket_.bind(receive_endpoint_);

        // Join the multicast group.
        receive_socket_.set_option(
            boost::asio::ip::multicast::join_group(multicast_address));

        // Listen to receive data
        do_receive();
    }
    
    ~messenger()
    {
        std::cout << "Destructor of the messenger class." << std::endl;
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
    std::string message_; // the message to send
    std::array<char, 1024> data_; // the data received
};


int main(int argc, char* argv[])
{
    try
    {
        // All programs that use asio need to have at least one I/O execution context.
        // An I/O execution context provides access to I/O functionality.
        boost::asio::io_context io_context;
        
        // "0.0.0.0" means listen on every available network interface in this contex
        std::string listen_address_raw = "0.0.0.0"; 
        
        // The multicast addresses range from 239.0.0.0 to 239.255.255.255 are the administratively scoped addresses.
        // They would be considered local, not globally unique, 
        // and can be reused in domains administered by different organizations. 
        std::string multicast_address_raw = "239.255.0.1"; 

        // Construct a new messenger
        messenger s(io_context,
            boost::asio::ip::make_address(listen_address_raw),
            boost::asio::ip::make_address(multicast_address_raw));

        // Use thread t for io_context
        std::thread t([&io_context]() { io_context.run(); });

        // Get and send messages
        std::string line;
        while (std::getline(std::cin, line))
        {
            s.do_send(line);
        }

        // Terminate thread t
        t.join();
    }
    catch (std::exception& e)
    {
        std::cerr << "Exception: " << e.what() << "\n";
    }

    return 0;
}
```
