---
title: "Información general acerca de las tablas en SQL Data Warehouse | Microsoft Docs"
description: "Introducción a las tablas de Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 2114d9ad-c113-43da-859f-419d72604bdf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/29/2016
ms.author: shigu;jrj
ms.openlocfilehash: c16fef2f302dbc56f257eaf2f0d2b68b6a3c1852
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-tables-in-sql-data-warehouse"></a><span data-ttu-id="62782-103">Información general de tablas en SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="62782-103">Overview of tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="62782-104">[Información general][Overview]</span><span class="sxs-lookup"><span data-stu-id="62782-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="62782-105">[Tipos de datos][Data Types]</span><span class="sxs-lookup"><span data-stu-id="62782-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="62782-106">[Distribución][Distribute]</span><span class="sxs-lookup"><span data-stu-id="62782-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="62782-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="62782-107">[Index][Index]</span></span>
> * <span data-ttu-id="62782-108">[Partición][Partition]</span><span class="sxs-lookup"><span data-stu-id="62782-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="62782-109">[Estadísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="62782-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="62782-110">[Temporal][Temporary]</span><span class="sxs-lookup"><span data-stu-id="62782-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="62782-111">Es sencillo empezar a crear tablas en SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="62782-111">Getting started with creating tables in SQL Data Warehouse is simple.</span></span>  <span data-ttu-id="62782-112">La sintaxis básica de [CREATE TABLE][CREATE TABLE] sigue la sintaxis común que probablemente ya conozca si ha trabajado con otras bases de datos.</span><span class="sxs-lookup"><span data-stu-id="62782-112">The basic [CREATE TABLE][CREATE TABLE] syntax follows the common syntax you are most likely already familiar with from working with other databases.</span></span>  <span data-ttu-id="62782-113">Para crear una tabla, solo es preciso asignarle un nombre, asignar un nombre a las columnas de la misma y definir los tipos de datos de cada columna.</span><span class="sxs-lookup"><span data-stu-id="62782-113">To create a table, you simply need to name your table, name your columns and define data types for each column.</span></span>  <span data-ttu-id="62782-114">Si ha creado las tablas en otras bases de datos, esto le resultará muy familiar.</span><span class="sxs-lookup"><span data-stu-id="62782-114">If you've create tables in other databases, this should look very familiar to you.</span></span>

```sql  
CREATE TABLE Customers (FirstName VARCHAR(25), LastName VARCHAR(25))
 ``` 

<span data-ttu-id="62782-115">El ejemplo anterior crea una tabla denominada Customers con dos columnas, FirstName y LastName.</span><span class="sxs-lookup"><span data-stu-id="62782-115">The above example creates a table named Customers with two columns, FirstName and LastName.</span></span>  <span data-ttu-id="62782-116">Cada columna se define con el tipo de datos VARCHAR(25), que limita los datos a 25 caracteres.</span><span class="sxs-lookup"><span data-stu-id="62782-116">Each column is defined with a data type of VARCHAR(25), which limits the data to 25 characters.</span></span>  <span data-ttu-id="62782-117">Estos atributos fundamentales de una tabla, así como otros, son prácticamente los mismos que los de otras bases de datos.</span><span class="sxs-lookup"><span data-stu-id="62782-117">These fundamental attributes of a table, as well as others, are mostly the same as other databases.</span></span>  <span data-ttu-id="62782-118">Los tipos de datos se definen para cada columna y garantizan la integridad de los datos.</span><span class="sxs-lookup"><span data-stu-id="62782-118">Data types are defined for each column and ensure the integrity of your data.</span></span>  <span data-ttu-id="62782-119">Los índices se pueden agregar para mejorar el rendimiento, ya que reducen la E/S.</span><span class="sxs-lookup"><span data-stu-id="62782-119">Indexes can be added to improve performance by reducing I/O.</span></span>  <span data-ttu-id="62782-120">La creación de particiones se puede agregar para mejorar el rendimiento cuando necesite modificar los datos.</span><span class="sxs-lookup"><span data-stu-id="62782-120">Partitioning can be added to improve performance when you need to modify data.</span></span>

<span data-ttu-id="62782-121">Así es el [cambio de nombre][RENAME] de una tabla de SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="62782-121">[Renaming][RENAME] a SQL Data Warehouse table looks like this:</span></span>

```sql  
RENAME OBJECT Customer TO CustomerOrig; 
 ```

