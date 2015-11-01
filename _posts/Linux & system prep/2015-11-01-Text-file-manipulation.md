---
layout: post
title: "Text files manipulation in Linu"
description: ""
category: [linux]
tags: []
---
{% include JB/setup %}


Redirect the output using > (replace) or >> (append)

##cat:
The cat command is short for catenate, and displays the contents of a file on screen.
Usage: cat filename.txt

##tail:
The tail command displays the last 10 lines of a file on screen. Press “q” to exit.
Usage: tail filename.txt

##head:
The head command displays the first 10 lines of a file on screen. Press “q” to exit.
Usage: head filename.txt

##echo:
The echo command repeats any text that comes after it back to the screen.
Usage: echo hello world

##paste:
The paste command puts the lines from two files together, side by side (by default) or
serially.
Usage: paste file1.txt file2.txt

##sort:
The sort command sorts the contents of a file, alphabetically by default.
Usage: sort file1.txt

##sed:
The sed command is used to search for and replace characters.
Usage: sed ‘s/term/replacement/flag’ file where “term” is the character(s) you are replacing,
and “replacement” is the character(s) you are replacing it with. If no flag is given, the first
instance of “term” is replaced, if the “g” flag is given all instances are replaced.