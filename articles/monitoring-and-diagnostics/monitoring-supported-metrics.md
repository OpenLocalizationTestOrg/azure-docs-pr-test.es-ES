---
title: "métricas de supervisión - métricas admitidas por el tipo de recurso aaaAzure | Documentos de Microsoft"
description: "Lista de métricas disponibles para cada tipo de recurso con Azure Monitor."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 63d4ac65-1688-40d1-85c8-7cd408285b0f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/05/2017
ms.author: johnkem
ms.openlocfilehash: 66834238a1a4fcd7db1464cc023c18ee2563517a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="supported-metrics-with-azure-monitor"></a>Métricas compatibles con Azure Monitor
El Monitor de Azure proporciona toointeract de varias maneras con las métricas, incluidos para ellos diagramas en el portal de hello, obtener acceso a ellos a través de la API de REST de Hola o consultar ellos usando PowerShell o CLI. A continuación se muestra una lista completa de todas las métricas disponibles actualmente en la canalización de métricas de Azure Monitor.

> [!NOTE]
> Otras métricas pueden estar disponibles en el portal de Hola o con las API heredadas. Esta lista solo incluye las métricas de versión preliminar pública disponibles con la versión preliminar pública de Hola de canalización de métrica de Monitor de Azure de hello consolidado.
>
>

## <a name="microsoftanalysisservicesservers"></a>Microsoft.AnalysisServices/servers

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Descripción|
|---|---|---|---|---|
|qpu_metric|QPU|Recuento|Media|QPU. Intervalo de 0-100 para S1, 0-200 para S2 y 0-400 para S4|
|memory_metric|Memoria|Bytes|Media|Memoria. Intervalo de 0-25 GB para S1, 0-50 GB para S2 y 0-100 GB para S4|
|TotalConnectionRequests|Número total de solicitudes de conexión|Recuento|Media|Número total de solicitudes de conexión. Se trata de llegadas.|
|SuccessfullConnectionsPerSec|Conexiones correctas por segundo|CountPerSecond|Media|Tasa de finalizaciones de conexión correctas.|
|TotalConnectionFailures|Número total de errores de conexión|Recuento|Media|Número total de intentos de conexión con error.|
|CurrentUserSessions|Sesiones de usuario actuales|Recuento|Media|Número actual de sesiones de usuario establecidas.|
|QueryPoolBusyThreads|Subprocesos ocupados de grupo de consultas|Recuento|Media|Número de subprocesos ocupados en el grupo de subprocesos de consulta de Hola.|
|CommandPoolJobQueueLength|Longitud de cola de trabajos de grupo de comandos|Recuento|Media|Número de trabajos en cola de hello del grupo de subprocesos de comando de Hola.|
|ProcessingPoolJobQueueLength|Longitud de cola de trabajos de grupo de procesamiento|Recuento|Media|Número de trabajos no son de e/s en cola Hola de hello grupo de subprocesos de procesamiento.|
|CurrentConnections|Conexión: conexiones actuales|Recuento|Media|Número actual de conexiones de cliente establecidas.|
|CleanerCurrentPrice|Memoria: precio actual de limpieza|Recuento|Media|Precio actual de memoria, $/ byte/tiempo, normalizado too1000.|
|CleanerMemoryShrinkable|Memoria: memoria de limpieza reducible|Bytes|Media|Cantidad de memoria, en bytes, asunto toopurging limpiador en segundo plano Hola.|
|CleanerMemoryNonshrinkable|Memoria: memoria de limpieza no reducible|Bytes|Media|Cantidad de memoria, en bytes, no el asunto toopurging limpiador en segundo plano Hola.|
|MemoryUsage|Memoria: uso de memoria|Bytes|Media|Uso de memoria de proceso de servidor hello tal y como se usa para calcular el precio de memoria de limpiador. Toocounter igual Proceso\Bytes privados más hello de datos asignado a la memoria, se omite la memoria que se ha asignado por el motor de análisis en memoria de xVelocity (VertiPaq) de Hola que sobrepasen el motor xVelocity de hello límite de memoria.|
|MemoryLimitHard|Memoria: límite de memoria física|Bytes|Media|Límite de memoria física del archivo de configuración.|
|MemoryLimitHigh|Memoria: límite alto de memoria|Bytes|Media|Límite alto de memoria del archivo de configuración.|
|MemoryLimitLow|Memoria: límite bajo de memoria|Bytes|Media|Límite bajo de memoria del archivo de configuración.|
|MemoryLimitVertiPaq|Memoria: VertiPaq de límite de memoria|Bytes|Media|Límite en memoria del archivo de configuración.|
|Quota|Memoria: cuota|Bytes|Media|Cuota de memoria actual, en bytes. La cuota de memoria también se denomina concesión de memoria o reserva de memoria.|
|QuotaBlocked|Memoria: cuota bloqueada|Recuento|Media|Número actual de solicitudes de cuota que están bloqueadas hasta que se liberen otras cuotas de memoria.|
|VertiPaqNonpaged|Memoria: VertiPaq no paginado|Bytes|Media|Bytes de memoria bloqueada en espacio de trabajo de Hola para su uso por el motor de hello en memoria.|
|VertiPaqPaged|Memoria: VertiPaq paginado|Bytes|Media|Bytes de memoria paginada en uso para datos en memoria.|
|RowsReadPerSec|Procesamiento: filas leídas por segundo|CountPerSecond|Media|Velocidad de filas leídas de todas las bases de datos relacionales.|
|RowsConvertedPerSec|Procesamiento: filas convertidas por segundo|CountPerSecond|Media|Velocidad de filas convertidas durante el procesamiento.|
|RowsWrittenPerSec|Procesamiento: filas escritas por segundo|CountPerSecond|Media|Velocidad de filas escritas durante el procesamiento.|
|CommandPoolBusyThreads|Subprocesos: subprocesos ocupados del grupo de comandos|Recuento|Media|Número de subprocesos ocupados en el grupo de subprocesos de comando de Hola.|
|CommandPoolIdleThreads|Subprocesos: subprocesos inactivos del grupo de comandos|Recuento|Media|Número de subprocesos inactivos en el grupo de subprocesos de comando de Hola.|
|LongParsingBusyThreads|Subprocesos: subprocesos ocupados en análisis largos|Recuento|Media|Número de subprocesos ocupados en el grupo de subprocesos de análisis largo de Hola.|
|LongParsingIdleThreads|Subprocesos: subprocesos inactivos en análisis largos|Recuento|Media|Número de subprocesos inactivos en hello grupo de subprocesos de análisis largo.|
|LongParsingJobQueueLength|Subprocesos: longitud de cola de trabajos en análisis largos|Recuento|Media|Número de trabajos en cola de Hola de hello grupo de subprocesos de análisis largo.|
|ProcessingPoolBusyIOJobThreads|Subprocesos: subprocesos de trabajo de E/S ocupados del grupo de procesamiento|Recuento|Media|Número de subprocesos que se ejecutan trabajos de E/S en el grupo de subprocesos de procesamiento de Hola.|
|ProcessingPoolBusyNonIOThreads|Subprocesos: subprocesos de trabajo ocupados que no son de E/S del grupo de procesamiento|Recuento|Media|Número de subprocesos que se ejecutan los trabajos no son de e/s en el grupo de subprocesos de procesamiento de Hola.|
|ProcessingPoolIOJobQueueLength|Subprocesos: longitud de cola de trabajos de E/S del grupo de procesamiento|Recuento|Media|Número de trabajos de E/S en cola de hello del grupo de subprocesos de procesamiento de Hola.|
|ProcessingPoolIdleIOJobThreads|Subprocesos: subprocesos de trabajo de E/S inactivos del grupo de procesamiento|Recuento|Media|Número de subprocesos inactivos de trabajos de E/S en el grupo de subprocesos de procesamiento de Hola.|
|ProcessingPoolIdleNonIOThreads|Subprocesos: subprocesos de trabajo inactivos que no son de E/S del grupo de procesamiento|Recuento|Media|Número de subprocesos inactivos en el grupo de subprocesos de procesamiento de hello dedicado trabajos toonon de e/s.|
|QueryPoolIdleThreads|Subprocesos: subprocesos inactivos del grupo de consultas|Recuento|Media|Número de subprocesos inactivos de trabajos de E/S en el grupo de subprocesos de procesamiento de Hola.|
|QueryPoolJobQueueLength|Subprocesos: longitud de cola de trabajos del grupo de consultas|Recuento|Media|Número de trabajos en cola de hello del grupo de subprocesos de consulta de Hola.|
|ShortParsingBusyThreads|Subprocesos: subprocesos ocupados en análisis cortos|Recuento|Media|Número de subprocesos ocupados en hello grupo de subprocesos de análisis corto.|
|ShortParsingIdleThreads|Subprocesos: subprocesos inactivos en análisis cortos|Recuento|Media|Número de subprocesos inactivos en hello grupo de subprocesos de análisis corto.|
|ShortParsingJobQueueLength|Subprocesos: longitud de cola de trabajos en análisis cortos|Recuento|Media|Número de trabajos en cola de Hola de hello grupo de subprocesos de análisis corto.|
|memory_thrashing_metric|Paginación excesiva de memoria|Percent|Media|Paginación excesiva media de memoria.|

## <a name="microsoftapimanagementservice"></a>Microsoft.ApiManagement/service

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Descripción|
|---|---|---|---|---|
|TotalRequests|Solicitudes de puerta de enlace en total|Recuento|Total|Número de solicitudes de puerta de enlace|
|SuccessfulRequests|Solicitudes de puerta de enlace correctas|Recuento|Total|Número de solicitudes de puerta de enlace correctas|
|UnauthorizedRequests|Solicitudes de puerta de enlace no autorizadas|Recuento|Total|Número de solicitudes de puerta de enlace no autorizadas|
|FailedRequests|Solicitudes de puerta de enlace con error|Recuento|Total|Número de errores en solicitudes de puerta de enlace|
|OtherRequests|Otras solicitudes de puerta de enlace|Recuento|Total|Número de otras solicitudes de puerta de enlace|

