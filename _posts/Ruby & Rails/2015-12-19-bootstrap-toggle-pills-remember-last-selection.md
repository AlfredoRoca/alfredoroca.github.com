---
layout: post
title: "Remember selected tab using bootstrap toogle pills in rails and localstorage"
description: ""
category: [rails, bootstrap]
tags: []
---
{% include JB/setup %}


remember-toggle-pills.js

    var remember = function () {
      $('a[data-toggle="pill"]').on('shown.bs.tab', function (e) {
        // save the latest tab; use cookies if you like 'em better:
        localStorage.setItem('lastTab', $(this).attr('href'));
      });
      // go to the latest tab, if it exists:
      var lastTab = localStorage.getItem('lastTab');
      if (lastTab) {
          $('[href="' + lastTab + '"]').tab('show');
      }
    }

    $(document).ready(remember);
    $(document).on('page:load', remember);

index.html.erb

    <% content_for :js do %>
      <%= javascript_include_tag 'remember-toggle-pill.js', 'data-turbolinks-track' => true %>
    <% end -%>

    <div class="col-md-2 col-sm-2">
      <nav>
        <ul class="nav nav-pills nav-stacked" id="myTabCollection">
          <li><%= link_to t(:My_services), my_makers_path , class: "btn-primary btn-block link-as-button" if policy(Maker).my_makers? %></li>
          <li class="nav-divider"></li>
          <li class="active"><%= link_to t(:Closed_orders), "#tab1", data: { toggle: "pill" },:class => 'beige' %></li>
          <li><%= link_to t(:In_progress_orders),           "#tab2", data: { toggle: "pill" },:class => 'beige' %></li>
          <li><%= link_to t(:Delivered_orders),             "#tab3", data: { toggle: "pill" },:class => 'beige' %></li>
        </ul>
      </nav>
    </div>

    <div class="col-md-10 col-md-offset-0 col-sm-10 col-sm-offset-0 beige beige_border">
      <div class="spacer"></div>
      <div class="tab-content">
        <div id="tab1" class="tab-pane tab_overflow active">
          <%= render partial: 'orders_list_partial', locals: { orders: @closed_orders, paginate: @paginate, iamkeeper: @iamkeeper } %>
        </div>
        <div id="tab2" class="tab-pane tab_overflow">
          <%= render partial: 'orders_list_partial', locals: { orders: @in_progress_orders, paginate: @paginate, iamkeeper: @iamkeeper } %>
          <p><%= link_to t(:Destroy_all_empty_in_progress_orders), destroy_all_empty_in_progress_carts_path, data: { confirm: t(:Are_you_sure) }, class: "btn btn-info" %></p>
        </div>
        <div id="tab3" class="tab-pane tab_overflow">
          <%= render partial: 'orders_list_partial', locals: { orders: @delivered_orders, paginate: @paginate, iamkeeper: @iamkeeper } %>
        </div>
      </div>
    </div>




