---
layout: post
title: "Testing sanitization of user entries"
description: ""
category: [test, rails]
tags: []
---
{% include JB/setup %}

Introduce JS code in text form fields

    <a href="javascript:alert('Boom!')">link</a>

If alert is fired, sanitization is not working and you are in danger!