---
title: "tablas de aaaPartitioning en el almacén de datos de SQL | Documentos de Microsoft"
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
ms.openlocfilehash: aa63c51562f3e6f83063320860b195e135a721e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-tables-in-sql-data-warehouse"></a><span data-ttu-id="001d2-103">Creación de particiones de tablas en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="001d2-103">Partitioning tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="001d2-104">[Información general][Overview]</span><span class="sxs-lookup"><span data-stu-id="001d2-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="001d2-105">[Tipos de datos][Data Types]</span><span class="sxs-lookup"><span data-stu-id="001d2-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="001d2-106">[Distribución][Distribute]</span><span class="sxs-lookup"><span data-stu-id="001d2-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="001d2-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="001d2-107">[Index][Index]</span></span>
> * <span data-ttu-id="001d2-108">[Partición][Partition]</span><span class="sxs-lookup"><span data-stu-id="001d2-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="001d2-109">[Estadísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="001d2-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="001d2-110">[Temporal][Temporary]</span><span class="sxs-lookup"><span data-stu-id="001d2-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="001d2-111">La creación de particiones es compatible con todos los tipos de tabla de Almacenamiento de datos SQL, entre los que se incluyen almacén de columnas en clúster, índice agrupado y montón.</span><span class="sxs-lookup"><span data-stu-id="001d2-111">Partitioning is supported on all SQL Data Warehouse table types; including clustered columnstore, clustered index, and heap.</span></span>  <span data-ttu-id="001d2-112">La creación de particiones también es compatible con todos los tipos de distribución, incluidos la distribución por hash o la distribución Round Robin.</span><span class="sxs-lookup"><span data-stu-id="001d2-112">Partitioning is also supported on all distribution types, including both hash or round robin distributed.</span></span>  <span data-ttu-id="001d2-113">Creación de particiones permite toodivide los datos en grupos más pequeños de datos y en la mayoría de los casos, creación de particiones se realiza en una columna de fecha.</span><span class="sxs-lookup"><span data-stu-id="001d2-113">Partitioning enables you toodivide your data into smaller groups of data and in most cases, partitioning is done on a date column.</span></span>

## <a name="benefits-of-partitioning"></a><span data-ttu-id="001d2-114">Ventajas de la creación de particiones</span><span class="sxs-lookup"><span data-stu-id="001d2-114">Benefits of partitioning</span></span>
<span data-ttu-id="001d2-115">La creación de particiones puede beneficiar el mantenimiento de datos y el rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="001d2-115">Partitioning can benefit data maintenance and query performance.</span></span>  <span data-ttu-id="001d2-116">Si se beneficia tanto o simplemente uno depende de cómo se cargan los datos y si hello misma columna se puede usar ambos fines, puesto que la creación de particiones solo puede realizarse en una columna.</span><span class="sxs-lookup"><span data-stu-id="001d2-116">Whether it benefits both or just one is dependent on how data is loaded and whether hello same column can be used for both purposes, since partitioning can only be done on one column.</span></span>

### <a name="benefits-tooloads"></a><span data-ttu-id="001d2-117">Ventajas tooloads</span><span class="sxs-lookup"><span data-stu-id="001d2-117">Benefits tooloads</span></span>
<span data-ttu-id="001d2-118">Hola de las principales ventajas de crear particiones en el almacén de datos SQL es mejorar Hola eficacia y el rendimiento de carga de datos mediante el uso de eliminación de la partición, cambiando y combinar.</span><span class="sxs-lookup"><span data-stu-id="001d2-118">hello primary benefit of partitioning in SQL Data Warehouse is improve hello efficiency and performance of loading data by use of partition deletion, switching and merging.</span></span>  <span data-ttu-id="001d2-119">En la mayoría de los casos se crean particiones de una fecha de columna que está estrechamente ligada secuencia toohello qué datos hello están la base de datos de toohello cargado.</span><span class="sxs-lookup"><span data-stu-id="001d2-119">In most cases data is partitioned on a date column that is closely tied toohello sequence which hello data is loaded toohello database.</span></span>  <span data-ttu-id="001d2-120">Una de las mayores ventajas de hello consiste en utilizar particiones toomaintain datos Hola anulación de registro de transacciones.</span><span class="sxs-lookup"><span data-stu-id="001d2-120">One of hello greatest benefits of using partitions toomaintain data it hello avoidance of transaction logging.</span></span>  <span data-ttu-id="001d2-121">Mientras que simplemente insertar, actualizar o eliminar datos puede ser el enfoque más sencillo de hello, con un poco de pensamiento y esfuerzo, utilizan las particiones durante el proceso de carga puede mejorar considerablemente el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="001d2-121">While simply inserting, updating or deleting data can be hello most straightforward approach, with a little thought and effort, using partitioning during your load process can substantially improve performance.</span></span>

