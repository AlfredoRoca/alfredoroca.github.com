---
layout: post
title: "CSS Centering"
description: ""
category: [css]
tags: []
---
{% include JB/setup %}

Source: <https://css-tricks.com/centering-css-complete-guide/>

    .parent {
      position: relative;
    }

    .child  {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }