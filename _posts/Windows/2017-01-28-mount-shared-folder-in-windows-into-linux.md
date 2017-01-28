---
layout: post
title: "Mount shared folder in windows into linux"
description: ""
category: [linux,windows]
tags: []
---
{% include JB/setup %}

    mkdir /mnt/temp
    mount -t cifs -o username=<login username>,password=<login pw>,file_mode=0777,dir_mode=0777 //windows_host_ip/shared_windows_folder /mnt/temp/

    en fstab: //192.168.1.100/temp    /mnt/temp/              cifs username=aaaaaaa,password=xxxxx,rw,file_mode=0777,dir_mode=0777 0 0

