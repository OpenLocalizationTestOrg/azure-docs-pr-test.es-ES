---
title: "datos de la aplicación de Azure Application Insights aaaView | Documentos de Microsoft"
description: "Puede usar los problemas de rendimiento Hola Application Insights Connector solución toodiagnose y entender qué hacer los usuarios con la aplicación al supervisar con Application Insights."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 49280cad-3526-43e1-a365-c6a3bf66db52
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: banders
ms.openlocfilehash: 38109337ebbc8970dccb65365ba8284d9cee19a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-connector-solution-preview-in-operations-management-suite-oms"></a>Solución Application Insights Connector (versión preliminar) en Operations Management Suite (OMS)

![Símbolo de Application Insights](./media/log-analytics-app-insights-connector/app-insights-connector-symbol.png)

Hola solución de conector de visión de las aplicaciones le ayuda a diagnosticar problemas de rendimiento y determinar las características a los usuarios con la aplicación cuando se esté supervisando con [Application Insights](../application-insights/app-insights-overview.md). Vistas de hello mismo telemetría de aplicación que los desarrolladores ven en Application Insights están disponibles en OMS. Sin embargo, cuando integra las aplicaciones de Application Insights con OMS, la visibilidad de las aplicaciones aumenta debido a que los datos de operación y de aplicación están en el mismo lugar. Tener Hola mismo vistas le ayuda a toocollaborate con los desarrolladores de aplicaciones. vistas comunes de Hello pueden ayudar a reducir Hola tiempo toodetect y resolver la aplicación y problemas de plataforma.

Cuando se utiliza la solución de hello, hacer lo siguiente:

- Ver todas las aplicaciones de Application Insights en un solo lugar, incluso si se encuentran en suscripciones de Azure distintas.
- Correlacionar datos de infraestructura con datos de aplicación.
- Visualizar datos de aplicación con perspectivas en la búsqueda de registros.
- Tabla dinámica de análisis de registros datos tooyour Application Insights aplicación Hola OMS y los portales de Azure

## <a name="connected-sources"></a>Orígenes conectados

A diferencia de la mayoría de soluciones de análisis de registros, no se recopilan los datos de hello Application Insights Connector por los agentes. Todos los datos utilizados por la solución de hello proceden directamente de Azure.

| Origen conectado | Compatible | Descripción |
| --- | --- | --- |
| [Agentes de Windows](log-analytics-windows-agents.md) | No | solución de Hello no recopila información de agentes de Windows. |
| [Agentes de Linux](log-analytics-linux-agents.md) | No | solución de Hello no recopilar información de agentes de Linux. |
| [Grupo de administración de SCOM](log-analytics-om-agents.md) | No | solución de Hello no recopila información de agentes en un grupo de administración de SCOM conectado. |
| [Cuenta de Almacenamiento de Azure](log-analytics-azure-storage.md) | No | solución de Hello no no información de recopilación del almacenamiento de Azure. |

## <a name="prerequisites"></a>Requisitos previos

- tooaccess información de conector de visión de la aplicación, debe tener una suscripción de Azure
- Debe tener como mínimo un recurso de Application Insights configurado.
- Debe ser propietario de Hola o colaborador de hello recursos de Application Insights.

## <a name="configuration"></a>Configuración

1. Habilitar la solución de análisis de aplicaciones Web de Azure Hola de hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ApplicationInsights?tab=Overview) o mediante el proceso de hello descrito en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).
2. En el portal de OMS de hello, haga clic en **configuración** &gt; **datos** &gt; **Application Insights**.
3. En **Seleccionar una suscripción**, seleccione una suscripción que tenga recursos de Application Insights y, luego, en **Nombre de la aplicación**, seleccione una o varias aplicaciones.
4. Haga clic en **Guardar**.

En aproximadamente 30 minutos, los datos están disponibles y Hola Application Insights icono se actualiza con datos, como Hola después de imagen:

![Icono de Application Insights](./media/log-analytics-app-insights-connector/app-insights-tile.png)

Otros puntos tookeep en cuenta:

