---
layout: post
title: "Move a local branch to the head"
description: ""
category: [git]
tags: [git, rebase, fetch, conflict_resolution]
---
{% include JB/setup %}


          A---B---C localb
         /
    D---E---F---G master ---H---I---J origin/master


    * a09ab50 (origin/master, origin/HEAD) again modified two lines in deploy.rake
    * c45186b modified two lines in deploy.rake
    * 33fd82a Send email to maker and surfer while buy booing service and find food by menu and type
    * 8d76de0 Solved issue on maker page and send email while book maker food.
    * 4766b1e (master) blog page with comming soon mssage


    [master] git fetch
    [master] git diff master origin/master
    [master] git merge origin/master
    ==>
    Updating 4766b1e..a09ab50
    Fast-forward
    ... list of files ...
    [master] git checkout localb
    [localb] git rebase master
    ==> ... conflicts ...
    Resolve conflicts and 
    [localb] git add files
    [localb] git rebase --continue
    ==> ... conflicts ...
    Resolve conflicts and 
    [localb] git add files
    [localb] git rebase --continue


                  A'--B'--C' localb
                 /
    D---E---F---G master


    * a09ab50 (HEAD, origin/master, origin/HEAD, master) again modified two lines in deploy.rake
    * c45186b modified two lines in deploy.rake
    * 33fd82a Send email to maker and surfer while buy booing service and find food by menu and type
    * 8d76de0 Solved issue on maker page and send email while book maker food.
    * 4766b1e blog page with comming soon mssage

