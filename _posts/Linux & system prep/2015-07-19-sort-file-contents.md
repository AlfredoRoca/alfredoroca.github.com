---
layout: post
title: "sort file contents"
description: ""
category: Linux
tags: [sort, file manipulation]
---
{% include JB/setup %}

    cp file1 copia && sort -u copia > file1 && rm copia
    sort file1 file2 | uniq > file3

-u === | uniq

