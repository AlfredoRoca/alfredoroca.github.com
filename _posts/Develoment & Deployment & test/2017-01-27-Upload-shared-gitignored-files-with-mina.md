---
layout: post
title: "Upload shared gitignored files with mina"
description: ""
category: [mina]
tags: []
---
{% include JB/setup %}

In `deploy.rb` you have:

    set :shared_files, ['config/database.yml', 'config/application.yml']

and right before deploy do
run

    run(:local){
        desc 'upload shared files'
        fetch(:shared_files, []).each do |linked_dir|
          command "scp #{linked_dir} #{fetch(:user)}@#{fetch(:domain)}:#{fetch(:shared_path)}/#{linked_dir}"
        end
      }
