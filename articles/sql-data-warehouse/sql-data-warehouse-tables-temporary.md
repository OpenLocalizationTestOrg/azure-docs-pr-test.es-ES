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
# <a name="temporary-tables-in-sql-data-warehouse"></a><span data-ttu-id="4ae24-103">Tablas temporales en el Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="4ae24-103">Temporary tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="4ae24-104">[Información general][Overview]</span><span class="sxs-lookup"><span data-stu-id="4ae24-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="4ae24-105">[Tipos de datos][Data Types]</span><span class="sxs-lookup"><span data-stu-id="4ae24-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="4ae24-106">[Distribución][Distribute]</span><span class="sxs-lookup"><span data-stu-id="4ae24-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="4ae24-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="4ae24-107">[Index][Index]</span></span>
> * <span data-ttu-id="4ae24-108">[Partición][Partition]</span><span class="sxs-lookup"><span data-stu-id="4ae24-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="4ae24-109">[Estadísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="4ae24-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="4ae24-110">[Temporal][Temporary]</span><span class="sxs-lookup"><span data-stu-id="4ae24-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="4ae24-111">Tablas temporales son muy útiles al procesar datos, especialmente durante la transformación donde los resultados intermedios de hello son transitorios.</span><span class="sxs-lookup"><span data-stu-id="4ae24-111">Temporary tables are very useful when processing data - especially during transformation where hello intermediate results are transient.</span></span> <span data-ttu-id="4ae24-112">En el almacén de datos de SQL tablas temporales existen en el nivel de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ae24-112">In SQL Data Warehouse temporary tables exist at hello session level.</span></span>  <span data-ttu-id="4ae24-113">Son solo visibles toohello sesión en el que se crearon y se quitan automáticamente cuando se cierra la sesión de esa sesión.</span><span class="sxs-lookup"><span data-stu-id="4ae24-113">They are only visible toohello session in which they were created and are automatically dropped when that session logs off.</span></span>  <span data-ttu-id="4ae24-114">Tablas temporales ofrecen una ventaja de rendimiento ya se escriben sus resultados toolocal en lugar de almacenamiento remoto.</span><span class="sxs-lookup"><span data-stu-id="4ae24-114">Temporary tables offer a performance benefit because their results are written toolocal rather than remote storage.</span></span>  <span data-ttu-id="4ae24-115">Las tablas temporales son ligeramente diferentes en el almacén de datos de SQL Azure de la base de datos de SQL Azure, tal y como puede tener acceso desde cualquier lugar dentro de la sesión de hello, incluidos tanto dentro como fuera de un procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="4ae24-115">Temporary tables are slightly different in Azure SQL Data Warehouse than Azure SQL Database as they can be accessed from anywhere inside hello session, including both inside and outside of a stored procedure.</span></span>

<span data-ttu-id="4ae24-116">Este artículo contiene instrucciones esenciales para el uso de tablas temporales y resalta los principios de Hola de tablas temporales de nivel de sesión.</span><span class="sxs-lookup"><span data-stu-id="4ae24-116">This article contains essential guidance for using temporary tables and highlights hello principles of session level temporary tables.</span></span> <span data-ttu-id="4ae24-117">Uso de información de Hola en este artículo puede ayudarle a modularizar el código, mejorar la reusabilidad y la facilidad de mantenimiento del código.</span><span class="sxs-lookup"><span data-stu-id="4ae24-117">Using hello information in this article can help you modularize your code, improving both reusability and ease of maintenance of your code.</span></span>

## <a name="create-a-temporary-table"></a><span data-ttu-id="4ae24-118">Creación de una tabla temporal</span><span class="sxs-lookup"><span data-stu-id="4ae24-118">Create a temporary table</span></span>
<span data-ttu-id="4ae24-119">Las tablas temporales se crean colocando simplemente `#`delante del nombre de la tabla.</span><span class="sxs-lookup"><span data-stu-id="4ae24-119">Temporary tables are created by simply prefixing your table name with a `#`.</span></span>  <span data-ttu-id="4ae24-120">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4ae24-120">For example:</span></span>

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

