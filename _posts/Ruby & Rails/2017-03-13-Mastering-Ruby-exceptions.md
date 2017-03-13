---
layout: post
title: "Mastering Ruby exceptions"
description: ""
category: [ruby, exceptions]
tags: []
---
{% include JB/setup %}

Source: Honeybadger ebook: Mastering Ruby exceptions

Rescuing Specifc Errors (The Best Way)

Full rescue syntax:

    begin
    action
    rescue ClassError => e
        retry_request
    rescue
        send_alert
    else
        record_success
    ensure
        close_network_connection
    else
    end 

Method Rescue Syntax

    def my_method
    ...
    rescue
    ...
    else
    ...
    ensure
    ...
    end

This is particularly useful if you want to return a “fallback” value when an
exception occurs. Here’s an example:

    def data
        JSON.parse(@input)
        rescue JSON::JSONError
        {}
    end 