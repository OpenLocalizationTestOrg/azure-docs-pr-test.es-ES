---
title: "Creación de particiones en tablas en SQL Data Warehouse | Microsoft Docs"
description: "Introducción a la creación de particiones en tablas en Almacenamiento de datos SQL de Azure."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 6cef870c-114f-470c-af10-02300c58885d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 3edfd34d368228be32afef48688739639a3b03ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="partitioning-tables-in-sql-data-warehouse"></a><span data-ttu-id="8f779-103">Creación de particiones de tablas en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="8f779-103">Partitioning tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="8f779-104">[Información general][Overview]</span><span class="sxs-lookup"><span data-stu-id="8f779-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="8f779-105">[Tipos de datos][Data Types]</span><span class="sxs-lookup"><span data-stu-id="8f779-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="8f779-106">[Distribución][Distribute]</span><span class="sxs-lookup"><span data-stu-id="8f779-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="8f779-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="8f779-107">[Index][Index]</span></span>
> * <span data-ttu-id="8f779-108">[Partición][Partition]</span><span class="sxs-lookup"><span data-stu-id="8f779-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="8f779-109">[Estadísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="8f779-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="8f779-110">[Temporal][Temporary]</span><span class="sxs-lookup"><span data-stu-id="8f779-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="8f779-111">La creación de particiones es compatible con todos los tipos de tabla de Almacenamiento de datos SQL, entre los que se incluyen almacén de columnas en clúster, índice agrupado y montón.</span><span class="sxs-lookup"><span data-stu-id="8f779-111">Partitioning is supported on all SQL Data Warehouse table types; including clustered columnstore, clustered index, and heap.</span></span>  <span data-ttu-id="8f779-112">La creación de particiones también es compatible con todos los tipos de distribución, incluidos la distribución por hash o la distribución Round Robin.</span><span class="sxs-lookup"><span data-stu-id="8f779-112">Partitioning is also supported on all distribution types, including both hash or round robin distributed.</span></span>  <span data-ttu-id="8f779-113">La creación de particiones permite dividir los datos en grupos de datos más pequeños y en la mayoría de los casos, se realiza en una columna de fecha.</span><span class="sxs-lookup"><span data-stu-id="8f779-113">Partitioning enables you to divide your data into smaller groups of data and in most cases, partitioning is done on a date column.</span></span>

## <a name="benefits-of-partitioning"></a><span data-ttu-id="8f779-114">Ventajas de la creación de particiones</span><span class="sxs-lookup"><span data-stu-id="8f779-114">Benefits of partitioning</span></span>
<span data-ttu-id="8f779-115">La creación de particiones puede beneficiar el mantenimiento de datos y el rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="8f779-115">Partitioning can benefit data maintenance and query performance.</span></span>  <span data-ttu-id="8f779-116">El hecho de que beneficie a ambos aspectos, o solo a uno de ellos, dependerá de la forma en que se carguen los datos y de la misma columna se puede usar para ambos propósitos, ya que la creación de particiones solo se puede hacer en una columna.</span><span class="sxs-lookup"><span data-stu-id="8f779-116">Whether it benefits both or just one is dependent on how data is loaded and whether the same column can be used for both purposes, since partitioning can only be done on one column.</span></span>

### <a name="benefits-to-loads"></a><span data-ttu-id="8f779-117">Ventajas para las cargas</span><span class="sxs-lookup"><span data-stu-id="8f779-117">Benefits to loads</span></span>
<span data-ttu-id="8f779-118">La principal ventaja de la creación de particiones en Almacenamiento de datos SQL es mejorar la eficiencia y el rendimiento de la carga de datos mediante el uso de la eliminación, conmutación y combinación de particiones.</span><span class="sxs-lookup"><span data-stu-id="8f779-118">The primary benefit of partitioning in SQL Data Warehouse is improve the efficiency and performance of loading data by use of partition deletion, switching and merging.</span></span>  <span data-ttu-id="8f779-119">En la mayoría de los casos, la creación de particiones de los datos se realiza en una columna de fecha que está estrechamente relacionada con la secuencia con la que se cargan los datos en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="8f779-119">In most cases data is partitioned on a date column that is closely tied to the sequence which the data is loaded to the database.</span></span>  <span data-ttu-id="8f779-120">Una de las mayores ventajas de utilizar particiones para mantener los datos es que se evita el registro de transacciones.</span><span class="sxs-lookup"><span data-stu-id="8f779-120">One of the greatest benefits of using partitions to maintain data it the avoidance of transaction logging.</span></span>  <span data-ttu-id="8f779-121">Aunque la mera inserción, actualización o eliminación de datos puede ser el enfoque más sencillo, con un poco de esfuerzo, el uso de la creación de particiones durante el proceso de carga puede mejorar considerablemente el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="8f779-121">While simply inserting, updating or deleting data can be the most straightforward approach, with a little thought and effort, using partitioning during your load process can substantially improve performance.</span></span>

