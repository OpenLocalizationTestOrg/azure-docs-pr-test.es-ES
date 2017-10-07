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
# <a name="partitioning-tables-in-sql-data-warehouse"></a>Creación de particiones de tablas en Almacenamiento de datos SQL
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

La creación de particiones es compatible con todos los tipos de tabla de Almacenamiento de datos SQL, entre los que se incluyen almacén de columnas en clúster, índice agrupado y montón.  La creación de particiones también es compatible con todos los tipos de distribución, incluidos la distribución por hash o la distribución Round Robin.  Creación de particiones permite toodivide los datos en grupos más pequeños de datos y en la mayoría de los casos, creación de particiones se realiza en una columna de fecha.

## <a name="benefits-of-partitioning"></a>Ventajas de la creación de particiones
La creación de particiones puede beneficiar el mantenimiento de datos y el rendimiento de las consultas.  Si se beneficia tanto o simplemente uno depende de cómo se cargan los datos y si hello misma columna se puede usar ambos fines, puesto que la creación de particiones solo puede realizarse en una columna.

### <a name="benefits-tooloads"></a>Ventajas tooloads
Hola de las principales ventajas de crear particiones en el almacén de datos SQL es mejorar Hola eficacia y el rendimiento de carga de datos mediante el uso de eliminación de la partición, cambiando y combinar.  En la mayoría de los casos se crean particiones de una fecha de columna que está estrechamente ligada secuencia toohello qué datos hello están la base de datos de toohello cargado.  Una de las mayores ventajas de hello consiste en utilizar particiones toomaintain datos Hola anulación de registro de transacciones.  Mientras que simplemente insertar, actualizar o eliminar datos puede ser el enfoque más sencillo de hello, con un poco de pensamiento y esfuerzo, utilizan las particiones durante el proceso de carga puede mejorar considerablemente el rendimiento.

Modificación de las particiones se puede quitar tooquickly usado o reemplazar una sección de una tabla.  Por ejemplo, una tabla de hechos de ventas podría contener solo los datos para hello últimos 36 meses.  Al final de Hola de cada mes, hello mes más antiguo de los datos de ventas se elimina de hello tabla.  Estos datos se pudieron eliminar mediante delete instrucción toodelete Hola datos para hello mes más antiguo.  Sin embargo, al eliminar una gran cantidad de datos fila por fila con una instrucción delete puede tardar mucho tiempo, así como generar un riesgo de Hola de las transacciones grandes que pueden durar un toorollback mucho tiempo si algo va mal.  Un enfoque más óptimo es la partición más antigua Hola de toosimply colocación de datos.  Donde eliminar filas individuales de hello podría tardar horas, eliminando una partición completa puede tardar a segundos.

### <a name="benefits-tooqueries"></a>Ventajas tooqueries
Creación de particiones, también puede ser usado tooimprove rendimiento de las consultas.  Si una consulta aplica un filtro en una columna de partición, esto puede limitar Hola examen tooonly Hola calificar las particiones que pueden ser un subconjunto mucho más pequeño de datos de hello, evitando un recorrido de tabla completa.  Con la introducción de Hola de índices de almacén de columnas agrupado, ventajas de rendimiento de eliminación de predicado de hello son menos beneficiosas, pero en algunos casos puede ser una ventaja tooqueries.  Por ejemplo, si la tabla de hechos de ventas de Hola se divide en 36 meses mediante el campo de fecha de ventas de hello, a continuación, las consultas que filtrar por fecha de venta de Hola pueden omitir la búsqueda en las particiones que no coinciden con el filtro de Hola.

## <a name="partition-sizing-guidance"></a>Guía sobre el tamaño de las particiones
Durante la creación de particiones pueden mejorar el rendimiento tooimprove usa algunos escenarios, crear una tabla con **demasiados** particiones pueden afectar al rendimiento en algunas circunstancias.  Estas cuestiones se dan especialmente en las tablas de almacén de columnas en clúster.  Para crear particiones toobe útil, es importante toounderstand al número de hello y creación de particiones de toouse de toocreate de particiones.  No existe se ninguna regla de disco duro rápida como toohow número de particiones es demasiado elevado, depende de los datos y cuántas particiones va a cargar toosimultaneously.  Pero como regla general, piense en Agregar 10s too100s de particiones, no 1000s.

