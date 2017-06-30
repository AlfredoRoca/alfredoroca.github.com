---
layout: post
title: "How to create new rails app using rvm"
description: ""
category: [rails, rvm]
tags: []
---
{% include JB/setup %}

update rvm

    rvm get stable

list rubies

    rvm list known

install ruby 2.4

    rvm install 2.4

new application

    rvm gemset create newapp
    rvm gemset use newapp

    gem install rails --version 4.2.6

    gem install rails --pre # last one

    rails new newapp -T -d postgresql --skip-bundle
    cd newapp
    rvm --ruby-version use 2.2.0@newapp --create

edit Gemfile

    bundle

Configurar database.yml

    rake db:create

