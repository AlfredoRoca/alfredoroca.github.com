---
layout: post
title: "How to manually detect and ban the attacker ips"
description: ""
category: [fail2ban, sysops, security]
tags: [security]
---
{% include JB/setup %}

To retrieve which ips are trying wrong routes

Localize `FATAL` in the log file

    grep -B2 -n --color=always FATAL /var/www/shk/shared/log/production.log | less -R

    3552-I, [2017-07-19T08:46:56.844056 #15072]  INFO -- : Started GET "/admin" for 5.3.198.247 at 2017-07-19 08:46:56 +0200
    3553-I, [2017-07-19T08:46:56.862056 #15072]  INFO -- : Firefox 34.0 (Windows, Windows Vista)
    3554:F, [2017-07-19T08:46:57.024926 #15072] FATAL -- : 
    --
    3601-I, [2017-07-19T08:48:00.081827 #15072]  INFO -- : Started GET "/administrator/" for 87.238.234.132 at 2017-07-19 08:48:00 +0200
    3602-I, [2017-07-19T08:48:00.095895 #15072]  INFO -- : Firefox 34.0 (Windows, Windows Vista)
    3603:F, [2017-07-19T08:48:00.106838 #15072] FATAL -- : 
    --
    3661-I, [2017-07-19T08:54:06.221600 #15072]  INFO -- : Started GET "/wp-admin/" for 87.238.234.132 at 2017-07-19 08:54:06 +0200
    3662-I, [2017-07-19T08:54:06.226690 #15072]  INFO -- : Firefox 34.0 (Windows, Windows Vista)
    3663:F, [2017-07-19T08:54:06.235463 #15072] FATAL -- : 

Print request IPs

    grep -E "(for [0-9]+)" /var/www/shk/shared/log/production.log | less -R

    I, [2017-07-19T08:28:13.511663 #15072]  INFO -- : Started GET "/administrator/" for 5.3.198.247 at 2017-07-19 08:28:13 +0200
    I, [2017-07-19T08:30:55.185346 #15072]  INFO -- : Started GET "/spaces/20-cafeteria-y-obrador-gracia" for 164.132.161.44 at 2017-07-19 08:30:55 +0200


Print guilty IPs and check if it is really an attacker

    grep 'Started POST "/"' /var/www/shk/shared/log/production.log

    I, [2017-06-30T19:14:46.055273 #20700]  INFO -- : Started POST "/" for 87.238.234.132 at 2017-06-30 19:14:46 +0200
    I, [2017-06-30T19:16:46.185932 #20700]  INFO -- : Started POST "/" for 87.238.234.132 at 2017-06-30 19:16:46 +0200
    ... a lot of occurrences

To know jail name:

    fail2ban-client status

    Status
    |- Number of jail:      1
    `- Jail list:   sshd

To ban ip

    generic: fail2ban-client -vvv set JAIL banip IP

    fail2ban-client -vvv set sshd banip 87.238.234.132

To list banned ips

    iptables -L -n

    Chain f2b-sshd (1 references)
    target     prot opt source               destination         
    REJECT     all  --  87.238.234.132      0.0.0.0/0            reject-with icmp-port-unreachable
    REJECT     all  --  5.3.198.247         0.0.0.0/0            reject-with icmp-port-unreachable

To remove an IP address from the banned SSH list

    iptables -D f2b-sshd -s banned_ip -j DROP

