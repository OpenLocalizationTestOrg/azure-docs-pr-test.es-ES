---
title: "Supervisión de Azure SQL Database con vistas de administración dinámica | Microsoft Docs"
description: "Obtenga información sobre cómo detectar y diagnosticar problemas comunes de rendimiento con vistas de administración dinámica para supervisar Base de datos SQL de Microsoft Azure."
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
ms.openlocfilehash: d9b007d29e06e672db71b4a8415673f258c3fd89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a><span data-ttu-id="1a37b-103">Supervisión de Base de datos SQL de Azure con vistas de administración dinámica</span><span class="sxs-lookup"><span data-stu-id="1a37b-103">Monitoring Azure SQL Database using dynamic management views</span></span>
<span data-ttu-id="1a37b-104">Base de datos de SQL de Microsoft Azure habilita un subconjunto de vistas de administración dinámica para diagnosticar problemas de rendimiento, que pueden deberse a consultas bloqueadas o de ejecución prolongada, cuellos de botella de recursos, planes de consulta deficientes, etc.</span><span class="sxs-lookup"><span data-stu-id="1a37b-104">Microsoft Azure SQL Database enables a subset of dynamic management views to diagnose performance problems, which might be caused by blocked or long-running queries, resource bottlenecks, poor query plans, and so on.</span></span> <span data-ttu-id="1a37b-105">En este tema se ofrece información sobre cómo encontrar problemas comunes de rendimiento con vistas de administración dinámica.</span><span class="sxs-lookup"><span data-stu-id="1a37b-105">This topic provides information on how to detect common performance problems by using dynamic management views.</span></span>

<span data-ttu-id="1a37b-106">Base de datos SQL admite parcialmente tres categorías de vistas de administración dinámica:</span><span class="sxs-lookup"><span data-stu-id="1a37b-106">SQL Database partially supports three categories of dynamic management views:</span></span>

* <span data-ttu-id="1a37b-107">Vistas de administración dinámica relacionadas con bases de datos.</span><span class="sxs-lookup"><span data-stu-id="1a37b-107">Database-related dynamic management views.</span></span>
* <span data-ttu-id="1a37b-108">Vistas de administración dinámica relacionadas con ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="1a37b-108">Execution-related dynamic management views.</span></span>
* <span data-ttu-id="1a37b-109">Vistas de administración dinámica relacionadas con transacciones.</span><span class="sxs-lookup"><span data-stu-id="1a37b-109">Transaction-related dynamic management views.</span></span>

