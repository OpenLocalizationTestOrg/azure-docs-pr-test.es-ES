---
title: Depurar aplicaciones con Azure Application Insights en Visual Studio | Microsoft Docs
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
ms.openlocfilehash: e0ac2bf01992520cdbea22a232dc42d678d77c7f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a><span data-ttu-id="ff76c-103">Depure sus aplicaciones con Azure Application Insights en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ff76c-103">Debug your applications with Azure Application Insights in Visual Studio</span></span>
<span data-ttu-id="ff76c-104">En Visual Studio (2015 y versiones posteriores), se pueden diagnosticar y analizar los problemas de rendimiento de las aplicaciones web, tanto en tiempo de depuración como en producción, mediante los datos de telemetría de [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ff76c-104">In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="ff76c-105">Si ha creado la aplicación web de ASP.NET mediante Visual Studio 2017 o versiones posteriores, ya tiene el SDK de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ff76c-105">If you created your ASP.NET web app using Visual Studio 2017 or later, it already has the Application Insights SDK.</span></span> <span data-ttu-id="ff76c-106">Si todavía no lo ha hecho, [agregue Application Insights a su aplicación](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="ff76c-106">Otherwise, if you haven't done so already, [add Application Insights to your app](app-insights-asp-net.md).</span></span>

<span data-ttu-id="ff76c-107">Para supervisar la aplicación cuando se encuentra activa en producción, normalmente verá la telemetría de Application Insights en [Azure Portal](https://portal.azure.com), donde puede establecer alertas y aplicar eficaces herramientas de supervisión.</span><span class="sxs-lookup"><span data-stu-id="ff76c-107">To monitor your app when it's in live production, you normally view the Application Insights telemetry in the [Azure portal](https://portal.azure.com), where you can set alerts and apply powerful monitoring tools.</span></span> <span data-ttu-id="ff76c-108">Pero para la depuración, también puede buscar y analizar la telemetría en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ff76c-108">But for debugging, you can also search and analyze the telemetry in Visual Studio.</span></span> <span data-ttu-id="ff76c-109">Puede usar Visual Studio para analizar la telemetría desde su sitio de producción y desde los procesos de depuración que se ejecutan en el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="ff76c-109">You can use Visual Studio to analyze telemetry both from your production site and from debugging runs on your development machine.</span></span> <span data-ttu-id="ff76c-110">En este caso, puede analizar los procesos de depuración aunque todavía no haya configurado el SDK para enviar telemetría a Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ff76c-110">In the latter case, you can analyze debugging runs even if you haven't yet configured the SDK to send telemetry to the Azure portal.</span></span> 

## <span data-ttu-id="ff76c-111"><a name="run"></a> Depure el proyecto</span><span class="sxs-lookup"><span data-stu-id="ff76c-111"><a name="run"></a> Debug your project</span></span>
<span data-ttu-id="ff76c-112">Ejecute la aplicación web en modo de depuración local mediante F5.</span><span class="sxs-lookup"><span data-stu-id="ff76c-112">Run your web app in local debug mode by using F5.</span></span> <span data-ttu-id="ff76c-113">Abra distintas páginas para generar telemetría.</span><span class="sxs-lookup"><span data-stu-id="ff76c-113">Open different pages to generate some telemetry.</span></span>

<span data-ttu-id="ff76c-114">En Visual Studio, puede ver un recuento de los eventos que el módulo Application Insights ha registrado en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ff76c-114">In Visual Studio, you see a count of the events that have been logged by the Application Insights module in your project.</span></span>

![En Visual Studio, el botón de Application Insights se muestra durante la depuración.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

<span data-ttu-id="ff76c-116">Haga clic en este botón para buscar la telemetría.</span><span class="sxs-lookup"><span data-stu-id="ff76c-116">Click this button to search your telemetry.</span></span> 

## <a name="application-insights-search"></a><span data-ttu-id="ff76c-117">Búsqueda de Application Insights</span><span class="sxs-lookup"><span data-stu-id="ff76c-117">Application Insights search</span></span>
<span data-ttu-id="ff76c-118">La ventana de búsqueda de Application Insights muestra los eventos que se han registrado.</span><span class="sxs-lookup"><span data-stu-id="ff76c-118">The Application Insights Search window shows events that have been logged.</span></span> <span data-ttu-id="ff76c-119">(Si inició sesión en Azure al configurar Application Insights, puede buscar los mismos eventos en Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="ff76c-119">(If you signed in to Azure when you set up Application Insights, you can search the same events in the Azure portal.)</span></span>

![Haga clic con el botón derecho en el proyecto y seleccione Application Insights, Búsqueda.](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> <span data-ttu-id="ff76c-121">Después de seleccionar o anular la selección de filtros, haga clic en el botón de búsqueda al final del campo de búsqueda de texto.</span><span class="sxs-lookup"><span data-stu-id="ff76c-121">After you select or deselect filters, click the Search button at the end of the text search field.</span></span>
>

<span data-ttu-id="ff76c-122">La búsqueda de texto sin formato funciona en todos los campos de los eventos.</span><span class="sxs-lookup"><span data-stu-id="ff76c-122">The free text search works on any fields in the events.</span></span> <span data-ttu-id="ff76c-123">Por ejemplo, buscar parte de la dirección URL de una página; o el valor de una propiedad, como la ciudad del cliente; o palabras específicas en un registro de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="ff76c-123">For example, search for part of the URL of a page; or the value of a property such as client city; or specific words in a trace log.</span></span>

<span data-ttu-id="ff76c-124">Haga clic en cualquier evento para ver sus propiedades con todo detalle.</span><span class="sxs-lookup"><span data-stu-id="ff76c-124">Click any event to see its detailed properties.</span></span>

<span data-ttu-id="ff76c-125">Para las solicitudes a la aplicación web, puede hacer clic en el código.</span><span class="sxs-lookup"><span data-stu-id="ff76c-125">For requests to your web app, you can click through to the code.</span></span>

![En Detalles de la solicitud, haga clic en el código](./media/app-insights-visual-studio/31.png)

<span data-ttu-id="ff76c-127">También puede abrir los elementos relacionados para ayudar a diagnosticar las solicitudes con errores o excepciones.</span><span class="sxs-lookup"><span data-stu-id="ff76c-127">You can also open related items to help diagnose failed requests or exceptions.</span></span>

![En Detalles de la solicitud, desplácese hasta los elementos relacionados](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a><span data-ttu-id="ff76c-129">Ver solicitudes con error y excepciones</span><span class="sxs-lookup"><span data-stu-id="ff76c-129">View exceptions and failed requests</span></span>
<span data-ttu-id="ff76c-130">Informes de excepciones en la ventana de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="ff76c-130">Exception reports show in the Search window.</span></span> <span data-ttu-id="ff76c-131">(En algunos tipos anteriores de aplicaciones de ASP.NET, tendrá que [configurar la supervisión de excepciones](app-insights-asp-net-exceptions.md) para ver las excepciones que el entorno administra).</span><span class="sxs-lookup"><span data-stu-id="ff76c-131">(In some older types of ASP.NET application, you have to [set up exception monitoring](app-insights-asp-net-exceptions.md) to see exceptions that are handled by the framework.)</span></span>

<span data-ttu-id="ff76c-132">Haga clic en una excepción para obtener un seguimiento de la pila.</span><span class="sxs-lookup"><span data-stu-id="ff76c-132">Click an exception to get a stack trace.</span></span> <span data-ttu-id="ff76c-133">Si el código de la aplicación es abierto en Visual Studio, puede hacer clic para recorrer el seguimiento de la pila hasta dar con la línea correspondiente del código.</span><span class="sxs-lookup"><span data-stu-id="ff76c-133">If the code of the app is open in Visual Studio, you can click through from the stack trace to the relevant line of the code.</span></span>

![Seguimiento de la pila de excepción](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-the-code"></a><span data-ttu-id="ff76c-135">Ver resúmenes de solicitudes y excepciones en el código</span><span class="sxs-lookup"><span data-stu-id="ff76c-135">View request and exception summaries in the code</span></span>
<span data-ttu-id="ff76c-136">En la línea de Code Lens, encima de cada método de controlador, puede ver un recuento de las solicitudes y excepciones registradas por Application Insights en las últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="ff76c-136">In the Code Lens line above each handler method, you see a count of the requests and exceptions logged by Application Insights in the past 24 h.</span></span>

![Seguimiento de la pila de excepción](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> <span data-ttu-id="ff76c-138">Code Lens muestra los datos de Application Insights solo si tiene [configurada la aplicación para enviar telemetría al portal de Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="ff76c-138">Code Lens shows Application Insights data only if you have [configured your app to send telemetry to the Application Insights portal](app-insights-asp-net.md).</span></span>
>

[<span data-ttu-id="ff76c-139">Más información acerca de Application Insights en Code Lens</span><span class="sxs-lookup"><span data-stu-id="ff76c-139">More about Application Insights in Code Lens</span></span>](app-insights-visual-studio-codelens.md)

## <a name="trends"></a><span data-ttu-id="ff76c-140">Tendencias</span><span class="sxs-lookup"><span data-stu-id="ff76c-140">Trends</span></span>
<span data-ttu-id="ff76c-141">Tendencias es una herramienta para visualizar cómo se comporta la aplicación con el paso del tiempo.</span><span class="sxs-lookup"><span data-stu-id="ff76c-141">Trends is a tool for visualizing how your app behaves over time.</span></span> 

<span data-ttu-id="ff76c-142">Elija **Explorar tendencias de telemetría** con el botón de la barra de herramientas de Application Insights o en la ventana Búsqueda de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ff76c-142">Choose **Explore Telemetry Trends** from the Application Insights toolbar button or Application Insights Search window.</span></span> <span data-ttu-id="ff76c-143">Seleccione una de las cinco consultas comunes para empezar.</span><span class="sxs-lookup"><span data-stu-id="ff76c-143">Choose one of five common queries to get started.</span></span> <span data-ttu-id="ff76c-144">Puede analizar diferentes conjuntos de datos en función de los tipos de telemetría, los intervalos de tiempo y otras propiedades.</span><span class="sxs-lookup"><span data-stu-id="ff76c-144">You can analyze different datasets based on telemetry types, time ranges, and other properties.</span></span> 

<span data-ttu-id="ff76c-145">Para detectar anomalías en los datos, elija una de las opciones de anomalía en la lista desplegable "Tipo de vista".</span><span class="sxs-lookup"><span data-stu-id="ff76c-145">To find anomalies in your data, choose one of the anomaly options under the "View Type" dropdown.</span></span> <span data-ttu-id="ff76c-146">Con las opciones de filtrado de la parte inferior de la ventana, resulta más sencillo centrarse en subconjuntos específicos de la telemetría.</span><span class="sxs-lookup"><span data-stu-id="ff76c-146">The filtering options at the bottom of the window make it easy to hone in on specific subsets of your telemetry.</span></span>

![Tendencias](./media/app-insights-visual-studio/51.png)

<span data-ttu-id="ff76c-148">[Más sobre Tendencias](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="ff76c-148">[More about Trends](app-insights-visual-studio-trends.md).</span></span>

## <a name="local-monitoring"></a><span data-ttu-id="ff76c-149">Supervisión local</span><span class="sxs-lookup"><span data-stu-id="ff76c-149">Local monitoring</span></span>
<span data-ttu-id="ff76c-150">(Desde Visual Studio 2015 Update 2) Si no ha configurado el SDK para enviar datos de telemetría al portal de Application Insights (para que no haya ninguna clave de instrumentación en ApplicationInsights.config), la ventana diagnóstico muestra los datos de telemetría de la sesión de depuración más reciente.</span><span class="sxs-lookup"><span data-stu-id="ff76c-150">(From Visual Studio 2015 Update 2) If you haven't configured the SDK to send telemetry to the Application Insights portal (so that there is no instrumentation key in ApplicationInsights.config) then the diagnostics window displays telemetry from your latest debugging session.</span></span> 

<span data-ttu-id="ff76c-151">Esto es conveniente si ya ha publicado una versión anterior de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ff76c-151">This is desirable if you have already published a previous version of your app.</span></span> <span data-ttu-id="ff76c-152">No quiere que los datos de telemetría de las sesiones de depuración se mezclen con los datos de telemetría en el portal de Application Insights de la aplicación publicada.</span><span class="sxs-lookup"><span data-stu-id="ff76c-152">You don't want the telemetry from your debugging sessions to be mixed up with the telemetry on the Application Insights portal from the published app.</span></span>

<span data-ttu-id="ff76c-153">También es útil si tiene [datos de telemetría personalizados](app-insights-api-custom-events-metrics.md) que desea depurar antes de enviarlos al portal.</span><span class="sxs-lookup"><span data-stu-id="ff76c-153">It's also useful if you have some [custom telemetry](app-insights-api-custom-events-metrics.md) that you want to debug before sending telemetry to the portal.</span></span>

* <span data-ttu-id="ff76c-154">*En primer lugar, configuré totalmente Application Insights para enviar los datos de telemetría al portal. Pero ahora me gustaría ver los datos de telemetría solo en Visual Studio.*</span><span class="sxs-lookup"><span data-stu-id="ff76c-154">*At first, I fully configured Application Insights to send telemetry to the portal. But now I'd like to see the telemetry only in Visual Studio.*</span></span>
  
  * <span data-ttu-id="ff76c-155">En la configuración de la ventana de búsqueda, hay una opción para buscar diagnósticos locales, incluso si la aplicación envía datos de telemetría al portal.</span><span class="sxs-lookup"><span data-stu-id="ff76c-155">In the Search window's Settings, there's an option to search local diagnostics even if your app sends telemetry to the portal.</span></span>
  * <span data-ttu-id="ff76c-156">Para detener el envío de datos de telemetría al portal, convierta en comentario la línea `<instrumentationkey>...` de ApplicationInsights.config. Cuando esté listo para enviar de nuevo datos de telemetría al portal, quite los comentarios.</span><span class="sxs-lookup"><span data-stu-id="ff76c-156">To stop telemetry being sent to the portal, comment out the line `<instrumentationkey>...` from ApplicationInsights.config. When you're ready to send telemetry to the portal again, uncomment it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ff76c-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ff76c-157">Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="ff76c-158">**[Incorporación de datos adicionales](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="ff76c-158">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="ff76c-159">Supervise el uso, la disponibilidad, las dependencias y las excepciones.</span><span class="sxs-lookup"><span data-stu-id="ff76c-159">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="ff76c-160">Integrar seguimientos de marcos de registro.</span><span class="sxs-lookup"><span data-stu-id="ff76c-160">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="ff76c-161">Escribir telemetría personalizada.</span><span class="sxs-lookup"><span data-stu-id="ff76c-161">Write custom telemetry.</span></span> |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| <span data-ttu-id="ff76c-163">**[Trabajo con el portal de Application Insights](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="ff76c-163">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="ff76c-164">Consulte paneles, eficaces herramientas de diagnóstico y análisis, alertas, un mapa activo de dependencias de la aplicación y datos de telemetría exportados.</span><span class="sxs-lookup"><span data-stu-id="ff76c-164">View dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and exported telemetry data.</span></span> |![Visual Studio](./media/app-insights-visual-studio/62.png) |