<span data-ttu-id="001d2-122">Modificación de las particiones se puede quitar tooquickly usado o reemplazar una sección de una tabla.</span><span class="sxs-lookup"><span data-stu-id="001d2-122">Partition switching can be used tooquickly remove or replace a section of a table.</span></span>  <span data-ttu-id="001d2-123">Por ejemplo, una tabla de hechos de ventas podría contener solo los datos para hello últimos 36 meses.</span><span class="sxs-lookup"><span data-stu-id="001d2-123">For example, a sales fact table might contain just data for hello past 36 months.</span></span>  <span data-ttu-id="001d2-124">Al final de Hola de cada mes, hello mes más antiguo de los datos de ventas se elimina de hello tabla.</span><span class="sxs-lookup"><span data-stu-id="001d2-124">At hello end of every month, hello oldest month of sales data is deleted from hello table.</span></span>  <span data-ttu-id="001d2-125">Estos datos se pudieron eliminar mediante delete instrucción toodelete Hola datos para hello mes más antiguo.</span><span class="sxs-lookup"><span data-stu-id="001d2-125">This data could be deleted by using a delete statement toodelete hello data for hello oldest month.</span></span>  <span data-ttu-id="001d2-126">Sin embargo, al eliminar una gran cantidad de datos fila por fila con una instrucción delete puede tardar mucho tiempo, así como generar un riesgo de Hola de las transacciones grandes que pueden durar un toorollback mucho tiempo si algo va mal.</span><span class="sxs-lookup"><span data-stu-id="001d2-126">However, deleting a large amount of data row-by-row with a delete statement can take a very long time, as well as create hello risk of large transactions which could take a long time toorollback if something goes wrong.</span></span>  <span data-ttu-id="001d2-127">Un enfoque más óptimo es la partición más antigua Hola de toosimply colocación de datos.</span><span class="sxs-lookup"><span data-stu-id="001d2-127">A more optimal approach is toosimply drop hello oldest partition of data.</span></span>  <span data-ttu-id="001d2-128">Donde eliminar filas individuales de hello podría tardar horas, eliminando una partición completa puede tardar a segundos.</span><span class="sxs-lookup"><span data-stu-id="001d2-128">Where deleting hello individual rows could take hours, deleting an entire partition could take seconds.</span></span>

