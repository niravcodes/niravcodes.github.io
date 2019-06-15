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

I was asked to animate a dot-matrix display for the robotics club recently. They wanted something that said "Robotics Club" to hang over their door. We had some old P10 (1r) DMDs which I had worked on in the past to make a little scoreboard for the robot football. Plus, even though I suck at it, I really love making animations. So I decided to give it a shot.

<!--more-->

This is the final result:

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/zjk1e-JFNFA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Yes. That's a little Wall-E looking at you. After thinking long and hard about it, I decided that Wall-E would be the best robot to look over us all while we do our stuff.

I wanted to animate some other things too, like a gear train driven by a hamster, and GIR from Invader Zim (remember that show?). But of course, a monochrome 32x32 matrix doesn't give you much space to play with. I was also limited by time. I'm working almost full time on our [minor project](), and I also have to attend my classes. For the next version, I'm planning a much cooler animation, that takes up the whole 32x32 screen.

I'm going to talk about all the things I did to make the thing.

# Electronics

I made all the electronics for the project last semester with [Bhuwan](https://bhuwanadhikari.com.np/). We made the circuit board by hand, doing everything from hack-sawing the PCBs, etching the copper traces with a fumigating solution of FeCl<sub>3</sub>, drilling the boards and soldering the components. That process, while manual, was very enjoyable. The resulting circuit looks nice and works very well.

![](https://nirav.com.np/assets/img/one.jpg)

The board is straightforward. It's an Atmega32A with it's support circuitry (oscillators, decoupling capacitors and such) and a bunch of headers: one for connecting the In-System Programmer, one for connecting to a control remote, and one for the Dot-Matrix display.

The display itself (`P10(1r)-V70`) is a matrix of LEDs all connected to a bunch of `74HC595` shift registers in series. I had worked with these in the past, so I understood the mechanism of the board very easily. The DMD takes the following inputs:

1. Output Enable (OE)
2. Row Selectors (A and B)
3. A data line (D)
4. A clock line (CLK)
5. A Latch line (SCLK)
6. A ground

The data line D inputs the data serially, clocked by the CLK line. On the rising edge of the SCLK pin, the data shifted in is displayed on the LEDs. So far, it is exactly as if we were using the 74HC595 directly. But the row selectors complicate things slightly. The people who designed this board have done something really cool. Perhaps to reduce part count, or to keep the board layout simple, or maybe because of fanout issues, they have connected every fourth row of the LEDs to the same set of shift registers. Which row of the matrix you are addressing depends on the inputs to the selector pins. That is, for A = LOW, B = LOW, the first of the four rows is selected; for A = LOW, B = HIGH, the second; and so on.

# The Animation Software

For various reasons, I had to write the animation software myself. The last time, I had written an animation program on Python using Tkinter. Actually, 'written' is a bad verb to describe that process. I had jerrybuilt the whole system in an hour. And over the course of the next week, I had haphazardly stuck various appendages and functions which made the code very difficult to navigate. On top of that, the program itself was very ugly. So this time, I picked a language I have worked with a little before: JavaScript. I had never gotten a chance to play with the HTML5 canvas API, but it literally takes [5 minutes]() to get the hang of it. 

This time, I took a whole day to make the program. It is still bad code, and is very inefficient in all respects. But because it is a means to an end, I allowed myself to take shortcuts. The result is the screenshot below.  
![](https://nirav.com.np/assets/img/Screenshot-2019-6-15 Animator-inator.png)

This is the software I made

# The Firmware

The firmware was very simple to write. But 