---
layout: post
title: "How to filter registers whose has many association is empty"
description: ""
category: [rails, activerecord]
tags: [associations]
---
{% include JB/setup %}


Models Order HM OrderItem

    Order.includes(:order_items).where(order_items: { order_id: nil })