## <a name="microsoftbatchbatchaccounts"></a>Microsoft.Batch/batchAccounts

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Description|
|---|---|---|---|---|
|CoreCount|Recuento de núcleos dedicados|Recuento|Total|Número total de núcleos dedicados en la cuenta de lote de Hola|
|TotalNodeCount|Recuento de nodos dedicados|Recuento|Total|Número total de nodos dedicados en la cuenta de lote de Hola|
|LowPriorityCoreCount|Recuento de núcleos de baja prioridad|Recuento|Total|Número total de núcleos de prioridad baja en la cuenta de lote de Hola|
|TotalLowPriorityNodeCount|Recuento de nodos de baja prioridad|Recuento|Total|Número total de nodos de prioridad baja en la cuenta de lote de Hola|
|CreatingNodeCount|Recuento de nodos creados|Recuento|Total|Número de nodos que se van a crear|
|StartingNodeCount|Recuento de nodos de inicio|Recuento|Total|Número de nodos que se van a iniciar|
|WaitingForStartTaskNodeCount|Recuento de nodos esperando a la tarea de inicio|Recuento|Total|Número de nodos esperando Hola Iniciar tarea toocomplete|
|StartTaskFailedNodeCount|Recuento de nodos con error de la tarea de inicio|Recuento|Total|Número de nodos que ha fallado Hola Iniciar tarea|
|IdleNodeCount|Recuento de nodos inactivos|Recuento|Total|Número de nodos inactivos|
|OfflineNodeCount|Recuento de nodos sin conexión|Recuento|Total|Número de nodos sin conexión|
|RebootingNodeCount|Recuento de nodos de reinicio|Recuento|Total|Número de nodos de reinicio|
|ReimagingNodeCount|Recuento de nodos de restablecimiento de imagen inicial|Recuento|Total|Número de nodos de restablecimiento de imagen inicial|
|RunningNodeCount|Recuento de nodos en ejecución|Recuento|Total|Número de nodos en ejecución|
|LeavingPoolNodeCount|Recuento de nodos que salen del grupo|Recuento|Total|Número de nodos dejando Hola grupo|
|UnusableNodeCount|Recuento de nodos no utilizables|Recuento|Total|Número de nodos inutilizables|
|PreemptedNodeCount|Recuento de nodos con prioridad|Recuento|Total|Número de nodos con prioridad|
|TaskStartEvent|Eventos de inicio de tarea|Recuento|Total|Número total de tareas que se han iniciado|
|TaskCompleteEvent|Eventos de tarea completada|Recuento|Total|Número total de tareas que se han completado|
|TaskFailEvent|Eventos de error en tareas|Recuento|Total|Número total de tareas que se han completado con errores|
|PoolCreateEvent|Eventos de creación de grupo|Recuento|Total|Número total de grupos que se han creado|
|PoolResizeStartEvent|Eventos de inicio de cambio de tamaño de grupo|Recuento|Total|Número total de cambios de tamaño de grupo que se han iniciado|
|PoolResizeCompleteEvent|Eventos de finalización de cambio de tamaño de grupo|Recuento|Total|Número total de cambios de tamaño de grupo completados|
|PoolDeleteStartEvent|Eventos de inicio de eliminación de grupo|Recuento|Total|Número total de eliminaciones de grupo que se han iniciado|
|PoolDeleteCompleteEvent|Eventos de finalización de eliminaciones de grupo|Recuento|Total|Número total de eliminaciones de grupo que se han completado|

## <a name="microsoftcacheredis"></a>Microsoft.Cache/redis

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Description|
|---|---|---|---|---|
|connectedclients|Clientes conectados|Recuento|Máxima||
|totalcommandsprocessed|Total de operaciones|Recuento|Total||
|cachehits|Aciertos de caché|Recuento|Total||
|cachemisses|Errores de caché|Recuento|Total||
|getcommands|Gets|Recuento|Total||
|setcommands|Sets|Recuento|Total||
|evictedkeys|Claves expulsadas|Recuento|Total||
|totalkeys|Total de claves|Recuento|Máxima||
|expiredkeys|Claves expiradas|Recuento|Total||
|usedmemory|Memoria usada|Bytes|Máxima||
|usedmemoryRss|Memoria RSS usada|Bytes|Máxima||
|serverLoad|Carga de servidor|Percent|Máxima||
|cacheWrite|Escritura de caché|BytesPerSecond|Máxima||
|cacheRead|Lectura de caché|BytesPerSecond|Máxima||
|percentProcessorTime|CPU|Percent|Máxima||
|connectedclients0|Clientes conectados (partición 0)|Recuento|Máxima||
|totalcommandsprocessed0|Total de operaciones (partición 0)|Recuento|Total||
|cachehits0|Aciertos de caché (partición 0)|Recuento|Total||
|cachemisses0|Errores de caché (partición 0)|Recuento|Total||
|getcommands0|Obtenciones (partición 0)|Recuento|Total||
|setcommands0|Definiciones (partición 0)|Recuento|Total||
|evictedkeys0|Claves expulsadas (partición 0)|Recuento|Total||
|totalkeys0|Total de claves (partición 0)|Recuento|Máxima||
|expiredkeys0|Claves expiradas (partición 0)|Recuento|Total||
|usedmemory0|Memoria usada (partición 0)|Bytes|Máxima||
|usedmemoryRss0|Memoria RSS usada (partición 0)|Bytes|Máxima||
|serverLoad0|Carga de servidor (partición 0)|Percent|Máxima||
|cacheWrite0|Escritura de caché (partición 0)|BytesPerSecond|Máxima||
|cacheRead0|Lectura de caché (partición 0)|BytesPerSecond|Máxima||
|percentProcessorTime0|CPU (partición 0)|Percent|Máxima||
|connectedclients1|Clientes conectados (partición 1)|Recuento|Máxima||
|totalcommandsprocessed1|Total de operaciones (partición 1)|Recuento|Total||
|cachehits1|Aciertos de caché (partición 1)|Recuento|Total||
|cachemisses1|Errores de caché (partición 1)|Recuento|Total||
|getcommands1|Obtenciones (partición 1)|Recuento|Total||
|setcommands1|Definiciones (partición 1)|Recuento|Total||
|evictedkeys1|Claves expulsadas (partición 1)|Recuento|Total||
|totalkeys1|Total de claves (partición 1)|Recuento|Máxima||
|expiredkeys1|Claves expiradas (partición 1)|Recuento|Total||
|usedmemory1|Memoria usada (partición 1)|Bytes|Máxima||
|usedmemoryRss1|Memoria RSS usada (partición 1)|Bytes|Máxima||
|serverLoad1|Carga de servidor (partición 1)|Percent|Máxima||
|cacheWrite1|Escritura de caché (partición 1)|BytesPerSecond|Máxima||
|cacheRead1|Lectura de caché (partición 1)|BytesPerSecond|Máxima||
|percentProcessorTime1|CPU (partición 1)|Percent|Máxima||
|connectedclients2|Clientes conectados (partición 2)|Recuento|Máxima||
|totalcommandsprocessed2|Total de operaciones (partición 2)|Recuento|Total||
|cachehits2|Aciertos de caché (partición 2)|Recuento|Total||
|cachemisses2|Errores de caché (partición 2)|Recuento|Total||
|getcommands2|Obtenciones (partición 2)|Recuento|Total||
|setcommands2|Definiciones (partición 2)|Recuento|Total||
|evictedkeys2|Claves expulsadas (partición 2)|Recuento|Total||
|totalkeys2|Total de claves (partición 2)|Recuento|Máxima||
|expiredkeys2|Claves expiradas (partición 2)|Recuento|Total||
|usedmemory2|Memoria usada (partición 2)|Bytes|Máxima||
|usedmemoryRss2|Memoria RSS usada (partición 2)|Bytes|Máxima||
|serverLoad2|Carga de servidor (partición 2)|Percent|Máxima||
|cacheWrite2|Escritura de caché (partición 2)|BytesPerSecond|Máxima||
|cacheRead2|Lectura de caché (partición 2)|BytesPerSecond|Máxima||
|percentProcessorTime2|CPU (partición 2)|Percent|Máxima||
|connectedclients3|Clientes conectados (partición 3)|Recuento|Máxima||
|totalcommandsprocessed3|Total de operaciones (partición 3)|Recuento|Total||
|cachehits3|Aciertos de caché (partición 3)|Recuento|Total||
|cachemisses3|Errores de caché (partición 3)|Recuento|Total||
|getcommands3|Obtenciones (partición 3)|Recuento|Total||
|setcommands3|Definiciones (partición 3)|Recuento|Total||
|evictedkeys3|Claves expulsadas (partición 3)|Recuento|Total||
|totalkeys3|Total de claves (partición 3)|Recuento|Máxima||
|expiredkeys3|Claves expiradas (partición 3)|Recuento|Total||
|usedmemory3|Memoria usada (partición 3)|Bytes|Máxima||
|usedmemoryRss3|Memoria RSS usada (partición 3)|Bytes|Máxima||
|serverLoad3|Carga de servidor (partición 3)|Percent|Máxima||
|cacheWrite3|Escritura de caché (partición 3)|BytesPerSecond|Máxima||
|cacheRead3|Lectura de caché (partición 3)|BytesPerSecond|Máxima||
|percentProcessorTime3|CPU (partición 3)|Percent|Máxima||
|connectedclients4|Clientes conectados (partición 4)|Recuento|Máxima||
|totalcommandsprocessed4|Total de operaciones (partición 4)|Recuento|Total||
|cachehits4|Aciertos de caché (partición 4)|Recuento|Total||
|cachemisses4|Errores de caché (partición 4)|Recuento|Total||
|getcommands4|Obtenciones (partición 4)|Recuento|Total||
|setcommands4|Definiciones (partición 4)|Recuento|Total||
|evictedkeys4|Claves expulsadas (partición 4)|Recuento|Total||
|totalkeys4|Total de claves (partición 4)|Recuento|Máxima||
|expiredkeys4|Claves expiradas (partición 4)|Recuento|Total||
|usedmemory4|Memoria usada (partición 4)|Bytes|Máxima||
|usedmemoryRss4|Memoria RSS usada (partición 4)|Bytes|Máxima||
|serverLoad4|Carga de servidor (partición 4)|Percent|Máxima||
|cacheWrite4|Escritura de caché (partición 4)|BytesPerSecond|Máxima||
|cacheRead4|Lectura de caché (partición 4)|BytesPerSecond|Máxima||
|percentProcessorTime4|CPU (partición 4)|Percent|Máxima||
|connectedclients5|Clientes conectados (partición 5)|Recuento|Máxima||
|totalcommandsprocessed5|Total de operaciones (partición 5)|Recuento|Total||
|cachehits5|Aciertos de caché (partición 5)|Recuento|Total||
|cachemisses5|Errores de caché (partición 5)|Recuento|Total||
|getcommands5|Obtenciones (partición 5)|Recuento|Total||
|setcommands5|Definiciones (partición 5)|Recuento|Total||
|evictedkeys5|Claves expulsadas (partición 5)|Recuento|Total||
|totalkeys5|Total de claves (partición 5)|Recuento|Máxima||
|expiredkeys5|Claves expiradas (partición 5)|Recuento|Total||
|usedmemory5|Memoria usada (partición 5)|Bytes|Máxima||
|usedmemoryRss5|Memoria RSS usada (partición 5)|Bytes|Máxima||
|serverLoad5|Carga de servidor (partición 5)|Percent|Máxima||
|cacheWrite5|Escritura de caché (partición 5)|BytesPerSecond|Máxima||
|cacheRead5|Lectura de caché (partición 5)|BytesPerSecond|Máxima||
|percentProcessorTime5|CPU (partición 5)|Percent|Máxima||
|connectedclients6|Clientes conectados (partición 6)|Recuento|Máxima||
|totalcommandsprocessed6|Total de operaciones (partición 6)|Recuento|Total||
|cachehits6|Aciertos de caché (partición 6)|Recuento|Total||
|cachemisses6|Errores de caché (partición 6)|Recuento|Total||
|getcommands6|Obtenciones (partición 6)|Recuento|Total||
|setcommands6|Definiciones (partición 6)|Recuento|Total||
|evictedkeys6|Claves expulsadas (partición 6)|Recuento|Total||
|totalkeys6|Total de claves (partición 6)|Recuento|Máxima||
|expiredkeys6|Claves expiradas (partición 6)|Recuento|Total||
|usedmemory6|Memoria usada (partición 6)|Bytes|Máxima||
|usedmemoryRss6|Memoria RSS usada (partición 6)|Bytes|Máxima||
|serverLoad6|Carga de servidor (partición 6)|Percent|Máxima||
|cacheWrite6|Escritura de caché (partición 6)|BytesPerSecond|Máxima||
|cacheRead6|Lectura de caché (partición 6)|BytesPerSecond|Máxima||
|percentProcessorTime6|CPU (partición 6)|Percent|Máxima||
|connectedclients7|Clientes conectados (partición 7)|Recuento|Máxima||
|totalcommandsprocessed7|Total de operaciones (partición 7)|Recuento|Total||
|cachehits7|Aciertos de caché (partición 7)|Recuento|Total||
|cachemisses7|Errores de caché (partición 7)|Recuento|Total||
|getcommands7|Obtenciones (partición 7)|Recuento|Total||
|setcommands7|Definiciones (partición 7)|Recuento|Total||
|evictedkeys7|Claves expulsadas (partición 7)|Recuento|Total||
|totalkeys7|Total de claves (partición 7)|Recuento|Máxima||
|expiredkeys7|Claves expiradas (partición 7)|Recuento|Total||
|usedmemory7|Memoria usada (partición 7)|Bytes|Máxima||
|usedmemoryRss7|Memoria RSS usada (partición 7)|Bytes|Máxima||
|serverLoad7|Carga de servidor (partición 7)|Percent|Máxima||
|cacheWrite7|Escritura de caché (partición 7)|BytesPerSecond|Máxima||
|cacheRead7|Lectura de caché (partición 7)|BytesPerSecond|Máxima||
|percentProcessorTime7|CPU (partición 7)|Percent|Máxima||
|connectedclients8|Clientes conectados (partición 8)|Recuento|Máxima||
|totalcommandsprocessed8|Total de operaciones (partición 8)|Recuento|Total||
|cachehits8|Aciertos de caché (partición 8)|Recuento|Total||
|cachemisses8|Errores de caché (partición 8)|Recuento|Total||
|getcommands8|Obtenciones (partición 8)|Recuento|Total||
|setcommands8|Definiciones (partición 8)|Recuento|Total||
|evictedkeys8|Claves expulsadas (partición 8)|Recuento|Total||
|totalkeys8|Total de claves (partición 8)|Recuento|Máxima||
|expiredkeys8|Claves expiradas (partición 8)|Recuento|Total||
|usedmemory8|Memoria usada (partición 8)|Bytes|Máxima||
|usedmemoryRss8|Memoria RSS usada (partición 8)|Bytes|Máxima||
|serverLoad8|Carga de servidor (partición 8)|Percent|Máxima||
|cacheWrite8|Escritura de caché (partición 8)|BytesPerSecond|Máxima||
|cacheRead8|Lectura de caché (partición 8)|BytesPerSecond|Máxima||
|percentProcessorTime8|CPU (partición 8)|Percent|Máxima||
|connectedclients9|Clientes conectados (partición 9)|Recuento|Máxima||
|totalcommandsprocessed9|Total de operaciones (partición 9)|Recuento|Total||
|cachehits9|Aciertos de caché (partición 9)|Recuento|Total||
|cachemisses9|Errores de caché (partición 9)|Recuento|Total||
|getcommands9|Obtenciones (partición 9)|Recuento|Total||
|setcommands9|Definiciones (partición 9)|Recuento|Total||
|evictedkeys9|Claves expulsadas (partición 9)|Recuento|Total||
|totalkeys9|Total de claves (partición 9)|Recuento|Máxima||
|expiredkeys9|Claves expiradas (partición 9)|Recuento|Total||
|usedmemory9|Memoria usada (partición 9)|Bytes|Máxima||
|usedmemoryRss9|Memoria RSS usada (partición 9)|Bytes|Máxima||
|serverLoad9|Carga de servidor (partición 9)|Percent|Máxima||
|cacheWrite9|Escritura de caché (partición 9)|BytesPerSecond|Máxima||
|cacheRead9|Lectura de caché (partición 9)|BytesPerSecond|Máxima||
|percentProcessorTime9|CPU (partición 9)|Percent|Máxima||

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.CognitiveServices/accounts

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Descripción|
|---|---|---|---|---|
|TotalCalls|Total de llamadas|Recuento|Total|Número total de llamadas.|
|SuccessfulCalls|Llamadas correctas|Recuento|Total|Número de llamadas correctas.|
|TotalErrors|Total de errores|Recuento|Total|Número total de llamadas con respuesta de error (código de respuesta HTTP 4xx o 5xx).|
|BlockedCalls|Llamadas bloqueadas|Recuento|Total|Número de llamadas que han superado la tasa o el límite de cuota.|
|ServerErrors|Errores del servidor|Recuento|Total|Número de llamadas con error interno del servicio (código de respuesta HTTP 5xx).|
|ClientErrors|Errores de cliente|Recuento|Total|Número de llamadas con error interno del lado cliente (código de respuesta HTTP 4xx).|
|DataIn|Entrada de datos|Bytes|Total|Tamaño de los datos de entrada en bytes.|
|DataOut|Salida de datos|Bytes|Total|Tamaño de los datos de salida en bytes.|
|Latency|Latency|MilliSeconds|Media|Latencia en milisegundos.|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.Compute/virtualMachines

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Description|
|---|---|---|---|---|
|Percentage CPU|Porcentaje de CPU|Percent|Media|porcentaje de Hola de unidades de proceso asignados que están actualmente en uso por hello máquinas virtuales|
|Red interna|Red interna|Bytes|Total|número de Hola de bytes recibidos en todas las interfaces de red por hello máquinas virtuales (tráfico entrante)|
|Red interna|Red interna|Bytes|Total|número de Hola de bytes en todas las interfaces de red por hello máquinas virtuales (tráfico saliente)|
|Bytes de lectura de disco|Bytes de lectura de disco|Bytes|Total|Número total de bytes que se leen desde el disco durante el período de supervisión|
|Bytes de escritura de disco|Bytes de escritura de disco|Bytes|Total|Número total de bytes escrito toodisk durante el período de supervisión|
|Operaciones de lectura de disco por segundo|Operaciones de lectura de disco por segundo|CountPerSecond|Media|E/S por segundo de lectura de disco|
|Disk Write Operations/Sec|Operaciones de escritura por segundo en disco|CountPerSecond|Media|E/S por segundo de escritura en disco|

