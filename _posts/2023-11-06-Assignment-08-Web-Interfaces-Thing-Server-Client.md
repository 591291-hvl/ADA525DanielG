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

On the client side i did exactly the same as the last assignment but this time i use two arrays to store data. I then used the arrays to plot x and y rotation between -90 degrees and +90 degrees.


Because just plotting x and y rotation is boring and there is something really cool you can do with those values i did something extra. Since i have the rotations of the drone, why not try to animate an object to mimic the drone rotations.

For this i ended up just using three.js which was really simple but i could and i would have been more fun to bruteforce it through canvas with xyz cordinates. But since i have allready done something similar i decided not to, https://github.com/591291-hvl/3D-PolarCordinates and https://github.com/591291-hvl/Lorenz-System.

Three.js has multiple examples, so i just found an example for a rotating cube. Removed the texture and edited the rotation to be the latest x and y rotation value stored in the array.

Function to initialize the 3D-object.

```
function init() {

    camera = new THREE.PerspectiveCamera( 70, window.innerWidth / window.innerHeight, 0.1, 100 );
    camera.position.z = 2;

    scene = new THREE.Scene();

    const geometry = new THREE.BoxGeometry();
    const material = new THREE.MeshBasicMaterial( { color: "ff0000" } );

    mesh = new THREE.Mesh( geometry, material );
    scene.add( mesh );

    renderer = new THREE.WebGLRenderer( { antialias: true } );
    renderer.setPixelRatio( window.devicePixelRatio );
    renderer.setSize( window.innerWidth, window.innerHeight );
    document.body.appendChild( renderer.domElement );

    window.addEventListener( 'resize', onWindowResize );

}
```

The rotation function in three.js uses radians for rotations, so i did a simple degree to rad convertion. This code is inside the same function that handles new rotation data and updates the chart.

```
mesh.rotation.x = (parseInt(xArray[xArray.length - 1])*Math.PI)/180;
mesh.rotation.z = -(parseInt(yArray[yArray.length - 1])*Math.PI)/180;

renderer.render( scene, camera );

```

## Result

<img src="{{ '/assets/images/drone_website.gif' | prepend: site.baseurl | prepend: site.url}}" alt="Displaying drone data on a website" height=400px/>

<img src="{{ '/assets/images/drone_website0.gif' | prepend: site.baseurl | prepend: site.url}}" alt="Displaying drone data on a website" height=400px/>


## Discussion

- Something that could have been really fun would be to make an interface on the website that controls the drone. I think it could have easily been done by encoding a string with four values corresponding to the four joystick values used to controll the drone. I mostly decide against doing this because i dont see it as a challenge and i dont see it providing any real value to the project as a whole.

- The cube displayed on the site should ideally have been modeled to look like the drone. Since i am rotating a mesh of a box, i could create a mesh of the drone. Unfortunately i have not done this yet. The drone frame i am using is from a kit and not designed and 3D-printed. A goal future goal for this project is to design everything my self. So if i end up doing it, i could swap model for the website.