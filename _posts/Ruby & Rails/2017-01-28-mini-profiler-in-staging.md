---
layout: post
title: "Mini profiler in staging"
description: ""
category: [mini-profiler]
tags: []
---
{% include JB/setup %}

`gemfile`

    gem 'rack-mini-profiler', require: false


`config/initializers/rack_profiler.rb`

    if Rails.env.development? || Rails.env.staging?
      require 'rack-mini-profiler'

      # Initialization is skipped so trigger it
      Rack::MiniProfilerRails.initialize!(Rails.application)

      # Needed for staging env
      Rack::MiniProfiler.config.pre_authorize_cb = lambda { |env| true }
      Rack::MiniProfiler.config.authorization_mode = :allowall
    end
