---
layout: post
title: "Prevent YUM from updating the kernel"
description: ""
category: [linux]
tags: []
---
{% include JB/setup %}


#How to Prevent YUM from Updating the Kernel

<http://www.howtogeek.com/50898/how-to-prevent-yum-from-updating-the-kernel/>

Kernel update is the unique linux operation that needs rebooting the machine

To prevent accidentally updating kernel:

    # yum –exclude=kernel* update

Or in **/etc/yum.conf** and **/etc/dnf/dnf.conf**

    exclude=kernel*
