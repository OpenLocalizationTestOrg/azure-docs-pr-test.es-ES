---
title: datos de tooload aaaUse bcp en almacenamiento de datos SQL | Documentos de Microsoft
description: "Obtenga información acerca de qué bcp es y cómo toouse para escenarios de almacenamiento de datos."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: f9467d11-fcd6-4131-a65a-2022d2c32d24
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 09a2980585097644924c71899f9e74fb32fbc26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-bcp"></a><span data-ttu-id="831ed-103">Carga de datos con BCP</span><span class="sxs-lookup"><span data-stu-id="831ed-103">Load data with bcp</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="831ed-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="831ed-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="831ed-105">Factoría de datos</span><span class="sxs-lookup"><span data-stu-id="831ed-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="831ed-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="831ed-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="831ed-107">BCP</span><span class="sxs-lookup"><span data-stu-id="831ed-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="831ed-108">**[BCP] [ bcp]**  es una utilidad de carga masiva de línea de comandos que le permite toocopy datos entre SQL Server, archivos de datos y almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="831ed-108">**[bcp][bcp]** is a command-line bulk load utility that allows you toocopy data between SQL Server, data files, and SQL Data Warehouse.</span></span> <span data-ttu-id="831ed-109">Usar bcp tooimport grandes cantidades de filas en tablas de almacenamiento de datos SQL o tooexport datos de tablas de SQL Server a archivos de datos.</span><span class="sxs-lookup"><span data-stu-id="831ed-109">Use bcp tooimport large numbers of rows into SQL Data Warehouse tables or tooexport data from SQL Server tables into data files.</span></span> <span data-ttu-id="831ed-110">Excepto cuando se usa con la opción queryout de hello, bcp no requiere ningún conocimiento de Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="831ed-110">Except when used with hello queryout option, bcp requires no knowledge of Transact-SQL.</span></span>

<span data-ttu-id="831ed-111">bcp es una manera rápida y sencilla toomove más pequeños conjuntos de datos dentro y fuera de una base de datos de almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="831ed-111">bcp is a quick and easy way toomove smaller data sets into and out of a SQL Data Warehouse database.</span></span> <span data-ttu-id="831ed-112">cantidad exacta de Hola de datos que se recomienda tooload/extract mediante bcp dependerá en su centro de datos de Azure toohello de conexión de red.</span><span class="sxs-lookup"><span data-stu-id="831ed-112">hello exact amount of data that is recommended tooload/extract via bcp will depend on you network connection toohello Azure data center.</span></span>  <span data-ttu-id="831ed-113">Por lo general, las tablas de dimensiones se pueden cargar y extraer fácilmente con bcp; sin embargo, no se recomienda bcp para cargar o extraer grandes volúmenes de datos.</span><span class="sxs-lookup"><span data-stu-id="831ed-113">Generally, dimension tables can be loaded and extracted readily with bcp, however, bcp is not recommended for loading or extracting large volumes of data.</span></span>  <span data-ttu-id="831ed-114">Polybase es hello recomendada herramienta para cargar y extraer grandes volúmenes de datos como lo hace un mejor trabajo para aprovechar la arquitectura de procesamiento paralelo masivo Hola de almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="831ed-114">Polybase is hello recommended tool for loading and extracting large volumes of data as it does a better job leveraging hello massively parallel processing architecture of SQL Data Warehouse.</span></span>

<span data-ttu-id="831ed-115">Con bcp puede:</span><span class="sxs-lookup"><span data-stu-id="831ed-115">With bcp you can:</span></span>

* <span data-ttu-id="831ed-116">Use una utilidad de línea de comandos simple tooload de datos en almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="831ed-116">Use a simple command-line utility tooload data into SQL Data Warehouse.</span></span>
* <span data-ttu-id="831ed-117">Utilizar la utilidad de línea de comandos simple tooextract datos de almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="831ed-117">Use a simple command-line utility tooextract data from SQL Data Warehouse.</span></span>

<span data-ttu-id="831ed-118">Este tutorial le mostrará cómo:</span><span class="sxs-lookup"><span data-stu-id="831ed-118">This tutorial will show you how to:</span></span>

