---
layout: post
title: "Check_box_tag for collections"
description: ""
category: [rails]
tags: [check_box, form, collections]
---
{% include JB/setup %}


    <%= form_tag(url_path(@model, format: :js), multipart: true, remote: true) do |f| %>
      <%= submit_tag t(:update), class: "btn btn-primary" %> <br>
      <% @model.each do |co| %>
        <%= check_box_tag 'checked_collection[]', co.id, co.checked_value %>  <br>
      <% end %>
    <% end -%>

Example in saap

    <%= form_tag(update_allways_call_in_rest_companies_path(@emergency, format: :js), multipart: true, remote: true) do |f| %>
      <%= submit_tag t(:update), class: "btn btn-primary" %> <br>
      <% @emergency.rest_companies.each do |co| %>
        <%= co.name %> <%= check_box_tag 'allwcall[]', co.id, co.allways_call %>  <br>
      <% end %>
    <% end -%>

