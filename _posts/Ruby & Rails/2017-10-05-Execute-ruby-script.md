---
layout: post
title: "How to execute a ruby script outside project root folder"
description: ""
category: [rails, ruby]
tags: [script]
---
{% include JB/setup %}

When executing any ruby script outside the project root, to avoid errors like

    Gemfile not found

or 

    .bundle folder not found add BUNDLE_GEMFILE path

Do this

    execute "BUNDLE_GEMFILE=#{current_path}/Gemfile ~/.rvm/wrappers/<ruby-version>@<gemset>/bundle exec ruby #{current_path}/path/to/script.rb
