---
title: Azure Application Insights para ASP.NET Core | Microsoft Docs
description: Supervise la disponibilidad, el rendimiento y el uso de las aplicaciones web.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 3b722e47-38bd-4667-9ba4-65b7006c074c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: d86495eea467977f6c079de72e2b49a2a1da2b60
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-aspnet-core"></a><span data-ttu-id="aff38-103">Application Insights para ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="aff38-103">Application Insights for ASP.NET Core</span></span>
<span data-ttu-id="aff38-104">[Application Insights](app-insights-overview.md) permite supervisar la disponibilidad, el rendimiento y el uso de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="aff38-104">[Application Insights](app-insights-overview.md) lets you monitor your web application for availability, performance and usage.</span></span> <span data-ttu-id="aff38-105">Con los comentarios que obtendrá sobre el rendimiento y la eficacia de la aplicación en su entorno natural, pueda tomar decisiones meditadas sobre la dirección del diseño en cada ciclo de vida de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="aff38-105">With the feedback you get about the performance and effectiveness of your app in the wild, you can make informed choices about the direction of the design in each development lifecycle.</span></span>

![Ejemplo](./media/app-insights-asp-net-core/sample.png)

<span data-ttu-id="aff38-107">Necesitará una suscripción a [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="aff38-107">You'll need a subscription with [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="aff38-108">Inicie sesión con una cuenta Microsoft, que podría tener para Windows, XBox Live u otros servicios en la nube de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="aff38-108">Sign in with a Microsoft account, which you might have for Windows, XBox Live, or other Microsoft cloud services.</span></span> <span data-ttu-id="aff38-109">Si su equipo tiene una suscripción organizativa a Azure, el propietario puede agregarle a esta con la cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="aff38-109">Your team might have an organizational subscription to Azure: ask the owner to add you to it using your Microsoft account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="aff38-110">Introducción</span><span class="sxs-lookup"><span data-stu-id="aff38-110">Getting started</span></span>

* <span data-ttu-id="aff38-111">En el Explorador de soluciones de Visual Studio, haga clic con el botón derecho en el proyecto y elija **Configurar Application Insights** o **Agregar > Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="aff38-111">In Visual Studio Solution Explorer, right-click your project and select **Configure Application Insights**, or **Add > Application Insights**.</span></span> <span data-ttu-id="aff38-112">[Más información](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="aff38-112">[Learn more](app-insights-asp-net.md).</span></span>
* <span data-ttu-id="aff38-113">Si no ve los comandos de menú, siga la [guía de introducción manual](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span><span class="sxs-lookup"><span data-stu-id="aff38-113">If you don't see those menu commands, follow the [manual getting Started guide](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span></span> <span data-ttu-id="aff38-114">Puede necesitar hacerlo si el proyecto se creó con una versión de Visual Studio anterior a 2017.</span><span class="sxs-lookup"><span data-stu-id="aff38-114">You may need to do this if your project was created with a version of Visual Studio before 2017.</span></span>

## <a name="using-application-insights"></a><span data-ttu-id="aff38-115">Uso de Application Insights</span><span class="sxs-lookup"><span data-stu-id="aff38-115">Using Application Insights</span></span>
<span data-ttu-id="aff38-116">Inicie sesión en [Microsoft Azure portal](https://portal.azure.com), seleccione **Todos los recursos** o **Application Insights**; luego, seleccione el recurso que ha creado para supervisar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aff38-116">Sign into the [Microsoft Azure portal](https://portal.azure.com), select **All Resources** or **Application Insights**, and then select the resource you created to monitor your app.</span></span>

<span data-ttu-id="aff38-117">En una ventana del explorador independiente, use la aplicación durante un tiempo.</span><span class="sxs-lookup"><span data-stu-id="aff38-117">In a separate browser window, use your app for a while.</span></span> <span data-ttu-id="aff38-118">Verá los datos que aparecen en los gráficos de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="aff38-118">You'll see data appearing in the Application Insights charts.</span></span> <span data-ttu-id="aff38-119">(Es posible que tenga que hacer clic en Actualizar). Solo habrá una pequeña cantidad de datos mientras está desarrollando, pero estos gráficos realmente cobrarán vida cuando publique su aplicación y disponga de varios usuarios.</span><span class="sxs-lookup"><span data-stu-id="aff38-119">(You might have to click Refresh.) There will be only a small amount of data while you're developing, but these charts really come alive when you publish your app and have many users.</span></span> 

<span data-ttu-id="aff38-120">La página de información general muestra los gráficos de rendimiento clave: tiempo de respuesta del servidor, tiempo de carga de la página y recuentos de solicitudes con error.</span><span class="sxs-lookup"><span data-stu-id="aff38-120">The overview page shows key performance charts: server response time,  page load time, and counts of failed requests.</span></span> <span data-ttu-id="aff38-121">Haga clic en cualquier gráfico para ver más gráficos y datos.</span><span class="sxs-lookup"><span data-stu-id="aff38-121">Click any chart to see more charts and data.</span></span>

<span data-ttu-id="aff38-122">Las vistas del portal se dividen en tres categorías principales:</span><span class="sxs-lookup"><span data-stu-id="aff38-122">Views in the portal fall into three main categories:</span></span>

* <span data-ttu-id="aff38-123">El [Explorador de métricas](app-insights-metrics-explorer.md) muestra gráficos y tablas de métricas y recuentos, como tiempos de respuesta, tasas de errores o las métricas que crea el usuario con la [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="aff38-123">[Metrics Explorer](app-insights-metrics-explorer.md) shows graphs and tables of metrics and counts, such as response times, failure rates, or metrics you create yourself with the [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="aff38-124">Filtre y segmente los datos por valores de propiedad para obtener una mejor comprensión de la aplicación y sus usuarios.</span><span class="sxs-lookup"><span data-stu-id="aff38-124">Filter and segment the data by property values to get a better understanding of your app and its users.</span></span>
* <span data-ttu-id="aff38-125">El [Explorador de búsqueda](app-insights-diagnostic-search.md) enumera los eventos individuales, como solicitudes específicas, excepciones, seguimientos de registros o eventos creados por el usuario con la [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="aff38-125">[Search Explorer](app-insights-diagnostic-search.md) lists individual events, such as specific requests, exceptions, log traces, or events you created yourself with the [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="aff38-126">Filtre y busque en los eventos y desplácese entre los eventos relacionados para investigar los problemas.</span><span class="sxs-lookup"><span data-stu-id="aff38-126">Filter and search in the events, and navigate among related events to investigate issues.</span></span>
* <span data-ttu-id="aff38-127">[Analytics](app-insights-analytics.md) permite ejecutar consultas de tipo SQL a través de los datos de telemetría; además, constituye una eficaz herramienta de análisis y diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="aff38-127">[Analytics](app-insights-analytics.md) lets you run SQL-like queries over your telemetry, and is a powerful analytical and diagnostic tool.</span></span>

## <a name="alerts"></a><span data-ttu-id="aff38-128">Alertas</span><span class="sxs-lookup"><span data-stu-id="aff38-128">Alerts</span></span>
* <span data-ttu-id="aff38-129">Obtendrá automáticamente [alertas de diagnóstico proactivo](app-insights-proactive-diagnostics.md) que le comunican cambios anómalos en las tasas de error y otras métricas.</span><span class="sxs-lookup"><span data-stu-id="aff38-129">You automatically get [proactive diagnostic alerts](app-insights-proactive-diagnostics.md) that tell you about anomalous changes in failure rates and other metrics.</span></span>
* <span data-ttu-id="aff38-130">Configure [pruebas de disponibilidad](app-insights-monitor-web-app-availability.md) para probar su sitio web continuamente desde ubicaciones de todo el mundo y obtener correos electrónicos en cuanto alguna prueba falle.</span><span class="sxs-lookup"><span data-stu-id="aff38-130">Set up [availability tests](app-insights-monitor-web-app-availability.md) to test your website continually from locations worldwide, and get emails as soon as any test fails.</span></span>
* <span data-ttu-id="aff38-131">Configure [alertas de métricas](app-insights-monitor-web-app-availability.md) para saber si métricas como los tiempos de respuesta o las tasas de excepciones sobrepasan los límites aceptables.</span><span class="sxs-lookup"><span data-stu-id="aff38-131">Set up [metric alerts](app-insights-monitor-web-app-availability.md) to know if metrics such as response times or exception rates go outside acceptable limits.</span></span>

## <a name="video"></a><span data-ttu-id="aff38-132">Vídeo</span><span class="sxs-lookup"><span data-stu-id="aff38-132">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a><span data-ttu-id="aff38-133">Código abierto</span><span class="sxs-lookup"><span data-stu-id="aff38-133">Open source</span></span>
[<span data-ttu-id="aff38-134">Lectura y contribución al código</span><span class="sxs-lookup"><span data-stu-id="aff38-134">Read and contribute to the code</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a><span data-ttu-id="aff38-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aff38-135">Next steps</span></span>
* <span data-ttu-id="aff38-136">[Agregue datos de telemetría a las páginas web](app-insights-javascript.md) para supervisar el uso y el rendimiento de las páginas.</span><span class="sxs-lookup"><span data-stu-id="aff38-136">[Add telemetry to your web pages](app-insights-javascript.md) to monitor page usage and performance.</span></span>
* <span data-ttu-id="aff38-137">[Supervise dependencias](app-insights-asp-net-dependencies.md) para ver si REST, SQL u otros recursos externos se están ralentizando.</span><span class="sxs-lookup"><span data-stu-id="aff38-137">[Monitor dependencies](app-insights-asp-net-dependencies.md) to see if REST, SQL or other external resources are slowing you down.</span></span>
* <span data-ttu-id="aff38-138">[Use la API](app-insights-api-custom-events-metrics.md) para enviar sus propios eventos y métricas para obtener una vista más detallada del rendimiento y el uso de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aff38-138">[Use the API](app-insights-api-custom-events-metrics.md) to send your own events and metrics for a more detailed view of your app's performance and usage.</span></span>
* <span data-ttu-id="aff38-139">[Las pruebas de disponibilidad](app-insights-monitor-web-app-availability.md) comprueban su aplicación constantemente desde cualquier parte del mundo.</span><span class="sxs-lookup"><span data-stu-id="aff38-139">[Availability tests](app-insights-monitor-web-app-availability.md) check your app constantly from around the world.</span></span> 

