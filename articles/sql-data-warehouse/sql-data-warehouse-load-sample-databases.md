---
title: datos de ejemplo de aaaLoad en almacenamiento de datos SQL | Documentos de Microsoft
description: Carga de datos de ejemplo en Almacenamiento de datos SQL
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e338ecf8-cfee-419b-b7b6-98108d381c62
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 3459c42f3aae51c27fd35db7874faf99e1e577e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a><span data-ttu-id="59af1-103">Carga de datos de ejemplo en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="59af1-103">Load sample data into SQL Data Warehouse</span></span>
<span data-ttu-id="59af1-104">Siga estas tooload pasos sencillos y base de datos de ejemplo Adventure Works de Hola de consultas.</span><span class="sxs-lookup"><span data-stu-id="59af1-104">Follow these simple steps tooload and query hello Adventure Works Sample database.</span></span> <span data-ttu-id="59af1-105">Estas secuencias de comandos en primer lugar utilizan sqlcmd toorun SQL que se crea tablas y vistas.</span><span class="sxs-lookup"><span data-stu-id="59af1-105">These scripts first use sqlcmd toorun SQL which will create tables and views.</span></span> <span data-ttu-id="59af1-106">Una vez que se han creado las tablas, las secuencias de comandos de hello utilizará los datos de tooload de bcp.</span><span class="sxs-lookup"><span data-stu-id="59af1-106">Once tables have been created, hello scripts will use bcp tooload data.</span></span>  <span data-ttu-id="59af1-107">Si aún no tiene sqlcmd y bcp instalado, siga estos vínculos demasiado[instalar bcp] [ install bcp] y demasiado[instalar sqlcmd][install sqlcmd].</span><span class="sxs-lookup"><span data-stu-id="59af1-107">If you don't already have sqlcmd and bcp installed, follow these links too[install bcp][install bcp] and too[install sqlcmd][install sqlcmd].</span></span>

## <a name="load-sample-data"></a><span data-ttu-id="59af1-108">Carga de datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="59af1-108">Load sample data</span></span>
1. <span data-ttu-id="59af1-109">Descargar hello [Scripts de ejemplo de Adventure Works para almacenamiento de datos SQL] [ Adventure Works Sample Scripts for SQL Data Warehouse] archivo zip.</span><span class="sxs-lookup"><span data-stu-id="59af1-109">Download hello [Adventure Works Sample Scripts for SQL Data Warehouse][Adventure Works Sample Scripts for SQL Data Warehouse] zip file.</span></span>
2. <span data-ttu-id="59af1-110">Extraiga los archivos de hello del directorio de tooa zip descargado en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="59af1-110">Extract hello files from downloaded zip tooa directory on your local machine.</span></span>
3. <span data-ttu-id="59af1-111">Edite Hola extraído archivo aw_create.bat y establezca Hola después de las variables que se encuentra al principio de hello del archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="59af1-111">Edit hello extracted file aw_create.bat and set hello following variables found at hello top of hello file.</span></span>  <span data-ttu-id="59af1-112">No ser seguro tooleave ningún espacio en blanco entre ="hello" y el parámetro hello.</span><span class="sxs-lookup"><span data-stu-id="59af1-112">Be sure tooleave no whitespace between hello "=" and hello parameter.</span></span>  <span data-ttu-id="59af1-113">A continuación, puede ver ejemplos del aspecto que deberían tener las modificaciones.</span><span class="sxs-lookup"><span data-stu-id="59af1-113">Below are examples of how your edits might look.</span></span>
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. <span data-ttu-id="59af1-114">Desde un símbolo del sistema de Windows, ejecute aw_create.bat Hola editado.</span><span class="sxs-lookup"><span data-stu-id="59af1-114">From a Windows cmd prompt, run hello edited aw_create.bat.</span></span>  <span data-ttu-id="59af1-115">Asegúrese de que se encuentra en el directorio de Hola donde guardó la versión editada de aw_create.bat.</span><span class="sxs-lookup"><span data-stu-id="59af1-115">Be sure you are in hello directory where you saved your edited version of aw_create.bat.</span></span>
   <span data-ttu-id="59af1-116">Este script le permitirá hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="59af1-116">This script will...</span></span>
   
   * <span data-ttu-id="59af1-117">Anular cualquier tabla o vista de Adventure Works que ya exista en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="59af1-117">Drop any Adventure Works tables or views that already exist in your database</span></span>
   * <span data-ttu-id="59af1-118">Crear vistas y tablas de Adventure Works Hola</span><span class="sxs-lookup"><span data-stu-id="59af1-118">Create hello Adventure Works tables and views</span></span>
   * <span data-ttu-id="59af1-119">Cargar cada tabla de Adventure Works con bcp.</span><span class="sxs-lookup"><span data-stu-id="59af1-119">Load each Adventure Works table using bcp</span></span>
   * <span data-ttu-id="59af1-120">Validar Hola recuentos de filas para cada tabla de Adventure Works</span><span class="sxs-lookup"><span data-stu-id="59af1-120">Validate hello row counts for each Adventure Works table</span></span>
   * <span data-ttu-id="59af1-121">Recopilar estadísticas en cada columna de cada tabla de Adventure Works.</span><span class="sxs-lookup"><span data-stu-id="59af1-121">Collect statistics on every column for each Adventure Works table</span></span>

