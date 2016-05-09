---
layout: post
title: "How to check glibc version in Linux"
description: ""
category: [linux, glibc]
tags: []
---
{% include JB/setup %}


Check

    ldd --version
    yum info glibc

Update

    yum -y update glibc

Clear cache before updating

   yum clean all

Check services using glibc

    lsof +c0 -d DEL | awk 'NR==1 || /libc-/ {print $2,$1,$4,$NF}' | column -t

Reboot

   sudo reboot



