---
title: "Detección inteligente en Azure Application Insights | Microsoft Docs"
description: "Application Insights realiza un análisis profundo automático de la telemetría de la aplicación y le advierte de los posibles problemas."
services: application-insights
documentationcenter: windows
author: rakefetj
manager: carmonm
ms.assetid: 2eeb4a35-c7a1-49f7-9b68-4f4b860938b2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: f203b2a532ea721d9797c67a4750896e3ab2b9f7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="smart-detection-in-application-insights"></a><span data-ttu-id="b2af6-103">Detección inteligente en Application Insights</span><span class="sxs-lookup"><span data-stu-id="b2af6-103">Smart Detection in Application Insights</span></span>
 <span data-ttu-id="b2af6-104">La detección inteligente avisa automáticamente de posibles problemas de rendimiento en su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="b2af6-104">Smart Detection automatically warns you of potential performance problems in your web application.</span></span> <span data-ttu-id="b2af6-105">Realiza un análisis proactivo de la telemetría que su aplicación envía a [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b2af6-105">It performs proactive analysis of the telemetry that your app sends to [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="b2af6-106">Si hay un aumento repentino de las tasas de error o patrones de rendimiento anormales en el cliente o el servidor, recibirá una alerta.</span><span class="sxs-lookup"><span data-stu-id="b2af6-106">If there is a sudden rise in failure rates, or abnormal patterns in client or server performance, you get an alert.</span></span> <span data-ttu-id="b2af6-107">Esta característica no necesita ninguna configuración.</span><span class="sxs-lookup"><span data-stu-id="b2af6-107">This feature needs no configuration.</span></span> <span data-ttu-id="b2af6-108">Funciona si la aplicación envía suficiente telemetría.</span><span class="sxs-lookup"><span data-stu-id="b2af6-108">It operates if your application sends enough telemetry.</span></span>

<span data-ttu-id="b2af6-109">Puede acceder a las alertas de detección inteligente desde los correos electrónicos que recibe y desde la hoja de detección inteligente.</span><span class="sxs-lookup"><span data-stu-id="b2af6-109">You can access Smart Detection alerts both from the emails you receive, and from the Smart Detection blade.</span></span>

## <a name="review-your-smart-detections"></a><span data-ttu-id="b2af6-110">Revisión de las detecciones inteligentes</span><span class="sxs-lookup"><span data-stu-id="b2af6-110">Review your Smart Detections</span></span>
<span data-ttu-id="b2af6-111">Puede detectar las detecciones de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="b2af6-111">You can discover detections in two ways:</span></span>

* <span data-ttu-id="b2af6-112">**Recibirá un correo electrónico** de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b2af6-112">**You receive an email** from Application Insights.</span></span> <span data-ttu-id="b2af6-113">Este es un ejemplo típico:</span><span class="sxs-lookup"><span data-stu-id="b2af6-113">Here's a typical example:</span></span>
  
    ![Alerta de correo electrónico](./media/app-insights-proactive-diagnostics/03.png)
  
    <span data-ttu-id="b2af6-115">Haga clic en el botón grande para abrir más detalles en el portal.</span><span class="sxs-lookup"><span data-stu-id="b2af6-115">Click the big button to open more detail in the portal.</span></span>
* <span data-ttu-id="b2af6-116">**El icono de detección inteligente** en la hoja de información general de la aplicación muestra un recuento de las alertas recientes.</span><span class="sxs-lookup"><span data-stu-id="b2af6-116">**The Smart Detection tile** on your app's overview blade shows a count of recent alerts.</span></span> <span data-ttu-id="b2af6-117">Haga clic en el icono para ver una lista de las alertas recientes.</span><span class="sxs-lookup"><span data-stu-id="b2af6-117">Click the tile to see a list of recent alerts.</span></span>

![Visualización de detecciones recientes](./media/app-insights-proactive-diagnostics/04.png)

<span data-ttu-id="b2af6-119">Seleccione una alerta para ver sus detalles.</span><span class="sxs-lookup"><span data-stu-id="b2af6-119">Select an alert to see its details.</span></span>

## <a name="what-problems-are-detected"></a><span data-ttu-id="b2af6-120">¿Qué problemas se detectan?</span><span class="sxs-lookup"><span data-stu-id="b2af6-120">What problems are detected?</span></span>
<span data-ttu-id="b2af6-121">Hay tres tipos de detección:</span><span class="sxs-lookup"><span data-stu-id="b2af6-121">There are three kinds of detection:</span></span>

* <span data-ttu-id="b2af6-122">[Detección inteligente: anomalías de errores](app-insights-proactive-failure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="b2af6-122">[Smart detection - Failure Anomalies](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="b2af6-123">Usamos el aprendizaje automático para establecer la tasa esperada de solicitudes con error para su aplicación, correlacionando la carga y otros factores.</span><span class="sxs-lookup"><span data-stu-id="b2af6-123">We use machine learning to set the expected rate of failed requests for your app, correlating with load and other factors.</span></span> <span data-ttu-id="b2af6-124">Si la tasa de error queda fuera del rango esperado, se enviará una alerta.</span><span class="sxs-lookup"><span data-stu-id="b2af6-124">If the failure rate goes outside the expected envelope, we send an alert.</span></span>
* <span data-ttu-id="b2af6-125">[Detección inteligente: anomalías de rendimiento](app-insights-proactive-performance-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="b2af6-125">[Smart detection - Performance Anomalies](app-insights-proactive-performance-diagnostics.md).</span></span> <span data-ttu-id="b2af6-126">Recibe notificaciones si la duración del tiempo de respuesta de operación o dependencia se ralentiza en comparación con la línea de base histórica, o si se identifica un patrón anómalo en el tiempo de respuesta o en el tiempo de carga de página.</span><span class="sxs-lookup"><span data-stu-id="b2af6-126">You get notifications if response time of an operation or dependency duration is slowing down compared to historical baseline or if we identify an anomalous pattern in response time or page load time.</span></span>   
* <span data-ttu-id="b2af6-127">[Detección inteligente: problemas del servicio en la nube de Azure](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span><span class="sxs-lookup"><span data-stu-id="b2af6-127">[Smart detection - Azure Cloud Service issues](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span></span> <span data-ttu-id="b2af6-128">Recibe alertas si la aplicación se hospeda en Servicios en la nube de Azure y una instancia de rol tiene errores de inicio, repetición de ciclos frecuentes o bloqueos en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="b2af6-128">You get alerts if your app is hosted in Azure Cloud Services and a role instance has startup failures, frequent recycling, or runtime crashes.</span></span>

<span data-ttu-id="b2af6-129">(Los vínculos a la Ayuda de cada notificación llevan a los artículos pertinentes).</span><span class="sxs-lookup"><span data-stu-id="b2af6-129">(The help links in each notification take you to the relevant articles.)</span></span>

## <a name="video"></a><span data-ttu-id="b2af6-130">Vídeo</span><span class="sxs-lookup"><span data-stu-id="b2af6-130">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="b2af6-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b2af6-131">Next steps</span></span>
<span data-ttu-id="b2af6-132">Estas herramientas de diagnóstico lo ayudarán a inspeccionar los datos de telemetría de su aplicación:</span><span class="sxs-lookup"><span data-stu-id="b2af6-132">These diagnostic tools help you inspect the telemetry from your app:</span></span>

* [<span data-ttu-id="b2af6-133">Explorador de métricas</span><span class="sxs-lookup"><span data-stu-id="b2af6-133">Metric explorer</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="b2af6-134">Explorador de búsqueda</span><span class="sxs-lookup"><span data-stu-id="b2af6-134">Search explorer</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="b2af6-135">Analytics: Lenguaje de consulta eficaz</span><span class="sxs-lookup"><span data-stu-id="b2af6-135">Analytics - powerful query language</span></span>](app-insights-analytics-tour.md)

<span data-ttu-id="b2af6-136">La detección inteligente es completamente automática.</span><span class="sxs-lookup"><span data-stu-id="b2af6-136">Smart Detection is completely automatic.</span></span> <span data-ttu-id="b2af6-137">Pero ¿quizás le gustaría configurar algunas alertas más?</span><span class="sxs-lookup"><span data-stu-id="b2af6-137">But maybe you'd like to set up some more alerts?</span></span>

* [<span data-ttu-id="b2af6-138">Alertas de métricas configuradas manualmente</span><span class="sxs-lookup"><span data-stu-id="b2af6-138">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="b2af6-139">Pruebas web de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="b2af6-139">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md) 