## <a name="distributed-tables"></a><span data-ttu-id="62782-122">Tablas distribuidas</span><span class="sxs-lookup"><span data-stu-id="62782-122">Distributed tables</span></span>
<span data-ttu-id="62782-123">Un nuevo atributo fundamental introducido por sistemas distribuidos como SQL Data Warehouse es la **columna de distribución**.</span><span class="sxs-lookup"><span data-stu-id="62782-123">A new fundamental attribute introduced by distributed systems like SQL Data Warehouse is the **distribution column**.</span></span>  <span data-ttu-id="62782-124">La columna de distribución es mucho lo que parece.</span><span class="sxs-lookup"><span data-stu-id="62782-124">The distribution column is very much what it sounds like.</span></span>  <span data-ttu-id="62782-125">Es la columna que determina cómo distribuir, o dividir, los datos en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="62782-125">It is the column that determines how to distribute, or divide, your data behind the scenes.</span></span>  <span data-ttu-id="62782-126">Si se crea una tabla sin especificar la columna de distribución, la tabla se distribuye automáticamente mediante el método **Round Robin**.</span><span class="sxs-lookup"><span data-stu-id="62782-126">When you create a table without specifying the distribution column, the table is automatically distributed using **round robin**.</span></span>  <span data-ttu-id="62782-127">Aunque las tablas Round Robin pueden ser suficientes en algunos escenarios, la definición de columnas de distribución puede reducir considerablemente el movimiento de datos durante las consultas, lo que optimiza el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="62782-127">While round robin tables can be sufficient in some scenarios, defining distribution columns can greatly reduce data movement during queries, thus optimizing performance.</span></span>  <span data-ttu-id="62782-128">En situaciones en las que hay una pequeña cantidad de datos en una tabla, la elección de crear la tabla con el tipo de distribución **replica** copia los datos a cada nodo de ejecución y ahorra movimiento de datos en tiempo de ejecución de consulta.</span><span class="sxs-lookup"><span data-stu-id="62782-128">In situations where there is a small amount of data in a table, choosing to create the table with the **replicate** distribution type copies data to each compute node and saves data movement at query execution time.</span></span> <span data-ttu-id="62782-129">Para más información acerca de cómo seleccionar una columna de distribución, consulte [Distribución de tablas en SQL Data Warehouse][Distribute].</span><span class="sxs-lookup"><span data-stu-id="62782-129">See [Distributing a Table][Distribute] to learn more about how to select a distribution column.</span></span>

## <a name="indexing-and-partitioning-tables"></a><span data-ttu-id="62782-130">Indexación y creación de particiones de tablas</span><span class="sxs-lookup"><span data-stu-id="62782-130">Indexing and partitioning tables</span></span>
<span data-ttu-id="62782-131">A medida que el uso de SQL Data Warehouse es más avanzado y con el fin de optimizar el rendimiento, deseará más información acerca del diseño de tablas.</span><span class="sxs-lookup"><span data-stu-id="62782-131">As you become more advanced in using SQL Data Warehouse and want to optimize performance, you'll want to learn more about Table Design.</span></span>  <span data-ttu-id="62782-132">Para más información, consulte los artículos [Tipos de datos de las tablas en SQL Data Warehouse][Data Types], [Distribución de tablas en SQL Data Warehouse][Distribute], [Indexación de tablas en SQL Data Warehouse][Index] y [Creación de particiones de tablas en SQL Data Warehouse][Partition].</span><span class="sxs-lookup"><span data-stu-id="62782-132">To learn more, see the articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index] and  [Partitioning a Table][Partition].</span></span>

## <a name="table-statistics"></a><span data-ttu-id="62782-133">Estadísticas de tabla</span><span class="sxs-lookup"><span data-stu-id="62782-133">Table statistics</span></span>
<span data-ttu-id="62782-134">Las estadísticas son muy importantes para obtener el máximo rendimiento de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="62782-134">Statistics are an extremely important to getting the best performance out of your SQL Data Warehouse.</span></span>  <span data-ttu-id="62782-135">Dado que SQL Data Warehouse aún no crea ni actualiza automáticamente las estadísticas, como se pueda esperar de Azure SQL Database, la lectura del artículo sobre [estadísticas][Statistics] puede ser muy importante para asegurarse de que obtiene el máximo rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="62782-135">Since SQL Data Warehouse does not yet automatically create and update statistics for you, like you may have come to expect in Azure SQL Database, reading our article on [Statistics][Statistics] might be one of the most important articles you read to ensure that you get the best performance from your queries.</span></span>

