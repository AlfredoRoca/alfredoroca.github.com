---
layout: post
title: "Ngnx netstat"
description: ""
category: [nginx, networking]
tags: [netstat]
---
{% include JB/setup %}

To show the current global count of connections in the queue, you can break this up per port and put this in exec statements in 'snmpd.conf' if you wanted to poll it from a monitoring application.

    netstat -an | grep -c SYN_RECV 


To track how close you are to the limit you would have to look at the average and max from the tx_queue and rx_queue fields from (on a regular basis):

    clear && cat /proc/net/tcp

    netstat -s | grep error

