---
excerpt_separator: "<!--more-->"
layout: post
title: 'Making Mnsa: a Nepali Programming Language'
tags:
- programming
- c++
- nepali
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

The boon that is unique pointers. Problems with recursivedescent. talk about pratt parsing.

Have photos of parse trees both terminal generated and made proper

USE **PRESENTATION's MATERIAL**

# Makefile

was using -o3 without knowing it. 