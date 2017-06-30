---
layout: post
title: "RVM hook to binstubs"
description: ""
category: [rvm]
tags: []
---
{% include JB/setup %}

Source: [https://rvm.io/integration/bundler#global-executables](https://rvm.io/integration/bundler#global-executables)

<https://robots.thoughtbot.com/use-bundlers-binstubs>

Enabling hook (one time)

    rvm get head && rvm reload
    chmod +x $rvm_path/hooks/after_cd_bundler

Generating bundler stubs (binaries wrappers)

    cd /path/to/project
    bundle install --binstubs

With RVM integration enabled, the bin directory is added to your path each time you cd into a project directory with binstubs. That means you can just run rake. If you aren’t ignoring the bin directory in your project, you should do so:

    # .gitignore
    bin/

Now, you don’t have to type “bundle exec” again.