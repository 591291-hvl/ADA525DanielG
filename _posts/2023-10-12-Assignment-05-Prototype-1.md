---
layout: post
title:  "Assignment 05: Final Project - Prototype 1"
date:   2023-12-24 14:00:00 +0200
categories: Assignment
--- 

## List of content

- [Background](#background)
- [Design process](#design-process)
- [Result](#result)


## Background

The goal for this assignment was to create a first prototype for the final project. The prototype should be used for testing and further development. The end goal i am working towards is to create a working quadcopter drone with auto stabilization. I decided to work towards completing the drone controller so i have something finalized i can use for further developing the drone. Last time i worked on the controller i ended up with a box were i could attach joysticks, and enough space to hide away electronics. Unfortunately there was not enough space because i did not do a good enough job in messuring how much space was needed. The design also did not account for me still using a breadboard for the electronics which also did not fit in the box.

The prototype needs to solve the following.
- Make space for radio transceiver, usb-type b powerplug for arduino, and electronics.
- Find a better solution for electronic wiring

## Design process

Whilst trying to recalibrate drone motors a electronics teacher found interest in what i was doing and ended up helping me for almost an hour. Before he left i asked if he had any ideas how i would fit everything into the controller box and he told me to design a circuit board instead of using a breadboard. Designing circuit boards was originally planned for this course so this was the best opportunity i could get.

The main reason i had to use a breadboard is because the arduino is limited in ground and power connections, everything else has a direct wire from a component to the arduino. The breadboard is mainly used to help parallel connecting components with power. So the circuit board does not need to be complicated. The other reqirement is that it needs to take up less space. To do this i need to create an arduino shield, which from my understanding is just a circuit board that is placed on top of an arduino with some extra "stuff".

KiCad, the program i am using for designing the circuit board has an arduino "symbol" which gives me a "schematic" "object" for the shield i am trying to build. It also have the same for the radio transceiver i am using. But it did not have "symbols" for the joysticks i am using.

This next part i spent 5 hours on troubleshooting but i found out that i can create my own components. To do this i had to create a "symbol" and a "footprint". A symbol is how the component is representet on schematic view, and footprint is how the compoentent is representet on PCB view. These also needs to be linked in footprint assignment if not the component does not exist in PCB view, which means that there is no physical model for the component.

The image below shows the schematic and PCB view of the joystick component, and the footprint assignment.

<img src="{{ '/assets/images/kicad_symbol_creation.png' | prepend: site.baseurl | prepend: site.url}}" alt="KiCad Symbol Creation" height=400px/>

Otherwise, creating a schematic for the circuit board is easy once you have all the components placed down. For my level of complexity i just connect lines, but i imagine it could be more advanced later. Image below is how the results looked like.

<img src="{{ '/assets/images/controller_schematic.png' | prepend: site.baseurl | prepend: site.url}}" alt="Controller Schematic" height=400px/>

The main problem i had with creating the PCB for the circuit was that i did not know i had to select where the edge of the circuit board is. In hindsight this is sounds like a really obvious thing to do, but there was a 3D-view for the PCB which tricked my by showing me the circuit board with apparently imaginary cut out lines. I only found out about this problem when i got an email from the manufacturing site telling me my build failed because of "there is no Keepout layer (Board Outline)". After multiple resubmissions and emails i figured out i just had to create a box around and put the box on "Edge.Cuts" layer. Image below is the PCB view of the circuit board.

<img src="{{ '/assets/images/controller_circuit_board.png' | prepend: site.baseurl | prepend: site.url}}" alt="Controller Circuit Board" height=400px/>

When i received the circuit board i realized that the holes for the components i created were a different size than the others. The holes was too small but i found out i could use pins that was malleble enough to be forced through the holes. I then used an soldering iron to attach pins to the circuit board.

<img src="{{ '/assets/images/controller_circuit_board.gif' | prepend: site.baseurl | prepend: site.url}}" alt="Controller Circuit Board" height=400px/>

Now that i had working electronics i then needed to fit everything inside some sort of container. Since i already had a design i only needed to make small adjustments. I expanded the inside just enough so the circuit board does not jiggle inside. Created enough height inside for the wires. Made sure the powercord hole was in the right posistion. Created a hole for the radio transceiver.

<img src="{{ '/assets/images/controller_sketchv2.png' | prepend: site.baseurl | prepend: site.url}}" alt="Controller Sketch v2" height=400px/>

## Result

<img src="{{ '/assets/images/controller.gif' | prepend: site.baseurl | prepend: site.url}}" alt="Controller" height=400px/>

## Discussion

## What am i missing

## Next step for the final project


- What is it made from? What does it do? How do we interact with it?
^Result

- How are these properties represented in your design?
^???

- Am I targeting the correct fabrication technique? Is there a better way to make this?
^???

- What did you learn from making this prototype?
^Discussion?

- What are you missing?

- What are the next steps for your project? What would you like to explore further?
