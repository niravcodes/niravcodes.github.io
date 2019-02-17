---
excerpt_separator: "<!--more-->"
layout: post
title: Meet the silent whitespace stealer
tags:
- coding
- random
- c++
feature-img: https://nirav.com.np/assets/img/animal-birds-clouds-62667.jpg
thumbnail: ''
date: 2019-02-17 16:36:55 +0000

---
Oh >>. You lovely little monster. You yellow sunshine and soggy cloudbrust. You 90° rotation of the nubivagant VV. You avian symbol of death. You ugly angular whitespace eater. You forward-facing time-stealing progressive peckerhead. You suck! I don't like you anymore. From now onwards, I devote my unwavering loyalty to the archaic get().
<!--more-->

What did it do to me, you ask? It ate away my whitespace. But we'll get to that in a second.
For now, take this trivial code:

{% highlight c++ %}
string input;
cin >> input;
cout << "Hi, " << input << endl;
{% endhighlight %}

When you run it, the program pauses for your input. Say you type in `John Doe` and hit `↵` key. The program will output `Hi, John`. No, the code is not trying to get to know you on a first name basis. The >> (istream) operator is simply programmed to delimit input by spaces. This comes in handy when, for example, you want to input a list of numbers. You can write code like this:

{% highlight c++ %}
int a, b, c, d;
cin >> a >> b >> c >> d;
cout << (a+b+c+d) << endl;
{% endhighlight %}

On execution, say you type in `10 20 30 40` and hit `↵`. The >> operator takes the input, delimits it by whitespace, converts the strings to integer and puts the final value into corresponding variables (a, b, c, d) to give you the output `100`. Convenient, right?

Yeah, pretty much. That is, until you get so comfortable that you start doing this:

{% highlight c++ linenos %}
struct stat stat_buf; //"man -s 2 stat" for more on this
int rc = stat(filename.c_str(), &stat_buf);
if (rc == 0)
long filesize = stat_buf.st_size;
else
return 1;

ifstream in;
char x;
in.open(filename, ios::binary | ios::in);
    
for (long i = 0; i < filesize; i++){
    in >> x;
    // ...
    // insert your favourite
    // complicated and
    // hard to debug code here
    // ...
}
{% endhighlight %}

I wrote something similar to this in my (huffman coding program)[https://github.com/niravcodes/huffman_compression]. Two key things to note here are that the ifstream is in **binary** mode, and that a byte is extracted with >>. In binary mode, you don't have whitespaces. You don't have any meaningful data. You just have a vast desert of soulless bytes.

So I guess I trusted the convenient >> operator to have enough common sense to not treat whitespaces separately on binary mode. I mean, whitespaces are an interpretation of the byte stream, independent from the byte stream itself. They are just the empty hallucinations of the good old ASCII. 

Why then, for any reason other than to make me beat my head on the wall several thousand times, did >> ignore the whitespace characters? Maybe to be consistent with itself? Maybe. But what kind of douchebag would you have to be to sacrifice pragmatism for self-consistency? By ignoring arbitrary bytes, the >> operator loses all meaning in the binary mode. 

So I spent many hours today trying to find out why the files decompressed by my program kind of resembled the actual files but not really. 