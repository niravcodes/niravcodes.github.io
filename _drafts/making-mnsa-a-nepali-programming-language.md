---
excerpt_separator: "<!--more-->"
layout: post
title: 'Making मनसा: a Nepali Programming Language v0.1'
tags:
- programming
- c++
- nepali
- mnsa
enableNepali: true
feature-img: ''
thumbnail: https://nirav.com.np/assets/img/mnsabanner-1.png

---
**Draft**

I'm currently working on this post and if it's visible to you, it means I've published this temporarily to see how it looks. Sorry.

<!--more-->

![](https://nirav.com.np/assets/img/mnsabanner.png)

I've been working on and off on a programming language in Nepali language for quite some time. It isn't finished yet,

1. VSCODE with c++ extentino is incredible. They seem to be making proper ASTs for my syntax on the fly. So far, I've only ever used vim and sublime without much configuration (for c and c++, that is). It makes things so much easier.
2. c++17 is great. I'm ysing things in ways they perhaps weren't meant to be used for better code management. One of them is I'm using lambdas for organisation of function code. it is fun.
3. pratt and recursive descent
4. I'm also working on a website **LINK SCREENSHOT**
5. Unique Pointer is a lifesaver. supereffective once you get the hang of it. in previous c-like c++ code, I'd used raw poitners like in C. SO fucked.  
   but with _unique POinters_ it's easy to forget if you've already moved things, and end up with null pointers. Specially matters in complex mutually recursive functions that pass around pointers to subtrees as if they were joints.

# Short description of language

# Lexer

Unicode shenanigans, ingenuities, and stupidities + code redundancy and not invented here syndrome. mid coding change of conventions

# Parser

The boon that is unique pointers. Problems with recursivedescent. talk about pratt parsing .

recursive descent with backtracking.

Have photos of parse trees both terminal generated and made proper

USE **PRESENTATION's MATERIAL**

# Makefile

was using -o3 without knowing it.

# Interesting observatoins

1. One interesting thing I noticed isL
   1. VSCODE with c++ extention enabled takes insane amount 1.3 of memory,. So does chrome USes smem to find out
   2. at some point, you **_need_** _a second, prefreably vertical monitor._

# Reaching 2500 lines and what that means

1. at some point, you need to rethink your build system. Blog idea: Moving to Cmake? or is it too boring??
2. Compilation takes way too long. That's wasted time.
3. Cross system compilation is important
4. _*Most of the code is pointless_*

## Making Vector Website

I proposed that an event of this scale would benefit from having a centralized information bank on the web. specially because it's so targeted towards young people, who are used to using the web for everything anyway. Also, we are so reliant on Google forms that dilutes the brand and so on.

But as it turns out, it's hard to do everything by yourself. I was doing the content-writing, the designing and the web front and back ends and the server maintenance at

I was astounded at the amount of hacking attempts that were being made at the site.

1 the PHP site kind

1. The SSH kind. Woah

Website maintainence is a many-people job. Trying to do all things at once

### gtksourceview bug

gtksourcview has some errors that make it impossible to setup a syntax highlighting system. It fails to highlight _insert pic here_

Plus I had to make a desktop application to write generated code into AVR. so I couldn't just use a web app. I turned to electron.js. I had never used it before, and had hoped I'd never have to use it because I'm inherently repulsed by large systems. Plus, I use a 5 year old laptop with 4 gig ram, so I'm naturally inclined towards slimmer packages.

But time is a factor.

Surprisingly, it took me literally ---

Luckily codemirror is awesome. Marijn Haverbeke is literally my fabourite person rn.

The strange thing about time is that there's too much of it in the future but too little in the present I can't wrap my head arund the concept of time there seems to be ..