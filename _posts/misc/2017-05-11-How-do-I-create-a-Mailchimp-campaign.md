---
layout: post
title: "Cómo he creado una campaña de correo Mailchimp"
description: ""
category: [mailchimp]
tags: []
---
{% include JB/setup %}

Lista de contactos "Suscriptores" inicial en la cuenta de Gmail "A".
Exportar el grupo "Suscriptores" de "A" a CSV Google.
Crear nueva cuenta "B" en google exclusiva para Mailchimp.
Importar "CSV" en la cuenta "B".

En Mailchimp, crear nueva lista la primera vez.
Importar contactos como "Suscribed" usando servicio integrado "Google Contacts" y conectar a la cuenta "B"

Los nuevos contactos se añaden a la lista.
Los contactos existentes se mantienen en su estatus.
Los contactos que ya no aparecen en la importación se mantienen en la lista.
