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


# Digital Fabrication Q1, Q2

//Mention how joysticks are attached on the controller

A large part of this project has been done in some kind of digital fabrication software. This project has alot of electronic parts that needs protection and housing. If one were to breakdown this to its simplest form of abstraction, I have created two boxes which contains electronics. These boxes however is made so the lid is removable. This was done with "threaded inserts", which is screw holes made out of metal that you insert into 3D printed objects by melting plastic. By doing this you actually solve the biggest problem i have found with 3D printed designs. 3D printing is really bad at any kind of overhang, so bad that common strategy is to print excess plastic that is used for support. This of course is wasteful and takes more time to print.

In terms of functionality the most useful fabrication technique i have used is designing circuit boards. How i see it, there are 3 levels of working with electronics. First level is just connecting wires between components. Next level is using breadboards, with this you are forced into more structure as things are usualy contained on the same breadboard. Next level is designing a circuit board and soldering components onto the board. With this the circuit takes much less space and everything is secured in one place. For the drone this is really important. The motors on a drone operates with an RPM above thousands. Any movable part on the drone could experience large amount of stress, due to the vibrations the motors produces. Because of this soldering electrical components to a circuit board is integral for the durability of the system. In terms of space managment this solution made it so the box containing the electronics could fit on its foundation and also be somewhat aerodynamic.

Since its important to reduce stress on the system, having an exact fit between the circuit board and the box is important. This introduces a challenge in having accurate measurements. The first circuit board i designed for the drone i somehow messured wrong so i had to reduce the size of the circuit board by filing down the edges. I also ended up mixing up connections so i had to tape a component onto the circuit board. Making mistakes on a circuit board is much more punishing than some thing that is 3D-printed. You can always just reprint something, but with a circuit board i have to pay someone to create it and then wait for it to arrive. I really should not complain since its only a week shipping, but there is still a bigger insentive to just try to make it work rather than order a new circuit board.

A easy solution could still be to just create holes in the circuit board and then screw it into the 3D-printed box that is the drone housing. For some reason i wanted to have an exact fit, and kinda still do now that i have tried multiple times to achive this over multiple projects. I have noticed that my teacher for this course is usualy using a screw and a bolt to combine two parts. This is something i should start to do as its just fast and simple. I think i still prefere to have metal screwholes as i think its more aesthetically pleasing. I have also seen people screwing metal straight into plastic creating contact point between plastic and metal. I really dont see how this is any good due to how little reusable this is for wood. If you were to take a screw out of wood, that hole is almost no longer usable. Plastic is way worse because the inside not solid most of the time. 3D-printed oject is a hard shell with support inside. One would have to use more infill and be content with never removing the screw to do this.

During the project i strongly considered building a testing rig for drone stabilization testing. This would work by attaching the drone on a pivot point. Then i could easily test software and see if its able to stabilize on its own without me flying it and risking destroying parts Out of the two fabrication methods we learned about in this course one method is way faster and produces material more capable of this task. This method is laser cutting, it allows for fast production of larger pieces and since it is out of wood(or metal) it should handle being strapped between a table and the drone.


# Physical Computing Application Q3, Q4

As mentioned in # Introduction the basis of the project is comunication between two arduinos. In reality any component that is able to do computation and has memory could do this task. The reason arduino is my choice for this is because of how easy it is to use. The community around arduino is amazing and there are alot of modules and open souce libraries. The radio module i am using(nRF24L01) has an arduino library that allows me to create an array, and then send the whole object in one go. Without this library i would have to go down on the byte level and encode and decode packets of information. 

