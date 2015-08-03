---
layout: post
title: "Change characters inside a file"
description: ""
category: [Linux]
tags: [file processing, text processing]
---
{% include JB/setup %}


    $ tr '{}' '()' < inputfile > outputfile => Translate braces into parenthesis

    $ cat <file> | tr a-z A-Z  => Convert lower case to upper case

    $ echo "the geek stuff" | tr -d 't'  => Delete specified characters using -d option

    $ tr '\t' [:space:]  => changes tabs by spaces