## <a name="microsoftcomputevirtualmachinescalesets"></a>Microsoft.Compute/virtualMachineScaleSets

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Description|
|---|---|---|---|---|
|Percentage CPU|Porcentaje de CPU|Percent|Media|porcentaje de Hola de unidades de proceso asignados que están actualmente en uso por hello máquinas virtuales|
|Red interna|Red interna|Bytes|Total|número de Hola de bytes recibidos en todas las interfaces de red por hello máquinas virtuales (tráfico entrante)|
|Red interna|Red interna|Bytes|Total|número de Hola de bytes en todas las interfaces de red por hello máquinas virtuales (tráfico saliente)|
|Bytes de lectura de disco|Bytes de lectura de disco|Bytes|Total|Número total de bytes que se leen desde el disco durante el período de supervisión|
|Bytes de escritura de disco|Bytes de escritura de disco|Bytes|Total|Número total de bytes escrito toodisk durante el período de supervisión|
|Operaciones de lectura de disco por segundo|Operaciones de lectura de disco por segundo|CountPerSecond|Media|E/S por segundo de lectura de disco|
|Disk Write Operations/Sec|Operaciones de escritura por segundo en disco|CountPerSecond|Media|E/S por segundo de escritura en disco|

## <a name="microsoftcomputevirtualmachinescalesetsvirtualmachines"></a>Microsoft.Compute/virtualMachineScaleSets/virtualMachines

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Description|
|---|---|---|---|---|
|Percentage CPU|Porcentaje de CPU|Percent|Media|porcentaje de Hola de unidades de proceso asignados que están actualmente en uso por hello máquinas virtuales|
|Red interna|Red interna|Bytes|Total|número de Hola de bytes recibidos en todas las interfaces de red por hello máquinas virtuales (tráfico entrante)|
|Red interna|Red interna|Bytes|Total|número de Hola de bytes en todas las interfaces de red por hello máquinas virtuales (tráfico saliente)|
|Bytes de lectura de disco|Bytes de lectura de disco|Bytes|Total|Número total de bytes que se leen desde el disco durante el período de supervisión|
|Bytes de escritura de disco|Bytes de escritura de disco|Bytes|Total|Número total de bytes escrito toodisk durante el período de supervisión|
|Operaciones de lectura de disco por segundo|Operaciones de lectura de disco por segundo|CountPerSecond|Media|E/S por segundo de lectura de disco|
|Disk Write Operations/Sec|Operaciones de escritura por segundo en disco|CountPerSecond|Media|E/S por segundo de escritura en disco|

