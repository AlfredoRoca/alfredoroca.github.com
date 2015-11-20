---
layout: post
title: "SSL in local development"
description: ""
category: [rails, ssl]
tags: [development]
---
{% include JB/setup %}

#Using SSL in your local Rails environment

    http://www.railway.at/2013/02/12/using-ssl-in-your-local-rails-environment/ => thin server with SSL


how to set up a self-signed SSL certificate for your localhost: https://gist.github.com/trcarden/3295935

    openssl req -new -newkey rsa:2048 -sha1 -days 365 -nodes -x509 -keyout server.key -out server.crt

it will ask for: hostname must be localhost.ssl

    Country Name (2 letter code) [XX]:ES
    State or Province Name (full name) []:TARRAGONA    
    Locality Name (eg, city) [Default City]:TORREDEMBARRA
    Organization Name (eg, company) [Default Company Ltd]:67WEBS.COM
    Organizational Unit Name (eg, section) []:
    Common Name (eg, your name or your server's hostname) []:localhost.ssl
    Email Address []:alfredo.roca.mas@gmail.com

# move key to .ssl folder
    $ mkdir ~/.ssl && mv server.* ~/.ssl

Finally Add localhost.ssl to your hosts file

    echo "127.0.0.1 localhost.ssl" | sudo tee -a /private/etc/hosts


#Starting thin

    thin start -p 3001 --ssl --ssl-key-file ~/.ssl/server.key --ssl-cert-file ~/.ssl/server.crt

#sslmate

Secure your website the easy way with **sslmate**

SSLMate makes it easy to buy, deploy, and manage your SSL certs.

<https://sslmate.com/> => to automate buying and renewing SSL certificates