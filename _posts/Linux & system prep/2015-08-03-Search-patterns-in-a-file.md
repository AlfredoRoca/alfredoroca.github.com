---
layout: post
title: "Search patterns in a file"
description: ""
category: [Linux]
tags: [file processing, text processing]
---
{% include JB/setup %}

    grep 'RoutingError\|FATAL\|ERROR\|Error' development.log

    egrep -wi 'Error|RoutingError' development.log

    where w words   i ignore case

