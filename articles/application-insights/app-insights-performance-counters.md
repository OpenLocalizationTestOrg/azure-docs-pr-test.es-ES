---
title: Contadores de rendimiento en Application Insights | Microsoft Docs
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
ms.openlocfilehash: 038d6e051be8112b9264e7efa6485965d11e32c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="system-performance-counters-in-application-insights"></a><span data-ttu-id="b5afe-103">Contadores de rendimiento de sistema en Application Insights</span><span class="sxs-lookup"><span data-stu-id="b5afe-103">System performance counters in Application Insights</span></span>
<span data-ttu-id="b5afe-104">Windows proporciona una amplia variedad de [contadores de rendimiento](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters), como la ocupación de la CPU, memoria, disco y uso de la red.</span><span class="sxs-lookup"><span data-stu-id="b5afe-104">Windows provides a wide variety of [performance counters](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) such as CPU occupancy, memory, disk, and network usage.</span></span> <span data-ttu-id="b5afe-105">También puede definir sus propios contadores.</span><span class="sxs-lookup"><span data-stu-id="b5afe-105">You can also define your own.</span></span> <span data-ttu-id="b5afe-106">[Application Insights](app-insights-overview.md) puede mostrar estos contadores de rendimiento si la aplicación se ejecuta en IIS en un host local o en una máquina virtual para la que tenga acceso administrativo.</span><span class="sxs-lookup"><span data-stu-id="b5afe-106">[Application Insights](app-insights-overview.md) can show these performance counters if your application is running under IIS on an on-premises host or virtual machine to which you have administrative access.</span></span> <span data-ttu-id="b5afe-107">Los gráficos indican los recursos disponibles para su aplicación activa y pueden ayudar a identificar la carga no equilibrada entre las instancias de servidor.</span><span class="sxs-lookup"><span data-stu-id="b5afe-107">The charts indicate the resources available to your live application, and can help to identify unbalanced load between server instances.</span></span>

<span data-ttu-id="b5afe-108">Los contadores de rendimiento aparecen en la hoja Servidores, que incluye una tabla que segmenta por instancia de servidor.</span><span class="sxs-lookup"><span data-stu-id="b5afe-108">Performance counters appear in the Servers blade, which includes a table that segments by server instance.</span></span>

![Contadores de rendimiento notificados en Application Insights](./media/app-insights-performance-counters/counters-by-server-instance.png)

