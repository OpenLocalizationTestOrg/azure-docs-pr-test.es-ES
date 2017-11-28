---
title: "Azure SQL base de datos de uso de vistas de administración dinámica aaaMonitoring | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodetect y diagnosticar problemas comunes de rendimiento mediante el uso de vistas de administración dinámica toomonitor base de datos de SQL de Microsoft Azure."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: d08f505f-3c62-47d4-bab7-35c9a834b79b
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 43d5fe2dd9a38d031e9334f6ad49fce5866e3bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a><span data-ttu-id="95765-103">Supervisión de Base de datos SQL de Azure con vistas de administración dinámica</span><span class="sxs-lookup"><span data-stu-id="95765-103">Monitoring Azure SQL Database using dynamic management views</span></span>
<span data-ttu-id="95765-104">Base de datos de SQL de Microsoft Azure permite un subconjunto de administración dinámica considera los problemas de rendimiento de toodiagnose, que pueden deberse a consultas bloqueadas o de ejecución prolongada, cuellos de botella de recursos, planes de consulta deficientes y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="95765-104">Microsoft Azure SQL Database enables a subset of dynamic management views toodiagnose performance problems, which might be caused by blocked or long-running queries, resource bottlenecks, poor query plans, and so on.</span></span> <span data-ttu-id="95765-105">Este tema proporciona información acerca de cómo toodetect problemas habituales de rendimiento mediante el uso de vistas de administración dinámica.</span><span class="sxs-lookup"><span data-stu-id="95765-105">This topic provides information on how toodetect common performance problems by using dynamic management views.</span></span>

<span data-ttu-id="95765-106">Base de datos SQL admite parcialmente tres categorías de vistas de administración dinámica:</span><span class="sxs-lookup"><span data-stu-id="95765-106">SQL Database partially supports three categories of dynamic management views:</span></span>

* <span data-ttu-id="95765-107">Vistas de administración dinámica relacionadas con bases de datos.</span><span class="sxs-lookup"><span data-stu-id="95765-107">Database-related dynamic management views.</span></span>
* <span data-ttu-id="95765-108">Vistas de administración dinámica relacionadas con ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="95765-108">Execution-related dynamic management views.</span></span>
* <span data-ttu-id="95765-109">Vistas de administración dinámica relacionadas con transacciones.</span><span class="sxs-lookup"><span data-stu-id="95765-109">Transaction-related dynamic management views.</span></span>

