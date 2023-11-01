---
layout: post
title:  "Assignment 06: Input-Output"
date:   2023-12-24 14:00:00 +0200
categories: Assignment
--- 


# Testing of auto stabilization system

The result i am getting from the sensors are tilt in x and y axis. From this i created a system with 4 variables, positive and negative xy. This means that power of front right motor would be determined by positive x and postive y variables. The tilt to power converter most likely needs to be a non linear function, but for simple testing it is linear. The reason why i think it should not be linear is because i assume the higher tilt the drone has the more power it should give to correct the tilt. A linear function works for this of course, but i am not sure the rate in change is enough. Therefore i want to end up with an exponential function, but all this is something i will find out whilst testing. Right now i multiply tilt in degrees with 15. The power range i am using for the motors are 0 to 1000. Meaning a tilt of 66 degrees would result in max power output. The tilt would not alone reach the max because some of the power would be required to keep the drone of the ground. If it was a seperate power output, then i would have 45 degrees give max power output. Right now i dont know what the minimum for lift is, so this should be enough for testing.

From this i performed on the ground flight testing for stabilization. By on the ground i mean that power cables prevent it from flying freely and of course my arm holding it. When i tilted the drone diagonal in 2 of the direction i feelt a noticable force pushing it upright. But the 2 other diagnoals it tried to tilt even more. When i tried to tilt the drone straight into x or y axises it wanted to turn against the clock. I originaly thought the propeller was mixed up somehow. In the motor kit i bought there are 2 identical motors and propellers, so this could not be the case as propellers cant be assembled on the wrong motor. This could only mean that 2 of the motors rotate the wrong way. I noticed that air flow from 2 of motors was pushing upwards, and when i checked which way they rotated, i saw that they spun with the clock. A motor is from my new understanding an electrical field that rotates a magnet, this magnet in this cae is attached to the rotors that spins. This electical field can be reversed by flipping power and ground, and now the magnet or rotor spins the opposite direction. With this the auto stabilization system works perfectly. 

I thought the reason why the drone was rotating on the ground when i performed flight tests before was because the motors are not calibrated correctly, but now i know it was because i failed to check if i had done the assembly of the drone correctly. 