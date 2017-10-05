---
title: "Migración de una base de datos mediante importación y exportación en Azure Database for PostgreSQL | Microsoft Docs"
description: "Describe cómo extraer una base de datos PostgreSQL en un archivo de script e importar los datos en la base de datos de destino desde ese archivo."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 5e306d516d04789e4526bfd09bf99139b83573ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="migrate-your-postgresql-database-using-export-and-import"></a><span data-ttu-id="8b8ae-103">Migración de una base de datos de PostgreSQL mediante exportación e importación</span><span class="sxs-lookup"><span data-stu-id="8b8ae-103">Migrate your PostgreSQL database using export and import</span></span>
<span data-ttu-id="8b8ae-104">Puede usar [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) para extraer una base de datos PostgreSQL en un archivo de script y [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) para importar los datos en la base de datos de destino desde ese archivo.</span><span class="sxs-lookup"><span data-stu-id="8b8ae-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) to extract a PostgreSQL database into a script file and [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) to import the data into the target database from that file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b8ae-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8b8ae-105">Prerequisites</span></span>
<span data-ttu-id="8b8ae-106">Para seguir esta guía, necesitará:</span><span class="sxs-lookup"><span data-stu-id="8b8ae-106">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="8b8ae-107">Un [servidor de Azure Database for PostgreSQL](quickstart-create-server-database-portal.md) con reglas de firewall para permitir el acceso a las bases de datos que hay en él.</span><span class="sxs-lookup"><span data-stu-id="8b8ae-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules to allow access and database under it.</span></span>
- <span data-ttu-id="8b8ae-108">La utilidad de línea de comandos [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) instalada.</span><span class="sxs-lookup"><span data-stu-id="8b8ae-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) command-line utility installed</span></span>
- <span data-ttu-id="8b8ae-109">La utilidad de línea de comandos [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) instalada.</span><span class="sxs-lookup"><span data-stu-id="8b8ae-109">[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) command-line utility installed</span></span>

<span data-ttu-id="8b8ae-110">Siga estos pasos para exportar e importar la base de datos de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8b8ae-110">Follow these steps to export and import your PostgreSQL database.</span></span>

## <a name="create-a-script-file-using-pgdump-that-contains-the-data-to-be-loaded"></a><span data-ttu-id="8b8ae-111">Creación de un archivo de script mediante pg_dump con los datos que se van a cargar</span><span class="sxs-lookup"><span data-stu-id="8b8ae-111">Create a script file using pg_dump that contains the data to be loaded</span></span>
<span data-ttu-id="8b8ae-112">Para exportar la base de datos de PostgreSQL existente en el entorno local o en una máquina virtual a un archivo de script de SQL, ejecute el siguiente comando en el entorno existente:</span><span class="sxs-lookup"><span data-stu-id="8b8ae-112">To export your existing PostgreSQL database on-premises or in a VM to a sql script file, run the following command in your existing environment:</span></span>
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
<span data-ttu-id="8b8ae-113">Por ejemplo, si tiene un servidor local y una base de datos llamada **testdb** en él:</span><span class="sxs-lookup"><span data-stu-id="8b8ae-113">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-the-data-on-target-azure-database-for-postrgesql"></a><span data-ttu-id="8b8ae-114">Importación de los datos en la instancia de Azure Database for PostrgeSQL de destino</span><span class="sxs-lookup"><span data-stu-id="8b8ae-114">Import the data on target Azure Database for PostrgeSQL</span></span>
<span data-ttu-id="8b8ae-115">Puede usar la utilidad de la línea de comandos psql y el parámetro -d, --dbname para importar los datos en la instancia de Azure Database for PostrgeSQL que creamos y cargar los datos desde el archivo de SQL.</span><span class="sxs-lookup"><span data-stu-id="8b8ae-115">You can use the psql command line and the -d, --dbname parameter to import the data into Azure Database for PostrgeSQL we created and load data from the sql file.</span></span>
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
<span data-ttu-id="8b8ae-116">En este ejemplo se usa la utilidad psql y el archivo de script **testdb.sql** del paso anterior para importar los datos en la base de datos **mypgsqldb**, en el servidor de destino **mypgserver-20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="8b8ae-116">This example uses psql utility and a script file named **testdb.sql** from previous step to import data into the database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a><span data-ttu-id="8b8ae-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8b8ae-117">Next steps</span></span>
- <span data-ttu-id="8b8ae-118">Para migrar una base de datos de PostgreSQL mediante volcado y restauración, consulte [Migración de una base de datos de PostgreSQL mediante volcado y restauración](howto-migrate-using-dump-and-restore.md).</span><span class="sxs-lookup"><span data-stu-id="8b8ae-118">To migrate a PostgreSQL database using dump and restore, see [Migrate your PostgreSQL database using dump and restore](howto-migrate-using-dump-and-restore.md)</span></span>