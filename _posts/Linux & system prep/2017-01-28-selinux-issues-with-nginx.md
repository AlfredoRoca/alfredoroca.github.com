---
layout: post
title: "SELinux issues with nginx"
description: ""
category: [selinux,nginx]
tags: []
---
{% include JB/setup %}

    sudo cat /var/log/audit/audit.log | grep nginx | grep denied

    =>
    type=AVC msg=audit(1472992700.903:5853): avc:  denied  { name_connect } for  pid=18318 comm="nginx" dest=3000 scontext=system_u:system_r:httpd_t:s0 tcontext=system_u:object_r:ntop_port_t:s0 tclass=tcp_socket

Solution:

    chcon -Rt httpd_sys_content_t /var/www/clubs/
    setsebool -P httpd_can_network_connect 1
