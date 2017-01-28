---
layout: post
title: "Add a new disk to Virtualbox machine"
description: ""
category: [virtualbox]
tags: []
---
{% include JB/setup %}


    mount /dev/sdb /mnt/provisional/
    fdisk /dev/sdb
    mkfs -t ext4 /dev/sdb
    mount /dev/sdb /mnt/provisional/
    cp -a /home/* -r /mnt/provisional/

