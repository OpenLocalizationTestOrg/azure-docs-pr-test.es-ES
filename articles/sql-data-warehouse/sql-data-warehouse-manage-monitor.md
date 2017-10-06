---
title: aaaMonitor la carga de trabajo mediante DMV | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomonitor la carga de trabajo mediante DMV."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 69ecd479-0941-48df-b3d0-cf54c79e6549
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: acccf952d165ccec3de3b4b1c633b18bbbf78077
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-workload-using-dmvs"></a><span data-ttu-id="622e8-103">Supervisión de la carga de trabajo mediante DMV</span><span class="sxs-lookup"><span data-stu-id="622e8-103">Monitor your workload using DMVs</span></span>
<span data-ttu-id="622e8-104">Este artículo se describe cómo toouse vistas de administración dinámica (DMV) toomonitor la carga de trabajo e investigar la ejecución de la consulta en el almacén de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="622e8-104">This article describes how toouse Dynamic Management Views (DMVs) toomonitor your workload and investigate query execution in Azure SQL Data Warehouse.</span></span>

## <a name="permissions"></a><span data-ttu-id="622e8-105">Permisos</span><span class="sxs-lookup"><span data-stu-id="622e8-105">Permissions</span></span>
<span data-ttu-id="622e8-106">Hola tooquery DMV en este artículo, debe tener permiso VIEW DATABASE STATE o CONTROL.</span><span class="sxs-lookup"><span data-stu-id="622e8-106">tooquery hello DMVs in this article, you need either VIEW DATABASE STATE or CONTROL permission.</span></span> <span data-ttu-id="622e8-107">Normalmente la concesión VIEW DATABASE STATE es permiso Hola preferida ya que es mucho más restrictiva.</span><span class="sxs-lookup"><span data-stu-id="622e8-107">Usually granting VIEW DATABASE STATE is hello preferred permission as it is much more restrictive.</span></span>

```sql
GRANT VIEW DATABASE STATE toomyuser;
```

