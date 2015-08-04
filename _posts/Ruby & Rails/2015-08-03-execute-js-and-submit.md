---
layout: post
title: "Execute JS and submit form"
description: ""
category: [rails, js]
tags: [js]
---
{% include JB/setup %}

    <%= f.submit onclick: "calc_space_rates_table();", class: "btn btn-primary btn-block" %>
