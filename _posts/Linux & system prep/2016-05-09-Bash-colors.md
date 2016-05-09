---
layout: post
title: "Bash colors"
description: ""
category: [bash]
tags: []
---
{% include JB/setup %}


Source: ready-for.sh from Linux-foundation

    #!/bin/bash
    RED="\e[0;31m"
    GREEN="\e[0;32m"
    YELLOW="\e[0;33m"
    BLUE="\e[0;34m"
    BACK="\e[0m"


    fail() {
        echo -e "${RED}FAIL${BACK}: $*"
    }
    #-------------------------------------------------------------------------------
    highlight() {
        echo -e "${YELLOW}$*${BACK}"
    }
    #-------------------------------------------------------------------------------
    dothis() {
        echo -e "${BLUE}$*${BACK}"
    }
    #-------------------------------------------------------------------------------
    debug() {
        [[ -z "$DEBUG" ]] || echo D: $* >&2
    }
      
    #===============================================================================
    # Check that we're running on Linux
    if [[ $(uname -s) != Linux || -n "$SIMULATE_FAILURE" ]] ; then
        fail "You need to run this on Linux machine you intend to use for the class, not on $(uname -s)"
        exit 1
    fi

    #===============================================================================
    # The minimum version of bash required to run this script is bash v4
    if bash --version | egrep -q 'GNU bash, version [1-3]' ; then
        fail "This script requires at least version 4 of bash"
        fail "You are running: $(bash --version | head -1)"
        exit 1
    fi

    #===============================================================================
    check_root() {
        if [[ $USER == root ]] ; then
            warn "This script is intended to be run as a regular user (not as root)"
            exit 1
        fi
    }
    #===============================================================================

