---
title: rendimiento de la base de datos de aaaMonitoring en la base de datos de SQL de Azure | Documentos de Microsoft
description: "Obtenga información acerca de las opciones de hello para la supervisión de la base de datos con las herramientas de Azure y vistas de administración dinámica."
keywords: "supervisión de base de datos, rendimiento de base de datos"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: a2e47475-c955-4a8d-a65c-cbef9a6d9b9f
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: b13771183d4ccf37f58e2fc518b9b14de38212dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-database-performance-in-azure-sql-database"></a>Supervisión de rendimiento de bases de datos con la Base de datos SQL de Azure
Supervisar el rendimiento de Hola de una base de datos SQL de Azure se inicia con la supervisión del nivel de toohello relativa de uso de recursos de Hola de rendimiento de base de datos que elija. La supervisión ayuda a determinar si la base de datos tiene capacidad de sobra o está teniendo problemas para porque se alcanzó recursos y, a continuación, decidir si es nivel de rendimiento de tiempo tooadjust hello y [nivel de servicio](sql-database-service-tiers.md) de la base de datos. Puede supervisar la base de datos con las herramientas gráficas de hello [portal de Azure](https://portal.azure.com) o mediante SQL [vistas de administración dinámica](https://msdn.microsoft.com/library/ms188754.aspx).

## <a name="monitor-databases-using-hello-azure-portal"></a>Supervisar bases de datos mediante Hola portal de Azure
Hola [portal de Azure](https://portal.azure.com/), puede supervisar el uso de una sola base de datos, seleccione la base de datos y al hacer clic en hello **supervisión** gráfico. Se abrirá una **métrica** ventana que se puede cambiar haciendo clic en hello **Editar gráfico** botón. Agregue Hola siguientes métricas:

* Porcentaje de CPU
* Porcentaje de DTU
* Porcentaje de E/S de datos
* Porcentaje de tamaño de base de datos

Una vez haya agregado estas métricas, puede seguir tooview ellas en hello **supervisión** gráfico con más detalles sobre hello **métrica** ventana. Las métricas de cuatro muestran toohello relativa del porcentaje de utilización promedio hello **DTU** de la base de datos. Vea hello [niveles de servicio](sql-database-service-tiers.md) artículo para obtener más información acerca de la Dtu.

![Supervisión del nivel de servicio del rendimiento de la base de datos.](./media/sql-database-service-tiers/sqldb_service_tier_monitoring.png)

También puede configurar alertas en las métricas de rendimiento de Hola. Haga clic en hello **Agregar alerta** botón en hello **métrica** ventana. Siga hello tooconfigure de Asistente para la alerta. Tener Hola opción tooalert si las métricas de hello superan un umbral determinado o si Hola está por debajo de un umbral determinado.

Por ejemplo, si espera cargas de trabajo de hello en su toogrow de base de datos, puede tooconfigure una alerta de correo electrónico cada vez que la base de datos alcanza el 80% en cualquiera de las métricas de rendimiento de Hola. Puede utilizar esto como un toofigure de advertencia temprano out cuando es posible que tenga tooswitch toohello siguiente nivel de rendimiento superior.

las métricas de rendimiento de Hello también pueden ayudarle a determinar si es capaz de toodowngrade tooa nivel de rendimiento inferior. Se supone que usa una base de datos para estándar S2 y todos los programa de métricas de rendimiento que hello en promedio de base de datos no utiliza más del 10% en un momento dado. Es probable que esa base de datos de hello funcionarán bien en S1 estándar. Sin embargo, sea consciente de las cargas de trabajo que tienen picos o fluctúan antes de realizar el nivel de rendimiento inferior de hello decisión toomove tooa.

## <a name="monitor-databases-using-dmvs"></a>Supervisión de bases de datos mediante DMV
Hello mismas métricas que se exponen en el portal de hello también están disponibles a través de vistas del sistema: [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) Hola lógico **maestro** base de datos del servidor, y [sys.dm_db_ resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) en la base de datos de usuario de Hola. Use **sys.resource_stats** si necesita toomonitor menos datos pormenorizados durante un período más largo de tiempo. Use **sys.dm_db_resource_stats** si necesita toomonitor datos más pormenorizados durante un período de tiempo menor. Para obtener más información, consulte la [Guía de rendimiento de la Base de datos SQL de Azure](sql-database-single-database-monitor.md#monitor-resource-use).

> [!NOTE]
> **sys.dm_db_resource_stats** devuelve un conjunto de resultados vacío cuando se utiliza en las bases de datos Web Edition y Business Edition, que se retiraron.
>
>

### <a name="monitor-resource-use"></a>Supervisión del uso de recursos

Puede supervisar el uso de recursos con [Información de rendimiento de consultas de SQL Database](sql-database-query-performance.md) y [Almacén de consultas](https://msdn.microsoft.com/library/dn817826.aspx).

También puede supervisar el uso con estas dos vistas:

* [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx)
* [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx)

#### <a name="sysdmdbresourcestats"></a>sys.dm_db_resource_stats
Puede usar hello [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) vista en cada base de datos SQL. Hola **sys.dm_db_resource_stats** vista muestra el nivel de servicio de toohello relativa datos de uso de recursos recientes. Porcentajes medios para CPU, E/S de datos, escritura de registros y memoria, se registran cada 15 segundos y se mantienen durante una hora.

Dado que esta vista proporciona una panorámica más granular del uso de recursos, use primero **sys.dm_db_resource_stats** para cualquier análisis o solución de problemas de estado actual. Por ejemplo, esta consulta muestra recursos máximo y promedio de hello usan para base de datos actual de hello sobre Hola última hora:

    SELECT  
        AVG(avg_cpu_percent) AS 'Average CPU use in percent',
        MAX(avg_cpu_percent) AS 'Maximum CPU use in percent',
        AVG(avg_data_io_percent) AS 'Average data I/O in percent',
        MAX(avg_data_io_percent) AS 'Maximum data I/O in percent',
        AVG(avg_log_write_percent) AS 'Average log write use in percent',
        MAX(avg_log_write_percent) AS 'Maximum log write use in percent',
        AVG(avg_memory_usage_percent) AS 'Average memory use in percent',
        MAX(avg_memory_usage_percent) AS 'Maximum memory use in percent'
    FROM sys.dm_db_resource_stats;  

Para otras consultas, vea los ejemplos de hello en [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx).

#### <a name="sysresourcestats"></a>Sys.resource_stats
Hola [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) vista Hola **maestro** base de datos tiene información adicional que puede ayudarle a supervisar el rendimiento de saludo de la base de datos SQL en su nivel de rendimiento y de nivel de servicio específico . datos de Hola se recopilan cada 5 minutos y se mantienen durante aproximadamente 35 días. Esta vista es útil para realizar análisis históricos a largo plazo de cómo la base de datos SQL usa los recursos.

Hello gráfico siguiente muestra hello uso de recursos de CPU para una base de datos Premium con hello nivel de rendimiento P2 durante cada hora de una semana. Este gráfico comienza en lunes, muestra los 5 días de trabajo y, a continuación, se muestra un fin de semana, cuando se produce mucho menor en la aplicación hello.

![Uso de recursos de base de datos SQL](./media/sql-database-performance-guidance/sql_db_resource_utilization.png)

Según los datos de hello, esta base de datos tiene actualmente una carga de CPU máxima de aproximadamente un 50 por ciento el uso de CPU nivel de rendimiento relativa toohello P2 (el mediodía del martes). Si la CPU es un factor dominante hello en perfil de recursos de la aplicación hello, podría decidir que P2 es Hola derecho tooguarantee de nivel de rendimiento que Hola cargas de trabajo siempre se ajusta. Si espera un toogrow de aplicación con el tiempo, es un toohave buena idea un búfer de recursos adicionales para que la aplicación hello alguna vez no alcanza el límite de nivel de rendimiento de Hola. Si se aumenta el nivel de rendimiento de hello, puede ayudar a evitar errores visibles para el cliente que pueden producirse cuando una base de datos no tiene suficiente solicitudes de tooprocess de alimentación de forma eficaz, especialmente en entornos sensibles a la latencia. Un ejemplo es una base de datos que admite una aplicación que dibuja páginas Web en función de los resultados de Hola de llamadas de base de datos.

Otros tipos de aplicaciones podrían interpretar Hola mismo gráfico de manera diferente. Por ejemplo, si una aplicación trata los datos de nóminas tooprocess cada día y ha Hola mismo gráfico, este tipo de modelo de "proceso por lotes" podría funcionar bien en un nivel de rendimiento P1. Hola nivel de rendimiento P1 tiene 100 Dtu en comparación con too200 Dtu en hello nivel de rendimiento P2. Hola nivel de rendimiento P1 proporciona un rendimiento Hola mitad del programa Hola a nivel de rendimiento P2. Por lo tanto, el 50 por ciento de uso de CPU en P2 es igual al 100 por cien de uso de CPU en P1. Si la aplicación hello no tiene los tiempos de espera, podría ser importante si un trabajo tarde 2 o 2,5 horas toofinish, si se complete hoy. Una aplicación de esta categoría puede usar probablemente un nivel de rendimiento P1. Puede aprovechar las ventajas del hecho de Hola que hay períodos de tiempo durante el día de hello cuando el uso de recursos es menor, por lo que cualquier "carga elevada" se puede retrasar a uno de esos momentos de hello más adelante en el día de Hola de. nivel de rendimiento P1 Hola podría ser más conveniente para ese tipo de aplicación (y ahorrar dinero), siempre y cuando los trabajos de hello pueden finalizar a tiempo cada día.

Expone de base de datos de SQL Azure consumidos información de recursos para cada base de datos activa en hello **sys.resource_stats** vista de hello **maestro** base de datos en cada servidor. datos de Hello en la tabla de Hola se agregan a intervalos de 5 minutos. Con los niveles de servicio Basic, Standard y Premium hello, Hola datos pueden tardar más de 5 minutos tooappear en la tabla de hello, por lo que estos datos son más útiles para análisis históricos en lugar de análisis en tiempo casi real. Hola de consulta **sys.resource_stats** vista toosee Hola historial reciente de una base de datos y toovalidate si reserva Hola eligió entrega rendimiento de Hola que desea cuando sea necesario.

> [!NOTE]
> Debe ser conectado toohello **maestro** base de datos de la lógica tooquery de servidor de base de datos SQL **sys.resource_stats** en hello en los ejemplos siguientes.
> 
> 

Este ejemplo muestra cómo se exponen los datos hello en esta vista:

    SELECT TOP 10 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![vista de catálogo sys.resource_stats Hola](./media/sql-database-performance-guidance/sys_resource_stats.png)

Hello en el ejemplo siguiente se muestra distintas formas que puede usar hello **sys.resource_stats** tooget de ver información acerca de cómo la base de datos SQL usa los recursos de catálogo:

1. toolook en hello más allá de los recursos de la semana utilice para hello userdb1 de base de datos, puede ejecutar esta consulta:
   
        SELECT *
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND
              start_time > DATEADD(day, -7, GETDATE())
        ORDER BY start_time DESC;
2. tooevaluate la medida de la carga de trabajo se ajuste a nivel de rendimiento de hello, necesita toodrill hacia abajo en todos los aspectos de métricas de recursos de hello: CPU, lecturas, escrituras, número de trabajadores y número de sesiones. Aquí es revisada consultar mediante **sys.resource_stats** tooreport Hola valores promedio y máximos de estas métricas de recursos:
   
        SELECT
            avg(avg_cpu_percent) AS 'Average CPU use in percent',
            max(avg_cpu_percent) AS 'Maximum CPU use in percent',
            avg(avg_data_io_percent) AS 'Average physical data I/O use in percent',
            max(avg_data_io_percent) AS 'Maximum physical data I/O use in percent',
            avg(avg_log_write_percent) AS 'Average log write use in percent',
            max(avg_log_write_percent) AS 'Maximum log write use in percent',
            avg(max_session_percent) AS 'Average % of sessions',
            max(max_session_percent) AS 'Maximum % of sessions',
            avg(max_worker_percent) AS 'Average % of workers',
            max(max_worker_percent) AS 'Maximum % of workers'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
3. Con esta información acerca de los valores de hello promedio y máximo de cada métrica de recurso, se puede evaluar cómo bien la carga de trabajo se ajusta al nivel de rendimiento de Hola que eligió. Normalmente, los valores promedio de **sys.resource_stats** ofrecerle una toouse buena línea base con tamaño de destino de Hola. Debería ser su vara de medida principal. Para obtener un ejemplo, puede que esté usando capa de servicio estándar Hola con nivel de rendimiento de S2. promedio de Hello utilizar los porcentajes para las lecturas de E/S y CPU y escrituras están por debajo de 40 por ciento, promedio de Hola de trabajadores está por debajo de 50 y Hola cantidad promedio de sesiones es menor que 200. La carga de trabajo podría ajustarse en hello nivel de rendimiento S1. Es fácil toosee si la base de datos se ajusta a trabajo hello y límites de la sesión. toosee si una base de datos se ajusta a un nivel de rendimiento inferior con lo que respecta a tooCPU, lecturas y escrituras, divida el número DTU de Hola de nivel de rendimiento inferior Hola por número de DTU del nivel de rendimiento actual de hello y, a continuación, multiplique el resultado de hello por 100:
   
    **S1 DTU / S2 DTU * 100 = 20 / 50 * 100 = 40**
   
    resultado de Hello es la diferencia de rendimiento relativo de hello entre dos niveles de rendimiento hello en porcentaje. Si el uso de recursos no supera esta cantidad, la carga de trabajo podría ajustarse en el nivel de rendimiento inferior Hola. Sin embargo, es necesario toolook todos los intervalos de valores de uso de recursos y determinar, por porcentaje, la frecuencia con la carga de trabajo de la base de datos se ajustaría al nivel de rendimiento inferior Hola. Hello siguiente consulta expresa Hola ajustarse porcentaje por dimensión de recursos, en función de umbral de Hola de 40 por ciento que se calcula en este ejemplo:
   
        SELECT
            (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log Write Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical Data IO Fit Percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    En función de su objetivo de nivel de servicio (SLO) de base de datos, puede decidir si la carga de trabajo se adapta a nivel de rendimiento inferior Hola. Si la carga de trabajo de base de datos SLO es de 99,9% y hello consulta anterior devuelve valores mayores que 99,9% para todas las tres dimensiones de recursos, la carga de trabajo es probable que se ajusta al nivel de rendimiento inferior Hola.
   
    Examinando el porcentaje de hello ajustar también ofrece una visión general de si debe mover los toohello siguiente superior toomeet de nivel de rendimiento su SLO. Por ejemplo, userdb1 muestra hello consecuencia del uso de CPU para hello semana anterior:
   
   | Porcentaje medio de CPU | Porcentaje máximo de CPU |
   | --- | --- |
   | 24,5 |100,00 |
   
    Hola promedio de CPU es aproximadamente un cuarto del límite de Hola de nivel de rendimiento de hello, lo que se ajustaría bien en el nivel de rendimiento de Hola de base de datos de Hola. Sin embargo, valor máximo de hello muestra que esa base de datos de hello alcanza el límite de Hola de nivel de rendimiento de Hola. ¿Necesita toomove toohello siguiente nivel de rendimiento superior? Observar cómo muchas veces la carga de trabajo alcanza el 100 por ciento y, a continuación, comparar cargas de trabajo de base de datos de tooyour SLO.
   
        SELECT
        (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log write fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical data I/O fit percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    Si esta consulta devuelve un valor menor que 99,9 por ciento para cualquiera de las dimensiones de recursos de hello tres, considere la posibilidad de cualquier móvil toohello siguiente nivel de rendimiento superior o use carga hello tooreduce técnicas de optimización de aplicaciones en la base de datos SQL de Hola.
4. Este ejercicio también tiene en cuenta el aumento de carga de trabajo prevista en hello futuras.

Para los grupos elásticos, puede supervisar las bases de datos individuales en el grupo de hello con técnicas de hello descritas en esta sección. Pero también puede supervisar el grupo de Hola como un todo. Para más información, consulte el artículo sobre la [supervisión y administración de un grupo de bases de datos elásticas](sql-database-elastic-pool-manage-portal.md).


### <a name="maximum-concurrent-requests"></a>Número máximo de solicitudes simultáneas
número de hello toosee de solicitudes simultáneas, ejecute esta consulta de Transact-SQL en la base de datos SQL:

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R

carga de trabajo de tooanalyze Hola de una base de datos de SQL Server local, modifique este toofilter de consulta en la base de datos específica de hello desea tooanalyze. Por ejemplo, si tiene una base de datos local denominado MyDatabase, esta consulta de Transact-SQL devuelve el recuento de Hola de solicitudes simultáneas en esa base de datos:

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R
    INNER JOIN sys.databases D ON D.database_id = R.database_id
    AND D.name = 'MyDatabase'

Se trata simplemente de una instantánea en un solo momento dado. tooget una mejor comprensión de la carga de trabajo y los requisitos de solicitudes simultáneas, necesitará toocollect número de muestras con el tiempo.

### <a name="maximum-concurrent-logins"></a>Número máximo de inicios de sesión simultáneos
Puede analizar el tooget de patrones una idea de frecuencia de Hola de inicios de sesión de usuario y la aplicación. También puede ejecutar las cargas reales en un toomake de entorno de prueba seguro de que no tiene este u otros límites que se explican en este artículo. No hay una única consulta o vista de administración dinámica (DMV) que pueda mostrar el número o el historial de inicios de sesión simultáneos.

Si usan varios clientes Hola misma cadena de conexión, hello servicio autentica cada inicio de sesión. Si 10 usuarios se conecten simultáneamente tooa base de datos mediante el uso de Hola el mismo nombre de usuario y contraseña, sería 10 inicios de sesión simultáneos. Este límite aplica solo toohello duración del inicio de sesión de Hola y la autenticación. Si los usuarios de hello 10 mismo conectan secuencialmente toohello base de datos, número de Hola de inicios de sesión simultáneos nunca sería mayor que 1.

> [!NOTE]
> Actualmente, este límite no aplica toodatabases en grupos elásticos.
> 
> 

### <a name="maximum-sessions"></a>Número máximo de sesiones
número de hello toosee de sesiones activas actuales, ejecute esta consulta de Transact-SQL en la base de datos SQL:

    SELECT COUNT(*) AS [Sessions]
    FROM sys.dm_exec_connections

Si está analizando una carga de trabajo de SQL Server local, modifique hello toofocus de consulta en una base de datos. Esta consulta le ayuda a determinar las necesidades de sesión posibles para la base de datos de hello si se va a mover tooAzure base de datos SQL.

    SELECT COUNT(*)  AS [Sessions]
    FROM sys.dm_exec_connections C
    INNER JOIN sys.dm_exec_sessions S ON (S.session_id = C.session_id)
    INNER JOIN sys.databases D ON (D.database_id = S.database_id)
    WHERE D.name = 'MyDatabase'

Nuevamente, estas consultas devuelven un número puntual. Si recopila varias muestras con el tiempo, tendrá usar mejor comprensión de saludo de la sesión.

Para el análisis de la base de datos SQL, puede obtener estadísticas históricas en las sesiones consultando hello [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) vista y revisar hello **active_session_count** columna. 