<span data-ttu-id="8f779-122">La conmutación de particiones se puede utilizar para quitar o reemplazar rápidamente cualquier sección de una tabla.</span><span class="sxs-lookup"><span data-stu-id="8f779-122">Partition switching can be used to quickly remove or replace a section of a table.</span></span>  <span data-ttu-id="8f779-123">Por ejemplo, una tabla de datos de ventas podría contener datos solo de los últimos 36 meses.</span><span class="sxs-lookup"><span data-stu-id="8f779-123">For example, a sales fact table might contain just data for the past 36 months.</span></span>  <span data-ttu-id="8f779-124">Al final de cada mes, el mes más antiguo de datos de ventas se elimina de la tabla.</span><span class="sxs-lookup"><span data-stu-id="8f779-124">At the end of every month, the oldest month of sales data is deleted from the table.</span></span>  <span data-ttu-id="8f779-125">Estos datos pueden eliminarse mediante el uso de una instrucción delete para eliminar los datos del mes más antiguo.</span><span class="sxs-lookup"><span data-stu-id="8f779-125">This data could be deleted by using a delete statement to delete the data for the oldest month.</span></span>  <span data-ttu-id="8f779-126">Sin embargo, la eliminación una gran cantidad de datos fila a fila con una instrucción delete puede tardar mucho tiempo, así como crear el riesgo de transacciones grandes que podría tardar mucho tiempo en revertirse si algo va mal.</span><span class="sxs-lookup"><span data-stu-id="8f779-126">However, deleting a large amount of data row-by-row with a delete statement can take a very long time, as well as create the risk of large transactions which could take a long time to rollback if something goes wrong.</span></span>  <span data-ttu-id="8f779-127">Un enfoque mejor es simplemente colocar la partición de datos más antigua.</span><span class="sxs-lookup"><span data-stu-id="8f779-127">A more optimal approach is to simply drop the oldest partition of data.</span></span>  <span data-ttu-id="8f779-128">Aunque la eliminación de las filas individuales podría tardar horas, la de toda una partición puede tardar segundos.</span><span class="sxs-lookup"><span data-stu-id="8f779-128">Where deleting the individual rows could take hours, deleting an entire partition could take seconds.</span></span>

### <a name="benefits-to-queries"></a><span data-ttu-id="8f779-129">Ventajas para las consultas</span><span class="sxs-lookup"><span data-stu-id="8f779-129">Benefits to queries</span></span>
<span data-ttu-id="8f779-130">La creación de particiones también puede utilizarse para mejorar el rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="8f779-130">Partitioning can also be used to improve query performance.</span></span>  <span data-ttu-id="8f779-131">Si una consulta aplica un filtro a una columna con particiones, el examen puede verse limitado a las particiones cualificadas, que pueden ser un subconjunto mucho menor de los datos, con lo que se evita un examen de toda la tabla.</span><span class="sxs-lookup"><span data-stu-id="8f779-131">If a query applies a filter on a partitioned column, this can limit the scan to only the qualifying partitions which may be a much smaller subset of the data, avoiding a full table scan.</span></span>  <span data-ttu-id="8f779-132">Con la introducción de índices de almacén de columnas en clúster, las ventajas de rendimiento de la eliminación del predicado son menores, pero en algunos casos puede haber beneficios para las consultas.</span><span class="sxs-lookup"><span data-stu-id="8f779-132">With the introduction of clustered columnstore indexes, the predicate elimination performance benefits are less beneficial, but in some cases there can be a benefit to queries.</span></span>  <span data-ttu-id="8f779-133">Por ejemplo, si la tabla de datos de ventas se particiona en 36 meses con el campo de fecha de ventas, las consultas que se filtren por esa fecha de ventas pueden omitir la búsqueda en las particiones que no se ajusten al filtro.</span><span class="sxs-lookup"><span data-stu-id="8f779-133">For example, if the sales fact table is partitioned into 36 months using the sales date field, then queries that filter on the sale date can skip searching in partitions that don’t match the filter.</span></span>

