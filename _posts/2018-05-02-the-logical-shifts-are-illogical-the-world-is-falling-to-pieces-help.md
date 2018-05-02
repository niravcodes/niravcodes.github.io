---
layout: post
published: true
title: The logical shifts are illogical the world is falling to pieces HELP
tags:
  - code
---
*+1 for the clickbaity title. Ding!*

I'm obviously a fool for not realizing straight away that anything labeled logical is actually not logical at all in this sad world that we live in.

logical = ~logical;

My naïvety, perhaps coupled with my stupidity, cost me my entire afternoon debugging through a trivial program that accumulates the MSBs of 4 bytes into one byte. I needed it to convert a recording to 2 bits so that I could store it in my tiny attiny. Naturally that meant using the logical shifts, particularly the right shift.

So as it turns out, depending on whether the datatype(char in my case) is signed or unsigned, these "logical" operators can either be actually logical or change into the ugly arthimetic shifts(see notes section of the [wikipedia page](https://en.wikipedia.org/wiki/Arithmetic_shift)). The thing about these ugly arthimetic shifts is that they are not logical at all. Arthimetic shifts essentially mean division or multiplication by powers of two(refer to the wikipedia page) whereas logical shifts mean shifting a bit pattern whether left or right padded by either 0 or 1. 

So when the bitwise operators are named "logical" shifts, I don't see why there has to be any complication at all with regards to what kind of shift the programmer wants performed. This world has let me down again.

But well, what is done is done. I have yet again learned my lesson to not trust my intuition too blindly. [This is a previous example of me learning the same lesson](http://nirav.com.np/2018/04/20/so-yeah-precedence-sucks.html).
