---
layout: post
title: "Sublime Pluggin for ERB templates"
description: ""
category: [sublime]
tags: []
---
{% include JB/setup %}

Package: ERB Snippets

<https://packagecontrol.io/packages/ERB%20Snippets>

Snippets and Bindings

    **Snippet Tab                 Trigger     Output**
    ERB tags                    er          <% %>
    print ERB tags              pe          <%= %>
    print ERB comment           pc          <%# %>
    if block                    if          <% if %>...<% end %>
    if / else block             ife         <% if %>...<% else %>...<% end %>
    else tag                    else        <% else %>
    elsif tag                   elsif       <% elsif %>
    unless block                unless      <% unless %>...<% end %>
    end block                   end         <% end %>
    submit_tag helper           st          <%= submit_tag ..., ... %>
    text_field_tag helper       tft         <%= text_field_tag ..., ... %>
    password_field_tag helper   pft         <%= password_field_tag ..., ... %>
    label_tag helper            lblt        <%= label_tag ..., ... %>
    link_to helper              lt          <%= link_to ..., ... %>
    each helper                 each        <% @things.each do |thing| %> ... <% end %>
    form_for helper             ff          <%= form_for(@ ) do |f| %> ... <% end %>
    t() helper                  t           <%= t('@') %>

