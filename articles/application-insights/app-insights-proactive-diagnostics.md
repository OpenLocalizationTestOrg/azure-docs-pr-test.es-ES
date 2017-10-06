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
# <a name="smart-detection-in-application-insights"></a>Detección inteligente en Application Insights
 La detección inteligente avisa automáticamente de posibles problemas de rendimiento en su aplicación web. Realiza un análisis proactivo de telemetría de Hola que la aplicación envía demasiado[Application Insights](app-insights-overview.md). Si hay un aumento repentino de las tasas de error o patrones de rendimiento anormales en el cliente o el servidor, recibirá una alerta. Esta característica no necesita ninguna configuración. Funciona si la aplicación envía suficiente telemetría.

Puede tener acceso a las alertas de detección inteligente de los mensajes de saludo recibidos y de hoja de detección inteligente de Hola.

## <a name="review-your-smart-detections"></a>Revisión de las detecciones inteligentes
Puede detectar las detecciones de dos maneras:

* **Recibirá un correo electrónico** de Application Insights. Este es un ejemplo típico:
  
    ![Alerta de correo electrónico](./media/app-insights-proactive-diagnostics/03.png)
  
    Haga clic en hello botón grande tooopen más detalle en el portal de Hola.
* **icono de detección inteligente de Hello** en información general de la aplicación hoja muestra un recuento de las alertas recientes. Haga clic en el icono de hello toosee una lista de las alertas recientes.

![Visualización de detecciones recientes](./media/app-insights-proactive-diagnostics/04.png)

Seleccione una alerta toosee sus detalles.

## <a name="what-problems-are-detected"></a>¿Qué problemas se detectan?
Hay tres tipos de detección:

* [Detección inteligente: anomalías de errores](app-insights-proactive-failure-diagnostics.md). Se utiliza aprendizaje automático de velocidad de tooset Hola esperada de solicitudes con error para la aplicación, correlacionar con carga y otros factores. Si deja de tasa de error de hello fuera Hola esperado sobres, se enviará una alerta.
* [Detección inteligente: anomalías de rendimiento](app-insights-proactive-performance-diagnostics.md). Recibir notificaciones si el tiempo de respuesta de una duración de la operación o dependencia se ralentice previsto toohistorical comparados o si se identifica un patrón anómalo en tiempo de respuesta o en tiempo de carga de página.   
* [Detección inteligente: problemas del servicio en la nube de Azure](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/). Recibe alertas si la aplicación se hospeda en Servicios en la nube de Azure y una instancia de rol tiene errores de inicio, repetición de ciclos frecuentes o bloqueos en tiempo de ejecución.

(vínculos de Ayuda de hello en cada notificación permitirán artículos relevantes toohello.)

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Pasos siguientes
Estas herramientas de diagnóstico le ayudarán a inspeccionar telemetría Hola desde su aplicación:

* [Explorador de métricas](app-insights-metrics-explorer.md)
* [Explorador de búsqueda](app-insights-diagnostic-search.md)
* [Analytics: Lenguaje de consulta eficaz](app-insights-analytics-tour.md)

La detección inteligente es completamente automática. ¿Pero quizás le gustaría tooset algunas alertas más?

* [Alertas de métricas configuradas manualmente](app-insights-alerts.md)
* [Pruebas web de disponibilidad](app-insights-monitor-web-app-availability.md) 

