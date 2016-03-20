---
layout: post
title: "Regular expressions"
description: ""
category: [regex]
tags: [regex]
---
{% include JB/setup %}

- [Email](#Email)
- [Find phone numbers](#Find phone numbers)
- [Any symbol](#Any symbol)

# Email

    /\b[A-Za-z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}\b/

# Find phone numbers

    /\d{9}|\d{3} \d{3}.\d{3}|\d{3}.\d{2}.\d{2}.\d{2}|\d.\d.\d.\d.\d.\d.\d.\d.\d|\d{2}.\d{3}.\d{2}.\d{2}/

# Any symbol

    /[ -#$-\/:-?{-~!\"@^_`\[\]]/