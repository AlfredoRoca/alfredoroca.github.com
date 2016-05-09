---
layout: post
title: "Bootstrap Glyphicons"
description: ""
category: [bootstrap, icon]
tags: []
---
{% include JB/setup %}

<http://stackoverflow.com/a/18225474/4191133>

If you want to use the Glyphicons separately, you can do that by directly referencing the Glyphicons css on Bootstrap CDN.

In html:

    <link href="//netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap-glyphicons.css" rel="stylesheet">

In css:

    @import url("//netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap-glyphicons.css");

Since the css file already includes all the needed Glyphicons dependencies (which are in a relative path on the Bootstrap CDN site), adding the css file is all there is to do to start using Glyphicons.
