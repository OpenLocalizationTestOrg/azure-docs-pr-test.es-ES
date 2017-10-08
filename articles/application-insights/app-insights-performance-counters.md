---
title: contadores de aaaPerformance en Application Insights | Documentos de Microsoft
description: Supervise los contadores de rendimiento de .NET, tanto del sistema como personalizados, en Application Insights.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b816f4c-a77a-4674-ae36-802ee3a2f56d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/11/2016
ms.author: bwren
ms.openlocfilehash: 0a51c225f1d1124c9e7fe89f34e747cb26a3589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="system-performance-counters-in-application-insights"></a><span data-ttu-id="0d3a2-103">Contadores de rendimiento de sistema en Application Insights</span><span class="sxs-lookup"><span data-stu-id="0d3a2-103">System performance counters in Application Insights</span></span>
<span data-ttu-id="0d3a2-104">Windows proporciona una amplia variedad de [contadores de rendimiento](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters), como la ocupación de la CPU, memoria, disco y uso de la red.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-104">Windows provides a wide variety of [performance counters](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) such as CPU occupancy, memory, disk, and network usage.</span></span> <span data-ttu-id="0d3a2-105">También puede definir sus propios contadores.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-105">You can also define your own.</span></span> <span data-ttu-id="0d3a2-106">[Application Insights](app-insights-overview.md) puede mostrar estos contadores de rendimiento si la aplicación que ejecuta en IIS en un toowhich de host o máquina virtual local tengan acceso administrativo.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-106">[Application Insights](app-insights-overview.md) can show these performance counters if your application is running under IIS on an on-premises host or virtual machine toowhich you have administrative access.</span></span> <span data-ttu-id="0d3a2-107">gráficos de Hello indican Hola recursos disponibles tooyour vivo de las aplicaciones y pueden ayudar a tooidentify carga desequilibrada entre instancias de servidor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-107">hello charts indicate hello resources available tooyour live application, and can help tooidentify unbalanced load between server instances.</span></span>

<span data-ttu-id="0d3a2-108">Contadores de rendimiento aparecen en la hoja de servidores de hello, que incluye una tabla que segmenta por instancia de servidor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-108">Performance counters appear in hello Servers blade, which includes a table that segments by server instance.</span></span>

![Contadores de rendimiento notificados en Application Insights](./media/app-insights-performance-counters/counters-by-server-instance.png)

<span data-ttu-id="0d3a2-110">(Los contadores de rendimiento no están disponibles para Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-110">(Performance counters aren't available for Azure Web Apps.</span></span> <span data-ttu-id="0d3a2-111">Pero puede [enviar información de diagnóstico de Azure tooApplication](app-insights-azure-diagnostics.md).)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-111">But you can [send Azure Diagnostics tooApplication Insights](app-insights-azure-diagnostics.md).)</span></span>

## <a name="view-counters"></a><span data-ttu-id="0d3a2-112">Visualización de contadores</span><span class="sxs-lookup"><span data-stu-id="0d3a2-112">View counters</span></span>
<span data-ttu-id="0d3a2-113">hoja de servidores de Hello muestra un conjunto predeterminado de contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-113">hello Servers blade shows a default set of performance counters.</span></span> 

<span data-ttu-id="0d3a2-114">toosee otros contadores, edite los gráficos de hello en la hoja de servidores de Hola o abra una nueva [Explorer métricas](app-insights-metrics-explorer.md) hoja y agregar nuevos gráficos.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-114">toosee other counters, either edit hello charts on hello Servers blade, or open a new [Metrics Explorer](app-insights-metrics-explorer.md) blade and add new charts.</span></span> 

<span data-ttu-id="0d3a2-115">se enumeran los contadores disponibles de Hello métricas cuando se edita un gráfico.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-115">hello available counters are listed as metrics when you edit a chart.</span></span>

![Contadores de rendimiento notificados en Application Insights](./media/app-insights-performance-counters/choose-performance-counters.png)

