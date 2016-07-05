---
layout: post
title: "How to solve RVM ERROR GEM_PATH NOT SET"
description: ""
category: [rails, rvm]
tags: []
---
{% include JB/setup %}


Source: <http://unix.stackexchange.com/a/224974>

    rvm list

    => ruby-2.2.0


.bashrc

    export GEM_HOME=/home/deployer/.rvm/gems/ruby-2.2.0
    export GEM_PATH=/home/deployer/.rvm/gems/ruby-2.2.0:/home/deployer/.rvm/gems/ruby-2.2.0@global

    export RAILS_ENV=production
    export RAKE_ENV=production
