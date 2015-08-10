---
layout: post
title: "About users and groups"
description: ""
category: [linux, fedora]
tags: [users, groups]
---
{% include JB/setup %}

#Identifying current user

To list the currently logged-on users, type

    $ who

#To identify the current user, type

    $ whoami

    /user/sbin

#Adding/deleting users

    $ sudo useradd <alfredo>
    $ sudo passwd <alfredo>

    sudo useradd <name> -p PASSWORD
    sudo useradd <name< -G GROUP1[,GROUP2,...[,GROUPN]]]

##Home directory:

    /home/user_name

    id
    => alfredo:x:1000:1000::/home/alfredo:/bin/bash

##Home directory remains (temporary inactivation)

    $ sudo userdel <user name>

##Home directory is deleted.

    $ sudo userdel <user_name> -r

#Identifying
    $ id
    uid=0(root) gid=0(root) groups=0(root)
    $ id alfredo
    uid=1000(alfredo) gid=1000(alfredo) groups=1000(alfredo),10(wheel)

#Change user password

    passwd <user_name>

#Adding/deleting groups

    $ sudo groupadd <group_name>
    $ sudo groupdel <group_name>

    $ groups alfredo
    alfredo : alfredo wheel

#Add user to groups and removes from others groups

    $ sudo usermod -G <group1>,<grouop2> <user_name>

#Add user to group and preserves other groups

    $ sudo usermod -a -G <group1> <user_name>

##Creates and add user to groups

    $ sudo useradd -G <group1>,<grouop2> <user_name>

##Refresh group membership without logging out

    exec su -l alfredo

##Files

    /etc/group  --> list of groups
    /etc/passwd

##Set up sudo user

    echo "student ALL=(ALL) ALL" > /etc/sudoers.d/student
    chmod 440 /etc/sudoers.d/student

##Sudoers list

    visudo
    visudo -f /etc/sudoers.d/<file>

The basic structure of a line is

    who where = (as whom) what

Reco:

    /etc/sudoers    --> for all users
    /etc/sudoers.d/ --> one file for each user named like user's name

Logging (depending on distro)

    /etc/log/auth.log
    /etc/log/secure
    /etc/log/messages

Ex:

    Jun 10 12:14:50 VBoxDev1 sudo:  alfredo : TTY=pts/0 ; PWD=/home/alfredo ; USER=root ; COMMAND=/bin/cat /etc/sudoers.d/README

##Which group user belongs to
    groups <user name>


#Profile

On boot:

    /etc/profile

Then, the first in /home/<user> of these

    .bash_profile
    .bash_login
    .profile

On a new shell or terminal window

    .bashrc

#change user quickly
    su - <name>