<span data-ttu-id="1a37b-110">Para obtener información detallada sobre las vistas de administración dinámica, vea [Vistas y funciones de administración dinámica (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) en los libros en pantalla de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1a37b-110">For detailed information on dynamic management views, see [Dynamic Management Views and Functions (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) in SQL Server Books Online.</span></span>

## <a name="permissions"></a><span data-ttu-id="1a37b-111">Permisos</span><span class="sxs-lookup"><span data-stu-id="1a37b-111">Permissions</span></span>
<span data-ttu-id="1a37b-112">En Base de datos SQL, para realizar consultas en una vista de administración dinámica se requiere disponer de permisos **VIEW DATABASE STATE** .</span><span class="sxs-lookup"><span data-stu-id="1a37b-112">In SQL Database, querying a dynamic management view requires **VIEW DATABASE STATE** permissions.</span></span> <span data-ttu-id="1a37b-113">El permiso **VIEW DATABASE STATE** devuelve información sobre todos los objetos de la base de datos actual.</span><span class="sxs-lookup"><span data-stu-id="1a37b-113">The **VIEW DATABASE STATE** permission returns information about all objects within the current database.</span></span>
<span data-ttu-id="1a37b-114">Para conceder el permiso **VIEW DATABASE STATE** a un usuario de base de datos en concreto, ejecute la consulta siguiente:</span><span class="sxs-lookup"><span data-stu-id="1a37b-114">To grant the **VIEW DATABASE STATE** permission to a specific database user, run the following query:</span></span>

```GRANT VIEW DATABASE STATE TO database_user; ```

<span data-ttu-id="1a37b-115">En una instancia de SQL Server local, las vistas de administración dinámica devuelven la información de estado del servidor.</span><span class="sxs-lookup"><span data-stu-id="1a37b-115">In an instance of on-premises SQL Server, dynamic management views return server state information.</span></span> <span data-ttu-id="1a37b-116">En Base de datos SQL, devuelven información relativa únicamente a la base de datos lógica actual.</span><span class="sxs-lookup"><span data-stu-id="1a37b-116">In SQL Database, they return information regarding your current logical database only.</span></span>

## <a name="calculating-database-size"></a><span data-ttu-id="1a37b-117">Calculando tamaño de la base de datos</span><span class="sxs-lookup"><span data-stu-id="1a37b-117">Calculating database size</span></span>
<span data-ttu-id="1a37b-118">La siguiente consulta devuelve el tamaño de la base de datos en megabytes:</span><span class="sxs-lookup"><span data-stu-id="1a37b-118">The following query returns the size of your database (in megabytes):</span></span>

```
-- Calculates the size of the database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

<span data-ttu-id="1a37b-119">La consulta siguiente devuelve el tamaño de objetos individuales (en megabytes) de la base de datos:</span><span class="sxs-lookup"><span data-stu-id="1a37b-119">The following query returns the size of individual objects (in megabytes) in your database:</span></span>

```
-- Calculates the size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a><span data-ttu-id="1a37b-120">Supervisión de conexiones</span><span class="sxs-lookup"><span data-stu-id="1a37b-120">Monitoring connections</span></span>
<span data-ttu-id="1a37b-121">Puede usar la vista [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) para recuperar información sobre las conexiones establecidas con un servidor concreto de Azure SQL Database y los detalles de cada conexión.</span><span class="sxs-lookup"><span data-stu-id="1a37b-121">You can use the [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) view to retrieve information about the connections established to a specific Azure SQL Database server and the details of each connection.</span></span> <span data-ttu-id="1a37b-122">Además, la vista [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) resulta útil para recuperar información sobre todas las conexiones de usuario activas y las tareas internas.</span><span class="sxs-lookup"><span data-stu-id="1a37b-122">In addition, the [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) view is helpful when retrieving information about all active user connections and internal tasks.</span></span>
<span data-ttu-id="1a37b-123">La siguiente consulta recupera información sobre la conexión actual:</span><span class="sxs-lookup"><span data-stu-id="1a37b-123">The following query retrieves information on the current connection:</span></span>

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
> <span data-ttu-id="1a37b-124">Al ejecutar las vistas **sys.dm_exec_requests** y **sys.dm_exec_sessions**, si el usuario tiene permiso **VIEW DATABASE STATE** en la base de datos, verá todas las sesiones en ejecución en la base de datos; en caso contrario, el usuario solo verá la sesión actual.</span><span class="sxs-lookup"><span data-stu-id="1a37b-124">When executing the **sys.dm_exec_requests** and **sys.dm_exec_sessions views**, if you have **VIEW DATABASE STATE** permission on the database, you see all executing sessions on the database; otherwise, you see only the current session.</span></span>
> 
> 

## <a name="monitoring-query-performance"></a><span data-ttu-id="1a37b-125">Supervisión del rendimiento de las consultas</span><span class="sxs-lookup"><span data-stu-id="1a37b-125">Monitoring query performance</span></span>
<span data-ttu-id="1a37b-126">Las consultas de ejecución lenta o prolongada pueden consumir una cantidad significativa de recursos del sistema.</span><span class="sxs-lookup"><span data-stu-id="1a37b-126">Slow or long running queries can consume significant system resources.</span></span> <span data-ttu-id="1a37b-127">En esta sección se muestra cómo usar vistas de administración dinámica para detectar algunos problemas comunes de rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="1a37b-127">This section demonstrates how to use dynamic management views to detect a few common query performance problems.</span></span> <span data-ttu-id="1a37b-128">Una referencia anterior pero todavía útil para solucionar problemas, es el artículo de Microsoft TechNet, [Solución de problemas de rendimiento en SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) .</span><span class="sxs-lookup"><span data-stu-id="1a37b-128">An older but still helpful reference for troubleshooting, is the [Troubleshooting Performance Problems in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) article on Microsoft TechNet.</span></span>

### <a name="finding-top-n-queries"></a><span data-ttu-id="1a37b-129">Búsqueda de las N mejores consultas</span><span class="sxs-lookup"><span data-stu-id="1a37b-129">Finding top N queries</span></span>
<span data-ttu-id="1a37b-130">El siguiente ejemplo devuelve información acerca de las cinco consultas principales clasificadas en función del tiempo promedio de CPU.</span><span class="sxs-lookup"><span data-stu-id="1a37b-130">The following example returns information about the top five queries ranked by average CPU time.</span></span> <span data-ttu-id="1a37b-131">Este ejemplo agrega las consultas conforme a sus hash de consulta, por lo que las consultas lógicamente equivalentes se agrupan por sus consumos de recursos acumulativos.</span><span class="sxs-lookup"><span data-stu-id="1a37b-131">This example aggregates the queries according to their query hash, so that logically equivalent queries are grouped by their cumulative resource consumption.</span></span>

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

### <a name="monitoring-blocked-queries"></a><span data-ttu-id="1a37b-132">Supervisión de consultas bloqueadas</span><span class="sxs-lookup"><span data-stu-id="1a37b-132">Monitoring blocked queries</span></span>
<span data-ttu-id="1a37b-133">Las consultas lentas o de larga ejecución pueden contribuir al consumo excesivo de recursos y ser la consecuencia de consultas bloqueadas.</span><span class="sxs-lookup"><span data-stu-id="1a37b-133">Slow or long-running queries can contribute to excessive resource consumption and be the consequence of blocked queries.</span></span> <span data-ttu-id="1a37b-134">La causa del bloqueo puede ser un diseño deficiente de las aplicaciones, los planes de consulta incorrectos, la falta de índices útiles, etc.</span><span class="sxs-lookup"><span data-stu-id="1a37b-134">The cause of the blocking can be poor application design, bad query plans, the lack of useful indexes, and so on.</span></span> <span data-ttu-id="1a37b-135">Puede usar la vista sys.dm_tran_locks para obtener información sobre la actividad de bloqueo actual en el servidor de Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="1a37b-135">You can use the sys.dm_tran_locks view to get information about the current locking activity in your Azure SQL Database.</span></span> <span data-ttu-id="1a37b-136">Para obtener un ejemplo de código, consulte [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) en los Libros en pantalla de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1a37b-136">For example code, see [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) in SQL Server Books Online.</span></span>

### <a name="monitoring-query-plans"></a><span data-ttu-id="1a37b-137">Supervisión de planes de consulta</span><span class="sxs-lookup"><span data-stu-id="1a37b-137">Monitoring query plans</span></span>
<span data-ttu-id="1a37b-138">Un plan de consulta ineficaz también puede aumentar el consumo de CPU.</span><span class="sxs-lookup"><span data-stu-id="1a37b-138">An inefficient query plan also may increase CPU consumption.</span></span> <span data-ttu-id="1a37b-139">En el ejemplo siguiente, se usa la vista [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) para determinar qué consulta emplea la mayor cantidad acumulativa de CPU.</span><span class="sxs-lookup"><span data-stu-id="1a37b-139">The following example uses the [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) view to determine which query uses the most cumulative CPU.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="1a37b-140">Consulte también</span><span class="sxs-lookup"><span data-stu-id="1a37b-140">See also</span></span>
[<span data-ttu-id="1a37b-141">Introducción a Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="1a37b-141">Introduction to SQL Database</span></span>](sql-database-technical-overview.md)

