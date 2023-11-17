---
layout: post
title:  "Assignment 10: Final"
date:   2023-12-24 14:00:00 +0200
categories: Assignment
--- 

# Introduction

For this project the idea was to build a drone. Of course this is not some new concept, as it is more intended to be a challenge for a person who is coming from a background in computer science. Other than just building a drone I also want to build the controller for it. The reason is that i have more controll of what kind of data is being sendt to the drone. By having two seperate systems i have the option to develop both systems at the same time or to focus on one at the time.

# System Implementation

The drone is a quadcopter, meaning it has 4 motors and 4 propellors. Each motor is connected to a ESC which is then connected to an arduino. The arduino serves as logical controll unit on the drone, and manages every other component. This also includes radio communication with the controller and a sensor(MPU6050) which has a gyro and accelerometer. The arduino takes data from the radio and uses it to controll the drones direction of movement. It also takes data from the sensor and uses it to balance its tilt.

The controller consists of two joysticks and a radio. This system is also using an arduino as its logical controller, so a large part of this project is to get reliable radio communication between two arduinos. The arduino reads the input from the joysticks and then sends them to the drone.


# Digital Fabrication

//Mention how joysticks are attached on the controller

A large part of this project has been done in some kind of digital fabrication software. This project has alot of electronic parts that needs protection and housing. If one were to breakdown this to its simplest form of abstraction, I have created two boxes which contains electronics. These boxes however is made so the lid is removable. This was done with "threaded inserts", which is screw holes made out of metal that you insert into 3D printed objects by melting plastic. By doing this you actually solve the biggest problem i have found with 3D printed designs. 3D printing is really bad at any kind of overhang, so bad that common strategy is to print excess plastic that is used for support. This of course is wasteful and takes more time to print.

In terms of functionality the most useful fabrication technique i have used is designing circuit boards. How i see it, there are 3 levels of working with electronics. First level is just connecting wires between components. Next level is using breadboards, with this you are forced into more structure as things are usualy contained on the same breadboard. Next level is designing a circuit board and soldering components onto the board. With this the circuit takes much less space and everything is secured in one place. For the drone this is really important. The motors on a drone operates with an RPM above thousands. Any movable part on the drone could experience large amount of stress, due to the vibrations the motors produces. Because of this soldering electrical components to a circuit board is integral for the durability of the system. In terms of space managment this solution made it so the box containing the electronics could fit on its foundation and also be somewhat aerodynamic.

Since its important to reduce stress on the system, having an exact fit between the circuit board and the box is important. This introduces a challenge in having accurate measurements. The first circuit board i designed for the drone i somehow messured wrong so i had to reduce the size of the circuit board by filing down the edges. I also ended up mixing up connections so i had to tape a component onto the circuit board. Making mistakes on a circuit board is much more punishing than some thing that is 3D-printed. You can always just reprint something, but with a circuit board i have to pay someone to create it and then wait for it to arrive. I really should not complain since its only a week shipping, but there is still a bigger insentive to just try to make it work rather than order a new circuit board.

A easy solution could still be to just create holes in the circuit board and then screw it into the 3D-printed box that is the drone housing. For some reason i wanted to have an exact fit, and kinda still do now that i have tried multiple times to achive this over multiple projects. I have noticed that my teacher for this course is usualy using a screw and a bolt to combine two parts. This is something i should start to do as its just fast and simple. I think i still prefere to have metal screwholes as i think its more aesthetically pleasing. I have also seen people screwing metal straight into plastic creating contact point between plastic and metal. I really dont see how this is any good due to how little reusable this is for wood. If you were to take a screw out of wood, that hole is almost no longer usable. Plastic is way worse because the inside not solid most of the time. 3D-printed oject is a hard shell with support inside. One would have to use more infill and be content with never removing the screw to do this.

During the project i strongly considered building a testing rig for drone stabilization testing. This would work by attaching the drone on a pivot point. Then i could easily test software and see if its able to stabilize on its own without me flying it and risking destroying parts Out of the two fabrication methods we learned about in this course one method is way faster and produces material more capable of this task. This method is laser cutting, it allows for fast production of larger pieces and since it is out of wood(or metal) it should handle being strapped between a table and the drone.


# Physical Computing Application Q3, Q4

As mentioned in # Introduction the basis of the project is comunication between two arduinos. In reality any component that is able to computation and has memory could do this task. The reason arduino is my choice for this is because of how easy it is to use. The community around arduino is amazing and there are alot of modules and open souce libraries. The radio module i am using(nRF24L01) has an arduino library that allows me to create an array, and then send the hole datatype in one go. Without this library i would have to go down on the byte level and encode and decode small packets of information. 

