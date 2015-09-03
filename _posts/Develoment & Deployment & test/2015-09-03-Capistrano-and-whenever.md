---
layout: post
title: "Capistrano & whenever"
description: ""
category: [capistrano, whenever, deployment]
tags: [cronjobs]
---
{% include JB/setup %}

Respect order, see Capistrano vars <http://theadmin.org/articles/capistrano-variables/>

production.rb

    server 'saap', user: 'alfredo', roles: %w{web app db}, primary: true

    set :deploy_to, '/home/alfredo/rails_apps/saap/'

    set :whenever_command, lambda { "cd #{release_path} && sudo /opt/rubies/ruby-2.2.0/lib/ruby/gems/2.2.0/gems/bundler-1.10.6/bin/bundle exec whenever -i -u alfredo" }
    set :whenever_identifier, 'saap'


Full paths for logging files

schedule.rb

    set :output, { error: "/home/alfredo/rails_apps/saap/current/log/cron_error.log", standard: "/home/alfredo/rails_apps/saap/current/log/cron.log" }