## <a name="query-sample-data"></a><span data-ttu-id="59af1-122">Datos de ejemplo de consultas</span><span class="sxs-lookup"><span data-stu-id="59af1-122">Query sample data</span></span>
<span data-ttu-id="59af1-123">Una vez que carga algunos datos de ejemplo en Almacenamiento de datos SQL, puede ejecutar rápidamente algunas consultas.</span><span class="sxs-lookup"><span data-stu-id="59af1-123">Once you've loaded some sample data into your SQL Data Warehouse, you can quickly run a few queries.</span></span>  <span data-ttu-id="59af1-124">toorun una consulta, conectar la base de datos de Adventure Works de tooyour recién creado en el almacenamiento de datos de SQL de Azure con Visual Studio como SSDT, como se describe en hello [consulta con Visual Studio] [ query with Visual Studio] documento.</span><span class="sxs-lookup"><span data-stu-id="59af1-124">toorun a query, connect tooyour newly created Adventure Works database in Azure SQL DW using Visual Studio and SSDT, as described in hello [query with Visual Studio][query with Visual Studio] document.</span></span>

<span data-ttu-id="59af1-125">Ejemplo de simple seleccione instrucción tooget toda la información de empleados de Hola Hola:</span><span class="sxs-lookup"><span data-stu-id="59af1-125">Example of simple select statement tooget all hello info of hello employees:</span></span>

```sql
SELECT * FROM DimEmployee;
```

<span data-ttu-id="59af1-126">Ejemplo de una consulta más compleja con construcciones como toolook GROUP BY en la cantidad total de Hola para todas las ventas en cada día:</span><span class="sxs-lookup"><span data-stu-id="59af1-126">Example of a more complex query using constructs such as GROUP BY toolook at hello total amount for all sales on each day:</span></span>

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="59af1-127">Ejemplo de una instrucción SELECT con una toofilter de cláusula WHERE las órdenes de antes de una fecha determinada:</span><span class="sxs-lookup"><span data-stu-id="59af1-127">Example of a SELECT with a WHERE clause toofilter out orders from before a certain date:</span></span>

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="59af1-128">Almacenamiento de datos SQL admite casi todas las construcciones T-SQL compatibles con SQL Server.</span><span class="sxs-lookup"><span data-stu-id="59af1-128">SQL Data Warehouse supports almost all T-SQL constructs which SQL Server supports.</span></span>  <span data-ttu-id="59af1-129">Todas las diferencias existentes se registran en nuestra documentación sobre la [migración del código][migrate code].</span><span class="sxs-lookup"><span data-stu-id="59af1-129">Any differences are documented in our [migrate code][migrate code] documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59af1-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="59af1-130">Next steps</span></span>
<span data-ttu-id="59af1-131">Ahora que ha tenido una oportunidad tootry algunas consultas con datos de ejemplo, consulte cómo demasiado[desarrollar][develop], [cargar][load], o [ migrar] [ migrate] tooSQL almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="59af1-131">Now that you've had a chance tootry some queries with sample data, check out how too[develop][develop], [load][load], or [migrate][migrate] tooSQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[query with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[migrate code]: sql-data-warehouse-migrate-code.md
[install bcp]: sql-data-warehouse-load-with-bcp.md
[install sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--Other Web references-->
[Adventure Works Sample Scripts for SQL Data Warehouse]: https://migrhoststorage.blob.core.windows.net/sqldwsample/AdventureWorksSQLDW2012.zip
