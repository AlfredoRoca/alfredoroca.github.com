---
layout: post
title: "Find ports used by tcp for services imap3 and imaps"
description: ""
category: [linux, bash]
tags: [grep, cut]
---
{% include JB/setup %}


    cat /etc/services | grep imap[3s] | grep tcp | cut -f1 -d '/' | cut -f12 -d ' '
