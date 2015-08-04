---
layout: post
title: "Mark some photos with a boolean field to be included in a carrousel"
description: ""
category: [rails]
tags: []
---
{% include JB/setup %}

In the form, a collection of photos with the boolean field 'for_carrousel' in a checkbox

    <%= form_tag update_photos_for_carrousel_path, method: :post do -%>
      
      <%= submit_tag t(:Update), class: "btn btn-primary btn-block" %>

      <% @spacephotos.each do |pair| %>
        <p><%= pair[:space].title %></p>
        <div class="photo_tile_wrapper">
          <% pair[:photos].each do |photo| %>
            <div class="photo_tile">
              <%= image_tag photo.photo_url(:thumb175).to_s %> <br>
              <label>
                <%= check_box_tag "for_carrousel[#{photo.id}]", nil, photo.for_carrousel %>
                <%= t(:For_carrousel) %>
              </label>
            </div>
          <% end %>
        </div>
      <% end %>

    <% end -%>

The controller receives a hash with the checked boxes like

    for_carrousel = {"72"=>"on", "51"=>"on", "52"=>"on", "78"=>"on"}

In the controller, editing @space:

    if params[:for_carrousel]
      @space.spacephotos.update_all(for_carrousel: false)}
      checked = params[:for_carrousel].map{|ph,x| ph.to_i}
      @space.spacephotos.where(id: checked).update_all(for_carrousel: true)
    end

Updating all spaces at once:

    Spacephoto.update_all(for_carrousel: false)
    checked = params[:for_carrousel].map{|ph,x| ph.to_i}
    Spacephoto.where(id: checked).update_all(for_carrousel: true)