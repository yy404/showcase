# Intro
[SFML](https://www.sfml-dev.org/) is a C++ library for a simple application programming interface to various multimedia components in computers.

Timberman is a 2D retro-style casual game, where the player controls a timberman (left/right arrow keys) to chop a tree and dodge branches.

The game was built from scratch using the SFML library, based on the ["Learning Path: C++ Game Programming"](https://www.udemy.com/course/learning-path-c-game-programming/) course.

![Timberman demo gif](pics/TimbermanGif.gif)

# Motivation
[The original tutorial code](https://github.com/yy404/showcase/blob/main/SFML/TutorialCode.md) is straightforward to implement the Timberman gameplay. 

It is great to learn SFML for the first time, but the code is less ***reusable*** and ***extensible***.

[By rewriting the code base](https://github.com/yy404/Timber/tree/master/Code), I made it as a more general engine for similar games based on 2D sprites.

# Contributions
There are two key contributions: abstracting game actors and organising the game loop.

## Abstracting game actors

**Observation**: creating similar things *repetitively*, and drawing each sprite *manually*.
```c++
// From the original tutorial code file

...

// Prepare the player
sf::Texture texturePlayer;
texturePlayer.loadFromFile(resourcePath() + "graphics/player.png");
sf::Sprite spritePlayer;
spritePlayer.setTexture(texturePlayer);
spritePlayer.setPosition(580, 720);

// Prepare the gravestone
sf::Texture textureRIP;
textureRIP.loadFromFile(resourcePath() + "graphics/rip.png");
sf::Sprite spriteRIP;
spriteRIP.setTexture(textureRIP);
spriteRIP.setPosition(600, 860);

// Prepare the axe
sf::Texture textureAxe;
textureAxe.loadFromFile(resourcePath() + "graphics/axe.png");
sf::Sprite spriteAxe;
spriteAxe.setTexture(textureAxe);
spriteAxe.setPosition(700, 830);
    
// And more repetitions ...

...

// Draw the player
window.draw(spritePlayer);

// Draw the gravestone
window.draw(spriteRIP);

// Draw the axe
window.draw(spriteAxe);

// And more repetitions ...

...
```

**Solution**: abstracting game actors as an Actor class base.
```c++
// Actor.cpp

#include "Actor.hpp"

// Define a static vector to record all actors
std::vector<Actor*> Actor::actorPtrVector;

Actor::Actor(std::string spritePath) : speedX(0.0f), speedY(0.0f), isHidden(false)
{
    // Set the sprite given the full path of a texture 
    std::string fullPath = resourcePath() + spritePath;
    if (texture.loadFromFile(fullPath))
    {
        sprite.setTexture(texture);
    }

    // Record the pointer of this actor
    Actor::actorPtrVector.push_back(this);
}

...

void Actor::drawActors(sf::RenderWindow& window)
{
    // Draw the sprite of all actors
    for (auto actorPtr : Actor::actorPtrVector)
    {
        if (actorPtr != nullptr && !actorPtr->isHidden)
        {
            window.draw(actorPtr->getSprite());
        }
    }
}

...
```

## Organising the game loop

**Observation and solution**: dividing functionalities of the Timberman game into 6 classes: 

GameEngine, GameUI, GameManager, Actor, Tree(Actor), Player(Actor).

```c++
// main.cpp
#include "GameEngine.hpp"
int main()
{
    GameEngine gameEngine;
    gameEngine.run();
    return EXIT_SUCCESS;
}
```
```c++
// GameEngine.cpp
...
void GameEngine::run()
{
    // Start the game loop
    while (window.isOpen())
    {
        input();
        update();
        draw();
    }
}
...
```
```c++
// GameEngine.hpp
#pragma once
#include <SFML/Graphics.hpp>
#include "GameUI.hpp"
#include "GameManager.hpp"
#include "Actor.hpp"
#include "Tree.hpp"
#include "Player.hpp"

class GameEngine
{
public:
    GameEngine();
    void run();
    
private:
    void input();
    void update();
    void draw();
    
    sf::RenderWindow window;
    float windowWidth;
    float windowHeight;

    GameUI gameUI;
    GameManager gameManager;

    Actor background;
    Tree tree;
    Player player;
};
```