## <a name="partition-sizing-guidance"></a><span data-ttu-id="8f779-134">Guía sobre el tamaño de las particiones</span><span class="sxs-lookup"><span data-stu-id="8f779-134">Partition sizing guidance</span></span>
<span data-ttu-id="8f779-135">Aunque la creación de particiones se puede usar para mejorar el rendimiento en algunos escenarios, la creación de una tabla con **demasiadas** particiones pueden afectar negativamente al rendimiento en algunas circunstancias.</span><span class="sxs-lookup"><span data-stu-id="8f779-135">While partitioning can be used to improve performance some scenarios, creating a table with **too many** partitions can hurt performance under some circumstances.</span></span>  <span data-ttu-id="8f779-136">Estas cuestiones se dan especialmente en las tablas de almacén de columnas en clúster.</span><span class="sxs-lookup"><span data-stu-id="8f779-136">These concerns are especially true for clustered columnstore tables.</span></span>  <span data-ttu-id="8f779-137">Para que la creación de particiones sea útil, es importante saber cuándo usarla y el número de particiones que se deben crear.</span><span class="sxs-lookup"><span data-stu-id="8f779-137">For partitioning to be helpful, it is important to understand when to use partitioning and the number of partitions to create.</span></span>  <span data-ttu-id="8f779-138">No hay ninguna regla inamovible con respecto a cuántas particiones son demasiadas, depende de los datos y del número de particiones en que se realiza la carga de manera simultánea.</span><span class="sxs-lookup"><span data-stu-id="8f779-138">There is no hard fast rule as to how many partitions are too many, it depends on your data and how many partitions you are loading to simultaneously.</span></span>  <span data-ttu-id="8f779-139">No obstante, como regla general, se recomienda agregar entre decenas y centenares de particiones, no millares.</span><span class="sxs-lookup"><span data-stu-id="8f779-139">But as a general rule of thumb, think of adding 10s to 100s of partitions, not 1000s.</span></span>

<span data-ttu-id="8f779-140">Al crear particiones en tablas de **almacén de columnas en clúster** , es importante considerar el número de filas que se colocarán en cada partición.</span><span class="sxs-lookup"><span data-stu-id="8f779-140">When creating partitioning on **clustered columnstore** tables, it is important to consider how many rows will land in each partition.</span></span>  <span data-ttu-id="8f779-141">Para que tanto la compresión como el rendimiento de las tablas de almacén de columnas en clúster sean óptimos, se necesita un mínimo de un millón de filas por partición y distribución.</span><span class="sxs-lookup"><span data-stu-id="8f779-141">For optimal compression and performance of clustered columnstore tables, a minimum of 1 million rows per distribution and partition is needed.</span></span>  <span data-ttu-id="8f779-142">Antes de que se creen particiones, Almacenamiento de datos SQL ya divide cada tabla en 60 bases de datos distribuidas.</span><span class="sxs-lookup"><span data-stu-id="8f779-142">Before partitions are created, SQL Data Warehouse already divides each table into 60 distributed databases.</span></span>  <span data-ttu-id="8f779-143">Todas las particiones que se agreguen a una tabla se sumarán a las distribuciones creadas en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="8f779-143">Any partitioning added to a table is in addition to the distributions created behind the scenes.</span></span>  <span data-ttu-id="8f779-144">Usando este ejemplo, si la tabla de datos de ventas contenía 36 particiones mensuales, y dado que Almacenamiento de datos SQL tiene 60 distribuciones, la tabla de datos de ventas debería contener 60 millones de filas por mes, o 2 100 millones de filas cuando se rellenen todos los meses.</span><span class="sxs-lookup"><span data-stu-id="8f779-144">Using this example, if the sales fact table contained 36 monthly partitions, and given that SQL Data Warehouse has 60 distributions, then the sales fact table should contain 60 million rows per month, or 2.1 billion rows when all months are populated.</span></span>  <span data-ttu-id="8f779-145">Si una tabla contiene muchas menos filas que el número mínimo recomendado de filas por partición, considere utilizar menos particiones para hacer que aumente el número de filas por partición.</span><span class="sxs-lookup"><span data-stu-id="8f779-145">If a table contains significantly less rows than the recommended minimum number of rows per partition, consider using fewer partitions in order to make increase the number of rows per partition.</span></span>  <span data-ttu-id="8f779-146">Consulte también el artículo sobre [indexación][Index] que incluye las consultas que se pueden ejecutar en SQL Data Warehouse para evaluar la calidad de los índices de almacén de columnas en clúster.</span><span class="sxs-lookup"><span data-stu-id="8f779-146">Also see the [Indexing][Index] article which includes queries that can be run on SQL Data Warehouse to assess the quality of cluster columnstore indexes.</span></span>

