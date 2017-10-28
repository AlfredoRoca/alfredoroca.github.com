---
layout: post
title: "Smart way to fetch a value from a hash (array) giving a default value if key is missing"
description: ""
category: [ruby, rails]
tags: []
---
{% include JB/setup %}

    {saludo: 'hola'}.fetch(:saludo) { 'aloha' }
    => hola

    {saludo: 'hola'}.fetch(:greeting) { 'aloha' }
    => aloha
