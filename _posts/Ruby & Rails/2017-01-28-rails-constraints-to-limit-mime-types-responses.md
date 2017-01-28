---
layout: post
title: "Rails constraints to limit mime types responses"
description: ""
category: [rails]
tags: []
---
{% include JB/setup %}

    resources :resource_name, constraints: { format: :html }
