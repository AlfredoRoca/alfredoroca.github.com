---
layout: post
title: "How to fit bounds in Google Maps"
description: ""
category: [google, maps]
tags: []
---
{% include JB/setup %}

    newMapBounds = new google.maps.LatLngBounds();
    newMapBounds.extend(new google.maps.LatLng(this._south, this._west));
    newMapBounds.extend(new google.maps.LatLng(this._north, this._east));
    map.fitBounds(newMapBounds);
