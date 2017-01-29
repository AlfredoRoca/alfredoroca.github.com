---
layout: post
title: "How to get last registers of each group in PostgreSQL"
description: ""
category: [postgresql]
tags: []
---
{% include JB/setup %}

    ContractedPlan.all.order(:user_id, start: :desc).select('DISTINCT ON(user_id) *')