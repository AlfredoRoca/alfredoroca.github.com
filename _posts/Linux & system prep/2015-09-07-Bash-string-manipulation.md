---
layout: post
title: "String manipulation in Bash"
description: ""
category: [bash]
tags: [string]
---
{% include JB/setup %}


Compare sorted:

    if [[ string1 > string2 ]]; then

Compare characters

    if [[ string1 = string2 ]]; then

Length of string

    myLen1=${#string1}

Parts of string (start at 0)

    part=${string1:start:length} --> string1 can not be a parameter, must be a var

Extract characters after some char

    after=${string#*somechar}
    after=${string#*.}  --> after the dot

