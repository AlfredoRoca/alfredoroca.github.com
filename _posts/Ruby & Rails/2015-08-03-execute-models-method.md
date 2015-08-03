---
layout: post
title: "EXECUTE MODEL'S METHOD IN COMMAND CONSOLE OR WITH A CRONJOB"
description: ""
category: [Rails, cronjob]
tags: [cronjob]
---
{% include JB/setup %}

    class Booking < ActiveRecord::Base      
      def self.pay_the_keepers        
        puts "It's time to pay the keepers!"      
      end
    end

    $ rails runner Booking.pay_the_keepers

whenever schedule taskhttps://github.com/javan/whenever

    every 1.day, at: '23:00' do
        runner 'Booking.pay_the_keepers"
    end