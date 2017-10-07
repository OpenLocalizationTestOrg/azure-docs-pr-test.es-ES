---
title: "diagnóstico de aaaSmart de cambios de rendimiento de aplicaciones web en Azure Application Insights | Documentos de Microsoft"
description: "Diagnóstico automático de subidas o pasos en la telemetría de rendimiento desde la aplicación web."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: cfreeman
ms.openlocfilehash: 8891762c4a4bfdb08b647fe3b702349eb30ec9c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a><span data-ttu-id="1053f-103">Diagnóstico de los cambios repentinos en la telemetría de aplicación</span><span class="sxs-lookup"><span data-stu-id="1053f-103">Diagnose sudden changes in your app telemetry</span></span>

<span data-ttu-id="1053f-104">*Esta característica se encuentra en versión preliminar.*</span><span class="sxs-lookup"><span data-stu-id="1053f-104">*This feature is in preview.*</span></span>

<span data-ttu-id="1053f-105">Diagnostique los cambios repentinos en el rendimiento o el uso de la aplicación web con un simple clic.</span><span class="sxs-lookup"><span data-stu-id="1053f-105">Diagnose sudden changes in your web app’s performance or usage with a single click!</span></span> <span data-ttu-id="1053f-106">característica de diagnóstico inteligente de Hello está disponible siempre que cree un gráfico de tiempo en [análisis](app-insights-analytics.md) en [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1053f-106">hello Smart Diagnostics feature is available whenever you create a time chart in [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="1053f-107">Siempre que hay un cambio inusual de tendencia de Hola de los resultados, como un pico o una dip, diagnósticos inteligentes identifica un patrón de dimensiones y los valores relacionados que puedan explicar los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="1053f-107">Wherever there is an unusual change from hello trend of your results, such as a spike or a dip, Smart Diagnostics identifies a pattern of dimensions and related values that might explain hello change.</span></span> <span data-ttu-id="1053f-108">Esto ayuda a diagnosticar el problema de hello rápidamente.</span><span class="sxs-lookup"><span data-stu-id="1053f-108">This helps you diagnose hello problem quickly.</span></span> 

<span data-ttu-id="1053f-109">En este ejemplo, diagnósticos inteligentes ha identificado un patrón de los valores de propiedad asociado con el cambio de Hola y pone de manifiesto Hola diferencia entre los resultados con y sin que ese modelo:</span><span class="sxs-lookup"><span data-stu-id="1053f-109">In this example, Smart Diagnostics has identified a pattern of property values associated with hello change, and highlights hello difference between results with and without that pattern:</span></span>

![resultados de diagnóstico de análisis de ejemplo](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a><span data-ttu-id="1053f-111">Diagnóstico de cambios en los datos</span><span class="sxs-lookup"><span data-stu-id="1053f-111">Diagnose data changes</span></span>

1.  <span data-ttu-id="1053f-112">Ejecute una consulta en Analytics y represéntela como un gráfico de tiempo.</span><span class="sxs-lookup"><span data-stu-id="1053f-112">Run a query in Analytics, and render it as a time chart.</span></span> 
2.  <span data-ttu-id="1053f-113">Haga clic en cualquier punto de subida resaltado, si lo hay.</span><span class="sxs-lookup"><span data-stu-id="1053f-113">Click any highlighted peak point, if there is one.</span></span>
 
    ![punto de subida](./media/app-insights-analytics-diagnostics/peak.png)

    <span data-ttu-id="1053f-115">Diagnóstico tarda unos segundos toodiscover un patrón.</span><span class="sxs-lookup"><span data-stu-id="1053f-115">Diagnostics takes a few seconds toodiscover a pattern.</span></span>

3. <span data-ttu-id="1053f-116">pestaña de resultados de diagnóstico de Hello muestra un patrón que puedan explicar la discontinuidad de datos.</span><span class="sxs-lookup"><span data-stu-id="1053f-116">hello Diagnostics Results tab shows a pattern which may explain your data discontinuity.</span></span>

    ![result](./media/app-insights-analytics-diagnostics/result.png)
 
    <span data-ttu-id="1053f-118">texto Hello muestra valores de la dimensión de Hola que aparecen toocorrelate con desplazamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="1053f-118">hello text shows hello dimension values that appear toocorrelate with hello shift.</span></span> <span data-ttu-id="1053f-119">En este ejemplo, está asociado a una solicitud determinada y una versión de explorador determinado.</span><span class="sxs-lookup"><span data-stu-id="1053f-119">In this example, it’s associated with a particular request and a particular browser version.</span></span>

    <span data-ttu-id="1053f-120">Tenga en cuenta también los componentes de hello dos del gráfico de hello, con hello filtro true y false.</span><span class="sxs-lookup"><span data-stu-id="1053f-120">Notice also hello two components of hello chart, with hello filter true and false.</span></span> <span data-ttu-id="1053f-121">componente false Hello muestra una tendencia sin cambios.</span><span class="sxs-lookup"><span data-stu-id="1053f-121">hello false component shows an unchanged trend.</span></span> <span data-ttu-id="1053f-122">En otras palabras, no hay ningún cambio en los resultados de telemetría de hello, si se excluye la combinación problemático de Hola de dimensiones que ha identificado los diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="1053f-122">In other words, there is no change in hello telemetry results, if we exclude hello problematic combination of dimensions that Diagnostics has identified.</span></span> <span data-ttu-id="1053f-123">Por el contrario, los resultados de hello dentro de esa combinación muestran un cambio significativo en área de hello resaltado de investigación.</span><span class="sxs-lookup"><span data-stu-id="1053f-123">By contrast, hello results within that combination do show a dramatic change within hello highlighted area of investigation.</span></span> <span data-ttu-id="1053f-124">Esto muestra que diagnósticos ha encontrado una combinación de propiedades que explica el cambio de Hola.</span><span class="sxs-lookup"><span data-stu-id="1053f-124">This shows that Diagnostics has found a combination of properties that explains hello change.</span></span>

4.  <span data-ttu-id="1053f-125">Si el patrón de hello es complejo, necesitará toohover sobre **mostrar todo** dimensiones de hello toosee.</span><span class="sxs-lookup"><span data-stu-id="1053f-125">If hello pattern is complex, you need toohover over **Show all** toosee hello dimensions.</span></span>

    ![mostrar todo](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  <span data-ttu-id="1053f-127">En caso de diagnósticos no buscan ningún toonotify patrón significativo sobre Hola que se mostrará la página 'sin resultados'.</span><span class="sxs-lookup"><span data-stu-id="1053f-127">In case Diagnostics finds no significant pattern toonotify about, hello ‘no results’ page will be presented.</span></span> <span data-ttu-id="1053f-128">En este momento, puede cambiar la consulta.</span><span class="sxs-lookup"><span data-stu-id="1053f-128">At this point, you may change your query.</span></span> <span data-ttu-id="1053f-129">Por ejemplo, podría restringir el intervalo de tiempo de Hola y de discretización de consulta de análisis, para un análisis posterior y potencialmente mejores resultados.</span><span class="sxs-lookup"><span data-stu-id="1053f-129">For example, you could narrow hello time range and binning in Analytics query, for a further analysis and potentially better results.</span></span>

<span data-ttu-id="1053f-130">Gracias a que una página concreta de su sitio Web tiene un problema en un explorador determinado de conocimiento de hello, ahora puede ir a página de problema toohello recta e investigar los cambios recientes.</span><span class="sxs-lookup"><span data-stu-id="1053f-130">Armed with hello knowledge that a particular page of your website has a problem on a particular browser, you can now go straight toohello problem page, and investigate recent changes.</span></span>

## <a name="try-hello-demo"></a><span data-ttu-id="1053f-131">Pruebe Hola demostración</span><span class="sxs-lookup"><span data-stu-id="1053f-131">Try hello demo</span></span>

<span data-ttu-id="1053f-132">[Haga clic aquí toosee una demostración](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1053f-132">[Click here toosee a demonstration](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) on sample data.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="1053f-133">Cómo funciona</span><span class="sxs-lookup"><span data-stu-id="1053f-133">How it works</span></span>

<span data-ttu-id="1053f-134">Diagnóstico inteligente utiliza un algoritmo de aprendizaje automático supervisados avanzada basado en hello [DiffPatterns](app-insights-analytics-reference.md) operación.</span><span class="sxs-lookup"><span data-stu-id="1053f-134">Smart Diagnostics uses an advanced unsupervised machine learning algorithm based on hello [DiffPatterns](app-insights-analytics-reference.md) operation.</span></span> <span data-ttu-id="1053f-135">Busca patrones de los candidatos que puedan explicar los cambios de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1053f-135">It looks for candidate patterns that might explain hello data change.</span></span> <span data-ttu-id="1053f-136">Análisis de impacto de Hola de cada candidato en la métrica de hello y muestra el patrón de Hola que mejor se correlaciona con cambio de Hola.</span><span class="sxs-lookup"><span data-stu-id="1053f-136">It analyses hello impact of each candidate on hello metric, and shows hello pattern that best correlates with hello change.</span></span>

## <a name="no-diagnostic-points"></a><span data-ttu-id="1053f-137">¿No hay puntos de diagnóstico?</span><span class="sxs-lookup"><span data-stu-id="1053f-137">No diagnostic points?</span></span>

<span data-ttu-id="1053f-138">Diagnóstico inteligente sólo funciona cuando se cumple Hola siguiendo criterios:</span><span class="sxs-lookup"><span data-stu-id="1053f-138">Smart Diagnostics only works when hello following criteria are satisfied:</span></span>

 * <span data-ttu-id="1053f-139">La opción Smart Diagnostics está activada.</span><span class="sxs-lookup"><span data-stu-id="1053f-139">Smart Diagnostics setting is switched on.</span></span> <span data-ttu-id="1053f-140">Haga clic en el icono de configuración de hello en el análisis.</span><span class="sxs-lookup"><span data-stu-id="1053f-140">Look under hello Settings icon in Analytics.</span></span>
 * <span data-ttu-id="1053f-141">Hola opción de diagnósticos inteligentes en la configuración de análisis está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="1053f-141">hello Smart Diagnostics option in Analytics settings is selected.</span></span> 
 * <span data-ttu-id="1053f-142">Eje de tiempo: Hola eje x del gráfico de hello debe ser de tipo `datetime`.</span><span class="sxs-lookup"><span data-stu-id="1053f-142">Time axis: hello X-axis of hello chart must be of type `datetime`.</span></span>
 * <span data-ttu-id="1053f-143">Gráfico de líneas o de áreas: Diagnostics solo funciona con estos tipos de gráfico.</span><span class="sxs-lookup"><span data-stu-id="1053f-143">Line or area chart: Diagnostics only works these types of chart.</span></span> <span data-ttu-id="1053f-144">Use `| render timechart` o `| render areachart` al final de saludo de la consulta; o seleccione la línea o un gráfico de áreas del selector de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="1053f-144">Use `| render timechart` or `| render areachart` at hello end of your query; or select Line or Area Chart from hello drop-down selector.</span></span>
 * <span data-ttu-id="1053f-145">Discontinuidad: Debe haber una discontinuidad significativa en los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1053f-145">Discontinuity: There must be a significant discontinuity in hello data.</span></span>
 * <span data-ttu-id="1053f-146">Tooanalyze suficientes puntos.</span><span class="sxs-lookup"><span data-stu-id="1053f-146">Sufficient points tooanalyze.</span></span>
 * <span data-ttu-id="1053f-147">No más de un resumen de cláusula de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="1053f-147">No more than one summarize clause in hello query.</span></span>
 * <span data-ttu-id="1053f-148">Ninguna cláusula del proyecto que contiene una definición de nombre antes de hello resumir cláusula.</span><span class="sxs-lookup"><span data-stu-id="1053f-148">No project clause that contains a name definition before hello summarize clause.</span></span>

 
 ## <a name="related-articles"></a><span data-ttu-id="1053f-149">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="1053f-149">Related articles</span></span>

 * [<span data-ttu-id="1053f-150">Tutorial de Analytics</span><span class="sxs-lookup"><span data-stu-id="1053f-150">Analytics tutorial</span></span>](app-insights-analytics-tour.md)
 * <span data-ttu-id="1053f-151">[Detección de Smart](app-insights-proactive-diagnostics.md) avisa tooperformance problemas automáticamente.</span><span class="sxs-lookup"><span data-stu-id="1053f-151">[Smart detection](app-insights-proactive-diagnostics.md) automatically alerts you tooperformance issues.</span></span>
