---
layout: post
title: "SSH passwordless authentication with public key"
description: ""
category: [linux, ssh]
tags: [public_key]
---
{% include JB/setup %}

You can see if you already have an SSH key by running:
  
    ls ~/.ssh

If you see any files with the .pub extension, then you already have a key generated; otherwise, you can generate one with the following command:
  
    ssh-keygen -C "your.email@example.com"

Note that we’re using the -C flag to create a label for our key for easy identification, and it’s typical to set it to your email address. When the command runs, it’ll prompt you to enter a path and passphrase, but the default path is fine. This will store both the private and public keys in the ~/.ssh/ directory, and they will be named according to the type of encryption used, the default being RSA authentication. Your private key will be stored in a file called id_rsa, while id_rsa.pub will hold your public key.

We’ll then need to add the newly generated keys to ssh-agent, which is a program that caches your private key and provides it to the SSH client program on your behalf. You can do so with the following command:
  
    ssh-add ~/.ssh/id_rsa

It’ll then ask you for the passphrase entered before.

Having our keys generated, we’re now ready to copy our public key over to the remote server using the ssh-copy-id command. Below is the full ssh-copy-id command that will copy our key over to the server:
  
    ssh-copy-id -i ~/.ssh/id_rsa.pub  name@remote-server

This will create a new file called authorized_keys on your remote server inside the ~/.ssh directory and store your public key in it. If you now try to ssh into your server, you should be authenticated and logged in without entering your password.