Al crear particiones en **almacén de columnas agrupado** tablas, es importante tooconsider cuántas filas se dirigirán a cada partición.  Para que tanto la compresión como el rendimiento de las tablas de almacén de columnas en clúster sean óptimos, se necesita un mínimo de un millón de filas por partición y distribución.  Antes de que se creen particiones, Almacenamiento de datos SQL ya divide cada tabla en 60 bases de datos distribuidas.  Cualquier partición tabla tooa agregado además es distribuciones toohello creadas en segundo plano de Hola.  Con este ejemplo, si tabla de hechos de ventas de hello incluido 36 particiones mensuales y dado que el almacenamiento de datos de SQL tiene 60 distribuciones, a continuación, Hola hechos de ventas tabla debe contener 60 millones de filas por mes o 2.1 millones de filas cuando se rellenan todos los meses.  Si una tabla contiene significativamente menos filas de hello recomienda un mínimo de filas por partición, considere la posibilidad de usar menos particiones en el número de pedido toomake aumento Hola de filas por partición.  Consulte también hello [indización] [ Index] artículo que incluye las consultas que se pueden ejecutar en la calidad del almacenamiento de datos SQL tooassess Hola de índices de almacén de columnas clúster.

## <a name="syntax-difference-from-sql-server"></a>Diferencia con respecto a la sintaxis de SQL Server
Almacenamiento de datos SQL introduce una definición simplificada de particiones que difiere ligeramente de la de SQL Server.  Las funciones y los esquemas de la creación de particiones no se usan en Almacenamiento de datos SQL como en SQL Server.  En su lugar, todo lo que necesita toodo es identificar puntos de límite de hello y columnas con particiones.  Aunque sintaxis Hola de particionamiento pueden ser ligeramente diferente de SQL Server, los conceptos básicos de Hola se Hola mismo.  SQL Server y Almacenamiento de datos SQL admiten una columna de partición por tabla, que puede ser una partición con intervalos.  toolearn más información acerca de la creación de particiones, vea [Partitioned Tables and Indexes][Partitioned Tables and Indexes].

Hola siguiente ejemplo de un almacén de datos de SQL con particiones [CREATE TABLE] [ CREATE TABLE] instrucción, particiones de tabla de hello FactInternetSales en la columna OrderDateKey de hello:

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

## <a name="migrating-partitioning-from-sql-server"></a>Migración de particiones de SQL Server
toomigrate SQL Server simplemente cree particiones definiciones tooSQL almacenamiento de datos:

* Eliminar Hola SQL Server [esquema de partición][partition scheme].
* Agregar hello [función de partición] [ partition function] tooyour crear tabla de definición.

Si va a migrar una tabla con particiones de un saludo de la instancia de SQL Server por debajo de SQL puede ayudarle a número de hello toointerrogate de filas que se encuentran en cada partición.  Tenga en cuenta que si hello se usa misma granularidad de partición en el almacén de datos de SQL, número de Hola de filas por partición disminuirá por un factor de 60.  

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

## <a name="workload-management"></a>Administración de cargas de trabajo
Es un último fragmento consideración toofactor en la decisión de partición de tabla toohello [administración de cargas de trabajo][workload management].  Administración de cargas de trabajo en el almacén de datos de SQL es principalmente un Hola administración de memoria y la simultaneidad.  Hola de almacenamiento de datos SQL memoria máxima asignada tooeach distribución durante la ejecución de la consulta es clases de recursos controlados.  Lo ideal es que se dimensionarán las particiones en consideración a otros factores como Hola necesidades de memoria de la creación de índices de almacén de columnas agrupado.  Los índices de almacén de columnas en clúster suponen una mayor ventaja cuando se les asigna más memoria.  Por lo tanto, le interesará no necesite tooensure que volver a generar un índice de partición de memoria. Aumentar Hola cantidad de memoria disponible tooyour consulta se puede lograr mediante el cambio de rol predeterminado de hello, smallrc, tooone de Hola otros roles, como largerc.

