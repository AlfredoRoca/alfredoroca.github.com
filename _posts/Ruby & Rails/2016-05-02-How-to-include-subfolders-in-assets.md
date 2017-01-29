---
layout: post
title: "How to include subfolders in assets"
description: ""
category: [rails]
tags: [assets]
---
{% include JB/setup %}


"javascripts" and "stylesheets" folders are included by default in assets.rb
    
    Rails.application.config.assets.paths << "#{Rails.root}/vendor/assets/path"