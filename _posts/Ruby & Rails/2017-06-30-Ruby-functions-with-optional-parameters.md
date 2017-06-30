---
layout: post
title: "Ruby functions with optional parameters"
description: ""
category: [ruby]
tags: [splat]
---
{% include JB/setup %}

    # receive an array
    def some_func(*args)
     puts args.count
    end
    some_func("x", nil)
    # 2

    # receive a hash
    def some_func(**args)
      puts args.count
    end

    some_func(a: "x", b: nil)
    # 2