## <a name="syntax-difference-from-sql-server"></a><span data-ttu-id="8f779-147">Diferencia con respecto a la sintaxis de SQL Server</span><span class="sxs-lookup"><span data-stu-id="8f779-147">Syntax difference from SQL Server</span></span>
<span data-ttu-id="8f779-148">Almacenamiento de datos SQL introduce una definición simplificada de particiones que difiere ligeramente de la de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8f779-148">SQL Data Warehouse introduces a simplified definition of partitions which is slightly different from SQL Server.</span></span>  <span data-ttu-id="8f779-149">Las funciones y los esquemas de la creación de particiones no se usan en Almacenamiento de datos SQL como en SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8f779-149">Partitioning functions and schemes are not used in SQL Data Warehouse as they are in SQL Server.</span></span>  <span data-ttu-id="8f779-150">En su lugar, lo único que se debe hacer es identificar la columna con particiones y los puntos limítrofes.</span><span class="sxs-lookup"><span data-stu-id="8f779-150">Instead, all you need to do is identify partitioned column and the boundary points.</span></span>  <span data-ttu-id="8f779-151">Aunque la sintaxis de la creación de particiones puede variar ligeramente con respecto a la de SQL Server, los conceptos básicos son los mismos.</span><span class="sxs-lookup"><span data-stu-id="8f779-151">While the syntax of partitioning may be slightly different from SQL Server, the basic concepts are the same.</span></span>  <span data-ttu-id="8f779-152">SQL Server y Almacenamiento de datos SQL admiten una columna de partición por tabla, que puede ser una partición con intervalos.</span><span class="sxs-lookup"><span data-stu-id="8f779-152">SQL Server and SQL Data Warehouse support one partition column per table, which can be ranged partition.</span></span>  <span data-ttu-id="8f779-153">Para obtener más información sobre las particiones, consulte [Tablas e índices con particiones][Partitioned Tables and Indexes].</span><span class="sxs-lookup"><span data-stu-id="8f779-153">To learn more about partitioning, see [Partitioned Tables and Indexes][Partitioned Tables and Indexes].</span></span>

<span data-ttu-id="8f779-154">El siguiente ejemplo de una instrucción [CREATE TABLE][CREATE TABLE] con particiones de SQL Data Warehouse particiona la tabla FactInternetSales en la columna OrderDateKey:</span><span class="sxs-lookup"><span data-stu-id="8f779-154">The below example of a SQL Data Warehouse partitioned [CREATE TABLE][CREATE TABLE] statement, partitions the FactInternetSales table on the OrderDateKey column:</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

## <a name="migrating-partitioning-from-sql-server"></a><span data-ttu-id="8f779-155">Migración de particiones de SQL Server</span><span class="sxs-lookup"><span data-stu-id="8f779-155">Migrating partitioning from SQL Server</span></span>
<span data-ttu-id="8f779-156">Para migrar las definiciones de particiones de SQL Server a Almacenamiento de datos SQL:</span><span class="sxs-lookup"><span data-stu-id="8f779-156">To migrate SQL Server partition definitions to SQL Data Warehouse simply:</span></span>

* <span data-ttu-id="8f779-157">Elimine el [esquema de particiones][partition scheme] de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8f779-157">Eliminate the SQL Server [partition scheme][partition scheme].</span></span>
* <span data-ttu-id="8f779-158">Agregue la definición de [función de partición][partition function] a CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="8f779-158">Add the [partition function][partition function] definition to your CREATE TABLE.</span></span>

<span data-ttu-id="8f779-159">Si va a migrar una tabla con particiones de una instancia de SQL Server, la instrucción SQL siguiente puede ayudarle a consultar el número de filas que se encuentran en cada partición.</span><span class="sxs-lookup"><span data-stu-id="8f779-159">If you are migrating a partitioned table from a SQL Server instance the below SQL can help you to interrogate the number of rows that are in each partition.</span></span>  <span data-ttu-id="8f779-160">Tenga en cuenta que si se utiliza la misma granularidad de particiones en Almacenamiento de datos SQL, el número de filas por partición se reducirá en un factor de 60.</span><span class="sxs-lookup"><span data-stu-id="8f779-160">Keep in mind that if the same partitioning granularity is used on SQL Data Warehouse, the number of rows per partition will decrease by a factor of 60.</span></span>  

```sql
-- Partition information for a SQL Server Database
SELECT      s.[name]                        AS      [schema_name]
,           t.[name]                        AS      [table_name]
,           i.[name]                        AS      [index_name]
,           p.[partition_number]            AS      [partition_number]
,           SUM(a.[used_pages]*8.0)         AS      [partition_size_kb]
,           SUM(a.[used_pages]*8.0)/1024    AS      [partition_size_mb]
,           SUM(a.[used_pages]*8.0)/1048576 AS      [partition_size_gb]
,           p.[rows]                        AS      [partition_row_count]
,           rv.[value]                      AS      [partition_boundary_value]
,           p.[data_compression_desc]       AS      [partition_compression_desc]
FROM        sys.schemas s
JOIN        sys.tables t                    ON      t.[schema_id]         = s.[schema_id]
JOIN        sys.partitions p                ON      p.[object_id]         = t.[object_id]
JOIN        sys.allocation_units a          ON      a.[container_id]      = p.[partition_id]
JOIN        sys.indexes i                   ON      i.[object_id]         = p.[object_id]
                                            AND     i.[index_id]          = p.[index_id]
JOIN        sys.data_spaces ds              ON      ds.[data_space_id]    = i.[data_space_id]
LEFT JOIN   sys.partition_schemes ps        ON      ps.[data_space_id]    = ds.[data_space_id]
LEFT JOIN   sys.partition_functions pf      ON      pf.[function_id]      = ps.[function_id]
LEFT JOIN   sys.partition_range_values rv   ON      rv.[function_id]      = pf.[function_id]
                                            AND     rv.[boundary_id]      = p.[partition_number]
WHERE       p.[index_id] <=1
GROUP BY    s.[name]
,           t.[name]
,           i.[name]
,           p.[partition_number]
,           p.[rows]
,           rv.[value]
,           p.[data_compression_desc]
;
```

