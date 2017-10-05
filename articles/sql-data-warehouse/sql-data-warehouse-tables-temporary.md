---
title: Tablas temporales en SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: fd8c31a727dae3b011aa8294a81f005bad72a278
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="temporary-tables-in-sql-data-warehouse"></a><span data-ttu-id="a6380-103">Tablas temporales en el Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="a6380-103">Temporary tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="a6380-104">[Información general][Overview]</span><span class="sxs-lookup"><span data-stu-id="a6380-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="a6380-105">[Tipos de datos][Data Types]</span><span class="sxs-lookup"><span data-stu-id="a6380-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="a6380-106">[Distribución][Distribute]</span><span class="sxs-lookup"><span data-stu-id="a6380-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="a6380-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="a6380-107">[Index][Index]</span></span>
> * <span data-ttu-id="a6380-108">[Partición][Partition]</span><span class="sxs-lookup"><span data-stu-id="a6380-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="a6380-109">[Estadísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="a6380-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="a6380-110">[Temporal][Temporary]</span><span class="sxs-lookup"><span data-stu-id="a6380-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="a6380-111">Las tablas temporales son muy útiles al procesar datos, especialmente durante la transformación donde los resultados intermedios son transitorios.</span><span class="sxs-lookup"><span data-stu-id="a6380-111">Temporary tables are very useful when processing data - especially during transformation where the intermediate results are transient.</span></span> <span data-ttu-id="a6380-112">Las tablas temporales de Almacenamiento de datos SQL existen en el nivel de sesión.</span><span class="sxs-lookup"><span data-stu-id="a6380-112">In SQL Data Warehouse temporary tables exist at the session level.</span></span>  <span data-ttu-id="a6380-113">Solo son visibles para la sesión en la que se crearon y se eliminan automáticamente cuando esa sesión se cierra.</span><span class="sxs-lookup"><span data-stu-id="a6380-113">They are only visible to the session in which they were created and are automatically dropped when that session logs off.</span></span>  <span data-ttu-id="a6380-114">Las tablas temporales ofrecen ventajas para el rendimiento porque sus resultados se escriben en el almacenamiento local en lugar de en el remoto.</span><span class="sxs-lookup"><span data-stu-id="a6380-114">Temporary tables offer a performance benefit because their results are written to local rather than remote storage.</span></span>  <span data-ttu-id="a6380-115">No son iguales en Almacenamiento de datos SQL que en Base de datos SQL de Azure en el sentido de que se puede acceder a ellas desde cualquier parte de la sesión, incluso dentro y fuera de un procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="a6380-115">Temporary tables are slightly different in Azure SQL Data Warehouse than Azure SQL Database as they can be accessed from anywhere inside the session, including both inside and outside of a stored procedure.</span></span>

<span data-ttu-id="a6380-116">Este artículo contiene directrices esenciales para el uso de tablas temporales y resalta los principios de las tablas temporales de nivel de sesión.</span><span class="sxs-lookup"><span data-stu-id="a6380-116">This article contains essential guidance for using temporary tables and highlights the principles of session level temporary tables.</span></span> <span data-ttu-id="a6380-117">La información de este artículo puede ayudarle a dividir en secciones el código y así mejorar su reusabilidad y facilidad de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="a6380-117">Using the information in this article can help you modularize your code, improving both reusability and ease of maintenance of your code.</span></span>

## <a name="create-a-temporary-table"></a><span data-ttu-id="a6380-118">Creación de una tabla temporal</span><span class="sxs-lookup"><span data-stu-id="a6380-118">Create a temporary table</span></span>
<span data-ttu-id="a6380-119">Las tablas temporales se crean colocando simplemente `#`delante del nombre de la tabla.</span><span class="sxs-lookup"><span data-stu-id="a6380-119">Temporary tables are created by simply prefixing your table name with a `#`.</span></span>  <span data-ttu-id="a6380-120">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a6380-120">For example:</span></span>

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

<span data-ttu-id="a6380-121">También se pueden crear tablas temporales mediante `CTAS` siguiendo exactamente el mismo método:</span><span class="sxs-lookup"><span data-stu-id="a6380-121">Temporary tables can also be created with a `CTAS` using exactly the same approach:</span></span>

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
> <span data-ttu-id="a6380-122">`CTAS` es un comando muy eficaz, con la ventaja adicional de que ofrece un uso muy eficiente del espacio de registro de transacciones.</span><span class="sxs-lookup"><span data-stu-id="a6380-122">`CTAS` is a very powerful command and has the added advantage of being very efficient in its use of transaction log space.</span></span> 
> 
> 

## <a name="dropping-temporary-tables"></a><span data-ttu-id="a6380-123">Eliminación de tablas temporales</span><span class="sxs-lookup"><span data-stu-id="a6380-123">Dropping temporary tables</span></span>
<span data-ttu-id="a6380-124">Cuando se crea una nueva sesión, no debe existir ninguna tabla temporal.</span><span class="sxs-lookup"><span data-stu-id="a6380-124">When a new session is created, no temporary tables should exist.</span></span>  <span data-ttu-id="a6380-125">Sin embargo, si llama al mismo procedimiento almacenado, lo que crea un archivo temporal con el mismo nombre, para tener la seguridad de que las instrucciones `CREATE TABLE` se ejecutan correctamente, se puede usar una sencilla comprobación de existencia previa con `DROP`, como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a6380-125">However, if you are calling the same stored procedure, which creates a temporary with the same name, to ensure that your `CREATE TABLE` statements are successful a simple pre-existence check with a `DROP` can be used as in the below example:</span></span>

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

