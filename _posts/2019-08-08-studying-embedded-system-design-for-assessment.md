---
excerpt_separator: "<!--more-->"
layout: post
title: Studying Embedded System Design for Assessment
tags:
- study
feature-img: ''
thumbnail: https://nirav.com.np/assets/img/pexels/circuit.jpeg

---
Studying for exams is so boring, you know? You study and study, with no intention or time to put any of it in practice, just so that you can wake up super early one morning, rush to the exam hall, make sure you haven't forgotten your admit card, and regurgitate it all with teachers patrolling like vultures, as if we're prisoners.

We have test of Embedded system tomorrow. So I want to test if writing about what I'm studying in my blog will motivate me better. In this post, I'll try to summarize everything I manage to study today. I'm using the Frank Vahid and Tony Givargis book, and I'll be following the IOE syllabus (CT 655). A lot of the information below, including the diagrams, is summarized, paraphrased or downright plagiarized from the book.

<!--more-->

# Introduction

There doesn't seem to be a universally applicable definition of embedded systems. The book says, "An embedded system is any computing system other than a desktop computer." I don't like this very much. Richard Nass from embedded.com describes embedded system as, "any computer whose end function is not to be a computer". This is slightly better. But this won't do for the exam. Teachers expect definitions to be long and full of jargon.

Let us look at some examples and characteristics of these systems. Embedded systems are put into electronic and electric devices like cameras, phones, washing machines, printers and so on to electronically control other parts of the system. So if you want your device to react to events, or perform a coordinated sequence of procedures, you'd embed an embedded system into it. Some characteristics particular to embedded systems are:

1. **Single-functioned**  
   Embedded systems are designed to perform a single, or a set of closely related functions repeatedly. This characteristic distinguished embedded systems from desktop and mobile computing systems which support general programmability and the ability to perform virtually any conceivable algorithm. Modern smartphones shouldn't be classified as embedded systems because they are general-purpose.
2. **Tightly constrained**
   Embedded systems often have to be kept in small, cheap, battery operated devices. So, they are designed with constraints on power usage, size and price.  This naturally means that the system will have the _bare minimum_ resources necessary to execute the expected functions reliably. The clock speed, component count, power usage, RAM size, CPU power, number of pins, the size of the components relative to the PCB area, the EMF radiated, and every other factor has to be carefully analyzed and minimized.
3. **Reactive and real-time**  
   Many embedded systems are meant as control systems. They monitor the inputs and generate outputs that must vary in real time and be sufficiently accurate. Consider a car's Electronic Braking Mechanism. Failure in such systems can't be tolerated. There are hard constraints on the time it takes for the system to crunch the inputs and generate an output. In contrast, desktop computing systems are not expected to react with millisecond or microsecond level granularity.

## Digital Camera Example

I didn't want to write this, but they ask this in the exam.

![](https://nirav.com.np/assets/img/esfig1.jpg)

As is evident from the horrid diagram I've drawn (cut me some slack, guys. I picked up this thing a day ago), the camera is a complex ES. A Charge-Coupled Device (CCD) captures the image, which is converted to digital signals using the Analog to Digital converter (A2D). The CCD preprocessor is the chip that controls the CCD and gives it low level commands. The JPEG codec compresses and decompresses the image, because RAW photos take up heck ton of storage space. This part gives very little information on what the pixel coprocessor does, but I'm assuming it is able to parallelly perform operations on a lot of pixels at once (color correction, noise filtering and stuff like that) without overloading the microprocessor. The multiplier/accumulator does mathematical computations which take a lot of time when done by the microprocessor. All other components are self-explanatory.

This camera is a great example of an ES. It is small, portable, battery operated and it performs a group of closely related functions repeatedly. It must be fast enough to process many images per second, consume little power, be low cost and all that. But the camera isn't obligated to be real time. As far as the photographer is concerned, one second latency is not dangerous.

# Design Challenges

I'm getting tired of typing in Embedded System all the time. So from here onwards, I'll write ES instead. Anyway, as we saw in the characteristics, ESes have to be optimized for tons of factors. In this section, we'll talk about some important design metrics and trade-offs.

## Common Design Metrics

A design metric is a measurable feature of a system's implementation. Here's a short list:

 1. **Non-Recurring Engineering cost**: One time cost need for R&D.
 2. **Unit cost**: Price of building one copy of the system. NRE cost not included.
 3. **Size**: Both software size and hardware size needed to implement the system.
 4. **Performance**
 5. **Power Consumed**
 6. **Flexibility**: ability to alter functionality of system without incurring additional NRE cost.
 7. **Time-to-prototype**: How long will it take to create a working proof-of-concept?
 8. **Time-to-market**: How long will it take to sell the finished product? Take design time, manufacturing time and testing time into account.
 9. **Maintainability**
10. **Correctness**
11. **Safety**

## The Time-to-Market metric

It is more profitable if you launch your product within a fixed window. For ESes this window is very small, because the market is competitive. Sometimes, each day delayed causes more than a million dollar loss.

But because ES design has become increasingly complex, it is hard for the designer to do more in less time. Consider a simplified diagram below:  
![](https://nirav.com.np/assets/img/esfig2.jpg)

The areas under these triangles are proportional to the revenues generated in each scenario. The revenue loss can be calculated using the above diagram:

> percentage revenue loss = (D (3W-W)/2W<sup>2</sup>)*100

Clearly, it is important to market the product in time. To do this, the designer has to be aware of all the latest technologies and have expertise in both hardware and software design. 

## NRE and Unit Cost

The measures we are concerned with are:

> Total Cost = NRE cost + Unit cost * number of units
>
> Per-product cost = Total Cost / Number of units = NRE Cost / Number of units + Unit cost

The total cost increases linearly with increase in quantity. That is obvious. But the per-production cost decreases hyperbolically with quantity because the NRE cost gets shared among the units. If your product requires lot of R&D but is sold for less money, you can profit by selling large quantities of it (of course, in literally every other case you profit by selling large quantities of it).

## Performance

Measures of performance help understand how long it will take to execute the functions we require. Clock speed, instructions per second, sampling frequency, etc. help measure performance. But these metrics are not well suited for getting specialized understanding of the system at hand. We should be more concerned with factors like how many functions it can execute in a second, or how fast will it react to events, and things like that. It doesn't matter if the washing machine has a 128 kHz processor if it can get the motor rolling on the press of a button. 

Some better measures of performance are:

1. _Latency_ or _response time_: Time between the start and end of a process.
2. _Throughput_: Number of high level functions that can be executed per second.

When comparing two systems, we use _speedup_ which is simply a ratio of the performance of a pair of systems. 

# Processor technology

This book says, "technology is a manner of accomplishing a task, especially using technical processes ...", which is interesting because even though I have used the word technology a lot, I never thought about what it really meant. 

## General-Purpose Processors

Also called microprocessors. Defining characteristic of General-purpose processors is that they have a program memory necessary to hold data in them. They have a wide variety of peripherals embedded in the chip to maximize flexibility. They have a general data-path to allow whatever software to run on them. With general purpose processors, the designer has to mainly worry about software, which is very easy to modify, debug or throw away. Advantages include flexibility, maintainability, lowered NRE and Time-to-market, and ease of use.

But these processors have a lot of features and peripherals that go unused, while still taking up space and costing money. If the quantity is large enough, then it is cheaper to build a custom single-purpose integrated circuit (NRE is cancelled out by the scale). Also, for applications requiring parallel data processing (facial recognition, pixel processing, audio processing etc. the microprocessor is woefully inadequate. Also, when not properly selected, microprocessors are wasteful (for example, when someone uses an AVR or Arduino to control LED brightness).