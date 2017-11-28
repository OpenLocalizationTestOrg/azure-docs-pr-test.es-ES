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
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a><span data-ttu-id="fb16c-103">Migración de una base de datos de PostgreSQL mediante volcado y restauración</span><span class="sxs-lookup"><span data-stu-id="fb16c-103">Migrate your PostgreSQL database using dump and restore</span></span>
<span data-ttu-id="fb16c-104">Puede usar [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract una base de datos PostgreSQL en un archivo de volcado de memoria y [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) toorestore base de datos de PostgreSQL de Hola desde un archivo de almacenamiento creado por pg_dump.</span><span class="sxs-lookup"><span data-stu-id="fb16c-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract a PostgreSQL database into a dump file and [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) toorestore hello PostgreSQL database from an archive file created by pg_dump.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb16c-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fb16c-105">Prerequisites</span></span>
<span data-ttu-id="fb16c-106">toostep a través de este tooguide cómo, necesita:</span><span class="sxs-lookup"><span data-stu-id="fb16c-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="fb16c-107">Un [base de datos de Azure para PostgreSQL server](quickstart-create-server-database-portal.md) con acceso de tooallow de reglas de firewall y la base de datos en él.</span><span class="sxs-lookup"><span data-stu-id="fb16c-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules tooallow access and database under it.</span></span>
- <span data-ttu-id="fb16c-108">Utilidades de línea de comandos [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) y [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) instaladas</span><span class="sxs-lookup"><span data-stu-id="fb16c-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) and [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) command-line utilities installed</span></span>

<span data-ttu-id="fb16c-109">Siga estos pasos toodump y restaurar la base de datos PostgreSQL:</span><span class="sxs-lookup"><span data-stu-id="fb16c-109">Follow these steps toodump and restore your PostgreSQL database:</span></span>

## <a name="create-a-dump-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a><span data-ttu-id="fb16c-110">Cree un archivo de volcado de memoria mediante pg_dump que contenga Hola datos toobe cargado</span><span class="sxs-lookup"><span data-stu-id="fb16c-110">Create a dump file using pg_dump that contains hello data toobe loaded</span></span>
<span data-ttu-id="fb16c-111">tooback de una existente PostgreSQL local de la base de datos o en una máquina virtual, ejecute el siguiente comando de Hola:</span><span class="sxs-lookup"><span data-stu-id="fb16c-111">tooback up an existing PostgreSQL database on-premises or in a VM, run hello following command:</span></span>
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
<span data-ttu-id="fb16c-112">Por ejemplo, si tiene un servidor local y una base de datos llamada **testdb** en él:</span><span class="sxs-lookup"><span data-stu-id="fb16c-112">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-hello-data-into-hello-target-azure-database-for-postrgesql-using-pgrestore"></a><span data-ttu-id="fb16c-113">Restaurar los datos de hello en base de datos de destino de Hola para PostrgeSQL con pg_restore</span><span class="sxs-lookup"><span data-stu-id="fb16c-113">Restore hello data into hello target Azure Database for PostrgeSQL using pg_restore</span></span>
<span data-ttu-id="fb16c-114">Una vez haya creado la base de datos de destino de hello, puede usar comandos de pg_restore de Hola y Hola -d, datos de saludo--dbname parámetro toorestore en base de datos de destino de Hola desde el archivo de volcado de memoria de hello.</span><span class="sxs-lookup"><span data-stu-id="fb16c-114">Once you have created hello target database, you can use hello pg_restore command and hello -d, --dbname parameter toorestore hello data into hello target database from hello dump file.</span></span>
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
<span data-ttu-id="fb16c-115">En este ejemplo, restaurar los datos de Hola desde el archivo de volcado de memoria de hello **testdb.dump** en la base de datos de hello **mypgsqldb** en el servidor de destino **mypgserver-20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="fb16c-115">In this example, restore hello data from hello dump file **testdb.dump** into hello database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a><span data-ttu-id="fb16c-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fb16c-116">Next steps</span></span>
- <span data-ttu-id="fb16c-117">toomigrate una base de datos PostgreSQL mediante la exportación e importación, consulte [migrar la base de datos PostgreSQL utilizando exportar e importar](howto-migrate-using-export-and-import.md)</span><span class="sxs-lookup"><span data-stu-id="fb16c-117">toomigrate a PostgreSQL database using export and import, see [Migrate your PostgreSQL database using export and import](howto-migrate-using-export-and-import.md)</span></span>
