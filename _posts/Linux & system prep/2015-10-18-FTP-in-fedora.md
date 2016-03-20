---
layout: post
title: "ftp server in fedora"
description: ""
category: [linux, ftp]
tags: []
---
{% include JB/setup %}

# SFTP

<https://docs.fedoraproject.org/en-US/Fedora/17/html/System_Administrators_Guide/s3-ftp-vsftpd-conf.html>

    sudo yum install vsftpd

    systemctl start/stop/restart vsftpd.service

start auto at boot

    systemctl enable vsftpd

