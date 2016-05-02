---
layout: post
title: "Config to log request parameters"
description: ""
category: [rails, activerecord]
tags: []
---
{% include JB/setup %}


Config to log request parameters

    Rails.application.configure do
      config.lograge.enabled = false
      # add time to lograge
      config.lograge.custom_options = lambda do |event|
        {:time => event.time}
        params = event.payload[:params].reject { |k| %w(controller action).include?(k) }
        { "params" => params }
      end
    end

