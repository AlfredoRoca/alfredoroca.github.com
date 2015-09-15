---
layout: post
title: "Linux monitoring tools - load average"
description: ""
category: [linux, monitoring, tools, system, load_average]
tags: []
---
{% include JB/setup %}

Source: LinuxFoundationX: LFS101x.2 Introduction to Linux

[Top] (/server/system/monitoring/2015/09/15/Monitoring-linux-with-top/)

w - uptime, load average and user processes

     09:48:49 up  2:01,  4 users,  load average: 0.33, 0.37, 0.37
    USER     TTY        LOGIN@   IDLE   JCPU   PCPU WHAT
    alfredo  :0        07:49   ?xdm?  20:53   0.25s gdm-session-worker [pam/gdm-password]
    alfredo  pts/0     07:52   23:32   7.12s  6.89s /home/alfredo/.rvm/rubies/ruby-2.2.0/bin/ruby bin/rails s
    alfredo  pts/1     07:52   12:11   0.91s  0.70s spring server | shk | started 1 hour ago                        
    alfredo  pts/2     08:26    1.00s  0.44s  0.00s w

uptime - uptime and load average

    09:49:46 up  2:02,  4 users,  load average: 0.47, 0.41, 0.39


##Interpreting Load Averages

The load average is displayed using three different sets of numbers, as shown in the following example:

The last piece of information is the average load of the system. Assuming our system is a single-CPU system, the 0.25 means that for the past minute, on average, the system has been 25% utilized. 0.12 in the next position means that over the past 5 minutes, on average, the system has been 12% utilized; and 0.15 in the final position means that over the past 15 minutes, on average, the system has been 15% utilized. If we saw a value of 1.00 in the second position, that would imply that the single-CPU system was 100% utilized, on average, over the past 5 minutes; this is good if we want to fully use a system. A value over 1.00 for a single-CPU system implies that the system was over-utilized: there were more processes needing CPU than CPU was available.

If we had more than one CPU, say a quad-CPU system, we would divide the load average numbers by the number of CPUs. In this case, for example, seeing a 1 minute load average of 4.00 implies that the system as a whole was 100% (4.00/4) utilized during the last minute.

Short term increases are usually not a problem. A high peak you see is likely a burst of activity, not a new level. For example, at start up, many processes start and then activity settles down. If a high peak is seen in the 5 and 15 minute load averages, it would may be cause for concern.

    load average: 0.47, 0.41, 0.39
                  1min  5min  15min

