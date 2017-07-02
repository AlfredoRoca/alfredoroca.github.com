---
layout: post
title: "Nginx redirection routes"
description: ""
category: [nginx]
tags: []
---
{% include JB/setup %}

When someone visit `http://localhost/route/abc` the server response exactly the same as `http://localhost:9000/abc`

Now I configure my Nginx like this:

Simply adding / is well documented as the way to remove the prefix listed in the location.

    location /route {
        proxy_pass  http://127.0.0.1:9000/;
    }
