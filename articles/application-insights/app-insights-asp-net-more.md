---
title: mayor rendimiento de Azure Application Insights aaaGet | Documentos de Microsoft
description: "Después de la introducción a Application Insights, este es un resumen de las características de hello que puede explorar."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 7ec10a2d-c669-448d-8d45-b486ee32c8db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: bwren
ms.openlocfilehash: 2023728afcf5aa5ecab8b957c8517d4872668765
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="more-telemetry-from-application-insights"></a>Más telemetría desde Application Insights
Una vez haya [agregó código ASP.NET de Application Insights tooyour](app-insights-asp-net.md), hay algunas cosas que puede hacer tooget incluso más telemetría. 

| Acción | Lo que obtiene|
|---|---|
|(Servidores IIS) [Instale Monitor de estado](http://go.microsoft.com/fwlink/?LinkId=506648) en cada máquina del servidor.<br/>(Aplicaciones web de azure) En el panel de control de Azure de hello para la aplicación web de hello, abrirá la hoja de Application Insights de Hola.| [**Contadores de rendimiento**](app-insights-performance-counters.md).<br/>[**Excepciones**](app-insights-asp-net-exceptions.md): seguimiento de la pila detallado.<br/>[**Dependencias**](app-insights-asp-net-dependencies.md).|
|[Agregar fragmento de código de JavaScript de hello tooyour páginas de web](app-insights-javascript.md)|[Rendimiento de página](app-insights-web-track-usage.md), excepciones de explorador y rendimiento de AJAX. Telemetría del lado cliente personalizada.|
|[Cree pruebas web de disponibilidad](app-insights-monitor-web-app-availability.md).|Obtención de alertas si el sitio deja de estar disponible.|
|[Asegúrese de que se genera buildinfo.config](https://msdn.microsoft.com/library/dn449058.aspx) mediante MSBuild.|[Generación de anotaciones en gráficos de métricas](https://blogs.msdn.microsoft.com/visualstudioalm/2013/11/14/implementing-deployment-markers-in-application-insights/).
|[Cree eventos y métricas personalizados](app-insights-api-custom-events-metrics.md).|Recuento de métricas y eventos empresariales, seguimiento de uso detallado y mucho más.|
|[Genere un perfil del sitio activo.](https://aka.ms/AIProfilerPreview)|Intervalos de función detallados de la aplicación web activa.|






