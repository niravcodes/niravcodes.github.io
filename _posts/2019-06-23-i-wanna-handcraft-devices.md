---
excerpt_separator: "<!--more-->"
layout: post
title: I wanna handcraft devices
tags:
- ramblings
feature-img: https://nirav.com.np/assets/img/clutter-drill-garage-115558.jpg
thumbnail: ''

---
I happened upon a video talking about the iPod shuffles today. I fell in love with the design of the devices, so I went to the [ifixit](https://www.ifixit.com/Teardown/iPod+shuffle+3rd+Generation+Teardown/673) website and looked at the teardowns. From the inside, they looked even more beautiful. I already like designing small gadgets that I might never build. Starting with the rough sketches, then thinking about the electronics, the user experience and all other constraints is a great mental exercise (not to mention the best way to sit through long boring lectures).

<!--more-->

In this post, I am going to write down what I would do if I had the time and the resources to make one of my dream products. Keep in mind that these are just sad fantasies of a clumsy boy, and might never see the light of day.

![](https://nirav.com.np/assets/img/EamggrwEhwoBS16W.full.jpg)

I would start out by sketching many ideas for the device and think about how the user might interface with it. Since I'm not concerned about appealing to a wide audience, I can pick strange and arcane inputs, like Morse code or gestures on capacitive-touch sensor array. I had researched extensively on fabricating capacitive-touch sensors last semester, and it seemed doable even with the little resources that I have.

Anyway, after simplifying and refining the initial ideas, I would design a 3D model in Blender or Fusion360, and print it out on a 3D printer to get a general feel of the device. That 3D printout would also help me think about the volumetric arrangement of electronic components inside the device body. At this point, I would have to really think about whether all the electronics fit inside the housing I designed. In fact, at this stage, I would have to work with IC datasheets and tolerances, technical drawings of batteries etc. just to make sure that all things fit properly like a 3D jigsaw.

![](https://nirav.com.np/assets/img/ipodsh3.jpg)

After the design phase finishes, I think I would start working on the electronics immediately. First make a list of all the components, then collect their datasheets and read them to make sure they are compatible with each other. They nearly never are. So I'd have to first design proper voltage regulation and logic translation. I wouldn't mind working with SMD parts as long as Sauhard can get them for me. (Which he probably can't. But this only a dream, anyway.) I would design the Printed Circuit Board in KiCAD and do all the routing by hand.

I would then transfer the circuit routing on a 2-layer PCB using toner-transfer method. Those plated I'd dip into a boiling tub of FeCL<sub>3</sub> and stir them to etch away the excess copper. Next, I'd take that plate and drill tiny 1 mm holes where the through-hole components go. Then I'd solder everything and test the electronics.

I love writing software for custom electronics. It feels so cool to write firmware for your own, extremely specialized hardware. I would start working on that next. Naturally, I'd have some temporary headers for  In-System Programming the circuit. After I am satisfied with the firmware and all the interfaces feel natural and intuitive, I'd test it the entire system inside the 3D printed case. After making sure that everything behaves beautifully, I'd reach the final part of the development process.

At this point, the innards are done. The interface feels solid. The firmware works without a hitch. And the CPU sleep wake cycles as well as all other peripherals have been meticulously programmed to consume as little power as possible, it is time to build a beautiful case for the product.

I would either mill the body with CNC or manually craft the piece in the workshop. Or I could cast metal to get the desired shape. This is the a crucial part of the product development because the choice of metal and the time I spend working on it directly influence how it feels in the hands.

If I end up working with aluminium then I could anodize the body and dye it to get nice colors. With laser cut acrylic, I could showcase the internal electronics, but plastic doesn't feel so good in the hand. I could also incorporate glass.

![](https://nirav.com.np/assets/img/tech_1.jpg)

There is a particular charm to a thing that is built by passionate craftsmen.

_The first two pictures are from_ [_ifixit_](https://ifixit.com) _licensed under creative commons. The last exploded view was drawn by_ [_Silvan Linn_](http://www.silvanlinn.com) _(license not stated)._