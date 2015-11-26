---
layout: post
title: "How to find and colour a pattern in a text file with grep"
description: ""
category: [linux, grep, file]
tags: [file_manipulation, grep]
---
{% include JB/setup %}


    grep -nT -B20 -A10 --color=always FATAL /var/www/shk/shared/log/production.log | less -R

Explicación:

    -n              mostrar números de línea
    T               tabular la impresión de la línea del texto
    -B20            mostrar 20 líneas previas a la ocurrencia
    -A10            mostrar 10 líneas posteriores a la incidencia
    --color=always  colorear cadena buscada
    FATAL           cadena buscsada
    | less          mostrar con less para poder desplazar
    -R              convertir códigos de colores en colores en la visualización con less

