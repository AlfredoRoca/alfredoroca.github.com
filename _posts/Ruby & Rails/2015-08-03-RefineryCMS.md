---
layout: post
title: "REFINERY CMS clean install"
description: ""
category: [rails, refinerycms]
tags: [new_install]
---
{% include JB/setup %}

- rvm
- ruby 2.2.1
- rails 4.2.3
- git
- exec js
- nodeJs


RVM
    gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
    \curl -sSL https://get.rvm.io | bash -s stable

set 'run command as login shell' in terminal preferences

new terminal window/tab

    rvm list known ==> list of versions
    rvm install 2.2.1
    rvm gemset create gemset_name    # create a gemset
    rvm ruby_version@gemset_name  # specify Ruby version and our new gemset
    gem install rails [-v rails_version  # install specific Rails version]

    sudo apt-get install git
    git config --global user.name "Alfredo Roca"
    git config --global user.email "alfredo.roca.mas@gmail.com"

    rails new my_new_application -m http://refinerycms.com/t/edge

If needed, a message will ask for JS Runtime:

    gem install execjs
    yum -y install nodejs  or sudo apt-get install nodejs

http://localhost:3000/refinery the 1st time

