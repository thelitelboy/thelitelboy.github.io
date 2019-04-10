---
layout: post
title:  "DX11 Animations"
date:   2018-11-17 18:29:09 +0000
categories: 
description: Animation System using DX11 rendering
imageSRC: /data/dx11animation.png
tag: post
---

### Details
* C++
* Windows
* DirectX11
* State machines

![DX11Animation][DX11-DX11Animation]

## Hierarchical Class

A new class has been created to create the hierarchy, called Node. It has a secondary class Called SubNode which represents the bones of the hierarchy. Each Node contains a vector of SubNodes and a vector with the information of each SubNode parent. 

The SubNodes has another class called Transform, which is responsible for calculating the global and local matrix of itself. The node also holds a transform. 

All this organised in this way to use the flat tree model in the bone transform, where each parent is before its children, that way we only have to update the SubNodes Transforms once each frame following the vector. I have used this model to avoid doing multiple loops for updating all the transforms and because it’s the easiest way to update all the global matrixes consecutively, just looping the vector once. 
 
![Node][DX11-Node]

Subnodes also load the .x file to have its mesh. So as I don’t want to replicate the robot information I’m loading one skeleton and the robots are just saving a pointer to the meshes. This way all the information is loaded just once. Key Frame Animation System.

## Animation System & Blending System

The animation class which holds the information of all the animation for one bone in each aspect (Position, Rotation in X-axis, Rotation in Y-axis, Rotation in Z-axis) using four vectors, and it exact animation times for each keyframe.  Key Frame is a small struct which holds its type (again a position or a rotation in one of the three axes) on an enumeration, a float value with the time and a vector4 for the value. Keyframe also has two overloaded operators to handle with them in an easier way. 
The second class is the Animation Manager, which holds a map of animations and its names. One animation for each bone of the Collada file loaded. It also holds a map of maximum durations for each animation. This class holds all the animations loaded but it gets the current animation state information from the class which wants to be animated. For example, current animation time, if the current animation is blending or not, the skeleton (Node pointer) to be animated…
Play should be executed once per frame per each object who wants to be animated. The play function is quite complex but in summary, it calculates with the animation time in the middle of what keyframes we are and lerps the current animation with the necessary alpha value. 
 
![Animation][DX11-Animation]


If we are blending from one animation to another the calculus is more complex, it also calculates in the middle of what keyframes we are in the secondary animation and it does a linear interpolation between the current and next animation lerped values. 

Also, play function adds the specified time to the animation, we are currently passing 0.016 as the time between frames, which means 60 frames per second. To slow down or accelerate animation we can multiply that value. It should receive the real in-between frame time but in this case, I’m not doing that calculus. 

Each animation has an option to don’t be looping. When we call the robot’s PlayAnimation function we can specify the blending duration and if we want the animation to be looping. In the case, we don’t want the animation to loop we use a small trick, once the animation time is higher than the animation duration instead of returning the animation time to zero we hold it on the animation duration value. That way the animation holds static on the last keyframe. 

One of the main problems once the animation system is complete is the information replication, we don’t want to load many animation files for each robot we summon. So I am creating an animation manager on the Application and constructing the robots with a reference to the animation manager. That’s why the play function takes so many arguments. 

Anyway, the animation processing is quite heavy to process so once many robots are using it the framerate falls. It could be more efficient if we save most of the Key Frames so we only have to read, not to calculate anything. But also this would have an enormous cost of memory.

[DX11-DX11Animation]: /data/dx11animation.png
[DX11-Node]: /data/NodeDX11.png
[DX11-Animation]: /data/animation.png