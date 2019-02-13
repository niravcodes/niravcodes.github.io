---
excerpt_separator: "<!--more-->"
layout: post
title: How premature optimization cost me half a day
tags:
- thoughts
- coding
feature-img: ''
thumbnail: ''
date: 2019-02-12 17:11:38 +0000

---
I have been programming in 8-bit AVRs exclusively for some time to make things like huge Dot-Matrix Displays, self-balancing robots and DACs. And as it turns out, I have been unwittingly picking up the conventions specific to embedded programming and 8-bit devices.

The one that cost me some amount of consternation lately is the habit of using `unsigned char` instead of `int` when you can. On 8-bit AVRs, this is an important thing to do whenever you can, because they have extremely limited memories (counted in bytes!). It doesn't help that I often select the cheapest and least powerful chips in my box to do a job (which, incidentally, means that I find myself programming for the 8051 much frequently than I'd like).

So anyway, I seem to have carried over this specific ritual even when I'm programming for desktops. The idea is simple. If you are sure values don't exceed 256, don't use `int`. Of course, saving a few bytes doesn't matter much when you have the room for literally billions of bytes, but still, why be wasteful, right?

Wrong. A couple of things:

1. As it turns out, most processors require data in the memory to be word-aligned. That is, a 32 bit system is only be able to read data at addresses that are divisible by 2. I suppose this is done to reduce the number of lines in the address bus but for whatever reason that's how it is. This essentially means that your one byte char might be occupying full 4 bytes of memory for alignment reasons.
2. It is likely that the `unsigned char` needs to be converted to `int` to perform arithmetic operations and then back. The smaller datatype you innocently chose for it's size cost you several extra clock cycles without actually saving any memory.

Of course, processors and compilers are complex beasts and the only way of being sure of these things is to benchmark extensively.

What actually happened was this. I am programming a [Huffman compression program](https://github.com/niravcodes/huffman_compression "github link to huffman compression") because I have always been fascinated with data compression. I will talk about it a little more in a future post but for now suffice it to say that my implementation required a priority queue.

Since I was sure that I would have less than or exactly 256 items in the queue, I decided to use an `unsigned char` to represent the number of characters. 

{% highlight c++ linenos %}
class priority_queue
{
private:
  tree::node *alphabets;
  unsigned char top;

public:
  priority_queue();
  ~priority_queue();
  bool is_empty();
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

The problem with this code is that it tries to solve a problem that it created itself. There was virtually no reason for the `top` variable to be `unsigned char`. Yet, it is, because of the programmer's eagerness to micro-optimize. This is what intelligent people call 'premature optimization'. To prevent the queue from overwriting previous data, enqueue is not performed if the queue is full. But notice that the `top` pointer is overloaded. It has two distinct jobs to perform. One of them is obvious: to store the index of the array where next insertion is supposed to take place. i.e if `top` is 10, it means that next element is to be inserted at the 10th position.

The other is somewhat hidden. `top` is also used to infer if the queue is empty or full. This is actually an elegant way to repurpose the same counter for two purposes, and this idea can be represented eloquently using the increment and decrement operators in C++. But it fails in this case because `top` is not big enough to do both things at once. The `unsigned char` `top` can encode 256 values. If the array is empty, then the value of `top` is 0. If array is full, then the value is 256. From 0 through 256 there are actually 257 values. So using `unsigned char` won't be enough to encode both pieces of informaton at once. In other words, we won't be able to tell if the array is full or empty. They call this the Pigeonhole theorem.

At any rate, this means that the naively placed code

{% highlight c++ %}
if (top == 255)
        return;
{% endhighlight %}

doesn't help prevent the overflow. Instead, it simply refuses to insert the last element in the array. Which is what I failed to realize for half a day as I looked here and there to find the bug that occured in another part of the system. 