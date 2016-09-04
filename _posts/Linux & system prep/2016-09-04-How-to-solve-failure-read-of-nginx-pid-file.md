---
layout: post
title: "How to solve 'Failed to read PID from file /run/nginx.pid: Invalid argument' error in Nginx"
description: ""
category: [nginx]
tags: []
---
{% include JB/setup %}


The issue: Failed to read PID from file /run/nginx.pid: Invalid argument

    [root@vps311327 ~]# systemctl status nginx
    ● nginx.service - The nginx HTTP and reverse proxy server
       Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; vendor preset: disabled)
       Active: active (running) since Sun 2016-09-04 12:01:22 CEST; 4min 14s ago
      Process: 12055 ExecReload=/bin/kill -s HUP $MAINPID (code=exited, status=0/SUCCESS)
      Process: 12033 ExecStart=/usr/sbin/nginx (code=exited, status=0/SUCCESS)
      Process: 12030 ExecStartPre=/usr/sbin/nginx -t (code=exited, status=0/SUCCESS)
      Process: 12029 ExecStartPre=/usr/bin/rm -f /run/nginx.pid (code=exited, status=0/SUCCESS)
     Main PID: 12036 (nginx)
       CGroup: /system.slice/nginx.service
               ├─12036 nginx: master process /usr/sbin/nginx
               └─12057 nginx: worker process

    Sep 04 12:01:22 vps311327.ovh.net systemd[1]: Starting The nginx HTTP and reverse proxy server...
    Sep 04 12:01:22 vps311327.ovh.net nginx[12030]: nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
    Sep 04 12:01:22 vps311327.ovh.net nginx[12030]: nginx: configuration file /etc/nginx/nginx.conf test is successful
    Sep 04 12:01:22 vps311327.ovh.net systemd[1]: Failed to read PID from file /run/nginx.pid: Invalid argument
    Sep 04 12:01:22 vps311327.ovh.net systemd[1]: Started The nginx HTTP and reverse proxy server.
    Sep 04 12:05:33 vps311327.ovh.net systemd[1]: Reloaded The nginx HTTP and reverse proxy server.


Workaround:

It seems to be a race between systemd and nginx. As if systemd was expecting the PID file to be populated before nginx had the time to create it.

    mkdir /etc/systemd/system/nginx.service.d
    printf "[Service]\nExecStartPost=/bin/sleep 0.1\n" > /etc/systemd/system/nginx.service.d/override.conf
    systemctl daemon-reload
    systemctl restart nginx

    [root@vps311327 ~]# systemctl status nginx
    ● nginx.service - The nginx HTTP and reverse proxy server
       Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; vendor preset: disabled)
      Drop-In: /etc/systemd/system/nginx.service.d
               └─override.conf
       Active: active (running) since Sun 2016-09-04 12:15:40 CEST; 5s ago
      Process: 12119 ExecStartPost=/bin/sleep 0.1 (code=exited, status=0/SUCCESS)
      Process: 12115 ExecStart=/usr/sbin/nginx (code=exited, status=0/SUCCESS)
      Process: 12113 ExecStartPre=/usr/sbin/nginx -t (code=exited, status=0/SUCCESS)
      Process: 12109 ExecStartPre=/usr/bin/rm -f /run/nginx.pid (code=exited, status=0/SUCCESS)
     Main PID: 12118 (nginx)
       CGroup: /system.slice/nginx.service
               ├─12118 nginx: master process /usr/sbin/nginx
               └─12120 nginx: worker process

    Sep 04 12:15:40 vps311327.ovh.net systemd[1]: Starting The nginx HTTP and reverse proxy server...
    Sep 04 12:15:40 vps311327.ovh.net nginx[12113]: nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
    Sep 04 12:15:40 vps311327.ovh.net nginx[12113]: nginx: configuration file /etc/nginx/nginx.conf test is successful
    Sep 04 12:15:40 vps311327.ovh.net systemd[1]: Started The nginx HTTP and reverse proxy server.


    [root@vps311327 ~]# cat /etc/systemd/system/nginx.service.d/override.conf 
    [Service]
    ExecStartPost=/bin/sleep 0.1