The main role the arudino serves is managing how much goes into the motors(actually controlling the ESC's(electronic speed controllers)). Using the data recived from the radio on the drone side, power output is then given to the motors. Another goal for this project was to have the drone auto level. Without auto level the drone would be prone to flipping. Any external force(wind) on the drone whilst in flight would tilt the drone slightly and it would immediately flip(i think, 99% sure). Therefore i use a sensor(MPU6050), which has a accelerometer and gyro. The arduino should then take the data from this sensor to autonomously adjust power given to the motor to prevent it from flipping, or just keep it at the desired level of tilt.

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
    TODO v EXPAND THIS PART!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
The system on the controller is really simple since there is just an arduino that sends joystick data to the other arduino through radio.
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!1

Something that is really important when designing this kind of system is making sure everything operates smoothly and everything is responsive. How an arduino executes code is by running a function called loop on repeat, everything that is executed more than once is inside this function. Therefore it is important to make sure nothing is blocking or taking too much computing time. A common practice on an arduino when you want to limit how often something happens is by blocking the CPU by making it wait. This is fine when there is only one component running, but on the drone there are 3 seperate parts working together(MPU, Radio, Motors). The MPU(gyro and accelerometer sensor) is really important and needs to sample data as often as possible, if possible the sample rate should be maximized and other not so important parts should limited. The MPU output is directly affecting the motors, if motors are limited then there might occour a delay in the stabilization and it would work suboptimal. The radio however is not so important, it only affects how responsive the drone seems, but as long its not limited too much it should not be noticable for humans. The limiting is done by checking current time each loop, if current time is larger than last time the radio code was executed and interval then radio can run once. This interval can be changed if the controllers does not seems responsive enough. 

To actually fly the drone it obviously needs to be powered. During its development the arduino was powered through usb, and the motors was powered through a stationary power supply. The usb connection is how code is uploaded to the arduino and used for plotting data through serial print. Stationary power supply is helpful as you can set how much volts that is being sendt and you can see how much amps the system draws. When flying the drone, this needs to be changed. The input pin on the arduino(vin) has a recommended range of 7 to 12 volts, whilst the motors require higher voltage to operate optimal. Therefore a step down voltage regulator(buck converter) was used. I should probably know exactly how this works, but it was really easy to use and i have almost no pior electrical knowledge. To use it, I attached input and output wires. The output voltage was tuned by checking with a voltmeter and turning a knob. TODO: EXPAND THIS


# Interaction Design Q5, Q6

Every controll device for a drone i have seen uses some kind of joysticks. Some drones are controlled via a phone app, and they use touch screen based joysticks. There is a good reason why joysticks are used. I would say the biggest reason i decided to order joysticks rather than just use buttons that i already had many of, was because they are intuitive, easy to use, and has many different values that can be used. Having something that outputs a range of numerical values as opposed to only binary values is beneficial when the motor input values also is a range of numerical values. Also when letting go of the joysticks they return to its orignial position(original value) which mean you dont have to think about implementing a toggle system you would have to do with buttons. A joystick has 5 usable values and two of the values are an inverse of two of the other values, just like on a drone. You can not steer a drone left and right at the same time, and same with forwards and backwards.

This course has had focus on interacting with our device through internet(internet of things device(IoT device)), but if i were to do this then it would be the same as just using buttons. Probably the most ideal configuration for controlling the drone through web would be with WASD and arrow buttons. By doing this i would not have the advantages of using joysticks. Another alternative would be to develop a phone app, then i would have the advantage of joysticks. The reason why i have not done this is because apps are out of the scope of the course and i have no prio experience with app development. Having a phone app is acctualy more advantageous than the current system. If i where to attach a camera on the drone, then i would already have a screen to display the video feed. The would also be more easy to use as currently i need to connect the controller to a pc, with an app i only need my phone and the drone.

Actually developing the user interface was a bit challenging prior to this course. The joystick i was using was branded as an arduino module but there was no clear easy way to make them non free standing. Prio to this course my solution was to just plug them directly in a breadboard, but as you can see from attached picture this was not ideal. In retrospect what i should have done was to just attach them to a piece of cardboard or similar. When i first learned about 3D-printing as a fabrication method i quickly printed a flat rectangle and used screws and bolts to attach them. The final design is really similar but now the rectangle is a lid for the controller box.

//image of controller before and after

- Q6. Illustrate the interaction flow and feedback mechanisms in your system. How does this interface facilitate user interaction?

//Drawing on ipad
^This system facilitate user interaction by having...

# System evaluation Q7, Q8

// TODO: Expand this part
// TODO: Alot of this does not make any sense
// Joysticks are also sensors
// Also i am not answering any question what so ever
// DOES NOT ANSWER INTERPLAY AND SYNERGY

As mentioned the module about digital fabrication was mainly used as housing and forcing a structure for electrical components. Ideally this part should have played a larger part of the project. The drone frame was not designed but rather bought online. If not limited on time then the frame should also have been 3D-printed using. The design of the drone frame should then have been designed using generative design. By applying structural constraints the drone model could then have been generated. Since there was a time limit, most of the focus for this module has been used secure electronics. Small holes allows for wires to go out of the box(wire to ESC), and exact fit has been made to secure circuit boards and arduinos. Digital fabrication of PCB's(printed circuit boards) has played the largest part in reducing the space usage of the electronics and making the circuit somewhat comprehandable.

The module physical computing mainly consist of how the electrical components(MPU, motors, and radio) interact with the arduino. As mentioned the arduino is the logical computation component that handles input and output between from the other components. It takes sensor data from the MPU component and turns on actuators(motors)... TODO: EXPAND


// TODO: INTERACTION


By employing different computational tools and techniques it allowed my workflow to be incredibly dynamic. Whilst building the electronics for the project, i iteratively changed the CAD model to fit the changes i made to the electronics. If i miscalculated something i could quickly change the CAD design and reprint the part(drill a hole in the original model first whilst i wait for the print to finish). If something was done incorrectly with the electronics i could quickly change the model in KiCad(ended up breaking a wire cutter whilst attempting to reduce the size of the circuit board. I also ended up using tape to attach parts to a faulty made circuit board, and use hotfix soldering solutions). All this made it so whilst i worked on the project i was not stuck in one module trying to get something to work, i was actually using everything at once. It also allowed me to have a deeper insight to what every part of the design was doing, which i think made this project easier than it should have been. I imagine if i just focused on one module at the time i would have difficulty trying to get everything to work together in the end. Thats atlest the impression i got when talking to other people in my class. Some people were so focused on just the CAD design that the rest of the system is not yet working in the last weeks of the semester.



- Q7. How did you integrate the three modules (Digital Fabrication, Physical Computing, and Interaction) in your project? Discuss the interplay and synergy between these components in your prototype.
-> Digital fabrication was mainly used as housing
-> Physical computing, important whole design?
-> interaction, also important??????

- Q8. Reflect on the multidisciplinary nature of your project. How did the combination of different computational tools and techniques influence your design approach and final outcome?


# Discussion Q9, Q10, Q11



- Q9. What unique problem does your system address? Explain the innovative aspects of your design.
-> not innovative but its kinda modular since i created the system i can modify it as much i would like(add more things)

- Q10. Describe the problem-solving strategies you employed during the project. How did you overcome the challenges and constraints you faced?
->stationary power source is really good, multimeter is useful

- Q11. Critically evaluate your system. What are its strengths and limitations?
-> For a drone, this is a very crude and rough design of what you can buy for very cheap. Main use for a drone is aerial pictures, which this design is not yet able to do. Currently if one wanted to film something you would have to attach a phone to the drone and then fly it. The positive with this is that you do not require a licence to fly it(i think) since it does not have a camere. Since it is self-made and open-source, implementing a camera could be done without too much trouble.

# Conclusion and Future Work Q12

- Q12. Propose potential improvements or future developments for your project. How would you advance the project further with more time or resources?
-> Better auto stabilization, testing rig, 3d print everything, gps for auto return, live camera feed

# Testing of auto stabilization system Q10?

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