---
layout: post
title: "Deploying with Capistrano: warning: setlocale: LC_CTYPE: Can not change locale"
description: ""
category: [linux, capistrano, deployment]
tags: [LC_CTYPE]
---
{% include JB/setup %}


The message 

    warning: setlocale: LC_CTYPE: cannot change locale (UTF-8)

can be avoided adding the following line to ~/.bash_profile

    export LC_CTYPE="en_US.UTF-8"

