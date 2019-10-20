---
excerpt_separator: "<!--more-->"
layout: post
title: Sandboxing Unsafe Executables on Linux for an Online Compiler with Minijail
tags:
- linux
- cloud
- sandbox
feature-img: https://nirav.com.np/assets/img/blurred-blurry-fence-967933.jpg
thumbnail: ''

---
I wrote a toy compiler few months back. I wanted people to see it, so I put the code up on Github. But as it turns out, not everyone is willing or capable of going through the convoluted process of cloning the repository, compiling the program, installing a Nepali language keyboard and learning an obscure half-baked programming language just because some idiot put it on Github.

So, I started to write a web app to make the program easily accessible.<!--more--> The web app lets user write code in their browser, then compiles and executes the program on the server, and allows the user to send input from the browser to the server as it executes.

My first instinct was to use something like AWS Lambda to compile and run each process as a cloud function, but then I looked into the deep abyss of my wallet and found myself lost in the darkness.

Another idea was to forego the cloud altogether. Compiling code into assembly can be done in any under-powered Virtual Private Server. I can write an implementation of a simple virtual machine in JavaScript, then I can add a new backend to my compiler to generate code for the virtual machine. Then I can embed the JS virtual machine in the webpage, and when the user hits compile, all server has to do is compile the language into machine code for the virtual machine and send that back to the client. Execution becomes client-side headache. Something like (a slightly saner version of) Brainfuck could be perfect for this kind of application. It's relatively simple to make a [Brainfuck Virtual machine](https://https://thorstenball.com/blog/2017/01/04/a-virtual-brainfuck-machine-in-go/).

Anyway, I decided that AWS Lambda is too wasteful for my needs. Virtual Machine on Webpage idea is going to significantly increase code maintenance related tasks in the future. I tried to find some other way of executing user's programs on the server.

### Issues with executing unsafe binaries on server

But huge security issues emerge by allowing user-generated executables to run on your server. Just to name a few:

1. The executable can start an **expensive infinite loop** (for example: listing all prime numbers above 10^5), which makes the system unbearably slow for other processes.
2. It can generate and **store a huge amount of data** which either completely fills up the RAM, the storage system, or both, causing the system to slow down or crash, and making it physically impossible for other users to store and run their executables.
3. It can **overwrite important files** in the server (for example, the very node.js program responsible for compiling and executing user programs) and infect all clients with malicious payloads.
4. It can utilise the program bugs or kernel bugs to **elevate it's status to root** to install stealthy rootkits or bitcoin mining software to use our servers for their benefit.

This is just the tip of the iceberg. So many other malicious attacks are possible depending on the system and infrastructure arrangement. The system designer has to be very careful in setting up the system where untrusted and potentially unsafe executables are run, without causing significant lags for genuine users.

### Solutions and preventive measures

This was the first time I had to design a system like this, so I had to research quite a bit. In this post, I highlight some results of my research. First, lets see how the above issues can be dealt with in a general way.

1. To prevent expensive infinite loops, we can limit the maximum CPU percentage allowed to each user process and kill it after a fixed time.
2. To prevent memory overuse, simply limit the maximum memory allowed per process.
3. Either completely block file writes, or have a sandboxing file layer which redirects all file accesses of the process to a safe temporary directory. Or run the process on a virtual file system in a separate mount namespace.
4. Use redundant security measures and tightly constrain the execution environment using whitelists to minimize the kernel attack surface.
5. Execute the user process in a _sandbox_, which essentially manages most of the above concerns and provides more isolation.

These are, of course, just the general guidelines. In my case, because _i._ the users actually can't directly craft the machine code that runs in the server and _ii._ I have full control over and knowledge of the assembly code that is being generated, things are a little easier security-wise. But this will eventually change as I add more features and as more contributors join. So taking some time to tighten the security is more future-proof.

### Features the Linux Kernel provides

I'll start with the features already provided by a relatively recent Linux kernel by default.

1. **Users and Groups:** It's obvious, but by simply ensuring that there's no case in which the unsafe binary will be run as root and that no program started with sudo executes the unsafe binary, we cut off a big chunk of attacks. But let's take it a step further. Make a new user account with limited privileges and run the unsafe binary as that user. Set up permissions accordingly so that the new user account cannot read what need not be read. Add the user only to groups which it absolutely requires.
2. **Namespaces:** Namespace is a feature of Linux kernel that allows you to isolate a process from other processes in certain respects. For example, if you run the untrusted executable in a separate process namespace, the process is not able to see or interact with any other process running in the system. It literally becomes the `init` process in it's view. Namespaces allow containers like dockers to fake isolated systems without the overhead of the full Virtual Machine.
3. **Control groups:** Control groups (also called cgroups) allow you to allocate resources and set limits on CPU time and memory, among other things. This, when used in conjunction with namespaces allows for effective containerization of apps.
4. **Capabilities:** Capabilities in Linux allows selective provisioning of root privileges. If you really have to allow the untrusted program to do things that only root is able to, then capabilities allows you to allocate only the required root-only operations to the running process
5. **Seccomp-bpf:** Seccomp-bpf stands for Secure Computing mode-Berkeley Packet Filter (although no one calls it this). Seccomp by itself blocks any syscalls four (exit(), sigreturn(), read() and write() on already open file descriptors) so unsafe compute-bound processes can be run without many risks as almost 99% of the syscalls are blocked by the kernel. BPF is an addon to seccomp which allows you to block any syscalls you want. _strace_ is a linux tool that allows you to trace syscalls made by a process.