### <a name="benefits-tooqueries"></a><span data-ttu-id="001d2-129">Ventajas tooqueries</span><span class="sxs-lookup"><span data-stu-id="001d2-129">Benefits tooqueries</span></span>
<span data-ttu-id="001d2-130">Creación de particiones, también puede ser usado tooimprove rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="001d2-130">Partitioning can also be used tooimprove query performance.</span></span>  <span data-ttu-id="001d2-131">Si una consulta aplica un filtro en una columna de partición, esto puede limitar Hola examen tooonly Hola calificar las particiones que pueden ser un subconjunto mucho más pequeño de datos de hello, evitando un recorrido de tabla completa.</span><span class="sxs-lookup"><span data-stu-id="001d2-131">If a query applies a filter on a partitioned column, this can limit hello scan tooonly hello qualifying partitions which may be a much smaller subset of hello data, avoiding a full table scan.</span></span>  <span data-ttu-id="001d2-132">Con la introducción de Hola de índices de almacén de columnas agrupado, ventajas de rendimiento de eliminación de predicado de hello son menos beneficiosas, pero en algunos casos puede ser una ventaja tooqueries.</span><span class="sxs-lookup"><span data-stu-id="001d2-132">With hello introduction of clustered columnstore indexes, hello predicate elimination performance benefits are less beneficial, but in some cases there can be a benefit tooqueries.</span></span>  <span data-ttu-id="001d2-133">Por ejemplo, si la tabla de hechos de ventas de Hola se divide en 36 meses mediante el campo de fecha de ventas de hello, a continuación, las consultas que filtrar por fecha de venta de Hola pueden omitir la búsqueda en las particiones que no coinciden con el filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="001d2-133">For example, if hello sales fact table is partitioned into 36 months using hello sales date field, then queries that filter on hello sale date can skip searching in partitions that don’t match hello filter.</span></span>

## <a name="partition-sizing-guidance"></a><span data-ttu-id="001d2-134">Guía sobre el tamaño de las particiones</span><span class="sxs-lookup"><span data-stu-id="001d2-134">Partition sizing guidance</span></span>
<span data-ttu-id="001d2-135">Durante la creación de particiones pueden mejorar el rendimiento tooimprove usa algunos escenarios, crear una tabla con **demasiados** particiones pueden afectar al rendimiento en algunas circunstancias.</span><span class="sxs-lookup"><span data-stu-id="001d2-135">While partitioning can be used tooimprove performance some scenarios, creating a table with **too many** partitions can hurt performance under some circumstances.</span></span>  <span data-ttu-id="001d2-136">Estas cuestiones se dan especialmente en las tablas de almacén de columnas en clúster.</span><span class="sxs-lookup"><span data-stu-id="001d2-136">These concerns are especially true for clustered columnstore tables.</span></span>  <span data-ttu-id="001d2-137">Para crear particiones toobe útil, es importante toounderstand al número de hello y creación de particiones de toouse de toocreate de particiones.</span><span class="sxs-lookup"><span data-stu-id="001d2-137">For partitioning toobe helpful, it is important toounderstand when toouse partitioning and hello number of partitions toocreate.</span></span>  <span data-ttu-id="001d2-138">No existe se ninguna regla de disco duro rápida como toohow número de particiones es demasiado elevado, depende de los datos y cuántas particiones va a cargar toosimultaneously.</span><span class="sxs-lookup"><span data-stu-id="001d2-138">There is no hard fast rule as toohow many partitions are too many, it depends on your data and how many partitions you are loading toosimultaneously.</span></span>  <span data-ttu-id="001d2-139">Pero como regla general, piense en Agregar 10s too100s de particiones, no 1000s.</span><span class="sxs-lookup"><span data-stu-id="001d2-139">But as a general rule of thumb, think of adding 10s too100s of partitions, not 1000s.</span></span>

