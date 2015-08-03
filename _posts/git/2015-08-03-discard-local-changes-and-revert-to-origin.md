---
layout: post
title: "Discard local changes and rever local master to origin"
description: ""
category: [git]
tags: [discard, revert, workflow]
---
{% include JB/setup %}

It blows away local changes, keeps you up to date with master BUT makes sure you don't just pull in new changes on top on current changes and make a mess. 

A lot safer in practice: Just be sure to add/commit/stash any work-in-progress first!

    git fetch; git reset --hard origin/master