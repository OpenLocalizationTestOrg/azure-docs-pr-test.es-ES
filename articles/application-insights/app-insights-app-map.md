---
title: "aaaApplication mapa de visión de la aplicación de Azure | Documentos de Microsoft"
description: "Una presentación visual de las dependencias de hello entre componentes de aplicación, con la etiqueta con los KPI y las alertas."
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
ms.openlocfilehash: 96ab753a100ea53ec7d367e3559b6622ab6fd182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-map-in-application-insights"></a><span data-ttu-id="830e4-103">Mapa de aplicación en Application Insights</span><span class="sxs-lookup"><span data-stu-id="830e4-103">Application Map in Application Insights</span></span>
<span data-ttu-id="830e4-104">En [Azure Application Insights](app-insights-overview.md), asignación de aplicación no es un aspecto visual de las relaciones de dependencia de Hola de los componentes de aplicación.</span><span class="sxs-lookup"><span data-stu-id="830e4-104">In [Azure Application Insights](app-insights-overview.md), Application Map is a visual layout of hello dependency relationships of your application components.</span></span> <span data-ttu-id="830e4-105">Cada componente muestra KPI como toohelp de carga, el rendimiento, errores y alertas, detectar cualquier componente que se produce un error o problema de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="830e4-105">Each component shows KPIs such as load, performance, failures, and alerts, toohelp you discover any component causing a performance issue or failure.</span></span> <span data-ttu-id="830e4-106">Puede hacer clic en a través de cualquier componente toomore obtener diagnósticos, tales como eventos de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="830e4-106">You can click through from any component toomore detailed diagnostics, such as Application Insights events.</span></span> <span data-ttu-id="830e4-107">Si su aplicación usa los servicios de Azure, también puede hacer clic a través de diagnósticos de tooAzure, como las recomendaciones del Asistente de la base de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="830e4-107">If your app uses Azure services, you can also click through tooAzure diagnostics, such as SQL Database Advisor recommendations.</span></span>

<span data-ttu-id="830e4-108">Al igual que otros gráficos, puede anclar un toohello de asignación de aplicación panel de Azure, donde es totalmente funcional.</span><span class="sxs-lookup"><span data-stu-id="830e4-108">Like other charts, you can pin an application map toohello Azure dashboard, where it is fully functional.</span></span> 

## <a name="open-hello-application-map"></a><span data-ttu-id="830e4-109">Asignación de la aplicación hello abierto</span><span class="sxs-lookup"><span data-stu-id="830e4-109">Open hello application map</span></span>
<span data-ttu-id="830e4-110">Hola abrir mapa de hoja de información general de hello para la aplicación:</span><span class="sxs-lookup"><span data-stu-id="830e4-110">Open hello map from hello overview blade for your application:</span></span>

![abrir el mapa de aplicación](./media/app-insights-app-map/01.png)

![mapa de aplicación](./media/app-insights-app-map/02.png)

<span data-ttu-id="830e4-113">mapa de Hello muestra:</span><span class="sxs-lookup"><span data-stu-id="830e4-113">hello map shows:</span></span>

* <span data-ttu-id="830e4-114">Pruebas de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="830e4-114">Availability tests</span></span>
* <span data-ttu-id="830e4-115">Componente de cliente (que se supervisan con hello SDK de JavaScript)</span><span class="sxs-lookup"><span data-stu-id="830e4-115">Client-side component (monitored with hello JavaScript SDK)</span></span>
* <span data-ttu-id="830e4-116">Componente del lado servidor</span><span class="sxs-lookup"><span data-stu-id="830e4-116">Server-side component</span></span>
* <span data-ttu-id="830e4-117">Dependencias de los componentes de cliente y servidor de Hola</span><span class="sxs-lookup"><span data-stu-id="830e4-117">Dependencies of hello client and server components</span></span>

<span data-ttu-id="830e4-118">Puede expandir y contraer los grupos de vínculos de dependencia:</span><span class="sxs-lookup"><span data-stu-id="830e4-118">You can expand and collapse dependency link groups:</span></span>

![contraer](./media/app-insights-app-map/03.png)

