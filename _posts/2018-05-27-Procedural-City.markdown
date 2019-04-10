---
layout: post
title:  "Procedural City"
date:   2018-05-27 18:29:09 +0000
categories: 
description: First Approach to OpenGL
imageSRC: /data/Procedural-City.png
tag: post
---

### Details
* C++
* Windows
* OpenGL

This is my first approach to OpenGL, the exercise was to generate a "procedural City" so we rendered many boxes with building textures and other boxes (scalen in Y) so they look like floor. In my case I generated some City Centers, and after some iterations where there was very probable to appear a building if there is another one near the city looked like a real one, more or less. I also implemented algorithms to place roads, trees and fountains around the buildings, althought everything was made of cubes. We also worked with many interesting things, such as skyboxes, post processes, frame buffers...

![Procedural City Image][PC-ProceduralCity]


[PC-ProceduralCity]: /data/Procedural-City.png "Procedural City"