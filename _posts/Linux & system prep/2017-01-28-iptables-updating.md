---
layout: post
title: "IPTABLES updating"
description: ""
category: [iptables,linux,security]
tags: []
---
{% include JB/setup %}


https://www.digitalocean.com/community/tutorials/how-to-set-up-a-basic-iptables-firewall-on-centos-6


    iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
    iptables -A -p icmp -j ACCEPT
    iptables -A INPUT -p icmp -j ACCEPT
    iptables -A INPUT -i lo -j ACCEPT
    iptables -A INPUT -p tcp -m state --state NEW -m tcp --dport 80 -j ACCEPT
    iptables -A INPUT -p tcp -m state --state NEW -m tcp --dport 443 -j ACCEPT
    iptables -A INPUT -p tcp -m state --state NEW -m tcp --dport 21999 -j ACCEPT
    iptables -L
    iptables -A INPUT -j REJECT --reject-with icmp-host-prohibited
    iptables -A FORWARD -j REJECT --reject-with icmp-host-prohibited
    iptables -I INPUT 1 -p tcp --tcp-flags ALL NONE -j DROP
    iptables -I INPUT 2 -p tcp ! --syn -m state --state NEW -j DROP
    iptables -I INPUT 3 -p tcp --tcp-flags ALL ALL -j DROP
    iptables -P OUTPUT ACCEPT
    iptables -P INPUT DROP




