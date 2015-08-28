---
layout: post
title: "Linux System info"
description: ""
category: [linux]
tags: [server, system, administration]
---
{% include JB/setup %}

#Kernel data

    /proc

    /proc/cpuinfo
    /proc/interrupts
    /proc/meminfo
    /proc/mounts
    /proc/partitions
    /proc/version

    /etc/os-release

    lsb_release -a


    uname -a

        ==> i686    ==> 32-bit version of Linux.
        ==> x86_64  ==> 64-bit version of Linux.

    uname -a -m -p

        ==> Linux shk-1.novalocal 4.1.3-100.fc21.x86_64 #1 SMP Wed Jul 29 18:59:46 UTC 2015 x86_64 x86_64 x86_64 GNU/Linux

#Devices

    fdisk -l
    lsblk

