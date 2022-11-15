---
layout: post
title: "Second Attempt LFS Part 1"
date: 2021-07-25 19:09:03 -0400 
catagories: LFS
---


Well well well, guess who’s back with a second LFS attempt after the first one flopped? That right, this sad endian. So I will be describing my process again right from the start. I will be repeating many things since this is mostly an educational endeavor, and I don’t trust myself to retain things from a year ago - so reading the previous attempt isn’t necessary. 

I’m making my machine with VMware and Lubuntu again as that set up worked well last time.



![images](/assets/2aLFSpart1/image1.png)


A note about the architecture, the build that I will be doing is a ‘pure’ 64-bit system, not a multi-lib one that supports both 32 and 64-bit systems. This is for simplification.

The book also assumes basic knowledge in unix commands and familiarity with building from source. 

I am familiar with the unix commands - but besides my previous LFS attempt, I have no experience building source code from scratch, relying entirely on package managers.

 In the book two links are given as a prereq for this topic: [Building and Installing Software packages for Linux](https://tldp.org/HOWTO/Software-Building-HOWTO.html) written by Mendel Cooper and the [Beginner’s Guide to installing from Source](http://moi.vonos.net/linux/beginners-installing-from-source/).  Written by Simon Kitching (directly inspired by the former article).  In the interest of being thorough I will be going through these resources.

In resource Building and Installing Software, we get a peek at the ancient methods of 1999.

Greatly simplified, the steps are

move the file into the working directory and unpack the file using tar xzvf filename 

Then read the configuration or README file  to see if the files need to be put in certain directories /src for an example. 

Then use some form of make to build. The command make -n can be used to preview the commands make will trigger.

Then, often wrangling around in the make file

In this resource there is a fascinating section detailing [The Problem with Prepackaged Binaries ](https://tldp.org/HOWTO/Software-Building-HOWTO-4.html)that is an interesting view into software development in 1999. The solution presented, of course, is to learn how to manually install packages rather than the current solutions we have being containers. I will leave it here for curiosity's sake.

The next resource is the Beginner’s Guide to Installing from Source, which is more recent, published in 2015. 

The first step here is to do the security check through md5sum or gpg. 

The second is to unpack the archive files using tar, same as before

Sometimes patches are necessary in the form of a sed or awk command or a patch file

Build with some form of make typically.

Sometimes environment variables need to be fandangled with or changed 


![images](/assets/2aLFSpart1/image5.png)


And then possibly install docs into their proper place. 

Now that the extremely basic refresher is written down - time to start drowning in the deep end of the pool. The partitions I have in my host machine is:



![images](/assets/2aLFSpart1/image2.png)

Around 10.24 GiB for the host and 14 GiB for my linux from scratch machine. Is this ludicrously overkill for both machines? Yes, but this is nice if I’d want to add things or accumulate notes here.  As I install each package I will write down the rationale of what the package does and why it is needed. 

Now for the version check:


![images](/assets/2aLFSpart1/image4.png)



As before there are a couple missing packages and a bad symbolic link. Doing the same as before, I installed install build-essential, gawk, texinfo, m4, bison and changed the symbolic link for bash (‘sudo ln -sf bash /bin/sh’)


![images](/assets/2aLFSpart1/image3.png)


Im taking a snapshot here, next week we will continue from here.  I’m going to try to make a real effort to have a new part out every Sunday. Thanks for reading!

I hope you found this useful, or at the very least entertaining. 

-naidneelttil

