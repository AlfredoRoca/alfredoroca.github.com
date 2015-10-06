---
layout: post
title: "Bootstrap - hidden columns"
description: ""
category: [bootstrap, design]
tags: []
---
{% include JB/setup %}


    class="hidden-xs hidden-sm ..."

Example (used in SharingKitchN)

    <div class="row">  
          <!-- show 1, 2 or 3 ratings depending on screen width -->
          <div class="col-xs-12 col-sm-6 col-md-4">
            <% unless @spaces_ratings.blank? || @spaces_ratings.first.nil? %>
              <%= render partial: 'rating_partial', locals: { sp_ra: @spaces_ratings.first } %>
            <% end -%>
          </div>
          <div class="hidden-xs col-sm-6 col-md-4">
            <% unless @spaces_ratings.blank? || @spaces_ratings.second.nil? %>
              <%= render partial: 'rating_partial', locals: { sp_ra: @spaces_ratings.second } %>
            <% end -%>
          </div>
          <div class="hidden-xs hidden-sm col-md-4">
            <% unless @spaces_ratings.blank? || @spaces_ratings.third.nil? %>
              <%= render partial: 'rating_partial', locals: { sp_ra: @spaces_ratings.third } %>
            <% end -%>
          </div>
    </div>