## <a name="microsoftcustomerinsightshubs"></a>Microsoft.CustomerInsights/hubs

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Descripción|
|---|---|---|---|---|
|DCIApiCalls|Llamadas API Customer Insights|Recuento|Total||
|DCIMappingImportOperationSuccessfulLines|Líneas correctas de la operación de importación de asignaciones|Recuento|Total||
|DCIMappingImportOperationFailedLines|Líneas con error de la operación de importación de asignaciones|Recuento|Total||
|DCIMappingImportOperationTotalLines|Líneas totales de la operación de importación de asignaciones|Recuento|Total||
|DCIMappingImportOperationRuntimeInSeconds|Tiempo de ejecución en segundos de la operación de importación de asignaciones|Segundos|Total||
|DCIOutboundProfileExportSucceeded|Exportación correcta del perfil saliente|Recuento|Total||
|DCIOutboundProfileExportFailed|Error de exportación del perfil saliente|Recuento|Total||
|DCIOutboundProfileExportDuration|Duración de la exportación del perfil saliente|Segundos|Total||
|DCIOutboundKpiExportSucceeded|Exportación correcta de KPI saliente|Recuento|Total||
|DCIOutboundKpiExportFailed|Error de exportación de KPI saliente|Recuento|Total||
|DCIOutboundKpiExportDuration|Duración de exportación de KPI saliente|Segundos|Total||
|DCIOutboundKpiExportStarted|Inicio de exportación de KPI saliente|Segundos|Total||
|DCIOutboundKpiRecordCount|Recuento de registros de KPI saliente|Segundos|Total||
|DCIOutboundProfileExportCount|Recuento de exportación de perfil saliente|Segundos|Total||
|DCIOutboundInitialProfileExportFailed|Recuento de exportación de perfil inicial saliente|Segundos|Total||
|DCIOutboundInitialProfileExportSucceeded|Exportación correcta de perfil inicial saliente|Segundos|Total||
|DCIOutboundInitialKpiExportFailed|Error de exportación de KPI inicial saliente|Segundos|Total||
|DCIOutboundInitialKpiExportSucceeded|Exportación correcta de KPI inicial saliente|Segundos|Total||
|DCIOutboundInitialProfileExportDurationInSeconds|Duración en segundos de exportación de perfil inicial saliente|Segundos|Total||
|AdlaJobForStandardKpiFailed|Error en segundos de trabajo de Adla para KPI estándar|Segundos|Total||
|AdlaJobForStandardKpiTimeOut|Tiempo de espera en segundos del trabajo de Adla para KPI estándar|Segundos|Total||
|AdlaJobForStandardKpiCompleted|Tiempo de finalización en segundos del trabajo de Adla para KPI estándar|Segundos|Total||
|ImportASAValuesFailed|Error de recuento de valores ASA de importación|Recuento|Total||
|ImportASAValuesSucceeded|Recuento correcto de valores ASA de importación|Recuento|Total||

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.DataLakeAnalytics/accounts

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Descripción|
|---|---|---|---|---|
|JobEndedSuccess|Trabajos correctos|Recuento|Total|Recuento de trabajos realizados correctamente|
|JobEndedFailure|Trabajos con error|Recuento|Total|Recuento de trabajos con error|
|JobEndedCancelled|Trabajos cancelados|Recuento|Total|Recuento de trabajos cancelados|
|JobAUEndedSuccess|Tiempo AU correcto|Segundos|Total|Tiempo total AU para trabajos realizados correctamente|
|JobAUEndedFailure|Error de tiempo AU|Segundos|Total|Tiempo total AU para trabajos con error|
|JobAUEndedCancelled|Tiempo AU para cancelados|Segundos|Total|Tiempo total AU para trabajos cancelados|

## <a name="microsoftdbformysqlservers"></a>Microsoft.DBforMySQL/servers

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Description|
|---|---|---|---|---|
|cpu_percent|Porcentaje de CPU|Percent|Media|Porcentaje de CPU|
|compute_limit|Límite de unidad de proceso|Recuento|Media|Límite de unidad de proceso|
|compute_consumption_percent|Porcentaje de unidad de proceso|Percent|Media|Porcentaje de unidad de proceso|
|memory_percent|Porcentaje de memoria|Percent|Media|Porcentaje de memoria|
|io_consumption_percent|Porcentaje de E/S|Percent|Media|Porcentaje de E/S|
|storage_percent|Porcentaje de almacenamiento|Percent|Media|Porcentaje de almacenamiento|
|storage_used|Almacenamiento utilizado|Bytes|Media|Almacenamiento utilizado|
|storage_limit|Límite de almacenamiento|Bytes|Media|Límite de almacenamiento|
|active_connections|Conexiones activas totales|Recuento|Media|Conexiones activas totales|
|connections_failed|Conexiones con errores totales|Recuento|Media|Conexiones con errores totales|

## <a name="microsoftdbforpostgresqlservers"></a>Microsoft.DBforPostgreSQL/servers

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Description|
|---|---|---|---|---|
|cpu_percent|Porcentaje de CPU|Percent|Media|Porcentaje de CPU|
|compute_limit|Límite de unidad de proceso|Recuento|Media|Límite de unidad de proceso|
|compute_consumption_percent|Porcentaje de unidad de proceso|Percent|Media|Porcentaje de unidad de proceso|
|memory_percent|Porcentaje de memoria|Percent|Media|Porcentaje de memoria|
|io_consumption_percent|Porcentaje de E/S|Percent|Media|Porcentaje de E/S|
|storage_percent|Porcentaje de almacenamiento|Percent|Media|Porcentaje de almacenamiento|
|storage_used|Almacenamiento utilizado|Bytes|Media|Almacenamiento utilizado|
|storage_limit|Límite de almacenamiento|Bytes|Media|Límite de almacenamiento|
|active_connections|Conexiones activas totales|Recuento|Media|Conexiones activas totales|
|connections_failed|Conexiones con errores totales|Recuento|Media|Conexiones con errores totales|

## <a name="microsoftdevicesiothubs"></a>Microsoft.Devices/IotHubs

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Description|
|---|---|---|---|---|
|d2c.telemetry.ingress.allProtocol|Intentos de envío de mensajes de telemetría|Recuento|Total|Número de toobe intento de telemetría de dispositivo para la nube mensajes enviados tooyour centro de IoT|
|d2c.telemetry.ingress.success|Mensajes de telemetría enviados|Recuento|Total|Número de mensajes de telemetría de dispositivo para la nube enviado correctamente el centro de IoT tooyour|
|c2d.commands.egress.complete.success|Comandos completados|Recuento|Total|Número de comandos en la nube al dispositivo que se completó correctamente por dispositivo de Hola|
|c2d.commands.egress.abandon.success|Comandos abandonados|Recuento|Total|Número de comandos en la nube al dispositivo abandonados por el dispositivo de Hola|
|c2d.commands.egress.reject.success|Comandos rechazados|Recuento|Total|Número de comandos en la nube al dispositivo rechazado por dispositivo de Hola|
|devices.totalDevices|Número total de dispositivos|Recuento|Total|Número de dispositivos registrados tooyour centro de IoT|
|devices.connectedDevices.allProtocol|Dispositivos conectados|Recuento|Total|Centro de IoT tooyour el número de dispositivos conectados|
|d2c.telemetry.egress.success|Mensajes de telemetría entregados|Recuento|Total|Número de veces que los mensajes se han escrito correctamente tooendpoints (total)|
|d2c.telemetry.egress.dropped|Mensajes descartados|Recuento|Total|Número de mensajes descartados porque el punto de conexión de hello entrega estaba inactivo|
|d2c.telemetry.egress.orphaned|Mensajes huérfanos|Recuento|Total|recuento de Hola de mensajes no coincide con ninguna ruta incluida la ruta de reserva de Hola|
|d2c.telemetry.egress.invalid|Mensajes no válidos|Recuento|Total|Hello número de mensajes no entregados debido tooincompatibility con punto de conexión de Hola|
|d2c.telemetry.egress.fallback|Mensajes que coinciden con la condición de reserva|Recuento|Total|Número de mensajes enviados de extremo de reserva toohello|
|d2c.endpoints.egress.eventHubs|Mensajes entregan tooEvent los extremos del centro|Recuento|Total|Número de veces que los mensajes se trataban tooEvent escrito correctamente los extremos del centro|
|d2c.endpoints.latency.eventHubs|Latencia de mensajes para los puntos de conexión del Centro de eventos|Milisegundos|Media|Hola promedio de latencia entre la entrada de mensaje y el centro de IoT toohello de mensaje de entrada en un punto de conexión de concentrador de eventos, en milisegundos|
|d2c.endpoints.egress.serviceBusQueues|Mensajes entregan tooService puntos de conexión de la cola de Bus|Recuento|Total|Número de veces mensajes se trataban como puntos de conexión de la cola de Bus tooService escrito correctamente|
|d2c.endpoints.latency.serviceBusQueues|Latencia de mensajes para los puntos de conexión de la cola de Service Bus|Milisegundos|Media|Hola promedio de latencia entre la entrada de mensaje y el centro de IoT toohello de mensaje de entrada en un punto de conexión de la cola de Bus de servicio, en milisegundos|
|d2c.endpoints.egress.serviceBusTopics|Mensajes entregan tooService puntos de conexión de tema de Bus|Recuento|Total|Número de veces mensajes se trataban como puntos de conexión de tema de Bus tooService escrito correctamente|
|d2c.endpoints.latency.serviceBusTopics|Latencia de mensajes para los puntos de conexión del tema de Service Bus|Milisegundos|Media|Hola promedio de latencia entre la entrada de mensaje y el centro de IoT toohello de mensaje de entrada en un punto de conexión de tema de Bus de servicio, en milisegundos|
|d2c.endpoints.egress.builtIn.events|Mensajes entregados extremo predefinido toohello (mensajes y eventos)|Recuento|Total|Número de veces que los mensajes se trataban extremo predefinido toohello correctamente escrito (mensajes y eventos)|
|d2c.endpoints.latency.builtIn.events|Latencia de mensajes para punto de conexión Hola integrados (mensajes y eventos)|Milisegundos|Media|Hola promedio de latencia entre la entrada de mensaje y el centro de IoT de mensaje de entrada toohello en extremo predefinido hello (mensajes y eventos), en milisegundos |
|d2c.twin.read.success|Lecturas gemelas correctas de los dispositivos|Recuento|Total|recuento de Hola de correctamente todas las lecturas gemelos iniciadas por el dispositivo.|
|d2c.twin.read.failure|Lecturas gemelas con error de los dispositivos|Recuento|Total|recuento de Hola de todas las no pudo lecturas gemelos iniciadas por el dispositivo.|
|d2c.twin.read.size|Tamaño de la respuesta de las lecturas gemelas de dispositivos|Bytes|Media|promedio de Hello, min y max del todo correcta iniciadas por el dispositivo dos lecturas.|
|d2c.twin.update.success|Actualizaciones gemelas correctas de los dispositivos|Recuento|Total|recuento de Hola de correctamente todas las actualizaciones de gemelas iniciadas por el dispositivo.|
|d2c.twin.update.failure|Actualizaciones gemelas con error de los dispositivos|Recuento|Total|recuento de Hola de todas las actualizaciones de gemelas iniciadas por el dispositivo con error.|
|d2c.twin.update.size|Tamaño de las actualizaciones gemelas de los dispositivos|Bytes|Media|Hola average, min y el tamaño máximo de todos los correcta iniciadas por el dispositivo dos actualizaciones.|
|c2d.methods.success|Invocaciones correctas al método directo|Recuento|Total|recuento de Hola de correctamente todas las llamadas a métodos directas.|
|c2d.methods.failure|Invocaciones al método directo con error|Recuento|Total|recuento de Hola de todas las no pudo llamadas directas.|
|c2d.methods.requestSize|Tamaño de la solicitud de las invocaciones a métodos directos|Bytes|Media|Hola average, min y número máximo de solicitudes de método directo todas correctas.|
|c2d.methods.responseSize|Tamaño de la respuesta de las invocaciones a métodos directos|Bytes|Media|promedio de Hello, min y max de todas las respuestas de método directo correcta.|
|c2d.twin.read.success|Lecturas gemelas correctas del back-end|Recuento|Total|recuento de Hola de correctamente todas las lecturas gemelos iniciado por back-end.|
|c2d.twin.read.failure|Lecturas gemelas con error del back-end|Recuento|Total|recuento de Hola de todas las no pudo lecturas gemelos iniciado por back-end.|
|c2d.twin.read.size|Tamaño de la respuesta de las lecturas gemelas del back-end|Bytes|Media|promedio de Hello, min y max del todo correcta iniciadas por el back end dos lecturas.|
|c2d.twin.update.success|Actualizaciones gemelas correctas del back-end|Recuento|Total|recuento de Hola de correctamente todas las actualizaciones de gemelas iniciado por back-end.|
|c2d.twin.update.failure|Actualizaciones gemelas con error del back-end|Recuento|Total|recuento de Hola de todas las actualizaciones de gemelas iniciado por back-end con error.|
|c2d.twin.update.size|Tamaño de las actualizaciones gemelas del back-end|Bytes|Media|Hola average, min y tamaño máximo de todos los correcta iniciadas por el back end dos actualizaciones.|
|twinQueries.success|Consultas gemelas correctas|Recuento|Total|recuento de Hola de todas las consultas de gemelas correcta.|
|twinQueries.failure|Consultas gemelas con error|Recuento|Total|recuento de Hola de todas las consultas de dos errores.|
|twinQueries.resultSize|Tamaño de resultado de consultas gemelas|Bytes|Media|Hola average, min y máximo de tamaño de los resultados de todas las consultas de gemelas correcta Hola.|
|jobs.createTwinUpdateJob.success|Creaciones correctas de trabajos de actualización gemelos|Recuento|Total|recuento de Hola de toda la creación correcta de los trabajos de actualización gemelas.|
|jobs.createTwinUpdateJob.failure|Creaciones con error de trabajos de actualización gemelos|Recuento|Total|recuento de Hola de todos los error en la creación de trabajos de actualización de gemelas.|
|jobs.createDirectMethodJob.success|Creaciones correctas de trabajos de invocación de método|Recuento|Total|recuento de Hola de toda la creación correcta de los trabajos de invocación de método directo.|
|jobs.createDirectMethodJob.failure|Creaciones con error de trabajos de invocación de método|Recuento|Total|recuento de Hola de todos los error en la creación de trabajos de invocación de método directo.|
|jobs.listJobs.success|Trabajos de toolist de llamadas correctas|Recuento|Total|recuento de Hola de todos los trabajos de toolist de llamadas correctas.|
|jobs.listJobs.failure|Errores llamadas toolist trabajos|Recuento|Total|recuento de Hola de todos los trabajos de toolist de errores de llamadas.|
|jobs.cancelJob.success|Cancelaciones de trabajos correctas|Recuento|Total|recuento de Hello correctos todas las llamadas a toocancel un trabajo.|
|jobs.cancelJob.failure|Cancelaciones de trabajos con error|Recuento|Total|recuento de Hola de todos los errores llamadas toocancel un trabajo.|
|jobs.queryJobs.success|Consultas de trabajo correctas|Recuento|Total|recuento de Hola de todos los trabajos de tooquery de llamadas correctas.|
|jobs.queryJobs.failure|Consultas de trabajo con error|Recuento|Total|recuento de Hola de todos los trabajos de tooquery de errores de llamadas.|
|jobs.completed|Trabajos completados|Recuento|Total|recuento de Hola de todos los trabajos completados.|
|jobs.failed|Trabajos con error|Recuento|Total|recuento de Hola de todos los trabajos con errores.|
|d2c.telemetry.ingress.sendThrottle|Número de errores de limitación|Recuento|Total|Número de errores de limitación debido a limitaciones de rendimiento toodevice|
|dailyMessageQuotaUsed|Número total de mensajes usados|Recuento|Media|Número de mensajes totales usados hoy|

