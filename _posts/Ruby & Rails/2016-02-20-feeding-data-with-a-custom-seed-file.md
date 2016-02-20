---
layout: post
title: "Feeding data with a custom seed file"
description: ""
category: [rails, activerecord]
tags: []
---
{% include JB/setup %}

    # lib/tasks/custom_seed.rake
    namespace :db do
      namespace :seed do
        Dir[File.join(Rails.root, 'db', 'seeds', '*.rb')].each do |filename|
          task_name = File.basename(filename, '.rb').intern    
          task task_name => :environment do
            load(filename) if File.exist?(filename)
          end
        end
      end
    end

This rakefile accepts the name of a seed file in the db/seeds directory (excluding the .rb extension), then runs it as it would run seeds.rb. You can execute the rake task by issuing the following from the command line:

    rake db:seed:seed_file_name # Name of the file EXCLUDING the .rb extension




