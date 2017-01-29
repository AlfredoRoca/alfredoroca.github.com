---
layout: post
title: "How to convert a string into date in JS"
description: ""
category: [js, date, string]
tags: [convert]
---
{% include JB/setup %}

    var str = "23/11/2015 23:45:13";
    var p = str.split(/[\s//:]+/);
    var date = new Date(p[2],p[1]-1,p[0],p[3],p[4],p[5]);
    console.log(date);
    => Date 2015-11-23T22:45:13.000Z

    var str = "23/06/2015 23:45:13";
    var p = str.split(/[\s//:]+/);
    var date = new Date(p[2],p[1]-1,p[0],p[3],p[4],p[5]);
    console.log(date)
    => Date 2015-06-23T21:45:13.000Z

    var str = "23/06/2015 23:45:13";
    var p = str.split(/[\s//:]+/);
    var date = new Date(Date.UTC(p[2],p[1]-1,p[0],p[3],p[4],p[5]));
    console.log(date)
    => Date 2015-06-23T23:45:13.000Z
