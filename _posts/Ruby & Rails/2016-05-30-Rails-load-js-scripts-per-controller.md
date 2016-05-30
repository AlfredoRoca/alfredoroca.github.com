---
layout: post
title: "Rails load js scripts per controller"
description: ""
category: [Rails, scripts]
tags: []
---
{% include JB/setup %}

Each assets/javascripts/controller.js has all the 'requires' needed

    <%= javascript_include_tag "application", params[:controller] %>