Obtener información sobre la asignación de Hola de memoria por distribución está disponible al consultar vistas de administración dinámica del regulador de recursos de Hola. En realidad la concesión de memoria será menor que las cifras de Hola a continuación. Sin embargo, esto proporciona un nivel de instrucciones que puede utilizar al cambiar el tamaño de las particiones para las operaciones de administración de datos.  Intente tooavoid ajustar el tamaño de las particiones más allá de la concesión de memoria de hello proporcionado por clase de recurso extragrande Hola. Si las particiones aumenta más allá de esta ilustración se corre el riesgo de Hola de presión de memoria, lo que conduce a su vez compresión óptimo que no requiere herramientas.

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

## <a name="partition-switching"></a>Modificación de particiones
Almacenamiento de datos SQL admite la separación, combinación y modificación de particiones. Cada una de estas funciones es ejecutarse con hello [ALTER TABLE] [ ALTER TABLE] instrucción.

tooswitch particiones entre dos tablas que debe asegurarse de que las particiones de Hola se alinean en sus respectivos límites y que coinciden con las definiciones de tabla de Hola. Ya que las restricciones check no están disponibles tooenforce intervalo de Hola de valores en una tabla de origen de tabla Hola debe contener Hola mismo los límites de partición como tabla de destino de Hola. Si este no es el caso de hello, a continuación, cambio de partición de hello generará un error y no se sincronizarán los metadatos de la partición de Hola.

### <a name="how-toosplit-a-partition-that-contains-data"></a>¿Cómo toosplit una partición que contiene los datos
Hola toosplit de método más eficaz una partición que ya contenga datos es toouse un `CTAS` instrucción. Si la tabla con particiones de hello es un almacén de columnas en clúster, a continuación, partición de tabla de hello debe estar vacío antes de se puede dividir.

A continuación, se muestra una tabla de ejemplo con particiones del almacén de columnas que contiene una fila en cada partición:

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
> Crear objeto de estadísticas de hello, garantizamos que metadatos de la tabla están más preciso. Si se omite la creación de estadísticas, Almacenamiento de datos SQL utilizará los valores predeterminados. Para obtener detalles sobre las estadísticas, consulte las [estadísticas][statistics].
> 
> 

A continuación, podemos realizar una consulta de recuento de filas de hello mediante hello `sys.partitions` vista de catálogo:

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

Si intentamos toosplit en esta tabla, se producirá un error:

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

No se pudo msg 35346, nivel 15, estado 1, línea 44 DIVIDIDO cláusula de la instrucción ALTER PARTITION porque Hola partición no está vacía.  Solo las particiones vacías se pueden dividir en cuando existe un índice de almacén de columnas en la tabla de Hola. Considere la posibilidad de deshabilitar el índice de almacén de columnas de hello antes de emitir la instrucción ALTER PARTITION de hello, a continuación, volver a generar el índice de almacén de columnas de hello una vez completada la ALTER PARTITION.

Sin embargo, podemos usar `CTAS` toocreate un nuevo toohold tabla nuestros datos.

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

Tal y como se alinean los límites de partición de Hola se permite un conmutador. Tabla de origen de hello dejará con una partición vacía que posteriormente se puede dividir.

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 too FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

Todo lo que queda toodo es tooalign nuestro toohello datos nuevos de partición límites mediante `CTAS` y cambiar los datos en la tabla principal de toohello

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

Cuando haya completado el movimiento de Hola de datos de hello es estadísticas buena idea toorefresh hello en tooensure de tabla de destino de Hola que reflejan con precisión distribución nueva de Hola de los datos de hello en sus respectivos particiones:

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a>Control de código fuente de particiones de tabla
tooavoid la definición de tabla **int** en el sistema de control de código fuente puede hello tooconsider enfoque:

1. Crear tabla de hello como una tabla con particiones pero sin valores de partición

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

1. `SPLIT`tabla de Hello como parte del proceso de implementación de hello:

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

Con esta hello enfoque código de control de código fuente sigue siendo estático y valores de límite de partición de Hola se permiten toobe dinámico; evolucionado con el almacenamiento de hello con el tiempo.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información, vea los artículos de hello en [información general de la tabla][Overview], [tipos de datos de tabla][Data Types], [distribuir una tabla] [ Distribute], [Indiza una tabla][Index], [mantener las estadísticas de tabla] [ Statistics] y [ Tablas temporales][Temporary].  Para obtener más información sobre los procedimientos recomendados, consulte [Procedimientos recomendados para SQL Data Warehouse de Azure][SQL Data Warehouse Best Practices].

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
