---
layout: post
title: "Cómo he creado una campaña de correo Mailchimp"
description: ""
category: [mailchimp]
tags: []
---
{% include JB/setup %}

Antecedentes:

La importación de CSV generado por Google Contacts no sirve para Mailchimp. 

La importación mediante servicio integrado Google Contacts no discrimina grupos o círculos de Google.

Para solucionarlo, he creado una cuenta "B" exclusiva para hacer de puente entre los contactos de la cuenta principal "A" y Mailchimp.

Procedimiento:

- Partimos del grupo "Suscriptores" en la cuenta de Gmail "A".
- Exportar el grupo "Suscriptores" de "A" a CSV Google.
- Importar "CSV" en la cuenta "B".

En Mailchimp, 

- crear nueva lista la primera vez.
- Importar contactos como "Suscribed" usando servicio integrado "Google Contacts" y conectar a la cuenta "B"

Comportamiento:

- Los nuevos contactos se añaden a la lista.
- Los contactos existentes se mantienen en su Marketing status (suscribed, unsuscribed, cleared)
- Los contactos que ya no aparecen en la importación se mantienen en la lista, no se eliminan.
