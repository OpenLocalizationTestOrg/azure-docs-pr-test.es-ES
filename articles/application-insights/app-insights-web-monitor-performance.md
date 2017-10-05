---
title: "Supervisar el estado y el uso de su aplicación con Application Insights"
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
ms.openlocfilehash: 5b7b1f4a53cd2624ee8e2ab684ba6ba63252674f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-performance-in-web-applications"></a><span data-ttu-id="cb7ea-104">Supervisar el rendimiento de aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="cb7ea-104">Monitor performance in web applications</span></span>


<span data-ttu-id="cb7ea-105">Asegúrese de que la aplicación tendrá un rendimiento correcto y descubra rápidamente los posibles errores.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-105">Make sure your application is performing well, and find out quickly about any failures.</span></span> <span data-ttu-id="cb7ea-106">[Application Insights][start] le indicará las excepciones y los problemas de rendimiento, y lo ayudará a buscar y diagnosticar las causas principales.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-106">[Application Insights][start] will tell you about any performance issues and exceptions, and help you find and diagnose the root causes.</span></span>

<span data-ttu-id="cb7ea-107">Application Insights puede supervisar aplicaciones y servicios web Java y ASP.NET y servicios WCF.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-107">Application Insights can monitor both Java and ASP.NET web applications and services, WCF services.</span></span> <span data-ttu-id="cb7ea-108">Pueden estar hospedados localmente, en máquinas virtuales o como sitios web de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-108">They can be hosted on-premises, on virtual machines, or as Microsoft Azure websites.</span></span> 

<span data-ttu-id="cb7ea-109">En el lado del cliente, Application Insights puede obtener datos de telemetría de páginas web y una amplia variedad de dispositivos, entre los que se incluyen iOS, Android y aplicaciones de la Tienda Windows.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-109">On the client side, Application Insights can take telemetry from web pages and a wide variety of devices including iOS, Android and Windows Store apps.</span></span>

>[!Note]
> <span data-ttu-id="cb7ea-110">Hemos puesto a su disposición una nueva experiencia que permite buscar las páginas que funcionan con lentitud en su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-110">We have made a new experience available for finding slow performing pages in your web application.</span></span> <span data-ttu-id="cb7ea-111">Si no tiene acceso a ella, para habilitarla configure las opciones de vista previa con el [hoja Vista previa](app-insights-previews.md).</span><span class="sxs-lookup"><span data-stu-id="cb7ea-111">If you don't have access to it, enable it by configuring your preview options with the [Preview blade](app-insights-previews.md).</span></span> <span data-ttu-id="cb7ea-112">Para obtener información acerca de esta nueva experiencia, lea [Búsqueda y corrección de cuellos de botella de rendimiento con la investigación interactiva del rendimiento](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span><span class="sxs-lookup"><span data-stu-id="cb7ea-112">Read about this new experience in [Find and fix performance bottlenecks with the interactive Performance investigation](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span></span>

## <span data-ttu-id="cb7ea-113"><a name="setup"></a>Configuración de la supervisión de rendimiento</span><span class="sxs-lookup"><span data-stu-id="cb7ea-113"><a name="setup"></a>Set up performance monitoring</span></span>
<span data-ttu-id="cb7ea-114">Si todavía no ha agregado Application Insights a un proyecto (es decir, si no dispone de ApplicationInsights.config), puede comenzar con uno de estos procedimientos:</span><span class="sxs-lookup"><span data-stu-id="cb7ea-114">If you haven't yet added Application Insights to your project (that is, if it doesn't have ApplicationInsights.config), choose one of these ways to get started:</span></span>

