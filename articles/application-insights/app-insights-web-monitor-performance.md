---
title: "aaaMonitor estado de su aplicación y de uso con Application Insights"
description: "Introducción a Application Insights. Analice el uso, la disponibilidad y el rendimiento de sus aplicaciones web de Microsoft Azure o local."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 9230a6e65e5afb00c36122ff1d1de01ba19cd7f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-in-web-applications"></a><span data-ttu-id="e47bb-104">Supervisar el rendimiento de aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="e47bb-104">Monitor performance in web applications</span></span>


<span data-ttu-id="e47bb-105">Asegúrese de que la aplicación tendrá un rendimiento correcto y descubra rápidamente los posibles errores.</span><span class="sxs-lookup"><span data-stu-id="e47bb-105">Make sure your application is performing well, and find out quickly about any failures.</span></span> <span data-ttu-id="e47bb-106">[Application Insights] [ start] se le permiten sobre los problemas de rendimiento y excepciones, y le ayudan a encontrar y diagnosticar Hola causas raíz.</span><span class="sxs-lookup"><span data-stu-id="e47bb-106">[Application Insights][start] will tell you about any performance issues and exceptions, and help you find and diagnose hello root causes.</span></span>

<span data-ttu-id="e47bb-107">Application Insights puede supervisar aplicaciones y servicios web Java y ASP.NET y servicios WCF.</span><span class="sxs-lookup"><span data-stu-id="e47bb-107">Application Insights can monitor both Java and ASP.NET web applications and services, WCF services.</span></span> <span data-ttu-id="e47bb-108">Pueden estar hospedados localmente, en máquinas virtuales o como sitios web de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e47bb-108">They can be hosted on-premises, on virtual machines, or as Microsoft Azure websites.</span></span> 

<span data-ttu-id="e47bb-109">En el lado del cliente hello, Application Insights puede tardar telemetría de páginas web y una amplia variedad de dispositivos, incluidos iOS, Android y Windows aplicaciones de la tienda.</span><span class="sxs-lookup"><span data-stu-id="e47bb-109">On hello client side, Application Insights can take telemetry from web pages and a wide variety of devices including iOS, Android and Windows Store apps.</span></span>

>[!Note]
> <span data-ttu-id="e47bb-110">Hemos puesto a su disposición una nueva experiencia que permite buscar las páginas que funcionan con lentitud en su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="e47bb-110">We have made a new experience available for finding slow performing pages in your web application.</span></span> <span data-ttu-id="e47bb-111">Si no tienes acceso tooit, habilitarlo mediante la configuración de las opciones de vista previa con hello [hoja de vista previa](app-insights-previews.md).</span><span class="sxs-lookup"><span data-stu-id="e47bb-111">If you don't have access tooit, enable it by configuring your preview options with hello [Preview blade](app-insights-previews.md).</span></span> <span data-ttu-id="e47bb-112">Obtenga información sobre esta nueva experiencia en [buscar y corregir cuellos de botella de rendimiento con la investigación de rendimiento interactivo de hello](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span><span class="sxs-lookup"><span data-stu-id="e47bb-112">Read about this new experience in [Find and fix performance bottlenecks with hello interactive Performance investigation](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span></span>

## <span data-ttu-id="e47bb-113"><a name="setup"></a>Configuración de la supervisión de rendimiento</span><span class="sxs-lookup"><span data-stu-id="e47bb-113"><a name="setup"></a>Set up performance monitoring</span></span>
<span data-ttu-id="e47bb-114">Si aún no ha agregado tooyour Application Insights (es decir, si no tiene ApplicationInsights.config) del proyecto, elija una de estas formas tooget iniciado:</span><span class="sxs-lookup"><span data-stu-id="e47bb-114">If you haven't yet added Application Insights tooyour project (that is, if it doesn't have ApplicationInsights.config), choose one of these ways tooget started:</span></span>

