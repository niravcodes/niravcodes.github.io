---
layout: post
title: Humbird
tags:
- javascript
- project
- cloud
- aws
img: https://nirav.com.np/assets/img/sshot-1.png
feature-img: https://nirav.com.np/assets/img/pexels-photo-37728.jpeg
date: 2019-01-20 07:46:50 +0000

---
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

The design of this webapp is not something I am proud of. It looks okay I guess, but there are so many subtle nuances and expressions that I could have put in but I didn't. This is of course in line with my objectives but I still feel bad. I console myself thinking that I'm saving my best UI/UX work for the software engineering project, merely using this as a stepping stone.

I decided to completely use HTTPS for this project. I used letsencrypt to generate the certificates and verify the domain. Letsencrypt is surprisingly easy to set up for single domains. I even set up a cron job to auto-renew my expiring certificates. But wildcard subdomains presented a hassle. My DNS provider's API was not supported for automatic renewal so I had to get down and dirty. I suppose if I really wanted to, I could write it but this project is not serious enough to warrant that.

I had a few questions about provision of dynamic subdomains. My first thought was to use the DNS provider's API to update DNS records every time a chat was registered. Digging a little deeper I found that directly modifying DNS records was not necessary as long as the subdomains redirected to inside the main site. I was quite resolved to go down that path with finally I realized that for my small project, it wasn't remotely necessary to handle anything serverside. I finally decided on complete client side logic for subdomain rerouting. I'm pleased with how great it performs.

![](https://nirav.com.np/assets/img/socde.png)

I did all the client side coding on an online platform called [codesandbox.io](https://codesandbox.io/ "codesandbox") because I was back home and didn't have my laptop with me. Code Sandbox was amazing and I enjoyed using it. The prettify-on-save still makes my heart leap with joy. 

I also learnt a great deal about clouds in general. I went from not knowing what exactly the cloud is to completely falling in love with it in a few days. I am hosting the backend (expressjs on node) on an Amazon EC2 instance and the database is hosted on Azure cosmosdb. I fiddled around with many services offered by aws and I think they are great.