## <a name="temporary-tables"></a><span data-ttu-id="62782-136">Tablas temporales</span><span class="sxs-lookup"><span data-stu-id="62782-136">Temporary tables</span></span>
<span data-ttu-id="62782-137">Las tablas temporales son tablas que solo existen durante el inicio de sesión y no pueden verlas los restantes usuarios.</span><span class="sxs-lookup"><span data-stu-id="62782-137">Temporary tables are tables which only exist for the duration of your logon and cannot be seen by other users.</span></span>  <span data-ttu-id="62782-138">Las tablas temporales no solo pueden ser una buena forma de evitar que otros vean los resultados temporales, sino que también reducen la necesidad de limpieza.</span><span class="sxs-lookup"><span data-stu-id="62782-138">Temporary tables can be a good way to prevent others from seeing temporary results and also reduce the need for cleanup.</span></span>  <span data-ttu-id="62782-139">Dado que las tablas temporales también utilizan el almacenamiento local, pueden ofrecer un rendimiento más rápido para algunas operaciones.</span><span class="sxs-lookup"><span data-stu-id="62782-139">Since temporary tables also utilize local storage, they can offer faster performance for some operations.</span></span>  <span data-ttu-id="62782-140">Consulte el artículo [Tablas temporales en SQL Data Warehouse][Temporary] para más información acerca de las tablas temporales.</span><span class="sxs-lookup"><span data-stu-id="62782-140">See the [Temporary Table][Temporary] articles for more details about temporary tables.</span></span>

