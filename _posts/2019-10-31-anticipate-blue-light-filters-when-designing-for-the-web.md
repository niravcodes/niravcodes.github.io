---
excerpt_separator: "<!--more-->"
layout: post
title: Anticipate Blue Light Filters When Designing For The Web
tags:
- accessibility
- web design
enableNepali: false
feature-img: https://nirav.com.np/assets/img/bluelightgirl.jpg
thumbnail: https://nirav.com.np/assets/img/bluelightgirl.jpg

---
I just noticed that I can't tell a link apart from normal text on this blog when I have blue light filter enabled, specially when it's nestled in a large body of continuous text. There are a few reasons for this: I use a dark shade of blue as the accent color of this blog, and I have chosen to remove underlines from links because of [typographical](https://practicaltypography.com/underlining.html) reasons (although, there is [evidence](https://adrianroselli.com/2014/03/i-dont-care-what-google-did-just-keep.html) to suggest contrarily).

I started using a blue light filter called [Redshift](http://jonls.dk/redshift/ "Redshift Night Mode link") on my computer more than 5 years ago (which reminds me, I need to digitize my old journals quick!). Back then, blue light filters weren't quite as hyped as they are now. So I always assumed that I was one of the very few people who ever used them. These days, every layman-oriented operating system comes with blue light filtering feature baked in. Even phones come night mode by default.

<!--more-->

So I think it's better to start designing with blue light filters in mind. I'll admit that this is a fairly specialized problem. The proportion of people that access your website at night time and happen to have a fairly strong blue light filter enabled is probably not very high.

But I mostly write technical posts targeting programmers and similarly computer-facing people. And programmers are exactly the kind of people who stay up late _and_ have enough incentive and initiative to set up blue light filters. So, it seems that I'm the kind of person who needs to keep the possibility of blue light filters in mind.

And it is a fairly easy thing to do. I simply have to ask myself: "is the meaning of this element lost when the blue-light filter is cranked up?" In other words, is color the only indicator of the element's properties? If so, changes need to be made.

If you're already designing your websites for accessibility then you've probably already solved this problem without even caring about it. But then again, there might be some night light specific design problem that you didn't realise.

I try to design websites with accessibility when the time allows for it, but I just caught this blue light filter problem today. Actually, I already had this problem years ago, but by default response has always been to turn off the filter temporarily. In fact, I can probably type `Ctrl+R pkill redshift ⏎` faster than I can type `aiypwzqp` or some other [GTA San Andreas cheat](https://www.ign.com/wikis/grand-theft-auto-san-andreas/Cheat_Codes_and_Secrets).

The default assumption has always been that it's my fault when the website or video doesn't work as intended because of night light. But, I think, with more and more people starting to have their blue light filters turned on, I think it's time that web designers start anticipating it and designing around it.

In [niravko.com](http://niravko.com "My other website"), I get around the problem by simply italicizing the links. It's a very small site, so this works. But in a blog such as this, italics in text often has other meanings. I wouldn't want a link in my paragraph to convey emphasis or sarcasm to the blue light enabled monitor. I need to work on this problem soon.