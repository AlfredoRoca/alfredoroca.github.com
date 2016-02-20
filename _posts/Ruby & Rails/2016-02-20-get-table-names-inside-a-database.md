---
layout: post
title: "Get table names inside a database"
description: ""
category: [rails, activerecord]
tags: []
---
{% include JB/setup %}

    ActiveRecord::Base.connection.tables.map do |model|
      model.capitalize.singularize.camelize
    end

