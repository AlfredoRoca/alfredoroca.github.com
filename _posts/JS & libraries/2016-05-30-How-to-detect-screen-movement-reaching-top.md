---
layout: post
title: "How to detect screen movement reaching top"
description: ""
category: [js]
tags: [screen top]
---
{% include JB/setup %}

    
    $( document ).ready(function() {
        window.addEventListener('scroll', detectTop, false);
    }

    function detectTop() {
     if (window.pageYOffset < 1) {
        //   console.log("inside detectTop");
      }
    }