* [<span data-ttu-id="cb7ea-115">Aplicaciones web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="cb7ea-115">ASP.NET web apps</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="cb7ea-116">Agregar supervisión de excepciones</span><span class="sxs-lookup"><span data-stu-id="cb7ea-116">Add exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
  * [<span data-ttu-id="cb7ea-117">Agregar supervisión de dependencias</span><span class="sxs-lookup"><span data-stu-id="cb7ea-117">Add dependency monitoring</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="cb7ea-118">Aplicaciones web J2EE</span><span class="sxs-lookup"><span data-stu-id="cb7ea-118">J2EE web apps</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="cb7ea-119">Agregar supervisión de dependencias</span><span class="sxs-lookup"><span data-stu-id="cb7ea-119">Add dependency monitoring</span></span>](app-insights-java-agent.md)

## <span data-ttu-id="cb7ea-120"><a name="view"></a>Exploración de las métricas de rendimiento</span><span class="sxs-lookup"><span data-stu-id="cb7ea-120"><a name="view"></a>Exploring performance metrics</span></span>
<span data-ttu-id="cb7ea-121">En el [Portal de Azure](https://portal.azure.com), busque el recurso de Application Insights que configuró para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-121">In [the Azure portal](https://portal.azure.com), browse to the Application Insights resource that you set up for your application.</span></span> <span data-ttu-id="cb7ea-122">La hoja de información general muestra los datos de rendimiento básicos:</span><span class="sxs-lookup"><span data-stu-id="cb7ea-122">The overview blade shows basic performance data:</span></span>

<span data-ttu-id="cb7ea-123">Haga clic en cualquier gráfico para ver su contenido con mayor detalle y los resultados durante más tiempo.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-123">Click any chart to see more detail, and to see results for a longer period.</span></span> <span data-ttu-id="cb7ea-124">Por ejemplo, haga clic en el mosaico Solicitudes y seleccione un intervalo de tiempo:</span><span class="sxs-lookup"><span data-stu-id="cb7ea-124">For example, click the Requests tile and then select a time range:</span></span>

![Haga clic en las distintas opciones para obtener más datos y seleccionar un intervalo de tiempo](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

<span data-ttu-id="cb7ea-126">Haga clic en un gráfico para elegir las métricas mostradas o para agregar un nuevo gráfico y seleccionar sus métricas:</span><span class="sxs-lookup"><span data-stu-id="cb7ea-126">Click a chart to choose which metrics it displays, or add a new chart and select its metrics:</span></span>

![Haga clic en un gráfico para elegir las métricas](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> <span data-ttu-id="cb7ea-128">**Desactive todas las métricas** para ver todas las métricas disponibles.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-128">**Uncheck all the metrics** to see the full selection that is available.</span></span> <span data-ttu-id="cb7ea-129">Las métricas se organizan en grupos. Cuando se selecciona un miembro de un grupo, solo aparecen los demás miembros de dicho grupo.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-129">The metrics fall into groups; when any member of a group is selected, only the other members of that group appear.</span></span>

## <span data-ttu-id="cb7ea-130"><a name="metrics"></a>¿Qué significa todo esto?</span><span class="sxs-lookup"><span data-stu-id="cb7ea-130"><a name="metrics"></a>What does it all mean?</span></span> <span data-ttu-id="cb7ea-131">Informes y mosaicos de rendimiento</span><span class="sxs-lookup"><span data-stu-id="cb7ea-131">Performance tiles and reports</span></span>
<span data-ttu-id="cb7ea-132">Puede obtener una gran variedad de métricas de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-132">There are various performance metrics you can get.</span></span> <span data-ttu-id="cb7ea-133">Comencemos por las que aparecen de forma predeterminada en la hoja de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-133">Let's start with those that appear by default on the application blade.</span></span>

### <a name="requests"></a><span data-ttu-id="cb7ea-134">Solicitudes</span><span class="sxs-lookup"><span data-stu-id="cb7ea-134">Requests</span></span>
<span data-ttu-id="cb7ea-135">El número de solicitudes HTTP que se reciben en un período específico.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-135">The number of HTTP requests received in a specified period.</span></span> <span data-ttu-id="cb7ea-136">Compare este dato con los resultados de otros informes para ver cómo se comporta la aplicación cuando la carga varía.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-136">Compare this with the results on other reports to see how your app behaves as the load varies.</span></span>

<span data-ttu-id="cb7ea-137">Las solicitudes HTTP incluyen todas las solicitudes GET o POST de páginas, datos e imágenes.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-137">HTTP requests include all GET or POST requests for pages, data, and images.</span></span>

<span data-ttu-id="cb7ea-138">Haga clic en el mosaico para obtener las cuentas de URL específicas.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-138">Click on the tile to get counts for specific URLs.</span></span>

### <a name="average-response-time"></a><span data-ttu-id="cb7ea-139">Tiempo de respuesta promedio</span><span class="sxs-lookup"><span data-stu-id="cb7ea-139">Average response time</span></span>
<span data-ttu-id="cb7ea-140">Mide el tiempo entre la entrada de una solicitud web y la devolución de la respuesta correspondiente.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-140">Measures the time between a web request entering your application and the response being returned.</span></span>

<span data-ttu-id="cb7ea-141">Los puntos muestran una media móvil.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-141">The points show a moving average.</span></span> <span data-ttu-id="cb7ea-142">Si se producen muchas solicitudes, es posible que algunas de ellas se desvíen de la media sin que en el gráfico se muestre ningún pico o descenso evidente.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-142">If there are a lot of requests, there might be some that deviate from the average without an obvious peak or dip in the graph.</span></span>

<span data-ttu-id="cb7ea-143">Busque picos poco habituales.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-143">Look for unusual peaks.</span></span> <span data-ttu-id="cb7ea-144">Por lo general, el tiempo de respuesta aumenta cuando aumentan las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-144">In general, expect response time to rise with a rise in requests.</span></span> <span data-ttu-id="cb7ea-145">Si este aumento es desproporcionado, la aplicación puede alcanzar el límite de recursos (por ejemplo, de CPU o de un servicio que esté usando).</span><span class="sxs-lookup"><span data-stu-id="cb7ea-145">If the rise is disproportionate, your app might be hitting a resource limit such as CPU or the capacity of a service it uses.</span></span>

<span data-ttu-id="cb7ea-146">Haga clic en el icono para obtener los tiempos de direcciones URL concretas.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-146">Click the tile to get times for specific URLs.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a><span data-ttu-id="cb7ea-147">Solicitudes más lentas</span><span class="sxs-lookup"><span data-stu-id="cb7ea-147">Slowest requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

<span data-ttu-id="cb7ea-148">Muestra las solicitudes que pueden precisar un ajuste de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-148">Shows which requests might need performance tuning.</span></span>

### <a name="failed-requests"></a><span data-ttu-id="cb7ea-149">Error en las solicitudes</span><span class="sxs-lookup"><span data-stu-id="cb7ea-149">Failed requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

<span data-ttu-id="cb7ea-150">Un recuento de las solicitudes que inician excepciones no detectadas.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-150">A count of requests that threw uncaught exceptions.</span></span>

<span data-ttu-id="cb7ea-151">Haga clic en el mosaico para ver los detalles de errores específicos y seleccione una solicitud individual para revisarla de forma más exhaustiva.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-151">Click the tile to see the details of specific failures, and select an individual request to see its detail.</span></span> 

<span data-ttu-id="cb7ea-152">Solo se conserva una muestra representativa de los errores para su inspección individual.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-152">Only a representative sample of failures is retained for individual inspection.</span></span>

### <a name="other-metrics"></a><span data-ttu-id="cb7ea-153">Otras métricas</span><span class="sxs-lookup"><span data-stu-id="cb7ea-153">Other metrics</span></span>
<span data-ttu-id="cb7ea-154">Si desea ver las demás métricas que puede mostrar, haga clic en un gráfico y desactive todas las métricas para ver el conjunto completo de opciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-154">To see what other metrics you can display, click a graph, and then deselect all the metrics to see the full available set.</span></span> <span data-ttu-id="cb7ea-155">Haga clic en (i) para ver la definición de cada métrica.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-155">Click (i) to see each metric's definition.</span></span>

![Cancele todas las métricas para ver el conjunto completo](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

<span data-ttu-id="cb7ea-157">Si selecciona una métrica, se deshabilitan las demás, por lo que no pueden aparecer en el mismo gráfico.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-157">Selecting any metric disables the others that can't appear on the same chart.</span></span>

## <a name="set-alerts"></a><span data-ttu-id="cb7ea-158">Establecer alertas</span><span class="sxs-lookup"><span data-stu-id="cb7ea-158">Set alerts</span></span>
<span data-ttu-id="cb7ea-159">Para recibir notificaciones por correo electrónico de los valores no habituales de cualquier métrica, agregue una alerta.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-159">To be notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="cb7ea-160">Puede decidir si se debe enviar un mensaje de correo electrónico a los administradores de cuentas o a direcciones de correo electrónico específicas.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-160">You can choose either to send the email to the account administrators, or to specific email addresses.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

<span data-ttu-id="cb7ea-161">Establezca el recurso antes de las demás propiedades.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-161">Set the resource before the other properties.</span></span> <span data-ttu-id="cb7ea-162">No elija los recursos de la prueba web si desea establecer alertas en las métricas de rendimiento o de uso.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-162">Don't choose the webtest resources if you want to set alerts on performance or usage metrics.</span></span>

<span data-ttu-id="cb7ea-163">Asegúrese de tener en cuenta las unidades en las que se le pide que escriba el valor de umbral.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-163">Be careful to note the units in which you're asked to enter the threshold value.</span></span>

<span data-ttu-id="cb7ea-164">*No puedo ver el botón Agregar alerta*</span><span class="sxs-lookup"><span data-stu-id="cb7ea-164">*I don't see the Add Alert button.*</span></span> <span data-ttu-id="cb7ea-165">: ¿es una cuenta de grupo a la que tiene acceso de solo lectura?</span><span class="sxs-lookup"><span data-stu-id="cb7ea-165">- Is this a group account to which you have read-only access?</span></span> <span data-ttu-id="cb7ea-166">Consulte con el administrador de cuenta.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-166">Check with the account administrator.</span></span>

## <span data-ttu-id="cb7ea-167"><a name="diagnosis"></a>Diagnóstico de problemas</span><span class="sxs-lookup"><span data-stu-id="cb7ea-167"><a name="diagnosis"></a>Diagnosing issues</span></span>
<span data-ttu-id="cb7ea-168">Para buscar y diagnosticar problemas de rendimiento, lea estas sugerencias:</span><span class="sxs-lookup"><span data-stu-id="cb7ea-168">Here are a few tips for finding and diagnosing performance issues:</span></span>

* <span data-ttu-id="cb7ea-169">Configure las [pruebas web][availability] para recibir una alerta si el sitio web deja de funcionar o si no responde correctamente, o lo hace más lentamente de lo habitual.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-169">Set up [web tests][availability] to be alerted if your web site goes down or responds incorrectly or slowly.</span></span> 
* <span data-ttu-id="cb7ea-170">Compare el recuento de Solicitudes con otras métricas para ver si la lentitud de respuesta o los errores se encuentran relacionados con la carga.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-170">Compare the Request count with other metrics to see if failures or slow response are related to load.</span></span>
* <span data-ttu-id="cb7ea-171">[Inserte y busque instrucciones de seguimiento][diagnostic] en el código para facilitar la identificación de los problemas.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-171">[Insert and search trace statements][diagnostic] in your code to help pinpoint problems.</span></span>
* <span data-ttu-id="cb7ea-172">Supervise el funcionamiento de la aplicación web junto con [Live Metrics Stream][livestream].</span><span class="sxs-lookup"><span data-stu-id="cb7ea-172">Monitor your Web app in operation with [Live Metrics Stream][livestream].</span></span>
* <span data-ttu-id="cb7ea-173">Capture el estado de una aplicación .Net con [Snapshot Debugger][snapshot].</span><span class="sxs-lookup"><span data-stu-id="cb7ea-173">Capture the state of your .Net application with [Snapshot Debugger][snapshot].</span></span>

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a><span data-ttu-id="cb7ea-174">Búsqueda y corrección de cuellos de botella de rendimiento con la investigación interactiva del rendimiento</span><span class="sxs-lookup"><span data-stu-id="cb7ea-174">Find and fix performance bottlenecks with an interactive performance investigation</span></span>

<span data-ttu-id="cb7ea-175">Puede usar la nueva función de investigación interactiva del rendimiento de Application Insights para buscar las áreas de cualquier aplicación web que ralentizan el rendimiento general.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-175">You can use the new Application Insights interactive performance investigation to locate areas of your Web app that are slowing down overall performance.</span></span> <span data-ttu-id="cb7ea-176">Puede encontrar rápidamente las páginas concretas que funcionan con mayor lentitud y usar de forma rápida el [herramienta de generación de perfiles](app-insights-profiler.md) para ver si hay alguna correlación entre dichas páginas.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-176">You can quickly find specific pages that are slowing down, and use the [Profiling tool](app-insights-profiler.md) to see if there is a correlation between these pages.</span></span>

### <a name="create-a-list-of-slow-performing-pages"></a><span data-ttu-id="cb7ea-177">Creación de una lista de páginas con un rendimiento lento</span><span class="sxs-lookup"><span data-stu-id="cb7ea-177">Create a list of slow performing pages</span></span> 

<span data-ttu-id="cb7ea-178">El primer paso para encontrar problemas de rendimiento es obtener una lista de las páginas que responden con lentitud.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-178">The first step for finding performance issues is to get a list of the slow responding pages.</span></span> <span data-ttu-id="cb7ea-179">La siguiente captura de pantalla muestra cómo utilizar la hoja Rendimiento para obtener una lista de posibles páginas que hay que investigar con mayor profundidad.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-179">The screen shot below demonstrates using the Performance blade to get a list of potential pages to investigate further.</span></span> <span data-ttu-id="cb7ea-180">Desde esta página se puede ver rápidamente que se ha producido un aumento puntual del tiempo de respuesta de la aplicación aproximadamente a las 6:00 p.m. y de nuevo aproximadamente a las 10:00 p.m.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-180">You can quickly see from this page that there was a slow-down in the response time of the app at approximately 6:00 PM and again at approximately 10 PM.</span></span> <span data-ttu-id="cb7ea-181">También puede ver que la operación GET de cliente o detalles tenía algunas operaciones de larga ejecución con un tiempo de respuesta medio de 507,05 milisegundos.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-181">You can also see that the GET customer/details operation had some long running operations with a median response time of 507.05 milliseconds.</span></span> 

![Rendimiento interactivo de Application Insights](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a><span data-ttu-id="cb7ea-183">Exploración en profundidad de páginas concretas</span><span class="sxs-lookup"><span data-stu-id="cb7ea-183">Drill down on specific pages</span></span>

<span data-ttu-id="cb7ea-184">Una vez que tenga una instantánea del rendimiento de su aplicación, puede obtener más información sobre las operaciones concretas cuyo rendimiento es bajo.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-184">Once you have a snapshot of your app's performance, you can get more details on specific slow-performing operations.</span></span> <span data-ttu-id="cb7ea-185">Haga clic en cualquier operación de la lista para ver los detalles que se muestran a continuación.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-185">Click on any operation in the list to see the details as shown below.</span></span> <span data-ttu-id="cb7ea-186">En el gráfico puede ver si el rendimiento se basaba en una dependencia.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-186">From the chart you can see if the performance was based on a dependency.</span></span> <span data-ttu-id="cb7ea-187">También puede ver el número de usuarios que han tenido los distintos tiempos de respuesta.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-187">You can also see how many users experienced the various response times.</span></span> 

![Hoja de operaciones de Application Insights](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a><span data-ttu-id="cb7ea-189">Exploración en profundidad de un período concreto</span><span class="sxs-lookup"><span data-stu-id="cb7ea-189">Drill down on a specific time period</span></span>

<span data-ttu-id="cb7ea-190">Después de haber identificado el punto específico que se va a investigar, explore en mayor profundidad para examinar las operaciones específicas que pueden haber provocado que la disminución de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-190">After you have identified a point in time to investigate, drill down even further to look at the specific operations that might have caused the performance slow-down.</span></span> <span data-ttu-id="cb7ea-191">Al hacer clic en un punto específico, se obtienen los detalles de la página, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-191">When you click on a specific point in time you get the details of the page as shown below.</span></span> <span data-ttu-id="cb7ea-192">En el ejemplo siguiente se pueden ver las operaciones enumeradas durante un período dado junto con los códigos de respuesta del servidor y la duración de la operación.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-192">In the example below you can see the operations listed for a given time period along with the server response codes and the operation duration.</span></span> <span data-ttu-id="cb7ea-193">También tiene la dirección URL para abrir un elemento de trabajo de TFS si necesita enviar esta información a su equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-193">You also have the url for opening a TFS work item if you need to send this information to your development team.</span></span>

![Porción de tiempo de Application Insights](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a><span data-ttu-id="cb7ea-195">Exploración en profundidad de una operación concreta</span><span class="sxs-lookup"><span data-stu-id="cb7ea-195">Drill down on a specific operation</span></span>

<span data-ttu-id="cb7ea-196">Después de haber identificado el punto específico que se va a investigar, explore en mayor profundidad para examinar las operaciones específicas que pueden haber provocado que la disminución de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-196">After you have identified a point in time to investigate, drill down even further to look at the specific operations that might have caused the performance slow-down.</span></span> <span data-ttu-id="cb7ea-197">Haga clic en cualquier operación de la lista para ver sus detalles como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-197">Click on an operation from the list to see the details of the operation as shown below.</span></span> <span data-ttu-id="cb7ea-198">En este ejemplo puede ver que la operación no se pudo realizar y que Application Insights ha proporcionado los detalles de la excepción que inició la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-198">In this example you can see that the operation failed, and Application Insights has provided the details of the exception the application threw.</span></span> <span data-ttu-id="cb7ea-199">Una vez más, desde esta hoja se puede crear fácilmente un elemento de trabajo de TFS.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-199">Again, you can easily create a TFS work item from this blade.</span></span>

![Hoja de operaciones de Application Insights](./media/app-insights-web-monitor-performance/performance3.png)


## <span data-ttu-id="cb7ea-201"><a name="next"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cb7ea-201"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="cb7ea-202">[Pruebas web][availability]: reciba solicitudes web en su aplicación de forma periódica desde distintos lugares del mundo.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-202">[Web tests][availability] - Have web requests sent to your application at regular intervals from around the world.</span></span>

<span data-ttu-id="cb7ea-203">[Capture y busque seguimientos de diagnóstico][diagnostic]: inserte llamadas de seguimiento y cribe los resultados para identificar los problemas.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-203">[Capture and search diagnostic traces][diagnostic] - Insert trace calls and sift through the results to pinpoint issues.</span></span>

<span data-ttu-id="cb7ea-204">[Seguimiento del uso][usage]: averigüe cuántas personas usan la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cb7ea-204">[Usage tracking][usage] - Find out how people use your application.</span></span>

<span data-ttu-id="cb7ea-205">[Solución de problemas][qna]: con preguntas y respuestas</span><span class="sxs-lookup"><span data-stu-id="cb7ea-205">[Troubleshooting][qna] - and Q & A</span></span>



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



