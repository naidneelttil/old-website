---
layout: post
title: "Writeup for VirSecCTF 2020"
date:   2020-04-04 16:34:35 -0400
categories: CTF
---

Hello everyone! So, taking a slight break from my Linux From Scratch journey (I know I just started. But eeeeey, CTFS tho) to compete solo in VirSecCon CTF 2020. So, here are all the writeups for the challenges I got. 


---


## Countdown for 60 points. Category: Web 


**Details: We hear something beeping... is there something in the oven?
Connect here: http://jh2i.com:50036.
This takes you to this site, where a bomb is supposed to go off.**
  

![image](/assets/image1.png)


When you click on the link to defuse the bomb, you get redirected to detonate.php
  

![image](/assets/image3.png)


To solve this challenge, I changed the value of the detonate_time cookie from 1586040368 to a bunch of nines to delay the time:


![image](/assets/image2.png) 


And then when you try to detonate the bomb, you get the flag.
  

![image](/assets/image5.png)


---



## Hidden for 60 points. Category: Miscellaneous


**Details: What secret is this server hiding?!
Connect with:
ssh user@jh2i.com -p 50015 # password is 'userpass'**


Doing a  ls -a (listing all files including hidden ones) on the box gets:
  

![image](/assets/image4.png)


You see that .secret boys? We got ‘em. The command cd is restricted for some reason though   


![image](/assets/image7.png)


However, that’s nothing that tab completion can’t solve. We can cat that file!
  

![image](/assets/image6.png)



---



## Read the Rules for 5 points. Category : Warmup


**Please follow the rules for this CTF!
Connect here: http://ctf.virseccon.com/rules.**

This was very easy, while the page itself didn’t have the code, spelled out for you, instead, saying ‘If you look closely, you can even find a flag on this page!’
Time to look at the page source for this, and sure enough, it’s in a comment
  
![image](/assets/image9.png)



---



## Believe your Eyes for 10 points. Category: Warmup


**Details: You would not believe your eyes...
Download the file below.**

The file was called 'belive_your_eyes.rar'. while the .rar filetype makes you think that it was a compressed file, checking the type of file with properties shows that it can be open with VLC.  And behold, our flag! 
I will also admit that I kinda stumbled into this one. Windows, seemed to automatically recognize that the file extension was a lie, so when I tried to extract it, the software wouldn’t let me, except with VLC.


  
![image](/assets/image8.png)



---



## DotCom Scavenger Hunt for 25 points. Category: Warmup

**Details: It’s a website scavenger hunt!
Download the file below.**

The file downloaded was 'dotcom_scavenger_hunt.zip'. when extracted, it was a folder with all the website parts for a site called nothinginthebox.com, it essentially sells ~nothing~


![image](/assets/image12.png)
 

After finding nothing interesting in the index.html, PAY.html, or robots.txt, (or at least nothing that popped out to me) I turned to the JavaScript.


![image](/assets/image10.png)
 

The .min.js extension popped out to me as I did a problem similar to this where once putting the .min.js file in a JS beautifier (I like https://beautifier.io/)  doing a /f to find LLS, the flag format, gave me the flag. 


![image](/assets/image11.png)
 

I didn’t find it with grep, but yeah, I’d imagine that would be smoother.




---



I also got **Linux Kiosk** but couldent submit the flag because time had run out (I AM LIVID)
When man command is done it uses less pager to display the documentation. Well you can use it to your advangate and run unix commands in less. All you must do is enter this before your commands

> : ! 

A few rounds of this and I found out the flag. With

> :! Pwd; ls -a ; cat flag.txt

Beating myself up on not putting the flag in fast enough though. I’m salty, but at least you all  know I could solve it.


![image](/assets/image13.png)


That’s all the challenges I was able to solve! It’s a bit pathetic but it was a fun way to kill some time in quarantine (I really wanted to at least get the easiest binary exploit but eeeehhhhg I’m going to have to dig for more write ups). Shout out to all the organizers of VirSecCon 2020! Can’t wait to participate in more, with hopefully a larger team then me, myself, and I.

-naidneelttil
