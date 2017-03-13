---
layout: post
title: "Grep to find duplicated css"
description: ""
category: [css]
tags: []
---
{% include JB/setup %}

This video at min 22

    https://www.youtube.com/watch?v=0NDyopLKE1w



    https://www.eriwen.com/tools/grep-is-a-beautiful-tool/

    grep -r h[1-6] ./*.css | wc -l

    grep -r h[1-6] app/assets/stylesheets/*.*css | wc -l
    grep -r font-size app/assets/stylesheets/*.*css | wc -l
    grep -r margin app/assets/stylesheets/*.*css | wc -l
    grep -r padding app/assets/stylesheets/*.*css | wc -l
    grep -r padding:0 app/assets/stylesheets/*.*css | wc -l
    grep -r margin:0 app/assets/stylesheets/*.*css | wc -l
    grep -r important app/assets/stylesheets/*.*css | wc -l
    grep -r color app/assets/stylesheets/*.*css | wc -l
    grep -r background app/assets/stylesheets/*.*css | wc -l


Other tags: `left, height, width, position, right, float, display`
