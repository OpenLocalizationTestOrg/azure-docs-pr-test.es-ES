---
title: aplicaciones de aaaDebug con Azure Application Insights en Visual Studio | Documentos de Microsoft
description: "Análisis del rendimiento y diagnóstico de aplicaciones web durante la depuración y en producción."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/7/2017
ms.author: bwren
ms.openlocfilehash: 20491fbe4505bf719039e5d1c220b1afec01db25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a><span data-ttu-id="6f435-103">Depure sus aplicaciones con Azure Application Insights en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6f435-103">Debug your applications with Azure Application Insights in Visual Studio</span></span>
<span data-ttu-id="6f435-104">En Visual Studio (2015 y versiones posteriores), se pueden diagnosticar y analizar los problemas de rendimiento de las aplicaciones web, tanto en tiempo de depuración como en producción, mediante los datos de telemetría de [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6f435-104">In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="6f435-105">Si ha creado la aplicación web ASP.NET mediante Visual Studio de 2017 o versiones posteriores, ya tiene Hola Application Insights SDK.</span><span class="sxs-lookup"><span data-stu-id="6f435-105">If you created your ASP.NET web app using Visual Studio 2017 or later, it already has hello Application Insights SDK.</span></span> <span data-ttu-id="6f435-106">En caso contrario, si aún no lo ha hecho lo ha hecho, [agregar Application Insights tooyour aplicación](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="6f435-106">Otherwise, if you haven't done so already, [add Application Insights tooyour app](app-insights-asp-net.md).</span></span>

<span data-ttu-id="6f435-107">toomonitor la aplicación cuando se encuentra en producción en vivo, normalmente ver telemetría de Application Insights Hola Hola [portal de Azure](https://portal.azure.com), donde puede establecer alertas y aplicar las eficaces herramientas de supervisión.</span><span class="sxs-lookup"><span data-stu-id="6f435-107">toomonitor your app when it's in live production, you normally view hello Application Insights telemetry in hello [Azure portal](https://portal.azure.com), where you can set alerts and apply powerful monitoring tools.</span></span> <span data-ttu-id="6f435-108">Pero para la depuración, también puede buscar y analizar la telemetría de hello en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6f435-108">But for debugging, you can also search and analyze hello telemetry in Visual Studio.</span></span> <span data-ttu-id="6f435-109">Puede usar la telemetría de tooanalyze de Visual Studio desde su sitio de producción y de depuración se ejecuta en el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="6f435-109">You can use Visual Studio tooanalyze telemetry both from your production site and from debugging runs on your development machine.</span></span> <span data-ttu-id="6f435-110">En este último caso hello, puede analizar ejecuciones de depuración incluso si todavía no ha configurado Hola SDK toosend telemetría toohello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6f435-110">In hello latter case, you can analyze debugging runs even if you haven't yet configured hello SDK toosend telemetry toohello Azure portal.</span></span> 

## <span data-ttu-id="6f435-111"><a name="run"></a> Depure el proyecto</span><span class="sxs-lookup"><span data-stu-id="6f435-111"><a name="run"></a> Debug your project</span></span>
<span data-ttu-id="6f435-112">Ejecute la aplicación web en modo de depuración local mediante F5.</span><span class="sxs-lookup"><span data-stu-id="6f435-112">Run your web app in local debug mode by using F5.</span></span> <span data-ttu-id="6f435-113">Abra distintas páginas toogenerate algunos telemetría.</span><span class="sxs-lookup"><span data-stu-id="6f435-113">Open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="6f435-114">En Visual Studio, verá un recuento de eventos de Hola que se han registrado por el módulo de Application Insights de hello en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="6f435-114">In Visual Studio, you see a count of hello events that have been logged by hello Application Insights module in your project.</span></span>

![En Visual Studio, el botón de Application Insights de Hola muestra durante la depuración.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

<span data-ttu-id="6f435-116">Haga clic en este botón toosearch la telemetría.</span><span class="sxs-lookup"><span data-stu-id="6f435-116">Click this button toosearch your telemetry.</span></span> 

## <a name="application-insights-search"></a><span data-ttu-id="6f435-117">Búsqueda de Application Insights</span><span class="sxs-lookup"><span data-stu-id="6f435-117">Application Insights search</span></span>
<span data-ttu-id="6f435-118">ventana de búsqueda de visión de la aplicación Hello muestra eventos que se han registrado.</span><span class="sxs-lookup"><span data-stu-id="6f435-118">hello Application Insights Search window shows events that have been logged.</span></span> <span data-ttu-id="6f435-119">(Si se suscribió en tooAzure al configurar Application Insights, puede buscar Hola mismos eventos Hola portal de Azure.)</span><span class="sxs-lookup"><span data-stu-id="6f435-119">(If you signed in tooAzure when you set up Application Insights, you can search hello same events in hello Azure portal.)</span></span>

![Haga clic en proyecto de Hola y elija Application Insights, búsqueda](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> <span data-ttu-id="6f435-121">Después de seleccionar o anular la selección de filtros, haga clic en botón de búsqueda de hello final Hola del campo de búsqueda de texto hello.</span><span class="sxs-lookup"><span data-stu-id="6f435-121">After you select or deselect filters, click hello Search button at hello end of hello text search field.</span></span>
>

<span data-ttu-id="6f435-122">búsqueda de texto sin formato de Hello funciona en todos los campos de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f435-122">hello free text search works on any fields in hello events.</span></span> <span data-ttu-id="6f435-123">Por ejemplo, buscar una parte de hello URL de una página; u Hola valor de una propiedad como ciudad del cliente; o palabras específicas en un registro de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="6f435-123">For example, search for part of hello URL of a page; or hello value of a property such as client city; or specific words in a trace log.</span></span>

<span data-ttu-id="6f435-124">Haga clic en cualquier evento toosee sus propiedades en detalle.</span><span class="sxs-lookup"><span data-stu-id="6f435-124">Click any event toosee its detailed properties.</span></span>

<span data-ttu-id="6f435-125">Para la aplicación web de solicitudes tooyour, puede hacer clic en a través del código de toohello.</span><span class="sxs-lookup"><span data-stu-id="6f435-125">For requests tooyour web app, you can click through toohello code.</span></span>

![En detalles de la solicitud, haga clic en a través del código de toohello](./media/app-insights-visual-studio/31.png)

<span data-ttu-id="6f435-127">También puede abrir elementos relacionados toohelp diagnosticar las solicitudes con error o las excepciones.</span><span class="sxs-lookup"><span data-stu-id="6f435-127">You can also open related items toohelp diagnose failed requests or exceptions.</span></span>

![En detalles de la solicitud, desplácese hacia abajo toorelated elementos](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a><span data-ttu-id="6f435-129">Ver solicitudes con error y excepciones</span><span class="sxs-lookup"><span data-stu-id="6f435-129">View exceptions and failed requests</span></span>
<span data-ttu-id="6f435-130">Mostrar informes de excepción en la ventana de búsqueda de hello.</span><span class="sxs-lookup"><span data-stu-id="6f435-130">Exception reports show in hello Search window.</span></span> <span data-ttu-id="6f435-131">(En algunos tipos anteriores de la aplicación ASP.NET, tienen también[configurar la supervisión de excepciones](app-insights-asp-net-exceptions.md) toosee excepciones controladas por el marco de trabajo de Hola.)</span><span class="sxs-lookup"><span data-stu-id="6f435-131">(In some older types of ASP.NET application, you have too[set up exception monitoring](app-insights-asp-net-exceptions.md) toosee exceptions that are handled by hello framework.)</span></span>

<span data-ttu-id="6f435-132">Haga clic en un tooget un seguimiento de pila de excepción.</span><span class="sxs-lookup"><span data-stu-id="6f435-132">Click an exception tooget a stack trace.</span></span> <span data-ttu-id="6f435-133">Si el código de hello de aplicación hello está abierto en Visual Studio, puede hacer clic a través de hello pila seguimiento toohello relevantes de línea de código de hello.</span><span class="sxs-lookup"><span data-stu-id="6f435-133">If hello code of hello app is open in Visual Studio, you can click through from hello stack trace toohello relevant line of hello code.</span></span>

![Seguimiento de la pila de excepción](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-hello-code"></a><span data-ttu-id="6f435-135">Ver resúmenes de solicitud y la excepción en el código de hello</span><span class="sxs-lookup"><span data-stu-id="6f435-135">View request and exception summaries in hello code</span></span>
<span data-ttu-id="6f435-136">Hola línea Code Lens por encima de cada método de controlador, verá un recuento de las solicitudes de Hola y excepciones registradas por Application Insights en hello últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="6f435-136">In hello Code Lens line above each handler method, you see a count of hello requests and exceptions logged by Application Insights in hello past 24 h.</span></span>

![Seguimiento de la pila de excepción](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> <span data-ttu-id="6f435-138">Code Lens muestra datos de Application Insights solo si tiene [configurado el portal de Application Insights de aplicación toosend telemetría toohello](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="6f435-138">Code Lens shows Application Insights data only if you have [configured your app toosend telemetry toohello Application Insights portal](app-insights-asp-net.md).</span></span>
>

[<span data-ttu-id="6f435-139">Más información acerca de Application Insights en Code Lens</span><span class="sxs-lookup"><span data-stu-id="6f435-139">More about Application Insights in Code Lens</span></span>](app-insights-visual-studio-codelens.md)

## <a name="trends"></a><span data-ttu-id="6f435-140">Tendencias</span><span class="sxs-lookup"><span data-stu-id="6f435-140">Trends</span></span>
<span data-ttu-id="6f435-141">Tendencias es una herramienta para visualizar cómo se comporta la aplicación con el paso del tiempo.</span><span class="sxs-lookup"><span data-stu-id="6f435-141">Trends is a tool for visualizing how your app behaves over time.</span></span> 

<span data-ttu-id="6f435-142">Elija **explorar las tendencias de telemetría** de botón de barra de herramientas de Application Insights de Hola o una ventana de búsqueda de visión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6f435-142">Choose **Explore Telemetry Trends** from hello Application Insights toolbar button or Application Insights Search window.</span></span> <span data-ttu-id="6f435-143">Elija uno de los cinco tooget consultas comunes iniciado.</span><span class="sxs-lookup"><span data-stu-id="6f435-143">Choose one of five common queries tooget started.</span></span> <span data-ttu-id="6f435-144">Puede analizar diferentes conjuntos de datos en función de los tipos de telemetría, los intervalos de tiempo y otras propiedades.</span><span class="sxs-lookup"><span data-stu-id="6f435-144">You can analyze different datasets based on telemetry types, time ranges, and other properties.</span></span> 

<span data-ttu-id="6f435-145">toofind anomalías en los datos, elija una de las opciones de anomalías de hello en el cuadro desplegable de "Tipo de vista" Hola.</span><span class="sxs-lookup"><span data-stu-id="6f435-145">toofind anomalies in your data, choose one of hello anomaly options under hello "View Type" dropdown.</span></span> <span data-ttu-id="6f435-146">Opciones de filtrado de Hello en parte inferior de Hola de ventana hello que sea fácil toohone en subconjuntos específicos de la telemetría.</span><span class="sxs-lookup"><span data-stu-id="6f435-146">hello filtering options at hello bottom of hello window make it easy toohone in on specific subsets of your telemetry.</span></span>

![Tendencias](./media/app-insights-visual-studio/51.png)

<span data-ttu-id="6f435-148">[Más sobre Tendencias](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="6f435-148">[More about Trends](app-insights-visual-studio-trends.md).</span></span>

## <a name="local-monitoring"></a><span data-ttu-id="6f435-149">Supervisión local</span><span class="sxs-lookup"><span data-stu-id="6f435-149">Local monitoring</span></span>
<span data-ttu-id="6f435-150">(Desde Visual Studio 2015 Update 2) Si no ha configurado el portal de Application Insights de hello SDK toosend telemetría toohello (de modo que no hay ninguna clave de instrumentación en ApplicationInsights.config), a continuación, ventana de diagnóstico de hello muestra telemetría de la sesión de depuración más reciente.</span><span class="sxs-lookup"><span data-stu-id="6f435-150">(From Visual Studio 2015 Update 2) If you haven't configured hello SDK toosend telemetry toohello Application Insights portal (so that there is no instrumentation key in ApplicationInsights.config) then hello diagnostics window displays telemetry from your latest debugging session.</span></span> 

<span data-ttu-id="6f435-151">Esto es conveniente si ya ha publicado una versión anterior de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6f435-151">This is desirable if you have already published a previous version of your app.</span></span> <span data-ttu-id="6f435-152">No desea la telemetría de Hola desde su toobe de las sesiones de depuración mezclarse telemetría hello en hello portal de Application Insights desde la aplicación publicada Hola.</span><span class="sxs-lookup"><span data-stu-id="6f435-152">You don't want hello telemetry from your debugging sessions toobe mixed up with hello telemetry on hello Application Insights portal from hello published app.</span></span>

<span data-ttu-id="6f435-153">También es útil si tiene algunas [telemetría personalizada](app-insights-api-custom-events-metrics.md) que desea toodebug antes de enviar el portal de toohello de telemetría.</span><span class="sxs-lookup"><span data-stu-id="6f435-153">It's also useful if you have some [custom telemetry](app-insights-api-custom-events-metrics.md) that you want toodebug before sending telemetry toohello portal.</span></span>

* <span data-ttu-id="6f435-154">*En primer lugar, completamente configurado portal de Application Insights toosend telemetría toohello. Pero ahora me gustaría telemetría de hello toosee solo en Visual Studio.*</span><span class="sxs-lookup"><span data-stu-id="6f435-154">*At first, I fully configured Application Insights toosend telemetry toohello portal. But now I'd like toosee hello telemetry only in Visual Studio.*</span></span>
  
  * <span data-ttu-id="6f435-155">En la configuración de la ventana de búsqueda de hello, hay un diagnóstico local de opción toosearch incluso si la aplicación envía portal toohello de telemetría.</span><span class="sxs-lookup"><span data-stu-id="6f435-155">In hello Search window's Settings, there's an option toosearch local diagnostics even if your app sends telemetry toohello portal.</span></span>
  * <span data-ttu-id="6f435-156">telemetría toostop enviarse toohello portal, comente la línea hello `<instrumentationkey>...` desde ApplicationInsights.config. Cuando estés nuevo portal de toohello de telemetría toosend listo, quitar los comentarios.</span><span class="sxs-lookup"><span data-stu-id="6f435-156">toostop telemetry being sent toohello portal, comment out hello line `<instrumentationkey>...` from ApplicationInsights.config. When you're ready toosend telemetry toohello portal again, uncomment it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6f435-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6f435-157">Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="6f435-158">**[Incorporación de datos adicionales](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="6f435-158">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="6f435-159">Supervise el uso, la disponibilidad, las dependencias y las excepciones.</span><span class="sxs-lookup"><span data-stu-id="6f435-159">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="6f435-160">Integrar seguimientos de marcos de registro.</span><span class="sxs-lookup"><span data-stu-id="6f435-160">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="6f435-161">Escribir telemetría personalizada.</span><span class="sxs-lookup"><span data-stu-id="6f435-161">Write custom telemetry.</span></span> |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| <span data-ttu-id="6f435-163">**[Trabajar con el portal de Application Insights Hola](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="6f435-163">**[Working with hello Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="6f435-164">Consulte paneles, eficaces herramientas de diagnóstico y análisis, alertas, un mapa activo de dependencias de la aplicación y datos de telemetría exportados.</span><span class="sxs-lookup"><span data-stu-id="6f435-164">View dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and exported telemetry data.</span></span> |![Visual Studio](./media/app-insights-visual-studio/62.png) |

