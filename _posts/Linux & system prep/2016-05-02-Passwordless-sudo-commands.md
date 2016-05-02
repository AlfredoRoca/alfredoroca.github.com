---
layout: post
title: "Passwordless sudo commands"
description: ""
category: []
tags: []
---
{% include JB/setup %}


Edit sudoers file

    #visudo

    alfredo ALL = (root) NOPASSWD: /bin/cp *.yml /etc/thin
