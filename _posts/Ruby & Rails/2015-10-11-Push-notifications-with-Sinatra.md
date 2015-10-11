---
layout: post
title: "Push notifications with Sinatra"
description: ""
category: [push, sinatra, notifications]
tags: []
---
{% include JB/setup %}

ruby stream.rb

For admin panel: localhost:4567/admin

The receiver: localhost:4567


stream.rb

    require 'json'
    require 'sinatra'
    set :public_folder, Proc.new { File.join(root, "public") }
    set server: 'thin'

    get '/' do
      erb :receiver, layout: :index
    end

    get '/admin' do
      erb :admin, layout: :index
    end

    connections = []
    notifications = []

    get '/connect', provides: 'text/event-stream' do
      stream :keep_open do |out|
        connections << out

        #out.callback on stream close evt. 
        out.callback {
          #delete the connection 
          connections.delete(out)
        }
      end
    end

    post '/push' do
      #Add the timestamp to the notification
      notification = params.merge( {'timestamp' => Time.now.strftime("%H:%M:%S")}).to_json
      puts params

      notifications << notification

      notifications.shift if notifications.length > 10
      connections.each { |out| out << "data: #{notification}\n\n"}
    end

public/es.js

    var push = function () {
      var es = new EventSource('/connect');
      es.onmessage = function (event) {
        var msg = $.parseJSON(event.data);
        $('#notification').html(msg.notification);
      } 
    }

    $(document).ready(push);

public/push.js

    var bind_push = function () {
      $('#send').click(function (event) {
        event.preventDefault();

        var notification = {notification: $('#notification').val()};

        $.post('/push', notification, 'json');
      });
    }

    $(document).ready(bind_push);

views/index.erb

    <html>
      <head>
        <title>HTML5 Hacks - Server Sent Events</title>
        <meta charset="utf-8" />

        <script src="https://code.jquery.com/jquery-2.1.4.min.js"></script>
        <script src="push.js" type="text/javascript"></script>
        <script src="es.js" type="text/javascript"></script>

      </head>
      <body>
        <%= yield %>
      </body>
    </html>

views/admin.erb

    <div id="wrapper">
        <input type="text" id="notification" placeholder="Enter Notification Here" /><br>
        <input type="button" id="send" value="Push" data-role="button"/>
    </div>

views/receiver.erb

    <div id="notification">
    </div>


