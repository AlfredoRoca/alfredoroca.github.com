---
layout: post
title: "bash aliases"
description: ""
category: [linux, system]
tags: [linux, system, configuration]
---
{% include JB/setup %}

## easier navigation: .., …, …., ….., ~ and -
alias ..=“cd ..”
alias …=“cd ../..”
alias ….=“cd ../../..”
alias …..=“cd ../../../..”
alias ~=“cd ~” ## `cd` is probably faster to type though
alias – -=“cd -“

## shortcuts
alias d=“cd ~/Documents/Dropbox”
alias dl=“cd ~/Downloads”
alias dt=“cd ~/Desktop”
alias p=“cd ~/projects” ## shared folder with host (and sublime)
alias g=“git”
alias h=“history”
alias j=“jobs”
alias ga=“git add -A”
alias gc=“git commit -m $1”
alias gp=“git push origin master”
alias gph=“git push heroku master”
alias gs=“git status”
alias gl=“git log”
alias glb=“git log –oneline –decorate –graph –all”

colorflag=”–color”
## List all files colorized in long format
alias l=“ls -lF ${colorflag}“

## List all files colorized in long format, including dot files
alias la=“ls -laF ${colorflag}“

## List only directories
alias lsd=“ls -lF ${colorflag} | grep –color=never '^d'“
