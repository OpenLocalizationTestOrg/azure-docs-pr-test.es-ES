---
title: "aaaExploring las métricas de visión de la aplicación de Azure | Documentos de Microsoft"
description: "Cómo toointerpret gráficos en el Explorador de métrica y cómo toocustomize hojas de métrica del explorador."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: bwren
ms.openlocfilehash: b77ae227ae61e800ad6f3af8a05cd123ea1d69e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-metrics-in-application-insights"></a><span data-ttu-id="5079e-103">Exploración de métricas en Application Insights</span><span class="sxs-lookup"><span data-stu-id="5079e-103">Exploring Metrics in Application Insights</span></span>
<span data-ttu-id="5079e-104">Las métricas de [Application Insights][start] son valores medidos y recuentos de eventos que se envían en telemetría desde la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5079e-104">Metrics in [Application Insights][start] are measured values and counts of events that are sent in telemetry from your application.</span></span> <span data-ttu-id="5079e-105">Ayudar a detectar problemas de rendimiento y a observar las tendencias sobre cómo se utiliza la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5079e-105">They help you detect performance issues and watch trends in how your application is being used.</span></span> <span data-ttu-id="5079e-106">Hay una amplia gama de métricas estándar y también se pueden crear los propios eventos y métricas personalizados.</span><span class="sxs-lookup"><span data-stu-id="5079e-106">There's a wide range of standard metrics, and you can also create your own custom metrics and events.</span></span>

<span data-ttu-id="5079e-107">Los recuentos de métricas y eventos se muestran en los gráficos de valores agregados, como sumas, promedios o recuentos.</span><span class="sxs-lookup"><span data-stu-id="5079e-107">Metrics and event counts are displayed in charts of aggregated values such as sums, averages, or counts.</span></span>

<span data-ttu-id="5079e-108">A continuación encontrará un conjunto de ejemplo de gráficos:</span><span class="sxs-lookup"><span data-stu-id="5079e-108">Here's a sample set of charts:</span></span>

![](./media/app-insights-metrics-explorer/01-overview.png)

<span data-ttu-id="5079e-109">Buscar en todas partes gráficos de métricas en el portal de Application Insights Hola.</span><span class="sxs-lookup"><span data-stu-id="5079e-109">You find metrics charts everywhere in hello Application Insights portal.</span></span> <span data-ttu-id="5079e-110">En la mayoría de los casos, puede personalizarse y puede agregar más hoja toohello de gráficos.</span><span class="sxs-lookup"><span data-stu-id="5079e-110">In most cases, they can be customized, and you can add more charts toohello blade.</span></span> <span data-ttu-id="5079e-111">En la hoja de información general de hello, haga clic en a través de toomore detallada gráficos (que tienen también como "Servidores"), o haga clic en **Explorer métricas** tooopen una nueva hoja donde puede crear gráficos personalizados.</span><span class="sxs-lookup"><span data-stu-id="5079e-111">From hello Overview blade, click through toomore detailed charts (which have titles such as "Servers"), or click **Metrics Explorer** tooopen a new blade where you can create custom charts.</span></span>

## <a name="time-range"></a><span data-ttu-id="5079e-112">Intervalo de tiempo</span><span class="sxs-lookup"><span data-stu-id="5079e-112">Time range</span></span>
<span data-ttu-id="5079e-113">Puede cambiar Hola cubierto por los gráficos de Hola o cuadrículas en cualquier hoja de intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="5079e-113">You can change hello Time range covered by hello charts or grids on any blade.</span></span>

![Hoja de información general de hello abierta de la aplicación Hola portal de Azure](./media/app-insights-metrics-explorer/03-range.png)

<span data-ttu-id="5079e-115">Si espera algunos datos que no ha aparecido todavía, haga clic en Actualizar.</span><span class="sxs-lookup"><span data-stu-id="5079e-115">If you're expecting some data that hasn't appeared yet, click Refresh.</span></span> <span data-ttu-id="5079e-116">Gráficos actualización por sí mismas a intervalos, pero los intervalos de hello son más largos para los intervalos de tiempo mayor.</span><span class="sxs-lookup"><span data-stu-id="5079e-116">Charts refresh themselves at intervals, but hello intervals are longer for larger time ranges.</span></span> <span data-ttu-id="5079e-117">Puede tardar unos instantes para toocome de datos a través de la canalización de análisis de hello en un gráfico.</span><span class="sxs-lookup"><span data-stu-id="5079e-117">It can take a while for data toocome through hello analysis pipeline onto a chart.</span></span>