## <a name="workload-management"></a><span data-ttu-id="8f779-161">Administración de cargas de trabajo</span><span class="sxs-lookup"><span data-stu-id="8f779-161">Workload management</span></span>
<span data-ttu-id="8f779-162">Una última consideración que debe tenerse a la hora de decidir el número de particiones de una tabla es la [administración de la carga de trabajo][workload management].</span><span class="sxs-lookup"><span data-stu-id="8f779-162">One final piece consideration to factor in to the table partition decision is [workload management][workload management].</span></span>  <span data-ttu-id="8f779-163">La administración de la carga de trabajo en Almacenamiento de datos SQL es principalmente la administración de memoria y de la concurrencia.</span><span class="sxs-lookup"><span data-stu-id="8f779-163">Workload management in SQL Data Warehouse is primarily the management of memory and concurrency.</span></span>  <span data-ttu-id="8f779-164">En Almacenamiento de datos SQL, las clases de recursos son las que rigen la cantidad máxima de memoria que se asigna a cada distribución durante la ejecución de la consulta.</span><span class="sxs-lookup"><span data-stu-id="8f779-164">In SQL Data Warehouse the maximum memory allocated to each distribution during query execution is governed resource classes.</span></span>  <span data-ttu-id="8f779-165">Lo ideal es que los tamaños de las particiones dependan de otros factores, como las necesidades de creación de índices de almacén de columnas en clúster que tiene la memoria.</span><span class="sxs-lookup"><span data-stu-id="8f779-165">Ideally your partitions will be sized in consideration of other factors like the memory needs of building clustered columnstore indexes.</span></span>  <span data-ttu-id="8f779-166">Los índices de almacén de columnas en clúster suponen una mayor ventaja cuando se les asigna más memoria.</span><span class="sxs-lookup"><span data-stu-id="8f779-166">Clustered columnstore indexes benefit greatly when they are allocated more memory.</span></span>  <span data-ttu-id="8f779-167">Por lo tanto, deberá asegurarse de que ninguna recompilación del índice de particiones se queda sin memoria.</span><span class="sxs-lookup"><span data-stu-id="8f779-167">Therefore, you will want to ensure that a partition index rebuild is not starved of memory.</span></span> <span data-ttu-id="8f779-168">Para aumentar la cantidad de memoria disponible para las consultas se puede conmutar del rol predeterminado, smallrc, a uno de los otros roles, como largerc.</span><span class="sxs-lookup"><span data-stu-id="8f779-168">Increasing the amount of memory available to your query can be achieved by switching from the default role, smallrc, to one of the other roles such as largerc.</span></span>

<span data-ttu-id="8f779-169">Para obtener información sobre la asignación de memoria por distribución, consulte las vistas de administración dinámica del regulador de recursos.</span><span class="sxs-lookup"><span data-stu-id="8f779-169">Information on the allocation of memory per distribution is available by querying the resource governor dynamic management views.</span></span> <span data-ttu-id="8f779-170">En realidad, la concesión de memoria será inferior a la que se indica en las ilustraciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="8f779-170">In reality your memory grant will be less than the figures below.</span></span> <span data-ttu-id="8f779-171">Sin embargo, esto proporciona un nivel de instrucciones que puede utilizar al cambiar el tamaño de las particiones para las operaciones de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="8f779-171">However, this provides a level of guidance that you can use when sizing your partitions for data management operations.</span></span>  <span data-ttu-id="8f779-172">Intente evitar cambiar el tamaño de las particiones por encima de la concesión de memoria proporcionada por la clase de recurso extra grande.</span><span class="sxs-lookup"><span data-stu-id="8f779-172">Try to avoid sizing your partitions beyond the memory grant provided by the extra large resource class.</span></span> <span data-ttu-id="8f779-173">Si las particiones crecen más allá de lo que se muestra en esta ilustración, se corre el riesgo de presionar la memoria, lo que a su vez conlleva una compresión menos óptima.</span><span class="sxs-lookup"><span data-stu-id="8f779-173">If your partitions grow beyond this figure you run the risk of memory pressure which in turn leads to less optimal compression.</span></span>

