---
layout: post
title: "Scope of a range of dates"
description: ""
category: [rails, activerecord]
tags: [activerecord]
---
{% include JB/setup %}

    scope :in_daterange, ->(start_date, end_date) { where(created_at: start_date.to_date.beginning_of_day..end_date.to_date.end_of‌ _day) }

