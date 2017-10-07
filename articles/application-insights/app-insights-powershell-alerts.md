---
title: aaaUse Powershell tooset alertas en Application Insights | Documentos de Microsoft
description: "Automatizar la configuración de Application Insights tooget correos de todos los cambios de métrica."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 05d6a9e0-77a2-4a35-9052-a7768d23a196
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: d68e5f9511bb4015f59175724bc1a4a04ecf43e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooset-alerts-in-application-insights"></a>Usar PowerShell tooset alertas en Application Insights
Puede automatizar la configuración de hello [alertas](app-insights-alerts.md) en [Application Insights](app-insights-overview.md).

Además, puede [establecer la alerta de tooan de respuesta de webhooks tooautomate](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

> [!NOTE]
> Si desea que los recursos de toocreate y alertas en Hola mismo tiempo, considere la posibilidad de [usando una plantilla de Azure Resource Manager](app-insights-powershell.md).
>
>

## <a name="one-time-setup"></a>Instalación única
Si no ha usado PowerShell con su suscripción de Azure antes:

Instale el módulo de Powershell de Azure de hello en la máquina de Hola donde desea que las secuencias de comandos de toorun Hola.

* Instale el [Instalador de plataforma web de Microsoft (v5 o superior)](http://www.microsoft.com/web/downloads/platform.aspx).
* Usar tooinstall Microsoft Azure Powershell

## <a name="connect-tooazure"></a>Conectar tooAzure
Inicie PowerShell de Azure y [conectar tooyour suscripción](/powershell/azure/overview):

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a>Obtención de alertas
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a>Agregar alerta
    Add-AlertRule  -Name "{ALERT NAME}" -Description "{TEXT}" `
     -ResourceGroup "{GROUP NAME}" `
     -ResourceId "/subscriptions/{SUBSCRIPTION ID}/resourcegroups/{GROUP NAME}/providers/microsoft.insights/components/{APP RESOURCE NAME}" `
     -MetricName "{METRIC NAME}" `
     -Operator GreaterThan  `
     -Threshold {NUMBER}   `
     -WindowSize {HH:MM:SS}  `
     [-SendEmailToServiceOwners] `
     [-CustomEmails "EMAIL1@X.COM","EMAIL2@Y.COM" ] `
     -Location "East US" // must be East US at present
     -RuleType Metric



## <a name="example-1"></a>Ejemplo 1
Enviarme un correo electrónico si las solicitudes de tooHTTP de respuesta del servidor de hello, promedio de más de 5 minutos, es menor que 1 segundo. Mi recurso de Application Insights se denomina IceCreamWebApp, y está en el grupo de recursos Fabrikam. Soy propietario Hola de hello suscripción de Azure.

Hola GUID es el Id. de suscripción de hello (no Hola clave de instrumentación de la aplicación hello).

    Add-AlertRule -Name "slow responses" `
     -Description "email me if hello server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a>Ejemplo 2
Tengo una aplicación en el que utilizo [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport una métrica con el nombre "salesPerHour." Enviar un correo electrónico toomy compañeros si "salesPerHour" cae por debajo de 100, promedio de más de 24 horas.

    Add-AlertRule -Name "poor sales" `
     -Description "slow sales alert" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "salesPerHour" `
     -Operator LessThan `
     -Threshold 100 `
     -WindowSize 24:00:00 `
     -CustomEmails "satish@fabrikam.com","lei@fabrikam.com" `
     -Location "East US" -RuleType Metric

Hola misma regla puede usarse para la métrica de hello informes utilizando hello [parámetro medida](app-insights-api-custom-events-metrics.md#properties) de seguimiento de otra llamada como TrackEvent o trackPageView.

## <a name="metric-names"></a>Nombres de métrica
| Nombre de métrica | Nombre de pantalla | Descripción |
| --- | --- | --- |
| `basicExceptionBrowser.count` |Excepciones de explorador |Recuento de excepciones no detectadas en el Explorador de Hola. |
| `basicExceptionServer.count` |Excepciones de servidor |Recuento de las excepciones no controladas producidas por la aplicación hello |
| `clientPerformance.clientProcess.value` |Tiempo de procesamiento del cliente |Tiempo transcurrido entre recibir el último byte de un documento Hola hasta que se cargue DOM Hola. Todavía se pueden procesar solicitudes asincrónicas. |
| `clientPerformance.networkConnection.value` |Tiempo de conexión de red de carga de página |Explorador de hello tiempo toma tooconnect toohello red. Puede ser 0 si se almacena en caché. |
| `clientPerformance.receiveRequest.value` |Tiempo de recepción de respuesta |Tiempo transcurrido entre el explorador envía solicitud toostarting tooreceive respuesta. |
| `clientPerformance.sendRequest.value` |Tiempo de solicitud de envío |Tiempo empleado por solicitud toosend del explorador. |
| `clientPerformance.total.value` |Tiempo de carga de página del explorador |Tiempo que transcurre entre la solicitud del usuario hasta que se cargan el DOM, las hojas de estilo, los scripts y las imágenes. |
| `performanceCounter.available_bytes.value` |Memoria disponible |Memoria física inmediatamente disponible para un proceso o para su uso por parte del sistema. |
| `performanceCounter.io_data_bytes_per_sec.value` |Velocidad de E/S del proceso |Número total de bytes por segundo lectura y toofiles escrito, red y dispositivos. |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |velocidad de excepciones |Excepciones iniciadas por segundo. |
| `performanceCounter.percentage_processor_time.value` |CPU de procesos |Hola porcentaje de tiempo de todos los subprocesos del proceso utilizado las instrucciones de tooexecution de procesador de hello para el proceso de las aplicaciones de Hola. |
| `performanceCounter.percentage_processor_total.value` |Tiempo de procesador |porcentaje de Hola de tiempo que Hola el procesador invierte en subprocesos no inactivos. |
| `performanceCounter.process_private_bytes.value` |Bytes privados del proceso |Memoria asignada exclusivamente toohello supervisa los procesos de la aplicación. |
| `performanceCounter.request_execution_time.value` |Tiempo de ejecución de solicitud ASP.NET |Tiempo de ejecución de la solicitud más reciente de Hola. |
| `performanceCounter.requests_in_application_queue.value` |Solicitudes ASP.NET en la cola de ejecución |Longitud de cola de solicitudes de aplicación Hola. |
| `performanceCounter.requests_per_sec.value` |Velocidad de solicitudes ASP.NET |De todas las solicitudes de aplicación toohello por segundo de ASP.NET. |
| `remoteDependencyFailed.durationMetric.count` |Errores de dependencia |Recuento de errores llamadas realizadas por los recursos de tooexternal de aplicación de servidor de Hola. |
| `request.duration` |Tiempo de respuesta del servidor |Tiempo transcurrido entre la recepción de una solicitud HTTP y el acabado enviar respuesta Hola. |
| `request.rate` |Velocidad de solicitudes |Velocidad de todas las aplicaciones de toohello de solicitudes por segundo. |
| `requestFailed.count` |Error en las solicitudes |Recuento de solicitudes HTTP que dieron lugar a un código de respuesta >= 400 |
| `view.count` |Vistas de página |Recuento de solicitudes de usuario de cliente de una página web. Se filtra el tráfico sintético. |
| {el nombre de métrica personalizado} |{El nombre de métrica} |El valor de métrica notificados por [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) o en hello [parámetro mediciones de una llamada de seguimiento](app-insights-api-custom-events-metrics.md#properties). |

las métricas de Hola se envían por los módulos de telemetría diferentes:

| Grupo de métricas | Módulo de recopilador |
| --- | --- |
| basicExceptionBrowser,<br/>clientPerformance,<br/>view |[JavaScript de explorador](app-insights-javascript.md) |
| performanceCounter |[Rendimiento](app-insights-configuration-with-applicationinsights-config.md) |
| remoteDependencyFailed |[Dependencia](app-insights-configuration-with-applicationinsights-config.md) |
| request,<br/>requestFailed |[Solicitud de servidor](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a>Webhooks
También puede [automatizar la alerta de tooan respuesta](../monitoring-and-diagnostics/insights-webhooks-alerts.md). Azure llamará a una dirección web de su elección cuando se genere una alerta.

## <a name="see-also"></a>Otras referencias
* [Secuencia de comandos tooconfigure Application Insights](app-insights-powershell-script-create-resource.md)
* [Crear Application Insights y recursos de pruebas web a partir de plantillas](app-insights-powershell.md)
* [Automatizar Microsoft Azure Diagnostics tooApplication visión de acoplamiento](app-insights-powershell-azure-diagnostics.md)
* [Automatizar la alerta de tooan de respuesta](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
