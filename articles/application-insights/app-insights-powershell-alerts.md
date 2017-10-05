---
title: Uso de PowerShell para configurar alertas en Application Insights | Microsoft Docs
description: "Automatice la configuración de Application Insights para recibir correos electrónicos sobre los cambios en las métricas."
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
ms.openlocfilehash: 64675c51abf80daa3a55220f910aa8fdee1042ca
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-set-alerts-in-application-insights"></a><span data-ttu-id="a8e90-103">Uso de PowerShell para configurar alertas en Application Insights</span><span class="sxs-lookup"><span data-stu-id="a8e90-103">Use PowerShell to set alerts in Application Insights</span></span>
<span data-ttu-id="a8e90-104">Puede automatizar la configuración de [alertas](app-insights-alerts.md) en [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a8e90-104">You can automate the configuration of [alerts](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="a8e90-105">Además, puede [establecer webhooks para automatizar su respuesta ante una alerta](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="a8e90-105">In addition, you can [set webhooks to automate your response to an alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a8e90-106">Si quiere crear alertas y recursos al mismo tiempo, considere la posibilidad de [usar una plantilla de Azure Resource Manager](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a8e90-106">If you want to create resources and alerts at the same time, consider [using an Azure Resource Manager template](app-insights-powershell.md).</span></span>
>
>

## <a name="one-time-setup"></a><span data-ttu-id="a8e90-107">Instalación única</span><span class="sxs-lookup"><span data-stu-id="a8e90-107">One-time setup</span></span>
<span data-ttu-id="a8e90-108">Si no ha usado PowerShell con su suscripción de Azure antes:</span><span class="sxs-lookup"><span data-stu-id="a8e90-108">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="a8e90-109">Instale el módulo de Azure Powershell en el equipo donde desea ejecutar los scripts.</span><span class="sxs-lookup"><span data-stu-id="a8e90-109">Install the Azure Powershell module on the machine where you want to run the scripts.</span></span>

* <span data-ttu-id="a8e90-110">Instale el [Instalador de plataforma web de Microsoft (v5 o superior)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8e90-110">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="a8e90-111">Úselo para instalar Microsoft Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="a8e90-111">Use it to install Microsoft Azure Powershell</span></span>

## <a name="connect-to-azure"></a><span data-ttu-id="a8e90-112">Conexión a Azure</span><span class="sxs-lookup"><span data-stu-id="a8e90-112">Connect to Azure</span></span>
<span data-ttu-id="a8e90-113">Inicie Azure PowerShell y [conéctese a su suscripción](/powershell/azure/overview):</span><span class="sxs-lookup"><span data-stu-id="a8e90-113">Start Azure PowerShell and [connect to your subscription](/powershell/azure/overview):</span></span>

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a><span data-ttu-id="a8e90-114">Obtención de alertas</span><span class="sxs-lookup"><span data-stu-id="a8e90-114">Get alerts</span></span>
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a><span data-ttu-id="a8e90-115">Agregar alerta</span><span class="sxs-lookup"><span data-stu-id="a8e90-115">Add alert</span></span>
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



## <a name="example-1"></a><span data-ttu-id="a8e90-116">Ejemplo 1</span><span class="sxs-lookup"><span data-stu-id="a8e90-116">Example 1</span></span>
<span data-ttu-id="a8e90-117">Enviarme un correo electrónico si la respuesta del servidor a las solicitudes HTTP, calculada durante 5 minutos, tarda más de 1 segundo.</span><span class="sxs-lookup"><span data-stu-id="a8e90-117">Email me if the server's response to HTTP requests, averaged over 5 minutes, is slower than 1 second.</span></span> <span data-ttu-id="a8e90-118">Mi recurso de Application Insights se denomina IceCreamWebApp, y está en el grupo de recursos Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="a8e90-118">My Application Insights resource is called IceCreamWebApp, and it is in resource group Fabrikam.</span></span> <span data-ttu-id="a8e90-119">Soy el propietario de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e90-119">I am the owner of the Azure subscription.</span></span>

<span data-ttu-id="a8e90-120">El GUID es el identificador de la suscripción (no la clave de instrumentación de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="a8e90-120">The GUID is the subscription ID (not the instrumentation key of the application).</span></span>

    Add-AlertRule -Name "slow responses" `
     -Description "email me if the server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a><span data-ttu-id="a8e90-121">Ejemplo 2</span><span class="sxs-lookup"><span data-stu-id="a8e90-121">Example 2</span></span>
<span data-ttu-id="a8e90-122">Tengo una aplicación en la que uso [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) para informar de una métrica denominada "salesPerHour".</span><span class="sxs-lookup"><span data-stu-id="a8e90-122">I have an application in which I use [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) to report a metric named "salesPerHour."</span></span> <span data-ttu-id="a8e90-123">Enviar un correo electrónico a mis colegas si "salesPerHour" es menor que 100, calculado durante 24 horas.</span><span class="sxs-lookup"><span data-stu-id="a8e90-123">Send an email to my colleagues if "salesPerHour" drops below 100, averaged over 24 hours.</span></span>

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

<span data-ttu-id="a8e90-124">La misma regla puede usarse con la métrica notificada mediante el [parámetro de medida](app-insights-api-custom-events-metrics.md#properties) de otra llamada de seguimiento, como TrackEvent o trackPageView.</span><span class="sxs-lookup"><span data-stu-id="a8e90-124">The same rule can be used for the metric reported by using the [measurement parameter](app-insights-api-custom-events-metrics.md#properties) of another tracking call such as TrackEvent or trackPageView.</span></span>

## <a name="metric-names"></a><span data-ttu-id="a8e90-125">Nombres de métrica</span><span class="sxs-lookup"><span data-stu-id="a8e90-125">Metric names</span></span>
| <span data-ttu-id="a8e90-126">Nombre de métrica</span><span class="sxs-lookup"><span data-stu-id="a8e90-126">Metric name</span></span> | <span data-ttu-id="a8e90-127">Nombre de pantalla</span><span class="sxs-lookup"><span data-stu-id="a8e90-127">Screen name</span></span> | <span data-ttu-id="a8e90-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="a8e90-128">Description</span></span> |
| --- | --- | --- |
| `basicExceptionBrowser.count` |<span data-ttu-id="a8e90-129">Excepciones de explorador</span><span class="sxs-lookup"><span data-stu-id="a8e90-129">Browser exceptions</span></span> |<span data-ttu-id="a8e90-130">Recuento de excepciones no detectadas en el explorador.</span><span class="sxs-lookup"><span data-stu-id="a8e90-130">Count of uncaught exceptions thrown in the browser.</span></span> |
| `basicExceptionServer.count` |<span data-ttu-id="a8e90-131">Excepciones de servidor</span><span class="sxs-lookup"><span data-stu-id="a8e90-131">Server exceptions</span></span> |<span data-ttu-id="a8e90-132">Número de excepciones no controladas producidas por la aplicación</span><span class="sxs-lookup"><span data-stu-id="a8e90-132">Count of unhandled exceptions thrown by the app</span></span> |
| `clientPerformance.clientProcess.value` |<span data-ttu-id="a8e90-133">Tiempo de procesamiento del cliente</span><span class="sxs-lookup"><span data-stu-id="a8e90-133">Client processing time</span></span> |<span data-ttu-id="a8e90-134">Tiempo transcurrido entre la recepción del último byte de un documento hasta que se carga el DOM.</span><span class="sxs-lookup"><span data-stu-id="a8e90-134">Time between receiving the last byte of a document until the DOM is loaded.</span></span> <span data-ttu-id="a8e90-135">Todavía se pueden procesar solicitudes asincrónicas.</span><span class="sxs-lookup"><span data-stu-id="a8e90-135">Async requests may still be processing.</span></span> |
| `clientPerformance.networkConnection.value` |<span data-ttu-id="a8e90-136">Tiempo de conexión de red de carga de página</span><span class="sxs-lookup"><span data-stu-id="a8e90-136">Page load network connect time</span></span> |<span data-ttu-id="a8e90-137">Tiempo que tarda el explorador en conectarse a la red.</span><span class="sxs-lookup"><span data-stu-id="a8e90-137">Time the browser takes to connect to the network.</span></span> <span data-ttu-id="a8e90-138">Puede ser 0 si se almacena en caché.</span><span class="sxs-lookup"><span data-stu-id="a8e90-138">Can be 0 if cached.</span></span> |
| `clientPerformance.receiveRequest.value` |<span data-ttu-id="a8e90-139">Tiempo de recepción de respuesta</span><span class="sxs-lookup"><span data-stu-id="a8e90-139">Receiving response time</span></span> |<span data-ttu-id="a8e90-140">Tiempo que transcurre entre que el explorador envía la solicitud hasta que comienza a recibir la respuesta.</span><span class="sxs-lookup"><span data-stu-id="a8e90-140">Time between browser sending request to starting to receive response.</span></span> |
| `clientPerformance.sendRequest.value` |<span data-ttu-id="a8e90-141">Tiempo de solicitud de envío</span><span class="sxs-lookup"><span data-stu-id="a8e90-141">Send request time</span></span> |<span data-ttu-id="a8e90-142">Tiempo que tarda el explorador en enviar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="a8e90-142">Time taken by browser to send request.</span></span> |
| `clientPerformance.total.value` |<span data-ttu-id="a8e90-143">Tiempo de carga de página del explorador</span><span class="sxs-lookup"><span data-stu-id="a8e90-143">Browser page load time</span></span> |<span data-ttu-id="a8e90-144">Tiempo que transcurre entre la solicitud del usuario hasta que se cargan el DOM, las hojas de estilo, los scripts y las imágenes.</span><span class="sxs-lookup"><span data-stu-id="a8e90-144">Time from user request until DOM, stylesheets, scripts and images are loaded.</span></span> |
| `performanceCounter.available_bytes.value` |<span data-ttu-id="a8e90-145">Memoria disponible</span><span class="sxs-lookup"><span data-stu-id="a8e90-145">Available memory</span></span> |<span data-ttu-id="a8e90-146">Memoria física inmediatamente disponible para un proceso o para su uso por parte del sistema.</span><span class="sxs-lookup"><span data-stu-id="a8e90-146">Physical memory immediately available for a process or for system use.</span></span> |
| `performanceCounter.io_data_bytes_per_sec.value` |<span data-ttu-id="a8e90-147">Velocidad de E/S del proceso</span><span class="sxs-lookup"><span data-stu-id="a8e90-147">Process IO Rate</span></span> |<span data-ttu-id="a8e90-148">Número total de bytes por segundo leídos y escritos en los archivos, la red y los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a8e90-148">Total bytes per second read and written to files, network and devices.</span></span> |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |<span data-ttu-id="a8e90-149">velocidad de excepciones</span><span class="sxs-lookup"><span data-stu-id="a8e90-149">exception rate</span></span> |<span data-ttu-id="a8e90-150">Excepciones iniciadas por segundo.</span><span class="sxs-lookup"><span data-stu-id="a8e90-150">Exceptions thrown per second.</span></span> |
| `performanceCounter.percentage_processor_time.value` |<span data-ttu-id="a8e90-151">CPU de procesos</span><span class="sxs-lookup"><span data-stu-id="a8e90-151">Process CPU</span></span> |<span data-ttu-id="a8e90-152">El porcentaje de tiempo transcurrido de todos los subprocesos del proceso usados por el procesador en las instrucciones de ejecución del proceso de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a8e90-152">The percentage of elapsed time of all process threads used by the processor to execution instructions for the applications process.</span></span> |
| `performanceCounter.percentage_processor_total.value` |<span data-ttu-id="a8e90-153">Tiempo de procesador</span><span class="sxs-lookup"><span data-stu-id="a8e90-153">Processor time</span></span> |<span data-ttu-id="a8e90-154">El porcentaje de tiempo que invierte el procesador en subprocesos no inactivos.</span><span class="sxs-lookup"><span data-stu-id="a8e90-154">The percentage of time that the processor spends in non-Idle threads.</span></span> |
| `performanceCounter.process_private_bytes.value` |<span data-ttu-id="a8e90-155">Bytes privados del proceso</span><span class="sxs-lookup"><span data-stu-id="a8e90-155">Process private bytes</span></span> |<span data-ttu-id="a8e90-156">Memoria asignada exclusivamente a los procesos de la aplicación supervisada.</span><span class="sxs-lookup"><span data-stu-id="a8e90-156">Memory exclusively assigned to the monitored application's processes.</span></span> |
| `performanceCounter.request_execution_time.value` |<span data-ttu-id="a8e90-157">Tiempo de ejecución de solicitud ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a8e90-157">ASP.NET request execution time</span></span> |<span data-ttu-id="a8e90-158">Tiempo de ejecución de la solicitud más reciente.</span><span class="sxs-lookup"><span data-stu-id="a8e90-158">Execution time of the most recent request.</span></span> |
| `performanceCounter.requests_in_application_queue.value` |<span data-ttu-id="a8e90-159">Solicitudes ASP.NET en la cola de ejecución</span><span class="sxs-lookup"><span data-stu-id="a8e90-159">ASP.NET requests in execution queue</span></span> |<span data-ttu-id="a8e90-160">Longitud de la cola de solicitudes de aplicación.</span><span class="sxs-lookup"><span data-stu-id="a8e90-160">Length of the application request queue.</span></span> |
| `performanceCounter.requests_per_sec.value` |<span data-ttu-id="a8e90-161">Velocidad de solicitudes ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a8e90-161">ASP.NET request rate</span></span> |<span data-ttu-id="a8e90-162">Velocidad de todas las solicitudes a la aplicación por segundo desde ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a8e90-162">Rate of all requests to the application per second from ASP.NET.</span></span> |
| `remoteDependencyFailed.durationMetric.count` |<span data-ttu-id="a8e90-163">Errores de dependencia</span><span class="sxs-lookup"><span data-stu-id="a8e90-163">Dependency failures</span></span> |<span data-ttu-id="a8e90-164">Recuento de llamadas erróneas realizadas por la aplicación de servidor a recursos externos.</span><span class="sxs-lookup"><span data-stu-id="a8e90-164">Count of failed calls made by the server application to external resources.</span></span> |
| `request.duration` |<span data-ttu-id="a8e90-165">Tiempo de respuesta del servidor</span><span class="sxs-lookup"><span data-stu-id="a8e90-165">Server response time</span></span> |<span data-ttu-id="a8e90-166">Tiempo entre que se recibe una solicitud HTTP y se termina de enviar la respuesta.</span><span class="sxs-lookup"><span data-stu-id="a8e90-166">Time between receiving an HTTP request and finishing sending the response.</span></span> |
| `request.rate` |<span data-ttu-id="a8e90-167">Velocidad de solicitudes</span><span class="sxs-lookup"><span data-stu-id="a8e90-167">Request rate</span></span> |<span data-ttu-id="a8e90-168">Velocidad de todas las solicitudes a la aplicación por segundo.</span><span class="sxs-lookup"><span data-stu-id="a8e90-168">Rate of all requests to the application per second.</span></span> |
| `requestFailed.count` |<span data-ttu-id="a8e90-169">Error en las solicitudes</span><span class="sxs-lookup"><span data-stu-id="a8e90-169">Failed requests</span></span> |<span data-ttu-id="a8e90-170">Recuento de solicitudes HTTP que dieron lugar a un código de respuesta >= 400</span><span class="sxs-lookup"><span data-stu-id="a8e90-170">Count of HTTP requests that resulted in a response code >= 400</span></span> |
| `view.count` |<span data-ttu-id="a8e90-171">Vistas de página</span><span class="sxs-lookup"><span data-stu-id="a8e90-171">Page views</span></span> |<span data-ttu-id="a8e90-172">Recuento de solicitudes de usuario de cliente de una página web.</span><span class="sxs-lookup"><span data-stu-id="a8e90-172">Count of client user requests for a web page.</span></span> <span data-ttu-id="a8e90-173">Se filtra el tráfico sintético.</span><span class="sxs-lookup"><span data-stu-id="a8e90-173">Synthetic traffic is filtered out.</span></span> |
| <span data-ttu-id="a8e90-174">{el nombre de métrica personalizado}</span><span class="sxs-lookup"><span data-stu-id="a8e90-174">{your custom metric name}</span></span> |<span data-ttu-id="a8e90-175">{El nombre de métrica}</span><span class="sxs-lookup"><span data-stu-id="a8e90-175">{Your metric name}</span></span> |<span data-ttu-id="a8e90-176">El valor de métrica que notifica [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) o en el [parámetro de medidas de una llamada de seguimiento](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="a8e90-176">Your metric value reported by [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) or in the [measurements parameter of a tracking call](app-insights-api-custom-events-metrics.md#properties).</span></span> |

<span data-ttu-id="a8e90-177">Las métricas se envían por módulos de telemetría diferentes:</span><span class="sxs-lookup"><span data-stu-id="a8e90-177">The metrics are sent by different telemetry modules:</span></span>

| <span data-ttu-id="a8e90-178">Grupo de métricas</span><span class="sxs-lookup"><span data-stu-id="a8e90-178">Metric group</span></span> | <span data-ttu-id="a8e90-179">Módulo de recopilador</span><span class="sxs-lookup"><span data-stu-id="a8e90-179">Collector module</span></span> |
| --- | --- |
| <span data-ttu-id="a8e90-180">basicExceptionBrowser,</span><span class="sxs-lookup"><span data-stu-id="a8e90-180">basicExceptionBrowser,</span></span><br/><span data-ttu-id="a8e90-181">clientPerformance,</span><span class="sxs-lookup"><span data-stu-id="a8e90-181">clientPerformance,</span></span><br/><span data-ttu-id="a8e90-182">view</span><span class="sxs-lookup"><span data-stu-id="a8e90-182">view</span></span> |[<span data-ttu-id="a8e90-183">JavaScript de explorador</span><span class="sxs-lookup"><span data-stu-id="a8e90-183">Browser JavaScript</span></span>](app-insights-javascript.md) |
| <span data-ttu-id="a8e90-184">performanceCounter</span><span class="sxs-lookup"><span data-stu-id="a8e90-184">performanceCounter</span></span> |[<span data-ttu-id="a8e90-185">Rendimiento</span><span class="sxs-lookup"><span data-stu-id="a8e90-185">Performance</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="a8e90-186">remoteDependencyFailed</span><span class="sxs-lookup"><span data-stu-id="a8e90-186">remoteDependencyFailed</span></span> |[<span data-ttu-id="a8e90-187">Dependencia</span><span class="sxs-lookup"><span data-stu-id="a8e90-187">Dependency</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="a8e90-188">request,</span><span class="sxs-lookup"><span data-stu-id="a8e90-188">request,</span></span><br/><span data-ttu-id="a8e90-189">requestFailed</span><span class="sxs-lookup"><span data-stu-id="a8e90-189">requestFailed</span></span> |[<span data-ttu-id="a8e90-190">Solicitud de servidor</span><span class="sxs-lookup"><span data-stu-id="a8e90-190">Server request</span></span>](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a><span data-ttu-id="a8e90-191">Webhooks</span><span class="sxs-lookup"><span data-stu-id="a8e90-191">Webhooks</span></span>
<span data-ttu-id="a8e90-192">También puede [automatizar la respuesta ante una alerta](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="a8e90-192">You can [automate your response to an alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="a8e90-193">Azure llamará a una dirección web de su elección cuando se genere una alerta.</span><span class="sxs-lookup"><span data-stu-id="a8e90-193">Azure will call a web address of your choice when an alert is raised.</span></span>

## <a name="see-also"></a><span data-ttu-id="a8e90-194">Consulte también</span><span class="sxs-lookup"><span data-stu-id="a8e90-194">See also</span></span>
* [<span data-ttu-id="a8e90-195">Script para configurar Application Insights</span><span class="sxs-lookup"><span data-stu-id="a8e90-195">Script to configure Application Insights</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="a8e90-196">Crear Application Insights y recursos de pruebas web a partir de plantillas</span><span class="sxs-lookup"><span data-stu-id="a8e90-196">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="a8e90-197">Uso de PowerShell para enviar Diagnósticos de Azure a Application Insights</span><span class="sxs-lookup"><span data-stu-id="a8e90-197">Automate coupling Microsoft Azure Diagnostics to Application Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="a8e90-198">Automatización de la respuesta ante una alerta</span><span class="sxs-lookup"><span data-stu-id="a8e90-198">Automate your response to an alert</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
