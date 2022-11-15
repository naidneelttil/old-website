---
layout: post
title: "Second Attempt LFS Part 2"
date: 2021-08-03 19:09:03 -0400 
catagories: LFS
---


Welcome back to the next installment of this LFS adventure. I want to get to the part of the LFS install that I haven’t gotten to yet (a little after the start of chapter 5) , but that will entail quite a bit of prep work and retracing. For now the prepwork needs to be completed. 

The partitions need to be made. I still am using the archwiki for information on fdisk. For my LFS system I’m keeping it simple and making a small boot partition, a swap partition, and the rest will be the root partition. More space would be needed if I wanted to move on to the BLFS, but frankly, that is beyond the scope of this project so in the end this is the final product. If you notice the difference between the way I set up this LFS build and the last, you will notice that I forgot to put the boot flag in my bios boot partition. Hopefully /etc/fstab will be nice to me!


![images](/assets/2aLFSpart2/image11.png)


/dev/sda2 is my swap partition 

/dev/sda3 is my root partition and will use the ext4 format

/dev/sda4 is my boot partition and will use the ext2 format

The next step is to make filesystems on these new partitions using these commands:

<code> mkswap /dev/sda2 </code>

<code> mkfs -v -t ext4 /dev/sda3 </code>

<code> mkfs -v -t ext2 /dev/sda4 </code>

The next part is setting the $LFS variable by editing the .bash_profile and /root/.bash_profile to have export LFS=/mnt/lfs

While doing this,  my host machine told me that vim, my preferred editor,  isn’t installed. I could obviously use vi but I don’t want to so vim will need to be an additional quality of life install (it’s suuuper necessary I swear).

Then we need to mount the partitions and edit /etc/fstab to make sure they stay mounted throughout the install.

While trying to mount the partitions, I seemed to have run into some misunderstandings regarding my /boot partition. I think it is unnecessary as I have a msdos MBR partition instead of a GPT partition that will require it, so I am deleting my /dev/sda4 partition and leaving the root partition unbootable for now. 


![images](/assets/2aLFSpart2/image8.png)


There is no mention of turning on a boot flag or making anything bootable  in the LFS book so I am cautiously changing my disk partitions to look like this:

![images](/assets/2aLFSpart2/image3.png)



So I’m down to a swap partition and a root partition. It is bare bones, but since I’m not planning on doing anything special afterwards to the system it will do for now. 

Since I’ve mounted all and turned on swap for my /dev/sda2 partition, all I need is to edit /etc/fstab so it automatically mounts.


![images](/assets/2aLFSpart2/image1.png)



Hopefully this will work. It's been a while since my Arch linux days where I was playing around with all these partitioning tools. Now, the next step is chapter 3 where we are downloading all the packages and patches.

The shortest and sweetest chapter, I’ve made the $LFS/sources directory and after changing around permissions, I am using wget to download all the packages to the directory.  First wget-list needs to be installed and put into the home directory and the the given command can be runned.


![images](/assets/2aLFSpart2/image2.png)



We are also doing the mu5sum hash check because we are responsible citizens. And LO and BEHOLD it was useful. One of the packages didn’t install through wget 


![images](/assets/2aLFSpart2/image10.png)



So we are going to try to install that one singular package again. I’ve edited the wget list to this one line and reran the wget command above so I can assess the problem.


![images](/assets/2aLFSpart2/image4.png)



This ended up being the output of the command. Seems that the link doesn’t work.


![images](/assets/2aLFSpart2/image6.png)



Guess I really have to do this manually huh. So, like a scrub, I’m going to actually open a web browser

![images](/assets/2aLFSpart2/image9.png)



but  - ALAS, it's the wrong version! I downloaded 2.4.1 and I actually need 2.2.10. So, with some internet sleuthing github gave me a version:

![images](/assets/2aLFSpart2/image5.png)



 And now FINALLY, the md5sum runs perfectly.


![images](/assets/2aLFSpart2/image7.png)



That was certainly an unexpected hurdle. Might have to mention to the maintainers of the project that the expat -2.2.10.tar.xz link in the wget-list doesn’t work. 

For now though, I’m going to end this post here. I hope you found this post useful or at the very least entertaining. 

-naidneelttil

