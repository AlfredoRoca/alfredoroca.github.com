---
layout: post
title: "Force SSH do not use key and ask for password"
description: ""
category: [linux, ssh]
tags: []
---
{% include JB/setup %}

    ssh -o PreferredAuthentications=password -o PubkeyAuthentication=no remote-server


