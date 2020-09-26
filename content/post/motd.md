---
layout:     post 
title:      "Customizing Server Welcome Message"
subtitle:   "... bcz the little details matter ..."
description: ""
date:       2020-03-21
author:     "Rola Dali"
URL: "/2020/linux_motd/index.html"
tags:
    - Linux
    - Bash
    - Home Server
    
categories: [ Tech, Linux ]
image:      ""
---

# Customizing Server Welcome Message

I recently set up a home server as a small project to keep me sane during the COVID-19 social distancing period. I have been slowly customizing it to my liking to have a fully functional server that I can host files on and to learn a thing or two about Linux Sys Admin tasks.

I wanted to customize the text that gets printed out when you first log into a server. This is what the Compute Canada log in screen looks like on the Beluga server. 

![Beluga Welcome Screen](https://raw.githubusercontent.com/rdali/Food4Thought/master/content/imgs/2020/motd_beluga.png)

After a quick Google search, it turns out that this is called the "Message of The Day" or "motd" for short and is stored in a file (/etc/motd).

So I created the text I wanted to print out: "WELCOME TO ChezHD"; *ChezHD* being the server name (HD are our family name initials).  
I had written a small python script, [PicAscii](https://github.com/rdali/PicAscii), a few years ago that takes in text and draws it in ASCII characters, so I used it to draw my text.


```
wget -O picascii.zip https://github.com/rdali/PicAscii/archive/master.zip
unzip picascii.zip
cd PicAscii-master
python ./picascii.py -s 'WELCOME TO ChezHD' -t "@" -d "#"
```
I copied the resulting text and pasted in /etc/motd on my home server.

```
nano /etc/motd
#paste text, save and close
```

This is the result when I log in now:

![ChezHD Welcome Screen](https://raw.githubusercontent.com/rdali/Food4Thought/master/content/imgs/2020/motd_chezhd.png)


**Note:** You have to be an admin or super user to be able to edit certain system files. If you are a regular user on a system, you will not be able to edit the motd file.
<br/>

