---
layout: post
title: "Filter files by date with bash"
description: ""
category: [bash]
tags: [find, filter]
---
{% include JB/setup %}




Files older than 1/1/2016:

    find . ! -newermt 2016-01-01 -type f

To check file timestamp:

    ls -alc $(find . ! -newermt 2016-01-01 -type f)

To delete them

    find ...... -delete
