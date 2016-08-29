---
layout: post
title: "How to execute script/command at boot time"
description: ""
category: [linux, system]
tags: [security, limits]
---
{% include JB/setup %}


## systemd.service tutorial

Source: <http://unix.stackexchange.com/a/47715>

Create `/etc/systemd/system/my_service.service` (copy structure from existing file)

    [Unit]
    description=Mi servicio

    [Service]
    Type=oneshot
    ExecStart=/bin/bash -c "bla bla bla"

    [Install]
    WantedBy=multi-user.target



Enable new service 

    systemctl enable my_service

To execute bash command directly: 

    /bin/bash -c "<bash comand>"

