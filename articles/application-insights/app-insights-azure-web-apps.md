---
title: "Supervisión del rendimiento de aplicaciones web de Azure | Microsoft Docs"
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
ms.openlocfilehash: f2bbadfbcb93873ed910aeff050bd6896e2e8fec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-azure-web-app-performance"></a><span data-ttu-id="bae7e-104">Supervisión del rendimiento de Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="bae7e-104">Monitor Azure web app performance</span></span>
<span data-ttu-id="bae7e-105">En [Azure Portal](https://portal.azure.com), puede configurar la supervisión de rendimiento de sus aplicaciones de [Azure Web Apps](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bae7e-105">In the [Azure Portal](https://portal.azure.com) you can set up application performance monitoring for your [Azure web apps](../app-service-web/app-service-web-overview.md).</span></span> <span data-ttu-id="bae7e-106">[Azure Application Insights](app-insights-overview.md) instrumenta la aplicación para que envíe datos de telemetría sobre sus actividades al servicio Application Insights, donde se almacenan y analizan.</span><span class="sxs-lookup"><span data-stu-id="bae7e-106">[Azure Application Insights](app-insights-overview.md) instruments your app to send telemetry about its activities to the Application Insights service, where it is stored and analyzed.</span></span> <span data-ttu-id="bae7e-107">En esta plataforma, se pueden usar los gráficos de métricas y las herramientas de búsqueda para ayudar a diagnosticar problemas, mejorar el rendimiento y evaluar el uso.</span><span class="sxs-lookup"><span data-stu-id="bae7e-107">There, metric charts and search tools can be used to help diagnose issues, improve performance, and assess usage.</span></span>

## <a name="run-time-or-build-time"></a><span data-ttu-id="bae7e-108">Tiempo de ejecución o de compilación</span><span class="sxs-lookup"><span data-stu-id="bae7e-108">Run time or build time</span></span>
<span data-ttu-id="bae7e-109">Puede configurar la supervisión mediante la instrumentación de la aplicación de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="bae7e-109">You can configure monitoring by instrumenting the app in either of two ways:</span></span>

* <span data-ttu-id="bae7e-110">**Tiempo de ejecución**: puede seleccionar una extensión de supervisión de rendimiento cuando la aplicación web ya esté activa.</span><span class="sxs-lookup"><span data-stu-id="bae7e-110">**Run-time** - You can select a performance monitoring extension when your web app is already live.</span></span> <span data-ttu-id="bae7e-111">No es necesario volver a compilar o instalar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bae7e-111">It isn't necessary to rebuild or re-install your app.</span></span> <span data-ttu-id="bae7e-112">Tendrá a disposición un conjunto estándar de paquetes que supervisan tiempos de respuesta, tasas de éxito, excepciones, dependencias, etc.</span><span class="sxs-lookup"><span data-stu-id="bae7e-112">You get a standard set of packages that monitor response times, success rates, exceptions, dependencies, and so on.</span></span> 
* <span data-ttu-id="bae7e-113">**Tiempo de compilación** : puede instalar un paquete en la aplicación que esté en desarrollo.</span><span class="sxs-lookup"><span data-stu-id="bae7e-113">**Build time** - You can install a package in your app in development.</span></span> <span data-ttu-id="bae7e-114">Esta opción es más versátil.</span><span class="sxs-lookup"><span data-stu-id="bae7e-114">This option is more versatile.</span></span> <span data-ttu-id="bae7e-115">Además de los mismos paquetes estándares, puede escribir código para personalizar los datos de telemetría o enviar los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="bae7e-115">In addition to the same standard packages, you can write code to customize the telemetry or to send your own telemetry.</span></span> <span data-ttu-id="bae7e-116">Puede registrar las actividades específicas o grabar eventos según la semántica del dominio de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bae7e-116">You can log specific activities or record events according to the semantics of your app domain.</span></span> 

## <a name="run-time-instrumentation-with-application-insights"></a><span data-ttu-id="bae7e-117">Instrumentación del tiempo de ejecución con Application Insights</span><span class="sxs-lookup"><span data-stu-id="bae7e-117">Run time instrumentation with Application Insights</span></span>
<span data-ttu-id="bae7e-118">Si ya está ejecutando una aplicación web en Azure, ya goza de cierta supervisión: tasas de solicitudes y errores.</span><span class="sxs-lookup"><span data-stu-id="bae7e-118">If you're already running a web app in Azure, you already get some monitoring: request and error rates.</span></span> <span data-ttu-id="bae7e-119">Agregue Application Insights para obtener más características, como tiempos de respuesta, supervisión de las llamadas a las dependencias, detección inteligente y el eficaz lenguaje de consulta de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="bae7e-119">Add Application Insights to get more, such as response times, monitoring calls to dependencies, smart detection, and the powerful Log Analytics query language.</span></span> 

1. <span data-ttu-id="bae7e-120">**Seleccione Application Insights** en el panel de control de Azure para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bae7e-120">**Select Application Insights** in the Azure control panel for your web app.</span></span>
   
    ![En Supervisión, elija Application Insights.](./media/app-insights-azure-web-apps/05-extend.png)
   
   * <span data-ttu-id="bae7e-122">Elija crear un nuevo recurso a menos que ya haya configurado un recurso de Application Insights para esta aplicación por otra ruta.</span><span class="sxs-lookup"><span data-stu-id="bae7e-122">Choose to create a new resource, unless you already set up an Application Insights resource for this app by another route.</span></span>
2. <span data-ttu-id="bae7e-123">**Instrumente la aplicación web** después de haber instalado Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bae7e-123">**Instrument your web app** after Application Insights has been installed.</span></span> 
   
    ![Instrumentación de la aplicación web](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   <span data-ttu-id="bae7e-125">**Habilite la supervisión de cliente** para la vista de página y la telemetría de usuario.</span><span class="sxs-lookup"><span data-stu-id="bae7e-125">**Enable client side monitoring** for page view and user telemetry.</span></span>

   * <span data-ttu-id="bae7e-126">Seleccione Configuración > Configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bae7e-126">Select Settings > Application Settings</span></span>
   * <span data-ttu-id="bae7e-127">En Configuración de la aplicación, agregue un nuevo par clave-valor:</span><span class="sxs-lookup"><span data-stu-id="bae7e-127">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="bae7e-128">Clave: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="bae7e-128">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="bae7e-129">Valor: `true`</span><span class="sxs-lookup"><span data-stu-id="bae7e-129">Value: `true`</span></span>
   * <span data-ttu-id="bae7e-130">**Guarde** la configuración y **reinicie** la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bae7e-130">**Save** the settings and **Restart** your app.</span></span>
3. <span data-ttu-id="bae7e-131">**Supervise la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="bae7e-131">**Monitor your app**.</span></span>  <span data-ttu-id="bae7e-132">[Explore los datos](#explore-the-data).</span><span class="sxs-lookup"><span data-stu-id="bae7e-132">[Expore the data](#explore-the-data).</span></span>

<span data-ttu-id="bae7e-133">Posteriormente, si quiere, puede compilar la aplicación con Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bae7e-133">Later, you can build the app with Application Insights if you want.</span></span>

<span data-ttu-id="bae7e-134">*¿Cómo puedo quitar Application Insights o cambiar para enviar a otro recurso?*</span><span class="sxs-lookup"><span data-stu-id="bae7e-134">*How do I remove Application Insights, or switch to sending to another resource?*</span></span>

* <span data-ttu-id="bae7e-135">En Azure, abra la hoja de control de la aplicación web y en Herramientas de desarrollo, abra **Extensiones**.</span><span class="sxs-lookup"><span data-stu-id="bae7e-135">In Azure, open the web app control blade, and under Development Tools, open **Extensions**.</span></span> <span data-ttu-id="bae7e-136">Elimine la extensión de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bae7e-136">Delete the Application Insights extension.</span></span> <span data-ttu-id="bae7e-137">En Supervisión, elija Application Insights y cree o seleccione el recurso que desee.</span><span class="sxs-lookup"><span data-stu-id="bae7e-137">Then under Monitoring, choose Application Insights and create or select the resource you want.</span></span>

## <a name="build-the-app-with-application-insights"></a><span data-ttu-id="bae7e-138">Compilación de la aplicación con Application Insights</span><span class="sxs-lookup"><span data-stu-id="bae7e-138">Build the app with Application Insights</span></span>
<span data-ttu-id="bae7e-139">Application Insights puede proporcionar una telemetría más detallada instalando un SDK en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bae7e-139">Application Insights can provide more detailed telemetry by installing an SDK into your app.</span></span> <span data-ttu-id="bae7e-140">En concreto, puede recopilar registros de seguimiento, [escribir telemetría personalizada](app-insights-api-custom-events-metrics.md), y obtener informes de excepción más detallados.</span><span class="sxs-lookup"><span data-stu-id="bae7e-140">In particular, you can collect trace logs, [write custom telemetry](app-insights-api-custom-events-metrics.md), and get more detailed exception reports.</span></span>

1. <span data-ttu-id="bae7e-141">**En Visual Studio** (2013 Update 2 o posterior), configure Application Insights para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="bae7e-141">**In Visual Studio** (2013 update 2 or later), configure Application Insights for your project.</span></span>

    <span data-ttu-id="bae7e-142">Haga clic con el botón derecho en el proyecto web y seleccione **Agregar > Application Insights** o **Configurar Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="bae7e-142">Right-click the web project, and select **Add > Application Insights** or **Configure Application Insights**.</span></span>
   
    ![Haga clic con el botón derecho en el proyecto web y elija Agregar o Configurar Application Insights](./media/app-insights-azure-web-apps/03-add.png)
   
    <span data-ttu-id="bae7e-144">Cuando se la pide que inicie sesión, use las credenciales de su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="bae7e-144">If you're asked to sign in, use the credentials for your Azure account.</span></span>
   
    <span data-ttu-id="bae7e-145">La operación tiene dos efectos:</span><span class="sxs-lookup"><span data-stu-id="bae7e-145">The operation has two effects:</span></span>
   
   1. <span data-ttu-id="bae7e-146">Crea un recurso de Application Insights en Azure, donde se almacenan, analizan y muestran los datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="bae7e-146">Creates an Application Insights resource in Azure, where telemetry is stored, analyzed and displayed.</span></span>
   2. <span data-ttu-id="bae7e-147">Agrega el paquete NuGet de Application Insights al código (si todavía no está) y lo configura para enviar los datos de telemetría al recurso de Azure.</span><span class="sxs-lookup"><span data-stu-id="bae7e-147">Adds the Application Insights NuGet package to your code (if it isn't there already), and configures it to send telemetry to the Azure resource.</span></span>
2. <span data-ttu-id="bae7e-148">**Pruebe la telemetría** ejecutando la aplicación en la máquina de desarrollo (F5).</span><span class="sxs-lookup"><span data-stu-id="bae7e-148">**Test the telemetry** by running the app in your development machine (F5).</span></span>
3. <span data-ttu-id="bae7e-149">**Publique la aplicación** en Azure de la forma habitual.</span><span class="sxs-lookup"><span data-stu-id="bae7e-149">**Publish the app** to Azure in the usual way.</span></span> 

<span data-ttu-id="bae7e-150">*¿Cómo cambio para enviar a un recurso de Application Insights diferente?*</span><span class="sxs-lookup"><span data-stu-id="bae7e-150">*How do I switch to sending to a different Application Insights resource?*</span></span>

* <span data-ttu-id="bae7e-151">En Visual Studio, haga clic con el botón derecho en el proyecto, elija **Configurar Application Insights** y seleccione el recurso que desea.</span><span class="sxs-lookup"><span data-stu-id="bae7e-151">In Visual Studio, right-click the project, choose **Configure Application Insights** and choose the resource you want.</span></span> <span data-ttu-id="bae7e-152">Tiene la opción de crear un nuevo recurso.</span><span class="sxs-lookup"><span data-stu-id="bae7e-152">You get the option to create a new resource.</span></span> <span data-ttu-id="bae7e-153">Vuelva a compilar e implementar.</span><span class="sxs-lookup"><span data-stu-id="bae7e-153">Rebuild and redeploy.</span></span>

## <a name="explore-the-data"></a><span data-ttu-id="bae7e-154">Exploración de los datos</span><span class="sxs-lookup"><span data-stu-id="bae7e-154">Explore the data</span></span>
1. <span data-ttu-id="bae7e-155">En la hoja Application Insights del panel de control de la aplicación web, verá Live Metrics, que muestra los errores y solicitudes al segundo o dos segundos de producirse.</span><span class="sxs-lookup"><span data-stu-id="bae7e-155">On the Application Insights blade of your web app control panel, you see Live Metrics, which shows requests and failures within a second or two of them occurring.</span></span> <span data-ttu-id="bae7e-156">Esta información es muy útil cuando se vuelve a publicar la aplicación ya que permite ver inmediatamente cualquier problema.</span><span class="sxs-lookup"><span data-stu-id="bae7e-156">It's very useful display when you're republishing your app - you can see any problems immediately.</span></span>
2. <span data-ttu-id="bae7e-157">Haga clic en las distintas opciones hasta llegar al recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bae7e-157">Click through to the full Application Insights resource.</span></span>

    ![Hacer clic en las distintas opciones](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    <span data-ttu-id="bae7e-159">También puede ir allí directamente desde la exploración de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="bae7e-159">You can also go there either directly from Azure resource navigation.</span></span>

1. <span data-ttu-id="bae7e-160">Haga clic en cualquier gráfico para obtener información más detallada:</span><span class="sxs-lookup"><span data-stu-id="bae7e-160">Click through any chart to get more detail:</span></span>
   
    ![En la hoja de información general de Application Insights, haga clic en un gráfico.](./media/app-insights-azure-web-apps/07-dependency.png)
   
    <span data-ttu-id="bae7e-162">También puede [personalizar las hojas de métricas](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="bae7e-162">You can [customize metrics blades](app-insights-metrics-explorer.md).</span></span>
2. <span data-ttu-id="bae7e-163">Siga haciendo clic para ver los eventos individuales y sus propiedades:</span><span class="sxs-lookup"><span data-stu-id="bae7e-163">Click through further to see individual events and their properties:</span></span>
   
    ![Haga clic en un tipo de evento para abrir una búsqueda filtrada en ese tipo.](./media/app-insights-azure-web-apps/08-requests.png)
   
    <span data-ttu-id="bae7e-165">Observe el vínculo "..." para abrir todas las propiedades.</span><span class="sxs-lookup"><span data-stu-id="bae7e-165">Notice the "..." link to open all properties.</span></span>
   
    <span data-ttu-id="bae7e-166">También puede [personalizar las búsquedas](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="bae7e-166">You can [customize searches](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="bae7e-167">Para realizar búsquedas más eficaces sobre los datos de telemetría, use el [lenguaje de consulta de Log Analytics](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="bae7e-167">For more powerful searches over your telemetry, use the [Log Analytics query language](app-insights-analytics-tour.md).</span></span>

## <a name="more-telemetry"></a><span data-ttu-id="bae7e-168">Más telemetría</span><span class="sxs-lookup"><span data-stu-id="bae7e-168">More telemetry</span></span>

* [<span data-ttu-id="bae7e-169">Datos de carga de página web</span><span class="sxs-lookup"><span data-stu-id="bae7e-169">Web page load data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="bae7e-170">Telemetría personalizada</span><span class="sxs-lookup"><span data-stu-id="bae7e-170">Custom telemetry</span></span>](app-insights-api-custom-events-metrics.md)

## <a name="video"></a><span data-ttu-id="bae7e-171">Vídeo</span><span class="sxs-lookup"><span data-stu-id="bae7e-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="bae7e-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bae7e-172">Next steps</span></span>
* <span data-ttu-id="bae7e-173">[Ejecute el generador de perfiles en la aplicación activa](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="bae7e-173">[Run the profiler on your live app](app-insights-profiler.md).</span></span>
* <span data-ttu-id="bae7e-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample): supervisar Azure Functions con Application Insights</span><span class="sxs-lookup"><span data-stu-id="bae7e-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - monitor Azure Functions with Application Insights</span></span>
* <span data-ttu-id="bae7e-175">[Diagnósticos de Microsoft Azure](app-insights-azure-diagnostics.md) para enviar este tipo de información a Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bae7e-175">[Enable Azure diagnostics](app-insights-azure-diagnostics.md) to be sent to Application Insights.</span></span>
* <span data-ttu-id="bae7e-176">[Supervise las métricas del estado del servicio](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) para asegurarse de que el servicio está disponible y responde adecuadamente.</span><span class="sxs-lookup"><span data-stu-id="bae7e-176">[Monitor service health metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
* <span data-ttu-id="bae7e-177">[Reciba notificaciones de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) cada vez que se produzcan eventos de operaciones o las métricas traspasen un umbral.</span><span class="sxs-lookup"><span data-stu-id="bae7e-177">[Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="bae7e-178">Use [aplicaciones y páginas web de Application Insights para JavaScript](app-insights-javascript.md) para obtener la telemetría del cliente de los exploradores que visitan una página web.</span><span class="sxs-lookup"><span data-stu-id="bae7e-178">Use [Application Insights for JavaScript apps and web pages](app-insights-javascript.md) to get client telemetry from the browsers that visit a web page.</span></span>
* <span data-ttu-id="bae7e-179">[Configure pruebas web de disponibilidad](app-insights-monitor-web-app-availability.md) para recibir una alerta si el sitio deja de estar activo.</span><span class="sxs-lookup"><span data-stu-id="bae7e-179">[Set up Availability web tests](app-insights-monitor-web-app-availability.md) to be alerted if your site is down.</span></span>

