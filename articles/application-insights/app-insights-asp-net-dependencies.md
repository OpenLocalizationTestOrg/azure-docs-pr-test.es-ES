---
title: aaaDependency seguimiento en Azure Application Insights | Documentos de Microsoft
description: "Analice el uso, la disponibilidad y el rendimiento de su aplicación web de Microsoft Azure o local con Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d15c4ca8-4c1a-47ab-a03d-c322b4bb2a9e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: e72f5465462ae8e64363cbbaa62911aff636c504
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a><span data-ttu-id="14736-103">Configurar Application Insights: seguimiento de dependencias</span><span class="sxs-lookup"><span data-stu-id="14736-103">Set up Application Insights: Dependency tracking</span></span>
<span data-ttu-id="14736-104">Una *dependencia* es un componente externo al que llama la aplicación.</span><span class="sxs-lookup"><span data-stu-id="14736-104">A *dependency* is an external component that is called by your app.</span></span> <span data-ttu-id="14736-105">Suele ser un servicio al que se llama mediante HTTP, una base de datos o un sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="14736-105">It's typically a service called using HTTP, or a database, or a file system.</span></span> <span data-ttu-id="14736-106">[Application Insights](app-insights-overview.md) mide cuánto tiempo espera su aplicación a las dependencias y la frecuencia con que se produce un error en una llamada de dependencia.</span><span class="sxs-lookup"><span data-stu-id="14736-106">[Application Insights](app-insights-overview.md) measures how long your application waits for dependencies and how often a dependency call fails.</span></span> <span data-ttu-id="14736-107">Puede investigar llamadas específicas y relacionarlos toorequests y excepciones.</span><span class="sxs-lookup"><span data-stu-id="14736-107">You can investigate specific calls, and relate them toorequests and exceptions.</span></span>

![gráficos de ejemplo](./media/app-insights-asp-net-dependencies/10-intro.png)

<span data-ttu-id="14736-109">monitor de dependencia del cuadro de Hello actualmente emite llamadas toothese tipos de dependencias:</span><span class="sxs-lookup"><span data-stu-id="14736-109">hello out-of-the-box dependency monitor currently reports calls toothese  types of dependencies:</span></span>

* <span data-ttu-id="14736-110">Server</span><span class="sxs-lookup"><span data-stu-id="14736-110">Server</span></span>
  * <span data-ttu-id="14736-111">Bases de datos SQL</span><span class="sxs-lookup"><span data-stu-id="14736-111">SQL databases</span></span>
  * <span data-ttu-id="14736-112">Servicios WFC y web de ASP.NET que usan enlaces basados en HTTP</span><span class="sxs-lookup"><span data-stu-id="14736-112">ASP.NET web and WCF services that use HTTP-based bindings</span></span>
  * <span data-ttu-id="14736-113">Llamadas HTTP locales o remotas</span><span class="sxs-lookup"><span data-stu-id="14736-113">Local or remote HTTP calls</span></span>
  * <span data-ttu-id="14736-114">Azure Cosmos DB, Table Storage, Blob Storage y Queue Storage</span><span class="sxs-lookup"><span data-stu-id="14736-114">Azure Cosmos DB, table, blob storage, and queue</span></span>
* <span data-ttu-id="14736-115">Páginas web</span><span class="sxs-lookup"><span data-stu-id="14736-115">Web pages</span></span>
  * <span data-ttu-id="14736-116">Llamadas AJAX</span><span class="sxs-lookup"><span data-stu-id="14736-116">AJAX calls</span></span>

