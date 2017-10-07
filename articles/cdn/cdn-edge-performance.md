---
title: rendimiento del nodo aaaAnalyze perimetral de red CDN de Azure | Documentos de Microsoft
description: "Análisis del rendimiento del nodo perimetral en la red CDN de Microsoft Azure. Análisis de rendimiento de borde proporciona el uso de ancho de banda y el tráfico de información detallada para CDN Hola."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 8cc596a7-3e01-4f76-af7b-a05a1421517e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 35361d1c5e27fc6b8536c29e33c2ed217ee4d17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-edge-node-performance-in-microsoft-azure-cdn"></a>Análisis del rendimiento del nodo perimetral en la red CDN de Microsoft Azure
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Información general
Análisis de rendimiento de borde proporciona el uso de ancho de banda y el tráfico de información detallada para CDN Hola. Esta información puede ser, a continuación, estadísticas de tendencias toogenerate usado, lo que permite una visión general de toogain en cómo los activos se están almacenados en caché y entregado tooyour clientes. A su vez, esto permite tooform debe ser una estrategia sobre cómo entrega de hello toooptimize de su contenido y toodetermine lo emite abordó toobetter Aproveche Hola CDN. Como resultado, no solo será tooimprove capaz de rendimiento de entrega de datos, sino también ser capaz de tooreduce los costos de red CDN.

> [!NOTE]
> Todos los informes usan la notación de hora UTC/GMT al especificar una fecha y hora.
> 
> 

## <a name="reports-and-log-collection"></a>Informes y recopilación de registros
Módulo de análisis de rendimiento de borde de hello deben recopila datos de actividad de red CDN antes de que puede generar informes en él. Este proceso de recopilación tiene lugar una vez al día y trata de actividad de hello que tuvieron lugar durante el saludo día anterior. Esto significa que las estadísticas de un informe representan una muestra de las estadísticas del día de hello en tiempo de Hola se procesó y no necesariamente contienen el conjunto completo de Hola de datos para hello día actual. función principal de Hola de estos informes es tooassess de rendimiento. No deben usarse con fines de facturación o estadísticas numéricas exactas.

> [!NOTE]
> datos sin procesar de Hola desde el que se generan los informes de análisis de rendimiento del borde están disponibles para al menos 90 días.
> 
> 

## <a name="dashboard"></a>Panel
panel de análisis de rendimiento de borde de Hello realiza un seguimiento de tráfico de red CDN actual e histórico a través de un gráfico y las estadísticas. Utilice este panel toodetect reciente y a largo plazo las tendencias en el rendimiento de Hola de tráfico de red CDN para su cuenta.

Este panel consta de:

* Un gráfico interactivo que permite la visualización de Hola de las métricas clave y tendencias.
* Una escala de tiempo que proporciona una sensación de patrones a largo plazo de las tendencias y las métricas clave.
* Las métricas clave y la información estadística acerca de cómo nuestra red CDN mejora el tráfico del sitio con relación al rendimiento general, el uso y la eficiencia.

### <a name="accessing-hello-edge-performance-dashboard"></a>Al tener acceso al panel de rendimiento de hello borde
1. En la hoja de perfil CDN Hola, haga clic en hello **administrar** botón.
   
    ![Botón de administración de hoja de perfil de red CDN](./media/cdn-edge-performance/cdn-manage-btn.png)
   
    se abre el portal de administración de red CDN Hola.
2. Mantenga el mouse sobre hello **análisis** ficha y, a continuación, mantenga el mouse sobre hello **análisis de rendimiento de borde** ventana flotante.  Haga clic en **Panel**.
   
    se muestra el panel de análisis de nodo de Hello borde.

### <a name="chart"></a>Gráfico
Hola, contiene un gráfico que realiza el seguimiento de una métrica sobre Hola período de tiempo seleccionado en la escala de tiempo de Hola que aparece justo debajo de ella.  Se muestra una escala de tiempo que representa gráficamente la toohello en los últimos dos años de actividad de red CDN directamente por debajo del gráfico de Hola.

#### <a name="using-hello-chart"></a>Usar el gráfico de Hola
* De forma predeterminada, se se representan gráficamente tasa de eficiencia de caché de Hola para hello últimos 30 días.
* Este gráfico se genera a partir de datos que se recopilan a diario.
* Mantiene el mouse sobre un día en el gráfico de líneas de hello indicará un valor de fecha y Hola de métrica de hello en esa fecha.
* Haga clic en Resaltar los fines de semana tootoggle una superposición de barras verticales grises claros que representan los fines de semana en el gráfico de Hola. Este tipo de superposición es útil para identificar patrones de tráfico durante los fines de semana.
* Haga clic en ver un año hace tootoggle una superposición de hello anterior actividad del año sobre Hola mismo período en el gráfico de Hola de tiempo. Este tipo de comparación proporciona información sobre los patrones de uso de la red CDN a largo plazo. Hola superior derecha esquina del gráfico de hello contiene una leyenda que indica el código de color de Hola para cada gráfico de líneas.

#### <a name="updating-hello-chart"></a>Actualizar gráfico Hola
* Intervalo de tiempo: Realizar uno de hello siguientes:
  * Seleccionar región deseada de hello en escala de tiempo de Hola. gráfico de Hola se actualizará con los datos correspondientes toohello período de tiempo seleccionado.
  * Haga doble clic en Hola toodisplay gráfico todos los datos históricos disponibles seguridad tooa máximo de dos años.
* Métrica: Haga clic en el icono de gráfico de Hola que aparece la siguiente métrica de toohello deseado. gráfico de Hola y escala de tiempo de Hola se actualizarán con los datos de métrica de hello correspondiente.

### <a name="key-metrics-and-statistics"></a>Estadísticas y mediciones clave
#### <a name="efficiency-metrics"></a>Métricas de eficiencia
Hola de estas métricas sirve toosee si se puede mejorar la eficacia de la caché. ventajas principales de Hello derivados de la eficacia de la caché son:

* Reducción de la carga en servidor de origen de hello puede dar lugar a:
  * Mejor rendimiento del servidor web
  * Reducción de los costos operacionales.
* Mejora la aceleración de la entrega de datos desde que se enviará más solicitudes directamente desde la red CDN Hola.

| Campo | Descripción |
| --- | --- |
| Eficiencia de la memoria caché |Indica el porcentaje de Hola de datos transferidos que se realizó el servicio de caché. Esta métrica medidas cuando hay una versión en caché de hello solicita contenido se ofreció directamente desde hello toorequesters (servidores perimetrales) de CDN (por ejemplo, un explorador web) |
| Frecuencia de aciertos |Indica el porcentaje de Hola de solicitudes que han sido atendidas desde la caché. Esta métrica medidas cuando hay una versión en caché de hello solicita contenido se ofreció directamente desde hello toorequesters (servidores perimetrales) de CDN (por ejemplo, un explorador web). |
| % de bytes remotos - ninguna configuración de caché |Indica el porcentaje de Hola de tráfico que se realizó el servicio de servidores de origen toohello CDN (servidores perimetrales) que no se almacenarán en caché como resultado de la característica de omisión caché hello (motor de reglas de HTTP). |
| % de bytes remotos - caché expirada |Indica el porcentaje de Hola de tráfico que se realizó el servicio de servidores de origen toohello CDN (servidores perimetrales) como resultado de la revalidación de contenido obsoleto. |

#### <a name="usage-metrics"></a>Métricas de uso
Hola de estas métricas sirve visión tooprovide Hola siguiendo las medidas de reducción de costos:

* Minimizar los costos operativos a través de la red CDN Hola.
* Reducción de gastos de red CDN mediante compresión y la eficiencia de la memoria caché.

> [!NOTE]
> Números de volumen de tráfico representan el tráfico que se usa en los cálculos de proporciones y porcentajes y puede mostrar sólo una parte del tráfico total de Hola para los clientes de gran volumen.
> 
> 

