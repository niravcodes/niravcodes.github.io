---
excerpt_separator: "<!--more-->"
layout: post
title: Sandboxing Untrusted Executables on Linux for an Online Compiler
tags:
- linux
- cloud
- sandbox
feature-img: ''
thumbnail: ''

---
I wrote a toy compiler few months back. The compiler is interesting because it allows you to write code in Nepali and compile it. I wanted people to see it, so I put the code up on Github. But as it turns out, not a lot of people are willing or capable of going through the convoluted process of cloning your repository, compiling the program, installing a Nepali language keyboard and learning an obscure half-baked programming language just because some idiot put it on Github. (_note to self: link the repo here once it's ready for release_) 

So, I decided to write a web app to easily demonstrate the program.<!--more--> The web app takes the code written in my language in the client side and compiles and executes the program on the server. But huge security issues emerge by allowing user-generated executable to run on your server. Just to name a few:

1. The executable can run an **expensive infinite loop** (for example: listing all prime numbers above 10^5), which makes the system unbearably slow for other processes.
2. It can generate and **store a huge amount of data** which either completely fills up the RAM, the storage system, or both, causing the system to slow down or crash, and making it physically impossible for other users to store and run their executables.
3. It can **overwrite important files** in the server (for example, the very node.js program responsible for compiling and executing user programs) and infect all clients with malicious payloads. 
4. It can utilise the program bugs or kernel bugs to **elevate it's status to root** to install stealthy rootkits or bitcoin mining software to use our servers for their benefit.

Many other malicious things are possible. The system designer has to be very careful in setting up the system where untrusted and potentially unsafe executables are run, without causing significant lags for genuine users.

This was the first time I had to design a system like this, so I had to look into lots of stuff. I learnt a fair bit about Linux security along the way. In this post, I highlight some results of my research. 

nsjail doesn't install because of protobuf problems perhaps some kind of protobuf versioning inconsistency. It doesn't help that the git page doesn't have any installation steps/dependency+version info. Might look deeper into this in the future,

mbox doesn't work in 2019. -n still allows networks. Guessing that it relies on kernel specific features. Development halted 4 years ago. Also, reading the author's paper and ycombinator comments, you get the feeling that he's much more proud of his filesystem layering work than his sandboxing work. Also, it seems more like some academic/proof-of-concept work someone coded to escape real life (much like I coded Huffman Compression). Doesn't fit my requirements.

Docker Heavy and not built for my use case. Not for security. Can be broken out of. At any rate, I'm not gonna be instantiating full containers for executing a sub-megabyte program.

minijail I found about 2 days after i began my search.

custom:

namespaces, chroot, seccomp-bpf, kafel, cgroups, users etc

PS: Mosh is really cool substutite to ssh.

For problems that include running untrusted executables on sensitive servers, a software tool called _sandbox_ is often used. Unsafe binaries are executed inside the sandbox