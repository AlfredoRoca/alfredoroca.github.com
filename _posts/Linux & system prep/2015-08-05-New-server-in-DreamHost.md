---
layout: post
title: "Creating server in DreamHost.com"
description: ""
category: [system, server]
tags: [new_install, rvm, git, rails, ruby, capistrano, deployment, ssh, linux, firewall, iptables, selinux, nginx, locate, postgres, dns]
---
{% include JB/setup %}

#DH Dashboard,
####Launch instance

Details:
- Flavour: subsonic
- Boot source: Boot from image (creates new volume)
- Image: Fedora 21
- Dev size: 80 GB (default for subsonic)
- Dev name: vda (default)

Access & security
- Import SSH public key and choose it
- Security group: default

#### Associate floating IP

OpenStack client for accessing through ssh console

[http://wiki.dreamhost.com/Launch_an_Instance_from_the_Command_Line](http://wiki.dreamhost.com/Launch_an_Instance_from_the_Command_Line){:target="_blank"}

[http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html){:target="_blank"}

and set environment variables using the OpenStack RC file: [http://docs.openstack.org/user-guide/common/cli_set_environment_variables_using_openstack_rc.html](http://docs.openstack.org/user-guide/common/cli_set_environment_variables_using_openstack_rc.html)

SSH login to floating IP addr


#1st configuration
Source: [https://www.digitalocean.com/community/tutorials/initial-setup-of-a-fedora-21-server](https://www.digitalocean.com/community/tutorials/initial-setup-of-a-fedora-21-server)

Source: [http://vladigleba.com/blog/2014/03/05/deploying-rails-apps-part-1-securing-the-server/](http://vladigleba.com/blog/2014/03/05/deploying-rails-apps-part-1-securing-the-server/)

The following done as root

##SYSTEM UPDATE
    yum update
    reboot

login again as superuser
    
##GROUPS AND USERS

###Create password for root
    passwd  => pw for root

###Deployers group with root access
    groupadd deployers

###Sudoers config
Create file /etc/sudoers.d/myuser with one or more lines like
    myuser ALL=(ALL) NOPASSWD: /usr/sbin/service nginx start,/usr/sbin/service nginx stop,/usr/sbin/service nginx restart

    chmod 0440 /etc/sudoers.d/myuser

###Add users to deployers group
    useradd -G deployers,rvm <deployer-name>
    userpw <deployer-name>

## SSH ACCESS

###Config port

    /etc/ssh/sshd_config
    => change Port #PORTNUMBER
    => PermitRootLogin no
    => last line UseDNS no
    => PasswordAuthentication yes

### Restart ssh service
    service restart sshd

### Check if ssh service is running
    ps aux | grep sshd
    service sshd status

### Check who is listening on port #PORT
    netstat -plant | grep #PORT

### Check open ports
    lsof -i

### Tell SELinux about the port    
    semanage port -a -t ssh_port_t -p tcp #PORTNUMBER

### SSH keys for developer
    ssh-key-gen -C "dev email"
    ssh-copy-id dev@your_server_ip 

### SSH keys for developer for deployment
    ssh-key-gen -C "dev email"   -> if there is no key pair in .ssh
    ssh-add -L (or cat id_rsa.pub)
    copy and add the pubkey to authorization_keys of deployer user name in remote server

### PROCEDURE FOR ADDING A NEW DEVELOPER TO DEPLOY
    1. Ask for his/her public key
    2. Add it to deployer/.ssh/authorization_keys file

### SSH keys for login user with custom file name 
    ssh-keygen -f custom-name -C "user email"
    => creates custom-name and custom-name.pub files
    ssh-copy-id -i custom-name user@your_server_ip 

## CONFIGURING THE TIME ZONE
Localize proper zone file in */usr/share/zoneinfo/*

    ln -sf /usr/share/zoneinfo/Europe/Madrid /etc/localtime

Check with

    date

## FIREWALL: IPTABLES
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

## LOCATE (optional)
    yum install -y mlocate
    updatedb

## NGINX
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

## SELINUX
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
    usermod -a -G rvm <deployer user>
    exit
    su <deployer user>
    gpg2 --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
    \curl -sSL https://get.rvm.io | bash -s stable
    source /home/alfredo/.rvm/scripts/rvm

    rvm info -> gives lot of info

### Ruby
As deployer user
    rvm install 2.2.1
    rvm gemset create gemset_name    # create a gemset
    rvm 2.2.1@gemset_name  # specify Ruby version and our new gemset

### Rails
As deployer user

Edit ~/.gemrc

    install: --no-document
    update: --no-document

    gem install rails [-v rails_version  # install specific Rails version]

## PostgreSQL

Source: [https://fedoraproject.org/wiki/PostgreSQL](https://fedoraproject.org/wiki/PostgreSQL)

As deployer user

    sudo yum install postgresql-server postgresql-contrib postgresql-devel
    sudo systemctl enable postgresql
    sudo postgresql-setup initdb
    sudo systemctl start postgresql
    sudo yum install pgadmin3   -> optional
    sudo su - postgres
    psql
    => postgres=# 
        \password postgres
        create user <user-name> with password <pw>;
        ALTER USER myuser WITH SUPERUSER;

    Alternative:
    $ sudo -u postgres psql postgres
    => postgres=#
            CREATE USER username WITH PASSWORD 'password';
            ALTER ROLE username WITH SUPERUSER;


Change /var/lib/pgsql/data/postgresql.conf 

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

## ExecJs runtime and NodeJS
As deployer user
    gem install execjs
    sudo yum -y install nodejs

## GIT
    sudo yum -y install git
    git --version
    sudo git config --global user.name "testuser"
    sudo git config --global user.email "testuser@example.com"
    sudo git config --list

    
## Rails App folder
    mkdir /var/www/shk
    chown -R /var/www deployer:deployers
    chmod 755 /var/www -R

## Capistrano

    # staging.rb
    server 'xx.xx.xx.xx', user: 'xxxxxxx', roles: %w{web app db}, primary: true, port: xxxx
    set :deploy_to, '/var/www/shk/'
    set :use_sudo, false
    set :rvm_ruby_version, '2.2.1@shk'
    set :rvm_custom_path, '/home/alfredo/.rvm' # rvm installed by alfredo!
    set :rails_env, 'staging'
    set :rake_env, 'staging'


    cap staging rvm:check
    cap staging rvm1:check
    cap staging check_write_permissions
    cap staging deploy:check
    cap staging setup:upload_sensitive_files
    cap staging deploy

Login server, cd /app_folder/releases/<release> and execute

    RAILS_ENV=staging bundle exec rake db:create
    RAILS_ENV=staging bundle exec rake db:seed

##Thin
As root
    gem install thin
    thin install
    mv /etc/rc.d/thin /etc/rc.d/init.d/
    /sbin/chkconfig --level 345 thin on

    service thin start
    => /usr/bin/env: ruby_executable_hooks: No such file or directory
    rvm @global do gem regenerate_binstubs
    gem regenerate_binstubs
    gem install executable-hooks
    gem regenerate_binstubs
    error not fixed ***********
    systemctl start thin.service -> does nothing

    ln -s `which ruby_executable_hooks` /usr/bin/ruby_executable_hooks
    ln -s `which ruby` /usr/bin/ruby
    login as deployer user
    rvm gemset use global
    gem install thin

    rvm use 2.2.0 --default

    =>
    /home/deployer/.rvm/rubies/ruby-2.2.1/lib/ruby/site_ruby/2.2.0/rubygems/dependency.rb:315:in `to_specs': Could not find 'thin' (>= 0) among 15 total gem(s) (Gem::LoadError)
    Checked in 'GEM_PATH=/.gem/ruby/2.2.0:/home/deployer/.rvm/rubies/ruby-2.2.1/lib/ruby/gems/2.2.0', execute `gem env` for more information
        from /home/deployer/.rvm/rubies/ruby-2.2.1/lib/ruby/site_ruby/2.2.0/rubygems/dependency.rb:324:in `to_spec'
        from /home/deployer/.rvm/rubies/ruby-2.2.1/lib/ruby/site_ruby/2.2.0/rubygems/core_ext/kernel_gem.rb:64:in `gem'
        from /home/deployer/.rvm/gems/ruby-2.2.0@shk/bin/thin:22:in `<main>'
        from /bin/ruby_executable_hooks:15:in `eval'
        from /bin/ruby_executable_hooks:15:in `<main>'