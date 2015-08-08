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


Add to deploy.rake

    desc "updates BRANCH file to 'block' deploy when some other or other's branch is deployed"
    task :put_branch do
      branch_to_deploy = "#{fetch(:branch)}"
      on roles(:app) do
        execute "echo \"#{branch_to_deploy}:#{ENV['USER']}\" > #{release_path}/BRANCH"
      end
    end

    desc "read BRANCH file to let branch deploy when there is no other or other's branch deployed"
    task :check_branch do
      on roles(:app) do
        current_branch_info = capture("cat #{current_path}/BRANCH")
        current_branch_info ||= "master"
        current_branch = current_branch_info.split(':')[0]
        deployer = current_branch_info.split(':')[1]
        branch_to_deploy = "#{fetch(:branch)}"

        if branch_to_deploy != 'master' && current_branch != 'master' && current_branch != branch_to_deploy
          puts "*************************************************************"
          puts " Sorry, #{deployer} is already deploying the feature #{current_branch}"
          puts "*************************************************************"
          exit
        end
      end
    end

    if ENV['BRANCH']
      before "deploy", "deploy:check_branch"
    end
    after :published, "deploy:put_branch"


