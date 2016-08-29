---
layout: post
title: "GIT list tags with dates"
description: ""
category: [git]
tags: [log]
---
{% include JB/setup %}


    git log --graph --tags --date-order --simplify-by-decoration  --decorate --oneline --pretty=format:"%h %ai %d %s" | grep tag: