---
layout: post
title: "Resolve a conflict and test a remote branch in local machine before merging"
description: ""
category: [git]
tags: [conflict_resolution, workflow]
---
{% include JB/setup %}


In the app folder, with local/master sync with origin/master

    git checkout -b remote_branch_to_test
    git pull remote_branch_to_test
    git checkout master

==> asure local master is up to date

    git fetch origin
    git pull origin master

==> open new branch to merge

    git checkout -b new_local_branch
    git merge remote_branch_to_test
    
==> resolve conflicts

    git commit -m "remote branch conflict resolved"
    git push origin new_local_branch

==> PR for new_local_branch merged with remote_branch_to_test with resolved conflicts

==> update local master again

  git checkout master
  git pull