<span data-ttu-id="5079e-118">toozoom en parte de un gráfico, arrastre sobre él:</span><span class="sxs-lookup"><span data-stu-id="5079e-118">toozoom into part of a chart, drag over it:</span></span>

![Arrastre por parte de un gráfico.](./media/app-insights-metrics-explorer/12-drag.png)

<span data-ttu-id="5079e-120">Haga clic en toorestore botón Deshacer Zoom de Hola.</span><span class="sxs-lookup"><span data-stu-id="5079e-120">Click hello Undo Zoom button toorestore it.</span></span>

## <a name="granularity-and-point-values"></a><span data-ttu-id="5079e-121">Valores de granularidad y punto</span><span class="sxs-lookup"><span data-stu-id="5079e-121">Granularity and point values</span></span>
<span data-ttu-id="5079e-122">Mantenga el mouse sobre los valores de hello gráfico toodisplay Hola de métricas de hello en ese momento.</span><span class="sxs-lookup"><span data-stu-id="5079e-122">Hover your mouse over hello chart toodisplay hello values of hello metrics at that point.</span></span>

![Mantenga el mouse de hello sobre un gráfico](./media/app-insights-metrics-explorer/02-focus.png)

<span data-ttu-id="5079e-124">valor de Hola de métrica de hello en un momento determinado se agrega en hello precede el intervalo de muestreo.</span><span class="sxs-lookup"><span data-stu-id="5079e-124">hello value of hello metric at a particular point is aggregated over hello preceding sampling interval.</span></span>

<span data-ttu-id="5079e-125">intervalo de muestreo de Hola o "granularidad" se muestra en la parte superior de Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="5079e-125">hello sampling interval or "granularity" is shown at hello top of hello blade.</span></span>

![encabezado de Hola de una hoja.](./media/app-insights-metrics-explorer/11-grain.png)

<span data-ttu-id="5079e-127">Puede ajustar la granularidad de hello en la hoja de intervalo de tiempo de hello:</span><span class="sxs-lookup"><span data-stu-id="5079e-127">You can adjust hello granularity in hello Time range blade:</span></span>

![encabezado de Hola de una hoja.](./media/app-insights-metrics-explorer/grain.png)

<span data-ttu-id="5079e-129">granularidades Hola disponibles dependen de intervalo de tiempo de Hola que seleccione.</span><span class="sxs-lookup"><span data-stu-id="5079e-129">hello granularities available depend on hello time range you select.</span></span> <span data-ttu-id="5079e-130">granularidades explícita Hola son toohello "automático" granularidad de alternativas para el intervalo de tiempo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5079e-130">hello explicit granularities are alternatives toohello "automatic" granularity for hello time range.</span></span>


## <a name="editing-charts-and-grids"></a><span data-ttu-id="5079e-131">Edición de gráficos y cuadrículas</span><span class="sxs-lookup"><span data-stu-id="5079e-131">Editing charts and grids</span></span>
<span data-ttu-id="5079e-132">tooadd una nueva hoja de gráfico toohello:</span><span class="sxs-lookup"><span data-stu-id="5079e-132">tooadd a new chart toohello blade:</span></span>

![En el Explorador de métricas, elija Agregar gráfico](./media/app-insights-metrics-explorer/04-add.png)

<span data-ttu-id="5079e-134">Seleccione **editar** en un tooedit de gráfico nuevo o existente lo que muestra:</span><span class="sxs-lookup"><span data-stu-id="5079e-134">Select **Edit** on an existing or new chart tooedit what it shows:</span></span>

![Seleccionar una o más métricas](./media/app-insights-metrics-explorer/08-select.png)

