---
layout: post
title: "Thin server configuration file"
description: ""
category: [thin, server, configuration, system]
tags: []
---
{% include JB/setup %}

#app-name.yml

  ---
  chdir: "/var/www/app/current"
  environment: production
  address: 0.0.0.0
  port: 3010
  timeout: 30
  log: "/var/www/log/app_thin.log"
  pid: "tmp/pids/thin.pid"
  rackup: config.ru
  max_conns: 1024
  max_persistent_conns: 100
  require: []
  wait: 30
  threadpool_size: 20
  daemonize: true
  tag: shk
  servers: 2
  onebyone: true
  socket: tmp/sockets/thin.sock