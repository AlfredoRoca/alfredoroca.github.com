---
layout: post
title: "SysAdmin strace for tracing rake assets precompilation"
description: ""
category: [sysops]
tags: []
---
{% include JB/setup %}

If the server is Linux-based, `strace` is great for figuring out
what's going on with a "stuck" process.

    $ strace -e file rake assets:precompile
    ... runs `rake assets:precompile`, printing out any time a file is
    opened or checked

    $ strace -e file,network,process rake assets:precompile
    ... the same as above, but also printing network process and subcommands run

    $ strace -e file,process -f rake assets:precompile
    ... the -f parameter follows forks -- in case it's not `rake` but a
    subshell that you're interested in

    $ strace -p 1234
    ... connect to pid 1234 and start tracing
