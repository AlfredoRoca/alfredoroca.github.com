---
layout: post
title: "How to print status of all Fail2ban jails"
description: ""
category: [fail2ban]
tags: []
---
{% include JB/setup %}

    JAILS=`fail2ban-client status | grep "Jail list" | sed -E 's/^[^:]+:[ \t]+//' | sed 's/,//g'`
    for JAIL in $JAILS
    do
      fail2ban-client status $JAIL
    done

Equivalent for jail 'sshd' 

    fail2ban-client status sshd

