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

###Example: Serv different photo each time a new photo is requested

    def new_photo
      big_photos = ["fondos/foto-1.jpg", "fondos/foto-2.jpg", "fondos/foto-3.jpg"]
      index = session[:big_photo] ||= 0
      index += 1
      index = 0 if index >= big_photos.size
      session[:big_photo] = index
      render json: {url: ActionController::Base.helpers.image_url(big_photos[index])}
    end

