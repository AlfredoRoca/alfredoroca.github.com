---
layout: post
title: "How to untrack a folder locally in git and push to production without deleting it"
description: ""
category: [git]
tags: []
---
{% include JB/setup %}


    git update-index --assume-unchanged images/*

The only problem is that if others' change these image files and push to git server, you will still get these changes when you pull.

One other alternative to consider that might be better for new teammates is using the following in the future for adding directories that are needed, yet omitting their contents:

    **/images/*
    !**/images/readme.md

Since Git does not concern itself with empty directories, the trick is to tell Git to not track anything within the images directory. But to create the directory in the first place, we need a file, thus in the end we are saying "don't track anything in this directory except for this Read Me."

