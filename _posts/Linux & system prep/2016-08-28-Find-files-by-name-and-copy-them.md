---
layout: post
title: "Find files by name and copy them"
description: ""
category: [linux, bash]
tags: [find]
---
{% include JB/setup %}


    find /home/student/Downloads/ -name '*kk*' -execdir cp {} /home/student/Public/ \;