<span data-ttu-id="4ae24-121">También se pueden crear tablas temporales con un `CTAS` exactamente utilizando Hola mismo enfoque:</span><span class="sxs-lookup"><span data-stu-id="4ae24-121">Temporary tables can also be created with a `CTAS` using exactly hello same approach:</span></span>

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
> <span data-ttu-id="4ae24-122">`CTAS`es un comando muy eficaces y añadió hello ventaja de estar muy eficaz en el uso de espacio de registro de transacciones.</span><span class="sxs-lookup"><span data-stu-id="4ae24-122">`CTAS` is a very powerful command and has hello added advantage of being very efficient in its use of transaction log space.</span></span> 
> 
> 

## <a name="dropping-temporary-tables"></a><span data-ttu-id="4ae24-123">Eliminación de tablas temporales</span><span class="sxs-lookup"><span data-stu-id="4ae24-123">Dropping temporary tables</span></span>
<span data-ttu-id="4ae24-124">Cuando se crea una nueva sesión, no debe existir ninguna tabla temporal.</span><span class="sxs-lookup"><span data-stu-id="4ae24-124">When a new session is created, no temporary tables should exist.</span></span>  <span data-ttu-id="4ae24-125">Sin embargo, si se está llamando a Hola mismo procedimiento almacenado, que crea un archivo temporal con hello homónimas, tooensure que su `CREATE TABLE` instrucciones son correctas una comprobación de existencia previa simple con un `DROP` puede utilizarse como en hello ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4ae24-125">However, if you are calling hello same stored procedure, which creates a temporary with hello same name, tooensure that your `CREATE TABLE` statements are successful a simple pre-existence check with a `DROP` can be used as in hello below example:</span></span>

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

<span data-ttu-id="4ae24-126">Para la codificación de coherencia, es una buena práctica toouse este patrón para las tablas y las tablas temporales.</span><span class="sxs-lookup"><span data-stu-id="4ae24-126">For coding consistency, it is a good practice toouse this pattern for both tables and temporary tables.</span></span>  <span data-ttu-id="4ae24-127">También es una buena idea toouse `DROP TABLE` tooremove tablas temporales cuando haya terminado con ellos en el código.</span><span class="sxs-lookup"><span data-stu-id="4ae24-127">It is also a good idea toouse `DROP TABLE` tooremove temporary tables when you have finished with them in your code.</span></span>  <span data-ttu-id="4ae24-128">En el desarrollo del procedimiento almacenado es bastante común toosee Hola comandos drop agrupados final Hola de un procedimiento tooensure que estos objetos se limpian.</span><span class="sxs-lookup"><span data-stu-id="4ae24-128">In stored procedure development it is quite common toosee hello drop commands bundled together at hello end of a procedure tooensure these objects are cleaned up.</span></span>

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a><span data-ttu-id="4ae24-129">Modularización de código</span><span class="sxs-lookup"><span data-stu-id="4ae24-129">Modularizing code</span></span>
<span data-ttu-id="4ae24-130">Puesto que las tablas temporales se pueden ver en cualquier parte en una sesión de usuario, puede ser aprovechada toohelp modularizar el código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="4ae24-130">Since temporary tables can be seen anywhere in a user session, this can be exploited toohelp you modularize your application code.</span></span>  <span data-ttu-id="4ae24-131">Por ejemplo, hello procedimiento almacenado siguiente reúne Hola procedimientos desde encima toogenerate DDL que se actualizará todas las estadísticas de la base de datos de hello recomendado por el nombre de estadística.</span><span class="sxs-lookup"><span data-stu-id="4ae24-131">For example, hello stored procedure below brings together hello recommended practices from above toogenerate DDL which will update all statistics in hello database by statistic name.</span></span>

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

