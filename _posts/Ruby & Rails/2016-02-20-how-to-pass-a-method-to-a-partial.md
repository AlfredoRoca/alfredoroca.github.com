---
layout: post
title: "How to pass a method to a partial"
description: ""
category: [rails]
tags: []
---
{% include JB/setup %}


Source: <http://ruby-doc.org/core-2.2.2/Object.html#method-i-method>

In the view:

        <%= render partial: 'partial_name, locals: { url: method(:method_name) } %>

In the partial

      <th><%= link_to t(:Code), url.call() %></th>


