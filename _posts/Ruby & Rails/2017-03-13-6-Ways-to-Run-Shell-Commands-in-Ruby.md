---
layout: post
title: "6 Ways to Run Shell Commands in Ruby"
description: ""
category: [ruby, shell]
tags: []
---
{% include JB/setup %}

<http://tech.natemurray.com/2007/03/ruby-shell-commands.html>
<http://stackoverflow.com/a/2400>
<http://stackoverflow.com/a/37329716> -> decision flowchart

    directorylist = %x[find . -name '*test.rb' | sort]

Which, in this case, will populate file list with all test files under the current directory, which you can process as expected:

    directorylist.each do |filename|
      filename.chomp!
      # work with file
    end
