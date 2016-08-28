---
layout: post
title: "Add line to text files that contains some pattern"
description: ""
category: [linux, bash]
tags: [grep]
---
{% include JB/setup %}


    grep -e "pattern" -l * | while read line; do echo $'\n' >> $line; done

