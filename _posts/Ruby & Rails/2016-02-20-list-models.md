---
layout: post
title: "List models"
description: ""
category: [rails]
tags: []
---
{% include JB/setup %}

    @models = Dir['app/models/*.rb'].map {|f| File.basename(f, '.*').camelize.constantize.name }

