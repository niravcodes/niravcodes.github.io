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
I've been working on and off on a Nepali programming language with my friends for the last few months. It's called मनसा (IAST: _mansā_) and I think it's ready for an alpha release. If you'd like to try the language out, visit [mnsa.cc](http://mnsa.cc/) - the official website. You can play around with the language right in the browser without having to download anything, not even a Devanagari keyboard layout.

This post is a collection of random things I want to say about the language, including how the idea came about, the interesting things I learnt making the project, and the problems faced.

<!--more-->

### How it all started

In the sixth semester, we are required to submit a team project by the end of the term. Most teams in my class were making boring things, like hotel management systems, or polling websites. If you get to chose your own project, why not do something exciting and new? We settled on making a programming language. "Why not in Nepali?", I said, and after a long debate, we settled on building a Nepali programming language. 

In the beginning, we thought a Nepali programming language wouldn't have any practical use at all. We thought that all this thing would ever be is a novelty, a fun thing to play with and forget about, something like Brainfuck or Befunge. But as we continued to look into things to include in our proposal, we realized that a Nepali programming language might have a few very niche but very practical uses.

After some more deliberation, we decided that it had to be a compiled language, because that was the most difficult to make in terms of code, and the "coolest". It was exciting and somewhat uncertain because we don't have Compiler Construction classes in our syllabus, so we had basically zero idea on how we'd proceed. Plus we didn't know how to work with Nepali characters in the program. It was a great learning experience.

### The language

The language is actually very tentative at this point and we're still refining it. You should be able to get the general idea of the syntax by the small example code below. If you don't, wait for the official documentation to be finished. It's in the works. 

![](https://nirav.com.np/assets/img/programmnsa.jpg)

We have made a few changes to the conventional structure of a program statement to make it more expressive. For example, in function calls, the name of the function comes after the parameters, as verb comes at the end of sentence in Nepali. So "print Something" becomes "something लेख". We similarly modified other constructs such as conditionals and loops to fit into the Nepali grammar structure more. Technically, it is a very small change but it really does help make the programs more readable in Nepali. It was surprising how fluid the language becomes by changes so simple.

### The compiler

The compiler was written in C++ completely from scratch. I didn't want to use lexer or parser generators because these tools hide the interesting and complicated details. That is a good thing if your goal is to make good, maintainable compilers but, as a student, I wanted to explore all the gory details and learn everything I could. I should mention here that the [series of lectures by Alex Aiken](https://www.youtube.com/playlist?list=PLDcmCgguL9rxPoVn2ykUFc8TOpLyDU5gx "Compiler Making Lectures Alex Aiken") is an amazing resource, and if you're planning on doing compilers too, you must at least skim through the videos to see the big picture.

I used Visual Studio Code to write C++ code this time. I actually started coding using plain old vim as always, but eventually it became so unmanageable with files all over that I had to find a more manageable tool. I went with vscode, and I'm glad I did because vscode is so well made. And the c/c++ extension is so good. It apparently makes an AST for my code on the fly and checks for all kinds of errors. I had never before used these sophisticated tools for writing C++. I generally used vanilla sublime with vim extention, or just command line vim. But really it's so nice. It's like discovering geysers for the first time when you've been showering with cold water all your life (strangely specific simile? sorry). 

When writing the compiler, I used many new C++17 features. I was drawn into modern C++ first because of constexpr which allows you to make functions that are evaluated at compile time. I wanted to build a fast but manageable lexical analyser using a composition of constexpr functions but I realised that I was trying to prematurely optimise, so I controlled myself. Maybe in version 0.2.

I also used C++17 lambda functions to declare nested functions to eliminate repeated actions that are only relevant inside a specific function. Here's an example:

     auto makeDeclNode = [&](ast::astType a) {
       stmt.reset(new ast::Ast);
       astNode declaration;
       if (declaration = declList()) {
          stmt->type = a;
          stmt->left = std::move(declaration);
       } else
          errQuit("declarations");
    };
    
    if (accept(lexer::tokenType::_int)) {
       makeDeclNode(ast::astType::_intDecl);
    } else if (accept(lexer::tokenType::_str)) {
       makeDeclNode(ast::astType::_strDecl);
    } else if (accept(lexer::tokenType::_bool)) {
       makeDeclNode(ast::astType::_boolDecl);
    }

Maybe it's because I've coding a lot in javascript these days, but nested functions feel like an important language feature to have. मनसा has nested function support too.

I also tried to use C++ smart pointers everywhere. They make memory management so pleasant and take away most of the issues I used to deal when using raw pointers. But I did find the lack of good observer pointer idiom annoying and dangerous. Maybe they'll make it better by C++20, but hopefully I'll already be using Rust by then.

In v0.1, I have only implemented the lexer, parser, semantic analyser and a rudimentary code generator with emits C++ code. In the new versions, I will progressively add new modules like optimiser, and redo some old ones.

1. The lexical analyser is a simple finite state machine which iterates over each each UTF8 encoded character and converts them into tokens. I learnt a lot about Unicode while making the lexer. I am interested in world languages and scripts, so reading the Unicode documentation and other articles was fascinating to me. I have written about Unicode 

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

Learnt a few new things not related to programming

1: Its' not enough to just know the best way to do things. You have to put in the time to do the thing and take the time to see it through. I have been very critical of many people's work in the past because I could point out the errors in their work. But this experience taught me that perfectionism is not always the best sometimes showing up and makign shit works too