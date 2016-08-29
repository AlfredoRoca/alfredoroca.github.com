---
layout: post
title: "Recursively travers folders and change file name"
description: ""
category: [windows]
tags: [traverse]
---
{% include JB/setup %}

    forfiles /S /M "en.yml" /C "cmd /c ren * it.yml"

