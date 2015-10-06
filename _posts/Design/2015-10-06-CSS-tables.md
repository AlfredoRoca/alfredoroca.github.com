---
layout: post
title: "CSS tables"
description: ""
category: [css, tables, desing]
tags: []
---
{% include JB/setup %}


HTML to have cols

    <col>  # --> column for row headers
    <% quantity.times do %>
      <col>   # --> column for data
    <% end %>

CSS select even-odd columns

    col:first-child {background: #FF0}
    col:nth-child(2n+3) {background: #CCC}

CSS select even-odd rows

    tr:nth-child(even) {background: #CCC}
    tr:nth-child(odd) {background: #FFF}