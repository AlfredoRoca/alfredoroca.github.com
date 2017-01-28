---
layout: post
title: "ActiveRecord query with regexp"
description: ""
category: [rails,activerecord,regexp]
tags: []
---
{% include JB/setup %}

    where('field ~* ?', 'regexp')