- Sólo se puede vincular el área de trabajo de Application Insights aplicaciones tooone OMS.
- Sólo se puede vincular [recursos estándar o Premium Application Insights](https://azure.microsoft.com/pricing/details/application-insights) tooOMS análisis de registros. Sin embargo, puede usar el nivel gratuito de Hola de análisis de registros.

## <a name="management-packs"></a>Módulos de administración

Esta solución no instala ningún módulo de administración en grupos de administración conectados.

## <a name="use-hello-solution"></a>Utilice la solución Hola

Hello las secciones siguientes describen cómo puede usar módulos de Hola que se muestra en el panel tooview de hello Application Insights e interactuar con los datos de las aplicaciones.

### <a name="view-application-insights-connector-information"></a>Visualización de la información de Application Insights Connector

Haga clic en hello **Application Insights** icono tooopen hello **Application Insights** Hola de toosee panel después de hojas.

![Panel Application Insights](./media/log-analytics-app-insights-connector/app-insights-dash01.png)

![Panel Application Insights](./media/log-analytics-app-insights-connector/app-insights-dash02.png)

panel de Hello incluye módulos de Hola que se muestra en la tabla de Hola. Cada hoja se enumera los elementos de too10 coincidentes que han especificado criterios del módulo para hello ámbito y el tiempo de intervalo. Puede ejecutar una búsqueda de registros que devuelve todos los registros al hacer clic en **ver todas** en parte inferior de la hoja de Hola o al hacer clic en el encabezado de la hoja de Hola de Hola.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

| **Columna** | **Descripción** |
| --- | --- |
| Aplicaciones: número de aplicaciones | Muestra el número de Hola de aplicaciones de recursos de la aplicación. También aplicación listas de nombres y para cada uno, Hola recuento de registros de aplicación. Haga clic en hello número toorun una búsqueda de registros de<code>Type=ApplicationInsights &#124; measure sum(SampledCount) by ApplicationName</code> <br><br>  Haga clic en un toorun de nombre de aplicación una búsqueda de registros de aplicación Hola que muestra registros de aplicaciones por host, los registros de tipo de telemetría y todos los datos por tipo (basado en hello último día). |
| Volumen de datos: hosts que envían datos | Muestra el número de Hola de hosts de equipo que envían datos. También muestra los hosts de equipos y números de registros para cada host. Haga clic en hello número toorun una búsqueda de registros de<code>Type=ApplicationInsights &#124; measure sum(SampledCount) by Host</code> <br><br> Haga clic en un toorun de nombre de equipo una búsqueda de registro de host de Hola que muestra registros de aplicaciones por host, los registros de tipo de telemetría y todos los datos por tipo (basado en hello último día). |
| Disponibilidad: resultados de WebTest | Muestra un gráfico de anillos para los resultados de pruebas web, que indican una prueba correcta o errónea. Haga clic en hello gráfico toorun una búsqueda de registros de<code>Type=ApplicationInsights TelemetryType=Availability &#124; measure sum(SampledCount) by AvailabilityResult</code> <br><br> Resultados Mostrar número de Hola de pasadas y con errores para todas las pruebas. Muestra todas las aplicaciones Web con tráfico de hello en el último minuto. Haga clic en un tooview de nombre de la aplicación una búsqueda de registros con los detalles de las pruebas web error. |
| Solicitudes de servidor: solicitudes por hora | Muestra un gráfico de líneas de hello las solicitudes del servidor por hora para varias aplicaciones. Mantenga el mouse sobre una línea en hello gráfico toosee Hola 3 las aplicaciones principales recibir las solicitudes de un punto en el tiempo. También muestra una lista de aplicaciones de Hola recibir solicitudes y número de Hola de solicitudes durante el período de hello seleccionado. <br><br>Haga clic en hello gráfico toorun una búsqueda de registros para <code>Type=ApplicationInsights TelemetryType=Request &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> que muestra un gráfico de líneas más detallado de hello las solicitudes del servidor por hora para varias aplicaciones. <br><br> Haga clic en una aplicación en hello lista toorun una búsqueda de registros para <code>Type=ApplicationInsights  ApplicationName=yourapplicationname  TelemetryType=Request</code> que muestra una lista de las solicitudes, gráficos para las solicitudes a través de una duración de tiempo y la solicitud y una lista de solicitud de códigos de respuesta.   |
| Errores: solicitudes erróneas por hora | Muestra un gráfico de líneas de las solicitudes de aplicación erróneas por hora. Mantenga el mouse sobre Hola gráfico toosee Hola 3 aplicaciones principales con las solicitudes con error para un punto en el tiempo. También muestra una lista de aplicaciones con el número de Hola de solicitudes con error para cada uno. Haga clic en hello gráfico toorun una búsqueda de registros para <code>Type=ApplicationInsights TelemetryType=Request  RequestSuccess = false &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> que muestra un gráfico de líneas más detallado de las solicitudes de aplicación que ha fallado. <br><br>Haga clic en un elemento de hello lista toorun una búsqueda de registros para <code>Type=ApplicationInsights ApplicationName=yourapplicationname TelemetryType=Request  RequestSuccess=false</code> que se muestra en solicitudes erróneas, gráficos para solicitudes con error a través de una duración de tiempo y la solicitud y una lista de códigos de respuesta de solicitudes con error. |
| Excepciones: excepciones por hora | Muestra un gráfico de líneas de las excepciones por hora. Mantenga el mouse sobre Hola gráfico toosee Hola 3 aplicaciones principales con excepciones para un punto en el tiempo. También muestra una lista de aplicaciones con el número de Hola de excepciones para cada uno. Haga clic en hello gráfico toorun una búsqueda de registros para <code>Type=ApplicationInsights TelemetryType=Exception &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> que muestra un gráfico de vínculo más detallado de las excepciones. <br><br>Haga clic en un elemento de hello lista toorun una búsqueda de registros para <code>Type=ApplicationInsights  ApplicationName=yourapplicationname TelemetryType=Exception</code> que muestra una lista de excepciones, los gráficos de las excepciones a través de las solicitudes de tiempo pero no lo consiguió y una lista de tipos de excepción.  |

### <a name="view-hello-application-insights-perspective-with-log-search"></a>Ver la perspectiva de Application Insights Hola con búsqueda de registros

Al hacer clic en cualquier elemento de panel de hello, verá una perspectiva de Application Insights que se muestra en la búsqueda. perspectiva de Hello proporciona una visualización extendida, en función de tipo de telemetría de Hola que ha seleccionado. Por lo tanto, el contenido de la visualización cambia según los distintos tipos de telemetría.

Al hacer clic en cualquier parte en la hoja de aplicaciones de hello, vea predeterminado hello **aplicaciones** perspectiva.

![Perspectiva Aplicaciones de Application Insights](./media/log-analytics-app-insights-connector/applications-blade-drill-search.png)

perspectiva de Hello muestra un resumen de la aplicación hello que seleccionó.

Hola **disponibilidad** hoja muestra una vista en perspectiva diferentes donde puede ver los resultados de pruebas web y las solicitudes relacionadas con error.

![Perspectiva Disponibilidad de Application Insights](./media/log-analytics-app-insights-connector/availability-blade-drill-search.png)

Al hacer clic en cualquier lugar en hello **solicitudes de servidor** o **errores** hojas, perspectiva Hola componentes cambien toogive es una visualización que relacionan toorequests.

![Hoja Errores de Application Insights](./media/log-analytics-app-insights-connector/server-requests-failures-drill-search.png)

Al hacer clic en cualquier lugar en hello **excepciones** hoja, verá una visualización que se adapta tooexceptions.

![Hoja Excepciones de Application Insights](./media/log-analytics-app-insights-connector/exceptions-blade-drill-search.png)

Independientemente de si hace clic en algo uno hello **Application Insights Connector** panel dentro de hello **búsqueda** página, cualquier consulta que devuelve datos de Application Insights muestran hello Perspectiva de visión de la aplicación. Por ejemplo, si está viendo los datos de Application Insights, una **&#42;** consulta también muestra la pestaña de la perspectiva de hello como Hola después de la imagen:

![Application Insights ](./media/log-analytics-app-insights-connector/app-insights-search.png)

Componentes de perspectiva se actualizan en función de consulta de búsqueda de Hola. Esto significa que puede filtrar los resultados de hello mediante el uso de cualquier campo de búsqueda que proporciona Hola capacidad toosee Hola datos desde:

- Todas las aplicaciones
- Una sola aplicación seleccionada
- Un grupo de aplicaciones

### <a name="pivot-tooan-app-in-hello-azure-portal"></a>Pivot tooan aplicación Hola portal de Azure

Las hojas de conector de visión de aplicación son tooenable diseñada seleccionado se toopivot toohello aplicación Application Insights *al usar el portal de OMS hello*. Puede usar soluciones de hello como una plataforma de supervisión de alto nivel que le ayude a solucionar problemas de una aplicación. Cuando vea un posible problema en cualquiera de las aplicaciones conectadas, puede que cualquier profundizar en la búsqueda OMS o puede dinamizar directamente toohello Application Insights aplicación.

toopivot, haga clic en el botón de puntos suspensivos hello (**...** ) que aparece al final de Hola de cada línea y seleccione **abierto en Application Insights**.

>[!NOTE]
>**Abrir en Application Insights** no está disponible en hello portal de Azure.

![Abrir en Application Insights](./media/log-analytics-app-insights-connector/open-in-app-insights.png)

### <a name="sample-corrected-data"></a>Datos de ejemplo corregidos

Proporciona información de la aplicación  *[muestreo corrección](../application-insights/app-insights-sampling.md)*  toohelp reducir el tráfico de telemetría. Cuando se habilita el muestreo en la aplicación de Application Insights, obtiene un número reducido de entradas almacenadas en Application Insights y en OMS. Mientras se conserva la coherencia de los datos en hello **Application Insights Connector** página y perspectivas, debe corregir manualmente los datos de ejemplo para las consultas personalizadas.

A continuación, se muestra un ejemplo de una corrección de muestreo en una consulta de búsqueda de registros:

```
Type=ApplicationInsights | measure sum(SampledCount) by TelemetryType
```

Hola **muestrear recuento** campo está presente en todas las entradas y muestra Hola número de puntos de datos que representa la entrada de Hola. Si activa el muestreo para la aplicación de Application Insights, el campo **Sampled Count** es mayor que 1. toocount Hola número real de entradas que genera, a la aplicación hello suma **muestrear recuento** campos.

Muestreo afecta solo Hola número total de entradas que genera la aplicación. No es necesario toocorrect de muestreo para campos métricas como **RequestDuration** o **AvailabilityDuration** porque esos campos mostrar promedio de Hola para entradas representadas.

## <a name="input-data"></a>Datos de entrada

solución de Hello recibe Hola siguientes tipos de telemetría de datos de las aplicaciones de Application Insights conectadas:

- Disponibilidad
- Excepciones
- Solicitudes
- Vistas de página de vistas de página: para su tooreceive de área de trabajo, debe configurar su toocollect aplicaciones esa información. Para más información, consulte [PageViews](../application-insights/app-insights-api-custom-events-metrics.md#page-views).
- Eventos personalizados: para los eventos personalizados tooreceive de área de trabajo, debe configurar su toocollect aplicaciones esa información. Para más información, consulte [TrackEvent](../application-insights/app-insights-api-custom-events-metrics.md#trackevent).

OMS recibe los datos desde Application Insights en cuanto están disponibles.

## <a name="output-data"></a>Datos de salida

Se crea un registro con un *tipo* de *ApplicationInsights* para cada tipo de datos de entrada. Registros de ApplicationInsights tienen propiedades que se muestran en hello las secciones siguientes:

### <a name="generic-fields"></a>Campos genéricos

| Propiedad | Descripción |
| --- | --- |
| Tipo | ApplicationInsights |
| ClientIP |   |
| TimeGenerated | Tiempo de registro de hello |
| ApplicationId | Clave de instrumentación de la aplicación de hello Application Insights |
| ApplicationName | Nombre de aplicación de hello Application Insights |
| RoleInstance | Identificador del host del servidor |
| DeviceType | Dispositivo de cliente |
| ScreenResolution |   |
| Continent | Continente donde se originó la solicitud de Hola |
| País | País donde se originó la solicitud de Hola |
| Province | Provincia, estado o configuración regional donde Hola solicitud se originó |
| City | Ciudad o localidad donde se originó la solicitud de Hola |
| isSynthetic | Indica si se creó la solicitud de Hola por un usuario o por el método automatizado. True = generada por el usuario o false = método automatizado |
| SamplingRate | Porcentaje de telemetría generado por hello SDK que se envía tooportal. Intervalo 0,0 a 100,0. |
| SampledCount | 100/(SamplingRate). Por ejemplo, 4 =&gt; 25 % |
| IsAuthenticated | Verdadero o falso |
| OperationID | Elementos que tienen el mismo Id. de operación se muestran como elementos relacionados en el portal de Hola de Hola. Hola normalmente el identificador de la solicitud |
| ParentOperationID | Id. de operación de hello primario |
| nombreOperación |   |
| SessionId | GUID toouniquely identificar sesión Hola donde se creó la solicitud de Hola |
| SourceSystem | ApplicationInsights |

### <a name="availability-specific-fields"></a>Campos específicos de disponibilidad

| Propiedad | Descripción |
| --- | --- |
| TelemetryType | Disponibilidad |
| AvailabilityTestName | Nombre de la prueba de hello web |
| AvailabilityRunLocation | Origen geográfico de la solicitud HTTP |
| AvailabilityResult | Indica el resultado de éxito de Hola de prueba de hello web |
| AvailabilityMessage | mensaje de saludo adjunta toohello de prueba web |
| AvailabilityCount | 100/(velocidad de muestreo). Por ejemplo, 4 =&gt; 25 % |
| DataSizeMetricValue | 1,0 o 0,0 |
| DataSizeMetricCount | 100/(velocidad de muestreo). Por ejemplo, 4 =&gt; 25 % |
| AvailabilityDuration | Tiempo, en milisegundos, de duración de la prueba web Hola |
| AvailabilityDurationCount | 100/(velocidad de muestreo). Por ejemplo, 4 =&gt; 25 % |
| AvailabilityValue |   |
| AvailabilityMetricCount |   |
| AvailabilityTestId | GUID único para la prueba de hello web |
| AvailabilityTimestamp | Marca de tiempo precisa de prueba de disponibilidad de Hola |
| AvailabilityDurationMin | Para los registros muestreados, este campo muestra hello web mínimo duración de la prueba (milisegundos) Hola representan puntos de datos |
| AvailabilityDurationMax | Para los registros muestreados, este campo muestra hello web máxima duración de la prueba (milisegundos) Hola representan puntos de datos |
| AvailabilityDurationStdDev | Para los registros muestreados, este campo muestra la desviación estándar de hello entre todas las duraciones de prueba de web (milisegundos) Hola representan puntos de datos |
| AvailabilityMin |   |
| AvailabilityMax |   |
| AvailabilityStdDev | &nbsp;  |

### <a name="exception-specific-fields"></a>Campos específicos de excepción

| Tipo | ApplicationInsights |
| --- | --- |
| TelemetryType | Excepción |
| ExceptionType | Tipo de excepción de Hola |
| ExceptionMethod | método Hello que crea excepciones Hola |
| ExceptionAssembly | Ensamblado incluye framework hello y versión, así como el token de clave pública de Hola |
| ExceptionGroup | Tipo de excepción de Hola |
| ExceptionHandledAt | Indica el nivel de Hola que controla la excepción de Hola |
| ExceptionCount | 100/(velocidad de muestreo). Por ejemplo, 4 =&gt; 25 % |
| ExceptionMessage | Mensaje de excepción de Hola |
| ExceptionStack | Completo de la pila de excepción de Hola |
| ExceptionHasStack | Verdadero, si la excepción tiene una pila |



### <a name="request-specific-fields"></a>Campos específicos de solicitud

| Propiedad | Descripción |
| --- | --- |
| Tipo | ApplicationInsights |
| TelemetryType | Solicitud |
| ResponseCode | Tooclient de respuesta enviado de HTTP |
| RequestSuccess | Indica una solicitud correcta o errónea. True o false. |
| RequestID | Id. toouniquely identificar la solicitud de Hola |
| RequestName | GET/POST + dirección URL base |
| RequestDuration | Tiempo, en segundos de duración de la solicitud de Hola |
| URL | Dirección URL de solicitud de hello sin incluir el host |
| Host | Host del servidor web |
| URLBase | Dirección URL completa de la solicitud de Hola |
| ApplicationProtocol | Tipo de protocolo utilizado por la aplicación hello |
| RequestCount | 100/(velocidad de muestreo). Por ejemplo, 4 =&gt; 25 % |
| RequestDurationCount | 100/(velocidad de muestreo). Por ejemplo, 4 =&gt; 25 % |
| RequestDurationMin | Para los registros muestreados, este campo muestra la duración de solicitud mínima de hello (milisegundos) Hola representan puntos de datos. |
| RequestDurationMax | Para los registros muestreados, este campo muestra duración de máximo de la solicitud de hello (milisegundos) Hola representan puntos de datos |
| RequestDurationStdDev | Para los registros muestreados, este campo muestra desviación estándar de hello entre todas las duraciones de solicitud (milisegundos) Hola representan puntos de datos |

## <a name="sample-log-searches"></a>Búsquedas de registros de ejemplo

Esta solución no tiene un conjunto de búsquedas de registros de ejemplo que se muestra en el panel de Hola. Sin embargo, se muestran las consultas de búsqueda del registro de ejemplo con descripciones de hello [información de vista Application Insights Connector](#view-application-insights-connector-information) sección.

## <a name="next-steps"></a>Pasos siguientes

- Use [Log Search](log-analytics-log-searches.md) tooview información detallada acerca de las aplicaciones de Application Insights.
