---
excerpt_separator: "<!--more-->"
layout: post
title: Hello Mr Huffman. You're cool.
tags:
- huffman_code
- c++
- coding
- project
feature-img: ''
thumbnail: ''
date: 2019-02-14 13:05:22 +0000

---
Da Vinci is quoted saying, "Art is never finished, only abandoned". I don't see why it should be any different for code. With that said, I'd like to declare my latest project: an implementation of Huffman's algorithm, finis— abandoned. I meant to say abandoned. Missed my chance.

So anyway, I've been working on it for about a week. I started a day before my Data Communication assessment inspired by a chapter on the Information Theory. There I was, at 11 in the night, having read for the first time in my life about Huffman's algorithm and **I was thrilled!** I decided then, in the spur of the moment, to pull an all-nighter and write code for the Huffman algorithm. Then I boiled some water, made myself a cup of strong coffee. And then I fell asleep.

After the anticlimactic beginning, though, I did start to code in earnest. And by the end of the week, I got it working. I've got to say that the it took a lot longer that I had estimated. I think that's in part due to my decision not to use the C++ standard template library. But all the same, it took way longer than I thought it would.

For those of you who don't know, Huffman's algorithm takes a very simple idea and finds an elegant way to implement it. At it's heart is the observation that the more a symbol repeats itself, the shorter it's name should be. This idea manifests itself in daily life too. For example, we have nicknames for people we call often, we have abbreviations for long words we often have to use, and when texting we use 'lol', 'tbh', 'imho' and other short forms that have become words of their own.

Translated to the world of computers, it means that if a byte (or a chunk of data) repeats itself often, it is best to encode it with the shortest number of bits. 