<span data-ttu-id="14736-117">La supervisión funciona mediante la [instrumentación del código de byte](https://msdn.microsoft.com/library/z9z62c29.aspx) alrededor de los métodos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="14736-117">Monitoring works by using [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) around selected methods.</span></span> <span data-ttu-id="14736-118">La sobrecarga de rendimiento es mínima.</span><span class="sxs-lookup"><span data-stu-id="14736-118">Performance overhead is minimal.</span></span>

<span data-ttu-id="14736-119">También puede escribir su propio SDK llama toomonitor otras dependencias, tanto en el código de cliente y servidor hello, con hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="14736-119">You can also write your own SDK calls toomonitor other dependencies, both in hello client and server code, using hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

## <a name="set-up-dependency-monitoring"></a><span data-ttu-id="14736-120">Configuración de la supervisión de dependencias</span><span class="sxs-lookup"><span data-stu-id="14736-120">Set up dependency monitoring</span></span>
<span data-ttu-id="14736-121">Hola recopila automáticamente información de dependencia parcial [Application Insights SDK](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="14736-121">Partial dependency information is collected automatically by hello [Application Insights SDK](app-insights-asp-net.md).</span></span> <span data-ttu-id="14736-122">tooget completa de los datos, instalar agente adecuado de hello para el servidor de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="14736-122">tooget complete data, install hello appropriate agent for hello host server.</span></span>

| <span data-ttu-id="14736-123">Plataforma</span><span class="sxs-lookup"><span data-stu-id="14736-123">Platform</span></span> | <span data-ttu-id="14736-124">Instalación</span><span class="sxs-lookup"><span data-stu-id="14736-124">Install</span></span> |
| --- | --- |
| <span data-ttu-id="14736-125">Servidor IIS</span><span class="sxs-lookup"><span data-stu-id="14736-125">IIS Server</span></span> |<span data-ttu-id="14736-126">Cualquier [instalar el Monitor de estado en el servidor](app-insights-monitor-performance-live-website-now.md) o [actualizar el marco de aplicación de too.NET 4.6 o posterior](http://go.microsoft.com/fwlink/?LinkId=528259) e instalar hello [Application Insights SDK](app-insights-asp-net.md) en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="14736-126">Either [install Status Monitor on your server](app-insights-monitor-performance-live-website-now.md) or [Upgrade your application too.NET framework 4.6 or later](http://go.microsoft.com/fwlink/?LinkId=528259) and install hello [Application Insights SDK](app-insights-asp-net.md)  in your app.</span></span> |
| <span data-ttu-id="14736-127">Aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="14736-127">Azure Web App</span></span> |<span data-ttu-id="14736-128">En el panel de control de aplicación web, [hoja de Application Insights Hola abierto en el panel de control de aplicación web](app-insights-azure-web-apps.md) y elija instalar si se le solicita.</span><span class="sxs-lookup"><span data-stu-id="14736-128">In your web app control panel, [open hello Application Insights blade in your web app control panel](app-insights-azure-web-apps.md) and choose Install if prompted.</span></span> |
| <span data-ttu-id="14736-129">Servicio en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="14736-129">Azure Cloud Service</span></span> |<span data-ttu-id="14736-130">[Uso de tarea de inicio](app-insights-cloudservices.md) o [Instalación de .NET Framework 4.6 o versiones posteriores](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="14736-130">[Use startup task](app-insights-cloudservices.md) or [Install .NET framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span></span> |

## <a name="where-toofind-dependency-data"></a><span data-ttu-id="14736-131">Donde los datos de dependencia toofind</span><span class="sxs-lookup"><span data-stu-id="14736-131">Where toofind dependency data</span></span>
* <span data-ttu-id="14736-132">[Asignación de aplicación](#application-map) visualiza las dependencias entre la aplicación y los componentes colindantes.</span><span class="sxs-lookup"><span data-stu-id="14736-132">[Application Map](#application-map) visualizes dependencies between your app and neighbouring components.</span></span>
* <span data-ttu-id="14736-133">Las hojas [Rendimiento, Exploradores y Errores](#performance-and-blades) muestran datos de dependencia del servidor.</span><span class="sxs-lookup"><span data-stu-id="14736-133">[Performance, browser, and failure blades](#performance-and-blades) show server dependency data.</span></span>
* <span data-ttu-id="14736-134">La hoja [Exploradores](#ajax-calls) muestra las llamadas AJAX de los exploradores de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="14736-134">[Browsers blade](#ajax-calls) shows AJAX calls from your users' browsers.</span></span>
* <span data-ttu-id="14736-135">[Haga clic en a través de solicitudes lentas o con errores](#diagnose-slow-requests) toocheck llama a su dependencia.</span><span class="sxs-lookup"><span data-stu-id="14736-135">[Click through from slow or failed requests](#diagnose-slow-requests) toocheck their dependency calls.</span></span>
* <span data-ttu-id="14736-136">[Análisis de](#analytics) pueden ser datos de dependencia de tooquery usado.</span><span class="sxs-lookup"><span data-stu-id="14736-136">[Analytics](#analytics) can be used tooquery dependency data.</span></span>

## <a name="application-map"></a><span data-ttu-id="14736-137">Mapa de aplicación</span><span class="sxs-lookup"><span data-stu-id="14736-137">Application Map</span></span>
<span data-ttu-id="14736-138">Asignación de la aplicación actúa como una ayuda visual toodiscovering de dependencias entre componentes de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="14736-138">Application Map acts as a visual aid toodiscovering dependencies between hello components of your application.</span></span> <span data-ttu-id="14736-139">Se genera automáticamente de telemetría de Hola desde la aplicación.</span><span class="sxs-lookup"><span data-stu-id="14736-139">It is automatically generated from hello telemetry from your app.</span></span> <span data-ttu-id="14736-140">Este ejemplo muestra llamadas de AJAX de las secuencias de comandos del explorador de Hola y las llamadas REST del servidor de hello servicios externos tootwo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="14736-140">This example shows AJAX calls from hello browser scripts and REST calls from hello server app tootwo external services.</span></span>

![Mapa de aplicación](./media/app-insights-asp-net-dependencies/08.png)

* <span data-ttu-id="14736-142">**Navegar desde los cuadros de hello** toorelevant dependencia y otros gráficos.</span><span class="sxs-lookup"><span data-stu-id="14736-142">**Navigate from hello boxes** toorelevant dependency and other charts.</span></span>
* <span data-ttu-id="14736-143">**Mapa de hello PIN** toohello [panel](app-insights-dashboards.md), donde será totalmente funcional.</span><span class="sxs-lookup"><span data-stu-id="14736-143">**Pin hello map** toohello [dashboard](app-insights-dashboards.md), where it will be fully functional.</span></span>

<span data-ttu-id="14736-144">[Más información](app-insights-app-map.md).</span><span class="sxs-lookup"><span data-stu-id="14736-144">[Learn more](app-insights-app-map.md).</span></span>

## <a name="performance-and-failure-blades"></a><span data-ttu-id="14736-145">Hojas Rendimiento y Errores</span><span class="sxs-lookup"><span data-stu-id="14736-145">Performance and failure blades</span></span>
<span data-ttu-id="14736-146">hoja de rendimiento de Hello muestra la duración de Hola de dependencia las llamadas realizadas por la aplicación de servidor hello.</span><span class="sxs-lookup"><span data-stu-id="14736-146">hello performance blade shows hello duration of dependency calls made by hello server app.</span></span> <span data-ttu-id="14736-147">Hay un gráfico de resumen y una tabla segmentada por llamadas.</span><span class="sxs-lookup"><span data-stu-id="14736-147">There's a summary chart and a table segmented by call.</span></span>

![Gráficos de dependencia de la hoja Rendimiento](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

<span data-ttu-id="14736-149">Desplazarse por los gráficos de resumen de Hola u Hola tabla elementos toosearch sin procesar las instancias de estas llamadas.</span><span class="sxs-lookup"><span data-stu-id="14736-149">Click through hello summary charts or hello table items toosearch raw occurrences of these calls.</span></span>

![Instancias de llamadas de dependencia](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

<span data-ttu-id="14736-151">**Número de errores** se muestran en hello **errores** hoja.</span><span class="sxs-lookup"><span data-stu-id="14736-151">**Failure counts** are shown on hello **Failures** blade.</span></span> <span data-ttu-id="14736-152">Un error es cualquier código de retorno que no está en hello intervalo 200-399, o desconocido.</span><span class="sxs-lookup"><span data-stu-id="14736-152">A failure is any return code that is not in hello range 200-399, or unknown.</span></span>

> [!NOTE]
> <span data-ttu-id="14736-153">**¿El porcentaje de errores es 100?**</span><span class="sxs-lookup"><span data-stu-id="14736-153">**100% failures?**</span></span> <span data-ttu-id="14736-154">Probablemente, esto signifique que está obteniendo datos de dependencias parciales.</span><span class="sxs-lookup"><span data-stu-id="14736-154">- This probably indicates that you are only getting partial dependency data.</span></span> <span data-ttu-id="14736-155">Necesita demasiado[configurar tooyour adecuado orientada a servicios de dependencia](#set-up-dependency-monitoring).</span><span class="sxs-lookup"><span data-stu-id="14736-155">You need too[set up dependency monitoring appropriate tooyour platform](#set-up-dependency-monitoring).</span></span>
>
>

## <a name="ajax-calls"></a><span data-ttu-id="14736-156">Llamadas AJAX</span><span class="sxs-lookup"><span data-stu-id="14736-156">AJAX Calls</span></span>
<span data-ttu-id="14736-157">hoja de exploradores de Hello muestra la duración de Hola y llama a tasa de error de AJAX de [JavaScript en las páginas web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="14736-157">hello Browsers blade shows hello duration and failure rate of AJAX calls from [JavaScript in your web pages](app-insights-javascript.md).</span></span> <span data-ttu-id="14736-158">Se muestran como dependencias.</span><span class="sxs-lookup"><span data-stu-id="14736-158">They are shown as Dependencies.</span></span>

## <span data-ttu-id="14736-159"><a name="diagnosis"></a> Diagnóstico de solicitudes lentas</span><span class="sxs-lookup"><span data-stu-id="14736-159"><a name="diagnosis"></a> Diagnose slow requests</span></span>
<span data-ttu-id="14736-160">Cada evento de solicitud está asociado a las llamadas de dependencia de hello, excepciones y otros eventos que se realiza el seguimiento mientras se procesa la aplicación Hola solicitud.</span><span class="sxs-lookup"><span data-stu-id="14736-160">Each request event is associated with hello dependency calls, exceptions and other events that are tracked while your app is processing hello request.</span></span> <span data-ttu-id="14736-161">Por lo que si realización algunas solicitudes incorrecto, puede averiguar si es debido a las respuestas de tooslow de una dependencia.</span><span class="sxs-lookup"><span data-stu-id="14736-161">So if some requests are performing badly, you can find out whether it's due tooslow responses from a dependency.</span></span>

<span data-ttu-id="14736-162">Veamos un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="14736-162">Let's walk through an example of that.</span></span>

### <a name="tracing-from-requests-toodependencies"></a><span data-ttu-id="14736-163">Seguimiento de solicitudes toodependencies</span><span class="sxs-lookup"><span data-stu-id="14736-163">Tracing from requests toodependencies</span></span>
<span data-ttu-id="14736-164">Abra la hoja de rendimiento de Hola y examine cuadrícula Hola de solicitudes:</span><span class="sxs-lookup"><span data-stu-id="14736-164">Open hello Performance blade, and look at hello grid of requests:</span></span>

![Lista de solicitudes con promedios y recuentos](./media/app-insights-asp-net-dependencies/02-reqs.png)

<span data-ttu-id="14736-166">parte superior de Hello uno está tardando mucho.</span><span class="sxs-lookup"><span data-stu-id="14736-166">hello top one is taking very long.</span></span> <span data-ttu-id="14736-167">Veamos si podemos descubrimos que transcurre el tiempo de Hola.</span><span class="sxs-lookup"><span data-stu-id="14736-167">Let's see if we can find out where hello time is spent.</span></span>

<span data-ttu-id="14736-168">Haga clic en ese eventos de solicitud individual de toosee de fila:</span><span class="sxs-lookup"><span data-stu-id="14736-168">Click that row toosee individual request events:</span></span>

![Lista de casos de solicitudes](./media/app-insights-asp-net-dependencies/03-instances.png)

<span data-ttu-id="14736-170">Haga clic en cualquier tooinspect de instancia de ejecución prolongada más y desplácese hacia abajo toohello dependencia remoto llamadas relacionadas toothis solicitud:</span><span class="sxs-lookup"><span data-stu-id="14736-170">Click any long-running instance tooinspect it further, and scroll down toohello remote dependency calls related toothis request:</span></span>

![Buscar llamadas tooRemote dependencias, identifique duración inusual](./media/app-insights-asp-net-dependencies/04-dependencies.png)

<span data-ttu-id="14736-172">Parece que la mayor parte del servicio de hora de hello que un servicio local de llamada tooa dedicada a esta solicitud.</span><span class="sxs-lookup"><span data-stu-id="14736-172">It looks like most of hello time servicing this request was spent in a call tooa local service.</span></span>

<span data-ttu-id="14736-173">Seleccione esa fila tooget obtener más información:</span><span class="sxs-lookup"><span data-stu-id="14736-173">Select that row tooget more information:</span></span>

![Haga clic en a través de ese punto de entrada y dependencia remoto tooidentify Hola](./media/app-insights-asp-net-dependencies/05-detail.png)

<span data-ttu-id="14736-175">Parece que esto es donde el problema Hola.</span><span class="sxs-lookup"><span data-stu-id="14736-175">Looks like this is where hello problem is.</span></span> <span data-ttu-id="14736-176">Se ha detectado el problema de hello, por lo que ahora le necesario toofind out ¿por qué llamada está tardando tanto.</span><span class="sxs-lookup"><span data-stu-id="14736-176">We've pinpointed hello problem, so now we just need toofind out why that call is taking so long.</span></span>

### <a name="request-timeline"></a><span data-ttu-id="14736-177">Escala de tiempo de solicitudes</span><span class="sxs-lookup"><span data-stu-id="14736-177">Request timeline</span></span>
<span data-ttu-id="14736-178">En otro caso, no hay ninguna llamada de dependencia especialmente larga.</span><span class="sxs-lookup"><span data-stu-id="14736-178">In a different case, there is no dependency call that is particularly long.</span></span> <span data-ttu-id="14736-179">Pero, al cambiar la vista de escala de tiempo toohello, podemos ver dónde se produjo el retraso de hello en el procesamiento interno:</span><span class="sxs-lookup"><span data-stu-id="14736-179">But by switching toohello timeline view, we can see where hello delay occurred in our internal processing:</span></span>

![Buscar llamadas tooRemote dependencias, identifique duración inusual](./media/app-insights-asp-net-dependencies/04-1.png)

<span data-ttu-id="14736-181">Parece que hay toobe un gran espacio después de hello primera dependencia llamada, por lo que debemos mirar en nuestro toosee de código por qué es decir.</span><span class="sxs-lookup"><span data-stu-id="14736-181">There seems toobe a big gap after hello first dependency call, so we should look at our code toosee why that is.</span></span>

### <a name="profile-your-live-site"></a><span data-ttu-id="14736-182">Generación de un perfil del sitio activo</span><span class="sxs-lookup"><span data-stu-id="14736-182">Profile your live site</span></span>

<span data-ttu-id="14736-183">¿No sabe dónde va el tiempo de presentación? Hola [el generador de perfiles de Application Insights](app-insights-profiler.md) seguimientos HTTP llama tooyour sitio en vivo y muestra las funciones en el código han tardado hello más largo.</span><span class="sxs-lookup"><span data-stu-id="14736-183">No idea where hello time goes? hello [Application Insights profiler](app-insights-profiler.md) traces HTTP calls tooyour live site and shows you which functions in your code took hello longest time.</span></span>

## <a name="failed-requests"></a><span data-ttu-id="14736-184">Error en las solicitudes</span><span class="sxs-lookup"><span data-stu-id="14736-184">Failed requests</span></span>
<span data-ttu-id="14736-185">Las solicitudes con error también podrían estar asociadas con errores llamadas toodependencies.</span><span class="sxs-lookup"><span data-stu-id="14736-185">Failed requests might also be associated with failed calls toodependencies.</span></span> <span data-ttu-id="14736-186">Una vez más, podemos desplazarse tootrack problema Hola.</span><span class="sxs-lookup"><span data-stu-id="14736-186">Again, we can click through tootrack down hello problem.</span></span>

![Haga clic en el gráfico de hello las solicitudes con error](./media/app-insights-asp-net-dependencies/06-fail.png)

<span data-ttu-id="14736-188">Desplazarse por los tooan aparición de una solicitud errónea y examine los eventos asociados.</span><span class="sxs-lookup"><span data-stu-id="14736-188">Click through tooan occurrence of a failed request, and look at its associated events.</span></span>

![Haga clic en un tipo de solicitud, haga clic en hello instancia tooget tooa vista diferente de Hola misma instancia, haga clic en detalles de la excepción de tooget.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a><span data-ttu-id="14736-190">Análisis</span><span class="sxs-lookup"><span data-stu-id="14736-190">Analytics</span></span>
<span data-ttu-id="14736-191">Puede realizar un seguimiento de las dependencias en hello [lenguaje de consulta de análisis de registros](https://docs.loganalytics.io/).</span><span class="sxs-lookup"><span data-stu-id="14736-191">You can track dependencies in hello [Log Analytics query language](https://docs.loganalytics.io/).</span></span> <span data-ttu-id="14736-192">Estos son algunos ejemplos.</span><span class="sxs-lookup"><span data-stu-id="14736-192">Here are some examples.</span></span>

* <span data-ttu-id="14736-193">Búsqueda de llamadas de dependencia con errores:</span><span class="sxs-lookup"><span data-stu-id="14736-193">Find any failed dependency calls:</span></span>

```

    dependencies | where success != "True" | take 10
```

* <span data-ttu-id="14736-194">Búsqueda de llamadas AJAX:</span><span class="sxs-lookup"><span data-stu-id="14736-194">Find AJAX calls:</span></span>

```

    dependencies | where client_Type == "Browser" | take 10
```

* <span data-ttu-id="14736-195">Búsqueda de llamadas de dependencia asociadas a solicitudes:</span><span class="sxs-lookup"><span data-stu-id="14736-195">Find dependency calls associated with requests:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* <span data-ttu-id="14736-196">Búsqueda de llamadas AJAX asociadas a vistas de página:</span><span class="sxs-lookup"><span data-stu-id="14736-196">Find AJAX calls associated with page views:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a><span data-ttu-id="14736-197">Seguimiento de dependencias personalizadas</span><span class="sxs-lookup"><span data-stu-id="14736-197">Custom dependency tracking</span></span>
<span data-ttu-id="14736-198">módulo de seguimiento de dependencias estándar Hola detecta automáticamente las dependencias externas, como las bases de datos y las API de REST.</span><span class="sxs-lookup"><span data-stu-id="14736-198">hello standard dependency-tracking module automatically discovers external dependencies such as databases and REST APIs.</span></span> <span data-ttu-id="14736-199">Pero puede que desee trata de algunos componentes adicionales toobe Hola misma manera.</span><span class="sxs-lookup"><span data-stu-id="14736-199">But you might want some additional components toobe treated in hello same way.</span></span>

<span data-ttu-id="14736-200">Puede escribir código que envía información de dependencia, utilizando Hola mismo [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) utilizado por los módulos estándares Hola.</span><span class="sxs-lookup"><span data-stu-id="14736-200">You can write code that sends dependency information, using hello same [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) that is used by hello standard modules.</span></span>

<span data-ttu-id="14736-201">Por ejemplo, si compila el código con un ensamblado que no es suyo a usted mismo, podría tiempo todos los tooit de llamadas de hello, toofind out qué contribución dificulta la respuesta de tooyour el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="14736-201">For example, if you build your code with an assembly that you didn't write yourself, you could time all hello calls tooit, toofind out what contribution it makes tooyour response times.</span></span> <span data-ttu-id="14736-202">toohave este datos que se muestran en los gráficos de dependencia de Hola de Application Insights, enviarla a través de `TrackDependency`.</span><span class="sxs-lookup"><span data-stu-id="14736-202">toohave this data displayed in hello dependency charts in Application Insights, send it using `TrackDependency`.</span></span>

```C#

            var startTime = DateTime.UtcNow;
            var timer = System.Diagnostics.Stopwatch.StartNew();
            try
            {
                success = dependency.Call();
            }
            finally
            {
                timer.Stop();
                telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
            }
```

<span data-ttu-id="14736-203">Si desea tooswitch desactivar el módulo de seguimiento de dependencia estándar de hello, quite tooDependencyTrackingTelemetryModule de referencia de hello en [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="14736-203">If you want tooswitch off hello standard dependency tracking module, remove hello reference tooDependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="14736-204">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="14736-204">Troubleshooting</span></span>
<span data-ttu-id="14736-205">*La marca de éxito de dependencia siempre muestra true o false.*</span><span class="sxs-lookup"><span data-stu-id="14736-205">*Dependency success flag always shows either true or false.*</span></span>

<span data-ttu-id="14736-206">*La consulta SQL no se muestra en su totalidad.*</span><span class="sxs-lookup"><span data-stu-id="14736-206">*SQL query not shown in full.*</span></span>

* <span data-ttu-id="14736-207">Versión más reciente de actualización toohello de hello SDK.</span><span class="sxs-lookup"><span data-stu-id="14736-207">Upgrade toohello latest version of hello SDK.</span></span> <span data-ttu-id="14736-208">Si la versión de .NET es inferior a la 4.6, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="14736-208">If your .NET version is less than 4.6:</span></span>
  * <span data-ttu-id="14736-209">Host de IIS: instalar [agente de visión de la aplicación](app-insights-monitor-performance-live-website-now.md) en los servidores de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="14736-209">IIS host: Install [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on hello host servers.</span></span>
  * <span data-ttu-id="14736-210">Aplicación web de Azure: abrir Application Insights pestaña en el panel de control de aplicación de hello web e instale Application Insights.</span><span class="sxs-lookup"><span data-stu-id="14736-210">Azure web app: Open Application Insights tab in hello web app control panel, and install Application Insights.</span></span>

## <a name="video"></a><span data-ttu-id="14736-211">Vídeo</span><span class="sxs-lookup"><span data-stu-id="14736-211">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="14736-212">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="14736-212">Next steps</span></span>
* [<span data-ttu-id="14736-213">Excepciones</span><span class="sxs-lookup"><span data-stu-id="14736-213">Exceptions</span></span>](app-insights-asp-net-exceptions.md)
* [<span data-ttu-id="14736-214">Datos de página y usuario</span><span class="sxs-lookup"><span data-stu-id="14736-214">User & page data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="14736-215">Disponibilidad</span><span class="sxs-lookup"><span data-stu-id="14736-215">Availability</span></span>](app-insights-monitor-web-app-availability.md)
