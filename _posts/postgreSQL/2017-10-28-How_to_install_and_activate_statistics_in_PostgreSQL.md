---
layout: post
title: "How to install and activate statistics in PostgreSQL"
description: ""
category: [postgresql]
tags: []
---
{% include JB/setup %}

Hay que instalar la extensión `pg_stat_statemens`

<https://www.postgresql.org/docs/9.4/static/pgstatstatements.html>

    # postgresql.conf
    shared_preload_libraries = 'pg_stat_statements'

    pg_stat_statements.max = 10000
    pg_stat_statements.track = all
    log_statement = 'all'
    log_min_duration_statement = 100
    log_duration = on
