---
layout: post
title: "How to use scp command with Vagrant machine"
description: ""
category: [vagrant]
tags: []
---
{% include JB/setup %}

Plugin for Vagrant

    vagrant plugin install vagrant-scp

Vagrant machine name:

    vagrant global-status
    =>
    id       name   provider state   directory                           
    ---------------------------------------------------------------------
    430eb6e  web    libvirt running /home/alfredo/eelp/eelp_environment 

Sintaxis:

    vagrant scp <some_local_file_or_dir> [vm_name]:<somewhere_on_the_vm>


Example

    vagrant scp web:/vagrant/db/migrate/20171023161310_add_helloumi_customer_id_to_client.rb /tmp