<span data-ttu-id="001d2-140">Al crear particiones en **almacén de columnas agrupado** tablas, es importante tooconsider cuántas filas se dirigirán a cada partición.</span><span class="sxs-lookup"><span data-stu-id="001d2-140">When creating partitioning on **clustered columnstore** tables, it is important tooconsider how many rows will land in each partition.</span></span>  <span data-ttu-id="001d2-141">Para que tanto la compresión como el rendimiento de las tablas de almacén de columnas en clúster sean óptimos, se necesita un mínimo de un millón de filas por partición y distribución.</span><span class="sxs-lookup"><span data-stu-id="001d2-141">For optimal compression and performance of clustered columnstore tables, a minimum of 1 million rows per distribution and partition is needed.</span></span>  <span data-ttu-id="001d2-142">Antes de que se creen particiones, Almacenamiento de datos SQL ya divide cada tabla en 60 bases de datos distribuidas.</span><span class="sxs-lookup"><span data-stu-id="001d2-142">Before partitions are created, SQL Data Warehouse already divides each table into 60 distributed databases.</span></span>  <span data-ttu-id="001d2-143">Cualquier partición tabla tooa agregado además es distribuciones toohello creadas en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="001d2-143">Any partitioning added tooa table is in addition toohello distributions created behind hello scenes.</span></span>  <span data-ttu-id="001d2-144">Con este ejemplo, si tabla de hechos de ventas de hello incluido 36 particiones mensuales y dado que el almacenamiento de datos de SQL tiene 60 distribuciones, a continuación, Hola hechos de ventas tabla debe contener 60 millones de filas por mes o 2.1 millones de filas cuando se rellenan todos los meses.</span><span class="sxs-lookup"><span data-stu-id="001d2-144">Using this example, if hello sales fact table contained 36 monthly partitions, and given that SQL Data Warehouse has 60 distributions, then hello sales fact table should contain 60 million rows per month, or 2.1 billion rows when all months are populated.</span></span>  <span data-ttu-id="001d2-145">Si una tabla contiene significativamente menos filas de hello recomienda un mínimo de filas por partición, considere la posibilidad de usar menos particiones en el número de pedido toomake aumento Hola de filas por partición.</span><span class="sxs-lookup"><span data-stu-id="001d2-145">If a table contains significantly less rows than hello recommended minimum number of rows per partition, consider using fewer partitions in order toomake increase hello number of rows per partition.</span></span>  <span data-ttu-id="001d2-146">Consulte también hello [indización] [ Index] artículo que incluye las consultas que se pueden ejecutar en la calidad del almacenamiento de datos SQL tooassess Hola de índices de almacén de columnas clúster.</span><span class="sxs-lookup"><span data-stu-id="001d2-146">Also see hello [Indexing][Index] article which includes queries that can be run on SQL Data Warehouse tooassess hello quality of cluster columnstore indexes.</span></span>

## <a name="syntax-difference-from-sql-server"></a><span data-ttu-id="001d2-147">Diferencia con respecto a la sintaxis de SQL Server</span><span class="sxs-lookup"><span data-stu-id="001d2-147">Syntax difference from SQL Server</span></span>
<span data-ttu-id="001d2-148">Almacenamiento de datos SQL introduce una definición simplificada de particiones que difiere ligeramente de la de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="001d2-148">SQL Data Warehouse introduces a simplified definition of partitions which is slightly different from SQL Server.</span></span>  <span data-ttu-id="001d2-149">Las funciones y los esquemas de la creación de particiones no se usan en Almacenamiento de datos SQL como en SQL Server.</span><span class="sxs-lookup"><span data-stu-id="001d2-149">Partitioning functions and schemes are not used in SQL Data Warehouse as they are in SQL Server.</span></span>  <span data-ttu-id="001d2-150">En su lugar, todo lo que necesita toodo es identificar puntos de límite de hello y columnas con particiones.</span><span class="sxs-lookup"><span data-stu-id="001d2-150">Instead, all you need toodo is identify partitioned column and hello boundary points.</span></span>  <span data-ttu-id="001d2-151">Aunque sintaxis Hola de particionamiento pueden ser ligeramente diferente de SQL Server, los conceptos básicos de Hola se Hola mismo.</span><span class="sxs-lookup"><span data-stu-id="001d2-151">While hello syntax of partitioning may be slightly different from SQL Server, hello basic concepts are hello same.</span></span>  <span data-ttu-id="001d2-152">SQL Server y Almacenamiento de datos SQL admiten una columna de partición por tabla, que puede ser una partición con intervalos.</span><span class="sxs-lookup"><span data-stu-id="001d2-152">SQL Server and SQL Data Warehouse support one partition column per table, which can be ranged partition.</span></span>  <span data-ttu-id="001d2-153">toolearn más información acerca de la creación de particiones, vea [Partitioned Tables and Indexes][Partitioned Tables and Indexes].</span><span class="sxs-lookup"><span data-stu-id="001d2-153">toolearn more about partitioning, see [Partitioned Tables and Indexes][Partitioned Tables and Indexes].</span></span>

