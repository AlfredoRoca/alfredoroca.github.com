---
layout: post
title: "SQL Server with Rails"
description: ""
category: [rails, sqlserver]
tags: []
---
{% include JB/setup %}

**Using TinyTds gem**

Connection to DB

    client = TinyTds::Client.new username: 'Dixquimics', password: 'D123456', host: '192.168.0.51', database: 'StreamlineDB'

Query

    res = client.execute("select * from DixEstadisticas")
    res.active?

Data usage

    res.each do |row|
    puts row
    end

    res.affected_rows

    res.fields

    rows = res.each(as: :array, symbolize_keys: true)
    rows.count

query to return only first row from a huge table

    res.each(first: true)

For saap (return only one record)

    res.first
