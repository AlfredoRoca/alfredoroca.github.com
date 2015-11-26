---
layout: post
title: "How to clear session variables in Rails"
description: ""
category: [rails]
tags: []
---
{% include JB/setup %}

YES

    session.delete(:order_id)

NO

    session[:order_id] = nil

