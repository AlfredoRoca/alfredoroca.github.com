---
layout: post
title: "Read text file"
description: ""
category: [file]
tags: [file_manipulation]
---
{% include JB/setup %}

    if File.exist?("wind_info.txt")
      wind = IO.readlines("wind_info.txt")
      w = WindCondition.new(timestamp: wind[0].chomp, direction: wind[1].chomp, speed: wind[2].chomp)
    else
      w = WindCondition.new(timestamp: '--', direction: '--', speed: '--')
    end
    w.save


    # application.rb
    # 
    # read env vars file and export vars
    # 
    config.before_configuration do
      # env_file = File.join(Rails.root, 'config', 'local_env.yml')
      # YAML.load(File.open(env_file)).each do |key, value|
      #   ENV[key.to_s] = value
      # end if File.exists?(env_file)
      filepath = Rails.root + 'config/local_env.yml'
      if File.exists?(filepath)
        lines = IO.readlines(filepath)
        lines.each do |l|
          ENV[l.split('=')[0]] = l.split('=')[1]
        end
      end
    end