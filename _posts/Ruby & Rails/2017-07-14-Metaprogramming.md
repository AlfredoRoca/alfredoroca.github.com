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

**Express declaration of finders and accessors**

    class Purchase < ActiveRecord::Base
      validates :status,
        :presence => true,
        :inclusion => { :in => %w(in_progress submitted approved shipped received canceled) }

      # Status Finders
      scope :all_in_progress, where(:status => "in_progress")
      scope :all_submitted, where(:status => "submitted")
      scope :all_approved, where(:status => "approved")
      scope :all_shipped, where(:status => "shipped")
      scope :all_received, where(:status => "received")
      scope :all_canceled, where(:status => "canceled")

      # Status Accessors
      def in_progress?
        status == "in_progress"
      end
      def submitted?
        status == "submitted"
      end
      def approved?
        status == "approved"
      end
      def shipped?
        status == "shipped"
      end
      def received?
        status == "received"
      end
      def canceled?
        status == "canceled"
      end
    end


**Metaprogramming**

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

**Extending classes**

    # lib/extensions/statuses.rb
    class ActiveRecord::Base
      def self.has_statuses(*status_names)
        validates :status,
          :presence => true,
          :inclusion => { :in => status_names }

        # Status Finders
        status_names.each do |status_name|
          scope "all_#{status_name}", where(:status => status_name)
        end

        # Status accessors
        status_names.each do |status_name|
          define_method "#{status_name}?" do
            status == status_name
          end
        end
      end
    end
    
    class Purchase < ActiveRecord::Base
      has_statuses :in_progress, :submitted, :approved, :shipped,
      :received
    end
