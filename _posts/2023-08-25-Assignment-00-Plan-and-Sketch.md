---
layout: post
title:  "Assignment 00: Plan and Sketch."
date:   2023-08-25 14:00:00 +0200
categories: Assignment
---

## List of content

- [Project description](#project-description)
- [What has been done so far](#what-has-been-done-so-far)
- [Detailed project description](#detailed-project-description)



# Project description

The goal of the project is to design, build, and program a remote controlled quadcopter(drone) and it's corresponding controller. 

The end product should include a radio based communication between 2 arduino's, gyroscope/accelerometer for drone stabilization, and in real time controll over drone movement.

Components needed for the project are:
- 2 Arduinos
- 2 Radio transceiver
- Motors and electronic speed controller (esc)
- Drone frame
- Drone arduino casing
- Controller arduino casing

# What has been done so far

### Arduino Controller

A controller made with a breadboard and 2 joysticks connected to an arudino. Currently only sends a single number via a radio transceiver which determines the power output of the drone motors.

<img src="{{ '/assets/images/arduino_controller0.jpg' | prepend: site.baseurl | prepend: site.url}}" alt="Arduino Controller" height=400px/>

### Arduino Drone

Arduino based drone attatched to a frame that has a integrated circuit of providing the motors with electricity. The drone has a transceiver in which it recives...

<img src="{{ '/assets/images/arduino_drone0.gif' | prepend: site.baseurl | prepend: site.url}}" alt="Arduino Drone" height=400px/>

# Detailed project description

As of now the project has a few problems that needs to fixed in order to continue development. The problems are desyncronized motors and weight.

### Desyncronized motors

Whilst testing the circuit and arduino by powering on the motors it was observed that the motors turned on in response to different output strength. This was further testet by attempting to fly the drone which lead to the drone spinning around before take off.

Possible solution are to deconstruct the drone and troubleshoot each motor individually. If the motors are desynced and this offset does not change, it would be easy to synchronize them in software. If not gyro is required. Worst case solution would be to buy new motors. 

### Weight

When attempting to fly the drone, 70% of max power output was used. The drone did not achieve flight but this could be mainly due to desync between motors. Still an attempt to lighten to load would be beneficial.

A way to lighten the load may be solved by 3D-printing a new drone frame as the current one used is heavier than needed.

### TODO's

After the problems are solved the project would mainly consist of:
- Arduino casing <br>
Currently the arduino and breadboard containing the circuit are strapped to the frame using zip ties. A casing would be benificial to both hide the circuit and protect it from weather and high velocity damage.
- Controller <br>
Currently the controller is a breadboard with 2 joysticks sticking out of it. Designing a more friendly looking and ergonomic controller would be benificial.
- Radio communication <br>
Currently the radio communication is only used for motor power output directly up. No attempts has been made to allow 3-dimensjonal navigation.
- Gyro/accelerometer <br>
Currently this component has not been utilized. Auto stabilization is an integral part of drone design.