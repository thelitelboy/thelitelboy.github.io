---
layout: post
title:  "First 3D Engine"
date:   2018-06-17 18:29:09 +0000
categories: 
description: A 3D game engine using C++ and OpenGL
imageSRC: /data/3DEngine-Shadows.png
tag: post
---

### Details
<div style="display: inline-block; margin-right: 20px;">
  <div style="display: inline-block;">
    <ul>
      <li>C++</li>
      <li>Windows</li>
      <li>OpenGL 3.X</li>
      <li>GLFW</li>
      <li>Forward Rendering</li>
    </ul>
  </div>
  <div style="display: inline-block; vertical-align: top;">
    <ul>
      <li>Oclussion Culling</li>
      <li>Lightning</li>
      <li>PBR</li>
      <li>Bullet</li>
      <li>ImGui</li>
    </ul>
  </div>
</div>
<br>


This is the first 3D Game engine I have done, written in C++, multithread and using OpenGL. It has been developed by [Xavier Rebasa Moll][XAVI-Link] and me in our last year on [ESAT][ESAT-Link].

### Rendering

We use a forward rendering to render the scene. Each object is added to a list if it has to be rendered and at the end of the frame, each object of the list will be rendered directly.

![Viewport][PE-ViewPort]

### Lighting and Shadows

Our engine can process up to 64 point lights, 32 spot lights and 8 directional lights. Only directional lights cast shadows. Each one generates a depth texture from the position and orientation of the node holding the point light, then sends that information as a texture2D to the shader to render shadows. 

![Shadows][PE-Shadows]

### Occlusion Culling

We make use of OpenGL queries to use the occlusion culling. If any object to render has at least one visible pixel it will be rendered, else it will be ignored. 

### Physically based rendering (PBR)

One of the elements that I am most proud of in this engine is the PBR. This means trying to render materials according to their physical properties. It was really hard to learn what it was exactly and understand what the code was doing, because the Rendering Equation is quite heavy and I did not want to just copy paste and see it work.

![PBR][PE-PBR]

![Material][PE-Material]

### External Libraries

* #### ImGui
A User Interface library. Really usefull and easy to use. This is not the first time I have worked with this library, It gives really good results in the projects for debuging purposes.

  * [GitHub][PE-ImGui-Github]

![ImGui][PE-ImGui] 

* #### Bullet
A physics library. Really interesting how it works with a private "world" where everything is calculated in another thread and it's your job to synchronize it with your world.

  * [GitHub][PE-Bullet-Github]

### References to learn how to work with OpenGL
* [LearnOpenGL][PE-LearnOpenGL]
* [OpenGL Tutorials][PE-OpenGLTutorials]



[ESAT-Link]: http://www.esat.es
[XAVI-Link]: https://www.linkedin.com/in/xavier-rebasa-moll-b5723715b/
[PE-ViewPort]: /data/3DEngine-Viewport.png
[PE-Shadows]: /data/3DEngine-Shadows.png

[PE-PBR]: /data/pbr.png
[PE-Material]: /data/Material.png

[PE-ImGui]: /data/ImGui.png
[PE-ImGui-Github]: http://www.github.com/ocornut/imgui
[PE-Bullet-Github]: https://github.com/bulletphysics/bullet3

[PE-LearnOpenGL]: https://learnopengl.com/
[PE-OpenGLTutorials]: http://www.opengl-tutorial.org/