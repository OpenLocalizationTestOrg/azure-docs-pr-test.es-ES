---
title: "aaaMonitor estado de su aplicación y de uso con Application Insights"
description: "Introducción a Application Insights. Analice el uso, la disponibilidad y el rendimiento de sus aplicaciones web de Microsoft Azure o local."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 9230a6e65e5afb00c36122ff1d1de01ba19cd7f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-in-web-applications"></a>Supervisar el rendimiento de aplicaciones web


Asegúrese de que la aplicación tendrá un rendimiento correcto y descubra rápidamente los posibles errores. [Application Insights] [ start] se le permiten sobre los problemas de rendimiento y excepciones, y le ayudan a encontrar y diagnosticar Hola causas raíz.

Application Insights puede supervisar aplicaciones y servicios web Java y ASP.NET y servicios WCF. Pueden estar hospedados localmente, en máquinas virtuales o como sitios web de Microsoft Azure. 

En el lado del cliente hello, Application Insights puede tardar telemetría de páginas web y una amplia variedad de dispositivos, incluidos iOS, Android y Windows aplicaciones de la tienda.

>[!Note]
> Hemos puesto a su disposición una nueva experiencia que permite buscar las páginas que funcionan con lentitud en su aplicación web. Si no tienes acceso tooit, habilitarlo mediante la configuración de las opciones de vista previa con hello [hoja de vista previa](app-insights-previews.md). Obtenga información sobre esta nueva experiencia en [buscar y corregir cuellos de botella de rendimiento con la investigación de rendimiento interactivo de hello](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).

## <a name="setup"></a>Configuración de la supervisión de rendimiento
Si aún no ha agregado tooyour Application Insights (es decir, si no tiene ApplicationInsights.config) del proyecto, elija una de estas formas tooget iniciado:

* [Aplicaciones web ASP.NET](app-insights-asp-net.md)
  * [Agregar supervisión de excepciones](app-insights-asp-net-exceptions.md)
  * [Agregar supervisión de dependencias](app-insights-monitor-performance-live-website-now.md)
* [Aplicaciones web J2EE](app-insights-java-get-started.md)
  * [Agregar supervisión de dependencias](app-insights-java-agent.md)

