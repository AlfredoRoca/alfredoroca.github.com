---
layout: post
title: "How to eliminate values from params hash that are not valid option keys"
description: ""
category: [rails]
tags: [params]
---
{% include JB/setup %}


    params.slice(*available_option_keys)

ex.

    available_option_keys = [:first_option, :second_option]
    params = {first_option: 'first_value', strange_option: 'strange_value'}
    params.slice(*available_option_keys)
    => {:first_option=>"first_value"}

