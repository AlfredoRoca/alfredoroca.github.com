---
layout: post
title: "Creating temporary files and folders"
description: ""
category: [bash, temporary]
tags: []
---
{% include JB/setup %}

#Creating Temporary Files and Directories

Consider a situation where you want to retrieve 100 records from a file with 10,000 records. You will need a place to store the extracted information, perhaps in a temporary file, while you do further processing on it.

Temporary files (and directories) are meant to store data for a short time. Usually one arranges it so that these files disappear when the program using them terminates. While you can also use touch to create a temporary file, this may make it easy for hackers to gain access to your data.

The best practice is to create random and unpredictable filenames for temporary storage. One way to do this is with the mktemp utility as in these examples:

The XXXXXXXX is replaced by the mktemp utility with random characters to ensure the name of the temporary file cannot be easily predicted and is only known within your program.

    **Command                                     Usage**

    TEMP=$(mktemp /tmp/tempfile.XXXXXXXX)       To create a temporary file
    TEMPDIR=$(mktemp -d /tmp/tempdir.XXXXXXXX)  To create a temporary directory

