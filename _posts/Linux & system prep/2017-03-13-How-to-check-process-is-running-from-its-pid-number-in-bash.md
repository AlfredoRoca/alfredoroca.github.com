---
layout: post
title: "How to check process is running from its pid number, in bash"
description: ""
category: [bash, process]
tags: []
---
{% include JB/setup %}

    #!/bin/sh

    PID=`cat /var/www/etecnic/shared/tmp/pids/http_server.pid`
    RESULT=`ps aux | grep http_server | grep $PID`

    if [ "${RESULT:-null}" = null ]; then
        echo ">>>> :( OCPP SERVER NOT RUNNING !!!"
    else
        echo ">>>> OK - OCPP SERVER RUNNING"
    fi