<span data-ttu-id="001d2-154">Hola siguiente ejemplo de un almacén de datos de SQL con particiones [CREATE TABLE] [ CREATE TABLE] instrucción, particiones de tabla de hello FactInternetSales en la columna OrderDateKey de hello:</span><span class="sxs-lookup"><span data-stu-id="001d2-154">hello below example of a SQL Data Warehouse partitioned [CREATE TABLE][CREATE TABLE] statement, partitions hello FactInternetSales table on hello OrderDateKey column:</span></span>

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

## <a name="migrating-partitioning-from-sql-server"></a><span data-ttu-id="001d2-155">Migración de particiones de SQL Server</span><span class="sxs-lookup"><span data-stu-id="001d2-155">Migrating partitioning from SQL Server</span></span>
<span data-ttu-id="001d2-156">toomigrate SQL Server simplemente cree particiones definiciones tooSQL almacenamiento de datos:</span><span class="sxs-lookup"><span data-stu-id="001d2-156">toomigrate SQL Server partition definitions tooSQL Data Warehouse simply:</span></span>

* <span data-ttu-id="001d2-157">Eliminar Hola SQL Server [esquema de partición][partition scheme].</span><span class="sxs-lookup"><span data-stu-id="001d2-157">Eliminate hello SQL Server [partition scheme][partition scheme].</span></span>
* <span data-ttu-id="001d2-158">Agregar hello [función de partición] [ partition function] tooyour crear tabla de definición.</span><span class="sxs-lookup"><span data-stu-id="001d2-158">Add hello [partition function][partition function] definition tooyour CREATE TABLE.</span></span>

<span data-ttu-id="001d2-159">Si va a migrar una tabla con particiones de un saludo de la instancia de SQL Server por debajo de SQL puede ayudarle a número de hello toointerrogate de filas que se encuentran en cada partición.</span><span class="sxs-lookup"><span data-stu-id="001d2-159">If you are migrating a partitioned table from a SQL Server instance hello below SQL can help you toointerrogate hello number of rows that are in each partition.</span></span>  <span data-ttu-id="001d2-160">Tenga en cuenta que si hello se usa misma granularidad de partición en el almacén de datos de SQL, número de Hola de filas por partición disminuirá por un factor de 60.</span><span class="sxs-lookup"><span data-stu-id="001d2-160">Keep in mind that if hello same partitioning granularity is used on SQL Data Warehouse, hello number of rows per partition will decrease by a factor of 60.</span></span>  

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

## <a name="workload-management"></a><span data-ttu-id="001d2-161">Administración de cargas de trabajo</span><span class="sxs-lookup"><span data-stu-id="001d2-161">Workload management</span></span>
<span data-ttu-id="001d2-162">Es un último fragmento consideración toofactor en la decisión de partición de tabla toohello [administración de cargas de trabajo][workload management].</span><span class="sxs-lookup"><span data-stu-id="001d2-162">One final piece consideration toofactor in toohello table partition decision is [workload management][workload management].</span></span>  <span data-ttu-id="001d2-163">Administración de cargas de trabajo en el almacén de datos de SQL es principalmente un Hola administración de memoria y la simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="001d2-163">Workload management in SQL Data Warehouse is primarily hello management of memory and concurrency.</span></span>  <span data-ttu-id="001d2-164">Hola de almacenamiento de datos SQL memoria máxima asignada tooeach distribución durante la ejecución de la consulta es clases de recursos controlados.</span><span class="sxs-lookup"><span data-stu-id="001d2-164">In SQL Data Warehouse hello maximum memory allocated tooeach distribution during query execution is governed resource classes.</span></span>  <span data-ttu-id="001d2-165">Lo ideal es que se dimensionarán las particiones en consideración a otros factores como Hola necesidades de memoria de la creación de índices de almacén de columnas agrupado.</span><span class="sxs-lookup"><span data-stu-id="001d2-165">Ideally your partitions will be sized in consideration of other factors like hello memory needs of building clustered columnstore indexes.</span></span>  <span data-ttu-id="001d2-166">Los índices de almacén de columnas en clúster suponen una mayor ventaja cuando se les asigna más memoria.</span><span class="sxs-lookup"><span data-stu-id="001d2-166">Clustered columnstore indexes benefit greatly when they are allocated more memory.</span></span>  <span data-ttu-id="001d2-167">Por lo tanto, le interesará no necesite tooensure que volver a generar un índice de partición de memoria.</span><span class="sxs-lookup"><span data-stu-id="001d2-167">Therefore, you will want tooensure that a partition index rebuild is not starved of memory.</span></span> <span data-ttu-id="001d2-168">Aumentar Hola cantidad de memoria disponible tooyour consulta se puede lograr mediante el cambio de rol predeterminado de hello, smallrc, tooone de Hola otros roles, como largerc.</span><span class="sxs-lookup"><span data-stu-id="001d2-168">Increasing hello amount of memory available tooyour query can be achieved by switching from hello default role, smallrc, tooone of hello other roles such as largerc.</span></span>