<span data-ttu-id="5079e-136">Puede mostrar más de una métrica en un gráfico, aunque hay restricciones sobre las combinaciones de Hola que se pueden mostrar juntos.</span><span class="sxs-lookup"><span data-stu-id="5079e-136">You can display more than one metric on a chart, though there are restrictions about hello combinations that can be displayed together.</span></span> <span data-ttu-id="5079e-137">En cuanto elija una métrica, algunos de hello que otros están deshabilitados.</span><span class="sxs-lookup"><span data-stu-id="5079e-137">As soon as you choose one metric, some of hello others are disabled.</span></span>

<span data-ttu-id="5079e-138">Si se codificó [métricas personalizadas] [ track] en la aplicación (llamadas tooTrackMetric y TrackEvent) se mostrarán aquí.</span><span class="sxs-lookup"><span data-stu-id="5079e-138">If you coded [custom metrics][track] into your app (calls tooTrackMetric and TrackEvent) they will be listed here.</span></span>

## <a name="segment-your-data"></a><span data-ttu-id="5079e-139">Segmentación de los datos</span><span class="sxs-lookup"><span data-stu-id="5079e-139">Segment your data</span></span>
<span data-ttu-id="5079e-140">Puede dividir una métrica al propiedad: por ejemplo, toocompare las vistas de página en los clientes con sistemas operativos diferentes.</span><span class="sxs-lookup"><span data-stu-id="5079e-140">You can split a metric by property - for example, toocompare page views on clients with different operating systems.</span></span>

<span data-ttu-id="5079e-141">Seleccione un diagrama o cuadrícula, cambie de agrupación y elegir un toogroup de propiedad por:</span><span class="sxs-lookup"><span data-stu-id="5079e-141">Select a chart or grid, switch on grouping and pick a property toogroup by:</span></span>

