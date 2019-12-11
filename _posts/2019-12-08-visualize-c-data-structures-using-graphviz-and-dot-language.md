---
excerpt_separator: "<!--more-->"
layout: post
title: Visualize C++ Data Structures using Graphviz and the DOT language
tags:
- c++
- graphviz
enableNepali: false
feature-img: ''
thumbnail: ''

---
Data structures help structure and organize data effectively, and provide several abstracted operations on the data. They are elegant and convinient, and computer scientists love to use them. Implementing these data structures in the computer require the programmer to flatten the structure into a one-dimensional model using pointers or references because the memory is actually arranged as a one-dimensional sequencial run of data elements.

It is often necessary to inspect the data structure in debugging and program verification phases. But some data structures happen to be particularly graphical, in that they have multiple associations and elaborate hierarchies or layers. Think of a Rope or a Graph. Due to many associations between nodes, it's not possible to properly display the graph on the terminal.

<!--more-->

I recently ran into such problem, and found an interesting solution. In this post, I will try to document it. I've written mainly about the Abstract Syntax Tree in this post, but it should be trivial to translate it to any other deterministically traversable data structure.

I'm currently working on writing a compiler for my own Nepali programming language. The front-end part of a compiler converts the program code into a data structure called AST. AST, or Abstract Syntax Tree, is a tree-based representation of the source code. It's much more suitable to further transformations in the semantic analysis, optimization and code generation phases.

But AST is also an incredibly complex data structure. It has to store a bunch of information and maintain a tree structure. It is not immediately obvious how one might present it on the terminal screen. Several ideas to exist, but they don't scale well. Two solutions that I thought up were:

1. Print in the terminal
2. Unparse the AST back to source code.

## Unparse the AST back to source code

The AST is a lossless transformation of the source code as far as intent is concerned. So it should be possible to go the other direction and retrieve the source code back from the AST. If the AST doesn't have any errors, then it's unparsing should result in code that's nearly identical to the original source code. This step is also essential when trying to verify compiler correctness.

I'm going to have to explore this option further in the future. But because this method doesn't allow me to directly observe the AST at several stages of the compilation process, I didn't use this.

## Print in the terminal

I had written a compiler for my minor project in my 6<sup>th</sup> semester but the language it accepted was very basic. So, back then, I got away with simply printing the tree in the terminal. For example, this code

