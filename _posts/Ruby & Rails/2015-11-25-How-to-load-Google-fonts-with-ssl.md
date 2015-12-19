---
layout: post
title: "How to load Google fonts with SSL"
description: ""
category: [rails, ssl]
tags: []
---
{% include JB/setup %}

<https://developer.mozilla.org/en-US/docs/Security/MixedConten>

Instead of putting the css link in ```application_layout.html.erb```, import it in ```main.scss``` without https specification. The browser will choose the proper one.

    @import url(//fonts.googleapis.com/css?family=Nunito:300);

