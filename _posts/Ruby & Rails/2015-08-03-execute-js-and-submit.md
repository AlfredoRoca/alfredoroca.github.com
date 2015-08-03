---
layout: post
title: "Execute JS and submit form"
description: ""
category: [Rails, JS]
tags: [js]
---
{% include JB/setup %}

    <%= f.submit onclick: "calc_space_rates_table();", class: "btn btn-primary btn-block" %>
