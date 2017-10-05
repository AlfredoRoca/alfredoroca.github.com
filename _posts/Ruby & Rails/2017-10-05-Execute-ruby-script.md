---
layout: post
title: "How to execute a ruby script outside project root folder"
description: ""
category: [rails, ruby]
tags: [script]
---
{% include JB/setup %}

When executing any ruby script outside the project root, to avoid Gemfile or .bundle folder not found add BUNDLE_GEMFILE path

    execute "BUNDLE_GEMFILE=#{current_path}/Gemfile ~/.rvm/wrappers/ruby-2.2.3@etecnic/bundle exec ruby #{current_path}/lib/ocpps/http_server.rb ...
