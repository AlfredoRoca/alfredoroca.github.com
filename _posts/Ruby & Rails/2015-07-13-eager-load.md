---
layout: post
title: "Eager load"
description: ""
category: [activerecord, associations] 
tags: [activerecord, associations]
---
{% include JB/setup %}

# INCLUDES - EAGER LOAD

multiple relationships

    users = User.includes(:address, :friends)

Nested relationships is possible using a Hash:

    users = User.includes(:address, friends: [:address, :followers])

Conditions with references:

    User.includes(:posts).where('posts.name = ?', 'example').references(:posts) 

SHK: 

    Coupon.includes(:booking, booking:[:space]).all.each{|c| puts c.booking.space.title if c.booking}