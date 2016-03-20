---
layout: post
title: "Bash initialisation files"
description: ""
category: [linux, bash]
tags: [initialisation, bash]
---
{% include JB/setup %}

Source: 

- <http://www.solipsys.co.uk/new/BashInitialisationFiles.html>

# Shell modes
See source for more info on other shells

- <https://github.com/sstephenson/rbenv/wiki/Unix-shell-initialization>


Which initialization files get sourced by the shell is dependent on the combination of modes in which a particular shell process runs. There are two main, non-exclusive modes:

    login - e.g. when user logs in to a system with non-graphical interface or via SSH;
    interactive - shell that has a prompt and whose standard input and error are both connected to terminals.

These modes can be manually activated with the following flags to bash/zsh:

    -l, --login
    -i

Here are some common operations and shell modes they result in:

    log in to a remote system via SSH: login + interactive
    execute a script remotely, e.g. ssh user@host 'echo $PWD' or with Capistrano: non‑login, non‑interactive
    execute a script remotely and request a terminal, e.g. ssh user@host -t 'echo $PWD': non-login, interactive
    start a new shell process, e.g. bash: non‑login, interactive
    run a script, bash myscript.sh: non‑login, non‑interactive
    run an executable with #!/usr/bin/env bash shebang: non‑login, non‑interactive
    open a new graphical terminal window/tab:
        on Mac OS X: login, interactive
        on Linux: non‑login, interactive


# Shell init files

In order of activation:

bash

    login mode:
        /etc/profile
        ~/.bash_profile, ~/.bash_login, ~/.profile (only first one that exists)
    interactive non-login:
        /etc/bash.bashrc (some Linux; not on Mac OS X)
        ~/.bashrc
    non-interactive:
        source file in $BASH_ENV

# Practical guide to which files get sourced when

    Opening a new Terminal window/tab:
        bash
            OS X: .bash_profile or .profile (1st found)
            Linux: .profile (Ubuntu, once per desktop login session) + .bashrc
    Logging into a system via SSH:
        bash: .bash_profile or .profile (1st found)
    Executing a command remotely with ssh or Capistrano:
        bash: source file in $BASH_ENV
    Remote git hook triggered by push over SSH:
        no init files get sourced, since hooks are running within a restricted shell
        PATH will be roughly: /usr/libexec/git-core:/usr/bin:/usr/bin:/bin:/usr/sbin:/sbin
