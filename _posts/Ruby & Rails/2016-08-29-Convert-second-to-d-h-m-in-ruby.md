---
layout: post
title: "Convert seconds to d h m"
description: ""
category: [ruby]
tags: [date]
---
{% include JB/setup %}


    def long_duration_to_s(total_seconds)
      total_seconds = total_seconds.to_i

      days  = total_seconds/86400
      remaining_seconds_after_days = total_seconds - days*86400
      hours = remaining_seconds_after_days/3600
      remaining_seconds_after_hours = remaining_seconds_after_days - hours*3600
      minutes = remaining_seconds_after_hours/60

      format("%02dd %02dh %02dm", days, hours, minutes)
    end

