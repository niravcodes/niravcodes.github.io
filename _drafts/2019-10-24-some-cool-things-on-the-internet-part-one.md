---
excerpt_separator: "<!--more-->"
layout: post
title: Some Cool Things on the Internet
tags:
- internet
- random
enableNepali: false
feature-img: https://nirav.com.np/assets/img/backgroundcoolthings.jpg
thumbnail: ''

---
I randomly came across Marijn Haverbeke's [website](https://marijnhaverbeke.nl/ "Marijn's Website"). He has done a lot of extremely important and interesting stuff (codemirror, Eloquent Javascript, Tern), but his submission to [js1k](https://js1k.com "js1k code golfing") was particularly impressive. As always, when I come across really interesting on the internet, I hit `Ctrl+S` to save it for offline browsing. This strategy used to work nicely up till a few years ago because, thanks to the long power-cuts and on-and-off internet connectivity, you had no choice but to 'surf' your local hard drive most of the time. But these days I rarely, if ever, care to wander into the abandoned folders and files of the offline-land. So, in an effort to not forget, I am compiling lists of cool internet stuff right here on this blog.

<!--more-->

I need to set a few ground rules so as not to go overboard with this. It is important that I:

1. add things to this list as I find them on the internet and write a short description.
2. use minimal effort per entry.
3. refrain from listing extremely specialized information.

### Marijn Haverbeke's Bouncing Beholder

