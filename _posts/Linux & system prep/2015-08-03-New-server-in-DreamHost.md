---
layout: post
title: "Creating server in DreamHost.com"
description: ""
category: [system_configuration]
tags: [new_install]
---
{% include JB/setup %}

From DH Dashboard,
Launch instance
Details:
    Flavour: subsonic
    Boot source: Boot from image (creates new volume)
    Image: Fedora 21
    Dev size: 80 GB (default for subsonic)
    Dev name: vda (default)
Access & security
    Import SSH public key and choose it
    Security group: default

Associate floating IP

OpenStack client for accessing through ssh console

[http://wiki.dreamhost.com/Launch_an_Instance_from_the_Command_Line](http://wiki.dreamhost.com/Launch_an_Instance_from_the_Command_Line){:target="_blank"}

[http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html){:target="_blank"}

and set environment variables using the OpenStack RC file: http://docs.openstack.org/user-guide/common/cli_set_environment_variables_using_openstack_rc.html
SSH login to floating IP addr

Login:
    ssh dhc-user@67.205.57.114