| Campo | Descripción |
| --- | --- |
| Promedio de bytes de salida |Indica Hola número promedio de bytes transferidos por cada solicitud de atender las solicitudes de solicitante de toohello (servidores perimetrales) de hello CDN (por ejemplo, un explorador web). |
| Velocidad de bytes de ninguna configuración de caché |Indica el porcentaje de Hola de tráfico provienen Hola CDN (servidores perimetrales) toohello solicitante (p. ej., un explorador web) que no se almacenarán en caché debido a característica de omisión caché toohello. |
| Velocidad de bytes comprimidos |Indica el porcentaje de Hola de tráfico enviado desde hello toorequesters (servidores perimetrales) de CDN (por ejemplo, un explorador web) en un formato comprimido. |
| Bytes de salida |Indica la cantidad de Hola de datos, en bytes, que se enviaron del solicitante de toohello (servidores perimetrales) de hello CDN (por ejemplo, un explorador web). |
| Bytes de entrada |Indica la cantidad de Hola de datos, en bytes, que se envían desde los solicitantes (p. ej., un explorador web) toohello CDN (servidores perimetrales). |
| Bytes remotos |Indica la cantidad de Hola de datos, en bytes, que se envían desde CDN y customer toohello de servidores de origen CDN (servidores perimetrales). |

#### <a name="performance-metrics"></a>Métricas de rendimiento.
Hola de estas métricas sirve tootrack el rendimiento general para el tráfico de red CDN.

| Campo | Descripción |
| --- | --- |
| Transfer Rate |Indica la velocidad media de hello en el que el contenido se transfiere del solicitante de tooa CDN Hola. |
| Duration |Indica el tiempo promedio de hello, en milisegundos, que tardó toodeliver un solicitante de tooa activos (por ejemplo, un explorador web). |
| Compressed Request Rate |Indica el porcentaje de Hola de aciertos que se enviaron del solicitante de toohello (servidores perimetrales) de hello CDN (por ejemplo, un explorador web) en un formato comprimido. |
| 4xx Error Rate |Indica el porcentaje de Hola de resultados que genera un código de estado 4xx. |
| 5xx Error Rate |Indica el porcentaje de Hola de resultados que genera un código de estado 5xx. |
| Aciertos |Indica el número de Hola de solicitudes para el contenido de la red CDN. |

#### <a name="secure-traffic-metrics"></a>Secure Traffic Metrics
sirve a Hola de estas métricas de rendimiento de la red CDN de tootrack para el tráfico HTTPS.

| Campo | Descripción |
| --- | --- |
| Secure Cache Efficiency |Indica el porcentaje de Hola de datos transferidos para las solicitudes HTTPS que se atienden desde la memoria caché. Esta métrica mide cuando una versión almacenada en caché de hello solicita contenido se ofreció directamente desde hello toorequesters (servidores perimetrales) de CDN (por ejemplo, un explorador web) a través de HTTPS. |
| Secure Transfer Rate |Indica la velocidad media de hello en el que se transfiere contenido de hello toorequesters (servidores perimetrales) de CDN (por ejemplo, servidores web) a través de HTTPS. |
| Average Secure Duration |Indica el tiempo promedio de hello, en milisegundos, que tardó toodeliver un solicitante de tooa activos (por ejemplo, un explorador web) a través de HTTPS. |
| Secure Hits |Indica el número de Hola de solicitudes HTTPS para el contenido de la red CDN. |
| Secure Bytes Out |Indica la cantidad de Hola de tráfico HTTPS, en bytes, que se enviaron del solicitante de toohello (servidores perimetrales) de hello CDN (por ejemplo, un explorador web). |

## <a name="reports"></a>Informes
Cada informe de este módulo contiene un gráfico y las estadísticas de uso del ancho de banda y del tráfico para distintos tipos de métricas (por ejemplo, códigos de estado HTTP, códigos de estado de la memoria caché, solicitud de dirección URL, etc.). Esta información puede ser usado toodelve profundiza en cómo se sirve contenido tooyour clientes y el rendimiento de entrega de datos de toofine ajustar CDN comportamiento tooimprove.

