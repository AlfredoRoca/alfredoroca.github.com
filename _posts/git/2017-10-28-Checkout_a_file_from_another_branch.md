---
layout: post
title: "Checkout a file from another branch"
description: ""
category: [git]
tags: []
---
{% include JB/setup %}

In a branch, checkout file from master branch:

    git checkout master -- <file>
    git reset HEAD <file>
    git commit -m "blabla"

