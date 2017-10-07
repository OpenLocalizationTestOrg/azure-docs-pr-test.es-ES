---
title: "aaaOverview de tablas en el almacén de datos de SQL | Documentos de Microsoft"
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
ms.openlocfilehash: 4edabcb4b0754bf6c99c2b6b3f0c077749051d9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-tables-in-sql-data-warehouse"></a>Información general de tablas en SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Información general][Overview]
> * [Tipos de datos][Data Types]
> * [Distribución][Distribute]
> * [Índice][Index]
> * [Partición][Partition]
> * [Estadísticas][Statistics]
> * [Temporal][Temporary]
> 
> 

Es sencillo empezar a crear tablas en SQL Data Warehouse.  Hola básica [CREATE TABLE] [ CREATE TABLE] sintaxis sigue la sintaxis común de hello es más probable que ya están familiarizados con la hora de trabajar con otras bases de datos.  toocreate una tabla, basta tooname la tabla, el nombre de las columnas y definir tipos de datos para cada columna.  Si ha creado tablas en otras bases de datos, esto debería ser tooyou muy familiar.

```sql  
CREATE TABLE Customers (FirstName VARCHAR(25), LastName VARCHAR(25))
 ``` 

Hola anteriormente en el ejemplo crea una tabla denominada a Customers con dos columnas: FirstName y LastName.  Cada columna se define con un tipo de datos de VARCHAR(25), lo que limita los caracteres de hello datos too25.  Estos atributos fundamentales de una tabla, así como otros usuarios, son principalmente Hola igual que otras bases de datos.  Tipos de datos se definen para cada columna y garantizan la integridad de Hola de los datos.  Los índices se pueden agregar tooimprove rendimiento mediante la reducción de E/S.  Creación de particiones se puede agregar tooimprove rendimiento cuando necesita datos toomodify.

Así es el [cambio de nombre][RENAME] de una tabla de SQL Data Warehouse:

```sql  
RENAME OBJECT Customer tooCustomerOrig; 
 ```

## <a name="distributed-tables"></a>Tablas distribuidas
Un nuevo atributo fundamental introducido por sistemas distribuidos como almacén de datos SQL es hello **columna de distribución**.  columna de distribución de Hello es mucho lo que puede que parezca.  Es la columna de Hola que determina cómo toodistribute, o de división, los datos entre bastidores de Hola.  Cuando se crea una tabla sin especificar la columna de distribución de hello, tabla de Hola se distribuye automáticamente mediante **round-robin**.  Aunque las tablas Round Robin pueden ser suficientes en algunos escenarios, la definición de columnas de distribución puede reducir considerablemente el movimiento de datos durante las consultas, lo que optimiza el rendimiento.  En situaciones donde hay una pequeña cantidad de datos de una tabla, elegir tabla de hello toocreate con hello **replicar** tipo de distribución copia el nodo de proceso de datos tooeach y guarda el movimiento de datos en tiempo de ejecución de consulta. Vea [distribuir una tabla] [ Distribute] toolearn más información acerca de cómo tooselect una columna de distribución.

## <a name="indexing-and-partitioning-tables"></a>Indexación y creación de particiones de tablas
Tal y como se convierten en más avanzadas de uso de almacenamiento de datos SQL y desea toooptimize rendimiento, le interesará toolearn más información sobre el diseño de la tabla.  toolearn más información, vea los artículos de hello en [tipos de datos de tabla][Data Types], [distribuir una tabla][Distribute], [indiza una tabla] [ Index] y [creación de particiones de una tabla][Partition].

## <a name="table-statistics"></a>Estadísticas de tabla
Las estadísticas tienen un rendimiento óptimo de hello toogetting importantísimo fuera de su almacenamiento de datos de SQL.  Como almacenamiento de datos de SQL no se haya automáticamente crear y actualizar estadísticas automáticamente, como se puede proceder tooexpect en la base de datos de SQL Azure, lea nuestro artículo en [estadísticas] [ Statistics] podría ser uno de Hola artículos más importantes que lea tooensure que obtendrá un rendimiento mejor Hola de las consultas.

