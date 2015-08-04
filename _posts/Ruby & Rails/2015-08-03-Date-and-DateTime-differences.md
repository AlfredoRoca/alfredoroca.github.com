---
layout: post
title: "Date and DateTime differences"
description: ""
category: [ruby, rails]
tags: [date, datetime]
---
{% include JB/setup %}


    a1 = DateTime.strptime("10/6/1986", "%d/%m/%Y").to_time.to_i 
    => 518745600

    a2 = Date.strptime("10/6/1986", "%d/%m/%Y").to_time.to_i
    => 518738400
    
    a1-a2
    => 7200 (2 horas => hora local verano - UTC


