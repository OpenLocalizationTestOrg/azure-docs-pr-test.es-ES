---
title: "Muestreo de telemetría en Azure Application Insights | Microsoft Docs"
description: "Cómo mantener el volumen de telemetría bajo control."
services: application-insights
documentationcenter: windows
author: vgorbenko
manager: carmonm
ms.assetid: 015ab744-d514-42c0-8553-8410eef00368
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bwren
ms.openlocfilehash: ceaeced414c9c302fba335b4578bcdcbfaef0410
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="sampling-in-application-insights"></a><span data-ttu-id="36119-103">Muestreo en Application Insights.</span><span class="sxs-lookup"><span data-stu-id="36119-103">Sampling in Application Insights</span></span>


<span data-ttu-id="36119-104">El muestreo es una característica de [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="36119-104">Sampling is a feature in [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="36119-105">Se trata de la manera recomendada de reducir el almacenamiento y el tráfico de telemetría conservando, al mismo tiempo, un análisis estadísticamente correcto de datos de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="36119-105">It is the recommended way to reduce telemetry traffic and storage, while preserving  a statistically correct analysis of application data.</span></span> <span data-ttu-id="36119-106">El filtro selecciona los elementos relacionado para que pueda desplazarse entre los elementos de diagnóstico cuando esté realizando investigaciones de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="36119-106">The filter selects items that are related, so that you can navigate between items when you are doing diagnostic investigations.</span></span>
<span data-ttu-id="36119-107">Cuando los recuentos de métrica se presentan al usuario en el portal, se renormalizan para tener en cuenta el muestreo y minimizar cualquier efecto en las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="36119-107">When metric counts are presented to you in the portal, they are renormalized to take account of the sampling, to minimize any effect on the statistics.</span></span>

<span data-ttu-id="36119-108">El muestreo reduce los costos de tráfico y datos y le ayuda a evitar la limitación.</span><span class="sxs-lookup"><span data-stu-id="36119-108">Sampling reduces traffic and data costs, and helps you avoid throttling.</span></span>

## <a name="in-brief"></a><span data-ttu-id="36119-109">En resumen:</span><span class="sxs-lookup"><span data-stu-id="36119-109">In brief:</span></span>
* <span data-ttu-id="36119-110">Muestreo conserva 1 en  *n*  registra y descarta el resto.</span><span class="sxs-lookup"><span data-stu-id="36119-110">Sampling retains 1 in *n* records and discards the rest.</span></span> <span data-ttu-id="36119-111">Por ejemplo, podría retener los eventos de 1 a 5, una velocidad de muestreo del 20 %.</span><span class="sxs-lookup"><span data-stu-id="36119-111">For example, it might retain 1 in 5 events, a sampling rate of 20%.</span></span> 
* <span data-ttu-id="36119-112">El muestreo se produce automáticamente si la aplicación envía una gran cantidad de telemetría en las aplicaciones de servidor web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="36119-112">Sampling happens automatically if your application sends a lot of telemetry, in ASP.NET web server apps.</span></span>
* <span data-ttu-id="36119-113">También puede establecer el muestreo manualmente, bien en el portal en la página de precios, bien en el SDK de ASP.NET en el archivo .config, también para reducir el tráfico de red.</span><span class="sxs-lookup"><span data-stu-id="36119-113">You can also set sampling manually, either in the portal on the pricing page; or in the ASP.NET SDK in the .config file, to also reduce the network traffic.</span></span>
* <span data-ttu-id="36119-114">Si registra eventos personalizados y desea asegurarse de que un conjunto de eventos se retienen o se descartan juntos, asegúrese de que tengan el mismo valor para OperationId.</span><span class="sxs-lookup"><span data-stu-id="36119-114">If you log custom events and you want to make sure that a set of events is either retained or discarded together, make sure that they have the same OperationId value.</span></span>
* <span data-ttu-id="36119-115">El divisor de muestreo  *n*  se notifica en cada registro de la propiedad `itemCount`, que en la búsqueda aparece bajo el nombre descriptivo "número de solicitudes" o "recuento de eventos".</span><span class="sxs-lookup"><span data-stu-id="36119-115">The sampling divisor *n* is reported in each record in the property `itemCount`, which in Search appears under the friendly name "request count" or "event count".</span></span> <span data-ttu-id="36119-116">Cuando el muestreo no está en funcionamiento, `itemCount==1`.</span><span class="sxs-lookup"><span data-stu-id="36119-116">When sampling is not in operation, `itemCount==1`.</span></span>
* <span data-ttu-id="36119-117">Si escribe consultas de Analytics, debería [tener en cuenta el muestreo](app-insights-analytics-tour.md#counting-sampled-data).</span><span class="sxs-lookup"><span data-stu-id="36119-117">If you write Analytics queries, you should [take account of sampling](app-insights-analytics-tour.md#counting-sampled-data).</span></span> <span data-ttu-id="36119-118">En concreto, en lugar de simplemente contar registros, debería usar `summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="36119-118">In particular, instead of simply counting records, you should use `summarize sum(itemCount)`.</span></span>

## <a name="types-of-sampling"></a><span data-ttu-id="36119-119">Tipos de muestreo</span><span class="sxs-lookup"><span data-stu-id="36119-119">Types of sampling</span></span>
<span data-ttu-id="36119-120">Existen tres métodos de muestreo alternativos:</span><span class="sxs-lookup"><span data-stu-id="36119-120">There are three alternative sampling methods:</span></span>

* <span data-ttu-id="36119-121">**muestreo adaptable** ajusta automáticamente el volumen de telemetría enviado desde el SDK en la aplicación de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="36119-121">**Adaptive sampling** automatically adjusts the volume of telemetry sent from the SDK in your ASP.NET app.</span></span> <span data-ttu-id="36119-122">Valor predeterminado del SDK v 2.0.0-beta3.</span><span class="sxs-lookup"><span data-stu-id="36119-122">Default from SDK v 2.0.0-beta3.</span></span> <span data-ttu-id="36119-123">Actualmente solo está disponible para la telemetría de servidor ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="36119-123">Currently available for ASP.NET server-side telemetry only.</span></span> 
* <span data-ttu-id="36119-124">**muestreo de frecuencia fija** reduce el volumen de telemetría enviado desde el servidor ASP.NET y desde los exploradores de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="36119-124">**Fixed-rate sampling** reduces the volume of telemetry sent from both your ASP.NET server and from your users' browsers.</span></span> <span data-ttu-id="36119-125">El usuario establece la frecuencia.</span><span class="sxs-lookup"><span data-stu-id="36119-125">You set the rate.</span></span> <span data-ttu-id="36119-126">El cliente y el servidor sincronizarán su muestreo por lo que, en Búsqueda, puede desplazarse entre las solicitudes y las vistas de página relacionadas.</span><span class="sxs-lookup"><span data-stu-id="36119-126">The client and server will synchronize their sampling so that, in Search, you can navigate between related page views and requests.</span></span>
* <span data-ttu-id="36119-127">El **muestreo de ingesta** funciona en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="36119-127">**Ingestion sampling** works in the Azure portal.</span></span> <span data-ttu-id="36119-128">Lo que hace es descartar algunos de los datos de telemetría que llegan desde su aplicación según la frecuencia establecida.</span><span class="sxs-lookup"><span data-stu-id="36119-128">It discards some of the telemetry that arrives from your app, at a rate that you set.</span></span> <span data-ttu-id="36119-129">Aunque no reduce el tráfico de telemetría, le ayuda a mantenerse dentro de su cuota mensual.</span><span class="sxs-lookup"><span data-stu-id="36119-129">It doesn't reduce telemetry traffic, but helps you keep within your monthly quota.</span></span> <span data-ttu-id="36119-130">La gran ventaja del muestreo de ingesta es que puede establecerlo sin volver a implementar la aplicación, y funciona de manera uniforme en todos los clientes y servidores.</span><span class="sxs-lookup"><span data-stu-id="36119-130">The big advantage of ingestion sampling is that you can set it without redeploying your app, and it works uniformly for all servers and clients.</span></span> 

<span data-ttu-id="36119-131">Si el muestreo de velocidad adaptable o fija está funcionando, el muestreo de ingesta se deshabilita.</span><span class="sxs-lookup"><span data-stu-id="36119-131">If Adaptive or Fixed rate sampling are in operation, Ingestion sampling is disabled.</span></span>

## <a name="ingestion-sampling"></a><span data-ttu-id="36119-132">muestreo de ingesta</span><span class="sxs-lookup"><span data-stu-id="36119-132">Ingestion sampling</span></span>
<span data-ttu-id="36119-133">Esta forma de muestreo funciona en el punto donde la telemetría de su servidor web, de sus exploradores y de sus dispositivos alcanza el punto de conexión del servicio de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="36119-133">This form of sampling operates at the point where the telemetry from your web server, browsers, and devices reaches the Application Insights service endpoint.</span></span> <span data-ttu-id="36119-134">Aunque no reduce el tráfico de telemetría enviado desde su aplicación, sí reduce la cantidad procesada y retenida (y cobrada) por Application Insights.</span><span class="sxs-lookup"><span data-stu-id="36119-134">Although it doesn't reduce the telemetry traffic sent from your app, it does reduce the amount processed and retained (and charged for) by Application Insights.</span></span>

<span data-ttu-id="36119-135">Utilice este tipo de muestreo si con frecuencia su aplicación sobrepasa su cuota mensual y no tiene la opción de usar ninguno de los tipos de muestreo basados en el SDK.</span><span class="sxs-lookup"><span data-stu-id="36119-135">Use this type of sampling if your app often goes over its monthly quota and you don't have the option of using either of the SDK-based types of sampling.</span></span> 

<span data-ttu-id="36119-136">Establezca la frecuencia de muestreo en la hoja Cuotas y precios:</span><span class="sxs-lookup"><span data-stu-id="36119-136">Set the sampling rate in the Quotas and Pricing blade:</span></span>

![En la hoja Información general de la aplicación, haga clic en Configuración, Cuota, Ejemplos y, luego, seleccione una frecuencia de muestreo y haga clic en Actualizar.](./media/app-insights-sampling/04.png)

<span data-ttu-id="36119-138">Al igual que otros tipos de muestreo, el algoritmo conserva elementos de telemetría relacionados.</span><span class="sxs-lookup"><span data-stu-id="36119-138">Like other types of sampling, the algorithm retains related telemetry items.</span></span> <span data-ttu-id="36119-139">Por ejemplo, cuando se inspeccione la telemetría en Búsqueda, podrá buscar la solicitud relacionada con una excepción determinada.</span><span class="sxs-lookup"><span data-stu-id="36119-139">For example, when you're inspecting the telemetry in Search, you'll be able to find the request related to a particular exception.</span></span> <span data-ttu-id="36119-140">Los recuentos de métrica, como la tasa de solicitudes y la tasa de excepciones se mantienen correctamente.</span><span class="sxs-lookup"><span data-stu-id="36119-140">Metric counts such as request rate and exception rate are correctly retained.</span></span>

<span data-ttu-id="36119-141">Los puntos de datos que se descartan por muestreo no están disponibles en ninguna característica de Application Insights como [exportación continua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="36119-141">Data points that are discarded by sampling are not available in any Application Insights feature such as [Continuous Export](app-insights-export-telemetry.md).</span></span>

<span data-ttu-id="36119-142">El muestreo de ingesta no funciona mientras el muestreo adaptativo o de frecuencia fija basado en el SDK está en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="36119-142">Ingestion sampling doesn't operate while SDK-based adaptive or fixed-rate sampling is in operation.</span></span> <span data-ttu-id="36119-143">Si la velocidad de muestreo en el SDK es inferior al 100 %, se omite la velocidad de muestreo de ingesta que haya establecido.</span><span class="sxs-lookup"><span data-stu-id="36119-143">If the sampling rate at the SDK is less than 100%, then the ingestion sampling rate that you set is ignored.</span></span>

> [!WARNING]
> <span data-ttu-id="36119-144">El valor que se muestra en el icono indica el valor que ha establecido para el muestreo de ingesta.</span><span class="sxs-lookup"><span data-stu-id="36119-144">The value shown on the tile indicates the value that you set for ingestion sampling.</span></span> <span data-ttu-id="36119-145">Si el muestreo del SDK está en funcionamiento, no representa la frecuencia real de muestreo.</span><span class="sxs-lookup"><span data-stu-id="36119-145">It doesn't represent the actual sampling rate if SDK sampling is in operation.</span></span>
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a><span data-ttu-id="36119-146">Muestreo adaptable en el servidor web</span><span class="sxs-lookup"><span data-stu-id="36119-146">Adaptive sampling at your web server</span></span>
<span data-ttu-id="36119-147">El muestreo adaptable está disponible para el SDK de Application Insights para ASP.NET v 2.0.0-beta3 y versiones posteriores y está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="36119-147">Adaptive sampling is available for the Application Insights SDK for ASP.NET v 2.0.0-beta3 and later, and is enabled by default.</span></span> 

<span data-ttu-id="36119-148">Influye en el volumen de telemetría enviado desde su aplicación de servidor web hasta el servicio de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="36119-148">Adaptive sampling affects the volume of telemetry sent from your web server app to the Application Insights service.</span></span> <span data-ttu-id="36119-149">El volumen se ajusta automáticamente para mantenerlo dentro de una tasa de tráfico máxima especificada.</span><span class="sxs-lookup"><span data-stu-id="36119-149">The volume is adjusted automatically to keep within a specified maximum rate of traffic.</span></span>

<span data-ttu-id="36119-150">No funciona con volúmenes bajos de telemetría, así que una aplicación en proceso de depuración o un sitio web con poca utilización no se verán afectados.</span><span class="sxs-lookup"><span data-stu-id="36119-150">It doesn't operate at low volumes of telemetry, so an app in debugging or a website with low usage won't be affected.</span></span>

<span data-ttu-id="36119-151">Para lograr el volumen objetivo, alguna de la telemetría generada se descarta.</span><span class="sxs-lookup"><span data-stu-id="36119-151">To achieve the target volume, some of the telemetry generated is discarded.</span></span> <span data-ttu-id="36119-152">Pero, al igual que otros tipos de muestreo, el algoritmo conserva los elementos de telemetría relacionados.</span><span class="sxs-lookup"><span data-stu-id="36119-152">But like other types of sampling, the algorithm retains related telemetry items.</span></span> <span data-ttu-id="36119-153">Por ejemplo, cuando se inspeccione la telemetría en Búsqueda, podrá buscar la solicitud relacionada con una excepción determinada.</span><span class="sxs-lookup"><span data-stu-id="36119-153">For example, when you're inspecting the telemetry in Search, you'll be able to find the request related to a particular exception.</span></span> 

<span data-ttu-id="36119-154">Los recuentos de métrica, como la tasa de solicitudes y la tasa de excepciones, se ajustan para compensar la frecuencia de muestreo, de modo que exhiban valores aproximadamente correctos en el Explorador de métricas.</span><span class="sxs-lookup"><span data-stu-id="36119-154">Metric counts such as request rate and exception rate are adjusted to compensate for the sampling rate, so that they show approximately correct values in Metric Explorer.</span></span>

<span data-ttu-id="36119-155">**Actualice los paquetes de NuGet del proyecto** a la última *versión preliminar* de Application Insights: haga clic con el botón derecho en el proyecto en el Explorador de soluciones, elija Administrar paquetes NuGet, active **Incluir versión preliminar** y busque Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="36119-155">**Update your project's NuGet** packages to the latest *pre-release* version of Application Insights: Right-click the project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 

<span data-ttu-id="36119-156">En [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), puede ajustar varios parámetros en el nodo `AdaptiveSamplingTelemetryProcessor`.</span><span class="sxs-lookup"><span data-stu-id="36119-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), you can adjust several parameters in the `AdaptiveSamplingTelemetryProcessor` node.</span></span> <span data-ttu-id="36119-157">Las cifras que se muestran son los valores predeterminados:</span><span class="sxs-lookup"><span data-stu-id="36119-157">The figures shown are the default values:</span></span>

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    <span data-ttu-id="36119-158">Velocidad objetivo que el algoritmo de adaptación intenta lograr **en cada host de servidor**.</span><span class="sxs-lookup"><span data-stu-id="36119-158">The target rate that the adaptive algorithm aims for **on each server host**.</span></span> <span data-ttu-id="36119-159">Si la aplicación web se ejecuta en varios hosts, reduzca este valor para que se mantenga dentro de la velocidad objetivo de tráfico en el portal de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="36119-159">If your web app runs on many hosts, reduce this value so as to remain within your target rate of traffic at the Application Insights portal.</span></span>
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    <span data-ttu-id="36119-160">Intervalo en el que se vuelve a evaluar la velocidad actual de telemetría.</span><span class="sxs-lookup"><span data-stu-id="36119-160">The interval at which the current rate of telemetry is re-evaluated.</span></span> <span data-ttu-id="36119-161">La evaluación se realiza como una media móvil.</span><span class="sxs-lookup"><span data-stu-id="36119-161">Evaluation is performed as a moving average.</span></span> <span data-ttu-id="36119-162">Se recomienda acortar este intervalo si la telemetría experimenta ráfagas repentinas.</span><span class="sxs-lookup"><span data-stu-id="36119-162">You might want to shorten this interval if your telemetry is liable to sudden bursts.</span></span>
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    <span data-ttu-id="36119-163">Cuando se cambia el valor de porcentaje de muestreo, tiempo mínimo que se tarda en permitir de nuevo que se reduzca el porcentaje de muestreo para capturar menos datos.</span><span class="sxs-lookup"><span data-stu-id="36119-163">When sampling percentage value changes, how soon after are we allowed to lower sampling percentage again to capture less data.</span></span>
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    <span data-ttu-id="36119-164">Cuando se cambia el valor de porcentaje de muestreo, tiempo mínimo que se tarda en permitir de nuevo que se aumente el porcentaje de muestreo para capturar más datos.</span><span class="sxs-lookup"><span data-stu-id="36119-164">When sampling percentage value changes, how soon after are we allowed to increase sampling percentage again to capture more data.</span></span>
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    <span data-ttu-id="36119-165">Como el porcentaje de muestreo varía, valor mínimo que se permite establecer.</span><span class="sxs-lookup"><span data-stu-id="36119-165">As sampling percentage varies, what is the minimum value we're allowed to set.</span></span>
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    <span data-ttu-id="36119-166">Como el porcentaje de muestreo varía, valor máximo que se permite establecer.</span><span class="sxs-lookup"><span data-stu-id="36119-166">As sampling percentage varies, what is the maximum value we're allowed to set.</span></span>
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    <span data-ttu-id="36119-167">En el cálculo de la media móvil, peso asignado al valor más reciente.</span><span class="sxs-lookup"><span data-stu-id="36119-167">In the calculation of the moving average, the weight assigned to the most recent value.</span></span> <span data-ttu-id="36119-168">Use un valor igual o menor que 1.</span><span class="sxs-lookup"><span data-stu-id="36119-168">Use a value equal to or less than 1.</span></span> <span data-ttu-id="36119-169">Los valores menores hacen que el algoritmo reaccione con menor agilidad a los cambios repentinos.</span><span class="sxs-lookup"><span data-stu-id="36119-169">Smaller values make the algorithm less reactive to sudden changes.</span></span>
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    <span data-ttu-id="36119-170">Valor asignado cuando se acaba de iniciar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="36119-170">The value assigned when the app has just started.</span></span> <span data-ttu-id="36119-171">No lo reduzca durante la depuración.</span><span class="sxs-lookup"><span data-stu-id="36119-171">Don't reduce this while you're debugging.</span></span> 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    <span data-ttu-id="36119-172">Una lista delimitada por puntos y coma de tipos que no desea que se muestreen.</span><span class="sxs-lookup"><span data-stu-id="36119-172">A semi-colon delimited list of types that you do not want to be sampled.</span></span> <span data-ttu-id="36119-173">Los tipos reconocidos son Dependency, Event, Exception, PageView, Request, Trace.</span><span class="sxs-lookup"><span data-stu-id="36119-173">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="36119-174">Todas las instancias de los tipos especificados se transmiten; los tipos no especificados se muestrean.</span><span class="sxs-lookup"><span data-stu-id="36119-174">All instances of the specified types are transmitted; the types that are not specified are sampled.</span></span>

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    <span data-ttu-id="36119-175">Una lista delimitada por puntos y coma de tipos que desea que se muestreen.</span><span class="sxs-lookup"><span data-stu-id="36119-175">A semi-colon delimited list of types that you want to be sampled.</span></span> <span data-ttu-id="36119-176">Los tipos reconocidos son Dependency, Event, Exception, PageView, Request, Trace.</span><span class="sxs-lookup"><span data-stu-id="36119-176">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="36119-177">Los tipos especificados se muestrean, todas las instancias del resto de tipos siempre se transmitirán.</span><span class="sxs-lookup"><span data-stu-id="36119-177">The specified types are sampled; all instances of the other types will always be transmitted.</span></span>


<span data-ttu-id="36119-178">**Para desactivar** el muestreo adaptable, quite el nodo AdaptiveSamplingTelemetryProcessor de applicationinsights-config.</span><span class="sxs-lookup"><span data-stu-id="36119-178">**To switch off** adaptive sampling, remove the AdaptiveSamplingTelemetryProcessor node from applicationinsights-config.</span></span>

### <a name="alternative-configure-adaptive-sampling-in-code"></a><span data-ttu-id="36119-179">Alternativa: configure el muestreo adaptivo en el código</span><span class="sxs-lookup"><span data-stu-id="36119-179">Alternative: configure adaptive sampling in code</span></span>
<span data-ttu-id="36119-180">En lugar de ajustar el muestreo en el archivo .config, puede usar código.</span><span class="sxs-lookup"><span data-stu-id="36119-180">Instead of adjusting sampling in the .config file, you can use code.</span></span> <span data-ttu-id="36119-181">Esto le permite especificar una función de devolución de llamada que se invoca cuando se vuelve a evaluar la frecuencia de muestreo.</span><span class="sxs-lookup"><span data-stu-id="36119-181">This allows you to specify a callback function that is invoked whenever the sampling rate is re-evaluated.</span></span> <span data-ttu-id="36119-182">Puede utilizarlo, por ejemplo, para averiguar la velocidad de muestreo que se está usando.</span><span class="sxs-lookup"><span data-stu-id="36119-182">You could use this, for example, to find out what sampling rate is being used.</span></span>

<span data-ttu-id="36119-183">Quite el nodo `AdaptiveSamplingTelemetryProcessor` del archivo .config.</span><span class="sxs-lookup"><span data-stu-id="36119-183">Remove the `AdaptiveSamplingTelemetryProcessor` node from the .config file.</span></span>

<span data-ttu-id="36119-184">*C#*</span><span class="sxs-lookup"><span data-stu-id="36119-184">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust the settings from their defaults.

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;

    builder.UseAdaptiveSampling(
         adaptiveSamplingSettings,

        // Callback on rate re-evaluation:
        (double afterSamplingTelemetryItemRatePerSecond,
         double currentSamplingPercentage,
         double newSamplingPercentage,
         bool isSamplingPercentageChanged,
         SamplingPercentageEstimatorSettings s
        ) =>
        {
          if (isSamplingPercentageChanged)
          {
             // Report the sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="36119-185">([Más información sobre los procesadores de telemetría](app-insights-api-filtering-sampling.md#filtering)).</span><span class="sxs-lookup"><span data-stu-id="36119-185">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a><span data-ttu-id="36119-186">Muestreo para páginas web con JavaScript</span><span class="sxs-lookup"><span data-stu-id="36119-186">Sampling for web pages with JavaScript</span></span>
<span data-ttu-id="36119-187">Puede configurar páginas web para el muestreo de frecuencia fija desde cualquier servidor.</span><span class="sxs-lookup"><span data-stu-id="36119-187">You can configure web pages for fixed-rate sampling from any server.</span></span> 

<span data-ttu-id="36119-188">Cuando [configure las páginas web para Application Insights](app-insights-javascript.md), modifique el fragmento que obtiene del portal de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="36119-188">When you [configure the web pages for Application Insights](app-insights-javascript.md), modify the snippet that you get from the Application Insights portal.</span></span> <span data-ttu-id="36119-189">(En las aplicaciones ASP.NET, el fragmento normalmente está en _Layout.cshtml).  Inserte una línea como `samplingPercentage: 10,` antes de la clave de instrumentación:</span><span class="sxs-lookup"><span data-stu-id="36119-189">(In ASP.NET apps, the snippet typically goes in _Layout.cshtml.)  Insert a line like `samplingPercentage: 10,` before the instrumentation key:</span></span>

    <script>
    var appInsights= ... 
    }({ 


    // Value must be 100/N where N is an integer.
    // Valid examples: 50, 25, 20, 10, 5, 1, 0.1, ...
    samplingPercentage: 10, 

    instrumentationKey:...
    }); 

    window.appInsights=appInsights; 
    appInsights.trackPageView(); 
    </script> 

<span data-ttu-id="36119-190">Para el porcentaje de muestreo, elija un porcentaje que esté cerca de 100/N, donde N es un número entero.</span><span class="sxs-lookup"><span data-stu-id="36119-190">For the sampling percentage, choose a percentage that is close to 100/N where N is an integer.</span></span>  <span data-ttu-id="36119-191">Actualmente el muestreo no es compatible con otros valores.</span><span class="sxs-lookup"><span data-stu-id="36119-191">Currently sampling doesn't support other values.</span></span>

<span data-ttu-id="36119-192">Si también habilita el muestreo de frecuencia fija en el servidor, los clientes y el servidor se sincronizarán de modo que, en Búsqueda, puede desplazarse entre las solicitudes y las vistas de página relacionadas.</span><span class="sxs-lookup"><span data-stu-id="36119-192">If you also enable fixed-rate sampling at the server, the clients and server will synchronize so that, in Search, you can  navigate between related page views and requests.</span></span>

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a><span data-ttu-id="36119-193">Muestreo de frecuencia fija para sitios web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="36119-193">Fixed-rate sampling for ASP.NET web sites</span></span>
<span data-ttu-id="36119-194">El muestreo de frecuencia fija reduce el tráfico enviado desde el servidor web y los exploradores web.</span><span class="sxs-lookup"><span data-stu-id="36119-194">Fixed rate sampling reduces the traffic sent from your web server and web browsers.</span></span> <span data-ttu-id="36119-195">A diferencia del muestreo adaptable, reduce la telemetría a una tasa fija que usted decide.</span><span class="sxs-lookup"><span data-stu-id="36119-195">Unlike adaptive sampling, it reduces telemetry at a fixed rate decided by you.</span></span> <span data-ttu-id="36119-196">También sincroniza el muestreo del cliente y el servidor para que los elementos relacionados se conserven; por ejemplo, para que si mira una vista de página en Búsqueda, pueda encontrar su solicitud relacionada.</span><span class="sxs-lookup"><span data-stu-id="36119-196">It also synchronizes the client and server sampling so that related items are retained - for example, so that if you look at a page view in Search, you can find its related request.</span></span>

<span data-ttu-id="36119-197">El algoritmo de muestreo conserva los elementos relacionados.</span><span class="sxs-lookup"><span data-stu-id="36119-197">The sampling algorithm retains related items.</span></span> <span data-ttu-id="36119-198">Para cada evento de solicitud HTTP, este y sus eventos relacionados se descartan o transmiten.</span><span class="sxs-lookup"><span data-stu-id="36119-198">For each HTTP request event, it and its related events are either discarded or transmitted.</span></span> 

<span data-ttu-id="36119-199">En el Explorador de métricas, las tasas, como los recuentos de solicitudes y de excepciones, se multiplican por un factor para compensar la frecuencia de muestreo, de forma que sean aproximadamente correctas.</span><span class="sxs-lookup"><span data-stu-id="36119-199">In Metrics Explorer, rates such as request and exception counts are multiplied by a factor to compensate for the sampling rate, so that they are approximately correct.</span></span>

1. <span data-ttu-id="36119-200">**Actualice los paquetes de NuGet del proyecto** a la *versión preliminar* más reciente de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="36119-200">**Update your project's NuGet packages** to the latest *pre-release* version of Application Insights.</span></span> <span data-ttu-id="36119-201">Haga clic con el botón derecho en el Explorador de soluciones, elija Administrar paquetes NuGet, active la opción **Incluir versión preliminar** y busque Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="36119-201">Right-click the project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 
2. <span data-ttu-id="36119-202">**Deshabilite el muestreo adaptable**: en [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), quite o convierta en comentario el nodo `AdaptiveSamplingTelemetryProcessor`.</span><span class="sxs-lookup"><span data-stu-id="36119-202">**Disable adaptive sampling**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), remove or comment out the `AdaptiveSamplingTelemetryProcessor` node.</span></span>
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. <span data-ttu-id="36119-203">**Habilite el módulo de muestreo de frecuencia fija.**</span><span class="sxs-lookup"><span data-stu-id="36119-203">**Enable the fixed-rate sampling module.**</span></span> <span data-ttu-id="36119-204">Agregue este fragmento a [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="36119-204">Add this snippet to [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close to 100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> <span data-ttu-id="36119-205">Para el porcentaje de muestreo, elija un porcentaje que esté cerca de 100/N, donde N es un número entero.</span><span class="sxs-lookup"><span data-stu-id="36119-205">For the sampling percentage, choose a percentage that is close to 100/N where N is an integer.</span></span>  <span data-ttu-id="36119-206">Actualmente el muestreo no es compatible con otros valores.</span><span class="sxs-lookup"><span data-stu-id="36119-206">Currently sampling doesn't support other values.</span></span>
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a><span data-ttu-id="36119-207">Alternativa: habilitación del muestreo de frecuencia fija en el código de servidor</span><span class="sxs-lookup"><span data-stu-id="36119-207">Alternative: enable fixed-rate sampling in your server code</span></span>
<span data-ttu-id="36119-208">En lugar de establecer el parámetro de muestreo en el archivo .config, puede usar código.</span><span class="sxs-lookup"><span data-stu-id="36119-208">Instead of setting the sampling parameter in the .config file, you can use code.</span></span> 

<span data-ttu-id="36119-209">*C#*</span><span class="sxs-lookup"><span data-stu-id="36119-209">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var builder = TelemetryConfiguration.Active.GetTelemetryProcessorChainBuilder();
    builder.UseSampling(10.0); // percentage

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="36119-210">([Más información sobre los procesadores de telemetría](app-insights-api-filtering-sampling.md#filtering)).</span><span class="sxs-lookup"><span data-stu-id="36119-210">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

## <a name="when-to-use-sampling"></a><span data-ttu-id="36119-211">¿Cuándo usar un muestreo?</span><span class="sxs-lookup"><span data-stu-id="36119-211">When to use sampling?</span></span>
<span data-ttu-id="36119-212">El muestreo adaptable está habilitado automáticamente si usa el SDK de ASP.NET versión 2.0.0-beta3 o posterior.</span><span class="sxs-lookup"><span data-stu-id="36119-212">Adaptive sampling is automatically enabled if you use the ASP.NET SDK version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="36119-213">Independientemente de la versión del SDK que utilice, puede emplear el muestreo de ingesta (en nuestro servidor).</span><span class="sxs-lookup"><span data-stu-id="36119-213">No matter what SDK version you use, you can use ingestion sampling (at our server).</span></span>

<span data-ttu-id="36119-214">Para la mayoría de las aplicaciones pequeñas y medianas no es necesario realizar muestreos.</span><span class="sxs-lookup"><span data-stu-id="36119-214">You don’t need sampling for most small and medium size applications.</span></span> <span data-ttu-id="36119-215">La información de diagnóstico más útil y las estadísticas más precisas se obtienen mediante la recopilación de datos en todas las actividades del usuario.</span><span class="sxs-lookup"><span data-stu-id="36119-215">The most useful diagnostic information and most accurate statistics are obtained by collecting data on all your user activities.</span></span> 

<span data-ttu-id="36119-216">Las principales ventajas del muestreo son:</span><span class="sxs-lookup"><span data-stu-id="36119-216">The main advantages of sampling are:</span></span>

* <span data-ttu-id="36119-217">El servicio de Application Insights descarta ("limita") puntos de datos cuando la aplicación envía un número muy elevado de telemetría en un intervalo de tiempo corto.</span><span class="sxs-lookup"><span data-stu-id="36119-217">Application Insights service drops ("throttles") data points when your app sends a very high rate of telemetry in short time interval.</span></span> 
* <span data-ttu-id="36119-218">Para mantenerse dentro de la [cuota](app-insights-pricing.md) de puntos de datos de su plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="36119-218">To keep within the [quota](app-insights-pricing.md) of data points for your pricing tier.</span></span> 
* <span data-ttu-id="36119-219">Para reducir el tráfico de red de la recopilación de telemetría.</span><span class="sxs-lookup"><span data-stu-id="36119-219">To reduce network traffic from the collection of telemetry.</span></span> 

### <a name="which-type-of-sampling-should-i-use"></a><span data-ttu-id="36119-220">¿Qué tipo de muestreo debo utilizar?</span><span class="sxs-lookup"><span data-stu-id="36119-220">Which type of sampling should I use?</span></span>
<span data-ttu-id="36119-221">**Use el muestreo de ingesta si:**</span><span class="sxs-lookup"><span data-stu-id="36119-221">**Use ingestion sampling if:**</span></span>

* <span data-ttu-id="36119-222">Con frecuencia sobrepasa su cuota mensual de telemetría.</span><span class="sxs-lookup"><span data-stu-id="36119-222">You often go through your monthly quota of telemetry.</span></span>
* <span data-ttu-id="36119-223">Usa una versión del SDK que no admite muestreo; por ejemplo, el SDK de Java o las versiones de ASP.NET anteriores a la 2.</span><span class="sxs-lookup"><span data-stu-id="36119-223">You're using a version of the SDK that doesn't support sampling - for example, the Java SDK or ASP.NET versions earlier than 2.</span></span>
* <span data-ttu-id="36119-224">Recibe mucha telemetría de los exploradores web de sus usuarios.</span><span class="sxs-lookup"><span data-stu-id="36119-224">You're getting a lot of telemetry from your users' web browsers.</span></span>

<span data-ttu-id="36119-225">**Use el muestreo de frecuencia fija si:**</span><span class="sxs-lookup"><span data-stu-id="36119-225">**Use fixed-rate sampling if:**</span></span>

* <span data-ttu-id="36119-226">Usa el SDK de Application Insights para servicios web de ASP.NET versión 2.0.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="36119-226">You're using the Application Insights SDK for ASP.NET web services version 2.0.0 or later, and</span></span>
* <span data-ttu-id="36119-227">Quiere un muestreo sincronizado entre cliente y servidor para que, cuando investigue eventos en [Búsqueda](app-insights-diagnostic-search.md), pueda desplazarse entre los eventos relacionados en el cliente y el servidor, como vistas de página y solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="36119-227">You want synchronized sampling between client and server, so that, when you're investigating events in [Search](app-insights-diagnostic-search.md), you can navigate between related events on the client and server, such as page views and http requests.</span></span>
* <span data-ttu-id="36119-228">Está seguro del porcentaje de muestreo adecuado para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="36119-228">You are confident of the appropriate sampling percentage for your app.</span></span> <span data-ttu-id="36119-229">Debe ser lo bastante alto como para obtener métricas precisas, pero inferior a la frecuencia que supera la cuota de precios y los valores de limitación.</span><span class="sxs-lookup"><span data-stu-id="36119-229">It should be high enough to get accurate metrics, but below the rate that exceeds your pricing quota and the throttling limits.</span></span> 

<span data-ttu-id="36119-230">**Use el muestreo adaptable si:**</span><span class="sxs-lookup"><span data-stu-id="36119-230">**Use adaptive sampling:**</span></span>

<span data-ttu-id="36119-231">De lo contrario, se recomienda el muestreo adaptable.</span><span class="sxs-lookup"><span data-stu-id="36119-231">Otherwise, we recommend adaptive sampling.</span></span> <span data-ttu-id="36119-232">Esta opción está habilitada de forma predeterminada en el SDK de servidor de ASP.NET versión 2.0.0-beta3 o posterior.</span><span class="sxs-lookup"><span data-stu-id="36119-232">This is enabled by default in the ASP.NET server SDK, version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="36119-233">No reduce el tráfico hasta una determinada tasa mínima, así que no afectará a los sitios de utilización baja.</span><span class="sxs-lookup"><span data-stu-id="36119-233">It doesn't reduce traffic until a certain minimum rate, so it won't affect a low-use site.</span></span>

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a><span data-ttu-id="36119-234">¿Cómo se puede saber si el muestreo está en funcionamiento?</span><span class="sxs-lookup"><span data-stu-id="36119-234">How do I know whether sampling is in operation?</span></span>
<span data-ttu-id="36119-235">Para conocer la frecuencia de muestreo real independientemente de dónde se ha aplicado, use una [consulta de Analytics](app-insights-analytics.md) como esta:</span><span class="sxs-lookup"><span data-stu-id="36119-235">To discover the actual sampling rate no matter where it has been applied, use an [Analytics query](app-insights-analytics.md) such as this:</span></span>

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

<span data-ttu-id="36119-236">En cada registro retenido, `itemCount` indica el número de registros originales que representa, equivale a 1 + el número de registros descartados anteriores.</span><span class="sxs-lookup"><span data-stu-id="36119-236">In each retained record, `itemCount` indicates the number of original records that it represents, equal to 1 + the number of previous discarded records.</span></span> 

## <a name="how-does-sampling-work"></a><span data-ttu-id="36119-237">¿Cómo funciona el muestreo?</span><span class="sxs-lookup"><span data-stu-id="36119-237">How does sampling work?</span></span>
<span data-ttu-id="36119-238">El muestreo adaptable y de frecuencia fija es una característica del SDK de ASP.NET 2.0.0 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="36119-238">Fixed-rate and adaptive sampling are a feature of the SDK in ASP.NET versions from 2.0.0 onwards.</span></span> <span data-ttu-id="36119-239">El muestreo de ingesta es una característica del servicio de Application Insights y puede funcionar si el SDK no realiza muestreo.</span><span class="sxs-lookup"><span data-stu-id="36119-239">Ingestion sampling is a feature of the Application Insights service, and can be in operation if the SDK is not performing sampling.</span></span> 

<span data-ttu-id="36119-240">El algoritmo de muestreo decide qué elementos de telemetría quitar y cuáles conservar (ya sea en el SDK o en el servicio de Application Insights).</span><span class="sxs-lookup"><span data-stu-id="36119-240">The sampling algorithm decides which telemetry items to drop, and which ones to keep (whether it's in the SDK or in the Application Insights service).</span></span> <span data-ttu-id="36119-241">La decisión del muestreo se basa en varias reglas que tienen como objetivo conservar intactos todos los puntos de datos interrelacionados, manteniendo una experiencia de diagnóstico en Application Insights que sea práctica y confiable, incluso con un conjunto reducido de datos.</span><span class="sxs-lookup"><span data-stu-id="36119-241">The sampling decision is based on several rules that aim to preserve all interrelated data points intact, maintaining a diagnostic experience in Application Insights that is actionable and reliable even with a reduced data set.</span></span> <span data-ttu-id="36119-242">Por ejemplo, si para una solicitud errónea su aplicación envía elementos de telemetría adicionales (como la excepción y los seguimientos registrados para dicha solicitud), el muestreo no dividirá esta solicitud y otra telemetría.</span><span class="sxs-lookup"><span data-stu-id="36119-242">For example, if for a failed request your app sends additional telemetry items (such as exception and traces logged from this request), sampling will not split this request and other telemetry.</span></span> <span data-ttu-id="36119-243">Escogerá mantenerlos o descartarlos todos juntos</span><span class="sxs-lookup"><span data-stu-id="36119-243">It either keeps or drops them all together.</span></span> <span data-ttu-id="36119-244">Como resultado, al examinar los detalles de solicitud en Application Insights, siempre puede ver la solicitud junto con sus elementos de telemetría asociados.</span><span class="sxs-lookup"><span data-stu-id="36119-244">As a result, when you look at the request details in Application Insights, you can always see the request along with its associated telemetry items.</span></span> 

<span data-ttu-id="36119-245">Para las aplicaciones que definen "usuario" (es decir, las aplicaciones web más típicas), la decisión de muestreo se basa en el hash del identificador de usuario, lo que significa que toda la telemetría para cualquier usuario específico o se conservan o se descarta.</span><span class="sxs-lookup"><span data-stu-id="36119-245">For applications that define "user" (that is, most typical web applications), the sampling decision is based on the hash of the user id, which means that all telemetry for any particular user is either preserved or dropped.</span></span> <span data-ttu-id="36119-246">Para los tipos de aplicaciones que no definen a los usuarios (como los servicios web) la decisión de muestreo se basa en el identificador de operación de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="36119-246">For the types of applications that don't define users (such as web services) the sampling decision is based on the operation id of the request.</span></span> <span data-ttu-id="36119-247">Por último, para los elementos de telemetría que no tienen establecido ni identificador de usuario ni identificador de operación (por ejemplo elementos de telemetría notificados desde subprocesos asincrónicos sin contexto de http), el muestreo simplemente captura un porcentaje de elementos de telemetría de cada tipo.</span><span class="sxs-lookup"><span data-stu-id="36119-247">Finally, for the telemetry items that neither have user nor operation id set (for example telemetry items reported from asynchronous threads with no http context) sampling simply captures a percentage of telemetry items of each type.</span></span> 

<span data-ttu-id="36119-248">Al presentarle la telemetría, el servicio de Application Insights ajusta las métricas con el mismo porcentaje de muestreo que se usó en el momento de la recopilación, para compensar por los puntos de datos que faltan.</span><span class="sxs-lookup"><span data-stu-id="36119-248">When presenting telemetry back to you, the Application Insights service adjusts the metrics by the same sampling percentage that was used at the time of collection, to compensate for the missing data points.</span></span> <span data-ttu-id="36119-249">Por lo tanto, al examinar la telemetría en Application Insights, los usuarios ven aproximaciones estadísticamente correctas que están muy próximas a los números reales.</span><span class="sxs-lookup"><span data-stu-id="36119-249">Hence, when looking at the telemetry in Application Insights, the users are seeing statistically correct approximations that are very close to the real numbers.</span></span>

<span data-ttu-id="36119-250">La precisión de la aproximación depende en gran medida del porcentaje de muestreo configurado.</span><span class="sxs-lookup"><span data-stu-id="36119-250">The accuracy of the approximation largely depends on the configured sampling percentage.</span></span> <span data-ttu-id="36119-251">También, la precisión aumenta en las aplicaciones que administran un gran volumen de solicitudes básicamente similares de muchos usuarios.</span><span class="sxs-lookup"><span data-stu-id="36119-251">Also, the accuracy increases for applications that handle a large volume of generally similar requests from lots of users.</span></span> <span data-ttu-id="36119-252">Por otro lado, para las aplicaciones que no funcionan con una carga significativa, el muestreo no es necesario ya que estas aplicaciones normalmente pueden enviar toda su telemetría manteniéndose dentro de la cuota, sin causar pérdida de datos por causa de la limitación.</span><span class="sxs-lookup"><span data-stu-id="36119-252">On the other hand, for applications that don't work with a significant load, sampling is not needed as these applications can usually send all their telemetry while staying within the quota, without causing data loss from throttling.</span></span> 

<span data-ttu-id="36119-253">Tenga en cuenta que Application Insights no muestrea tipos de telemetría de Métricas y Sesiones, ya que para estos tipos la reducción en la precisión puede ser no deseable en absoluto.</span><span class="sxs-lookup"><span data-stu-id="36119-253">Note that Application Insights does not sample Metrics and Sessions telemetry types, since for these types, reduction in the precision can be highly undesirable.</span></span> 

### <a name="adaptive-sampling"></a><span data-ttu-id="36119-254">muestreo adaptable</span><span class="sxs-lookup"><span data-stu-id="36119-254">Adaptive sampling</span></span>
<span data-ttu-id="36119-255">El muestreo adaptable agrega un componente que supervisa la velocidad actual de transmisión desde el SDK y ajusta el porcentaje de muestreo para mantenerse dentro de la velocidad objetivo máxima.</span><span class="sxs-lookup"><span data-stu-id="36119-255">Adaptive sampling adds a component that monitors the current rate of transmission from the SDK, and adjusts the sampling percentage to try to stay within the target maximum rate.</span></span> <span data-ttu-id="36119-256">El ajuste se actualiza a intervalos regulares y se basa en una media móvil de la velocidad de transmisión de salida.</span><span class="sxs-lookup"><span data-stu-id="36119-256">The adjustment is recalculated at regular intervals, and is based on a moving average of the outgoing transmission rate.</span></span>

## <a name="sampling-and-the-javascript-sdk"></a><span data-ttu-id="36119-257">Muestreo y el SDK de JavaScript</span><span class="sxs-lookup"><span data-stu-id="36119-257">Sampling and the JavaScript SDK</span></span>
<span data-ttu-id="36119-258">El SDK del lado cliente (JavaScript) participa en el muestreo de frecuencia fija junto con el SDK del lado servidor.</span><span class="sxs-lookup"><span data-stu-id="36119-258">The client-side (JavaScript) SDK participates in fixed-rate sampling in conjunction with the server-side SDK.</span></span> <span data-ttu-id="36119-259">Las páginas instrumentadas solo enviarán telemetría de cliente desde los mismos usuarios para los que el lado del servidor decidió tomar el muestreo.</span><span class="sxs-lookup"><span data-stu-id="36119-259">The instrumented pages will only send client-side telemetry from the same users for which the server-side made its decision to "sample in."</span></span> <span data-ttu-id="36119-260">Esta lógica está diseñada para mantener la integridad de la sesión de usuario a través de los lados cliente y servidor.</span><span class="sxs-lookup"><span data-stu-id="36119-260">This logic is designed to maintain integrity of user session across client- and server-sides.</span></span> <span data-ttu-id="36119-261">Como resultado, a partir de cualquier elemento específico de telemetría en Application Insights, puede encontrar todos los demás elementos de telemetría para ese usuario o esa sesión.</span><span class="sxs-lookup"><span data-stu-id="36119-261">As a result, from any particular telemetry item in Application Insights you can find all other telemetry items for this user or session.</span></span> 

<span data-ttu-id="36119-262">*Las telemetrías del lado de cliente y de servidor no muestran ejemplos coordinados tal y como se describe anteriormente.*</span><span class="sxs-lookup"><span data-stu-id="36119-262">*My client and server-side telemetry don't show coordinated samples as you describe above.*</span></span>

* <span data-ttu-id="36119-263">Compruebe que habilitó el muestreo de frecuencia fija tanto en el cliente como en el servidor.</span><span class="sxs-lookup"><span data-stu-id="36119-263">Verify that you enabled fixed-rate sampling both on server and client.</span></span>
* <span data-ttu-id="36119-264">Asegúrese de que la versión del SDK es 2.0 o superior.</span><span class="sxs-lookup"><span data-stu-id="36119-264">Make sure that the SDK version is 2.0 or above.</span></span>
* <span data-ttu-id="36119-265">Compruebe que establece el mismo porcentaje de muestreo en el cliente y el servidor.</span><span class="sxs-lookup"><span data-stu-id="36119-265">Check that you set the same sampling percentage in both the client and server.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="36119-266">Preguntas frecuentes</span><span class="sxs-lookup"><span data-stu-id="36119-266">Frequently Asked Questions</span></span>
<span data-ttu-id="36119-267">*¿Por qué realizar un muestreo no consiste simplemente en "recopilar X por ciento de cada tipo de telemetría"?*</span><span class="sxs-lookup"><span data-stu-id="36119-267">*Why isn't sampling a simple "collect X percent of each telemetry type"?*</span></span>

* <span data-ttu-id="36119-268">Aunque este método de muestreo proporcionaría un nivel de precisión muy alto en las aproximaciones métricas, destruiría la capacidad para poner en correlación datos de diagnóstico por usuario, sesión y solicitud, lo cual es crítico para el diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="36119-268">While this sampling approach would provide with a very high precision in metric approximations, it would break ability to correlate diagnostic data per user, session, and request, which is critical for diagnostics.</span></span> <span data-ttu-id="36119-269">Por lo tanto, el muestreo funciona mejor con una lógica "recopilar todos los elementos de telemetría para X por ciento de los usuarios de la aplicación", o "recopilar toda la telemetría para X por ciento de las solicitudes de aplicación".</span><span class="sxs-lookup"><span data-stu-id="36119-269">Therefore, sampling works better with "collect all telemetry items for X percent of app users", or "collect all telemetry for X percent of app requests" logic.</span></span> <span data-ttu-id="36119-270">Para los elementos de telemetría no asociados con las solicitudes (por ejemplo, el procesamiento asincrónico en segundo plano), el recurso es "recopilar X por ciento de todos los elementos para cada tipo de telemetría".</span><span class="sxs-lookup"><span data-stu-id="36119-270">For the telemetry items not associated with the requests (such as background asynchronous processing), the fall back is to "collect X percent of all items for each telemetry type."</span></span> 

<span data-ttu-id="36119-271">*¿Se puede cambiar el porcentaje de muestreo con el tiempo?*</span><span class="sxs-lookup"><span data-stu-id="36119-271">*Can the sampling percentage change over time?*</span></span>

* <span data-ttu-id="36119-272">Sí, el muestreo adaptable cambia gradualmente el porcentaje de muestreo, en función del volumen de datos de telemetría observado en ese momento.</span><span class="sxs-lookup"><span data-stu-id="36119-272">Yes, adaptive sampling gradually changes the sampling percentage, based on the currently observed volume of the telemetry.</span></span>

<span data-ttu-id="36119-273">*Si uso el muestreo de frecuencia fija, ¿cómo sé cuál es el porcentaje de muestreo que funcionará mejor para mi aplicación?*</span><span class="sxs-lookup"><span data-stu-id="36119-273">*If I use fixed-rate sampling, how do I know which sampling percentage will work the best for my app?*</span></span>

* <span data-ttu-id="36119-274">Una manera de comenzar es con muestreo adaptable, averigüe qué velocidad elige (consulte la pregunta anterior) y luego cambie a muestreo de tasa fija con esa velocidad.</span><span class="sxs-lookup"><span data-stu-id="36119-274">One way is to start with adaptive sampling, find out what rate it settles on (see the above question), and then switch to fixed-rate sampling using that rate.</span></span> 
  
    <span data-ttu-id="36119-275">Si no, lo tendrá que adivinar.</span><span class="sxs-lookup"><span data-stu-id="36119-275">Otherwise, you have to guess.</span></span> <span data-ttu-id="36119-276">Analice su uso actual de telemetría en AI, observe las limitaciones que se produzcan y estime el volumen de telemetría recopilado.</span><span class="sxs-lookup"><span data-stu-id="36119-276">Analyze your current telemetry usage in AI, observe any throttling that is occurring, and estimate the volume of the collected telemetry.</span></span> <span data-ttu-id="36119-277">Estas tres entradas, junto con el plan de tarifa seleccionado, le sugerirán cuánto debería reducir el volumen de telemetría recopilado.</span><span class="sxs-lookup"><span data-stu-id="36119-277">These three inputs, together with your selected pricing tier, suggest how much you might want to reduce the volume of the collected telemetry.</span></span> <span data-ttu-id="36119-278">Sin embargo, un aumento del número de usuarios o algún otro incremento en el volumen de datos de telemetría podrían provocar que la estimación no fuese válida.</span><span class="sxs-lookup"><span data-stu-id="36119-278">However, an increase in the number of your users or some other shift in the volume of telemetry might invalidate your estimate.</span></span>

<span data-ttu-id="36119-279">*¿Qué sucede si configuro un porcentaje de muestreo demasiado bajo?*</span><span class="sxs-lookup"><span data-stu-id="36119-279">*What happens if I configure sampling percentage too low?*</span></span>

* <span data-ttu-id="36119-280">Un porcentaje de muestreo excesivamente bajo (muestreo demasiado drástico) reduce la precisión de las aproximaciones cuando Application Insights intenta compensar la visualización de los datos por la reducción del volumen de datos.</span><span class="sxs-lookup"><span data-stu-id="36119-280">Excessively low sampling percentage (over-aggressive sampling) reduces the accuracy of the approximations, when Application Insights attempts to compensate the visualization of the data for the data volume reduction.</span></span> <span data-ttu-id="36119-281">Además, la experiencia de diagnóstico puede verse afectada negativamente, ya que algunas de las solicitudes con poca frecuencia errores o lentas pueden quedar fuera del muestreo.</span><span class="sxs-lookup"><span data-stu-id="36119-281">Also, diagnostic experience might be negatively impacted, as some of the infrequently failing or slow requests may be sampled out.</span></span>

<span data-ttu-id="36119-282">*¿Qué sucede si configuro un porcentaje de muestreo demasiado alto?*</span><span class="sxs-lookup"><span data-stu-id="36119-282">*What happens if I configure sampling percentage too high?*</span></span>

* <span data-ttu-id="36119-283">Configurar un porcentaje de muestreo demasiado alto (no suficientemente drástico) da como resultado una reducción insuficiente del volumen de telemetría recopilada.</span><span class="sxs-lookup"><span data-stu-id="36119-283">Configuring too high sampling percentage (not aggressive enough) results in an insufficient reduction in the volume of the collected telemetry.</span></span> <span data-ttu-id="36119-284">Se pueden seguir produciendo pérdidas de datos de telemetría relacionadas con la limitación, y el costo de usar Application Insights puede ser mayor de lo planeado, debido a los cargos debidos al uso por encima del límite.</span><span class="sxs-lookup"><span data-stu-id="36119-284">You may still experience telemetry data loss related to throttling, and the cost of using Application Insights might be higher than you planned due to overage charges.</span></span>

<span data-ttu-id="36119-285">*¿En qué plataformas puedo usar muestreo?*</span><span class="sxs-lookup"><span data-stu-id="36119-285">*On what platforms can I use sampling?*</span></span>

* <span data-ttu-id="36119-286">El muestreo de ingesta puede producirse automáticamente cuando cualquier dato de telemetría se sitúa por encima de un determinado volumen, si el SDK no realiza muestreo.</span><span class="sxs-lookup"><span data-stu-id="36119-286">Ingestion sampling can occur automatically for any telemetry above a certain volume, if the SDK is not performing sampling.</span></span> <span data-ttu-id="36119-287">Este sería el caso, por ejemplo, si su aplicación utiliza un servidor Java o si usa una versión anterior del SDK de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="36119-287">This would work, for example, if your app uses a Java server, or if you are using an older version of the ASP.NET SDK.</span></span>
* <span data-ttu-id="36119-288">Si usa el SDK de ASP.NET 2.0.0 y versiones posteriores (hospedado en Azure o en su propio servidor), obtendrá de forma predeterminada muestreo adaptable, pero puede cambiar al de frecuencia fija como se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="36119-288">If you're using ASP.NET SDK versions 2.0.0 and above (hosted either in Azure or on your own server), you get adaptive sampling by default, but you can switch to fixed-rate as described above.</span></span> <span data-ttu-id="36119-289">Con el muestreo de frecuencia fija, el SDK del explorador se sincroniza automáticamente con los eventos relacionados con el muestreo.</span><span class="sxs-lookup"><span data-stu-id="36119-289">With fixed-rate sampling, the browser SDK automatically synchronizes to sample related events.</span></span> 

<span data-ttu-id="36119-290">*Hay ciertos eventos excepcionales que siempre quiero ver. ¿Cómo se consigue que el módulo de muestreo los reconozca?*</span><span class="sxs-lookup"><span data-stu-id="36119-290">*There are certain rare events I always want to see. How can I get them past the sampling module?*</span></span>

* <span data-ttu-id="36119-291">Inicialice una instancia independiente de TelemetryClient con un nuevo valor de TelemetryConfiguration (no el activo de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="36119-291">Initialize a separate instance of TelemetryClient with a new TelemetryConfiguration (not the default Active one).</span></span> <span data-ttu-id="36119-292">Úsela para enviar sus eventos excepcionales.</span><span class="sxs-lookup"><span data-stu-id="36119-292">Use that to send your rare events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36119-293">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="36119-293">Next steps</span></span>
* <span data-ttu-id="36119-294">[filtro](app-insights-api-filtering-sampling.md) puede proporcionar un control más estricto de los SDK que envía.</span><span class="sxs-lookup"><span data-stu-id="36119-294">[Filtering](app-insights-api-filtering-sampling.md) can provide more strict control of what your SDK sends.</span></span>

