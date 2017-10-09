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
# <a name="migrate-your-postgresql-database-using-export-and-import"></a><span data-ttu-id="bfcf3-103">Migración de una base de datos de PostgreSQL mediante exportación e importación</span><span class="sxs-lookup"><span data-stu-id="bfcf3-103">Migrate your PostgreSQL database using export and import</span></span>
<span data-ttu-id="bfcf3-104">Puede usar [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract una base de datos PostgreSQL en un archivo de script y [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport datos de hello en la base de datos de destino de Hola desde ese archivo.</span><span class="sxs-lookup"><span data-stu-id="bfcf3-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract a PostgreSQL database into a script file and [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport hello data into hello target database from that file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfcf3-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bfcf3-105">Prerequisites</span></span>
<span data-ttu-id="bfcf3-106">toostep a través de este tooguide cómo, necesita:</span><span class="sxs-lookup"><span data-stu-id="bfcf3-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="bfcf3-107">Un [base de datos de Azure para PostgreSQL server](quickstart-create-server-database-portal.md) con acceso de tooallow de reglas de firewall y la base de datos en él.</span><span class="sxs-lookup"><span data-stu-id="bfcf3-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules tooallow access and database under it.</span></span>
- <span data-ttu-id="bfcf3-108">La utilidad de línea de comandos [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) instalada.</span><span class="sxs-lookup"><span data-stu-id="bfcf3-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) command-line utility installed</span></span>
- <span data-ttu-id="bfcf3-109">La utilidad de línea de comandos [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) instalada.</span><span class="sxs-lookup"><span data-stu-id="bfcf3-109">[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) command-line utility installed</span></span>

<span data-ttu-id="bfcf3-110">Siga estos pasos tooexport e importar la base de datos PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="bfcf3-110">Follow these steps tooexport and import your PostgreSQL database.</span></span>

## <a name="create-a-script-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a><span data-ttu-id="bfcf3-111">Cree un archivo de script mediante pg_dump que contenga Hola datos toobe cargado</span><span class="sxs-lookup"><span data-stu-id="bfcf3-111">Create a script file using pg_dump that contains hello data toobe loaded</span></span>
<span data-ttu-id="bfcf3-112">tooexport su existente PostgreSQL local de la base de datos o en un archivo de script sql de tooa de máquina virtual, ejecute hello siguiente comando en el entorno existente:</span><span class="sxs-lookup"><span data-stu-id="bfcf3-112">tooexport your existing PostgreSQL database on-premises or in a VM tooa sql script file, run hello following command in your existing environment:</span></span>
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
<span data-ttu-id="bfcf3-113">Por ejemplo, si tiene un servidor local y una base de datos llamada **testdb** en él:</span><span class="sxs-lookup"><span data-stu-id="bfcf3-113">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-hello-data-on-target-azure-database-for-postrgesql"></a><span data-ttu-id="bfcf3-114">Importar datos de hello en la base de datos de destino para PostrgeSQL</span><span class="sxs-lookup"><span data-stu-id="bfcf3-114">Import hello data on target Azure Database for PostrgeSQL</span></span>
<span data-ttu-id="bfcf3-115">Puede usar la línea de comandos de psql de Hola y Hola -d, datos de saludo de--dbname parámetro tooimport en la base de datos de Azure para PostrgeSQL se crea y cargar datos desde el archivo de sql de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfcf3-115">You can use hello psql command line and hello -d, --dbname parameter tooimport hello data into Azure Database for PostrgeSQL we created and load data from hello sql file.</span></span>
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
<span data-ttu-id="bfcf3-116">Este ejemplo utiliza psql utilidad y un archivo de script denominado **testdb.sql** de datos de tooimport paso anterior en la base de datos de hello **mypgsqldb** en el servidor de destino  **mypgserver 20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="bfcf3-116">This example uses psql utility and a script file named **testdb.sql** from previous step tooimport data into hello database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a><span data-ttu-id="bfcf3-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bfcf3-117">Next steps</span></span>
- <span data-ttu-id="bfcf3-118">toomigrate una base de datos PostgreSQL mediante el volcado de memoria y la restauración, vea [migrar la base de datos PostgreSQL mediante dump y restore](howto-migrate-using-dump-and-restore.md)</span><span class="sxs-lookup"><span data-stu-id="bfcf3-118">toomigrate a PostgreSQL database using dump and restore, see [Migrate your PostgreSQL database using dump and restore](howto-migrate-using-dump-and-restore.md)</span></span>