<span data-ttu-id="830e4-120">Si tiene un gran número de dependencias de un tipo (SQL, HTTP, etc.), aparecen agrupadas.</span><span class="sxs-lookup"><span data-stu-id="830e4-120">If you have many dependencies of one type (SQL, HTTP etc.), they may appear grouped.</span></span> 

![dependencias agrupadas](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a><span data-ttu-id="830e4-122">Detección de problemas</span><span class="sxs-lookup"><span data-stu-id="830e4-122">Spot problems</span></span>
<span data-ttu-id="830e4-123">Cada nodo tiene indicadores de rendimiento pertinentes, como las velocidades de carga y rendimiento, error de Hola para ese componente.</span><span class="sxs-lookup"><span data-stu-id="830e4-123">Each node has relevant performance indicators, such as hello load, performance, and failure rates for that component.</span></span> 

<span data-ttu-id="830e4-124">Los iconos de advertencia resaltan los posibles problemas.</span><span class="sxs-lookup"><span data-stu-id="830e4-124">Warning icons highlight possible problems.</span></span> <span data-ttu-id="830e4-125">Una advertencia naranja significa que hay errores en las solicitudes, las vistas de página o las llamadas de dependencia.</span><span class="sxs-lookup"><span data-stu-id="830e4-125">An orange warning means there are failures in requests, page views or dependency calls.</span></span> <span data-ttu-id="830e4-126">Rojo significa un porcentaje de error superior al 5 %.</span><span class="sxs-lookup"><span data-stu-id="830e4-126">Red means a failure rate above 5%.</span></span> <span data-ttu-id="830e4-127">Si desea tooadjust estos umbrales, abra Opciones.</span><span class="sxs-lookup"><span data-stu-id="830e4-127">If you want tooadjust these thresholds, open Options.</span></span>

![iconos de error](./media/app-insights-app-map/04.png)

<span data-ttu-id="830e4-129">También se muestran las alertas activas:</span><span class="sxs-lookup"><span data-stu-id="830e4-129">Active alerts also show up:</span></span> 

![alertas activas](./media/app-insights-app-map/05.png)

<span data-ttu-id="830e4-131">Si usa SQL Azure, hay un icono que se muestra cuando hay recomendaciones sobre cómo mejorar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="830e4-131">If you use SQL Azure, there's an icon that shows when there are recommendations on how you can improve performance.</span></span> 

![recomendación de Azure](./media/app-insights-app-map/06.png)

<span data-ttu-id="830e4-133">Haga clic en cualquier icono tooget más detalles:</span><span class="sxs-lookup"><span data-stu-id="830e4-133">Click any icon tooget more details:</span></span>

![recomendación de Azure](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a><span data-ttu-id="830e4-135">Recorrido por los diagnósticos mediante clic</span><span class="sxs-lookup"><span data-stu-id="830e4-135">Diagnostic click through</span></span>
<span data-ttu-id="830e4-136">Cada uno de los nodos de hello en el mapa de hello ofrece destino click-through para diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="830e4-136">Each of hello nodes on hello map offers targeted click through for diagnostics.</span></span> <span data-ttu-id="830e4-137">Opciones de Hello varían según el tipo hello del nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="830e4-137">hello options vary depending on hello type of hello node.</span></span>

![opciones de servidor](./media/app-insights-app-map/09.png)

<span data-ttu-id="830e4-139">Para los componentes que se hospedan en Azure, las opciones de hello incluyen toothem de vínculos directos.</span><span class="sxs-lookup"><span data-stu-id="830e4-139">For components that are hosted in Azure, hello options include direct links toothem.</span></span>

## <a name="filters-and-time-range"></a><span data-ttu-id="830e4-140">Filtros e intervalo de tiempo</span><span class="sxs-lookup"><span data-stu-id="830e4-140">Filters and time range</span></span>
<span data-ttu-id="830e4-141">De forma predeterminada, mapa de hello resume todos los datos de hello disponibles para hello elegido el intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="830e4-141">By default, hello map summarizes all hello data available for hello chosen time range.</span></span> <span data-ttu-id="830e4-142">Pero puede filtrar nombres de las operaciones determinadas tooinclude o dependencias.</span><span class="sxs-lookup"><span data-stu-id="830e4-142">But you can filter it tooinclude only specific operation names or dependencies.</span></span>

* <span data-ttu-id="830e4-143">Nombre de la operación: incluye vistas de página y tipos de solicitud del lado servidor.</span><span class="sxs-lookup"><span data-stu-id="830e4-143">Operation name: This includes both page views and server-side request types.</span></span> <span data-ttu-id="830e4-144">Con esta opción, Hola mapa muestra Hola KPI en el nodo de cliente/servidor hello para las operaciones de hello seleccionado solo.</span><span class="sxs-lookup"><span data-stu-id="830e4-144">With this option, hello map shows hello KPI on hello server/client-side node for hello selected operations only.</span></span> <span data-ttu-id="830e4-145">Muestra las dependencias de hello llamadas en el contexto de Hola de esas operaciones específicas.</span><span class="sxs-lookup"><span data-stu-id="830e4-145">It shows hello dependencies called in hello context of those specific operations.</span></span>
* <span data-ttu-id="830e4-146">Nombre de base de dependencia: Esto incluye dependencias de explorador de AJAX de Hola y de servidor.</span><span class="sxs-lookup"><span data-stu-id="830e4-146">Dependency base name: This includes hello AJAX browser dependencies and server-side dependencies.</span></span> <span data-ttu-id="830e4-147">Si informe de telemetría de dependencia personalizada con hello TrackDependency API, también aparecen aquí.</span><span class="sxs-lookup"><span data-stu-id="830e4-147">If you report custom dependency telemetry with hello TrackDependency API, they also appear here.</span></span> <span data-ttu-id="830e4-148">Puede seleccionar tooshow de dependencias de hello en el mapa de Hola.</span><span class="sxs-lookup"><span data-stu-id="830e4-148">You can select hello dependencies tooshow on hello map.</span></span> <span data-ttu-id="830e4-149">Actualmente esta selección no filtra las solicitudes del servidor de Hola o vistas de página del lado cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="830e4-149">Currently this selection does not filter hello server-side requests, or hello client-side page views.</span></span>

![Establecer filtros](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a><span data-ttu-id="830e4-151">Guardado de los filtros</span><span class="sxs-lookup"><span data-stu-id="830e4-151">Save filters</span></span>
<span data-ttu-id="830e4-152">filtros de hello toosave ha aplicado, Hola pin filtra vista en una [panel](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="830e4-152">toosave hello filters you have applied, pin hello filtered view onto a [dashboard](app-insights-dashboards.md).</span></span>

![Toodashboard de PIN](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a><span data-ttu-id="830e4-154">Panel de errores</span><span class="sxs-lookup"><span data-stu-id="830e4-154">Error pane</span></span>
<span data-ttu-id="830e4-155">Al hacer clic en un nodo del mapa de hello, un panel de error se muestra en el lado derecho de hello resumir los errores de ese nodo.</span><span class="sxs-lookup"><span data-stu-id="830e4-155">When you click a node in hello map, an error pane is displayed on hello right-hand side summarizing failures for that node.</span></span> <span data-ttu-id="830e4-156">Los errores se agrupan en primer lugar por identificador de operación y, luego, por identificador de problema.</span><span class="sxs-lookup"><span data-stu-id="830e4-156">Failures are grouped first by operation ID and then grouped by problem ID.</span></span>

![Panel de errores](./media/app-insights-app-map/error-pane.png)

<span data-ttu-id="830e4-158">Al hacer clic en un error, le toohello instancia más reciente de ese error.</span><span class="sxs-lookup"><span data-stu-id="830e4-158">Clicking on a failure takes you toohello most recent instance of that failure.</span></span>

## <a name="resource-health"></a><span data-ttu-id="830e4-159">Estado de los recursos</span><span class="sxs-lookup"><span data-stu-id="830e4-159">Resource health</span></span>
<span data-ttu-id="830e4-160">Para algunos tipos de recursos, estado de los recursos se muestra en la parte superior de hello del panel de errores de Hola.</span><span class="sxs-lookup"><span data-stu-id="830e4-160">For some resource types, resource health is displayed at hello top of hello error pane.</span></span> <span data-ttu-id="830e4-161">Por ejemplo, al hacer clic en un nodo de SQL se mostrará de estado de base de datos de Hola y las alertas que se ha activado.</span><span class="sxs-lookup"><span data-stu-id="830e4-161">For example, clicking a SQL node will show hello database health and any alerts that have fired.</span></span>

![Estado de los recursos](./media/app-insights-app-map/resource-health.png)

<span data-ttu-id="830e4-163">Puede hacer clic en hello recurso nombre tooview estándar información general sobre las métricas para ese recurso.</span><span class="sxs-lookup"><span data-stu-id="830e4-163">You can click hello resource name tooview standard overview metrics for that resource.</span></span>

## <a name="end-to-end-system-app-maps"></a><span data-ttu-id="830e4-164">Mapas de la aplicación del sistema completo</span><span class="sxs-lookup"><span data-stu-id="830e4-164">End-to-end system app maps</span></span>

<span data-ttu-id="830e4-165">*Se requiere la versión 2.3 o posterior del SDK*</span><span class="sxs-lookup"><span data-stu-id="830e4-165">*Requires SDK version 2.3 or higher*</span></span>

<span data-ttu-id="830e4-166">Si la aplicación tiene varios componentes: por ejemplo, un servicio back-end además toohello web app -, a continuación, se puede mostrar usarlas en mapa de una aplicación integrada.</span><span class="sxs-lookup"><span data-stu-id="830e4-166">If your application has several components - for example, a back-end service in addition toohello web app - then you can show them all on one integrated app map.</span></span>

![Establecer filtros](./media/app-insights-app-map/multi-component-app-map.png)

<span data-ttu-id="830e4-168">asignación de aplicación Hola busca los nodos de servidor siguiendo las llamadas de la dependencia HTTP entre los servidores con hello que Application Insights SDK instalado.</span><span class="sxs-lookup"><span data-stu-id="830e4-168">hello app map finds server nodes by following any HTTP dependency calls made between servers with hello Application Insights SDK installed.</span></span> <span data-ttu-id="830e4-169">Se supone que cada recurso de Application Insights toocontain un servidor.</span><span class="sxs-lookup"><span data-stu-id="830e4-169">Each Application Insights resource is assumed toocontain one server.</span></span>

### <a name="multi-role-app-map-preview"></a><span data-ttu-id="830e4-170">Mapa de aplicación de varios roles (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="830e4-170">Multi-role app map (preview)</span></span>

<span data-ttu-id="830e4-171">característica de asignación de aplicación de varios roles de vista previa de Hello le permite toouse Hola aplicación asigna con varios servidores de envío de datos toohello mismo recurso de Application Insights / clave de instrumentación.</span><span class="sxs-lookup"><span data-stu-id="830e4-171">hello preview multi-role app map feature allows you toouse hello app map with multiple servers sending data toohello same Application Insights resource  / instrumentation key.</span></span> <span data-ttu-id="830e4-172">Servidores de asignación de hello están segmentados por propiedad de cloud_RoleName hello en los elementos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="830e4-172">Servers in hello map are segmented by hello cloud_RoleName property on telemetry items.</span></span> <span data-ttu-id="830e4-173">Establecer *asignación de la aplicación de varios roles* demasiado*en* de Hola tooenable de hoja de las vistas previas, esta configuración.</span><span class="sxs-lookup"><span data-stu-id="830e4-173">Set *Multi-role Application Map* too*On* from hello Previews blade tooenable this configuration.</span></span>

<span data-ttu-id="830e4-174">Este enfoque puede ser deseable en una aplicación de servicios de micro o en otros escenarios donde desea toocorrelate eventos a través de varios servidores dentro de un único recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="830e4-174">This approach may be desired in a micro-services application, or in other scenarios where you want toocorrelate events across multiple servers within a single Application Insights resource.</span></span>

## <a name="video"></a><span data-ttu-id="830e4-175">Vídeo</span><span class="sxs-lookup"><span data-stu-id="830e4-175">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a><span data-ttu-id="830e4-176">Comentarios</span><span class="sxs-lookup"><span data-stu-id="830e4-176">Feedback</span></span>
<span data-ttu-id="830e4-177">Proporcione sus comentarios a través de la opción de comentarios de portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="830e4-177">Please provide feedback through hello portal feedback option.</span></span>

![Imagen MapLink-1](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a><span data-ttu-id="830e4-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="830e4-179">Next steps</span></span>

* [<span data-ttu-id="830e4-180">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="830e4-180">Azure portal</span></span>](https://portal.azure.com)
