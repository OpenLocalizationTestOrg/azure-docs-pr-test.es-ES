---
title: "aaaManage los datos históricos en las tablas temporales con directiva de retención | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse retención temporal directiva tookeep datos históricos bajo su control."
services: sql-database
documentationcenter: 
author: bonova
manager: drasumic
editor: 
ms.assetid: 76cfa06a-e758-453e-942c-9f1ed6a38c2a
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 10/12/2016
ms.author: bonova
ms.openlocfilehash: a72a6111a6cd7322d734d08bf3852e95f5ffea8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a><span data-ttu-id="abdeb-103">Administración de datos históricos en tablas temporales con directivas de retención</span><span class="sxs-lookup"><span data-stu-id="abdeb-103">Manage historical data in Temporal Tables with retention policy</span></span>
<span data-ttu-id="abdeb-104">Las tablas temporales pueden aumentar el tamaño de la base de datos más que las tablas normales, especialmente si conserva datos históricos durante un período de tiempo más largo.</span><span class="sxs-lookup"><span data-stu-id="abdeb-104">Temporal Tables may increase database size more than regular tables, especially if you retain historical data for a longer period of time.</span></span> <span data-ttu-id="abdeb-105">Por lo tanto, la directiva de retención para datos históricos es un aspecto importante de planeación y la administración del ciclo de vida de Hola de cada tabla temporal.</span><span class="sxs-lookup"><span data-stu-id="abdeb-105">Hence, retention policy for historical data is an important aspect of planning and managing hello lifecycle of every temporal table.</span></span> <span data-ttu-id="abdeb-106">Las tablas temporales de Azure SQL Database incluyen un mecanismo de retención fácil de usar que ayuda a realizar esta tarea.</span><span class="sxs-lookup"><span data-stu-id="abdeb-106">Temporal Tables in Azure SQL Database come with easy-to-use retention mechanism that helps you accomplish this task.</span></span>

<span data-ttu-id="abdeb-107">Retención de historial temporal puede configurarse en el nivel de tabla individuales de hello, que permite a los usuarios las directivas de caducidad flexible toocreate.</span><span class="sxs-lookup"><span data-stu-id="abdeb-107">Temporal history retention can be configured at hello individual table level, which allows users toocreate flexible aging polices.</span></span> <span data-ttu-id="abdeb-108">Aplicar la retención temporal es simple: requiere un único toobe parámetro establecido durante el cambio de esquema o de creación de tabla.</span><span class="sxs-lookup"><span data-stu-id="abdeb-108">Applying temporal retention is simple: it requires only one parameter toobe set during table creation or schema change.</span></span>

<span data-ttu-id="abdeb-109">Después de definir la directiva de retención, Azure SQL Database comenzará a comprobar periódicamente si hay filas históricas que son aptas para la limpieza automática de datos.</span><span class="sxs-lookup"><span data-stu-id="abdeb-109">After you define retention policy, Azure SQL Database starts checking regularly if there are historical rows that are eligible for automatic data cleanup.</span></span> <span data-ttu-id="abdeb-110">Identificación de las filas coincidentes y su eliminación de la tabla de historial de Hola se producen de forma transparente, en la tarea en segundo plano Hola programado y ejecutado por el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="abdeb-110">Identification of matching rows and their removal from hello history table occur transparently, in hello background task that is scheduled and run by hello system.</span></span> <span data-ttu-id="abdeb-111">Se comprueba la condición de edad para las filas de tabla de historial de hello en función de la columna de Hola que representa el final del período de SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="abdeb-111">Age condition for hello history table rows is checked based on hello column representing end of SYSTEM_TIME period.</span></span> <span data-ttu-id="abdeb-112">Si el período de retención, por ejemplo, se establece toosix en meses, filas aptas para la limpieza de la tabla satisfacen Hola siguiente condición:</span><span class="sxs-lookup"><span data-stu-id="abdeb-112">If retention period, for example, is set toosix months, table rows eligible for cleanup satisfy hello following condition:</span></span>

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

<span data-ttu-id="abdeb-113">En el anterior ejemplo de Hola, asumimos que **ValidTo** columna corresponde toohello final del período de SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="abdeb-113">In hello preceding example, we assumed that **ValidTo** column corresponds toohello end of SYSTEM_TIME period.</span></span>

