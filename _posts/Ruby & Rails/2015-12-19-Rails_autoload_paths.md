---
layout: post
title: "Rails autoload paths"
description: ""
category: []
tags: []
---
{% include JB/setup %}

    $ rails runner 'pp ActiveSupport::Dependencies.autoload_paths'
    =>
    ["/home/alfredo/rails_apps/shk/app/assets",
     "/home/alfredo/rails_apps/shk/app/controllers",
     "/home/alfredo/rails_apps/shk/app/helpers",
     "/home/alfredo/rails_apps/shk/app/mailers",
     "/home/alfredo/rails_apps/shk/app/models",
     "/home/alfredo/rails_apps/shk/app/policies",
     "/home/alfredo/rails_apps/shk/app/uploaders",
     "/home/alfredo/rails_apps/shk/app/controllers/concerns",
     "/home/alfredo/rails_apps/shk/app/models/concerns",
     "/home/alfredo/.rvm/gems/ruby-2.2.0@shk/gems/mailboxer-0.13.0/app/builders",
     "/home/alfredo/.rvm/gems/ruby-2.2.0@shk/gems/mailboxer-0.13.0/app/mailers",
     "/home/alfredo/.rvm/gems/ruby-2.2.0@shk/gems/mailboxer-0.13.0/app/models",
     "/home/alfredo/.rvm/gems/ruby-2.2.0@shk/gems/mailboxer-0.13.0/app/uploaders",
     "/home/alfredo/.rvm/gems/ruby-2.2.0@shk/gems/devise-3.4.1/app/controllers",
     "/home/alfredo/.rvm/gems/ruby-2.2.0@shk/gems/devise-3.4.1/app/helpers",
     "/home/alfredo/.rvm/gems/ruby-2.2.0@shk/gems/devise-3.4.1/app/mailers",
     "/home/alfredo/rails_apps/shk/spec/mailers/previews"]
