---
layout: post
title: "Hide standard output"
description: ""
category: [bash, redirect, dev/null]
tags: []
---
{% include JB/setup %}

**Redirect the output to /dev/null

Example

    find / > /dev/null

    The entire standard output stream is ignored, but any errors will still appear on the console.

