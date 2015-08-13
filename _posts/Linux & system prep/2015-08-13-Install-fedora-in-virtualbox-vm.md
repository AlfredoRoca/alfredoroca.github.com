---
layout: post
title: "Install Fedora in VirtualBox VM"
description: ""
category: [fedora, installation]
tags: [virtualbox, vm]
---
{% include JB/setup %}

#Install Fedora ina new VM
- Download Latest version of Fedora Live Image from <https://getfedora.org/en/workstation/download/>
- Burn DVD or USB  with downloaded iso image or copy it to host
- Create new VM on host and make boot from DVD
- Add DVD and open Live IMAGE iso
- Start VM
- Install Fedora in HDD following instructions
- Add root password
- Create user with password - make it administrator (group wheel)
- After installation, shutdown the machine and remove DVD
- Start the machine

#Install Guest Additions prerequisites
Source: <http://www.if-not-true-then-false.com/2010/install-virtualbox-guest-additions-on-fedora-centos-red-hat-rhel/comment-page-7/>

    su -
    yum update kernel*
    reboot
    
    su -
    dnf install gcc kernel-devel kernel-headers dkms make bzip2 perl

    VirtualBox menu - Device/Ïnsert Guest Additions CD and install

##Change screen resolution
In Virtualbox, menu File/Preferences/DIsplay

- Change max to 1920x1080
- Display VM in full screen mode

    


by selectiong Insert Guest additions CD image in VirtualBox Device menu
