---
layout: post
title: "How to downgrade a gem in Rails"
description: ""
category: [rails]
tags: [downgrade, gemfile]
---
{% include JB/setup %}

    
Specify gem version in Gemfile and bundle update gem-name

    #Gemfile
    gem 'gem-name', 'version'

Bundle

    bundle update gem-name

