---
layout: post
title: "Search and Filter Rails Models Without Bloating Your Controller"
description: ""
category: [rails]
tags: [scope]
---
{% include JB/setup %}

Source: http://www.justinweiss.com/articles/search-and-filter-rails-models-without-bloating-your-controller/

    # app/models/concerns/filterable.rb
    module Filterable
      extend ActiveSupport::Concern

      module ClassMethods
        def filter(filtering_params)
          results = self.where(nil)
          filtering_params.each do |key, value|
            results = results.public_send(key, value) if value.present?
          end
          results
        end
      end
    end
    
    # app/models/product.rb
    class Product
      include Filterable
      ...
    end
    
    #app/controllers/product_controller.rb
    def index
      @products = Product.filter(params.slice(:status, :location, :starts_with))
    end

