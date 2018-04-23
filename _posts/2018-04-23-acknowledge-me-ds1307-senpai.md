---
layout: post
published: false
title: 'Acknowledge me, DS1307 senpai!'
---
I might be one of the few people who find 2 ICs talking to each other absolutely cute, but so be it.

Yes, I hooked up my cute little 8 legged ATtiny to a similarly cute DS1307 RTC chip using I2C. Self implemented I2C. Sure, it is pretty easy, but see,0 *it had leds*. I used a very small frequency(0.5Hz) for the clock and put leds on the data and clock lines. So it was practically like watching 2 chips talk to each other. And when the DS1307 chip pulled the line low for the first time, it was positively like looking at 3x10^8 kittens at once yes it was that wild.

So anywho, after I had had my fun and I made the chips say hello to each other and so on and so forth. I did little experiments on a breadboard to make sure my understanding of the protocol was complete. The highlight of today was storing and retrieving a byte from the SRAM of the DS chip. Even though I wrote the program myself, it was really amazing to see the communication take place in real life. It was specially fun to look at the DS echo back what the tiny had previously written to the SRAM. It was almost like it was alive and sentient. I might give a name to it and keep it as a pet.

I was really surprised to find that there was a little SRAM on the DS chip independent of the timekeeping features that I could use for literally anything.