## <a name="view"></a>Exploración de las métricas de rendimiento
En [Hola portal de Azure](https://portal.azure.com), examinar los recursos de Application Insights toohello que configuró para la aplicación. hoja de información general de Hello muestra datos de rendimiento básicas:

Haga clic en cualquier toosee gráfico más detalle y los resultados de toosee durante un periodo de tiempo. Por ejemplo, haga clic en mosaico de las solicitudes de hello y, a continuación, seleccione un intervalo de tiempo:

![Desplazarse por los datos de toomore y seleccione un intervalo de tiempo](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

Haga clic en un gráfico toochoose las métricas que muestra, o agregar un nuevo gráfico y seleccione sus métricas:

![Haga clic en una métrica de toochoose gráfico](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> **Desactive todas las métricas de hello** selección completa de toosee Hola que está disponible. las métricas de Hola se dividen en grupos; Cuando se selecciona cualquier miembro de un grupo, solo aparecen hello otros miembros de ese grupo.

## <a name="metrics"></a>¿Qué significa todo esto? Informes y mosaicos de rendimiento
Puede obtener una gran variedad de métricas de rendimiento. Comencemos con los que aparecen de forma predeterminada en el módulo de aplicación Hola.

### <a name="requests"></a>Solicitudes
número de Hola de solicitudes HTTP recibidas en un período especificado. Compare esto con resultados de hello en otro toosee informes cómo la aplicación se comporta como carga de hello varía.

Las solicitudes HTTP incluyen todas las solicitudes GET o POST de páginas, datos e imágenes.

Haga clic en hello mosaico tooget recuentos de direcciones URL específicas.

### <a name="average-response-time"></a>Tiempo medio de respuesta
Mide el tiempo de hello entre la entrada de la respuesta de hello y aplicación que se devuelve de una solicitud de web.

puntos de Hello muestran un movimiento promedio. Si hay una gran cantidad de solicitudes, puede haber otras que se desvían de promedio de hello sin un pico obvio o variaciones en los gráficos de Hola.

Busque picos poco habituales. En general, esperar toorise de tiempo de respuesta con un aumento de las solicitudes. Si el aumento de hello es desproporcionado, la aplicación podría se esté enfrentando a un límite de recursos, como la capacidad de CPU u Hola de un servicio que utiliza.

Haga clic en tiempos de hello mosaico tooget de direcciones URL específicas.

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a>Solicitudes más lentas
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

Muestra las solicitudes que pueden precisar un ajuste de rendimiento.

### <a name="failed-requests"></a>Error en las solicitudes
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

Un recuento de las solicitudes que inician excepciones no detectadas.

Haga clic en hello mosaico toosee Hola detalles de errores específicos y seleccione una solicitud individual toosee sus detalles. 

Solo se conserva una muestra representativa de los errores para su inspección individual.

### <a name="other-metrics"></a>Otras métricas
toosee qué otras métricas que puede mostrar, haga clic en un gráfico y, a continuación, anule la selección de hello métricas toosee Hola completa disponible establecidos. Haga clic en (i) toosee definición de cada métrica.

![Anule la selección de todas las métricas toosee Hola conjunto](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

Al seleccionar cualquier Hola deshabilita métrica Hola otras personas que no pueden aparecer en mismo gráfico.

## <a name="set-alerts"></a>Establecer alertas
toobe una notificación por correo electrónico de los valores inusuales de cualquier métrica, agregar una alerta. Puede elegir los administradores de cuentas de toosend Hola correo electrónico toohello o direcciones de correo electrónico toospecific.

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

Configurar otras propiedades de recursos de hello antes de Hola. No elija recursos de webtest Hola si desea que las alertas de tooset en el rendimiento o las métricas de uso.

Ser unidades de hello toonote cuidado en el que se le pide el valor del umbral de tooenter Hola.

*No se ve botón alerta de hello agregar.* ¿-Es un toowhich de cuenta de grupo tienen acceso de sólo lectura? Póngase en contacto con el Administrador de la cuenta de hello.

## <a name="diagnosis"></a>Diagnóstico de problemas
Para buscar y diagnosticar problemas de rendimiento, lea estas sugerencias:

* Configurar [pruebas web] [ availability] toobe una alerta si el sitio web deja de funcionar o responde lentamente o incorrectamente. 
* Comparar el número de solicitudes de hello con otro toosee de métricas si hay errores o respuesta es lento tooload relacionado.
* [Insertar y buscar las instrucciones de seguimiento] [ diagnostic] en su código toohelp identificar problemas.
* Supervise el funcionamiento de la aplicación web junto con [Live Metrics Stream][livestream].
* Capturar el estado de saludo de la aplicación .net con [depurador instantánea][snapshot].

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a>Búsqueda y corrección de cuellos de botella de rendimiento con la investigación interactiva del rendimiento

Puede usar Hola nuevas Application Insights rendimiento interactivo investigación toolocate áreas de la aplicación Web que se ralentizan el rendimiento general. Se pueden buscar páginas específicas que se ralentizan y use Hola rápidamente [herramienta de generación de perfiles](app-insights-profiler.md) toosee si no hay una correlación entre estas páginas.

### <a name="create-a-list-of-slow-performing-pages"></a>Creación de una lista de páginas con un rendimiento lento 

Hola primer paso para buscar problemas de rendimiento es tooget una lista de hello lenta responde páginas. Hola captura de pantalla siguiente muestra cómo utilizar Hola rendimiento hoja tooget una lista de posibles tooinvestigate de páginas más. Puede ver rápidamente desde esta página que ha habido una disminución del tiempo de respuesta de Hola de aplicación hello aproximadamente 6:00 p.m. y de nuevo a aproximadamente 10 P.M.. También puede ver que operación de hello GET/detalles del cliente tenía algunas larga ejecución operaciones con un tiempo de respuesta medio de 507.05 milisegundos. 

![Rendimiento interactivo de Application Insights](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a>Exploración en profundidad de páginas concretas

Una vez que tenga una instantánea del rendimiento de su aplicación, puede obtener más información sobre las operaciones concretas cuyo rendimiento es bajo. Haga clic en cualquier operación detalladamente Hola lista toosee Hola tal y como se muestra a continuación. En el gráfico de hello puede ver si el rendimiento de Hola se basa en una dependencia. También puede ver cuántos Hola con experiencia de los usuarios distintos tiempos de respuesta. 

![Hoja de operaciones de Application Insights](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a>Exploración en profundidad de un período concreto

Después de haber identificado un punto en el tiempo tooinvestigate, explorar en profundidad aún más toolook en operaciones específicas de Hola que podría haber causado la disminución del rendimiento de Hola. Al hacer clic en un punto específico en el tiempo se obtienen detalles de Hola de página de hello tal y como se muestra a continuación. Hola ejemplo siguiente puede ver las operaciones de hello enumeradas para un período de tiempo determinado junto con los códigos de respuesta del servidor de Hola y duración de la operación de Hola. Tiene también la dirección url de Hola para abrir un elemento de trabajo TFS si necesita toosend este equipo de desarrollo de tooyour de información.

![Porción de tiempo de Application Insights](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a>Exploración en profundidad de una operación concreta

Después de haber identificado un punto en el tiempo tooinvestigate, explorar en profundidad aún más toolook en operaciones específicas de Hola que podría haber causado la disminución del rendimiento de Hola. Haga clic en una operación de hello muestra toosee Hola los detalles de operación de hello tal y como se muestra a continuación. En este ejemplo que puede ver que falló la operación de Hola y Application Insights ha proporcionado detalles Hola de hello aplicación hello de excepción se produjo. Una vez más, desde esta hoja se puede crear fácilmente un elemento de trabajo de TFS.

![Hoja de operaciones de Application Insights](./media/app-insights-web-monitor-performance/performance3.png)


## <a name="next"></a>Pasos siguientes
[Pruebas Web] [ availability] -han enviado solicitudes web tooyour aplicación a intervalos regulares desde alrededor de Hola a todos.

[Capturar y buscar seguimientos de diagnóstico] [ diagnostic] : insertar llamadas de seguimiento y examinar los problemas de hello resultados toopinpoint.

[Seguimiento del uso][usage]: averigüe cuántas personas usan la aplicación.

[Solución de problemas][qna]: con preguntas y respuestas



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md



