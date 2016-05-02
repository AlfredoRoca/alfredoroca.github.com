---
layout: post
title: "Implement MINA for deploying in existing app"
description: ""
category: [mina, deploy]
tags: []
---
{% include JB/setup %}

For instance, the app is 'helpjuicetest'

1. Add gems: mina, mina-multistage
1. Add config files: config/deploy.rb, config/deploy/staging.rb, ...
1. Create remote folder /var/www/app-name
1. [root@shk-1 www]# mkdir /var/www/helpjuicetest
1. [root@shk-1 www]# chown deployer:deployer /var/www/helpjuicetest/
1. ```mina staging setup:create_database```
1. ```mina staging setup```
1. => create folders structure
1. ```mina staging setup:upload_sensitive_files```
1. ```mina staging setup:thin```
1. => copies thin-staging.yml into server@/etc/thin/
1. ```mina staging deploy```