```sql
SELECT  rp.[name]                                AS [pool_name]
,       rp.[max_memory_kb]                        AS [max_memory_kb]
,       rp.[max_memory_kb]/1024                    AS [max_memory_mb]
,       rp.[max_memory_kb]/1048576                AS [mex_memory_gb]
,       rp.[max_memory_percent]                    AS [max_memory_percent]
,       wg.[name]                                AS [group_name]
,       wg.[importance]                            AS [group_importance]
,       wg.[request_max_memory_grant_percent]    AS [request_max_memory_grant_percent]
FROM    sys.dm_pdw_nodes_resource_governor_workload_groups    wg
JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools    rp ON wg.[pool_id] = rp.[pool_id]
WHERE   wg.[name] like 'SloDWGroup%'
AND     rp.[name]    = 'SloDWPool'
;
```

## <a name="partition-switching"></a><span data-ttu-id="8f779-174">Modificación de particiones</span><span class="sxs-lookup"><span data-stu-id="8f779-174">Partition switching</span></span>
<span data-ttu-id="8f779-175">Almacenamiento de datos SQL admite la separación, combinación y modificación de particiones.</span><span class="sxs-lookup"><span data-stu-id="8f779-175">SQL Data Warehouse supports partition splitting, merging, and switching.</span></span> <span data-ttu-id="8f779-176">Cada una de estas funciones se ejecuta mediante la instrucción [ALTER TABLE][ALTER TABLE].</span><span class="sxs-lookup"><span data-stu-id="8f779-176">Each of these functions is excuted using the [ALTER TABLE][ALTER TABLE] statement.</span></span>

<span data-ttu-id="8f779-177">Para cambiar particiones entre dos tablas, debe asegurarse de que las particiones se alinean en sus límites correspondientes y que las definiciones de tablas coinciden.</span><span class="sxs-lookup"><span data-stu-id="8f779-177">To switch partitions between two tables you must ensure that the partitions align on their respective boundaries and that the table definitions match.</span></span> <span data-ttu-id="8f779-178">Como las restricciones check no están disponibles para aplicar el intervalo de valores en una tabla, la tabla de origen debe contener los mismos límites de partición que la tabla de destino.</span><span class="sxs-lookup"><span data-stu-id="8f779-178">As check constraints are not available to enforce the range of values in a table the source table must contain the same partition boundaries as the target table.</span></span> <span data-ttu-id="8f779-179">Si no es así, el modificador de particionamiento generará un error, ya que los metadatos de la partición no estarán sincronizados.</span><span class="sxs-lookup"><span data-stu-id="8f779-179">If this is not the case, then the partition switch will fail as the partition metadata will not be synchronized.</span></span>

### <a name="how-to-split-a-partition-that-contains-data"></a><span data-ttu-id="8f779-180">División de una partición que contiene datos</span><span class="sxs-lookup"><span data-stu-id="8f779-180">How to split a partition that contains data</span></span>
<span data-ttu-id="8f779-181">El método más eficaz para dividir una partición que ya contiene datos es usar una instrucción `CTAS` .</span><span class="sxs-lookup"><span data-stu-id="8f779-181">The most efficient method to split a partition that already contains data is to use a `CTAS` statement.</span></span> <span data-ttu-id="8f779-182">Si la tabla con particiones es un almacén de columnas en clúster, la partición de tabla debe estar vacía antes de que se pueda dividir.</span><span class="sxs-lookup"><span data-stu-id="8f779-182">If the partitioned table is a clustered columnstore then the table partition must be empty before it can be split.</span></span>

<span data-ttu-id="8f779-183">A continuación, se muestra una tabla de ejemplo con particiones del almacén de columnas que contiene una fila en cada partición:</span><span class="sxs-lookup"><span data-stu-id="8f779-183">Below is a sample partitioned columnstore table containing one row in each partition:</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
        [ProductKey]            int          NOT NULL
    ,   [OrderDateKey]          int          NOT NULL
    ,   [CustomerKey]           int          NOT NULL
    ,   [PromotionKey]          int          NOT NULL
    ,   [SalesOrderNumber]      nvarchar(20) NOT NULL
    ,   [OrderQuantity]         smallint     NOT NULL
    ,   [UnitPrice]             money        NOT NULL
    ,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101
                    )
                )
)
;

INSERT INTO dbo.FactInternetSales
VALUES (1,19990101,1,1,1,1,1,1);
INSERT INTO dbo.FactInternetSales
VALUES (1,20000101,1,1,1,1,1,1);


