---
title: How premature optimization cost me half a day
date: 2019-02-12T17:11:38.000+00:00
tags:
- thoughts
- coding
excerpt_separator: "<!--more-->"
layout: post
feature-img: https://nirav.com.np/assets/img/business-code-coding-943096.jpg
thumbnail: ''

---
I have been programming in 8-bit AVRs exclusively for some time to make things like huge dot-matrix displays, self-balancing robots and DACs. And as it turns out, I have been unwittingly picking up the conventions specific to embedded programming and 8-bit devices.
<!--more-->

The one that cost me some amount of consternation recently is the habit of using `unsigned char` instead of `int` when I can. On 8-bit AVRs, this is an important thing to do because they have extremely limited memories (counted in bytes!). It doesn't help that I often select the cheapest and least powerful chip in my box to do a job (which, incidentally, means that I find myself programming for the 8051 much often than I'd like).

So anyway, I seem to have carried over this specific ritual even when I'm programming for desktops. The idea is simple. If you are sure values don't exceed 256, don't use `int`. Of course, saving a few bytes doesn't matter much when you have the room for literally billions of bytes, but still, why be wasteful, right?

Wrong. A couple of things:

1. As it turns out, most processors require data in the memory to be word-aligned. That is, a 32 bit system is only be able to read data at addresses that are divisible by 4. I suppose this is done to reduce the number of lines in the address bus but for whatever reason that's how it is. This essentially means that your one byte char might be occupying full 4 bytes of memory for alignment reasons.
2. It is likely that the `unsigned char` needs to be converted to `int` to perform arithmetic operations and then back. The smaller datatype you innocently chose for it's size cost you several extra clock cycles without actually saving any memory.

Of course, processors and compilers are complex beasts and the only way of being sure of these things is to benchmark extensively.

What happened was this. I was programming a [Huffman compression program](https://github.com/niravcodes/huffman_compression "github link to huffman compression"). I will talk about it a little more in a future post but for now suffice it to say that my implementation required a priority queue.

Since I was sure that the priority queue was not going to have more than 256 items, I decided to use an `unsigned char` to represent the number of elements (`top`).

{% highlight c++ linenos %}
class priority_queue
{
private:
  tree::node *alphabets;
  unsigned char top;

public:
  priority_queue();  
  ~priority_queue();
  bool s_empty();
  void enqueue(tree::node &);
  unsigned element_count();
  tree::node dequeue();
};
{% endhighlight %}

And to prevent cyclically overwriting data in case of overflow, I wrote my enqueue code as thus:

{% highlight c++ linenos %}
priority_queue::priority_queue()
{
  alphabets = new tree::node[256];
  top = 0;
}
void priority_queue::enqueue(tree::node &lf)
{
  if (top == 255)
    return;
  alphabets[top++] = lf;
}
{% endhighlight %}

The problem with this code is that it tries to solve a problem that it created itself. There was virtually no reason for the `top` variable to be `unsigned char`. Yet, it is, because of the my eagerness to micro-optimize. This is what intelligent people call 'premature optimization'. To prevent the queue from overwriting previous data, enqueue is not performed if the queue is deemed full. But notice that the `top` pointer is overloaded. It has two distinct jobs to perform. One of them is obvious: to store the index of the array where next insertion is supposed to take place. i.e if `top` is 10, it means that next element is to be inserted at the 10th position.

The other is somewhat hidden. `top` is also used to infer if the queue is empty or full. This is actually an elegant way to repurpose the same counter for two purposes, and this idea can be written eloquently using the increment and decrements operators in C++. But it fails in this case because `top` is not big enough to do both things at once. The `unsigned char` `top` can encode 256 values. If the array is empty, then the value of `top` is 0. If array is full, then its value has to be 256. From 0 through 256 there are 257 values. So using `unsigned char` won't be enough to encode all pieces of information at once. In other words, we won't be able to tell if the array is full or empty only using `top` if we also want to keep track of all 256 items. They call this the Pigeonhole theorem.

At any rate, this means that the naively placed code

{% highlight c++ %}
if (top == 255)
  return;
{% endhighlight %}

doesn't help prevent the overflow. Instead, it simply refuses to insert the last element in the array. Which is what I failed to realize for half a day as I looked here and there to find the bug that occurred in another part of the system that used the queue. In trying to save a few bytes, I had written a code which was much more susceptible to oversights like this.

So after realizing that I had fallen victim to the textbook example of premature optimization, I rushed to write about it. It was exciting to me because I have read about premature optimization before but assumed that I would never have to deal with it. As it often happens, people think they are immune to the affliction until it befalls them.

In any case, the long and short of this post is that it's okay to make the computer work a little harder to simplify your job as a programmer. I stop my with the lines from Andrew Motion's poem _Run_ (which is perhaps irrelevant to the post but I still feel like it belongs here):

> and you had just died  
> so I was excited, still thinking your death was a thing apart