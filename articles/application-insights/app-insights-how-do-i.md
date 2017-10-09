---
title: aaaHow puedo... en Azure Application Insights | Documentos de Microsoft
description: P+F en Application Insights.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 48b2b644-92e4-44c3-bc14-068f1bbedd22
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: bwren
ms.openlocfilehash: 89294c3583b7c4e7998143be6d359f2deb3c8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-i--in-application-insights"></a><span data-ttu-id="431a3-103">¿Cómo ... en Application Insights?</span><span class="sxs-lookup"><span data-stu-id="431a3-103">How do I ... in Application Insights?</span></span>
## <a name="get-an-email-when-"></a><span data-ttu-id="431a3-104">Recibir un correo electrónico cuando...</span><span class="sxs-lookup"><span data-stu-id="431a3-104">Get an email when ...</span></span>
### <a name="email-if-my-site-goes-down"></a><span data-ttu-id="431a3-105">Enviar un correo electrónico si mi sitio deja de funcionar</span><span class="sxs-lookup"><span data-stu-id="431a3-105">Email if my site goes down</span></span>
<span data-ttu-id="431a3-106">Establecer una [prueba web de disponibilidad](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="431a3-106">Set an [availability web test](app-insights-monitor-web-app-availability.md).</span></span>

### <a name="email-if-my-site-is-overloaded"></a><span data-ttu-id="431a3-107">Enviar un correo electrónico si mi sitio está sobrecargado</span><span class="sxs-lookup"><span data-stu-id="431a3-107">Email if my site is overloaded</span></span>
<span data-ttu-id="431a3-108">Establecer una [alerta](app-insights-alerts.md) en **Tiempo de respuesta del servidor**.</span><span class="sxs-lookup"><span data-stu-id="431a3-108">Set an [alert](app-insights-alerts.md) on **Server response time**.</span></span> <span data-ttu-id="431a3-109">Un umbral entre 1 y 2 segundos debería funcionar.</span><span class="sxs-lookup"><span data-stu-id="431a3-109">A threshold between 1 and 2 seconds should work.</span></span>

![](./media/app-insights-how-do-i/030-server.png)

<span data-ttu-id="431a3-110">La aplicación también podría mostrar señales de esfuerzo al devolver códigos de error.</span><span class="sxs-lookup"><span data-stu-id="431a3-110">Your app might also show signs of strain by returning failure codes.</span></span> <span data-ttu-id="431a3-111">Establezca una alerta en **Solicitudes con error**.</span><span class="sxs-lookup"><span data-stu-id="431a3-111">Set an alert on **Failed requests**.</span></span>

<span data-ttu-id="431a3-112">Si desea tooset una alerta en **excepciones de servidor**, es posible que tenga toodo [alguna configuración adicional](app-insights-asp-net-exceptions.md) datos de pedidos toosee.</span><span class="sxs-lookup"><span data-stu-id="431a3-112">If you want tooset an alert on **Server exceptions**, you might have toodo [some additional setup](app-insights-asp-net-exceptions.md) in order toosee data.</span></span>

### <a name="email-on-exceptions"></a><span data-ttu-id="431a3-113">Envío de excepciones por correo electrónico</span><span class="sxs-lookup"><span data-stu-id="431a3-113">Email on exceptions</span></span>
1. [<span data-ttu-id="431a3-114">Configurar supervisión de excepciones</span><span class="sxs-lookup"><span data-stu-id="431a3-114">Set up exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
2. <span data-ttu-id="431a3-115">[Establecer una alerta](app-insights-alerts.md) en hello excepción contar métrica</span><span class="sxs-lookup"><span data-stu-id="431a3-115">[Set an alert](app-insights-alerts.md) on hello Exception count metric</span></span>

### <a name="email-on-an-event-in-my-app"></a><span data-ttu-id="431a3-116">Enviar un correo electrónico sobre un evento en mi aplicación</span><span class="sxs-lookup"><span data-stu-id="431a3-116">Email on an event in my app</span></span>
<span data-ttu-id="431a3-117">Supongamos que le gustaría tooget un correo electrónico cuando se produce un evento específico.</span><span class="sxs-lookup"><span data-stu-id="431a3-117">Let's suppose you'd like tooget an email when a specific event occurs.</span></span> <span data-ttu-id="431a3-118">Application Insights no ofrece esta función directamente, pero puede [enviar una alerta cuando una métrica sobrepasa un umbral](app-insights-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="431a3-118">Application Insights doesn't provide this facility directly, but it can [send an alert when a metric crosses a threshold](app-insights-alerts.md).</span></span>

<span data-ttu-id="431a3-119">Las alertas se pueden establecer en [métricas personalizadas](app-insights-api-custom-events-metrics.md#trackmetric), aunque no así los eventos no personalizados.</span><span class="sxs-lookup"><span data-stu-id="431a3-119">Alerts can be set on [custom metrics](app-insights-api-custom-events-metrics.md#trackmetric), though not custom events.</span></span> <span data-ttu-id="431a3-120">Escribir algunas tooincrease código una métrica cuando se produce el evento de hello:</span><span class="sxs-lookup"><span data-stu-id="431a3-120">Write some code tooincrease a metric when hello event occurs:</span></span>

    telemetry.TrackMetric("Alarm", 10);

<span data-ttu-id="431a3-121">o:</span><span class="sxs-lookup"><span data-stu-id="431a3-121">or:</span></span>

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

<span data-ttu-id="431a3-122">Dado que las alertas tienen dos Estados, deberá toosend un valor bajo cuando considere la posibilidad de alerta de hello toohave finalizado:</span><span class="sxs-lookup"><span data-stu-id="431a3-122">Because alerts have two states, you have toosend a low value when you consider hello alert toohave ended:</span></span>

    telemetry.TrackMetric("Alarm", 0.5);

<span data-ttu-id="431a3-123">Crear un gráfico en [explorer métrica](app-insights-metrics-explorer.md) toosee la alarma:</span><span class="sxs-lookup"><span data-stu-id="431a3-123">Create a chart in [metric explorer](app-insights-metrics-explorer.md) toosee your alarm:</span></span>

![](./media/app-insights-how-do-i/010-alarm.png)

<span data-ttu-id="431a3-124">Establecer ahora una alerta toofire cuando métrica Hola supera un valor mid durante un breve período:</span><span class="sxs-lookup"><span data-stu-id="431a3-124">Now set an alert toofire when hello metric goes above a mid value for a short period:</span></span>

![](./media/app-insights-how-do-i/020-threshold.png)

<span data-ttu-id="431a3-125">Establecer Hola promedio toohello período mínimo.</span><span class="sxs-lookup"><span data-stu-id="431a3-125">Set hello averaging period toohello minimum.</span></span>

<span data-ttu-id="431a3-126">Verá mensajes de correo electrónico cuando la métrica de hello está por encima y por debajo del umbral de Hola.</span><span class="sxs-lookup"><span data-stu-id="431a3-126">You'll get emails both when hello metric goes above and below hello threshold.</span></span>

<span data-ttu-id="431a3-127">Algunos tooconsider puntos:</span><span class="sxs-lookup"><span data-stu-id="431a3-127">Some points tooconsider:</span></span>

* <span data-ttu-id="431a3-128">Una alerta tiene dos estados ("alerta" y "correcto").</span><span class="sxs-lookup"><span data-stu-id="431a3-128">An alert has two states ("alert" and "healthy").</span></span> <span data-ttu-id="431a3-129">se evalúa el estado de Hello solo cuando se recibe una métrica.</span><span class="sxs-lookup"><span data-stu-id="431a3-129">hello state is evaluated only when a metric is received.</span></span>
* <span data-ttu-id="431a3-130">Se envía un correo electrónico sólo cuando cambia el estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="431a3-130">An email is sent only when hello state changes.</span></span> <span data-ttu-id="431a3-131">Por lo tanto, tendrá que toosend las métricas de alto y bajo valor.</span><span class="sxs-lookup"><span data-stu-id="431a3-131">This is why you have toosend both high and low-value metrics.</span></span>
* <span data-ttu-id="431a3-132">alerta de hello tooevaluate, promedio de hello queda recogido de valores de hello recibido Hola anterior período.</span><span class="sxs-lookup"><span data-stu-id="431a3-132">tooevaluate hello alert, hello average is taken of hello received values over hello preceding period.</span></span> <span data-ttu-id="431a3-133">Esto se produce cada vez que se recibe una métrica, por lo que los mensajes de correo electrónico pueden enviarse con más frecuencia que establece el período de Hola.</span><span class="sxs-lookup"><span data-stu-id="431a3-133">This occurs every time a metric is received, so emails can be sent more frequently than hello period you set.</span></span>
* <span data-ttu-id="431a3-134">Puesto que se envían correos electrónicos de "alerta" y "correcto", puede ser conveniente tooconsider volver a pensar en el evento Monoestable como una condición de dos Estados.</span><span class="sxs-lookup"><span data-stu-id="431a3-134">Since emails are sent both on "alert" and "healthy", you might want tooconsider re-thinking your one-shot event as a two-state condition.</span></span> <span data-ttu-id="431a3-135">Por ejemplo, en lugar de un evento de "trabajo completado", tiene una condición de "trabajo en curso", donde se obtienen mensajes de correo electrónico en hello inicial y final de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="431a3-135">For example, instead of a "job completed" event, have a "job in progress" condition, where you get emails at hello start and end of a job.</span></span>

### <a name="set-up-alerts-automatically"></a><span data-ttu-id="431a3-136">Configuración de alertas automáticamente</span><span class="sxs-lookup"><span data-stu-id="431a3-136">Set up alerts automatically</span></span>
[<span data-ttu-id="431a3-137">Usar PowerShell toocreate nuevas alertas</span><span class="sxs-lookup"><span data-stu-id="431a3-137">Use PowerShell toocreate new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="use-powershell-toomanage-application-insights"></a><span data-ttu-id="431a3-138">Usar PowerShell tooManage Application Insights</span><span class="sxs-lookup"><span data-stu-id="431a3-138">Use PowerShell tooManage Application Insights</span></span>
* [<span data-ttu-id="431a3-139">Creación de nuevos recursos</span><span class="sxs-lookup"><span data-stu-id="431a3-139">Create new resources</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="431a3-140">Creación de nuevas alertas</span><span class="sxs-lookup"><span data-stu-id="431a3-140">Create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a><span data-ttu-id="431a3-141">Telemetría independiente de diferentes versiones</span><span class="sxs-lookup"><span data-stu-id="431a3-141">Separate telemetry from different versions</span></span>

* <span data-ttu-id="431a3-142">Varios roles en una aplicación: usar un único recurso de Application Insights y filtrar por cloud_NombreDelRol.</span><span class="sxs-lookup"><span data-stu-id="431a3-142">Multiple roles in an app: Use a single Application Insights resource, and filter on cloud_Rolename.</span></span> [<span data-ttu-id="431a3-143">Más información</span><span class="sxs-lookup"><span data-stu-id="431a3-143">Learn more</span></span>](app-insights-monitor-multi-role-apps.md)
* <span data-ttu-id="431a3-144">Separación de versiones de desarrollo, prueba y publicación: utilizar diferentes recursos de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="431a3-144">Separating development, test, and release versions: Use different Application Insights resources.</span></span> <span data-ttu-id="431a3-145">Seleccionar las claves de la instrumentación de Hola de web.config. [Más información](app-insights-separate-resources.md)</span><span class="sxs-lookup"><span data-stu-id="431a3-145">Pick up hello instrumentation keys from web.config. [Learn more](app-insights-separate-resources.md)</span></span>
* <span data-ttu-id="431a3-146">Generación de informes de versiones de compilación: agregar una propiedad usando un inicializador de telemetría.</span><span class="sxs-lookup"><span data-stu-id="431a3-146">Reporting build versions: Add a property using a telemetry initializer.</span></span> [<span data-ttu-id="431a3-147">Más información</span><span class="sxs-lookup"><span data-stu-id="431a3-147">Learn more</span></span>](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a><span data-ttu-id="431a3-148">Supervisar servidores back-end y aplicaciones de escritorio</span><span class="sxs-lookup"><span data-stu-id="431a3-148">Monitor backend servers and desktop apps</span></span>
<span data-ttu-id="431a3-149">[Utilizar el módulo de SDK de Windows Server hello](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="431a3-149">[Use hello Windows Server SDK module](app-insights-windows-desktop.md).</span></span>

## <a name="visualize-data"></a><span data-ttu-id="431a3-150">Visualización de datos</span><span class="sxs-lookup"><span data-stu-id="431a3-150">Visualize data</span></span>
#### <a name="dashboard-with-metrics-from-multiple-apps"></a><span data-ttu-id="431a3-151">Panel con métricas de varias aplicaciones</span><span class="sxs-lookup"><span data-stu-id="431a3-151">Dashboard with metrics from multiple apps</span></span>
* <span data-ttu-id="431a3-152">En el [Explorador de métricas](app-insights-metrics-explorer.md), personalice el gráfico y guárdelo como favorito.</span><span class="sxs-lookup"><span data-stu-id="431a3-152">In [Metric Explorer](app-insights-metrics-explorer.md), customize your chart and save it as a favorite.</span></span> <span data-ttu-id="431a3-153">Puede anclar toohello panel de Azure.</span><span class="sxs-lookup"><span data-stu-id="431a3-153">Pin it toohello Azure dashboard.</span></span>

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a><span data-ttu-id="431a3-154">Panel con datos de otros orígenes y Application Insights</span><span class="sxs-lookup"><span data-stu-id="431a3-154">Dashboard with data from other sources and Application Insights</span></span>
* <span data-ttu-id="431a3-155">[Exportar telemetría tooPower BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="431a3-155">[Export telemetry tooPower BI](app-insights-export-power-bi.md).</span></span>

<span data-ttu-id="431a3-156">O</span><span class="sxs-lookup"><span data-stu-id="431a3-156">Or</span></span>

* <span data-ttu-id="431a3-157">Use SharePoint como panel, mostrando los datos en elementos web de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="431a3-157">Use SharePoint as your dashboard, displaying data in SharePoint web parts.</span></span> <span data-ttu-id="431a3-158">[Usar exportación continua y análisis de transmisiones tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="431a3-158">[Use continuous export and Stream Analytics tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).</span></span>  <span data-ttu-id="431a3-159">Usar base de datos de PowerView tooexamine hello y crear un elemento web de SharePoint para PowerView.</span><span class="sxs-lookup"><span data-stu-id="431a3-159">Use PowerView tooexamine hello database, and create a SharePoint web part for PowerView.</span></span>

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a><span data-ttu-id="431a3-160">Filtrado de usuarios anónimos o autenticados</span><span class="sxs-lookup"><span data-stu-id="431a3-160">Filter out anonymous or authenticated users</span></span>
<span data-ttu-id="431a3-161">Si los usuarios inician sesión, puede establecer hello [autenticado Id. de usuario](app-insights-api-custom-events-metrics.md#authenticated-users). (No ocurre automáticamente).</span><span class="sxs-lookup"><span data-stu-id="431a3-161">If your users sign in, you can set hello [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users). (It doesn't happen automatically.)</span></span>

<span data-ttu-id="431a3-162">A continuación, puede:</span><span class="sxs-lookup"><span data-stu-id="431a3-162">You can then:</span></span>

* <span data-ttu-id="431a3-163">Buscar identificadores de usuario específicos</span><span class="sxs-lookup"><span data-stu-id="431a3-163">Search on specific user ids</span></span>

![](./media/app-insights-how-do-i/110-search.png)

* <span data-ttu-id="431a3-164">Filtrar las métricas tooeither anónimos o autenticados los usuarios</span><span class="sxs-lookup"><span data-stu-id="431a3-164">Filter metrics tooeither anonymous or authenticated users</span></span>

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a><span data-ttu-id="431a3-165">Modificación de valores o nombres de propiedad</span><span class="sxs-lookup"><span data-stu-id="431a3-165">Modify property names or values</span></span>
<span data-ttu-id="431a3-166">Cree un [filtro](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="431a3-166">Create a [filter](app-insights-api-filtering-sampling.md#filtering).</span></span> <span data-ttu-id="431a3-167">Esto le permite modificar o filtrar telemetría antes de que se envíe desde su visión tooApplication de aplicación.</span><span class="sxs-lookup"><span data-stu-id="431a3-167">This lets you modify or filter telemetry before it is sent from your app tooApplication Insights.</span></span>

## <a name="list-specific-users-and-their-usage"></a><span data-ttu-id="431a3-168">Enumeración de usuarios específicos y su uso</span><span class="sxs-lookup"><span data-stu-id="431a3-168">List specific users and their usage</span></span>
<span data-ttu-id="431a3-169">Si su intención es demasiado[buscar usuarios específicos](#search-specific-users), puede establecer hello [autenticado Id. de usuario](app-insights-api-custom-events-metrics.md#authenticated-users).</span><span class="sxs-lookup"><span data-stu-id="431a3-169">If you just want too[search for specific users](#search-specific-users), you can set hello [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users).</span></span>

<span data-ttu-id="431a3-170">Si desea obtener una lista de usuarios con datos como las páginas que ven o la frecuencia con la que inician sesión, tiene dos opciones:</span><span class="sxs-lookup"><span data-stu-id="431a3-170">If you want a list of users with data such as what pages they look at or how often they log in, you have two options:</span></span>

* <span data-ttu-id="431a3-171">[Id. de usuario autenticado de conjunto](app-insights-api-custom-events-metrics.md#authenticated-users), [exportar base de datos de tooa](app-insights-code-sample-export-sql-stream-analytics.md) y uso adecuado de herramientas tooanalyze los datos de usuario no existe.</span><span class="sxs-lookup"><span data-stu-id="431a3-171">[Set authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users), [export tooa database](app-insights-code-sample-export-sql-stream-analytics.md) and use suitable tools tooanalyze your user data there.</span></span>
* <span data-ttu-id="431a3-172">Si tiene sólo un número reducido de usuarios, envíe eventos personalizados o las métricas, con datos de saludo de interés como Hola valor métrico o el nombre de evento y el Id. de usuario de configuración hello como una propiedad.</span><span class="sxs-lookup"><span data-stu-id="431a3-172">If you have only a small number of users, send custom events or metrics, using hello data of interest as hello metric value or event name, and setting hello user id as a property.</span></span> <span data-ttu-id="431a3-173">vistas de página tooanalyze, reemplace las llamadas de trackPageView de JavaScript estándar de Hola.</span><span class="sxs-lookup"><span data-stu-id="431a3-173">tooanalyze page views, replace hello standard JavaScript trackPageView call.</span></span> <span data-ttu-id="431a3-174">telemetría de servidor tooanalyze, usar una telemetría telemetría inicializador tooadd Hola usuario id tooall server.</span><span class="sxs-lookup"><span data-stu-id="431a3-174">tooanalyze server-side telemetry, use a telemetry initializer tooadd hello user id tooall server telemetry.</span></span> <span data-ttu-id="431a3-175">Puede, a continuación, las métricas de filtro y de segmento y búsquedas en el Id. de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="431a3-175">You can then filter and segment metrics and searches on hello user id.</span></span>

## <a name="reduce-traffic-from-my-app-tooapplication-insights"></a><span data-ttu-id="431a3-176">Reducir el tráfico de mi tooApplication de app Insights</span><span class="sxs-lookup"><span data-stu-id="431a3-176">Reduce traffic from my app tooApplication Insights</span></span>
* <span data-ttu-id="431a3-177">En [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), deshabilite los módulos que no es necesario, tal Recopilador del contador de rendimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="431a3-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), disable any modules you don't need, such hello performance counter collector.</span></span>
* <span data-ttu-id="431a3-178">Use [muestreo y filtrado](app-insights-api-filtering-sampling.md) en hello SDK.</span><span class="sxs-lookup"><span data-stu-id="431a3-178">Use [Sampling and filtering](app-insights-api-filtering-sampling.md) at hello SDK.</span></span>
* <span data-ttu-id="431a3-179">En las páginas web, limite el número de Hola de llamadas Ajax notificados para cada vista de página.</span><span class="sxs-lookup"><span data-stu-id="431a3-179">In your web pages, Limit hello number of Ajax calls reported for every page view.</span></span> <span data-ttu-id="431a3-180">En el fragmento de script de Hola después `instrumentationKey:...` , insertar: `,maxAjaxCallsPerView:3` (o un número adecuado).</span><span class="sxs-lookup"><span data-stu-id="431a3-180">In hello script snippet after `instrumentationKey:...` , insert: `,maxAjaxCallsPerView:3` (or a suitable number).</span></span>
* <span data-ttu-id="431a3-181">Si usas [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), agregado Hola de lotes de valores de métrica de proceso antes de enviar el resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="431a3-181">If you're using [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), compute hello aggregate of batches of metric values before sending hello result.</span></span> <span data-ttu-id="431a3-182">Hay una sobrecarga de TrackMetric() que se proporciona para eso.</span><span class="sxs-lookup"><span data-stu-id="431a3-182">There's an overload of TrackMetric() that provides for that.</span></span>

<span data-ttu-id="431a3-183">Obtenga más información sobre [precios y cuotas](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="431a3-183">Learn more about [pricing and quotas](app-insights-pricing.md).</span></span>

## <a name="disable-telemetry"></a><span data-ttu-id="431a3-184">Deshabilitar la telemetría</span><span class="sxs-lookup"><span data-stu-id="431a3-184">Disable telemetry</span></span>
<span data-ttu-id="431a3-185">demasiado**dinámicamente detener e iniciar** Hola recopilación y transmisión de telemetría de servidor hello:</span><span class="sxs-lookup"><span data-stu-id="431a3-185">too**dynamically stop and start** hello collection and transmission of telemetry from hello server:</span></span>

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



<span data-ttu-id="431a3-186">demasiado**deshabilitar los recopiladores estándares seleccionados** : por ejemplo, los contadores de rendimiento, las solicitudes HTTP o dependencias - eliminar o marque como comentario las líneas relevantes de hello en [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). Por ejemplo, podría hacer esto, si desea que toosend sus propios datos TrackRequest.</span><span class="sxs-lookup"><span data-stu-id="431a3-186">too**disable selected standard collectors** - for example, performance counters, HTTP requests, or dependencies - delete or comment out hello relevant lines in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). You could do this, for example, if you want toosend your own TrackRequest data.</span></span>

## <a name="view-system-performance-counters"></a><span data-ttu-id="431a3-187">Visualización de contadores de rendimiento del sistema</span><span class="sxs-lookup"><span data-stu-id="431a3-187">View system performance counters</span></span>
<span data-ttu-id="431a3-188">Entre hello las métricas que puede mostrar en el Explorador de métricas son un conjunto de contadores de rendimiento del sistema.</span><span class="sxs-lookup"><span data-stu-id="431a3-188">Among hello metrics you can show in metrics explorer are a set of system performance counters.</span></span> <span data-ttu-id="431a3-189">Hay una hoja predefinida denominada **Servidores** que muestra varios de ellos.</span><span class="sxs-lookup"><span data-stu-id="431a3-189">There's a predefined blade titled **Servers** that displays several of them.</span></span>

![Abra el recurso de Application Insights y haga clic en Servidores](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a><span data-ttu-id="431a3-191">Si no ve ningún dato de contadores de rendimiento</span><span class="sxs-lookup"><span data-stu-id="431a3-191">If you see no performance counter data</span></span>
* <span data-ttu-id="431a3-192">**servidor IIS** en su propia máquina o en una VM.</span><span class="sxs-lookup"><span data-stu-id="431a3-192">**IIS server** on your own machine or on a VM.</span></span> <span data-ttu-id="431a3-193">[Instale el Monitor de estado](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="431a3-193">[Install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="431a3-194">**Sitio web de Azure** : todavía no se admiten los contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="431a3-194">**Azure web site** - we don't support performance counters yet.</span></span> <span data-ttu-id="431a3-195">Hay varias métricas que se puede obtener como una parte estándar de panel de control de sitio web de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="431a3-195">There are several metrics you can get as a standard part of hello Azure web site control panel.</span></span>
* <span data-ttu-id="431a3-196">**Servidor Unix** - [instale collectd](app-insights-java-collectd.md)</span><span class="sxs-lookup"><span data-stu-id="431a3-196">**Unix server** - [Install collectd](app-insights-java-collectd.md)</span></span>

### <a name="toodisplay-more-performance-counters"></a><span data-ttu-id="431a3-197">toodisplay más contadores de rendimiento</span><span class="sxs-lookup"><span data-stu-id="431a3-197">toodisplay more performance counters</span></span>
* <span data-ttu-id="431a3-198">En primer lugar, [agregar un nuevo gráfico](app-insights-metrics-explorer.md) y vea si hello es Hola básica conjunto de contadores que ofrecemos.</span><span class="sxs-lookup"><span data-stu-id="431a3-198">First, [add a new chart](app-insights-metrics-explorer.md) and see if hello counter is in hello basic set that we offer.</span></span>
* <span data-ttu-id="431a3-199">Si no es así, [Agregar conjunto de toohello de hello contadores recopilado por el módulo del contador de rendimiento de hello](app-insights-performance-counters.md).</span><span class="sxs-lookup"><span data-stu-id="431a3-199">If not, [add hello counter toohello set collected by hello performance counter module](app-insights-performance-counters.md).</span></span>