## <a name="microsofteventhubnamespaces"></a>Microsoft.EventHub/namespaces

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Description|
|---|---|---|---|---|
|INREQS|Solicitudes de envío entrantes|Recuento|Total|Solicitudes de envío entrantes totales de un centro de notificaciones|
|SUCCREQ|Solicitudes correctas|Recuento|Total|Número total de solicitudes correctas para un espacio de nombres|
|FAILREQ|Solicitudes con error|Recuento|Total|Número total de solicitudes erróneas para un espacio de nombres|
|SVRBSY|Errores de servidor ocupado|Recuento|Total|Errores totales de servidor ocupado para un espacio de nombres|
|INTERR|Errores internos del servidor|Recuento|Total|Errores totales de servidor interno para un espacio de nombres|
|MISCERR|Otros errores|Recuento|Total|Número total de solicitudes erróneas para un espacio de nombres|
|INMSGS|Mensajes entrantes|Recuento|Total|Total de mensajes entrantes para un espacio de nombres|
|OUTMSGS|Mensajes salientes|Recuento|Total|Total de mensajes salientes para un espacio de nombres|
|EHINMBS|Bytes de entrada|Bytes|Total|Rendimiento de mensajes entrantes del centro de eventos para un espacio de nombres|
|EHOUTMBS|Bytes de salida|Bytes|Total|Total de mensajes salientes para un espacio de nombres|
|EHABL|Mensajes de trabajo pendiente de archivado|Recuento|Total|Mensajes de archivo del centro de eventos en el trabajo pendiente para un espacio de nombres|
|EHAMSGS|Mensajes de archivado|Recuento|Total|Mensajes archivados del centro de eventos en un espacio de nombres|
|EHAMBS|Rendimiento de mensajes de archivado|Bytes|Total|Rendimiento de mensajes archivados del centro de eventos en un espacio de nombres|

## <a name="microsoftlogicworkflows"></a>Microsoft.Logic/workflows

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Description|
|---|---|---|---|---|
|RunsStarted|Ejecuciones iniciadas|Recuento|Total|Número de ejecuciones de flujo de trabajo iniciadas|
|RunsCompleted|Ejecuciones completadas|Recuento|Total|Número de ejecuciones de flujo de trabajo completadas|
|RunsSucceeded|Ejecuciones correctas|Recuento|Total|Número de ejecuciones de flujo de trabajo correctas|
|RunsFailed|Ejecuciones con errores|Recuento|Total|Número de ejecuciones de flujo de trabajo con errores|
|RunsCancelled|Ejecuciones canceladas|Recuento|Total|Número de ejecuciones de flujo de trabajo canceladas|
|RunLatency|Latencia de ejecución|Segundos|Media|Latencia de ejecuciones de flujo de trabajo completadas|
|RunSuccessLatency|Latencia de ejecuciones correctas|Segundos|Media|Latencia de ejecuciones de flujo de trabajo correctas|
|RunThrottledEvents|Ejecución de eventos limitados|Recuento|Total|Número de eventos limitados de desencadenador o acciones de flujo de trabajo|
|RunFailurePercentage|Porcentaje de errores de ejecución|Percent|Total|Porcentaje de ejecuciones de flujo de trabajo con errores.|
|ActionsStarted|Acciones iniciadas |Recuento|Total|Número de acciones de flujo de trabajo iniciadas|
|ActionsCompleted|Acciones completadas |Recuento|Total|Número de acciones de flujo de trabajo completadas|
|ActionsSucceeded|Acciones correctas |Recuento|Total|Número de acciones de flujo de trabajo correctas|
|ActionsFailed|Acciones con errores|Recuento|Total|Número de acciones de flujo de trabajo con errores|
|ActionsSkipped|Acciones omitidas |Recuento|Total|Número de acciones de flujo de trabajo omitidas|
|ActionLatency|Latencia de acciones |Segundos|Media|Latencia de acciones de flujo de trabajo completadas|
|ActionSuccessLatency|Latencia de acciones correctas |Segundos|Media|Latencia de acciones de flujo de trabajo correctas|
|ActionThrottledEvents|Eventos limitados de acciones|Recuento|Total|Número de eventos limitados de acciones de flujo de trabajo|
|TriggersStarted|Desencadenadores iniciados |Recuento|Total|Número de desencadenadores de flujo de trabajo iniciados|
|TriggersCompleted|Desencadenadores completados |Recuento|Total|Número de desencadenadores de flujo de trabajo completados|
|TriggersSucceeded|Desencadenadores correctos |Recuento|Total|Número de desencadenadores de flujo de trabajo correctos|
|TriggersFailed|Desencadenadores con errores |Recuento|Total|Número de desencadenadores de flujo de trabajo con errores|
|TriggersSkipped|Desencadenadores omitidos|Recuento|Total|Número de desencadenadores de flujo de trabajo omitidos|
|TriggersFired|Desencadenadores activados |Recuento|Total|Número de desencadenadores de flujo de trabajo activados|
|TriggerLatency|Latencia de desencadenador |Segundos|Media|Latencia de desencadenadores de flujo de trabajo completados|
|TriggerFireLatency|Latencia de desencadenador activado |Segundos|Media|Latencia de desencadenadores de flujo de trabajo activados|
|TriggerSuccessLatency|Latencia de desencadenadores correctos |Segundos|Media|Latencia de desencadenadores de flujo de trabajo correctos|
|TriggerThrottledEvents|Eventos limitados de desencadenadores|Recuento|Total|Número de eventos limitados de desencadenador de flujo de trabajo|
|BillableActionExecutions|Ejecuciones de acciones facturables|Recuento|Total|Número de ejecuciones de acciones de flujo de trabajo que se facturan.|
|BillableTriggerExecutions|Ejecuciones del desencadenador facturable|Recuento|Total|Número de ejecuciones del desencadenador de flujo de trabajo que se factura.|
|TotalBillableExecutions|Total de ejecuciones facturables|Recuento|Total|Número de ejecuciones de flujo de trabajo que se factura.|

## <a name="microsoftnetworkapplicationgateways"></a>Microsoft.Network/applicationGateways

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Description|
|---|---|---|---|---|
|Throughput|Rendimiento|BytesPerSecond|Media||

## <a name="microsoftnetworkexpressroutecircuits"></a>Microsoft.Network/expressRouteCircuits

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Descripción|
|---|---|---|---|---|
|BytesIn|BytesIn|Recuento|Total||
|BytesOut|BytesOut|Recuento|Total||

