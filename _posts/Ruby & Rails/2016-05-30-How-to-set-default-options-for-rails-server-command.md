---
layout: post
title: "How to set defaults options for rails server command"
description: ""
category: [rails]
tags: [server]
---
{% include JB/setup %}

    #boot.rb
    require 'rails/commands/server'
    module Rails
      class Server
        def default_options
          super.merge(Host: '0.0.0.0', Port: 3001)
        end
      end
    end

`Rails s` will do the same as in `rails s -b 0.0.0.0 -p 3001`