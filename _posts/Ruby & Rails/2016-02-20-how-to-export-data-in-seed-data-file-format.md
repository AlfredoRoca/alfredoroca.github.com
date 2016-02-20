---
layout: post
title: "How to export data in a seeds data file format"
description: ""
category: [rails]
tags: []
---
{% include JB/setup %}


    #
    #  USAGE: rake export:seeds_format > db/seeds.rb
    #  
    namespace :export do
      desc "Prints data in a seeds.rb way."
      task :seeds_format => :environment do
        # next array with model names
        [
          "Area",
          "Company",
          "User",
        ].each do |model|
          model.constantize.order(:id).all.each do |register|
            puts "#{model}.create(#{register.serializable_hash.delete_if {|key, value| ['created_at','updated_at','id'].include?(key)}.to_s.gsub(/[{}]/,'')})"
          end
        end
      end
    end

