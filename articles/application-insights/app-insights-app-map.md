---
title: "Mapa de aplicación en Azure Application Insights | Microsoft Docs"
description: "Una presentación visual de las dependencias entre los componentes de la aplicación, con etiquetas para KPI y alertas."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 3bf37fe9-70d7-4229-98d6-4f624d256c36
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 207526b7a675f92134d045ebefb9a372749bce92
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="application-map-in-application-insights"></a><span data-ttu-id="8814b-103">Mapa de aplicación en Application Insights</span><span class="sxs-lookup"><span data-stu-id="8814b-103">Application Map in Application Insights</span></span>
<span data-ttu-id="8814b-104">En [Azure Application Insights](app-insights-overview.md), el mapa de aplicación es un diseño visual de las relaciones de dependencia de los componentes de aplicación.</span><span class="sxs-lookup"><span data-stu-id="8814b-104">In [Azure Application Insights](app-insights-overview.md), Application Map is a visual layout of the dependency relationships of your application components.</span></span> <span data-ttu-id="8814b-105">Cada componente muestra indicadores clave de rendimiento (KPI), como carga, rendimiento, errores y alertas, para ayudarle a detectar los componentes que provocan problemas o errores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="8814b-105">Each component shows KPIs such as load, performance, failures, and alerts, to help you discover any component causing a performance issue or failure.</span></span> <span data-ttu-id="8814b-106">Puede hacer clic a través de cualquier componente para ver un diagnóstico más detallado, como los eventos de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8814b-106">You can click through from any component to more detailed diagnostics, such as Application Insights events.</span></span> <span data-ttu-id="8814b-107">Si su aplicación usa los servicios de Azure, también puede hacer clic por los diagnósticos de Azure, como las recomendaciones SQL Database Advisor.</span><span class="sxs-lookup"><span data-stu-id="8814b-107">If your app uses Azure services, you can also click through to Azure diagnostics, such as SQL Database Advisor recommendations.</span></span>

<span data-ttu-id="8814b-108">Al igual que otros gráficos, puede anclar un mapa de aplicación al panel de Azure, donde es totalmente funcional.</span><span class="sxs-lookup"><span data-stu-id="8814b-108">Like other charts, you can pin an application map to the Azure dashboard, where it is fully functional.</span></span> 

## <a name="open-the-application-map"></a><span data-ttu-id="8814b-109">Apertura del mapa de aplicación</span><span class="sxs-lookup"><span data-stu-id="8814b-109">Open the application map</span></span>
<span data-ttu-id="8814b-110">Abra el mapa desde la hoja de información general de su aplicación:</span><span class="sxs-lookup"><span data-stu-id="8814b-110">Open the map from the overview blade for your application:</span></span>

![abrir el mapa de aplicación](./media/app-insights-app-map/01.png)

![mapa de aplicación](./media/app-insights-app-map/02.png)

<span data-ttu-id="8814b-113">El mapa muestra:</span><span class="sxs-lookup"><span data-stu-id="8814b-113">The map shows:</span></span>

* <span data-ttu-id="8814b-114">Pruebas de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="8814b-114">Availability tests</span></span>
* <span data-ttu-id="8814b-115">Componente del lado cliente (que se supervisa con el SDK de JavaScript)</span><span class="sxs-lookup"><span data-stu-id="8814b-115">Client-side component (monitored with the JavaScript SDK)</span></span>
* <span data-ttu-id="8814b-116">Componente del lado servidor</span><span class="sxs-lookup"><span data-stu-id="8814b-116">Server-side component</span></span>
* <span data-ttu-id="8814b-117">Dependencias de los componentes cliente y servidor</span><span class="sxs-lookup"><span data-stu-id="8814b-117">Dependencies of the client and server components</span></span>

<span data-ttu-id="8814b-118">Puede expandir y contraer los grupos de vínculos de dependencia:</span><span class="sxs-lookup"><span data-stu-id="8814b-118">You can expand and collapse dependency link groups:</span></span>

![contraer](./media/app-insights-app-map/03.png)

<span data-ttu-id="8814b-120">Si tiene un gran número de dependencias de un tipo (SQL, HTTP, etc.), aparecen agrupadas.</span><span class="sxs-lookup"><span data-stu-id="8814b-120">If you have many dependencies of one type (SQL, HTTP etc.), they may appear grouped.</span></span> 