Because these features are provided natively by the Linux kernel, we can apply them using corresponding syscalls and parameters and make with a relatively robust sandbox. I toyed with the idea of making my own restricted micro-sandboxing program (and I really wanted to) but decided not to because I was already juggling more things than I'd like to.

There are programs which use these kernel features and more to sandbox applications for us. I had expected there to be many, specially in this age of cloud computing and lambda functions.

**nsjail:** I couldn't get it to compile because of some strange protobuf dependency error. It doesn't help that the GitHub readme doesn't have any build steps or the versions of dependencies required. Which is a shame because this was almost exactly what I was looking for: a lightweight application sandbox. I might look into it some more later. [This](https://nsjail.com "https://nsjail.com") is the official site for nsjail.

**mbox:** It doesn't seem to work in 2019. The example usages in GitHub fail to do any kind of blocking. The `-n` still doesn't block internet access. I'm guessing that it relies on some old kernel specific features. It was last updated 3 or 4 years ago on github. Also, reading the author's paper and ycombinator comments, I got the feeling that he's much more proud of his filesystem layering work than his sandboxing work. Also, Mbox seems more like some academic/proof-of-concept work. Doesn't fit my requirements. [This](https://pdos.csail.mit.edu/archive/mbox/ "Mbox website") is the official site for Mbox.

**Docker:** Heavy and not built for my use case. It is also not as security-focused, and apparently it can be broken out of. At any rate, I'm not gonna be instantiating full containers for executing a sub-megabyte programs. Although Docker running small distros like Puppy linux is an interesting idea. [This](https://docker.com "Docker") is the official site for Docker.

**systemd-nspawn** is really interesting. It needs a full chown-able filesystem I didn't use it this time, but I'm definitely going to use this in some future project.

**minijail:** This little software is apparently used by Google to sandbox chromium programs. It is not as feature rich as nsjail so I ended up using this in conjunction with cgroups and some other programs to isolate the unsafe binary.

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/oGmj6CUEup0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

[https://en.wikipedia.org/wiki/OS-level_virtualisation#Implementations](https://en.wikipedia.org/wiki/OS-level_virtualisation#Implementations "https://en.wikipedia.org/wiki/OS-level_virtualisation#Implementations")

PS [Mosh](https://mosh.org/ "Mosh website") is really cool substitute to SSH, specially when you're using vim to code directly on the server. Plus, the fact that I don't have to restart SSH connection every time I wake my laptop is such a convenience.

**Resources**

1. [https://en.wikipedia.org/wiki/OS-level_virtualisation#Implementations](https://en.wikipedia.org/wiki/OS-level_virtualisation#Implementations "https://en.wikipedia.org/wiki/OS-level_virtualisation#Implementations")  
   This page has a list of many sandboxing tools that don't use full VMs.
2. [https://chromium.googlesource.com/chromiumos/docs/+/master/sandboxing.md](https://chromium.googlesource.com/chromiumos/docs/+/master/sandboxing.md "https://chromium.googlesource.com/chromiumos/docs/+/master/sandboxing.md")  
   Explains how minijail can be used for security. If you're using Minijail, also check out the embedded video.
3. [https://people.csail.mit.edu/nickolai/papers/kim-mbox.pdf](https://people.csail.mit.edu/nickolai/papers/kim-mbox.pdf "https://people.csail.mit.edu/nickolai/papers/kim-mbox.pdf")  
   The author's paper explaining Mbox.
4. [https://blogs.rdoproject.org/2015/08/hands-on-linux-sandbox-with-namespaces-and-cgroups/](https://blogs.rdoproject.org/2015/08/hands-on-linux-sandbox-with-namespaces-and-cgroups/ "https://blogs.rdoproject.org/2015/08/hands-on-linux-sandbox-with-namespaces-and-cgroups/")  
   [https://www.toptal.com/linux/separation-anxiety-isolating-your-system-with-linux-namespaces](https://www.toptal.com/linux/separation-anxiety-isolating-your-system-with-linux-namespaces "https://www.toptal.com/linux/separation-anxiety-isolating-your-system-with-linux-namespaces")  
   Use these two links if you're going baremetal. Also try finding pages in chromium.googlesource.com about sandboxing. They have done a lot of work in that area. A representative page is below: [https://chromium.googlesource.com/chromium/src/+/master/docs/design/sandbox.md](https://chromium.googlesource.com/chromium/src/+/master/docs/design/sandbox.md "https://chromium.googlesource.com/chromium/src/+/master/docs/design/sandbox.md")
5. [http://static.googleusercontent.com/media/research.google.com/en//pubs/archive/34913.pdf](http://static.googleusercontent.com/media/research.google.com/en//pubs/archive/34913.pdf "http://static.googleusercontent.com/media/research.google.com/en//pubs/archive/34913.pdf")  
   This is the paper explaining Native Client, a sandboxing system developed by Chrome developers to allow execution of C/C++ programs in the web browser with near-native speed.