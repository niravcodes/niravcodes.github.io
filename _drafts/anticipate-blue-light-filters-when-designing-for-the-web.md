---
excerpt_separator: "<!--more-->"
layout: post
title: Anticipate Blue Light Filters When Designing For The Web
tags:
- accessibility
- web design
enableNepali: false
feature-img: ''
thumbnail: ''

---
I just noticed that I can't tell a link apart from normal text on this blog when I have blue light filter enabled, specially when it's nestled in a large body of continuous text. There are a few reasons for this: I use a dark shade of blue as the accent color of this blog, and I have chosen to remove underlines from links because that tends to draw more attention to the links. 

<!--more-->

I started using a blue light filter called [Redshift](http://jonls.dk/redshift/ "Redshift Night Mode link") on my computer more than 5 years ago (which reminds me, I need to digitize my old journals quick!). Back then, blue light filters weren't quite as hyped as they are now. So I always assumed that I was one of the very few people who ever used them. These days, every layman-oriented operating system comes with blue light filtering feature baked in. Even phones come night mode by default.

So I think it's better to start designing with blue light filters in mind. I'll admit that this is a fairly specialized problem. The proportion of people that access your website at night time and happen to have a fairly strong blue light filter enabled is probably not very high. 

But I mostly write technical posts targeting programmers and similarly computer-facing people. And programmers are exactly the kind of people who stay up late _and_ have enough incentive and initiative to set up blue light filters. So, it seems that I'm the kind of person who needs to keep the possibility of blue light filters in mind.

And it is a fairly easy thing to do. I simply have to ask myself: "is the meaning of this element lost when the blue-light filter is cranked up?" In other words, is color the only indicator of the element's properties? If so, changes need to be made. 

If you're already designing your websites for accessibility then you've probably already solved this problem without even caring about it. But then again, there might be some night light specific design problem that you didn't realise. I try to design websites with accessibility when the time allows, but I just caught this blue light filter problem today.

In [niravko.com](niravko.com "My other website"), I fixed the problem by simply italicizing the links. It's a very small site, so this works. But in a blog as this, italics in text often has other meanings. I wouldn't want a link in my paragraph to convey emphasis or sarcasm to the blue light enabled monitor. 