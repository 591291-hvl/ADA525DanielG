---
layout: post
title:  "Assignment 10: Final"
date:   2023-12-24 14:00:00 +0200
categories: Assignment
--- 

# Describe the thing

# ???


# CAD Design iterations
Digital Fabrication Focus:
- Go into detail about each iteration of design

- Q1 How did you integrate digital fabrication techniques (CAD, 3D printing, laser cutting) in your project? Describe the process and tools used.

- Q2 Reflect on the challenges and learnings you encountered while using digital fabrication methods. How did these techniques influence your final design?






# Testing of auto stabilization system Q9?

After the processing of raw sensor data what i end up with is tilt in x and y axis. From this i created a system with 4 variables, positive and negative xy. This means that power of front right motor would be determined by positive x and postive y variables. The tilt to power converter most likely needs to be a non linear function, but for simple testing it is linear. The reason why i think it should not be linear is because i assume the higher tilt the drone has the more power it should give to correct the tilt. A linear function works for this of course, but i am not sure the rate in change is enough. Therefore i want to end up with an exponential function, but all this is something i will find out whilst testing. Right now i multiply tilt in degrees with 15. The power range i am using for the motors are 0 to 1000. Meaning a tilt of 66 degrees would result in max power output. The tilt would not alone reach the max because some of the power would be required to keep the drone of the ground. If it was a seperate power output, then i would have 45 degrees give max power output. Right now i dont know what the minimum for lift is, so this should be enough for testing.

From this i performed on the ground flight testing for stabilization. By on the ground i mean that power cables prevent it from flying freely and of course my arm holding it. When i tilted the drone diagonal in 2 of the direction i feelt a noticable force pushing it upright. But the 2 other diagnoals it tried to tilt even more in that direction. When i tried to tilt the drone straight into x or y axises it wanted to turn against the clock. I originaly thought i had assembled the propellers wrong somehow. In the motor kit i bought there are 2 identical motors and propellers, so this could not be the case as propellers cant be assembled on the wrong motor. This could only mean that 2 of the motors rotate the wrong way. I noticed that air flow from 2 of motors was pushing upwards, and when i checked which way they rotated, i saw that they all spun with the clock. 

After doing some research, a motor is from my new understanding an electrical field that rotates a magnet, this magnet in this case is attached to the rotors that spins. This electical field can be reversed by flipping power and ground. By flipping the direction of the electrical field the magnet or rotor spins the opposite direction. With this fixed the motors are pushing the drone upright when i attempt to tilt it. When i performed "flight" tests before implementing auto stabilization system i thought the reason why the drone was rotating on the ground was because the motors was not calibrated correctly, but now i know it was because i failed to check if i had done the assembly of the drone correctly. 

//attach video of first flight test with auto stabilization system

Attached video above is of the first real flight with auto stabilization system. As you might notice the test was not perfect, but it did show great potential. Just before this test i implemented a emergency power off button. I had to implement this because if the drone were to flip the motors would rotate based on the tilt and i would have to unplug the battery. This test proved that the system worked perfectly. Another concern was if i had enough lift. Based on the momentum the drone had before i managed to turn off the power i would say the power is sufficient.





# Electrical Design


# User interactbility Q6

Emergency power off - Press both joysticks at the same time - Sends minimum throttle to all motors
Disable emergency power off - Press both joysticks again at the same time - Disables minimum throttle to all motors
Move upwards - Push left joystick forward - Increments main throttle variable
Move downwards - Push left joystick backwards - Decrement main throttle variable
Move forwads - Push right joystick forwards - 
Move backwards - Push right joystick backwards -
Move left - Push right joystick left - 
Move right - Push right joystick right -