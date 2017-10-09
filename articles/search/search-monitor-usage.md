---
title: "aaaMonitor uso y estadísticas en un servicio de búsqueda de Azure | Documentos de Microsoft"
description: "Realice el seguimiento del consumo de recursos y el tamaño de índice para Azure Search, un servicio de búsqueda hospedado en la nube en Microsoft Azure."
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
tags: azure-portal
ms.assetid: 122948de-d29a-426e-88b4-58cbcee4bc23
ms.service: search
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/01/2017
ms.author: betorres
ms.openlocfilehash: f38eabb5d04a410e11eaaff22157da8aba9e4845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-an-azure-search-service"></a>Supervisión de un servicio de Azure Search

Azure Search ofrece varios recursos para realizar el seguimiento del uso y rendimiento de los servicios de búsqueda. Proporciona acceso a toometrics, registros, las estadísticas de índices y las capacidades de supervisión extendidas en Power BI. Este artículo describe cómo tooenable Hola diferentes estrategias de supervisión y cómo toointerpret Hola datos resultantes.

## <a name="azure-search-metrics"></a>Métricas de Azure Search
Las métricas ofrecen visibilidad casi en tiempo real de cualquier servicio de búsqueda y están disponibles para todos los servicios, no es preciso realizar ningún tipo de configuración adicional. Le permiten realizar un seguimiento de rendimiento Hola del servicio para los días de too30.

Azure Search recopila datos de tres métricas diferentes:

* Buscar latencia: tiempo de servicio de búsqueda de hello necesarios tooprocess consultas de búsqueda, actualizadas cada minuto.
* Consultas de búsqueda por segundo (QPS): número de consultas de búsqueda recibidas por segundo, agregadas por minuto.
* Porcentaje de consultas de búsqueda limitadas: porcentaje de consultas de búsqueda que se han limitado, agregadas por minuto.

![Captura de pantalla de la actividad de QPS][1]

### <a name="set-up-alerts"></a>Configuración de alertas
Desde la página de detalles de la medición de hello, puede configurar alertas tootrigger una notificación por correo electrónico o una acción automatizada cuando una métrica supera un umbral que haya definido.

Para obtener más información acerca de las métricas, compruebe la documentación completa de hello en Monitor de Azure.  

## <a name="how-tootrack-resource-usage"></a>¿Cómo uso de recursos de tootrack
Seguimiento de crecimiento de Hola de índices y el tamaño de documento puede ayudarle a ajustar proactivamente capacidad antes de alcanzar el límite superior de Hola que haya establecido para el servicio. Puede hacerlo en el portal de Hola o mediante programación con API de REST de Hola.

### <a name="using-hello-portal"></a>Mediante el portal de Hola

