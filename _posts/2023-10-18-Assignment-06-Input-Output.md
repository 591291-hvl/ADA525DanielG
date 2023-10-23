---
layout: post
title:  "Assignment 06: Input-Output"
date:   2023-10-18 14:00:00 +0200
categories: Assignment
--- 

## List of content

- [Background](#background)
- [Sensors](#sensors)
- [Angular System](#angular-system)
- [Result](#result)
- [Discussion](#discussion)


## Background


The goal of this assignment is to use a microcontoller to read something from the world around us and to then use a microcontroller to interact with the very same world. The thing i am building for my final project is a drone, which uses motors to interact with the world. The thing i am going to read is the drone's angular velocity and acceleration. With the use of these measurements the goal is to write a self balancing algorithm to help control the drone. 



## Sensors
//Explain accelerometer and gyro, with pictures.

I wont be giving an in depth explanation of what a gyroscope is as the physics behind it is complicated and out of scope of this assignment. The only thing thats important is that a gyroscope conserves angular momentum given to it, whilst what we are using is an electrical gyroscope which measures angular momentum. For simplisity i will be refering to this as just gyro. The image below shows the axises a gyro measures angular momentum in. 


<img src="{{ '/assets/images/gyroscope.png' | prepend: site.baseurl | prepend: site.url}}" alt="Gyroscope" height=400px/>


An accelerometer measures change in movement, think about what happens when you go from low speed to high speed in a car. You get pushed into the seat when the speed increases, but when you already are at high speed nothing happens. An acceloremeter does the same, but outputs an electrical signal according to the acceleration. Same as the gyro, this also measures in x,y, and z-axises.



## Angular System
//Explain why i am going to convert it into a angular system(?), and then show how(with math and code).

If a gyro measures angular momentum, how much change in rotation an object has, why do we need an accelerometer also? This is because a gyro is prone to drift over a long period of time. The accelerometer will account for this error.

The reason why we need both a gyro and an accelerometer is because both is inaccurate in its own way. A gyro provides accurate data in the short term but drift over longer time. An accelerometer provides accurate data over a long term, but is noisy in the short term. The goal is to combine the two to get accurate angular measurements. Which can be done with a complementary filter. A complementary filter is just a quicker approximation of kalman filter which is the proper way of combining accelerometer and gyro data. 

//show math here



//Show how raw data looks like(?)

//Show how angular system looks like(?)

## Result

//retake video with tape on motors.

## Discussion



Using a microcontroller to messure movement in 3 dimensions(?). Converting it into an angular system, x and y axis tilt. Using the tilt to turn on motors.