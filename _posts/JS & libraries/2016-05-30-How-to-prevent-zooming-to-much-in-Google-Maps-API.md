---
layout: post
title: "How to prevent zooming to much in Google Maps API"
description: ""
category: [Google, maps, js]
tags: []
---
{% include JB/setup %}

    
    map.setOptions({ maxZoom: 15 });
    map.fitBounds(bounds);
    map.setOptions({ maxZoom: null });

