---
layout: post
title: "Checkout only some file from origin/master"
description: ""
category: [git]
tags: []
---
{% include JB/setup %}

    git fetch
    git checkout origin/master -- path/to/file

git fetch will download all the recent changes, but it will not put it in your current checked out code (working area).

git checkout origin/master -- path/to/file will checkout the particular file from the the downloaded changes (origin/master).