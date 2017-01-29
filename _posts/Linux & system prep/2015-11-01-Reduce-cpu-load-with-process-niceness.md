---
layout: post
title: "Reduce cpu load during deployment controlling the niceness of linux processes"
description: ""
category: [linux, deployment, sysops]
tags: []
---
{% include JB/setup %}


```renice``` comes with linux-tools

To play with it, install ```mathomatic``` to create a very demanding task

    sudo yum install mathomatic mathomatic-tools

Generate a demanding task (calculate prime numbers in background task - notice the & symbol at the end)

    matho-primes 1 9999999999 > p1.txt &
    => process id 1
    matho-primes 1 9999999999 > p2.txt &
    => process id 2

    sudo renice 20 <process id 1>

Check with ```top``` command the cpu load for each process

Applied to Rails app deployment to reduce the assets compilation cpu demand

Wait for "node" process to start, get its pid and execute

    renice 20 node-pid


