---
excerpt_separator: "<!--more-->"
layout: post
title: The >> ate my whitespace
tags:
- coding
- random
- c++
feature-img: ''
thumbnail: ''
date: 2019-02-17 16:36:55 +0000

---
Oh >>. You lovely little monster. You yellow sunshine and soggy cloudbrust. You 90° rotation of the nubivagant VV. You avian symbol of death. You ugly angular whitespace eater. You forward-facing time-stealing progressive peckerhead. You suck. I don't like you anymore. From today onwards, I devote my unwavering loyalty to the beautiful get().
<!--more-->

What did it do to me, you ask? It ate away my whitespace. Take this trivial code:

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

On execution, say you type in `10 20 30 40` and hit `↵`. The >> operator takes the input, delimits it by whitespace, converts the strings to integer and puts the final value into corresponding variables (a, b, c, d). Convenient, right?

Yeah, pretty much. That is, until you get so comfortable that you start doing this:

{% highlight c++ %}
	struct stat stat_buf;
    long filesize = stat(filename.c_str(), &stat_buf).st_size;
    
    ifstream in;
    in.open(filename, ios::binary | ios::in);
	
    for (

    
{% endhighlight %}