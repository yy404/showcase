# Using NPC Manager System

## Overview

[The NPC Manager System](https://www.unrealengine.com/marketplace/en-US/product/npc-manager-system) 
is a product provided by the Unreal Engine marketplace.

I mainly made 3 contributions, by using it in a Third-Person Action Role-Playing Game project (cooperated with 10+ team members).

## 1. Workflow Documentation

The workflow of using NPC Manager System was documented, based on its [video tutorials](https://www.youtube.com/watch?v=vZ2Svyb1vio&list=PLziQlhUd357hXTKzhm_U5WswPrbJbVRRO).

This document was used to report weekly to the project leader.

[Document Available Online as Google Doc](https://docs.google.com/document/d/1iXxkULiVVd8wTTEx0adqSmqz9vc8MzKe12o9aDRWOKQ/edit)

## 2. Scene Prototype 

A scene prototype was created as a demonstration, for the team artists who want to make characters act like they are at a club.
* Objective: Create a simple nightclub with NPCs milling around, watching stages, sitting and chatting, etc.
* Scene: A club with a bar, several stripper stages, booths, and a mezzanine (overlook) area with stairs.
* Extra: Try to make it look like a popular, packed bar.

Reference: ["UE4: What is BSP and When Should You Use It?" Tutorial by World of Level Design](https://www.worldofleveldesign.com/categories/ue4/bsp-01-what-is-bsp.php)
 
***Club Scene Prototype (26s Video):***

[![Club Scene Prototype](http://img.youtube.com/vi/3V_RR_bHeis/0.jpg)](http://www.youtube.com/watch?v=3V_RR_bHeis "Club Scene Prototype")

Screenshot (Club Scene)
![Screenshot (Club Scene)](pics/pic1.png "Screenshot (Club Scene)")

## 3. Scripts Development

Scripts were developed for NPC locomotions using layered animations. 

This enables a custom task for walking with upper-body montages (e.g. talking/smoking).

References: 
* ["BP 3rd Person Game" Tutorial Series by Unreal Engine](https://www.youtube.com/watch?v=hRO82u1phyw&list=PLhf5YCdusazmDTAEdV5jDhKWeGE1iqF2X)
* ["Using Layered Animations" Unreal Engine 4 Documentation](https://docs.unrealengine.com/en-US/AnimatingObjects/SkeletalMeshAnimation/AnimHowTo/AdditiveAnimations/index.html)
* ["Custom Logic" Tutorial of NPC Manager](https://www.youtube.com/watch?v=e5femnMekSg)

***Locomotions with Upper-Body Montages (30s Video):***

[![Locomotions with Upper-Body Montages](http://img.youtube.com/vi/0CJ4hmiWiMI/0.jpg)](http://www.youtube.com/watch?v=0CJ4hmiWiMI "Locomotions with Upper-Body Montages")

Screenshot (Main Logic for Locomotions)
![Screenshot (Main Logic for Locomotions)](pics/pic2.png "Screenshot (Main Logic for Locomotions)")

Screenshot (Animation Blueprints for Locomotions)
![Screenshot (Animation Blueprints for Locomotions)](pics/pic3.png "Screenshot (Animation Blueprints for Locomotions)")