<span data-ttu-id="0d3a2-117">toosee todos los gráficos más útiles en un solo lugar, cree un [panel](app-insights-dashboards.md) y anclarlos tooit.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-117">toosee all your most useful charts in one place, create a [dashboard](app-insights-dashboards.md) and pin them tooit.</span></span>

## <a name="add-counters"></a><span data-ttu-id="0d3a2-118">Adición de contadores</span><span class="sxs-lookup"><span data-stu-id="0d3a2-118">Add counters</span></span>
<span data-ttu-id="0d3a2-119">Si desea que el contador de rendimiento de hello no se muestre en lista de Hola de métricas, eso es porque Hola Application Insights SDK no está recopilando en el servidor web.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-119">If hello performance counter you want isn't shown in hello list of metrics, that's because hello Application Insights SDK isn't collecting it in your web server.</span></span> <span data-ttu-id="0d3a2-120">Se puede configurar toodo así.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-120">You can configure it toodo so.</span></span>

1. <span data-ttu-id="0d3a2-121">Averiguar qué contadores están disponibles en el servidor mediante el uso de este comando de PowerShell en el servidor de hello:</span><span class="sxs-lookup"><span data-stu-id="0d3a2-121">Find out what counters are available in your server by using this PowerShell command at hello server:</span></span>
   
    `Get-Counter -ListSet *`
   
    <span data-ttu-id="0d3a2-122">(Consulte [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx)).</span><span class="sxs-lookup"><span data-stu-id="0d3a2-122">(See [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span></span>
2. <span data-ttu-id="0d3a2-123">Abra ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-123">Open ApplicationInsights.config.</span></span>
   
   * <span data-ttu-id="0d3a2-124">Si agrega Application Insights tooyour aplicación durante el desarrollo, editar ApplicationInsights.config en el proyecto y, a continuación, volver a implementarlo tooyour servidores.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-124">If you added Application Insights tooyour app during development, edit ApplicationInsights.config in your project, and then re-deploy it tooyour servers.</span></span>
   * <span data-ttu-id="0d3a2-125">Si utiliza el Monitor de estado tooinstrument una aplicación web en tiempo de ejecución, buscar ApplicationInsights.config en el directorio raíz de saludo de la aplicación hello en IIS.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-125">If you used Status Monitor tooinstrument a web app at runtime, find ApplicationInsights.config in hello root directory of hello app in IIS.</span></span> <span data-ttu-id="0d3a2-126">Actualícelo allí en cada instancia del servidor.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-126">Update it there in each server instance.</span></span>
3. <span data-ttu-id="0d3a2-127">Editar directiva de recopilador de rendimiento de hello:</span><span class="sxs-lookup"><span data-stu-id="0d3a2-127">Edit hello performance collector directive:</span></span>
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

<span data-ttu-id="0d3a2-128">Puede capturar tanto los contadores estándar como los que ha implementado usted mismo.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-128">You can capture both standard counters and those you have implemented yourself.</span></span> <span data-ttu-id="0d3a2-129">`\Objects\Processes` es un ejemplo de contador estándar, disponible en todos los sistemas Windows.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-129">`\Objects\Processes` is an example of a standard counter, available on all Windows systems.</span></span> <span data-ttu-id="0d3a2-130">`\Sales(photo)\# Items Sold` es un ejemplo de contador personalizado que podría implementarse en un servicio web.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-130">`\Sales(photo)\# Items Sold` is an example of a custom counter that might be implemented in a web service.</span></span> 

<span data-ttu-id="0d3a2-131">formato de Hello es `\Category(instance)\Counter"`, o en categorías que no tienen instancias, simplemente `\Category\Counter`.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-131">hello format is `\Category(instance)\Counter"`, or for categories that don't have instances, just `\Category\Counter`.</span></span>

<span data-ttu-id="0d3a2-132">`ReportAs`es necesario para los nombres de contadores que no coinciden `[a-zA-Z()/-_ \.]+` : es decir, que contienen caracteres que no están en hello siguientes conjuntos de: letras de ida y vuelta entre corchetes, barra diagonal, guión, subrayado, espacio, punto.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-132">`ReportAs` is required for counter names that do not match `[a-zA-Z()/-_ \.]+` - that is, they contain characters that are not in hello following sets: letters, round brackets, forward slash, hyphen, underscore, space, dot.</span></span>

<span data-ttu-id="0d3a2-133">Si especifica una instancia, se recopilará como una dimensión "CounterInstanceName" de hello indica métrica.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-133">If you specify an instance, it will be collected as a dimension "CounterInstanceName" of hello reported metric.</span></span>

### <a name="collecting-performance-counters-in-code"></a><span data-ttu-id="0d3a2-134">Recopilación de contadores de rendimiento en el código</span><span class="sxs-lookup"><span data-stu-id="0d3a2-134">Collecting performance counters in code</span></span>
<span data-ttu-id="0d3a2-135">los contadores de rendimiento del sistema toocollect y enviarlos tooApplication visión, puede adaptar el siguiente fragmento de hello:</span><span class="sxs-lookup"><span data-stu-id="0d3a2-135">toocollect system performance counters and send them tooApplication Insights, you can adapt hello snippet below:</span></span>


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

<span data-ttu-id="0d3a2-136">O bien puede hacerlo Hola lo mismo con métricas personalizadas que creó:</span><span class="sxs-lookup"><span data-stu-id="0d3a2-136">Or you can do hello same thing with custom metrics you created:</span></span>

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a><span data-ttu-id="0d3a2-137">Contadores de rendimiento en Analytics</span><span class="sxs-lookup"><span data-stu-id="0d3a2-137">Performance counters in Analytics</span></span>
<span data-ttu-id="0d3a2-138">Puede buscar y mostrar informes de contador de rendimiento en [Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="0d3a2-138">You can search and display performance counter reports in [Analytics](app-insights-analytics.md).</span></span>

<span data-ttu-id="0d3a2-139">Hola **performanceCounters** esquema expone hello `category`, `counter` nombre, y `instance` nombre de cada contador de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-139">hello **performanceCounters** schema exposes hello `category`, `counter` name, and `instance` name of each performance counter.</span></span>  <span data-ttu-id="0d3a2-140">En la telemetría de Hola para cada aplicación, verá solo los contadores de Hola para esa aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-140">In hello telemetry for each application, you’ll see only hello counters for that application.</span></span> <span data-ttu-id="0d3a2-141">Por ejemplo, toosee qué contadores están disponibles:</span><span class="sxs-lookup"><span data-stu-id="0d3a2-141">For example, toosee what counters are available:</span></span> 

![Contadores de rendimiento en Application Insights Analytics](./media/app-insights-performance-counters/analytics-performance-counters.png)

<span data-ttu-id="0d3a2-143">(Aquí 'Instance' hace referencia la instancia de contador de rendimiento de toohello, no Hola instancia de máquina del servidor o rol.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-143">('Instance' here refers toohello performance counter instance,  not hello role or server machine instance.</span></span> <span data-ttu-id="0d3a2-144">nombre de instancia de contador de rendimiento de Hello segmenta normalmente contadores como el tiempo de procesador por nombre de hello del proceso de Hola o la aplicación.)</span><span class="sxs-lookup"><span data-stu-id="0d3a2-144">hello performance counter instance name typically segments counters such as processor time by hello name of hello process or application.)</span></span>

<span data-ttu-id="0d3a2-145">tooget un gráfico de memoria disponible a través de hello período de tiempo reciente:</span><span class="sxs-lookup"><span data-stu-id="0d3a2-145">tooget a chart of available memory over hello recent period:</span></span> 

![Gráfico de tiempo de la memoria in Application Insights Analytics](./media/app-insights-performance-counters/analytics-available-memory.png)

<span data-ttu-id="0d3a2-147">Al igual que otros telemetría **performanceCounters** también tiene una columna `cloud_RoleInstance` que indica la identidad de Hola de instancia del servidor de host de hello en el que se ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-147">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates hello identity of hello host server instance on which your app is running.</span></span> <span data-ttu-id="0d3a2-148">Por ejemplo, toocompare Hola rendimiento de la aplicación en equipos diferentes de hello:</span><span class="sxs-lookup"><span data-stu-id="0d3a2-148">For example, toocompare hello performance of your app on hello different machines:</span></span> 

![Rendimiento segmentado por instancia de rol en Application Insights Analytics](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a><span data-ttu-id="0d3a2-150">Recuentos de ASP.NET y Application Insights</span><span class="sxs-lookup"><span data-stu-id="0d3a2-150">ASP.NET and Application Insights counts</span></span>
<span data-ttu-id="0d3a2-151">*¿Cuál es la diferencia de hello entre la tasa de excepción de Hola y métricas de excepciones?*</span><span class="sxs-lookup"><span data-stu-id="0d3a2-151">*What's hello difference between hello Exception rate and Exceptions metrics?*</span></span>

* <span data-ttu-id="0d3a2-152">*tasa de excepciones* es un contador de rendimiento del sistema.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-152">*Exception rate* is a system performance counter.</span></span> <span data-ttu-id="0d3a2-153">Hola CLR cuenta todos los Hola controlan y las excepciones no controladas que se producen y total de Hola se divide en un intervalo de muestreo por longitud de Hola de intervalo de saludo.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-153">hello CLR counts all hello handled and unhandled exceptions that are thrown, and divides hello total in a sampling interval by hello length of hello interval.</span></span> <span data-ttu-id="0d3a2-154">Hola Application Insights SDK recopila este resultado y lo envía toohello portal.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-154">hello Application Insights SDK collects this result and sends it toohello portal.</span></span>
* <span data-ttu-id="0d3a2-155">*Excepciones* es un recuento de hello informes TrackException recibidos por el portal de hello en el intervalo de muestreo de saludo del gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-155">*Exceptions* is a count of hello TrackException reports received by hello portal in hello sampling interval of hello chart.</span></span> <span data-ttu-id="0d3a2-156">Incluye solo Hola excepciones controladas en donde haya terminado de escribir TrackException llama en el código y no incluye todos los [las excepciones no controladas](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="0d3a2-156">It includes only hello handled exceptions where you have written TrackException calls in your code, and doesn't include all [unhandled exceptions](app-insights-asp-net-exceptions.md).</span></span> 

## <a name="alerts"></a><span data-ttu-id="0d3a2-157">Alertas</span><span class="sxs-lookup"><span data-stu-id="0d3a2-157">Alerts</span></span>
<span data-ttu-id="0d3a2-158">Al igual que otras métricas, puede [establecer una alerta](app-insights-alerts.md) toowarn si un contador de rendimiento queda fuera de un límite especifique.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-158">Like other metrics, you can [set an alert](app-insights-alerts.md) toowarn you if a performance counter goes outside a limit you specify.</span></span> <span data-ttu-id="0d3a2-159">Abra la hoja de alertas de Hola y haga clic en Agregar alerta.</span><span class="sxs-lookup"><span data-stu-id="0d3a2-159">Open hello Alerts blade and click Add Alert.</span></span>

## <span data-ttu-id="0d3a2-160"><a name="next"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0d3a2-160"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="0d3a2-161">Seguimiento de dependencias</span><span class="sxs-lookup"><span data-stu-id="0d3a2-161">Dependency tracking</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="0d3a2-162">Seguimiento de excepciones</span><span class="sxs-lookup"><span data-stu-id="0d3a2-162">Exception tracking</span></span>](app-insights-asp-net-exceptions.md)

