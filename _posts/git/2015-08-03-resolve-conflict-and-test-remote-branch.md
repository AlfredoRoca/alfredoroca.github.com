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
    git checkout -b new_local_branch_to_text
    git merge remote_branch_to_test
    
==> resolve conflicts