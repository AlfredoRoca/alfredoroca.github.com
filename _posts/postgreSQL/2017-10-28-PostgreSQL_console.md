---
layout: post
title: "PostgreSQL console"
description: ""
category: [postgresql]
tags: []
---
{% include JB/setup %}

**Dónde está el fichero de configuración**

    # show config_file;
                 config_file
    -------------------------------------
     /var/lib/pgsql/data/postgresql.conf


**Dónde están los logs**

<http://blog.endpoint.com/2014/11/dear-postgresql-where-are-my-logs.html>

    psql -U <user> -d <database>
    #show log_destination;
     log_destination
    -----------------
     stderr

    #show logging_colector;
     logging_collector
    -------------------
     on

log directory is relative to data directory

    # show log_directory;
     log_directory
    ---------------
     pg_log

    #show data_directory;
       data_directory
    ---------------------
     /var/lib/pgsql/data

    # show log_filename;
         log_filename
    ----------------------
     postgresql-%G-%m.log


**Añadir la extensión a la base de datos**

<http://www.craigkerstiens.com/2013/01/10/more-on-postgres-performance/>

    psql -U <user> -d <database>

    # create extension pg_stat_statements;

Consulta estadísticas

    SELECT 
      (total_time / 1000 / 60) as total_minutes, 
      (total_time/calls) as average_time, 
      query 
    FROM pg_stat_statements 
    ORDER BY 1 DESC 
    LIMIT 100;

    **EXPLAIN ANALYZE query

    # explain analyze
    SELECT "cities".* FROM "cities" INNER JOIN "spaces" ON "spaces"."city_id" = "cities"."id" GROUP BY "cities"."id" HAVING count(*) > 0
    ;
                                                    QUERY PLAN
    ------------------------------------------------------------------------------------------------------------------
     HashAggregate  (cost=24.76..24.81 rows=4 width=52) (actual time=0.302..0.303 rows=3 loops=1)
       Filter: (count(*) > 0)
       ->  Hash Join  (cost=1.09..24.74 rows=4 width=52) (actual time=0.284..0.287 rows=4 loops=1)
             Hash Cond: (cities.id = spaces.city_id)
             ->  Seq Scan on cities  (cost=0.00..19.90 rows=990 width=52) (actual time=0.017..0.019 rows=4 loops=1)
             ->  Hash  (cost=1.04..1.04 rows=4 width=4) (actual time=0.024..0.024 rows=4 loops=1)
                   Buckets: 1024  Batches: 1  Memory Usage: 1kB
                   ->  Seq Scan on spaces  (cost=0.00..1.04 rows=4 width=4) (actual time=0.017..0.018 rows=4 loops=1)
     Total runtime: 0.437 ms
