---
layout: post
title: "Change sidebar font size in Sublime"
description: ""
category: [sublime, configuration]
tags: []
---
{% include JB/setup %}

    vi ~/.config/sublime-text-3/Packages/User/Default.sublime-theme

    [
        {
            "class": "sidebar_label",
            "color": [0, 0, 0],
            "font.bold": true,
            "font.size": 12
        },
    ]

