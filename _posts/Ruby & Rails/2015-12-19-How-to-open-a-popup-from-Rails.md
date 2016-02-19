---
layout: post
title: "How to open a popup from Rails"
description: ""
category: [rails]
tags: [popup]
---
{% include JB/setup %}

In the view where the popup is wanted

    <%= render 'popup_con_mensaje' %>


_popup_con_mensaje.html.erb

    <!-- Modal -->
    <div class="modal" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel">
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
            <h4 class="modal-title" id="myModalLabel"><%= t(:Modal_title) %></h4>
          </div>
          <div class="modal-body">
            <h4><%= t(:Modal_message) %></h4>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-primary" data-dismiss="modal"><%= t(:Close_modal) %></button>
          </div>
        </div>
      </div>
    </div>


show_popup.js.erb

    $('#myModal').modal('show')

In controller action

    render :show_popup

In the view

    <%= link_to ...., onclick: "$('#myModal').modal('show');" ...


In bootstrap-sprockets.js

    //= require ./bootstrap/modal

More information at <http://getbootstrap.com/javascript/#modals>
