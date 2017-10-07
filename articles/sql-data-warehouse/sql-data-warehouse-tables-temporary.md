---
title: "tablas de aaaTemporary en el almacén de datos de SQL | Documentos de Microsoft"
description: "Introducción a las tablas temporales en Almacenamiento de datos SQL de Azure."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 9b1119eb-7f54-46d0-ad74-19c85a2a555a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 2e8b122eb6d71d5bc0a99ce8a2ecab5dbe2d1b49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="temporary-tables-in-sql-data-warehouse"></a>Tablas temporales en el Almacenamiento de datos SQL
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

Tablas temporales son muy útiles al procesar datos, especialmente durante la transformación donde los resultados intermedios de hello son transitorios. En el almacén de datos de SQL tablas temporales existen en el nivel de sesión de Hola.  Son solo visibles toohello sesión en el que se crearon y se quitan automáticamente cuando se cierra la sesión de esa sesión.  Tablas temporales ofrecen una ventaja de rendimiento ya se escriben sus resultados toolocal en lugar de almacenamiento remoto.  Las tablas temporales son ligeramente diferentes en el almacén de datos de SQL Azure de la base de datos de SQL Azure, tal y como puede tener acceso desde cualquier lugar dentro de la sesión de hello, incluidos tanto dentro como fuera de un procedimiento almacenado.

Este artículo contiene instrucciones esenciales para el uso de tablas temporales y resalta los principios de Hola de tablas temporales de nivel de sesión. Uso de información de Hola en este artículo puede ayudarle a modularizar el código, mejorar la reusabilidad y la facilidad de mantenimiento del código.

## <a name="create-a-temporary-table"></a>Creación de una tabla temporal
Las tablas temporales se crean colocando simplemente `#`delante del nombre de la tabla.  Por ejemplo:

```sql
CREATE TABLE #stats_ddl
(
    [schema_name]        NVARCHAR(128) NOT NULL
,    [table_name]            NVARCHAR(128) NOT NULL
,    [stats_name]            NVARCHAR(128) NOT NULL
,    [stats_is_filtered]     BIT           NOT NULL
,    [seq_nmbr]              BIGINT        NOT NULL
,    [two_part_name]         NVARCHAR(260) NOT NULL
,    [three_part_name]       NVARCHAR(400) NOT NULL
)
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
```

También se pueden crear tablas temporales con un `CTAS` exactamente utilizando Hola mismo enfoque:

```sql
CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
``` 

> [!NOTE]
> `CTAS`es un comando muy eficaces y añadió hello ventaja de estar muy eficaz en el uso de espacio de registro de transacciones. 
> 
> 

## <a name="dropping-temporary-tables"></a>Eliminación de tablas temporales
Cuando se crea una nueva sesión, no debe existir ninguna tabla temporal.  Sin embargo, si se está llamando a Hola mismo procedimiento almacenado, que crea un archivo temporal con hello homónimas, tooensure que su `CREATE TABLE` instrucciones son correctas una comprobación de existencia previa simple con un `DROP` puede utilizarse como en hello ejemplo siguiente:

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

Para la codificación de coherencia, es una buena práctica toouse este patrón para las tablas y las tablas temporales.  También es una buena idea toouse `DROP TABLE` tooremove tablas temporales cuando haya terminado con ellos en el código.  En el desarrollo del procedimiento almacenado es bastante común toosee Hola comandos drop agrupados final Hola de un procedimiento tooensure que estos objetos se limpian.

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a>Modularización de código
Puesto que las tablas temporales se pueden ver en cualquier parte en una sesión de usuario, puede ser aprovechada toohelp modularizar el código de aplicación.  Por ejemplo, hello procedimiento almacenado siguiente reúne Hola procedimientos desde encima toogenerate DDL que se actualizará todas las estadísticas de la base de datos de hello recomendado por el nombre de estadística.

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_update_stats]
(   @update_type    tinyint -- 1 default 2 fullscan 3 sample 4 resample
    ,@sample_pct     tinyint
)
AS

IF @update_type NOT IN (1,2,3,4)
BEGIN;
    THROW 151000,'Invalid value for @update_type parameter. Valid range 1 (default), 2 (fullscan), 3 (sample) or 4 (resample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END

CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
GO
```

En esta fase Hola única acción que se ha producido es creación de hello de un procedimiento almacenado, lo que simplemente genera una tabla temporal, stats_ddl #, con instrucciones de DDL.  Este procedimiento almacenado colocará #stats_ddl si ya existe tooensure que no producirá un error si ejecuta más de una vez dentro de una sesión.  Sin embargo, dado que no hay ningún `DROP TABLE` al final de Hola de procedimiento almacenado de hello, cuando hello procedimiento almacenado se completa, dejará tabla Hola creado para que sólo pueda leerlo fuera de procedimiento almacenado de Hola.  En el almacén de datos de SQL, a diferencia de otras bases de datos de SQL Server, es tabla temporal de hello toouse posibles fuera de procedimiento de Hola que lo creó.  Tablas temporales de almacenamiento de datos de SQL se pueden usar **en cualquier lugar** dentro de la sesión de Hola. Esto puede provocar toomore código modular y fácil de administrar en hello ejemplo siguiente:

```sql
EXEC [dbo].[prc_sqldw_update_stats] @update_type = 1, @sample_pct = NULL;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''

WHILE @i <= @t
BEGIN
    SET @s=(SELECT update_stats_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

## <a name="temporary-table-limitations"></a>Limitaciones de tablas temporales
El Almacenamiento de datos SQL impone algunas limitaciones al implementar las tablas temporales.  Actualmente, solo se admiten tablas temporales con ámbito de sesión.  No se admiten tablas temporales globales.  Además, no se pueden crear vistas en las tablas temporales.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información, vea los artículos de hello en [información general de la tabla][Overview], [tipos de datos de tabla][Data Types], [distribuir una tabla] [ Distribute], [Indiza una tabla][Index], [creación de particiones de una tabla] [ Partition] y [ Mantener las estadísticas de tabla][Statistics].  Para obtener más información sobre los procedimientos recomendados, consulte [Procedimientos recomendados para SQL Data Warehouse de Azure][SQL Data Warehouse Best Practices].

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

<!--MSDN references-->

<!--Other Web references-->
