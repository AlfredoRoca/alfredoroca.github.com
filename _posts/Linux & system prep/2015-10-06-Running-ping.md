---
layout: post
title: "Keep pinging until host is known"
description: ""
category: [linux, monitoring]
tags: []
---
{% include JB/setup %}


    while ! ping -c1 www.google.com &>/dev/null; do :; done
