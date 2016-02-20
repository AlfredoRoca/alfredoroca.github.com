---
layout: post
title: "How to filter registers whose has many association is empty"
description: ""
category: [rails, activerecord]
tags: []
---
{% include JB/setup %}


Config to log request parameters also

    Rails.application.configure do
      config.lograge.enabled = false
      # add time to lograge
      config.lograge.custom_options = lambda do |event|
        {:time => event.time}
        params = event.payload[:params].reject { |k| %w(controller action).include?(k) }
        { "params" => params }
      end
    end