uso de recursos de toomonitor, ver los recuentos de Hola y estadísticas para el servicio en hello [portal](https://portal.azure.com).

1. Inicie sesión en toohello [portal](https://portal.azure.com).
2. Abra Panel de servicio de Hola de su servicio de búsqueda de Azure. Iconos para servicio de hello pueden encontrarse en la página de inicio de hello, o también puede examinar el servicio de toohello desde Examinar en hello JumpBar.

Hola la sección uso incluye un medidor que indica qué parte de los recursos disponibles están en uso. Para más información sobre los límites de cada servicio en cuanto a índices, documentos y almacenamiento, consulte [Límites de servicio](search-limits-quotas-capacity.md).

  ![Icono de Uso][2]

> [!NOTE]
> captura de pantalla de Hello anterior es para el servicio gratuito de hello, que tiene un máximo de una réplica y cada partición y puede solo índices de host 3, 10.000 documentos o 50 MB de datos, lo que ocurra primero. Los servicios creados en un nivel Básico o Estándar tienen límites de servicio mucho mayores. Para más información sobre cómo elegir un nivel, consulte [Selección de un nivel o una SKU](search-sku-tier.md).
>
>

### <a name="using-hello-rest-api"></a>Uso de hello API de REST
API de REST de búsqueda de Azure de Hola y Hola SDK de .NET proporcionan las métricas de tooservice de acceso mediante programación.  Si utilizas [indizadores](https://msdn.microsoft.com/library/azure/dn946891.aspx) tooload un índice de base de datos de SQL Azure o base de datos de Azure Cosmos, una API adicional es números de hello tooget disponibles que necesite.

* [Obtención de estadísticas de índice](/rest/api/searchservice/get-index-statistics)
* [Recuento de documentos](/rest/api/searchservice/count-documents)
* [Obtención del estado del indizador](/rest/api/searchservice/get-indexer-status)

## <a name="how-tooexport-logs-and-metrics"></a>Funcionamiento de los registros tooexport y métricas

Puede exportar los registros de operaciones de Hola para los datos sin procesar de hello y servicio para las métricas de Hola que se describe en la sección anterior de Hola. Registros de operaciones que sepan cómo servicio Hola se usa y se puede consumir desde Power BI cuando los datos se copia tooa cuenta de almacenamiento. Azure Search proporciona un paquete de contenido de supervisión de Power BI para este fin.


### <a name="enabling-monitoring"></a>Habilitación de la supervisión
Abra el servicio de búsqueda de Azure en hello [portal de Azure](http://portal.azure.com) en hello opción de habilitar la supervisión.

Elegir datos Hola desea tooexport: registros, las métricas o ambos. Puede copiar tooa cuenta de almacenamiento, enviar tooan concentrador de eventos o exportarlo tooLog análisis.

![¿Cómo tooenable supervisión en el portal de Hola][3]

tooenable con PowerShell u Hola CLI de Azure, consulte la documentación de hello [aquí](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs#how-to-enable-collection-of-diagnostic-logs).

### <a name="logs-and-metrics-schemas"></a>Registros y esquemas de métricas
Cuando los datos de hello están copiados tooa almacenamiento de la cuenta, hello datos tienen el formato JSON y en su lugar en dos contenedores:

* insights-logs-operationlogs: para los registros del tráfico de búsqueda
* insights-metrics-pt1m: para las métricas

Hay un blob, por hora y por contenedor.

Ruta de acceso de ejemplo: `resourceId=/subscriptions/<subscriptionID>/resourcegroups/<resourceGroupName>/providers/microsoft.search/searchservices/<searchServiceName>/y=2015/m=12/d=25/h=01/m=00/name=PT1H.json`

#### <a name="log-schema"></a>Esquema de registro
Hola registros blobs contienen los registros de tráfico del servicio de búsqueda.
Cada blob tiene un objeto raíz llamado **registros** que contiene una matriz de objetos de registro.
Cada blob tiene registros en todas las operaciones de Hola que tuvieron lugar durante el saludo misma hora.

| Nombre | Tipo | Ejemplo | Notas |
| --- | --- | --- | --- |
| Twitter en tiempo |datetime |"2015-12-07T00:00:43.6872559Z" |Marca de tiempo de la operación de Hola |
| resourceId |string |"/SUBSCRIPTIONS/11111111-1111-1111-1111-111111111111/<br/>RESOURCEGROUPS/DEFAULT/PROVIDERS/<br/> MICROSOFT.SEARCH/SEARCHSERVICES/SEARCHSERVICE" |Su ResourceId |
| operationName |string |"Query.Search" |nombre de Hola de operación de Hola |
| operationVersion |string |"2015-02-28" |Hola api-version usa |
| categoría |string |"OperationLogs" |constant |
| resultType |string |"Success" |Valores posibles: Success o Failure |
| resultSignature |int |200 |Código de resultado HTTP |
| durationMS |int |50 |Duración de la operación de hello en milisegundos |
| propiedades |objeto |vea hello en la tabla siguiente |Objeto que contiene datos específicos de la operación |

**Esquema de propiedades**
| Nombre | Tipo | Ejemplo | Notas |
| --- | --- | --- | --- |
| Description |string |"GET /indexes('content')/docs" |punto de conexión de la operación de Hola |
| Consultar |string |"?search=AzureSearch&$count=true&api-version=2015-02-28" |parámetros de consulta de Hola |
| Documentos |int |42 |Número de documentos procesados |
| IndexName |string |"testindex" |Nombre del índice de hello asociado a la operación de Hola |

#### <a name="metrics-schema"></a>Esquema de métricas
| Nombre | Tipo | Ejemplo | Notas |
| --- | --- | --- | --- |
| resourceId |string |"/SUBSCRIPTIONS/11111111-1111-1111-1111-111111111111/<br/>RESOURCEGROUPS/DEFAULT/PROVIDERS/<br/>MICROSOFT.SEARCH/SEARCHSERVICES/SEARCHSERVICE" |el identificador de recurso |
| metricName |string |"Latency" |nombre de Hola de métrica de Hola |
| Twitter en tiempo |datetime |"2015-12-07T00:00:43.6872559Z" |marca de tiempo de la operación de Hola |
| average |int |64 |valor promedio de Hola de muestras sin procesar de hello en el intervalo de tiempo de métrica de Hola |
| minimum |int |37 |valor mínimo de Hola de muestras sin procesar de hello en el intervalo de tiempo de métrica de Hola |
| maximum |int |78 |valor máximo de Hola de muestras sin procesar de hello en el intervalo de tiempo de métrica de Hola |
| total |int |258 |valor total de Hola de muestras sin procesar de hello en el intervalo de tiempo de métrica de Hola |
| count |int |4 |número de Hola de muestras sin formato utiliza métrica de hello toogenerate |
| timegrain |string |"PT1M" |detalle de tiempo de Hola de métrica de hello en ISO 8601 |

Todas las métricas se notifican en intervalos de un minuto. Cada métrica expone los valores mínimo, máximo y promedio por minuto.

De métrica de SearchQueriesPerSecond hello, mínimo es el valor más bajo de Hola para las consultas de búsqueda por segundo que se registró durante ese minuto. Hello mismo aplica toohello más alto. Promedio, es hello agregado por minuto toda Hola.
Piense en este escenario durante un minuto: un segundo de carga elevada que es hello máximo para SearchQueriesPerSecond, seguido de 58 segundos de tiempo medio de carga y, por último, un segundo con una sola consulta, que es hello mínimo.

Para ThrottledSearchQueriesPercentage, como mínimo, máximo, promedio y total, todos tienen Hola mismo valor: Hola porcentaje de consultas de búsqueda que se han limitado, desde el número total de Hola de consultas de búsqueda durante un minuto.

## <a name="analyzing-your-data-with-power-bi"></a>Análisis de datos con Power BI

Se recomienda usar [Power BI](https://powerbi.microsoft.com) tooexplore y visualizar los datos. Puede fácilmente conectarlo tooyour cuenta de almacenamiento de Azure y comenzar rápidamente a analizar los datos.

Búsqueda de Azure proporciona un [paquete de contenido de Power BI](https://app.powerbi.com/getdata/services/azure-search) que le permite toomonitor y comprender el tráfico de búsqueda con las tablas y gráficos predefinidos. Contiene un conjunto de informes de Power BI que se conecte tooyour datos automáticamente y proporcionan información visual acerca del servicio de búsqueda. Para obtener más información, vea hello [página de Ayuda del paquete de contenido](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-search/).

![Panel de Power BI para Azure Search][4]

## <a name="next-steps"></a>Pasos siguientes
Revisión [escalar las réplicas y particiones](search-limits-quotas-capacity.md) para obtener instrucciones sobre cómo toobalance Hola asignación de particiones y réplicas de un servicio existente.

Visite [Administración de servicios de Azure Search en Microsoft Azure](search-manage.md) para más información sobre la administración de servicios, o [Rendimiento y optimización](search-performance-optimization.md) para que le sirva de guía de ajuste.

Obtenga más información sobre cómo crear informes increíbles. Consulte [Introducción a Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/) para obtener más información

<!--Image references-->
[1]: ./media/search-monitor-usage/AzSearch-Monitor-BarChart.PNG
[2]: ./media/search-monitor-usage/AzureSearch-Monitor1.PNG
[3]: ./media/search-monitor-usage/AzureSearch-Enable-Monitoring.PNG
[4]: ./media/search-monitor-usage/AzureSearch-PowerBI-Dashboard.png
