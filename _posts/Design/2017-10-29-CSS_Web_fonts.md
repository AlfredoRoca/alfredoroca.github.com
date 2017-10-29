---
layout: post
title: "CSS web fonts"
description: ""
category: []
tags: []
---
{% include JB/setup %}

<https://feedly.com/i/entry/Fr3jBijaGYsqKfY0ZJAYuAXvHrE03yR6qzptYNhpnp8=_15ee27e429b:3e3344:6aebb31f>

Simplified version: not supporting IE8 and Android 4.4

    @font-face {
        font-family: Elena;
        src: local("Elena"),
             url(elena-regular.woff2) format("woff2"),
             url(elena-regular.woff) format("woff");
    }

Note: `local` avoids downloading if is in the system.

Add `url(elena.otf) format("opentype");` to support Android 4.4 and earlier.
