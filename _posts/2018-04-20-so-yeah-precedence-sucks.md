---
layout: post
published: true
title: The Long Sad Story Of How My Life Was Ruined By Precedence In C
tags:
  - random
  - code
  - thoughts
  - ATtiny
---
Did you know that the equality (==) operator takes precedence over bitwise operators(&, |) in c? You probably did, because you must have memorized the precedence table in the first semester. Being a lazy ass, however, I didn't. Now, at that time, I didn't think much of it because I could use parenthesis whenever I was confused about precedence. I was wrong.

Let me tell you a sad story. Few days ago, I decided that I should start practically learning electronics. This was mostly because I am going to fail EDC this semester (having written 3 Harry Potter fanfictions to pass time in the exam hall). Thus I bought random capacitors, transistors, diodes and the like. I also already had an ATtiny13 and an Arduino. So I download the AVR toolchain and the trusty avrdude, and decide to learn the avr dialect of C. It was lovely. The datasheet detailed every little register, all the bits that could be flipped to output highs and lows. This was all beautiful because this would allow me to use my programming knowledge to make real physical things happen (IRL!!). So yeah, I fantasized, I dreamed, I made little sketches and designs of things I would eventually make. Hell, I even read books on product designing.

Turns out, reality is harsh. Cold and unforgiving. I paid back for the slacking off in first sem. Fuck this world that runs on debts and karma.

What happened was I got things connected just fine. I could program the tiny using avrdude and Arduino Uno as the ISP. Sure, I had some fun. I made leds blink; and using my L293D IC ran motors. Obviously the next step was reading inputs. The lovely datasheet describes how output and input works on the tiny. There are registers in the system that keep track of whether a certain pin on the chip will function as output or input. These are the DDRs. Flipping, for instance, the fourth bit of DDR to one will enable you to use the pin right below reset pin as an Output pin. Then, flipping the fourth bit of PORTB register will turn it on. Essentially, now you can connect a led to that pin and ground and the led lights up! Nice.

Then there are the PIN registers, which tell you whether the input to a certain pin (that has been set to a 0 in DDR) is High or Low. So I went ahead and wired the circuit. In fact, in the next 2 days, I had wired the same circuit and its various functionally equivalent circuits millions of times. It just didn't work. I checked everything. The push button giving the input could be faulty. So I tried shorting the pins. Nothing. I tried changing the pins, bla bla. Nothing. The led was indifferent to the button. I was melancholy. I tried changing the breadboard. I even tried external pull ups and pull downs, because maybe I had somehow fucked the internal one. Nothing.

Now, I have always thought myself to be a good programmer. Granted, I never finsh anything I start, but my programs always have the well designed architectures and well placed data strucutres. But I had skipped several topics that I decided weren't important enough. One of the topics I always skimmed through was the topic of bitwise operators. And rightly so. There is barely any situation when you actually need them while programming the high level stuff.

Reading the example code in the datasheet made me realize that there was no clean way to set a flip a bit in C. You would have to operate on an entire byte of register (like DDR) at a time with bitwise operators. Nice, I said. I had a reason to read bitwise operators now. I then wrote the following code:

	#define F_CPU 1200000
    #include <avr/io.h>
    
    int main(){
    DDRB = 0x10;    // 00010000 : Set the pin PB4 as an output pin
    PORTB = 0x18;   // 00011000 : Set the pin PB4 to High (LED is connected here)
    				// and turn on internal pullup resistor on pin PB3
                    // this means that when switch is not pressed, the corresponding PIN bit is high

    while (1){
    	if (PINB & 0x08 == 0)   // if switch is ON (PB3 is reading LOW)
        	PORTB = 0x08; // turn off the led
        else
        	PORTB = 0x18; // turn on the led
        }
    }

I had worked out the hexadecimal numbers on paper to check for errors. I had consulted the datasheet again and again to make sure that the pins on the tiny matched with the pins I was setting and reading from. Sure, the register values are hardcoded and it shouldn't be done this way. But for something so simple, I didn't have to adhere to the correct coding practice.

But the circuit didn't work, you see. I went bald from going pulling on my hair, the switch didn't work. I lost my chin beard from stroking it too hard, the switch didn't work. Nothing I did made any difference, the switch just wouldn't work.

It was because I was new to electronics, I had already unconsciously decided that problem was with the circuit, and not the code. I didn't give the code a second thought.

Any logical person would think that the == operator has to be applied last. You can not check if 2 expressions are equal without evaluating them first. For instance 2+2=4 evaluating to 2+(2==4) makes no sense. Well, it turns out, that is exactly how bitwise operators are treated. In short, `PINB & 0x08 == 0` is treated like `PINB & (0x08 == 0)`. This is ridiculous.

So in the end, after several sad days of contemplating the melancholy Chopin and furiously banging my head on the  wall because of tears in my eyes, I looked back at the code. I made 2 changes, both of them I thought to be redundant. BUT IT WORKED.

	#define F_CPU 1200000
    #include <avr/io.h>
    
    int main(){
    DDRB = 0x10;    // 00010000 : Set the pin PB4 as an output pin
    PORTB = 0x18;   // 00011000 : Set the pin PB4 to High (LED is connected here)
    				// and turn on internal pullup resistor on pin PB3
                    // this means that when switch is not pressed, the corresponding PIN bit is high

    while (1==1){
    	if ( (PINB & 0x08) == 0)   // if switch is ON (PB3 is reading LOW)
        	PORTB = 0x08; // turn off the led
        else
        	PORTB = 0x18; // turn on the led
        }
    }
    
With tears of happiness welling up in my eyes, I thought, "Ohh, so 1 does not evaluate to a true with avr-gcc! The while loop wasn't working."

No. Okay most of this story is exaggerated but it was quite frustrating. And I was stupid. But well, that is what it is and I have most definitely learnt my lesson. Time to dream of more cool spy equipment I can make with this.