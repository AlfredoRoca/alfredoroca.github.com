---
layout: post
title: "Server-Sent Events with Rails 4"
description: ""
category: [rails, sse]
tags: []
---
{% include JB/setup %}

Source:

- <http://www.slideshare.net/piotrkarbownik5/rails-4-server-sent-events>
- <http://dius.com.au/2014/03/21/server-sent-events-rails-4-angularjs/>
- <http://blogs.sequoiainc.com/blogs/easy-streams-with-rails-4-actioncontroller-live>

Requirements:

- Rails 4 (and a non-buffering web server (Thin, Rainbows!, Puma etc.., Apache w/Passenger))
- Some Javascript
- Users on a modern browser


development.rb

    # In the development environment your application's code is reloaded on
    # every request. This slows down response time but is perfect for development
    # since you don't have to restart the web server when you make code changes.
    config.cache_classes = true # SSE needs this true

    # Do not eager load code on boot.
    config.eager_load = true # SSE needs this true


push_notifications_controller.rb

    class PushNotificationsController < ApplicationController
      include ActionController::Live
      Mime::Type.register "text/event-stream", :stream

      def index
        respond_to do |format|
          format.html
          format.stream {
            response.headers['Content-Type'] = 'text/event-stream'
            begin
              # loop do
                response.stream.write "data: #{System.status}\n\n"
                # sleep 2.second
              # end
            rescue IOError # Raised when browser interrupts the connection
            ensure
              response.stream.close # Prevents stream from being open forever
            end
          }
        end
      end
    end


connect_to_sse.js

    var connectToSSE = function () {
      var source = new EventSource('/connect');
      source.onopen = function (event) {
        console.log("Open connection!");
      }
      source.onerror = function (event) {
        var txt;
        switch( event.target.readyState ){
            // if reconnecting
            case EventSource.CONNECTING:
                txt = 'Reconnecting...';
                break;
            // if error was fatal
            case EventSource.CLOSED:
                txt = 'Connection failed. Will not retry.';
                break;
        }
        console.log(txt);
      }
      source.onmessage = function(event) {
        console.log("Message: " + event.data);
      }
    }
    $(document).ready(connectToSSE);

routes.rb

    # 
    # HTTP streaming for push notifications
    # 
    get '/connect_to_sse' => 'push_notifications#index', as: :connect_to_sse


application.html.erb

    <%= render 'layouts/system_status' %>

layouts/_system_status.html.erb

    <%= System.check %>

system.rb

    class System < ActiveRecord::Base

      def self.columns() @columns ||= []; end
     
      def self.column(name, sql_type = nil, default = nil, null = true)
        columns << ActiveRecord::ConnectionAdapters::Column.new(name.to_s, default, sql_type.to_s, null)
      end
      
      column :status, :string

      def self.check
        if Rails.env.production?
          "OK"
        else
          # "OK" 
          "505 fake status"
        end
      end
      
      #
      # to stream to clients
      # 
      def self.status
        "data: #{self.check}"
      end
      
    end

database.yml

    pool = 20 # = thin server max threads


