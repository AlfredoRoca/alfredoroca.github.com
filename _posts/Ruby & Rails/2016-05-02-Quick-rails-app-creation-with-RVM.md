---
layout: post
title: "How to create new rails app using rvm"
description: ""
category: [rails, rvm]
tags: []
---
{% include JB/setup %}

    rvm gemset create newapp
    rvm gemset use newapp
    gem install rails --version 4.2.6
    rails new newapp -T -d postgresql --skip-bundle
    cd newapp
    rvm --ruby-version use 2.2.0@newapp --create

edit Gemfile

    bundle


