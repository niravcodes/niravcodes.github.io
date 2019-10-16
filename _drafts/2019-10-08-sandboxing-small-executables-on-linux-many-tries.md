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

So, I decided to write a web app to make the program easily accessible.<!--more--> The web app lets user write code in their browser, then compiles and executes the program on the server, and allows the user to send input from the browser to the server as it executes.

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

Because these features are provided natively by the Linux kernel, we can apply them using corresponding syscalls and parameters and make with a relatively robust sandbox. 

There are programs which use these features and more to sandbox applications for us. I looked at ones below:

**nsjail:** I couldn't get it to compile because of some strange protobuf dependency error. It doesn't help that the GitHub readme doesn't have any build steps or the versions of dependencies required. Which is a shame because this was almost exactly what I was looking for: a lightweight application sandbox. I might look into it some more later. [This ](https://nsjail.com "https://nsjail.com")is the official site.

**mbox:** doesn't work in 2019. -n still allows networks. Guessing that it relies on kernel specific features. Development halted 4 years ago. Also, reading the author's paper and ycombinator comments, you get the feeling that he's much more proud of his filesystem layering work than his sandboxing work. Also, it seems more like some academic/proof-of-concept work someone coded to escape real life (much like I coded Huffman Compression). Doesn't fit my requirements.

Docker Heavy and not built for my use case. Not for security. Can be broken out of. At any rate, I'm not gonna be instantiating full containers for executing a sub-megabyte program.

minijail I found about 2 days after i began my search.

systemd-nspawn looks interesting, but too heavy for my case

custom:

namespaces, chroot, seccomp-bpf, kafel, cgroups, users etc

PS: Mosh is really cool substutite to ssh.

For problems that include running untrusted executables on sensitive servers, a software tool called _sandbox_ is often used. Unsafe binaries are executed inside the sandbox