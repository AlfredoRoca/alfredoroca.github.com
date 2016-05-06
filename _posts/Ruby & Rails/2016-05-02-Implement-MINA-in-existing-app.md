---
layout: post
title: "Implement MINA for deploying in existing app"
description: ""
category: [mina, deploy]
tags: []
---
{% include JB/setup %}

For instance, the app is 'helpjuicetest'

Add gems in `Gemfile`

```
gem 'mina'

gem 'mina-multistage'

```

`bundle`

Add config files: `config/deploy.rb`, `config/deploy/staging.rb`, ...

Create remote folder `/var/www/app-name` and ssh to server

[root@shk-1 www]# `mkdir /var/www/helpjuicetest`

[root@shk-1 www]# `chown deployer:deployer /var/www/helpjuicetest/`


```mina staging setup```

```mina staging setup:create_database```

```mina staging setup:upload_sensitive_files```

Customize and copy `thin-staging.yml` into `server@/etc/thin/`

```mina staging setup:thin```

```mina staging deploy```

