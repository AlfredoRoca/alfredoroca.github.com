---
layout: post
title: "Encode string for url in ruby"
description: ""
category: [ruby]
tags: []
---
{% include JB/setup %}


    require 'open-uri'
    str = "RDAM 123"
    puts URI::encode(str)

    => RDAM%20123