## <a name="microsoftnotificationhubsnamespacesnotificationhubs"></a>Microsoft.NotificationHubs/Namespaces/NotificationHubs

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Descripción|
|---|---|---|---|---|
|registration.all|Operación de registro|Recuento|Total|recuento de Hola de todas las operaciones de registro correctas (creaciones actualizaciones consultas y eliminaciones). |
|registration.create|Operaciones de creación de registros|Recuento|Total|recuento de Hola de todas las creaciones de registro correctas.|
|registration.update|Operaciones de actualización de registros|Recuento|Total|recuento de Hola de todas las actualizaciones de registro correctas.|
|registration.get|Operaciones de lectura de registros|Recuento|Total|recuento de Hola de todas las consultas de registro correctas.|
|registration.delete|Operaciones de eliminación de registros|Recuento|Total|recuento de Hola de todas las eliminaciones de registro correctas.|
|incoming|Mensajes entrantes|Recuento|Total|recuento de Hello del todo correcta enviar llamadas API. |
|incoming.scheduled|Notificaciones push programadas enviadas|Recuento|Total|Notificaciones push programadas canceladas|
|incoming.scheduled.cancel|Notificaciones push programadas canceladas|Recuento|Total|Notificaciones push programadas canceladas|
|scheduled.pending|Notificaciones programadas pendientes|Recuento|Total|Notificaciones programadas pendientes|
|installation.all|Operaciones de administración de instalaciones|Recuento|Total|Operaciones de administración de instalaciones|
|installation.get|Obtener operaciones de instalación|Recuento|Total|Obtener operaciones de instalación|
|installation.upsert|Crear o actualizar operaciones de instalación|Recuento|Total|Crear o actualizar operaciones de instalación|
|installation.patch|Aplicar revisión a operaciones de instalación|Recuento|Total|Aplicar revisión a operaciones de instalación|
|installation.delete|Eliminar operaciones de instalación|Recuento|Total|Eliminar operaciones de instalación|
|outgoing.allpns.success|Notificaciones correctas|Recuento|Total|recuento de Hola de todas las notificaciones correctas.|
|outgoing.allpns.invalidpayload|Errores de carga útil|Recuento|Total|recuento de Hola de inserciones que dieron error porque hello PNS devolvió un error de carga.|
|outgoing.allpns.pnserror|Errores del sistema de notificación externo|Recuento|Total|recuento de Hola de inserciones que dieron error porque se produjo un problema al comunicarse con hello PNS (excluye los problemas de autenticación).|
|outgoing.allpns.channelerror|Errores de canal|Recuento|Total|recuento de Hola de inserciones que dieron error porque el canal de hello no era válido no esté asociado a Hola correcta aplicación limitado o expirado.|
|outgoing.allpns.badorexpiredchannel|Errores de canal incorrecto o expirado|Recuento|Total|recuento de Hola de inserciones que dieron error porque Hola canal token o el identificador en el registro de hello ha expirado o no es válido.|
|outgoing.wns.success|Notificaciones de WNS correctas|Recuento|Total|recuento de Hola de todas las notificaciones correctas.|
|outgoing.wns.invalidcredentials|Errores de autorización de WNS (credenciales no válidas)|Recuento|Total|recuento de Hola de inserciones que dieron error porque hello PNS no aceptó Hola proporcionado credenciales u Hola están bloqueados. (Windows Live no reconoce las credenciales de hello).|
|outgoing.wns.badchannel|Error de canal incorrecto de WNS|Recuento|Total|Hola recuento de inserciones que dieron error porque no se reconoció Hola URI del canal en el registro de hello (estado de WNS: 404 no encontrado).|
|outgoing.wns.expiredchannel|Error de canal expirado de WNS|Recuento|Total|Hola recuento de inserciones que dieron error porque hello ChannelURI ha expirado (estado de WNS: 410 desaparecido).|
|outgoing.wns.throttled|Notificaciones limitadas de WNS|Recuento|Total|Hola recuento de inserciones que dieron error porque WNS está limitando esta aplicación (estado de WNS: 406 No aceptable).|
|outgoing.wns.tokenproviderunreachable|Errores de autorización de WNS (inaccesible)|Recuento|Total|No se puede acceder a Windows Live.|
|outgoing.wns.invalidtoken|Errores de autorización de WNS (token no válido)|Recuento|Total|Hello proporciona token tooWNS no es válido (estado de WNS: 401 no autorizado).|
|outgoing.wns.wrongtoken|Errores de autorización de WNS (token erróneo)|Recuento|Total|Hola token proporcionado por tooWNS es válido, pero para otra aplicación (estado de WNS: 403 Prohibido). Esto puede ocurrir si Hola URI del canal en el registro de hello está asociado a otra aplicación. Compruebe que esa aplicación de cliente hello está asociada con hello misma aplicación cuyas credenciales están en el centro de notificaciones de Hola.|
|outgoing.wns.invalidnotificationformat|Formato de notificación no válido de WNS|Recuento|Total|formato de Hola de notificación de hello no es válido (estado de WNS: 400). Tenga en cuenta que WNS no rechaza todas las cargas útiles no válidas.|
|outgoing.wns.invalidnotificationsize|Error de tamaño de notificación no válido de WNS|Recuento|Total|carga de notificaciones de Hello es demasiado grande (estado de WNS: 413).|
|outgoing.wns.channelthrottled|Canal de WNS limitado|Recuento|Total|Hola notificación se eliminó porque Hola URI del canal en el registro de hello está limitado (encabezado de respuesta WNS: X-WNS-Channelthrottled).|
|outgoing.wns.channeldisconnected|Canal de WNS desconectado|Recuento|Total|Hola notificación se eliminó porque Hola URI del canal en el registro de hello está limitado (encabezado de respuesta WNS: X-WNS-DeviceConnectionStatus: desconectado).|
|outgoing.wns.dropped|Notificaciones descartadas de WNS|Recuento|Total|Hola notificación se eliminó porque Hola URI del canal en el registro de hello está limitado (X-WNS-NotificationStatus: colocarlo pero no X-WNS-DeviceConnectionStatus: desconectado).|
|outgoing.wns.pnserror|Errores de WNS|Recuento|Total|La notificación no se entregó debido a errores de comunicación con WNS.|
|outgoing.wns.authenticationerror|Errores de autenticación de WNS|Recuento|Total|La notificación no se entregó debido a errores de comunicación con Windows Live, credenciales no válidas o token erróneo.|
|outgoing.apns.success|Notificaciones de APNS correctas|Recuento|Total|recuento de Hola de todas las notificaciones correctas.|
|outgoing.apns.invalidcredentials|Errores de autorización de APNS|Recuento|Total|recuento de Hola de inserciones que dieron error porque hello PNS no aceptó Hola proporcionado credenciales u Hola están bloqueados.|
|outgoing.apns.badchannel|Error de canal incorrecto de APNS|Recuento|Total|Hola recuento de inserciones que dieron error porque Hola token no es válido (código de estado APNS: 8).|
|outgoing.apns.expiredchannel|Error de canal expirado de APNS|Recuento|Total|recuento de Hola de tokens invalidados por canal de comentarios APNS Hola.|
|outgoing.apns.invalidnotificationsize|Error de tamaño de notificación no válido de APNS|Recuento|Total|Hola recuento de inserciones que dieron error porque Hola carga era demasiado grande (código de estado APNS: 7).|
|outgoing.apns.pnserror|Errores de APNS|Recuento|Total|recuento de Hola de inserciones que dieron error debido a errores de comunicación con APNS.|
|outgoing.gcm.success|Notificaciones de GCM correctas|Recuento|Total|recuento de Hola de todas las notificaciones correctas.|
|outgoing.gcm.invalidcredentials|Errores de autorización de GCM (credenciales no válidas)|Recuento|Total|recuento de Hola de inserciones que dieron error porque hello PNS no aceptó Hola proporcionado credenciales u Hola están bloqueados.|
|outgoing.gcm.badchannel|Error de canal incorrecto de GCM|Recuento|Total|Hola recuento de inserciones que dieron error porque no se reconoció el identificador hello registro de hello (resultado de GCM: registro no válido).|
|outgoing.gcm.expiredchannel|Error de canal expirado de GCM|Recuento|Total|Hola recuento de inserciones que dieron error porque el identificador hello registro de hello había expirado (resultado de GCM: no registrado).|
|outgoing.gcm.throttled|Notificaciones limitadas de GCM|Recuento|Total|Hola recuento de inserciones que dieron error porque GCM limitó esta aplicación (código de estado GCM: 501-599 o resultado: no disponible).|
|outgoing.gcm.invalidnotificationformat|Formato de notificación no válido de GCM|Recuento|Total|Hola recuento de inserciones que dieron error porque la carga de hello no tenía el formato correcto (resultado de GCM: InvalidDataKey o InvalidTtl).|
|outgoing.gcm.invalidnotificationsize|Error de tamaño de notificación no válido de GCM|Recuento|Total|Hola recuento de inserciones que dieron error porque Hola carga era demasiado grande (resultado de GCM: MessageTooBig).|
|outgoing.gcm.wrongchannel|Error de canal incorrecto de GCM|Recuento|Total|recuento de Hola de inserciones que dieron error porque no es el identificador hello registro de hello asociados toohello de aplicación actual (resultado de GCM: InvalidPackageName).|
|outgoing.gcm.pnserror|Errores de GCM|Recuento|Total|recuento de Hola de inserciones que dieron error debido a errores de comunicación con GCM.|
|outgoing.gcm.authenticationerror|Errores de autenticación de GCM|Recuento|Total|Hola recuento de inserciones que dieron error porque hello PNS no aceptó Hola proporcionado credenciales Hola credenciales están bloqueadas o hello Id. de remitente no está configurado correctamente en la aplicación hello (resultado de GCM: MismatchedSenderId).|
|outgoing.mpns.success|Notificaciones de MPNS correctas|Recuento|Total|recuento de Hola de todas las notificaciones correctas.|
|outgoing.mpns.invalidcredentials|Credenciales no válidas de MPNS|Recuento|Total|recuento de Hola de inserciones que dieron error porque hello PNS no aceptó Hola proporcionado credenciales u Hola están bloqueados.|
|outgoing.mpns.badchannel|Error de canal incorrecto de MPNS|Recuento|Total|Hola recuento de inserciones que dieron error porque no se reconoció Hola URI del canal en el registro de hello (estado de MPNS: 404 no encontrado).|
|outgoing.mpns.throttled|Notificaciones limitadas de MPNS|Recuento|Total|Hola recuento de inserciones que dieron error porque MPNS está limitando esta aplicación (WNS MPNS: 406 No aceptable).|
|outgoing.mpns.invalidnotificationformat|Formato de notificación no válido de MPNS|Recuento|Total|recuento de Hola de inserciones que dieron error porque la carga de Hola de notificación de hello era demasiado grande.|
|outgoing.mpns.channeldisconnected|Canal de MPNS desconectado|Recuento|Total|Hola recuento de inserciones que dieron error porque se desconectó Hola URI del canal en el registro de hello (estado de MPNS: 412 no encontrado).|
|outgoing.mpns.dropped|Notificaciones descartadas de MPNS|Recuento|Total|Hola recuento de inserciones que eliminó MPNS (encabezado de respuesta MPNS: X-NotificationStatus: QueueFull o Suppressed).|
|outgoing.mpns.pnserror|Errores de MPNS|Recuento|Total|recuento de Hola de inserciones que dieron error debido a errores de comunicación con MPNS.|
|outgoing.mpns.authenticationerror|Errores de autenticación de MPNS|Recuento|Total|recuento de Hola de inserciones que dieron error porque hello PNS no aceptó Hola proporcionado credenciales u Hola están bloqueados.|
|notificationhub.pushes|Todas las notificaciones salientes|Recuento|Total|Todas las notificaciones salientes de centro de notificaciones de Hola|
|incoming.all.requests|Todas las solicitudes entrantes|Recuento|Total|Solicitudes entrantes totales de un centro de notificaciones|
|incoming.all.failedrequests|Todas las solicitudes entrantes con error|Recuento|Total|Solicitudes entrantes totales con error de un centro de notificaciones|

