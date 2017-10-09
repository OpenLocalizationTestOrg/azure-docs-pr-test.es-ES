---
title: datos de aaaLoad de SQL Server en almacenamiento de datos de SQL Azure (PolyBase) | Documentos de Microsoft
description: Utiliza bcp tooexport datos desde archivos de tooflat de SQL Server, el almacenamiento de blobs de AZCopy tooimport datos tooAzure y datos de PolyBase tooingest hello en almacenamiento de datos de SQL Azure.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4d42786a-fb28-43c9-9c3b-72d19c0ecc11
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 89e2a91bc97642e9fc18545cb802b42d8dc4ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-azcopy"></a><span data-ttu-id="3146d-103">Carga de datos de SQL Server en Almacenamiento de datos SQL de Azure (AZCopy)</span><span class="sxs-lookup"><span data-stu-id="3146d-103">Load data from SQL Server into Azure SQL Data Warehouse (AZCopy)</span></span>
<span data-ttu-id="3146d-104">Usar bcp y los datos de tooload de utilidades de línea de comandos de AZCopy desde almacenamiento de blobs de SQL Server tooAzure.</span><span class="sxs-lookup"><span data-stu-id="3146d-104">Use bcp and AZCopy command-line utilities tooload data from SQL Server tooAzure blob storage.</span></span> <span data-ttu-id="3146d-105">A continuación, usar datos de Hola de tooload de PolyBase o Data Factory de Azure en almacenamiento de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3146d-105">Then use PolyBase or Azure Data Factory tooload hello data into Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3146d-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3146d-106">Prerequisites</span></span>
<span data-ttu-id="3146d-107">toostep a través de este tutorial, necesitará:</span><span class="sxs-lookup"><span data-stu-id="3146d-107">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="3146d-108">Una base de datos de Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="3146d-108">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="3146d-109">utilidad de línea de comandos bcp Hola instalado</span><span class="sxs-lookup"><span data-stu-id="3146d-109">hello bcp command line utility installed</span></span>
* <span data-ttu-id="3146d-110">Hola instalada la utilidad de línea de comandos SQLCMD</span><span class="sxs-lookup"><span data-stu-id="3146d-110">hello SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="3146d-111">Puede descargar las utilidades de bcp y sqlcmd de Hola de hello [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="3146d-111">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="3146d-112">Importación de datos en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="3146d-112">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="3146d-113">En este tutorial, creará una tabla en el almacén de datos de SQL Azure e importar datos en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="3146d-113">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into hello table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="3146d-114">Paso 1: Crear una tabla en Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="3146d-114">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="3146d-115">Desde un símbolo del sistema, use sqlcmd toorun Hola siguiente toocreate consulta una tabla de la instancia:</span><span class="sxs-lookup"><span data-stu-id="3146d-115">From a command prompt, use sqlcmd toorun hello following query toocreate a table on your instance:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    WITH
    (
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    );
"
```

> [!NOTE]
> <span data-ttu-id="3146d-116">Vea [información general de la tabla] [ Table Overview] o [sintaxis de CREATE TABLE] [ CREATE TABLE syntax] para obtener más información acerca de cómo crear una tabla en hello y almacenamiento de datos SQL  opciones disponibles en la cláusula WITH de Hola.</span><span class="sxs-lookup"><span data-stu-id="3146d-116">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and hello  options available in hello WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="3146d-117">Paso 2: Crear un archivo de datos de origen</span><span class="sxs-lookup"><span data-stu-id="3146d-117">Step 2: Create a source data file</span></span>
<span data-ttu-id="3146d-118">Abra el Bloc de notas y copie Hola después de líneas de datos en un nuevo archivo de texto y, a continuación, guarde este archivo tooyour directorio temporal local, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="3146d-118">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

> [!NOTE]
> <span data-ttu-id="3146d-119">Es importante tooremember ese bcp.exe no admite la codificación del archivo hello UTF-8.</span><span class="sxs-lookup"><span data-stu-id="3146d-119">It is important tooremember that bcp.exe does not support hello UTF-8 file encoding.</span></span> <span data-ttu-id="3146d-120">Use archivos ASCII o archivos codificados UTF-16 al usar bcp.exe.</span><span class="sxs-lookup"><span data-stu-id="3146d-120">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a><span data-ttu-id="3146d-121">Paso 3: Conectarse e importar datos de Hola</span><span class="sxs-lookup"><span data-stu-id="3146d-121">Step 3: Connect and import hello data</span></span>
<span data-ttu-id="3146d-122">Usar bcp, puede conectarse e importar datos de hello mediante Hola después de reemplazar valores de hello comando según corresponda:</span><span class="sxs-lookup"><span data-stu-id="3146d-122">Using bcp, you can connect and import hello data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="3146d-123">También puede comprobar Hola se cargaron los datos mediante la ejecución de hello después de consulta mediante sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="3146d-123">You can verify hello data was loaded by running hello following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="3146d-124">Se debe devolver Hola siguientes resultados:</span><span class="sxs-lookup"><span data-stu-id="3146d-124">This should return hello following results:</span></span>

| <span data-ttu-id="3146d-125">DateId</span><span class="sxs-lookup"><span data-stu-id="3146d-125">DateId</span></span> | <span data-ttu-id="3146d-126">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="3146d-126">CalendarQuarter</span></span> | <span data-ttu-id="3146d-127">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="3146d-127">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3146d-128">20150101</span><span class="sxs-lookup"><span data-stu-id="3146d-128">20150101</span></span> |<span data-ttu-id="3146d-129">1</span><span class="sxs-lookup"><span data-stu-id="3146d-129">1</span></span> |<span data-ttu-id="3146d-130">3</span><span class="sxs-lookup"><span data-stu-id="3146d-130">3</span></span> |
| <span data-ttu-id="3146d-131">20150201</span><span class="sxs-lookup"><span data-stu-id="3146d-131">20150201</span></span> |<span data-ttu-id="3146d-132">1</span><span class="sxs-lookup"><span data-stu-id="3146d-132">1</span></span> |<span data-ttu-id="3146d-133">3</span><span class="sxs-lookup"><span data-stu-id="3146d-133">3</span></span> |
| <span data-ttu-id="3146d-134">20150301</span><span class="sxs-lookup"><span data-stu-id="3146d-134">20150301</span></span> |<span data-ttu-id="3146d-135">1</span><span class="sxs-lookup"><span data-stu-id="3146d-135">1</span></span> |<span data-ttu-id="3146d-136">3</span><span class="sxs-lookup"><span data-stu-id="3146d-136">3</span></span> |
| <span data-ttu-id="3146d-137">20150401</span><span class="sxs-lookup"><span data-stu-id="3146d-137">20150401</span></span> |<span data-ttu-id="3146d-138">2</span><span class="sxs-lookup"><span data-stu-id="3146d-138">2</span></span> |<span data-ttu-id="3146d-139">4</span><span class="sxs-lookup"><span data-stu-id="3146d-139">4</span></span> |
| <span data-ttu-id="3146d-140">20150501</span><span class="sxs-lookup"><span data-stu-id="3146d-140">20150501</span></span> |<span data-ttu-id="3146d-141">2</span><span class="sxs-lookup"><span data-stu-id="3146d-141">2</span></span> |<span data-ttu-id="3146d-142">4</span><span class="sxs-lookup"><span data-stu-id="3146d-142">4</span></span> |
| <span data-ttu-id="3146d-143">20150601</span><span class="sxs-lookup"><span data-stu-id="3146d-143">20150601</span></span> |<span data-ttu-id="3146d-144">2</span><span class="sxs-lookup"><span data-stu-id="3146d-144">2</span></span> |<span data-ttu-id="3146d-145">4</span><span class="sxs-lookup"><span data-stu-id="3146d-145">4</span></span> |
| <span data-ttu-id="3146d-146">20150701</span><span class="sxs-lookup"><span data-stu-id="3146d-146">20150701</span></span> |<span data-ttu-id="3146d-147">3</span><span class="sxs-lookup"><span data-stu-id="3146d-147">3</span></span> |<span data-ttu-id="3146d-148">1</span><span class="sxs-lookup"><span data-stu-id="3146d-148">1</span></span> |
| <span data-ttu-id="3146d-149">20150801</span><span class="sxs-lookup"><span data-stu-id="3146d-149">20150801</span></span> |<span data-ttu-id="3146d-150">3</span><span class="sxs-lookup"><span data-stu-id="3146d-150">3</span></span> |<span data-ttu-id="3146d-151">1</span><span class="sxs-lookup"><span data-stu-id="3146d-151">1</span></span> |
| <span data-ttu-id="3146d-152">20150801</span><span class="sxs-lookup"><span data-stu-id="3146d-152">20150801</span></span> |<span data-ttu-id="3146d-153">3</span><span class="sxs-lookup"><span data-stu-id="3146d-153">3</span></span> |<span data-ttu-id="3146d-154">1</span><span class="sxs-lookup"><span data-stu-id="3146d-154">1</span></span> |
| <span data-ttu-id="3146d-155">20151001</span><span class="sxs-lookup"><span data-stu-id="3146d-155">20151001</span></span> |<span data-ttu-id="3146d-156">4</span><span class="sxs-lookup"><span data-stu-id="3146d-156">4</span></span> |<span data-ttu-id="3146d-157">2</span><span class="sxs-lookup"><span data-stu-id="3146d-157">2</span></span> |
| <span data-ttu-id="3146d-158">20151101</span><span class="sxs-lookup"><span data-stu-id="3146d-158">20151101</span></span> |<span data-ttu-id="3146d-159">4</span><span class="sxs-lookup"><span data-stu-id="3146d-159">4</span></span> |<span data-ttu-id="3146d-160">2</span><span class="sxs-lookup"><span data-stu-id="3146d-160">2</span></span> |
| <span data-ttu-id="3146d-161">20151201</span><span class="sxs-lookup"><span data-stu-id="3146d-161">20151201</span></span> |<span data-ttu-id="3146d-162">4</span><span class="sxs-lookup"><span data-stu-id="3146d-162">4</span></span> |<span data-ttu-id="3146d-163">2</span><span class="sxs-lookup"><span data-stu-id="3146d-163">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="3146d-164">Paso 4: Crear estadísticas de los datos recién cargados</span><span class="sxs-lookup"><span data-stu-id="3146d-164">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="3146d-165">Almacenamiento de datos SQL de Azure todavía no permite crear ni actualizar automáticamente las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="3146d-165">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="3146d-166">En orden tooget Hola un mejor rendimiento de las consultas, es importante que las estadísticas se crean en todas las columnas de todas las tablas después de la primera carga de Hola o se producen cambios sustanciales en datos Hola.</span><span class="sxs-lookup"><span data-stu-id="3146d-166">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span> <span data-ttu-id="3146d-167">Para obtener una explicación detallada de las estadísticas, vea hello [estadísticas] [ Statistics] tema en el grupo de desarrollo de Hola de temas.</span><span class="sxs-lookup"><span data-stu-id="3146d-167">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span> <span data-ttu-id="3146d-168">A continuación se muestra un ejemplo rápido de cómo cargarán toocreate estadísticas en la tabla de hello en este ejemplo</span><span class="sxs-lookup"><span data-stu-id="3146d-168">Below is a quick example of how toocreate statistics on hello tabled loaded in this example</span></span>

<span data-ttu-id="3146d-169">Ejecute hello siguiendo las instrucciones CREATE STATISTICS desde un símbolo del sistema de sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="3146d-169">Execute hello following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="3146d-170">Exportación de datos de Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="3146d-170">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="3146d-171">En este tutorial, creará un archivo de datos a partir de una tabla de Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="3146d-171">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="3146d-172">Se exportará datos Hola que hemos creado anteriormente tooa nuevo archivo de datos denominado DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="3146d-172">We will export hello data we created above tooa new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-hello-data"></a><span data-ttu-id="3146d-173">Paso 1: Exportar datos de Hola</span><span class="sxs-lookup"><span data-stu-id="3146d-173">Step 1: Export hello data</span></span>
<span data-ttu-id="3146d-174">Mediante la utilidad bcp de hello, puede conectar y exportar datos mediante Hola después de reemplazar valores de hello comando según corresponda:</span><span class="sxs-lookup"><span data-stu-id="3146d-174">Using hello bcp utility, you can connect and export data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="3146d-175">Puede comprobar Hola datos se exportaron correctamente, abra el archivo nuevo de hello.</span><span class="sxs-lookup"><span data-stu-id="3146d-175">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="3146d-176">datos de Hello en el archivo hello deben coincidir con texto hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="3146d-176">hello data in hello file should match hello text below:</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

> [!NOTE]
> <span data-ttu-id="3146d-177">Debido a la naturaleza toohello de sistemas distribuidos, Hola datos orden no sea el mismo Hola entre bases de datos de almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="3146d-177">Due toohello nature of distributed systems, hello data order may not be hello same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="3146d-178">Otra opción es hello toouse **queryout** función de bcp toowrite una consulta extraer en lugar de exportar toda la tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="3146d-178">Another option is toouse hello **queryout** function of bcp toowrite a query extract rather than export hello entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="3146d-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3146d-179">Next steps</span></span>
<span data-ttu-id="3146d-180">Para obtener información general sobre la carga, vea [Carga de datos en SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="3146d-180">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="3146d-181">Para obtener más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo de Almacenamiento de datos SQL][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="3146d-181">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Load data into SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Table Overview]: ./sql-data-warehouse-tables-overview.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
