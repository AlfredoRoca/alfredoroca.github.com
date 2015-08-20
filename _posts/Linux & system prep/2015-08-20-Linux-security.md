---
layout: post
title: "Security"
description: ""
category: [linux, security]
tags: [security]
---
{% include JB/setup %}


list of open ports with information of service

    nmap -sT -O localhost

check if ports is associated with a known service

    cat /etc/services | grep PORT

network connections

    netstat -anp | grep PORT

list open files

    lsof -i | grep PORT
