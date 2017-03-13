---
layout: post
title: "Difference between &, disown, NOHUP"
description: ""
category: [linux]
tags: []
---
{% include JB/setup %}

<http://unix.stackexchange.com/questions/3886/difference-between-nohup-disown-and>

Example:

Start Rails Server in background (for staging machines)

    bundle exec nohup rails s -p 3001 -e production -b 0.0.0.0 &

