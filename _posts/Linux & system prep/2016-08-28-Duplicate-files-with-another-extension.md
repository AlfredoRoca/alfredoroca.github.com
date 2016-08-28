---
layout: post
title: "Duplicate files with another extension"
description: ""
category: [linux, bash]
tags: [find, read, cut]
---
{% include JB/setup %}


    find *.erb > list_of_files && cut -d. -f1 list_of_files | while read -r; do  cp "$REPLY.html.erb" "$REPLY.it.html.erb"; done && rm list_of_files

