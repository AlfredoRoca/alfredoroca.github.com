---
layout: post
title: "Specify order in has_many association"
description: ""
category: [rails, associations]
tags: []
---
{% include JB/setup %}

    has_many   :actions, -> { order :id }, dependent: :destroy


