# Light Gun Shooter Game

## Intro

Full Metal Exorcist is intended to be a game in the form of a horror light gun game inspired by the House of the Dead and Resident Evil light gun games. 
It is a one-player game where the player stars as a Robocop-like non-human robot exorcist, controlled remotely by a human priest, that goes through a variety of locations “exorcising” spiritual and demonic enemies with a series of guns and simple cinematic actions. 

***Work-In-Progress Mini Demo Preview (Video in 22s):***

[![Video Link of Mini Demo Preview](http://img.youtube.com/vi/er8fd8DuEs4/0.jpg)](http://www.youtube.com/watch?v=er8fd8DuEs4 "Video Link of Mini Demo Preview")


## Milestone Planning

*Note: the bold-italic font indicating DONE*

|        | Mini Demo <br /> (Single Room) | Full Demo <br /> (Single Level) | Full Game <br /> (More Levels) |
| ------ | ----------------------- | ------------------------ | ----------------------- |
| System | ***Menu (start/pause/end)*** <br /> ***HUD (crosshair/text)*** <br /> ***Audio (weapon)*** | Menu (options/credits) <br /> HUD (image/effects) <br /> Audio (SFX/BGM) | Menu (modes) <br /> Checkpoints <br /> Cinematic |
| Shooter | ***Player Movement*** <br /> ***Player Stats*** (score) <br /> ***Weapon*** (***reload***/damage) | Player Orientation <br /> Weapon (splash/accuracy) <br /> Weapon (switch/auto) | Weapon (penetration) <br /> Weapon (bullet/missile) <br /> Weapon (bomb) |
| Shootable | ***Enemy Spawner (pop up)*** <br /> ***Enemy AI (chasing)*** <br /> Enemy Attack (physical) <br /> Enemy Health/***Destroy***  | Enemy AI (in distance) <br /> Enemy Attack (magical) <br /> Animations/Particles <br /> Items | Enemy (Objects) <br /> Enemy (Boss) <br /> Hidden items/rooms  <br /> Hit box|

### Done
* Player movement: the player's location automatically changes along a spline; the start/stop can be triggered by custom events. 
* Enemy spawner: a spawner generate an enemy at the spawner location; the spawner's tag binds it with a segment of the spline.
* Enemy AI: simply chasing the player based on NavMesh. 
* Player shooting: left click to eliminate an enemy and right click to refill ammo; three placeholder audio files for shooting/reloading/no-ammo. 
* UI: widgets for basic menu ("TAB" key to toggle pause) and gameplay information; one placeholder crosshair image for the mouse cursor.

