---
layout: post
title:  "Assignment 07: Web Interfaces, Server -> Client"
date:   2023-11-03 14:00:00 +0200
categories: Assignment
--- 


## List of content

- [Background](#background)
- [Design process](#design-process)
- [Result](#result)
- [Discussion](#discussion)


## Background

After multiple assignments where we have learned about different manufacturing techniques. Ways we interact with the device, and how the device interacts with the world. It is finally time to start learning how to create an IoT-device (Internet of things). For this assignment we are going to experiment with simple get requests and then plot the data we receive. 

# Design process

Since we want to send data from a server to a client we want an open port on a website that sends some data when i receives an get request. This might not be a completely accurate explanation, but this is how i understand it. When you connect your pc to the internet, it only alows communication through "ports". Each port has a function connected to it that handels a specific task and they are universal. Meaning that port 4000 is only used for Diablo II and nothing else. This is good system because it means that when information is sendt to a pc, it does not have to find the correct port. Web pages functions similarly, the /something on a webpage has a function that handels connections. These ports are not universal however, so i can use /getData without any problems.


Since i just want to send some data to display, i use sinus and a incremental variable so i can visualize a sinus curve on the client. This data is then sendt everytime the pathing /getData receives an request.

```
var time = 0;
const timeUnit = 0.1

app.get('/getData', (req, res) => {
    res.send({data: Math.sin(time*timeUnit)});
    time +=1;
});    
```


On the client side we want to display a .html file, in node the best way to do this is by redirecting the user to the .html file with the routint /, this is equivalent to the user writing example.com. instead of example.com/getData from above.

```
app.get('/', (req, res) => {
    res.sendFile(__dirname + '/index.html');
});
```

Since i am now trying to visualize a sinus curve chart.js works fine as a way to visualize the data. I declared a chart object with y-axis between -1 and 1. I am using 2 different arrays to store the data i am plotting, dataArray and labelArray.

```
var chart  = new Chart("myChart", {
    type: "line",
    data: {
        labels: labelArray,
        datasets: [{
        fill: false,
        lineTension: 0,
        pointBackgroundColor: "rgba(0,0,255,1)",
        data: dataArray
        }]
    },
        options: {
        legend: {display: false},
        scales: {
        yAxes: [{ticks: {min: -1, max:1}}],
        }
    }
});
```


Now the only thing we need is to get the data, this is done by the fetch method which returns a promise object. A promise is kind of a weird datatype that is best handled with asyncronus programming. A promise is a empty datatype that waits untill it fulfills its promise, by doing this is essentaly blocks the rest of the program from doing anything untill it gets fulfilled. This might be ok for really simple programs but for large programs this should never happen. We can circumvent the blocking by using asyncronous programming with the async tag. By placing an async tag before a function that uses fetch, the rest of the program does not wait for the fetch to get fulfilled and when the fetch gets fulfilled it blocks the kernal and runs the rest of the code inside the function.

What i did was use an async function that does fetch calls to /getData, a function that simulates time by calling itself and waiting, and a function that calls upon the asyn function and pushes the data to an array.

```
async function getData() {
    const response = await fetch("/getData");
    const data = await response.json();
    return data;
};
function pushData () {
    getData().then(data => {
    dataArray.push(data.data);
});
}

var time = 1;
function simulateTime(){
    setTimeout(function(){
        pushData();
        labelArray.push((labelArray[labelArray.length - 1]+1));
        
        if(dataArray.length > 100){
            dataArray.shift();
            labelArray.shift();
        }
        chart.update();
        time++;
        if(time < 1000){
            simulateTime();
        }
    }, 100)
}
simulateTime();
```



# Result

