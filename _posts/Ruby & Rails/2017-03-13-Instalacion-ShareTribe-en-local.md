---
layout: post
title: "instalación ShareTribe en local"
description: ""
category: [rails, sharetribe]
tags: []
---
{% include JB/setup %}

    git clone git@github.com:AlfredoRoca/sharetribe.git
    cd sharetribe/
    rvm --ruby-version use 2.3.1@sharetribe --create
    sudo yum remove epel-release
    sudo yum install nodejs npm
    node -v
    => v0.10.36

    Sphinx:
    http://freelancing-gods.com/thinking-sphinx/installing_sphinx.html
    Install from source: http://sphinxsearch.com/downloads/sphinx-2.2.11-release.tar.gz/thankyou.html
    gunzip sphinx-2.2.11-release.tar.gz
    tar -xf sphinx-2.2.11-release.tar
    cd sphinx-2.2.11-release/
    ./configure
    make
    sudo make install

    gem install bundler
    bundle install
    npm install -> no necesario, se instala después del nvm -> ver más adelante
    cp config/database.example.yml config/database.yml
    cp config/config.example.yml config/config.yml
    rake db:create
    rake db:structure:load
    bundle exec rake ts:index
    bundle exec rake ts:start

    # no necesario al instalar npm después de nvm
    en home directory: npm install check-node-version
    añadir al path:
    PATH=$PATH:/home/alfredo/node_modules/.bin

NVM: <https://github.com/creationix/nvm/releases/tag/v0.33.1>
download <https://github.com/creationix/nvm/archive/v0.33.1.tar.gz>

    gunzip nvm-0.33.1.tar.gz
    tar -xf nvm-0.33.1.tar
    cd nvm-0.33.1/
    . install.sh
    nvm --version
    => 0.33.1

    open new shell
    nvm install 6.9

    cd path/to/rails/application
    npm install

    foreman start -f Procfile.static

en otro shell: 
    
    foreman start -f Procfile.client-hot

en otro shell: 

    rails server

en otro shell: 

    bundle exec rake jobs:work

    gem install mailcatcher