## <a name="how-tooconfigure-retention-policy"></a><span data-ttu-id="abdeb-114">¿La directiva de retención de tooconfigure?</span><span class="sxs-lookup"><span data-stu-id="abdeb-114">How tooconfigure retention policy?</span></span>
<span data-ttu-id="abdeb-115">Antes de configurar la directiva de retención para una tabla temporal, primero compruebe si está habilitada la retención de historial temporal *en el nivel de base de datos de hello*.</span><span class="sxs-lookup"><span data-stu-id="abdeb-115">Before you configure retention policy for a temporal table, check first whether temporal historical retention is enabled *at hello database level*.</span></span>

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

<span data-ttu-id="abdeb-116">Marca la base de datos **is_temporal_history_retention_enabled** es tooON de conjunto de forma predeterminada, pero los usuarios pueden cambiar con la instrucción ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="abdeb-116">Database flag **is_temporal_history_retention_enabled** is set tooON by default, but users can change it with ALTER DATABASE statement.</span></span> <span data-ttu-id="abdeb-117">También es automáticamente set tooOFF después [punto de restauración a un momento](sql-database-recovery-using-backups.md) operación.</span><span class="sxs-lookup"><span data-stu-id="abdeb-117">It is also automatically set tooOFF after [point in time restore](sql-database-recovery-using-backups.md) operation.</span></span> <span data-ttu-id="abdeb-118">tooenable la limpieza de la retención de historial temporal para la base de datos, ejecute hello siguiente instrucción:</span><span class="sxs-lookup"><span data-stu-id="abdeb-118">tooenable temporal history retention cleanup for your database, execute hello following statement:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> <span data-ttu-id="abdeb-119">Puede configurar la retención para tablas temporales aunque **is_temporal_history_retention_enabled** esté establecida en OFF, pero en ese caso no se desencadenará la limpieza automática de las filas de datos antiguos.</span><span class="sxs-lookup"><span data-stu-id="abdeb-119">You can configure retention for temporal tables even if **is_temporal_history_retention_enabled** is OFF, but automatic cleanup for aged rows is not triggered in that case.</span></span>
> 
> 

<span data-ttu-id="abdeb-120">Directiva de retención se configura durante la creación de una tabla especificando el valor de parámetro de hello HISTORY_RETENTION_PERIOD:</span><span class="sxs-lookup"><span data-stu-id="abdeb-120">Retention policy is configured during table creation by specifying value for hello HISTORY_RETENTION_PERIOD parameter:</span></span>

````
CREATE TABLE dbo.WebsiteUserInfo
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH
 (
     SYSTEM_VERSIONING = ON
     (
        HISTORY_TABLE = dbo.WebsiteUserInfoHistory,
        HISTORY_RETENTION_PERIOD = 6 MONTHS
     )
 );
````

<span data-ttu-id="abdeb-121">La base de datos de SQL Azure le permite toospecify período de retención mediante el uso de unidades de tiempo diferentes: días, semanas, meses y años.</span><span class="sxs-lookup"><span data-stu-id="abdeb-121">Azure SQL Database allows you toospecify retention period by using different time units: DAYS, WEEKS, MONTHS, and YEARS.</span></span> <span data-ttu-id="abdeb-122">Si se omite HISTORY_RETENTION_PERIOD, se supone una retención INFINITA.</span><span class="sxs-lookup"><span data-stu-id="abdeb-122">If HISTORY_RETENTION_PERIOD is omitted, INFINITE retention is assumed.</span></span> <span data-ttu-id="abdeb-123">También puede usar explícitamente la palabra clave INFINITO.</span><span class="sxs-lookup"><span data-stu-id="abdeb-123">You can also use INFINITE keyword explicitly.</span></span>

