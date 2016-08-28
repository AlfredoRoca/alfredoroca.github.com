---
layout: post
title: "Get and set default target"
description: ""
category: [linux, system]
tags: [target]
---
{% include JB/setup %}


    systemctl get-default
    systemctl set-default multi-user.target
    systemctl set-default graphical.target
