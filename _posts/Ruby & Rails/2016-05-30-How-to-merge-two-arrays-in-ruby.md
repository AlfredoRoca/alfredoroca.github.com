---
layout: post
title: "How to merge arrays in Ruby"
description: ""
category: [ruby]
tags: [merge, array]
---
{% include JB/setup %}

## zip + flatten + uniq ##

    arr1.zip(arr2, arr3).flatten.uniq


## union operator ##

    arr1 | arr2 | arr3 
