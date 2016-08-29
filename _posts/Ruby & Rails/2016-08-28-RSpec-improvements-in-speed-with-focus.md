---
layout: post
title: "RSpec improvements in speed with focus"
description: ""
category: [rspec]
tags: [rspec, focus]
---
{% include JB/setup %}


<https://medium.com/table-xi/focus-your-rspec-workflow-4cd5798d2a3e#.h4uujojsd>



Uncomment lines in `spec_helper.rb` to enable focused tests, execute only with `:focus` metadata or fit or `fdescribe` blocks

    config.filter_run :focus
    config.run_all_when_everything_filtered = true
