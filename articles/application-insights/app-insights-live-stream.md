---
title: "Secuencia de métricas con métricas personalizadas y diagnósticos en Azure Application Insights aaaLive | Documentos de Microsoft"
description: "Supervise la aplicación web en tiempo real con métricas personalizadas y diagnostique problemas con una fuente directa de errores, seguimientos y eventos."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: bwren
ms.openlocfilehash: 68ddfbf387379ea778c20280c4ec96baa06d3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a>Live Metrics Stream: supervisión y diagnóstico con una latencia de 1 segundo 

Sondeo de núcleo de latidos de hello de la aplicación web en directo, en producción mediante el uso de la secuencia en directo de las métricas de [Application Insights](app-insights-overview.md). Seleccionar y filtrar las métricas y rendimiento toowatch de contadores en tiempo real, sin ningún servicio de tooyour alteraciones. Inspeccione seguimientos de la pila procedentes de ejemplos de errores de solicitudes y excepciones. Junto con [Profiler](app-insights-profiler.md), el [depurador de instantáneas](app-insights-snapshot-debugger.md) y la [prueba de rendimiento](app-insights-monitor-web-app-availability.md#performance-tests), Live Metrics Stream proporciona una herramienta de diagnóstico eficaz y no invasiva para sitios web activos.

Con Live Metrics Stream, puede:

* Inspeccionar el rendimiento y los recuentos de errores mientras se publica una solución para validarla.
* Ver el efecto de Hola de probar las cargas máximas y diagnosticar problemas en vivo. 
* Centrarse en las sesiones de pruebas determinado o filtrar los problemas conocidos, seleccionar y filtrar las métricas de hello desea toowatch.
* Obtener seguimientos de las excepciones cuando se produzcan.
* Experimente con filtros toofind Hola KPI más relevantes.
* Supervisar cualquier contador de rendimiento de Windows en tiempo real.
* Fácilmente identificar un servidor que tiene problemas y filtrar Hola todos los KPI/live toojust fuente ese servidor.

[![Vídeo de Live Metrics Stream](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)

Secuencia en directo de métricas está actualmente disponible en aplicaciones ASP.NET que se ejecutan en local o en hello en la nube. 

## <a name="get-started"></a>Primeros pasos

1. Si aún no ha [instalado Application Insights](app-insights-asp-net.md) en la aplicación web de ASP.NET o la [aplicación de Windows Server](app-insights-windows-services.md), hágalo ahora. 
2. **Una versión más reciente de actualización toohello** del paquete de Application Insights Hola. En Visual Studio, haga clic con el botón derecho en el proyecto y elija **Administrar paquetes NuGet**. Hola abierto **actualizaciones** ficha, verificación **incluir versión preliminar**y seleccione todos los paquetes de Microsoft.ApplicationInsights.* Hola.

    Vuelva a implementar la aplicación.

3. Hola [portal de Azure](https://portal.azure.com), abra el recurso de Application Insights de hello para la aplicación y, a continuación, abra la secuencia en directo.

4. [Canal de control seguro hello](#secure-the-control-channel) si puede usar los datos confidenciales como nombres de cliente en los filtros.


![En la hoja de información general de hello, haga clic en secuencia en directo](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a>¿No hay datos? Comprobación del firewall del servidor

Comprobar hello [puertos de salida de la secuencia en directo de métricas](app-insights-ip-addresses.md#outgoing-ports) están abiertos en firewall de Hola de los servidores. 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a>¿En qué se diferencia Live Metrics Stream de Explorador de métricas y Analytics?

| |Live Stream | Explorador de métricas y Analytics |
|---|---|---|
|Latency|Los datos se muestran en un segundo.|La agregación se realiza en minutos.|
|Sin retención|Datos que se conservan mientras se está en el gráfico de hello y, a continuación, se descartan|[Los datos se conservan durante 90 días.](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|A petición|Se transmiten datos mientras se abre Live Metrics.|Los datos se envían cuando Hola SDK está instalado y habilitado|
|Gratuito|No se efectúa ningún cargo por los datos de Live Stream.|Asunto demasiado[precios](app-insights-pricing.md)
|muestreo|Se transmiten todas las métricas y los contadores seleccionados. Se muestrean los errores y seguimientos de la pila. No se aplican elementos TelemetryProcessor.|Se pueden [muestrear](app-insights-api-filtering-sampling.md) eventos.|
|Canal de control|Las señales de control de filtro se envían toohello SDK. Se recomienda [proteger este canal](#secure-channel).|La comunicación es unidireccional, toohello portal|


## <a name="select-and-filter-your-metrics"></a>Selección y filtrado de métricas

(Disponible en clásico aplicaciones ASP.NET con Hola SDK más reciente.)

Puede supervisar KPI personalizado en vivo aplicando filtros arbitrarios en cualquier telemetría de Application Insights desde el portal de Hola. Haga clic en el control de filtro de Hola que muestra al pasar el mouse cualquiera de los gráficos de Hola. Hola después de gráfico es trazar un número de solicitudes personalizado KPI con filtros en atributos de dirección URL y la duración. Validar los filtros con hello sección de vista previa de flujo que muestra una fuente directa de telemetría que coincida con los criterios de Hola que ha especificado en cualquier momento en el tiempo. 

![KPI personalizado de solicitudes](./media/app-insights-live-stream/live-stream-filteredMetric.png)

Puede supervisar un valor que no sea el de recuento. Opciones de Hello dependen de tipo hello de secuencia, que puede ser cualquier telemetría de Application Insights: solicitudes, dependencias, excepciones, seguimientos, eventos o las métricas. Puede ser su propia [medida personalizada](app-insights-api-custom-events-metrics.md#properties):

![Opciones de valor](./media/app-insights-live-stream/live-stream-valueoptions.png)

Además tooApplication telemetría de visión, también puede supervisar cualquier contador de rendimiento de Windows seleccionando de opciones de flujo de Hola y proporcionar nombre Hola Hola del contador de rendimiento.

Las métricas activas se agregan en dos puntos: localmente en cada servidor y, a continuación, en todos los servidores. Puede cambiar predeterminado de hello en seleccionando otras opciones en hello respectivos listas desplegables.

## <a name="sample-telemetry-custom-live-diagnostic-events"></a>Telemetría de ejemplo: eventos personalizados de diagnóstico en vivo
De forma predeterminada, fuente directa de Hola de eventos muestra ejemplos de solicitudes con error y llamadas de dependencia, excepciones, eventos y seguimientos. Haga clic en criterios Hola aplica toosee de icono de filtro de Hola en cualquier momento en el tiempo. 

![Fuente directa predeterminada](./media/app-insights-live-stream/live-stream-eventsdefault.png)

Como con métricas, puede especificar cualquier tooany criterios arbitrarios de tipos de telemetría de Application Insights Hola. En este ejemplo, seleccionaremos los eventos, seguimientos y errores de solicitud específicos. También se han seleccionado todas las excepciones y errores de dependencia.

![Fuente personalizada en vivo](./media/app-insights-live-stream/live-stream-events.png)

Nota: Actualmente, por criterios basada en mensajes de excepción, use mensaje de excepción de extremo de saludo. Hola anterior ejemplo, toofilter out excepción supone un riesgo de hello con mensaje de excepción interna (sigue Hola "<--" delimitador) ""Hola cliente desconectado. Use un mensaje que no contenga criterios de error al leer el contenido de la solicitud.

Ver detalles de Hola de un elemento de hello live fuente haciendo clic en él. Puede pausar Hola fuente haciendo clic en **pausar** simplemente desplazarse hacia abajo o haga clic en un elemento. Fuente directa se reanudará una vez que se desplaza toohello Atrás arriba, o haciendo clic en el contador de Hola de elementos recopilados mientras estaba en pausa.

![Errores de muestreo de Live](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a>Filtrado por instancia de servidor

Si desea toomonitor una instancia de rol de servidor en particular, puede filtrar por servidor.

![Errores de muestreo de Live](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a>Requisitos de SDK
Las secuencias personalizadas de Live Metrics Stream están disponibles con la versión 2.4.0-beta2 o la más reciente del [SDK de Application Insights para la web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/). Recuerde la opción de "Incluye versión preliminar" tooselect desde el Administrador de paquetes de NuGet.

## <a name="secure-hello-control-channel"></a>Proteger el canal de control de Hola
criterios de filtros personalizados de Hola que especifique se envían componente de métricas de Live toohello atrás en hello Application Insights SDK. filtros de Hello podrían contener información confidencial, como customerIDs. Puede hacer canal Hola seguro con una clave secreta de API además toohello clave de instrumentación.
### <a name="create-an-api-key"></a>Creación de una clave de API

![Creación de una clave de API](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-tooconfiguration"></a>Agregar tooConfiguration clave de API
En el archivo applicationinsights.config de hello, agregue hello AuthenticationApiKey toohello QuickPulseTelemetryModule:
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
O bien, en el código, establezca esta opción en Hola QuickPulseTelemetryModule:

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

Sin embargo, si lo reconoce y confía que Hola a todos los servidores conectados, puede intentar filtros personalizados de hello sin canal Hola autenticado. Esta opción está disponible durante seis meses. Esta invalidación se requiere una vez cada nueva sesión, o cuando se pone en línea un nuevo servidor.

![Opciones de autenticación de Live Metrics](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
>Se recomienda que configure canal Hola autenticado antes de introducir información potencialmente confidencial, como CustomerID en criterios de filtro de Hola.
>

## <a name="generating-a-performance-test-load"></a>Generación de una carga de prueba de rendimiento

Si desea aumentar toowatch efecto de Hola de una carga, hoja de prueba de rendimiento de uso Hola. Simula solicitudes de varios usuarios simultáneos. Se pueden ejecutar cualquier "pruebas manuales" (ping pruebas) de una sola dirección URL, o puede ejecutarse un [prueba de rendimiento web de varios pasos](app-insights-monitor-web-app-availability.md#multi-step-web-tests) que se carga (de Hola de igual forma que una disponibilidad de prueba).

> [!TIP]
> Después de crear la prueba de rendimiento de hello, abra la prueba de Hola y Hola hoja de secuencia en directo en ventanas independientes. Puede ver al hello en cola inicia de prueba de rendimiento y la secuencia en directo de inspección en hello mismo tiempo.
>


## <a name="troubleshooting"></a>Solución de problemas

¿No hay datos? Si la aplicación está en una red protegida, Live Metrics Stream usará una dirección IP diferente que otra telemetría de Application Insights. Asegúrese de que [esas direcciones IP](app-insights-ip-addresses.md) están abiertos en el firewall.



## <a name="next-steps"></a>Pasos siguientes
* [Supervisión del uso con Application Insights](app-insights-web-track-usage.md)
* [Uso de la Búsqueda de diagnóstico](app-insights-diagnostic-search.md)
* [Generador de perfiles](app-insights-profiler.md)
* [Depurador de instantáneas](app-insights-snapshot-debugger.md)
