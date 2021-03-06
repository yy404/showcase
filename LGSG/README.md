# Light Gun Shooter Game

## Intro

Full Metal Exorcist is intended to be a game in the form of a horror light gun game inspired by the House of the Dead and Resident Evil light gun games. 
It is a one-player game where the player stars as a Robocop-like non-human robot exorcist, controlled remotely by a human priest, that goes through a variety of locations “exorcising” spiritual and demonic enemies with a series of guns and simple cinematic actions. 

*Contributions: I'm a programmer, cooperating with a level designer and an artist.*

***Work-In-Progress Preview Video (37s):***

[![Video Link of Mini Demo Preview](http://img.youtube.com/vi/FnAuh5XTzfY/0.jpg)](https://youtu.be/FnAuh5XTzfY "Video Link of Mini Demo Preview")

Demo Level (Making by Teammates):
![Demo Level Making by Teammates](https://i.imgur.com/ieK8H9j.jpeg "Demo Level Making by Teammates")

## Milestone Planning

*Note: the bold-italic font indicating DONE*

|        | Mini Demo <br /> (Single Room) | Full Demo <br /> (Single Level) | Full Game <br /> (More Levels) |
| ------ | ----------------------- | ------------------------ | ----------------------- |
| System | ***Menu (start/pause/end)*** <br /> ***HUD (crosshair/text)*** <br /> ***Audio (weapon)*** | Menu (options/credits) <br /> HUD (image/effects) <br /> Audio (SFX/BGM) | Menu (modes) <br /> Checkpoints <br /> Cinematic |
| Shooter | ***Player Movement*** <br /> ***Player Stats (score)*** <br /> ***Weapon (reload/damage)*** | Player Orientation <br /> Weapon (splash/accuracy) <br /> Weapon (switch/auto) | Weapon (penetration) <br /> Weapon (bullet/missile) <br /> Weapon (bomb) |
| Shootable | ***Enemy Spawner (pop up)*** <br /> ***Enemy AI (chasing)*** <br /> ***Enemy Attack (physical)*** <br /> Enemy Health/***Destroy***  | Enemy AI (in distance) <br /> Enemy Attack (magical) <br /> Animations/Particles <br /> Items | Enemy (Objects) <br /> Enemy (Boss) <br /> Hidden items/rooms  <br /> Hit box|

### Key Features Done
* System: 
  * Menu: widgets for basic menu ("TAB" key to toggle pause).
  * HUD: health, ammo, score, crosshair cursor.
  * Damage feedback: camera shake, red screen, hit sound.
* Shooter (Player) 
  * Movement: the player's location automatically changes along a spline; the start/stop can be triggered by custom events. 
  * Shooting: left click to eliminate an enemy and right click to refill ammo; audio files for shooting/reloading/no-ammo.
  * Orientation: using spline's tangent to set the rotation of camera pawn.
* Shootable (Enemy)
  * Spawner: a spawner generate an enemy at the spawner location; the spawner's tag binds it with a segment of the spline.
  * AI: chase the player based on NavMesh, and stop moving when attack the player.
  * Damage: each EnemyCharacter has a box volume as the damage trigger (periodically damaging player when it overlaps with the player capsule volume).


## References

### Perforce on AWS
* ["Getting Started with Amazon Web Services"](https://aws.amazon.com/getting-started/)
* ["Perforce: How To Deploy Helix Core on AWS"](https://www.perforce.com/webinars/vcs/how-deploy-helix-core-aws)
* ["Setting Up Perforce: How to Install Helix Core on AWS"](https://www.perforce.com/products/helix-core/install-helix-core-on-aws#tab-panel-43116)
* ["Populating Perforce With An Unreal Engine Source Build"](https://allarsblog.com/2017/04/05/populating-perforce-with-an-unreal-engine-source-build/)

### Unreal Engine Basics
* ["Understanding the Basics" Unreal Engine 4 Documentation](https://docs.unrealengine.com/en-US/Basics/index.html)
* ["Programming Quick Start" Unreal Engine 4 Documentation](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/ProgrammingWithCPP/CPPProgrammingQuickStart/index.html)
* ["C++ Programming Tutorials" Unreal Engine 4 Documentation](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/ProgrammingWithCPP/CPPTutorials/index.html)
* ["Blueprints Quick Start Guide" Unreal Engine 4 Documentation](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/Blueprints/QuickStart/index.html)

### Tutorials
* ["Blueprints - Essential Concepts" Unreal Online Learning](https://www.unrealengine.com/en-US/onlinelearning-courses/blueprints---essential-concepts)
* ["Converting Blueprints to C++" Unreal Online Learning](https://www.unrealengine.com/en-US/onlinelearning-courses/converting-blueprints-to-c)
* ["Twin Stick Shooter with Blueprints" Unreal Online Learning](https://www.unrealengine.com/en-US/onlinelearning-courses/twin-stick-shooter-with-blueprints)
* ["LightGun Arcade Shooters - Unreal Engine Tutorial (Part 1 - Shooting)"](https://www.youtube.com/watch?v=ydrl5WNvlW8)
* ["Arcade Lightgun Shooters - Unreal Engine Tutorial (Part 2 - Spline Camera Movement)"](https://www.youtube.com/watch?v=HzDbcM22mig)

### Standards
* ["Coding Standard" Unreal Engine 4 Documentation](https://docs.unrealengine.com/en-US/ProductionPipelines/DevelopmentSetup/CodingStandard/index.html)
* ["Gamemakin UE4 Style Guide"](https://github.com/Allar/ue4-style-guide) 

### Miscellaneous
* ["Engine/BasicShapes/Cube versus StarterContent/Shape_Cube differences"](https://forums.unrealengine.com/development-discussion/content-creation/1816442-engine-basicshapes-cube-versus-startercontent-shape_cube-differences)
* ["Spawning/Destroying an Actor Overview" Unreal Engine 4 Documentation](https://docs.unrealengine.com/en-US/Gameplay/HowTo/SpawnAndDestroyActors/Blueprints/index.html)
* ["How to make character move along spline with input keys"](https://answers.unrealengine.com/questions/900011/how-to-make-character-move-along-spline-with-input.html)

