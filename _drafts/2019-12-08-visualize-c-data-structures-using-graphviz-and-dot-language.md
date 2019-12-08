---
excerpt_separator: "<!--more-->"
layout: post
title: Visualize C++ Data Structures using Graphviz and DOT language
tags:
- c++
- graphviz
enableNepali: false
feature-img: ''
thumbnail: ''

---
Generally, if you're working with a program that works with data, you'll use some data structure or another to conveniently work with it. Linked Lists, Trees, Graphs, Ropes, et cetera are all amazing tools which make working with data lot more fun.

I'm currently working on writing a compiler for my own programming language. And that entails, among many many other things, working on the AST, the Abstract Syntax Tree. The AST is basically a tree representation of a program. To make sure that my compiler is understanding the language that it's meant to compile, I often have to feed it some test program and inspect the generated AST.

<!--more-->

I wrote a compiler for my minor project in my 6<sup>th</sup> semester but the language it compiled to assembly was very basic. So back then, I got away with simply printing the tree in the terminal. For example, for this code:

![](https://nirav.com.np/assets/img/2019-12-09-003859_1366x768_scrot.png)

generates this AST:

![](https://nirav.com.np/assets/img/2019-12-09-004011_1366x768_scrot.png)

Yes, and this was quite enough for me at the time. Frankly, for a language that didn't even have an else if clause, there's are limited ways to complicate the AST other than by writing longer code. But the current language I'm working on is quite extensive. So, I couldn't rely on this method. The tree it creates is immense and it isn't a strictly binary tree this time. So I had to come up with some other way to analyse the data structures.

Brian Kernighan has given a very [interesting talk](https://www.youtube.com/watch?v=Sg4U4r_AgJU "Brian Kernighan's talk on successful computer language design") on successful language design, where he also described Pic, a programming language he designed for specifying graphs. When I watched the talk a few months ago, I thought Pic was very cool, because using a laptop touchpad or even a mouse to make graphs is extremely annoying. It is often the most annoying part of writing reports. 

So I thought maybe it

Funnily enough, I spent less time writing code to actually generate the graph than I spent trying to make it look cooler. But given how much time I'm going to have to stare at and navigate these graphs, I think the time was worth it.

notes:

1. get gif of the debugging workflow cuz it's so cool
2. get a gif of scrolling through the tree output
3. explain that it's a nepali programming language