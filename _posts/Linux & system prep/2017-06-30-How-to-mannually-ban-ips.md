---
layout: post
title: "How to manually ban the attacker ips"
description: ""
category: [fail2ban, sysops]
tags: [security]
---
{% include JB/setup %}

To retrieve which ips are trying wrong routes

Localize `FATAL` in the log file

    grep -B5 --color=always FATAL /var/www/shk/shared/log/production.log | less -R

    I, [2017-06-30T03:00:39.824964 #17720]  INFO -- : Started POST "/" for 68.81.30.180 at 2017-06-30 03:00:39 +0200
    I, [2017-06-30T03:00:39.835094 #17720]  INFO -- : Internet Explorer 11.0 (Windows, Windows 7)
    F, [2017-06-30T03:00:39.845191 #17720] FATAL -- : 

Print guilty IPs and check if it is really an attacker

    grep 'Started POST "/"' /var/www/shk/shared/log/production.log

    I, [2017-06-30T19:14:46.055273 #20700]  INFO -- : Started POST "/" for 217.248.244.157 at 2017-06-30 19:14:46 +0200
    I, [2017-06-30T19:16:46.185932 #20700]  INFO -- : Started POST "/" for 217.248.244.157 at 2017-06-30 19:16:46 +0200
    ... a lot of occurrences

To know jail name:

    fail2ban-client status

    Status
    |- Number of jail:      1
    `- Jail list:   sshd

To ban ip

    generic: fail2ban-client -vvv set JAIL banip IP

    fail2ban-client -vvv set sshd banip 217.248.244.157

To list banned ips

    iptables -L -n

    Chain f2b-sshd (1 references)
    target     prot opt source               destination         
    REJECT     all  --  217.248.244.157      0.0.0.0/0            reject-with icmp-port-unreachable
    REJECT     all  --  68.81.30.180         0.0.0.0/0            reject-with icmp-port-unreachable

To remove an IP address from the banned SSH list

    iptables -D f2b-sshd -s banned_ip -j DROP

