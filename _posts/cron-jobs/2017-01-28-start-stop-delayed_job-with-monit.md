---
layout: post
title: "start stop delayed_job with monit"
description: ""
category: [monit,delayed_job]
tags: []
---
{% include JB/setup %}

`/etc/init.d/delayed_job`

    #! /bin/sh
    set_path="cd /var/www/shk/shared/bin"

    case "$1" in
      start)
            echo -n "Starting delayed_job: "
                    su - deployer -c "$set_path; RAILS_ENV=staging delayed_job start" >> /var/www/shk/shared/log/delayed_job.log 2>&1
            echo "done."
            ;;
      stop)
            echo -n "Stopping delayed_job "
                    su - deployer -c "$set_path; RAILS_ENV=staging delayed_job stop" >> /var/www/shk/shared/log/delayed_job.log 2>&1
            echo "done."
            ;;
          *)
                N=/etc/init.d/delayed_job
                echo "Usage: $N {start|stop}" >&2
                exit 1
                ;;
        esac

        exit 0


Make it executable

    chmod +x /etc/init.d/delayed_job


`/etc/monitrc`

    #
    #       delayed_job
    #
    check process delayed_job with pidfile /var/www/shk/shared/tmp/pids/delayed_job.pid
            start program = "/etc/init.d/delayed_job start"
            stop program = "/etc/init.d/delayed_job stop"
            if mem is greater than 300.0 MB for 1 cycles then restart
            if cpu is greater than 50% for 2 cycles then alert
            if cpu is greater than 80% for 3 cycles then restart
            group background
