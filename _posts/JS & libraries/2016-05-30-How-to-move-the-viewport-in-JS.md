---
layout: post
title: "How to move the viewport in JS"
description: ""
category: [js]
tags: [viewport]
---
{% include JB/setup %}

##With animation

    $('html, body').animate({
        scrollTop: offset.top,
        scrollLeft: offset.left
    }, 'fast');

##Without animation:

    window.scroll(0,0)

