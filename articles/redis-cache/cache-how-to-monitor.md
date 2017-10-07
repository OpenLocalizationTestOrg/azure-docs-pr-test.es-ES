---
title: "aaaHow toomonitor caché en Redis de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomonitor Hola de estado y rendimiento de las instancias de caché en Redis de Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 7e70b153-9c87-4290-85af-2228f31df118
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: c474d485dfcbb109d5bb634a980f6db080598e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-azure-redis-cache"></a>Cómo toomonitor Redis de Azure almacenan en caché
Caché en Redis de Azure usa [Monitor Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) tooprovide varias opciones para supervisar las instancias de la memoria caché. Puede ver las métricas, anclar gráficos de métricas toohello panel de inicio, personalizar el intervalo de fecha y hora de Hola de gráficos de supervisión, agregar y quitar métricas de los gráficos de Hola y establecer alertas cuando se cumplen determinadas condiciones. Estas herramientas permiten toomonitor Hola estado de las instancias de caché en Redis de Azure y ayudan a administrar las aplicaciones de almacenamiento en caché.

Las métricas para instancias de caché en Redis de Azure se recopilan mediante Hola Redis [información](http://redis.io/commands/info) comando aproximadamente dos veces por minuto y se almacenan automáticamente durante 30 días (vea [exportar las métricas de caché](#export-cache-metrics) tooconfigure un Directiva de retención diferente) por lo que se pueden mostrar en los gráficos de métricas de Hola y evalúa las reglas de alerta. Para obtener más información acerca de los valores de información diferentes Hola usan para cada métrica de caché, consulte [métricas disponibles e intervalos de notificación](#available-metrics-and-reporting-intervals).

<a name="view-cache-metrics"></a>

las métricas de caché de tooview [examinar](cache-configure.md#configure-redis-cache-settings) tooyour de instancia de caché en hello [portal de Azure](https://portal.azure.com).  Caché en Redis de Azure proporciona algunos gráficos integrados en hello **Introducción** hello y hoja **Redis métricas** hoja. Cada gráfico puede personalizarse agregando o quitando las métricas y cambiando Hola intervalo de informes.

![Caché en Redis](./media/cache-how-to-monitor/redis-cache-redis-metrics-blade.png)

## <a name="view-pre-configured-metrics-charts"></a>Visualización de gráficos de métricas preconfigurados

Hola **Introducción** hoja tiene Hola siguiendo los gráficos de supervisión configurados previamente.

* [Gráficos de supervisión](#monitoring-charts)
* [Gráficos de uso](#usage-charts)

### <a name="monitoring-charts"></a>Gráficos de supervisión
Hola **supervisión** sección Hola **Introducción** hoja **aciertos y errores**, **obtiene y establece**, **conexiones**, y **comandos totales** gráficos.

![Gráficos de supervisión](./media/cache-how-to-monitor/redis-cache-monitoring-part.png)

### <a name="usage-charts"></a>Gráficos de uso
Hola **uso** sección Hola **Introducción** hoja **carga del servidor Redis**, **uso de memoria**, **ancho de banda de red** , y **el uso de CPU** gráficos y también muestra hello **tarifa** Hola la instancia de caché.

![Gráficos de uso](./media/cache-how-to-monitor/redis-cache-usage-part.png)

Hola **tarifa** precios de caché de Hola de muestra de nivel y se puede utilizar demasiado[escala](cache-how-to-scale.md) Hola tooa de caché diferente de nivel de precios.

## <a name="view-metrics-with-azure-monitor"></a>Visualización de métricas con Azure Monitor
tooview Redis métricas y crear gráficos personalizados mediante el Monitor de Azure, haga clic en **métricas** de hello **menú recursos**y personalizar el gráfico mediante las métricas de hello deseado, intervalo, tipo de gráfico, de informe y más.

![Caché en Redis](./media/cache-how-to-monitor/redis-cache-monitor.png)

Para más información acerca de cómo trabajar con métricas mediante Azure Monitor, consulte [Información general sobre las métricas en Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).

<a name="how-to-view-metrics-and-customize-chart"></a>
<a name="enable-cache-diagnostics"></a>
## <a name="export-cache-metrics"></a>Exportación de métricas de caché
De manera predeterminada, en Azure Monitor las métricas de caché se [almacenan durante 30 días](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) y después se eliminan. toopersist las métricas de la memoria caché durante más de 30 días, puede [designar una cuenta de almacenamiento](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md) y especifique un **retención (días)** directiva para las métricas de memoria caché. 

tooconfigure una cuenta de almacenamiento para las métricas de caché:

1. Haga clic en **diagnósticos** de hello **menú recursos** en hello **caché en Redis** hoja.
2. Haga clic en **Activado**.
3. Comprobar **tooa cuenta de almacenamiento de archivo**.
4. Seleccione la cuenta de almacenamiento de hello en las métricas de caché toostore Hola.
5. Comprobar hello **1 minuto** casilla de verificación y especifique una **retención (días)** directiva. Si no desea tooapply cualquier directiva de retención y conservar los datos de forma permanente, establezca **retención (días)** demasiado**0**.
6. Haga clic en **Guardar**.

![Diagnósticos de Redis](./media/cache-how-to-monitor/redis-cache-diagnostics.png)

>[!NOTE]
>En suma tooarchiving su toostorage de métricas de caché, también puede [transmitirlos tooan concentrador de eventos o enviarlos tooLog análisis](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).
>
>

tooaccess las métricas, puede verlos en hello portal de Azure como se describió anteriormente en este artículo, y también puede acceder a ellos mediante hello [API de REST de métricas de supervisión de Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md#access-metrics-via-the-rest-api).

> [!NOTE]
> Si cambia las cuentas de almacenamiento, datos de hello en la cuenta de almacenamiento de hello configurado previamente sigue estando disponibles para su descarga, pero no se muestra en hello portal de Azure.  
> 
> 

## <a name="available-metrics-and-reporting-intervals"></a>Métricas disponibles e intervalos de informes
Los informes de las métricas de caché se generan utilizando diferentes intervalos, como **Última hora**, **Hoy**, **Semana anterior** y **Personalizado**. Hola **métrica** hoja para cada gráfico de métricas muestra los valores de promedio, mínimo y máximo de Hola para cada métrica en el gráfico de Hola y algunas métricas muestran un total de hello intervalo de informes. 

Cada métrica incluye dos versiones. Una métrica mide el rendimiento de caché completa de Hola y de memorias caché que usan [de agrupación en clústeres](cache-how-to-premium-clustering.md), una segunda versión de métrica de Hola que incluye `(Shard 0-9)` Hola el rendimiento de las medidas de nombre de una sola partición en una memoria caché. Por ejemplo, si una caché tiene 4 particiones, `Cache Hits` es Hola cantidad total de aciertos de caché completa de hello, y `Cache Hits (Shard 3)` es simplemente los resultados de Hola para esa partición de memoria caché de Hola.

> [!NOTE]
> Incluso cuando está inactiva y no tenga ninguna aplicación cliente activa conectada caché hello, puede que vea alguna actividad de la memoria caché, como los clientes conectados, el uso de memoria y se realizan operaciones. Esta actividad es normal durante la operación de Hola de una instancia de caché en Redis de Azure.
> 
> 

| Métrica | Description |
| --- | --- |
| Aciertos de caché |número de Hola de búsquedas con éxito claves durante el intervalo de notificación especificado Hola. Se asigna demasiado`keyspace_hits` de hello Redis [información](http://redis.io/commands/info) comando. |
| Errores de caché |número de Hello errores de búsquedas de claves durante el intervalo de notificación especificado Hola. Se asigna demasiado`keyspace_misses` de hello comando Redis INFO. Errores de caché no significa necesariamente que hay un problema con la caché de Hola. Por ejemplo, cuando se usa Hola caché-aside patrón de programación, una aplicación busca primera en memoria caché de Hola para un elemento. Si hello elemento no está allí (error de caché), elemento de Hola se recupera de la base de datos de Hola y agregar caché toohello para la próxima vez. Errores de caché son el comportamiento normal de hello patrón de programación de caché-aside. Si el número de Hola de errores de caché es mayor de lo esperado, examine lógica de la aplicación hello que rellena y lee de la memoria caché de Hola. Si se desalojan elementos de caché de hello debido a presión toomemory, a continuación, puede haber algunos errores de caché, pero sería una mejor toomonitor métrica para presión de memoria `Used Memory` o `Evicted Keys`. |
| Clientes conectados |número de Hola de memoria caché del toohello de conexiones de cliente durante el intervalo de notificación especificado Hola. Se asigna demasiado`connected_clients` de hello comando Redis INFO. Una vez Hola [límite de conexiones](cache-configure.md#default-redis-server-configuration) se alcanza los intentos de conexión posteriores se producirá un error en la memoria caché de toohello. Tenga en cuenta que incluso si no hay ninguna aplicación cliente activa, se puede ser algunas instancias de clientes conectados debido a conexiones y procesos de toointernal. |
| Claves expulsadas |número de elementos que se eliminan de la caché de Hola durante Hola Hola especificado intervalo de notificación toohello due `maxmemory` límite. Se asigna demasiado`evicted_keys` de hello comando Redis INFO. |
| Claves expiradas |número de Hola de elementos caducado en memoria caché de Hola durante el intervalo de notificación especificado Hola. Este valor se asigna demasiado`expired_keys` de hello comando Redis INFO. |
| Total de claves  | número máximo de Hola de claves de caché de Hola durante hello más allá de período de tiempo de informe. Se asigna demasiado`keyspace` de hello comando Redis INFO. Pagar tooa limitación de hello subyacente sistema métricas, para las memorias caché con el clúster está habilitada, Total de claves devuelve número máximo de Hola de claves de partición de Hola que tenía el número máximo de Hola de claves durante el intervalo de informes de Hola.  |
| Gets |número de Hola de operaciones get de caché de Hola durante el intervalo de notificación especificado Hola. Este valor es la suma de Hola de siguiente Hola valores de hello Redis información de todos los comandos: `cmdstat_get`, `cmdstat_hget`, `cmdstat_hgetall`, `cmdstat_hmget`, `cmdstat_mget`, `cmdstat_getbit`, y `cmdstat_getrange`, y es la suma de toohello equivalente de aciertos de caché y errores durante el intervalo de informes de Hola. |
| Carga de servidor de Redis |porcentaje de Hola de ciclos de qué Hola servidor de Redis está ocupado procesando y no espera de inactividad para los mensajes. Si este contador llega a 100 significa que servidor de Redis Hola alcanza un límite superior de rendimiento y no se puede procesar Hola CPU funciona en cualquier con mayor rapidez. Si está viendo alta carga del servidor Redis verá las excepciones de tiempo de espera en el cliente de Hola. En este caso, debería considerar la posibilidad de un escalado vertical o el particionamiento de los datos en varias cachés. |
| Sets |número de Hola de memoria caché del conjunto de operaciones toohello durante Hola especifica intervalo de notificación. Este valor es la suma de Hola de siguiente Hola valores de hello Redis información de todos los comandos: `cmdstat_set`, `cmdstat_hset`, `cmdstat_hmset`, `cmdstat_hsetnx`, `cmdstat_lset`, `cmdstat_mset`, `cmdstat_msetnx`, `cmdstat_setbit`, `cmdstat_setex`, `cmdstat_setrange` , y `cmdstat_setnx`. |
| Total de operaciones |número total de Hola de comandos procesados por el servidor de caché de Hola durante Hola especifica el intervalo de notificación. Este valor se asigna demasiado`total_commands_processed` de hello comando Redis INFO. Tenga en cuenta que cuando la caché en Redis de Azure se usan exclusivamente para pub/sub no habrá ninguna métrica de `Cache Hits`, `Cache Misses`, `Gets`, o `Sets`, pero habrá `Total Operations` métricas que reflejen el uso de la memoria caché de Hola para las operaciones de pub/sub. |
| Memoria usada |cantidad de Hola de memoria caché utilizada para los pares clave/valor en memoria caché de hello en MB durante Hola especifica el intervalo de informes. Este valor se asigna demasiado`used_memory` de hello comando Redis INFO. Esto no incluye los metadatos o la fragmentación. |
| Memoria RSS usada |cantidad de Hola de memoria caché utilizada en MB durante Hola especifica intervalo de informes, incluidas la fragmentación y metadatos. Este valor se asigna demasiado`used_memory_rss` de hello comando Redis INFO. |
| CPU |uso de CPU del servidor de caché de Redis de Azure de Hola como un porcentaje durante Hola Hola especifica intervalo de notificación. Este valor asigna sistema de operativo toohello `\Processor(_Total)\% Processor Time` contador de rendimiento. |
| Lectura de caché |cantidad de Hola de los datos leídos desde la caché de hello en Megabytes por segundo (MB/s) durante el saludo especifica el intervalo de informes. Este valor se deriva de tarjetas de interfaz de red de Hola que admiten Hola de máquina virtual que hospeda la caché de Hola y es no Redis específico. **Este valor corresponde toohello de ancho de banda de red utilizado por esta memoria caché. Si desea tooset las alertas para los límites de ancho de banda de red de lado de servidor, a continuación, crear mediante este `Cache Read` contador. Vea [esta tabla](cache-faq.md#cache-performance) para hello observado límites de ancho de banda para caché de distintos tamaños y niveles de precios.** |
| Escritura de caché |Hola cantidad de datos escritos toohello caché en Megabytes por segundo (MB/s) durante el intervalo de notificación especificado Hola. Este valor se deriva de tarjetas de interfaz de red de Hola que admiten Hola de máquina virtual que hospeda la caché de Hola y es no Redis específico. Este valor corresponde toohello ancho de banda de red de los datos enviados toohello caché de cliente de Hola. |

<a name="operations-and-alerts"></a>
## <a name="alerts"></a>Alertas
Puede configurar alertas de tooreceive basadas en métricas y registros de actividades. Monitor de Azure permite tooconfigure una alerta toodo hello las siguientes cuando se desencadena:

* Enviar una notificación por correo electrónico
* Llamar a un webhook
* Invocar una aplicación lógica de Azure

reglas de alerta de tooconfigure para la memoria caché, haga clic en **reglas de alerta** de hello **menú recursos**.

![Supervisión](./media/cache-how-to-monitor/redis-cache-monitoring.png)

Para más información acerca de la configuración y uso de alertas, consulte [Información general de las alertas](../monitoring-and-diagnostics/insights-alerts-portal.md).

## <a name="activity-logs"></a>Registros de actividad
Registros de actividad proporcionan una visión general de las operaciones de Hola que se realizaron en las instancias de caché en Redis de Azure. Antes se los conocía como "registros de auditoría" o "registros operativos". Utilizar registros de actividad, puede determinar Hola "qué, quién y cuándo" para las operaciones (PUT, POST, DELETE) realizadas en las instancias de caché en Redis de Azure de escritura. 

> [!NOTE]
> Los registros de actividad no incluyen operaciones de lectura (GET).
>
>

registros de actividad de tooview para la memoria caché, haga clic en **registros de actividad** de hello **menú recursos**.

Para obtener más información acerca de los registros de actividad, vea [información general de hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).











