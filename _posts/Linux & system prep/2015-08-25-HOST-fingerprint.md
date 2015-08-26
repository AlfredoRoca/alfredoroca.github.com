---
layout: post
title: "HOST fingerprint"
description: ""
category: [server, system, security]
tags: [RSA, ECDSA, fingerprint]
---
{% include JB/setup %}

    ssh-keygen -lf ~/.ssh/id_rsa.pub


ECDSA Fingerprint

At host

    ssh-keyscan -t ecdsa localhost > ecdsa_localhost
    ssh-keygen -lf ecdsa_localhost
    ==> 256 bf:da:61:24:00:d2:2e:9c:13:49:a2:a8:b6:64:e6:f1 localhost (ECDSA)

At client

    ssh-keygen -l -F host
    ==> 256 bf:da:61:24:00:d2:2e:9c:13:49:a2:a8:b6:64:e6:f1 46.101.186.164 (ECDSA)
