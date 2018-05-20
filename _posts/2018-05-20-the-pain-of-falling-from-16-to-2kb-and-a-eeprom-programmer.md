---
layout: post
published: false
title: The pain of falling from 16 to 2KB and a EEPROM PROGRAMMER
---
So EEPROM sizes are measured in bits... who knew. I spent the last several days in the happy illusion that I had EEPROM chips capable of holding 16KB of data. With 16KB, I can store about 4 seconds of 4 bit data sampled at 8000 khz, which is enough for my little sound playing project.

But, when I revisited the datasheets yesterday, I realized that the B in KB actually stood for bits. Ahh, the pain of falling from 16 kilobytes down to two.

One must, however, learn to improvise overcome adapt hence I downsampled the audio down to 4khz and truncated the sound sample down to 2 kb. It hurt.

Here is the code I wrote to program the EEPROM chip I have (AT24C16A)