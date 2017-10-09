---
title: muestreo de aaaTelemetry en Azure Application Insights | Documentos de Microsoft
description: "¿Cómo tookeep Hola volumen de telemetría bajo control."
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
ms.openlocfilehash: e19c350d0a5f16736c100322a9922fcfbf5d7b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sampling-in-application-insights"></a><span data-ttu-id="0606a-103">Muestreo en Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0606a-103">Sampling in Application Insights</span></span>


<span data-ttu-id="0606a-104">El muestreo es una característica de [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0606a-104">Sampling is a feature in [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="0606a-105">Es tráfico de manera tooreduce telemetría y almacenamiento, recomienda Hola conservando un análisis estadísticamente correcto de datos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0606a-105">It is hello recommended way tooreduce telemetry traffic and storage, while preserving  a statistically correct analysis of application data.</span></span> <span data-ttu-id="0606a-106">filtro de Hello selecciona los elementos que están relacionados, por lo que puede navegar entre elementos cuando realiza una de las investigaciones de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="0606a-106">hello filter selects items that are related, so that you can navigate between items when you are doing diagnostic investigations.</span></span>
<span data-ttu-id="0606a-107">Cuando los recuentos de métrica se presentan tooyou en el portal de hello, son normalizarse tootake cuenta de hello de muestreo, toominimize cualquier efecto en las estadísticas de Hola.</span><span class="sxs-lookup"><span data-stu-id="0606a-107">When metric counts are presented tooyou in hello portal, they are renormalized tootake account of hello sampling, toominimize any effect on hello statistics.</span></span>

<span data-ttu-id="0606a-108">El muestreo reduce los costos de tráfico y datos y le ayuda a evitar la limitación.</span><span class="sxs-lookup"><span data-stu-id="0606a-108">Sampling reduces traffic and data costs, and helps you avoid throttling.</span></span>

## <a name="in-brief"></a><span data-ttu-id="0606a-109">En resumen:</span><span class="sxs-lookup"><span data-stu-id="0606a-109">In brief:</span></span>
* <span data-ttu-id="0606a-110">Muestreo conserva 1 en  *n*  registra y descarta el resto de Hola.</span><span class="sxs-lookup"><span data-stu-id="0606a-110">Sampling retains 1 in *n* records and discards hello rest.</span></span> <span data-ttu-id="0606a-111">Por ejemplo, podría retener los eventos de 1 a 5, una velocidad de muestreo del 20 %.</span><span class="sxs-lookup"><span data-stu-id="0606a-111">For example, it might retain 1 in 5 events, a sampling rate of 20%.</span></span> 
* <span data-ttu-id="0606a-112">El muestreo se produce automáticamente si la aplicación envía una gran cantidad de telemetría en las aplicaciones de servidor web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0606a-112">Sampling happens automatically if your application sends a lot of telemetry, in ASP.NET web server apps.</span></span>
* <span data-ttu-id="0606a-113">También puede establecer muestreo manualmente, ya sea en hello portal en hello página; de precios o bien, en hello SDK para ASP.NET en el archivo .config de hello, tooalso reducir el tráfico de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="0606a-113">You can also set sampling manually, either in hello portal on hello pricing page; or in hello ASP.NET SDK in hello .config file, tooalso reduce hello network traffic.</span></span>
* <span data-ttu-id="0606a-114">Si registra eventos personalizados y desea toomake seguro de que un conjunto de eventos se conservan o se descartan juntas, asegúrese de que haya Hola mismo valor de Id.</span><span class="sxs-lookup"><span data-stu-id="0606a-114">If you log custom events and you want toomake sure that a set of events is either retained or discarded together, make sure that they have hello same OperationId value.</span></span>
* <span data-ttu-id="0606a-115">divisor de muestreo de Hello  *n*  se notifica en cada registro de la propiedad de hello `itemCount`, que en la búsqueda aparece bajo nombre descriptivo de Hola "número de solicitudes" o "recuento de eventos".</span><span class="sxs-lookup"><span data-stu-id="0606a-115">hello sampling divisor *n* is reported in each record in hello property `itemCount`, which in Search appears under hello friendly name "request count" or "event count".</span></span> <span data-ttu-id="0606a-116">Cuando el muestreo no está en funcionamiento, `itemCount==1`.</span><span class="sxs-lookup"><span data-stu-id="0606a-116">When sampling is not in operation, `itemCount==1`.</span></span>
* <span data-ttu-id="0606a-117">Si escribe consultas de Analytics, debería [tener en cuenta el muestreo](app-insights-analytics-tour.md#counting-sampled-data).</span><span class="sxs-lookup"><span data-stu-id="0606a-117">If you write Analytics queries, you should [take account of sampling](app-insights-analytics-tour.md#counting-sampled-data).</span></span> <span data-ttu-id="0606a-118">En concreto, en lugar de simplemente contar registros, debería usar `summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="0606a-118">In particular, instead of simply counting records, you should use `summarize sum(itemCount)`.</span></span>

## <a name="types-of-sampling"></a><span data-ttu-id="0606a-119">Tipos de muestreo</span><span class="sxs-lookup"><span data-stu-id="0606a-119">Types of sampling</span></span>
<span data-ttu-id="0606a-120">Existen tres métodos de muestreo alternativos:</span><span class="sxs-lookup"><span data-stu-id="0606a-120">There are three alternative sampling methods:</span></span>

* <span data-ttu-id="0606a-121">**Muestreo adaptativo** ajusta automáticamente el volumen de Hola de telemetría enviado desde Hola SDK en la aplicación ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0606a-121">**Adaptive sampling** automatically adjusts hello volume of telemetry sent from hello SDK in your ASP.NET app.</span></span> <span data-ttu-id="0606a-122">Valor predeterminado del SDK v 2.0.0-beta3.</span><span class="sxs-lookup"><span data-stu-id="0606a-122">Default from SDK v 2.0.0-beta3.</span></span> <span data-ttu-id="0606a-123">Actualmente solo está disponible para la telemetría de servidor ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0606a-123">Currently available for ASP.NET server-side telemetry only.</span></span> 
* <span data-ttu-id="0606a-124">**Muestreo de tipo fijo** reduce el volumen de Hola de telemetría que se envían desde el servidor de ASP.NET y de los exploradores de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="0606a-124">**Fixed-rate sampling** reduces hello volume of telemetry sent from both your ASP.NET server and from your users' browsers.</span></span> <span data-ttu-id="0606a-125">Establecer la velocidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="0606a-125">You set hello rate.</span></span> <span data-ttu-id="0606a-126">Hola cliente y servidor sincronizarán su muestreo por lo que, la búsqueda en, puede navegar entre las vistas de página relacionados y las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="0606a-126">hello client and server will synchronize their sampling so that, in Search, you can navigate between related page views and requests.</span></span>
* <span data-ttu-id="0606a-127">**Muestreo de ingesta** funciona en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0606a-127">**Ingestion sampling** works in hello Azure portal.</span></span> <span data-ttu-id="0606a-128">Descarta algunas de telemetría de Hola que llega desde su aplicación a una velocidad que se establece.</span><span class="sxs-lookup"><span data-stu-id="0606a-128">It discards some of hello telemetry that arrives from your app, at a rate that you set.</span></span> <span data-ttu-id="0606a-129">Aunque no reduce el tráfico de telemetría, le ayuda a mantenerse dentro de su cuota mensual.</span><span class="sxs-lookup"><span data-stu-id="0606a-129">It doesn't reduce telemetry traffic, but helps you keep within your monthly quota.</span></span> <span data-ttu-id="0606a-130">Hola gran ventaja de muestreo de ingesta es que puede establecer sin volver a implementar la aplicación y uniformemente funciona para todos los clientes y servidores.</span><span class="sxs-lookup"><span data-stu-id="0606a-130">hello big advantage of ingestion sampling is that you can set it without redeploying your app, and it works uniformly for all servers and clients.</span></span> 

<span data-ttu-id="0606a-131">Si el muestreo de velocidad adaptable o fija está funcionando, el muestreo de ingesta se deshabilita.</span><span class="sxs-lookup"><span data-stu-id="0606a-131">If Adaptive or Fixed rate sampling are in operation, Ingestion sampling is disabled.</span></span>

## <a name="ingestion-sampling"></a><span data-ttu-id="0606a-132">muestreo de ingesta</span><span class="sxs-lookup"><span data-stu-id="0606a-132">Ingestion sampling</span></span>
<span data-ttu-id="0606a-133">Esta forma de muestreo se aplica en punto de Hola donde telemetría Hola desde el servidor web, exploradores y dispositivos alcanza el extremo de servicio de Application Insights de Hola.</span><span class="sxs-lookup"><span data-stu-id="0606a-133">This form of sampling operates at hello point where hello telemetry from your web server, browsers, and devices reaches hello Application Insights service endpoint.</span></span> <span data-ttu-id="0606a-134">Aunque no reduce el tráfico de telemetría de hello enviado desde la aplicación, reducir la cantidad de hello procesados y conservan (y cobra por) con Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0606a-134">Although it doesn't reduce hello telemetry traffic sent from your app, it does reduce hello amount processed and retained (and charged for) by Application Insights.</span></span>

<span data-ttu-id="0606a-135">Use este tipo de muestreo si la aplicación a menudo supera la cuota mensual y no tendrá posibilidad de Hola de mediante cualquiera de los tipos basados en SDK de Hola de muestreo.</span><span class="sxs-lookup"><span data-stu-id="0606a-135">Use this type of sampling if your app often goes over its monthly quota and you don't have hello option of using either of hello SDK-based types of sampling.</span></span> 

<span data-ttu-id="0606a-136">Establecer la frecuencia de muestreo de Hola Hola cuotas y hoja de precios:</span><span class="sxs-lookup"><span data-stu-id="0606a-136">Set hello sampling rate in hello Quotas and Pricing blade:</span></span>

![Desde la hoja de información general sobre la aplicación hello, haga clic en configuración, cuota, ejemplos, a continuación, seleccione una frecuencia de muestreo y haga clic en actualizar.](./media/app-insights-sampling/04.png)

<span data-ttu-id="0606a-138">Al igual que otros tipos de muestreo, el algoritmo de hello conserva elementos de telemetría relacionada.</span><span class="sxs-lookup"><span data-stu-id="0606a-138">Like other types of sampling, hello algorithm retains related telemetry items.</span></span> <span data-ttu-id="0606a-139">Por ejemplo, al inspeccionar la telemetría de hello en la búsqueda, podrá excepciones concretas tooa relacionados con la solicitud de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="0606a-139">For example, when you're inspecting hello telemetry in Search, you'll be able toofind hello request related tooa particular exception.</span></span> <span data-ttu-id="0606a-140">Los recuentos de métrica, como la tasa de solicitudes y la tasa de excepciones se mantienen correctamente.</span><span class="sxs-lookup"><span data-stu-id="0606a-140">Metric counts such as request rate and exception rate are correctly retained.</span></span>

<span data-ttu-id="0606a-141">Los puntos de datos que se descartan por muestreo no están disponibles en ninguna característica de Application Insights como [exportación continua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="0606a-141">Data points that are discarded by sampling are not available in any Application Insights feature such as [Continuous Export](app-insights-export-telemetry.md).</span></span>

<span data-ttu-id="0606a-142">El muestreo de ingesta no funciona mientras el muestreo adaptativo o de frecuencia fija basado en el SDK está en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="0606a-142">Ingestion sampling doesn't operate while SDK-based adaptive or fixed-rate sampling is in operation.</span></span> <span data-ttu-id="0606a-143">Si la velocidad de muestreo de hello en hello SDK es menor del 100%, a continuación, hello frecuencia de muestreo de ingesta que establezca se omite.</span><span class="sxs-lookup"><span data-stu-id="0606a-143">If hello sampling rate at hello SDK is less than 100%, then hello ingestion sampling rate that you set is ignored.</span></span>

> [!WARNING]
> <span data-ttu-id="0606a-144">valor de Hola que se muestra en el icono de hello indica valor Hola que establezca para el muestreo de recopilación.</span><span class="sxs-lookup"><span data-stu-id="0606a-144">hello value shown on hello tile indicates hello value that you set for ingestion sampling.</span></span> <span data-ttu-id="0606a-145">Frecuencia de muestreo de hello real, no representa si el muestreo de SDK está en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="0606a-145">It doesn't represent hello actual sampling rate if SDK sampling is in operation.</span></span>
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a><span data-ttu-id="0606a-146">Muestreo adaptable en el servidor web</span><span class="sxs-lookup"><span data-stu-id="0606a-146">Adaptive sampling at your web server</span></span>
<span data-ttu-id="0606a-147">Muestreo adaptable está disponible para hello Application Insights SDK para ASP.NET v 2.0.0-beta3 y versiones posteriores y está habilitada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0606a-147">Adaptive sampling is available for hello Application Insights SDK for ASP.NET v 2.0.0-beta3 and later, and is enabled by default.</span></span> 

<span data-ttu-id="0606a-148">Muestreo adaptativo afecta al volumen de Hola de telemetría enviado desde su aplicación de servidor web toohello servicio Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0606a-148">Adaptive sampling affects hello volume of telemetry sent from your web server app toohello Application Insights service.</span></span> <span data-ttu-id="0606a-149">Hello volumen se ajusta automáticamente tookeep dentro de un tipo de tráfico máximo especificado.</span><span class="sxs-lookup"><span data-stu-id="0606a-149">hello volume is adjusted automatically tookeep within a specified maximum rate of traffic.</span></span>

<span data-ttu-id="0606a-150">No funciona con volúmenes bajos de telemetría, así que una aplicación en proceso de depuración o un sitio web con poca utilización no se verán afectados.</span><span class="sxs-lookup"><span data-stu-id="0606a-150">It doesn't operate at low volumes of telemetry, so an app in debugging or a website with low usage won't be affected.</span></span>

<span data-ttu-id="0606a-151">se descarta el volumen de destino de hello tooachieve, algunos de telemetría de hello generado.</span><span class="sxs-lookup"><span data-stu-id="0606a-151">tooachieve hello target volume, some of hello telemetry generated is discarded.</span></span> <span data-ttu-id="0606a-152">Pero al igual que otros tipos de muestreo, el algoritmo de hello conserva elementos de telemetría relacionada.</span><span class="sxs-lookup"><span data-stu-id="0606a-152">But like other types of sampling, hello algorithm retains related telemetry items.</span></span> <span data-ttu-id="0606a-153">Por ejemplo, al inspeccionar la telemetría de hello en la búsqueda, podrá excepciones concretas tooa relacionados con la solicitud de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="0606a-153">For example, when you're inspecting hello telemetry in Search, you'll be able toofind hello request related tooa particular exception.</span></span> 

<span data-ttu-id="0606a-154">Métrica de cuenta como tasa de solicitud y la tasa de excepciones están toocompensate ajustada para hello muestreo velocidad, para que muestren los valores correctos aproximadamente en el Explorador de métrica.</span><span class="sxs-lookup"><span data-stu-id="0606a-154">Metric counts such as request rate and exception rate are adjusted toocompensate for hello sampling rate, so that they show approximately correct values in Metric Explorer.</span></span>

<span data-ttu-id="0606a-155">**Actualizar NuGet su proyecto** paquetes toohello más reciente *preliminares* versión de Application Insights: haga clic en proyecto de hello en el Explorador de soluciones, elija Administrar paquetes de NuGet, consulte **Include versión preliminar** y busque Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="0606a-155">**Update your project's NuGet** packages toohello latest *pre-release* version of Application Insights: Right-click hello project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 

<span data-ttu-id="0606a-156">En [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), puede ajustar varios parámetros en hello `AdaptiveSamplingTelemetryProcessor` nodo.</span><span class="sxs-lookup"><span data-stu-id="0606a-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), you can adjust several parameters in hello `AdaptiveSamplingTelemetryProcessor` node.</span></span> <span data-ttu-id="0606a-157">cifras de Hola que se muestran son valores predeterminados de hello:</span><span class="sxs-lookup"><span data-stu-id="0606a-157">hello figures shown are hello default values:</span></span>

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    <span data-ttu-id="0606a-158">Hello velocidad de destino que Hola algoritmo adaptable tiene como objetivo **en cada host de servidor**.</span><span class="sxs-lookup"><span data-stu-id="0606a-158">hello target rate that hello adaptive algorithm aims for **on each server host**.</span></span> <span data-ttu-id="0606a-159">Si la aplicación web se ejecuta en varios hosts, por lo tanto como tooremain dentro de la tasa de destino de tráfico en el portal de Application Insights Hola reducir este valor.</span><span class="sxs-lookup"><span data-stu-id="0606a-159">If your web app runs on many hosts, reduce this value so as tooremain within your target rate of traffic at hello Application Insights portal.</span></span>
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    <span data-ttu-id="0606a-160">intervalo de saludo en qué Hola tasa actual de telemetría se vuelve a evaluar.</span><span class="sxs-lookup"><span data-stu-id="0606a-160">hello interval at which hello current rate of telemetry is re-evaluated.</span></span> <span data-ttu-id="0606a-161">La evaluación se realiza como una media móvil.</span><span class="sxs-lookup"><span data-stu-id="0606a-161">Evaluation is performed as a moving average.</span></span> <span data-ttu-id="0606a-162">Conviene tooshorten este intervalo si la telemetría es responsable toosudden ráfagas.</span><span class="sxs-lookup"><span data-stu-id="0606a-162">You might want tooshorten this interval if your telemetry is liable toosudden bursts.</span></span>
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    <span data-ttu-id="0606a-163">Una vez cambia de valor de porcentaje de muestreo, ¿con qué frecuencia después se permite toolower muestreo de porcentaje nuevo toocapture menos datos.</span><span class="sxs-lookup"><span data-stu-id="0606a-163">When sampling percentage value changes, how soon after are we allowed toolower sampling percentage again toocapture less data.</span></span>
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    <span data-ttu-id="0606a-164">Una vez cambia de valor de porcentaje de muestreo, ¿con qué frecuencia después se permite tooincrease muestreo de porcentaje nuevo toocapture más datos.</span><span class="sxs-lookup"><span data-stu-id="0606a-164">When sampling percentage value changes, how soon after are we allowed tooincrease sampling percentage again toocapture more data.</span></span>
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    <span data-ttu-id="0606a-165">Medida que varía de muestreo de porcentaje, ¿qué es el valor mínimo de Hola nos estamos permite tooset.</span><span class="sxs-lookup"><span data-stu-id="0606a-165">As sampling percentage varies, what is hello minimum value we're allowed tooset.</span></span>
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    <span data-ttu-id="0606a-166">Medida que varía de muestreo de porcentaje, ¿cuál es el valor máximo de hello nos estamos permite tooset.</span><span class="sxs-lookup"><span data-stu-id="0606a-166">As sampling percentage varies, what is hello maximum value we're allowed tooset.</span></span>
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    <span data-ttu-id="0606a-167">En el cálculo de Hola de hello Media móvil, peso Hola asignado valor más reciente de toohello.</span><span class="sxs-lookup"><span data-stu-id="0606a-167">In hello calculation of hello moving average, hello weight assigned toohello most recent value.</span></span> <span data-ttu-id="0606a-168">Use un tooor igual valor menor que 1.</span><span class="sxs-lookup"><span data-stu-id="0606a-168">Use a value equal tooor less than 1.</span></span> <span data-ttu-id="0606a-169">Los valores más pequeños modificar algoritmo Hola menos reactiva toosudden.</span><span class="sxs-lookup"><span data-stu-id="0606a-169">Smaller values make hello algorithm less reactive toosudden changes.</span></span>
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    <span data-ttu-id="0606a-170">valor de Hello asignado cuando se acaba de iniciar aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="0606a-170">hello value assigned when hello app has just started.</span></span> <span data-ttu-id="0606a-171">No lo reduzca durante la depuración.</span><span class="sxs-lookup"><span data-stu-id="0606a-171">Don't reduce this while you're debugging.</span></span> 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    <span data-ttu-id="0606a-172">Lista de tipos que no desea toobe muestrear delimitada por un punto y coma.</span><span class="sxs-lookup"><span data-stu-id="0606a-172">A semi-colon delimited list of types that you do not want toobe sampled.</span></span> <span data-ttu-id="0606a-173">Los tipos reconocidos son Dependency, Event, Exception, PageView, Request, Trace.</span><span class="sxs-lookup"><span data-stu-id="0606a-173">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="0606a-174">Todas las instancias de hello especifican se transmiten los tipos; se muestrean los tipos de Hola que no se especifican.</span><span class="sxs-lookup"><span data-stu-id="0606a-174">All instances of hello specified types are transmitted; hello types that are not specified are sampled.</span></span>

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    <span data-ttu-id="0606a-175">Una lista delimitada por punto y coma de tipos que desee toobe muestrear.</span><span class="sxs-lookup"><span data-stu-id="0606a-175">A semi-colon delimited list of types that you want toobe sampled.</span></span> <span data-ttu-id="0606a-176">Los tipos reconocidos son Dependency, Event, Exception, PageView, Request, Trace.</span><span class="sxs-lookup"><span data-stu-id="0606a-176">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="0606a-177">Hola especificado se muestrean tipos; todas las instancias de hello siempre se transmitirá otros tipos.</span><span class="sxs-lookup"><span data-stu-id="0606a-177">hello specified types are sampled; all instances of hello other types will always be transmitted.</span></span>


<span data-ttu-id="0606a-178">**tooswitch desactivar** muestreo adaptable, quitar un nodo AdaptiveSamplingTelemetryProcessor Hola desde la configuración de applicationinsights.</span><span class="sxs-lookup"><span data-stu-id="0606a-178">**tooswitch off** adaptive sampling, remove hello AdaptiveSamplingTelemetryProcessor node from applicationinsights-config.</span></span>

### <a name="alternative-configure-adaptive-sampling-in-code"></a><span data-ttu-id="0606a-179">Alternativa: configure el muestreo adaptivo en el código</span><span class="sxs-lookup"><span data-stu-id="0606a-179">Alternative: configure adaptive sampling in code</span></span>
<span data-ttu-id="0606a-180">En lugar de ajuste de muestreo en el archivo .config de hello, puede utilizar código.</span><span class="sxs-lookup"><span data-stu-id="0606a-180">Instead of adjusting sampling in hello .config file, you can use code.</span></span> <span data-ttu-id="0606a-181">Esto le permite toospecify una función de devolución de llamada que se invoca cuando se vuelve a evaluar la frecuencia de muestreo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0606a-181">This allows you toospecify a callback function that is invoked whenever hello sampling rate is re-evaluated.</span></span> <span data-ttu-id="0606a-182">Podría utilizar esto, por ejemplo, está usándola toofind fuera de la velocidad de muestreo.</span><span class="sxs-lookup"><span data-stu-id="0606a-182">You could use this, for example, toofind out what sampling rate is being used.</span></span>

<span data-ttu-id="0606a-183">Quitar hello `AdaptiveSamplingTelemetryProcessor` nodo desde el archivo .config de Hola.</span><span class="sxs-lookup"><span data-stu-id="0606a-183">Remove hello `AdaptiveSamplingTelemetryProcessor` node from hello .config file.</span></span>

<span data-ttu-id="0606a-184">*C#*</span><span class="sxs-lookup"><span data-stu-id="0606a-184">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust hello settings from their defaults.

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
             // Report hello sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="0606a-185">([Más información sobre los procesadores de telemetría](app-insights-api-filtering-sampling.md#filtering)).</span><span class="sxs-lookup"><span data-stu-id="0606a-185">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a><span data-ttu-id="0606a-186">Muestreo para páginas web con JavaScript</span><span class="sxs-lookup"><span data-stu-id="0606a-186">Sampling for web pages with JavaScript</span></span>
<span data-ttu-id="0606a-187">Puede configurar páginas web para el muestreo de frecuencia fija desde cualquier servidor.</span><span class="sxs-lookup"><span data-stu-id="0606a-187">You can configure web pages for fixed-rate sampling from any server.</span></span> 

<span data-ttu-id="0606a-188">Cuando se [configurar páginas web de Hola para Application Insights](app-insights-javascript.md), modificar el fragmento de código de hello que obtendrá de portal de Application Insights de Hola.</span><span class="sxs-lookup"><span data-stu-id="0606a-188">When you [configure hello web pages for Application Insights](app-insights-javascript.md), modify hello snippet that you get from hello Application Insights portal.</span></span> <span data-ttu-id="0606a-189">(En las aplicaciones ASP.NET, el fragmento de código de hello normalmente va en _Layout.cshtml.)  Insertar una línea como `samplingPercentage: 10,` antes de la clave de instrumentación de hello:</span><span class="sxs-lookup"><span data-stu-id="0606a-189">(In ASP.NET apps, hello snippet typically goes in _Layout.cshtml.)  Insert a line like `samplingPercentage: 10,` before hello instrumentation key:</span></span>

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

<span data-ttu-id="0606a-190">Para el porcentaje de muestreo de hello, elija un porcentaje que es cerrar too100/N donde N es un entero.</span><span class="sxs-lookup"><span data-stu-id="0606a-190">For hello sampling percentage, choose a percentage that is close too100/N where N is an integer.</span></span>  <span data-ttu-id="0606a-191">Actualmente el muestreo no es compatible con otros valores.</span><span class="sxs-lookup"><span data-stu-id="0606a-191">Currently sampling doesn't support other values.</span></span>

<span data-ttu-id="0606a-192">Si también habilita el muestreo de tipo fijo en el servidor de hello, servidor y los clientes de hello sincronizará por lo que, la búsqueda en, puede navegar entre las vistas de página relacionados y las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="0606a-192">If you also enable fixed-rate sampling at hello server, hello clients and server will synchronize so that, in Search, you can  navigate between related page views and requests.</span></span>

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a><span data-ttu-id="0606a-193">Muestreo de frecuencia fija para sitios web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0606a-193">Fixed-rate sampling for ASP.NET web sites</span></span>
<span data-ttu-id="0606a-194">Muestreo de tarifa fija que reduce el tráfico de hello enviado desde el servidor web y los exploradores web.</span><span class="sxs-lookup"><span data-stu-id="0606a-194">Fixed rate sampling reduces hello traffic sent from your web server and web browsers.</span></span> <span data-ttu-id="0606a-195">A diferencia del muestreo adaptable, reduce la telemetría a una tasa fija que usted decide.</span><span class="sxs-lookup"><span data-stu-id="0606a-195">Unlike adaptive sampling, it reduces telemetry at a fixed rate decided by you.</span></span> <span data-ttu-id="0606a-196">También sincroniza cliente hello y muestreo de servidor para que se conservan elementos relacionados: por ejemplo, por lo que si observa una vista de página en la búsqueda, puede encontrar su solicitud relacionadas.</span><span class="sxs-lookup"><span data-stu-id="0606a-196">It also synchronizes hello client and server sampling so that related items are retained - for example, so that if you look at a page view in Search, you can find its related request.</span></span>

<span data-ttu-id="0606a-197">algoritmo de muestreo de Hello conserva los elementos relacionados.</span><span class="sxs-lookup"><span data-stu-id="0606a-197">hello sampling algorithm retains related items.</span></span> <span data-ttu-id="0606a-198">Para cada evento de solicitud HTTP, este y sus eventos relacionados se descartan o transmiten.</span><span class="sxs-lookup"><span data-stu-id="0606a-198">For each HTTP request event, it and its related events are either discarded or transmitted.</span></span> 

<span data-ttu-id="0606a-199">En el Explorador de métricas, velocidades como recuentos de solicitud y la excepción se multiplican por un toocompensate de factor de velocidad de muestreo de hello, para que sean aproximadamente correctos.</span><span class="sxs-lookup"><span data-stu-id="0606a-199">In Metrics Explorer, rates such as request and exception counts are multiplied by a factor toocompensate for hello sampling rate, so that they are approximately correct.</span></span>

1. <span data-ttu-id="0606a-200">**Actualizar paquetes de NuGet de su proyecto** toohello más reciente *preliminares* versión de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0606a-200">**Update your project's NuGet packages** toohello latest *pre-release* version of Application Insights.</span></span> <span data-ttu-id="0606a-201">Haga clic en proyecto de hello en el Explorador de soluciones, elija Administrar paquetes de NuGet, consulte **incluir versión preliminar** y busque Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="0606a-201">Right-click hello project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 
2. <span data-ttu-id="0606a-202">**Deshabilitar muestreo adaptativo**: en [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), quite o marque como comentario hello `AdaptiveSamplingTelemetryProcessor` nodo.</span><span class="sxs-lookup"><span data-stu-id="0606a-202">**Disable adaptive sampling**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), remove or comment out hello `AdaptiveSamplingTelemetryProcessor` node.</span></span>
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. <span data-ttu-id="0606a-203">**Habilitar el módulo de tipo fijo muestreo de Hola.**</span><span class="sxs-lookup"><span data-stu-id="0606a-203">**Enable hello fixed-rate sampling module.**</span></span> <span data-ttu-id="0606a-204">Agregue este fragmento demasiado[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="0606a-204">Add this snippet too[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> <span data-ttu-id="0606a-205">Para el porcentaje de muestreo de hello, elija un porcentaje que es cerrar too100/N donde N es un entero.</span><span class="sxs-lookup"><span data-stu-id="0606a-205">For hello sampling percentage, choose a percentage that is close too100/N where N is an integer.</span></span>  <span data-ttu-id="0606a-206">Actualmente el muestreo no es compatible con otros valores.</span><span class="sxs-lookup"><span data-stu-id="0606a-206">Currently sampling doesn't support other values.</span></span>
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a><span data-ttu-id="0606a-207">Alternativa: habilitación del muestreo de frecuencia fija en el código de servidor</span><span class="sxs-lookup"><span data-stu-id="0606a-207">Alternative: enable fixed-rate sampling in your server code</span></span>
<span data-ttu-id="0606a-208">En lugar de establecer el parámetro de muestreo de hello en el archivo .config de hello, puede utilizar código.</span><span class="sxs-lookup"><span data-stu-id="0606a-208">Instead of setting hello sampling parameter in hello .config file, you can use code.</span></span> 

<span data-ttu-id="0606a-209">*C#*</span><span class="sxs-lookup"><span data-stu-id="0606a-209">*C#*</span></span>

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

<span data-ttu-id="0606a-210">([Más información sobre los procesadores de telemetría](app-insights-api-filtering-sampling.md#filtering)).</span><span class="sxs-lookup"><span data-stu-id="0606a-210">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

## <a name="when-toouse-sampling"></a><span data-ttu-id="0606a-211">¿Cuando toouse muestreo?</span><span class="sxs-lookup"><span data-stu-id="0606a-211">When toouse sampling?</span></span>
<span data-ttu-id="0606a-212">Muestreo adaptable se habilita automáticamente si usas hello 2.0.0-beta3 de versión de SDK de ASP.NET o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="0606a-212">Adaptive sampling is automatically enabled if you use hello ASP.NET SDK version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="0606a-213">Independientemente de la versión del SDK que utilice, puede emplear el muestreo de ingesta (en nuestro servidor).</span><span class="sxs-lookup"><span data-stu-id="0606a-213">No matter what SDK version you use, you can use ingestion sampling (at our server).</span></span>

<span data-ttu-id="0606a-214">Para la mayoría de las aplicaciones pequeñas y medianas no es necesario realizar muestreos.</span><span class="sxs-lookup"><span data-stu-id="0606a-214">You don’t need sampling for most small and medium size applications.</span></span> <span data-ttu-id="0606a-215">información de diagnóstico más útil de Hola y estadísticas más precisas se obtienen mediante la recopilación de datos en todas las actividades de usuario.</span><span class="sxs-lookup"><span data-stu-id="0606a-215">hello most useful diagnostic information and most accurate statistics are obtained by collecting data on all your user activities.</span></span> 

<span data-ttu-id="0606a-216">son las principales ventajas de Hola de muestreo:</span><span class="sxs-lookup"><span data-stu-id="0606a-216">hello main advantages of sampling are:</span></span>

* <span data-ttu-id="0606a-217">El servicio de Application Insights descarta ("limita") puntos de datos cuando la aplicación envía un número muy elevado de telemetría en un intervalo de tiempo corto.</span><span class="sxs-lookup"><span data-stu-id="0606a-217">Application Insights service drops ("throttles") data points when your app sends a very high rate of telemetry in short time interval.</span></span> 
* <span data-ttu-id="0606a-218">tookeep dentro de hello [cuota](app-insights-pricing.md) de puntos de datos para el nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="0606a-218">tookeep within hello [quota](app-insights-pricing.md) of data points for your pricing tier.</span></span> 
* <span data-ttu-id="0606a-219">tráfico de red tooreduce de colección de Hola de telemetría.</span><span class="sxs-lookup"><span data-stu-id="0606a-219">tooreduce network traffic from hello collection of telemetry.</span></span> 

### <a name="which-type-of-sampling-should-i-use"></a><span data-ttu-id="0606a-220">¿Qué tipo de muestreo debo utilizar?</span><span class="sxs-lookup"><span data-stu-id="0606a-220">Which type of sampling should I use?</span></span>
<span data-ttu-id="0606a-221">**Use el muestreo de ingesta si:**</span><span class="sxs-lookup"><span data-stu-id="0606a-221">**Use ingestion sampling if:**</span></span>

* <span data-ttu-id="0606a-222">Con frecuencia sobrepasa su cuota mensual de telemetría.</span><span class="sxs-lookup"><span data-stu-id="0606a-222">You often go through your monthly quota of telemetry.</span></span>
* <span data-ttu-id="0606a-223">Está usando una versión de Hola SDK que no admite el muestreo - por ejemplo, hello Java SDK o versiones ASP.NET anteriores a 2.</span><span class="sxs-lookup"><span data-stu-id="0606a-223">You're using a version of hello SDK that doesn't support sampling - for example, hello Java SDK or ASP.NET versions earlier than 2.</span></span>
* <span data-ttu-id="0606a-224">Recibe mucha telemetría de los exploradores web de sus usuarios.</span><span class="sxs-lookup"><span data-stu-id="0606a-224">You're getting a lot of telemetry from your users' web browsers.</span></span>

<span data-ttu-id="0606a-225">**Use el muestreo de frecuencia fija si:**</span><span class="sxs-lookup"><span data-stu-id="0606a-225">**Use fixed-rate sampling if:**</span></span>

* <span data-ttu-id="0606a-226">Usa Hola Application Insights SDK para la versión de servicios web ASP.NET 2.0.0 o posterior, y</span><span class="sxs-lookup"><span data-stu-id="0606a-226">You're using hello Application Insights SDK for ASP.NET web services version 2.0.0 or later, and</span></span>
* <span data-ttu-id="0606a-227">Desea muestreo sincronizados entre cliente y servidor, por lo que, cuando se está investigando eventos en [búsqueda](app-insights-diagnostic-search.md), puede navegar entre los eventos relacionados en el cliente de Hola y servidor, como las vistas de página y las solicitudes http.</span><span class="sxs-lookup"><span data-stu-id="0606a-227">You want synchronized sampling between client and server, so that, when you're investigating events in [Search](app-insights-diagnostic-search.md), you can navigate between related events on hello client and server, such as page views and http requests.</span></span>
* <span data-ttu-id="0606a-228">Esté seguro de porcentaje de hello muestreo adecuado para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0606a-228">You are confident of hello appropriate sampling percentage for your app.</span></span> <span data-ttu-id="0606a-229">Debe estar suficientemente alto tooget métricas precisas, pero a continuación Hola velocidad que supera la cuota de precios y Hola límites de procesos.</span><span class="sxs-lookup"><span data-stu-id="0606a-229">It should be high enough tooget accurate metrics, but below hello rate that exceeds your pricing quota and hello throttling limits.</span></span> 

<span data-ttu-id="0606a-230">**Use el muestreo adaptable si:**</span><span class="sxs-lookup"><span data-stu-id="0606a-230">**Use adaptive sampling:**</span></span>

<span data-ttu-id="0606a-231">De lo contrario, se recomienda el muestreo adaptable.</span><span class="sxs-lookup"><span data-stu-id="0606a-231">Otherwise, we recommend adaptive sampling.</span></span> <span data-ttu-id="0606a-232">Esta opción está habilitada de forma predeterminada en el servidor ASP.NET Hola SDK, versión 2.0.0-beta3 o posterior.</span><span class="sxs-lookup"><span data-stu-id="0606a-232">This is enabled by default in hello ASP.NET server SDK, version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="0606a-233">No reduce el tráfico hasta una determinada tasa mínima, así que no afectará a los sitios de utilización baja.</span><span class="sxs-lookup"><span data-stu-id="0606a-233">It doesn't reduce traffic until a certain minimum rate, so it won't affect a low-use site.</span></span>

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a><span data-ttu-id="0606a-234">¿Cómo se puede saber si el muestreo está en funcionamiento?</span><span class="sxs-lookup"><span data-stu-id="0606a-234">How do I know whether sampling is in operation?</span></span>
<span data-ttu-id="0606a-235">hello toodiscover real muestreo tasa independientemente de donde se ha aplicado, use un [consulta de análisis](app-insights-analytics.md) como este:</span><span class="sxs-lookup"><span data-stu-id="0606a-235">toodiscover hello actual sampling rate no matter where it has been applied, use an [Analytics query](app-insights-analytics.md) such as this:</span></span>

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

<span data-ttu-id="0606a-236">En cada uno de ellos conserva el registro, `itemCount` indica Hola número de registros original que representa, too1 igual + número de Hola de registros descartados anteriores.</span><span class="sxs-lookup"><span data-stu-id="0606a-236">In each retained record, `itemCount` indicates hello number of original records that it represents, equal too1 + hello number of previous discarded records.</span></span> 

## <a name="how-does-sampling-work"></a><span data-ttu-id="0606a-237">¿Cómo funciona el muestreo?</span><span class="sxs-lookup"><span data-stu-id="0606a-237">How does sampling work?</span></span>
<span data-ttu-id="0606a-238">Tipo fijo y muestreo adaptativo son una característica de hello SDK en las versiones de ASP.NET de 2.0.0 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="0606a-238">Fixed-rate and adaptive sampling are a feature of hello SDK in ASP.NET versions from 2.0.0 onwards.</span></span> <span data-ttu-id="0606a-239">Muestreo de recopilación es una característica de hello servicio Application Insights y puede estar en funcionamiento si Hola SDK no está realizando el muestreo.</span><span class="sxs-lookup"><span data-stu-id="0606a-239">Ingestion sampling is a feature of hello Application Insights service, and can be in operation if hello SDK is not performing sampling.</span></span> 

<span data-ttu-id="0606a-240">algoritmo de muestreo de Hello decide qué toodrop de elementos de telemetría y qué tookeep los (si está en hello SDK o en servicio de Application Insights de hello).</span><span class="sxs-lookup"><span data-stu-id="0606a-240">hello sampling algorithm decides which telemetry items toodrop, and which ones tookeep (whether it's in hello SDK or in hello Application Insights service).</span></span> <span data-ttu-id="0606a-241">Decisión de muestreo de Hola se basa en varias reglas que tienen como objetivo toopreserve todos los puntos de datos interrelacionados intacto y mantener una experiencia de diagnóstico en Application Insights que es práctica y confiable incluso con un conjunto de datos reducido.</span><span class="sxs-lookup"><span data-stu-id="0606a-241">hello sampling decision is based on several rules that aim toopreserve all interrelated data points intact, maintaining a diagnostic experience in Application Insights that is actionable and reliable even with a reduced data set.</span></span> <span data-ttu-id="0606a-242">Por ejemplo, si para una solicitud errónea su aplicación envía elementos de telemetría adicionales (como la excepción y los seguimientos registrados para dicha solicitud), el muestreo no dividirá esta solicitud y otra telemetría.</span><span class="sxs-lookup"><span data-stu-id="0606a-242">For example, if for a failed request your app sends additional telemetry items (such as exception and traces logged from this request), sampling will not split this request and other telemetry.</span></span> <span data-ttu-id="0606a-243">Escogerá mantenerlos o descartarlos todos juntos</span><span class="sxs-lookup"><span data-stu-id="0606a-243">It either keeps or drops them all together.</span></span> <span data-ttu-id="0606a-244">Como resultado, cuando se examina en detalles de la solicitud de hello en Application Insights, siempre puede ver solicitud Hola junto con sus elementos de telemetría asociado.</span><span class="sxs-lookup"><span data-stu-id="0606a-244">As a result, when you look at hello request details in Application Insights, you can always see hello request along with its associated telemetry items.</span></span> 

<span data-ttu-id="0606a-245">Para las aplicaciones que definen el "usuario" (es decir, las aplicaciones web más típicas), decisión de muestreo de Hola se basa en el hash de Hola de Id. de usuario de hello, lo que significa que todos los telemetría para un usuario concreto se conserva o se quita.</span><span class="sxs-lookup"><span data-stu-id="0606a-245">For applications that define "user" (that is, most typical web applications), hello sampling decision is based on hello hash of hello user id, which means that all telemetry for any particular user is either preserved or dropped.</span></span> <span data-ttu-id="0606a-246">Para los tipos de Hola de aplicaciones que no definen los usuarios (por ejemplo, servicios web) Decisión de muestreo de Hola se basa en Id. de operación de saludo de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="0606a-246">For hello types of applications that don't define users (such as web services) hello sampling decision is based on hello operation id of hello request.</span></span> <span data-ttu-id="0606a-247">Por último, para los elementos de telemetría de Hola que no tienen el identificador de usuario ni la operación de conjunto (por ejemplo elementos de telemetría notificados de subprocesos asincrónicos no tienen ningún contexto de http) muestreo simplemente captura un porcentaje de elementos de telemetría de cada tipo.</span><span class="sxs-lookup"><span data-stu-id="0606a-247">Finally, for hello telemetry items that neither have user nor operation id set (for example telemetry items reported from asynchronous threads with no http context) sampling simply captures a percentage of telemetry items of each type.</span></span> 

<span data-ttu-id="0606a-248">Cuando se presentan tooyou atrás de telemetría, Hola Application Insights servicio ajusta las métricas de Hola por Hola mismo porcentaje de muestreo que se usaron en tiempo de Hola de colección, toocompensate para hello puntos de datos que faltan.</span><span class="sxs-lookup"><span data-stu-id="0606a-248">When presenting telemetry back tooyou, hello Application Insights service adjusts hello metrics by hello same sampling percentage that was used at hello time of collection, toocompensate for hello missing data points.</span></span> <span data-ttu-id="0606a-249">Por lo tanto, al examinar telemetría hello en Application Insights, los usuarios de hello están viendo aproximaciones estadísticamente correctas que son muy próxima toohello los números reales.</span><span class="sxs-lookup"><span data-stu-id="0606a-249">Hence, when looking at hello telemetry in Application Insights, hello users are seeing statistically correct approximations that are very close toohello real numbers.</span></span>

<span data-ttu-id="0606a-250">precisión de Hola de aproximación de hello depende en gran medida de porcentaje de muestreo de hello configurado.</span><span class="sxs-lookup"><span data-stu-id="0606a-250">hello accuracy of hello approximation largely depends on hello configured sampling percentage.</span></span> <span data-ttu-id="0606a-251">Asimismo, precisión Hola aumenta para aplicaciones que manejan un gran volumen de solicitudes suelen ser parecidos de una gran cantidad de usuarios.</span><span class="sxs-lookup"><span data-stu-id="0606a-251">Also, hello accuracy increases for applications that handle a large volume of generally similar requests from lots of users.</span></span> <span data-ttu-id="0606a-252">En Hola otra parte, para las aplicaciones que no funcionan con una carga significativa, no es necesario el muestreo como para estas aplicaciones normalmente pueden enviar todas su telemetría manteniéndose dentro de la cuota de hello, sin causar pérdida de datos de la limitación.</span><span class="sxs-lookup"><span data-stu-id="0606a-252">On hello other hand, for applications that don't work with a significant load, sampling is not needed as these applications can usually send all their telemetry while staying within hello quota, without causing data loss from throttling.</span></span> 

<span data-ttu-id="0606a-253">Tenga en cuenta que Application Insights no muestra tipos de telemetría de métricas y las sesiones, desde para estos tipos, reducción de la precisión de hello puede ser muy deseable.</span><span class="sxs-lookup"><span data-stu-id="0606a-253">Note that Application Insights does not sample Metrics and Sessions telemetry types, since for these types, reduction in hello precision can be highly undesirable.</span></span> 

### <a name="adaptive-sampling"></a><span data-ttu-id="0606a-254">muestreo adaptable</span><span class="sxs-lookup"><span data-stu-id="0606a-254">Adaptive sampling</span></span>
<span data-ttu-id="0606a-255">Muestreo adaptativo agrega esa tasa actual de Hola de monitores de transmisión de un componente de hello SDK y ajusta Hola muestreo porcentaje tootry toostay dentro de la velocidad máxima del destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="0606a-255">Adaptive sampling adds a component that monitors hello current rate of transmission from hello SDK, and adjusts hello sampling percentage tootry toostay within hello target maximum rate.</span></span> <span data-ttu-id="0606a-256">ajuste de Hola se vuelve a calcular a intervalos regulares y se basa en una media móvil de hello velocidad de transmisión de salida.</span><span class="sxs-lookup"><span data-stu-id="0606a-256">hello adjustment is recalculated at regular intervals, and is based on a moving average of hello outgoing transmission rate.</span></span>

## <a name="sampling-and-hello-javascript-sdk"></a><span data-ttu-id="0606a-257">Hello SDK de JavaScript y muestreo</span><span class="sxs-lookup"><span data-stu-id="0606a-257">Sampling and hello JavaScript SDK</span></span>
<span data-ttu-id="0606a-258">Hola cliente (JavaScript) SDK participa en tipo fijo muestreo junto con el servidor de hello SDK.</span><span class="sxs-lookup"><span data-stu-id="0606a-258">hello client-side (JavaScript) SDK participates in fixed-rate sampling in conjunction with hello server-side SDK.</span></span> <span data-ttu-id="0606a-259">páginas de Hello instrumentado sólo enviará telemetría de cliente de hello mismos usuarios para qué Hola servidor realiza su decisión demasiado "de ejemplo en."</span><span class="sxs-lookup"><span data-stu-id="0606a-259">hello instrumented pages will only send client-side telemetry from hello same users for which hello server-side made its decision too"sample in."</span></span> <span data-ttu-id="0606a-260">Esta lógica es la integridad de toomaintain diseñada de sesión de usuario a través de lado cliente y servidor.</span><span class="sxs-lookup"><span data-stu-id="0606a-260">This logic is designed toomaintain integrity of user session across client- and server-sides.</span></span> <span data-ttu-id="0606a-261">Como resultado, a partir de cualquier elemento específico de telemetría en Application Insights, puede encontrar todos los demás elementos de telemetría para ese usuario o esa sesión.</span><span class="sxs-lookup"><span data-stu-id="0606a-261">As a result, from any particular telemetry item in Application Insights you can find all other telemetry items for this user or session.</span></span> 

<span data-ttu-id="0606a-262">*Las telemetrías del lado de cliente y de servidor no muestran ejemplos coordinados tal y como se describe anteriormente.*</span><span class="sxs-lookup"><span data-stu-id="0606a-262">*My client and server-side telemetry don't show coordinated samples as you describe above.*</span></span>

* <span data-ttu-id="0606a-263">Compruebe que habilitó el muestreo de frecuencia fija tanto en el cliente como en el servidor.</span><span class="sxs-lookup"><span data-stu-id="0606a-263">Verify that you enabled fixed-rate sampling both on server and client.</span></span>
* <span data-ttu-id="0606a-264">Asegúrese de que esa versión SDK de hello es 2.0 o superior.</span><span class="sxs-lookup"><span data-stu-id="0606a-264">Make sure that hello SDK version is 2.0 or above.</span></span>
* <span data-ttu-id="0606a-265">Compruebe que establece Hola mismo muestreo de porcentaje en el cliente de Hola y el servidor.</span><span class="sxs-lookup"><span data-stu-id="0606a-265">Check that you set hello same sampling percentage in both hello client and server.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="0606a-266">Preguntas frecuentes</span><span class="sxs-lookup"><span data-stu-id="0606a-266">Frequently Asked Questions</span></span>
<span data-ttu-id="0606a-267">*¿Por qué realizar un muestreo no consiste simplemente en "recopilar X por ciento de cada tipo de telemetría"?*</span><span class="sxs-lookup"><span data-stu-id="0606a-267">*Why isn't sampling a simple "collect X percent of each telemetry type"?*</span></span>

* <span data-ttu-id="0606a-268">Aunque este método de muestreo se proporcionan con una precisión de muy alta en aproximaciones métricas, interrumpirá datos de diagnóstico de capacidad toocorrelate por usuario, la sesión y la solicitud, lo cual resulta esencial para diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="0606a-268">While this sampling approach would provide with a very high precision in metric approximations, it would break ability toocorrelate diagnostic data per user, session, and request, which is critical for diagnostics.</span></span> <span data-ttu-id="0606a-269">Por lo tanto, el muestreo funciona mejor con una lógica "recopilar todos los elementos de telemetría para X por ciento de los usuarios de la aplicación", o "recopilar toda la telemetría para X por ciento de las solicitudes de aplicación".</span><span class="sxs-lookup"><span data-stu-id="0606a-269">Therefore, sampling works better with "collect all telemetry items for X percent of app users", or "collect all telemetry for X percent of app requests" logic.</span></span> <span data-ttu-id="0606a-270">Para los elementos de telemetría de hello no asociados a las solicitudes de hello (por ejemplo, el procesamiento asincrónico en segundo plano), otoño de hello volver resulta demasiado "recopilar X por ciento de todos los elementos de cada tipo de telemetría."</span><span class="sxs-lookup"><span data-stu-id="0606a-270">For hello telemetry items not associated with hello requests (such as background asynchronous processing), hello fall back is too"collect X percent of all items for each telemetry type."</span></span> 

<span data-ttu-id="0606a-271">*¿Porcentaje de muestreo de hello cambian con el tiempo?*</span><span class="sxs-lookup"><span data-stu-id="0606a-271">*Can hello sampling percentage change over time?*</span></span>

* <span data-ttu-id="0606a-272">Sí, cambia porcentaje de muestreo de hello, en función de hello observados actualmente el volumen de telemetría de hello adaptable gradualmente de muestreo.</span><span class="sxs-lookup"><span data-stu-id="0606a-272">Yes, adaptive sampling gradually changes hello sampling percentage, based on hello currently observed volume of hello telemetry.</span></span>

<span data-ttu-id="0606a-273">*Si utiliza el muestreo de tipo fijo, ¿cómo puedo saber qué muestreo de porcentaje funcionará Hola mejor para mi aplicación?*</span><span class="sxs-lookup"><span data-stu-id="0606a-273">*If I use fixed-rate sampling, how do I know which sampling percentage will work hello best for my app?*</span></span>

* <span data-ttu-id="0606a-274">Una manera es toostart con muestreo adaptable, obtenga más información sobre qué clasificarlo liquida en (consulte Hola pregunta anterior), y, a continuación, con esa tasa de muestreo de velocidad toofixed de conmutador.</span><span class="sxs-lookup"><span data-stu-id="0606a-274">One way is toostart with adaptive sampling, find out what rate it settles on (see hello above question), and then switch toofixed-rate sampling using that rate.</span></span> 
  
    <span data-ttu-id="0606a-275">De lo contrario, tendrá que tooguess.</span><span class="sxs-lookup"><span data-stu-id="0606a-275">Otherwise, you have tooguess.</span></span> <span data-ttu-id="0606a-276">Analizar el uso actual de telemetría en AI, observe cualquier limitación es decir que se producen y volumen de Hola de estimación de telemetría recopilado de Hola.</span><span class="sxs-lookup"><span data-stu-id="0606a-276">Analyze your current telemetry usage in AI, observe any throttling that is occurring, and estimate hello volume of hello collected telemetry.</span></span> <span data-ttu-id="0606a-277">Estas tres entradas, junto con el nivel de precios seleccionado, sugieren cuánto puede tooreduce volumen de Hola de telemetría recopilado de Hola.</span><span class="sxs-lookup"><span data-stu-id="0606a-277">These three inputs, together with your selected pricing tier, suggest how much you might want tooreduce hello volume of hello collected telemetry.</span></span> <span data-ttu-id="0606a-278">Sin embargo, un aumento en número de Hola de los usuarios o algunas otras MAYÚS en volumen de Hola de telemetría podrían invalidar la estimación.</span><span class="sxs-lookup"><span data-stu-id="0606a-278">However, an increase in hello number of your users or some other shift in hello volume of telemetry might invalidate your estimate.</span></span>

<span data-ttu-id="0606a-279">*¿Qué sucede si configuro un porcentaje de muestreo demasiado bajo?*</span><span class="sxs-lookup"><span data-stu-id="0606a-279">*What happens if I configure sampling percentage too low?*</span></span>

* <span data-ttu-id="0606a-280">Porcentaje de muestreo excesivamente baja (muestreo demasiado minuciosa) reduce precisión Hola de aproximaciones hello, cuando trate de Application Insights visualización de hello toocompensate de datos de hello para la reducción de volumen de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0606a-280">Excessively low sampling percentage (over-aggressive sampling) reduces hello accuracy of hello approximations, when Application Insights attempts toocompensate hello visualization of hello data for hello data volume reduction.</span></span> <span data-ttu-id="0606a-281">Además, diagnóstico experiencia podría verse afectado negativamente, como algunos de hello con poca frecuencia se producen errores o se pueden muestrear solicitudes lentas.</span><span class="sxs-lookup"><span data-stu-id="0606a-281">Also, diagnostic experience might be negatively impacted, as some of hello infrequently failing or slow requests may be sampled out.</span></span>

<span data-ttu-id="0606a-282">*¿Qué sucede si configuro un porcentaje de muestreo demasiado alto?*</span><span class="sxs-lookup"><span data-stu-id="0606a-282">*What happens if I configure sampling percentage too high?*</span></span>

* <span data-ttu-id="0606a-283">Configurar muestreo demasiado alto porcentaje (no agresiva suficientemente) resultados una reducción insuficiente del volumen Hola de hello recopilan telemetría.</span><span class="sxs-lookup"><span data-stu-id="0606a-283">Configuring too high sampling percentage (not aggressive enough) results in an insufficient reduction in hello volume of hello collected telemetry.</span></span> <span data-ttu-id="0606a-284">Todavía puede experimentar pérdida de datos relacionados con toothrottling y el costo de Hola de usar Application Insights pueden ser mayor que el planeó debido toooverage cargos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="0606a-284">You may still experience telemetry data loss related toothrottling, and hello cost of using Application Insights might be higher than you planned due toooverage charges.</span></span>

<span data-ttu-id="0606a-285">*¿En qué plataformas puedo usar muestreo?*</span><span class="sxs-lookup"><span data-stu-id="0606a-285">*On what platforms can I use sampling?*</span></span>

* <span data-ttu-id="0606a-286">Muestreo de ingesta podrá realizarse automáticamente para cualquier telemetría por encima de un volumen si Hola SDK no está realizando el muestreo.</span><span class="sxs-lookup"><span data-stu-id="0606a-286">Ingestion sampling can occur automatically for any telemetry above a certain volume, if hello SDK is not performing sampling.</span></span> <span data-ttu-id="0606a-287">Esto podría funcionar, por ejemplo, si su aplicación usa un servidor de Java, o si está utilizando una versión anterior de hello SDK de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0606a-287">This would work, for example, if your app uses a Java server, or if you are using an older version of hello ASP.NET SDK.</span></span>
* <span data-ttu-id="0606a-288">Si usa las versiones del SDK de ASP.NET 2.0.0 y versiones posteriores (hospedado en Azure o en su propio servidor), recibirá adaptable de muestreo de forma predeterminada, pero puede cambiar la tasa de toofixed tal y como se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0606a-288">If you're using ASP.NET SDK versions 2.0.0 and above (hosted either in Azure or on your own server), you get adaptive sampling by default, but you can switch toofixed-rate as described above.</span></span> <span data-ttu-id="0606a-289">Con el muestreo de tipo fijo, Explorador de hello SDK sincroniza automáticamente toosample eventos relacionados.</span><span class="sxs-lookup"><span data-stu-id="0606a-289">With fixed-rate sampling, hello browser SDK automatically synchronizes toosample related events.</span></span> 

<span data-ttu-id="0606a-290">*Hay ciertos eventos excepcionales toosee suele. ¿Cómo se puede obtener ellos más allá de muestreo de hello módulo?*</span><span class="sxs-lookup"><span data-stu-id="0606a-290">*There are certain rare events I always want toosee. How can I get them past hello sampling module?*</span></span>

* <span data-ttu-id="0606a-291">Inicializar una instancia independiente de TelemetryClient con un nuevo TelemetryConfiguration (no Hola de forma predeterminada está activa).</span><span class="sxs-lookup"><span data-stu-id="0606a-291">Initialize a separate instance of TelemetryClient with a new TelemetryConfiguration (not hello default Active one).</span></span> <span data-ttu-id="0606a-292">Use ese toosend los eventos excepcionales.</span><span class="sxs-lookup"><span data-stu-id="0606a-292">Use that toosend your rare events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0606a-293">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0606a-293">Next steps</span></span>
* <span data-ttu-id="0606a-294">[filtro](app-insights-api-filtering-sampling.md) puede proporcionar un control más estricto de los SDK que envía.</span><span class="sxs-lookup"><span data-stu-id="0606a-294">[Filtering](app-insights-api-filtering-sampling.md) can provide more strict control of what your SDK sends.</span></span>