## <a name="temporary-tables"></a>Tablas temporales
Las tablas temporales son tablas que solo existen durante el inicio de sesión que dure hello y no pueden ver otros usuarios.  Tablas temporales pueden ser una buena forma tooprevent otras personas vean resultados temporales y también reduce la necesidad de hello para la limpieza.  Dado que las tablas temporales también utilizan el almacenamiento local, pueden ofrecer un rendimiento más rápido para algunas operaciones.  Vea hello [tabla temporal] [ Temporary] artículos para obtener más información acerca de las tablas temporales.

## <a name="external-tables"></a>Tablas externas
Tablas externas, también conocido como tablas de Polybase, son tablas que se pueden consultar desde el almacenamiento de datos SQL, pero toodata punto externos de almacenamiento de datos SQL.  Por ejemplo, puede crear una tabla externa que toofiles puntos en el almacenamiento de blobs de Azure.  Para obtener más detalles sobre cómo ver la consulta una tabla externa y toocreate [carga los datos con Polybase][Load data with Polybase].  

## <a name="unsupported-table-features"></a>Características no compatibles de las tablas
Mientras que el almacenamiento de datos SQL contiene muchas de las mismas características de tabla que ofrece otras bases de datos de hello, hay algunas características que aún no se admiten.  A continuación se muestra una lista de algunas de hello características para tablas que aún no se admiten.

| Características no admitidas |
| --- |
| Clave principal, claves externas, única y comprobar [restricciones de tabla][Table Constraints] |
| [Índices únicos][Unique Indexes] |
| [Columnas calculadas][Computed Columns] |
| [Columnas dispersas][Sparse Columns] |
| [Tipos definidos por el usuario][User-Defined Types] |
| [Secuencia][Sequence] |
| [Desencadenadores][Triggers] |
| [Vistas indizadas][Indexed Views] |
| [Sinónimos][Synonyms] |

## <a name="table-size-queries"></a>Consultas de tamaño de tabla
Un espacio de tooidentify de manera sencilla y utilizados por una tabla en cada una de las distribuciones de hello 60, de filas es toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].

```sql
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

Sin embargo, el uso de los comandos DBCC puede resultar muy limitador.  Vistas de administración dinámica (DMV) le permitirá toosee mucho más detalle, así como ofrecen un mayor control sobre resultados de la consulta de Hola.  Empiece por crear esta vista, que será la que se hace referencia tooby muchos de los ejemplos en este y otros artículos.

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

### <a name="table-space-summary"></a>Resumen de espacio de tabla
Esta consulta devuelve filas de Hola y el espacio por tabla.  Es un toosee de consulta excelente qué tablas son las tablas más grandes y que sean round robin, replican o hash distribuidas.  Para las tablas hash que se distribuyen también se muestra la columna de distribución de Hola.  En la mayoría de los casos, las tablas más grandes deben distribuirse por hash con un índice de almacén de columnas agrupados.

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

### <a name="table-space-by-distribution-type"></a>Espacio de tabla por tipo de distribución
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

### <a name="table-space-by-index-type"></a>Espacio de tabla por tipo de índice
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

### <a name="distribution-space-summary"></a>Resumen de espacio de distribución
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

## <a name="next-steps"></a>Pasos siguientes
toolearn más información, vea los artículos de hello en [tipos de datos de tabla][Data Types], [distribuir una tabla][Distribute], [indiza una tabla] [ Index], [Creación de particiones de una tabla][Partition], [mantener las estadísticas de tabla] [ Statistics] y [ Tablas temporales][Temporary].  Para obtener más información sobre los procedimientos recomendados, consulte [Procedimientos recomendados para SQL Data Warehouse de Azure][SQL Data Warehouse Best Practices].

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
