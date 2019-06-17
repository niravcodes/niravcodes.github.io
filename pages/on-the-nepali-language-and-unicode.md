---
layout: post
title: 'DRAFT : On the Nepali Language and Unicode'
tags: []
feature-img: ''
permalink: "/draft2/"
hide: true

---
# Part one

The Nepali language gets very little representation on the internet. Take, for example, the Nepali Wikipedia which has about 33 thousand articles. The Esperanto Wikipedia boasts 8 times that number (at around two hundred thousand articles). Which is kind of sad, because Esperanto is an artificial language created by **one** person in the 19th century. It is spoken by a meager 2 million people worldwide. Compare this to the Nepali language, which has more than 25 million speakers.

It's as they say, “whoever controls the media controls the mind”. And the media of the 21st century, the internet, is so desperately out of the Nepali’s hands that, not only do we read the news, articles, the weather, and novels in English, but we go on to caption our photos, of warm, intimate moments in English. My little brother, who is not even 10, will sniff my phone from a mile away and hide out in some corner to watch Motu Patlu, the Hindi cartoon, on YouTube. He might not be as fluent in Hindi as he is in Nepali. But in his little world, Hindi is the language that superheroes speak. And Nepali? Only his annoying brother.

I'm not saying that I'm any better. If anything, I'm worse. I'm one of those people who, after being told a phone number, says, "Okay, repeat that. But in English". I've been writing blogs for more than a year now, and I haven't written a single Nepali post. Ask me to translate this very post to Nepali and watch how fast I run away.

Now don’t get me wrong here. I am not saying that at some point Nepali will just disappear into oblivion. What I’m saying is that, without even knowing it, we’ll wake up one day to find our own language so detached, so out of sync from the everyday reality which we live in, that it will just stop meaning anything important. And that, when we finally realize it, we will not feel दुःखि or even चिन्तित. We’ll feel ‘depressed’. So no, I’m not saying that it will be forgotten. Much worse. It will be neglected, much like one of those pencils which fall into the space between the bed and the wall and which we just leave there.

It’s as T.S. Eliot once wrote,  
“This is the way the world ends  
Not with a bang but a whimper.”

So far in this article, I have only talked about Nepali. But Nepal has a lot more languages than just Nepali. Lot of them are in a lot worse state than Nepali. For example the Nepal Bhasa (Newa) which was the lingua franca of Kathmandu Valley 80 years ago is now UNESCO listed engangered language. It is written in the Ranjana script and the Prachalit script. I want to talk about what mechanisms currently exist to support those languages too. 

It will be a long article, with many many things. So bear with me.

# Part two

# ASCII

_Note: The numbers starting with ‘0x’ and 'U+' are Hexadecimal numbers. 'U+' additionally implies that the number following it is a Unicode code point._

Computers only understand numbers. To a computer, a picture is not, say, people or the hills, but a 2D matrix of numbers representing the color values at each point. An audio recording is not two people speaking, nor, maybe a string quartet, but simply a sequences of numbers representing amplitude of the pressure wave felt by the recorder. It goes without saying that text is also read by the computer as a sequence of numbers.

ASCII is simply a mapping from these numbers to characters. So if you put the number 65 in the memory of a computer and ask it to show what the number means as text, it will _probably_ display a capital A.

ASCII was the first widely adopted character encoding scheme. It is still used. 

![](https://nirav.com.np/assets/img/2019-06-16-180457_1366x768_scrot.png)

and many more

So how do you type Nepali in ASCII? Well, you don't. ASCII is, by it's very definition, American. What you can do is is put a Nepali character's mask over an ASCII character. In other words, design a font which has Nepali characters instead of English ones. For example, in the above table, the Nepali letters द्व and अ are overlaid over the letter A. Based on what font you are using, you might have to type a different key on the keyboard to get the same Nepali alphabet.

**Unicode**

The Unicode is a text-encoding specification. It was designed from the ground up to support **all** scripts of the world. Unicode currently encodes 1,37,994 characters from 150 scripts throughout. 

In Unicode, each character gets it's own number. For example, the number 2325 (0x0915) uniquely identifies the Devanagari letter क, the number 70658 (0x11402) identifies the Newari letter 𑐂, the number 65 (0x41) the English capital letter A and the number 24859 (0x611b) the unified Chinese, Japanese and Korean letter 愛, meaning love. 

Scripts are given a block to live in. A block is essentially a range of numbers. For example, Devanagari lives in the U+

The advantage of separating language into blocks, is that each block can get it's own kind of treatment from the software. We know that all scripts behave differently. In Devanagari, some characters go above the previous character, some under. Some change the character itself. In Tibetean, characters stack up vertically. Persian and Urdu characters, when they appear can, change how the entire word looks. Not to mention that scripts have different directions of reading. Chinese and Japanese are written from top to bottom, right to left. Urdu is written from right to left, top to bottom. 

For Devanagari, Unicode has allocated the space from 0x0900 to 0x097F.

![](https://nirav.com.np/assets/img/2019-06-16-175754_1366x768_scrot.png)

And this image

![](https://nirav.com.np/assets/img/2019-06-16-174910_1366x768_scrot.png)

and this image

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
6. Metadatas on HTML, lang=np ...