<span data-ttu-id="001d2-169">Obtener información sobre la asignación de Hola de memoria por distribución está disponible al consultar vistas de administración dinámica del regulador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="001d2-169">Information on hello allocation of memory per distribution is available by querying hello resource governor dynamic management views.</span></span> <span data-ttu-id="001d2-170">En realidad la concesión de memoria será menor que las cifras de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="001d2-170">In reality your memory grant will be less than hello figures below.</span></span> <span data-ttu-id="001d2-171">Sin embargo, esto proporciona un nivel de instrucciones que puede utilizar al cambiar el tamaño de las particiones para las operaciones de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="001d2-171">However, this provides a level of guidance that you can use when sizing your partitions for data management operations.</span></span>  <span data-ttu-id="001d2-172">Intente tooavoid ajustar el tamaño de las particiones más allá de la concesión de memoria de hello proporcionado por clase de recurso extragrande Hola.</span><span class="sxs-lookup"><span data-stu-id="001d2-172">Try tooavoid sizing your partitions beyond hello memory grant provided by hello extra large resource class.</span></span> <span data-ttu-id="001d2-173">Si las particiones aumenta más allá de esta ilustración se corre el riesgo de Hola de presión de memoria, lo que conduce a su vez compresión óptimo que no requiere herramientas.</span><span class="sxs-lookup"><span data-stu-id="001d2-173">If your partitions grow beyond this figure you run hello risk of memory pressure which in turn leads tooless optimal compression.</span></span>

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

## <a name="partition-switching"></a><span data-ttu-id="001d2-174">Modificación de particiones</span><span class="sxs-lookup"><span data-stu-id="001d2-174">Partition switching</span></span>
<span data-ttu-id="001d2-175">Almacenamiento de datos SQL admite la separación, combinación y modificación de particiones.</span><span class="sxs-lookup"><span data-stu-id="001d2-175">SQL Data Warehouse supports partition splitting, merging, and switching.</span></span> <span data-ttu-id="001d2-176">Cada una de estas funciones es ejecutarse con hello [ALTER TABLE] [ ALTER TABLE] instrucción.</span><span class="sxs-lookup"><span data-stu-id="001d2-176">Each of these functions is excuted using hello [ALTER TABLE][ALTER TABLE] statement.</span></span>

<span data-ttu-id="001d2-177">tooswitch particiones entre dos tablas que debe asegurarse de que las particiones de Hola se alinean en sus respectivos límites y que coinciden con las definiciones de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="001d2-177">tooswitch partitions between two tables you must ensure that hello partitions align on their respective boundaries and that hello table definitions match.</span></span> <span data-ttu-id="001d2-178">Ya que las restricciones check no están disponibles tooenforce intervalo de Hola de valores en una tabla de origen de tabla Hola debe contener Hola mismo los límites de partición como tabla de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="001d2-178">As check constraints are not available tooenforce hello range of values in a table hello source table must contain hello same partition boundaries as hello target table.</span></span> <span data-ttu-id="001d2-179">Si este no es el caso de hello, a continuación, cambio de partición de hello generará un error y no se sincronizarán los metadatos de la partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="001d2-179">If this is not hello case, then hello partition switch will fail as hello partition metadata will not be synchronized.</span></span>

