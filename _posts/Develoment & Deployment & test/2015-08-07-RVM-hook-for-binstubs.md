---
layout: post
title: "RVM hook to binstubs"
description: ""
category: [rvm, ]
tags: [rvm, binstubs, bundle]
---
{% include JB/setup %}

Source: [https://rvm.io/integration/bundler#global-executables](https://rvm.io/integration/bundler#global-executables)

Enabling hook
    rvm get head && rvm reload
    chmod +x $rvm_path/hooks/after_cd_bundler

Generating bundler stubs (binaries wrappers)

    cd /path/to/project
    bundle install --binstubs=./bundler_stubs

From now on, any project which was generated this way will automatically add *$PWD/bundler_stubs* to the PATH.


After that, when entering into the app folder, appear this:

  The bundler binstubs directory is in the current directory, which may be unsafe.
  Consider using rubygems-bundler instead => [https://github.com/mpapis/rubygems-bundler](https://github.com/mpapis/rubygems-bundler)
  Remove the BUNDLE_BIN line from .bundle/config to disable this prompt.
  Are you sure you want to add the bundler binstubs directory to the path?
  (anything other than 'Yes' will cancel) > 
