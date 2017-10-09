---
title: datos de aaaLoad de SQL Server en almacenamiento de datos de SQL Azure (copia masiva bcp) | Documentos de Microsoft
description: "Un pequeño tamaño de datos, se utiliza bcp tooexport datos de archivos de SQL Server tooflat e importar los datos de hello directamente en el almacenamiento de datos de SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: f87d8d7c-8276-43c5-90e7-d4ccc0e3a224
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: a03b5403d123e8814ae73a7cce8e6851c8b264a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a><span data-ttu-id="e0676-103">Carga de datos de SQL Server en Almacenamiento de datos SQL de Azure (archivos planos)</span><span class="sxs-lookup"><span data-stu-id="e0676-103">Load data from SQL Server into Azure SQL Data Warehouse (flat files)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e0676-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="e0676-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="e0676-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="e0676-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="e0676-106">bcp</span><span class="sxs-lookup"><span data-stu-id="e0676-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="e0676-107">Para conjuntos de datos pequeños, puede usar datos de tooexport Hola bcp utilidad de línea de comandos de SQL Server y, a continuación, cargarlo directamente del almacenamiento de datos SQL tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e0676-107">For small data sets, you can use hello bcp command-line utility tooexport data from SQL Server and then load it directly tooAzure SQL Data Warehouse.</span></span>

<span data-ttu-id="e0676-108">En este tutorial, usará bcp para:</span><span class="sxs-lookup"><span data-stu-id="e0676-108">In this tutorial, you will use bcp to:</span></span>

* <span data-ttu-id="e0676-109">Exportar una tabla a partir de SQL Server mediante la utilidad bcp Hola comando (o crear un archivo de ejemplo simple)</span><span class="sxs-lookup"><span data-stu-id="e0676-109">Export a table from from SQL Server by using hello bcp out command (or create a simple sample file)</span></span>
* <span data-ttu-id="e0676-110">Tabla de Hola de importación de un almacén de datos de archivo sin formato tooSQL.</span><span class="sxs-lookup"><span data-stu-id="e0676-110">Import hello table from a flat file tooSQL Data Warehouse.</span></span>
* <span data-ttu-id="e0676-111">Crear estadísticas en datos cargado de saludo.</span><span class="sxs-lookup"><span data-stu-id="e0676-111">Create statistics on hello loaded data.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="e0676-112">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="e0676-112">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="e0676-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e0676-113">Prerequisites</span></span>
<span data-ttu-id="e0676-114">toostep a través de este tutorial, necesitará:</span><span class="sxs-lookup"><span data-stu-id="e0676-114">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="e0676-115">Una base de datos de Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="e0676-115">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="e0676-116">utilidad de línea de comandos de Hello bcp instalado</span><span class="sxs-lookup"><span data-stu-id="e0676-116">hello bcp command-line utility installed</span></span>
* <span data-ttu-id="e0676-117">utilidad de línea de comandos de sqlcmd Hola instalada</span><span class="sxs-lookup"><span data-stu-id="e0676-117">hello sqlcmd command-line utility installed</span></span>

