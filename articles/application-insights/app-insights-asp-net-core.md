---
title: aaaAzure Application Insights para ASP.NET Core | Documentos de Microsoft
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
ms.openlocfilehash: a7a27f9eef1daec5b0deae9fd88906e646980659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-aspnet-core"></a><span data-ttu-id="f051e-103">Application Insights para ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="f051e-103">Application Insights for ASP.NET Core</span></span>
<span data-ttu-id="f051e-104">[Application Insights](app-insights-overview.md) permite supervisar la disponibilidad, el rendimiento y el uso de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="f051e-104">[Application Insights](app-insights-overview.md) lets you monitor your web application for availability, performance and usage.</span></span> <span data-ttu-id="f051e-105">Con los comentarios de Hola que obtendrá acerca del rendimiento de Hola y eficacia de la aplicación Hola comodín, pueda tomar decisiones meditadas sobre la dirección de Hola de diseño de hello en cada ciclo de vida de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="f051e-105">With hello feedback you get about hello performance and effectiveness of your app in hello wild, you can make informed choices about hello direction of hello design in each development lifecycle.</span></span>

![Ejemplo](./media/app-insights-asp-net-core/sample.png)

<span data-ttu-id="f051e-107">Necesitará una suscripción a [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="f051e-107">You'll need a subscription with [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="f051e-108">Inicie sesión con una cuenta Microsoft, que podría tener para Windows, XBox Live u otros servicios en la nube de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f051e-108">Sign in with a Microsoft account, which you might have for Windows, XBox Live, or other Microsoft cloud services.</span></span> <span data-ttu-id="f051e-109">El equipo puede tener una suscripción organizativa tooAzure: pida Hola propietario tooadd tooit con su cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f051e-109">Your team might have an organizational subscription tooAzure: ask hello owner tooadd you tooit using your Microsoft account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f051e-110">Introducción</span><span class="sxs-lookup"><span data-stu-id="f051e-110">Getting started</span></span>

* <span data-ttu-id="f051e-111">En el Explorador de soluciones de Visual Studio, haga clic con el botón derecho en el proyecto y elija **Configurar Application Insights** o **Agregar > Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="f051e-111">In Visual Studio Solution Explorer, right-click your project and select **Configure Application Insights**, or **Add > Application Insights**.</span></span> <span data-ttu-id="f051e-112">[Más información](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="f051e-112">[Learn more](app-insights-asp-net.md).</span></span>
* <span data-ttu-id="f051e-113">Si no ve los comandos de menú, siga hello [manual Guía de introducción al obtener](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span><span class="sxs-lookup"><span data-stu-id="f051e-113">If you don't see those menu commands, follow hello [manual getting Started guide](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span></span> <span data-ttu-id="f051e-114">Puede que necesite toodo si el proyecto se creó con una versión de Visual Studio antes de 2017.</span><span class="sxs-lookup"><span data-stu-id="f051e-114">You may need toodo this if your project was created with a version of Visual Studio before 2017.</span></span>

## <a name="using-application-insights"></a><span data-ttu-id="f051e-115">Uso de Application Insights</span><span class="sxs-lookup"><span data-stu-id="f051e-115">Using Application Insights</span></span>
<span data-ttu-id="f051e-116">Inicio de sesión en hello [portal de Microsoft Azure](https://portal.azure.com), seleccione **todos los recursos** o **Application Insights**y, a continuación, seleccione recursos Hola creó toomonitor la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f051e-116">Sign into hello [Microsoft Azure portal](https://portal.azure.com), select **All Resources** or **Application Insights**, and then select hello resource you created toomonitor your app.</span></span>

<span data-ttu-id="f051e-117">En una ventana del explorador independiente, use la aplicación durante un tiempo.</span><span class="sxs-lookup"><span data-stu-id="f051e-117">In a separate browser window, use your app for a while.</span></span> <span data-ttu-id="f051e-118">Podrá ver datos que aparecen en los gráficos de Application Insights Hola.</span><span class="sxs-lookup"><span data-stu-id="f051e-118">You'll see data appearing in hello Application Insights charts.</span></span> <span data-ttu-id="f051e-119">(Podría tener tooclick actualización). Solo habrá una pequeña cantidad de datos mientras está desarrollando, pero estos gráficos realmente cobrarán vida cuando publique su aplicación y disponga de varios usuarios.</span><span class="sxs-lookup"><span data-stu-id="f051e-119">(You might have tooclick Refresh.) There will be only a small amount of data while you're developing, but these charts really come alive when you publish your app and have many users.</span></span> 

<span data-ttu-id="f051e-120">página de información general de Hello muestra gráficos de rendimiento clave: tiempo de respuesta de servidor, el tiempo de carga de página y el número de solicitudes con error.</span><span class="sxs-lookup"><span data-stu-id="f051e-120">hello overview page shows key performance charts: server response time,  page load time, and counts of failed requests.</span></span> <span data-ttu-id="f051e-121">Haga clic en cualquier toosee gráfico más gráficos y los datos.</span><span class="sxs-lookup"><span data-stu-id="f051e-121">Click any chart toosee more charts and data.</span></span>

<span data-ttu-id="f051e-122">Vistas en el portal de Hola se dividen en tres categorías principales:</span><span class="sxs-lookup"><span data-stu-id="f051e-122">Views in hello portal fall into three main categories:</span></span>

* <span data-ttu-id="f051e-123">[El Explorador de métricas](app-insights-metrics-explorer.md) muestra gráficos y tablas de métricas y recuentos, como tiempos de respuesta, tasas de errores o las métricas crear usted mismo con hello [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="f051e-123">[Metrics Explorer](app-insights-metrics-explorer.md) shows graphs and tables of metrics and counts, such as response times, failure rates, or metrics you create yourself with hello [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="f051e-124">Filtro y el segmento de datos de Hola por tooget de valores de propiedad una mejor comprensión de la aplicación y sus usuarios.</span><span class="sxs-lookup"><span data-stu-id="f051e-124">Filter and segment hello data by property values tooget a better understanding of your app and its users.</span></span>
* <span data-ttu-id="f051e-125">[Buscar explorador](app-insights-diagnostic-search.md) muestra los eventos individuales, como solicitudes específicas, excepciones, seguimientos del registro o eventos que se haya creado con hello [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="f051e-125">[Search Explorer](app-insights-diagnostic-search.md) lists individual events, such as specific requests, exceptions, log traces, or events you created yourself with hello [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="f051e-126">Filtrar y buscar en eventos de Hola y desplazarse entre los problemas de tooinvestigate de eventos relacionados.</span><span class="sxs-lookup"><span data-stu-id="f051e-126">Filter and search in hello events, and navigate among related events tooinvestigate issues.</span></span>
* <span data-ttu-id="f051e-127">[Analytics](app-insights-analytics.md) permite ejecutar consultas de tipo SQL a través de los datos de telemetría; además, constituye una eficaz herramienta de análisis y diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="f051e-127">[Analytics](app-insights-analytics.md) lets you run SQL-like queries over your telemetry, and is a powerful analytical and diagnostic tool.</span></span>

## <a name="alerts"></a><span data-ttu-id="f051e-128">Alertas</span><span class="sxs-lookup"><span data-stu-id="f051e-128">Alerts</span></span>
* <span data-ttu-id="f051e-129">Obtendrá automáticamente [alertas de diagnóstico proactivo](app-insights-proactive-diagnostics.md) que le comunican cambios anómalos en las tasas de error y otras métricas.</span><span class="sxs-lookup"><span data-stu-id="f051e-129">You automatically get [proactive diagnostic alerts](app-insights-proactive-diagnostics.md) that tell you about anomalous changes in failure rates and other metrics.</span></span>
* <span data-ttu-id="f051e-130">Configurar [disponibilidad pruebas](app-insights-monitor-web-app-availability.md) tootest su sitio Web continuamente desde ubicaciones en todo el mundo y obtendrá los correos electrónicos en cuanto alguna prueba falla.</span><span class="sxs-lookup"><span data-stu-id="f051e-130">Set up [availability tests](app-insights-monitor-web-app-availability.md) tootest your website continually from locations worldwide, and get emails as soon as any test fails.</span></span>
* <span data-ttu-id="f051e-131">Configurar [alertas métricas](app-insights-monitor-web-app-availability.md) tooknow si dejan de métricas, como tiempos de respuesta o los tipos de excepción fuera de los límites aceptable.</span><span class="sxs-lookup"><span data-stu-id="f051e-131">Set up [metric alerts](app-insights-monitor-web-app-availability.md) tooknow if metrics such as response times or exception rates go outside acceptable limits.</span></span>

## <a name="video"></a><span data-ttu-id="f051e-132">Vídeo</span><span class="sxs-lookup"><span data-stu-id="f051e-132">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a><span data-ttu-id="f051e-133">Código abierto</span><span class="sxs-lookup"><span data-stu-id="f051e-133">Open source</span></span>
[<span data-ttu-id="f051e-134">Leer y contribuir en el código de toohello</span><span class="sxs-lookup"><span data-stu-id="f051e-134">Read and contribute toohello code</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a><span data-ttu-id="f051e-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f051e-135">Next steps</span></span>
* <span data-ttu-id="f051e-136">[Agregar páginas web de telemetría tooyour](app-insights-javascript.md) toomonitor página rendimiento y uso.</span><span class="sxs-lookup"><span data-stu-id="f051e-136">[Add telemetry tooyour web pages](app-insights-javascript.md) toomonitor page usage and performance.</span></span>
* <span data-ttu-id="f051e-137">[Supervisar las dependencias](app-insights-asp-net-dependencies.md) toosee si se REST, SQL u otros recursos externos se ralenticen.</span><span class="sxs-lookup"><span data-stu-id="f051e-137">[Monitor dependencies](app-insights-asp-net-dependencies.md) toosee if REST, SQL or other external resources are slowing you down.</span></span>
* <span data-ttu-id="f051e-138">[Usar la API de hello](app-insights-api-custom-events-metrics.md) toosend sus propios eventos y métricas para una vista más detallada de rendimiento y el uso de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f051e-138">[Use hello API](app-insights-api-custom-events-metrics.md) toosend your own events and metrics for a more detailed view of your app's performance and usage.</span></span>
* <span data-ttu-id="f051e-139">[Pruebas de disponibilidad](app-insights-monitor-web-app-availability.md) Compruebe la aplicación procedente de alrededor de Hola a todos.</span><span class="sxs-lookup"><span data-stu-id="f051e-139">[Availability tests](app-insights-monitor-web-app-availability.md) check your app constantly from around hello world.</span></span> 

