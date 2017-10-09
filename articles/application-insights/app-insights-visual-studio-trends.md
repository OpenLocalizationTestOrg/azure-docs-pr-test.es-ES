---
title: Tendencias de aaaAnalyzing en Visual Studio | Documentos de Microsoft
description: "Analizar, mostrar y explorar las tendencias de la telemetría de Application Insights en Visual Studio."
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 3150c6fc-2691-44f6-a290-fc5cd68e692a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: 5c623ec040363f05e80ca927dc8855eb016adc99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyzing-trends-in-visual-studio"></a>Análisis de tendencias en Visual Studio
herramienta de tendencias de Application Insights Hello muestra cómo los eventos de telemetría importante de la aplicación web cambian con el tiempo, ayudar a identificar rápidamente los problemas y las anomalías. Si vincula toomore detallada información de diagnóstico, tendencias pueden ayudarle a mejorar el rendimiento de la aplicación, realizar un seguimiento de las causas de excepciones hello y descubrir información de los eventos personalizados.

![Ejemplo de la ventana de tendencias](./media/app-insights-visual-studio-trends/app-insights-trends-hero-750.png)

## <a name="configure-your-web-app-for-application-insights"></a>Configuración de la aplicación web para Application Insights

Si aún no lo ha hecho, [configure la aplicación web para Application Insights](app-insights-overview.md). Esto le permite portal de Application Insights de toosend telemetría toohello. herramienta de tendencias de Hello lee telemetría Hola desde allí.

Tendencias de Application Insights está disponible en Visual Studio 2015 Update 3 y versiones posteriores.

## <a name="open-application-insights-trends"></a>Tendencias de Application Insights
ventana de tendencias de Application Insights de hello tooopen:

* En el botón de barra de herramientas de Application Insights de hello, elija **explorar las tendencias de telemetría**, o
* En el menú contextual del proyecto hello, elija **Application Insights > explorar las tendencias de telemetría**, o
* En la barra de menús de Visual Studio de hello, elija **Vista > otras ventanas > tendencias de Application Insights**.

Es posible que vea un símbolo del sistema tooselect un recurso. Haga clic en **seleccione un recurso**, inicie sesión con una suscripción de Azure, y luego elija un recurso de Application Insights de lista de hello para el que desea que las tendencias de telemetría de tooanalyze.

## <a name="choose-a-trend-analysis"></a>Elección de un análisis de tendencias
![Menú de tipos comunes de análisis de tendencias](./media/app-insights-visual-studio-trends/app-insights-trends-1-750.png)

Introducción mediante la elección de uno de los cinco análisis tendencia común, cada analizar los datos de hello últimas 24 horas:

* **Investigar los problemas de rendimiento con las solicitudes de servidor** -realizan solicitudes servicio tooyour, agrupado por tiempos de respuesta
* **Analizar los errores en las solicitudes de servidor** -realizan solicitudes servicio tooyour, agrupado por código de respuesta HTTP
* **Examinar las excepciones de hello en la aplicación** -excepciones de su servicio, agrupados por tipo de excepción
* **Compruebe el rendimiento de Hola de dependencias de la aplicación** -Services llama a su servicio, agrupados por tiempos de respuesta
* **Inspeccione sus eventos personalizados** : eventos personalizados que se ha configurado para el servicio, agrupados por tipo de evento.

Pregeneradas análisis están disponibles más tarde desde hello **ver tipos comunes de análisis de telemetría** botón en la esquina superior izquierda de Hola de ventana de las tendencias de hello.

## <a name="visualize-trends-in-your-application"></a>Visualización de tendencias en la aplicación
Tendencias de Application Insights crea una visualización de la serie temporal o de la telemetría de su aplicación. Cada visualización de la serie temporal muestra un tipo de telemetría, agrupados por una propiedad de esa telemetría, a lo largo de algún intervalo de tiempo. Por ejemplo, podría desea que las solicitudes de servidor de tooview, agrupadas por país Hola desde el que se originaron, sobre Hola últimas 24 horas. En este ejemplo, cada burbuja de visualización de hello representaría un recuento de las solicitudes de algún país o región en el servidor de Hola durante una hora.

Usar controles de hello en parte superior de Hola de hello ventana tooadjust qué tipos de telemetría ver. En primer lugar, elija los tipos de telemetría de hello en el que está interesado:

* **Tipo de telemetría** : solicitudes del servidor, excepciones, dependencias o eventos personalizados.
* **Intervalo de tiempo** : en cualquier lugar en los últimos 30 minutos toohello últimos 3 días de Hola
* **Agrupar por** : tipo excepción, identificador del problema, país o región, etc.

A continuación, haga clic en **analizar telemetría** consulta de hello toorun.

toonavigate entre las burbujas en la visualización de hello:

* Haga clic en tooselect una burbuja, que actualiza los filtros de hello en parte inferior de Hola de ventana hello, resumir los eventos de hello simplemente que se produjeron durante un período de tiempo específico
* Haga doble clic en una herramienta de búsqueda de burbujas toonavigate toohello y ver todos los eventos de telemetría individuales de Hola que se produjeron durante ese período de tiempo
* Mantenga pulsada la tecla CTRL y haga clic una burbuja toode-select en la visualización de Hola.

> [!TIP]
> Hola tendencias y busque herramientas funcionan conjuntamente toohelp identificar las causas de Hola de problemas en el servicio entre miles de eventos de telemetría. Por ejemplo, si una tarde sus clientes notan que la aplicación tiene menos capacidad de respuesta, empiece con Tendencias. Analizar las solicitudes realizadas tooyour servicio sobre Hola últimas horas, agrupados por tiempo de respuesta. Vea si hay un clúster de solicitudes lentas inusualmente grande. A continuación, haga doble clic en esa herramienta de búsqueda de burbujas toogo toohello, eventos de solicitud de filtrado toothose. De búsqueda, puede explorar el contenido de Hola de esas solicitudes y navegar por código toohello implicados problema de hello tooresolve.
> 
> 

## <a name="filter"></a>Filtrar
Detectar tendencias más específicas con controles de filtro de hello en parte inferior de Hola de ventana hello. tooapply un filtro, haga clic en su nombre. Puede cambiar rápidamente entre las tendencias de toodiscover filtros diferentes que pueden estar ocultos en una dimensión concreta de la telemetría. Si aplica un filtro en una dimensión, como el tipo de excepción, los filtros de otras dimensiones permanecen seleccionables aunque aparecen atenuados. tooun: aplicar un filtro, haga clic en nuevo. CTRL-clic tooselect varios filtros en Hola la misma dimensión.

![Filtros de tendencia](./media/app-insights-visual-studio-trends/TrendsFiltering-750.png)

¿Qué ocurre si desea tooapply varios filtros? 

1. Aplicar filtro primera Hola. 
2. Haga clic en hello **aplicar los filtros seleccionados y volver a consultar** botón por nombre de Hola de dimensión de Hola de su primer filtro. Esto vuelve a consultará la telemetría para solo los eventos que coinciden con el primer filtro de Hola. 
3. Aplique un segundo filtro. 
4. Repita las tendencias de toofind del proceso de hello en subconjuntos específicos de la telemetría. Por ejemplo, las solicitudes de servidor denominadas "GET Home/Index" *y* que procedían de Alemania *y* que recibieron un código de respuesta 500. 

tooun-aplicar uno de estos filtros, haga clic en hello **quitar los filtros seleccionados y volver a consultar** botón para la dimensión de Hola.

![Varios filtros](./media/app-insights-visual-studio-trends/TrendsFiltering2-750.png)

## <a name="find-anomalies"></a>Búsqueda de anomalías
herramienta de tendencias de Hello puede resaltar las burbujas de eventos anómalos tooother comparados burbujas en hello misma serie temporal. En la lista desplegable Tipo de vista de hello, elija **recuentos en depósitos de tiempo (resaltado anomalías)** o **porcentajes en depósitos de tiempo (resaltado anomalías)**. Las burbujas rojas son anómalas. Anomalías se definen como burbujas con recuentos y porcentajes superior más 2.1 veces Hola desviación estándar de recuentos y porcentajes de hello ocurridos en hello más allá de los dos períodos de tiempo (48 horas si está viendo Hola últimos 24 horas, etcetera)..

![Los puntos de color indican anomalías](./media/app-insights-visual-studio-trends/TrendsAnomalies-750.png)

> [!TIP]
> Resaltar las anomalías es especialmente útil para buscar valores atípicos en series temporales de pequeñas burbujas que, de lo contrario, pueden parecer de tamaño similar.  
> 
> 

## <a name="next"></a>Pasos siguientes
|  |  |
| --- | --- |
| **[Trabajo con Application Insights en Visual Studio](app-insights-visual-studio.md)**<br/>Busque la telemetría, consulte los datos de CodeLens y configure Application Insights. Todos desde Visual Studio. |![Haga clic en proyecto de Hola y elija Application Insights, búsqueda](./media/app-insights-visual-studio-trends/34.png) |
| **[Incorporación de datos adicionales](app-insights-asp-net-more.md)**<br/>Supervise el uso, la disponibilidad, las dependencias y las excepciones. Integrar seguimientos de marcos de registro. Escribir telemetría personalizada. |![Visual Studio](./media/app-insights-visual-studio-trends/64.png) |
| **[Trabajar con el portal de Application Insights Hola](app-insights-dashboards.md)**<br/>Paneles, eficaces herramientas de diagnóstico y análisis, alertas, un mapa activo de dependencias de la aplicación y exportación de la telemetría. |![Visual Studio](./media/app-insights-visual-studio-trends/62.png) |

