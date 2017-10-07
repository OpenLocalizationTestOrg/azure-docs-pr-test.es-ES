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
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a>Supervisión de Base de datos SQL de Azure con vistas de administración dinámica
Base de datos de SQL de Microsoft Azure permite un subconjunto de administración dinámica considera los problemas de rendimiento de toodiagnose, que pueden deberse a consultas bloqueadas o de ejecución prolongada, cuellos de botella de recursos, planes de consulta deficientes y así sucesivamente. Este tema proporciona información acerca de cómo toodetect problemas habituales de rendimiento mediante el uso de vistas de administración dinámica.

Base de datos SQL admite parcialmente tres categorías de vistas de administración dinámica:

* Vistas de administración dinámica relacionadas con bases de datos.
* Vistas de administración dinámica relacionadas con ejecuciones.
* Vistas de administración dinámica relacionadas con transacciones.

Para obtener información detallada sobre las vistas de administración dinámica, vea [Vistas y funciones de administración dinámica (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) en los libros en pantalla de SQL Server.

## <a name="permissions"></a>Permisos
En Base de datos SQL, para realizar consultas en una vista de administración dinámica se requiere disponer de permisos **VIEW DATABASE STATE** . Hola **VIEW DATABASE STATE** permiso devuelve información acerca de todos los objetos de base de datos actual de Hola.
Hola toogrant **VIEW DATABASE STATE** permiso tooa específico de la base de datos de usuario, ejecute hello después de consulta:

```GRANT VIEW DATABASE STATE toodatabase_user; ```

En una instancia de SQL Server local, las vistas de administración dinámica devuelven la información de estado del servidor. En Base de datos SQL, devuelven información relativa únicamente a la base de datos lógica actual.

## <a name="calculating-database-size"></a>Calculando tamaño de la base de datos
Hello consulta siguiente devuelve Hola tamaño de la base de datos (en megabytes):

```
-- Calculates hello size of hello database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

Hello siguiente consulta devuelve Hola tamaño de objetos individuales (en megabytes) en la base de datos:

```
-- Calculates hello size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a>Supervisión de conexiones
Puede usar hello [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) ver tooretrieve información acerca de servidor de base de datos de SQL Azure específico de hello conexiones establecidas tooa y detalles de Hola de cada conexión. Además, Hola [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) vista es útil para recuperar información acerca de todas las conexiones de usuario activas y las tareas internas.
Hello consulta siguiente recupera información de conexión actual de hello:

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
> Al ejecutar hello **sys.dm_exec_requests** y **vistas sys.dm_exec_sessions**, si tienes **VIEW DATABASE STATE** permiso en la base de datos de hello, vea ejecutar todos los sesiones en la base de datos de hello; de lo contrario, verá solo Hola sesión actual.
> 
> 

## <a name="monitoring-query-performance"></a>Supervisión del rendimiento de las consultas
Las consultas de ejecución lenta o prolongada pueden consumir una cantidad significativa de recursos del sistema. Esta sección muestra cómo toouse vistas de administración dinámica toodetect algunos problemas habituales de rendimiento de consulta. Una referencia anterior pero todavía útil para solucionar problemas, es hello [solucionar problemas de rendimiento en SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) artículo de Microsoft TechNet.

### <a name="finding-top-n-queries"></a>Búsqueda de las N mejores consultas
Hello en el ejemplo siguiente se devuelve información sobre Hola cinco primeras consultas clasificadas por promedio de tiempo de CPU. Este ejemplo agrega las consultas de hello según tootheir hash de consulta, para que las consultas lógicamente equivalentes se agrupen según su consumo acumulado de los recursos.

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

### <a name="monitoring-blocked-queries"></a>Supervisión de consultas bloqueadas
Consultas lentas o de ejecución prolongada pueden contribuir tooexcessive el consumo de recursos y ser consecuencia de Hola de consultas bloqueadas. causa de Hola de hello bloqueo puede ser diseño deficiente de la aplicación, incorrecta planes de consulta, Hola falta de índices útiles y así sucesivamente. Puede usar hello sys.dm_tran_locks ver tooget información acerca de la actividad de bloqueo actual de hello en la base de datos de SQL Azure. Para obtener un ejemplo de código, consulte [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) en los Libros en pantalla de SQL Server.

### <a name="monitoring-query-plans"></a>Supervisión de planes de consulta
Un plan de consulta ineficaz también puede aumentar el consumo de CPU. Hello en el ejemplo siguiente se usa hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) ver toodetermine qué consulta emplea hello más CPU acumulada.

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

## <a name="see-also"></a>Otras referencias
[Introducción tooSQL base de datos](sql-database-technical-overview.md)

