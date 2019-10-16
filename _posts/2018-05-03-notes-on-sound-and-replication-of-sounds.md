---
title: Notes on sound and replication of sounds
date: 2018-05-03 00:00:00 Z
published: false
layout: post
feature-img: ''
thumbnail: ''
---

I have been reading about sounds for the past few days. I have written this post as a note that I can refer to in the future. As such, details might have been left out for conciseness. I will, however, link to sites that helped me learn about sounds for reference.

A little background: The reason I wanted to learn about sounds was because I wanted to create an electronic circuit that can play back a recording; Basically an attiny controlled speaker that says 'Hi'. 



The way computer gets around this, obviously, is by using numbers. essentially, a certain range of voltages gets a specific number. A sample is in essence an pixel in time. But the thing about sound is that a pixel is nothing. Sound is made by motion. By change. As such, it is not the sample that represents the sound but rather its the change from the previous sample to that sample, and then from that sample to the next sample and so on that actually represent sound.


    (quantize s 2)
    (sum s -0.5)
    (sum s 0.5)
    
I did this to 