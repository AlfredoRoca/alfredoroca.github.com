---
layout: post
title: "sudo: no tty present and no askpass program specified"
description: ""
category: [capistrano, deployment, shell]
tags: [visudo, sudoers, deployment, shell]
---
{% include JB/setup %}

If deploying with Capistrano and get this error on some command:

    sudo: no tty present and no askpass program specified

Solution:

Modify sudoer file and add NOPASSWD for that command:

    visudo -f /eetc/sudoers.d/someuser

    someuser ALL=(ALL) NOPASSWD:/somecommand

