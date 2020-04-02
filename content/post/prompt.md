---
layout:     post 
title:      "Customizing your Prompt"
subtitle:   "... because little things matter..."
description: ""
date:       2020-03-20
author:     "Rola Dali"
URL: "/2020/linux_prompt/index.html"
tags:
    - Linux
    - Bash
    - prompt
    - Home Server
    
categories: [ Tech, Linux ]
image:      ""
---

# Customizing Your Prompt

I recently set up a home server as a small project to keep me sane during the COVID-19 social distancing period. I have been slowly customizing it to my liking to have a fully functional server that I can host files on and to learn a thing or two about Linux Sys Admin tasks.

One of the first things I do on any new server is to customize my prompt. Having a familiar prompt with the colors I like usually puts me in a good mood and makes things feel familiar across all the servers I use. It gives a new server a more "homey" feel.

The prompt format is controlled by a variable PS1. By changing the value of PS1 (for "Prompt String 1"), you can change your prompt format and color. Here are some values that might be helpful:

Selected values used in Shell prompt:

| Code | Value                                        |
|------|----------------------------------------------|
| \d   | Current Date                                 |
| \t   | Current Time                                 |
| \h   | Host Name                                    |
| \u   | User                                         |
| \W   | Working Directory                            |
| \\[   | Start of non-printed characters, like colors |
| \\]   | End of non-printed characters                |

Selected colors used in Shell prompt:

| Code       | Color        |
|------------|--------------|
| \033[0;30m | Black        |
| \033[0;31m | Red          |
| \033[0;32m | Green        |
| \033[0;33m | Brown        |
| \033[0;34m | Blue         |
| \033[0;35m | Purple       |
| \033[0;36m | Cyan         |
| \033[0;37m | Light Gray   |
| \033[1;30m | Dark Gray    |
| \033[1;31m | Light Red    |
| \033[1;32m | Light Green  |
| \033[1;33m | Yellow       |
| \033[1;34m | Light Blue   |
| \033[1;35m | Light Purple |
| \033[1;36m | Light Cyan   |
| \033[1;37m | White        |


I usually like to know the user I am under (\u), the server I am using (\h) and the folder I am in (\W). So my $PS1 looks like:

`export PS1=\[\033[0;36m\]\u\[\033[1;37m\]@\[\033[0;32m\]\h:\[\033[1;33m\]\W\[\033[1;37m\]$`


Here is the breakdown:

![PS1](https://raw.githubusercontent.com/rdali/Food4Thought/master/content/imgs/2020/prompt_details.png)

To edit yours, you can customize your PS1 string and then save your edited PS1 command in your .bashrc file. As an example:

```
nano ~/.bashrc

## paste your PS1
export PS1=\[\033[0;36m\]\u\[\033[1;37m\]@\[\033[0;32m\]\h:\[\033[1;33m\]\W\[\033[1;37m\]$

## Save and exit. You will need to source bashrc or open a new terminal to see the changes.
```

Here is what mine looks like:

![PS1](https://raw.githubusercontent.com/rdali/Food4Thought/master/content/imgs/2020/prompt.png)


<br/>

