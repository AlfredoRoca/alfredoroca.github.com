---
layout: post
title: "Deploy branches with Capistrano"
description: ""
category: [capistrano, deployment]
tags: []
---
{% include JB/setup %}

# workflow
1. Create a pull request from your branch.
1. Deploy the branch using Capistrano.
1. Verify that the changes work.
1. Merge in the pull request.
1. Deploy the master branch using Capistrano.

Add to deploy.rb

    set :branch, ENV['BRANCH'] || "master"

    if ENV['BRANCH']
      before "deploy", "deploy:check_branch"
    end
    after "deploy:finalize_update", "deploy:put_branch"

    namespace :deploy do
      task :check_branch do
        current_branch_info = capture("cat #{current_path}/BRANCH; true")
        current_branch = current_branch_info.split(':')[0]
        deployer = current_branch_info.split(':')[1]

        if branch != 'master' && current_branch != 'master' && current_branch != branch
          puts "Sorry, #{deployer} is already deploying the feature #{current_branch}"
          exit
        end
      end

      task :put_branch do
        put "#{branch}:#{ENV['USER']}", "#{release_path}/BRANCH"
      end
    end
