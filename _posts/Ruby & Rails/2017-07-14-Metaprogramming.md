---
layout: post
title: "Metaprogramming in Rails"
description: ""
category: [metaprogramming, rails, ruby]
tags: []
---
{% include JB/setup %}

Metaprogramming = code that produces code

Learn by example:


    class Purchase < ActiveRecord::Base
      STATUSES = %w(in_progress submitted approved shipped received)
      
      validates_presence_of :status
      validates_inclusion_of :status, :in => STATUSES
      
      # Status Finders
      class << self
        STATUSES.each do |status_name|
          define_method "all_#{status_name}"
            where(:status => status_name)
          end
        end
      end

      # Status Accessors
      STATUSES.each do |status_name|
        define_method "#{status_name}?"
        status == status_name
        end
      end
    end

