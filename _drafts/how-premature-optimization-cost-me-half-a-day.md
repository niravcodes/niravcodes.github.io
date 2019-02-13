---
excerpt_separator: "<!--more-->"
layout: post
title: How Premature Optimization Cost Me Half A Day
tags: []
feature-img: ''
thumbnail: ''
date: 2019-02-12 17:11:38 +0000

---
I have been programming in 8-bit AVRs exclusively for some time to make things like huge Dot-Matrix Displays, self-balancing robots and DACs. And as it turns out, I have been unwittingly picking up the conventions specific to embedded programming and 8-bit devices.

The one that cost me some amount of consternation lately is the habit of using `unsigned char` instead of `int` when you can. On 8-bit AVRs, this is an important thing to do whenever you can, because they have extremely limited memories (counted in bytes!). It doesn't help that I often select the cheapest and least powerful chips in my box to do a job (which, incidentally, means that I find myself programming for the 8051 much frequently than I'd like).

So anyway, I seem to have carried over this specific ritual even when I'm programming for desktops. The idea is simple. If you are sure values don't exceed 256, don't use `int`. Of course, saving a few bytes doesn't matter much when you have the room for literally billions of bytes, but still, why be wasteful, right?

 Wrong. A couple of things:

1. As it turns out, most processors require data in the memory to be word-aligned. That is, a 32 bit system is only be able to read data at addresses that are divisible by 2. I suppose this is done to reduce the number of lines in the address bus but for whatever reason that's how it is. This essentially means that your one byte char might be occupying full 4 bytes of memory for alignment reasons.
2. It is likely that the `unsigned char` needs to be converted to `int` to perform arithmetic operations and then back. The smaller datatype you innocently chose for it's size cost you several extra clock cycles without actually saving any memory.

Of course, processors and compilers are complex beasts and the only way of being sure of these things is to benchmark extensively. 

What actually happened was this. I am programming a [Huffman compression program](https://github.com/niravcodes/huffman_compression "github link to huffman compression") because I have always been fascinated with data compression. I will talk about it a little more in a future post but for now suffice it to say that my implementation required a priority queue. 

Since I was sure that I would have less than or exactly 256 items in the queue, I decided to 