<span data-ttu-id="95765-110">Para obtener información detallada sobre las vistas de administración dinámica, vea [Vistas y funciones de administración dinámica (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) en los libros en pantalla de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="95765-110">For detailed information on dynamic management views, see [Dynamic Management Views and Functions (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) in SQL Server Books Online.</span></span>

## <a name="permissions"></a><span data-ttu-id="95765-111">Permisos</span><span class="sxs-lookup"><span data-stu-id="95765-111">Permissions</span></span>
<span data-ttu-id="95765-112">En Base de datos SQL, para realizar consultas en una vista de administración dinámica se requiere disponer de permisos **VIEW DATABASE STATE** .</span><span class="sxs-lookup"><span data-stu-id="95765-112">In SQL Database, querying a dynamic management view requires **VIEW DATABASE STATE** permissions.</span></span> <span data-ttu-id="95765-113">Hola **VIEW DATABASE STATE** permiso devuelve información acerca de todos los objetos de base de datos actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="95765-113">hello **VIEW DATABASE STATE** permission returns information about all objects within hello current database.</span></span>
<span data-ttu-id="95765-114">Hola toogrant **VIEW DATABASE STATE** permiso tooa específico de la base de datos de usuario, ejecute hello después de consulta:</span><span class="sxs-lookup"><span data-stu-id="95765-114">toogrant hello **VIEW DATABASE STATE** permission tooa specific database user, run hello following query:</span></span>

```GRANT VIEW DATABASE STATE toodatabase_user; ```

<span data-ttu-id="95765-115">En una instancia de SQL Server local, las vistas de administración dinámica devuelven la información de estado del servidor.</span><span class="sxs-lookup"><span data-stu-id="95765-115">In an instance of on-premises SQL Server, dynamic management views return server state information.</span></span> <span data-ttu-id="95765-116">En Base de datos SQL, devuelven información relativa únicamente a la base de datos lógica actual.</span><span class="sxs-lookup"><span data-stu-id="95765-116">In SQL Database, they return information regarding your current logical database only.</span></span>

## <a name="calculating-database-size"></a><span data-ttu-id="95765-117">Calculando tamaño de la base de datos</span><span class="sxs-lookup"><span data-stu-id="95765-117">Calculating database size</span></span>
<span data-ttu-id="95765-118">Hello consulta siguiente devuelve Hola tamaño de la base de datos (en megabytes):</span><span class="sxs-lookup"><span data-stu-id="95765-118">hello following query returns hello size of your database (in megabytes):</span></span>

```
-- Calculates hello size of hello database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

<span data-ttu-id="95765-119">Hello siguiente consulta devuelve Hola tamaño de objetos individuales (en megabytes) en la base de datos:</span><span class="sxs-lookup"><span data-stu-id="95765-119">hello following query returns hello size of individual objects (in megabytes) in your database:</span></span>

```
-- Calculates hello size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a><span data-ttu-id="95765-120">Supervisión de conexiones</span><span class="sxs-lookup"><span data-stu-id="95765-120">Monitoring connections</span></span>
<span data-ttu-id="95765-121">Puede usar hello [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) ver tooretrieve información acerca de servidor de base de datos de SQL Azure específico de hello conexiones establecidas tooa y detalles de Hola de cada conexión.</span><span class="sxs-lookup"><span data-stu-id="95765-121">You can use hello [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) view tooretrieve information about hello connections established tooa specific Azure SQL Database server and hello details of each connection.</span></span> <span data-ttu-id="95765-122">Además, Hola [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) vista es útil para recuperar información acerca de todas las conexiones de usuario activas y las tareas internas.</span><span class="sxs-lookup"><span data-stu-id="95765-122">In addition, hello [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) view is helpful when retrieving information about all active user connections and internal tasks.</span></span>
<span data-ttu-id="95765-123">Hello consulta siguiente recupera información de conexión actual de hello:</span><span class="sxs-lookup"><span data-stu-id="95765-123">hello following query retrieves information on hello current connection:</span></span>

```
SELECT
    c.session_id, c.net_transport, c.encrypt_option,
    c.auth_scheme, s.host_name, s.program_name,
    s.client_interface_name, s.login_name, s.nt_domain,
    s.nt_user_name, s.original_login_name, c.connect_time,
    s.login_time
FROM sys.dm_exec_connections AS c
JOIN sys.dm_exec_sessions AS s
    ON c.session_id = s.session_id
WHERE c.session_id = @@SPID;
```

> [!NOTE]
> <span data-ttu-id="95765-124">Al ejecutar hello **sys.dm_exec_requests** y **vistas sys.dm_exec_sessions**, si tienes **VIEW DATABASE STATE** permiso en la base de datos de hello, vea ejecutar todos los sesiones en la base de datos de hello; de lo contrario, verá solo Hola sesión actual.</span><span class="sxs-lookup"><span data-stu-id="95765-124">When executing hello **sys.dm_exec_requests** and **sys.dm_exec_sessions views**, if you have **VIEW DATABASE STATE** permission on hello database, you see all executing sessions on hello database; otherwise, you see only hello current session.</span></span>
> 
> 

## <a name="monitoring-query-performance"></a><span data-ttu-id="95765-125">Supervisión del rendimiento de las consultas</span><span class="sxs-lookup"><span data-stu-id="95765-125">Monitoring query performance</span></span>
<span data-ttu-id="95765-126">Las consultas de ejecución lenta o prolongada pueden consumir una cantidad significativa de recursos del sistema.</span><span class="sxs-lookup"><span data-stu-id="95765-126">Slow or long running queries can consume significant system resources.</span></span> <span data-ttu-id="95765-127">Esta sección muestra cómo toouse vistas de administración dinámica toodetect algunos problemas habituales de rendimiento de consulta.</span><span class="sxs-lookup"><span data-stu-id="95765-127">This section demonstrates how toouse dynamic management views toodetect a few common query performance problems.</span></span> <span data-ttu-id="95765-128">Una referencia anterior pero todavía útil para solucionar problemas, es hello [solucionar problemas de rendimiento en SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) artículo de Microsoft TechNet.</span><span class="sxs-lookup"><span data-stu-id="95765-128">An older but still helpful reference for troubleshooting, is hello [Troubleshooting Performance Problems in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) article on Microsoft TechNet.</span></span>

### <a name="finding-top-n-queries"></a><span data-ttu-id="95765-129">Búsqueda de las N mejores consultas</span><span class="sxs-lookup"><span data-stu-id="95765-129">Finding top N queries</span></span>
<span data-ttu-id="95765-130">Hello en el ejemplo siguiente se devuelve información sobre Hola cinco primeras consultas clasificadas por promedio de tiempo de CPU.</span><span class="sxs-lookup"><span data-stu-id="95765-130">hello following example returns information about hello top five queries ranked by average CPU time.</span></span> <span data-ttu-id="95765-131">Este ejemplo agrega las consultas de hello según tootheir hash de consulta, para que las consultas lógicamente equivalentes se agrupen según su consumo acumulado de los recursos.</span><span class="sxs-lookup"><span data-stu-id="95765-131">This example aggregates hello queries according tootheir query hash, so that logically equivalent queries are grouped by their cumulative resource consumption.</span></span>

```
SELECT TOP 5 query_stats.query_hash AS "Query Hash",
    SUM(query_stats.total_worker_time) / SUM(query_stats.execution_count) AS "Avg CPU Time",
    MIN(query_stats.statement_text) AS "Statement Text"
FROM
    (SELECT QS.*,
    SUBSTRING(ST.text, (QS.statement_start_offset/2) + 1,
    ((CASE statement_end_offset
        WHEN -1 THEN DATALENGTH(ST.text)
        ELSE QS.statement_end_offset END
            - QS.statement_start_offset)/2) + 1) AS statement_text
     FROM sys.dm_exec_query_stats AS QS
     CROSS APPLY sys.dm_exec_sql_text(QS.sql_handle) as ST) as query_stats
GROUP BY query_stats.query_hash
ORDER BY 2 DESC;
```

### <a name="monitoring-blocked-queries"></a><span data-ttu-id="95765-132">Supervisión de consultas bloqueadas</span><span class="sxs-lookup"><span data-stu-id="95765-132">Monitoring blocked queries</span></span>
<span data-ttu-id="95765-133">Consultas lentas o de ejecución prolongada pueden contribuir tooexcessive el consumo de recursos y ser consecuencia de Hola de consultas bloqueadas.</span><span class="sxs-lookup"><span data-stu-id="95765-133">Slow or long-running queries can contribute tooexcessive resource consumption and be hello consequence of blocked queries.</span></span> <span data-ttu-id="95765-134">causa de Hola de hello bloqueo puede ser diseño deficiente de la aplicación, incorrecta planes de consulta, Hola falta de índices útiles y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="95765-134">hello cause of hello blocking can be poor application design, bad query plans, hello lack of useful indexes, and so on.</span></span> <span data-ttu-id="95765-135">Puede usar hello sys.dm_tran_locks ver tooget información acerca de la actividad de bloqueo actual de hello en la base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="95765-135">You can use hello sys.dm_tran_locks view tooget information about hello current locking activity in your Azure SQL Database.</span></span> <span data-ttu-id="95765-136">Para obtener un ejemplo de código, consulte [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) en los Libros en pantalla de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="95765-136">For example code, see [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) in SQL Server Books Online.</span></span>

### <a name="monitoring-query-plans"></a><span data-ttu-id="95765-137">Supervisión de planes de consulta</span><span class="sxs-lookup"><span data-stu-id="95765-137">Monitoring query plans</span></span>
<span data-ttu-id="95765-138">Un plan de consulta ineficaz también puede aumentar el consumo de CPU.</span><span class="sxs-lookup"><span data-stu-id="95765-138">An inefficient query plan also may increase CPU consumption.</span></span> <span data-ttu-id="95765-139">Hello en el ejemplo siguiente se usa hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) ver toodetermine qué consulta emplea hello más CPU acumulada.</span><span class="sxs-lookup"><span data-stu-id="95765-139">hello following example uses hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) view toodetermine which query uses hello most cumulative CPU.</span></span>

```
SELECT
    highest_cpu_queries.plan_handle,
    highest_cpu_queries.total_worker_time,
    q.dbid,
    q.objectid,
    q.number,
    q.encrypted,
    q.[text]
FROM
    (SELECT TOP 50
        qs.plan_handle,
        qs.total_worker_time
    FROM
        sys.dm_exec_query_stats qs
    ORDER BY qs.total_worker_time desc) AS highest_cpu_queries
    CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS q
ORDER BY highest_cpu_queries.total_worker_time DESC;
```

## <a name="see-also"></a><span data-ttu-id="95765-140">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="95765-140">See also</span></span>
[<span data-ttu-id="95765-141">Introducción tooSQL base de datos</span><span class="sxs-lookup"><span data-stu-id="95765-141">Introduction tooSQL Database</span></span>](sql-database-technical-overview.md)

