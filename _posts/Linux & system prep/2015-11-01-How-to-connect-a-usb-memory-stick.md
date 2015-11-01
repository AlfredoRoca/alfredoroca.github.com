---
layout: post
title: "How to connect a usb memory stick"
description: ""
category: [linux, usb, devices]
tags: []
---
{% include JB/setup %}


As root, Create udev rule:
    
    vi /etc/udev/conf.d/rules.d/75-my_usb.rules
    SUBSYSTEM=="usb", SYMLINK+="my_usb", MODE="0666"

Connect the usb and Get the block assigned
    
    dmesg

==>

    [ 9882.238491] usb-storage 1-1:1.0: USB Mass Storage device detected
    [ 9882.238607] scsi host5: usb-storage 1-1:1.0
    [ 9883.247574] scsi 5:0:0:0: Direct-Access     SanDisk  Extreme          0001 PQ: 0 ANSI: 6
    [ 9883.248043] sd 5:0:0:0: Attached scsi generic sg2 type 0
    [ 9883.462147] sd 5:0:0:0: [sdb] 122544516 512-byte logical blocks: (62.7 GB/58.4 GiB)
    [ 9883.471580] sd 5:0:0:0: [sdb] Write Protect is off
    [ 9883.471585] sd 5:0:0:0: [sdb] Mode Sense: 53 00 00 08
    [ 9883.482132] sd 5:0:0:0: [sdb] Write cache: disabled, read cache: enabled, doesn't support DPO or FUA
    [ 9883.536495]  sdb: sdb1
    [ 9883.582602] sd 5:0:0:0: [sdb] Attached SCSI removable disk

The block assigned is sdb1

Create folder for the usb filesystem

    mkdir /media/usb

    mount /dev/sdb1 /media/usb

Safely disconnect

    umount /media/usb
