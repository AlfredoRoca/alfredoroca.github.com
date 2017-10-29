---
layout: post
title: "Add sensible data in secrets file"
description: ""
category: [rails]
tags: [secrets]
---
{% include JB/setup %}

In `config/secrets.yml`

    development: 
      stripe_publishable_key: pk_test_xxxxxxxxxxxxxxxxxxxxxxxx 
      stripe_secret_key: sk_test_xxxxxxxxxxxxxxxxxxxxxxxx

In `config/initializers/stripe.rb`

    Rails.configuration.stripe = {
        :publishable_key => Rails.application.secrets.stripe_publishable_key,
        :secret_key      => Rails.application.secrets.stripe_secret_key
    }

Usage: 

    Stripe.api_key = Rails.application.secrets.stripe_secret_key
