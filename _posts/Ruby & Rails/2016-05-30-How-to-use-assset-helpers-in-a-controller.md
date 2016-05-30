---
layout: post
title: "How to use assset helpers in a controller"
description: ""
category: [rails]
tags: [helpers, assets]
---
{% include JB/setup %}

    ActionController::Base.helpers.asset_path("configuration.yml")

    render json: {url: ActionController::Base.helpers.image_path('fondos/big_MKF_1176-235.jpg')}
