---
layout: post
title:  "Assignment 08: Web Interfaces, Thing -> Server -> Client"
date:   2023-11-06 14:00:00 +0200
categories: Assignment
--- 


## List of content

- [Background](#background)
- [Design process](#design-process)
- [Result](#result)
- [Discussion](#discussion)


## Background

This assignment is a continuation of the previous assignment where we created a node application that sendt data via a get request and then displayed that data on the client side. The goal of this assignement is to instead of just displaying some random data, we want to display data related to the final project. To do this we need to find some way of sending data from arduino to a node project. Once the node project can read data from arduino it should be the same as before.

## Design process


The sensor on the drone(MPU6050) is used to calculate how many degrees the drone is rotated in x and y axis, so the natural thing to display on a website is these values. My initial idea is to just display these values on a graph just like the last assignment but just have 2 instead. This is also something arduino has inbuilt as Serial plotter. 

Node has a package called serialport.io that is able to open and send/read data on serial ports. I am not sure why but i always thought "serial port" was just some word arduino used but its actually a real port you can see in device manager. Since this is able to read data from serial port, we just need to send data from the arduino on the same serial port. Sending data on serial port is already done, as thats what i use as a console to read data on the arduino. 

The data the arduino sends to serial is on the format:
"x-angle: x.xx y-angle: x.xx"

The data received on js is a buffer object which contains 4 hexadecimals. Each hexadecimal is a single character each.

The buffer looks like this:
<Buffer 65 3a 20 2d>

And when i convert the hexadecimals i get:
"e: -"

So there is a small formating task that needs to be handeled here. Four and four characters are read at a time, so i can start building a string by combining them. But then i dont know where the start and end of a message is. When sending messages on bit level you often encode the message header with how many bits to read. Since i am one level above this i can simply use a character to indicate the start of a message. The perfect character for this is already in use, new line or "\n". When you press enter you actually write "\n" and the text editor interpret it as a new line. On the arduino i write "Serial.println()" and then the text inside. The ln part writes a "\n" at the end of the string.

Below is the code for this, there is a bit more string parsing to extract the numerical values from the string.

```
const serialPort = new SerialPort({ path: 'COM4', baudRate: 9600 })
serialPort.on('data', function (data) {
    output += data.toString();
    if(data.toString().includes("\n")){
        current = output.split("\n")[0];
        x_val = current.split(" ")[1];
        y_val = current.split(" ")[3];
        output = output.split("\n")[1];
    }
})
```

This only works because x_val and y_val is global variables, and when "/getData" gets a get request these values are then sendt. 

```
app.get('/getData', (req, res) => {
    res.send({x_val: x_val, y_val: y_val});
});   
```







## Result

## Discussion