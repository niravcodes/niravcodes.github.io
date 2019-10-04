---
excerpt_separator: "<!--more-->"
layout: post
title: 'Sandboxing small executables on Linux: Many tries'
tags:
- linux
- cloud
- sandbox
feature-img: ''
thumbnail: ''

---
nsjail doesn't install because of protobuf problems perhaps some kind of protobuf versioning inconsistency. It doesn't help that the git page doesn't have any installation steps/dependency+version info. Might look deeper into this in the future,

mbox doesn't work in 2019. -n still allows networks. Guessing that it relies on kernel specific features. Development halted 4 years ago. Also, reading the author's paper and ycombinator comments, you get the feeling that he's much more proud of his filesystem layering work than his sandboxing work. Also, it seems more like some academic/proof-of-concept work someone coded to escape real life (much like I coded Huffman Compression). Doesn't fit my requirements.

Docker Heavy and not built for my use case. Not for security. Can be broken out of. At any rate, I'm not gonna be instantiating full containers for executing a sub-megabyte program.

minijail I found about 2 days after i began my search. 