![dependencias agrupadas](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a><span data-ttu-id="8814b-122">Detección de problemas</span><span class="sxs-lookup"><span data-stu-id="8814b-122">Spot problems</span></span>
<span data-ttu-id="8814b-123">Cada nodo cuenta con indicadores de rendimiento relacionados, como los porcentajes de error, rendimiento y carga de ese componente.</span><span class="sxs-lookup"><span data-stu-id="8814b-123">Each node has relevant performance indicators, such as the load, performance, and failure rates for that component.</span></span> 

<span data-ttu-id="8814b-124">Los iconos de advertencia resaltan los posibles problemas.</span><span class="sxs-lookup"><span data-stu-id="8814b-124">Warning icons highlight possible problems.</span></span> <span data-ttu-id="8814b-125">Una advertencia naranja significa que hay errores en las solicitudes, las vistas de página o las llamadas de dependencia.</span><span class="sxs-lookup"><span data-stu-id="8814b-125">An orange warning means there are failures in requests, page views or dependency calls.</span></span> <span data-ttu-id="8814b-126">Rojo significa un porcentaje de error superior al 5 %.</span><span class="sxs-lookup"><span data-stu-id="8814b-126">Red means a failure rate above 5%.</span></span> <span data-ttu-id="8814b-127">Si quiere ajustar estos umbrales, abra Opciones.</span><span class="sxs-lookup"><span data-stu-id="8814b-127">If you want to adjust these thresholds, open Options.</span></span>

![iconos de error](./media/app-insights-app-map/04.png)

<span data-ttu-id="8814b-129">También se muestran las alertas activas:</span><span class="sxs-lookup"><span data-stu-id="8814b-129">Active alerts also show up:</span></span> 

![alertas activas](./media/app-insights-app-map/05.png)

<span data-ttu-id="8814b-131">Si usa SQL Azure, hay un icono que se muestra cuando hay recomendaciones sobre cómo mejorar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="8814b-131">If you use SQL Azure, there's an icon that shows when there are recommendations on how you can improve performance.</span></span> 

![recomendación de Azure](./media/app-insights-app-map/06.png)

<span data-ttu-id="8814b-133">Haga clic en cualquier icono para más detalles:</span><span class="sxs-lookup"><span data-stu-id="8814b-133">Click any icon to get more details:</span></span>

![recomendación de Azure](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a><span data-ttu-id="8814b-135">Recorrido por los diagnósticos mediante clic</span><span class="sxs-lookup"><span data-stu-id="8814b-135">Diagnostic click through</span></span>
<span data-ttu-id="8814b-136">Cada uno de los nodos del mapa ofrece un recorrido dirigido mediante clic por la información de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="8814b-136">Each of the nodes on the map offers targeted click through for diagnostics.</span></span> <span data-ttu-id="8814b-137">Las opciones varían según el tipo del nodo.</span><span class="sxs-lookup"><span data-stu-id="8814b-137">The options vary depending on the type of the node.</span></span>

![opciones de servidor](./media/app-insights-app-map/09.png)

<span data-ttu-id="8814b-139">En el caso de los componentes que se hospedan en Azure, las opciones incluyen vínculos directos a ellos.</span><span class="sxs-lookup"><span data-stu-id="8814b-139">For components that are hosted in Azure, the options include direct links to them.</span></span>

## <a name="filters-and-time-range"></a><span data-ttu-id="8814b-140">Filtros e intervalo de tiempo</span><span class="sxs-lookup"><span data-stu-id="8814b-140">Filters and time range</span></span>
<span data-ttu-id="8814b-141">De forma predeterminada, el mapa resume todos los datos disponibles para el intervalo de tiempo seleccionado.</span><span class="sxs-lookup"><span data-stu-id="8814b-141">By default, the map summarizes all the data available for the chosen time range.</span></span> <span data-ttu-id="8814b-142">Sin embargo, puede filtrar para incluir solo nombres de operaciones o dependencias específicos.</span><span class="sxs-lookup"><span data-stu-id="8814b-142">But you can filter it to include only specific operation names or dependencies.</span></span>

* <span data-ttu-id="8814b-143">Nombre de la operación: incluye vistas de página y tipos de solicitud del lado servidor.</span><span class="sxs-lookup"><span data-stu-id="8814b-143">Operation name: This includes both page views and server-side request types.</span></span> <span data-ttu-id="8814b-144">Con esta opción, el mapa muestra el KPI en el nodo del lado cliente o servidor solo de las operaciones seleccionadas.</span><span class="sxs-lookup"><span data-stu-id="8814b-144">With this option, the map shows the KPI on the server/client-side node for the selected operations only.</span></span> <span data-ttu-id="8814b-145">Muestra las dependencias que se invocan en el contexto de esas operaciones específicas.</span><span class="sxs-lookup"><span data-stu-id="8814b-145">It shows the dependencies called in the context of those specific operations.</span></span>
* <span data-ttu-id="8814b-146">Nombre base de dependencia: incluye las dependencias del explorador de AJAX y las dependencias del lado servidor.</span><span class="sxs-lookup"><span data-stu-id="8814b-146">Dependency base name: This includes the AJAX browser dependencies and server-side dependencies.</span></span> <span data-ttu-id="8814b-147">Si utiliza la API TrackDependency para notificar telemetría de dependencias personalizada, esta información también se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="8814b-147">If you report custom dependency telemetry with the TrackDependency API, they also appear here.</span></span> <span data-ttu-id="8814b-148">Puede seleccionar las dependencias que se mostrarán en el mapa.</span><span class="sxs-lookup"><span data-stu-id="8814b-148">You can select the dependencies to show on the map.</span></span> <span data-ttu-id="8814b-149">Actualmente esta selección no filtra las solicitudes del lado servidor ni las vistas de página del lado cliente.</span><span class="sxs-lookup"><span data-stu-id="8814b-149">Currently this selection does not filter the server-side requests, or the client-side page views.</span></span>

![Establecer filtros](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a><span data-ttu-id="8814b-151">Guardado de los filtros</span><span class="sxs-lookup"><span data-stu-id="8814b-151">Save filters</span></span>
<span data-ttu-id="8814b-152">Para guardar los filtros aplicados, ancle la vista filtrada a un [panel](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="8814b-152">To save the filters you have applied, pin the filtered view onto a [dashboard](app-insights-dashboards.md).</span></span>

![Anclar al panel](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a><span data-ttu-id="8814b-154">Panel de errores</span><span class="sxs-lookup"><span data-stu-id="8814b-154">Error pane</span></span>
<span data-ttu-id="8814b-155">Al hacer clic en un nodo del mapa, se muestra un panel de error se muestra en el lado derecho con un resumen de los errores de ese nodo.</span><span class="sxs-lookup"><span data-stu-id="8814b-155">When you click a node in the map, an error pane is displayed on the right-hand side summarizing failures for that node.</span></span> <span data-ttu-id="8814b-156">Los errores se agrupan en primer lugar por identificador de operación y, luego, por identificador de problema.</span><span class="sxs-lookup"><span data-stu-id="8814b-156">Failures are grouped first by operation ID and then grouped by problem ID.</span></span>

![Panel de errores](./media/app-insights-app-map/error-pane.png)

<span data-ttu-id="8814b-158">Al hacer clic en un error, se le redirige a la instancia más reciente de ese error.</span><span class="sxs-lookup"><span data-stu-id="8814b-158">Clicking on a failure takes you to the most recent instance of that failure.</span></span>

## <a name="resource-health"></a><span data-ttu-id="8814b-159">Estado de los recursos</span><span class="sxs-lookup"><span data-stu-id="8814b-159">Resource health</span></span>
<span data-ttu-id="8814b-160">En algunos tipos de recursos, se muestra el estado en la parte superior del panel de errores.</span><span class="sxs-lookup"><span data-stu-id="8814b-160">For some resource types, resource health is displayed at the top of the error pane.</span></span> <span data-ttu-id="8814b-161">Por ejemplo, al hacer clic en un nodo de SQL se mostrará el estado de la base de datos y las alertas activadas.</span><span class="sxs-lookup"><span data-stu-id="8814b-161">For example, clicking a SQL node will show the database health and any alerts that have fired.</span></span>

![Estado de los recursos](./media/app-insights-app-map/resource-health.png)

<span data-ttu-id="8814b-163">Puede hacer clic en el nombre del recurso para ver las métricas de información general estándar de ese recurso.</span><span class="sxs-lookup"><span data-stu-id="8814b-163">You can click the resource name to view standard overview metrics for that resource.</span></span>

## <a name="end-to-end-system-app-maps"></a><span data-ttu-id="8814b-164">Mapas de la aplicación del sistema completo</span><span class="sxs-lookup"><span data-stu-id="8814b-164">End-to-end system app maps</span></span>

<span data-ttu-id="8814b-165">*Se requiere la versión 2.3 o posterior del SDK*</span><span class="sxs-lookup"><span data-stu-id="8814b-165">*Requires SDK version 2.3 or higher*</span></span>

<span data-ttu-id="8814b-166">Si la aplicación tiene varios componentes, por ejemplo, un servicio back-end además de la aplicación web, puede mostrarlos todos en un mapa de la aplicación integrado.</span><span class="sxs-lookup"><span data-stu-id="8814b-166">If your application has several components - for example, a back-end service in addition to the web app - then you can show them all on one integrated app map.</span></span>

![Establecer filtros](./media/app-insights-app-map/multi-component-app-map.png)

<span data-ttu-id="8814b-168">El mapa de aplicación busca los nodos de servidor siguiendo las llamadas de una dependencia HTTP entre los servidores con el SDK de Application Insights instalado.</span><span class="sxs-lookup"><span data-stu-id="8814b-168">The app map finds server nodes by following any HTTP dependency calls made between servers with the Application Insights SDK installed.</span></span> <span data-ttu-id="8814b-169">Se da por hecho que cada recurso de Application Insights contiene un servidor.</span><span class="sxs-lookup"><span data-stu-id="8814b-169">Each Application Insights resource is assumed to contain one server.</span></span>

### <a name="multi-role-app-map-preview"></a><span data-ttu-id="8814b-170">Mapa de aplicación de varios roles (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="8814b-170">Multi-role app map (preview)</span></span>

<span data-ttu-id="8814b-171">La característica de mapa de aplicación de varios roles en versión preliminar permite usar el mapa de aplicación con varios servidores que envían datos al mismo recurso o la misma clave de instrumentación de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8814b-171">The preview multi-role app map feature allows you to use the app map with multiple servers sending data to the same Application Insights resource  / instrumentation key.</span></span> <span data-ttu-id="8814b-172">Los servidores del mapa están segmentados por la propiedad cloud_nombreDelRol en elementos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="8814b-172">Servers in the map are segmented by the cloud_RoleName property on telemetry items.</span></span> <span data-ttu-id="8814b-173">Establezca el *mapa de aplicación de varios roles* en *Activado* en la hoja de versiones preliminares para habilitar esta configuración.</span><span class="sxs-lookup"><span data-stu-id="8814b-173">Set *Multi-role Application Map* to *On* from the Previews blade to enable this configuration.</span></span>

<span data-ttu-id="8814b-174">Este enfoque puede ser útil en una aplicación de microservicios o en otros escenarios en los que desea correlacionar eventos de varios servidores de un único recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8814b-174">This approach may be desired in a micro-services application, or in other scenarios where you want to correlate events across multiple servers within a single Application Insights resource.</span></span>

## <a name="video"></a><span data-ttu-id="8814b-175">Vídeo</span><span class="sxs-lookup"><span data-stu-id="8814b-175">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a><span data-ttu-id="8814b-176">Comentarios</span><span class="sxs-lookup"><span data-stu-id="8814b-176">Feedback</span></span>
<span data-ttu-id="8814b-177">Proporcione sus comentarios mediante la opción de comentarios del portal.</span><span class="sxs-lookup"><span data-stu-id="8814b-177">Please provide feedback through the portal feedback option.</span></span>

![Imagen MapLink-1](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a><span data-ttu-id="8814b-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8814b-179">Next steps</span></span>

* [<span data-ttu-id="8814b-180">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8814b-180">Azure portal</span></span>](https://portal.azure.com)
