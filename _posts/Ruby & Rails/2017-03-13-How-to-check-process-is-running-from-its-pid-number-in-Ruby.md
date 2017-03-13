---
layout: post
title: "How to check process is running from its pid number, in Ruby"
description: ""
category: [ruby, process]
tags: []
---
{% include JB/setup %}

    #check_ocpps_server_status.rb
    PID = %x{ cat tmp/pids/http_server.pid }
    # => 19006
    result = %x{ ps aux | grep http_server | grep #{PID} }
    # =>
    # alfredo  19006  2.7  1.1 267096 45088 pts/8    Sl   13:08   0:00 ruby lib/ocpps/http_server.rb
    # alfredo  19060  0.0  0.0 113544  2948 pts/8    S+   13:08   0:00 sh -c  ps aux | grep http_server | grep 19006
    running = false
    result.split("\n").each{|line| running = true if /http_server.rb/=~line}
    puts running ? ">>>> :-) OK - OCPP SERVER RUNNING" : ">>>> :( OCPP SERVER NOT RUNNING !!!"

    Note: used in Etecnic webapp