---
layout: post
title: "Multiple has_many associations beetween same tables"
description: ""
category: [rails, active_record, associations]
tags: []
---
{% include JB/setup %}

This is an industrial site where a [pipe rack](https://en.wikipedia.org/wiki/Pipe_rack) runs through several kilometres. 
This rack, as usual, has several bents, in this case, they call loops (even though they are not loops!)
All the site is divided into areas. 
Each area can have several loops.
Each loop can have several pipes.
Not necessarily all the pipes that belong to an area pass through a loop.

My models are (simplified):

    # models/loop.rb
    class Loop < ActiveRecord::Base
      belongs_to :area
      has_many :pipes
    end

    # models/area.rb
    class Area < ActiveRecord::Base
      has_and_belongs_to_many :pipes
      has_many :loops
      has_many :looppipes, through: :loops, source: :pipes
    end

    # models/pipe.rb
    class Pipe < ActiveRecord::Base
      belongs_to :loop
      has_and_belongs_to_many :areas
    end

The line ```has_and_belongs_to_many :pipes``` gives the association for those pipes that have no loop associated.

To get the ```pipes``` that don't pass through any ```loop``` of certain ```area```, that is, pipes directly assigned, we can write 

    area.pipes

The line ```has_many :looppipes, through: :loops, source: :pipes``` in the area model gives the association area-pipe for those pipes that pass through a loop.

To get the ```pipes``` that go through any ```loop``` of certain ```area```, we can write 

    area.looppipes

To join both lists we can write

    area.pipes + area.looppipes

When the loop information is needed:

    area.looppipes.includes(:loop)
    area.looppipes.includes(:loop).first.loop.name

    area.pipes.includes(:loop)

In the views

area/show.html.erb

    <%= render partial: 'area_pipes', locals: { area: @area, pipes: @area.pipe, with_loop: false, listing_title: t(:Listing_pipes_without_loop) } unless @area.pipes.empty? %>

    <%= render partial: 'area_pipes', locals: { area: @area, pipes: @area.looppipes.includes(:loop), with_loop: true, listing_title: t(:Listing_pipes_through_loop)  } unless @area.looppipes.empty? %>

area/_area_pipes.html.erb

    <h3><%= listing_title %></h3>

    <table class="table table-striped">
      <thead>
        <tr>
          <th><%= t :Name %></th>
        <% if with_loop %>  <th><%= t :Loop %></th> <% end -%>
          <th class="centered"><%= t :Areas %></th>
          <th colspan="1"></th>
        </tr>
      </thead>

      <tbody>
        <% pipes.each do |pipe| %>
          <tr>
            <td><%= pipe.name %></td>
           <% if with_loop %> <td><%= pipe.loop.name %></td> <% end -%>
            <td class="centered"><%= pipe.areas.count %></td>
            <td><%= link_to t(:show_pipe_info), pipe if policy(Pipe).show? %></td>
            <td><%= link_to t(:Remove_pipe), area_remove_pipe_path(area, pipe), method: :delete, data: { confirm: t(:Are_you_sure) } if policy(Area).remove_pipe? %></td>
          </tr>
        <% end %>
      </tbody>
    </table>

