---
layout: post
title: "How to block php requests in Nginx"
description: ""
category: [nginx, sysops]
tags: [security]
---
{% include JB/setup %}

<https://www.datachomp.com/archives/nginx-block-php-requests/>

Añadir a server

    location ~ (\.php|.aspx|.asp|myadmin) {
        return 404;
    }
