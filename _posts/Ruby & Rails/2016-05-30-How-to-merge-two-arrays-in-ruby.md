---
layout: post
title: "How to merge arrays in Ruby"
description: ""
category: [ruby, array]
tags: [merge]
---
{% include JB/setup %}

1. zip + flatten + uniq

    arr1.zip(arr2, arr3).flatten.uniq


2. union operator

    arr1 | arr2 | arr3 
