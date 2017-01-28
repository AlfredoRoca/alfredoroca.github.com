---
layout: post
title: "Finding active sessions or connections in PostgreSQL"
description: ""
category: [postgresql]
tags: []
---
{% include JB/setup %}

    SELECT pid,datname,usename,application_name,client_hostname,client_port,backend_start,query_start,query FROM pg_stat_activity;