Link: [marijnhaerbeke.nl/js1k](https://marijnhaverbeke.nl/js1k/); License: MIT; Copyright © 2012 by Marijn Haverbeke [marijnh@gmail.com](mailto:marijnh@gmail.com)

{% highlight js %}
c=document.body.children\[0\];h=t=150;L=w=c.width=800;u=D=50;
H=\[\];R=Math.random;for($ in C=c.getContext('2d'))C\[$\[J=X=Y=0\]
\+($\[6\]||'')\]=C\[$\];setInterval("if(D)for(x=405,i=y=I=0;i<1e4;)L=H\[i++\]=
i<9|L<w&R()<.3?w:R()_u+80|0;$=++t%99-u;$=$_$/8+20;y+=Y;
x+=y-H\[(x+X)/u|0\]>9?0:X;j=H\[o=x/u|0\];Y=y<j|Y<0?Y+1:(y=j,J?-10:0);
with(C){A=function(c,x,y,r){r&&arc(x,y,r,0,7,0);fillStyle=c.P?
c:'#'+'ceff99ff78f86eeaaffffd45333'.substr(c_3,3);f();ba()};
for(D=Z=0;Z<21;Z++){Z<7&&A(Z%6,w/2,235,Z?250-15_Z:w);
i=o-5+Z;S=x-i_u;B=S>9&S<41;ta(u-S,0);G=cL(0,T=H\[i\],0,T+9);
T%6||(A(2,25,T-7,5),y^j||B&&(H\[i\]-=.1,I++));G.P=G.addColorStop;
G.P(0,i%7?'#7e3':(i^o||y^T||(y=H\[i\]+=$/99),'#c7a'));G.P(1,'#ca6');
i%4&&A(6,t/2%200,9,i%2?27:33);m(-6,h);qt(-6,T,3,T);l(47,T);
qt(56,T,56,h);A(G);i%3?0:T<w?(A(G,33,T-15,10),fc(31,T-7,4,9)):
(A(7,25,$,9),A(G,25,$,5),fc(24,$,2,h),D=B&y>$-9?1:D);ta(S-u,0)}
A(6,u,y-9,11);A(5,M=u+X_.7,Q=y-9+Y/5,8);A(8,M,Q,5);fx(I+'c',5,15)}
D=y>h?1:D",u);onkeydown=onkeyup=function(e){E=e.type\[5\]?4:0;
e=e.keyCode;J=e^38?J:E;X=e^37?e^39?X:E:-E}
{% endhighlight %}

The Javascript code above generates a playable version of the picture shown below. [Marijn's website](https://marijnhaverbeke.nl/js1k/) has both a fully playable version of the game, and some explanation of the source code and of some of the problems he faced.  
![](https://nirav.com.np/assets/img/bouncingBeholder.png)

### One-Bit Music by Tristan Perich

Link: [http://www.1bitmusic.com/](http://www.1bitmusic.com/ "http://www.1bitmusic.com/")

![](https://nirav.com.np/assets/img/Tristan_Perich_1_Bit_Symphony_Front_By_D_Yee_800.jpg)

_Photographed by Tristan Perich and taken from_ [_1bitsymphony.com_](http://www.1bitsymphony.com/ "http://www.1bitsymphony.com/")

Pictured above is an album with about 40 minutes of music. But it's not a conventional album. It has all the electronics and power required to play the music right in the Jewel case. Having done [some similar projects](https://nirav.com.np/2018/12/20/on-sound-and-audio-generation-using-atmega-microcontrollers.html) in the past, I loved what the artist [Tristan Perich](http://www.tristanperich.com/) has done here.

I found his website a long time ago, when researching to accomplish something similar, and it struck a chord with my sense of aesthetics. As I was writing this post, I remembered the project and decided that it must be included here.

### Build an electroluminescent display by Applied Science

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/Z2o_Sp2-aBo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

This video is one of my favourites on youtube, because Ben demonstrates the engineering process in such an incredibly interesting manner. If you liked this, also checkout his other video titled, "Electroluminescent paint and multi-channel control circuit".

Some other videos that I love to rewatch are:

1. [EEVblog Pebble Smartwatch Teardown](https://www.youtube.com/watch?v=MDJ0EOkU_Fg)
2. [Reverse Engineering the iPod Nano 6 LCD interface](https://www.youtube.com/watch?v=7TedIzmguP0)
3. [Interfacing a cheap phone camera module to a PIC32 microcontroller](https://www.youtube.com/watch?v=rQYByorpoFk)

### Things You Should Never Do by Joel Spolsky

Link: [https://www.joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i/](https://www.joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i/ "https://www.joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i/")

Joel On Software is an amazing blog on software engineering by none other than the co-founder of Stack Overflow. You'll find websites linking to one of his articles or quoting him in many nodes of the developer web-cluster. This article in particular puts forward some really good tips on software development that I always try to keep in mind, given my proclivity for wanting to restart start projects from scratch.

See also: Schlemiel the Painter's algorithm, the Joel Test

### Nepal Lipi Prakash by Hemraj Shakya

Published in 2030 BS (1973 AD), archived at [https://archive.org/details/NepalLipiPrakashHemrajShakya](https://archive.org/details/NepalLipiPrakashHemrajShakya "https://archive.org/details/NepalLipiPrakashHemrajShakya")

![](https://nirav.com.np/assets/img/scriptsHemraj.jpg)

This scanned copy of a book published about 50 years ago documenting scripts and inscriptions found in Nepal. It is also interesting to observe the artifacts of the printing press and the written language of that time.

### Epigrams in Programming by Alan Perlis

Link: [http://www.cs.yale.edu/homes/perlis-alan/quotes.html](http://www.cs.yale.edu/homes/perlis-alan/quotes.html "http://www.cs.yale.edu/homes/perlis-alan/quotes.html")

Alan J. Perlis, a computer scientist who received the inagural Turing Award for his work in designing ALGOL. He wrote a set of concise and witty sentences distilling his experiences in programming. They are often humorous, and give you a lot of food for thought. One of my favorites:

> In the long run every program becomes rococo - then rubble.

### Sed pathfinder

Link: [https://devpost.com/software/sed-pathfinder](https://devpost.com/software/sed-pathfinder "https://devpost.com/software/sed-pathfinder")

Yes. This guy wrote a text-based path finder in Sed! It is incredibly easy to try for yourself so give it a go. Then try to make sense of the code. 

### Mitxela's DIY video game console