---
layout: post
title: "Mount a Virtualbox shared folder"
description: ""
category: [virtualbox]
tags: [shared-folder]
---
{% include JB/setup %}

#Virtual Box Shared folder

*host-folder* is in shared folders virtualbox machine configuration

    $ su
    $ mkdir /home/myself/host_folder
    $ mount -t vboxsf -o rw,uid=myself,gid=myself <host folder> /home/myself/host_folder

