---
layout: post
title: "How to check if a process is running in Ruby"
description: ""
category: [Ruby]
tags: []
---
{% include JB/setup %}

    running = !(Process.getpgid(pid) rescue nil).nil?

Example:


    pid_file = "#{shared_dir}/tmp/pids/http_proxy_server.pid"
    if File.exist?(pid_file)
        pid = IO.readlines(pid_file).first.chomp
        running = !(Process.getpgid(pid) rescue nil).nil?
        log_message = running ? "Iniciando proceso #{pid}\nEscuchando en puerto #{port}..." : "Process #{pid} not running"
    else
        log_message = "pid file for http_proxy_server not found"
    end
    puts log_message

