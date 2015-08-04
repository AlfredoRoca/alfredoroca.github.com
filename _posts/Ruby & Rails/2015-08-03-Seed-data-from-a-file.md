---
layout: post
title: "Seed data from a file"
description: ""
category: [rails]
tags: [import_data, seed_data]
---
{% include JB/setup %}

    namespace :db do

      desc "creates sample data"
      task :sample => :environment do
        load File.join(Rails.root, "db", "samples.rb")
      end

    end


    $ rake db:sample
