---
layout: post
title: "How to create status methods"
description: ""
category: [ruby, oop]
tags: []
---
{% include JB/setup %}


#Extending ActiveRecord::Base#

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

        # Status Accessors
        status_names.each do |status_name|
          define_method "#{status_name}?" do
            status == status_name
          end
        end
      end
    end

#How to use it:#

    class Purchase < ActiveRecord::Base
      has_statuses %w(in_progress submitted approved partially_shipped fully_shipped)

      scope :all_not_shipped, where(:status => ["partially_shipped", "fully_shipped"])

      def not_shipped?
        !(partially_shipped? or fully_shipped?)
      end
    end
