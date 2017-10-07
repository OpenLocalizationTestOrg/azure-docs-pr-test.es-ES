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
# <a name="use-powershell-tooset-alerts-in-application-insights"></a><span data-ttu-id="94a68-103">Usar PowerShell tooset alertas en Application Insights</span><span class="sxs-lookup"><span data-stu-id="94a68-103">Use PowerShell tooset alerts in Application Insights</span></span>
<span data-ttu-id="94a68-104">Puede automatizar la configuración de hello [alertas](app-insights-alerts.md) en [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="94a68-104">You can automate hello configuration of [alerts](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="94a68-105">Además, puede [establecer la alerta de tooan de respuesta de webhooks tooautomate](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="94a68-105">In addition, you can [set webhooks tooautomate your response tooan alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="94a68-106">Si desea que los recursos de toocreate y alertas en Hola mismo tiempo, considere la posibilidad de [usando una plantilla de Azure Resource Manager](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="94a68-106">If you want toocreate resources and alerts at hello same time, consider [using an Azure Resource Manager template](app-insights-powershell.md).</span></span>
>
>

## <a name="one-time-setup"></a><span data-ttu-id="94a68-107">Instalación única</span><span class="sxs-lookup"><span data-stu-id="94a68-107">One-time setup</span></span>
<span data-ttu-id="94a68-108">Si no ha usado PowerShell con su suscripción de Azure antes:</span><span class="sxs-lookup"><span data-stu-id="94a68-108">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="94a68-109">Instale el módulo de Powershell de Azure de hello en la máquina de Hola donde desea que las secuencias de comandos de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="94a68-109">Install hello Azure Powershell module on hello machine where you want toorun hello scripts.</span></span>

* <span data-ttu-id="94a68-110">Instale el [Instalador de plataforma web de Microsoft (v5 o superior)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="94a68-110">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="94a68-111">Usar tooinstall Microsoft Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="94a68-111">Use it tooinstall Microsoft Azure Powershell</span></span>

## <a name="connect-tooazure"></a><span data-ttu-id="94a68-112">Conectar tooAzure</span><span class="sxs-lookup"><span data-stu-id="94a68-112">Connect tooAzure</span></span>
<span data-ttu-id="94a68-113">Inicie PowerShell de Azure y [conectar tooyour suscripción](/powershell/azure/overview):</span><span class="sxs-lookup"><span data-stu-id="94a68-113">Start Azure PowerShell and [connect tooyour subscription](/powershell/azure/overview):</span></span>

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a><span data-ttu-id="94a68-114">Obtención de alertas</span><span class="sxs-lookup"><span data-stu-id="94a68-114">Get alerts</span></span>
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a><span data-ttu-id="94a68-115">Agregar alerta</span><span class="sxs-lookup"><span data-stu-id="94a68-115">Add alert</span></span>
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



## <a name="example-1"></a><span data-ttu-id="94a68-116">Ejemplo 1</span><span class="sxs-lookup"><span data-stu-id="94a68-116">Example 1</span></span>
<span data-ttu-id="94a68-117">Enviarme un correo electrónico si las solicitudes de tooHTTP de respuesta del servidor de hello, promedio de más de 5 minutos, es menor que 1 segundo.</span><span class="sxs-lookup"><span data-stu-id="94a68-117">Email me if hello server's response tooHTTP requests, averaged over 5 minutes, is slower than 1 second.</span></span> <span data-ttu-id="94a68-118">Mi recurso de Application Insights se denomina IceCreamWebApp, y está en el grupo de recursos Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="94a68-118">My Application Insights resource is called IceCreamWebApp, and it is in resource group Fabrikam.</span></span> <span data-ttu-id="94a68-119">Soy propietario Hola de hello suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="94a68-119">I am hello owner of hello Azure subscription.</span></span>

<span data-ttu-id="94a68-120">Hola GUID es el Id. de suscripción de hello (no Hola clave de instrumentación de la aplicación hello).</span><span class="sxs-lookup"><span data-stu-id="94a68-120">hello GUID is hello subscription ID (not hello instrumentation key of hello application).</span></span>

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

## <a name="example-2"></a><span data-ttu-id="94a68-121">Ejemplo 2</span><span class="sxs-lookup"><span data-stu-id="94a68-121">Example 2</span></span>
<span data-ttu-id="94a68-122">Tengo una aplicación en el que utilizo [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport una métrica con el nombre "salesPerHour."</span><span class="sxs-lookup"><span data-stu-id="94a68-122">I have an application in which I use [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport a metric named "salesPerHour."</span></span> <span data-ttu-id="94a68-123">Enviar un correo electrónico toomy compañeros si "salesPerHour" cae por debajo de 100, promedio de más de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="94a68-123">Send an email toomy colleagues if "salesPerHour" drops below 100, averaged over 24 hours.</span></span>

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

<span data-ttu-id="94a68-124">Hola misma regla puede usarse para la métrica de hello informes utilizando hello [parámetro medida](app-insights-api-custom-events-metrics.md#properties) de seguimiento de otra llamada como TrackEvent o trackPageView.</span><span class="sxs-lookup"><span data-stu-id="94a68-124">hello same rule can be used for hello metric reported by using hello [measurement parameter](app-insights-api-custom-events-metrics.md#properties) of another tracking call such as TrackEvent or trackPageView.</span></span>

## <a name="metric-names"></a><span data-ttu-id="94a68-125">Nombres de métrica</span><span class="sxs-lookup"><span data-stu-id="94a68-125">Metric names</span></span>
| <span data-ttu-id="94a68-126">Nombre de métrica</span><span class="sxs-lookup"><span data-stu-id="94a68-126">Metric name</span></span> | <span data-ttu-id="94a68-127">Nombre de pantalla</span><span class="sxs-lookup"><span data-stu-id="94a68-127">Screen name</span></span> | <span data-ttu-id="94a68-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="94a68-128">Description</span></span> |
| --- | --- | --- |
| `basicExceptionBrowser.count` |<span data-ttu-id="94a68-129">Excepciones de explorador</span><span class="sxs-lookup"><span data-stu-id="94a68-129">Browser exceptions</span></span> |<span data-ttu-id="94a68-130">Recuento de excepciones no detectadas en el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="94a68-130">Count of uncaught exceptions thrown in hello browser.</span></span> |
| `basicExceptionServer.count` |<span data-ttu-id="94a68-131">Excepciones de servidor</span><span class="sxs-lookup"><span data-stu-id="94a68-131">Server exceptions</span></span> |<span data-ttu-id="94a68-132">Recuento de las excepciones no controladas producidas por la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="94a68-132">Count of unhandled exceptions thrown by hello app</span></span> |
| `clientPerformance.clientProcess.value` |<span data-ttu-id="94a68-133">Tiempo de procesamiento del cliente</span><span class="sxs-lookup"><span data-stu-id="94a68-133">Client processing time</span></span> |<span data-ttu-id="94a68-134">Tiempo transcurrido entre recibir el último byte de un documento Hola hasta que se cargue DOM Hola.</span><span class="sxs-lookup"><span data-stu-id="94a68-134">Time between receiving hello last byte of a document until hello DOM is loaded.</span></span> <span data-ttu-id="94a68-135">Todavía se pueden procesar solicitudes asincrónicas.</span><span class="sxs-lookup"><span data-stu-id="94a68-135">Async requests may still be processing.</span></span> |
| `clientPerformance.networkConnection.value` |<span data-ttu-id="94a68-136">Tiempo de conexión de red de carga de página</span><span class="sxs-lookup"><span data-stu-id="94a68-136">Page load network connect time</span></span> |<span data-ttu-id="94a68-137">Explorador de hello tiempo toma tooconnect toohello red.</span><span class="sxs-lookup"><span data-stu-id="94a68-137">Time hello browser takes tooconnect toohello network.</span></span> <span data-ttu-id="94a68-138">Puede ser 0 si se almacena en caché.</span><span class="sxs-lookup"><span data-stu-id="94a68-138">Can be 0 if cached.</span></span> |
| `clientPerformance.receiveRequest.value` |<span data-ttu-id="94a68-139">Tiempo de recepción de respuesta</span><span class="sxs-lookup"><span data-stu-id="94a68-139">Receiving response time</span></span> |<span data-ttu-id="94a68-140">Tiempo transcurrido entre el explorador envía solicitud toostarting tooreceive respuesta.</span><span class="sxs-lookup"><span data-stu-id="94a68-140">Time between browser sending request toostarting tooreceive response.</span></span> |
| `clientPerformance.sendRequest.value` |<span data-ttu-id="94a68-141">Tiempo de solicitud de envío</span><span class="sxs-lookup"><span data-stu-id="94a68-141">Send request time</span></span> |<span data-ttu-id="94a68-142">Tiempo empleado por solicitud toosend del explorador.</span><span class="sxs-lookup"><span data-stu-id="94a68-142">Time taken by browser toosend request.</span></span> |
| `clientPerformance.total.value` |<span data-ttu-id="94a68-143">Tiempo de carga de página del explorador</span><span class="sxs-lookup"><span data-stu-id="94a68-143">Browser page load time</span></span> |<span data-ttu-id="94a68-144">Tiempo que transcurre entre la solicitud del usuario hasta que se cargan el DOM, las hojas de estilo, los scripts y las imágenes.</span><span class="sxs-lookup"><span data-stu-id="94a68-144">Time from user request until DOM, stylesheets, scripts and images are loaded.</span></span> |
| `performanceCounter.available_bytes.value` |<span data-ttu-id="94a68-145">Memoria disponible</span><span class="sxs-lookup"><span data-stu-id="94a68-145">Available memory</span></span> |<span data-ttu-id="94a68-146">Memoria física inmediatamente disponible para un proceso o para su uso por parte del sistema.</span><span class="sxs-lookup"><span data-stu-id="94a68-146">Physical memory immediately available for a process or for system use.</span></span> |
| `performanceCounter.io_data_bytes_per_sec.value` |<span data-ttu-id="94a68-147">Velocidad de E/S del proceso</span><span class="sxs-lookup"><span data-stu-id="94a68-147">Process IO Rate</span></span> |<span data-ttu-id="94a68-148">Número total de bytes por segundo lectura y toofiles escrito, red y dispositivos.</span><span class="sxs-lookup"><span data-stu-id="94a68-148">Total bytes per second read and written toofiles, network and devices.</span></span> |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |<span data-ttu-id="94a68-149">velocidad de excepciones</span><span class="sxs-lookup"><span data-stu-id="94a68-149">exception rate</span></span> |<span data-ttu-id="94a68-150">Excepciones iniciadas por segundo.</span><span class="sxs-lookup"><span data-stu-id="94a68-150">Exceptions thrown per second.</span></span> |
| `performanceCounter.percentage_processor_time.value` |<span data-ttu-id="94a68-151">CPU de procesos</span><span class="sxs-lookup"><span data-stu-id="94a68-151">Process CPU</span></span> |<span data-ttu-id="94a68-152">Hola porcentaje de tiempo de todos los subprocesos del proceso utilizado las instrucciones de tooexecution de procesador de hello para el proceso de las aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="94a68-152">hello percentage of elapsed time of all process threads used by hello processor tooexecution instructions for hello applications process.</span></span> |
| `performanceCounter.percentage_processor_total.value` |<span data-ttu-id="94a68-153">Tiempo de procesador</span><span class="sxs-lookup"><span data-stu-id="94a68-153">Processor time</span></span> |<span data-ttu-id="94a68-154">porcentaje de Hola de tiempo que Hola el procesador invierte en subprocesos no inactivos.</span><span class="sxs-lookup"><span data-stu-id="94a68-154">hello percentage of time that hello processor spends in non-Idle threads.</span></span> |
| `performanceCounter.process_private_bytes.value` |<span data-ttu-id="94a68-155">Bytes privados del proceso</span><span class="sxs-lookup"><span data-stu-id="94a68-155">Process private bytes</span></span> |<span data-ttu-id="94a68-156">Memoria asignada exclusivamente toohello supervisa los procesos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="94a68-156">Memory exclusively assigned toohello monitored application's processes.</span></span> |
| `performanceCounter.request_execution_time.value` |<span data-ttu-id="94a68-157">Tiempo de ejecución de solicitud ASP.NET</span><span class="sxs-lookup"><span data-stu-id="94a68-157">ASP.NET request execution time</span></span> |<span data-ttu-id="94a68-158">Tiempo de ejecución de la solicitud más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="94a68-158">Execution time of hello most recent request.</span></span> |
| `performanceCounter.requests_in_application_queue.value` |<span data-ttu-id="94a68-159">Solicitudes ASP.NET en la cola de ejecución</span><span class="sxs-lookup"><span data-stu-id="94a68-159">ASP.NET requests in execution queue</span></span> |<span data-ttu-id="94a68-160">Longitud de cola de solicitudes de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="94a68-160">Length of hello application request queue.</span></span> |
| `performanceCounter.requests_per_sec.value` |<span data-ttu-id="94a68-161">Velocidad de solicitudes ASP.NET</span><span class="sxs-lookup"><span data-stu-id="94a68-161">ASP.NET request rate</span></span> |<span data-ttu-id="94a68-162">De todas las solicitudes de aplicación toohello por segundo de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="94a68-162">Rate of all requests toohello application per second from ASP.NET.</span></span> |
| `remoteDependencyFailed.durationMetric.count` |<span data-ttu-id="94a68-163">Errores de dependencia</span><span class="sxs-lookup"><span data-stu-id="94a68-163">Dependency failures</span></span> |<span data-ttu-id="94a68-164">Recuento de errores llamadas realizadas por los recursos de tooexternal de aplicación de servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="94a68-164">Count of failed calls made by hello server application tooexternal resources.</span></span> |
| `request.duration` |<span data-ttu-id="94a68-165">Tiempo de respuesta del servidor</span><span class="sxs-lookup"><span data-stu-id="94a68-165">Server response time</span></span> |<span data-ttu-id="94a68-166">Tiempo transcurrido entre la recepción de una solicitud HTTP y el acabado enviar respuesta Hola.</span><span class="sxs-lookup"><span data-stu-id="94a68-166">Time between receiving an HTTP request and finishing sending hello response.</span></span> |
| `request.rate` |<span data-ttu-id="94a68-167">Velocidad de solicitudes</span><span class="sxs-lookup"><span data-stu-id="94a68-167">Request rate</span></span> |<span data-ttu-id="94a68-168">Velocidad de todas las aplicaciones de toohello de solicitudes por segundo.</span><span class="sxs-lookup"><span data-stu-id="94a68-168">Rate of all requests toohello application per second.</span></span> |
| `requestFailed.count` |<span data-ttu-id="94a68-169">Error en las solicitudes</span><span class="sxs-lookup"><span data-stu-id="94a68-169">Failed requests</span></span> |<span data-ttu-id="94a68-170">Recuento de solicitudes HTTP que dieron lugar a un código de respuesta >= 400</span><span class="sxs-lookup"><span data-stu-id="94a68-170">Count of HTTP requests that resulted in a response code >= 400</span></span> |
| `view.count` |<span data-ttu-id="94a68-171">Vistas de página</span><span class="sxs-lookup"><span data-stu-id="94a68-171">Page views</span></span> |<span data-ttu-id="94a68-172">Recuento de solicitudes de usuario de cliente de una página web.</span><span class="sxs-lookup"><span data-stu-id="94a68-172">Count of client user requests for a web page.</span></span> <span data-ttu-id="94a68-173">Se filtra el tráfico sintético.</span><span class="sxs-lookup"><span data-stu-id="94a68-173">Synthetic traffic is filtered out.</span></span> |
| <span data-ttu-id="94a68-174">{el nombre de métrica personalizado}</span><span class="sxs-lookup"><span data-stu-id="94a68-174">{your custom metric name}</span></span> |<span data-ttu-id="94a68-175">{El nombre de métrica}</span><span class="sxs-lookup"><span data-stu-id="94a68-175">{Your metric name}</span></span> |<span data-ttu-id="94a68-176">El valor de métrica notificados por [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) o en hello [parámetro mediciones de una llamada de seguimiento](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="94a68-176">Your metric value reported by [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) or in hello [measurements parameter of a tracking call](app-insights-api-custom-events-metrics.md#properties).</span></span> |

<span data-ttu-id="94a68-177">las métricas de Hola se envían por los módulos de telemetría diferentes:</span><span class="sxs-lookup"><span data-stu-id="94a68-177">hello metrics are sent by different telemetry modules:</span></span>

| <span data-ttu-id="94a68-178">Grupo de métricas</span><span class="sxs-lookup"><span data-stu-id="94a68-178">Metric group</span></span> | <span data-ttu-id="94a68-179">Módulo de recopilador</span><span class="sxs-lookup"><span data-stu-id="94a68-179">Collector module</span></span> |
| --- | --- |
| <span data-ttu-id="94a68-180">basicExceptionBrowser,</span><span class="sxs-lookup"><span data-stu-id="94a68-180">basicExceptionBrowser,</span></span><br/><span data-ttu-id="94a68-181">clientPerformance,</span><span class="sxs-lookup"><span data-stu-id="94a68-181">clientPerformance,</span></span><br/><span data-ttu-id="94a68-182">view</span><span class="sxs-lookup"><span data-stu-id="94a68-182">view</span></span> |[<span data-ttu-id="94a68-183">JavaScript de explorador</span><span class="sxs-lookup"><span data-stu-id="94a68-183">Browser JavaScript</span></span>](app-insights-javascript.md) |
| <span data-ttu-id="94a68-184">performanceCounter</span><span class="sxs-lookup"><span data-stu-id="94a68-184">performanceCounter</span></span> |[<span data-ttu-id="94a68-185">Rendimiento</span><span class="sxs-lookup"><span data-stu-id="94a68-185">Performance</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="94a68-186">remoteDependencyFailed</span><span class="sxs-lookup"><span data-stu-id="94a68-186">remoteDependencyFailed</span></span> |[<span data-ttu-id="94a68-187">Dependencia</span><span class="sxs-lookup"><span data-stu-id="94a68-187">Dependency</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="94a68-188">request,</span><span class="sxs-lookup"><span data-stu-id="94a68-188">request,</span></span><br/><span data-ttu-id="94a68-189">requestFailed</span><span class="sxs-lookup"><span data-stu-id="94a68-189">requestFailed</span></span> |[<span data-ttu-id="94a68-190">Solicitud de servidor</span><span class="sxs-lookup"><span data-stu-id="94a68-190">Server request</span></span>](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a><span data-ttu-id="94a68-191">Webhooks</span><span class="sxs-lookup"><span data-stu-id="94a68-191">Webhooks</span></span>
<span data-ttu-id="94a68-192">También puede [automatizar la alerta de tooan respuesta](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="94a68-192">You can [automate your response tooan alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="94a68-193">Azure llamará a una dirección web de su elección cuando se genere una alerta.</span><span class="sxs-lookup"><span data-stu-id="94a68-193">Azure will call a web address of your choice when an alert is raised.</span></span>

## <a name="see-also"></a><span data-ttu-id="94a68-194">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="94a68-194">See also</span></span>
* [<span data-ttu-id="94a68-195">Secuencia de comandos tooconfigure Application Insights</span><span class="sxs-lookup"><span data-stu-id="94a68-195">Script tooconfigure Application Insights</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="94a68-196">Crear Application Insights y recursos de pruebas web a partir de plantillas</span><span class="sxs-lookup"><span data-stu-id="94a68-196">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="94a68-197">Automatizar Microsoft Azure Diagnostics tooApplication visión de acoplamiento</span><span class="sxs-lookup"><span data-stu-id="94a68-197">Automate coupling Microsoft Azure Diagnostics tooApplication Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="94a68-198">Automatizar la alerta de tooan de respuesta</span><span class="sxs-lookup"><span data-stu-id="94a68-198">Automate your response tooan alert</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
