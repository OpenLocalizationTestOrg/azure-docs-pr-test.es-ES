---
title: "análisis de retención de aaaUser para aplicaciones web con Azure Application Insights | Documentos de Microsoft"
description: "¿Cuántos usuarios devuelven tooyour aplicación?"
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 8bcee5f1611afbd69016ec3eef27832c304762a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a>Análisis de retención de usuarios para aplicaciones web con Application Insights

característica de retención de Hello en [Azure Application Insights](app-insights-overview.md) le ayuda a analizar el número de usuarios devolver tooyour aplicación, y con qué frecuencia realizar determinadas tareas o lograr objetivos. Por ejemplo, si ejecuta un sitio de juego, podría comparar números Hola de usuarios que devuelven toohello sitio después de perder un juego con número de Hola que devuelven después el ganador. Esta información puede ayudarlo a mejorar la experiencia de los usuarios y la estrategia empresarial.

## <a name="get-started"></a>Primeros pasos

Si aún no ve los datos en la herramienta de retención de hello en el portal de Application Insights hello, [Obtenga información acerca de cómo tooget a trabajar con herramientas de uso de hello](app-insights-usage-overview.md).

## <a name="hello-retention-tool"></a>herramienta de retención de Hola

![Herramienta Retención](./media/app-insights-usage-retention/retention.png)

1. barra de herramientas de Hello permite a los usuarios toocreate nuevos informes de retención, abra los informes existentes de retención, guardar el informe de retención actual o guardar como, revertir los cambios realizados toosaved informes, actualizar los datos en hello informe, recurso compartido a través de correo electrónico o vínculo directo y Hola de acceso página de documentación. 
2. De forma predeterminada, la herramienta de retención muestra todos los usuarios que hicieron algo y que , posteriormente, regresaron e hicieron algo más a lo largo de un período. Puede seleccionar una combinación diferente de eventos toonarrow Hola se centran en las actividades de usuario específico.
3. Agregue uno o varios filtros en las propiedades. Por ejemplo, puede centrarse en los usuarios de un país o una región determinados. Haga clic en **actualización** después de establecer filtros de Hola. 
4. Hello general retención gráfico muestra un resumen de retención del usuario a través de hello período de tiempo seleccionado. 
5. cuadrícula de Hello muestra número Hola de usuarios conserva correspondiente generador de consultas de toohello de #2. Cada fila representa un grupo de edad de los usuarios que llevó a cabo cualquier evento de hello período de tiempo mostrado. Cada celda de la fila de hello muestra cuántas de ese grupo de edad devuelve al menos una vez en un período más adelante. Algunos usuarios pueden regresar en más de un periodo. 
6. tarjetas de información de Hello muestran los cinco eventos superiores iniciadores y cinco superior devuelve a los usuarios de eventos toogive una mejor comprensión de su informe de retención. 

![Mantener el puntero sobre la retención](./media/app-insights-usage-retention/hover.png)

Los usuarios pueden desplazar el puntero sobre las celdas de botón de análisis de hello retención herramienta tooaccess hello y significa que explique qué celda Hola información sobre herramientas. botón de análisis de Hello toma la herramienta de análisis de los usuarios toohello con un toogenerate consultar rellena automáticamente a los usuarios de celda Hola. 

## <a name="use-business-events-tootrack-retention"></a>Utilizar la retención de tootrack de eventos empresariales

tooget hello más útil retención análisis, eventos de medida que representan actividades empresariales importantes. 

Por ejemplo, muchos usuarios pueden abrir una página de la aplicación sin juego Hola que muestra. Solo las vistas de página Hola de seguimiento, por tanto, proporcionaría una estimación inexacta de cuántas personas devuelven tooplay juego Hola después de se disfruta previamente. tooget una imagen clara de devolver reproductores, la aplicación debe enviar un evento personalizado cuando se reproduce realmente a un usuario.  

Es recomendable toocode los eventos personalizados que representan las acciones de la clave del negocio y usarlos para su análisis de retención. resultado de juegos de hello toocapture, deberá toowrite una línea de código toosend una visión tooApplication de evento personalizado. Si se escribe en el código de la página web de Hola o en Node.JS, parece similar al siguiente:

```JavaScript
    appinsights.trackEvent("won game");
```

O en el código del servidor ASP.NET:

```C#
   telemetry.TrackEvent("won game");
```

[Obtenga más información sobre la creación de eventos personalizados](app-insights-api-custom-events-metrics.md#trackevent).


## <a name="next-steps"></a>Pasos siguientes
- uso de tooenable experimenta, empezar a enviar [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) o [página vistas](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Si ya envía eventos personalizados o las vistas de página, explorar Hola uso herramientas toolearn cómo los usuarios utilizar el servicio.
    - [Usuarios, sesiones, eventos](app-insights-usage-segmentation.md)
    - [Embudos](usage-funnels.md)
    - [Flujos de usuario](app-insights-usage-flows.md)
    - [Libros](app-insights-usage-workbooks.md)
    - [Adición de contexto de usuario](app-insights-usage-send-user-context.md)


