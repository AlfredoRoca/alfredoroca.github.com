---
layout: post
title: "Useful bash commands"
description: ""
category: [bash, linux]
tags: []
---
{% include JB/setup %}

    alias tree="find . -print | sed -e 's;[^/]*/;|____;g;s;____|; |;g'"

    #webserver arranca un servidor http en la carpeta actual en el puerto 9000
    alias webserver="ruby -run -e httpd . -p 9000"

    # Para compartir un archivo en lan
    # share FILENAME te genera el link y te lo copia
    lohttp() { ifconfig | sed -n '/192.168/p' | cut -d' ' -f2 | awk '{print "http://"$1":9000"}'; }
    share() { echo "`lohttp`/$1" | pbcopy && echo "`lohttp`/$1"; }

