---
layout: post
title: "Disable turbolinks in specific links"
description: ""
category: [turbolinks]
tags: []
---
{% include JB/setup %}

With turbolinks (2.5.3), añadir `:"data-no-turbolink" => true` al link

Ej

    <%= link_to t(:Locutions), locutions_path, :"data-no-turbolink" => true %>

