---
layout: post
title: "Check if it's a login shell"
description: ""
category: [linux, fedora]
tags: [bash]
---
{% include JB/setup %}

    shopt -q login_shell && echo 'Login shell' || echo 'No login shell'