---
layout: post
title: "Whenever gem"
description: ""
category: [linux, cronjobs]
tags: []
---
{% include JB/setup %}

<https://github.com/javan/whenever>

Add to gemfile
    gem 'whenever'

    bundle install
    wheneverize .
  
Edit /config/schedule.rb
  
Write it on crontab
    whenever --update-crontab my_awesome_app

To edit crontab
    crontab -e

Update crontab
    bundle exec whenever -i

Overwrite the whole crontab (be careful with this one!)
    bundle exec whenever -w
    current/bin/whenever -w
