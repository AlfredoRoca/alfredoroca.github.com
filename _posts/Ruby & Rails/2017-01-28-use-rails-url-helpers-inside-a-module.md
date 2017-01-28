---
layout: post
title: "Use Rails url helpers inside a module"
description: ""
category: [rails]
tags: []
---
{% include JB/setup %}



`routes.rb`

    Rails.application.routes.draw do
      default_url_options Rails.application.config.action_mailer.default_url_options
    ...

in development, production, ... each environment config file add

`develpoment.rb`

    config.action_mailer.default_url_options = { protocol: 'https', host: 'localhost', port: 3001 }

