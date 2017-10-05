---
layout: post
title: "Rake assets:precompile error with EXECJS runtime error"
description: ""
category: [rails, nodejs]
tags: [rake]
---
{% include JB/setup %}

Solution applied:

Update nodejs reinstalling (previously need uninstall) with 

    yum remove -y nodejs npm
    curl --silent --location https://rpm.nodesource.com/setup | bash -
    yum -y install nodejs 

Edited runtimes.rb (remove //U and replace UTF-16L with UTF-8)

    sudo vi /var/www/shk/shared/bundle/ruby/2.2.0/gems/execjs-2.6.0/lib/execjs/runtimes.rb

    JScript = ExternalRuntime.new(
      :name => "JScript",
      :command => "cscript //E:jscript //Nologo",
      :runner_path => ExecJS.root + "/support/jscript_runner.js",
      :encoding => 'UTF-8' # CScript with //U returns UTF-16LE
    )