## <a name="microsoftpowerbidedicatedcapacities"></a>Microsoft.PowerBIDedicated/capacities

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Descripción|
|---|---|---|---|---|
|qpu_metric|QPU|Recuento|Media|QPU. Intervalo de 0-100 para S1, 0-200 para S2 y 0-400 para S4|
|memory_metric|Memoria|Bytes|Media|Memoria. Intervalo de 0-25 GB para S1, 0-50 GB para S2 y 0-100 GB para S4|
|TotalConnectionRequests|Número total de solicitudes de conexión|Recuento|Media|Número total de solicitudes de conexión. Se trata de llegadas.|
|SuccessfullConnectionsPerSec|Conexiones correctas por segundo|CountPerSecond|Media|Tasa de finalizaciones de conexión correctas.|
|TotalConnectionFailures|Número total de errores de conexión|Recuento|Media|Número total de intentos de conexión con error.|
|CurrentUserSessions|Sesiones de usuario actuales|Recuento|Media|Número actual de sesiones de usuario establecidas.|
|QueryPoolBusyThreads|Subprocesos ocupados de grupo de consultas|Recuento|Media|Número de subprocesos ocupados en el grupo de subprocesos de consulta de Hola.|
|CommandPoolJobQueueLength|Longitud de cola de trabajos de grupo de comandos|Recuento|Media|Número de trabajos en cola de hello del grupo de subprocesos de comando de Hola.|
|ProcessingPoolJobQueueLength|Longitud de cola de trabajos de grupo de procesamiento|Recuento|Media|Número de trabajos no son de e/s en cola Hola de hello grupo de subprocesos de procesamiento.|
|CurrentConnections|Conexión: conexiones actuales|Recuento|Media|Número actual de conexiones de cliente establecidas.|
|CleanerCurrentPrice|Memoria: precio actual de limpieza|Recuento|Media|Precio actual de memoria, $/ byte/tiempo, normalizado too1000.|
|CleanerMemoryShrinkable|Memoria: memoria de limpieza reducible|Bytes|Media|Cantidad de memoria, en bytes, asunto toopurging limpiador en segundo plano Hola.|
|CleanerMemoryNonshrinkable|Memoria: memoria de limpieza no reducible|Bytes|Media|Cantidad de memoria, en bytes, no el asunto toopurging limpiador en segundo plano Hola.|
|MemoryUsage|Memoria: uso de memoria|Bytes|Media|Uso de memoria de proceso de servidor hello tal y como se usa para calcular el precio de memoria de limpiador. Toocounter igual Proceso\Bytes privados más hello de datos asignado a la memoria, se omite la memoria que se ha asignado por el motor de análisis en memoria de xVelocity (VertiPaq) de Hola que sobrepasen el motor xVelocity de hello límite de memoria.|
|MemoryLimitHard|Memoria: límite de memoria física|Bytes|Media|Límite de memoria física del archivo de configuración.|
|MemoryLimitHigh|Memoria: límite alto de memoria|Bytes|Media|Límite alto de memoria del archivo de configuración.|
|MemoryLimitLow|Memoria: límite bajo de memoria|Bytes|Media|Límite bajo de memoria del archivo de configuración.|
|MemoryLimitVertiPaq|Memoria: VertiPaq de límite de memoria|Bytes|Media|Límite en memoria del archivo de configuración.|
|Quota|Memoria: cuota|Bytes|Media|Cuota de memoria actual, en bytes. La cuota de memoria también se denomina concesión de memoria o reserva de memoria.|
|QuotaBlocked|Memoria: cuota bloqueada|Recuento|Media|Número actual de solicitudes de cuota que están bloqueadas hasta que se liberen otras cuotas de memoria.|
|VertiPaqNonpaged|Memoria: VertiPaq no paginado|Bytes|Media|Bytes de memoria bloqueada en espacio de trabajo de Hola para su uso por el motor de hello en memoria.|
|VertiPaqPaged|Memoria: VertiPaq paginado|Bytes|Media|Bytes de memoria paginada en uso para datos en memoria.|
|RowsReadPerSec|Procesamiento: filas leídas por segundo|CountPerSecond|Media|Velocidad de filas leídas de todas las bases de datos relacionales.|
|RowsConvertedPerSec|Procesamiento: filas convertidas por segundo|CountPerSecond|Media|Velocidad de filas convertidas durante el procesamiento.|
|RowsWrittenPerSec|Procesamiento: filas escritas por segundo|CountPerSecond|Media|Velocidad de filas escritas durante el procesamiento.|
|CommandPoolBusyThreads|Subprocesos: subprocesos ocupados del grupo de comandos|Recuento|Media|Número de subprocesos ocupados en el grupo de subprocesos de comando de Hola.|
|CommandPoolIdleThreads|Subprocesos: subprocesos inactivos del grupo de comandos|Recuento|Media|Número de subprocesos inactivos en el grupo de subprocesos de comando de Hola.|
|LongParsingBusyThreads|Subprocesos: subprocesos ocupados en análisis largos|Recuento|Media|Número de subprocesos ocupados en el grupo de subprocesos de análisis largo de Hola.|
|LongParsingIdleThreads|Subprocesos: subprocesos inactivos en análisis largos|Recuento|Media|Número de subprocesos inactivos en hello grupo de subprocesos de análisis largo.|
|LongParsingJobQueueLength|Subprocesos: longitud de cola de trabajos en análisis largos|Recuento|Media|Número de trabajos en cola de Hola de hello grupo de subprocesos de análisis largo.|
|ProcessingPoolBusyIOJobThreads|Subprocesos: subprocesos de trabajo de E/S ocupados del grupo de procesamiento|Recuento|Media|Número de subprocesos que se ejecutan trabajos de E/S en el grupo de subprocesos de procesamiento de Hola.|
|ProcessingPoolBusyNonIOThreads|Subprocesos: subprocesos de trabajo ocupados que no son de E/S del grupo de procesamiento|Recuento|Media|Número de subprocesos que se ejecutan los trabajos no son de e/s en el grupo de subprocesos de procesamiento de Hola.|
|ProcessingPoolIOJobQueueLength|Subprocesos: longitud de cola de trabajos de E/S del grupo de procesamiento|Recuento|Media|Número de trabajos de E/S en cola de hello del grupo de subprocesos de procesamiento de Hola.|
|ProcessingPoolIdleIOJobThreads|Subprocesos: subprocesos de trabajo de E/S inactivos del grupo de procesamiento|Recuento|Media|Número de subprocesos inactivos de trabajos de E/S en el grupo de subprocesos de procesamiento de Hola.|
|ProcessingPoolIdleNonIOThreads|Subprocesos: subprocesos de trabajo inactivos que no son de E/S del grupo de procesamiento|Recuento|Media|Número de subprocesos inactivos en el grupo de subprocesos de procesamiento de hello dedicado trabajos toonon de e/s.|
|QueryPoolIdleThreads|Subprocesos: subprocesos inactivos del grupo de consultas|Recuento|Media|Número de subprocesos inactivos de trabajos de E/S en el grupo de subprocesos de procesamiento de Hola.|
|QueryPoolJobQueueLength|Subprocesos: longitud de cola de trabajos del grupo de consultas|Recuento|Media|Número de trabajos en cola de hello del grupo de subprocesos de consulta de Hola.|
|ShortParsingBusyThreads|Subprocesos: subprocesos ocupados en análisis cortos|Recuento|Media|Número de subprocesos ocupados en hello grupo de subprocesos de análisis corto.|
|ShortParsingIdleThreads|Subprocesos: subprocesos inactivos en análisis cortos|Recuento|Media|Número de subprocesos inactivos en hello grupo de subprocesos de análisis corto.|
|ShortParsingJobQueueLength|Subprocesos: longitud de cola de trabajos en análisis cortos|Recuento|Media|Número de trabajos en cola de Hola de hello grupo de subprocesos de análisis corto.|
|memory_thrashing_metric|Paginación excesiva de memoria|Percent|Media|Paginación excesiva media de memoria.|

## <a name="microsoftsearchsearchservices"></a>Microsoft.Search/searchServices

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Descripción|
|---|---|---|---|---|
|SearchLatency|Latencia de búsqueda|Segundos|Media|Latencia promedio de búsqueda para el servicio de búsqueda de Hola|
|SearchQueriesPerSecond|Consultas de búsqueda por segundo|CountPerSecond|Media|Consultas de búsqueda por segundo para el servicio de búsqueda de Hola|
|ThrottledSearchQueriesPercentage|Porcentaje de consultas de búsqueda limitadas|Percent|Media|Porcentaje de consultas de búsqueda que se limitaran para servicio de búsqueda de Hola|

## <a name="microsoftservicebusnamespaces"></a>Microsoft.ServiceBus/namespaces

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Description|
|---|---|---|---|---|
|CPUXNS|Uso de CPU por espacio de nombres|Percent|Máxima|Métrica de uso de CPU de espacio de nombres premium de Service Bus|
|WSXNS|Uso de tamaño de memoria por espacio de nombres|Percent|Máxima|Métrica de uso de memoria de espacio de nombres premium de Service Bus|

