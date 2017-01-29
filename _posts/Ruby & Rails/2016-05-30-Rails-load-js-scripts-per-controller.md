---
layout: post
title: "Rails load js scripts per controller"
description: ""
category: [rails]
tags: [assets]
---
{% include JB/setup %}

Each assets/javascripts/controller.js has all the 'requires' needed

    <%= javascript_include_tag "application", params[:controller] %>

