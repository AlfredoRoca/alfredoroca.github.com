---
layout: post
title: "Postgres service"
description: ""
category: [postgresql]
tags: [service]
---
{% include JB/setup %}

start

    sudo systemctl start postgresql-9.4.service

enable

    sudo systemctl enable postgresql-9.4.service
