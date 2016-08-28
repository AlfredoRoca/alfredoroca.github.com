---
layout: post
title: "Useful networking commands"
description: ""
category: [linux, bash]
tags: [find, read, cut]
---
{% include JB/setup %}


    ip addr show | grep inet

    hostnamectl

    hostname

    ip link show

    ip route show

    systemctl list-unit-files | grep firewall/iptables

    iptables -L -v

    lsmod | grep iptab

    firewall-cmd
