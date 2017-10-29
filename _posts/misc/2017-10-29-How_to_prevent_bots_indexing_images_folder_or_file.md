---
layout: post
title: "How to prevent bots indexing images folder or file"
description: ""
category: [sysops, server]
tags: [bots]
---
{% include JB/setup %}

In robots.txt

    User-Agent:*
    Disallow:/images/
    Disallow:/image.jpg
