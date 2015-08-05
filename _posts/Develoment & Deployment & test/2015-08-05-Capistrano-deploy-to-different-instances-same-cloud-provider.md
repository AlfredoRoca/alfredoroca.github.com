---
layout: post
title: "Capistrano deploy to different instances on same cloud provider"
description: ""
category: [capistrano, deployment]
tags: []
---
{% include JB/setup %}


Capistrano checks for unique server names. You can use ssh aliases in ~/.ssh/config to workaround the problem.

    server 'ssh_aliases1', roles: %w{web}
    server 'ssh_aliases2', roles: %w{web}

And add this to ~/.ssh/config

    Host ssh_aliases1
      HostName myservice.cloudapp.net
      User azureuser
      port 53458

    Host ssh_aliases2
      HostName myservice.cloudapp.net
      User azureuser
      port 62434


