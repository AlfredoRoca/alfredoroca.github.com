---
layout: post
title: "Ping a range of addresses in MSDOS"
description: ""
category: [windows]
tags: []
---
{% include JB/setup %}

    C:\>for /L %i in (1,1,255) do @ping 192.168.2.%i -n 1 |@find "TTL" >> PINGOK.LOG | echo %i

Explanation:

%i starts at 1 (1st parameter for loop)

2nd parameter = increment, in this case is 1

3rd parameter = last index value

    for /L %i in (1,1,255)


executes ping to the ip with %i and send only 1 packet

    @ping 192.168.0.%i -n 1

searchs for TTL in result and writes it in file `pingok.log`.

    |@find “TTL” >> pingok.log

prints the index to see the progress

    |echo %i


