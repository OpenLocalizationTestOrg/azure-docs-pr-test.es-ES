---
title: "Supervisión de la carga de trabajo mediante DMV | Microsoft Docs"
description: "Obtenga información sobre cómo supervisar la carga de trabajo mediante DMV."
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
ms.openlocfilehash: 7ce6c2cdf1e28852da536414533ccdcdaeb437e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-your-workload-using-dmvs"></a><span data-ttu-id="e37a3-103">Supervisión de la carga de trabajo mediante DMV</span><span class="sxs-lookup"><span data-stu-id="e37a3-103">Monitor your workload using DMVs</span></span>
<span data-ttu-id="e37a3-104">En este artículo se describe cómo usar las vistas de administración dinámica (DMV) para supervisar la carga de trabajo e investigar la ejecución de la consulta en Almacenamiento de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="e37a3-104">This article describes how to use Dynamic Management Views (DMVs) to monitor your workload and investigate query execution in Azure SQL Data Warehouse.</span></span>

## <a name="permissions"></a><span data-ttu-id="e37a3-105">Permisos</span><span class="sxs-lookup"><span data-stu-id="e37a3-105">Permissions</span></span>
<span data-ttu-id="e37a3-106">Para consultar las DMV de este artículo, necesita el permiso VER ESTADO DE BASE DE DATOS o CONTROL.</span><span class="sxs-lookup"><span data-stu-id="e37a3-106">To query the DMVs in this article, you need either VIEW DATABASE STATE or CONTROL permission.</span></span> <span data-ttu-id="e37a3-107">Normalmente la concesión VER ESTADO DE BASE DE DATOS es el permiso preferido ya que es mucho más restrictivo.</span><span class="sxs-lookup"><span data-stu-id="e37a3-107">Usually granting VIEW DATABASE STATE is the preferred permission as it is much more restrictive.</span></span>

```sql
GRANT VIEW DATABASE STATE TO myuser;
```

