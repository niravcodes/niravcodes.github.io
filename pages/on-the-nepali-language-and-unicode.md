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

It's as they say, “whoever controls the media controls the mind”. And the media of the 21st century, the internet, is so desperately out of Nepali's hands that, not only do we read the news, articles, the weather, and novels in English, but we go on to caption our photos, of warm, intimate moments in English. My little brother, who is not even 10, will sniff my phone from a mile away and hide out in some corner to watch Motu Patlu on YouTube. He might not be as fluent in Hindi as he is in Nepali. But in his little world, Hindi is the language that superheroes speak. And Nepali? Only his annoying brother.

I'm not saying that I'm any better. If anything, I'm worse. I'm one of those people who, after being told a phone number, says, "Okay, repeat that. But in English". Ask me to translate this very post to Nepali and watch how fast I run away. My friends are no better. 

But the issue is pretty pervasive

Now don’t get me wrong here. I am not saying that at some point Nepali will just disappear into oblivion. What I’m saying is that, without even knowing it, we’ll wake up one day to find our own language so detached, so out of sync from the everyday reality which we live in, that it will just stop meaning anything important. And that, when we finally realize it, we will not feel दुःखि or even चिन्तित. We’ll feel ‘depressed’. So no, I’m not saying that it will be forgotten. Much worse. It will be neglected, much like one of those pencils which fall into the space between the bed and the wall and which we just leave there.

asfd

So far in this article, I have only talked about Nepali. But Nepal has a lot more languages than just Nepali. Lot of them are in a lot worse state than Nepali. For example the Nepal Bhasa (Newa) which was the lingua franca of Kathmandu Valley 80 years ago is now UNESCO listed engangered language. It is written in the Ranjana script and the Prachalit script. I want to talk about what mechanisms currently exist to support those languages too. asdf ??

It will be a long article, with many many things. So bear with me. asfd

# Part two

# ASCII and similar encoding schemes

_Note: The numbers starting with ‘0x’ and 'U+' are Hexadecimal numbers. 'U+' additionally implies that the number following it is a Unicode code point._

Computers only understand numbers. To a computer, a picture is not, say, people or food, but a 2D matrix of numbers representing the color values at each point. An audio recording is, similarly, a sequence of amplitude of sound wave recorded several thousand times each second. It goes without saying that text is also read by the computer as a sequence of numbers.

ASCII is simply a mapping of these numbers to characters. So if you put the number 65 in the memory of a computer and ask it to show what that means in ASCII, it will display the capital letter A. An important thing to note about ASCII is that it uses numbers from 0 to 127 only. Since computers almost universally store data in blocks of 8 bits (a byte) which can represent 256 numbers (2<sup>8</sup>), half of the representational possibilities go unused when using ASCII. There have been several extensions to ASCII which make use of the unused space from 128 to 255.

So how do you type Nepali in ASCII? Well, you don't. ASCII is, by it's very definition, American. In the early 90's, Bureau of Indian Standards came up with it's very own encoding called ISCII. ISCII is essentially an extension of ASCII. From 128 to 255, it stores Devanagari consonants. An interesting thing to note is that ISCII actually unified a bunch of scripts like Devanagari, Tamil, Bengali, Oriya, Tamil etc. So a number 164 (0xA4) can mean all of the following: अ, அ, অ, ଅ and more. The idea with ISCII is that, since all these scripts are descendants of the same Brahmi script, they behave similarly and represent similar sounds. Which is true because all four of the above letters represent the same /ʌ/ sound. ISCII encodes all these characters with the same number but leaves it up to the font to render in required script. Unicode does the same for the Newari language. But more on that later.

It is important to keep ISCII in mind, because Unicode specification for Devanagari is based almost exclusively on ISCII.

In Nepal, however, government didn't initiate any efforts. What happened instead was that independent font makers arbitrarily assigned the 256 numbers to various characters and ligatures. Which character a specific number represented was completely up to the font you chose. That must have been messy. Fonts are meant to change how the text looks, not what it is! 

The table below shows the character mapping of two Nepali fonts in the late 90's. So if you typed something in _Sabdatara_ but then decided to change to _Annapurna_ halfway through, I don't even know what you'd have to do. I'm just thankful that I was not a computer operator in the 90's.

![](https://nirav.com.np/assets/img/2019-06-16-180457_1366x768_scrot.png)

But thankfully, over time these mappings stabilized to the what is now known as the Traditional or Remington's keyboard layout. It seems that this layout was based on the Mangal font, 

**Unicode**

The Unicode is a text-encoding specification. It was designed from the ground up to support **all** scripts of the world. Unicode currently encodes 1,37,994 characters from 150 scripts throughout.

In Unicode, each character gets it's own number. For example, the number 2325 (0x0915) uniquely identifies the Devanagari letter क, the number 70658 (0x11402) identifies the Newari letter 𑐂, the number 65 (0x41) the English capital letter A and the number 24859 (0x611b) the unified Chinese, Japanese and Korean letter 愛, meaning love.

Characters are given a block to live in. A block is essentially a range of numbers. For example, Devanagari characters live in the U+0900 to 097F block. Newa is in the U+1900 to U+194F block.

![](https://nirav.com.np/assets/img/2019-06-16-175754_1366x768_scrot.png)

The advantage of separating language into blocks, is that each block can get it's own kind of treatment from the software. We know that all scripts behave differently. In Devanagari, some characters go above the previous character, some under. Some change the character itself. In Tibetan, diacritics stack up vertically. A single Urdu character, when it appears, can change how the entire word looks. Not to mention that scripts have different directions of reading. Chinese and Japanese are written from top to bottom, right to left. Urdu is written from right to left, top to bottom. All these quirks can be handled by software based on what block the characters come from.

Now, if you look at the table above, you will notice a lot of characters missing. Where is, for example, क्ष? Or द्व? Or all the half forms like क्‍, ग्‍?

![](https://nirav.com.np/assets/img/2019-06-16-174910_1366x768_scrot.png)

and this image

![](https://nirav.com.np/assets/img/2019-06-17-090949_1366x768_scrot.png)

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

Abbreviations  
ASCII - American Standard for Information Exchange  
ISCII - Indian Standard for Information Exchange