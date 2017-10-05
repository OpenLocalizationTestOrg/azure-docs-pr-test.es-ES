---
title: "Paneles y navegación en Azure Application Insights | Microsoft Docs"
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
ms.openlocfilehash: 9987f04e7e71df5fe10c8bc209a390cb940ec4f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="navigation-and-dashboards-in-the-application-insights-portal"></a><span data-ttu-id="3b570-103">Navegación y paneles en el portal de Application Insights</span><span class="sxs-lookup"><span data-stu-id="3b570-103">Navigation and Dashboards in the Application Insights portal</span></span>
<span data-ttu-id="3b570-104">Una vez [configurado Application Insights en su proyecto](app-insights-overview.md), aparecerán los datos de telemetría acerca del rendimiento y el uso de la aplicación en el recurso del proyecto Application Insights en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3b570-104">After you have [set up Application Insights on your project](app-insights-overview.md), telemetry data about your app's performance and usage will appear in your project's Application Insights resource in the [Azure portal](https://portal.azure.com).</span></span>

## <a name="find-your-telemetry"></a><span data-ttu-id="3b570-105">Encontrar la telemetría</span><span class="sxs-lookup"><span data-stu-id="3b570-105">Find your telemetry</span></span>
<span data-ttu-id="3b570-106">Inicie sesión en [Azure Portal](https://portal.azure.com), vaya al recurso de Application Insights que ha creado para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3b570-106">Sign in to the [Azure portal](https://portal.azure.com) and navigate to the Application Insights resource that you created for your app.</span></span>

![Haga clic en Examinar, seleccione Application Insights y, después, seleccione su aplicación.](./media/app-insights-dashboards/00-start.png)

<span data-ttu-id="3b570-108">La hoja de información general (página) de la aplicación muestra un resumen de las métricas de diagnóstico clave de la aplicación y sirve de puerta de enlace a las demás características del portal.</span><span class="sxs-lookup"><span data-stu-id="3b570-108">The overview blade (page) for your app shows a summary of the key diagnostic metrics of your app, and is a gateway to the other features of the portal.</span></span>

![Rutas principales para ver los datos de telemetría](./media/app-insights-dashboards/010-oview.png)

<span data-ttu-id="3b570-110">Puede personalizar cualquiera de los gráficos y cuadrículas y anclarlos a un panel.</span><span class="sxs-lookup"><span data-stu-id="3b570-110">You can customize any of the charts and grids and pin them to a dashboard.</span></span> <span data-ttu-id="3b570-111">De este modo, se puede reunir la telemetría clave de aplicaciones diferentes en un panel central.</span><span class="sxs-lookup"><span data-stu-id="3b570-111">That way, you can bring together the key telemetry from different apps on a central dashboard.</span></span>

## <a name="dashboards"></a><span data-ttu-id="3b570-112">Paneles</span><span class="sxs-lookup"><span data-stu-id="3b570-112">Dashboards</span></span>
<span data-ttu-id="3b570-113">Lo primero que verá después de iniciar sesión en el [Portal de Microsoft Azure](https://portal.azure.com) es un panel.</span><span class="sxs-lookup"><span data-stu-id="3b570-113">The first thing you see after you sign in to the [Microsoft Azure portal](https://portal.azure.com) is a dashboard.</span></span> <span data-ttu-id="3b570-114">Aquí puede agrupar los gráficos que le resultan más importantes de todos los recursos de Azure, incluidos los datos de telemetría desde [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3b570-114">Here you can bring together the charts that are most important to you across all your Azure resources, including telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

![Panel personalizado.](./media/app-insights-dashboards/31.png)

1. <span data-ttu-id="3b570-116">**Vaya a los recursos específicos** como la aplicación en Application Insights: utilice la barra de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="3b570-116">**Navigate to specific resources** such as your app in Application Insights: Use the left bar.</span></span>
2. <span data-ttu-id="3b570-117">**Vuelva al panel actual** o cambie a otras vistas recientes: use el menú desplegable situado en la parte superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="3b570-117">**Return to the current dashboard**, or switch to other recent views: Use the drop-down menu at top left.</span></span>
3. <span data-ttu-id="3b570-118">**Cambie entre los paneles**: use el menú desplegable en el título del panel</span><span class="sxs-lookup"><span data-stu-id="3b570-118">**Switch dashboards**: Use the drop-down menu on the dashboard title</span></span>
4. <span data-ttu-id="3b570-119">**Cree, edite y comparta paneles** con la barra de herramientas del panel.</span><span class="sxs-lookup"><span data-stu-id="3b570-119">**Create, edit, and share dashboards** in the dashboard toolbar.</span></span>
5. <span data-ttu-id="3b570-120">**Edite el panel**: mantenga el puntero sobre un icono y, a continuación, utilice la barra superior para moverlo, personalizarlo o quitarlo.</span><span class="sxs-lookup"><span data-stu-id="3b570-120">**Edit the dashboard**: Hover over a tile and then use its top bar to move, customize, or remove it.</span></span>

## <a name="add-to-a-dashboard"></a><span data-ttu-id="3b570-121">Adición a un panel</span><span class="sxs-lookup"><span data-stu-id="3b570-121">Add to a dashboard</span></span>
<span data-ttu-id="3b570-122">Cuando esté consultando una hoja o un conjunto de gráficos especialmente interesante, puede anclar una copia al panel.</span><span class="sxs-lookup"><span data-stu-id="3b570-122">When you're looking at a blade or set of charts that's particularly interesting, you can pin a copy of it to the dashboard.</span></span> <span data-ttu-id="3b570-123">Lo verá la próxima vez que regrese.</span><span class="sxs-lookup"><span data-stu-id="3b570-123">You'll see it next time you return there.</span></span>

![Para anclar un gráfico, mantenga el puntero encima y haga clic en "..." en el encabezado.](./media/app-insights-dashboards/33.png)

1. <span data-ttu-id="3b570-125">Ancle un gráfico al panel.</span><span class="sxs-lookup"><span data-stu-id="3b570-125">Pin chart to dashboard.</span></span> <span data-ttu-id="3b570-126">Una copia del gráfico aparece en el panel.</span><span class="sxs-lookup"><span data-stu-id="3b570-126">A copy of the chart appears on the dashboard.</span></span>
2. <span data-ttu-id="3b570-127">Ancle la hoja completa en el panel: aparecerá en el panel como un icono en el que puede hacer clic.</span><span class="sxs-lookup"><span data-stu-id="3b570-127">Pin the whole blade to the dashboard - it appears on the dashboard as a tile that you can click through.</span></span>
3. <span data-ttu-id="3b570-128">Haga clic en la esquina superior izquierda para volver al panel actual.</span><span class="sxs-lookup"><span data-stu-id="3b570-128">Click the top left corner to return to the current dashboard.</span></span> <span data-ttu-id="3b570-129">A continuación, puede utilizar el menú desplegable para volver a la vista actual.</span><span class="sxs-lookup"><span data-stu-id="3b570-129">Then you can use the drop-down menu to return to the current view.</span></span>

<span data-ttu-id="3b570-130">Observe que los gráficos se agrupan en iconos: un icono puede contener más de un gráfico.</span><span class="sxs-lookup"><span data-stu-id="3b570-130">Notice that charts are grouped into tiles: a tile can contain more than one chart.</span></span> <span data-ttu-id="3b570-131">El icono se ancla entero al panel.</span><span class="sxs-lookup"><span data-stu-id="3b570-131">You pin the whole tile to the dashboard.</span></span>

<span data-ttu-id="3b570-132">El gráfico se actualiza automáticamente con una frecuencia que depende del intervalo de tiempo del gráfico:</span><span class="sxs-lookup"><span data-stu-id="3b570-132">The chart is automatically refreshed with a frequency that depends on the chart's time range:</span></span>

* <span data-ttu-id="3b570-133">Intervalo de tiempo hasta una hora: actualizar cada 5 minutos</span><span class="sxs-lookup"><span data-stu-id="3b570-133">Time range up to 1 hour: Refresh every 5 minutes</span></span>
* <span data-ttu-id="3b570-134">Intervalo de tiempo de 1 a 24 horas: actualizar cada 15 minutos</span><span class="sxs-lookup"><span data-stu-id="3b570-134">Time range 1 - 24 hours: Refresh every 15 minutes</span></span>
* <span data-ttu-id="3b570-135">Tiempo de intervalo superior a 24 horas: (intervalo de tiempo)/60.</span><span class="sxs-lookup"><span data-stu-id="3b570-135">Time range above 24 hours: (Time range)/60.</span></span>

### <a name="pin-any-query-in-analytics"></a><span data-ttu-id="3b570-136">Ancle cualquier consulta en Analytics</span><span class="sxs-lookup"><span data-stu-id="3b570-136">Pin any query in Analytics</span></span>
<span data-ttu-id="3b570-137">También puede [anclar gráficos de Analytics](app-insights-analytics-using.md#pin-to-dashboard) a un panel [compartido](#share-dashboards-with-your-team).</span><span class="sxs-lookup"><span data-stu-id="3b570-137">You can also [pin Analytics](app-insights-analytics-using.md#pin-to-dashboard) charts to a [shared](#share-dashboards-with-your-team) dashboard.</span></span> <span data-ttu-id="3b570-138">Esto permite agregar gráficos de cualquier consulta arbitraria junto con las métricas estándares.</span><span class="sxs-lookup"><span data-stu-id="3b570-138">This allows you to add charts of any arbitrary query alongside the standard metrics.</span></span> 

<span data-ttu-id="3b570-139">Los resultados se recalculan automáticamente cada hora.</span><span class="sxs-lookup"><span data-stu-id="3b570-139">Results are automatically recalculated every hour.</span></span> <span data-ttu-id="3b570-140">Haga clic en el icono de actualización en el gráfico para recalcular inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="3b570-140">Click the Refresh icon on the chart to recalculate immediately.</span></span> <span data-ttu-id="3b570-141">(Cuando el explorador se actualiza, no se recalculan los resultados).</span><span class="sxs-lookup"><span data-stu-id="3b570-141">(Browser refresh doesn't recalculate.)</span></span>

## <a name="adjust-a-tile-on-the-dashboard"></a><span data-ttu-id="3b570-142">Ajuste de un icono en el panel</span><span class="sxs-lookup"><span data-stu-id="3b570-142">Adjust a tile on the dashboard</span></span>
<span data-ttu-id="3b570-143">Una vez que un icono se encuentra en el panel, es posible ajustarlo.</span><span class="sxs-lookup"><span data-stu-id="3b570-143">Once a tile is on the dashboard, you can adjust it.</span></span>

![Mantenga el mouse sobre un gráfico para poder editarlo.](./media/app-insights-dashboards/36.png)

1. <span data-ttu-id="3b570-145">Agregue un gráfico al icono.</span><span class="sxs-lookup"><span data-stu-id="3b570-145">Add a chart to the tile.</span></span>
2. <span data-ttu-id="3b570-146">Configure la métrica, la dimensión de agrupación y el estilo (tabla, gráfico) de un gráfico.</span><span class="sxs-lookup"><span data-stu-id="3b570-146">Set the metric, group-by dimension and style (table, graph) of a chart.</span></span>
3. <span data-ttu-id="3b570-147">Arrastre por el diagrama para acercar; haga clic en el botón Deshacer para restablecer el intervalo de tiempo; establezca las propiedades de filtro para los gráficos del icono.</span><span class="sxs-lookup"><span data-stu-id="3b570-147">Drag across the diagram to zoom in; click the undo button to reset the timespan; set filter properties for the charts on the tile.</span></span>
4. <span data-ttu-id="3b570-148">Establezca el título del icono.</span><span class="sxs-lookup"><span data-stu-id="3b570-148">Set tile title.</span></span>

<span data-ttu-id="3b570-149">Los iconos anclados desde hojas del explorador de métricas tienen más opciones de edición que los iconos anclados desde una hoja de información general.</span><span class="sxs-lookup"><span data-stu-id="3b570-149">Tiles pinned from metric explorer blades have more editing options than tiles pinned from an Overview blade.</span></span>

<span data-ttu-id="3b570-150">El icono original que ancló no se ve afectado por las modificaciones.</span><span class="sxs-lookup"><span data-stu-id="3b570-150">The original tile that you pinned isn't affected by your edits.</span></span>

## <a name="switch-between-dashboards"></a><span data-ttu-id="3b570-151">Cambio entre paneles</span><span class="sxs-lookup"><span data-stu-id="3b570-151">Switch between dashboards</span></span>
<span data-ttu-id="3b570-152">Puede guardar más de un panel y cambiar de uno a otro.</span><span class="sxs-lookup"><span data-stu-id="3b570-152">You can save more than one dashboard and switch between them.</span></span> <span data-ttu-id="3b570-153">Cuando se ancla un gráfico o una hoja, se agrega al panel actual.</span><span class="sxs-lookup"><span data-stu-id="3b570-153">When you pin a chart or blade, they're added to the current dashboard.</span></span>

![Para cambiar entre los paneles, haga clic en Panel y seleccione un panel guardado.](./media/app-insights-dashboards/32.png)

<span data-ttu-id="3b570-157">Por ejemplo, podría tener un panel para mostrarlo en pantalla completa en la sala de reuniones y otro para el desarrollo general.</span><span class="sxs-lookup"><span data-stu-id="3b570-157">For example, you might have one dashboard for displaying full screen in the team room, and another for general development.</span></span>

<span data-ttu-id="3b570-158">En el panel, una hoja aparece como un icono. Haga clic en él para ir a la hoja.</span><span class="sxs-lookup"><span data-stu-id="3b570-158">On the dashboard, a blade appears as a tile: click it to go to the blade.</span></span> <span data-ttu-id="3b570-159">Un gráfico replica el gráfico en su ubicación original.</span><span class="sxs-lookup"><span data-stu-id="3b570-159">A chart replicates the chart in its original location.</span></span>

![Haga clic en un icono para abrir la hoja que representa.](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a><span data-ttu-id="3b570-161">Uso compartido de paneles</span><span class="sxs-lookup"><span data-stu-id="3b570-161">Share dashboards</span></span>
<span data-ttu-id="3b570-162">Cuando haya creado un panel, puede compartirlo con otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="3b570-162">When you've created a dashboard, you can share it with other users.</span></span>

![En el encabezado del panel, haga clic en Compartir.](./media/app-insights-dashboards/41.png)

<span data-ttu-id="3b570-164">Aprenda más acerca de [Roles y control de acceso](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="3b570-164">Learn about [Roles and access control](app-insights-resources-roles-access-control.md).</span></span>

## <a name="app-navigation"></a><span data-ttu-id="3b570-165">Navegación en la aplicación</span><span class="sxs-lookup"><span data-stu-id="3b570-165">App navigation</span></span>
<span data-ttu-id="3b570-166">La hoja de información general es la puerta de enlace para más información acerca de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3b570-166">The overview blade is the gateway to more information about your app.</span></span>

* <span data-ttu-id="3b570-167">**Cualquier gráfico o icono**: haga clic en cualquier icono o gráfico para ver más detalles acerca de lo que muestra.</span><span class="sxs-lookup"><span data-stu-id="3b570-167">**Any chart or tile** - Click any tile or chart to see more detail about what it displays.</span></span>

### <a name="overview-blade-buttons"></a><span data-ttu-id="3b570-168">Botones de la hoja de información general</span><span class="sxs-lookup"><span data-stu-id="3b570-168">Overview blade buttons</span></span>
![Barra de navegación superior de hoja de información general](./media/app-insights-dashboards/app-overview-top-nav.png)

* <span data-ttu-id="3b570-170">[**Explorador de métricas**](app-insights-metrics-explorer.md): cree sus propios gráficos de rendimiento y uso.</span><span class="sxs-lookup"><span data-stu-id="3b570-170">[**Metrics Explorer**](app-insights-metrics-explorer.md) - Create your own charts of performance and usage.</span></span>
* <span data-ttu-id="3b570-171">[**Búsqueda**](app-insights-diagnostic-search.md): investigue casos específicos de eventos como solicitudes, excepciones o seguimientos de registro.</span><span class="sxs-lookup"><span data-stu-id="3b570-171">[**Search**](app-insights-diagnostic-search.md) - Investigate specific instances of events such as requests, exceptions, or log traces.</span></span>
* <span data-ttu-id="3b570-172">[**Analytics**](app-insights-analytics.md): consultas eficaces sobre los datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="3b570-172">[**Analytics**](app-insights-analytics.md) - Powerful queries over your telemetry.</span></span>
* <span data-ttu-id="3b570-173">**Intervalo de tiempo**: ajuste el intervalo mostrado por todos los gráficos de la hoja.</span><span class="sxs-lookup"><span data-stu-id="3b570-173">**Time range** - Adjust the range displayed by all the charts on the blade.</span></span>
* <span data-ttu-id="3b570-174">**Eliminar**: elimine el recurso de Application Insights para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="3b570-174">**Delete** - Delete the Application Insights resource for this app.</span></span> <span data-ttu-id="3b570-175">Debe también quitar los paquetes de Application Insights del código de la aplicación, o editar la [clave de instrumentación](app-insights-create-new-resource.md#copy-the-instrumentation-key) de la aplicación para dirigir la telemetría a un recurso de Application Insights diferente.</span><span class="sxs-lookup"><span data-stu-id="3b570-175">You should also either remove the Application Insights packages from your app code, or edit the [instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) in your app to direct telemetry to a different Application Insights resource.</span></span>

### <a name="essentials-tab"></a><span data-ttu-id="3b570-176">Pestaña Essentials</span><span class="sxs-lookup"><span data-stu-id="3b570-176">Essentials tab</span></span>
* <span data-ttu-id="3b570-177">[Clave de instrumentación](app-insights-create-new-resource.md#copy-the-instrumentation-key): identifica este recurso de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3b570-177">[Instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) - Identifies this app resource.</span></span>
* <span data-ttu-id="3b570-178">Precios: hacen que las características estén disponibles y establecen límites de volumen.</span><span class="sxs-lookup"><span data-stu-id="3b570-178">Pricing - Make features available and set volume caps.</span></span>

### <a name="app-navigation-bar"></a><span data-ttu-id="3b570-179">Barra de navegación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="3b570-179">App navigation bar</span></span>
![Barra de navegación izquierda](./media/app-insights-dashboards/app-left-nav-bar.png)

* <span data-ttu-id="3b570-181">**Información general**: vuelve a la hoja de información general de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3b570-181">**Overview** - Return to the app overview blade.</span></span>
* <span data-ttu-id="3b570-182">**Registro de actividad**: alertas y eventos administrativos de Azure.</span><span class="sxs-lookup"><span data-stu-id="3b570-182">**Activity log** - Alerts and Azure administrative events.</span></span>
* <span data-ttu-id="3b570-183">[**Control de acceso**](app-insights-resources-roles-access-control.md): proporciona acceso a los miembros del equipo y a otros elementos.</span><span class="sxs-lookup"><span data-stu-id="3b570-183">[**Access control**](app-insights-resources-roles-access-control.md) - Provide access to team members and others.</span></span>
* <span data-ttu-id="3b570-184">[**Etiquetas**](../azure-resource-manager/resource-group-using-tags.md): usa etiquetas para agrupar la aplicación con otras.</span><span class="sxs-lookup"><span data-stu-id="3b570-184">[**Tags**](../azure-resource-manager/resource-group-using-tags.md) - Use tags to group your app with others.</span></span>

<span data-ttu-id="3b570-185">INVESTIGAR</span><span class="sxs-lookup"><span data-stu-id="3b570-185">INVESTIGATE</span></span>

* <span data-ttu-id="3b570-186">[**Mapa de aplicación**](app-insights-app-map.md): mapa activo que muestra los componentes de la aplicación, obtenidos de la información de dependencia.</span><span class="sxs-lookup"><span data-stu-id="3b570-186">[**Application map**](app-insights-app-map.md) - Active map showing the components of your application, derived from the dependency information.</span></span>
* <span data-ttu-id="3b570-187">[**Detección inteligente**](app-insights-proactive-diagnostics.md): revise las alertas recientes de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="3b570-187">[**Smart Detection**](app-insights-proactive-diagnostics.md) - Review recent performance alerts.</span></span>
* <span data-ttu-id="3b570-188">[**Stream en vivo**](app-insights-live-stream.md): un conjunto fijo de métricas casi instantáneas, útiles al implementar una nueva compilación o depurar.</span><span class="sxs-lookup"><span data-stu-id="3b570-188">[**Live Stream**](app-insights-live-stream.md) - A fixed set of near-instant metrics, useful when deploying a new build or debugging.</span></span>
* <span data-ttu-id="3b570-189">[**Disponibilidad / pruebas web**](app-insights-monitor-web-app-availability.md): envíe solicitudes regulares a la aplicación web desde cualquier parte del mundo*.</span><span class="sxs-lookup"><span data-stu-id="3b570-189">[**Availability / Web tests**](app-insights-monitor-web-app-availability.md) - Send regular requests to your web app from around the world.*</span></span>
* <span data-ttu-id="3b570-190">[**Errores, rendimiento**](app-insights-web-monitor-performance.md): excepciones, tasas de error y tiempos de respuesta para las solicitudes realizadas a la aplicación y para las solicitudes realizadas desde la aplicación a las [dependencias](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="3b570-190">[**Failures, Performance**](app-insights-web-monitor-performance.md) - Exceptions, failure rates and response times for requests to your app and for requests from your app to [dependencies](app-insights-asp-net-dependencies.md).</span></span>
* <span data-ttu-id="3b570-191">[**Rendimiento**](app-insights-web-monitor-performance.md): tiempo de respuesta, tiempos de respuesta de dependencia.</span><span class="sxs-lookup"><span data-stu-id="3b570-191">[**Performance**](app-insights-web-monitor-performance.md) - Response time, dependency response times.</span></span>
* <span data-ttu-id="3b570-192">[Servidores](app-insights-web-monitor-performance.md) : contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="3b570-192">[Servers](app-insights-web-monitor-performance.md) - Performance counters.</span></span> <span data-ttu-id="3b570-193">Está disponible si se [instala el Monitor de estado](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="3b570-193">Available if you [install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="3b570-194">**Explorador** : vista de página y rendimiento de AJAX.</span><span class="sxs-lookup"><span data-stu-id="3b570-194">**Browser** - Page view and AJAX performance.</span></span> <span data-ttu-id="3b570-195">Está disponible si se [instrumentan las páginas web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="3b570-195">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>
* <span data-ttu-id="3b570-196">**Uso** : vista de página, recuentos de usuarios y sesiones.</span><span class="sxs-lookup"><span data-stu-id="3b570-196">**Usage** - Page view, user, and session counts.</span></span> <span data-ttu-id="3b570-197">Está disponible si se [instrumentan las páginas web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="3b570-197">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>

<span data-ttu-id="3b570-198">CONFIGURAR</span><span class="sxs-lookup"><span data-stu-id="3b570-198">CONFIGURE</span></span>

* <span data-ttu-id="3b570-199">**Introducción** : tutorial en línea.</span><span class="sxs-lookup"><span data-stu-id="3b570-199">**Getting started** - inline tutorial.</span></span>
* <span data-ttu-id="3b570-200">**Propiedades** : clave de instrumentación, suscripción e identificador de recursos.</span><span class="sxs-lookup"><span data-stu-id="3b570-200">**Properties** - instrumentation key, subscription and resource id.</span></span>
* <span data-ttu-id="3b570-201">[Alertas](app-insights-alerts.md) : configuración de alertas de métricas.</span><span class="sxs-lookup"><span data-stu-id="3b570-201">[Alerts](app-insights-alerts.md) - metric alert configuration.</span></span>
* <span data-ttu-id="3b570-202">[Exportación continua](app-insights-export-telemetry.md) : configuración de la exportación de los datos de telemetría a Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="3b570-202">[Continuous export](app-insights-export-telemetry.md) - configure export of telemetry to Azure storage.</span></span>
* <span data-ttu-id="3b570-203">[Pruebas de rendimiento](app-insights-monitor-web-app-availability.md#performance-tests) : configuración de una carga simétrica en el sitio web.</span><span class="sxs-lookup"><span data-stu-id="3b570-203">[Performance testing](app-insights-monitor-web-app-availability.md#performance-tests) - set up a synthetic load on your website.</span></span>
* <span data-ttu-id="3b570-204">[Cuotas y precios](app-insights-pricing.md) y [muestreo de ingesta](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="3b570-204">[Quota and pricing](app-insights-pricing.md) and [ingestion sampling](app-insights-sampling.md).</span></span>
* <span data-ttu-id="3b570-205">**Acceso a API**: cree [anotaciones de versión](app-insights-annotations.md) y para la API de acceso a datos.</span><span class="sxs-lookup"><span data-stu-id="3b570-205">**API Access** - Create [release annotations](app-insights-annotations.md) and for the Data Access API.</span></span>
* <span data-ttu-id="3b570-206">[**Elementos de trabajo**](app-insights-diagnostic-search.md#create-work-item): conéctese a un sistema de seguimiento de trabajos de modo que pueda crear errores mientras se inspeccionan los datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="3b570-206">[**Work Items**](app-insights-diagnostic-search.md#create-work-item) - Connect to a work tracking system so that you can create bugs while inspecting telemetry.</span></span>

<span data-ttu-id="3b570-207">CONFIGURACIÓN</span><span class="sxs-lookup"><span data-stu-id="3b570-207">SETTINGS</span></span>

* <span data-ttu-id="3b570-208">[**Bloqueos**](../azure-resource-manager/resource-group-lock-resources.md): bloquee recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="3b570-208">[**Locks**](../azure-resource-manager/resource-group-lock-resources.md) - lock Azure resources</span></span>
* <span data-ttu-id="3b570-209">[**Script de automatización**](app-insights-powershell.md): exporte una definición del recurso de Azure de forma que pueda usarla como plantilla para crear nuevos recursos.</span><span class="sxs-lookup"><span data-stu-id="3b570-209">[**Automation script**](app-insights-powershell.md) - export a definition of the Azure resource so that you can use it as a template to create new resources.</span></span>


## <a name="video"></a><span data-ttu-id="3b570-210">Vídeo</span><span class="sxs-lookup"><span data-stu-id="3b570-210">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="3b570-211">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3b570-211">Next steps</span></span>

|  |  |
| --- | --- |
| [<span data-ttu-id="3b570-212">Explorador de métricas</span><span class="sxs-lookup"><span data-stu-id="3b570-212">Metrics explorer</span></span>](app-insights-metrics-explorer.md)<br/><span data-ttu-id="3b570-213">Filtre y segmente las métricas</span><span class="sxs-lookup"><span data-stu-id="3b570-213">Filter and segment metrics</span></span> |![Ejemplo de búsqueda](./media/app-insights-dashboards/64.png) |
| [<span data-ttu-id="3b570-215">Búsqueda de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="3b570-215">Diagnostic search</span></span>](app-insights-diagnostic-search.md)<br/><span data-ttu-id="3b570-216">Busque y examine eventos y eventos relacionados, y cree errores.</span><span class="sxs-lookup"><span data-stu-id="3b570-216">Find and inspect events, related events, and create bugs</span></span> |![Ejemplo de búsqueda](./media/app-insights-dashboards/61.png) |
| [<span data-ttu-id="3b570-218">Analytics</span><span class="sxs-lookup"><span data-stu-id="3b570-218">Analytics</span></span>](app-insights-analytics.md)<br/><span data-ttu-id="3b570-219">Lenguaje de consulta eficaz</span><span class="sxs-lookup"><span data-stu-id="3b570-219">Powerful query language</span></span> |![Ejemplo de búsqueda](./media/app-insights-dashboards/63.png) |
