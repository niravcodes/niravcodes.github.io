---
excerpt_separator: "<!--more-->"
layout: post
title: An Octopus and a Game Engine
tags:
  - javascript
  - game-development
  - game
enableNepali: false
feature-img: https://nirav.com.np/assets/img/browntrunk.jpg
thumbnail: ""
---

I started making this thing as a one-day experiment: a fun little browser-game I could craft before committing to the everlooming neverending self-judo one-man-deathwrestle called exams. But it instead ended up spreading out sparse as intense hour-long coding sessions throughout the Quarantine months.<!--more--> This is how it turned out finally:

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/zVu_AQDCDgY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

To play this game in your browser, [click here](https://nirav.com.np/Octopus-Game-JS).

Before starting, the question was how I would simulate the motion of an octopus in the ocean. So I started with a prototype in javascript. After some trial and error, and some primitive physics, I had the rough behavior of the octopus down.

![GIF of initial game prototype](/assets/img/octo/initOctoGif.gif)

It worked as I'd envisioned but looked rather drab. So I found a placeholder animation on Dribbble by [Narubalie](https://dribbble.com/shots/3492217-Octopus-gif-animation) and put it in. At this stage I had to write an animation-player for the game, because HTML5 canvas can't directly play a gif.

<video autoplay loop muted> <source src="/assets/img/octo/octo2.mp4" type="video/mp4"> </video>

Next I wrote an AABB collision detection system (meaning non-rotating rectangular bounding boxes can now detect when they overlap). So now I could finally make a little island for the octopus to land on.

<video autoplay loop muted> <source src="/assets/img/octo/octo0.mp4" type="video/mp4"> </video>

Next up is obviously an angry enemy angler fish. I found a cool animation on Tumblr made by [Blabberf](https://blabberf.whalecakes.com/), and coded it's motion.

<video autoplay loop muted> <source src="/assets/img/octo/octo3.mp4" type="video/mp4"> </video>

Now I wanted the octopus to be able to explore the ocean outside of the rectangular box it's confined in. So I wrote a camera system that will follow the octopus wherever it goes. I was also experimenting with different speeds at this time so it might seem jumpy in the video.

<video controls muted> <source src="/assets/img/octo/octocamera.mp4" type="video/mp4"> </video>

Then I wrote the level management system and made new components (text, static image, etc) to build the UI of the game with. I found a nice octopus icon made by [FreePik](http://www.freepik.com/) from [flaticon.com](https://www.flaticon.com/) for the title screen.

![Picture of Octupus Game UI](/assets/img/octo/ui.jpg)

At some point, I realized that I could decouple the game code from the game engine code, so I did. Then, just for kicks, I made a [Flappy Bird clone](https://nirav.com.np/2020/06/09/flappy-millennial-an-html5-canvas-game.html) using only the Engine code, which was rather fun.

Now I wanted to animate my own main character instead of using some random image on the internet. So I studied a lot of videos on octopus motion, and got to work on Piskel app, which is a nice browser-based pixel art software. After laboring over the motion for days, this is what I came up with:

![octopus swimming](/assets/img/octo/octoAnimOne.gif)

You'll notice that this octopus is far more exaggerated in motion than the previous one, which is intentional, and I'm rather proud of this.

Next, I made the animation of the octopus crawling on the floor.

![octopus crawling](/assets/img/octo/octoWalk.gif)

You might notice that the sprites are lacking colors. That's because I'm not a good artist, and colors are difficult.

Next I coded a quick background parallax system and a minimal emitter system to emit bubbles convincingly. This is the end result.

<video controls muted> <source src="/assets/img/octo/octo5.mp4" type="video/mp4"> </video>

Then I burned out. And now I can't bring myself to even look at the code. Maybe you can, though. So check out the [code on GitHub](https://github.com/niravcodes/Octopus-Game-JS).

### Conclusion

I worked on this project without much planning, or design.
So it was interesting to see the abstractions almost form themselves, and to see the architecture emerge spontaneously from beneath
the insignificant lines of code as I typed them.

Right in front of my eyes, the coordinate-based motion wrapped itself in a physics
interface and neatly exposed methods like `applyForce (magnitude, angle)`. The `Spritesheet` animation system amalgamated
with `Motion` and `Collider` to from a high level `Character` object for my benefit. Components
organised themselves into categories like `drawable`s and `manager`s, which allowed for other interesting experiments
like [duck-typing-aided composition](https://stackoverflow.com/q/62194995/2735127).

Not to mean that it is perfection, of course. Far from it. On the engine side, the API is painful, there's a lot of vestigial code, scenes are
not isolated (and colliders leak through by default), there is no obvious way to handle instantiation of multiple
objects, and there's a lot of cohesion among components. On the game side, the controls are terrible, the world is incomplete, and
moving around is clumsy at best. The only consolation is that my next game will be easier to make because of this exercise.