## <a name="external-tables"></a><span data-ttu-id="62782-141">Tablas externas</span><span class="sxs-lookup"><span data-stu-id="62782-141">External tables</span></span>
<span data-ttu-id="62782-142">Las tablas externas, que también se conocen como tablas de Polybase, son tablas que pueden consultarse desde SQL Data Warehouse, pero que apuntan a datos externos de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="62782-142">External tables, also known as Polybase tables, are tables which can be queried from SQL Data Warehouse, but point to data external from SQL Data Warehouse.</span></span>  <span data-ttu-id="62782-143">Por ejemplo, puede crear una tabla externa que apunte a archivos de Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="62782-143">For example, you can create an external table which points to files on Azure Blob Storage.</span></span>  <span data-ttu-id="62782-144">Para más información acerca de cómo crear y consultar una tabla externa, consulte [Load data from Azure blob storage into SQL Data Warehouse (PolyBase)][Load data with Polybase] [Carga de datos de Azure Blob Storage en SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="62782-144">For more details on how to create and query an external table, see [Load data with Polybase][Load data with Polybase].</span></span>  

## <a name="unsupported-table-features"></a><span data-ttu-id="62782-145">Características no compatibles de las tablas</span><span class="sxs-lookup"><span data-stu-id="62782-145">Unsupported table features</span></span>
<span data-ttu-id="62782-146">Mientras que SQL Data Warehouse contiene muchas de las características de tabla que ofrecen otras bases de datos, hay algunas características que aún no son compatibles.</span><span class="sxs-lookup"><span data-stu-id="62782-146">While SQL Data Warehouse contains many of the same table features offered by other databases, there are some features which are not yet supported.</span></span>  <span data-ttu-id="62782-147">A continuación se muestra una lista de algunas de las características de tabla que no son compatibles.</span><span class="sxs-lookup"><span data-stu-id="62782-147">Below is a list of some of the table features which are not yet supported.</span></span>

| <span data-ttu-id="62782-148">Características no admitidas</span><span class="sxs-lookup"><span data-stu-id="62782-148">Unsupported features</span></span> |
| --- |
| <span data-ttu-id="62782-149">Clave principal, claves externas, única y comprobar [restricciones de tabla][Table Constraints]</span><span class="sxs-lookup"><span data-stu-id="62782-149">Primary key, Foreign keys, Unique and Check [Table Constraints][Table Constraints]</span></span> |
| <span data-ttu-id="62782-150">[Índices únicos][Unique Indexes]</span><span class="sxs-lookup"><span data-stu-id="62782-150">[Unique Indexes][Unique Indexes]</span></span> |
| <span data-ttu-id="62782-151">[Columnas calculadas][Computed Columns]</span><span class="sxs-lookup"><span data-stu-id="62782-151">[Computed Columns][Computed Columns]</span></span> |
| <span data-ttu-id="62782-152">[Columnas dispersas][Sparse Columns]</span><span class="sxs-lookup"><span data-stu-id="62782-152">[Sparse Columns][Sparse Columns]</span></span> |
| <span data-ttu-id="62782-153">[Tipos definidos por el usuario][User-Defined Types]</span><span class="sxs-lookup"><span data-stu-id="62782-153">[User-Defined Types][User-Defined Types]</span></span> |
| <span data-ttu-id="62782-154">[Secuencia][Sequence]</span><span class="sxs-lookup"><span data-stu-id="62782-154">[Sequence][Sequence]</span></span> |
| <span data-ttu-id="62782-155">[Desencadenadores][Triggers]</span><span class="sxs-lookup"><span data-stu-id="62782-155">[Triggers][Triggers]</span></span> |
| <span data-ttu-id="62782-156">[Vistas indizadas][Indexed Views]</span><span class="sxs-lookup"><span data-stu-id="62782-156">[Indexed Views][Indexed Views]</span></span> |
| <span data-ttu-id="62782-157">[Sinónimos][Synonyms]</span><span class="sxs-lookup"><span data-stu-id="62782-157">[Synonyms][Synonyms]</span></span> |

## <a name="table-size-queries"></a><span data-ttu-id="62782-158">Consultas de tamaño de tabla</span><span class="sxs-lookup"><span data-stu-id="62782-158">Table size queries</span></span>
<span data-ttu-id="62782-159">Una forma sencilla de identificar el espacio y las filas que consume una tabla en cada una de las 60 distribuciones es usar [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span><span class="sxs-lookup"><span data-stu-id="62782-159">One simple way to identify space and rows consumed by a table in each of the 60 distributions, is to use [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span></span>

```sql
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="62782-160">Sin embargo, el uso de los comandos DBCC puede resultar muy limitador.</span><span class="sxs-lookup"><span data-stu-id="62782-160">However, using DBCC commands can be quite limiting.</span></span>  <span data-ttu-id="62782-161">Las vistas de administración dinámica (DMV) le permitirán ver mucho más detalle, además de proporcionar un control mucho mayor sobre los resultados de la consulta.</span><span class="sxs-lookup"><span data-stu-id="62782-161">Dynamic management views (DMVs) will allow you to see much more detail as well as give you much greater control over the query results.</span></span>  <span data-ttu-id="62782-162">Empiece por crear esta vista, a la que se hará referencia en muchos de los ejemplos de este y otros artículos.</span><span class="sxs-lookup"><span data-stu-id="62782-162">Start by creating this view, which will be referred to by many of our examples in this and other articles.</span></span>

```sql
CREATE VIEW dbo.vTableSizes
AS
WITH base
AS
(
SELECT 
 GETDATE()                                                             AS  [execution_time]
, DB_NAME()                                                            AS  [database_name]
, s.name                                                               AS  [schema_name]
, t.name                                                               AS  [table_name]
, QUOTENAME(s.name)+'.'+QUOTENAME(t.name)                              AS  [two_part_name]
, nt.[name]                                                            AS  [node_table_name]
, ROW_NUMBER() OVER(PARTITION BY nt.[name] ORDER BY (SELECT NULL))     AS  [node_table_name_seq]
, tp.[distribution_policy_desc]                                        AS  [distribution_policy_name]
, c.[name]                                                             AS  [distribution_column]
, nt.[distribution_id]                                                 AS  [distribution_id]
, i.[type]                                                             AS  [index_type]
, i.[type_desc]                                                        AS  [index_type_desc]
, nt.[pdw_node_id]                                                     AS  [pdw_node_id]
, pn.[type]                                                            AS  [pdw_node_type]
, pn.[name]                                                            AS  [pdw_node_name]
, di.name                                                              AS  [dist_name]
, di.position                                                          AS  [dist_position]
, nps.[partition_number]                                               AS  [partition_nmbr]
, nps.[reserved_page_count]                                            AS  [reserved_space_page_count]
, nps.[reserved_page_count] - nps.[used_page_count]                    AS  [unused_space_page_count]
, nps.[in_row_data_page_count] 
    + nps.[row_overflow_used_page_count] 
    + nps.[lob_used_page_count]                                        AS  [data_space_page_count]
, nps.[reserved_page_count] 
 - (nps.[reserved_page_count] - nps.[used_page_count]) 
 - ([in_row_data_page_count] 
         + [row_overflow_used_page_count]+[lob_used_page_count])       AS  [index_space_page_count]
, nps.[row_count]                                                      AS  [row_count]
from 
    sys.schemas s
INNER JOIN sys.tables t
    ON s.[schema_id] = t.[schema_id]
INNER JOIN sys.indexes i
    ON  t.[object_id] = i.[object_id]
    AND i.[index_id] <= 1
INNER JOIN sys.pdw_table_distribution_properties tp
    ON t.[object_id] = tp.[object_id]
INNER JOIN sys.pdw_table_mappings tm
    ON t.[object_id] = tm.[object_id]
INNER JOIN sys.pdw_nodes_tables nt
    ON tm.[physical_name] = nt.[name]
INNER JOIN sys.dm_pdw_nodes pn
    ON  nt.[pdw_node_id] = pn.[pdw_node_id]
INNER JOIN sys.pdw_distributions di
    ON  nt.[distribution_id] = di.[distribution_id]
INNER JOIN sys.dm_pdw_nodes_db_partition_stats nps
    ON nt.[object_id] = nps.[object_id]
    AND nt.[pdw_node_id] = nps.[pdw_node_id]
    AND nt.[distribution_id] = nps.[distribution_id]
LEFT OUTER JOIN (select * from sys.pdw_column_distribution_properties where distribution_ordinal = 1) cdp
    ON t.[object_id] = cdp.[object_id]
LEFT OUTER JOIN sys.columns c
    ON cdp.[object_id] = c.[object_id]
    AND cdp.[column_id] = c.[column_id]
)
, size
AS
(
SELECT
   [execution_time]
,  [database_name]
,  [schema_name]
,  [table_name]
,  [two_part_name]
,  [node_table_name]
,  [node_table_name_seq]
,  [distribution_policy_name]
,  [distribution_column]
,  [distribution_id]
,  [index_type]
,  [index_type_desc]
,  [pdw_node_id]
,  [pdw_node_type]
,  [pdw_node_name]
,  [dist_name]
,  [dist_position]
,  [partition_nmbr]
,  [reserved_space_page_count]
,  [unused_space_page_count]
,  [data_space_page_count]
,  [index_space_page_count]
,  [row_count]
,  ([reserved_space_page_count] * 8.0)                                 AS [reserved_space_KB]
,  ([reserved_space_page_count] * 8.0)/1000                            AS [reserved_space_MB]
,  ([reserved_space_page_count] * 8.0)/1000000                         AS [reserved_space_GB]
,  ([reserved_space_page_count] * 8.0)/1000000000                      AS [reserved_space_TB]
,  ([unused_space_page_count]   * 8.0)                                 AS [unused_space_KB]
,  ([unused_space_page_count]   * 8.0)/1000                            AS [unused_space_MB]
,  ([unused_space_page_count]   * 8.0)/1000000                         AS [unused_space_GB]
,  ([unused_space_page_count]   * 8.0)/1000000000                      AS [unused_space_TB]
,  ([data_space_page_count]     * 8.0)                                 AS [data_space_KB]
,  ([data_space_page_count]     * 8.0)/1000                            AS [data_space_MB]
,  ([data_space_page_count]     * 8.0)/1000000                         AS [data_space_GB]
,  ([data_space_page_count]     * 8.0)/1000000000                      AS [data_space_TB]
,  ([index_space_page_count]  * 8.0)                                   AS [index_space_KB]
,  ([index_space_page_count]  * 8.0)/1000                              AS [index_space_MB]
,  ([index_space_page_count]  * 8.0)/1000000                           AS [index_space_GB]
,  ([index_space_page_count]  * 8.0)/1000000000                        AS [index_space_TB]
FROM base
)
SELECT * 
FROM size
;
```

### <a name="table-space-summary"></a><span data-ttu-id="62782-163">Resumen de espacio de tabla</span><span class="sxs-lookup"><span data-stu-id="62782-163">Table space summary</span></span>
<span data-ttu-id="62782-164">Esta consulta devuelve las filas y el espacio por tabla.</span><span class="sxs-lookup"><span data-stu-id="62782-164">This query returns the rows and space by table.</span></span>  <span data-ttu-id="62782-165">Es una consulta excelente para ver qué tablas son las más grandes y si se han distribuido por hash, round robin o réplica.</span><span class="sxs-lookup"><span data-stu-id="62782-165">It is a great query to see which tables are your largest tables and whether they are round robin, replicated or hash distributed.</span></span>  <span data-ttu-id="62782-166">Para las tablas distribuidas por hash, también se muestra la columna de distribución.</span><span class="sxs-lookup"><span data-stu-id="62782-166">For hash distributed tables it also shows the distribution column.</span></span>  <span data-ttu-id="62782-167">En la mayoría de los casos, las tablas más grandes deben distribuirse por hash con un índice de almacén de columnas agrupados.</span><span class="sxs-lookup"><span data-stu-id="62782-167">In most cases your largest tables should be hash distributed with a clustered columnstore index.</span></span>

```sql
SELECT 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
,    COUNT(distinct partition_nmbr) as nbr_partitions
,    SUM(row_count)                 as table_row_count
,    SUM(reserved_space_GB)         as table_reserved_space_GB
,    SUM(data_space_GB)             as table_data_space_GB
,    SUM(index_space_GB)            as table_index_space_GB
,    SUM(unused_space_GB)           as table_unused_space_GB
FROM 
    dbo.vTableSizes
GROUP BY 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
ORDER BY
    table_reserved_space_GB desc
;
```

### <a name="table-space-by-distribution-type"></a><span data-ttu-id="62782-168">Espacio de tabla por tipo de distribución</span><span class="sxs-lookup"><span data-stu-id="62782-168">Table space by distribution type</span></span>
```sql
SELECT 
     distribution_policy_name
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY distribution_policy_name
;
```

### <a name="table-space-by-index-type"></a><span data-ttu-id="62782-169">Espacio de tabla por tipo de índice</span><span class="sxs-lookup"><span data-stu-id="62782-169">Table space by index type</span></span>
```sql
SELECT 
     index_type_desc
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY index_type_desc
;
```

### <a name="distribution-space-summary"></a><span data-ttu-id="62782-170">Resumen de espacio de distribución</span><span class="sxs-lookup"><span data-stu-id="62782-170">Distribution space summary</span></span>
```sql
SELECT 
    distribution_id
,    SUM(row_count)                as total_node_distribution_row_count
,    SUM(reserved_space_MB)        as total_node_distribution_reserved_space_MB
,    SUM(data_space_MB)            as total_node_distribution_data_space_MB
,    SUM(index_space_MB)           as total_node_distribution_index_space_MB
,    SUM(unused_space_MB)          as total_node_distribution_unused_space_MB
FROM dbo.vTableSizes
GROUP BY     distribution_id
ORDER BY    distribution_id
;
```

## <a name="next-steps"></a><span data-ttu-id="62782-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="62782-171">Next steps</span></span>
<span data-ttu-id="62782-172">Para más información, consulte los artículos sobre [Tipos de datos de las tablas en SQL Data Warehouse][Data Types], [Distribución de tablas en SQL Data Warehouse][Distribute], [Indexación de tablas en SQL Data Warehouse][Index], [Creación de particiones de tablas en SQL Data Warehouse][Partition], [Administración de estadísticas en tablas en SQL Data Warehouse][Statistics] y [Tablas temporales en SQL Data Warehouse][Temporary].</span><span class="sxs-lookup"><span data-stu-id="62782-172">To learn more, see the articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="62782-173">Para obtener más información sobre los procedimientos recomendados, consulte [Procedimientos recomendados para SQL Data Warehouse de Azure][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="62782-173">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md
[Load data with Polybase]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md

<!--MSDN references-->
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx
[DBCC PDW_SHOWSPACEUSED]: https://msdn.microsoft.com/library/mt204028.aspx
[Table Constraints]: https://msdn.microsoft.com/library/ms188066.aspx
[Computed Columns]: https://msdn.microsoft.com/library/ms186241.aspx
[Sparse Columns]: https://msdn.microsoft.com/library/cc280604.aspx
[User-Defined Types]: https://msdn.microsoft.com/library/ms131694.aspx
[Sequence]: https://msdn.microsoft.com/library/ff878091.aspx
[Triggers]: https://msdn.microsoft.com/library/ms189799.aspx
[Indexed Views]: https://msdn.microsoft.com/library/ms191432.aspx
[Synonyms]: https://msdn.microsoft.com/library/ms177544.aspx
[Unique Indexes]: https://msdn.microsoft.com/library/ms188783.aspx

<!--Other Web references-->
