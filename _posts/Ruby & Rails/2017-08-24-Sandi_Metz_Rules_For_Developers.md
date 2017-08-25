---
layout: post
title: "Sandi Metz' Rules For Developers"
description: ""
category: [ruby, oop]
tags: []
---
{% include JB/setup %}

<https://robots.thoughtbot.com/sandi-metz-rules-for-developers>

# Here are the rules:

1. Classes can be no longer than one hundred lines of code.
2. Methods can be no longer than five lines of code.
3. Pass no more than four parameters into a method. Hash options are parameters.
4. Controllers can instantiate only one object. Therefore, views can only know about one instance variable and views should only send messages to that object (@object.collaborator.value is not allowed).

# When to break these rules

Paraphrasing Sandi, “You should break these rules only if you have a good reason or your pair lets you.” Your pair or the person reviewing your code are the people who you should ask.

Think of this as rule zero. It is immutable.