<span data-ttu-id="e0676-118">Puede descargar las utilidades de bcp y sqlcmd de Hola de hello [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="e0676-118">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="e0676-119">Datos en los formatos ASCII o UTF-16</span><span class="sxs-lookup"><span data-stu-id="e0676-119">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="e0676-120">Si está tratando de este tutorial con sus propios datos, necesita los datos toouse Hola ASCII o la codificación UTF-16 dado bcp no es compatible con UTF-8.</span><span class="sxs-lookup"><span data-stu-id="e0676-120">If you are trying this tutorial with your own data, your data needs toouse hello ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

<span data-ttu-id="e0676-121">PolyBase admite UTF-8, pero aún no es compatible con UTF-16.</span><span class="sxs-lookup"><span data-stu-id="e0676-121">PolyBase supports UTF-8 but doesn't yet support UTF-16.</span></span> <span data-ttu-id="e0676-122">Tenga en cuenta que si desea que bcp toocombine con PolyBase necesitará tootransform Hola datos tooUTF-8 después de que se exportó desde SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0676-122">Note that if you want toocombine bcp with PolyBase you will need tootransform hello data tooUTF-8 after it is exported from SQL Server.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="e0676-123">1. Creación de una tabla de destino.</span><span class="sxs-lookup"><span data-stu-id="e0676-123">1. Create a destination table</span></span>
<span data-ttu-id="e0676-124">Definir una tabla en el almacén de datos de SQL que será la tabla de destino de Hola para carga Hola.</span><span class="sxs-lookup"><span data-stu-id="e0676-124">Define a table in SQL Data Warehouse that will be hello destination table for hello load.</span></span> <span data-ttu-id="e0676-125">columnas de Hello en la tabla de hello deben corresponder toohello datos en cada fila de su archivo de datos.</span><span class="sxs-lookup"><span data-stu-id="e0676-125">hello columns in hello table must correspond toohello data in each row of your data file.</span></span>

<span data-ttu-id="e0676-126">toocreate una tabla, abra un símbolo del sistema y use sqlcmd.exe toorun Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e0676-126">toocreate a table, open a command prompt and use sqlcmd.exe toorun hello following command:</span></span>

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


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="e0676-127">2. Creación de un archivo de datos de origen</span><span class="sxs-lookup"><span data-stu-id="e0676-127">2. Create a source data file</span></span>
<span data-ttu-id="e0676-128">Abra el Bloc de notas y copie Hola después de líneas de datos en un nuevo archivo de texto y, a continuación, guarde este archivo tooyour directorio temporal local, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="e0676-128">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="e0676-129">Estos datos están en formato ASCII.</span><span class="sxs-lookup"><span data-stu-id="e0676-129">This data is in ASCII format.</span></span>

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

<span data-ttu-id="e0676-130">(Opcional) tooexport sus propios datos de una base de datos de SQL Server, abra un símbolo del sistema y ejecute el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0676-130">(Optional) tooexport your own data from a SQL Server database, open a command prompt and run hello following command.</span></span> <span data-ttu-id="e0676-131">Reemplace TableName, ServerName, DatabaseName, Username y Password por su propia información.</span><span class="sxs-lookup"><span data-stu-id="e0676-131">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-hello-data"></a><span data-ttu-id="e0676-132">3. Cargar datos de Hola</span><span class="sxs-lookup"><span data-stu-id="e0676-132">3. Load hello data</span></span>
<span data-ttu-id="e0676-133">datos de hello tooload, abra un símbolo del sistema y ejecute hello siguiente comando, reemplazando los valores de hello para nombre del servidor, nombre de base de datos, nombre de usuario y contraseña con su propia información.</span><span class="sxs-lookup"><span data-stu-id="e0676-133">tooload hello data, open a command prompt and run hello following command, replacing hello values for Server Name, Database name, Username, and Password with your own information.</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="e0676-134">Utilice este comando tooverify hello se cargaron correctamente los datos</span><span class="sxs-lookup"><span data-stu-id="e0676-134">Use this command tooverify hello data was loaded properly</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="e0676-135">resultados de Hello deberían tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="e0676-135">hello results should look like this:</span></span>

| <span data-ttu-id="e0676-136">DateId</span><span class="sxs-lookup"><span data-stu-id="e0676-136">DateId</span></span> | <span data-ttu-id="e0676-137">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="e0676-137">CalendarQuarter</span></span> | <span data-ttu-id="e0676-138">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="e0676-138">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e0676-139">20150101</span><span class="sxs-lookup"><span data-stu-id="e0676-139">20150101</span></span> |<span data-ttu-id="e0676-140">1</span><span class="sxs-lookup"><span data-stu-id="e0676-140">1</span></span> |<span data-ttu-id="e0676-141">3</span><span class="sxs-lookup"><span data-stu-id="e0676-141">3</span></span> |
| <span data-ttu-id="e0676-142">20150201</span><span class="sxs-lookup"><span data-stu-id="e0676-142">20150201</span></span> |<span data-ttu-id="e0676-143">1</span><span class="sxs-lookup"><span data-stu-id="e0676-143">1</span></span> |<span data-ttu-id="e0676-144">3</span><span class="sxs-lookup"><span data-stu-id="e0676-144">3</span></span> |
| <span data-ttu-id="e0676-145">20150301</span><span class="sxs-lookup"><span data-stu-id="e0676-145">20150301</span></span> |<span data-ttu-id="e0676-146">1</span><span class="sxs-lookup"><span data-stu-id="e0676-146">1</span></span> |<span data-ttu-id="e0676-147">3</span><span class="sxs-lookup"><span data-stu-id="e0676-147">3</span></span> |
| <span data-ttu-id="e0676-148">20150401</span><span class="sxs-lookup"><span data-stu-id="e0676-148">20150401</span></span> |<span data-ttu-id="e0676-149">2</span><span class="sxs-lookup"><span data-stu-id="e0676-149">2</span></span> |<span data-ttu-id="e0676-150">4</span><span class="sxs-lookup"><span data-stu-id="e0676-150">4</span></span> |
| <span data-ttu-id="e0676-151">20150501</span><span class="sxs-lookup"><span data-stu-id="e0676-151">20150501</span></span> |<span data-ttu-id="e0676-152">2</span><span class="sxs-lookup"><span data-stu-id="e0676-152">2</span></span> |<span data-ttu-id="e0676-153">4</span><span class="sxs-lookup"><span data-stu-id="e0676-153">4</span></span> |
| <span data-ttu-id="e0676-154">20150601</span><span class="sxs-lookup"><span data-stu-id="e0676-154">20150601</span></span> |<span data-ttu-id="e0676-155">2</span><span class="sxs-lookup"><span data-stu-id="e0676-155">2</span></span> |<span data-ttu-id="e0676-156">4</span><span class="sxs-lookup"><span data-stu-id="e0676-156">4</span></span> |
| <span data-ttu-id="e0676-157">20150701</span><span class="sxs-lookup"><span data-stu-id="e0676-157">20150701</span></span> |<span data-ttu-id="e0676-158">3</span><span class="sxs-lookup"><span data-stu-id="e0676-158">3</span></span> |<span data-ttu-id="e0676-159">1</span><span class="sxs-lookup"><span data-stu-id="e0676-159">1</span></span> |
| <span data-ttu-id="e0676-160">20150801</span><span class="sxs-lookup"><span data-stu-id="e0676-160">20150801</span></span> |<span data-ttu-id="e0676-161">3</span><span class="sxs-lookup"><span data-stu-id="e0676-161">3</span></span> |<span data-ttu-id="e0676-162">1</span><span class="sxs-lookup"><span data-stu-id="e0676-162">1</span></span> |
| <span data-ttu-id="e0676-163">20150801</span><span class="sxs-lookup"><span data-stu-id="e0676-163">20150801</span></span> |<span data-ttu-id="e0676-164">3</span><span class="sxs-lookup"><span data-stu-id="e0676-164">3</span></span> |<span data-ttu-id="e0676-165">1</span><span class="sxs-lookup"><span data-stu-id="e0676-165">1</span></span> |
| <span data-ttu-id="e0676-166">20151001</span><span class="sxs-lookup"><span data-stu-id="e0676-166">20151001</span></span> |<span data-ttu-id="e0676-167">4</span><span class="sxs-lookup"><span data-stu-id="e0676-167">4</span></span> |<span data-ttu-id="e0676-168">2</span><span class="sxs-lookup"><span data-stu-id="e0676-168">2</span></span> |
| <span data-ttu-id="e0676-169">20151101</span><span class="sxs-lookup"><span data-stu-id="e0676-169">20151101</span></span> |<span data-ttu-id="e0676-170">4</span><span class="sxs-lookup"><span data-stu-id="e0676-170">4</span></span> |<span data-ttu-id="e0676-171">2</span><span class="sxs-lookup"><span data-stu-id="e0676-171">2</span></span> |
| <span data-ttu-id="e0676-172">20151201</span><span class="sxs-lookup"><span data-stu-id="e0676-172">20151201</span></span> |<span data-ttu-id="e0676-173">4</span><span class="sxs-lookup"><span data-stu-id="e0676-173">4</span></span> |<span data-ttu-id="e0676-174">2</span><span class="sxs-lookup"><span data-stu-id="e0676-174">2</span></span> |

## <a name="4-create-statistics"></a><span data-ttu-id="e0676-175">4. Creación de estadísticas</span><span class="sxs-lookup"><span data-stu-id="e0676-175">4. Create statistics</span></span>
<span data-ttu-id="e0676-176">Almacenamiento de datos SQL de Azure aún no admite la creación o actualización automáticas de estadísticas.</span><span class="sxs-lookup"><span data-stu-id="e0676-176">SQL Data Warehouse does not yet support auto-create or auto-update statistics.</span></span> <span data-ttu-id="e0676-177">tooget Hola mejor rendimiento de las consultas, es importante toocreate estadísticas en todas las columnas de todas las tablas después de la primera carga de Hola o después de que se producen cambios sustanciales en datos Hola.</span><span class="sxs-lookup"><span data-stu-id="e0676-177">tooget hello best query performance, it's important toocreate statistics on all columns of all tables after hello first load or after any substantial changes occur in hello data.</span></span> <span data-ttu-id="e0676-178">Para ver una explicación detallada de las estadísticas, vea [Estadísticas][Statistics].</span><span class="sxs-lookup"><span data-stu-id="e0676-178">For a detailed explanation of statistics, see [Statistics][Statistics].</span></span> 

<span data-ttu-id="e0676-179">Siguiente ejecución Hola comando toocreate estadísticas en la tabla recién cargada.</span><span class="sxs-lookup"><span data-stu-id="e0676-179">Run hello following command toocreate statistics on your newly loaded table.</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a><span data-ttu-id="e0676-180">5. Exportación de datos de Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="e0676-180">5. Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="e0676-181">Para divertirse, puede exportar datos de Hola que acabo de cargar volver fuera del almacén de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="e0676-181">For fun, you can export hello data that you just loaded back out of SQL Data Warehouse.</span></span>  <span data-ttu-id="e0676-182">Hola comando tooexport es exactamente Hola igual a la exportación de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0676-182">hello command tooexport is exactly hello same as exporting from SQL Server.</span></span>

<span data-ttu-id="e0676-183">Sin embargo, hay una diferencia en los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0676-183">However, there is a difference in hello results.</span></span> <span data-ttu-id="e0676-184">Puesto que los datos de Hola se almacenan en ubicaciones distribuidas en almacenamiento de datos de SQL, al exportar datos en cada nodo de ejecución se escribe en archivo de salida de toohello de datos.</span><span class="sxs-lookup"><span data-stu-id="e0676-184">Since hello data is stored in distributed locations within SQL Data Warehouse, when you export data each Compute node writes it data toohello output file.</span></span> <span data-ttu-id="e0676-185">orden de Hola de datos de hello en el archivo de salida de hello es probable que toobe diferente del orden de Hola de los datos de hello en el archivo de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0676-185">hello order of hello data in hello output file is likely toobe different than hello order of hello data in hello input file.</span></span>

### <a name="export-a-table-and-compare-exported-results"></a><span data-ttu-id="e0676-186">Exportación de una tabla y comparación de los resultados exportados</span><span class="sxs-lookup"><span data-stu-id="e0676-186">Export a table and compare exported results</span></span>
<span data-ttu-id="e0676-187">toosee Hola datos exportados, abra un símbolo del sistema y ejecute este comando con sus propios parámetros.</span><span class="sxs-lookup"><span data-stu-id="e0676-187">toosee hello exported data, open a command prompt and run this command using your own parameters.</span></span> <span data-ttu-id="e0676-188">NombreDeServidor es Hola nombre del servidor lógico SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e0676-188">ServerName is hello name of your Azure logical SQL Server.</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="e0676-189">Puede comprobar Hola datos se exportaron correctamente, abra el archivo nuevo de hello.</span><span class="sxs-lookup"><span data-stu-id="e0676-189">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="e0676-190">datos de Hello en el archivo hello deben coincidir con el texto hello siguiente, pero es probable que se va a ordenar en un orden diferente:</span><span class="sxs-lookup"><span data-stu-id="e0676-190">hello data in hello file should match hello text below, but will likely be sorted in a different order:</span></span>

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

### <a name="export-hello-results-of-a-query"></a><span data-ttu-id="e0676-191">Exportar resultados de Hola de una consulta</span><span class="sxs-lookup"><span data-stu-id="e0676-191">Export hello results of a query</span></span>
<span data-ttu-id="e0676-192">Puede usar hello **queryout** función de los resultados de hello tooexport de bcp de una consulta en lugar de exportar toda la tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="e0676-192">You can use hello **queryout** function of bcp tooexport hello results of a query instead of exporting hello entire table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e0676-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e0676-193">Next steps</span></span>
<span data-ttu-id="e0676-194">Para obtener información general sobre la carga, vea [Carga de datos en SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="e0676-194">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="e0676-195">Para obtener más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo de Almacenamiento de datos SQL][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="e0676-195">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="e0676-196">Consulte la [información general sobre las tablas][Table Overview] o la [sintaxis de CREATE TABLE][CREATE TABLE syntax] para obtener más información sobre cómo crear una tabla en SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e0676-196">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse.</span></span>

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
