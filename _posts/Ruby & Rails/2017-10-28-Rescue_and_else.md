---
layout: post
title: "Rescue + else"
description: ""
category: [ruby, rails]
tags: []
---
{% include JB/setup %}

Always execute `ensure` block

Without error executes 'else' block

    begin
      puts "1"
    rescue StandardError
      puts "std err"
    else
      puts "2"
    ensure
      puts "sure"
    end

Output: 

    1
    2
    sure
    => nil


With error executes `rescue` block, but not `else` one.

    begin
      puts "1"
      raise
    rescue StandardError
      puts "std err"
    else
      puts "2"
    ensure
      puts "sure"
    end

    Output:

    1
    std err
    sure
