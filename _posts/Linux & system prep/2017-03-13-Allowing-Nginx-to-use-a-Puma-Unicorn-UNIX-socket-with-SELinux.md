---
layout: post
title: "Allowing Nginx to use a Puma/Unicorn UNIX socket with SELinux"
description: ""
category: [nginx, selinux]
tags: []
---
{% include JB/setup %}

<http://nts.strzibny.name/allowing-nginx-to-use-a-pumaunicorn-unix-socket-with-selinux/>


En ` /var/www/etecnic/shared/log/nginx.error.log`

    connect() to unix:/var/www/etecnic/shared/tmp/sockets/puma.sock failed (13: Permission denied) while connecting to upstream

To check if it a SELinux issue,

    setenforcing Permissive


Solution:

    grep nginx /var/log/audit/audit.log | audit2allow -m nginx > nginx.te

    #cat nginx.te
    module nginx 1.0;

    require {
        type unconfined_t;
        type httpd_t;
        type httpd_sys_content_t;
        class sock_file write;
        class unix_stream_socket connectto;
        class capability2 block_suspend;
    }

    #============= httpd_t ==============
    allow httpd_t httpd_sys_content_t:sock_file write;
    allow httpd_t self:capability2 block_suspend;
    allow httpd_t unconfined_t:unix_stream_socket connectto;


    checkmodule -M -m -o nginx.mod nginx.te
    semodule_package -o nginx.pp -m nginx.mod
    semodule -i nginx.pp
    systemctl restart nginx
