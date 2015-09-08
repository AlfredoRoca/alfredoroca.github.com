---
layout: post
title: "67WEBS Procedures handbook"
description: ""
category: [67webs, procedures]
tags: []
---
{% include JB/setup %}


#Intercambio de documentos:

##Carpeta compartida en Dropbox

Se compartirá carpeta en Dropbox

* Nombre: como la aplicación
* Entre todos los colaboradores del proyecto con derechos para escritura
* Dentro de ésta se abrirán nuevas carpetas para alojamiento de
    * imagenes (fotos, logos, etc) 
    * especificaciones
    * propuestas de diseño
    * archivos de datos fuente
    * diseños finales

##Nombres de los archivos

```[prefijo - ]#NOMBRE_AUTOEXPLICATIVO - #FECHA_PUBLICACIÓN - Rev#REV```

Donde:

```#PREFIJO```: Opcional. Indica el estado del documento

* provisional -> contenido en desarrollo, no es definitivo
* final -> contenido listo para implementarse en beta o producción
* desarrollo -> en fase de implementación
* en beta -> contenido actualizado en beta
* producción -> operativo

```#NOMBRE_AUTOEXPLICATIVO```

- resume en 4 palabras el contenido del documento
- si hacen falta más de 4 palabras, hay que partir el documento en archivos más pequeños

```#FECHA_PUBLICACIÓN```: fecha en la que se sube el archivo a la carpeta compartida o cambia de prefijo

```#REVISIÓN```: número correlativo para distinguir versiones del mismo documento (ver las normas de modificación de contenidos)

##Modificación de contenidos en archivos de texto

Pueden modificarse documentos en los siguientes estados (prefijo del nombre):

- provisional
- final
- desarrollo
- en beta

No puede modificarse documento si está en fase:

- producción

Normas:

Nunca se eliminará contenido si está en "desarrollo" o "en beta".
Se marcará claramente la parte modificada mediante alguno de los siguientes métodos:

- tachar contenido
- cambiar letra a cursiva
- cambiar color letra a gris
- marcar como "antes"

Se marcará clarament el nuevo contenido mediante alguno de los siguientes métodos:

- cambiar letra a negrita
- remarcar con fondo amarillo
- marcar como "después"

El nuevo contenido se colocará inmediatamente después del viejo.

Si el alcance de la modificación afecta a prácticamente la totalidad del documento, se creará un nuevo documento aumentando el número de revisión.
En este caso no será necesario modificar el viejo y se notificará al equipo la publicación del nuevo documento.

##Modificación de contenidos gráficos

Podrán modificarse archivos en las fases

- provisional
- final

No podrán modificarse en fase

- desarrollo
- beta
- producción

Se sustituirá la parte modificada con lo nuevo.

#Diseño gráfico

El diseñador deberá aportar la siguiente información:

- Nombre de las fuentes utilizadas. Serán fuentes libres de derechos excepto el proyecto requiera una fuente que no pueda sustituirse por otra libre.
- Paleta de colores: muestra y código RGBA
- Texturas
- Iconos
- archivo PSD


Sobre el archivo PSD:

- Capas nombradas según su contenido para fácil identificación
- Se eliminarán las capas no utilizadas o, al menos, se marcarán para su selección rápida.


#Gestión de tareas

1. Se usará Trello
1. Las tarjetas contendrán tareas sencillas
1. Si es necesario dividirlas en varios pasos autónomos se explicitará en uno o varios checklists
1. Listas estándar:

    - Design
    - Functionality
    - Next
    - Pomodoro
    - System
    - Done
    - New ideas


1. Explicación estrategia/método de resolución:

    - En aquellas fichas que exijan una cierta elaboración o proceso, se explicará brevemente cómo se ha resuelto.
    - Para ello, se escribirá el proceso para incluirlo posteriormente en un post de la MemoWiki
    - Debe incluirse
        - el enunciado del problema,
        - el proyecto
        - los pasos seguidos
        - enlaces a las páginas consultadas


#Control de horas

1. Se usará ActivityLogger
1. Las fracciones de tiempo serán de 30 min (Pomodoros)


#Git workflow
1. Every minor significant change should be commited with proper description
1. Every method in models and controllers should be tested.

#Deploying workflow - resolve conflicts
http://alfredoroca.github.io/git/2015/08/03/resolve-conflict-and-test-remote-branch/

In the app folder, with local/master sync with origin/master

    git checkout -b remote_branch_to_test
    git pull remote_branch_to_test

==> asure local master is up to date

    git checkout master
    git fetch origin
    git pull origin master

==> open new branch to merge

    git checkout -b new_local_branch
    git merge remote_branch_to_test

==> resolve conflicts

    git commit -m "remote branch conflict resolved"
    git push origin new_local_branch

==> PR for new_local_branch merged with remote_branch_to_test with resolved conflicts. No conflicts, merge should be posible.

==> update local master again

    git checkout master
    git pull

==> deploy

    cap production deploy

==> Execute locally or the rails console

    rails c

==> Execute task to upload the version file that has to updated in development.

    cap production setup:upload_version_file

Version can be display in the '/version' route


#Deploying workflow - staging

##Rules to deploy to staging:

a branch:
- can only be deploy if the current deployment is master or itself
- on branch approval, PR to merge, merge to master, and deploy master to staging

master:
- can be deployed always overwriting any branch
- cap staging deploy:check_branch before deployment
- if there is a branch, arrange with branch owner before deployment


##How to push a branch to staging for live testing

code working on my-branch

update repo

    git push origin my-branch

deploy to staging server (it takes 10 min aprox)

    BRANCH=my-branch cap staging deploy

Last commit ref can be display in the '/version' route

##How to see remote logs

    cap staging logs:tail_rails
    cap staging logs:tail_thin

##Where are the logs

    /var/www/shk/current/log/staging.log    /var/www/log/thin.log

##How to connect to staging server

    ssh deployer@67.205.57.114

##Where is the web app

    /var/www/shk/current

##Where is the thin configuration file

    /etc/thin/shk.yml

##How stop/start/restart shk thin server instance

Connecting to server
 
    ssh deployer@...
    thin restart -C /etc/thin/shk.yml

Remotely
    cap staging deploy:restart

##How to know if there is some branch being tested in staging (and who did it)

    cap staging deploy:check_branch

        DEBUG [f48ca6b3] Command: cat /var/www/shk/current/BRANCH
        DEBUG [f48ca6b3]     master:alfredo
        DEBUG [f48ca6b3]    
        DEBUG [f48ca6b3] Finished in 0.299 seconds with exit status 0 (successful).

Deployed commit is in '/version' url

