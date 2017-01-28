---
layout: post
title: "Execute shell commands from ruby"
description: ""
category: [ruby,bash]
tags: []
---
{% include JB/setup %}

`test_shell_in_ruby.rb`

    system "bash", "-c", "echo 'running from bash shell!'"

Application:

**Remove folders under publc/uploads**

    uploads_dir = Rails.root.join('public/uploads')
    system "bash", "-c", "echo 'Borrando uploads... #{uploads_dir}'"
    system "bash", "-c", "rm -fr #{uploads_dir}/*"


