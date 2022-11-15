---
layout: post
title: "Second Attempt LFS Part 3"
date: 2021-08-07 19:09:03 -0400 
catagories: LFS
---


 Welcome back to another episode of this LFS adventure. In the last episode I got all the packages and patches downloaded in $LFS/sources and completed chapter 3. In this post I hope to finish chapter 4 ‘Final Preparations’ and finally get to chapter 5. 


![images](/assets/2aLFSpart3/image1.png)


First we are creating a limited directory at $LFS and an extra $LFS/tools directory so everything can eventually be installed in its proper place.

![images](/assets/2aLFSpart3/image9.png)

We are also making the underprivileged user lfs - this was one of the things that accidentally tripped me up the last time I did this. I would forget to switch to the lfs user to build packages. I’m going to be careful not to do that again. 

The lfs user will have to have just enough privileges to be able to manually build the packages, of course, so in the LFS book, it details how to do so.  

It looks like I have committed an oopsie and accidentally didn’t make $LFS echo back /mnt/lfs for the root user, and accidentally changed my usr, lib, var, etc, bin, sbin, tools, and lib64 of my host machine to lfs, which is not it chief. Didn’t notice until it was time to change the ownership of sources.


![images](/assets/2aLFSpart3/image6.png)


So now I'm rerunning the command to return these files back to root and making sure the $LFS variable is properly set in root. 


![images](/assets/2aLFSpart3/image3.png)

And now it should work. Except of course, it doesn’t.


![images](/assets/2aLFSpart3/image8.png)


It seems like that limited directory didn’t actually work out since I also used it under root and didn’t catch that the variable wasn't working then. At this point it seems like I need to revert back a snapshot to make sure I don't mess up anything more. 

luckily for me, my last snapshot was the end of chapter 3, packages and patches,  so I don't need to catch up on too much.

So now we are time traveling back. Remember kids, snapshots saves lives. Okay! Now that we are back to the end of 3.1, before we repeat the sins of the past we are going to change the /etc/bash.bashrc of root so that the $LFS variable will be recognized.


![images](/assets/2aLFSpart3/image4.png)


Now we can make the limited directory again:


![images](/assets/2aLFSpart3/image7.png)


And actually CHECK this time that it was indeed ACTUALLY created:


![images](/assets/2aLFSpart3/image2.png)


And now we can finally make the lfs user and start changing the ownership of those directories. Hallelujah. 


![images](/assets/2aLFSpart3/image5.png)


I know I’ve done comparatively little but I don’t want to do this again, so I’m taking a snapshot here.

I’m still going to make it to chapter 5 in this post though, don’t worry! The next step is 4.4 setting up the environment.  We are really just creating the startup scripts for bash for our lfs user. The book stresses that this is in the interest of having a completely clean environment to make sure any lingering configurations or variables don’t contaminate our build.

An incredibly important warning is that the book warns against having /etc/bash.bashrc for the root user at this point because it will override any particular changes we have in the currently made bashrc. This is very relevant since I specifically edited the /etc/bash.bashrc to add in the $LFS variable, so running this as root is pretty important to my build.


![images](/assets/2aLFSpart3/image10.png)


And then as the lfs user again, I just have to source the newly created .bash_profile to make it binding. 

The next section details what SBU or standard build unit. This is the time it takes to build binutils and will be the standard measurement of time that all other packages will be measured to. I remember the time for binutils not being too bad on my system the last time I attempted this, so I remain optimistic. I don’t have infinite amount of processing power to throw at this since it is all on a virtual machine, but as this project doesn’t have a due date per se, I don’t mind as much.

Test suites are provided as a sanity check -- and hopefully I won’t run into too many packages that call my sanity into question (lol). 

And with that, (besides some preliminary materials) we have reached part 3 and chapter 5 of the LFS book! I’ll take a snapshot here to save my progress and sign off for now. 

I hope you found this post useful or at the very least entertaining. 

-naidneelttil

