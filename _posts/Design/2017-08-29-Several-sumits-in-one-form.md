---
layout: post
title: "Several submit actions in same form"
description: ""
category: [html]
tags: []
---
{% include JB/setup %}

    <form action="/submit">
      
      <input type="submit" value="Submit">
      
      <input type="submit" value="Go Elsewhere" formaction="/elsewhere">
      
    </form>