### <a name="accessing-hello-edge-performance-reports"></a>Acceso a informes de rendimiento de hello borde
1. En la hoja de perfil CDN Hola, haga clic en hello **administrar** botón.
   
    ![Botón de administración de hoja de perfil de red CDN](./media/cdn-edge-performance/cdn-manage-btn.png)
   
    se abre el portal de administración de red CDN Hola.
2. Mantenga el mouse sobre hello **análisis** ficha y, a continuación, mantenga el mouse sobre hello **análisis de rendimiento de borde** ventana flotante.  Haga clic en **Objeto grande HTTP**.
   
    se muestra la pantalla de informes de análisis de Hello borde nodo.

| Informe | Descripción |
| --- | --- |
| Daily Summary |Le permite tooview tendencias diarias de tráfico durante un período de tiempo especificado. Cada barra de este gráfico representa una fecha determinada. tamaño de Hola de barra de hello indica número total de Hola de aciertos ocurridos en esa fecha. |
| Hourly Summary |Le permite tooview las tendencias del tráfico por hora durante un período de tiempo especificado. Cada barra de este gráfico representa una sola hora de una fecha determinada. tamaño de Hola de barra de hello indica número total de Hola de aciertos ocurridos durante esa hora. |
| Protocolos |Muestra el desglose de hello del tráfico entre Hola HTTP y protocolos HTTPS. Un gráfico de anillos indica el porcentaje de Hola de aciertos de que se produjo para cada tipo de protocolo. |
| HTTP Methods |Le permite tooget son un rápido resumen de los métodos HTTP que se va toorequest usa los datos. Normalmente, los métodos de solicitud HTTP más comunes de hello son GET, HEAD y POST. Un gráfico de anillos indica el porcentaje de Hola de aciertos de que se produjo para cada tipo de método de solicitud HTTP. |
| URLs |Contiene un gráfico que muestra hello top 10 solicitado las direcciones URL. Se muestra una barra para cada dirección URL. alto de Hola de barra de hello indica la cantidad de hits que ha generado la dirección URL determinada por intervalo de tiempo de hello abarcado por el informe de Hola. Las estadísticas de los 100 mejores de hello solicitado que se muestran las direcciones URL directamente debajo de este gráfico. |
| CNAMEs |Contiene un gráfico que muestra hello top 10 CNAME usa toorequest activos largo intervalo de tiempo de Hola de un informe. Las estadísticas de los 100 mejores de hello solicitado que CNAME aparecen directamente debajo de este gráfico. |
| Origins |Contiene un gráfico que muestra hello 10 mejores CDN o cliente servidores de origen desde el que se solicitaron activos durante un período de tiempo especificado. Las estadísticas de los 100 mejores de hello solicitado se muestran los servidores de origen CDN o un cliente directamente debajo de este gráfico. Los servidores de origen del cliente se identifican por nombre hello definido en hello opción de nombre de directorio. |
| Geo POPs |Muestra la cantidad del tráfico que se enruta a través de un determinado punto de presencia (POP). abreviatura de tres letras Hola representa un POP en nuestra red CDN. |
| Clientes |Contiene un gráfico que muestra a hello top 10 clientes que solicitaron activos durante un período de tiempo especificado. Para fines de Hola de este informe, todas las solicitudes que se originan en Hola misma dirección IP se considera toobe de hello mismo cliente. Se muestran las estadísticas para top 100 clientes de hello directamente debajo de este gráfico. Este informe resulta útil para determinar los patrones de actividad de descarga para los clientes principales. |
| Estados de la memoria caché |Proporciona un análisis detallado del comportamiento de la memoria caché, que puede revelar enfoques para mejorar Hola general experiencia del usuario final. Puesto que el rendimiento más rápido de hello procede de aciertos de caché, puede optimizar velocidades de entrega de datos por minimizar errores de caché y de aciertos de caché expirados. |
| NONE Details |Contiene un gráfico que muestra hello top 10 las direcciones URL para los activos para el que la actualización de contenido de la caché no se activó durante un período de tiempo especificado. Se muestran las estadísticas de hello top 100 las direcciones URL para estos tipos de recursos directamente debajo de este gráfico. |
| CONFIG_NOCACHE Details |Contiene un gráfico que muestra las direcciones URL de hello 10 principales para los activos que no se almacenaron en caché debido a configuración de red CDN de toohello cliente. Estos tipos de activos se atienden directamente desde el servidor de origen de Hola. Se muestran las estadísticas de hello top 100 las direcciones URL para estos tipos de recursos directamente debajo de este gráfico. |
| UNCACHEABLE Details |Contiene un gráfico que muestra hello top 10 las direcciones URL para los activos que pudieron no estar en la caché debido a los datos del encabezado toorequest. Se muestran las estadísticas de hello top 100 las direcciones URL para estos tipos de recursos directamente debajo de este gráfico. |
| TCP_HIT Details |Contiene un gráfico que muestra hello top 10 las direcciones URL para los activos que se atienden inmediatamente desde la memoria caché. Se muestran las estadísticas de hello top 100 las direcciones URL para estos tipos de recursos directamente debajo de este gráfico. |
| TCP_MISS Details |Contiene un gráfico que muestra hello top 10 las direcciones URL para los activos que tienen un estado de la caché de TCP_MISS. Se muestran las estadísticas de hello top 100 las direcciones URL para estos tipos de recursos directamente debajo de este gráfico. |
| TCP_EXPIRED_HIT Details |Contiene un gráfico que muestra hello top 10 las direcciones URL para los activos obsoletos que se provienen directamente Hola POP. Se muestran las estadísticas de hello top 100 las direcciones URL para estos tipos de recursos directamente debajo de este gráfico. |
| TCP_EXPIRED_MISS Details |Contiene un gráfico que muestra hello top 10 las direcciones URL para los recursos obsoletos para que una nueva versión tenía toobe recupera del servidor de origen de Hola. Se muestran las estadísticas de hello top 100 las direcciones URL para estos tipos de recursos directamente debajo de este gráfico. |
| TCP_CLIENT_REFRESH_MISS Details |Contiene un gráfico de barras que muestra hello superior las 10 direcciones URL para activos se recuperaron de un servidor de origen debido tooa sin caché solicitud de hello cliente. Se muestran las estadísticas de hello top 100 las direcciones URL para estos tipos de solicitudes directamente debajo de este gráfico. |
| Client Request Types |Indica el tipo de saludo de solicitudes realizadas por los clientes HTTP (por ejemplo, los exploradores). Este informe incluye un gráfico de anillos que proporciona un sentido como toohow controla las solicitudes. Información de ancho de banda y el tráfico para cada tipo de solicitud se muestra por debajo del gráfico de Hola. |
| User Agent |Contiene un gráfico de barras mostrar hello superior usuario 10 agentes toorequest su contenido a través de la red CDN. Normalmente, un agente de usuario es un explorador web, un reproductor multimedia o un explorador de teléfono móvil. Se muestran las estadísticas para los agentes de usuario 100 superior Hola directamente debajo de este gráfico. |
| Referrers |Contiene un gráfico de barras muestra hello remitentes 10 principales toocontent tiene acceso a través de la red CDN. Normalmente, un origen de referencia es Hola URL de página web de Hola o recurso que se vincula tooyour contenido. Se proporciona información detallada por debajo del gráfico de Hola para remitentes de 100 principales Hola. |
| Compression Types |Contiene un gráfico de anillos que divide los activos solicitados dependiendo de si fueron o no comprimidos por nuestros servidores perimetrales. porcentaje de Hola de activos comprimidos se divide en tipo hello de compresión utilizado. Por debajo del gráfico de Hola se proporciona información detallada para cada tipo de compresión y el estado. |
| File Types |Contiene un gráfico de barras que muestra los principales tipos de archivo 10 de Hola que se han solicitado a través de nuestro CDN para la cuenta. Para fines de Hola de este informe, se define un tipo de archivo por extensión de nombre de archivo del recurso de Hola y tipo de medio de Internet (por ejemplo, .html \[texto/html\], .htm \[texto/html\], .aspx \[texto/html\], etcetera.). Se proporciona información detallada por debajo del gráfico de Hola Hola top 100 para tipos de archivo. |
| Unique Files |Contiene un gráfico que represente el número total de Hola de activos únicos que se solicitaron en un día determinado durante un período de tiempo especificado. |
| Token Auth Summary |Contiene un gráfico circular que proporciona una descripción general acerca de si los activos solicitados se protegieron con una autenticación basada en token. Activos protegidos se muestran en el gráfico de hello según los resultados de toohello de su autenticación ha intentado. |
| Token Auth Deny Details |Contiene un gráfico de barras que le permite tooview Hola top 10 solicitudes que se han denegado debido a la autenticación tooToken. |
| HTTP Response Codes |Proporciona un desglose de los códigos de estado de hello HTTP (por ejemplo, 200 Aceptar, 403 Prohibido, 404 no encontrado, etc.) que se enviaron los clientes tooyour HTTP por nuestros servidores de borde. Un gráfico circular permite tooquickly evaluar cómo se atienden los activos. Se proporcionan datos estadísticos detallados para cada código de respuesta por debajo del gráfico de Hola. |
| 404 Errors |Contiene un gráfico de barras que le permite tooview Hola top 10 solicitudes que dan como resultado un código de respuesta 404 no encontrado. |
| 403 Errors |Contiene un gráfico de barras que le permite tooview Hola top 10 solicitudes que dan como resultado un código de respuesta 403 Prohibido. Un código de respuesta 403 Prohibido se produce cuando una solicitud ha sido denegada por el servidor de origen de un cliente o un servidor perimetral en nuestro POP. |
| 4xx Errors |Contiene un gráfico de barras que le permite tooview Hola top 10 solicitudes que dan como resultado un código de respuesta en el intervalo de 400 Hola. Los códigos de respuesta 403 Prohibido y 404 No encontrado están excluidos de este informe. Normalmente, un código de respuesta 4xx se produce cuando se deniega una solicitud debido a un error de cliente. |
| 504 Errors |Contiene un gráfico de barras que le permite tooview Hola top 10 solicitudes que dan como resultado un código de respuesta 504 tiempo de espera de puerta de enlace. Un código de respuesta 504 tiempo de espera de puerta de enlace se produce cuando se produce un tiempo de espera cuando un proxy HTTP está tratando de toocommunicate con otro servidor. En caso de hello de la red CDN, un código de respuesta de tiempo de espera de puerta de enlace 504 normalmente se produce cuando un servidor perimetral no se puede tooestablish comunicación con un servidor de origen del cliente. |
| 502 Errors |Contiene un gráfico de barras que le permite tooview Hola top 10 solicitudes que dan como resultado un código de respuesta 502 de puerta de enlace errónea. Un código de respuesta 502 Puerta de enlace incorrecta aparece cuando se produce un error de protocolo HTTP entre un servidor y un proxy HTTP. En caso de hello de la red CDN, un código de respuesta de puerta de enlace errónea 502 normalmente se produce cuando un servidor de origen del cliente devuelve un servidor perimetral de tooan de respuesta no válida. Una respuesta no es válida si no se puede analizar o si está incompleta. |
| 5xx Errors |Contiene un gráfico de barras que le permite tooview Hola top 10 solicitudes que dan como resultado un código de respuesta en el rango 500 Hola.  Los códigos de respuesta 502 Puerta de enlace incorrecta y 504 Tiempo de espera agotado para la puerta de enlace, están excluidos de este informe. |

## <a name="see-also"></a>Consulte también
* [Información general de la red CDN de Azure](cdn-overview.md)
* [Estadísticas en tiempo real en CDN de Microsoft Azure](cdn-real-time-stats.md)
* [Invalidar el comportamiento HTTP predeterminado mediante el motor de reglas de Hola](cdn-rules-engine.md)
* [Informes de HTTP avanzados](cdn-advanced-http-reports.md)

