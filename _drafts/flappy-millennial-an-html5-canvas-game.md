---
excerpt_separator: "<!--more-->"
layout: post
title: " Flappy Millennial: An HTML5 Canvas Game"
tags:
- javascript
- game
enableNepali: false
feature-img: ''
thumbnail: ''

---
Meet Flappy Millennial. He's an average guy in his mid 20's and the future looks bleak for him. With the threats of climate change, mass-extinctions, rising authoritarianism, economic depression, unprecedented wildfires and so much more ever-looming, nihilism has become his background music.

But worry not. For he has an antidote—well, not so much an antidote as a sedative. He has his phone! Come help this Flappy Millennial ignore reality while he scrolls through Instagram or something. You should play this game not because it's good or anything, but simply so you too can pretend that things are okay for a while.

![preview of the game](https://nirav.com.np/flappy-millennial/assets/preview.gif)

Play the game online at [nirav.com.np/flappy-millennial](https://nirav.com.np/flappy-millennial).

Browse the source code on GitHub at [niravcodes/flappy-millennial](https://github.com/niravcodes/flappy-millennial).

## How it came to be

I began writing a different game for HTML5 canvas a month or so ago. As I was programming the game, I realised that a lot of my code was game agnostic. The abstractions and modules that had organically emerged could be packaged up and used to make other games. So I separated the game logic from the lower level management code, and lo! I had created my first game engine essentially as a side effect of refactoring.

Over time, I began to notice some problems with the design of the game engine API, and to investigate further, I asked some of my friends to try using it to make a game and report issues. But apparently they had their own work to do and "ain't nobody got time for fun and games, we're doing Serious Work". So like a neglected grandpa weaving his own straw mat while his granddaughters make TikTok videos, I began making Flappy Millennial.


## But why another Flappy Bird clone?

Because I'm an unoriginal fuck. 

But also because Flappy Bird has an engaging gameplay with a remarkably simple game mechanic. It's a child's play to code a clone and for some reason even the worst clones turn out to be playable. To prove the assertion I wrote yet another flappy bird clone right here. Turns out just 60 lines of code and about an hour or two is enough to make a fun flappy clone. Completely playable and still addictive! Go ahead, try it out right here. Click on the square below to focus the game.

<canvas id="c" tabindex=1 style="outline:dashed 4px #000"></canvas>
<script>
let snd = new Audio("data:audio/wav;base64,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qJrx4KOQjahZxWbcZgztj2c49nKmkId44S71j0c8eV9yDK6uPRzx5X18eDvjvQ6yKo9ZSS6l//8elePK/Lf//IInrOF/FvDoADYAGBMGb7FtErm5MXMlmPAJQVgWta7Zx2go+8xJ0UiCb8LHHdftWyLJE0QIAIsI+UbXu67dZMjmgDGCGl1H+vpF4NSDckSIkk7Vd+sxEhBQMRU8j/12UIRhzSaUdQ+rQU5kGeFxm+hb1oh6pWWmv3uvmReDl0UnvtapVaIzo1jZbf/pD6ElLqSX+rUmOQNpJFa/r+sa4e/pBlAABoAAAAA3CUgShLdGIxsY7AUABPRrgCABdDuQ5GC7DqPQCgbbJUAoRSUj+NIEig0YfyWUho1VBBBA//uQZB4ABZx5zfMakeAAAAmwAAAAF5F3P0w9GtAAACfAAAAAwLhMDmAYWMgVEG1U0FIGCBgXBXAtfMH10000EEEEEECUBYln03TTTdNBDZopopYvrTTdNa325mImNg3TTPV9q3pmY0xoO6bv3r00y+IDGid/9aaaZTGMuj9mpu9Mpio1dXrr5HERTZSmqU36A3CumzN/9Robv/Xx4v9ijkSRSNLQhAWumap82WRSBUqXStV/YcS+XVLnSS+WLDroqArFkMEsAS+eWmrUzrO0oEmE40RlMZ5+ODIkAyKAGUwZ3mVKmcamcJnMW26MRPgUw6j+LkhyHGVGYjSUUKNpuJUQoOIAyDvEyG8S5yfK6dhZc0Tx1KI/gviKL6qvvFs1+bWtaz58uUNnryq6kt5RzOCkPWlVqVX2a/EEBUdU1KrXLf40GoiiFXK///qpoiDXrOgqDR38JB0bw7SoL+ZB9o1RCkQjQ2CBYZKd/+VJxZRRZlqSkKiws0WFxUyCwsKiMy7hUVFhIaCrNQsKkTIsLivwKKigsj8XYlwt/WKi2N4d//uQRCSAAjURNIHpMZBGYiaQPSYyAAABLAAAAAAAACWAAAAApUF/Mg+0aohSIRobBAsMlO//Kk4soosy1JSFRYWaLC4qZBYWFRGZdwqKiwkNBVmoWFSJkWFxX4FFRQWR+LsS4W/rFRb/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////VEFHAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAU291bmRib3kuZGUAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMjAwNGh0dHA6Ly93d3cuc291bmRib3kuZGUAAAAAAAAAACU=");  
let pnt = (r=0.20)=>{
    snd.playbackRate = r;
    snd.play();
}
let C = document.querySelector('#c');
let W=C.width=H=C.height=350;
let CC=C.getContext('2d');
colH=S=P=1;
let pipe1,pipe2;{
    let rH=()=>(Math.random()*100+50)|0;
    let pipe=(off)=>{
        let x=off, h=rH();
        return(rst)=>{
        if (rst){x=off;colH=0;return}
        if ((x=x-2)<-50) {x=W;h=rH()}
        (x>70&&x<100)?colH=h:0
        if (x==20){colH=0;++S;pnt(1)};
        CC.fillRect(x, 0,50,h);
        CC.fillRect(x,H,50,h-H+140);
    }}
    pipe1=pipe(W+100);pipe2=pipe(W+300);
}
let y=h=w=30;
window.vy=0,ay=0.4;
let LP=window.onload=()=>{
    CC.fillStyle="#235789"
    CC.fillRect(0,0,W,H);
    if (P) {
        pt("Press any key to play",H/2)
        pt("Score: "+S,H/2+40)
        pipe1(1);pipe2(1);
        return;
    }
    CC.fillStyle="#f1d302"
    y+=vy+=ay;
    CC.fillRect(70,y,w,h)
    if(colH&&(y<colH||y+h>colH+140)) {y=30;P=1;pnt()};
    y>H+h?(P=1)&(vy=0)&(y=30)&(pnt()):0;
    pipe1();pipe2();
    pt(S,40)
    requestAnimationFrame(LP);
}
CC.font = "24px 'Poiret One'"
var pt=(t,h)=>{
CC.fillStyle="#fff";
CC.fillText(t,(W-CC.measureText(t).width)/2,h)
}
c.ontouchstart=c.onkeydown=(e)=>P?(P=0)&(S=1)&(LP()):vy=-8;
</script>

Once you've played this to your heart's content, check out the JavaScript it took to make it work:

[Javascript]

That's about 60 lines of javascript which makes a playable Flappy Bird game, complete with touch screen support and sound effects.

Now, that should have been the end of it. A game in 60 lines of code is good enough. But something in me was begging to take it even further. And as if to tempt me yet more, the power went out and with it the WiFi. What is a young man in this lockdown to do without the umbilical cord of the Internet forever pumping numbness into his thoughts? 

So then I went ahead and made it even smaller.

[smaller code]

Yeah, that's right. It is 15 lines of the HTML and javascript code that will make a flappy bird game in your browser. Pretty cool, huh? But line count is not a valid metric for this. This code is less than 970 bytes. That's about 100 times smaller than the code size of flappy millennial. And it still works!

Of course, at that point I was left wondering why my actual Flappy Millennial code is so huge. 
