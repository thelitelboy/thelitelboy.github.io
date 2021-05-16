---
layout: post
title:  "Unity Experiments"
date:   2020-09-01
categories: 
description: Multiple experiments tested on Unity 3D
imageSRC: /data/raymarching.png
tag: post
---

2020-2021 Has been an interesting time, lots of time to stay at home so now and then I have been experimenting with different concepts at Unity3D

* [Boids][Boids-Link]
* [Ray Marching][RM-Link]
* [Inverse Kinemetics][IK-Link]

[Boids-Link]: #boids
[RM-Link]: #ray-marching
[IK-Link]: #inverse-kinematics

## **Boids**
One of the first things I wanted to play with was Boids, a kind of AI used to simulate flocking behaviors of birds or fish. It´s amazing how complex behaviors can appear with such simple rules and playing with different weights for each one.

* **Separation:** Avoid staying too close to other bodies
* **Alignment:** Look towards the average heading of other bodies
* **Cohesion:** Try to stay as close to the center of mass of nearby bodies as possible.

Also, I experimented with compute shaders for the first time to see how many boids could I handle. 

<blockquote class="twitter-tweet"><p lang="und" dir="ltr"><a href="https://t.co/A6RUI7VGbI">pic.twitter.com/A6RUI7VGbI</a></p>&mdash; Imanol Saenz (@The_LitelBoy) <a href="https://twitter.com/The_LitelBoy/status/1231213738780495872?ref_src=twsrc%5Etfw">February 22, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script> 

<p style="margin-bottom: 75px"></p>

## **Ray Marching**

Ray marching is an amazing technique where if you have an equation to define a certain shape you can draw it. 
It consists of going forward from the camera to all screen points step by step and detecting on each step if we are inside the surface, or in more technical words check on each step if the Signed Distance Function gives a negative value.

This means that if we can define an equation or a signed distance function to any shape we can draw it. It´s also possible to use constructive solid geometry, which is an amazing technique. We can use multiple SDFs to create different shapes, using intersection, union, or difference. For example, we can create a cube with a hole on it using the SDFs of a cube and a cylinder and getting their difference (basically the max between the distance of the cube and the negative distance of the cylinder).

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Thanks to <a href="https://twitter.com/SebastianLague?ref_src=twsrc%5Etfw">@SebastianLague</a> coding adventures I started plaing around with <a href="https://twitter.com/hashtag/raymarching?src=hash&amp;ref_src=twsrc%5Etfw">#raymarching</a>. Pretty happy with the result 😁. <a href="https://twitter.com/hashtag/screenshotsaturday?src=hash&amp;ref_src=twsrc%5Etfw">#screenshotsaturday</a> <a href="https://t.co/X5l3Em9v5b">pic.twitter.com/X5l3Em9v5b</a></p>&mdash; Imanol Saenz (@The_LitelBoy) <a href="https://twitter.com/The_LitelBoy/status/1236309677140586496?ref_src=twsrc%5Etfw">March 7, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script> 

<p style="margin-bottom: 75px"></p>

## **Inverse Kinematics**

Inverse kinematics is complicated, it´s a simple concept, you have a target point and you want your "arm" to reach it, So you calculate all the joint angles according to that point. It doesn't matter how many joints you have, you can just keep updating the next joint according to all the previous ones. 

In this case, I didn't want to have just a robotic hand performing the IK so I decided to try a spider. Maybe I should have chosen any other animal, with fewer legs so it´s easier but I thought a spider would be fun, and at least it´s not a centipede. 

I´ll be working on this spider every now and then because I want it to walk in walls and try to make it feel nice to move around.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">I´ve been playing around with <a href="https://twitter.com/hashtag/IK?src=hash&amp;ref_src=twsrc%5Etfw">#IK</a> and it´s all starting to come together :) Next step, walking nicely on walls. If anyone wants to start with Inverse kinematics allow me one small tip, start with two legs, but I wanted a spider!!<a href="https://twitter.com/hashtag/screenshotsaturday?src=hash&amp;ref_src=twsrc%5Etfw">#screenshotsaturday</a> <a href="https://t.co/JXWLtQbVeE">pic.twitter.com/JXWLtQbVeE</a></p>&mdash; Imanol Saenz (@The_LitelBoy) <a href="https://twitter.com/The_LitelBoy/status/1393597183455338503?ref_src=twsrc%5Etfw">May 15, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script> 