---
title: "diagnóstico de aaaSmart de cambios de rendimiento de aplicaciones web en Azure Application Insights | Documentos de Microsoft"
description: "Diagnóstico automático de subidas o pasos en la telemetría de rendimiento desde la aplicación web."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: cfreeman
ms.openlocfilehash: 8891762c4a4bfdb08b647fe3b702349eb30ec9c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a>Diagnóstico de los cambios repentinos en la telemetría de aplicación

*Esta característica se encuentra en versión preliminar.*

Diagnostique los cambios repentinos en el rendimiento o el uso de la aplicación web con un simple clic. característica de diagnóstico inteligente de Hello está disponible siempre que cree un gráfico de tiempo en [análisis](app-insights-analytics.md) en [Application Insights](app-insights-overview.md). Siempre que hay un cambio inusual de tendencia de Hola de los resultados, como un pico o una dip, diagnósticos inteligentes identifica un patrón de dimensiones y los valores relacionados que puedan explicar los cambios de Hola. Esto ayuda a diagnosticar el problema de hello rápidamente. 

En este ejemplo, diagnósticos inteligentes ha identificado un patrón de los valores de propiedad asociado con el cambio de Hola y pone de manifiesto Hola diferencia entre los resultados con y sin que ese modelo:

![resultados de diagnóstico de análisis de ejemplo](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a>Diagnóstico de cambios en los datos

1.  Ejecute una consulta en Analytics y represéntela como un gráfico de tiempo. 
2.  Haga clic en cualquier punto de subida resaltado, si lo hay.
 
    ![punto de subida](./media/app-insights-analytics-diagnostics/peak.png)

    Diagnóstico tarda unos segundos toodiscover un patrón.

3. pestaña de resultados de diagnóstico de Hello muestra un patrón que puedan explicar la discontinuidad de datos.

    ![result](./media/app-insights-analytics-diagnostics/result.png)
 
    texto Hello muestra valores de la dimensión de Hola que aparecen toocorrelate con desplazamiento Hola. En este ejemplo, está asociado a una solicitud determinada y una versión de explorador determinado.

    Tenga en cuenta también los componentes de hello dos del gráfico de hello, con hello filtro true y false. componente false Hello muestra una tendencia sin cambios. En otras palabras, no hay ningún cambio en los resultados de telemetría de hello, si se excluye la combinación problemático de Hola de dimensiones que ha identificado los diagnósticos. Por el contrario, los resultados de hello dentro de esa combinación muestran un cambio significativo en área de hello resaltado de investigación. Esto muestra que diagnósticos ha encontrado una combinación de propiedades que explica el cambio de Hola.

4.  Si el patrón de hello es complejo, necesitará toohover sobre **mostrar todo** dimensiones de hello toosee.

    ![mostrar todo](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  En caso de diagnósticos no buscan ningún toonotify patrón significativo sobre Hola que se mostrará la página 'sin resultados'. En este momento, puede cambiar la consulta. Por ejemplo, podría restringir el intervalo de tiempo de Hola y de discretización de consulta de análisis, para un análisis posterior y potencialmente mejores resultados.

Gracias a que una página concreta de su sitio Web tiene un problema en un explorador determinado de conocimiento de hello, ahora puede ir a página de problema toohello recta e investigar los cambios recientes.

## <a name="try-hello-demo"></a>Pruebe Hola demostración

[Haga clic aquí toosee una demostración](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) datos de ejemplo.

## <a name="how-it-works"></a>Cómo funciona

Diagnóstico inteligente utiliza un algoritmo de aprendizaje automático supervisados avanzada basado en hello [DiffPatterns](app-insights-analytics-reference.md) operación. Busca patrones de los candidatos que puedan explicar los cambios de datos de Hola. Análisis de impacto de Hola de cada candidato en la métrica de hello y muestra el patrón de Hola que mejor se correlaciona con cambio de Hola.

## <a name="no-diagnostic-points"></a>¿No hay puntos de diagnóstico?

Diagnóstico inteligente sólo funciona cuando se cumple Hola siguiendo criterios:

 * La opción Smart Diagnostics está activada. Haga clic en el icono de configuración de hello en el análisis.
 * Hola opción de diagnósticos inteligentes en la configuración de análisis está seleccionada. 
 * Eje de tiempo: Hola eje x del gráfico de hello debe ser de tipo `datetime`.
 * Gráfico de líneas o de áreas: Diagnostics solo funciona con estos tipos de gráfico. Use `| render timechart` o `| render areachart` al final de saludo de la consulta; o seleccione la línea o un gráfico de áreas del selector de lista desplegable de Hola.
 * Discontinuidad: Debe haber una discontinuidad significativa en los datos de Hola.
 * Tooanalyze suficientes puntos.
 * No más de un resumen de cláusula de consulta de Hola.
 * Ninguna cláusula del proyecto que contiene una definición de nombre antes de hello resumir cláusula.

 
 ## <a name="related-articles"></a>Artículos relacionados

 * [Tutorial de Analytics](app-insights-analytics-tour.md)
 * [Detección de Smart](app-insights-proactive-diagnostics.md) avisa tooperformance problemas automáticamente.
