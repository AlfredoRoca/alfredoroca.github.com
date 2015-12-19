---
layout: post
title: "Monitoring delayed jobs with monit"
description: ""
category: [monit, delayed_jobs]
tags: []
---
{% include JB/setup %}

    vi /etc/monitrc

    #
    #       delayed_job
    #
    check process shk_delayed_job
            with pidfile /var/www/shk/shared/tmp/pids/delayed_job.pid
            start program = "/bin/su - deployer -c '/var/www/shk/current/bin/delayed_job start'"
            stop program = "/bin/su - deployer -c '/var/www/shk/current/bin/delayed_job stop'"
            if 2 restarts within 2 cycles then timeout
