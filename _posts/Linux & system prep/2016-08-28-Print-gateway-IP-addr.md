---
layout: post
title: "Print gateway IP addr"
description: ""
category: [linux, bash]
tags: [grep, network, cut]
---
{% include JB/setup %}


    grep -i 'gateway' /etc/sysconfig/network-scripts/ifcfg-enp0s3 | cut -f2 -d=
