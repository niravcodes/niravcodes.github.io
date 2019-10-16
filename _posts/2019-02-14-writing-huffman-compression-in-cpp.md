---
title: Implementing the Huffman Compression Algorithm in C++
date: 2019-02-14 13:05:22 Z
tags:
- huffman_code
- c++
- coding
- project
excerpt_separator: "<!--more-->"
layout: post
feature-img: https://nirav.com.np/assets/img/Webp.net-resizeimage (1).jpg
thumbnail: ''
---

_The final code is in GitHub_ [_here_](https://github.com/niravcodes/huffman_compression "Link to NiravCodes's Huffman Compression on Github")_._

Da Vinci is quoted saying, "Art is never finished, only abandoned". I don't see why it should be any different for code. With that said, I'd like to declare my latest project: an [implementation of the huffman's algorithm](https://github.com/niravcodes/huffman_compression "Huffman Compression Implementation by Nirav"), abandoned. It works well as it is, but it can be made a lot better. I just don't want to be the one doing that.

<!--more-->

So anyway, I've been working on it for about a week. I started a day before my Data Communication assessment inspired by a chapter on the Information Theory. There I was, at 11 in the night, having read for the first time in my life about huffman's algorithm and **I was thrilled!** I decided then, in the spur of the moment, to pull an all-nighter and write code for the huffman algorithm. Then I boiled some water, made myself a cup of strong coffee.

And then I fell asleep.

Admittedly the beginning was lackluster, but in the days that followed, I did code in earnest. And by the end of the week, I got it working. It took a lot longer than I had estimated. Why? well,

1. The code doesn't use C++ templates.
2. [This](https://nirav.com.np/2019/02/17/the-hungry-operator-eats-whitespace.html) (I didn't know istream ignores the bytes that represent whitespace in ASCII **even in binary input mode**)
3. [This](https://nirav.com.np/2019/02/12/how-premature-optimization-cost-me-half-a-day.html) (I'm stupid)

# Huffman Compression

For those of you who don't know, huffman's algorithm takes a very simple idea and finds an elegant way to implement it. At its heart is the observation that the more a thing is mentioned, the shorter its name should be. This idea manifests itself in daily life too. For example, we use nicknames for people we call often, we have abbreviations for long words we often have to use and even the word ok was once an abbreviation for "all correct".

Translated to the world of computers, it means that if a chunk of data repeats itself more than another chunk of data in the same group, it is best to encode the more occurring chunk with smaller code word. Practically what it means is that the compressed file has two parts. First there is a dictionary of code words and their corresponding chunks of data. And then there is a the data itself, encoded using codewords (often called payload in compression jargon). During decompression, the dictionary is read and the codewords are sequentially translated into actual data.

Of course, the implementation of this idea requires us to first solve a few problems. For one, uncompressed data is easy to read. The specification of the file format is all you need to extract relevant information from uncompressed files. In uncompressed audio, say, a fixed number of bytes unambiguously make up a sample i.e a single amplitude in the sound wave. Simply by reading one sample at a time and setting a proportional voltage across the speaker you convert the digital representation into real sound. And if you time it right, you might even hear the music. But once you compress that raw file with the scheme I mentioned above things start to get tricky.

Say this is the data you want to compress:

> BANANA

The ASCII codes for the alphabets in binary are:

> B : 01000010
>
> A : 01000001
>
> N : 01001110

Thus the ASCII encoding of BANANA is:

> 01000010 01000001 01001110 01000001 01001110 01000001

Keep in mind that when the computer is reading ASCII text files, it always does so in chunks of 8 bits per character. That's the standard. So the computer always knows that every 8 bits can be read from the file and matched against the ASCII table already in it's memory to find which character was typed.

Let's try to compress this with the aforementioned scheme of calling more frequent chunks of data with smaller nicknames. We will start with a naive interpretation.

> A : Occurs thrice. Let's call it a 0
>
> N : Occurs twice. Let's call it a 1
>
> B : Occurs once. Let's call it a 10

The compressed data thus turns out to be:

> 1001010

Lets see the uncompressed data again.

> 01000010 01000001 01001110 01000001 01001110 01000001

That's a massive shrinkage. Now let's try decompressing it. We come across a massive problem. There are multiple ways to decode the compressed string based on how you divide the codewords. Here are a few:

> 10-0-1-0-1-0 : BANANA
>
> 1-0-0-10-10 : NAABB
>
> 1-0-0-1-0-1-0 : NAANANA

See the problem? We wanted to say BANANA but started singing Havana instead. Of what use is a compression scheme if you can't decompress deterministically? Think about it. It is mathematically impossible to derive the original message using only the compressed message and the the dictionary without also sending other information about the message (which ends up making the compressed file larger than the original).

This is where we introduce the concept of prefix code (also called prefix-free code). The idea is simple. In our naive compression scheme, we introduce a constraint. No codeword can start with another codeword. In other words, no codeword in the system is the prefix of another codeword. So if you read the bitstream from left to right, if you come across a valid entry in the code dictionary, it can be safely translated to the original symbol. We essentially scan the compressed data sequentially, recognize codewords, translate them, and carry on.

Applied to the BANANA example, the prefix constraint results in the following correction:

> A : Occurs thrice. Let's call it a 0
>
> N : Occurs twice. Let's call it a 10
>
> B : Occurs once. Let's call it a 11

Notice how, in this system, no codeword is the prefix of another codeword. BANANA now compresses to `110100100`. This can be deterministically recovered to BANANA.

And this is what the huffman compression does. Given a set of symbols and their respective frequencies, it churns out the smallest prefix codewords to represent them all. That is the huffman compression. And there are other algorithms to do this, most notably Shannon-Fano algorithm (which they also expect me to memorize for exams), but as wikipedia says, "[Shannon–Fano](https://en.wikipedia.org/wiki/Shannon%E2%80%93Fano_coding) is almost never used; [Huffman coding](https://en.wikipedia.org/wiki/Huffman_coding "Huffman coding") is almost as computationally simple and produces prefix codes that always achieve the lowest expected code word length \[as opposed to Shannon-Fano\]".

How huffman's algorithm does that is actually pretty interesting too. I am far too lazy to describe it all in this post, but this video by computerphile (along with all others related to compression) are great if you're just starting.

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/umTbivyJoiI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# The Implementation

The implementation is really the simplest I could find. It is very slow and not optimized for anything except coding efficiency. The alphabets are _always_ bytes, for the sake of simplicity. This means that the 'chunk of data' that I talked about is always a single byte.

Follow [this link](https://github.com/niravcodes/huffman_compression) to see the full code in GitHub.

Here is how it compresses a file:

1. `count_frequency()` returns an array of size 256 with the byte alphabet as index and it's corresponding frequency as the value. If, for instance, the byte 0x25 (37 in decimal) occurs 50 times in the file, the array\[37\] has value of 50.
2. The tree::node class (I used a nested class for some inexplicable reason) represents one single alphabet with a data and a frequency property. 256 new tree::node objects are created, one for each alphabet. They are pushed into a priority queue. The priority queue takes in elements in an arbitrary order, but dequeues them in a fixed order. In this case, the lowest frequency alphabets are always popped first.
3. The `make_huffman_code()` function pops two elements from the priority queue, makes a new element (say X) with the two elements as two leaves and puts the new element X back in the queue. X is a node in the huffman's tree. This goes on in a loop until only one element is left in the priority queue. That is the root of the huffman tree, and all other elements are it's descendants.
4. The huffman tree is traversed for every alphabet and a codeword is generated by the `generate_code()` function. This function returns an array of objects of class `huffman_code`. The class `huffman_code` encodes the huffman's code which needs to pieces of information to be correctly understood: the code itself, and the length of the code as that can vary too.
5. Using the array, we encode the original file. A class `bitstream` is used here to pack the variable-bit-length huffman codes. The `bitstream` class uses a little buffer in memory to pack the codes. Once the buffer overflows, it signals the buffer to be flushed to the file and restores the buffer with the overflowed contents. This helps keep the memory requirements independent of the size of file being compressed. The details of the file format are in the [README.md](https://github.com/niravcodes/huffman_compression/blob/master/README.md).

The soul of this entire code base is the following code.

{% highlight cpp linenos %}
tree *make_huffman_tree(input_param options)
{
    //open the file for inspection
    ifstream in_file;
    in_file.open(options.input_file, ios::binary | ios::in);

    // count the frequency of all 256 bytes
    unsigned *count = count_frequency(in_file, options.input_file_size);

    priority_queue<tree::node> *x = generate_alphabets(count);

    //count[] is no longer needed
    delete[] count;

    int cnt = 0;
    tree::node *a, *b, element, c;

    while (x->element_count() > 1)
    {
        element = x->dequeue();
        a = new tree::node(element);
        element = x->dequeue();
        b = new tree::node(element);
        c = tree::node(0, a->get_frequency() + b->get_frequency(), a, b);
        x->enqueue(c);
    }

    //there is only one element in the priority queue now: The root.
    element = x->dequeue();
    tree::node *root = new tree::node(element);
    tree *huffman_tree = new tree(root);

    in_file.close();
    return huffman_tree;
}
{% endhighlight %}

Since the huffman codes are of variable lengths, I had to write a special bit stream packing class. It can work with arbitrarily sized buffers and has a mechanism to avoid buffer overflows. I had the most fun working on that class. The header is below:

{% highlight linenos cpp %}
typedef unsigned char byte;
class bitstream
{
protected:
  byte *buffer;
  unsigned buffer_size; //in bytes
  unsigned bit_pos;     //in bits

  unsigned remainder; // to store overflowing data
  unsigned remainder_size;

  inline unsigned get_byte_pos();
  inline unsigned get_bit_offset();
  inline unsigned get_free_bits();
  int micropack(byte, unsigned);
  
  // after the buffer has been emptied, 
  // pack remainder inside buffer
  bool add_remainder(unsigned, unsigned);

public:
  bitstream(unsigned buffer_size_in_bytes);
  ~bitstream();

  unsigned get_occupied_bytes();

  // packs data into buffer upto specified size
  // returns true if okay
  // returns false if the buffer has filled up
  // if pack is false, flush then reset buffer
  bool pack(unsigned huffman_code, unsigned code_length);
  
  //gives you a pointer to the buffer
  const byte *flush_buffer();
  
  //clears the buffer then packs remainder in
  int reset_buffer();
};
{% endhighlight %}

During decompression:

1. The compressed file is checked for the file signature.
2. The table is read and stored in memory as an array (lets call it dictionary).
3. The `pluck_bit()` plucks successive bits from the file. Every bit of the file is appended to a variable, then the variable is checked with all 256 entries of the dictionary. If it matches, the corresponding byte is appended to the decompressed file and the variable is cleared.

This is the most naive way I can think of to decompress the file. But one good thing about a slow decompression is that I got to make a progress bar. This might be the first time I wrote a program that takes long enough to make progress-bar mandatory (apart from file-uploads, of course).

# Closing remarks

When I set out to implement Huffman's algorithm, I had two main objectives:

1. Compare it with gzip to see how well it fares.
   * I can tell you right away that compared to gzip, huffman sucks. There is a huge difference. If you want to try for yourself, [clone the repo from github](https://github.com/niravcodes/huffman_compression). But that is not the whole story. Gzip is itself a combination of LZ77 followed by a series of huffman compressions. Gzip is built with huffman compression as one of it's pillars (see also: [DEFLATE](https://en.wikipedia.org/wiki/DEFLATE)). So I suppose huffman wins.
   * See if it is feasible in memory constrained embedded systems (like atmega or at89c2051). It seems doable. Huffman decompression doesn't require a lot of RAM (with the compression table stored in PROGMEM) and it doesn't matter if the decompression is slow because it's okay to do it one sample at a time, every 1/8000th of a second. This might be my next project after the exams end.

I learnt a **lot** of things with this project. I got a glimpse of the immense mathematical complexity that is hidden underneath the abstractions and the tools of compression. I learnt a lot more about gzip compression and LZ77 algorithm. I learnt how a code can be slow, and [how to make it faster](https://commandlinefanatic.com/cgi-bin/showarticle.cgi?article=art007). But new things were not all that I learnt. I got to learn more about the good old C++. It's various idiosyncrasies, it's weaknesses and strengths, memory management, code segregation and better use of test programs. I know, I still have a long way to go, but this project has been a important step towards that destination.