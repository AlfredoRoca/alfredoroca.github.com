---
layout: post
title: "Automatic postgresql database backup"
description: ""
category: [postgres]
tags: [backup, pg_dump, psql]
---
{% include JB/setup %}

Fuente:

1. <https://wiki.postgresql.org/wiki/Automated_Backup_on_Linux>
2. <http://www.postgresql.org/docs/9.3/static/libpq-pgpass.html>

#BACKUP
El primer script crea backups diarios, semanales y mensuales para cada tabla del postgres.
El segundo explica el archivo de contraseñas de postgres para conexiones desatendidas.

Crear los archivos a partir de la fuente.
He puesto los archivos adjuntos en /home/alfredo/backups

Para forzar su ejecución ejecución:

    sudo sh pg_backup_rotated.sh -c ./pg_backup.config

Archivo de contraseñas postgres

    vi /root/.pgpass

    #hostname:port:database:username:password
    # ej para todas las BD
    *:*:*:alfredo:alfredo

    chmod 600 .pgpass”

Si se guarda archivo .pgpass en otro lugar declarar variable

    PGPASSFILE=/home/alfredo/backups/.pgpass

Con los datos de configuración adjuntos guarda 7 diarios y 5 semanales (los viernes), y 1 mensual (dia 1 del mes)

cronjob como root para que ejecute el script a las 4.30 cada día.

    30 04 * * * /home/alfredo/backups/pg_backup_rotated.sh -c /home/alfredo/backups/pg_backup.config

#RESTORE

Eliminar si existe y crear la BD con
    $ dropdb dbname
    $ createdb -T template0 dbname

Crear mismo role si no existe ya
    $ psql -U alfredo postgres
    # create role alfredo superuser;

Importar datos del backup "filename"; pero para si hay error

    $ gunzip -c filename.sql.gz | psql –set ON_ERROR_STOP=on dbname

O
    $ psql –set ON_ERROR_STOP=on dbname < filename.sql

