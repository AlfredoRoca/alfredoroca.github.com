---
layout: post
title: "nmap - Network mapper"
description: ""
category: [linux, system]
tags: []
---
{% include JB/setup %}


IP Scanning with range 192.168.0.0 – 192.168.0.255

    nmap -sP 192.168.1.0/24

IP Scanning with range 192.168.0.1 – 192.168.0.254

    nmap -sP 192.168.1.1-254

Port Scanning with range port 100 – port 139

    nmap 192.168.0.3 -p100-139 

Scanning Operating system on target IP

    nmap -O 192.168.0.3
