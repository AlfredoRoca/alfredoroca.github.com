---
layout: post
title: "Redirecting errors in  Bash"
description: ""
category: [bash, debug]
tags: []
---
{% include JB/setup %}

    File stream   Description                                                                               File Descriptor
    stdin         Standard Input,
                  by default the keyboard/terminal for programs run from the command line                   0
    stdout        Standard output,
                  by default the screen for programs run from the command line                              1
    stderr        Standard error,
                  where output error messages are shown or saved                                            2


Append errors output to a file

    ./script 2>>file.txt
