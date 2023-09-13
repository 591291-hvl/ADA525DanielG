---
layout: post
title:  "Assignment 02: 3D print."
date:   2023-08-25 14:00:00 +0200
categories: Assignment
---

## List of content


## Background 

This assignment requires design and 3D-printing of multiple parts that combine in some way. So for this assignment i am attempting to create a decoratively stand on my desk that rotates a cubic object. Idealy in a slow and aesthetically pleasing way. 


Background for this project is that i 3D-printed the third iteration of a fractal cube and i thought it looked cool so i wanted some way to have it as decoration. Since i have a leftover motor from a arduino startet kit i thought it could be of use. 


## Design 

The idea is based around attaching the cube to the motor and somehow fixing it all in place so it spins perpendicular to the ground. Therefore i would need some sort of stand that encases an arduino (for motor controll), and the motor. Since the cube is going to spin pointy side up, the stand should resemble a pyramid for symmetry. 

The individual parts should include a pyramid with space inside for an arduino and motor, idealy an opening for power supply. A attachment piece for the motor shaft. 


### Motor Shaft

<img src="{{ '/assets/images/motor_shaft.jpg' | prepend: site.baseurl | prepend: site.url}}" alt="Motor Shaft" height=400px/>

Image of the different design iterations of the motor shaft.

The first few iterations was focused on trying to create a part that fit onto the motor shaft. The shaft has a cog attached to the end which has 10 teeth. The design of this part proved to be a big challenge as i am still not sure how much spacing is required between the gear and the connecting piece. Spacing used in final versions is 0.4mm but i have had prints were i have had to use a knife to make the part fit, while other times it fit too loose. The depth of the connecting also ended having to be very precise.

The part that is supposed to hold the cube also went through multiple iterations. The connecting part to gear slots needed to have larger surface area to prevent the parts from disconnecting at high speed. Also the holder for the cube needs to be large enough to prevent the cube from flying out.

ROTATION
There also were problems with constructing the motor shaft in fusion360. Apparently rotating a cubic object to face pointy side up is not a 45degree rotation in 2 axis. The rotations was told should work are x = 145, y = 0, z = 45 but i ended up with x=45, y=325, z=0. So the solution i came up with is just to add 90 to 55 until its correct. Mathematically it should be arctan(1/sqrt(2)) which is 35.264. 90-55 is 35, so if 55 does not work try 35.264.


### Stand

Since the stand was going to be a pyramid, i started by constructing a square then using the "loft" function to raise it to a point above the square, this results in a pyramid. From then i began digging out space for the motor and arduino, as well as a hole for power supply.

<img src="{{ '/assets/images/stand.gif' | prepend: site.baseurl | prepend: site.url}}" alt="Motor Shaft" height=400px/>