---
layout: post
title: "W8-W10 no reconoce CD/DVD-ROM"
description: ""
category: [windows]
tags: [regedit]
---
{% include JB/setup %}

#Windows 8/8.1/10 no reconoce la unidad de CD/DVD

SOLUCIÓN:

1. Comando Ejecutar (win+R)

2. ```regedit``` 

3. HKEY_LOCAL_MACHINE/SYSTEM/CurrentControlSet/Services/atapi

4. Nueva clave: Controller0

6. Con nuevo DWORD(32-bit) nombre EnumDevice1 valor 1

8. Salir y reiniciar