![](https://nirav.com.np/assets/img/2019-12-09-003859_1366x768_scrot.png)

generates this AST:

![](https://nirav.com.np/assets/img/2019-12-09-004011_1366x768_scrot.png)

The AST is printed in the terminal rotated 90° counter-clockwise such that the root of the tree is at the bottom-left. This was served me well at the time. Frankly, for a language that didn't even have an else if clause, there's are limited ways to complicate the AST other than by writing longer code.

But the language I'm working on right now is extensive. And so the tree it creates is immense. I had to come up with some other way to analyse the AST.

## Enter Graphviz

Brian Kernighan has given an [amazing talk](https://www.youtube.com/watch?v=Sg4U4r_AgJU "Brian Kernighan's talk on successful computer language design") on successful language design, where he also talked about Pic, a language he designed for specifying graphs. I was immediately taken by the idea because this was a much better way to make graphs than the clumsy touchpad.

Well, Brian's Pic is antiquated now, but [Graphviz](http://www.graphviz.org/) does the same kind of thing. Graphviz uses the DOT graph specification language. DOT is extremely simple. It literally takes 5 minutes to be able to make nearly any graph you want. For example, consider the DOT code below

    digraph any_other_name{
        Brahma->Ram
        Brahma->Hari
        Ram->Tom
        Hari->Dick
        Hari->Harry
    }

It produces the Graph:

![](https://nirav.com.np/assets/img/graph1.png)

I can only imagine how many hours this thing could have saved me the previous semester when I was stuck making elaborate graphs for my minor project report and presentation.

## Generating the DOT

Generating the DOT for Graphviz is generally trivial. For linked list, a recursive function such as the one below suffices (for c++):

    printElement(listElement* el, int nodeNumber){
        string DOT;
        DOT = "n" + to_string(nodeNumber) + " [label=";
        DOT+= el->name+"\"]\n";
        
        if (el->right){
        	DOT += "n" + to_string(nodeNumber) + "->";
            DOT += "n" + to_string(nodeNumber+1) + "\n"; 
            printElement(el->right, nodeNumber+1);
        }
        
        cout << DOT;
    }

It is a little more complex for the AST.

    int rootNum = 0;
    void Parser::genDOT() {
    cout << "digraph G{\n";
    cout << "graph[fontname=Rajdhani, color=\"#242038\"]\n";
    cout << "node[fontname=Rajdhani, color=\"#242038\", shape=square]\n";
    cout << "edge[fontname=Rajdhani, color=\"#242038\"]\n";
    genDOT(root, false);
    cout << "}\n";
    }
    
    void Parser::genDOT(astNode &n, bool isLeft) {
    std::string print;
    
    // DOT for current node
    print = "n" + to_string(rootNum) + " [label=< <B>" + translateTypeStr(n->type) + "</B>";
    if (translateDataStr(n) != "")
        print += "<BR/>" + translateDataStr(n) + " >";
    else
        print += " >";
    if (isLeft)
        print += ", color=\"#FF595E\", fontcolor=\"#FF595E\"";
    else
        print += ", color=\"#274690\", fontcolor=\"#274690\"";
    
    if (n->type == ast::astType::numericConstant || n->type == ast::astType::stringConstant || n->type == ast::astType::boolConstant) {
        print += ", shape=egg";
    }
    print += "]\n";
    
    int rootNumBackup = rootNum;
    rootNum++;
    if (n->type == ast::astType::_if) {
        if (n->cond) {
            print += "n" + to_string(rootNumBackup) + "->n" + to_string(rootNum) + " [label=condition]\n";
            genDOT(n->cond);
        }
        rootNum += 1;
        if (n->_if) {
            print += "n" + to_string(rootNumBackup) + "->n" + to_string(rootNum) + " [label=if]\n";
            genDOT(n->_if);
        }
        rootNum += 1;
        if (n->_elseIf) {
            print += "n" + to_string(rootNumBackup) + "->n" + to_string(rootNum) + " [label=elseif]\n";
            genDOT(n->_elseIf);
        }
        rootNum += 1;
        if (n->_else) {
            print += "n" + to_string(rootNumBackup) + "->n" + to_string(rootNum) + " [label=else]\n";
            genDOT(n->_else);
        }
        rootNum += 1;
    } else if (n->type == ast::astType::_while) {
        if (n->cond) {
            print += "n" + to_string(rootNumBackup) + "->n" + to_string(rootNum) + " [label=condition]\n";
            genDOT(n->cond);
        }
        rootNum += 1;
        if (n->_if) {
            print += "n" + to_string(rootNumBackup) + "->n" + to_string(rootNum) + " [label=do]\n";
            genDOT(n->_if);
        }
        rootNum += 1;
    } else {
        if (n->left || n->right) {
            if (n->left) {
                print += "n" + to_string(rootNumBackup) + "->n" + to_string(rootNum) + " [color=\"#FF595E\"]\n";
                genDOT(n->left);
            } else {
                print += "n" + to_string(rootNum) + " [label=x]\n";
                print += "n" + to_string(rootNumBackup) + "->n" + to_string(rootNum) + "\n";
            }
            rootNum += 1;
            if (n->right) {
                print += "n" + to_string(rootNumBackup) + "->n" + to_string(rootNum) + " [color=\"#274690\"]\n";
                genDOT(n->right, false);
            } else {
                print += "n" + to_string(rootNum) + " [label=x]\n";
                print += "n" + to_string(rootNumBackup) + "->n" + to_string(rootNum) + "\n";
            }
        }
    }
    
    cout << print << endl;
    }

Firstly, this is not the complete code. It only covers if and while loops, but not function bodies and other blocks. 

## Results

<video controls autoplay loop muted> <source src="/assets/img/graphvizdemo1.mp4" type="video/mp4"> </video>

Funnily enough, I spent less time writing code to actually generate the graph than I spent trying to make it look cooler. But given how much time I'm going to have to stare at and navigate these graphs, I think the it was worth the effort.