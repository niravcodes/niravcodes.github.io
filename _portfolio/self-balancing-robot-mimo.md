---
title: Self-Balancing Robot (MIMO)
layout: post
img: https://nirav.com.np/assets/img/mimosmall.png
feature-img: https://nirav.com.np/assets/img/mimo.png
---

I really wish I had more photos. But we were so busy that the thought didn't even cross our minds. And because this we made this using college resources, we had to return the project back to college. So all I have is this one video which my friend had taken using his laptop's webcam.

<iframe width="560" height="315" src="https://www.youtube.com/embed/-HTUWfT0hFI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

This is my first proper electronics project. I had just learnt to make printed circuit boards, I had just started learning about 3D printing, and I hadn't had much experience with AVR's either.

Making the circuit board was most fun. We made two double-sided PCBs which we stacked one on top of the other. One of them had the AVR and the other had two L293Ds to drive the motors.

3D printing caused many problems. The initial chassis I had designed for the robot in FreeCAD was very large. It would have taken 6+ hours to print. But because of intermittent power-cuts we'd been having, I didn't get to print it at all. I spent the last few days preceding the exhibition in the Robotics Club room watching the chassis being printed, and praying for a. the power to stay and b. the filament to not run out. 

My prayers didn't work. The power kept cutting and eventually the filament ran out. It'd have been too late if we waited for another roll to ship. So in the end, Bhuban came up with the idea of using the half-made bodies of the robot to build a makeshift body for the bot. It's amazing what he was able to do with the parts.

Power supply was another issue. We didn't have time to wait for the shipping of boost-buck regulators. So we bought some mobile phone batteries, wired them together with LM7805s and used two to power the AVR and other two to power the motors and motor drivers. We ended up with a relatively robust power system, and the circuits were functioning fine. But because we didn't have time to loop tune the PID, the robot was never quite able to balance itself. Oh well, we tried.