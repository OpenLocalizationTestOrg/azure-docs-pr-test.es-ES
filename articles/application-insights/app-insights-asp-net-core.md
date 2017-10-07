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
# <a name="application-insights-for-aspnet-core"></a>Application Insights para ASP.NET Core
[Application Insights](app-insights-overview.md) permite supervisar la disponibilidad, el rendimiento y el uso de una aplicación web. Con los comentarios de Hola que obtendrá acerca del rendimiento de Hola y eficacia de la aplicación Hola comodín, pueda tomar decisiones meditadas sobre la dirección de Hola de diseño de hello en cada ciclo de vida de desarrollo.

![Ejemplo](./media/app-insights-asp-net-core/sample.png)

Necesitará una suscripción a [Microsoft Azure](http://azure.com). Inicie sesión con una cuenta Microsoft, que podría tener para Windows, XBox Live u otros servicios en la nube de Microsoft. El equipo puede tener una suscripción organizativa tooAzure: pida Hola propietario tooadd tooit con su cuenta de Microsoft.

## <a name="getting-started"></a>Introducción

* En el Explorador de soluciones de Visual Studio, haga clic con el botón derecho en el proyecto y elija **Configurar Application Insights** o **Agregar > Application Insights**. [Más información](app-insights-asp-net.md).
* Si no ve los comandos de menú, siga hello [manual Guía de introducción al obtener](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started). Puede que necesite toodo si el proyecto se creó con una versión de Visual Studio antes de 2017.

## <a name="using-application-insights"></a>Uso de Application Insights
Inicio de sesión en hello [portal de Microsoft Azure](https://portal.azure.com), seleccione **todos los recursos** o **Application Insights**y, a continuación, seleccione recursos Hola creó toomonitor la aplicación.

En una ventana del explorador independiente, use la aplicación durante un tiempo. Podrá ver datos que aparecen en los gráficos de Application Insights Hola. (Podría tener tooclick actualización). Solo habrá una pequeña cantidad de datos mientras está desarrollando, pero estos gráficos realmente cobrarán vida cuando publique su aplicación y disponga de varios usuarios. 

página de información general de Hello muestra gráficos de rendimiento clave: tiempo de respuesta de servidor, el tiempo de carga de página y el número de solicitudes con error. Haga clic en cualquier toosee gráfico más gráficos y los datos.

Vistas en el portal de Hola se dividen en tres categorías principales:

* [El Explorador de métricas](app-insights-metrics-explorer.md) muestra gráficos y tablas de métricas y recuentos, como tiempos de respuesta, tasas de errores o las métricas crear usted mismo con hello [API](app-insights-api-custom-events-metrics.md). Filtro y el segmento de datos de Hola por tooget de valores de propiedad una mejor comprensión de la aplicación y sus usuarios.
* [Buscar explorador](app-insights-diagnostic-search.md) muestra los eventos individuales, como solicitudes específicas, excepciones, seguimientos del registro o eventos que se haya creado con hello [API](app-insights-api-custom-events-metrics.md). Filtrar y buscar en eventos de Hola y desplazarse entre los problemas de tooinvestigate de eventos relacionados.
* [Analytics](app-insights-analytics.md) permite ejecutar consultas de tipo SQL a través de los datos de telemetría; además, constituye una eficaz herramienta de análisis y diagnóstico.

## <a name="alerts"></a>Alertas
* Obtendrá automáticamente [alertas de diagnóstico proactivo](app-insights-proactive-diagnostics.md) que le comunican cambios anómalos en las tasas de error y otras métricas.
* Configurar [disponibilidad pruebas](app-insights-monitor-web-app-availability.md) tootest su sitio Web continuamente desde ubicaciones en todo el mundo y obtendrá los correos electrónicos en cuanto alguna prueba falla.
* Configurar [alertas métricas](app-insights-monitor-web-app-availability.md) tooknow si dejan de métricas, como tiempos de respuesta o los tipos de excepción fuera de los límites aceptable.

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a>Código abierto
[Leer y contribuir en el código de toohello](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a>Pasos siguientes
* [Agregar páginas web de telemetría tooyour](app-insights-javascript.md) toomonitor página rendimiento y uso.
* [Supervisar las dependencias](app-insights-asp-net-dependencies.md) toosee si se REST, SQL u otros recursos externos se ralenticen.
* [Usar la API de hello](app-insights-api-custom-events-metrics.md) toosend sus propios eventos y métricas para una vista más detallada de rendimiento y el uso de la aplicación.
* [Pruebas de disponibilidad](app-insights-monitor-web-app-availability.md) Compruebe la aplicación procedente de alrededor de Hola a todos. 