## <a name="microsoftsqlserversdatabases"></a>Microsoft.Sql/servers/databases

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Description|
|---|---|---|---|---|
|cpu_percent|Porcentaje de CPU|Percent|Media|Porcentaje de CPU|
|physical_data_read_percent|Porcentaje de E/S de datos|Percent|Media|Porcentaje de E/S de datos|
|log_write_percent|Porcentaje de E/S de registro|Percent|Media|Porcentaje de E/S de registro|
|dtu_consumption_percent|Porcentaje de DTU|Percent|Media|Porcentaje de DTU|
|storage|Tamaño total de base de datos|Bytes|Máxima|Tamaño total de base de datos|
|connection_successful|Conexiones correctas|Recuento|Total|Conexiones correctas|
|connection_failed|Conexiones con errores|Recuento|Total|Conexiones con errores|
|blocked_by_firewall|Bloqueado por el firewall|Recuento|Total|Bloqueado por el firewall|
|deadlock|Interbloqueos|Recuento|Total|Interbloqueos|
|storage_percent|Porcentaje de tamaño de base de datos|Percent|Máxima|Porcentaje de tamaño de base de datos|
|xtp_storage_percent|Porcentaje de almacenamiento de OLTP en memoria|Percent|Media|Porcentaje de almacenamiento de OLTP en memoria|
|workers_percent|Porcentaje de trabajos|Percent|Media|Porcentaje de trabajos|
|sessions_percent|Porcentaje de sesiones|Percent|Media|Porcentaje de sesiones|
|dtu_limit|Límite de DTU|Recuento|Media|Límite de DTU|
|dtu_used|DTU utilizada|Recuento|Media|DTU utilizada|
|dwu_limit|Límite de DWU|Recuento|Máxima|Límite de DWU|
|dwu_consumption_percent|Porcentaje de DWU|Percent|Máxima|Porcentaje de DWU|
|dwu_used|DWU utilizada|Recuento|Máxima|DWU utilizada|

## <a name="microsoftsqlserverselasticpools"></a>Microsoft.Sql/servers/elasticPools

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Description|
|---|---|---|---|---|
|cpu_percent|Porcentaje de CPU|Percent|Media|Porcentaje de CPU|
|database_cpu_percent|Porcentaje de CPU|Percent|Media|Porcentaje de CPU|
|physical_data_read_percent|Porcentaje de E/S de datos|Percent|Media|Porcentaje de E/S de datos|
|database_physical_data_read_percent|Porcentaje de E/S de datos|Percent|Media|Porcentaje de E/S de datos|
|log_write_percent|Porcentaje de E/S de registro|Percent|Media|Porcentaje de E/S de registro|
|database_log_write_percent|Porcentaje de E/S de registro|Percent|Media|Porcentaje de E/S de registro|
|dtu_consumption_percent|Porcentaje de DTU|Percent|Media|Porcentaje de DTU|
|database_dtu_consumption_percent|Porcentaje de DTU|Percent|Media|Porcentaje de DTU|
|storage_percent|Porcentaje de almacenamiento|Percent|Media|Porcentaje de almacenamiento|
|workers_percent|Porcentaje de trabajos|Percent|Media|Porcentaje de trabajos|
|database_workers_percent|Porcentaje de trabajos|Percent|Media|Porcentaje de trabajos|
|sessions_percent|Porcentaje de sesiones|Percent|Media|Porcentaje de sesiones|
|database_sessions_percent|Porcentaje de sesiones|Percent|Media|Porcentaje de sesiones|
|eDTU_limit|Límite de eDTU|Recuento|Media|Límite de eDTU|
|storage_limit|Límite de almacenamiento|Bytes|Media|Límite de almacenamiento|
|eDTU_used|eDTU utilizada|Recuento|Media|eDTU utilizada|
|storage_used|Almacenamiento utilizado|Bytes|Media|Almacenamiento utilizado|
|database_storage_used|Almacenamiento utilizado|Bytes|Media|Almacenamiento utilizado|
|xtp_storage_percent|Porcentaje de almacenamiento de OLTP en memoria|Percent|Media|Porcentaje de almacenamiento de OLTP en memoria|

## <a name="microsoftsqlservers"></a>Microsoft.Sql/servers

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Descripción|
|---|---|---|---|---|
|dtu_consumption_percent|Porcentaje de DTU|Percent|Media|Porcentaje de DTU|
|database_dtu_consumption_percent|Porcentaje de DTU|Percent|Media|Porcentaje de DTU|
|storage_used|Almacenamiento utilizado|Bytes|Media|Almacenamiento utilizado|
|database_storage_used|Almacenamiento utilizado|Bytes|Media|Almacenamiento utilizado|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Description|
|---|---|---|---|---|
|ResourceUtilization|SU % uso|Percent|Máxima|SU % uso|
|InputEvents|Eventos de entrada|Recuento|Total|Eventos de entrada|
|InputEventBytes|Bytes del evento de entrada|Bytes|Total|Bytes del evento de entrada|
|LateInputEvents|Eventos de entrada retrasada|Recuento|Total|Eventos de entrada retrasada|
|OutputEvents|Eventos de salida|Recuento|Total|Eventos de salida|
|ConversionErrors|Errores de conversión de datos|Recuento|Total|Errores de conversión de datos|
|Errors|Errores de tiempo de ejecución|Recuento|Total|Errores de tiempo de ejecución|
|DroppedOrAdjustedEvents|Eventos de fuera de orden|Recuento|Total|Eventos de fuera de orden|
|AMLCalloutRequests|Solicitudes de función|Recuento|Total|Solicitudes de función|
|AMLCalloutFailedRequests|Solicitudes de función con errores|Recuento|Total|Solicitudes de función con errores|
|AMLCalloutInputEvents|Eventos de función|Recuento|Total|Eventos de función|

## <a name="microsoftwebserverfarms"></a>Microsoft.Web/serverfarms

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Description|
|---|---|---|---|---|
|CpuPercentage|Porcentaje de CPU|Percent|Media|Porcentaje de CPU|
|MemoryPercentage|Porcentaje de memoria|Percent|Media|Porcentaje de memoria|
|DiskQueueLength|Longitud de la cola de disco|Recuento|Total|Longitud de la cola de disco|
|HttpQueueLength|Longitud de la cola HTTP|Recuento|Total|Longitud de la cola HTTP|
|BytesReceived|Entrada de datos|Bytes|Total|Entrada de datos|
|BytesSent|Salida de datos|Bytes|Total|Salida de datos|

## <a name="microsoftwebsites-excluding-functions"></a>Microsoft.Web/sites (se excluye Functions)

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Description|
|---|---|---|---|---|
|CpuTime|Tiempo de CPU|Segundos|Total|Tiempo de CPU|
|Requests|Solicitudes|Recuento|Total|Solicitudes|
|BytesReceived|Entrada de datos|Bytes|Total|Entrada de datos|
|BytesSent|Salida de datos|Bytes|Total|Salida de datos|
|Http101|Http 101|Recuento|Total|Http 101|
|Http2xx|Http 2xx|Recuento|Total|Http 2xx|
|Http3xx|Http 3xx|Recuento|Total|Http 3xx|
|Http401|Http 401|Recuento|Total|Http 401|
|Http403|Http 403|Recuento|Total|Http 403|
|Http404|Http 404|Recuento|Total|Http 404|
|Http406|Http 406|Recuento|Total|Http 406|
|Http4xx|Http 4xx|Recuento|Total|Http 4xx|
|Http5xx|Errores de servidor HTTP|Recuento|Total|Errores de servidor HTTP|
|MemoryWorkingSet|Espacio de trabajo de memoria|Bytes|Media|Espacio de trabajo de memoria|
|AverageMemoryWorkingSet|Espacio de trabajo de memoria promedio|Bytes|Media|Espacio de trabajo de memoria promedio|
|AverageResponseTime|Tiempo de respuesta promedio|Segundos|Media|Tiempo de respuesta promedio|

## <a name="microsoftwebsites-functions"></a>Microsoft.Web/sites (Functions)

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Descripción|
|---|---|---|---|---|
|BytesReceived|Entrada de datos|Bytes|Total|Entrada de datos|
|BytesSent|Salida de datos|Bytes|Total|Salida de datos|
|Http5xx|Errores de servidor HTTP|Recuento|Total|Errores de servidor HTTP|
|MemoryWorkingSet|Espacio de trabajo de memoria|Bytes|Media|Espacio de trabajo de memoria|
|AverageMemoryWorkingSet|Espacio de trabajo de memoria promedio|Bytes|Media|Espacio de trabajo de memoria promedio|
|FunctionExecutionUnits|Unidades de ejecución de función|Recuento|Media|Unidades de ejecución de función|
|FunctionExecutionCount|Recuento de ejecución de funciones|Recuento|Media|Recuento de ejecución de funciones|

## <a name="microsoftwebsitesslots"></a>Microsoft.Web/sites/slots

|Métrica|Nombre de métrica para mostrar|Unidad|Tipo de agregación|Description|
|---|---|---|---|---|
|CpuTime|Tiempo de CPU|Segundos|Total|Tiempo de CPU|
|Requests|Solicitudes|Recuento|Total|Solicitudes|
|BytesReceived|Entrada de datos|Bytes|Total|Entrada de datos|
|BytesSent|Salida de datos|Bytes|Total|Salida de datos|
|Http101|Http 101|Recuento|Total|Http 101|
|Http2xx|Http 2xx|Recuento|Total|Http 2xx|
|Http3xx|Http 3xx|Recuento|Total|Http 3xx|
|Http401|Http 401|Recuento|Total|Http 401|
|Http403|Http 403|Recuento|Total|Http 403|
|Http404|Http 404|Recuento|Total|Http 404|
|Http406|Http 406|Recuento|Total|Http 406|
|Http4xx|Http 4xx|Recuento|Total|Http 4xx|
|Http5xx|Errores de servidor HTTP|Recuento|Total|Errores de servidor HTTP|
|MemoryWorkingSet|Espacio de trabajo de memoria|Bytes|Media|Espacio de trabajo de memoria|
|AverageMemoryWorkingSet|Espacio de trabajo de memoria promedio|Bytes|Media|Espacio de trabajo de memoria promedio|
|AverageResponseTime|Tiempo de respuesta promedio|Segundos|Media|Tiempo de respuesta promedio|
|FunctionExecutionUnits|Unidades de ejecución de función|Recuento|Media|Unidades de ejecución de función|
|FunctionExecutionCount|Recuento de ejecución de funciones|Recuento|Media|Recuento de ejecución de funciones|

## <a name="next-steps"></a>Pasos siguientes
* [Lea información sobre las métricas en Azure Monitor](monitoring-overview-metrics.md)
* [Creación de alertas basadas en métricas](insights-receive-alert-notifications.md)
* [Puede exportar las métricas toostorage, centro de eventos o análisis de registros](monitoring-overview-of-diagnostic-logs.md)
