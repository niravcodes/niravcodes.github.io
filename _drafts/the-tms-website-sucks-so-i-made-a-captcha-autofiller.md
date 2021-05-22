---
excerpt_separator: "<!--more-->"
layout: post
title: The TMS website sucks so I made a captcha autofiller
tags: []
enableNepali: false
feature-img: ''
thumbnail: ''

---
In keeping with the spirit of the times, I've started playing with the Nepali Stock Exchange. It is a strange, distorted world for someone like me who's used to the determinism of the computer realm. And so far, it has just proved to be a more fashionable way of losing money. But it's addictive!

If you've ever had to use Nepal Stock Exchange's Trade Management System (often called just TMS), you probably hate it.<!--more--> It is at best an incompetently made software with many glaring issues, hosted over a woefully underpowered infrastructure that cannot even handle the most predictable of traffic spikes. On more than one occasion I've oversold or undersold shares because it's UI was out of sync with it's database.

The TMS's login captcha is the epitome of this incompetence and negligence.

![](https://nirav.com.np/assets/img/captcha.png)

If you didn't know, a captcha is supposed to be a challenge that only humans can solve in a reasonable time. A malicious computer program which, if unopposed, could execute hundreds of thousands of requests every second testing various username:password combos or security vulnerabilities, or just plain overloading the system so that it becomes unresponsive to legitimate users, is blocked by the captcha.

  
With that definition, however, the TMS's "captcha" actually turns out to be an _anti-captcha_, the exact opposite. It appears as a challenge to the user, who has to manually type it out every time. **But it is completely transparent to any half-decent computer script**. In fact, when you hit the login button, the captcha is not even sent to the server. It's a purely cosmetic effect. It's like a gate that you have to painstakingly unlock every time, but every burglar can pass through it as if it wasn't even there.

![](https://lh6.googleusercontent.com/Gb2u0Fx_UPetJyFtK-NQphrDufu2nHuW-_bFAJkcyt16dfFQ6zb-V90VNsSui1nhGSd3GqDUd3xk0QFqevVKQK-hDynH1UwqJswgYNaaJQfi0ovWSv_XGqeOHZW2duunEfbl8v56 =408x402)

## The TMS captcha implementation

Even a cursory inspection will show that the implementation of the TMS captcha system is not an actual captcha. Any OCR like Google Lens can read it readily, making it very cheap to overcome.  
But you don't have to go that far. The captcha's random text is generated in the browser by a simple JavaScript code, and it's laid over an static image. The css \`user-select\` property is set to \`none\` so you can't just copy the text from over the image and paste it in the captcha field.   
Which means it should be accessible via the DOM:

![](https://lh4.googleusercontent.com/6tX3zV0oV03d1I1Ej0DjXiWEJ1HSS7Mp7R833CGKUjy29IFJoE3MyBywEMu3CZCJ0bN_FC9QUoHKGLEBmxjIpUzJV-8HIRQ6QhN1CpfyateBVYFXQ_6uKA9pusYmwsYVdJhGevAr =349x329)

Unsurprisingly, it is.

  
Now, if you can read the text from the DOM, it's not a big deal to write it back to DOM:

{% highlight %}

document.getElementById("captchaEnter").value = document.getElementById("randomfield").value;

{% end_highlight %}

This piece of code will autofill the captcha input.

### A problem arises

An interesting problem that emerges is that when you autofill the captcha input via JavaScript then and hit Login, the website still says "Incorrect Captcha" even when the captcha is actually correct.

But how could that be? Could the TMS's system be more well thought out than I expected?

You wish! Turns out, they're using a frontend framework (Angular.js). Angular.js internally maintains a state, with the values of all inputs. That state gets altered only when the corresponding input's \`input\` event is fired. But that's easy. Here:

{% highlight %}

{  
const $ = _ => document.getElementById(_) //aliasing a long fn call

function l() {

$("captchaEnter").value = $("randomfield").value

$("captchaEnter").dispatchEvent(new Event("input")) // Fire the event to trigger angular state change

}

window.onload = l;  
}

{% end_highlight %}

And with that, the captcha auto-filler works.

### Making a chrome extension

Now that I've come this far, I might as well make a chrome extension. so that I don't have to deal with this again. Chrome extensions are pretty easy to make. It takes like 10 minutes to make something this simple. Here's the relevant part of the code:

1. manifest.json

{% highlight %}

{

"name": "TMS Captcha Autofiller",

"description": "This extention will autofill TMS captchas. Made by nirav.com.np",

"version": "0.5",

"manifest_version": 3,

"content_scripts": \[

{

"matches": \["https://*.nepsetms.com.np/login"\],

"js": \["contentScript.js"\]

}

\]

}

{% end_highlight %}  
  
2\. contentScript.js  
  
{% highlight %}

{  
const $ = _ => document.getElementById(_) //aliasing a long fn call

function l() {

$("captchaEnter").value = $("randomfield").value

$("captchaEnter").dispatchEvent(new Event("input")) // Fire the event to trigger angular state change

}

window.onload = l;

}

{% end_highlight %}

Done. Put these two files in a folder and import it from the chrome extension page (chrome://extensions).

A slightly more decorated version is published in my Github: github.com/niravcodes/tmscaptchaautofiller  
You can go there and install that version instead.

**Request to the TMS devs**

Please change the font in the captcha field from sans serif to a serif one if that's the least you do. Thousands of people needlessly confuse \`capital i\` and \`small L\` everyday.

  
![](https://lh4.googleusercontent.com/H4Wl5NOcUt1NuzOlit_OS_KBxnjTHW5lq-yLgkwWZd6pkwPAsH3Cn9w11vFkfpwChrwE7t_4mFBN2GYV8RgbDE8e1k3cVd1T0Zyu3ugsIRI-CiQNsPODknGFWU8LHJIMKuZEcZ6q =624x121)