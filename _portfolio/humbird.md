---
layout: post
title: Humbird
tags:
- javascript
- project
- cloud
- aws
img: https://nirav.com.np/assets/img/sshot-1.png
feature-img: https://nirav.com.np/assets/img/vue2.jpg
date: 2019-01-20 07:46:50 +0000

---
Things to talk about:

1. what the project does
2. the design decisions
3. challanges : https, subdomain ...
4. what you'd like to add
5. wanderings in the cloud (nubivagant) and things learned

Humbird is a little chat application I made to gain more understanding of latest web technologies and cloud services. It took me a few days of sporadic effort to make and has given me a lot of insight into how things are made in the web these days. Humbird is not meant to be used seriously because I chose not to deal with the errors and exceptions that might occur.

When making Humbird, I had the following objectives in mind:

1. Leverage VueJS's Single Page Application spec and various tools associated with it
2. Learn to make an API with NodeJS, ExpressJS and MongoDB
3. Learn to use something like Fetch or Axios to communicate with the server
4. Learn to work with dynamic subdomains
5. Learn to deploy to the cloud
6. Learn all about HTTPS and use it in the site

The webapp essentially allows you to set up a chatroom for two people. It then provides you with a custom URL to access the chatroom. After you've registered your subdomain, you can send and receive text messages with the other user. 

![](https://nirav.com.np/assets/img/sshot.png)

On visiting <chatroom>.nirab.me, you are greeted with a login page. You type in your username to access the chatbox. Notice that there is no password protection for the chatroom. I think  that to secure anything reliably, you need to learn many different types of attacks, and proper defenses against them. That is a deep topic and I didn't think a few days of intermittent attention would have done it justice. I intend to read up on security the next time I have a huge block of free time.

![](https://nirav.com.np/assets/img/sshot-2.png)

The design of this webapp is not something I am proud of. 