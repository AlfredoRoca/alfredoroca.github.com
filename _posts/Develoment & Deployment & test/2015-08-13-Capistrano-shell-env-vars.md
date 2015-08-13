---
layout: post
title: "Capistrano shell environments variables"
description: ""
category: [capistrano, shell]
tags: []
---
{% include JB/setup %}

Deploy.rb

    set :default_environment, {
      :LANG => 'en_US.UTF-8'
    }