### <a name="how-toosplit-a-partition-that-contains-data"></a><span data-ttu-id="001d2-180">¿Cómo toosplit una partición que contiene los datos</span><span class="sxs-lookup"><span data-stu-id="001d2-180">How toosplit a partition that contains data</span></span>
<span data-ttu-id="001d2-181">Hola toosplit de método más eficaz una partición que ya contenga datos es toouse un `CTAS` instrucción.</span><span class="sxs-lookup"><span data-stu-id="001d2-181">hello most efficient method toosplit a partition that already contains data is toouse a `CTAS` statement.</span></span> <span data-ttu-id="001d2-182">Si la tabla con particiones de hello es un almacén de columnas en clúster, a continuación, partición de tabla de hello debe estar vacío antes de se puede dividir.</span><span class="sxs-lookup"><span data-stu-id="001d2-182">If hello partitioned table is a clustered columnstore then hello table partition must be empty before it can be split.</span></span>

<span data-ttu-id="001d2-183">A continuación, se muestra una tabla de ejemplo con particiones del almacén de columnas que contiene una fila en cada partición:</span><span class="sxs-lookup"><span data-stu-id="001d2-183">Below is a sample partitioned columnstore table containing one row in each partition:</span></span>

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
> <span data-ttu-id="001d2-184">Crear objeto de estadísticas de hello, garantizamos que metadatos de la tabla están más preciso.</span><span class="sxs-lookup"><span data-stu-id="001d2-184">By Creating hello statistic object, we ensure that table metadata is more accurate.</span></span> <span data-ttu-id="001d2-185">Si se omite la creación de estadísticas, Almacenamiento de datos SQL utilizará los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="001d2-185">If we omit creating statistics, then SQL Data Warehouse will use default values.</span></span> <span data-ttu-id="001d2-186">Para obtener detalles sobre las estadísticas, consulte las [estadísticas][statistics].</span><span class="sxs-lookup"><span data-stu-id="001d2-186">For details on statistics please review [statistics][statistics].</span></span>
> 
> 

<span data-ttu-id="001d2-187">A continuación, podemos realizar una consulta de recuento de filas de hello mediante hello `sys.partitions` vista de catálogo:</span><span class="sxs-lookup"><span data-stu-id="001d2-187">We can then query for hello row count using hello `sys.partitions` catalog view:</span></span>

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

<span data-ttu-id="001d2-188">Si intentamos toosplit en esta tabla, se producirá un error:</span><span class="sxs-lookup"><span data-stu-id="001d2-188">If we try toosplit this table, we will get an error:</span></span>

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="001d2-189">No se pudo msg 35346, nivel 15, estado 1, línea 44 DIVIDIDO cláusula de la instrucción ALTER PARTITION porque Hola partición no está vacía.</span><span class="sxs-lookup"><span data-stu-id="001d2-189">Msg 35346, Level 15, State 1, Line 44 SPLIT clause of ALTER PARTITION statement failed because hello partition is not empty.</span></span>  <span data-ttu-id="001d2-190">Solo las particiones vacías se pueden dividir en cuando existe un índice de almacén de columnas en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="001d2-190">Only empty partitions can be split in when a columnstore index exists on hello table.</span></span> <span data-ttu-id="001d2-191">Considere la posibilidad de deshabilitar el índice de almacén de columnas de hello antes de emitir la instrucción ALTER PARTITION de hello, a continuación, volver a generar el índice de almacén de columnas de hello una vez completada la ALTER PARTITION.</span><span class="sxs-lookup"><span data-stu-id="001d2-191">Consider disabling hello columnstore index before issuing hello ALTER PARTITION statement, then rebuilding hello columnstore index after ALTER PARTITION is complete.</span></span>