The main role the arudino serves is managing how much goes into the motors(actually controlling the ESC's). Using the data recived from the radio on the drone side power output it then given to the motors. Another goal for this project was to have the drone auto level. Without auto level the drone would be prone to flipping. Any external force(wind) on the drone whilst in flight would tilt the drone slightly and it would immediately flip(i think, 99% sure). Therefore i use a sensor(MPU6050), which has a accelerometer and gyro. The arduino should then take the data from this sensor to autonomously adjust power given to the motor to prevent it from flipping, or just keep it at the desired level of tilt.

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
    TODO v EXPAND THIS PART!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
The system on the controller is really simple since there is just an arduino that sends joystick data to the other arduino through radio.
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!1

Something that is really important when designing this kind of system is making sure everything operates smoothly and everything is responsive. How an arduino executes code is by running a function called loop on repeat, everything that is executed more than once is inside this function. Therefore it is important to make sure nothing is blocking or taking too much computing time. A common practice on an arduino when you want to limit how often something happens is by blocking the CPU by making it wait. This is fine when there is only one component running, but on the drone there are 3 seperate parts working together(MPU, Radio, Motors). The MPU(gyro and accelerometer sensor) is really important and needs to sample data as often as possible, if possible the sample rate should be maximized and other not so important parts should limited. The MPU output is directly affecting the motors, if motors are limited then there might occour a delay in the stabilization and it would work suboptimal. The radio however is not so important, it only affects how responsive the drone seems, but as long its not limited too much it should not be noticable. The limiting is done by checking current time each loop, if current time is larger than last time the radio code was executed and interval then radio can run once. This interval can be changed if the controlles does not seems responsive enough. 

To actually fly the drone it obviously needs to be powered. During its development the arduino was powered through usb, and the motors was powered through a stationary power supply. The usb connection is how code is uploaded to the arduino and used for plotting data through serial print. Stationary power supply is helpful as you can set how much volts that is being sendt and you can see how much amps the system draws. When flying the drone, this needs to be changed. The input pin on the arduino(vin) has a recommended range of 7 to 12 volts, whilst the motors require higher voltage to operate optimal. Therefore a step down voltage regulator was used. I should probably know exactly how this works, but it was really easy to use and i have almost no pior electrical knowledge. To use it, I attached input and output wires. The output voltage was tuned by checking with a voltmeter and turning a knob.


- Q3. Describe how you incorporated physical computing elements (using Arduinos, sensors, actuators) into your system. What was the rationale behind your choices?
->

- Q4. Discuss the data sampling and control mechanisms you implemented. How did these enhance the functionality of your prototype?


# Interaction Design Q5, Q6

- Q5. Explain how you developed the user interface for your system. Does it use a web interface, a mobile app, or a physical interface? What are the advantages of your choice?

- Q6. Illustrate the interaction flow and feedback mechanisms in your system. How does this interface facilitate user interaction?

# System evaluation Q7, Q8

- Q7. How did you integrate the three modules (Digital Fabrication, Physical Computing, and Interaction) in your project? Discuss the interplay and synergy between these components in your prototype.

- Q8. Reflect on the multidisciplinary nature of your project. How did the combination of different computational tools and techniques influence your design approach and final outcome?

# Discussion Q9, Q10, Q11

- Q9. What unique problem does your system address? Explain the innovative aspects of your design.
-> not innovative but its kinda modular since i created the system i can modify it as much i would like(add more things)

- Q10. Describe the problem-solving strategies you employed during the project. How did you overcome the challenges and constraints you faced?
->stationary power source is really good, multimeter is useful

- Q11. Critically evaluate your system. What are its strengths and limitations?

# Conclusion and Future Work Q12

- Q12. Propose potential improvements or future developments for your project. How would you advance the project further with more time or resources?
-> Better auto stabilization, testing rig, 3d print everything, gps for auto return, live camera feed

# Testing of auto stabilization system Q9?

After the processing of raw sensor data what i end up with is tilt in x and y axis. From this i created a system with 4 variables, positive and negative xy. This means that power of front right motor would be determined by positive x and postive y variables. The tilt to power converter most likely needs to be a non linear function, but for simple testing it is linear. The reason why i think it should not be linear is because i assume the higher tilt the drone has the more power it should give to correct the tilt. A linear function works for this of course, but i am not sure the rate in change is enough. Therefore i want to end up with an exponential function, but all this is something i will find out whilst testing. Right now i multiply tilt in degrees with 15. The power range i am using for the motors are 0 to 1000. Meaning a tilt of 66 degrees would result in max power output. The tilt would not alone reach the max because some of the power would be required to keep the drone of the ground. If it was a seperate power output, then i would have 45 degrees give max power output. Right now i dont know what the minimum for lift is, so this should be enough for testing.

From this i performed on the ground flight testing for stabilization. By on the ground i mean that power cables prevent it from flying freely and of course my arm holding it. When i tilted the drone diagonal in 2 of the direction i feelt a noticable force pushing it upright. But the 2 other diagnoals it tried to tilt even more in that direction. When i tried to tilt the drone straight into x or y axises it wanted to turn against the clock. I originaly thought i had assembled the propellers wrong somehow. In the motor kit i bought there are 2 identical motors and propellers, so this could not be the case as propellers cant be assembled on the wrong motor. This could only mean that 2 of the motors rotate the wrong way. I noticed that air flow from 2 of motors was pushing upwards, and when i checked which way they rotated, i saw that they all spun with the clock. 

After doing some research, a motor is from my new understanding an electrical field that rotates a magnet, this magnet in this case is attached to the rotors that spins. This electical field can be reversed by flipping power and ground. By flipping the direction of the electrical field the magnet or rotor spins the opposite direction. With this fixed the motors are pushing the drone upright when i attempt to tilt it. When i performed "flight" tests before implementing auto stabilization system i thought the reason why the drone was rotating on the ground was because the motors was not calibrated correctly, but now i know it was because i failed to check if i had done the assembly of the drone correctly. 

//attach video of first flight test with auto stabilization system

Attached video above is of the first real flight with auto stabilization system. As you might notice the test was not perfect, but it did show great potential. Just before this test i implemented a emergency power off button. I had to implement this because if the drone were to flip the motors would rotate based on the tilt and i would have to unplug the battery. This test proved that the system worked perfectly. Another concern was if i had enough lift. Based on the momentum the drone had before i managed to turn off the power i would say the power is sufficient.

//PID-regulator



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