---
layout: post
title: ""
description: "Security"
category: [linux, security]
tags: []
---
{% include JB/setup %}


list of open ports with information of service

    nmap -sT -O localhost

check if ports is associated with a known service

    cat /etc/services | grep PORT


    netstat -anp | grep PORT

    lsof -i | grep PORT

