---
layout: post
title: "Aggregate failures with RSpec"
description: ""
category: [rspec,test]
tags: []
---
{% include JB/setup %}

http://www.relishapp.com/rspec/rspec-expectations/v/3-5/docs/aggregating-failures

    aggregate_failures "testing response" do
      ....
    end

https://relishapp.com/rspec/rspec-core/docs/expectation-framework-integration/aggregating-failures#use-%60:aggregate-failures%60-metadata

    it "...", :aggregate_failures do
    ...