<span data-ttu-id="b5afe-110">(Los contadores de rendimiento no están disponibles para Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="b5afe-110">(Performance counters aren't available for Azure Web Apps.</span></span> <span data-ttu-id="b5afe-111">Pero puede [enviar Diagnósticos de Azure a Application Insights](app-insights-azure-diagnostics.md)).</span><span class="sxs-lookup"><span data-stu-id="b5afe-111">But you can [send Azure Diagnostics to Application Insights](app-insights-azure-diagnostics.md).)</span></span>

## <a name="view-counters"></a><span data-ttu-id="b5afe-112">Visualización de contadores</span><span class="sxs-lookup"><span data-stu-id="b5afe-112">View counters</span></span>
<span data-ttu-id="b5afe-113">La hoja Servidores muestra un conjunto predeterminado de contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="b5afe-113">The Servers blade shows a default set of performance counters.</span></span> 

<span data-ttu-id="b5afe-114">Para ver otros contadores, edite los gráficos de la hoja Servidores o abra una nueva hoja [Explorador de métricas](app-insights-metrics-explorer.md) y agregue nuevos gráficos.</span><span class="sxs-lookup"><span data-stu-id="b5afe-114">To see other counters, either edit the charts on the Servers blade, or open a new [Metrics Explorer](app-insights-metrics-explorer.md) blade and add new charts.</span></span> 

<span data-ttu-id="b5afe-115">Los contadores disponibles aparecen como las métricas cuando se edita un gráfico.</span><span class="sxs-lookup"><span data-stu-id="b5afe-115">The available counters are listed as metrics when you edit a chart.</span></span>

![Contadores de rendimiento notificados en Application Insights](./media/app-insights-performance-counters/choose-performance-counters.png)

<span data-ttu-id="b5afe-117">Para ver todos los gráficos más útiles en un solo lugar, cree un [panel](app-insights-dashboards.md) y ánclelos a él.</span><span class="sxs-lookup"><span data-stu-id="b5afe-117">To see all your most useful charts in one place, create a [dashboard](app-insights-dashboards.md) and pin them to it.</span></span>

## <a name="add-counters"></a><span data-ttu-id="b5afe-118">Adición de contadores</span><span class="sxs-lookup"><span data-stu-id="b5afe-118">Add counters</span></span>
<span data-ttu-id="b5afe-119">Si el contador de rendimiento que desea no aparece en la lista de métricas, eso es debido a que el SDK de Application Insights no lo está recopilando en el servidor web.</span><span class="sxs-lookup"><span data-stu-id="b5afe-119">If the performance counter you want isn't shown in the list of metrics, that's because the Application Insights SDK isn't collecting it in your web server.</span></span> <span data-ttu-id="b5afe-120">Puede configurarlo para que lo haga.</span><span class="sxs-lookup"><span data-stu-id="b5afe-120">You can configure it to do so.</span></span>

1. <span data-ttu-id="b5afe-121">Averigüe qué contadores están disponibles en el servidor mediante este comando de PowerShell en el servidor:</span><span class="sxs-lookup"><span data-stu-id="b5afe-121">Find out what counters are available in your server by using this PowerShell command at the server:</span></span>
   
    `Get-Counter -ListSet *`
   
    <span data-ttu-id="b5afe-122">(Consulte [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx)).</span><span class="sxs-lookup"><span data-stu-id="b5afe-122">(See [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span></span>
2. <span data-ttu-id="b5afe-123">Abra ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="b5afe-123">Open ApplicationInsights.config.</span></span>
   
   * <span data-ttu-id="b5afe-124">Si agrega Application Insights a la aplicación durante el desarrollo, edite ApplicationInsights.config en el proyecto y vuelva a implementarlo en los servidores.</span><span class="sxs-lookup"><span data-stu-id="b5afe-124">If you added Application Insights to your app during development, edit ApplicationInsights.config in your project, and then re-deploy it to your servers.</span></span>
   * <span data-ttu-id="b5afe-125">Si utiliza Monitor de estado para instrumentar una aplicación web en tiempo de ejecución, busque ApplicationInsights.config en el directorio raíz de la aplicación en IIS.</span><span class="sxs-lookup"><span data-stu-id="b5afe-125">If you used Status Monitor to instrument a web app at runtime, find ApplicationInsights.config in the root directory of the app in IIS.</span></span> <span data-ttu-id="b5afe-126">Actualícelo allí en cada instancia del servidor.</span><span class="sxs-lookup"><span data-stu-id="b5afe-126">Update it there in each server instance.</span></span>
3. <span data-ttu-id="b5afe-127">Edite la directiva del recopilador de rendimiento:</span><span class="sxs-lookup"><span data-stu-id="b5afe-127">Edit the performance collector directive:</span></span>
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

<span data-ttu-id="b5afe-128">Puede capturar tanto los contadores estándar como los que ha implementado usted mismo.</span><span class="sxs-lookup"><span data-stu-id="b5afe-128">You can capture both standard counters and those you have implemented yourself.</span></span> <span data-ttu-id="b5afe-129">`\Objects\Processes` es un ejemplo de contador estándar, disponible en todos los sistemas Windows.</span><span class="sxs-lookup"><span data-stu-id="b5afe-129">`\Objects\Processes` is an example of a standard counter, available on all Windows systems.</span></span> <span data-ttu-id="b5afe-130">`\Sales(photo)\# Items Sold` es un ejemplo de contador personalizado que podría implementarse en un servicio web.</span><span class="sxs-lookup"><span data-stu-id="b5afe-130">`\Sales(photo)\# Items Sold` is an example of a custom counter that might be implemented in a web service.</span></span> 

<span data-ttu-id="b5afe-131">El formato es `\Category(instance)\Counter"` o, para las categorías que no tienen instancias, simplemente `\Category\Counter`.</span><span class="sxs-lookup"><span data-stu-id="b5afe-131">The format is `\Category(instance)\Counter"`, or for categories that don't have instances, just `\Category\Counter`.</span></span>

<span data-ttu-id="b5afe-132">`ReportAs` es necesario para los nombres de contadores que no coinciden `[a-zA-Z()/-_ \.]+`: es decir, que contienen caracteres que no están en los siguientes conjuntos: letras, paréntesis, barra diagonal, guión, subrayado, espacio, punto.</span><span class="sxs-lookup"><span data-stu-id="b5afe-132">`ReportAs` is required for counter names that do not match `[a-zA-Z()/-_ \.]+` - that is, they contain characters that are not in the following sets: letters, round brackets, forward slash, hyphen, underscore, space, dot.</span></span>

<span data-ttu-id="b5afe-133">Si especifica una instancia, se recopilará como una dimensión "CounterInstanceName" de la métrica notificada.</span><span class="sxs-lookup"><span data-stu-id="b5afe-133">If you specify an instance, it will be collected as a dimension "CounterInstanceName" of the reported metric.</span></span>

### <a name="collecting-performance-counters-in-code"></a><span data-ttu-id="b5afe-134">Recopilación de contadores de rendimiento en el código</span><span class="sxs-lookup"><span data-stu-id="b5afe-134">Collecting performance counters in code</span></span>
<span data-ttu-id="b5afe-135">Para recopilar contadores de rendimiento del sistema y enviarlos a Application Insights, puede adaptar el siguiente fragmento:</span><span class="sxs-lookup"><span data-stu-id="b5afe-135">To collect system performance counters and send them to Application Insights, you can adapt the snippet below:</span></span>


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

<span data-ttu-id="b5afe-136">También puede hacer lo mismo con las métricas personalizadas que haya creado:</span><span class="sxs-lookup"><span data-stu-id="b5afe-136">Or you can do the same thing with custom metrics you created:</span></span>

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a><span data-ttu-id="b5afe-137">Contadores de rendimiento en Analytics</span><span class="sxs-lookup"><span data-stu-id="b5afe-137">Performance counters in Analytics</span></span>
<span data-ttu-id="b5afe-138">Puede buscar y mostrar informes de contador de rendimiento en [Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="b5afe-138">You can search and display performance counter reports in [Analytics](app-insights-analytics.md).</span></span>

<span data-ttu-id="b5afe-139">El esquema **performanceCounters** expone `category`, el nombre de `counter` y el nombre de `instance` de cada contador de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="b5afe-139">The **performanceCounters** schema exposes the `category`, `counter` name, and `instance` name of each performance counter.</span></span>  <span data-ttu-id="b5afe-140">En la telemetría de cada aplicación, solo se ven los contadores de dicha aplicación.</span><span class="sxs-lookup"><span data-stu-id="b5afe-140">In the telemetry for each application, you’ll see only the counters for that application.</span></span> <span data-ttu-id="b5afe-141">Por ejemplo, para ver qué contadores están disponibles:</span><span class="sxs-lookup"><span data-stu-id="b5afe-141">For example, to see what counters are available:</span></span> 

![Contadores de rendimiento en Application Insights Analytics](./media/app-insights-performance-counters/analytics-performance-counters.png)

<span data-ttu-id="b5afe-143">(Aquí 'Instance' hace referencia a la instancia de contador de rendimiento, no al rol o a la instancia de máquina de servidor.</span><span class="sxs-lookup"><span data-stu-id="b5afe-143">('Instance' here refers to the performance counter instance,  not the role or server machine instance.</span></span> <span data-ttu-id="b5afe-144">El nombre de la instancia del contador de rendimiento normalmente segmenta contadores, como el tiempo de procesador por el nombre del proceso o la aplicación).</span><span class="sxs-lookup"><span data-stu-id="b5afe-144">The performance counter instance name typically segments counters such as processor time by the name of the process or application.)</span></span>

<span data-ttu-id="b5afe-145">Para obtener un gráfico de la memoria disponible en un período reciente:</span><span class="sxs-lookup"><span data-stu-id="b5afe-145">To get a chart of available memory over the recent period:</span></span> 

![Gráfico de tiempo de la memoria in Application Insights Analytics](./media/app-insights-performance-counters/analytics-available-memory.png)

<span data-ttu-id="b5afe-147">Al igual que otros datos de telemetría, **performanceCounters** también tiene una columna `cloud_RoleInstance` que indica la identidad de la instancia del servidor host en el que se ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b5afe-147">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates the identity of the host server instance on which your app is running.</span></span> <span data-ttu-id="b5afe-148">Por ejemplo, para comparar el rendimiento de una aplicación en distintas máquinas:</span><span class="sxs-lookup"><span data-stu-id="b5afe-148">For example, to compare the performance of your app on the different machines:</span></span> 

![Rendimiento segmentado por instancia de rol en Application Insights Analytics](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a><span data-ttu-id="b5afe-150">Recuentos de ASP.NET y Application Insights</span><span class="sxs-lookup"><span data-stu-id="b5afe-150">ASP.NET and Application Insights counts</span></span>
<span data-ttu-id="b5afe-151">*¿En qué se diferencian la tasa de excepciones y las métricas de excepciones?*</span><span class="sxs-lookup"><span data-stu-id="b5afe-151">*What's the difference between the Exception rate and Exceptions metrics?*</span></span>

* <span data-ttu-id="b5afe-152">*tasa de excepciones* es un contador de rendimiento del sistema.</span><span class="sxs-lookup"><span data-stu-id="b5afe-152">*Exception rate* is a system performance counter.</span></span> <span data-ttu-id="b5afe-153">El CLR cuenta todas las excepciones controladas y no controladas que se producen, y divide el total de un intervalo de muestreo entre la duración del intervalo.</span><span class="sxs-lookup"><span data-stu-id="b5afe-153">The CLR counts all the handled and unhandled exceptions that are thrown, and divides the total in a sampling interval by the length of the interval.</span></span> <span data-ttu-id="b5afe-154">El SDK de Application Insights recopila este resultado y lo envía al portal.</span><span class="sxs-lookup"><span data-stu-id="b5afe-154">The Application Insights SDK collects this result and sends it to the portal.</span></span>
* <span data-ttu-id="b5afe-155">*Excepciones* es un recuento de los informes de TrackException recibidos a través del portal en el intervalo de muestreo del gráfico.</span><span class="sxs-lookup"><span data-stu-id="b5afe-155">*Exceptions* is a count of the TrackException reports received by the portal in the sampling interval of the chart.</span></span> <span data-ttu-id="b5afe-156">Solo incluye las excepciones controladas para las que ha escrito llamadas a TrackException en el código y no incluye todas las [excepciones no controladas](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="b5afe-156">It includes only the handled exceptions where you have written TrackException calls in your code, and doesn't include all [unhandled exceptions](app-insights-asp-net-exceptions.md).</span></span> 

## <a name="alerts"></a><span data-ttu-id="b5afe-157">Alertas</span><span class="sxs-lookup"><span data-stu-id="b5afe-157">Alerts</span></span>
<span data-ttu-id="b5afe-158">Al igual que otras métricas, puede [establecer una alerta](app-insights-alerts.md) para advertirle si un contador de rendimiento queda fuera de un límite especificado.</span><span class="sxs-lookup"><span data-stu-id="b5afe-158">Like other metrics, you can [set an alert](app-insights-alerts.md) to warn you if a performance counter goes outside a limit you specify.</span></span> <span data-ttu-id="b5afe-159">Abra la hoja de alertas y haga clic en Agregar alerta.</span><span class="sxs-lookup"><span data-stu-id="b5afe-159">Open the Alerts blade and click Add Alert.</span></span>

## <span data-ttu-id="b5afe-160"><a name="next"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b5afe-160"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="b5afe-161">Seguimiento de dependencias</span><span class="sxs-lookup"><span data-stu-id="b5afe-161">Dependency tracking</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="b5afe-162">Seguimiento de excepciones</span><span class="sxs-lookup"><span data-stu-id="b5afe-162">Exception tracking</span></span>](app-insights-asp-net-exceptions.md)

