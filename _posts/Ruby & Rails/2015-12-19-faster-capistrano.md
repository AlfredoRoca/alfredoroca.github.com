---
layout: post
title: "Faster Capistrano"
description: ""
category: [rails, capistrano]
tags: []
---
{% include JB/setup %}

  task :precompile, :roles => :web, :except => { :no_release => true } do
    run_locally("rm -rf public/assets/*")
    run_locally("bundle exec rake assets:precompile")
    servers = find_servers_for_task(current_task)
    port_option = port ? " -e 'ssh -p #{port}' " : ''
    servers.each do |server|
      run_locally("rsync --recursive --times --rsh=ssh --compress --human-readable #{port_option} --progress public/assets #{user}
@#{server}:#{shared_path}")
    end
  end

