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
I wrote a toy compiler few months back. The compiler is interesting because it allows you to write code in Nepali and compile it. I wanted people to see it, so I put the code up on Github. But as it turns out, not a lot of people are willing or capable of going through the convoluted process of cloning your repository, compiling the program, installing a Nepali language keyboard and learning an obscure half-baked programming language just because some idiot put it on Github. (_note to self: link the repo here_)

So, I decided to write a web app to easily demonstrate the program. In this post I discuss my decisions regarding the choice of sandboxing

nsjail doesn't install because of protobuf problems perhaps some kind of protobuf versioning inconsistency. It doesn't help that the git page doesn't have any installation steps/dependency+version info. Might look deeper into this in the future,

mbox doesn't work in 2019. -n still allows networks. Guessing that it relies on kernel specific features. Development halted 4 years ago. Also, reading the author's paper and ycombinator comments, you get the feeling that he's much more proud of his filesystem layering work than his sandboxing work. Also, it seems more like some academic/proof-of-concept work someone coded to escape real life (much like I coded Huffman Compression). Doesn't fit my requirements.

Docker Heavy and not built for my use case. Not for security. Can be broken out of. At any rate, I'm not gonna be instantiating full containers for executing a sub-megabyte program.

minijail I found about 2 days after i began my search.

custom:

namespaces, chroot, seccomp-bpf, kafel, cgroups, users etc

PS: Mosh is really cool substutite to ssh.