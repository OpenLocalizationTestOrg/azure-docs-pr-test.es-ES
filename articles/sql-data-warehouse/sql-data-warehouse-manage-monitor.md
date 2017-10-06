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
# <a name="monitor-your-workload-using-dmvs"></a>Supervisión de la carga de trabajo mediante DMV
Este artículo se describe cómo toouse vistas de administración dinámica (DMV) toomonitor la carga de trabajo e investigar la ejecución de la consulta en el almacén de datos de SQL Azure.

## <a name="permissions"></a>Permisos
Hola tooquery DMV en este artículo, debe tener permiso VIEW DATABASE STATE o CONTROL. Normalmente la concesión VIEW DATABASE STATE es permiso Hola preferida ya que es mucho más restrictiva.

```sql
GRANT VIEW DATABASE STATE toomyuser;
```

## <a name="monitor-connections"></a>Supervisión de conexiones
Todos los inicios de sesión tooSQL almacenamiento de datos se registran demasiado[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].  Esta DMV contiene Hola última 10.000 inicios de sesión.  Hola session_id es la clave principal de Hola y se asigna de forma secuencial para cada nuevo inicio de sesión.

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a>Supervisión de ejecuciones de consultas
Todas las consultas ejecutadas en almacenamiento de datos de SQL se registran demasiado[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].  Esta DMV contiene Hola última 10.000 consultas ejecutadas.  Hola request_id identifica cada consulta y es la clave principal de Hola para esta DMV.  Hola request_id se asigna de forma secuencial para cada nueva consulta y tiene como prefijo QID, que representa el identificador de consulta.  Al consultar en esta DMV sobre un campo session_id determinado, se muestran todas las consultas de un inicio de sesión concreto.

> [!NOTE]
> Los procedimientos almacenados utilizan varios identificadores de solicitud.  Los identificadores de solicitud se asignan en orden secuencial. 
> 
> 

Estos son los planes de ejecución de pasos toofollow tooinvestigate de consultas y las horas para una consulta determinada.

### <a name="step-1-identify-hello-query-you-wish-tooinvestigate"></a>PASO 1: Identificar consulta Hola que desea tooinvestigate
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

De hello anteriores resultados de la consulta, **Hola Nota Id. de solicitud** de consulta de Hola que desearía tooinvestigate.

Las consultas de hello **Suspended** estado se ponen en cola debido a límites de tooconcurrency. Estas consultas también aparecen en la consulta de las esperas de hello sys.dm_pdw_waits con un tipo de UserConcurrencyResourceType. Para más información acerca de los límites de simultaneidad, consulte [Simultaneidad y administración de cargas de trabajo en SQL Data Warehouse][Concurrency and workload management]. Las consultas también pueden esperar por otros motivos, como los bloqueos de objetos.  Si la consulta está esperando un recurso, consulte la sección [Supervisión de consultas en espera][Investigating queries waiting for resources] de este mismo artículo.

búsqueda de hello toosimplify de una consulta en la tabla de sys.dm_pdw_exec_requests hello, utilice [etiqueta] [ LABEL] tooassign una consulta de tooyour de comentario que se puede buscar en la vista de sys.dm_pdw_exec_requests Hola.

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-hello-query-plan"></a>PASO 2: Investigar el plan de consulta de Hola
Use plan de hello Id. de solicitud tooretrieve hello de la consulta distribuida SQL (DSQL) desde [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].

```sql
-- Find hello distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

Cuando un plan DSQL está tardando más de lo esperado, causa de hello puede ser un plan de complejo con muchos pasos DSQL o solamente un paso tarda mucho tiempo.  Si plan de hello muchos pasos con varias operaciones de movimiento, considere la posibilidad de optimizar el movimiento de datos de tabla distribuciones tooreduce. Hola [tabla distribución] [ Table distribution] artículo explica por qué datos deben ser una consulta de toosolve movida y explican algunos movimiento de datos de distribución estrategias toominimize.

tooinvestigate obtener más información acerca de un solo paso, hello *operation_type* columna de Hola Hola de paso y tenga en cuenta de consulta de ejecución prolongada **índice paso**:

* Continúe con el paso 3a sobre **operaciones SQL**: OnOperation, RemoteOperation, ReturnOperation.
* Continúe con el paso 3b sobre **operaciones de movimiento de datos**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.

### <a name="step-3a-investigate-sql-on-hello-distributed-databases"></a>PASO 3a: investigar SQL en bases de datos de hello distribuida
Usar Hola Id. de solicitud y detalles de tooretrieve del índice de paso de Hola de [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], que contiene información de ejecución de paso de consulta de hello en todos los de hello distribuidas bases de datos.

```sql
-- Find hello distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

