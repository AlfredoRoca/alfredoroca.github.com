---
layout: post
title: "Squash my last X commits together using Git"
description: ""
category: [git]
tags: []
---
{% include JB/setup %}

Source: <http://stackoverflow.com/a/5201642/4191133>

`git rebase -i <after-this-commit>` and replace "pick" on the second and subsequent commits with "squash" or "fixup", as described in the manual

Ejemplo: se quiere squashear toda la rama br1 en un solo commit

    - df30a00 (origin/master, master) adds file 17
    | * 6237ede (HEAD, origin/br1, br1) adds file 16
    | * eb1d49a adds file 15
    | * 18ce4f5 adds file 14
    | * f0b0b12 adds file 13
    |/  
    - 5a987e8 adds file 10
    - 9e0c45d adds file 7
    - 3ebd271 squashing all...
    - 4b47eb8 1st commit - creating repo with readme
    (END)

    git checkout br1
    git rebase -i HEAD~4

    =>
    pick f0b0b12 adds file 13
    pick 18ce4f5 adds file 14
    pick eb1d49a adds file 15
    pick 6237ede adds file 16

... squash

    pick f0b0b12 adds file 13
    s 18ce4f5 adds file 14
    s eb1d49a adds file 15
    s 6237ede adds file 16

edit commit message

    => Successfully rebased and updated refs/heads/br1.

New tree

    - 7e8de63 (HEAD, br1) adds file 13
    | * df30a00 (origin/master, master) adds file 17
    |/  
    | * 6237ede (origin/br1) adds file 16
    | * eb1d49a adds file 15
    | * 18ce4f5 adds file 14
    | * f0b0b12 adds file 13
    |/  
    - 5a987e8 adds file 10
    - 9e0c45d adds file 7
    - 3ebd271 squashing all...
    - 4b47eb8 1st commit - creating repo with readme

Update remote fast-forwarding

    git push -f origin br1

final tree

    - 7e8de63 (HEAD, origin/br1, br1) adds file 13
    | * df30a00 (origin/master, master) adds file 17
    |/  
    - 5a987e8 adds file 10
    - 9e0c45d adds file 7
    - 3ebd271 squashing all...
    - 4b47eb8 1st commit - creating repo with readme
    (END)