CREATE STATISTICS Stat_dbo_FactInternetSales_OrderDateKey ON dbo.FactInternetSales(OrderDateKey);
```

> [!NOTE]
> <span data-ttu-id="8f779-184">Al crear el objeto estadístico, nos aseguramos de que los metadatos de la tabla son más precisos.</span><span class="sxs-lookup"><span data-stu-id="8f779-184">By Creating the statistic object, we ensure that table metadata is more accurate.</span></span> <span data-ttu-id="8f779-185">Si se omite la creación de estadísticas, Almacenamiento de datos SQL utilizará los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="8f779-185">If we omit creating statistics, then SQL Data Warehouse will use default values.</span></span> <span data-ttu-id="8f779-186">Para obtener detalles sobre las estadísticas, consulte las [estadísticas][statistics].</span><span class="sxs-lookup"><span data-stu-id="8f779-186">For details on statistics please review [statistics][statistics].</span></span>
> 
> 

<span data-ttu-id="8f779-187">A continuación, podemos consultar el recuento de filas mediante la vista de catálogo `sys.partitions` :</span><span class="sxs-lookup"><span data-stu-id="8f779-187">We can then query for the row count using the `sys.partitions` catalog view:</span></span>

```sql
SELECT  QUOTENAME(s.[name])+'.'+QUOTENAME(t.[name]) as Table_name
,       i.[name] as Index_name
,       p.partition_number as Partition_nmbr
,       p.[rows] as Row_count
,       p.[data_compression_desc] as Data_Compression_desc
FROM    sys.partitions p
JOIN    sys.tables     t    ON    p.[object_id]   = t.[object_id]
JOIN    sys.schemas    s    ON    t.[schema_id]   = s.[schema_id]
JOIN    sys.indexes    i    ON    p.[object_id]   = i.[object_Id]
                            AND   p.[index_Id]    = i.[index_Id]
WHERE t.[name] = 'FactInternetSales'
;
```

<span data-ttu-id="8f779-188">Si intentamos dividir esta tabla, se producirá un error:</span><span class="sxs-lookup"><span data-stu-id="8f779-188">If we try to split this table, we will get an error:</span></span>

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="8f779-189">La cláusula Msg 35346, Level 15, State 1, Line 44 SPLIT de la instrucción ALTER PARTITION ha generado un error porque la partición no está vacía.</span><span class="sxs-lookup"><span data-stu-id="8f779-189">Msg 35346, Level 15, State 1, Line 44 SPLIT clause of ALTER PARTITION statement failed because the partition is not empty.</span></span>  <span data-ttu-id="8f779-190">Solo las particiones vacías se pueden dividir cuando existe un índice de almacén de columnas en la tabla.</span><span class="sxs-lookup"><span data-stu-id="8f779-190">Only empty partitions can be split in when a columnstore index exists on the table.</span></span> <span data-ttu-id="8f779-191">Considere la posibilidad de deshabilitar el índice de almacén de columnas antes de emitir la instrucción ALTER PARTITION y, a continuación, vuelva a generar el índice de almacén de columnas una vez completada la instrucción ALTER PARTITION.</span><span class="sxs-lookup"><span data-stu-id="8f779-191">Consider disabling the columnstore index before issuing the ALTER PARTITION statement, then rebuilding the columnstore index after ALTER PARTITION is complete.</span></span>

<span data-ttu-id="8f779-192">Sin embargo, se puede utilizar `CTAS` para crear una nueva tabla que contenga los datos.</span><span class="sxs-lookup"><span data-stu-id="8f779-192">However, we can use `CTAS` to create a new table to hold our data.</span></span>

```sql
CREATE TABLE dbo.FactInternetSales_20000101
    WITH    (   DISTRIBUTION = HASH(ProductKey)
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101
                                )
                            )
            )
AS
SELECT *
FROM    FactInternetSales
WHERE   1=2
;
```

<span data-ttu-id="8f779-193">Se permite la modificación porque los límites de partición están alineados.</span><span class="sxs-lookup"><span data-stu-id="8f779-193">As the partition boundaries are aligned a switch is permitted.</span></span> <span data-ttu-id="8f779-194">Esto dejará la tabla de origen con una partición vacía que podemos dividir posteriormente.</span><span class="sxs-lookup"><span data-stu-id="8f779-194">This will leave the source table with an empty partition that we can subsequently split.</span></span>

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 TO  FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="8f779-195">Lo único que falta por hacer es alinear los datos con los nuevos límites de partición mediante `CTAS` y volver a cambiar los datos a la tabla principal.</span><span class="sxs-lookup"><span data-stu-id="8f779-195">All that is left to do is to align our data to the new partition boundaries using `CTAS` and switch our data back in to the main table</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_20000101_20010101]
    WITH    (   DISTRIBUTION = HASH([ProductKey])
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101,20010101
                                )
                            )
            )
AS
SELECT  *
FROM    [dbo].[FactInternetSales_20000101]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

ALTER TABLE dbo.FactInternetSales_20000101_20010101 SWITCH PARTITION 2 TO dbo.FactInternetSales PARTITION 2;
```

