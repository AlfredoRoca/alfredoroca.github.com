---
layout: post
title: "Scheduling jobs with cron"
description: ""
category: [linux, scheduling, system, delayed_jobs, cronjobs]
tags: [cron, crontab]
---
{% include JB/setup %}

Source: LinuxFoundationX: LFS101x.2 Introduction to Linux

##cron 

**cron** is a time-based scheduling utility program. It can launch routine background jobs at specific times and/or days on an on-going basis. **cron** is driven by a configuration file called ```/etc/crontab``` (**cron** table) which contains the various shell commands that need to be run at the properly scheduled times. There are both system-wide crontab files and individual user-based ones. Each line of a crontab file represents a job, and is composed of a so-called CRON expression, followed by a shell command to execute.

The ```crontab -e``` command will open the crontab editor to edit existing jobs or to create new jobs. Each line of the crontab file will contain 6 fields:
Field   Description   Values
MIN   Minutes   0 to 59
HOUR  Hour field  0 to 23
DOM   Day of Month  1-31
MON   Month field   1-12
DOW   Day Of Week   0-6 (0 = Sunday)
CMD   Command   Any command to be executed

Examples:

- The entry ```* * * * * /usr/local/bin/execute/this/script.sh``` will schedule a job to execute 'script.sh' every minute of every hour of every day of the month, and every month and every day in the week.

- The entry ```30 08 10 06 * /home/sysadmin/full-backup``` will schedule a full-backup at 8.30am, 10-June irrespective of the day of the week.


##Delayed jobs

Sources: 

<https://github.com/collectiveidea/delayed_job>

<http://www.sitepoint.com/delayed-jobs-best-practices/>

<http://www.sitepoint.com/new-rails-shiny-activejob/>

<http://www.sitepoint.com/dont-get-activejob/>

<http://blog.andolasoft.com/2013/04/4-simple-steps-to-implement-delayed-job-in-rails.html>


