---
excerpt_separator: "<!--more-->"
layout: post
title: Studying Embedded System Design for Assessment
tags:
- study
feature-img: ''
thumbnail: ''

---
Studying for exams is so boring, you know? You study and study, with no intention or time to put any of it in practice, just so that you can wake up super early one morning, rush to the exam hall, make sure you haven't forgotten your admit card, and regurgitate it all with teachers patrolling like vultures, as if we're prisoners.

We have test of Embedded system tomorrow. So I want to test if writing about what I'm studying in my blog will motivate me better. In this post, I'll try to summarize everything I manage to study today. I'm using the Frank Vahid and Tony Givargis book, and I'll be following the IOE syllabus (CT 655).

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

As is evident from the horrid diagram I've drawn (cut me some slack, guys. I picked up this thing a day ago), 

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