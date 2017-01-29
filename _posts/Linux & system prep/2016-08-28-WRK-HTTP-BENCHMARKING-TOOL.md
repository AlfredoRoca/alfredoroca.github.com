---
layout: post
title: "WRK: HTTP BENCHMARKING TOOL"
description: ""
category: [linux, benchmarking, sysops]
tags: [wrk]
---
{% include JB/setup %}


<https://github.com/wg/wrk>

<https://github.com/wg/wrk/wiki/Installing-Wrk-on-Linux>

    [root@shk-1 wrk]# wrk -t12 -c400 -d30s https://shk.67webs.com/
    Running 30s test @ https://shk.67webs.com/
      12 threads and 400 connections
      Thread Stats   Avg      Stdev     Max   +/- Stdev
        Latency    79.74ms   28.52ms 343.18ms   72.84%
        Req/Sec   166.34    103.38   626.00     65.31%
      52797 requests in 30.08s, 17.40MB read
      Socket errors: connect 0, read 0, write 0, timeout 21
      Non-2xx or 3xx responses: 52776
    Requests/sec:   1754.94
    Transfer/sec:    592.20KB

    [root@shk-1 wrk]# ifstat -t 30
    #kernel
    Interface        RX Pkts/Rate    TX Pkts/Rate    RX Data/Rate    TX Data/Rate 
                     RX Errs/Drop    TX Errs/Drop    RX Over/Rate    TX Coll/Rate 
    eth0              187852 0        187095 0        37937K 0        37910K 0     
                           0 0             0 0             0 0             0 0  


    location / {
    ...
         aio threads;
    }



    [root@shk-1 nginx]# wrk -t12 -c400 -d30s https://shk.67webs.com/
    Running 30s test @ https://shk.67webs.com/
      12 threads and 400 connections
      Thread Stats   Avg      Stdev     Max   +/- Stdev
        Latency    81.30ms   28.87ms 828.91ms   70.37%
        Req/Sec   160.39    100.30   680.00     71.94%
      49475 requests in 30.08s, 16.35MB read
      Socket errors: connect 0, read 0, write 0, timeout 20
      Non-2xx or 3xx responses: 49454
    Requests/sec:   1644.60
    Transfer/sec:    556.53KB
    [root@shk-1 nginx]# ifstat -t 30
    #kernel
    Interface        RX Pkts/Rate    TX Pkts/Rate    RX Data/Rate    TX Data/Rate 
                     RX Errs/Drop    TX Errs/Drop    RX Over/Rate    TX Coll/Rate 
    eth0              177556 0        176744 0        35738K 0      18446744069450M 0     
                           0 0             0 0             0 0             0 0  