<span data-ttu-id="abdeb-124">En algunos escenarios, puede que desee tooconfigure retención después de la creación de una tabla o toochange valor configurado previamente.</span><span class="sxs-lookup"><span data-stu-id="abdeb-124">In some scenarios, you may want tooconfigure retention after table creation, or toochange previously configured value.</span></span> <span data-ttu-id="abdeb-125">En ese caso use la instrucción ALTER TABLE:</span><span class="sxs-lookup"><span data-stu-id="abdeb-125">In that case use ALTER TABLE statement:</span></span>

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> <span data-ttu-id="abdeb-126">Establecer SYSTEM_VERSIONING tooOFF *no conserva* valor de período de retención.</span><span class="sxs-lookup"><span data-stu-id="abdeb-126">Setting SYSTEM_VERSIONING tooOFF *does not preserve* retention period value.</span></span> <span data-ttu-id="abdeb-127">Establecer SYSTEM_VERSIONING tooON sin HISTORY_RETENTION_PERIOD especifica explícitamente resultados en el período de retención INFINITA de Hola.</span><span class="sxs-lookup"><span data-stu-id="abdeb-127">Setting SYSTEM_VERSIONING tooON without HISTORY_RETENTION_PERIOD specified explicitly results in hello INFINITE retention period.</span></span>
> 
> 

<span data-ttu-id="abdeb-128">tooreview el estado actual de la directiva de retención de hello, uso siguiente de hello consulta dicha marca de habilitación de retención temporal de combinaciones en el nivel de base de datos de hello con períodos de retención para tablas individuales:</span><span class="sxs-lookup"><span data-stu-id="abdeb-128">tooreview current state of hello retention policy, use hello following query that joins temporal retention enablement flag at hello database level with retention periods for individual tables:</span></span>

````
SELECT DB.is_temporal_history_retention_enabled,
SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,
T1.name as TemporalTableName,  SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,
T2.name as HistoryTableName,T1.history_retention_period,
T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases
where name = DB_NAME()) AS DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2
````


## <a name="how-sql-database-deletes-aged-rows"></a><span data-ttu-id="abdeb-129">¿Cómo SQL Database elimina las filas antiguas?</span><span class="sxs-lookup"><span data-stu-id="abdeb-129">How SQL Database deletes aged rows?</span></span>
<span data-ttu-id="abdeb-130">proceso de limpieza de Hello depende de diseño del índice de Hola de tabla de historial de Hola.</span><span class="sxs-lookup"><span data-stu-id="abdeb-130">hello cleanup process depends on hello index layout of hello history table.</span></span> <span data-ttu-id="abdeb-131">Es importante toonotice que *sólo tablas de historial con un índice agrupado (árbol B o almacén de columnas) pueden tener una directiva de retención finito configurado*.</span><span class="sxs-lookup"><span data-stu-id="abdeb-131">It is important toonotice that *only history tables with a clustered index (B-tree or columnstore) can have finite retention policy configured*.</span></span> <span data-ttu-id="abdeb-132">Una tarea en segundo plano se crea tooperform de limpieza de datos antiguos para todas las tablas temporales con el período de retención finito.</span><span class="sxs-lookup"><span data-stu-id="abdeb-132">A background task is created tooperform aged data cleanup for all temporal tables with finite retention period.</span></span>
<span data-ttu-id="abdeb-133">Lógica de limpieza para el índice agrupado de almacén de filas (árbol B) Hola elimina la fila antigua en fragmentos más pequeños (arriba too10K) minimizar la presión en el registro de base de datos y el subsistema de E/S.</span><span class="sxs-lookup"><span data-stu-id="abdeb-133">Cleanup logic for hello rowstore (B-tree) clustered index deletes aged row in smaller chunks (up too10K) minimizing pressure on database log and I/O subsystem.</span></span> <span data-ttu-id="abdeb-134">A pesar de que utiliza la lógica de limpieza necesarias índice de árbol B, orden de las eliminaciones de filas de hello antigüedad mayor que el período de retención no se puede garantizar bien.</span><span class="sxs-lookup"><span data-stu-id="abdeb-134">Although cleanup logic utilizes required B-tree index, order of deletions for hello rows older than retention period cannot be firmly guaranteed.</span></span> <span data-ttu-id="abdeb-135">Por lo tanto, *no tienen ninguna dependencia en el orden de limpieza de hello en sus aplicaciones*.</span><span class="sxs-lookup"><span data-stu-id="abdeb-135">Hence, *do not take any dependency on hello cleanup order in your applications*.</span></span>

