---
title: "aaaMonitor rendimiento de la aplicación web de Azure | Documentos de Microsoft"
description: "Supervisión del rendimiento de Azure Web Apps. Carga y tiempo de respuesta de gráfico, información de dependencia y establecer alertas en el rendimiento."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0b2deb30-6ea8-4bc4-8ed0-26765b85149f
ms.service: azure-portal
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: d1083254e5c504b18f2ac5ae2368610dc2790436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-web-app-performance"></a><span data-ttu-id="b3aca-104">Supervisión del rendimiento de Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="b3aca-104">Monitor Azure web app performance</span></span>
<span data-ttu-id="b3aca-105">Hola [Portal de Azure](https://portal.azure.com) puede configurar la supervisión de rendimiento de aplicaciones para su [aplicaciones web de Azure](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b3aca-105">In hello [Azure Portal](https://portal.azure.com) you can set up application performance monitoring for your [Azure web apps](../app-service-web/app-service-web-overview.md).</span></span> <span data-ttu-id="b3aca-106">[Azure Application Insights](app-insights-overview.md) instrumenta la telemetría de aplicación toosend acerca de su servicio de Application Insights, donde se almacena y analiza toohello de actividades.</span><span class="sxs-lookup"><span data-stu-id="b3aca-106">[Azure Application Insights](app-insights-overview.md) instruments your app toosend telemetry about its activities toohello Application Insights service, where it is stored and analyzed.</span></span> <span data-ttu-id="b3aca-107">Allí, los gráficos de métricas y herramientas de búsqueda se pueden usar toohelp diagnosticar problemas, mejorar el rendimiento y evaluar el uso.</span><span class="sxs-lookup"><span data-stu-id="b3aca-107">There, metric charts and search tools can be used toohelp diagnose issues, improve performance, and assess usage.</span></span>

## <a name="run-time-or-build-time"></a><span data-ttu-id="b3aca-108">Tiempo de ejecución o de compilación</span><span class="sxs-lookup"><span data-stu-id="b3aca-108">Run time or build time</span></span>
<span data-ttu-id="b3aca-109">Puede configurar la supervisión mediante la instrumentación de la aplicación hello en cualquiera de estas dos maneras:</span><span class="sxs-lookup"><span data-stu-id="b3aca-109">You can configure monitoring by instrumenting hello app in either of two ways:</span></span>

* <span data-ttu-id="b3aca-110">**Tiempo de ejecución**: puede seleccionar una extensión de supervisión de rendimiento cuando la aplicación web ya esté activa.</span><span class="sxs-lookup"><span data-stu-id="b3aca-110">**Run-time** - You can select a performance monitoring extension when your web app is already live.</span></span> <span data-ttu-id="b3aca-111">No es necesario toorebuild o volver a instalar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b3aca-111">It isn't necessary toorebuild or re-install your app.</span></span> <span data-ttu-id="b3aca-112">Tendrá a disposición un conjunto estándar de paquetes que supervisan tiempos de respuesta, tasas de éxito, excepciones, dependencias, etc.</span><span class="sxs-lookup"><span data-stu-id="b3aca-112">You get a standard set of packages that monitor response times, success rates, exceptions, dependencies, and so on.</span></span> 
* <span data-ttu-id="b3aca-113">**Tiempo de compilación** : puede instalar un paquete en la aplicación que esté en desarrollo.</span><span class="sxs-lookup"><span data-stu-id="b3aca-113">**Build time** - You can install a package in your app in development.</span></span> <span data-ttu-id="b3aca-114">Esta opción es más versátil.</span><span class="sxs-lookup"><span data-stu-id="b3aca-114">This option is more versatile.</span></span> <span data-ttu-id="b3aca-115">En suma toohello mismos paquetes estándares, puede escribir telemetría de código toocustomize Hola o toosend su propia telemetría.</span><span class="sxs-lookup"><span data-stu-id="b3aca-115">In addition toohello same standard packages, you can write code toocustomize hello telemetry or toosend your own telemetry.</span></span> <span data-ttu-id="b3aca-116">Puede registrar eventos de registro según la semántica de toohello de su dominio de aplicación o actividades específicas.</span><span class="sxs-lookup"><span data-stu-id="b3aca-116">You can log specific activities or record events according toohello semantics of your app domain.</span></span> 

## <a name="run-time-instrumentation-with-application-insights"></a><span data-ttu-id="b3aca-117">Instrumentación del tiempo de ejecución con Application Insights</span><span class="sxs-lookup"><span data-stu-id="b3aca-117">Run time instrumentation with Application Insights</span></span>
<span data-ttu-id="b3aca-118">Si ya está ejecutando una aplicación web en Azure, ya goza de cierta supervisión: tasas de solicitudes y errores.</span><span class="sxs-lookup"><span data-stu-id="b3aca-118">If you're already running a web app in Azure, you already get some monitoring: request and error rates.</span></span> <span data-ttu-id="b3aca-119">Agregar Application Insights tooget más, como tiempos de respuesta, supervisión toodependencies de llamadas, detección inteligente y eficaz lenguaje de consulta de análisis de registros Hola.</span><span class="sxs-lookup"><span data-stu-id="b3aca-119">Add Application Insights tooget more, such as response times, monitoring calls toodependencies, smart detection, and hello powerful Log Analytics query language.</span></span> 

1. <span data-ttu-id="b3aca-120">**Seleccionar Application Insights** hello Azure panel de control de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="b3aca-120">**Select Application Insights** in hello Azure control panel for your web app.</span></span>
   
    ![En Supervisión, elija Application Insights.](./media/app-insights-azure-web-apps/05-extend.png)
   
   * <span data-ttu-id="b3aca-122">Elija toocreate un nuevo recurso, a menos que ya ha configurado un recurso de Application Insights para esta aplicación por otra ruta.</span><span class="sxs-lookup"><span data-stu-id="b3aca-122">Choose toocreate a new resource, unless you already set up an Application Insights resource for this app by another route.</span></span>
2. <span data-ttu-id="b3aca-123">**Instrumente la aplicación web** después de haber instalado Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b3aca-123">**Instrument your web app** after Application Insights has been installed.</span></span> 
   
    ![Instrumentación de la aplicación web](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   <span data-ttu-id="b3aca-125">**Habilite la supervisión de cliente** para la vista de página y la telemetría de usuario.</span><span class="sxs-lookup"><span data-stu-id="b3aca-125">**Enable client side monitoring** for page view and user telemetry.</span></span>

   * <span data-ttu-id="b3aca-126">Seleccione Configuración > Configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b3aca-126">Select Settings > Application Settings</span></span>
   * <span data-ttu-id="b3aca-127">En Configuración de la aplicación, agregue un nuevo par clave-valor:</span><span class="sxs-lookup"><span data-stu-id="b3aca-127">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="b3aca-128">Clave: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="b3aca-128">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="b3aca-129">Valor: `true`</span><span class="sxs-lookup"><span data-stu-id="b3aca-129">Value: `true`</span></span>
   * <span data-ttu-id="b3aca-130">**Guardar** Hola configuración y **reiniciar** la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b3aca-130">**Save** hello settings and **Restart** your app.</span></span>
3. <span data-ttu-id="b3aca-131">**Supervise la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="b3aca-131">**Monitor your app**.</span></span>  <span data-ttu-id="b3aca-132">[Datos de hello Expore](#explore-the-data).</span><span class="sxs-lookup"><span data-stu-id="b3aca-132">[Expore hello data](#explore-the-data).</span></span>

<span data-ttu-id="b3aca-133">Más adelante, si lo desea puede incorporar aplicación hello con Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b3aca-133">Later, you can build hello app with Application Insights if you want.</span></span>

<span data-ttu-id="b3aca-134">*¿Cómo quitar Application Insights, o cambiar toosending tooanother recursos?*</span><span class="sxs-lookup"><span data-stu-id="b3aca-134">*How do I remove Application Insights, or switch toosending tooanother resource?*</span></span>

* <span data-ttu-id="b3aca-135">En Azure, hoja de control de la aplicación de web Hola abierto y en las herramientas de desarrollo, abra **extensiones**.</span><span class="sxs-lookup"><span data-stu-id="b3aca-135">In Azure, open hello web app control blade, and under Development Tools, open **Extensions**.</span></span> <span data-ttu-id="b3aca-136">Eliminar la extensión de Application Insights de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3aca-136">Delete hello Application Insights extension.</span></span> <span data-ttu-id="b3aca-137">A continuación, en supervisión, elija Application Insights y cree o seleccione recurso Hola que desee.</span><span class="sxs-lookup"><span data-stu-id="b3aca-137">Then under Monitoring, choose Application Insights and create or select hello resource you want.</span></span>

## <a name="build-hello-app-with-application-insights"></a><span data-ttu-id="b3aca-138">Compilar la aplicación hello con Application Insights</span><span class="sxs-lookup"><span data-stu-id="b3aca-138">Build hello app with Application Insights</span></span>
<span data-ttu-id="b3aca-139">Application Insights puede proporcionar una telemetría más detallada instalando un SDK en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b3aca-139">Application Insights can provide more detailed telemetry by installing an SDK into your app.</span></span> <span data-ttu-id="b3aca-140">En concreto, puede recopilar registros de seguimiento, [escribir telemetría personalizada](app-insights-api-custom-events-metrics.md), y obtener informes de excepción más detallados.</span><span class="sxs-lookup"><span data-stu-id="b3aca-140">In particular, you can collect trace logs, [write custom telemetry](app-insights-api-custom-events-metrics.md), and get more detailed exception reports.</span></span>

1. <span data-ttu-id="b3aca-141">**En Visual Studio** (2013 Update 2 o posterior), configure Application Insights para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="b3aca-141">**In Visual Studio** (2013 update 2 or later), configure Application Insights for your project.</span></span>

    <span data-ttu-id="b3aca-142">Haga clic en proyecto de web de Hola y seleccione **Agregar > Application Insights** o **configurar Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="b3aca-142">Right-click hello web project, and select **Add > Application Insights** or **Configure Application Insights**.</span></span>
   
    ![Haga clic en proyecto de web de Hola y elija Agregar o configurar Application Insights](./media/app-insights-azure-web-apps/03-add.png)
   
    <span data-ttu-id="b3aca-144">Si se le pregunta toosign en, usar credenciales de Hola para su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3aca-144">If you're asked toosign in, use hello credentials for your Azure account.</span></span>
   
    <span data-ttu-id="b3aca-145">operación de Hello tiene dos efectos:</span><span class="sxs-lookup"><span data-stu-id="b3aca-145">hello operation has two effects:</span></span>
   
   1. <span data-ttu-id="b3aca-146">Crea un recurso de Application Insights en Azure, donde se almacenan, analizan y muestran los datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="b3aca-146">Creates an Application Insights resource in Azure, where telemetry is stored, analyzed and displayed.</span></span>
   2. <span data-ttu-id="b3aca-147">Hola código del tooyour del paquete de NuGet de visión de aplicación (si no está allí ya), se agrega y configura toosend telemetría toohello recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3aca-147">Adds hello Application Insights NuGet package tooyour code (if it isn't there already), and configures it toosend telemetry toohello Azure resource.</span></span>
2. <span data-ttu-id="b3aca-148">**Probar la telemetría de hello** por aplicación hello en ejecución en el equipo de desarrollo (F5).</span><span class="sxs-lookup"><span data-stu-id="b3aca-148">**Test hello telemetry** by running hello app in your development machine (F5).</span></span>
3. <span data-ttu-id="b3aca-149">**Publicar la aplicación hello** tooAzure Hola forma habitual.</span><span class="sxs-lookup"><span data-stu-id="b3aca-149">**Publish hello app** tooAzure in hello usual way.</span></span> 

<span data-ttu-id="b3aca-150">*¿Cómo se puede cambiar el recurso de Application Insights toosending tooa diferente?*</span><span class="sxs-lookup"><span data-stu-id="b3aca-150">*How do I switch toosending tooa different Application Insights resource?*</span></span>

* <span data-ttu-id="b3aca-151">En Visual Studio, proyecto de hello del menú contextual, elija **configurar Application Insights** y elija el recurso de Hola que desee.</span><span class="sxs-lookup"><span data-stu-id="b3aca-151">In Visual Studio, right-click hello project, choose **Configure Application Insights** and choose hello resource you want.</span></span> <span data-ttu-id="b3aca-152">Obtener Hola opción toocreate un nuevo recurso.</span><span class="sxs-lookup"><span data-stu-id="b3aca-152">You get hello option toocreate a new resource.</span></span> <span data-ttu-id="b3aca-153">Vuelva a compilar e implementar.</span><span class="sxs-lookup"><span data-stu-id="b3aca-153">Rebuild and redeploy.</span></span>

## <a name="explore-hello-data"></a><span data-ttu-id="b3aca-154">Explorar datos Hola</span><span class="sxs-lookup"><span data-stu-id="b3aca-154">Explore hello data</span></span>
1. <span data-ttu-id="b3aca-155">En la hoja de Application Insights Hola de su panel de control de aplicación web, vea las métricas en vivo, que muestra las solicitudes y errores dentro de un segundo o dos de ellos que se producen.</span><span class="sxs-lookup"><span data-stu-id="b3aca-155">On hello Application Insights blade of your web app control panel, you see Live Metrics, which shows requests and failures within a second or two of them occurring.</span></span> <span data-ttu-id="b3aca-156">Esta información es muy útil cuando se vuelve a publicar la aplicación ya que permite ver inmediatamente cualquier problema.</span><span class="sxs-lookup"><span data-stu-id="b3aca-156">It's very useful display when you're republishing your app - you can see any problems immediately.</span></span>
2. <span data-ttu-id="b3aca-157">Desplazarse por los recursos de Application Insights completo toohello.</span><span class="sxs-lookup"><span data-stu-id="b3aca-157">Click through toohello full Application Insights resource.</span></span>

    ![Hacer clic en las distintas opciones](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    <span data-ttu-id="b3aca-159">También puede ir allí directamente desde la exploración de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3aca-159">You can also go there either directly from Azure resource navigation.</span></span>

1. <span data-ttu-id="b3aca-160">Haga clic en cualquier tooget gráfico más detalle:</span><span class="sxs-lookup"><span data-stu-id="b3aca-160">Click through any chart tooget more detail:</span></span>
   
    ![En la hoja de información general de Application Insights de hello, haga clic en un gráfico](./media/app-insights-azure-web-apps/07-dependency.png)
   
    <span data-ttu-id="b3aca-162">También puede [personalizar las hojas de métricas](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="b3aca-162">You can [customize metrics blades](app-insights-metrics-explorer.md).</span></span>
2. <span data-ttu-id="b3aca-163">Haga clic en más toosee los eventos individuales y sus propiedades:</span><span class="sxs-lookup"><span data-stu-id="b3aca-163">Click through further toosee individual events and their properties:</span></span>
   
    ![Haga clic en un tooopen del tipo de evento filtra una búsqueda en ese tipo](./media/app-insights-azure-web-apps/08-requests.png)
   
    <span data-ttu-id="b3aca-165">Tenga en cuenta Hola "..." vínculo tooopen todas las propiedades.</span><span class="sxs-lookup"><span data-stu-id="b3aca-165">Notice hello "..." link tooopen all properties.</span></span>
   
    <span data-ttu-id="b3aca-166">También puede [personalizar las búsquedas](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="b3aca-166">You can [customize searches](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="b3aca-167">Para realizar búsquedas más eficaces a través de la telemetría, usar hello [lenguaje de consulta de análisis de registros](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="b3aca-167">For more powerful searches over your telemetry, use hello [Log Analytics query language](app-insights-analytics-tour.md).</span></span>

## <a name="more-telemetry"></a><span data-ttu-id="b3aca-168">Más telemetría</span><span class="sxs-lookup"><span data-stu-id="b3aca-168">More telemetry</span></span>

* [<span data-ttu-id="b3aca-169">Datos de carga de página web</span><span class="sxs-lookup"><span data-stu-id="b3aca-169">Web page load data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="b3aca-170">Telemetría personalizada</span><span class="sxs-lookup"><span data-stu-id="b3aca-170">Custom telemetry</span></span>](app-insights-api-custom-events-metrics.md)

## <a name="video"></a><span data-ttu-id="b3aca-171">Vídeo</span><span class="sxs-lookup"><span data-stu-id="b3aca-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="b3aca-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b3aca-172">Next steps</span></span>
* <span data-ttu-id="b3aca-173">[Ejecutar el analizador de hello en la aplicación activa](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="b3aca-173">[Run hello profiler on your live app](app-insights-profiler.md).</span></span>
* <span data-ttu-id="b3aca-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample): supervisar Azure Functions con Application Insights</span><span class="sxs-lookup"><span data-stu-id="b3aca-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - monitor Azure Functions with Application Insights</span></span>
* <span data-ttu-id="b3aca-175">[Habilitar diagnósticos de Azure](app-insights-azure-diagnostics.md) tooApplication toobe enviado información.</span><span class="sxs-lookup"><span data-stu-id="b3aca-175">[Enable Azure diagnostics](app-insights-azure-diagnostics.md) toobe sent tooApplication Insights.</span></span>
* <span data-ttu-id="b3aca-176">[Supervisar las métricas de mantenimiento de servicio](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake que el servicio esté disponible y capacidad de respuesta.</span><span class="sxs-lookup"><span data-stu-id="b3aca-176">[Monitor service health metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
* <span data-ttu-id="b3aca-177">[Reciba notificaciones de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) cada vez que se produzcan eventos de operaciones o las métricas traspasen un umbral.</span><span class="sxs-lookup"><span data-stu-id="b3aca-177">[Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="b3aca-178">Use [Application Insights para las aplicaciones de JavaScript y páginas web](app-insights-javascript.md) tooget telemetría de cliente de exploradores de Hola que visite una página web.</span><span class="sxs-lookup"><span data-stu-id="b3aca-178">Use [Application Insights for JavaScript apps and web pages](app-insights-javascript.md) tooget client telemetry from hello browsers that visit a web page.</span></span>
* <span data-ttu-id="b3aca-179">[Configurar las pruebas web de disponibilidad](app-insights-monitor-web-app-availability.md) toobe una alerta si el sitio está inactivo.</span><span class="sxs-lookup"><span data-stu-id="b3aca-179">[Set up Availability web tests](app-insights-monitor-web-app-availability.md) toobe alerted if your site is down.</span></span>

