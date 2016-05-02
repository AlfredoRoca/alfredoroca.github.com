---
layout: post
title: "Implement MINA for deploying in existing app"
description: ""
category: [mina, deploy]
tags: []
---
{% include JB/setup %}

For instance, the app is 'helpjuicetest'

  1. Add gems in `Gemfile`
  ```gem 'mina'
  gem 'mina-multistage'
  ```
  1. Add config files: config/deploy.rb, config/deploy/staging.rb, ...
  1. Create remote folder `/var/www/app-name`
  1. [root@shk-1 www]# mkdir /var/www/helpjuicetest
  1. [root@shk-1 www]# chown deployer:deployer /var/www/helpjuicetest/
  1. ```mina staging setup:create_database```
  1. => create folders structure
  ```mina staging setup```
  ```mina staging setup:upload_sensitive_files```
  1. Copy `thin-staging.yml` into `server@/etc/thin/`
  ```mina staging setup:thin```
  ```mina staging deploy```

