---
layout: post
title: "Execute model's method in command console or with a cronjob"
description: ""
category: [rails, cronjob]
tags: [cronjob]
---
{% include JB/setup %}

    class Booking < ActiveRecord::Base      
      def self.pay_the_keepers        
        puts "It's time to pay the keepers!"      
      end
    end

    $ rails runner Booking.pay_the_keepers

whenever schedule task
https://github.com/javan/whenever

    every 1.day, at: '23:00' do
        runner 'Booking.pay_the_keepers"
    end