---
layout: post
title: "Change Postgres port on Fedora"
description: ""
category: [postgresql]
tags: []
---
{% include JB/setup %}

    vi /etc/systemd/system/postgresql.service

    .include /lib/systemd/system/postgresql.service
    [Service]
    Environment=PGPORT=5433
