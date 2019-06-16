---
layout: post
title: 'DRAFT : On the Nepali Language and Unicode'
tags: []
feature-img: ''
permalink: "/draft2/"
hide: true

---
_Notes: The numbers starting with ‘0x’ are Hexadecimal numbers._

The Nepali language gets very little representation on the internet. Take, for example, the Nepali Wikipedia which has about 33 thousand articles. The Esperanto Wikipedia boasts 8 times that number (at around two hundred thousand articles). Which is kind of sad, because Esperanto is an artificial language created by **one** person in the 19th century. It is spoken by a meager 2 million people worldwide. Compare this to the Nepali language, which has more than 25 million speakers.

It's as they say, “whoever controls the media controls the mind”. And the media of the 21st century, the internet, is so desperately out of the Nepali’s hands that, not only do we read the news, articles, the weather, and novels in English, but we go on to caption our photos, of warm, intimate moments in English. My little brother, who is not even 10, will sniff my phone from a mile away and hide out in some corner to watch Motu Patlu, the Hindi cartoon, on YouTube. He might not be as fluent in Hindi as he is in Nepali. But in his little world, Hindi is the language that superheroes speak. And Nepali? Only his annoying brother.

...

Now don’t get me wrong here. I am not saying that at some point Nepali will just disappear into oblivion. What I’m saying is that, without even knowing it, we’ll wake up one day to find our own language so detached, so out of sync from the everyday reality which we live in, that it will just stop meaning anything important. And that, when we finally realize it, we will not feel दुःखि or even चिन्तित. We’ll feel ‘depressed’. So no, I’m not saying that it will be forgotten. Much worse. It will be neglected, much like one of those pencils which fall into the space between the bed and the wall and which we just leave there.

It’s as T.S. Eliot once wrote,  
“This is the way the world ends  
Not with a bang but a whimper.”

<< fill in about motivation for this article and about unicode ...>>

# ASCII

All discussion of character encoding in the computer must begin with the ASCII ...

Computers only understand numbers. To a computer, a picture is not, say, people or the hills, but a 2D matrix of numbers representing the color values at each point. An audio recording is not two people speaking, nor, maybe a string quartet, but simply a sequences of numbers representing amplitude of the pressure wave felt by the recorder. It goes without saying that text is also read by the computer as a sequence of numbers. A string, as the programmers call it.

ASCII is simply a mapping from numbers to characters. So if you put the number 65 in the memory of a computer and ask it to print out what the number means, it will print a capital A.

ASCII was the first widely adopted encoding scheme. But, as the name says, it’s American.

**Unicode**

The Unicode is a specification. It standardizes what number inside the computer represent what character from language. Unicode currently encodes 1,37,994 characters from scripts throughout the world.

For Devanagari, Unicode has allocated the space from 0x0900 to 0x097F.

![](https://nirav.com.np/assets/img/2019-06-16-175754_1366x768_scrot.png)

And this image

![](https://nirav.com.np/assets/img/2019-06-16-174910_1366x768_scrot.png)

and this image

![](https://nirav.com.np/assets/img/2019-06-16-180457_1366x768_scrot.png)

andmany more

SUBHEADINGS:

1. ASCII
2. UNICODE
   1. Representation
   2. UTF
   3. input
   4. rendering
3. Devanagari
   1. fonts
   2. specification
   3. Ligatures क्ष श्र त्र ...
   4. virama
4. For designers
5. For developers