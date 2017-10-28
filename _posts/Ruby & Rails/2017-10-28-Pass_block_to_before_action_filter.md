---
layout: post
title: "Pass block to before_action filter"
description: ""
category: [rails]
tags: [before_action]
---
{% include JB/setup %}

    before_action { |controller| Rails.logger.info "-----------------Controller class: #{controller.class}" }

    before_action { |controller| Rails.logger.info "-----------------Es UsersController? #{controller.class == Api::V2::Users::UsersController}" }
