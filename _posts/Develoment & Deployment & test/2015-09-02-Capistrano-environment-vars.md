---
layout: post
title: "Capistrano environment variables"
description: ""
category: [capistrano, deployment]
tags: []
---
{% include JB/setup %}

#To let Capistrano db:migrate when database username and password are defined in environment variables

When you fire SSH, your app will load the SHELL variables which are defined in your .bashrc file. These only exist for the life of the shell, and therefore, we don't use them as much as ENV vars

You may be better putting the ENV vars in:

    /etc/environment

Like this:

    export ENVIRONMENT_VAR=value

This will make the variables available throughout the system, not just in different shell sessions


#Capistrano session variables

In deploy.rb

    set :default_environment, {
      'PATH' => "$PATH",
      'RUBY_VERSION' => 'ruby 2.2.0',
      'GEM_HOME'     => '/home/alfredo/.rvm/gems/ruby-2.2.0',
      'GEM_PATH'     => '/home/alfredo/.rvm/gems/ruby-2.2.0',
      'BUNDLE_PATH'  => '/home/alfredo/.rvm/gems/ruby-2.2.0'  # If you are using bundler.
    }

In production.rb

    set :rvm_ruby_version, '2.2.0@saap'

    set :rails_env, 'production'
    set :rake_env, 'production'

