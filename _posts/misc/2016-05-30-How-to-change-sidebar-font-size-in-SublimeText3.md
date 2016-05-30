---
layout: post
title: "How to change sidebar font size in SublimeText3"
description: ""
category: [sublime]
tags: []
---
{% include JB/setup %}

For the ST3 users who don't have the Default.sublime-theme file (which is actually the default configuration), the simplest procedure is:

1. Navigate to Sublime Text -> Preferences -> Browse Packages
2. Open the User directory
3. Create a file named Default.sublime-theme (if you're using the default theme, otherwise use the theme name, e.g. Material-Theme-Darker.sublime-theme) with the following content (modify font.size as required):

    [
        {
            "class": "sidebar_label",
            "color": [0, 0, 0],
            "font.bold": false,
            "font.size": 12
        },
    ]