<span data-ttu-id="8f779-196">Después de haber transferido los datos, es buena idea actualizar las estadísticas en la tabla de destino para asegurarse de que reflejan con precisión la distribución nueva de los datos en sus respectivas particiones:</span><span class="sxs-lookup"><span data-stu-id="8f779-196">Once you have completed the movement of the data it is a good idea to refresh the statistics on the target table to ensure they accurately reflect the new distribution of the data in their respective partitions:</span></span>

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a><span data-ttu-id="8f779-197">Control de código fuente de particiones de tabla</span><span class="sxs-lookup"><span data-stu-id="8f779-197">Table partitioning source control</span></span>
<span data-ttu-id="8f779-198">Para evitar que la definición de tabla se **oxide** en el sistema de control de código fuente, es conveniente tener en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8f779-198">To avoid your table definition from **rusting** in your source control system you may want to consider the following approach:</span></span>

1. <span data-ttu-id="8f779-199">Crear la tabla como una tabla con particiones, pero sin valores de partición</span><span class="sxs-lookup"><span data-stu-id="8f779-199">Create the table as a partitioned table but with no partition values</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    ()
                )
)
;
```

1. <span data-ttu-id="8f779-200">`SPLIT` la tabla como parte del proceso de implementación:</span><span class="sxs-lookup"><span data-stu-id="8f779-200">`SPLIT` the table as part of the deployment process:</span></span>

```sql
-- Create a table containing the partition boundaries

CREATE TABLE #partitions
WITH
(
    LOCATION = USER_DB
,   DISTRIBUTION = HASH(ptn_no)
)
AS
SELECT  ptn_no
,       ROW_NUMBER() OVER (ORDER BY (ptn_no)) as seq_no
FROM    (
        SELECT CAST(20000101 AS INT) ptn_no
        UNION ALL
        SELECT CAST(20010101 AS INT)
        UNION ALL
        SELECT CAST(20020101 AS INT)
        UNION ALL
        SELECT CAST(20030101 AS INT)
        UNION ALL
        SELECT CAST(20040101 AS INT)
        ) a
;

-- Iterate over the partition boundaries and split the table

DECLARE @c INT = (SELECT COUNT(*) FROM #partitions)
,       @i INT = 1                                 --iterator for while loop
,       @q NVARCHAR(4000)                          --query
,       @p NVARCHAR(20)     = N''                  --partition_number
,       @s NVARCHAR(128)    = N'dbo'               --schema
,       @t NVARCHAR(128)    = N'FactInternetSales' --table
;

WHILE @i <= @c
BEGIN
    SET @p = (SELECT ptn_no FROM #partitions WHERE seq_no = @i);
    SET @q = (SELECT N'ALTER TABLE '+@s+N'.'+@t+N' SPLIT RANGE ('+@p+N');');

    -- PRINT @q;
    EXECUTE sp_executesql @q;

    SET @i+=1;
END

-- Code clean-up

DROP TABLE #partitions;
```

<span data-ttu-id="8f779-201">Con este enfoque, el código de control de código fuente permanece estático y se permite que los valores de límite de partición sean dinámicos, de tal forma que evoluciona con el almacenamiento de datos con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="8f779-201">With this approach the code in source control remains static and the partitioning boundary values are allowed to be dynamic; evolving with the warehouse over time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f779-202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8f779-202">Next steps</span></span>
<span data-ttu-id="8f779-203">Para obtener más información, consulte los artículos sobre [información general de tablas][Overview], [tipos de datos de tabla][Data Types], [distribución de una tabla][Distribute], [indexación de una tabla][Index], [mantenimiento de estadísticas de tabla][Statistics] y [tablas temporales][Temporary].</span><span class="sxs-lookup"><span data-stu-id="8f779-203">To learn more, see the articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="8f779-204">Para obtener más información sobre los procedimientos recomendados, consulte [Procedimientos recomendados para SQL Data Warehouse de Azure][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="8f779-204">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[workload management]: ./sql-data-warehouse-develop-concurrency.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!-- MSDN Articles -->
[Partitioned Tables and Indexes]: https://msdn.microsoft.com/library/ms190787.aspx
[ALTER TABLE]: https://msdn.microsoft.com/en-us/library/ms190273.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[partition function]: https://msdn.microsoft.com/library/ms187802.aspx
[partition scheme]: https://msdn.microsoft.com/library/ms179854.aspx


<!-- Other web references -->
