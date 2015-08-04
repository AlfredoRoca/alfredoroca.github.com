---
layout: post
title: "Creating server in DreamHost.com"
description: ""
category: [system_configuration]
tags: [new_install]
---
{% include JB/setup %}

#DH Dashboard,
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


#1st configuration
Source: [https://www.digitalocean.com/community/tutorials/initial-setup-of-a-fedora-21-server](https://www.digitalocean.com/community/tutorials/initial-setup-of-a-fedora-21-server)

Login as superuser:

##system update
    yum update
    reboot

login again as superuser
    
##groups and users
    groupadd deployers
    useradd -G deployers <deployer-name>
    userpw <deployer-name>

##ssh keys for login
    ssh-copy-id <user>@your_server_ip

##configuring the Time Zone
Localize proper zone file in */usr/share/zoneinfo/*

    ln -sf /usr/share/zoneinfo/Europe/Madrid /etc/localtime

Check with

    date

#firewall
    yum install -y iptables-services
    systemctl enable iptables
    => Created symlink from /etc/systemd/system/basic.target.wants/iptables.service to /usr/lib/systemd/system/iptables.service.
    systemctl start iptables
    iptables -L
    => default rules
        Chain INPUT (policy ACCEPT)
        target     prot opt source               destination         
        ACCEPT     all  --  anywhere             anywhere             state RELATED,ESTABLISHED
        ACCEPT     icmp --  anywhere             anywhere            
        ACCEPT     all  --  anywhere             anywhere            
        ACCEPT     tcp  --  anywhere             anywhere             state NEW tcp dpt:ssh
        REJECT     all  --  anywhere             anywhere             reject-with icmp-host-prohibited

        Chain FORWARD (policy ACCEPT)
        target     prot opt source               destination         
        REJECT     all  --  anywhere             anywhere             reject-with icmp-host-prohibited

        Chain OUTPUT (policy ACCEPT)
        target     prot opt source               destination         

    /usr/libexec/iptables/iptables.init save
    => iptables: Saving firewall rules to /etc/sysconfig/iptables:[  OK  ]

    vi /etc/sysconfig/iptables and add this lines
    -A INPUT -p tcp -m state --state NEW -m tcp --dport 80 -j ACCEPT
    -A INPUT -p tcp -m state --state NEW -m tcp --dport 443 -j ACCEPT
    systemctl restart iptables
    iptables -L
    => 
        Chain INPUT (policy ACCEPT)
        target     prot opt source               destination         
        ACCEPT     all  --  anywhere             anywhere             state RELATED,ESTABLISHED
        ACCEPT     icmp --  anywhere             anywhere            
        ACCEPT     all  --  anywhere             anywhere            
        ACCEPT     tcp  --  anywhere             anywhere             state NEW tcp dpt:ssh
        ACCEPT     tcp  --  anywhere             anywhere             state NEW tcp dpt:http
        ACCEPT     tcp  --  anywhere             anywhere             state NEW tcp dpt:https
        REJECT     all  --  anywhere             anywhere             reject-with icmp-host-prohibited
        ...

    yum install -y mlocate
    updatedb

[https://fedoraproject.org/wiki/Nginx](https://fedoraproject.org/wiki/Nginx){:target='_blank'}

    yum install nginx
    systemctl enable nginx.service
    => Created symlink from /etc/systemd/system/multi-user.target.wants/nginx.service to /usr/lib/systemd/system/nginx.service.
    systemctl start nginx.service

Change user to rails app folder owner

    vi /etc/nginx/nginx.conf

In /etc/nginx/conf.d 
    vi /67webs.conf
    => server block configuration

    systemctl restart nginx.service

