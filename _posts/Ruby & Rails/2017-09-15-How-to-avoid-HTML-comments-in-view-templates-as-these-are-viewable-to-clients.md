---
layout: post
title: "Avoid HTML comments in view templates as these are viewable to clients"
description: ""
category: [rails, security]
tags: []
---
{% include JB/setup %}

Source: <https://github.com/eliotsykes/rails-security-checklist#viewshttps://github.com/eliotsykes/rails-security-checklist#viewsZ

Use server-side comments instead:

    # bad - HTML comments will be visible to users who "View Source":
    <!-- This will be sent to clients -->
    <!-- <%= link_to "Admin Site", "https://admin.example.org/login" %> -->

    # ok - ERB comments are removed by the server, and so not viewable to clients:
    <%# This will _not_ be sent to clients %>
    <%#= link_to "Admin Site", "https://admin.example.org/login" %>