<span data-ttu-id="abdeb-136">Hello tarea limpieza de hello en clúster de almacén de columnas quita todo [grupos de filas](https://msdn.microsoft.com/library/gg492088.aspx) a la vez (normalmente contiene 1 millón de filas cada uno), que es muy eficaz, especialmente cuando los datos históricos se generan a un ritmo alta.</span><span class="sxs-lookup"><span data-stu-id="abdeb-136">hello cleanup task for hello clustered columnstore removes entire [row groups](https://msdn.microsoft.com/library/gg492088.aspx) at once (typically contain 1 million of rows each), which is very efficient, especially when historical data is generated at a high pace.</span></span>

![Retención de almacén de columnas agrupado](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

<span data-ttu-id="abdeb-138">La excelente compresión de datos y la eficaz limpieza de retención convierten al índice del almacén de columnas agrupado en una perfecta opción en escenarios en los que la carga de trabajo genera rápidamente gran cantidad de datos históricos.</span><span class="sxs-lookup"><span data-stu-id="abdeb-138">Excellent data compression and efficient retention cleanup makes clustered columnstore index a perfect choice for scenarios when your workload rapidly generates high amount of historical data.</span></span> <span data-ttu-id="abdeb-139">Este patrón es típico de [cargas de trabajo intensivas de procesamiento de transacciones que usan tablas temporales](https://msdn.microsoft.com/library/mt631669.aspx) para el seguimiento de cambios y la auditoría, el análisis de tendencias o la ingesta de datos de IoT.</span><span class="sxs-lookup"><span data-stu-id="abdeb-139">That pattern is typical for intensive [transactional processing workloads that use temporal tables](https://msdn.microsoft.com/library/mt631669.aspx) for change tracking and auditing, trend analysis, or IoT data ingestion.</span></span>

## <a name="index-considerations"></a><span data-ttu-id="abdeb-140">Consideraciones sobre el índice</span><span class="sxs-lookup"><span data-stu-id="abdeb-140">Index considerations</span></span>
<span data-ttu-id="abdeb-141">tarea de limpieza de Hello para las tablas con índice agrupado de almacén requiere toostart de índice con finales Hola Hola columna correspondientes de periodo SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="abdeb-141">hello cleanup task for tables with rowstore clustered index requires index toostart with hello column corresponding hello end of SYSTEM_TIME period.</span></span> <span data-ttu-id="abdeb-142">Si este tipo de índice no existe, no se puede configurar un periodo de retención finito:</span><span class="sxs-lookup"><span data-stu-id="abdeb-142">If such index doesn't exist, you cannot configure a finite retention period:</span></span>

<span data-ttu-id="abdeb-143">*Msg 13765, nivel 16, estado 1 <br> </br> período de retención finito no se pudo establecer en la tabla temporal con versión del sistema 'temporalstagetestdb.dbo.WebsiteUserInfo' porque la tabla de historial de hello ' temporalstagetestdb.dbo.WebsiteUserInfoHistory' no contiene el índice clúster necesaria. Considere la posibilidad de crear un almacén de columnas agrupado o un índice de árbol B a partir de columna de Hola que coincide con el final de SYSTEM_TIME period, en la tabla de historial de Hola.*</span><span class="sxs-lookup"><span data-stu-id="abdeb-143">*Msg 13765, Level 16, State 1 <br></br> Setting finite retention period failed on system-versioned temporal table 'temporalstagetestdb.dbo.WebsiteUserInfo' because hello history table 'temporalstagetestdb.dbo.WebsiteUserInfoHistory' does not contain required clustered index. Consider creating a clustered columnstore or B-tree index starting with hello column that matches end of SYSTEM_TIME period, on hello history table.*</span></span>

<span data-ttu-id="abdeb-144">Es importante toonotice que Hola tabla de historial de predeterminada creada por base de datos de SQL Azure ya tiene el índice, que es compatible con directiva de retención de clúster.</span><span class="sxs-lookup"><span data-stu-id="abdeb-144">It is important toonotice that hello default history table created by Azure SQL Database already has clustered index, which is compliant for retention policy.</span></span> <span data-ttu-id="abdeb-145">Si intentas tooremove ese índice en una tabla con el período de retención finito, se produce un error en la operación con hello siguiente error:</span><span class="sxs-lookup"><span data-stu-id="abdeb-145">If you try tooremove that index on a table with finite retention period, operation fails with hello following error:</span></span>

<span data-ttu-id="abdeb-146">*Msg 13766, nivel 16, estado 1 <br> </br> no se puede quitar el índice agrupado de hello 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' porque está siendo utilizado para la limpieza automática de los datos antiguos. Considere la posibilidad de configuración HISTORY_RETENTION_PERIOD tooINFINITE en tabla temporal con versión del sistema correspondiente Hola si necesita toodrop este índice.*</span><span class="sxs-lookup"><span data-stu-id="abdeb-146">*Msg 13766, Level 16, State 1 <br></br> Cannot drop hello clustered index 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' because it is being used for automatic cleanup of aged data. Consider setting HISTORY_RETENTION_PERIOD tooINFINITE on hello corresponding system-versioned temporal table if you need toodrop this index.*</span></span>

<span data-ttu-id="abdeb-147">Liberador de espacio en el índice de almacén de columnas agrupado Hola funcione de manera óptima si se insertan filas históricas en orden ascendente (ordenado por final Hola de columna de período), que siempre es el caso de hello cuando se rellena la tabla de historial de hello exclusivamente por hello SYSTEM_ de Hola Mecanismo VERSIONIOING.</span><span class="sxs-lookup"><span data-stu-id="abdeb-147">Cleanup on hello clustered columnstore index works optimally if historical rows are inserted in hello ascending order (ordered by hello end of period column), which is always hello case when hello history table is populated exclusively by hello SYSTEM_VERSIONIOING mechanism.</span></span> <span data-ttu-id="abdeb-148">Si no se ordenan filas de tabla de historial de hello al final de la columna de periodo (que puede ser el caso de hello si ha migrado los datos históricos existentes), debe volver a crear índice de almacén de columnas agrupado sobre el índice de almacén de filas de árbol B que está ordenado correctamente, tooachieve óptimo rendimiento.</span><span class="sxs-lookup"><span data-stu-id="abdeb-148">If rows in hello history table are not ordered by end of period column (which may be hello case if you migrated existing historical data), you should re-create clustered columnstore index on top of B-tree rowstore index that is properly ordered, tooachieve optimal performance.</span></span>

<span data-ttu-id="abdeb-149">Evitar volver a generar índice de almacén de columnas agrupado en la tabla de historial de hello con período de retención finita de hello, ya que puede cambiar la ordenación en grupos de filas de hello naturalmente impuestos por la operación de control de versiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="abdeb-149">Avoid rebuilding clustered columnstore index on hello history table with hello finite retention period, because it may change ordering in hello row groups naturally imposed by hello system-versioning operation.</span></span> <span data-ttu-id="abdeb-150">Si necesita toorebuild índice de almacén de columnas agrupado en la tabla de historial de hello, hágalo por volver a crearla en la parte superior compatible con índice de árbol B, conserva la ordenación en grupos de filas de hello necesarios para la limpieza de datos normal.</span><span class="sxs-lookup"><span data-stu-id="abdeb-150">If you need toorebuild clustered columnstore index on hello history table, do that by re-creating it on top of compliant B-tree index, preserving ordering in hello rowgroups necessary for regular data cleanup.</span></span> <span data-ttu-id="abdeb-151">Hola mismo enfoque debe realizarse si crear tabla temporal con tabla de historial existente que tiene el índice de columna sin orden de datos garantizada clúster:</span><span class="sxs-lookup"><span data-stu-id="abdeb-151">hello same approach should be taken if you create temporal table with existing history table that has clustered column index without guaranteed data order:</span></span>

````
/*Create B-tree ordered by hello end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

<span data-ttu-id="abdeb-152">Cuando el período de retención finito está configurado para la tabla de historial de hello con índice de almacén de columnas agrupado hello, no se puede crear otros índices de árbol B no agrupado en la tabla:</span><span class="sxs-lookup"><span data-stu-id="abdeb-152">When finite retention period is configured for hello history table with hello clustered columnstore index, you cannot create additional non-clustered B-tree indexes on that table:</span></span>

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

<span data-ttu-id="abdeb-153">Se produce un error en un tooexecute intento por encima de la instrucción con hello siguiente error:</span><span class="sxs-lookup"><span data-stu-id="abdeb-153">An attempt tooexecute above statement fails with hello following error:</span></span>

<span data-ttu-id="abdeb-154">*Mens. 13772, Nivel 16, Estado 1 <br></br> No se puede crear un índice no agrupado en la tabla de historial temporal 'WebsiteUserInfoHistory' porque tiene definido un período de retención finito y un índice agrupado de almacén de columnas.*</span><span class="sxs-lookup"><span data-stu-id="abdeb-154">*Msg 13772, Level 16, State 1 <br></br> Cannot create non-clustered index on a temporal history table 'WebsiteUserInfoHistory' since it has finite retention period and clustered columnstore index defined.*</span></span>

## <a name="querying-tables-with-retention-policy"></a><span data-ttu-id="abdeb-155">Consulta de tablas con directiva de retención</span><span class="sxs-lookup"><span data-stu-id="abdeb-155">Querying tables with retention policy</span></span>
<span data-ttu-id="abdeb-156">Todas las consultas en una tabla temporal Hola filtran automáticamente históricas filas que coinciden con directiva de retención finito, tooavoid resultados impredecibles e incoherentes, ya que se pueden eliminar filas antiguos por la tarea de limpieza de hello, *en cualquier momento en el tiempo y en orden arbitrario*.</span><span class="sxs-lookup"><span data-stu-id="abdeb-156">All queries on hello temporal table automatically filter out historical rows matching finite retention policy, tooavoid unpredictable and inconsistent results, since aged rows can be deleted by hello cleanup task, *at any point in time and in arbitrary order*.</span></span>

<span data-ttu-id="abdeb-157">Hello siguiente imagen muestra hello plan de consulta para una consulta simple:</span><span class="sxs-lookup"><span data-stu-id="abdeb-157">hello following picture shows hello query plan for a simple query:</span></span>

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

<span data-ttu-id="abdeb-158">consulta de Hello plan incluye filtro adicional aplica tooend de columna de periodo (ValidTo) in Hola Clustered Index Scan (operador) en la tabla de historial de hello (resaltada).</span><span class="sxs-lookup"><span data-stu-id="abdeb-158">hello query plan includes additional filter applied tooend of period column (ValidTo) in hello Clustered Index Scan operator on hello history table (highlighted).</span></span> <span data-ttu-id="abdeb-159">En este ejemplo se supone que se ha establecido el período de retención de 1 MES en la tabla WebsiteUserInfo.</span><span class="sxs-lookup"><span data-stu-id="abdeb-159">This example assumes that one MONTH retention period was set on WebsiteUserInfo table.</span></span>

![Filtro de consulta de retención](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

<span data-ttu-id="abdeb-161">Sin embargo, si consulta la tabla de historial directamente, puede ver filas con una antigüedad mayor que el período de retención especificado, pero sin garantía de resultados de consulta repetibles.</span><span class="sxs-lookup"><span data-stu-id="abdeb-161">However, if you query history table directly, you may see rows that are older than specified retention period, but without any guarantee for repeatable query results.</span></span> <span data-ttu-id="abdeb-162">Hello siguiente imagen muestra plan de ejecución de consulta para consultas de hello en la tabla de historial de hello sin aplicar los filtros adicionales:</span><span class="sxs-lookup"><span data-stu-id="abdeb-162">hello following picture shows query execution plan for hello query on hello history table without additional filters applied:</span></span>

![Consulta del historial sin filtro de retención](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

<span data-ttu-id="abdeb-164">No se fíe de la lógica empresarial al leer la tabla de historial más allá del período de retención, ya que puede obtener resultados inesperados o incoherentes.</span><span class="sxs-lookup"><span data-stu-id="abdeb-164">Do not rely your business logic on reading history table beyond retention period as you may get inconsistent or unexpected results.</span></span> <span data-ttu-id="abdeb-165">Se recomienda usar consultas temporales con la cláusula FOR SYSTEM_TIME para analizar los datos de tablas temporales.</span><span class="sxs-lookup"><span data-stu-id="abdeb-165">We recommend that you use temporal queries with FOR SYSTEM_TIME clause for analyzing data in temporal tables.</span></span>

## <a name="point-in-time-restore-considerations"></a><span data-ttu-id="abdeb-166">Consideraciones sobre la restauración a un momento dado</span><span class="sxs-lookup"><span data-stu-id="abdeb-166">Point in time restore considerations</span></span>
<span data-ttu-id="abdeb-167">Cuando se crea la nueva base de datos por [restauración punto específico de tooa de base de datos existente en el tiempo](sql-database-recovery-using-backups.md), tiene retención temporal deshabilitada en el nivel de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="abdeb-167">When you create new database by [restoring existing database tooa specific point in time](sql-database-recovery-using-backups.md), it has temporal retention disabled at hello database level.</span></span> <span data-ttu-id="abdeb-168">(**is_temporal_history_retention_enabled** marca establece tooOFF).</span><span class="sxs-lookup"><span data-stu-id="abdeb-168">(**is_temporal_history_retention_enabled** flag set tooOFF).</span></span> <span data-ttu-id="abdeb-169">Esta funcionalidad le permite tooexamine todas las filas históricas durante la restauración, sin tener en cuenta que antiguos filas se quitan antes de obtener tooquery ellos.</span><span class="sxs-lookup"><span data-stu-id="abdeb-169">This functionality allows you tooexamine all historical rows upon restore, without worrying that aged rows are removed before you get tooquery them.</span></span> <span data-ttu-id="abdeb-170">Puede usar demasiado*inspeccionar los datos históricos más allá del período de retención configurado*.</span><span class="sxs-lookup"><span data-stu-id="abdeb-170">You can use it too*inspect historical data beyond configured retention period*.</span></span>

<span data-ttu-id="abdeb-171">Supongamos que una tabla temporal tiene especificado un período de retención de un MES.</span><span class="sxs-lookup"><span data-stu-id="abdeb-171">Say that a temporal table has one MONTH retention period specified.</span></span> <span data-ttu-id="abdeb-172">Si la base de datos se creó en el nivel de servicio Premium, sería toocreate capaz de copia de base de datos con el estado de base de datos de hello días laborables too35 en hello anterior.</span><span class="sxs-lookup"><span data-stu-id="abdeb-172">If your database was created in Premium Service tier, you would be able toocreate database copy with hello database state up too35 days back in hello past.</span></span> <span data-ttu-id="abdeb-173">Que eficazmente permitiría tooanalyze filas históricos que están funcionando too65 días de antigüedad consultando la tabla de historial de hello directamente.</span><span class="sxs-lookup"><span data-stu-id="abdeb-173">That effectively would allow you tooanalyze historical rows that are up too65 days old by querying hello history table directly.</span></span>

<span data-ttu-id="abdeb-174">Si desea que la limpieza de la retención temporal tooactivate, ejecute hello después de la instrucción de Transact-SQL después de punto de restauración a un momento dado:</span><span class="sxs-lookup"><span data-stu-id="abdeb-174">If you want tooactivate temporal retention cleanup, run hello following Transact-SQL statement after point in time restore:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a><span data-ttu-id="abdeb-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="abdeb-175">Next steps</span></span>
<span data-ttu-id="abdeb-176">cómo desproteger toouse las tablas temporales de las aplicaciones de toolearn [Introducción a las tablas temporales de base de datos de SQL Azure](sql-database-temporal-tables.md).</span><span class="sxs-lookup"><span data-stu-id="abdeb-176">toolearn how toouse Temporal Tables in your applications, check out [Getting Started with Temporal Tables in Azure SQL Database](sql-database-temporal-tables.md).</span></span>

<span data-ttu-id="abdeb-177">Visita Channel 9 toohear una [historia de éxito de clientes reales implementación temporal](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) inspección y un [live temporal demostración](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="abdeb-177">Visit Channel 9 toohear a [real customer temporal implementation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

<span data-ttu-id="abdeb-178">Para más información sobre las tablas temporales, revise la [documentación de MSDN](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="abdeb-178">For detailed information about Temporal Tables, review [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>

