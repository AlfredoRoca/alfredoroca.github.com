---
layout: post
title: "Developer's machine setup"
description: ""
category: [linux, system]
tags: []
---
{% include JB/setup %}

'/home/developer'

File '.gitconfig'

    [user]
        name = Alfredo Roca
        email = alfredo.roca.mas@gmail.com
    [credential]
        helper = cache --timeout=3600
    [alias]
        cm = !git add -A && git commit -m
        co = checkout
    [push]
        default = simple

The following maybe it's done by RVM automatically

File '.rvmrc'

    rvm_path="$HOME/.rvm"

Create ssh keys with 'ssh-keygen'

'.bash_aliases' en GIST
'.bashrc' - git coloured prompt GIST

