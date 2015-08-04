---
layout: post
title: "Sort file contents"
description: ""
category: [linux]
tags: [sort, file_manipulation, file_combination]
---
{% include JB/setup %}

# Sort
Sorts lines alfabetically
With -u or | uniq, removes repeated lines

    cp file1 copia && sort -u copia > file1 && rm copia

    sort file1 file2 | uniq > file3


