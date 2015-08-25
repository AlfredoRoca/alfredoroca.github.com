---
layout: post
title: "SSHD Logging"
description: ""
category: [linux, ssh, logging, monitoring]
tags: []
---
{% include JB/setup %}


Source: <http://linoxide.com/security/enable-sshd-logging/>

Configuration in /etc/ssh/sshd_config

    LogLevel VERBOSE

Review

    journalctl _COMM=sshd -e -f