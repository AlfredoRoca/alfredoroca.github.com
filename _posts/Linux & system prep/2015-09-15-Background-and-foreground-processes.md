---
layout: post
title: "Background and foreground processes, managing and scheduling"
description: ""
category: [linux, proceses, monitoring, system, scheduling]
tags: [jobs, at]
---
{% include JB/setup %}

Source: LinuxFoundationX: LFS101x.2 Introduction to Linux

# Background and Foreground Processes

Linux supports background and foreground job processing. (A job in this context is just a command launched from a terminal window.) Foreground jobs run directly from the shell, and when one foreground job is running, other jobs need to wait for shell access (at least in that terminal window if using the GUI) until it is completed. This is fine when jobs complete quickly. But this can have an adverse effect if the current job is going to take a long time (even several hours) to complete.

In such cases, you can run the job in the background and free the shell for other tasks. The background job will be executed at lower priority, which, in turn, will allow smooth execution of the interactive tasks, and you can type other commands in the terminal window while the background job is running. By default all jobs are executed in the foreground. You can put a job in the background by suffixing & to the command, for example: 

To run in background

    updatedb &

You can either use CTRL-Z to suspend a foreground job or CTRL-C to terminate a foreground job and can always use the bg and fg commands to run a process in the background and foreground, respectively.

# Managing Jobs

The jobs utility displays all jobs running in background. The display shows the job ID, state, and command name, as shown here.

    jobs -l

The background jobs are connected to the terminal window, so if you log off, the jobs utility will not show the ones started from that window.

# Scheduling Future Processes using at

Suppose you need to perform a task on a specific day sometime in the future. However, you know you will be away from the machine on that day. How will you perform the task? You can use the ```at``` utility program to execute any **non-interactive** command at a specified time, as illustrated in the diagram:

    $ at now + 2 minute    -> 2 days, ...
    at> ls -al
    at> <EOT>   --> CTRL+D
    ==> job 10 at Tue Sep 15 10:06:00 2015
