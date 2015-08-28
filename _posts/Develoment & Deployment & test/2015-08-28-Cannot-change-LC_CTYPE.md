---
layout: post
title: ""
description: ""
category: [linux, LC_CTYPE]
tags: [LC_CTYPE, capistrano, deployment]
---
{% include JB/setup %}


The message 

    warning: setlocale: LC_CTYPE: cannot change locale (UTF-8)

can be avoided adding the following line to ~/.bash_profile

    export LC_CTYPE="en_US.UTF-8"

