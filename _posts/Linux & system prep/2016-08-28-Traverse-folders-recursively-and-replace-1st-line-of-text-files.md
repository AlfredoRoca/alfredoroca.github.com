---
layout: post
title: "Traverse folders recursively and replace 1st line of text files"
description: ""
category: [linux, bash]
tags: [find, sed]
---
{% include JB/setup %}


    find . -iname '*.yml' -type f -execdir sed "1s/en:/it:/" {} -i  \;
    