---
layout: post
title: The pain of falling from 16 to 2KB and an EEPROM Programmer in Arduino
tags:
- code
- electronics
- eeprom
- arduino

---
So EEPROM sizes are measured in bits... who knew. I spent the last several days in the happy illusion that I had EEPROM chips capable of holding 16KB of data. With 16KB, I can store about 4 seconds of 4 bit data sampled at 8000 khz, which is enough for my little sound playing project.

But, when I revisited the datasheets yesterday, I realized that the B in KB actually stood for bits. Ahh, the pain of falling from 16 kilobytes down to two.

One must, however, learn to improvise adapt overcome hence I downsampled the audio to 4khz and truncated the sound sample down to 2KB. It hurt.

On a merrier note, here is the code I wrote to program the EEPROM chip I have (AT24C16A) in arduino.

Note that the data writing part is commented out. I should have taken some time to format and automate the code, but that's how it ended up.

{% highlight c linenos %}
#include <I2C.h>
//oppai sound from High School DXD as a tribute XD
unsigned int data_len = 0; // Define your length here
const char oppai\[data_len\] PROGMEM = {
// put the bytes here
};
void setup() {
// put your setup code here, to run once:
I2c.begin();
I2c.setSpeed(true);
Serial.begin(38400);
}

void loop(){
delay(2000); // in case I accidentally power arduino and corrupt data
/*
char data\[16\];
bool dataexhausted = false;
for (unsigned char  i = 0; i < 128; i++){

    //put 16 bytes from progmem into data here
    for (unsigned char x = 0; x < 16; x++){
    
    data[x] = pgm_read_byte(&(oppai[i << 4 | x]));
    if ( (i*16 + x)>=sizeof(oppai) ) {
    for (unsigned char m = x; m < 16; m++){
    data[m] = 0;
    }
    dataexhausted = true;
    break;
    }
    }
    
    //compute the device and word address here
    char device_address = 0x50 | (0x07 & (i >> 4 ));
    char dwordaddress = i << 4;
    
    //perform the final write here.
    /* debug information 
    Serial.print("I2c.write("); 
    Serial.print(device_address, HEX);
    Serial.print(", ");
    Serial.print(dwordaddress, HEX);
    Serial.print(", ");
    for (int j = 0; j < 16; j++) {Serial.print(data[j], HEX); Serial.println(", ");}
    Serial.println(")");
    Serial.println(i, DEC);
    Serial.println("-------------------------------");
    Serial.println("");
    
    
    I2c.write(device_address, dwordaddress, data, 16);
    
    //debug information
    Serial.print(i);
    Serial.println(" written");
    
    delay(12);
    
    //if data finishes before eeprom storage does (as it should) break the loop
    if (dataexhausted == true) break;
    }
    Serial.println("Finished!");
    Serial.println("echoing back bytes");
     */
    
    I2c.read(0x50, 0x00, 16) ;
    for (unsigned char i = 0; i < 128; i++){
    	for (char j = 0; j < 16; j++) Serial.println(I2c.receive(), HEX);
    	I2c.read(0x50, 16) ;
    }
    
    /*I2c.read(0x50,0x00,16);
      for (char i = 0; i < 16; i++){
      Serial.println(I2c.receive());
      }*/
    
    while (1) ;

}
{% endhighlight %}

It uses the I2C library provided on [dsscircuits.com](http://dsscircuits.com/articles/arduino-i2c-master-library).