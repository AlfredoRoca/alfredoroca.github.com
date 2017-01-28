---
layout: post
title: "Finding and copying files keeping folder structure"
description: ""
category: [linux,bash]
tags: []
---
{% include JB/setup %}

    find config/locales/ -iname ca.yml -print -exec cp --parents '{}' /home/alfredo/locales-saap-catalan/ \;
