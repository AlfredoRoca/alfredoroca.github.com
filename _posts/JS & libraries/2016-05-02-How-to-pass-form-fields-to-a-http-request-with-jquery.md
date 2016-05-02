---
layout: post
title: "How to pass all input fields of a form to a http request with jQuery"
description: ""
category: [jquery]
tags: [http, form]
---
{% include JB/setup %}


    $.get('/spots', $("#spots_search_form").serialize(), null, 'script');

    $("#spots_search_form").serialize()
    => lat=40.68100142652534&lng=2.0104988499999763&lat_min=38.85508911736183&lat_max=42.50691373568885&lng_min=0.5410774632812263&lng_max=3.4799202367187263&page=&more_filters_visible=false&city=&sort_by=distance
