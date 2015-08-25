---
layout: post
title: "System logging review with journalctl"
description: ""
category: [server, system, logging, journalctl, monitoring ]
tags: []
---
{% include JB/setup %}

    journalctl _COMM=sshd -e -f
    
      -e = go to the end of log
      -f = follow

