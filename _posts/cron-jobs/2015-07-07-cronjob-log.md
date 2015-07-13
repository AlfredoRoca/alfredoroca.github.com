---
layout: post
title: "cronjob log"
description: ""
category: [linux, cronjobs]
tags: []
---
{% include JB/setup %}

###### Cron log file ######
log file: /var/log/cron

  systemctl status crond.service -l
  journalctl -u crond