Cuando se ejecuta el paso de consulta de hello, [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] puede ser usado tooretrieve Hola estimado plan para SQL Server de hello memoria caché del plan de SQL Server para el paso de hello ejecutando en un determinado distribución.

```sql
-- Find hello SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-hello-distributed-databases"></a>PASO 3b: investigar el movimiento de datos en las bases de datos de hello distribuida
Usar Id. de solicitud de Hola y Hola información de índice de paso tooretrieve acerca de un paso de movimiento de datos con cada distribución de [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].

```sql
-- Find hello information about all hello workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* Comprobar hello *total_elapsed_time* toosee de columna si una distribución particular está tardando mucho más tiempo que otras personas para que el movimiento de datos.
* Para la distribución de ejecución prolongada de hello, comprobar hello *rows_processed* toosee de columna si el número de Hola de filas que se mueven de distribución es significativamente mayor que otros usuarios. En ese caso, esto puede indicar un sesgo de los datos subyacentes.

Si está ejecutando la consulta de hello, [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] puede ser usado tooretrieve Hola estimado plan para SQL Server de hello memoria caché del plan de SQL Server para hello actuales paso SQL dentro de un determinado distribución.

```sql
-- Find hello SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a>Supervisión de consultas en espera
Si descubre que la consulta no está realizando progresos porque está esperando un recurso, esta es una consulta que muestra todos los recursos de hello que está esperando una consulta.

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

Si consulta Hola activamente está esperando en recursos de otra consulta, estado de hello será **AcquireResources**.  Si consulta hello tiene todos los recursos necesario de hello, Hola estado será **Granted**.

## <a name="monitor-tempdb"></a>Supervisión de tempdb
Uso de tempdb alta puede ser Hola causa de un rendimiento lento y problemas de memoria insuficiente. Por favor, compruebe primero si tiene grupos de filas de sesgo o de mala calidad de datos y tome las medidas oportunas Hola. Si observa que tempdb llega a su limite durante la ejecución de consultas, considere la posibilidad de escalar el almacenamiento de datos. Hola a continuación se describe cómo tooidentify al uso de tempdb por cada consulta en cada nodo. 

Crear Hola siguiente Id. de hello nodo apropiado tooassociate de vista para sys.dm_pdw_sql_requests. Esto habilitará tooleverage otras DMV acceso directo y combinar las tablas con sys.dm_pdw_sql_requests.

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
Ejecute hello después consulta toomonitor tempdb:

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
## <a name="monitor-memory"></a>Supervisión de memoria

Memoria puede ser la causa de Hola para un rendimiento lento y problemas de memoria insuficiente. Por favor, compruebe primero si tiene grupos de filas de sesgo o de mala calidad de datos y tome las medidas oportunas Hola. Si observa que el uso de memoria de SQL Server llega a su limite durante la ejecución de consultas, considere la posibilidad de escalar el almacenamiento de datos.

Hola después de consulta devuelve presión de memoria y uso de memoria de SQL Server por nodo: 
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
## <a name="monitor-transaction-log-size"></a>Supervisión del tamaño del registro de transacciones
Hello consulta siguiente devuelve tamaño del registro de transacciones de hello en cada tipo de distribución. Compruebe si tiene grupos de filas de sesgo o de mala calidad de datos y tome las medidas oportunas Hola. Si uno de los archivos de registro de hello está llegando a 160GB, debería considerar el escalado de la instancia o limitar el tamaño de la transacción. 
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
## <a name="monitor-transaction-log-rollback"></a>Supervisión de la reversión del registro de transacciones
Si se producen errores en las consultas o llevar a cabo una tooproceed mucho tiempo, puede comprobar y supervisar si dispone de las transacciones de reversión.
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

## <a name="next-steps"></a>Pasos siguientes
Para más información acerca de las DMV, consulte [Vistas del sistema][System views].
Para más información acerca de los procedimientos recomendados, consulte [Procedimientos recomendados para SQL Data Warehouse][SQL Data Warehouse best practices]

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
