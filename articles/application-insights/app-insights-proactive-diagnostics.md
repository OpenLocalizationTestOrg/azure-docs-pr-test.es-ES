---
title: "la detección en Azure Application Insights aaaSmart | Documentos de Microsoft"
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
ms.openlocfilehash: f794476088fc69154eda2077b7a5cdc769fab3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection-in-application-insights"></a><span data-ttu-id="ea6a0-103">Detección inteligente en Application Insights</span><span class="sxs-lookup"><span data-stu-id="ea6a0-103">Smart Detection in Application Insights</span></span>
 <span data-ttu-id="ea6a0-104">La detección inteligente avisa automáticamente de posibles problemas de rendimiento en su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ea6a0-104">Smart Detection automatically warns you of potential performance problems in your web application.</span></span> <span data-ttu-id="ea6a0-105">Realiza un análisis proactivo de telemetría de Hola que la aplicación envía demasiado[Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ea6a0-105">It performs proactive analysis of hello telemetry that your app sends too[Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="ea6a0-106">Si hay un aumento repentino de las tasas de error o patrones de rendimiento anormales en el cliente o el servidor, recibirá una alerta.</span><span class="sxs-lookup"><span data-stu-id="ea6a0-106">If there is a sudden rise in failure rates, or abnormal patterns in client or server performance, you get an alert.</span></span> <span data-ttu-id="ea6a0-107">Esta característica no necesita ninguna configuración.</span><span class="sxs-lookup"><span data-stu-id="ea6a0-107">This feature needs no configuration.</span></span> <span data-ttu-id="ea6a0-108">Funciona si la aplicación envía suficiente telemetría.</span><span class="sxs-lookup"><span data-stu-id="ea6a0-108">It operates if your application sends enough telemetry.</span></span>

<span data-ttu-id="ea6a0-109">Puede tener acceso a las alertas de detección inteligente de los mensajes de saludo recibidos y de hoja de detección inteligente de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea6a0-109">You can access Smart Detection alerts both from hello emails you receive, and from hello Smart Detection blade.</span></span>

## <a name="review-your-smart-detections"></a><span data-ttu-id="ea6a0-110">Revisión de las detecciones inteligentes</span><span class="sxs-lookup"><span data-stu-id="ea6a0-110">Review your Smart Detections</span></span>
<span data-ttu-id="ea6a0-111">Puede detectar las detecciones de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="ea6a0-111">You can discover detections in two ways:</span></span>

* <span data-ttu-id="ea6a0-112">**Recibirá un correo electrónico** de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ea6a0-112">**You receive an email** from Application Insights.</span></span> <span data-ttu-id="ea6a0-113">Este es un ejemplo típico:</span><span class="sxs-lookup"><span data-stu-id="ea6a0-113">Here's a typical example:</span></span>
  
    ![Alerta de correo electrónico](./media/app-insights-proactive-diagnostics/03.png)
  
    <span data-ttu-id="ea6a0-115">Haga clic en hello botón grande tooopen más detalle en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea6a0-115">Click hello big button tooopen more detail in hello portal.</span></span>
* <span data-ttu-id="ea6a0-116">**icono de detección inteligente de Hello** en información general de la aplicación hoja muestra un recuento de las alertas recientes.</span><span class="sxs-lookup"><span data-stu-id="ea6a0-116">**hello Smart Detection tile** on your app's overview blade shows a count of recent alerts.</span></span> <span data-ttu-id="ea6a0-117">Haga clic en el icono de hello toosee una lista de las alertas recientes.</span><span class="sxs-lookup"><span data-stu-id="ea6a0-117">Click hello tile toosee a list of recent alerts.</span></span>

![Visualización de detecciones recientes](./media/app-insights-proactive-diagnostics/04.png)

<span data-ttu-id="ea6a0-119">Seleccione una alerta toosee sus detalles.</span><span class="sxs-lookup"><span data-stu-id="ea6a0-119">Select an alert toosee its details.</span></span>

## <a name="what-problems-are-detected"></a><span data-ttu-id="ea6a0-120">¿Qué problemas se detectan?</span><span class="sxs-lookup"><span data-stu-id="ea6a0-120">What problems are detected?</span></span>
<span data-ttu-id="ea6a0-121">Hay tres tipos de detección:</span><span class="sxs-lookup"><span data-stu-id="ea6a0-121">There are three kinds of detection:</span></span>

* <span data-ttu-id="ea6a0-122">[Detección inteligente: anomalías de errores](app-insights-proactive-failure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="ea6a0-122">[Smart detection - Failure Anomalies](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="ea6a0-123">Se utiliza aprendizaje automático de velocidad de tooset Hola esperada de solicitudes con error para la aplicación, correlacionar con carga y otros factores.</span><span class="sxs-lookup"><span data-stu-id="ea6a0-123">We use machine learning tooset hello expected rate of failed requests for your app, correlating with load and other factors.</span></span> <span data-ttu-id="ea6a0-124">Si deja de tasa de error de hello fuera Hola esperado sobres, se enviará una alerta.</span><span class="sxs-lookup"><span data-stu-id="ea6a0-124">If hello failure rate goes outside hello expected envelope, we send an alert.</span></span>
* <span data-ttu-id="ea6a0-125">[Detección inteligente: anomalías de rendimiento](app-insights-proactive-performance-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="ea6a0-125">[Smart detection - Performance Anomalies](app-insights-proactive-performance-diagnostics.md).</span></span> <span data-ttu-id="ea6a0-126">Recibir notificaciones si el tiempo de respuesta de una duración de la operación o dependencia se ralentice previsto toohistorical comparados o si se identifica un patrón anómalo en tiempo de respuesta o en tiempo de carga de página.</span><span class="sxs-lookup"><span data-stu-id="ea6a0-126">You get notifications if response time of an operation or dependency duration is slowing down compared toohistorical baseline or if we identify an anomalous pattern in response time or page load time.</span></span>   
* <span data-ttu-id="ea6a0-127">[Detección inteligente: problemas del servicio en la nube de Azure](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span><span class="sxs-lookup"><span data-stu-id="ea6a0-127">[Smart detection - Azure Cloud Service issues](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span></span> <span data-ttu-id="ea6a0-128">Recibe alertas si la aplicación se hospeda en Servicios en la nube de Azure y una instancia de rol tiene errores de inicio, repetición de ciclos frecuentes o bloqueos en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="ea6a0-128">You get alerts if your app is hosted in Azure Cloud Services and a role instance has startup failures, frequent recycling, or runtime crashes.</span></span>

<span data-ttu-id="ea6a0-129">(vínculos de Ayuda de hello en cada notificación permitirán artículos relevantes toohello.)</span><span class="sxs-lookup"><span data-stu-id="ea6a0-129">(hello help links in each notification take you toohello relevant articles.)</span></span>

## <a name="video"></a><span data-ttu-id="ea6a0-130">Vídeo</span><span class="sxs-lookup"><span data-stu-id="ea6a0-130">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="ea6a0-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ea6a0-131">Next steps</span></span>
<span data-ttu-id="ea6a0-132">Estas herramientas de diagnóstico le ayudarán a inspeccionar telemetría Hola desde su aplicación:</span><span class="sxs-lookup"><span data-stu-id="ea6a0-132">These diagnostic tools help you inspect hello telemetry from your app:</span></span>

* [<span data-ttu-id="ea6a0-133">Explorador de métricas</span><span class="sxs-lookup"><span data-stu-id="ea6a0-133">Metric explorer</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="ea6a0-134">Explorador de búsqueda</span><span class="sxs-lookup"><span data-stu-id="ea6a0-134">Search explorer</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="ea6a0-135">Analytics: Lenguaje de consulta eficaz</span><span class="sxs-lookup"><span data-stu-id="ea6a0-135">Analytics - powerful query language</span></span>](app-insights-analytics-tour.md)

<span data-ttu-id="ea6a0-136">La detección inteligente es completamente automática.</span><span class="sxs-lookup"><span data-stu-id="ea6a0-136">Smart Detection is completely automatic.</span></span> <span data-ttu-id="ea6a0-137">¿Pero quizás le gustaría tooset algunas alertas más?</span><span class="sxs-lookup"><span data-stu-id="ea6a0-137">But maybe you'd like tooset up some more alerts?</span></span>

* [<span data-ttu-id="ea6a0-138">Alertas de métricas configuradas manualmente</span><span class="sxs-lookup"><span data-stu-id="ea6a0-138">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="ea6a0-139">Pruebas web de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="ea6a0-139">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md) 

