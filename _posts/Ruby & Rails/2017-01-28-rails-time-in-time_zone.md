---
layout: post
title: "Rails time in time_zone"
description: ""
category: [rails,time,date]
tags: []
---
{% include JB/setup %}

Source: <http://danilenko.org/2012/7/6/rails_timezones/>

    Time.zone.now
     => Wed, 26 Oct 2016 23:34:12 CEST +02:00
    
    Time.zone.now.zone
     => "CEST"

    Time.zone.today
    Time.zone.today - 1.day