## <a name="monitor-connections"></a><span data-ttu-id="e37a3-108">Supervisión de conexiones</span><span class="sxs-lookup"><span data-stu-id="e37a3-108">Monitor connections</span></span>
<span data-ttu-id="e37a3-109">Todos los inicios de sesión en SQL Data Warehouse se registran en [sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span><span class="sxs-lookup"><span data-stu-id="e37a3-109">All logins to SQL Data Warehouse are logged to [sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span></span>  <span data-ttu-id="e37a3-110">Esta DMV contiene los 10.000 últimos inicios de sesión.</span><span class="sxs-lookup"><span data-stu-id="e37a3-110">This DMV contains the last 10,000 logins.</span></span>  <span data-ttu-id="e37a3-111">El campo session_id es la clave principal y se asigna de forma secuencial para cada nuevo inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="e37a3-111">The session_id is the primary key and is assigned sequentially for each new logon.</span></span>

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a><span data-ttu-id="e37a3-112">Supervisión de ejecuciones de consultas</span><span class="sxs-lookup"><span data-stu-id="e37a3-112">Monitor query execution</span></span>
<span data-ttu-id="e37a3-113">Todas las consultas ejecutadas en SQL Data Warehouse se registran en [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span><span class="sxs-lookup"><span data-stu-id="e37a3-113">All queries executed on SQL Data Warehouse are logged to [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span></span>  <span data-ttu-id="e37a3-114">Esta DMV contiene las últimas 10.000 consultas ejecutadas.</span><span class="sxs-lookup"><span data-stu-id="e37a3-114">This DMV contains the last 10,000 queries executed.</span></span>  <span data-ttu-id="e37a3-115">El campo request_id identifica cada consulta de forma única y es la clave principal de esta DMV.</span><span class="sxs-lookup"><span data-stu-id="e37a3-115">The request_id uniquely identifies each query and is the primary key for this DMV.</span></span>  <span data-ttu-id="e37a3-116">Este campo se asigna de forma secuencial para cada nueva consulta y lleva el prefijo QID, que representa el identificador de consulta.</span><span class="sxs-lookup"><span data-stu-id="e37a3-116">The request_id is assigned sequentially for each new query and is prefixed with QID, which stands for query ID.</span></span>  <span data-ttu-id="e37a3-117">Al consultar en esta DMV sobre un campo session_id determinado, se muestran todas las consultas de un inicio de sesión concreto.</span><span class="sxs-lookup"><span data-stu-id="e37a3-117">Querying this DMV for a given session_id shows all queries for a given logon.</span></span>

> [!NOTE]
> <span data-ttu-id="e37a3-118">Los procedimientos almacenados utilizan varios identificadores de solicitud.</span><span class="sxs-lookup"><span data-stu-id="e37a3-118">Stored procedures use multiple Request IDs.</span></span>  <span data-ttu-id="e37a3-119">Los identificadores de solicitud se asignan en orden secuencial.</span><span class="sxs-lookup"><span data-stu-id="e37a3-119">Request IDs are assigned in sequential order.</span></span> 
> 
> 

<span data-ttu-id="e37a3-120">Estos son los pasos que deben seguirse para investigar los planes de ejecución de consultas y las horas de una consulta determinada.</span><span class="sxs-lookup"><span data-stu-id="e37a3-120">Here are steps to follow to investigate query execution plans and times for a particular query.</span></span>

### <a name="step-1-identify-the-query-you-wish-to-investigate"></a><span data-ttu-id="e37a3-121">PASO 1: Identificación de la consulta que quiere investigar</span><span class="sxs-lookup"><span data-stu-id="e37a3-121">STEP 1: Identify the query you wish to investigate</span></span>
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

-- Find a query with the Label 'My Query'
-- Use brackets when querying the label column, as it it a key word
SELECT  *
FROM    sys.dm_pdw_exec_requests
WHERE   [label] = 'My Query';
```

<span data-ttu-id="e37a3-122">En los resultados de la consulta anterior, **fíjese en el id. de solicitud** de la consulta que quiere investigar.</span><span class="sxs-lookup"><span data-stu-id="e37a3-122">From the preceding query results, **note the Request ID** of the query that you would like to investigate.</span></span>

<span data-ttu-id="e37a3-123">Las consultas con estado **suspendido** se ponen en cola debido a los límites de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="e37a3-123">Queries in the **Suspended** state are being queued due to concurrency limits.</span></span> <span data-ttu-id="e37a3-124">Estas consultas también aparecen en la consulta sys.dm_pdw_waits con un tipo de UserConcurrencyResourceType.</span><span class="sxs-lookup"><span data-stu-id="e37a3-124">These queries also appear in the sys.dm_pdw_waits waits query with a type of UserConcurrencyResourceType.</span></span> <span data-ttu-id="e37a3-125">Para más información acerca de los límites de simultaneidad, consulte [Simultaneidad y administración de cargas de trabajo en SQL Data Warehouse][Concurrency and workload management].</span><span class="sxs-lookup"><span data-stu-id="e37a3-125">See [Concurrency and workload management][Concurrency and workload management] for more details on concurrency limits.</span></span> <span data-ttu-id="e37a3-126">Las consultas también pueden esperar por otros motivos, como los bloqueos de objetos.</span><span class="sxs-lookup"><span data-stu-id="e37a3-126">Queries can also wait for other reasons such as for object locks.</span></span>  <span data-ttu-id="e37a3-127">Si la consulta está esperando un recurso, consulte la sección [Supervisión de consultas en espera][Investigating queries waiting for resources] de este mismo artículo.</span><span class="sxs-lookup"><span data-stu-id="e37a3-127">If your query is waiting for a resource, see [Investigating queries waiting for resources][Investigating queries waiting for resources] further down in this article.</span></span>

<span data-ttu-id="e37a3-128">Para simplificar la búsqueda de una consulta en la tabla sys.dm_pdw_exec_requests, use [LABEL][LABEL] para asignar un comentario a la consulta que se pueda buscar en la vista sys.dm_pdw_exec_requests.</span><span class="sxs-lookup"><span data-stu-id="e37a3-128">To simplify the lookup of a query in the sys.dm_pdw_exec_requests table, use [LABEL][LABEL] to assign a comment to your query that can be looked up in the sys.dm_pdw_exec_requests view.</span></span>

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-the-query-plan"></a><span data-ttu-id="e37a3-129">PASO 2: investigación del plan de consulta</span><span class="sxs-lookup"><span data-stu-id="e37a3-129">STEP 2: Investigate the query plan</span></span>
<span data-ttu-id="e37a3-130">Use el identificador de la solicitud para recuperar el plan de SQL distribuido (DSQL) de la consulta desde [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span><span class="sxs-lookup"><span data-stu-id="e37a3-130">Use the Request ID to retrieve the query's distributed SQL (DSQL) plan from [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span></span>

```sql
-- Find the distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

<span data-ttu-id="e37a3-131">Si un plan DSQL tarda más de lo esperado, es posible que sea un plan complejo con muchos pasos DSQL o con un solo paso que tarda mucho tiempo.</span><span class="sxs-lookup"><span data-stu-id="e37a3-131">When a DSQL plan is taking longer than expected, the cause can be a complex plan with many DSQL steps or just one step taking a long time.</span></span>  <span data-ttu-id="e37a3-132">Si el plan tiene muchos pasos con varias operaciones de movimiento, considere la posibilidad de optimizar las distribuciones de la tabla para reducir el movimiento de datos.</span><span class="sxs-lookup"><span data-stu-id="e37a3-132">If the plan is many steps with several move operations, consider optimizing your table distributions to reduce data movement.</span></span> <span data-ttu-id="e37a3-133">El artículo [Distribución de tablas en SQL Data Warehouse][Table distribution] explica por qué deben moverse datos para resolver una consulta y explica algunas estrategias de distribución para minimizar el movimiento de datos.</span><span class="sxs-lookup"><span data-stu-id="e37a3-133">The [Table distribution][Table distribution] article explains why data must be moved to solve a query and explains some distribution strategies to minimize data movement.</span></span>

<span data-ttu-id="e37a3-134">Para investigar más detalles acerca de un solo paso, compruebe la columna *operation_type* del paso de consulta de larga ejecución y anote el valor de **Índice de pasos**:</span><span class="sxs-lookup"><span data-stu-id="e37a3-134">To investigate further details about a single step, the *operation_type* column of the long-running query step and note the **Step Index**:</span></span>

* <span data-ttu-id="e37a3-135">Continúe con el paso 3a sobre **operaciones SQL**: OnOperation, RemoteOperation, ReturnOperation.</span><span class="sxs-lookup"><span data-stu-id="e37a3-135">Proceed with Step 3a for **SQL operations**: OnOperation, RemoteOperation, ReturnOperation.</span></span>
* <span data-ttu-id="e37a3-136">Continúe con el paso 3b sobre **operaciones de movimiento de datos**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span><span class="sxs-lookup"><span data-stu-id="e37a3-136">Proceed with Step 3b for **Data Movement operations**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span></span>

### <a name="step-3a-investigate-sql-on-the-distributed-databases"></a><span data-ttu-id="e37a3-137">PASO 3a: investigación de SQL en las bases de datos distribuidas</span><span class="sxs-lookup"><span data-stu-id="e37a3-137">STEP 3a: Investigate SQL on the distributed databases</span></span>
<span data-ttu-id="e37a3-138">Use el identificador de la solicitud y el índice de pasos para recuperar información de [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], que contiene detalles sobre la ejecución del paso de la consulta en todas las instancias distribuidas.</span><span class="sxs-lookup"><span data-stu-id="e37a3-138">Use the Request ID and the Step Index to retrieve details from [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], which contains execution information of the query step on all of the distributed databases.</span></span>

```sql
-- Find the distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

<span data-ttu-id="e37a3-139">Si dicho paso se está ejecutando, se puede utilizar [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] para recuperar el plan estimado de SQL Server de la caché de planes de SQL Server para el paso que se ejecuta en una distribución concreta.</span><span class="sxs-lookup"><span data-stu-id="e37a3-139">When the query step is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used to retrieve the SQL Server estimated plan from the SQL Server plan cache for the step running on a particular distribution.</span></span>

```sql
-- Find the SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-the-distributed-databases"></a><span data-ttu-id="e37a3-140">PASO 3b: investigación del movimiento de datos en las bases de datos distribuidas</span><span class="sxs-lookup"><span data-stu-id="e37a3-140">STEP 3b: Investigate data movement on the distributed databases</span></span>
<span data-ttu-id="e37a3-141">Use el identificador de la solicitud y el índice de paso para recuperar información acerca del paso de movimiento de datos que se ejecuta en cada distribución desde [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span><span class="sxs-lookup"><span data-stu-id="e37a3-141">Use the Request ID and the Step Index to retrieve information about a data movement step running on each distribution from [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span></span>

```sql
-- Find the information about all the workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* <span data-ttu-id="e37a3-142">Compruebe la columna *total_elapsed_time* para ver si una distribución determinada tarda bastante más que otras en el movimiento de datos.</span><span class="sxs-lookup"><span data-stu-id="e37a3-142">Check the *total_elapsed_time* column to see if a particular distribution is taking significantly longer than others for data movement.</span></span>
* <span data-ttu-id="e37a3-143">Para la distribución de larga ejecución, compruebe la columna *rows_processed* para ver si el número de filas que se mueven desde esa distribución es mucho mayor que para las demás.</span><span class="sxs-lookup"><span data-stu-id="e37a3-143">For the long-running distribution, check the *rows_processed* column to see if the number of rows being moved from that distribution is significantly larger than others.</span></span> <span data-ttu-id="e37a3-144">En ese caso, esto puede indicar un sesgo de los datos subyacentes.</span><span class="sxs-lookup"><span data-stu-id="e37a3-144">If so, this may indicate skew of your underlying data.</span></span>

<span data-ttu-id="e37a3-145">Si la consulta se está ejecutando, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] se puede utilizar para recuperar el plan estimado de SQL Server de la caché de planes de SQL Server para el paso de SQL que se está ejecutando en una distribución particular.</span><span class="sxs-lookup"><span data-stu-id="e37a3-145">If the query is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used to retrieve the SQL Server estimated plan from the SQL Server plan cache for the currently running SQL Step within a particular distribution.</span></span>

```sql
-- Find the SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a><span data-ttu-id="e37a3-146">Supervisión de consultas en espera</span><span class="sxs-lookup"><span data-stu-id="e37a3-146">Monitor waiting queries</span></span>
<span data-ttu-id="e37a3-147">Si observa que la consulta no avanza porque está esperando un recurso, a continuación puede encontrar una consulta que muestra todos los recursos que está esperando una consulta.</span><span class="sxs-lookup"><span data-stu-id="e37a3-147">If you discover that your query is not making progress because it is waiting for a resource, here is a query that shows all the resources a query is waiting for.</span></span>

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

<span data-ttu-id="e37a3-148">Si la consulta espera activamente recursos de otra consulta, el estado será **AcquireResources**.</span><span class="sxs-lookup"><span data-stu-id="e37a3-148">If the query is actively waiting on resources from another query, then the state will be **AcquireResources**.</span></span>  <span data-ttu-id="e37a3-149">Si la consulta tiene todos los recursos necesarios, el estado será **Concedido**.</span><span class="sxs-lookup"><span data-stu-id="e37a3-149">If the query has all the required resources, then the state will be **Granted**.</span></span>

## <a name="monitor-tempdb"></a><span data-ttu-id="e37a3-150">Supervisión de tempdb</span><span class="sxs-lookup"><span data-stu-id="e37a3-150">Monitor tempdb</span></span>
<span data-ttu-id="e37a3-151">El uso elevado de tempdb puede ser la causa principal de problemas de rendimiento lento y falta de memoria.</span><span class="sxs-lookup"><span data-stu-id="e37a3-151">High tempdb utilization can be the root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="e37a3-152">Compruebe primero si tiene asimetría de datos o grupos de filas de calidad baja y emprenda las acciones adecuadas.</span><span class="sxs-lookup"><span data-stu-id="e37a3-152">Please first check if you have data skew or poor quality rowgroups and take the appropriate actions.</span></span> <span data-ttu-id="e37a3-153">Si observa que tempdb llega a su limite durante la ejecución de consultas, considere la posibilidad de escalar el almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="e37a3-153">Consider scaling your data warehouse if you find tempdb reaching its limits during query execution.</span></span> <span data-ttu-id="e37a3-154">A continuación se describe cómo identificar el uso de tempdb por consulta en cada nodo.</span><span class="sxs-lookup"><span data-stu-id="e37a3-154">The following describes how to identify tempdb usage per query on each node.</span></span> 

<span data-ttu-id="e37a3-155">Cree la siguiente vista para asociar el identificador de nodo apropiado para sys.dm_pdw_sql_requests.</span><span class="sxs-lookup"><span data-stu-id="e37a3-155">Create the following view to associate the appropriate node id for sys.dm_pdw_sql_requests.</span></span> <span data-ttu-id="e37a3-156">Esto le permitirá aprovechar otras DMV de paso y combinar esas tablas con sys.dm_pdw_sql_requests.</span><span class="sxs-lookup"><span data-stu-id="e37a3-156">This will enable you to leverage other pass-through DMVs and join those tables with sys.dm_pdw_sql_requests.</span></span>

```sql
-- sys.dm_pdw_sql_requests with the correct node id
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
<span data-ttu-id="e37a3-157">Ejecute la consulta siguiente para supervisar tempdb:</span><span class="sxs-lookup"><span data-stu-id="e37a3-157">Run the following query to monitor tempdb:</span></span>

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
## <a name="monitor-memory"></a><span data-ttu-id="e37a3-158">Supervisión de memoria</span><span class="sxs-lookup"><span data-stu-id="e37a3-158">Monitor memory</span></span>

<span data-ttu-id="e37a3-159">La causa principal de los problemas relacionados con el rendimiento lento y la falta de memoria puede ser la memoria.</span><span class="sxs-lookup"><span data-stu-id="e37a3-159">Memory can be the root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="e37a3-160">Compruebe primero si tiene asimetría de datos o grupos de filas de calidad baja y emprenda las acciones adecuadas.</span><span class="sxs-lookup"><span data-stu-id="e37a3-160">Please first check if you have data skew or poor quality rowgroups and take the appropriate actions.</span></span> <span data-ttu-id="e37a3-161">Si observa que el uso de memoria de SQL Server llega a su limite durante la ejecución de consultas, considere la posibilidad de escalar el almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="e37a3-161">Consider scaling your data warehouse if you find SQL Server memory usage reaching its limits during query execution.</span></span>

<span data-ttu-id="e37a3-162">La consulta siguiente devuelve el uso y la presión de memoria de SQL Server por nodo:</span><span class="sxs-lookup"><span data-stu-id="e37a3-162">The following query returns SQL Server memory usage and memory pressure per node:</span></span>   
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
## <a name="monitor-transaction-log-size"></a><span data-ttu-id="e37a3-163">Supervisión del tamaño del registro de transacciones</span><span class="sxs-lookup"><span data-stu-id="e37a3-163">Monitor transaction log size</span></span>
<span data-ttu-id="e37a3-164">La siguiente consulta devuelve el tamaño del registro de transacciones en cada distribución.</span><span class="sxs-lookup"><span data-stu-id="e37a3-164">The following query returns the transaction log size on each distribution.</span></span> <span data-ttu-id="e37a3-165">Compruebe primero si tiene asimetría de datos o grupos de filas de calidad baja y emprenda las acciones adecuadas.</span><span class="sxs-lookup"><span data-stu-id="e37a3-165">Please check if you have data skew or poor quality rowgroups and take the appropriate actions.</span></span> <span data-ttu-id="e37a3-166">Si uno de los archivos de registro está llegando a 160 GB, debería considerar la posibilidad de escalar verticalmente su instancia o limitar el tamaño de transacción.</span><span class="sxs-lookup"><span data-stu-id="e37a3-166">If one of the log files is reaching 160GB, you should consider scaling up your instance or limiting your transaction size.</span></span> 
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
## <a name="monitor-transaction-log-rollback"></a><span data-ttu-id="e37a3-167">Supervisión de la reversión del registro de transacciones</span><span class="sxs-lookup"><span data-stu-id="e37a3-167">Monitor transaction log rollback</span></span>
<span data-ttu-id="e37a3-168">Si las consultas producen errores o tardan mucho tiempo en continuar, puede comprobar y supervisar si tiene alguna reversión en las transacciones.</span><span class="sxs-lookup"><span data-stu-id="e37a3-168">If your queries are failing or taking a long time to proceed, you can check and monitor if you have any transactions rolling back.</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="e37a3-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e37a3-169">Next steps</span></span>
<span data-ttu-id="e37a3-170">Para más información acerca de las DMV, consulte [Vistas del sistema][System views].</span><span class="sxs-lookup"><span data-stu-id="e37a3-170">See [System views][System views] for more information on DMVs.</span></span>
<span data-ttu-id="e37a3-171">Para más información acerca de los procedimientos recomendados, consulte [Procedimientos recomendados para SQL Data Warehouse][SQL Data Warehouse best practices]</span><span class="sxs-lookup"><span data-stu-id="e37a3-171">See [SQL Data Warehouse best practices][SQL Data Warehouse best practices] for more information about best practices</span></span>

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
