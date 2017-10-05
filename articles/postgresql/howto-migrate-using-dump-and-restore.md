---
title: "Volcado y restauración en Azure Database for PostgreSQL | Microsoft Docs"
description: "Describe cómo extraer una base de datos de PostgreSQL en un archivo de volcado y restaurar la base de datos de PostgreSQL desde un archivo de almacenamiento creado por pg_dump en Azure Database for PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 190373c4980b67e16b58700e4b7e65658545c615
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a><span data-ttu-id="d9682-103">Migración de una base de datos de PostgreSQL mediante volcado y restauración</span><span class="sxs-lookup"><span data-stu-id="d9682-103">Migrate your PostgreSQL database using dump and restore</span></span>
<span data-ttu-id="d9682-104">Puede usar [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) para extraer una base de datos de PostgreSQL a un archivo de volcado y [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) para restaurar la base de datos de PostgreSQL desde un archivo de almacenamiento creado por pg_dump.</span><span class="sxs-lookup"><span data-stu-id="d9682-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) to extract a PostgreSQL database into a dump file and [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) to restore the PostgreSQL database from an archive file created by pg_dump.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9682-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d9682-105">Prerequisites</span></span>
<span data-ttu-id="d9682-106">Para seguir esta guía, necesitará:</span><span class="sxs-lookup"><span data-stu-id="d9682-106">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="d9682-107">Un [servidor de Azure Database for PostgreSQL](quickstart-create-server-database-portal.md) con reglas de firewall para permitir el acceso a las bases de datos que hay en él.</span><span class="sxs-lookup"><span data-stu-id="d9682-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules to allow access and database under it.</span></span>
- <span data-ttu-id="d9682-108">Utilidades de línea de comandos [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) y [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) instaladas</span><span class="sxs-lookup"><span data-stu-id="d9682-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) and [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) command-line utilities installed</span></span>

<span data-ttu-id="d9682-109">Siga estos pasos para realizar un volcado y restaurar la base de datos de PostgreSQL:</span><span class="sxs-lookup"><span data-stu-id="d9682-109">Follow these steps to dump and restore your PostgreSQL database:</span></span>

## <a name="create-a-dump-file-using-pgdump-that-contains-the-data-to-be-loaded"></a><span data-ttu-id="d9682-110">Creación de un archivo de volcado mediante pg_dump con los datos que se van a cargar</span><span class="sxs-lookup"><span data-stu-id="d9682-110">Create a dump file using pg_dump that contains the data to be loaded</span></span>
<span data-ttu-id="d9682-111">Para hacer una copia de seguridad de una base de datos de PostgreSQL existente en el entorno local o en una máquina virtual, ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="d9682-111">To back up an existing PostgreSQL database on-premises or in a VM, run the following command:</span></span>
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
<span data-ttu-id="d9682-112">Por ejemplo, si tiene un servidor local y una base de datos llamada **testdb** en él:</span><span class="sxs-lookup"><span data-stu-id="d9682-112">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-the-data-into-the-target-azure-database-for-postrgesql-using-pgrestore"></a><span data-ttu-id="d9682-113">Restauración de los datos a la instancia de Azure Database for PostrgeSQL con pg_restore</span><span class="sxs-lookup"><span data-stu-id="d9682-113">Restore the data into the target Azure Database for PostrgeSQL using pg_restore</span></span>
<span data-ttu-id="d9682-114">Después de crear la base de datos de destino, puede usar el comando pg_restore y el parámetro -d, --dbname para restaurar los datos en la base de datos de destino desde el archivo de volcado.</span><span class="sxs-lookup"><span data-stu-id="d9682-114">Once you have created the target database, you can use the pg_restore command and the -d, --dbname parameter to restore the data into the target database from the dump file.</span></span>
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
<span data-ttu-id="d9682-115">En este ejemplo, restaure los datos del archivo de copia de seguridad **testdb.dump** en la base de datos **mypgsqldb** en el servidor de destino **mypgserver-20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="d9682-115">In this example, restore the data from the dump file **testdb.dump** into the database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a><span data-ttu-id="d9682-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d9682-116">Next steps</span></span>
- <span data-ttu-id="d9682-117">Para migrar una base de datos de PostgreSQL mediante exportación e importación, consulte [Migración de una base de datos de PostgreSQL mediante exportación e importación](howto-migrate-using-export-and-import.md).</span><span class="sxs-lookup"><span data-stu-id="d9682-117">To migrate a PostgreSQL database using export and import, see [Migrate your PostgreSQL database using export and import](howto-migrate-using-export-and-import.md)</span></span>