<span data-ttu-id="001d2-192">Sin embargo, podemos usar `CTAS` toocreate un nuevo toohold tabla nuestros datos.</span><span class="sxs-lookup"><span data-stu-id="001d2-192">However, we can use `CTAS` toocreate a new table toohold our data.</span></span>

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

<span data-ttu-id="001d2-193">Tal y como se alinean los límites de partición de Hola se permite un conmutador.</span><span class="sxs-lookup"><span data-stu-id="001d2-193">As hello partition boundaries are aligned a switch is permitted.</span></span> <span data-ttu-id="001d2-194">Tabla de origen de hello dejará con una partición vacía que posteriormente se puede dividir.</span><span class="sxs-lookup"><span data-stu-id="001d2-194">This will leave hello source table with an empty partition that we can subsequently split.</span></span>

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 too FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="001d2-195">Todo lo que queda toodo es tooalign nuestro toohello datos nuevos de partición límites mediante `CTAS` y cambiar los datos en la tabla principal de toohello</span><span class="sxs-lookup"><span data-stu-id="001d2-195">All that is left toodo is tooalign our data toohello new partition boundaries using `CTAS` and switch our data back in toohello main table</span></span>

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

ALTER TABLE dbo.FactInternetSales_20000101_20010101 SWITCH PARTITION 2 toodbo.FactInternetSales PARTITION 2;
```

<span data-ttu-id="001d2-196">Cuando haya completado el movimiento de Hola de datos de hello es estadísticas buena idea toorefresh hello en tooensure de tabla de destino de Hola que reflejan con precisión distribución nueva de Hola de los datos de hello en sus respectivos particiones:</span><span class="sxs-lookup"><span data-stu-id="001d2-196">Once you have completed hello movement of hello data it is a good idea toorefresh hello statistics on hello target table tooensure they accurately reflect hello new distribution of hello data in their respective partitions:</span></span>

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a><span data-ttu-id="001d2-197">Control de código fuente de particiones de tabla</span><span class="sxs-lookup"><span data-stu-id="001d2-197">Table partitioning source control</span></span>
<span data-ttu-id="001d2-198">tooavoid la definición de tabla **int** en el sistema de control de código fuente puede hello tooconsider enfoque:</span><span class="sxs-lookup"><span data-stu-id="001d2-198">tooavoid your table definition from **rusting** in your source control system you may want tooconsider hello following approach:</span></span>

1. <span data-ttu-id="001d2-199">Crear tabla de hello como una tabla con particiones pero sin valores de partición</span><span class="sxs-lookup"><span data-stu-id="001d2-199">Create hello table as a partitioned table but with no partition values</span></span>

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

1. <span data-ttu-id="001d2-200">`SPLIT`tabla de Hello como parte del proceso de implementación de hello:</span><span class="sxs-lookup"><span data-stu-id="001d2-200">`SPLIT` hello table as part of hello deployment process:</span></span>

```sql
-- Create a table containing hello partition boundaries

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

-- Iterate over hello partition boundaries and split hello table

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

<span data-ttu-id="001d2-201">Con esta hello enfoque código de control de código fuente sigue siendo estático y valores de límite de partición de Hola se permiten toobe dinámico; evolucionado con el almacenamiento de hello con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="001d2-201">With this approach hello code in source control remains static and hello partitioning boundary values are allowed toobe dynamic; evolving with hello warehouse over time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="001d2-202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="001d2-202">Next steps</span></span>
<span data-ttu-id="001d2-203">toolearn más información, vea los artículos de hello en [información general de la tabla][Overview], [tipos de datos de tabla][Data Types], [distribuir una tabla] [ Distribute], [Indiza una tabla][Index], [mantener las estadísticas de tabla] [ Statistics] y [ Tablas temporales][Temporary].</span><span class="sxs-lookup"><span data-stu-id="001d2-203">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="001d2-204">Para obtener más información sobre los procedimientos recomendados, consulte [Procedimientos recomendados para SQL Data Warehouse de Azure][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="001d2-204">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
