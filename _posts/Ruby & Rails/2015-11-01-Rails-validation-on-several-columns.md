---
layout: post
title: "Rails - uniqueness validation on several columns"
description: ""
category: []
tags: []
---
{% include JB/setup %}


    validates_uniqueness_of :emergency_id, scope: [:company_id, :phone, :email]
