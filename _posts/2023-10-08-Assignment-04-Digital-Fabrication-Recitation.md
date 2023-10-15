---
layout: post
title:  "Assignment 04: Digital Fabrication Recitation"
date:   2023-12-24 14:00:00 +0200
categories: Assignment
--- 

# Digital fabrication techniques
-
Throughout this module we have learned about some additive and subtractive manufacturing methods. Mainly 3D-printing and laser cutting. 

## Capabilities: What capabilities does this technology afford you with that you did not have before?
The capabilites this technology allows me to do that i did not have before is to...

(This technology allows me )to design precise sketches which I can later send to machines which then manufacures my sketch. Before I learned about these methods my only way of being precise was with a ruler. I also had no manufacturing methods I was familiar enough with to use. The best way to showcase this is my attempt to build a drone controller prior to this course.

<img src="{{ '/assets/images/arduino_controller0.jpg' | prepend: site.baseurl | prepend: site.url}}" alt="Arduino Controller" height=400px/>

At that point in time of building that controller my only way of putting together a ciruit was with a breadboard. Therefore my best option to secure the joysticks in place was by attaching them to the breadboard as you can see in the picture above. Since then i have learned to make a controller(a box) in which i am able to use screws to fix the joysticks in place.

<img src="{{ '/assets/images/controller_sketch.png' | prepend: site.baseurl | prepend: site.url}}" alt="Controller Sketch" height=400px/>

The design is still very basic and there is much room for improvement, but it is still something robust that hides away electronics and attaches the joysticks to something.  

I also learned about creating circuit boards since i wanted to replace a breadboard into something smaller and more final.

<img src="{{ '/assets/images/controller_circuit_board.png' | prepend: site.baseurl | prepend: site.url}}" alt="Controller Circuit Board" height=400px/>

Despite me spening 4 hours to figure out i needed a footprint for my custom components, creating circuits are actually really easy and fun. The time from order to arrival of the circuit bord is allegedly one week meaning you could almost perform iterative prototyping if it was not for the shipping cost.

We also used laser cutting on wood, which is a faster and more precise method to cut in wood than any saw would be. We also experimented with design methods which made it possible to create 3D-shapes as you would with 3D-printing. Looked at finger joints and lattice hinge.


## Digital-Physical Relationship: What is the relationship between the digital and physical? Specifically what are the considerations you have to make when working with different materials and different manufacturing techniques?

When working with subtractive manufacturing methods you have to consider that it only removes material. The ones we worked with removes material from the top and all the way through. There are multiple limitations in what it is able to create. Pockets or indents are imposible so everything has to be designed in 2D with a material depth.

Another limitation for the laser cutter is that when it removes material it burns away a little more than originaly planned. This is called a "keft", and it essentially means that the thing you designed might be a little smaller. This is something that needs to be acountet for by designing additional width to the material for the laser to burn away.

When working with additive manufacturing methods you have to keep in mind that you are constantly adding material to something. Meaning that when you build up into the air the material you are adding needs somewhere to go. Adding building support for creating overhangs are important for stability. This is most often auto-generated in slicing programs, but it is possible to design builds with support that are easy to snap away. Print orientation is a way to try to circumvent creating support. When printing e.g. a lego brick without the use of support you need to flip it upside down. The inside overhang is not something a 3D-printer does well. So by printing it upside down you make sure the 3D-printer always have something to place the material on.

Another thing to consider when 3D-printing is the material size. When 3D-printing plastic is heated up and then inserted onto the rest of the plastic to create shapes. The plastic is limited in size, meaning that there is a limit in how small details it can create. Also holes can not be too small. Wall can not be too thin.

## Practical Examples: Do you have any practical examples of how your digital model might differ/deviates from your fabricated result?

-No flat surfaces from 3D-print
-Laser cut keft (shown)
-

## Limitations of Digital Design: In the typical digital fabrication workflows most of the design process takes place digitally. What limitations does this entail vs working directly with a material, for example like you would do in traditional carpentry?

-Since everything is digital it may be hard to imagine how it may fit with into real world objects
-

## Problem-Solving: Discuss a problem you encountered during the fabrication process and how you resolved it. What does this problem-solving process reveal about the limitations or advantages of digital fabrication?


Currently the largest project i have worked on so far is a stand for spinning a fractal cube or any other cubic objects. Since it is supposed to be a desk stand it needs to look good as well as being functional, meaning the electronics ideally needs to be hidden. The stand needs to attach a motor and support it vertical pointing up, and it needs to have empty space inside for electronics. 

The problems with attaching something to a 3D-printed model is that it either needs to fit perfectly in a hole, or use something like a screw. If the real life object is to fit perfectly in a hole, the geometry needs to be simple or else it is going to be really difficult to model the hole. If it does not fit perfectly it is going to wiggle around. The other alternativ is to use screws or something similar. Using screws are often not a possible solution as it requires the object to have screw holes or have geometry that allows for the creation of an encasement with screwholes. 

During my first iteration of the design i was using a motor with really diffucult geometry and it had no screw holes. The motor casing was an ellipse with flat long sides. The way i solved this was really brute force as all i did was design a square hole that was about 1mm too small. Meaning to fit the motor it almost had to be hammered into the hole. This is a really bad solution because there are empty space around the motor so it does not look appealing and removing the motor damages the plastic walls even more.

In the end i changed motor due to difficulty with controlling rotation speed. The new motor had simple geometry and screw holes, which made the solution super simple. Shown in the picture below. It has a circular hole to hide away the motor for aesthetic reasons and screw holes to lock the motor in place as well as a hole for wires.


<img src="{{ '/assets/images/motor_hole.png' | prepend: site.baseurl | prepend: site.url}}" alt="Motor Hole" height=400px/>

The problem with creating empty space is that a 3D-printer is not good at creating a large overhang due to when printing the material always needs support. Usually the easiest solution is to change the orientation before printing so there are no large overhang. Unfortunately the geometry of the stand has no ideal orientations to print from. The stand has a pyramid shape which leaves a small section to support too much weight if it were to be printed upside down. The solutions i know of are to either print multiple parts and then combine them or to remove overhangs. I chose the latter as i did not want to deal with more parts needing connection. The complete build already consists of 4 3D-printed parts, and replacing overhang with slopes smaller than 45 degrees is easier than creating screw holes.

A thing to consider when combining multiple parts is the hardness of the parts. Generally if the parts are of the same mohs hardness scale they are not going to destroy each other that quickly. Using a plastic screw for a plastic screw hole works fine, but if one of the parts are out of metal i have experienced the plastic gets destroyed really quick. Therefore my go to choice is always to use a soldering bolt to heat up the plastic and then insert a screw hole fitting. This extend the longevity of the build and makes the assembly process easier. 
