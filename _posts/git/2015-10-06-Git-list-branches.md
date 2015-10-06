---
layout: post
title: "List branches ordered by date"
description: ""
category: [git]
tags: []
---
{% include JB/setup %}

    git for-each-ref --sort=-committerdate refs/heads/ --format='%(refname:short) %(committerdate:short) %(authorname)'

Example

    master 2015-09-17 Alfredo Roca
    shoppingcart 2015-09-17 Alfredo Roca
    ratings 2015-09-13 Alfredo Roca
    SHK_index_maker 2015-09-11 Alfredo Roca


    git branch -av

where 

    a all local & remote
    v verbose

Example

    Gastro_maker                    30c0a18 fixing html
    SHK_index_maker                 d10ac6c fixed translations
    al-feature1                     62dee12 conflicts resolved after pulling al-feature-1 branch


