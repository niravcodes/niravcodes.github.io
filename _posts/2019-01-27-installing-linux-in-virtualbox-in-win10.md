---
excerpt_separator: "<!--more-->"
layout: post
title: Installing Linux in VirtualBox in WIN10
tags:
- tutorial
feature-img: https://nirav.com.np/assets/img/ubuntu-1710-default-wallpaper-artful.jpg
thumbnail: ''
date: 2019-01-27 16:08:17 +0000

---
_Written for the participants of the "Transitioning from Windows to Linux" program organised by iCES._

<!--more-->

## List of abbreviations

OS : Operating System  
VM : Virtual Machine  
VBox : Virtual Box  
IO : Input/Output  
MS : Microsoft  
NTC : Nepal Telecom  
HDD : Hard Disk Drive  
FSF : Free Software Foundation

## Technical Terms

* **Linux**  
  An OS just like Windows. The OS sits over your hardware and exposes only high level functions (files, IO, virtual memory ...) while abstracting away the low level details (interrupts, memory management, allocation tables ...). Linux is targeted towards developers and people who work closely with the hardware whereas Windows primarily targets the people who simply want to run programs on top of it (aka the layperson). Which means that while Windows might be the best OS for your dad to do his spreadsheets in and for your sister to watch Korean dramas, it certainly won't help you much to learn the inner workings of the computer system.
* **Virtual Box**  
  OSes are meant to have singular control over your hardware by definition. There is no way to simultaneously run more than one OS on the same set of hardware and resources unless the system is specifically engineered for that purpose (see also: Type-1 [hypervisor](https://en.wikipedia.org/wiki/Hypervisor "https://en.wikipedia.org/wiki/Hypervisor")). VBox is a special software that works on the OS like any other software program and it allows another OS to run on top of it. The guest OS runs over the VBox, and the VBox provides the guest OS with a simulated hardware set (IO devices, virtual HDD, virtual RAM and so on). This conjured set of resources is often referred to as a VM. An astute reader will notice that the host OS will always outperform the guest OS.
* **Host OS**  
  Your main operating system. The OS that your computer boots into after you press the power button. It has sole control of your hardware and bears full responsibility.
* **Guest OS**  
  The OS that runs on the virtual system conjured by VBox. Several guest OSes can coexist on a single host OS.
* **Distribution**   
  Also known as a distro. Technically the word Linux refers only to the _kernel._ A kernel provides programmatic interface to efficiently access the various components of the computer. There is not much you can do with the kernel unless there are programs running on top of it. The kernel combined with various GNU tools and libraries is called the GNU/Linux. When GNU/Linux is packaged with all the programs that run on top of it (a graphical interface, desktop managers, network managers, browsers and suchlike), it's called a distro.
* **GNU/Linux**  
  Long story short, at some point in the 90's, the [FSF](https://www.fsf.org/) had all components of an OS except for the kernel. At around the same time, Linus Torvalds had written a kernel he called Linux. At some point they decided to merge the two. The rest is history. (see also: [Richard Stallman](https://en.wikipedia.org/wiki/Richard_Stallman "https://en.wikipedia.org/wiki/Richard_Stallman"))
* **Ubuntu**  
  Ubuntu is one of many _distributions_ of the Linux system. Other distributions include Debian, Arch, Fedora and so on.

## Assumptions

1. You have a computer with at least 2 GB RAM, 30 GB free HDD space and a decent processor, running Win10 (maybe also Win7 but prefer the former).
2. You want to install Ubuntu on VBox.

## Steps

First you want to download the program Virtual Box. Do so by going to [this link](https://www.virtualbox.org/wiki/Downloads "Virtual box download site") and clicking on the "[Windows Host](https://download.virtualbox.org/virtualbox/6.0.2/VirtualBox-6.0.2-128162-Win.exe "Direct download")". We will be using the latest version (6.0.2 as of Jan 2019) which is roughly 200 MB in size. The installation process should be fairly straightforward. There is no need to tamper with the options. Just keep on hitting next till till it finishes.

Next, download the Ubuntu's official ISO files. NTC hosts [local mirrors](http://ubuntu.ntc.net.np) for the Ubuntu so downloading from there usually results in faster downloads. Go to [this link](http://ubuntu.ntc.net.np/ubuntureleases/bionic/) to download the 18.04 LTS version of Ubuntu. Be sure to download the [desktop image](http://ubuntu.ntc.net.np/ubuntureleases/bionic/ubuntu-18.04.1-desktop-amd64.iso), not the server install image.

With this, you have all the tools and images required to install Ubuntu on guest OS.

The actual process of installation is fairly involved. It consists of the following parts and sub-parts:

1. **Setting up the VM**  
   i. allocation of resources reserved for VM  
   \-  _What amount of RAM and CPU do you want to set aside for the VM? Too little will make the guest OS slow. Too much and the host OS will be rendered unstable, thus also destabilizing the guest OS. Aim for a solid middle._  
   ii. creation of Virtual HDD for the VM  
   \-  _The guest OS requires a different virtual HDD, possibly with a different file system. You need to provision space for this._
2. **Install the guest OS (Ubuntu)  
   \**You essentially boot up the virtual machine, load the Ubuntu system image (the ISO you downloaded earlier) and install the OS. This process required you to already be familiar with the Linux system. As such, we will cover this in the first day of the program. At any rate, familiarize yourself with the interface if you have the time and incentive. If you manage to successfully install Ubuntu on your VBox without our help, you will be fully qualified to boast about it on the first day and we'll think you are a cool person.

The process is detailed in this video. Go ahead and watch it full.

<iframe width="560" height="315" src="https://www.youtube.com/embed/QbmRXJJKsvs" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

After watching this video, you should feel confident about the whole process. Follow it thoroughly and if you encounter problems, we'll be there for you on the first day. After that, you're on your own, bud.