---
excerpt_separator: "<!--more-->"
layout: post
title: Visualize C++ Data Structures using Graphviz and the DOT language
tags:
- c++
- graphviz
enableNepali: false
feature-img: ''
thumbnail: ''

---
Data structures help structure and organize data effectively, and provide several abstracted operations on the data. They are elegant and convinient, and computer scientists love to use them. Implementing these data structures in the computer require the programmer to flatten the structure into a one-dimensional model using pointers or references because the memory is actually arranged as a one-dimensional sequencial run of data elements.

It is often necessary to inspect the data structure in debugging and program verification phases. But some data structures happen to be particularly graphical, in that they have multiple associations and elaborate hierarchies or layers. Think of a Rope or a Graph. Due to many associations between nodes, it's not possible to properly display the graph on the terminal.

<!--more-->

I recently ran into such problem, and found an interesting solution. In this post, I will try to document it.

I'm currently working on writing a compiler for my own Nepali programming language. The front-end part of a compiler converts the program code into a data structure called AST. AST, or Abstract Syntax Tree, is a tree-based representation of the source code. It's much more suitable to further transformations in the semantic analysis, optimization and code generation phases.

But AST is also an incredibly complex data structure. It has to store a bunch of information and maintain a tree structure. It is not immediately obvious how one might 


I wrote a compiler for my minor project in my 6<sup>th</sup> semester but the language it compiled to assembly was very basic. So back then, I got away with simply printing the tree in the terminal. For example, for this code:

![](https://nirav.com.np/assets/img/2019-12-09-003859_1366x768_scrot.png)

generates this AST:

![](https://nirav.com.np/assets/img/2019-12-09-004011_1366x768_scrot.png)

And this was quite enough for me at the time. Frankly, for a language that didn't even have an else if clause, there's are limited ways to complicate the AST other than by writing longer code. But the current language I'm working on is extensive. And so the tree it creates is immense. I had to come up with some other way to analyse the data structures.

Brian Kernighan has given an [amazing talk](https://www.youtube.com/watch?v=Sg4U4r_AgJU "Brian Kernighan's talk on successful computer language design") on successful language design, where he also described Pic, a language he designed for specifying graphs. It was interesting because I personally find having to make graphs using my touchpad to be an annoying experience.



So, I searched for something like Pic, and found Graphviz, which uses the DOT graph description language.

Funnily enough, I spent less time writing code to actually generate the graph than I spent trying to make it look cooler. But given how much time I'm going to have to stare at and navigate these graphs, I think the time was worth it.