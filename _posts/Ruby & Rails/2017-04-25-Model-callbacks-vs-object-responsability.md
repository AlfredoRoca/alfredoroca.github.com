---
layout: post
title: "Model callbacks vs object responsability"
description: "Extract callback logic to an object"
category: [rails]
tags: [callback, srp]
---
{% include JB/setup %}

<http://samuelmullen.com/2013/05/the-problem-with-rails-callbacks/>

## Why Are Callbacks So Problematic?

In his post on [ActiveRecord, Caching, and the Single Responsibility Principle](https://robots.thoughtbot.com/activerecord-caching-and-the-single-responsibility), Joshua Clayton noticed “after_* callbacks on Rails models seem to have some of the most tightly-coupled code, especially when it comes to models with associations.”

It’s no coincidence. “before_” callbacks are generally used to prepare an object to be saved. Updating timestamps or incrementing counters on the object are the sort of things we do “before” the object is saved. On the other hand, “after_*” callbacks are primarily used in relation to saving or persisting the object. Once the object is saved, the purpose (i.e. responsibility) of the object has been fulfilled, and so what we usually see are callbacks reaching outside of its area of responsibility, and that’s when we run into problems.

## Solving the Problem

Jonathan Wallace, over at the [Big Nerd Ranch](http://bignerdranch.com/), ran into to same problems and came up with one simple rule: **“Use a callback only when the logic refers to state internal to the object.”**

If we can’t use callbacks which extend responsibility outside their class, what do we do? We make an object whose responsibility is to handle that callback.

**Before**

    class Order < ActiveRecord::Base
      belongs_to :user
      has_many :line_items
      has_many :products, :through => :line_items
      
      after_create :purchase_completion_notification
      
      private
      
      def purchase_completion_notification
        Notifier.purchase_notifier(self).deliver
      end
    end

    class Notifier < ActionMailer...
      def purchase_notifier(order)
        @order = order
        @user = order.user
        @products = order.products

        rest of the action mailer logic
      end
    end


**After**

    class Order < ActiveRecord::Base
      belongs_to :user
      has_many :line_items
      has_many :products, :through => :line_items
    end

Here’s our new class:

    class OrderCompletion
      attr_accessor :order
      
      def initialize(order)
        @order = order
      end
      
      def create
        self.purchase_completion_notification if self.order.save
      end
      
      def purchase_completion_notification
        Notifier.purchase_notifier.deliver(self.order)
      end
    end

It’s a simple matter to use this in our controller too:

    def create
      @order = Order.new(params[:order])
      @order_completion = OrderCompletion.new(@order)
      
      if @order_completion.create
        redirect_to root_path, notice: 'Your order is being processed.'
      else
        render action: "new"
      end
    end
