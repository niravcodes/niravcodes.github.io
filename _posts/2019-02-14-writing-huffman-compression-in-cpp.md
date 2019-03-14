---
excerpt_separator: "<!--more-->"
layout: post
title: Implementing the Huffman Compression Algorithm in C++
tags:
- huffman_code
- c++
- coding
- project
feature-img: https://nirav.com.np/assets/img/Webp.net-resizeimage (1).jpg
thumbnail: ''
date: 2019-02-14 13:05:22 +0000

---
Da Vinci is quoted saying, "Art is never finished, only abandoned". I don't see why it should be any different for code. With that said, I'd like to declare my latest project: an [implementation of huffman's algorithm](https://github.com/niravcodes/huffman_compression "Huffman Compression Implementation by Nirav"), finis— abandoned. I meant to say abandoned. Missed my chance.

<!--more-->

So anyway, I've been working on it for about a week. I started a day before my Data Communication assessment inspired by a chapter on the Information Theory. There I was, at 11 in the night, having read for the first time in my life about huffman's algorithm and **I was thrilled!** I decided then, in the spur of the moment, to pull an all-nighter and write code for the huffman algorithm. Then I boiled some water, made myself a cup of strong coffee.

And then I fell asleep.

Admittedly the beginning was lackluster, but in the days that followed, I did write code in earnest. And by the end of the week, I got it working. I've got to say that the it took a lot longer that I had estimated. I think that's in part due to my decision not to use the C++ standard template library. But all the same, it took way longer than I thought it would.

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

When I set out to implement Huffman's algorithm, I had two main objectives:

1. Compare it with gzip to see how well it fares.
   * I can tell you right away that compared to gzip, huffman sucks. There is a huge difference. If you want to try for yourself, [clone the repo from github](https://github.com/niravcodes/huffman_compression). But that is not the whole story, because gzip is itself a combination of LZ77 followed by huffman compression. Gzip is built with huffman compression as one of it's pillars (see also: [DEFLATE](https://en.wikipedia.org/wiki/DEFLATE)).
2. See if it is feasible in memory constrained embedded systems (like atmega or at89c205x)
   * It seems doable. Huffman decompression doesn't require a lot of RAM (with the compression table in PROGMEM) and it doesn't matter if the decompression is slow because it's okay to do it one sample at a time, every 1/8000th of a second. This might be my next project after the exams end.

I learnt a **lot** of things with this project. This was my first time playing with binary files. 