---
layout: post
title: "Remove domains from letsencrypt"
description: ""
category: [letsencrypt]
tags: []
---
{% include JB/setup %}

Source: https://community.letsencrypt.org/t/remove-domain-not-required-from-cert/14010/6

Before you start, create a backup of `/etc/letsencrypt` just in case, i.e. 

    cp /etc/letsencrypt/ /etc/letsencrypt.backup -r

Let's say you have two certificate lineages, `foo.example.com` and `bar.example.com`.
The certificates for `foo.example.com` are stored in `/etc/letsencrypt/live/foo.example.com`, for `bar.example.com` in `/etc/letsencrypt/live/bar.example.com`.

If you're unsure which lineage contains which domains, try this for all subdirectories in `/etc/letsencrypt/live`:

    openssl x509 -in /etc/letsencrypt/live/example.com/cert.pem -text -noout | grep DNS

If you want to remove everything in the bar.example.com lineage (that is, bar.example.com and any other domains covered by that certificate), you can delete the following files:

    rm -rf /etc/letsencrypt/live/bar.example.com/
    rm -rf /etc/letsencrypt/archive/bar.example.com/
    rm /etc/letsencrypt/renewal/bar.example.com.conf

That's it.

If you just want to remove one (or a couple) of domains that were included in the `bar.example.com` - let's say you don't want `sample.bar.example.com`, but still need `othersample.bar.example.com` and `bar.example.com` - you can use the same `rm` commands, and afterwards request a new certificate using onlythe domains you want to keep. Full example (with webroot, but you can of course use whatever you initially used to get the certificates):

    rm -rf /etc/letsencrypt/live/bar.example.com/
    rm -rf /etc/letsencrypt/archive/bar.example.com/
    rm /etc/letsencrypt/renewal/bar.example.com.conf
    # this will install a new certificate in bar.example.com, excluding sample.bar.example.com
    ./letsencrypt-auto certonly --webroot -d bar.example.com -d othersample.bar.example.com -w /var/www/html/

If anything goes wrong while you're doing this, run `mv /etc/letsencrypt /etc/letsencrypt.broken && mv /etc/letsencrypt.backup/ /etc/letsencrypt` and you're back where you started. 
