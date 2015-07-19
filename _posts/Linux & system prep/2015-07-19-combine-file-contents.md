---
layout: post
title: "Combine file contents"
description: ""
category: Linux
tags: [paste, join, file manipulation, file combination]
---
{% include JB/setup %}

# Paste
Combine file contents joining rows with delimiters

    #file1.txt
    a345
    b2
    c457
    d3

    #file2.txt
    1
    2
    3
    4

    $ paste file1.txt file2.txt
    a345  1
    b2    2
    c457  3
    d3    4

    $ paste -d ':' file1.txt file2.txt
    a345:1
    b2:2
    c457:3
    d3:4

# join
Same as join checking common columns

    $ cat phonebook
    555-123-4567 Bob
    555-231-3325 Carol
    555-340-5678 Ted
    555-289-6193 Alice    

    $ cat directory
    555-123-4567 Anytown
    555-231-3325 Mytown
    555-340-5678 Yourtown
    555-289-6193 Youngstown    

The result of joining these two file is as shown in the output of the following command:

    $ join phonebook directory
    555-123-4567 Bob Anytown
    555-231-3325 Carol Mytown
    555-340-5678 Ted Yourtown
    555-289-6193 Alice Youngstown
