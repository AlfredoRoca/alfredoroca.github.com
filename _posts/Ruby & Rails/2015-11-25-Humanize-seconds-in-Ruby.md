---
layout: post
title: "Humanize seconds in Ruby"
description: ""
category: [ruby]
tags: [iso8601, time]
---
{% include JB/setup %}


    def humanize secs
      [[60, :seconds], [60, :minutes], [24, :hours], [1000, :days]].map{ |count, name|
        if secs > 0
          secs, n = secs.divmod(count)
          "#{n.to_i} #{name}"
        end
      }.compact.reverse.join(' ')
    end

Convert to UTC

    Time.now.utc

How to convert timestamp to ISO8601 to pass to moment.js

    timestamp.to_time.iso8601

