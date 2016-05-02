---
layout: post
title: "Time lapse between dates"
description: ""
category: []
tags: []
---
{% include JB/setup %}


<http://api.rubyonrails.org/classes/ActionView/Helpers/DateHelper.html#method-i-distance_of_time_in_words>

ApplicationController.rb

    include ActionView::Helpers::DateHelper

In Controller

      @project_starting_date = @activities.first.start
      @project_ending_date = (@activities.last.try(:ended) || @activities.last.start) + 1.day
      @project_age = distance_of_time_in_words(@project_starting_date, @project_ending_date)

