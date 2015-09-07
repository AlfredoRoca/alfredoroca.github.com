---
layout: post
title: "Security"
description: ""
category: [linux, security]
tags: [security, nmap, netstat, lsof]
---
{% include JB/setup %}


list of open ports with information of service

    nmap -sT -O localhost

Other

    nmap -sP 192.168.1.0/24           ==>  discovers IP addresses
    nmap 192.168.1.0/24               ==>  scan for open ports in the whole net
    nmap -O 192.168.1.50              ==>  Identify the Operating System of a host (requires root)
    nmap -sL 192.168.1.0/24           ==>  Identify Hostnames
    nmap -sS -sU -PN 192.168.1.50     ==>  TCP Syn and UDP Scan (requires root)
    nmap -T4 -F 192.168.1.50          ==>  Fast scan for open ports (100 most common)
    nmap -T4 -A 192.168.1.0/24        ==>  Agressive scan for open ports

    nmap -v ...                       ==> verbose command



check if ports is associated with a known service

    cat /etc/services | grep PORT

network connections

    netstat -anp | grep PORT

list open files

    lsof -i | grep PORT
