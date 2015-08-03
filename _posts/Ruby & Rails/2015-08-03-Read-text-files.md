---
layout: post
title: "Read text files"
description: ""
category: [Ruby]
tags: [read files]
---
{% include JB/setup %}


Open, read lines and closes it after

    File.foreach('testfile') {|x| print "GOT", x }
