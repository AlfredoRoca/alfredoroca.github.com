---
layout: post
title: "Rails 'presence' vs 'present?'"
description: ""
category: [rails]
tags: []
---
{% include JB/setup %}

Source: https://www.defmethod.com/blog/2016/12/7/nil-and-presence-in-ruby-on-rails

    some_string.present? some_string : some_default_string

Repeating some_string was redundant

    some_string.presence || some_default_string


    # rails console
    > ''.present?
    => false
    > ''.presence
    => nil
    > 'default'.present?
    => true
    > 'default'.presence
    => "default"