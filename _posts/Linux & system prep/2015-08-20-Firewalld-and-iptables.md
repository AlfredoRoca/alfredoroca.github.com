---
layout: post
title: "Firewalld and iptables"
description: ""
category: [linux, iptables]
tags: [iptables, firewall]
---
{% include JB/setup %}


    # systemctl list-unit-files|grep firewalld
    ==> firewalld.service                           enabled

    # systemctl disable firewalld
    ==> Removed symlink /etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service.
    ==> Removed symlink /etc/systemd/system/basic.target.wants/firewalld.service.

    # systemctl enable iptables


