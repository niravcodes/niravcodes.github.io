---
layout: post
published: true
title: I didn't find schottky diodes in Pokhara
tags:
  - thoughts
  - electronics
  - tinkering
---
Long story short, I made charge pump. Charge pump is a sweet little circuit that takes in a voltage and a clock input and outputs a multiple of that voltage.

I was instantly smitten by the simplicity of this beautiful configuration. I decided that this is the best way to run my attiny with a single AA cell. 

So I made myself a little astable oscillator circuit using 2 transistors and 2 capacitors. Then I fed the output of this oscillator to the charge pump which I must remind you is a sweet little circuit. To double the voltage you only need 2 capacitors and 2 diodes.

Well, it worked. Sort of. When I ran it off a 3.3v supply, It gave me a 6v output on no load. When I connected a reasonable load resistor across it, it still ran at about 5.8V. That was all I needed. Then I hooked it up to the AA cell. On no load it showed 2.5V. This is great, I thought. I was basically increasing the voltage of a battery without any external components (Switcher ICs or boost modules).

But then I connected it across the load resistor. Whooss. Down to 1.4V it was. Now I knew that the pump wouldn't be perfect. I required something >1.8V to power the Attiny. That's not a lot to ask for from a voltage doubler, is it?

I knew that if there was a problem somewhere, it was my use of general purpose 1N4007 diode. If only I could replace it with a Schottky, I would be all set.

*I will write the next part tomorrow.*