<span data-ttu-id="4ae24-132">En esta fase Hola única acción que se ha producido es creación de hello de un procedimiento almacenado, lo que simplemente genera una tabla temporal, stats_ddl #, con instrucciones de DDL.</span><span class="sxs-lookup"><span data-stu-id="4ae24-132">At this stage hello only action that has occurred is hello creation of a stored procedure which will simply generated a temporary table, #stats_ddl, with DDL statements.</span></span>  <span data-ttu-id="4ae24-133">Este procedimiento almacenado colocará #stats_ddl si ya existe tooensure que no producirá un error si ejecuta más de una vez dentro de una sesión.</span><span class="sxs-lookup"><span data-stu-id="4ae24-133">This stored procedure will drop #stats_ddl if it already exists tooensure it does not fail if run more than once within a session.</span></span>  <span data-ttu-id="4ae24-134">Sin embargo, dado que no hay ningún `DROP TABLE` al final de Hola de procedimiento almacenado de hello, cuando hello procedimiento almacenado se completa, dejará tabla Hola creado para que sólo pueda leerlo fuera de procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ae24-134">However, since there is no `DROP TABLE` at hello end of hello stored procedure, when hello stored procedure completes, it will leave hello created table so that it can be read outside of hello stored procedure.</span></span>  <span data-ttu-id="4ae24-135">En el almacén de datos de SQL, a diferencia de otras bases de datos de SQL Server, es tabla temporal de hello toouse posibles fuera de procedimiento de Hola que lo creó.</span><span class="sxs-lookup"><span data-stu-id="4ae24-135">In SQL Data Warehouse, unlike other SQL Server databases, it is possible toouse hello temporary table outside of hello procedure that created it.</span></span>  <span data-ttu-id="4ae24-136">Tablas temporales de almacenamiento de datos de SQL se pueden usar **en cualquier lugar** dentro de la sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ae24-136">SQL Data Warehouse temporary tables can be used **anywhere** inside hello session.</span></span> <span data-ttu-id="4ae24-137">Esto puede provocar toomore código modular y fácil de administrar en hello ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4ae24-137">This can lead toomore modular and manageable code as in hello below example:</span></span>

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

## <a name="temporary-table-limitations"></a><span data-ttu-id="4ae24-138">Limitaciones de tablas temporales</span><span class="sxs-lookup"><span data-stu-id="4ae24-138">Temporary table limitations</span></span>
<span data-ttu-id="4ae24-139">El Almacenamiento de datos SQL impone algunas limitaciones al implementar las tablas temporales.</span><span class="sxs-lookup"><span data-stu-id="4ae24-139">SQL Data Warehouse does impose a couple of limitations when implementing temporary tables.</span></span>  <span data-ttu-id="4ae24-140">Actualmente, solo se admiten tablas temporales con ámbito de sesión.</span><span class="sxs-lookup"><span data-stu-id="4ae24-140">Currently, only session scoped temporary tables are supported.</span></span>  <span data-ttu-id="4ae24-141">No se admiten tablas temporales globales.</span><span class="sxs-lookup"><span data-stu-id="4ae24-141">Global Temporary Tables are not supported.</span></span>  <span data-ttu-id="4ae24-142">Además, no se pueden crear vistas en las tablas temporales.</span><span class="sxs-lookup"><span data-stu-id="4ae24-142">In addition, views cannot be created on temporary tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ae24-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4ae24-143">Next steps</span></span>
<span data-ttu-id="4ae24-144">toolearn más información, vea los artículos de hello en [información general de la tabla][Overview], [tipos de datos de tabla][Data Types], [distribuir una tabla] [ Distribute], [Indiza una tabla][Index], [creación de particiones de una tabla] [ Partition] y [ Mantener las estadísticas de tabla][Statistics].</span><span class="sxs-lookup"><span data-stu-id="4ae24-144">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Maintaining Table Statistics][Statistics].</span></span>  <span data-ttu-id="4ae24-145">Para obtener más información sobre los procedimientos recomendados, consulte [Procedimientos recomendados para SQL Data Warehouse de Azure][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="4ae24-145">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
