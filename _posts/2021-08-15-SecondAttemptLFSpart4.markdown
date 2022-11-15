---
layout: post
title: "Second Attempt LFS Part 4"
date: 2021-08-15 19:09:03 -0400 
catagories: LFS
---

Welcome back to a new episode of installing LFS. In the last installment we reached chapter 5 of the book! (look how on top of it all the posts have been!) It is the preliminary information needed before starting building the packages in the book, so I am going to spend a bit of time off the virtual machine so I can read and absorb the information of the LFS book. In the first part of the preliminary information it suggests to use the tee utility to keep track of the output of commands - for better diagnostic.  Very good, but ah, one slight problem -- I don’t know how to use the tee utility. 

Thankfully, I live in the age of information and anything can be picked up after a quick google search. Blessed are the google gods. 

According to wikipedia, this is the format to pipe the information of a command to a .lint file:



![images](/assets/2aLFSpart4/image5.png)


AMAzing. Now back to our  regularly scheduled program.  The next section is the toolchain technician’s notes.  A big concept in this section is Cross-Compilation. It is said in this chapter that not all needs to be understood right away, but trying to is the type of admirability I aspire to -- so in layman’s terms:

Build - where programs are built

Host - where the built programs will run

Target - I assume this is the architecture that the host needs, the book says that this is only used for compilers -- however I don’t know what to make of the line  - “it may be different from  build or host” . Hopefully I will get more information about this later.

It seems that we are using what is on our build machine to build a package step by step to make sure the package eventually becomes usable for the lfs system. (I think this might only relate to the compiler? I’m not completely certain). This is the given process:


![images](/assets/2aLFSpart4/image4.png)



There is the cross-compiler and the compiler, which mean different things. I assume the cross-compiler’s sole job is to make sure that it can produce machine code in a target different from the build machine. 

I will, like the book recommends, reference this section when needed. For now, I will move on. 

The first things first -- some nice ~quality of life~ changes. I am but a simple modern linux user, and I demand that my terminal be colorful. So I’m going to find the configurations in my previous bashrc that made it colorful and add it to the bashrc of my lfs user. Why? Because I can. 

So now that my terminal looked like this:


![images](/assets/2aLFSpart4/image7.png)


Instead of this (for real can you blame me for changing it? blah):



![images](/assets/2aLFSpart4/image1.png)


I can finally start the first real task of chapter 5: the first pass of binutils. Remember that this will be the basis on which all other package build time will be compared to, so I will make sure to note the time.

Before we do anything we are going to check one more time that the $LFS variable is properly set up, and that the host system requirements check (the one we ran at the very beginning of this project) has no errors.



![images](/assets/2aLFSpart4/image3.png)



Yes,



![images](/assets/2aLFSpart4/image2.png)



And Yes.

Good, now we are also going to make sure that we follow the instructions of the general compilation instructions.


![images](/assets/2aLFSpart4/image9.png)


So of course, we tar -xvf &lt;binutils package> and cd into it and follow the instruction in 5.2. In order to automatically count the time for my SBU, I will follow the instruction to use the time command to do the first pass.

The configuration of binutils took this much time:


![images](/assets/2aLFSpart4/image8.png)


A time make command took this much time:

![images](/assets/2aLFSpart4/image6.png)


And finally time make install took this much time:


![images](/assets/2aLFSpart4/image10.png)


So compiling all this together (pun intended) our calculated SBU is 2 minutes and 2.43 seconds. A lot better than I thought I would have. 

And with that, I’ll take a snapshot here to save my progress and sign off for now. I know I’ve only built one package but it took some wrangling and this post is getting quite long. 

I hope you found this post useful or at the very least entertaining. 

-naidneelttil

