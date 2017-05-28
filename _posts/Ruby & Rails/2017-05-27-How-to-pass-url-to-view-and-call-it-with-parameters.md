---
layout: post
title: "How to pass url to view and call it with parameters"
description: ""
category: [rails]
tags: []
---
{% include JB/setup %}

In controller methods enter url names like for example

    @url = 'my_reservations_orders_path'
    render 'index'

or 

    @url = 'my_spaces_orders_path'
    render 'index'

or 

    @url = 'orders_path'
    render 'index'

In view 'index'

      <th><%= link_to t(:Code), method(@url).call(params.merge(order: 'by_id')) %></th>
      <th><%= link_to t(:Date), method(@url).call(params.merge(order: 'by_creation_date')) %></th>
      <th><%= link_to t(:Space), method(@url).call(params.merge(order: 'by_space')) %></th>


