---
excerpt_separator: "<!--more-->"
layout: post
title: Animating WALL-E on a LED dot-matrix display with AVR
tags:
- animation
- avr
- c
- coding
- javascript
feature-img: https://nirav.com.np/assets/img/tow.jpg
thumbnail: ''

---
_Reminder to myself to compress the images_

I was asked to animate a dot-matrix display for the robotics club recently. They wanted something that said "Robotics Club" to hang over their door. We had some old P10 (1r) DMDs which I had worked on in the past. Plus, even though I suck at it, I really love making animations. So I decided to give it a shot. This is the final result:

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/zjk1e-JFNFA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Yes. That's a little Wall-E looking at you. After thinking long and hard about it, I decided that Wall-E would be the best robot to look over us all while we do our stuff. 

I wanted to animate some other things too, like a gear train driven by a hamster, and GIR from Invader Zim (remember that show?). But of course, a monochrome 32x32 matrix doesn't give you much space to play with. 

I was also limited by time. I'm working almost full time on our [minor project](), and I also have to attend my classes. For the next version, I'm planning a much cooler animation, that takes up the whole 32x32 screen. 

I'm going to talk about all the things I did to make the thing.

# Electronics

I made all the electronics for the project last semester with [Bhuwan](https://bhuwanadhikari.com.np/). We made the circuit board by hand, doing everything from hack-sawing the PCBs, etching the copper traces with a fumigating solution of FeCl<sub>3</sub>, drilling the boards and soldering the components. That process, while manual, was very enjoyable.

![](https://nirav.com.np/assets/img/one.jpg)