---
layout: post
title: "How to limit value asignation"
description: ""
category: [ruby]
tags: []
---
{% include JB/setup %}


Simply as using Array `min` method.

    def accelerate
    # Cars accelerate quickly, and can go 100mph (in Los Angeles).
      self.speed = [speed + 10, 100].min
    end

