---
title: aplicaciones de aaaDebug con Azure Application Insights en Visual Studio | Documentos de Microsoft
description: "Análisis del rendimiento y diagnóstico de aplicaciones web durante la depuración y en producción."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/7/2017
ms.author: bwren
ms.openlocfilehash: 20491fbe4505bf719039e5d1c220b1afec01db25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a>Depure sus aplicaciones con Azure Application Insights en Visual Studio
En Visual Studio (2015 y versiones posteriores), se pueden diagnosticar y analizar los problemas de rendimiento de las aplicaciones web, tanto en tiempo de depuración como en producción, mediante los datos de telemetría de [Azure Application Insights](app-insights-overview.md).

Si ha creado la aplicación web ASP.NET mediante Visual Studio de 2017 o versiones posteriores, ya tiene Hola Application Insights SDK. En caso contrario, si aún no lo ha hecho lo ha hecho, [agregar Application Insights tooyour aplicación](app-insights-asp-net.md).

toomonitor la aplicación cuando se encuentra en producción en vivo, normalmente ver telemetría de Application Insights Hola Hola [portal de Azure](https://portal.azure.com), donde puede establecer alertas y aplicar las eficaces herramientas de supervisión. Pero para la depuración, también puede buscar y analizar la telemetría de hello en Visual Studio. Puede usar la telemetría de tooanalyze de Visual Studio desde su sitio de producción y de depuración se ejecuta en el equipo de desarrollo. En este último caso hello, puede analizar ejecuciones de depuración incluso si todavía no ha configurado Hola SDK toosend telemetría toohello portal de Azure. 

## <a name="run"></a> Depure el proyecto
Ejecute la aplicación web en modo de depuración local mediante F5. Abra distintas páginas toogenerate algunos telemetría.

En Visual Studio, verá un recuento de eventos de Hola que se han registrado por el módulo de Application Insights de hello en el proyecto.

![En Visual Studio, el botón de Application Insights de Hola muestra durante la depuración.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

Haga clic en este botón toosearch la telemetría. 

## <a name="application-insights-search"></a>Búsqueda de Application Insights
ventana de búsqueda de visión de la aplicación Hello muestra eventos que se han registrado. (Si se suscribió en tooAzure al configurar Application Insights, puede buscar Hola mismos eventos Hola portal de Azure.)

![Haga clic en proyecto de Hola y elija Application Insights, búsqueda](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> Después de seleccionar o anular la selección de filtros, haga clic en botón de búsqueda de hello final Hola del campo de búsqueda de texto hello.
>

búsqueda de texto sin formato de Hello funciona en todos los campos de eventos de Hola. Por ejemplo, buscar una parte de hello URL de una página; u Hola valor de una propiedad como ciudad del cliente; o palabras específicas en un registro de seguimiento.

Haga clic en cualquier evento toosee sus propiedades en detalle.

Para la aplicación web de solicitudes tooyour, puede hacer clic en a través del código de toohello.

![En detalles de la solicitud, haga clic en a través del código de toohello](./media/app-insights-visual-studio/31.png)

También puede abrir elementos relacionados toohelp diagnosticar las solicitudes con error o las excepciones.

![En detalles de la solicitud, desplácese hacia abajo toorelated elementos](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a>Ver solicitudes con error y excepciones
Mostrar informes de excepción en la ventana de búsqueda de hello. (En algunos tipos anteriores de la aplicación ASP.NET, tienen también[configurar la supervisión de excepciones](app-insights-asp-net-exceptions.md) toosee excepciones controladas por el marco de trabajo de Hola.)

Haga clic en un tooget un seguimiento de pila de excepción. Si el código de hello de aplicación hello está abierto en Visual Studio, puede hacer clic a través de hello pila seguimiento toohello relevantes de línea de código de hello.

![Seguimiento de la pila de excepción](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-hello-code"></a>Ver resúmenes de solicitud y la excepción en el código de hello
Hola línea Code Lens por encima de cada método de controlador, verá un recuento de las solicitudes de Hola y excepciones registradas por Application Insights en hello últimas 24 horas.

![Seguimiento de la pila de excepción](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> Code Lens muestra datos de Application Insights solo si tiene [configurado el portal de Application Insights de aplicación toosend telemetría toohello](app-insights-asp-net.md).
>

[Más información acerca de Application Insights en Code Lens](app-insights-visual-studio-codelens.md)

## <a name="trends"></a>Tendencias
Tendencias es una herramienta para visualizar cómo se comporta la aplicación con el paso del tiempo. 

Elija **explorar las tendencias de telemetría** de botón de barra de herramientas de Application Insights de Hola o una ventana de búsqueda de visión de la aplicación. Elija uno de los cinco tooget consultas comunes iniciado. Puede analizar diferentes conjuntos de datos en función de los tipos de telemetría, los intervalos de tiempo y otras propiedades. 

toofind anomalías en los datos, elija una de las opciones de anomalías de hello en el cuadro desplegable de "Tipo de vista" Hola. Opciones de filtrado de Hello en parte inferior de Hola de ventana hello que sea fácil toohone en subconjuntos específicos de la telemetría.

![Tendencias](./media/app-insights-visual-studio/51.png)

[Más sobre Tendencias](app-insights-visual-studio-trends.md).

## <a name="local-monitoring"></a>Supervisión local
(Desde Visual Studio 2015 Update 2) Si no ha configurado el portal de Application Insights de hello SDK toosend telemetría toohello (de modo que no hay ninguna clave de instrumentación en ApplicationInsights.config), a continuación, ventana de diagnóstico de hello muestra telemetría de la sesión de depuración más reciente. 

Esto es conveniente si ya ha publicado una versión anterior de la aplicación. No desea la telemetría de Hola desde su toobe de las sesiones de depuración mezclarse telemetría hello en hello portal de Application Insights desde la aplicación publicada Hola.

También es útil si tiene algunas [telemetría personalizada](app-insights-api-custom-events-metrics.md) que desea toodebug antes de enviar el portal de toohello de telemetría.

* *En primer lugar, completamente configurado portal de Application Insights toosend telemetría toohello. Pero ahora me gustaría telemetría de hello toosee solo en Visual Studio.*
  
  * En la configuración de la ventana de búsqueda de hello, hay un diagnóstico local de opción toosearch incluso si la aplicación envía portal toohello de telemetría.
  * telemetría toostop enviarse toohello portal, comente la línea hello `<instrumentationkey>...` desde ApplicationInsights.config. Cuando estés nuevo portal de toohello de telemetría toosend listo, quitar los comentarios.


## <a name="next-steps"></a>Pasos siguientes
|  |  |
| --- | --- |
| **[Incorporación de datos adicionales](app-insights-asp-net-more.md)**<br/>Supervise el uso, la disponibilidad, las dependencias y las excepciones. Integrar seguimientos de marcos de registro. Escribir telemetría personalizada. |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| **[Trabajar con el portal de Application Insights Hola](app-insights-dashboards.md)**<br/>Consulte paneles, eficaces herramientas de diagnóstico y análisis, alertas, un mapa activo de dependencias de la aplicación y datos de telemetría exportados. |![Visual Studio](./media/app-insights-visual-studio/62.png) |

