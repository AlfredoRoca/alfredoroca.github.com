---
layout: post
title: "Understanding SSHKit"
description: ""
category: [capistrano]
tags: [SSHKit]
---
{% include JB/setup %}

Source: [http://vladigleba.com/blog/2014/04/10/deploying-rails-apps-part-6-writing-capistrano-tasks/](http://vladigleba.com/blog/2014/04/10/deploying-rails-apps-part-6-writing-capistrano-tasks/)

#Understanding SSHKit

Capistrano 3 uses the Rake DSL (Domain Specific Language), which means if you ever wrote Rake tasks, you’ll be in familiar territory when writing Capistrano tasks; the only new thing you’ll need to learn about is SSHKit and the various methods it provides. SSHKit was actually developed and released with Capistrano 3, and it’s basically a lower-level tool that provides methods for connecting and interacting with remote servers; it does all the heavy lifting for Capistrano, in other words. There are four main methods you need to know about:

    on(): specifies the server to run on
    within(): specifies the directory path to run in
    as(): specifies the user to run as
    with(): specifies the environment variables to run with

Typically, you’ll start a task by using an on() method to specify the server on which you want your commands to run. Then you can use any combination of as(), within(), and with() methods, which are repeatable and stackable in any order, to provide additional details. For example, the upload_yml task we ran in setup.rake uses the on() method to specify that the resulting block of code should only be run on the application server. The seed_db task right below it has three parameters that specify how the resulting statement will run; it uses on(), within(), and with() to specify that the statement should only run on the application server, within the path specified, and with certain environment variables set.

Obviously, if SSHKit gives you methods to specify certain parameters that must be met before the actual statements are run, it should also give you methods to help you run those statements. That’s exactly what it does, and below are those methods:

    execute(): the workhorse that runs the commands on your server
    upload(): uploads a file from your local computer to your remote server
    capture(): executes a command and returns its output as a string
    puts(): writes the output returned by capture() to the screen
    background(): runs a command in the background
    test(): can be used for control flow since it works like the test command-line utility in Unix and returns false if its expression exits with a non-zero value
