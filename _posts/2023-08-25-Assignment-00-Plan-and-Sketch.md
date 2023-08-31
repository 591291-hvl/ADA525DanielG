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



<img src="{{ '/assets/images/arduino_drone0.gif' | prepend: site.baseurl | prepend: site.url}}" alt="Arduino Drone" height=400px/>

# Detailed project description