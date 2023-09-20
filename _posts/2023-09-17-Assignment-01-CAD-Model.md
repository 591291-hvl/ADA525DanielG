---
layout: post
title:  "Assignment 01: CAD Model"
date:   2023-09-17 14:00:00 +0200
categories: Assignment
---

## List of content

- [Background](#background)
- [Design](#design)
    - [Motor Shaft](#motor-shaft)
    - [Stand](#stand)
- [Problems](#problems)
    - [Analog-Arduino-Output](#analog-arduino-output)
    - [Voltage-Divider](#voltage-divider)
    - [Motor-Controller](#motor-controller)


## Background

The requirements for this assignment is to create a CAD model for the final project. Currently i have a very crude version of a radio controller, image below. 


<img src="{{ '/assets/images/arduino_controller0.jpg' | prepend: site.baseurl | prepend: site.url}}" alt="Arduino Controller" height=400px/>

## Design process

The design process behind creating the controller is that a controller is a box with electronic in it, and joysticks attached to that box. Ideally i want a lid for the box so the electronics are kinda protected and hidden away. The requirements for the lid is that i am able to remove and it needs to be locked in place. Using metal screws in plastic is not a good idea since the plastic takes damage over time and then the screws no longer holds the lid in place. I was given screw holes fittings which needs to be melted into plastic, so first step was to test how these worked.


<img src="{{ '/assets/images/screw_fitting_test.jpg' | prepend: site.baseurl | prepend: site.url}}" alt="Arduino Controller" height=400px/>

The screw hole fittings required that the plastic holes had 4mm in diameter. Applying the fittings was easy as all i needed was to use a pointy soldering iron to heat up the fittings and push down into the plastic. The metal reached melting temperatur of plastic almost instantly.

The screw holes in the controller was 3mm so i had to use a 4mm drill bit to make space for the screw hole fittings

<img src="{{ '/assets/images/arduino_controller2.jpg' | prepend: site.baseurl | prepend: site.url}}" alt="Arduino Controller" height=400px/>
