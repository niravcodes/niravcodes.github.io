---
excerpt_separator: "<!--more-->"
layout: post
title: Ambling Down The Javascript Rabbit Hole
tags:
- javascript
- coding
feature-img: https://nirav.com.np/assets/img/vue.png
thumbnail: ''
date: 2019-01-20 06:42:55 +0000

---
I'm finally getting somewhere. After a week of learning JS fundamentals, I decided to make a test app using modern web frameworks and technologies. More specifically, I picked the MEVN stack (MongoDB, ExpressJS, VueJS and NodeJS). Note that this stack is entirely based on javascript which is one of its touted benefits.

As a newcomer to the whole JS landscape, I must note that I find this whole ecosystem incredibly rich and intricate, lest I forget as I gain experience. First there is NodeJS which essentially provides runtime environment for javascript code outside of browsers. Over Node, vast assortment of programs have been written, which is managed and distributed over Node Package Manager (npm). These programs, among other things, easily integrate with your javascript code on Nodejs and allow you programmatic control over them. Using packages like webpack and babel you can create complex tooling and build systems that automatically compiles your SCSS down to CSS, transpiles your ES5 javascript code, minifies your codebase and gzips it and so on. 

Over NodeJS, there is ExpressJS which allows you to set up a server on NodeJS and efficiently respond to HTTP requests. It was sort of eye opening to realize that the relation between URL paths (example.com/path/to/something) and actual filesystem is completely arbitrary. That is to say, I can easily parse the URL using Express and return whatever I will for whichever URL with no relation to the file hierarchy. I suppose it is because I come from the world of PHP and Apache that I found it surprising.

MongoDB sits alongside ExpressJS and talks to the MongoDB server to read from and write to our DB. I had been using plain old MongoDB driver to test things out but my friend Bhuban introduced me to Mongoose. Mongoose brilliantly solves so many issues I hadn't even predicted or noticed and provides a pleasant interface to MongoDB.

Finally there's Vue. There are a few alternatives to Vue, most notably Angular and React. I picked Vue because I had been told that I Vue has a lot less friction than other frameworks. I can't attest to that because all I've ever used is Vue, but I must say that it's very pleasant to work with VueJS. It took me about 10 days to learn javascript, Vue, it's tooling and CLI, and make a small chat application with it's Single Page Application spec.