* <span data-ttu-id="831ed-119">Importar datos en una tabla mediante bcp de hello en comando</span><span class="sxs-lookup"><span data-stu-id="831ed-119">Import data into a table using hello bcp in command</span></span>
* <span data-ttu-id="831ed-120">Exportar datos de tabla usar Hola bcp out comando</span><span class="sxs-lookup"><span data-stu-id="831ed-120">Export data from a table uisng hello bcp out command</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="831ed-121">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="831ed-121">Prerequisites</span></span>
<span data-ttu-id="831ed-122">toostep a través de este tutorial, necesitará:</span><span class="sxs-lookup"><span data-stu-id="831ed-122">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="831ed-123">Una base de datos de Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="831ed-123">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="831ed-124">utilidad de línea de comandos bcp Hola instalado</span><span class="sxs-lookup"><span data-stu-id="831ed-124">hello bcp command line utility installed</span></span>
* <span data-ttu-id="831ed-125">Hola instalada la utilidad de línea de comandos SQLCMD</span><span class="sxs-lookup"><span data-stu-id="831ed-125">hello SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="831ed-126">Puede descargar las utilidades de bcp y sqlcmd de Hola de hello [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="831ed-126">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="831ed-127">Importación de datos en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="831ed-127">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="831ed-128">En este tutorial, creará una tabla en el almacén de datos de SQL Azure e importar datos en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="831ed-128">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into hello table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="831ed-129">Paso 1: Crear una tabla en Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="831ed-129">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="831ed-130">Desde un símbolo del sistema, use sqlcmd toorun Hola siguiente toocreate consulta una tabla de la instancia:</span><span class="sxs-lookup"><span data-stu-id="831ed-130">From a command prompt, use sqlcmd toorun hello following query toocreate a table on your instance:</span></span>

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
> <span data-ttu-id="831ed-131">Vea [información general de la tabla] [ Table Overview] o [sintaxis de CREATE TABLE] [ CREATE TABLE syntax] para obtener más información acerca de cómo crear una tabla en hello y almacenamiento de datos SQL  opciones disponibles en la cláusula WITH de Hola.</span><span class="sxs-lookup"><span data-stu-id="831ed-131">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and hello  options available in hello WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="831ed-132">Paso 2: Crear un archivo de datos de origen</span><span class="sxs-lookup"><span data-stu-id="831ed-132">Step 2: Create a source data file</span></span>
<span data-ttu-id="831ed-133">Abra el Bloc de notas y copie Hola después de líneas de datos en un nuevo archivo de texto y, a continuación, guarde este archivo tooyour directorio temporal local, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="831ed-133">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="831ed-134">Es importante tooremember ese bcp.exe no admite la codificación del archivo hello UTF-8.</span><span class="sxs-lookup"><span data-stu-id="831ed-134">It is important tooremember that bcp.exe does not support hello UTF-8 file encoding.</span></span> <span data-ttu-id="831ed-135">Use archivos ASCII o archivos codificados UTF-16 al usar bcp.exe.</span><span class="sxs-lookup"><span data-stu-id="831ed-135">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a><span data-ttu-id="831ed-136">Paso 3: Conectarse e importar datos de Hola</span><span class="sxs-lookup"><span data-stu-id="831ed-136">Step 3: Connect and import hello data</span></span>
<span data-ttu-id="831ed-137">Usar bcp, puede conectarse e importar datos de hello mediante Hola después de reemplazar valores de hello comando según corresponda:</span><span class="sxs-lookup"><span data-stu-id="831ed-137">Using bcp, you can connect and import hello data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="831ed-138">También puede comprobar Hola se cargaron los datos mediante la ejecución de hello después de consulta mediante sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="831ed-138">You can verify hello data was loaded by running hello following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="831ed-139">Se debe devolver Hola siguientes resultados:</span><span class="sxs-lookup"><span data-stu-id="831ed-139">This should return hello following results:</span></span>

| <span data-ttu-id="831ed-140">DateId</span><span class="sxs-lookup"><span data-stu-id="831ed-140">DateId</span></span> | <span data-ttu-id="831ed-141">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="831ed-141">CalendarQuarter</span></span> | <span data-ttu-id="831ed-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="831ed-142">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="831ed-143">20150101</span><span class="sxs-lookup"><span data-stu-id="831ed-143">20150101</span></span> |<span data-ttu-id="831ed-144">1</span><span class="sxs-lookup"><span data-stu-id="831ed-144">1</span></span> |<span data-ttu-id="831ed-145">3</span><span class="sxs-lookup"><span data-stu-id="831ed-145">3</span></span> |
| <span data-ttu-id="831ed-146">20150201</span><span class="sxs-lookup"><span data-stu-id="831ed-146">20150201</span></span> |<span data-ttu-id="831ed-147">1</span><span class="sxs-lookup"><span data-stu-id="831ed-147">1</span></span> |<span data-ttu-id="831ed-148">3</span><span class="sxs-lookup"><span data-stu-id="831ed-148">3</span></span> |
| <span data-ttu-id="831ed-149">20150301</span><span class="sxs-lookup"><span data-stu-id="831ed-149">20150301</span></span> |<span data-ttu-id="831ed-150">1</span><span class="sxs-lookup"><span data-stu-id="831ed-150">1</span></span> |<span data-ttu-id="831ed-151">3</span><span class="sxs-lookup"><span data-stu-id="831ed-151">3</span></span> |
| <span data-ttu-id="831ed-152">20150401</span><span class="sxs-lookup"><span data-stu-id="831ed-152">20150401</span></span> |<span data-ttu-id="831ed-153">2</span><span class="sxs-lookup"><span data-stu-id="831ed-153">2</span></span> |<span data-ttu-id="831ed-154">4</span><span class="sxs-lookup"><span data-stu-id="831ed-154">4</span></span> |
| <span data-ttu-id="831ed-155">20150501</span><span class="sxs-lookup"><span data-stu-id="831ed-155">20150501</span></span> |<span data-ttu-id="831ed-156">2</span><span class="sxs-lookup"><span data-stu-id="831ed-156">2</span></span> |<span data-ttu-id="831ed-157">4</span><span class="sxs-lookup"><span data-stu-id="831ed-157">4</span></span> |
| <span data-ttu-id="831ed-158">20150601</span><span class="sxs-lookup"><span data-stu-id="831ed-158">20150601</span></span> |<span data-ttu-id="831ed-159">2</span><span class="sxs-lookup"><span data-stu-id="831ed-159">2</span></span> |<span data-ttu-id="831ed-160">4</span><span class="sxs-lookup"><span data-stu-id="831ed-160">4</span></span> |
| <span data-ttu-id="831ed-161">20150701</span><span class="sxs-lookup"><span data-stu-id="831ed-161">20150701</span></span> |<span data-ttu-id="831ed-162">3</span><span class="sxs-lookup"><span data-stu-id="831ed-162">3</span></span> |<span data-ttu-id="831ed-163">1</span><span class="sxs-lookup"><span data-stu-id="831ed-163">1</span></span> |
| <span data-ttu-id="831ed-164">20150801</span><span class="sxs-lookup"><span data-stu-id="831ed-164">20150801</span></span> |<span data-ttu-id="831ed-165">3</span><span class="sxs-lookup"><span data-stu-id="831ed-165">3</span></span> |<span data-ttu-id="831ed-166">1</span><span class="sxs-lookup"><span data-stu-id="831ed-166">1</span></span> |
| <span data-ttu-id="831ed-167">20150801</span><span class="sxs-lookup"><span data-stu-id="831ed-167">20150801</span></span> |<span data-ttu-id="831ed-168">3</span><span class="sxs-lookup"><span data-stu-id="831ed-168">3</span></span> |<span data-ttu-id="831ed-169">1</span><span class="sxs-lookup"><span data-stu-id="831ed-169">1</span></span> |
| <span data-ttu-id="831ed-170">20151001</span><span class="sxs-lookup"><span data-stu-id="831ed-170">20151001</span></span> |<span data-ttu-id="831ed-171">4</span><span class="sxs-lookup"><span data-stu-id="831ed-171">4</span></span> |<span data-ttu-id="831ed-172">2</span><span class="sxs-lookup"><span data-stu-id="831ed-172">2</span></span> |
| <span data-ttu-id="831ed-173">20151101</span><span class="sxs-lookup"><span data-stu-id="831ed-173">20151101</span></span> |<span data-ttu-id="831ed-174">4</span><span class="sxs-lookup"><span data-stu-id="831ed-174">4</span></span> |<span data-ttu-id="831ed-175">2</span><span class="sxs-lookup"><span data-stu-id="831ed-175">2</span></span> |
| <span data-ttu-id="831ed-176">20151201</span><span class="sxs-lookup"><span data-stu-id="831ed-176">20151201</span></span> |<span data-ttu-id="831ed-177">4</span><span class="sxs-lookup"><span data-stu-id="831ed-177">4</span></span> |<span data-ttu-id="831ed-178">2</span><span class="sxs-lookup"><span data-stu-id="831ed-178">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="831ed-179">Paso 4: Crear estadísticas de los datos recién cargados</span><span class="sxs-lookup"><span data-stu-id="831ed-179">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="831ed-180">Almacenamiento de datos SQL de Azure todavía no permite crear ni actualizar automáticamente las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="831ed-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="831ed-181">En orden tooget Hola un mejor rendimiento de las consultas, es importante que las estadísticas se crean en todas las columnas de todas las tablas después de la primera carga de Hola o se producen cambios sustanciales en datos Hola.</span><span class="sxs-lookup"><span data-stu-id="831ed-181">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span> <span data-ttu-id="831ed-182">Para obtener una explicación detallada de las estadísticas, vea hello [estadísticas] [ Statistics] tema en el grupo de desarrollo de Hola de temas.</span><span class="sxs-lookup"><span data-stu-id="831ed-182">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span> <span data-ttu-id="831ed-183">A continuación se muestra un ejemplo rápido de cómo cargarán toocreate estadísticas en la tabla de hello en este ejemplo</span><span class="sxs-lookup"><span data-stu-id="831ed-183">Below is a quick example of how toocreate statistics on hello tabled loaded in this example</span></span>

<span data-ttu-id="831ed-184">Ejecute hello siguiendo las instrucciones CREATE STATISTICS desde un símbolo del sistema de sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="831ed-184">Execute hello following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="831ed-185">Exportación de datos de Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="831ed-185">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="831ed-186">En este tutorial, creará un archivo de datos a partir de una tabla de Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="831ed-186">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="831ed-187">Se exportará datos Hola que hemos creado anteriormente tooa nuevo archivo de datos denominado DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="831ed-187">We will export hello data we created above tooa new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-hello-data"></a><span data-ttu-id="831ed-188">Paso 1: Exportar datos de Hola</span><span class="sxs-lookup"><span data-stu-id="831ed-188">Step 1: Export hello data</span></span>
<span data-ttu-id="831ed-189">Mediante la utilidad bcp de hello, puede conectar y exportar datos mediante Hola después de reemplazar valores de hello comando según corresponda:</span><span class="sxs-lookup"><span data-stu-id="831ed-189">Using hello bcp utility, you can connect and export data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="831ed-190">Puede comprobar Hola datos se exportaron correctamente, abra el archivo nuevo de hello.</span><span class="sxs-lookup"><span data-stu-id="831ed-190">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="831ed-191">datos de Hello en el archivo hello deben coincidir con texto hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="831ed-191">hello data in hello file should match hello text below:</span></span>

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
> <span data-ttu-id="831ed-192">Debido a la naturaleza toohello de sistemas distribuidos, Hola datos orden no sea el mismo Hola entre bases de datos de almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="831ed-192">Due toohello nature of distributed systems, hello data order may not be hello same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="831ed-193">Otra opción es hello toouse **queryout** función de bcp toowrite una consulta extraer en lugar de exportar toda la tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="831ed-193">Another option is toouse hello **queryout** function of bcp toowrite a query extract rather than export hello entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="831ed-194">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="831ed-194">Next steps</span></span>
<span data-ttu-id="831ed-195">Para obtener información general sobre la carga, vea [Carga de datos en SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="831ed-195">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="831ed-196">Para obtener más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo de Almacenamiento de datos SQL][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="831ed-196">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
