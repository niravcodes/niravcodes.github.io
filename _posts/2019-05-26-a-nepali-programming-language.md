---
excerpt_separator: "<!--more-->"
layout: post
title: A Nepali Programming Language?
tags:
- project
- compiler
- devanagari
feature-img: https://nirav.com.np/assets/img/sanskrit.jpg
thumbnail: ''

---
Last semester, we made something entirely cloud based called JobCat. We wanted to make something for the average Joe who wants to have a professional to do something for him. Unfortunately, because I procrastinated most of the time, and because the "designer" didn't design anything except our unrelenting hopes, we ended up putting everything together in three sleep-deprived days and coffee-drenched nights. I am kind of proud of a few interesting details here and there and a few ingenious hacks but, all in all that thing is a big and ugly Gordian knot that no one can untangle. I think it's still in my [GitHub](https://github.com/niravcodes "Niravcodes Github"), if you want to try.

Anyway, this semester we are supposed to make a minor project and I have chosen something very interesting: a programming language in the Nepali language. It will be written in the Devanagari script (which García Márquez has described as resembling "clothes hung out to dry on a line") and will follow the conventional Nepali Subject-Object-Verb structure. <!--more--> For those of you who are curious, the Nepali language in Devanagari script looks like this:

कौसीमा उभिएर लज्जानत  
तिमीले मतिर गुलाफी हतारमा उडाएको  
दुइ सेता कलिला हत्केलाको परेवा :  
तिम्रो नम्सते ।  
\- [भूपी शेरचन](https://en.wikipedia.org/wiki/Bhupi_Sherchan "Bhupi Serchan")

Of course, designing a new programming language and building  compiler for it is a huge undertaking, and not something you would rationally choose to do when the deadline is 2 months away. But we have decided to do it anyway. We are not going to write the compiler to compile the entire language. For now, it will only compile a subset of the language.

And we still have a few other problems to tackle, the most pressing one being the text processing for UTF-8 encoded Devanagari text. There is a C++ library called International Components for Unicode that we want to use but the documentation is not as straightforward as I had hoped. Then there is the problem of input method. In Linux, I am using a custom made input method for typing in Nepali. I'm not sure what chops I'll have to bust to get it working in windows.

I'll keep you updated on the interesting things I run into.

_The feature image of a Devanagari scripture was photographed by_ [_Ms Sarah Welch_](//commons.wikimedia.org/wiki/User:Ms_Sarah_Welch "Ms Sarah Welch") _and is licensed_ [_CC BY-SA 4.0_](https://creativecommons.org/licenses/by-sa/4.0/)