## <a name="monitor-connections"></a><span data-ttu-id="622e8-108">Supervisión de conexiones</span><span class="sxs-lookup"><span data-stu-id="622e8-108">Monitor connections</span></span>
<span data-ttu-id="622e8-109">Todos los inicios de sesión tooSQL almacenamiento de datos se registran demasiado[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span><span class="sxs-lookup"><span data-stu-id="622e8-109">All logins tooSQL Data Warehouse are logged too[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span></span>  <span data-ttu-id="622e8-110">Esta DMV contiene Hola última 10.000 inicios de sesión.</span><span class="sxs-lookup"><span data-stu-id="622e8-110">This DMV contains hello last 10,000 logins.</span></span>  <span data-ttu-id="622e8-111">Hola session_id es la clave principal de Hola y se asigna de forma secuencial para cada nuevo inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="622e8-111">hello session_id is hello primary key and is assigned sequentially for each new logon.</span></span>

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a><span data-ttu-id="622e8-112">Supervisión de ejecuciones de consultas</span><span class="sxs-lookup"><span data-stu-id="622e8-112">Monitor query execution</span></span>
<span data-ttu-id="622e8-113">Todas las consultas ejecutadas en almacenamiento de datos de SQL se registran demasiado[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span><span class="sxs-lookup"><span data-stu-id="622e8-113">All queries executed on SQL Data Warehouse are logged too[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span></span>  <span data-ttu-id="622e8-114">Esta DMV contiene Hola última 10.000 consultas ejecutadas.</span><span class="sxs-lookup"><span data-stu-id="622e8-114">This DMV contains hello last 10,000 queries executed.</span></span>  <span data-ttu-id="622e8-115">Hola request_id identifica cada consulta y es la clave principal de Hola para esta DMV.</span><span class="sxs-lookup"><span data-stu-id="622e8-115">hello request_id uniquely identifies each query and is hello primary key for this DMV.</span></span>  <span data-ttu-id="622e8-116">Hola request_id se asigna de forma secuencial para cada nueva consulta y tiene como prefijo QID, que representa el identificador de consulta.</span><span class="sxs-lookup"><span data-stu-id="622e8-116">hello request_id is assigned sequentially for each new query and is prefixed with QID, which stands for query ID.</span></span>  <span data-ttu-id="622e8-117">Al consultar en esta DMV sobre un campo session_id determinado, se muestran todas las consultas de un inicio de sesión concreto.</span><span class="sxs-lookup"><span data-stu-id="622e8-117">Querying this DMV for a given session_id shows all queries for a given logon.</span></span>

> [!NOTE]
> <span data-ttu-id="622e8-118">Los procedimientos almacenados utilizan varios identificadores de solicitud.</span><span class="sxs-lookup"><span data-stu-id="622e8-118">Stored procedures use multiple Request IDs.</span></span>  <span data-ttu-id="622e8-119">Los identificadores de solicitud se asignan en orden secuencial.</span><span class="sxs-lookup"><span data-stu-id="622e8-119">Request IDs are assigned in sequential order.</span></span> 
> 
> 

<span data-ttu-id="622e8-120">Estos son los planes de ejecución de pasos toofollow tooinvestigate de consultas y las horas para una consulta determinada.</span><span class="sxs-lookup"><span data-stu-id="622e8-120">Here are steps toofollow tooinvestigate query execution plans and times for a particular query.</span></span>

### <a name="step-1-identify-hello-query-you-wish-tooinvestigate"></a><span data-ttu-id="622e8-121">PASO 1: Identificar consulta Hola que desea tooinvestigate</span><span class="sxs-lookup"><span data-stu-id="622e8-121">STEP 1: Identify hello query you wish tooinvestigate</span></span>
```sql
-- Monitor active queries
SELECT * 
FROM sys.dm_pdw_exec_requests 
WHERE status not in ('Completed','Failed','Cancelled')
  AND session_id <> session_id()
ORDER BY submit_time DESC;

-- Find top 10 queries longest running queries
SELECT TOP 10 * 
FROM sys.dm_pdw_exec_requests 
ORDER BY total_elapsed_time DESC;

-- Find a query with hello Label 'My Query'
-- Use brackets when querying hello label column, as it it a key word
SELECT  *
FROM    sys.dm_pdw_exec_requests
WHERE   [label] = 'My Query';
```

<span data-ttu-id="622e8-122">De hello anteriores resultados de la consulta, **Hola Nota Id. de solicitud** de consulta de Hola que desearía tooinvestigate.</span><span class="sxs-lookup"><span data-stu-id="622e8-122">From hello preceding query results, **note hello Request ID** of hello query that you would like tooinvestigate.</span></span>

<span data-ttu-id="622e8-123">Las consultas de hello **Suspended** estado se ponen en cola debido a límites de tooconcurrency.</span><span class="sxs-lookup"><span data-stu-id="622e8-123">Queries in hello **Suspended** state are being queued due tooconcurrency limits.</span></span> <span data-ttu-id="622e8-124">Estas consultas también aparecen en la consulta de las esperas de hello sys.dm_pdw_waits con un tipo de UserConcurrencyResourceType.</span><span class="sxs-lookup"><span data-stu-id="622e8-124">These queries also appear in hello sys.dm_pdw_waits waits query with a type of UserConcurrencyResourceType.</span></span> <span data-ttu-id="622e8-125">Para más información acerca de los límites de simultaneidad, consulte [Simultaneidad y administración de cargas de trabajo en SQL Data Warehouse][Concurrency and workload management].</span><span class="sxs-lookup"><span data-stu-id="622e8-125">See [Concurrency and workload management][Concurrency and workload management] for more details on concurrency limits.</span></span> <span data-ttu-id="622e8-126">Las consultas también pueden esperar por otros motivos, como los bloqueos de objetos.</span><span class="sxs-lookup"><span data-stu-id="622e8-126">Queries can also wait for other reasons such as for object locks.</span></span>  <span data-ttu-id="622e8-127">Si la consulta está esperando un recurso, consulte la sección [Supervisión de consultas en espera][Investigating queries waiting for resources] de este mismo artículo.</span><span class="sxs-lookup"><span data-stu-id="622e8-127">If your query is waiting for a resource, see [Investigating queries waiting for resources][Investigating queries waiting for resources] further down in this article.</span></span>

<span data-ttu-id="622e8-128">búsqueda de hello toosimplify de una consulta en la tabla de sys.dm_pdw_exec_requests hello, utilice [etiqueta] [ LABEL] tooassign una consulta de tooyour de comentario que se puede buscar en la vista de sys.dm_pdw_exec_requests Hola.</span><span class="sxs-lookup"><span data-stu-id="622e8-128">toosimplify hello lookup of a query in hello sys.dm_pdw_exec_requests table, use [LABEL][LABEL] tooassign a comment tooyour query that can be looked up in hello sys.dm_pdw_exec_requests view.</span></span>

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-hello-query-plan"></a><span data-ttu-id="622e8-129">PASO 2: Investigar el plan de consulta de Hola</span><span class="sxs-lookup"><span data-stu-id="622e8-129">STEP 2: Investigate hello query plan</span></span>
<span data-ttu-id="622e8-130">Use plan de hello Id. de solicitud tooretrieve hello de la consulta distribuida SQL (DSQL) desde [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span><span class="sxs-lookup"><span data-stu-id="622e8-130">Use hello Request ID tooretrieve hello query's distributed SQL (DSQL) plan from [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span></span>

```sql
-- Find hello distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

<span data-ttu-id="622e8-131">Cuando un plan DSQL está tardando más de lo esperado, causa de hello puede ser un plan de complejo con muchos pasos DSQL o solamente un paso tarda mucho tiempo.</span><span class="sxs-lookup"><span data-stu-id="622e8-131">When a DSQL plan is taking longer than expected, hello cause can be a complex plan with many DSQL steps or just one step taking a long time.</span></span>  <span data-ttu-id="622e8-132">Si plan de hello muchos pasos con varias operaciones de movimiento, considere la posibilidad de optimizar el movimiento de datos de tabla distribuciones tooreduce.</span><span class="sxs-lookup"><span data-stu-id="622e8-132">If hello plan is many steps with several move operations, consider optimizing your table distributions tooreduce data movement.</span></span> <span data-ttu-id="622e8-133">Hola [tabla distribución] [ Table distribution] artículo explica por qué datos deben ser una consulta de toosolve movida y explican algunos movimiento de datos de distribución estrategias toominimize.</span><span class="sxs-lookup"><span data-stu-id="622e8-133">hello [Table distribution][Table distribution] article explains why data must be moved toosolve a query and explains some distribution strategies toominimize data movement.</span></span>

<span data-ttu-id="622e8-134">tooinvestigate obtener más información acerca de un solo paso, hello *operation_type* columna de Hola Hola de paso y tenga en cuenta de consulta de ejecución prolongada **índice paso**:</span><span class="sxs-lookup"><span data-stu-id="622e8-134">tooinvestigate further details about a single step, hello *operation_type* column of hello long-running query step and note hello **Step Index**:</span></span>

* <span data-ttu-id="622e8-135">Continúe con el paso 3a sobre **operaciones SQL**: OnOperation, RemoteOperation, ReturnOperation.</span><span class="sxs-lookup"><span data-stu-id="622e8-135">Proceed with Step 3a for **SQL operations**: OnOperation, RemoteOperation, ReturnOperation.</span></span>
* <span data-ttu-id="622e8-136">Continúe con el paso 3b sobre **operaciones de movimiento de datos**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span><span class="sxs-lookup"><span data-stu-id="622e8-136">Proceed with Step 3b for **Data Movement operations**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span></span>

### <a name="step-3a-investigate-sql-on-hello-distributed-databases"></a><span data-ttu-id="622e8-137">PASO 3a: investigar SQL en bases de datos de hello distribuida</span><span class="sxs-lookup"><span data-stu-id="622e8-137">STEP 3a: Investigate SQL on hello distributed databases</span></span>
<span data-ttu-id="622e8-138">Usar Hola Id. de solicitud y detalles de tooretrieve del índice de paso de Hola de [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], que contiene información de ejecución de paso de consulta de hello en todos los de hello distribuidas bases de datos.</span><span class="sxs-lookup"><span data-stu-id="622e8-138">Use hello Request ID and hello Step Index tooretrieve details from [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], which contains execution information of hello query step on all of hello distributed databases.</span></span>

```sql
-- Find hello distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

<span data-ttu-id="622e8-139">Cuando se ejecuta el paso de consulta de hello, [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] puede ser usado tooretrieve Hola estimado plan para SQL Server de hello memoria caché del plan de SQL Server para el paso de hello ejecutando en un determinado distribución.</span><span class="sxs-lookup"><span data-stu-id="622e8-139">When hello query step is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used tooretrieve hello SQL Server estimated plan from hello SQL Server plan cache for hello step running on a particular distribution.</span></span>

```sql
-- Find hello SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-hello-distributed-databases"></a><span data-ttu-id="622e8-140">PASO 3b: investigar el movimiento de datos en las bases de datos de hello distribuida</span><span class="sxs-lookup"><span data-stu-id="622e8-140">STEP 3b: Investigate data movement on hello distributed databases</span></span>
<span data-ttu-id="622e8-141">Usar Id. de solicitud de Hola y Hola información de índice de paso tooretrieve acerca de un paso de movimiento de datos con cada distribución de [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span><span class="sxs-lookup"><span data-stu-id="622e8-141">Use hello Request ID and hello Step Index tooretrieve information about a data movement step running on each distribution from [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span></span>

```sql
-- Find hello information about all hello workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* <span data-ttu-id="622e8-142">Comprobar hello *total_elapsed_time* toosee de columna si una distribución particular está tardando mucho más tiempo que otras personas para que el movimiento de datos.</span><span class="sxs-lookup"><span data-stu-id="622e8-142">Check hello *total_elapsed_time* column toosee if a particular distribution is taking significantly longer than others for data movement.</span></span>
* <span data-ttu-id="622e8-143">Para la distribución de ejecución prolongada de hello, comprobar hello *rows_processed* toosee de columna si el número de Hola de filas que se mueven de distribución es significativamente mayor que otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="622e8-143">For hello long-running distribution, check hello *rows_processed* column toosee if hello number of rows being moved from that distribution is significantly larger than others.</span></span> <span data-ttu-id="622e8-144">En ese caso, esto puede indicar un sesgo de los datos subyacentes.</span><span class="sxs-lookup"><span data-stu-id="622e8-144">If so, this may indicate skew of your underlying data.</span></span>

<span data-ttu-id="622e8-145">Si está ejecutando la consulta de hello, [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] puede ser usado tooretrieve Hola estimado plan para SQL Server de hello memoria caché del plan de SQL Server para hello actuales paso SQL dentro de un determinado distribución.</span><span class="sxs-lookup"><span data-stu-id="622e8-145">If hello query is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used tooretrieve hello SQL Server estimated plan from hello SQL Server plan cache for hello currently running SQL Step within a particular distribution.</span></span>

```sql
-- Find hello SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a><span data-ttu-id="622e8-146">Supervisión de consultas en espera</span><span class="sxs-lookup"><span data-stu-id="622e8-146">Monitor waiting queries</span></span>
<span data-ttu-id="622e8-147">Si descubre que la consulta no está realizando progresos porque está esperando un recurso, esta es una consulta que muestra todos los recursos de hello que está esperando una consulta.</span><span class="sxs-lookup"><span data-stu-id="622e8-147">If you discover that your query is not making progress because it is waiting for a resource, here is a query that shows all hello resources a query is waiting for.</span></span>

```sql
-- Find queries 
-- Replace request_id with value from Step 1.

SELECT waits.session_id,
      waits.request_id,  
      requests.command,
      requests.status,
      requests.start_time,  
      waits.type,
      waits.state,
      waits.object_type,
      waits.object_name
FROM   sys.dm_pdw_waits waits
   JOIN  sys.dm_pdw_exec_requests requests
   ON waits.request_id=requests.request_id
WHERE waits.request_id = 'QID####'
ORDER BY waits.object_name, waits.object_type, waits.state;
```

<span data-ttu-id="622e8-148">Si consulta Hola activamente está esperando en recursos de otra consulta, estado de hello será **AcquireResources**.</span><span class="sxs-lookup"><span data-stu-id="622e8-148">If hello query is actively waiting on resources from another query, then hello state will be **AcquireResources**.</span></span>  <span data-ttu-id="622e8-149">Si consulta hello tiene todos los recursos necesario de hello, Hola estado será **Granted**.</span><span class="sxs-lookup"><span data-stu-id="622e8-149">If hello query has all hello required resources, then hello state will be **Granted**.</span></span>

## <a name="monitor-tempdb"></a><span data-ttu-id="622e8-150">Supervisión de tempdb</span><span class="sxs-lookup"><span data-stu-id="622e8-150">Monitor tempdb</span></span>
<span data-ttu-id="622e8-151">Uso de tempdb alta puede ser Hola causa de un rendimiento lento y problemas de memoria insuficiente.</span><span class="sxs-lookup"><span data-stu-id="622e8-151">High tempdb utilization can be hello root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="622e8-152">Por favor, compruebe primero si tiene grupos de filas de sesgo o de mala calidad de datos y tome las medidas oportunas Hola.</span><span class="sxs-lookup"><span data-stu-id="622e8-152">Please first check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="622e8-153">Si observa que tempdb llega a su limite durante la ejecución de consultas, considere la posibilidad de escalar el almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="622e8-153">Consider scaling your data warehouse if you find tempdb reaching its limits during query execution.</span></span> <span data-ttu-id="622e8-154">Hola a continuación se describe cómo tooidentify al uso de tempdb por cada consulta en cada nodo.</span><span class="sxs-lookup"><span data-stu-id="622e8-154">hello following describes how tooidentify tempdb usage per query on each node.</span></span> 

<span data-ttu-id="622e8-155">Crear Hola siguiente Id. de hello nodo apropiado tooassociate de vista para sys.dm_pdw_sql_requests.</span><span class="sxs-lookup"><span data-stu-id="622e8-155">Create hello following view tooassociate hello appropriate node id for sys.dm_pdw_sql_requests.</span></span> <span data-ttu-id="622e8-156">Esto habilitará tooleverage otras DMV acceso directo y combinar las tablas con sys.dm_pdw_sql_requests.</span><span class="sxs-lookup"><span data-stu-id="622e8-156">This will enable you tooleverage other pass-through DMVs and join those tables with sys.dm_pdw_sql_requests.</span></span>

```sql
-- sys.dm_pdw_sql_requests with hello correct node id
CREATE VIEW sql_requests AS
(SELECT
       sr.request_id,
       sr.step_index,
       (CASE 
              WHEN (sr.distribution_id = -1 ) THEN 
              (SELECT pdw_node_id FROM sys.dm_pdw_nodes WHERE type = 'CONTROL') 
              ELSE d.pdw_node_id END) AS pdw_node_id,
       sr.distribution_id,
       sr.status,
       sr.error_id,
       sr.start_time,
       sr.end_time,
       sr.total_elapsed_time,
       sr.row_count,
       sr.spid,
       sr.command
FROM sys.pdw_distributions AS d
RIGHT JOIN sys.dm_pdw_sql_requests AS sr ON d.distribution_id = sr.distribution_id)
```
<span data-ttu-id="622e8-157">Ejecute hello después consulta toomonitor tempdb:</span><span class="sxs-lookup"><span data-stu-id="622e8-157">Run hello following query toomonitor tempdb:</span></span>

```sql
-- Monitor tempdb
SELECT
    sr.request_id,
    ssu.session_id,
    ssu.pdw_node_id,
    sr.command,
    sr.total_elapsed_time,
    es.login_name AS 'LoginName',
    DB_NAME(ssu.database_id) AS 'DatabaseName',
    (es.memory_usage * 8) AS 'MemoryUsage (in KB)',
    (ssu.user_objects_alloc_page_count * 8) AS 'Space Allocated For User Objects (in KB)',
    (ssu.user_objects_dealloc_page_count * 8) AS 'Space Deallocated For User Objects (in KB)',
    (ssu.internal_objects_alloc_page_count * 8) AS 'Space Allocated For Internal Objects (in KB)',
    (ssu.internal_objects_dealloc_page_count * 8) AS 'Space Deallocated For Internal Objects (in KB)',
    CASE es.is_user_process
    WHEN 1 THEN 'User Session'
    WHEN 0 THEN 'System Session'
    END AS 'SessionType',
    es.row_count AS 'RowCount'
FROM sys.dm_pdw_nodes_db_session_space_usage AS ssu
    INNER JOIN sys.dm_pdw_nodes_exec_sessions AS es ON ssu.session_id = es.session_id AND ssu.pdw_node_id = es.pdw_node_id
    INNER JOIN sys.dm_pdw_nodes_exec_connections AS er ON ssu.session_id = er.session_id AND ssu.pdw_node_id = er.pdw_node_id
    INNER JOIN sql_requests AS sr ON ssu.session_id = sr.spid AND ssu.pdw_node_id = sr.pdw_node_id
WHERE DB_NAME(ssu.database_id) = 'tempdb'
    AND es.session_id <> @@SPID
    AND es.login_name <> 'sa' 
ORDER BY sr.request_id;
```
## <a name="monitor-memory"></a><span data-ttu-id="622e8-158">Supervisión de memoria</span><span class="sxs-lookup"><span data-stu-id="622e8-158">Monitor memory</span></span>

<span data-ttu-id="622e8-159">Memoria puede ser la causa de Hola para un rendimiento lento y problemas de memoria insuficiente.</span><span class="sxs-lookup"><span data-stu-id="622e8-159">Memory can be hello root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="622e8-160">Por favor, compruebe primero si tiene grupos de filas de sesgo o de mala calidad de datos y tome las medidas oportunas Hola.</span><span class="sxs-lookup"><span data-stu-id="622e8-160">Please first check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="622e8-161">Si observa que el uso de memoria de SQL Server llega a su limite durante la ejecución de consultas, considere la posibilidad de escalar el almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="622e8-161">Consider scaling your data warehouse if you find SQL Server memory usage reaching its limits during query execution.</span></span>

<span data-ttu-id="622e8-162">Hola después de consulta devuelve presión de memoria y uso de memoria de SQL Server por nodo:</span><span class="sxs-lookup"><span data-stu-id="622e8-162">hello following query returns SQL Server memory usage and memory pressure per node:</span></span> 
```sql
-- Memory consumption
SELECT
  pc1.cntr_value as Curr_Mem_KB, 
  pc1.cntr_value/1024.0 as Curr_Mem_MB,
  (pc1.cntr_value/1048576.0) as Curr_Mem_GB,
  pc2.cntr_value as Max_Mem_KB,
  pc2.cntr_value/1024.0 as Max_Mem_MB,
  (pc2.cntr_value/1048576.0) as Max_Mem_GB,
  pc1.cntr_value * 100.0/pc2.cntr_value AS Memory_Utilization_Percentage,
  pc1.pdw_node_id
FROM
-- pc1: current memory
sys.dm_pdw_nodes_os_performance_counters AS pc1
-- pc2: total memory allowed for this SQL instance
JOIN sys.dm_pdw_nodes_os_performance_counters AS pc2 
ON pc1.object_name = pc2.object_name AND pc1.pdw_node_id = pc2.pdw_node_id
WHERE
pc1.counter_name = 'Total Server Memory (KB)'
AND pc2.counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-size"></a><span data-ttu-id="622e8-163">Supervisión del tamaño del registro de transacciones</span><span class="sxs-lookup"><span data-stu-id="622e8-163">Monitor transaction log size</span></span>
<span data-ttu-id="622e8-164">Hello consulta siguiente devuelve tamaño del registro de transacciones de hello en cada tipo de distribución.</span><span class="sxs-lookup"><span data-stu-id="622e8-164">hello following query returns hello transaction log size on each distribution.</span></span> <span data-ttu-id="622e8-165">Compruebe si tiene grupos de filas de sesgo o de mala calidad de datos y tome las medidas oportunas Hola.</span><span class="sxs-lookup"><span data-stu-id="622e8-165">Please check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="622e8-166">Si uno de los archivos de registro de hello está llegando a 160GB, debería considerar el escalado de la instancia o limitar el tamaño de la transacción.</span><span class="sxs-lookup"><span data-stu-id="622e8-166">If one of hello log files is reaching 160GB, you should consider scaling up your instance or limiting your transaction size.</span></span> 
```sql
-- Transaction log size
SELECT
  instance_name as distribution_db,
  cntr_value*1.0/1048576 as log_file_size_used_GB,
  pdw_node_id 
FROM sys.dm_pdw_nodes_os_performance_counters 
WHERE 
instance_name like 'Distribution_%' 
AND counter_name = 'Log File(s) Used Size (KB)'
AND counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-rollback"></a><span data-ttu-id="622e8-167">Supervisión de la reversión del registro de transacciones</span><span class="sxs-lookup"><span data-stu-id="622e8-167">Monitor transaction log rollback</span></span>
<span data-ttu-id="622e8-168">Si se producen errores en las consultas o llevar a cabo una tooproceed mucho tiempo, puede comprobar y supervisar si dispone de las transacciones de reversión.</span><span class="sxs-lookup"><span data-stu-id="622e8-168">If your queries are failing or taking a long time tooproceed, you can check and monitor if you have any transactions rolling back.</span></span>
```sql
-- Monitor rollback
SELECT 
    SUM(CASE WHEN t.database_transaction_next_undo_lsn IS NOT NULL THEN 1 ELSE 0 END),
    t.pdw_node_id,
    nod.[type]
FROM sys.dm_pdw_nodes_tran_database_transactions t
JOIN sys.dm_pdw_nodes nod ON t.pdw_node_id = nod.pdw_node_id
GROUP BY t.pdw_node_id, nod.[type]
```

## <a name="next-steps"></a><span data-ttu-id="622e8-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="622e8-169">Next steps</span></span>
<span data-ttu-id="622e8-170">Para más información acerca de las DMV, consulte [Vistas del sistema][System views].</span><span class="sxs-lookup"><span data-stu-id="622e8-170">See [System views][System views] for more information on DMVs.</span></span>
<span data-ttu-id="622e8-171">Para más información acerca de los procedimientos recomendados, consulte [Procedimientos recomendados para SQL Data Warehouse][SQL Data Warehouse best practices]</span><span class="sxs-lookup"><span data-stu-id="622e8-171">See [SQL Data Warehouse best practices][SQL Data Warehouse best practices] for more information about best practices</span></span>

<!--Image references-->

<!--Article references-->
[Manage overview]: ./sql-data-warehouse-overview-manage.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[System views]: ./sql-data-warehouse-reference-tsql-system-views.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Concurrency and workload management]: ./sql-data-warehouse-develop-concurrency.md
[Investigating queries waiting for resources]: ./sql-data-warehouse-manage-monitor.md#waiting

<!--MSDN references-->
[sys.dm_pdw_dms_workers]: http://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_exec_requests]: http://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_exec_sessions]: http://msdn.microsoft.com/library/mt203883.aspx
[sys.dm_pdw_request_steps]: http://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: http://msdn.microsoft.com/library/mt203889.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: http://msdn.microsoft.com/library/mt204017.aspx
[DBCC PDW_SHOWSPACEUSED]: http://msdn.microsoft.com/library/mt204028.aspx
[LABEL]: https://msdn.microsoft.com/library/ms190322.aspx