* [<span data-ttu-id="e47bb-115">Aplicaciones web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e47bb-115">ASP.NET web apps</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="e47bb-116">Agregar supervisión de excepciones</span><span class="sxs-lookup"><span data-stu-id="e47bb-116">Add exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
  * [<span data-ttu-id="e47bb-117">Agregar supervisión de dependencias</span><span class="sxs-lookup"><span data-stu-id="e47bb-117">Add dependency monitoring</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="e47bb-118">Aplicaciones web J2EE</span><span class="sxs-lookup"><span data-stu-id="e47bb-118">J2EE web apps</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="e47bb-119">Agregar supervisión de dependencias</span><span class="sxs-lookup"><span data-stu-id="e47bb-119">Add dependency monitoring</span></span>](app-insights-java-agent.md)

## <span data-ttu-id="e47bb-120"><a name="view"></a>Exploración de las métricas de rendimiento</span><span class="sxs-lookup"><span data-stu-id="e47bb-120"><a name="view"></a>Exploring performance metrics</span></span>
<span data-ttu-id="e47bb-121">En [Hola portal de Azure](https://portal.azure.com), examinar los recursos de Application Insights toohello que configuró para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e47bb-121">In [hello Azure portal](https://portal.azure.com), browse toohello Application Insights resource that you set up for your application.</span></span> <span data-ttu-id="e47bb-122">hoja de información general de Hello muestra datos de rendimiento básicas:</span><span class="sxs-lookup"><span data-stu-id="e47bb-122">hello overview blade shows basic performance data:</span></span>

<span data-ttu-id="e47bb-123">Haga clic en cualquier toosee gráfico más detalle y los resultados de toosee durante un periodo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="e47bb-123">Click any chart toosee more detail, and toosee results for a longer period.</span></span> <span data-ttu-id="e47bb-124">Por ejemplo, haga clic en mosaico de las solicitudes de hello y, a continuación, seleccione un intervalo de tiempo:</span><span class="sxs-lookup"><span data-stu-id="e47bb-124">For example, click hello Requests tile and then select a time range:</span></span>

![Desplazarse por los datos de toomore y seleccione un intervalo de tiempo](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

<span data-ttu-id="e47bb-126">Haga clic en un gráfico toochoose las métricas que muestra, o agregar un nuevo gráfico y seleccione sus métricas:</span><span class="sxs-lookup"><span data-stu-id="e47bb-126">Click a chart toochoose which metrics it displays, or add a new chart and select its metrics:</span></span>

![Haga clic en una métrica de toochoose gráfico](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> <span data-ttu-id="e47bb-128">**Desactive todas las métricas de hello** selección completa de toosee Hola que está disponible.</span><span class="sxs-lookup"><span data-stu-id="e47bb-128">**Uncheck all hello metrics** toosee hello full selection that is available.</span></span> <span data-ttu-id="e47bb-129">las métricas de Hola se dividen en grupos; Cuando se selecciona cualquier miembro de un grupo, solo aparecen hello otros miembros de ese grupo.</span><span class="sxs-lookup"><span data-stu-id="e47bb-129">hello metrics fall into groups; when any member of a group is selected, only hello other members of that group appear.</span></span>

## <span data-ttu-id="e47bb-130"><a name="metrics"></a>¿Qué significa todo esto?</span><span class="sxs-lookup"><span data-stu-id="e47bb-130"><a name="metrics"></a>What does it all mean?</span></span> <span data-ttu-id="e47bb-131">Informes y mosaicos de rendimiento</span><span class="sxs-lookup"><span data-stu-id="e47bb-131">Performance tiles and reports</span></span>
<span data-ttu-id="e47bb-132">Puede obtener una gran variedad de métricas de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="e47bb-132">There are various performance metrics you can get.</span></span> <span data-ttu-id="e47bb-133">Comencemos con los que aparecen de forma predeterminada en el módulo de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="e47bb-133">Let's start with those that appear by default on hello application blade.</span></span>

### <a name="requests"></a><span data-ttu-id="e47bb-134">Solicitudes</span><span class="sxs-lookup"><span data-stu-id="e47bb-134">Requests</span></span>
<span data-ttu-id="e47bb-135">número de Hola de solicitudes HTTP recibidas en un período especificado.</span><span class="sxs-lookup"><span data-stu-id="e47bb-135">hello number of HTTP requests received in a specified period.</span></span> <span data-ttu-id="e47bb-136">Compare esto con resultados de hello en otro toosee informes cómo la aplicación se comporta como carga de hello varía.</span><span class="sxs-lookup"><span data-stu-id="e47bb-136">Compare this with hello results on other reports toosee how your app behaves as hello load varies.</span></span>

<span data-ttu-id="e47bb-137">Las solicitudes HTTP incluyen todas las solicitudes GET o POST de páginas, datos e imágenes.</span><span class="sxs-lookup"><span data-stu-id="e47bb-137">HTTP requests include all GET or POST requests for pages, data, and images.</span></span>

<span data-ttu-id="e47bb-138">Haga clic en hello mosaico tooget recuentos de direcciones URL específicas.</span><span class="sxs-lookup"><span data-stu-id="e47bb-138">Click on hello tile tooget counts for specific URLs.</span></span>

### <a name="average-response-time"></a><span data-ttu-id="e47bb-139">Tiempo medio de respuesta</span><span class="sxs-lookup"><span data-stu-id="e47bb-139">Average response time</span></span>
<span data-ttu-id="e47bb-140">Mide el tiempo de hello entre la entrada de la respuesta de hello y aplicación que se devuelve de una solicitud de web.</span><span class="sxs-lookup"><span data-stu-id="e47bb-140">Measures hello time between a web request entering your application and hello response being returned.</span></span>

<span data-ttu-id="e47bb-141">puntos de Hello muestran un movimiento promedio.</span><span class="sxs-lookup"><span data-stu-id="e47bb-141">hello points show a moving average.</span></span> <span data-ttu-id="e47bb-142">Si hay una gran cantidad de solicitudes, puede haber otras que se desvían de promedio de hello sin un pico obvio o variaciones en los gráficos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e47bb-142">If there are a lot of requests, there might be some that deviate from hello average without an obvious peak or dip in hello graph.</span></span>

<span data-ttu-id="e47bb-143">Busque picos poco habituales.</span><span class="sxs-lookup"><span data-stu-id="e47bb-143">Look for unusual peaks.</span></span> <span data-ttu-id="e47bb-144">En general, esperar toorise de tiempo de respuesta con un aumento de las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="e47bb-144">In general, expect response time toorise with a rise in requests.</span></span> <span data-ttu-id="e47bb-145">Si el aumento de hello es desproporcionado, la aplicación podría se esté enfrentando a un límite de recursos, como la capacidad de CPU u Hola de un servicio que utiliza.</span><span class="sxs-lookup"><span data-stu-id="e47bb-145">If hello rise is disproportionate, your app might be hitting a resource limit such as CPU or hello capacity of a service it uses.</span></span>

<span data-ttu-id="e47bb-146">Haga clic en tiempos de hello mosaico tooget de direcciones URL específicas.</span><span class="sxs-lookup"><span data-stu-id="e47bb-146">Click hello tile tooget times for specific URLs.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a><span data-ttu-id="e47bb-147">Solicitudes más lentas</span><span class="sxs-lookup"><span data-stu-id="e47bb-147">Slowest requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

<span data-ttu-id="e47bb-148">Muestra las solicitudes que pueden precisar un ajuste de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="e47bb-148">Shows which requests might need performance tuning.</span></span>

### <a name="failed-requests"></a><span data-ttu-id="e47bb-149">Error en las solicitudes</span><span class="sxs-lookup"><span data-stu-id="e47bb-149">Failed requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

<span data-ttu-id="e47bb-150">Un recuento de las solicitudes que inician excepciones no detectadas.</span><span class="sxs-lookup"><span data-stu-id="e47bb-150">A count of requests that threw uncaught exceptions.</span></span>

<span data-ttu-id="e47bb-151">Haga clic en hello mosaico toosee Hola detalles de errores específicos y seleccione una solicitud individual toosee sus detalles.</span><span class="sxs-lookup"><span data-stu-id="e47bb-151">Click hello tile toosee hello details of specific failures, and select an individual request toosee its detail.</span></span> 

<span data-ttu-id="e47bb-152">Solo se conserva una muestra representativa de los errores para su inspección individual.</span><span class="sxs-lookup"><span data-stu-id="e47bb-152">Only a representative sample of failures is retained for individual inspection.</span></span>

### <a name="other-metrics"></a><span data-ttu-id="e47bb-153">Otras métricas</span><span class="sxs-lookup"><span data-stu-id="e47bb-153">Other metrics</span></span>
<span data-ttu-id="e47bb-154">toosee qué otras métricas que puede mostrar, haga clic en un gráfico y, a continuación, anule la selección de hello métricas toosee Hola completa disponible establecidos.</span><span class="sxs-lookup"><span data-stu-id="e47bb-154">toosee what other metrics you can display, click a graph, and then deselect all hello metrics toosee hello full available set.</span></span> <span data-ttu-id="e47bb-155">Haga clic en (i) toosee definición de cada métrica.</span><span class="sxs-lookup"><span data-stu-id="e47bb-155">Click (i) toosee each metric's definition.</span></span>

![Anule la selección de todas las métricas toosee Hola conjunto](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

<span data-ttu-id="e47bb-157">Al seleccionar cualquier Hola deshabilita métrica Hola otras personas que no pueden aparecer en mismo gráfico.</span><span class="sxs-lookup"><span data-stu-id="e47bb-157">Selecting any metric disables hello others that can't appear on hello same chart.</span></span>

## <a name="set-alerts"></a><span data-ttu-id="e47bb-158">Establecer alertas</span><span class="sxs-lookup"><span data-stu-id="e47bb-158">Set alerts</span></span>
<span data-ttu-id="e47bb-159">toobe una notificación por correo electrónico de los valores inusuales de cualquier métrica, agregar una alerta.</span><span class="sxs-lookup"><span data-stu-id="e47bb-159">toobe notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="e47bb-160">Puede elegir los administradores de cuentas de toosend Hola correo electrónico toohello o direcciones de correo electrónico toospecific.</span><span class="sxs-lookup"><span data-stu-id="e47bb-160">You can choose either toosend hello email toohello account administrators, or toospecific email addresses.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

<span data-ttu-id="e47bb-161">Configurar otras propiedades de recursos de hello antes de Hola.</span><span class="sxs-lookup"><span data-stu-id="e47bb-161">Set hello resource before hello other properties.</span></span> <span data-ttu-id="e47bb-162">No elija recursos de webtest Hola si desea que las alertas de tooset en el rendimiento o las métricas de uso.</span><span class="sxs-lookup"><span data-stu-id="e47bb-162">Don't choose hello webtest resources if you want tooset alerts on performance or usage metrics.</span></span>

<span data-ttu-id="e47bb-163">Ser unidades de hello toonote cuidado en el que se le pide el valor del umbral de tooenter Hola.</span><span class="sxs-lookup"><span data-stu-id="e47bb-163">Be careful toonote hello units in which you're asked tooenter hello threshold value.</span></span>

<span data-ttu-id="e47bb-164">*No se ve botón alerta de hello agregar.*</span><span class="sxs-lookup"><span data-stu-id="e47bb-164">*I don't see hello Add Alert button.*</span></span> <span data-ttu-id="e47bb-165">¿-Es un toowhich de cuenta de grupo tienen acceso de sólo lectura?</span><span class="sxs-lookup"><span data-stu-id="e47bb-165">- Is this a group account toowhich you have read-only access?</span></span> <span data-ttu-id="e47bb-166">Póngase en contacto con el Administrador de la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="e47bb-166">Check with hello account administrator.</span></span>

## <span data-ttu-id="e47bb-167"><a name="diagnosis"></a>Diagnóstico de problemas</span><span class="sxs-lookup"><span data-stu-id="e47bb-167"><a name="diagnosis"></a>Diagnosing issues</span></span>
<span data-ttu-id="e47bb-168">Para buscar y diagnosticar problemas de rendimiento, lea estas sugerencias:</span><span class="sxs-lookup"><span data-stu-id="e47bb-168">Here are a few tips for finding and diagnosing performance issues:</span></span>

* <span data-ttu-id="e47bb-169">Configurar [pruebas web] [ availability] toobe una alerta si el sitio web deja de funcionar o responde lentamente o incorrectamente.</span><span class="sxs-lookup"><span data-stu-id="e47bb-169">Set up [web tests][availability] toobe alerted if your web site goes down or responds incorrectly or slowly.</span></span> 
* <span data-ttu-id="e47bb-170">Comparar el número de solicitudes de hello con otro toosee de métricas si hay errores o respuesta es lento tooload relacionado.</span><span class="sxs-lookup"><span data-stu-id="e47bb-170">Compare hello Request count with other metrics toosee if failures or slow response are related tooload.</span></span>
* <span data-ttu-id="e47bb-171">[Insertar y buscar las instrucciones de seguimiento] [ diagnostic] en su código toohelp identificar problemas.</span><span class="sxs-lookup"><span data-stu-id="e47bb-171">[Insert and search trace statements][diagnostic] in your code toohelp pinpoint problems.</span></span>
* <span data-ttu-id="e47bb-172">Supervise el funcionamiento de la aplicación web junto con [Live Metrics Stream][livestream].</span><span class="sxs-lookup"><span data-stu-id="e47bb-172">Monitor your Web app in operation with [Live Metrics Stream][livestream].</span></span>
* <span data-ttu-id="e47bb-173">Capturar el estado de saludo de la aplicación .net con [depurador instantánea][snapshot].</span><span class="sxs-lookup"><span data-stu-id="e47bb-173">Capture hello state of your .Net application with [Snapshot Debugger][snapshot].</span></span>

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a><span data-ttu-id="e47bb-174">Búsqueda y corrección de cuellos de botella de rendimiento con la investigación interactiva del rendimiento</span><span class="sxs-lookup"><span data-stu-id="e47bb-174">Find and fix performance bottlenecks with an interactive performance investigation</span></span>

<span data-ttu-id="e47bb-175">Puede usar Hola nuevas Application Insights rendimiento interactivo investigación toolocate áreas de la aplicación Web que se ralentizan el rendimiento general.</span><span class="sxs-lookup"><span data-stu-id="e47bb-175">You can use hello new Application Insights interactive performance investigation toolocate areas of your Web app that are slowing down overall performance.</span></span> <span data-ttu-id="e47bb-176">Se pueden buscar páginas específicas que se ralentizan y use Hola rápidamente [herramienta de generación de perfiles](app-insights-profiler.md) toosee si no hay una correlación entre estas páginas.</span><span class="sxs-lookup"><span data-stu-id="e47bb-176">You can quickly find specific pages that are slowing down, and use hello [Profiling tool](app-insights-profiler.md) toosee if there is a correlation between these pages.</span></span>

### <a name="create-a-list-of-slow-performing-pages"></a><span data-ttu-id="e47bb-177">Creación de una lista de páginas con un rendimiento lento</span><span class="sxs-lookup"><span data-stu-id="e47bb-177">Create a list of slow performing pages</span></span> 

<span data-ttu-id="e47bb-178">Hola primer paso para buscar problemas de rendimiento es tooget una lista de hello lenta responde páginas.</span><span class="sxs-lookup"><span data-stu-id="e47bb-178">hello first step for finding performance issues is tooget a list of hello slow responding pages.</span></span> <span data-ttu-id="e47bb-179">Hola captura de pantalla siguiente muestra cómo utilizar Hola rendimiento hoja tooget una lista de posibles tooinvestigate de páginas más.</span><span class="sxs-lookup"><span data-stu-id="e47bb-179">hello screen shot below demonstrates using hello Performance blade tooget a list of potential pages tooinvestigate further.</span></span> <span data-ttu-id="e47bb-180">Puede ver rápidamente desde esta página que ha habido una disminución del tiempo de respuesta de Hola de aplicación hello aproximadamente 6:00 p.m. y de nuevo a aproximadamente 10 P.M..</span><span class="sxs-lookup"><span data-stu-id="e47bb-180">You can quickly see from this page that there was a slow-down in hello response time of hello app at approximately 6:00 PM and again at approximately 10 PM.</span></span> <span data-ttu-id="e47bb-181">También puede ver que operación de hello GET/detalles del cliente tenía algunas larga ejecución operaciones con un tiempo de respuesta medio de 507.05 milisegundos.</span><span class="sxs-lookup"><span data-stu-id="e47bb-181">You can also see that hello GET customer/details operation had some long running operations with a median response time of 507.05 milliseconds.</span></span> 

![Rendimiento interactivo de Application Insights](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a><span data-ttu-id="e47bb-183">Exploración en profundidad de páginas concretas</span><span class="sxs-lookup"><span data-stu-id="e47bb-183">Drill down on specific pages</span></span>

<span data-ttu-id="e47bb-184">Una vez que tenga una instantánea del rendimiento de su aplicación, puede obtener más información sobre las operaciones concretas cuyo rendimiento es bajo.</span><span class="sxs-lookup"><span data-stu-id="e47bb-184">Once you have a snapshot of your app's performance, you can get more details on specific slow-performing operations.</span></span> <span data-ttu-id="e47bb-185">Haga clic en cualquier operación detalladamente Hola lista toosee Hola tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="e47bb-185">Click on any operation in hello list toosee hello details as shown below.</span></span> <span data-ttu-id="e47bb-186">En el gráfico de hello puede ver si el rendimiento de Hola se basa en una dependencia.</span><span class="sxs-lookup"><span data-stu-id="e47bb-186">From hello chart you can see if hello performance was based on a dependency.</span></span> <span data-ttu-id="e47bb-187">También puede ver cuántos Hola con experiencia de los usuarios distintos tiempos de respuesta.</span><span class="sxs-lookup"><span data-stu-id="e47bb-187">You can also see how many users experienced hello various response times.</span></span> 

![Hoja de operaciones de Application Insights](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a><span data-ttu-id="e47bb-189">Exploración en profundidad de un período concreto</span><span class="sxs-lookup"><span data-stu-id="e47bb-189">Drill down on a specific time period</span></span>

<span data-ttu-id="e47bb-190">Después de haber identificado un punto en el tiempo tooinvestigate, explorar en profundidad aún más toolook en operaciones específicas de Hola que podría haber causado la disminución del rendimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="e47bb-190">After you have identified a point in time tooinvestigate, drill down even further toolook at hello specific operations that might have caused hello performance slow-down.</span></span> <span data-ttu-id="e47bb-191">Al hacer clic en un punto específico en el tiempo se obtienen detalles de Hola de página de hello tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="e47bb-191">When you click on a specific point in time you get hello details of hello page as shown below.</span></span> <span data-ttu-id="e47bb-192">Hola ejemplo siguiente puede ver las operaciones de hello enumeradas para un período de tiempo determinado junto con los códigos de respuesta del servidor de Hola y duración de la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="e47bb-192">In hello example below you can see hello operations listed for a given time period along with hello server response codes and hello operation duration.</span></span> <span data-ttu-id="e47bb-193">Tiene también la dirección url de Hola para abrir un elemento de trabajo TFS si necesita toosend este equipo de desarrollo de tooyour de información.</span><span class="sxs-lookup"><span data-stu-id="e47bb-193">You also have hello url for opening a TFS work item if you need toosend this information tooyour development team.</span></span>

![Porción de tiempo de Application Insights](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a><span data-ttu-id="e47bb-195">Exploración en profundidad de una operación concreta</span><span class="sxs-lookup"><span data-stu-id="e47bb-195">Drill down on a specific operation</span></span>

<span data-ttu-id="e47bb-196">Después de haber identificado un punto en el tiempo tooinvestigate, explorar en profundidad aún más toolook en operaciones específicas de Hola que podría haber causado la disminución del rendimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="e47bb-196">After you have identified a point in time tooinvestigate, drill down even further toolook at hello specific operations that might have caused hello performance slow-down.</span></span> <span data-ttu-id="e47bb-197">Haga clic en una operación de hello muestra toosee Hola los detalles de operación de hello tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="e47bb-197">Click on an operation from hello list toosee hello details of hello operation as shown below.</span></span> <span data-ttu-id="e47bb-198">En este ejemplo que puede ver que falló la operación de Hola y Application Insights ha proporcionado detalles Hola de hello aplicación hello de excepción se produjo.</span><span class="sxs-lookup"><span data-stu-id="e47bb-198">In this example you can see that hello operation failed, and Application Insights has provided hello details of hello exception hello application threw.</span></span> <span data-ttu-id="e47bb-199">Una vez más, desde esta hoja se puede crear fácilmente un elemento de trabajo de TFS.</span><span class="sxs-lookup"><span data-stu-id="e47bb-199">Again, you can easily create a TFS work item from this blade.</span></span>

![Hoja de operaciones de Application Insights](./media/app-insights-web-monitor-performance/performance3.png)


## <span data-ttu-id="e47bb-201"><a name="next"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e47bb-201"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="e47bb-202">[Pruebas Web] [ availability] -han enviado solicitudes web tooyour aplicación a intervalos regulares desde alrededor de Hola a todos.</span><span class="sxs-lookup"><span data-stu-id="e47bb-202">[Web tests][availability] - Have web requests sent tooyour application at regular intervals from around hello world.</span></span>

<span data-ttu-id="e47bb-203">[Capturar y buscar seguimientos de diagnóstico] [ diagnostic] : insertar llamadas de seguimiento y examinar los problemas de hello resultados toopinpoint.</span><span class="sxs-lookup"><span data-stu-id="e47bb-203">[Capture and search diagnostic traces][diagnostic] - Insert trace calls and sift through hello results toopinpoint issues.</span></span>

<span data-ttu-id="e47bb-204">[Seguimiento del uso][usage]: averigüe cuántas personas usan la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e47bb-204">[Usage tracking][usage] - Find out how people use your application.</span></span>

<span data-ttu-id="e47bb-205">[Solución de problemas][qna]: con preguntas y respuestas</span><span class="sxs-lookup"><span data-stu-id="e47bb-205">[Troubleshooting][qna] - and Q & A</span></span>



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md