![Seleccionar Agrupación en, seleccione una propiedad en Agrupar por](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> <span data-ttu-id="5079e-143">Cuando se usa la agrupación, tipos de gráfico de barras y de área de hello proporcionan una presentación apilada.</span><span class="sxs-lookup"><span data-stu-id="5079e-143">When you use grouping, hello Area and Bar chart types provide a stacked display.</span></span> <span data-ttu-id="5079e-144">Esto es conveniente donde el método de agregación de hello es suma.</span><span class="sxs-lookup"><span data-stu-id="5079e-144">This is suitable where hello Aggregation method is Sum.</span></span> <span data-ttu-id="5079e-145">Pero en su tipo de agregación de hello es promedio, elegir los tipos de pantalla de línea o una cuadrícula de Hola.</span><span class="sxs-lookup"><span data-stu-id="5079e-145">But where hello aggregation type is Average, choose hello Line or Grid display types.</span></span>
>
>

<span data-ttu-id="5079e-146">Si se codificó [métricas personalizadas] [ track] en su aplicación e incluyen los valores de propiedad, podrá tooselect capaz de propiedad de hello en lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="5079e-146">If you coded [custom metrics][track] into your app and they include property values, you'll be able tooselect hello property in hello list.</span></span>

<span data-ttu-id="5079e-147">¿Es demasiado pequeño para los datos segmentados gráfico Hola?</span><span class="sxs-lookup"><span data-stu-id="5079e-147">Is hello chart too small for segmented data?</span></span> <span data-ttu-id="5079e-148">Ajuste el alto:</span><span class="sxs-lookup"><span data-stu-id="5079e-148">Adjust its height:</span></span>

![Ajustar el control deslizante de Hola](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a><span data-ttu-id="5079e-150">Tipos de agregación</span><span class="sxs-lookup"><span data-stu-id="5079e-150">Aggregation types</span></span>
<span data-ttu-id="5079e-151">leyenda de Hello en el lado de Hola de forma predeterminada muestra normalmente Hola agregado valor período de Hola de gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="5079e-151">hello legend at hello side by default usually shows hello aggregated value over hello period of hello chart.</span></span> <span data-ttu-id="5079e-152">Si mantiene el mouse sobre el gráfico de hello, muestra el valor de hello en ese momento.</span><span class="sxs-lookup"><span data-stu-id="5079e-152">If you hover over hello chart, it shows hello value at that point.</span></span>

<span data-ttu-id="5079e-153">Cada punto de datos en el gráfico de hello es un agregado Hola de valores de datos recibidos en hello anterior "granularidad" o intervalo de muestreo.</span><span class="sxs-lookup"><span data-stu-id="5079e-153">Each data point on hello chart is an aggregate of hello data values received in hello preceding sampling interval or "granularity".</span></span> <span data-ttu-id="5079e-154">granularidad de Hola se muestra en la parte superior de Hola de hoja de Hola y varía en función de hello escala temporal global del gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="5079e-154">hello granularity is shown at hello top of hello blade, and varies with hello overall timescale of hello chart.</span></span>

<span data-ttu-id="5079e-155">Se agregan métricas diferentes de distintas maneras:</span><span class="sxs-lookup"><span data-stu-id="5079e-155">Metrics can be aggregated in different ways:</span></span>

* <span data-ttu-id="5079e-156">**Recuento de** es un recuento de eventos de hello recibidos en el intervalo de muestreo de saludo.</span><span class="sxs-lookup"><span data-stu-id="5079e-156">**Count** is a count of hello events received in hello sampling interval.</span></span> <span data-ttu-id="5079e-157">Se usa para eventos como las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="5079e-157">It is used for events such as requests.</span></span> <span data-ttu-id="5079e-158">Variaciones en el alto de Hola de hello gráfico indica las variaciones de tasa de hello en el que se producen eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5079e-158">Variations in hello height of hello chart indicates variations in hello rate at which hello events occur.</span></span> <span data-ttu-id="5079e-159">Pero tenga en cuenta que el valor numérico de Hola cambia cuando se cambia el intervalo de muestreo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5079e-159">But note that hello numeric value changes when you change hello sampling interval.</span></span>
* <span data-ttu-id="5079e-160">**Suma** suma los valores de hello de todos los puntos de datos de hello recibidos a través de intervalo de muestreo de hello, o un período de hello del gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="5079e-160">**Sum** adds up hello values of all hello data points received over hello sampling interval, or hello period of hello chart.</span></span>
* <span data-ttu-id="5079e-161">**Promedio** divide Hola suma por número de Hola de puntos de datos recibidos a través de intervalo de saludo.</span><span class="sxs-lookup"><span data-stu-id="5079e-161">**Average** divides hello Sum by hello number of data points received over hello interval.</span></span>
* <span data-ttu-id="5079e-162">**únicos** se usan para los recuentos de usuarios y cuentas.</span><span class="sxs-lookup"><span data-stu-id="5079e-162">**Unique** counts are used for counts of users and accounts.</span></span> <span data-ttu-id="5079e-163">En el intervalo de muestreo de Hola o durante el período de hello del gráfico de hello, figura hello muestra el recuento de Hola de distintos usuarios que ve en ese momento.</span><span class="sxs-lookup"><span data-stu-id="5079e-163">Over hello sampling interval, or over hello period of hello chart, hello figure shows hello count of different users seen in that time.</span></span>
* <span data-ttu-id="5079e-164">**%**: solo se usan versiones porcentuales de cada agregación con gráficos segmentados.</span><span class="sxs-lookup"><span data-stu-id="5079e-164">**%** - percentage versions of each aggregation are used only with segmented charts.</span></span> <span data-ttu-id="5079e-165">Hola total siempre agrega too100% y gráfico de hello muestra la contribución relativa de Hola de diferentes componentes de un total.</span><span class="sxs-lookup"><span data-stu-id="5079e-165">hello total always adds up too100%, and hello chart shows hello relative contribution of different components of a total.</span></span>

    ![Agregación porcentual](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-hello-aggregation-type"></a><span data-ttu-id="5079e-167">Cambiar el tipo de agregación de Hola</span><span class="sxs-lookup"><span data-stu-id="5079e-167">Change hello aggregation type</span></span>

![Editar gráfico de hello y, a continuación, seleccione agregación](./media/app-insights-metrics-explorer/05-aggregation.png)

<span data-ttu-id="5079e-169">método de Hello predeterminado para cada métrica se muestra cuando se crea un nuevo gráfico o cuando se anula la selección de todas las métricas:</span><span class="sxs-lookup"><span data-stu-id="5079e-169">hello default method for each metric is shown when you create a new chart or when all metrics are deselected:</span></span>

![Anule la selección de todos los valores predeterminados de Hola de toosee de métricas](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a><span data-ttu-id="5079e-171">Anclado del eje Y</span><span class="sxs-lookup"><span data-stu-id="5079e-171">Pin Y-axis</span></span> 
<span data-ttu-id="5079e-172">De forma predeterminada un gráfico muestra los valores de eje empezando desde cero hasta valores máximos de rango de datos de hello, toogive una representación visual de quantum de valores de hello.</span><span class="sxs-lookup"><span data-stu-id="5079e-172">By default a chart shows Y axis values starting from zero till maximum values in hello data range, toogive a visual representation of quantum of hello values.</span></span> <span data-ttu-id="5079e-173">Pero en algunos casos más de quantum Hola podría ser interesante toovisually inspeccionar cambios menores en valores.</span><span class="sxs-lookup"><span data-stu-id="5079e-173">But in some cases more than hello quantum it might be interesting toovisually inspect minor changes in values.</span></span> <span data-ttu-id="5079e-174">Para las personalizaciones como este uso Hola intervalo edición característica toopin Hola eje y mínimo o máximo valor del eje y en el lugar deseado.</span><span class="sxs-lookup"><span data-stu-id="5079e-174">For customizations like this use hello Y-axis range editing feature toopin hello Y-axis minimum or maximum value at desired place.</span></span>
<span data-ttu-id="5079e-175">Haga clic en "Configuración avanzada" casilla de verificación toobring seguridad Hola intervalo del eje y configuración</span><span class="sxs-lookup"><span data-stu-id="5079e-175">Click on "Advanced Settings" check box toobring up hello Y-axis range Settings</span></span>

![Haga clic en Configuración avanzada, seleccione Intervalo personalizado y especifique los valores máximo y mínimo](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a><span data-ttu-id="5079e-177">Filtrado de los datos</span><span class="sxs-lookup"><span data-stu-id="5079e-177">Filter your data</span></span>
<span data-ttu-id="5079e-178">métricas de hello simplemente toosee para un conjunto de valores de propiedad seleccionado:</span><span class="sxs-lookup"><span data-stu-id="5079e-178">toosee just hello metrics for a selected set of property values:</span></span>

![Hacer clic en Filtro, expanda una propiedad y comprobar algunos valores](./media/app-insights-metrics-explorer/19-filter.png)

<span data-ttu-id="5079e-180">Si no selecciona ningún valor para una propiedad determinada, se Hola igual que la selección de todas ellas: no hay ningún filtro en esa propiedad.</span><span class="sxs-lookup"><span data-stu-id="5079e-180">If you don't select any values for a particular property, it's hello same as selecting them all: there is no filter on that property.</span></span>

<span data-ttu-id="5079e-181">Hola Observe los recuentos de eventos junto a cada valor de propiedad.</span><span class="sxs-lookup"><span data-stu-id="5079e-181">Notice hello counts of events alongside each property value.</span></span> <span data-ttu-id="5079e-182">Al seleccionar valores de una propiedad, Hola cuenta junto con otros valores se ajustan derechos de propiedad.</span><span class="sxs-lookup"><span data-stu-id="5079e-182">When you select values of one property, hello counts alongside other property values are adjusted.</span></span>

<span data-ttu-id="5079e-183">Los filtros aplican los gráficos de hello tooall en una hoja.</span><span class="sxs-lookup"><span data-stu-id="5079e-183">Filters apply tooall hello charts on a blade.</span></span> <span data-ttu-id="5079e-184">Si desea que los gráficos de toodifferent diferentes filtros aplicados, cree y guarde las hojas de métricas diferentes.</span><span class="sxs-lookup"><span data-stu-id="5079e-184">If you want different filters applied toodifferent charts, create and save different metrics blades.</span></span> <span data-ttu-id="5079e-185">Si lo desea, puede anclar gráficos en el panel de toohello módulos diferentes, para que se puedan ver junto a entre sí.</span><span class="sxs-lookup"><span data-stu-id="5079e-185">If you want, you can pin charts from different blades toohello dashboard, so that you can see them alongside each other.</span></span>

### <a name="remove-bot-and-web-test-traffic"></a><span data-ttu-id="5079e-186">Supresión de bots y de tráfico de prueba web</span><span class="sxs-lookup"><span data-stu-id="5079e-186">Remove bot and web test traffic</span></span>
<span data-ttu-id="5079e-187">Usar el filtro de hello **tráfico Real o sintético** y compruebe **Real**.</span><span class="sxs-lookup"><span data-stu-id="5079e-187">Use hello filter **Real or synthetic traffic** and check **Real**.</span></span>

<span data-ttu-id="5079e-188">También puede filtrar por **Origen del tráfico sintético**.</span><span class="sxs-lookup"><span data-stu-id="5079e-188">You can also filter by **Source of synthetic traffic**.</span></span>

### <a name="tooadd-properties-toohello-filter-list"></a><span data-ttu-id="5079e-189">lista de filtros de tooadd propiedades toohello</span><span class="sxs-lookup"><span data-stu-id="5079e-189">tooadd properties toohello filter list</span></span>
<span data-ttu-id="5079e-190">¿Le gustaría toofilter telemetría en una categoría de su elección?</span><span class="sxs-lookup"><span data-stu-id="5079e-190">Would you like toofilter telemetry on a category of your own choosing?</span></span> <span data-ttu-id="5079e-191">Por ejemplo, quizás divida los usuarios en distintas categorías y quiera segmentar los datos por estas categorías.</span><span class="sxs-lookup"><span data-stu-id="5079e-191">For example, maybe you divide up your users into different categories, and you would like segment your data by these categories.</span></span>

<span data-ttu-id="5079e-192">[Cree su propia propiedad](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="5079e-192">[Create your own property](app-insights-api-custom-events-metrics.md#properties).</span></span> <span data-ttu-id="5079e-193">Establézcalo un [telemetría inicializador](app-insights-api-custom-events-metrics.md#defaults) toohave aparecen en todos los telemetría - incluidos telemetría estándar Hola envían por módulos diferentes de SDK.</span><span class="sxs-lookup"><span data-stu-id="5079e-193">Set it in a [Telemetry Initializer](app-insights-api-custom-events-metrics.md#defaults) toohave it appear in all telemetry - including hello standard telemetry sent by different SDK modules.</span></span>

## <a name="edit-hello-chart-type"></a><span data-ttu-id="5079e-194">Editar el tipo de gráfico de Hola</span><span class="sxs-lookup"><span data-stu-id="5079e-194">Edit hello chart type</span></span>
<span data-ttu-id="5079e-195">Observe que puede cambiar entre cuadrículas y gráficos:</span><span class="sxs-lookup"><span data-stu-id="5079e-195">Notice that you can switch between grids and graphs:</span></span>

![Seleccionar una cuadrícula o gráfico y elegir un tipo de gráfico](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a><span data-ttu-id="5079e-197">Almacenamiento de la hoja de métricas</span><span class="sxs-lookup"><span data-stu-id="5079e-197">Save your metrics blade</span></span>
<span data-ttu-id="5079e-198">Cuando haya creado algunos gráficos, guárdelos como favorito.</span><span class="sxs-lookup"><span data-stu-id="5079e-198">When you've created some charts, save them as a favorite.</span></span> <span data-ttu-id="5079e-199">Puede elegir si tooshare con otros miembros del equipo, si utiliza una cuenta profesional.</span><span class="sxs-lookup"><span data-stu-id="5079e-199">You can choose whether tooshare it with other team members, if you use an organizational account.</span></span>

![Elegir un favorito](./media/app-insights-metrics-explorer/21-favorite-save.png)

<span data-ttu-id="5079e-201">nuevo, la hoja de Hola de toosee **hoja de información general de toohello vaya** y abrir favoritos:</span><span class="sxs-lookup"><span data-stu-id="5079e-201">toosee hello blade again, **go toohello overview blade** and open Favorites:</span></span>

![En la hoja de información general de hello, elija Favoritos](./media/app-insights-metrics-explorer/22-favorite-get.png)

<span data-ttu-id="5079e-203">Si opta por intervalo de tiempo relativo al guardar, hoja de Hola se actualizará con las métricas de hello más recientes.</span><span class="sxs-lookup"><span data-stu-id="5079e-203">If you chose Relative time range when you saved, hello blade will be updated with hello latest metrics.</span></span> <span data-ttu-id="5079e-204">Si opta por intervalo de tiempo absoluto, aparecerá Hola los mismos datos cada vez.</span><span class="sxs-lookup"><span data-stu-id="5079e-204">If you chose Absolute time range, it will show hello same data every time.</span></span>

## <a name="reset-hello-blade"></a><span data-ttu-id="5079e-205">Restablecimiento de hello hoja</span><span class="sxs-lookup"><span data-stu-id="5079e-205">Reset hello blade</span></span>
<span data-ttu-id="5079e-206">Si edita una hoja pero, a continuación, le gustaría tener tooget atrás toohello original guardan conjunto, haga clic en Restablecer.</span><span class="sxs-lookup"><span data-stu-id="5079e-206">If you edit a blade but then you'd like tooget back toohello original saved set, just click Reset.</span></span>

![En los botones de hello en parte superior de hello del explorador de métrica](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a><span data-ttu-id="5079e-208">Live Metrics Stream</span><span class="sxs-lookup"><span data-stu-id="5079e-208">Live metrics stream</span></span>

<span data-ttu-id="5079e-209">Para obtener una vista mucho más inmediata de la telemetría, abra [Live Stream](app-insights-live-stream.md).</span><span class="sxs-lookup"><span data-stu-id="5079e-209">For a much more immediate view of your telemetry, open [Live Stream](app-insights-live-stream.md).</span></span> <span data-ttu-id="5079e-210">La mayoría de las métricas tardar tooappear unos minutos, a causa de proceso de Hola de agregación.</span><span class="sxs-lookup"><span data-stu-id="5079e-210">Most metrics take a few minutes tooappear, because of hello process of aggregation.</span></span> <span data-ttu-id="5079e-211">Por el contrario, las métricas activas están optimizadas para conseguir una latencia baja.</span><span class="sxs-lookup"><span data-stu-id="5079e-211">By contrast, live metrics are optimized for low latency.</span></span> 

## <a name="set-alerts"></a><span data-ttu-id="5079e-212">Establecer alertas</span><span class="sxs-lookup"><span data-stu-id="5079e-212">Set alerts</span></span>
<span data-ttu-id="5079e-213">toobe una notificación por correo electrónico de los valores inusuales de cualquier métrica, agregar una alerta.</span><span class="sxs-lookup"><span data-stu-id="5079e-213">toobe notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="5079e-214">Puede elegir los administradores de cuentas de toosend Hola correo electrónico toohello o direcciones de correo electrónico toospecific.</span><span class="sxs-lookup"><span data-stu-id="5079e-214">You can choose either toosend hello email toohello account administrators, or toospecific email addresses.</span></span>

![En el Explorador de métricas, elija Reglas de alertas, Agregar alerta](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

<span data-ttu-id="5079e-216">[Obtenga más información sobre alertas][alerts].</span><span class="sxs-lookup"><span data-stu-id="5079e-216">[Learn more about alerts][alerts].</span></span>


## <a name="continuous-export"></a><span data-ttu-id="5079e-217">Exportación continua</span><span class="sxs-lookup"><span data-stu-id="5079e-217">Continuous Export</span></span>
<span data-ttu-id="5079e-218">Si quiere que los datos se exporten continuamente para procesarlos externamente, puede usar la [Exportación continua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="5079e-218">If you want data continuously exported so that you can process it externally, consider using [Continuous export](app-insights-export-telemetry.md).</span></span>

### <a name="power-bi"></a><span data-ttu-id="5079e-219">Power BI</span><span class="sxs-lookup"><span data-stu-id="5079e-219">Power BI</span></span>
<span data-ttu-id="5079e-220">Si desea que las vistas incluso más completa de los datos, puede [exportar tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span><span class="sxs-lookup"><span data-stu-id="5079e-220">If you want even richer views of your data, you can [export tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span></span>

## <a name="analytics"></a><span data-ttu-id="5079e-221">Análisis</span><span class="sxs-lookup"><span data-stu-id="5079e-221">Analytics</span></span>
<span data-ttu-id="5079e-222">[Análisis de](app-insights-analytics.md) es un tooanalyze de manera más versátil la telemetría mediante un lenguaje de consulta eficaces.</span><span class="sxs-lookup"><span data-stu-id="5079e-222">[Analytics](app-insights-analytics.md) is a more versatile way tooanalyze your telemetry using a powerful query language.</span></span> <span data-ttu-id="5079e-223">Utilícelo si desea toocombine o los resultados de las métricas de proceso o realizar una exploración exhaustiva de rendimiento reciente de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5079e-223">Use it if you want toocombine or compute results from metrics, or perform an in-depth exploration of your app's recent performance.</span></span> 

<span data-ttu-id="5079e-224">En un gráfico de métricas, puede hacer clic en hello análisis icono tooget directamente toohello equivalente consulta de análisis.</span><span class="sxs-lookup"><span data-stu-id="5079e-224">From a metric chart, you can click hello Analytics icon tooget directly toohello equivalent Analytics query.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5079e-225">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="5079e-225">Troubleshooting</span></span>
<span data-ttu-id="5079e-226">*No veo ningún dato en el gráfico.*</span><span class="sxs-lookup"><span data-stu-id="5079e-226">*I don't see any data on my chart.*</span></span>

* <span data-ttu-id="5079e-227">Los filtros aplican los gráficos de hello tooall en hoja Hola.</span><span class="sxs-lookup"><span data-stu-id="5079e-227">Filters apply tooall hello charts on hello blade.</span></span> <span data-ttu-id="5079e-228">Asegúrese de que, mientras que desea concentrarse en un gráfico, no ha configurado un filtro que excluye todos los datos de hello en otro.</span><span class="sxs-lookup"><span data-stu-id="5079e-228">Make sure that, while you're focusing on one chart, you didn't set a filter that excludes all hello data on another.</span></span>

    <span data-ttu-id="5079e-229">Si desea tooset filtros diferentes en distintos gráficos, crearlos en módulos diferentes, guárdelos independientes como favoritos.</span><span class="sxs-lookup"><span data-stu-id="5079e-229">If you want tooset different filters on different charts, create them in different blades, save them as separate favorites.</span></span> <span data-ttu-id="5079e-230">Si lo desea, puede anclarlos toohello panel para que se puedan ver junto a entre sí.</span><span class="sxs-lookup"><span data-stu-id="5079e-230">If you want, you can pin them toohello dashboard so that you can see them alongside each other.</span></span>
* <span data-ttu-id="5079e-231">Si un gráfico se agrupa por una propiedad que no está definida en la métrica de hello, a continuación, habrá nada en el gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="5079e-231">If you group a chart by a property that is not defined on hello metric, then there will be nothing on hello chart.</span></span> <span data-ttu-id="5079e-232">Intente borrar "Agrupar por" o elija una propiedad de agrupación diferente.</span><span class="sxs-lookup"><span data-stu-id="5079e-232">Try clearing 'group by', or choose a different grouping property.</span></span>
* <span data-ttu-id="5079e-233">Los datos de rendimiento (CPU, velocidad de E/S, etc.) están disponibles para servicios web de Java, aplicaciones de escritorio de Windows, [servicios y aplicaciones web IIS si instala el Monitor de estado](app-insights-monitor-performance-live-website-now.md) y [Azure Cloud Services](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="5079e-233">Performance data (CPU, IO rate, and so on) is available for Java web services, Windows desktop apps, [IIS web apps and services if you install status monitor](app-insights-monitor-performance-live-website-now.md), and [Azure Cloud Services](app-insights-azure.md).</span></span> <span data-ttu-id="5079e-234">No están disponible para los sitios web de Azure.</span><span class="sxs-lookup"><span data-stu-id="5079e-234">It isn't available for Azure websites.</span></span>

## <a name="video"></a><span data-ttu-id="5079e-235">Vídeo</span><span class="sxs-lookup"><span data-stu-id="5079e-235">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="5079e-236">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5079e-236">Next steps</span></span>
* [<span data-ttu-id="5079e-237">Supervisión del uso con Application Insights</span><span class="sxs-lookup"><span data-stu-id="5079e-237">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="5079e-238">Uso de la Búsqueda de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="5079e-238">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
