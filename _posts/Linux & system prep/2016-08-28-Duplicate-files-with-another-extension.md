---
layout: post
title: "Duplicate files with another extension"
description: ""
category: [linux, bash]
tags: [find, read, cut]
---
{% include JB/setup %}


    find *.erb > list_of_files && cut -d. -f1 list_of_files | while read -r; do  cp "$REPLY.html.erb" "$REPLY.it.html.erb"; done && rm list_of_files


Alternative:


    find . -name "*.txt" | while read a; do echo cp "$a" "`dirname $a``basename $a .txt`.texto"; done                         

`dirname` devuelve la carpeta                         

`basename` devuelve el nombre de fichero sin la carpeta

`basename` con la extension elimina la extension                         

    find . -name "*.txt" | while read a; do echo cp "$a" "`dirname $a``basename $a .html.erb`.it.html.erb"; done                        

con el basename $a .html.erb le quito la extension y al añadir después del apostrofe inverso el ".it.html.erb" se lo añade al resultado

