---
layout: post
title:  "DX11 Collisions"
date:   2019-02-18 18:29:09 +0000
categories: 
description: Collision demo using DX11 framework
imageSRC: /data/dx11collision.png
tag: post
---

* C++
* DX11 Framework
* Physics
* ImGui

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/yxcNzC-Scq0" frameborder="0" margin-left="auto" margin-right="auto" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

## Bounding Volume Hierarchy
One of the biggest systems used in this project is the Bounding Volume Hierarchy (BVH). It’s a system used to avoid testing each sphere with each triangle of the mesh, also, as the mesh is static it’s only generated once, not each frame. All the triangles are saved in a binary tree so each sphere has to test very few boxes instead of each triangle. 

### Generation
Let’s assume that we begin with a vector where we hold all the triangles information. Each triangle will be in a random position in space, so the first step is to find out on which axis are mostly distributed. For this we get the max and minimum coordinate of each triangle and we save the maximum and the minimum global coordinates in a “Node”. 
Once we got the longest axis (in the example X > Y) we sort all the triangles by their position on that axis on the vector. The next step is to divide that vector from the half and generate two new “Nodes” and attach them as left and right child of the parent Node, now we can iterate this algorithm with the new nodes and the half size vectors.
  
![BVH][BVH-Construction]

This way instead of a complexity of O(n) (linear with the number of triangles) we have a O(Log2(l) + 1) being l the number of triangles we have (and assuming the best case were a sphere only collides with one triangle, which should be the usual case).


### Analysis Sphere-BVH

The analysis algorithms is quite simple, we begin with a sphere and a node, root node in this case. We begin the algorithms pushing that first node to a std stack, and we continue executing the algorithm while the stack is not empty. We get top node from the stack (removing it from there) and using the triangle vector min and max coordinates we saved before with each node (note here we are not saving the vectors, just the coordinates) we can generate an Axis Aligned Bounding Box and test it against the sphere, if they don’t collide we do nothing, if they do collide we need to know if that node is a leaf node.
If is not we add to the stack this node’s childs (left and right) to analyse later. Otherwise we have a node whose box is colliding with the sphere and it’s a leaf. So we do triangle-sphere test. If it collides we save this collision information.

### Physics system
The physics system used on this project is the one from the book “Games Physics Cookbook” and it’s divided in four parts, collision detection, collision solving, rigid body updates, sinking solving. 
In the first part we detect sphere-triangle and sphere-sphere collisions, the first ones using the bounding volume hierarchy, but the second one using brute force algorithms. The reason I am using brute force on sphere-sphere detection is that it seems to be faster than using other acceleration algorithms such as bounding volumes. Even if the complexity of brute forcing them is **n * (n-1)/2**, being n the number of spheres, this might be because detecting sphere to sphere collisions is a really simple algorithm. 
The second part, the collision solving, uses the functions from “Games Physics Cookbook” and the data vectors we generated in the detection phase. This is executed in three parts, detecting if the bodies are approaching one to the other, solving velocities and solving friction. 
The next step, the update, only happens with the spheres, here is where we apply velocity and acceleration to the spheres and we move their positions. 
Finally, the last step, the sinking solving, tries to fix those sphere which are sinking in a triangle or in another sphere. This step moves directly the spheres positions so they don’t sink in the floor or in other spheres. 

### Performance
I am able to use up to 1600 spheres in stable 60fps and up to 2300 in stable 30fps. This could be improved by sending collision detection functions to other threads for example. (Intel i7-7700 Nvidia 1060 6Gb)



[BVH-Construction]: /data/BVHConstruction.png