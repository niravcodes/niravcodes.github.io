---
excerpt_separator: "<!--more-->"
layout: post
title: An easier Nepali keyboard layout
tags:
- unicode
- nepali
- keyboard
enableNepali: true
feature-img: ''
thumbnail: ''

---
As I wrote in my (excruciatingly long and boring) article on [the Nepali language and Unicode](https://nirav.com.np/2019/10/16/on-the-nepali-language-and-unicode-1.html "On the Nepali language and Unicode"), typing in Nepali doesn't have to be a pain. You are absolutely free to make your own keyboard layout to type in Nepali Unicode (which, by the way, has much better fonts than Preeti and Sagarmatha). In fact, a few months ago, I made my own keyboard layout because there's no way I'm going to be able to cram the random key mappings of the traditional Nepali typing layout. Sorry dad, your son has renounced ancestral typing for good.

<!--more-->

The layout I made is heavily based on the [LTK](http://ltk.org.np/ "Language Technology Kendra")'s phonetic keyboard layout (which is quite good on it's own). I made my layout to help me write code in the [मनसा programming language](http://mnsa.cc "manasa programming"). If you'd like to try out the language or the keyboard layout in your browser, head over to [mnsa.cc](http://mnsa.cc).

## Download the Keyboard layout

The keyboard layout is as systematic and fluid as I could make it. You should be able to get a grasp for the layout in about half an hour. Here are a few pointers to help you learn quicker.

* Nepali consonants are generally placed right in the key where their English consonant counterparts live. So क is in key 'k', प is in key 'p', च is in key 'c' and so on.
* Aspirate counterparts of consonants live in the uppercase letters. So ख which is the aspirate counterpart of क lives in capital 'K' key. Similarly छ which is aspirate counterpart to च lives in capital 'C' key.
* Half-forms (न्‍, च्‍, क्‍ etc) are automatically formed when you use the हलन्त character, which is in the key '/'. For more information on this mechanism, consult my article on [Unicode](https://nirav.com.np/2019/10/16/on-the-nepali-language-and-unicode-1.html "Unicode article at nirav.com.np").
* क्ष, त्र, ज्ञ, and श्र are compound consonants. Get them by typing in the constituent characters: क्‌ष, त्‌र, ज्‌ञ, and श्‌र respectively.
* There are some inconsistencies because some distinct Nepali phonemes are allophones for the English language. For example both ड and द are 'D' in English. To mitigate this issue, the letter ड had to be moved to an unused key 'x'. I'm sorry this had to be done but it has to be done.
* **Important:** आ is not the same as अा. There's a separate key for आ. Don't first type in अ then the ा key separately. Avoid this minor mistake to not seem like a middle-aged parent who has just learnt to use Facebook. 

![](https://nirav.com.np/assets/img/mnsalayout.png)

[Download for Windows here](/assets/img/keyboard.zip "Download this keyboard layout for Windows")

To install this keyboard on Windows, just download the layout, unzip, install using 'setup' file. You might have to reboot after installing. Then:

* Go to **Start** menu and click on **Settings**.
* Click on **Time & language** (_Speech, region, date_).
* Find and open **Region & language** settings.
* Under Languages, click on **+ Add a language**.
* Find and choose **नेपाली Nepali**.
* Click on **नेपाली** **(नेपाल) Nepali (Nepal)**.
* Pick the keyboard layout by clicking on the keyboard icon and selecting 'np-nirav'. 
* You're done. Have fun typing in Nepali.
* _PS: You might have to take some obvious extra steps. I don't remember much because it has been a long time since I used Windows._

If you'd like this layout for Linux, leave me a comment below or mail me. I'll put it up.