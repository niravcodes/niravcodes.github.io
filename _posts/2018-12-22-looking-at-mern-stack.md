---
title: Looking at MEAN stack
date: 2018-12-22 17:14:25 Z
tags:
- coding
- random
layout: post
feature-img: assets/img/thumbnails/desk-messy.jpeg
thumbnail: ''
---

Long ago, when I was a little kid, I found about the WAMP stack. It absolutely thrilled me to think that I could own a piece of web and make it do whatever I wanted. I was also a fan of 000webhost back then (then it got hacked). So in a frenzy of rapid coding and loads of cussing (I was a beginner in both) I built several web apps. Things like half baked social networking sites, blogging websites and suchlike. One such invention I remember with particular fondness is a small chat application. I built it in a day to talk to a girl I really liked. The idea was that we both loved to chat but hated Facebook.

For a SE class project, I was required to look into a back-end that can serve both a thin web client and a mobile client. As it turns out, these days the web is full of people talking about and using the MEAN and MERN stacks. They stand for {MongoDB, ExpressJS, Angular, NodeJS} and {MongoDB, ExpressJS, React, NodeJS} respectively.

The stacks are essentially based on NodeJS. NodeJS is a javascript runtime engine. Over NodeJS, we can implement a server and run it on the internet to serve pages and data to clients.

ExpressJS is a framework on top of NodeJS that makes it easier to manage requests from clients and respond to them easily. Obviously, since NodeJS is just a runtime engine, it is going to be fairly annoying to directly code a server over it.

MongoDB is a database system based on the NoSQL data storage mechanism. Where MySQL uses tables to store data, MongoDB opts for a JSON like key-value pair data storage mechanism. I need to look into this, because I think this is not exactly a replacement for MySQL for all applications.

Angular and React are two frameworks used to develop front-end for web and mobile apps.

With these four components, a full web software system can be realized. I think this is the best for the project I have picked.

But that is not why I am writing this blog post.  Just like WAMP stack made me realize that the interweb is full of possibilities, looking at these new stacks has filled me up with hope again. I am filled with new ideas of things I can make with these stacks.

I'm not thinking just web or mobile. I can absolutely connect this system up with ESP8266 modules and have it talk over the internet in JSON. Unlike WAMP, where I was essentially limited to sending webpages to client, I can just send the data in JSON to my clients. With this flexibility, I can continuously stream sensor data to the backend and get back just the results. With MEAN (minus the Angular), I have a very simple mechanism to send and receive data over internet. Processing it doesn't have to be done in NodeJS. 

All this is a really interesting to me, and I can't wait to do all kinds of things with it (of course, I am going to have to learn it first).