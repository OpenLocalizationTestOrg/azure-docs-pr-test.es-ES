---
title: "aaaHow tooDump y restauración de base de datos de Azure para PostgreSQL | Documentos de Microsoft"
description: "Describe cómo tooextract un PostgreSQL base de datos en un archivo de volcado de memoria y restaurar base de datos de PostgreSQL de Hola desde un archivo de almacenamiento creado por pg_dump en base de datos de Azure para PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 9ad28e9dec3927b0f80b5e6bab6423cc944f5156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a>Migración de una base de datos de PostgreSQL mediante volcado y restauración
Puede usar [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract una base de datos PostgreSQL en un archivo de volcado de memoria y [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) toorestore base de datos de PostgreSQL de Hola desde un archivo de almacenamiento creado por pg_dump.

## <a name="prerequisites"></a>Requisitos previos
toostep a través de este tooguide cómo, necesita:
- Un [base de datos de Azure para PostgreSQL server](quickstart-create-server-database-portal.md) con acceso de tooallow de reglas de firewall y la base de datos en él.
- Utilidades de línea de comandos [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) y [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) instaladas

Siga estos pasos toodump y restaurar la base de datos PostgreSQL:

## <a name="create-a-dump-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a>Cree un archivo de volcado de memoria mediante pg_dump que contenga Hola datos toobe cargado
tooback de una existente PostgreSQL local de la base de datos o en una máquina virtual, ejecute el siguiente comando de Hola:
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
Por ejemplo, si tiene un servidor local y una base de datos llamada **testdb** en él:
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-hello-data-into-hello-target-azure-database-for-postrgesql-using-pgrestore"></a>Restaurar los datos de hello en base de datos de destino de Hola para PostrgeSQL con pg_restore
Una vez haya creado la base de datos de destino de hello, puede usar comandos de pg_restore de Hola y Hola -d, datos de saludo--dbname parámetro toorestore en base de datos de destino de Hola desde el archivo de volcado de memoria de hello.
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
En este ejemplo, restaurar los datos de Hola desde el archivo de volcado de memoria de hello **testdb.dump** en la base de datos de hello **mypgsqldb** en el servidor de destino **mypgserver-20170401.postgres.database.azure.com**.
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a>Pasos siguientes
- toomigrate una base de datos PostgreSQL mediante la exportación e importación, consulte [migrar la base de datos PostgreSQL utilizando exportar e importar](howto-migrate-using-export-and-import.md)
