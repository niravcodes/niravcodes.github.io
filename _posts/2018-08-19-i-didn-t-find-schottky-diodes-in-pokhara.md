---
layout: post
published: true
title: So I didn't find schottky diodes in Pokhara
tags:
  - thoughts
  - electronics
  - tinkering
---
Long story short, I made charge pump. This is very exciting to me because:

1. this is my first time making a DC-DC voltage converter.
2. I made a transistor based oscillator to generate clock signal.

This whole quest started when I decided that I wanted to make my circuits work with just one AA battery. There is something so elegant about a single AA battery. It is just a cylinder that can make circuits come alive. When you use 2 of them in an AA battery holder, it loses that simplicity.

I researched methods to convert DC voltages and came across two core methods.

1. Capacitor based voltage multipliers (Charge pumps)
2. Inductor based voltage converters (Buck-Boost converters)

I decided to use charge pumping method mainly because they exactly multiply the voltage. Whereas with buck or boost converters, the output voltage is dependends on, among other things, changes in output current. As such, you need a fairly complex circuit to monitor the output voltage constantly and change PWM duty cycle to regulate voltage. 

At 1.5v, I couldn't use my trusty old attiny to generate clock input. So I made myself a little multivibrator circuit using 2 transistors. Then I wired it's clock output into the clock input of the charge pump. Charge pump sure sounds fancy but on a breadboard it just looks like a series of capacitors connected by diodes.

Well, it worked. Sort of. When I ran it off a 3.3v supply, It gave me a 6v output on no load. When I connected a reasonable load resistor across it, it still ran at about 5.8V. That was all I needed. Then I hooked it up to the AA cell. On no load it showed 2.5V. This is great, I thought. I was basically increasing the voltage of a battery without any external components (Switcher ICs or boost modules).

But then I connected it across the load resistor. Whooss. Multimeter read 1.4 volts. Now I knew that the pump wouldn't be perfect. But I just required something greater than 1.8V to power the attiny. That's not a lot to ask for from a voltage doubler, is it? I was hoping that I could use the attiny to regulate a boost converter's output voltage and power the rest of the circuit with that.

The problem was that I was using 1n4007 diodes in the charge pump. These diodes cause roughly 0.6 V drop at low current draws. Since I had two of them in the circuit, I was effectively losing 1.2 volts just because of the diode. If we also consider the drops in transistors and capacitors, we could easily be losing 1.6 volts.

Schottky diodes have a voltage drop of around 0.3 volts. So the obvious solution to this would be to replace the diodes with schottkys. So I set off the next day to buy schottky diodes. And trust me when I say this, I DIDN'T FIND THEM. Nowhere. No schottkys in Pokhara.

I mean, sure, there are loads of things you can't find in Pokhara. But come on, why would electronics repair shops not have schottky diodes? I returned disappointed. I might look into using mosfets wired as ideal diodes but two mosfets would cost the same as a boost converter module so they are not ideal.

So in the end, what I learnt from this is that I can probably just wire up transistors on a double sided pcb to do things I have been doing with a microcontroller.