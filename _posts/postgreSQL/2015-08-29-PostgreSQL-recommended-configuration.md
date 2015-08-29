---
layout: post
title: "PostgreSQL recommended configuration"
description: ""
category: [postgres, configuration]
tags: []
---
{% include JB/setup %}

<https://www.amberbit.com/blog/2014/2/4/postgresql-awesomeness-for-rails-developers/>

    vi /var/lib/pgsql/data/postgresql.conf


    listen_addresses = '*' # To which interface we should bind. '*'
                           # makes your PostgreSQL visible to the Internet

    max_connections = 200  # How many connections we should allow from
                           # our app, workers, delayed_jobs etc. combined
    shared_buffers = 16GB  # How much memory our PostgreSQL can use for
                           # buffers. Default value is insanely small.
                           # If PostgreSQL is the only thing we run on
                           # the machine, set it to 1/4 of available RAM
    work_mem = 10MB        # Increase the small value so the
                           # sorts perform better.
    maintenance_work_mem = 128MB 

    synchronous_commit = off # Speed up writes in exchange for possible
                             # loss of data (be careful here!)

    wal_buffers = 16MB # Basically how much data we can loose. But
                       # increasing makes things faster. Choose wisely.
                       # Also applies to settings below.
    wal_writer_delay = 400ms
    checkpoint_segments = 32
    checkpoint_timeout = 900s 
    checkpoint_completion_target = 0.9

    random_page_cost = 2.0 # Make planner use indices a bit more often
                           # vs. sequential table scans.

    effective_cache_size = 32GB  # How much memory in total our
                                 # PostgreSQL can use. Twice of
                                 # shared_buffers seems good.

