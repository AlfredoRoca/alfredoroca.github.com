---
layout: post
title: "Conditionally add css class"
description: ""
category: [ruby, rails, css]
tags: []
---
{% include JB/setup %}

Solution: use div_for rails form helper

    <%= div_for @person, class: (@success ? 'good' : 'bad') do %> 
    ...
    <% end %>
    => <div id="person_47" class="person good">

Solution 2: code a Ruby value

    <% klass = value ? "klass_1" : "klass_2" %>
    <div class=<%= klass %>>...</div> 

OR any HTML tag