<span data-ttu-id="a6380-126">Por coherencia con la codificación, se recomienda usar este patrón tanto para tablas como para tablas temporales.</span><span class="sxs-lookup"><span data-stu-id="a6380-126">For coding consistency, it is a good practice to use this pattern for both tables and temporary tables.</span></span>  <span data-ttu-id="a6380-127">También es buena idea usar `DROP TABLE` para quitar las tablas temporales cuando ya no las necesite en el código.</span><span class="sxs-lookup"><span data-stu-id="a6380-127">It is also a good idea to use `DROP TABLE` to remove temporary tables when you have finished with them in your code.</span></span>  <span data-ttu-id="a6380-128">En el desarrollo de procedimientos almacenados es bastante habitual que los comandos de eliminación se empaqueten juntos al final de un procedimiento para garantizar que estos objetos se limpian.</span><span class="sxs-lookup"><span data-stu-id="a6380-128">In stored procedure development it is quite common to see the drop commands bundled together at the end of a procedure to ensure these objects are cleaned up.</span></span>

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a><span data-ttu-id="a6380-129">Modularización de código</span><span class="sxs-lookup"><span data-stu-id="a6380-129">Modularizing code</span></span>
<span data-ttu-id="a6380-130">Como las tablas temporales se pueden ver en cualquier parte de una sesión de usuario, se puede aprovechar este hecho para ayudarle a dividir en secciones el código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="a6380-130">Since temporary tables can be seen anywhere in a user session, this can be exploited to help you modularize your application code.</span></span>  <span data-ttu-id="a6380-131">Por ejemplo, el siguiente procedimiento almacenado reúne los procedimientos recomendados anteriormente para generar DDL, que actualizará todas las estadísticas de la base de datos por el nombre de la estadística.</span><span class="sxs-lookup"><span data-stu-id="a6380-131">For example, the stored procedure below brings together the recommended practices from above to generate DDL which will update all statistics in the database by statistic name.</span></span>

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

<span data-ttu-id="a6380-132">En este punto, la única acción que se ha producido es la creación de un procedimiento almacenado que simplemente generará una tabla temporal, #stats_ddl, con instrucciones DDL.</span><span class="sxs-lookup"><span data-stu-id="a6380-132">At this stage the only action that has occurred is the creation of a stored procedure which will simply generated a temporary table, #stats_ddl, with DDL statements.</span></span>  <span data-ttu-id="a6380-133">Este procedimiento almacenado quitará #stats_ddl si ya existe para tener la seguridad de que no dará error si se ejecuta más de una vez dentro de una sesión.</span><span class="sxs-lookup"><span data-stu-id="a6380-133">This stored procedure will drop #stats_ddl if it already exists to ensure it does not fail if run more than once within a session.</span></span>  <span data-ttu-id="a6380-134">Sin embargo, puesto que no hay ningún elemento `DROP TABLE` al final del procedimiento almacenado, cuando se complete este, saldrá de la tabla creada para que se pueda leer fuera del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="a6380-134">However, since there is no `DROP TABLE` at the end of the stored procedure, when the stored procedure completes, it will leave the created table so that it can be read outside of the stored procedure.</span></span>  <span data-ttu-id="a6380-135">En Almacenamiento de datos SQL, a diferencia de otras bases de datos SQL Server, es posible usar la tabla temporal fuera del procedimiento almacenado que la ha creado.</span><span class="sxs-lookup"><span data-stu-id="a6380-135">In SQL Data Warehouse, unlike other SQL Server databases, it is possible to use the temporary table outside of the procedure that created it.</span></span>  <span data-ttu-id="a6380-136">Las tablas temporales de Almacenamiento de datos SQL se pueden usar **en cualquier parte** dentro de la sesión.</span><span class="sxs-lookup"><span data-stu-id="a6380-136">SQL Data Warehouse temporary tables can be used **anywhere** inside the session.</span></span> <span data-ttu-id="a6380-137">Esto puede dar lugar a código más modular y administrable como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a6380-137">This can lead to more modular and manageable code as in the below example:</span></span>

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

## <a name="temporary-table-limitations"></a><span data-ttu-id="a6380-138">Limitaciones de tablas temporales</span><span class="sxs-lookup"><span data-stu-id="a6380-138">Temporary table limitations</span></span>
<span data-ttu-id="a6380-139">El Almacenamiento de datos SQL impone algunas limitaciones al implementar las tablas temporales.</span><span class="sxs-lookup"><span data-stu-id="a6380-139">SQL Data Warehouse does impose a couple of limitations when implementing temporary tables.</span></span>  <span data-ttu-id="a6380-140">Actualmente, solo se admiten tablas temporales con ámbito de sesión.</span><span class="sxs-lookup"><span data-stu-id="a6380-140">Currently, only session scoped temporary tables are supported.</span></span>  <span data-ttu-id="a6380-141">No se admiten tablas temporales globales.</span><span class="sxs-lookup"><span data-stu-id="a6380-141">Global Temporary Tables are not supported.</span></span>  <span data-ttu-id="a6380-142">Además, no se pueden crear vistas en las tablas temporales.</span><span class="sxs-lookup"><span data-stu-id="a6380-142">In addition, views cannot be created on temporary tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6380-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a6380-143">Next steps</span></span>
<span data-ttu-id="a6380-144">Para obtener más información, consulte los artículos sobre [información general de tablas][Overview], [tipos de datos de tabla][Data Types], [distribución de una tabla][Distribute], [indexación de una tabla][Index], [creación de particiones de una tabla][Partition] y [mantenimiento de estadísticas de tabla][Statistics].</span><span class="sxs-lookup"><span data-stu-id="a6380-144">To learn more, see the articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Maintaining Table Statistics][Statistics].</span></span>  <span data-ttu-id="a6380-145">Para obtener más información sobre los procedimientos recomendados, consulte [Procedimientos recomendados para SQL Data Warehouse de Azure][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="a6380-145">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
