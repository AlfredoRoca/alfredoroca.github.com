---
layout: post
title: "Read text files"
description: ""
category: [ruby]
tags: [read_files]
---
{% include JB/setup %}


Open, read lines and closes it after

    File.foreach('testfile') {|x| print "GOT", x }
