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
Source: [http://vladigleba.com/blog/2014/03/05/deploying-rails-apps-part-1-securing-the-server/](http://vladigleba.com/blog/2014/03/05/deploying-rails-apps-part-1-securing-the-server/)

Login as superuser:

##system update
    yum update
    reboot

login again as superuser
    
##groups and users
###create password for root
    passwd  => pw for root
###deployers group with root access
    groupadd deployers
    visudo   and add line
        %deployers      ALL=(ALL) ALL
###add users to deployers group
    useradd -G deployers,rvm <deployer-name>
    userpw <deployer-name>

## SSH access
###Config port

    /etc/ssh/sshd_config
    => change Port #PORTNUMBER
    => PermitRootLogin no
    => last line UseDNS no
    => PasswordAuthentication yes

### restart ssh service
    service restart sshd

### check if ssh service is running
    ps aux | grep sshd
    service sshd status

###Check who is listening on port #PORT
    netstat -plant | grep #PORT

### Check open ports
    lsof -i

###Tell SELinux about the port    
    semanage port -a -t ssh_port_t -p tcp #PORTNUMBER

###ssh keys for login
    ssh-key-gen
    ssh-copy-id user@your_server_ip 

##configuring the Time Zone
Localize proper zone file in */usr/share/zoneinfo/*

    ln -sf /usr/share/zoneinfo/Europe/Madrid /etc/localtime

Check with

    date

##firewall
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

## locate (optional)
    yum install -y mlocate
    updatedb

##nginx
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

priviledges: apply 755 for directories and 644 for files
Nginx needs to have *read* permissions for the file as well as *execute* permissions for all the folders in the path
    namei -l /var/www/67webs.com/index.html
    =>
        f: /var/www/67webs.com/index.html
        dr-xr-xr-x root root /
        drwxr-xr-x root root var
        drwxr-xr-x root root www
        drwxrwxr-x root root 67webs.com
        -rw-rw-r-- root root index.html

##SELinux
If 403 error persists check and setup SELinux

Source: [http://stackoverflow.com/questions/22586166/why-does-nginx-return-a-403-even-though-all-permissions-are-set-properly](http://stackoverflow.com/questions/22586166/why-does-nginx-return-a-403-even-though-all-permissions-are-set-properly)

    getenforce
    => Enforcing
    setenforce Permissive

Check with curl localhost

If this solved the problem

    chcon -Rt httpd_sys_content_t /var/www
    setenforce Enforcing

## DNS
In register (Whois) change DNS to ns1, ns2, ns3.dreamhost.com
In DH, add custom DNS record type A "" and "www" pointing to the assigned IP

## RVM
Create rvm group as superuser

    groupadd rvm
    usermod -a -G rvm root
    usermod -a -G rvm <other users>  like 'deployer'
    exit
    su alfredo
    gpg2 --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
    \curl -sSL https://get.rvm.io | bash -s stable
    source /home/alfredo/.rvm/scripts/rvm

###Ruby
    rvm install 2.2.1
    rvm gemset create gemset_name    # create a gemset
    rvm 2.2.1@gemset_name  # specify Ruby version and our new gemset

###Rails
Edit ~/.gemrc

    install: --no-document
    update: --no-document

    gem install rails [-v rails_version  # install specific Rails version]

###PostgreSQL

Source: [https://fedoraproject.org/wiki/PostgreSQL](https://fedoraproject.org/wiki/PostgreSQL)

    sudo yum install postgresql-server postgresql-contrib
    sudo systemctl enable postgresql
    sudo postgresql-setup initdb
    sudo systemctl start postgresql
    sudo yum install pgadmin3   -> optional
    sudo su - postgres
    psql
    => postgres=# 
        \password postgres
        create user <user-name> with password <pw>;

/var/lib/pgsql/data/postgresql.conf change

    log_destination = 'stderr'
    logging_collector = on
    log_filename = 'postgresql-%G-%m.log'
    log_truncate_on_rotation = off
    log_rotation_age = 31d
    client_min_messages = notice
    log_min_messages = info
    log_min_error_statement = notice
    log_min_duration_statement = 1000  # in ms
    log_line_prefix = '%t %u@%r:%d [%p] '
    # %t -- timestamp
    # %u -- user
    # %r -- client's host
    # %d -- database
    # %p -- PID
    log_line_prefix = '%t [%p] '  -> simplified for one user one db

    systemctl restart postgresql
    
## Rails App folder
    mkdir /var/www/shk
    chown -R /var/www deployer:deployers





