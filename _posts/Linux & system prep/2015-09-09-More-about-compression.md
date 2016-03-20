---
layout: post
title: "Working with compression"
description: ""
category: [linux, compression]
tags: [compression]
---
{% include JB/setup %}


# FILE COMPRESSION TOOLS

gzip
bzip2
xz
zip
zcat
zless
zdiff
zgrep

# join and compress files in current folder and subfolders and copmress it with gzip

    tar zcvf file.tar.gz *

# decompress and restores file.tar.gz in current folder

    tar xf file.tar.gz

# compress into a gzip file

    tar -zcvfp filename.tar.gz files

Where 

    z uses gzip
    c creates new file
    v verbose
    f specifies where to put the new compression (filename.tar.gz)
    p preserves permissions

# uncompress in current folder

    tar -xvpzf filename.tar

# uncompress in folder path_to_folder

    tar -xvpzf filename.tar -C path_to_folder

# list contents

    tar -ztvf filename.tar.gz

