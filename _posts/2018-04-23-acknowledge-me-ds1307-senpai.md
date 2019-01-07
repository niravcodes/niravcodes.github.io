---
layout: post
title: Acknowledge me, DS1307 senpai!
tags:
- code
- electronics
- avr

---
I might be one of the few people who find 2 ICs talking to each other absolutely cute, but so be it.

Yes, I hooked up my cute little 8 legged ATtiny to a similarly cute DS1307 RTC chip using I2C. Self implemented I2C. Sure, it is pretty easy, but see, *it had leds*. I used a very small frequency(0.5Hz) for the clock and put leds on the data and clock lines. So it was practically like watching 2 chips talk to each other. And when the DS1307 chip pulled the line low for the first time, it was positively like looking at 3x10^8 kittens at once yes it was that wild.

So anywho, after I had had my fun and I made the chips say hello to each other and so on and so forth. I did little experiments on a breadboard to make sure my understanding of the protocol was complete. The highlight of today was storing and retrieving a byte from the SRAM of the DS chip. Even though I wrote the program myself, it was really amazing to see the communication take place in real life. It was specially fun to look at the DS echo back what the tiny had previously written to the SRAM. It was almost like it was alive and sentient. I might give a name to it and keep it as a pet.

I have done all the experiments I need. I now just need to build a little library that encapsulates the I2C communication. The write experiment code is below. (They are very ugly)

{% highlight c linenos %}
//Experiment #4 where I test if I can write to the SRAM

#define F_CPU 1200000UL

#include <avr/io.h>
#include <util/delay.h>

#define FREQUENCY 1000  //frequency of i2c data transfer
#define SDA PB3
#define SCL PB4

	void clockon();
	void clockoff();
	void sendzero();
	void sendone();
	void sendbit0();
	void sendbit1();
	void dance();
	void wait();
	void ledon();
	void ledoff();
	void cry();
	void waithalf();
	int main(){
		DDRB = 1<<SCL | 1<<PB0 | 1 << SDA; //SCL ALWAYS IN OUTPUT MODE

		PORTB = 0x00 ; //sda has intern4al pull up resistor enabled
		wait();

		sendone();
		wait();
		// START
		clockon();
		wait();
		sendzero();
		wait();
		clockoff();

		//send address bit of D1 = 11010001;
		sendbit1();
		sendbit1();
		sendbit0();
		sendbit1();
		sendbit0();
		sendbit0();
		sendbit0();
		sendbit0();

		sendone(); // wait for ack;
		wait();
		clockon();
		wait();
		clockoff();

		wait();

		sendbit0();
		sendbit0();
		sendbit0();
		sendbit0();
		sendbit0();
		sendbit0();
		sendbit0();
		sendbit0();

		sendone(); // wait for ack;
		wait();


		clockon();


		for (int i = 0; i < 1000; i++){
			if ((PINB & 1<<SDA) == 0x00){
				//success

				dance();
			}
		}
		cry();

	}

void dance(){
	while (1){
		PORTB |= 0x01;
		_delay_ms (500);
		PORTB &= ~(0X01);
		_delay_ms (500);
	}
}
void cry(){
	ledon();
	while (1) {}
}

void sendbit1(){
	waithalf();
	sendone();
	waithalf();
	clockon();
	wait();
	clockoff();     
}
void sendbit0(){
	waithalf();
	sendzero();
	waithalf();
	clockon();
	wait();
	clockoff();
}

void wait(){
	waithalf();
	waithalf();
}
void waithalf(){
	_delay_ms(500);
}
void ledon(){
	PORTB |= 0x01;
}
void ledoff(){
	PORTB &= 0xFE;
}
void sendzero(){
	DDRB |= 1<<SDA;
	PORTB &= ~(1<<SDA);
}
void sendone(){
	DDRB &= ~(1<<SDA);
}
void clockon(){
	PORTB |= 1<<SCL;
}
void clockoff(){
	PORTB &= ~(1<<SCL);
}
{% endhighlight %}

And the read code is here.

{% highlight c linenos %}
//Experiment #5 where I test if the byte was written

#define F_CPU 1200000UL

#include <avr/io.h>
#include <util/delay.h>

#define FREQUENCY 1000    //frequency of i2c data transfer
#define SDA   PB3
#define SCL   PB4

void clockon();
void clockoff();
void sendzero();
void sendone();
void sendbit0();
void sendbit1();
void dance();
void wait();
void ledon();
void ledoff();
void cry();
void waithalf();
int getreading();
int main(){
	DDRB = 1<<SCL | 1<<PB0 | 1 << SDA; //SCL ALWAYS IN OUTPUT MODE

	PORTB = 0x00 ; //sda has intern4al pull up resistor enabled
	wait();

	sendone();
	wait();
	// START
	clockon();
	wait();
	sendzero();
	wait();
	clockoff();

	//send address bit of D1 = 11010001;
	sendbit1();
	sendbit1();
	sendbit0();
	sendbit1();
	sendbit0();
	sendbit0();
	sendbit0();
	sendbit0();

	sendone(); // wait for ack;
	wait();
	clockon();
	if(((PINB & 1<<SDA) == 0)) {ledon(); wait(); ledoff();}
	clockoff();

	wait();

	sendbit0();
	sendbit0();
	sendbit0();
	sendbit1();
	sendbit0();
	sendbit0();
	sendbit0();
	sendbit0();

	sendone(); // wait for ack;
	wait();


	clockon();
	if ((PINB & 1<<SDA) == 0) {ledon(); wait(); ledoff();}
	clockoff();
	//now we would like to clock a 10101101 in the sram
	wait();
	sendbit1();
	sendbit0();
	sendbit1();
	sendbit0();
	sendbit1();
	sendbit1();
	sendbit0();
	sendbit1();

	sendone(); // wait for ack... I mean sendone should have been named release. that would've made sense

	clockon();
	if ((PINB & 1<<SDA) == 0 ) {ledon(); wait(); ledoff();}
	clockoff();

	sendone();
	clockon();
	waithalf();
	sendzero();
	waithalf();
	clockoff();
	/*int a = 0;
	  for (int i = 7; i >= 0 ; i--){  
	  wait();
	  clockon();
	  waithalf();
	  a |= getreading()<<i;
	  waithalf();
	  clockoff();
	  }

	  for (int i = 0; i < 1000; i++){
	  if (a != 0x00 && a != 0xff){
	//success

	dance();
	}
	}
	cry();
	 */

	while (1) {}

}

int getreading(){
	if ((PINB & 1<<SDA) == 0){
		return 0x00;
	}
	else return 0x01; 
}

void dance(){
	while (1){
		PORTB |= 0x01;
		_delay_ms (500);
		PORTB &= ~(0X01);
		_delay_ms (500);
	}
}
void cry(){
	ledon();
	while (1) {}
}

void sendbit1(){
	waithalf();
	sendone();
	waithalf();
	clockon();
	wait();
	clockoff();     
}
void sendbit0(){
	waithalf();
	sendzero();
	waithalf();
	clockon();
	wait();
	clockoff();
}

void wait(){
	waithalf();
	waithalf();
}
void waithalf(){
	_delay_ms(500);
}
void ledon(){
	PORTB |= 0x01;
}
void ledoff(){
	PORTB &= 0xFE;
}
void sendzero(){
	DDRB |= 1<<SDA;
	PORTB &= ~(1<<SDA);
}
void sendone(){
	DDRB &= ~(1<<SDA);
}
void clockon(){
	PORTB |= 1<<SCL;
}
void clockoff(){
	PORTB &= ~(1<<SCL);
}
{% endhighlight %}
