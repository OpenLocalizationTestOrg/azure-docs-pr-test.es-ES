---
title: "aaaDashboards y navegación en hello Azure Application Insights | Documentos de Microsoft"
description: "Cree vistas de los gráficos APM y consultas principales."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 39b0701b-2fec-4683-842a-8a19424f67bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 58811388205643bb672e0405b3226f12d0f447a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="navigation-and-dashboards-in-hello-application-insights-portal"></a><span data-ttu-id="9eb88-103">Navegación y paneles en el portal de Application Insights Hola</span><span class="sxs-lookup"><span data-stu-id="9eb88-103">Navigation and Dashboards in hello Application Insights portal</span></span>
<span data-ttu-id="9eb88-104">Una vez haya [configurar Application Insights en el proyecto](app-insights-overview.md), los datos de telemetría acerca del rendimiento y el uso de la aplicación aparecerá en el recurso del proyecto Application Insights en hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9eb88-104">After you have [set up Application Insights on your project](app-insights-overview.md), telemetry data about your app's performance and usage will appear in your project's Application Insights resource in hello [Azure portal](https://portal.azure.com).</span></span>

## <a name="find-your-telemetry"></a><span data-ttu-id="9eb88-105">Encontrar la telemetría</span><span class="sxs-lookup"><span data-stu-id="9eb88-105">Find your telemetry</span></span>
<span data-ttu-id="9eb88-106">Inicie sesión en toohello [portal de Azure](https://portal.azure.com) y navegar por los recursos de Application Insights toohello que creó para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9eb88-106">Sign in toohello [Azure portal](https://portal.azure.com) and navigate toohello Application Insights resource that you created for your app.</span></span>

![Haga clic en Examinar, seleccione Application Insights y, después, seleccione su aplicación.](./media/app-insights-dashboards/00-start.png)

<span data-ttu-id="9eb88-108">hoja de información general de Hello (página) para la aplicación muestra un resumen de hello diagnóstico las métricas clave de la aplicación y es una puerta de enlace toohello otras características del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="9eb88-108">hello overview blade (page) for your app shows a summary of hello key diagnostic metrics of your app, and is a gateway toohello other features of hello portal.</span></span>

![Las principales rutas tooview la telemetría](./media/app-insights-dashboards/010-oview.png)

<span data-ttu-id="9eb88-110">Puede personalizar cualquiera de las cuadrículas y gráficos de Hola y anclarlos tooa panel.</span><span class="sxs-lookup"><span data-stu-id="9eb88-110">You can customize any of hello charts and grids and pin them tooa dashboard.</span></span> <span data-ttu-id="9eb88-111">De este modo, se puede reunir telemetría clave Hola de diferentes aplicaciones en el panel central.</span><span class="sxs-lookup"><span data-stu-id="9eb88-111">That way, you can bring together hello key telemetry from different apps on a central dashboard.</span></span>

## <a name="dashboards"></a><span data-ttu-id="9eb88-112">Paneles</span><span class="sxs-lookup"><span data-stu-id="9eb88-112">Dashboards</span></span>
<span data-ttu-id="9eb88-113">Hello lo primero que verá después de iniciar sesión en toohello [portal de Microsoft Azure](https://portal.azure.com) es un panel.</span><span class="sxs-lookup"><span data-stu-id="9eb88-113">hello first thing you see after you sign in toohello [Microsoft Azure portal](https://portal.azure.com) is a dashboard.</span></span> <span data-ttu-id="9eb88-114">A continuación, se pueden reunir los gráficos de Hola que son más importante tooyou en todos los recursos de Azure, incluida la telemetría de [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9eb88-114">Here you can bring together hello charts that are most important tooyou across all your Azure resources, including telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

![Panel personalizado.](./media/app-insights-dashboards/31.png)

1. <span data-ttu-id="9eb88-116">**Navegar por los recursos toospecific** como la aplicación en Application Insights: barra izquierda Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="9eb88-116">**Navigate toospecific resources** such as your app in Application Insights: Use hello left bar.</span></span>
2. <span data-ttu-id="9eb88-117">**Panel actual devuelto toohello**, o cambia las vistas reciente tooother: uso Hola menú desplegable situado en la esquina superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="9eb88-117">**Return toohello current dashboard**, or switch tooother recent views: Use hello drop-down menu at top left.</span></span>
3. <span data-ttu-id="9eb88-118">**Cambiar paneles**: Use Hola menú desplegable situado en el título del panel de Hola</span><span class="sxs-lookup"><span data-stu-id="9eb88-118">**Switch dashboards**: Use hello drop-down menu on hello dashboard title</span></span>
4. <span data-ttu-id="9eb88-119">**Crear, editar y compartir paneles** en la barra de herramientas del panel Hola.</span><span class="sxs-lookup"><span data-stu-id="9eb88-119">**Create, edit, and share dashboards** in hello dashboard toolbar.</span></span>
5. <span data-ttu-id="9eb88-120">**Modificar el panel de Hola**: mantenga el mouse sobre un icono y, a continuación, utilizar su top barra toomove, personalizar o quitarlo.</span><span class="sxs-lookup"><span data-stu-id="9eb88-120">**Edit hello dashboard**: Hover over a tile and then use its top bar toomove, customize, or remove it.</span></span>

## <a name="add-tooa-dashboard"></a><span data-ttu-id="9eb88-121">Agregar panel tooa</span><span class="sxs-lookup"><span data-stu-id="9eb88-121">Add tooa dashboard</span></span>
<span data-ttu-id="9eb88-122">Cuando se ve una hoja o un conjunto de gráficos que es especialmente interesante, puede anclar una copia del mismo panel toohello.</span><span class="sxs-lookup"><span data-stu-id="9eb88-122">When you're looking at a blade or set of charts that's particularly interesting, you can pin a copy of it toohello dashboard.</span></span> <span data-ttu-id="9eb88-123">Lo verá la próxima vez que regrese.</span><span class="sxs-lookup"><span data-stu-id="9eb88-123">You'll see it next time you return there.</span></span>

![toopin un gráfico, mantenga el mouse sobre él y, a continuación, haga clic en "..." en el encabezado de Hola.](./media/app-insights-dashboards/33.png)

1. <span data-ttu-id="9eb88-125">Anclar toodashboard de gráfico.</span><span class="sxs-lookup"><span data-stu-id="9eb88-125">Pin chart toodashboard.</span></span> <span data-ttu-id="9eb88-126">Aparece una copia del gráfico de hello en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="9eb88-126">A copy of hello chart appears on hello dashboard.</span></span>
2. <span data-ttu-id="9eb88-127">Panel de PIN Hola hoja todo toohello - aparece en panel Hola como un icono que puede hacer clic en.</span><span class="sxs-lookup"><span data-stu-id="9eb88-127">Pin hello whole blade toohello dashboard - it appears on hello dashboard as a tile that you can click through.</span></span>
3. <span data-ttu-id="9eb88-128">Haga clic en hello esquina superior izquierda tooreturn toohello del panel actual.</span><span class="sxs-lookup"><span data-stu-id="9eb88-128">Click hello top left corner tooreturn toohello current dashboard.</span></span> <span data-ttu-id="9eb88-129">A continuación, puede usar Hola menú desplegable tooreturn toohello la vista actual.</span><span class="sxs-lookup"><span data-stu-id="9eb88-129">Then you can use hello drop-down menu tooreturn toohello current view.</span></span>

<span data-ttu-id="9eb88-130">Observe que los gráficos se agrupan en iconos: un icono puede contener más de un gráfico.</span><span class="sxs-lookup"><span data-stu-id="9eb88-130">Notice that charts are grouped into tiles: a tile can contain more than one chart.</span></span> <span data-ttu-id="9eb88-131">Anclar Hola todo icono toohello o panel.</span><span class="sxs-lookup"><span data-stu-id="9eb88-131">You pin hello whole tile toohello dashboard.</span></span>

<span data-ttu-id="9eb88-132">gráfico de Hola se actualiza automáticamente con una frecuencia que depende de intervalo de tiempo del gráfico de hello:</span><span class="sxs-lookup"><span data-stu-id="9eb88-132">hello chart is automatically refreshed with a frequency that depends on hello chart's time range:</span></span>

* <span data-ttu-id="9eb88-133">Tiempo de intervalo de hora too1: actualizar cada 5 minutos</span><span class="sxs-lookup"><span data-stu-id="9eb88-133">Time range up too1 hour: Refresh every 5 minutes</span></span>
* <span data-ttu-id="9eb88-134">Intervalo de tiempo de 1 a 24 horas: actualizar cada 15 minutos</span><span class="sxs-lookup"><span data-stu-id="9eb88-134">Time range 1 - 24 hours: Refresh every 15 minutes</span></span>
* <span data-ttu-id="9eb88-135">Tiempo de intervalo superior a 24 horas: (intervalo de tiempo)/60.</span><span class="sxs-lookup"><span data-stu-id="9eb88-135">Time range above 24 hours: (Time range)/60.</span></span>

### <a name="pin-any-query-in-analytics"></a><span data-ttu-id="9eb88-136">Ancle cualquier consulta en Analytics</span><span class="sxs-lookup"><span data-stu-id="9eb88-136">Pin any query in Analytics</span></span>
<span data-ttu-id="9eb88-137">También puede [anclar análisis](app-insights-analytics-using.md#pin-to-dashboard) gráficos tooa [compartido](#share-dashboards-with-your-team) panel.</span><span class="sxs-lookup"><span data-stu-id="9eb88-137">You can also [pin Analytics](app-insights-analytics-using.md#pin-to-dashboard) charts tooa [shared](#share-dashboards-with-your-team) dashboard.</span></span> <span data-ttu-id="9eb88-138">Esto le permite tooadd gráficos de cualquier consulta arbitraria junto con las métricas estándar de Hola.</span><span class="sxs-lookup"><span data-stu-id="9eb88-138">This allows you tooadd charts of any arbitrary query alongside hello standard metrics.</span></span> 

<span data-ttu-id="9eb88-139">Los resultados se recalculan automáticamente cada hora.</span><span class="sxs-lookup"><span data-stu-id="9eb88-139">Results are automatically recalculated every hour.</span></span> <span data-ttu-id="9eb88-140">Haga clic en icono de actualización de hello en hello gráfico toorecalculate inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="9eb88-140">Click hello Refresh icon on hello chart toorecalculate immediately.</span></span> <span data-ttu-id="9eb88-141">(Cuando el explorador se actualiza, no se recalculan los resultados).</span><span class="sxs-lookup"><span data-stu-id="9eb88-141">(Browser refresh doesn't recalculate.)</span></span>

## <a name="adjust-a-tile-on-hello-dashboard"></a><span data-ttu-id="9eb88-142">Ajustar un icono en el panel de Hola</span><span class="sxs-lookup"><span data-stu-id="9eb88-142">Adjust a tile on hello dashboard</span></span>
<span data-ttu-id="9eb88-143">Una vez un icono en el panel de hello, ajústela.</span><span class="sxs-lookup"><span data-stu-id="9eb88-143">Once a tile is on hello dashboard, you can adjust it.</span></span>

![Mantenga el mouse sobre un gráfico en orden tooedit.](./media/app-insights-dashboards/36.png)

1. <span data-ttu-id="9eb88-145">Agregar un icono de toohello gráfico.</span><span class="sxs-lookup"><span data-stu-id="9eb88-145">Add a chart toohello tile.</span></span>
2. <span data-ttu-id="9eb88-146">Establecer la métrica de hello, agrupar por dimensión y el estilo (tabla, gráfico) de un gráfico.</span><span class="sxs-lookup"><span data-stu-id="9eb88-146">Set hello metric, group-by dimension and style (table, graph) of a chart.</span></span>
3. <span data-ttu-id="9eb88-147">Arrastre Hola diagrama toozoom Haga clic en hello deshacer botón tooreset Hola timespan; establecer propiedades del filtro de gráficos de hello en mosaico Hola.</span><span class="sxs-lookup"><span data-stu-id="9eb88-147">Drag across hello diagram toozoom in; click hello undo button tooreset hello timespan; set filter properties for hello charts on hello tile.</span></span>
4. <span data-ttu-id="9eb88-148">Establezca el título del icono.</span><span class="sxs-lookup"><span data-stu-id="9eb88-148">Set tile title.</span></span>

<span data-ttu-id="9eb88-149">Los iconos anclados desde hojas del explorador de métricas tienen más opciones de edición que los iconos anclados desde una hoja de información general.</span><span class="sxs-lookup"><span data-stu-id="9eb88-149">Tiles pinned from metric explorer blades have more editing options than tiles pinned from an Overview blade.</span></span>

<span data-ttu-id="9eb88-150">icono original de Hola que haya anclado no se ve afectado por los cambios.</span><span class="sxs-lookup"><span data-stu-id="9eb88-150">hello original tile that you pinned isn't affected by your edits.</span></span>

## <a name="switch-between-dashboards"></a><span data-ttu-id="9eb88-151">Cambio entre paneles</span><span class="sxs-lookup"><span data-stu-id="9eb88-151">Switch between dashboards</span></span>
<span data-ttu-id="9eb88-152">Puede guardar más de un panel y cambiar de uno a otro.</span><span class="sxs-lookup"><span data-stu-id="9eb88-152">You can save more than one dashboard and switch between them.</span></span> <span data-ttu-id="9eb88-153">Al anclar un gráfico o la hoja, estas se agregan toohello del panel actual.</span><span class="sxs-lookup"><span data-stu-id="9eb88-153">When you pin a chart or blade, they're added toohello current dashboard.</span></span>

![tooswitch entre paneles, haga clic en el panel y seleccione un panel guardado.](./media/app-insights-dashboards/32.png)

<span data-ttu-id="9eb88-157">Por ejemplo, podría tener un panel para mostrar la pantalla completa en la sala de reuniones de hello y otro para el desarrollo general.</span><span class="sxs-lookup"><span data-stu-id="9eb88-157">For example, you might have one dashboard for displaying full screen in hello team room, and another for general development.</span></span>

<span data-ttu-id="9eb88-158">En el panel de hello, una hoja aparece como un icono: haga clic en él toogo toohello hoja.</span><span class="sxs-lookup"><span data-stu-id="9eb88-158">On hello dashboard, a blade appears as a tile: click it toogo toohello blade.</span></span> <span data-ttu-id="9eb88-159">Un gráfico de replica gráfico hello en su ubicación original.</span><span class="sxs-lookup"><span data-stu-id="9eb88-159">A chart replicates hello chart in its original location.</span></span>

![Haga clic en una hoja de hello tooopen de icono que representa](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a><span data-ttu-id="9eb88-161">Uso compartido de paneles</span><span class="sxs-lookup"><span data-stu-id="9eb88-161">Share dashboards</span></span>
<span data-ttu-id="9eb88-162">Cuando haya creado un panel, puede compartirlo con otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="9eb88-162">When you've created a dashboard, you can share it with other users.</span></span>

![En el encabezado del panel hello, haga clic en recurso compartido](./media/app-insights-dashboards/41.png)

<span data-ttu-id="9eb88-164">Aprenda más acerca de [Roles y control de acceso](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="9eb88-164">Learn about [Roles and access control](app-insights-resources-roles-access-control.md).</span></span>

## <a name="app-navigation"></a><span data-ttu-id="9eb88-165">Navegación en la aplicación</span><span class="sxs-lookup"><span data-stu-id="9eb88-165">App navigation</span></span>
<span data-ttu-id="9eb88-166">hoja de información general de Hello es la información de toomore de puerta de enlace de hello de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9eb88-166">hello overview blade is hello gateway toomore information about your app.</span></span>

* <span data-ttu-id="9eb88-167">**Cualquier icono o gráfico** : haga clic en cualquier icono o gráfico toosee información más detallada sobre lo que muestra.</span><span class="sxs-lookup"><span data-stu-id="9eb88-167">**Any chart or tile** - Click any tile or chart toosee more detail about what it displays.</span></span>

### <a name="overview-blade-buttons"></a><span data-ttu-id="9eb88-168">Botones de la hoja de información general</span><span class="sxs-lookup"><span data-stu-id="9eb88-168">Overview blade buttons</span></span>
![Barra de navegación superior de hoja de información general](./media/app-insights-dashboards/app-overview-top-nav.png)

* <span data-ttu-id="9eb88-170">[**Explorador de métricas**](app-insights-metrics-explorer.md): cree sus propios gráficos de rendimiento y uso.</span><span class="sxs-lookup"><span data-stu-id="9eb88-170">[**Metrics Explorer**](app-insights-metrics-explorer.md) - Create your own charts of performance and usage.</span></span>
* <span data-ttu-id="9eb88-171">[**Búsqueda**](app-insights-diagnostic-search.md): investigue casos específicos de eventos como solicitudes, excepciones o seguimientos de registro.</span><span class="sxs-lookup"><span data-stu-id="9eb88-171">[**Search**](app-insights-diagnostic-search.md) - Investigate specific instances of events such as requests, exceptions, or log traces.</span></span>
* <span data-ttu-id="9eb88-172">[**Analytics**](app-insights-analytics.md): consultas eficaces sobre los datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="9eb88-172">[**Analytics**](app-insights-analytics.md) - Powerful queries over your telemetry.</span></span>
* <span data-ttu-id="9eb88-173">**El intervalo de tiempo** -ajustar el intervalo de hello muestra todos los gráficos de hello en hoja Hola.</span><span class="sxs-lookup"><span data-stu-id="9eb88-173">**Time range** - Adjust hello range displayed by all hello charts on hello blade.</span></span>
* <span data-ttu-id="9eb88-174">**Eliminar** -eliminar el recurso de Application Insights de Hola para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="9eb88-174">**Delete** - Delete hello Application Insights resource for this app.</span></span> <span data-ttu-id="9eb88-175">Debe también quitar paquetes de Application Insights Hola de código de la aplicación, o editar hello [clave de instrumentación](app-insights-create-new-resource.md#copy-the-instrumentation-key) en su aplicación toodirect telemetría tooa otro recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9eb88-175">You should also either remove hello Application Insights packages from your app code, or edit hello [instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) in your app toodirect telemetry tooa different Application Insights resource.</span></span>

### <a name="essentials-tab"></a><span data-ttu-id="9eb88-176">Pestaña Essentials</span><span class="sxs-lookup"><span data-stu-id="9eb88-176">Essentials tab</span></span>
* <span data-ttu-id="9eb88-177">[Clave de instrumentación](app-insights-create-new-resource.md#copy-the-instrumentation-key): identifica este recurso de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9eb88-177">[Instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) - Identifies this app resource.</span></span>
* <span data-ttu-id="9eb88-178">Precios: hacen que las características estén disponibles y establecen límites de volumen.</span><span class="sxs-lookup"><span data-stu-id="9eb88-178">Pricing - Make features available and set volume caps.</span></span>

### <a name="app-navigation-bar"></a><span data-ttu-id="9eb88-179">Barra de navegación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="9eb88-179">App navigation bar</span></span>
![Barra de navegación izquierda](./media/app-insights-dashboards/app-left-nav-bar.png)

* <span data-ttu-id="9eb88-181">**Información general sobre** -hoja de información general sobre la aplicación toohello devuelto.</span><span class="sxs-lookup"><span data-stu-id="9eb88-181">**Overview** - Return toohello app overview blade.</span></span>
* <span data-ttu-id="9eb88-182">**Registro de actividad**: alertas y eventos administrativos de Azure.</span><span class="sxs-lookup"><span data-stu-id="9eb88-182">**Activity log** - Alerts and Azure administrative events.</span></span>
* <span data-ttu-id="9eb88-183">[**Control de acceso** ](app-insights-resources-roles-access-control.md) -proporcionar acceso a los miembros de tooteam y otros.</span><span class="sxs-lookup"><span data-stu-id="9eb88-183">[**Access control**](app-insights-resources-roles-access-control.md) - Provide access tooteam members and others.</span></span>
* <span data-ttu-id="9eb88-184">[**Etiquetas** ](../azure-resource-manager/resource-group-using-tags.md) -Use etiquetas toogroup la aplicación con otras personas.</span><span class="sxs-lookup"><span data-stu-id="9eb88-184">[**Tags**](../azure-resource-manager/resource-group-using-tags.md) - Use tags toogroup your app with others.</span></span>

<span data-ttu-id="9eb88-185">INVESTIGAR</span><span class="sxs-lookup"><span data-stu-id="9eb88-185">INVESTIGATE</span></span>

* <span data-ttu-id="9eb88-186">[**Asignación de la aplicación** ](app-insights-app-map.md) -Active mapa que muestra los componentes de saludo de la aplicación, se deriva de la información de dependencia de Hola.</span><span class="sxs-lookup"><span data-stu-id="9eb88-186">[**Application map**](app-insights-app-map.md) - Active map showing hello components of your application, derived from hello dependency information.</span></span>
* <span data-ttu-id="9eb88-187">[**Detección inteligente**](app-insights-proactive-diagnostics.md): revise las alertas recientes de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="9eb88-187">[**Smart Detection**](app-insights-proactive-diagnostics.md) - Review recent performance alerts.</span></span>
* <span data-ttu-id="9eb88-188">[**Stream en vivo**](app-insights-live-stream.md): un conjunto fijo de métricas casi instantáneas, útiles al implementar una nueva compilación o depurar.</span><span class="sxs-lookup"><span data-stu-id="9eb88-188">[**Live Stream**](app-insights-live-stream.md) - A fixed set of near-instant metrics, useful when deploying a new build or debugging.</span></span>
* <span data-ttu-id="9eb88-189">[**Disponibilidad / Web pruebas** ](app-insights-monitor-web-app-availability.md) -envío solicitudes regular tooyour aplicación web de alrededor de hello world.*</span><span class="sxs-lookup"><span data-stu-id="9eb88-189">[**Availability / Web tests**](app-insights-monitor-web-app-availability.md) - Send regular requests tooyour web app from around hello world.*</span></span>
* <span data-ttu-id="9eb88-190">[**Errores y rendimiento** ](app-insights-web-monitor-performance.md) -excepciones, las tasas de errores y respuesta el tiempo de espera para las solicitudes tooyour aplicación y para las solicitudes de la aplicación demasiado[dependencias](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="9eb88-190">[**Failures, Performance**](app-insights-web-monitor-performance.md) - Exceptions, failure rates and response times for requests tooyour app and for requests from your app too[dependencies](app-insights-asp-net-dependencies.md).</span></span>
* <span data-ttu-id="9eb88-191">[**Rendimiento**](app-insights-web-monitor-performance.md): tiempo de respuesta, tiempos de respuesta de dependencia.</span><span class="sxs-lookup"><span data-stu-id="9eb88-191">[**Performance**](app-insights-web-monitor-performance.md) - Response time, dependency response times.</span></span>
* <span data-ttu-id="9eb88-192">[Servidores](app-insights-web-monitor-performance.md) : contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="9eb88-192">[Servers](app-insights-web-monitor-performance.md) - Performance counters.</span></span> <span data-ttu-id="9eb88-193">Está disponible si se [instala el Monitor de estado](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="9eb88-193">Available if you [install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="9eb88-194">**Explorador** : vista de página y rendimiento de AJAX.</span><span class="sxs-lookup"><span data-stu-id="9eb88-194">**Browser** - Page view and AJAX performance.</span></span> <span data-ttu-id="9eb88-195">Está disponible si se [instrumentan las páginas web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="9eb88-195">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>
* <span data-ttu-id="9eb88-196">**Uso** : vista de página, recuentos de usuarios y sesiones.</span><span class="sxs-lookup"><span data-stu-id="9eb88-196">**Usage** - Page view, user, and session counts.</span></span> <span data-ttu-id="9eb88-197">Está disponible si se [instrumentan las páginas web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="9eb88-197">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>

<span data-ttu-id="9eb88-198">CONFIGURAR</span><span class="sxs-lookup"><span data-stu-id="9eb88-198">CONFIGURE</span></span>

* <span data-ttu-id="9eb88-199">**Introducción** : tutorial en línea.</span><span class="sxs-lookup"><span data-stu-id="9eb88-199">**Getting started** - inline tutorial.</span></span>
* <span data-ttu-id="9eb88-200">**Propiedades** : clave de instrumentación, suscripción e identificador de recursos.</span><span class="sxs-lookup"><span data-stu-id="9eb88-200">**Properties** - instrumentation key, subscription and resource id.</span></span>
* <span data-ttu-id="9eb88-201">[Alertas](app-insights-alerts.md) : configuración de alertas de métricas.</span><span class="sxs-lookup"><span data-stu-id="9eb88-201">[Alerts](app-insights-alerts.md) - metric alert configuration.</span></span>
* <span data-ttu-id="9eb88-202">[Exportación continua](app-insights-export-telemetry.md) -configurar la exportación de almacenamiento de información de telemetría tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9eb88-202">[Continuous export](app-insights-export-telemetry.md) - configure export of telemetry tooAzure storage.</span></span>
* <span data-ttu-id="9eb88-203">[Pruebas de rendimiento](app-insights-monitor-web-app-availability.md#performance-tests) : configuración de una carga simétrica en el sitio web.</span><span class="sxs-lookup"><span data-stu-id="9eb88-203">[Performance testing](app-insights-monitor-web-app-availability.md#performance-tests) - set up a synthetic load on your website.</span></span>
* <span data-ttu-id="9eb88-204">[Cuotas y precios](app-insights-pricing.md) y [muestreo de ingesta](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="9eb88-204">[Quota and pricing](app-insights-pricing.md) and [ingestion sampling](app-insights-sampling.md).</span></span>
* <span data-ttu-id="9eb88-205">**El acceso de API** -crear [anotaciones de la versión](app-insights-annotations.md) y para hello API de acceso a datos.</span><span class="sxs-lookup"><span data-stu-id="9eb88-205">**API Access** - Create [release annotations](app-insights-annotations.md) and for hello Data Access API.</span></span>
* <span data-ttu-id="9eb88-206">[**Los elementos de trabajo** ](app-insights-diagnostic-search.md#create-work-item) -conectarse al sistema de seguimiento para que pueda crear errores al inspeccionar la telemetría de trabajo de tooa.</span><span class="sxs-lookup"><span data-stu-id="9eb88-206">[**Work Items**](app-insights-diagnostic-search.md#create-work-item) - Connect tooa work tracking system so that you can create bugs while inspecting telemetry.</span></span>

<span data-ttu-id="9eb88-207">CONFIGURACIÓN</span><span class="sxs-lookup"><span data-stu-id="9eb88-207">SETTINGS</span></span>

* <span data-ttu-id="9eb88-208">[**Bloqueos**](../azure-resource-manager/resource-group-lock-resources.md): bloquee recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="9eb88-208">[**Locks**](../azure-resource-manager/resource-group-lock-resources.md) - lock Azure resources</span></span>
* <span data-ttu-id="9eb88-209">[**Script de automatización** ](app-insights-powershell.md) -exportar una definición de hello recursos de Azure para que se puede usar como un toocreate nuevos recursos de plantilla.</span><span class="sxs-lookup"><span data-stu-id="9eb88-209">[**Automation script**](app-insights-powershell.md) - export a definition of hello Azure resource so that you can use it as a template toocreate new resources.</span></span>


## <a name="video"></a><span data-ttu-id="9eb88-210">Vídeo</span><span class="sxs-lookup"><span data-stu-id="9eb88-210">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="9eb88-211">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9eb88-211">Next steps</span></span>

|  |  |
| --- | --- |
| [<span data-ttu-id="9eb88-212">Explorador de métricas</span><span class="sxs-lookup"><span data-stu-id="9eb88-212">Metrics explorer</span></span>](app-insights-metrics-explorer.md)<br/><span data-ttu-id="9eb88-213">Filtre y segmente las métricas</span><span class="sxs-lookup"><span data-stu-id="9eb88-213">Filter and segment metrics</span></span> |![Ejemplo de búsqueda](./media/app-insights-dashboards/64.png) |
| [<span data-ttu-id="9eb88-215">Búsqueda de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="9eb88-215">Diagnostic search</span></span>](app-insights-diagnostic-search.md)<br/><span data-ttu-id="9eb88-216">Busque y examine eventos y eventos relacionados, y cree errores.</span><span class="sxs-lookup"><span data-stu-id="9eb88-216">Find and inspect events, related events, and create bugs</span></span> |![Ejemplo de búsqueda](./media/app-insights-dashboards/61.png) |
| [<span data-ttu-id="9eb88-218">Analytics</span><span class="sxs-lookup"><span data-stu-id="9eb88-218">Analytics</span></span>](app-insights-analytics.md)<br/><span data-ttu-id="9eb88-219">Lenguaje de consulta eficaz</span><span class="sxs-lookup"><span data-stu-id="9eb88-219">Powerful query language</span></span> |![Ejemplo de búsqueda](./media/app-insights-dashboards/63.png) |
