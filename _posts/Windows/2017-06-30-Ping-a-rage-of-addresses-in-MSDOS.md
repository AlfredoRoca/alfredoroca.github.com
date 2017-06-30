---
layout: post
title: "Ping a range of addresses in MSDOS"
description: ""
category: [windows]
tags: []
---
{% include JB/setup %}

    C:\>for /L %i in (1,1,255) do @ping 192.168.2.%i -n 1 |@find "TTL" >>PINGOK.LOG|echo %i

Explanation:

%i vale 1 (primer valor del for)
el segundo valor = incremento en este caso vamos de 1 en 1.
tercer valor es el final.

    for /L %i in (1,1,255)


ejecuta ping a la ip especificada con el valor de %i y envia 1 solo paquete.

    @ping 192.168.0.%i -n 1

el resultado del ping busca el valor TTL y si existe lo pasa al fichero pingok.log.

    |@find “TTL” >>pingok.log

para ver el proceso

    |echo %i


