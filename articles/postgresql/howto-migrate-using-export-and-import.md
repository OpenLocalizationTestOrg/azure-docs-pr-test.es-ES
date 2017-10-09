---
title: "aaaMigrate una base de datos mediante importación y exportación de base de datos de Azure para PostgreSQL | Documentos de Microsoft"
description: "Describe cómo extraer una base de datos PostgreSQL en un archivo de script e importar datos de hello en la base de datos de destino de Hola desde ese archivo."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 5ca4650782b02e1067c5a8a3710f2dfbc8c76063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-postgresql-database-using-export-and-import"></a>Migración de una base de datos de PostgreSQL mediante exportación e importación
Puede usar [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract una base de datos PostgreSQL en un archivo de script y [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport datos de hello en la base de datos de destino de Hola desde ese archivo.

## <a name="prerequisites"></a>Requisitos previos
toostep a través de este tooguide cómo, necesita:
- Un [base de datos de Azure para PostgreSQL server](quickstart-create-server-database-portal.md) con acceso de tooallow de reglas de firewall y la base de datos en él.
- La utilidad de línea de comandos [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) instalada.
- La utilidad de línea de comandos [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) instalada.

Siga estos pasos tooexport e importar la base de datos PostgreSQL.

## <a name="create-a-script-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a>Cree un archivo de script mediante pg_dump que contenga Hola datos toobe cargado
tooexport su existente PostgreSQL local de la base de datos o en un archivo de script sql de tooa de máquina virtual, ejecute hello siguiente comando en el entorno existente:
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
Por ejemplo, si tiene un servidor local y una base de datos llamada **testdb** en él:
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-hello-data-on-target-azure-database-for-postrgesql"></a>Importar datos de hello en la base de datos de destino para PostrgeSQL
Puede usar la línea de comandos de psql de Hola y Hola -d, datos de saludo de--dbname parámetro tooimport en la base de datos de Azure para PostrgeSQL se crea y cargar datos desde el archivo de sql de Hola.
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
Este ejemplo utiliza psql utilidad y un archivo de script denominado **testdb.sql** de datos de tooimport paso anterior en la base de datos de hello **mypgsqldb** en el servidor de destino  **mypgserver 20170401.postgres.database.azure.com**.
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a>Pasos siguientes
- toomigrate una base de datos PostgreSQL mediante el volcado de memoria y la restauración, vea [migrar la base de datos PostgreSQL mediante dump y restore](howto-migrate-using-dump-and-restore.md)
