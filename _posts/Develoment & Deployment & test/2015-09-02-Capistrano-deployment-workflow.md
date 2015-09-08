---
layout: post
title: "Capistrano deployment workflow"
description: ""
category: [capistrano, deployment]
tags: []
---
{% include JB/setup %}


At some point of the deployment ...

extracted from shk, pending to verify in saap

... 

    cd /var/www/saap/repo && ( GIT_ASKPASS=/bin/echo GIT_SSH=/tmp/saap/git-ssh.sh /usr/bin/env git remote update )
    cd /var/www/saap/repo && ( GIT_ASKPASS=/bin/echo GIT_SSH=/tmp/saap/git-ssh.sh /usr/bin/env mkdir -p /var/www/saap/releases/20150830071011 )
    cd /var/www/saap/repo && ( GIT_ASKPASS=/bin/echo GIT_SSH=/tmp/saap/git-ssh.sh /usr/bin/env git archive master | tar -x -f - -C /var/www/saap/releases/20150830071011 )
    cd /var/www/saap/repo && ( GIT_ASKPASS=/bin/echo GIT_SSH=/tmp/saap/git-ssh.sh /usr/bin/env git rev-list --max-count=1 --abbrev-commit master )
    ==> a09ab50 (deployed commit)
    cd /var/www/saap/releases/20150830071011 && /usr/bin/env echo "a09ab50" >> REVISION
    /usr/bin/env ln -s /var/www/saap/shared/public/assets /var/www/saap/releases/20150830071011/public/assets
    /usr/bin/env ln -s /var/www/saap/shared/log /var/www/saap/releases/20150830071011/log
    /usr/bin/env ln -s /var/www/saap/shared/tmp/pids /var/www/saap/releases/20150830071011/tmp/pids
    /usr/bin/env ln -s /var/www/saap/shared/tmp/cache /var/www/saap/releases/20150830071011/tmp/cache
    /usr/bin/env ln -s /var/www/saap/shared/tmp/sockets /var/www/saap/releases/20150830071011/tmp/sockets
    /usr/bin/env ln -s /var/www/saap/shared/public/uploads /var/www/saap/releases/20150830071011/public/uploads
    bundle install --binstubs /var/www/saap/releases/20150830062510/bin --path /var/www/saap/shared/bundle --without development test
    cd /var/www/saap/releases/20150830071011 && ( RAILS_ENV=production /var/www/saap//rvm1scripts/rvm-auto.sh . ~/.rvm/bin/rvm 2.2.0@saap do bundle exec rake assets:precompile )
    cd /var/www/saap/releases/20150830071011 && /usr/bin/env mkdir -p /var/www/saap/releases/20150830071011/assets_manifest_backup
    cd /var/www/saap/releases/20150830071011 && /usr/bin/env ls /var/www/saap/releases/20150830071011/public/assets/.sprockets-manifest*
    cd /var/www/saap/releases/20150830071011 && /usr/bin/env cp /var/www/saap/releases/20150830071011/public/assets/.sprockets-manifest-980ef43d6d732a56bab733fbc1df0132.json /var/www/saap/releases/20150830071011/assets_manifest_backup
    cd /var/www/saap/releases/20150830072549 && ( RAILS_ENV=production /var/www/saap//rvm1scripts/rvm-auto.sh . ~/.rvm/bin/rvm 2.2.0@saap do bundle exec rake db:migrate )
    /usr/bin/env ln -s /var/www/saap/releases/20150830072549 /var/www/saap/releases/current
    /usr/bin/env mv /var/www/saap/releases/current /var/www/saap
    echo "master:alfredo" > /var/www/saap/releases/20150830072549/BRANCH
    /home/deployer/.rvm/wrappers/ruby-2.2.0@saap/thin restart -C /etc/thin/saap.yml