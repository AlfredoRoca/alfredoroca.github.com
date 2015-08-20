---
layout: post
title: "sshd config"
description: ""
category: [ssh, linux]
tags: [ssh]
---
{% include JB/setup %}


# Config file: /etc/ssh/sshd_config

=> change Port  49152..65535
=> PermitRootLogin no
=> last line UseDNS no
=> PasswordAuthentication yes

# Tell SELinux about the change

    semanage port -a -t ssh_port_t -p tcp PORTNUMBER

# Commands

Start on boot

    systemctl enable sshd

Start now

    systemctl start sshd

Status

    systemctl status sshd