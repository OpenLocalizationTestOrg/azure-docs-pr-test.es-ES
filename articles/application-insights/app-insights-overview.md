---
title: "¿Qué es Azure Application Insights de aaa? | Microsoft Docs"
description: "Application Performance Management y seguimiento del uso de la aplicación web en directo.  Detecte, evalúe y diagnostique problemas, y comprenda cómo utilizan las personas la aplicación."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 379721d1-0f82-445a-b416-45b94cb969ec
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/14/2017
ms.author: bwren
ms.openlocfilehash: d2596f53a36991fcd08551e6395ece68a5801e39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-application-insights"></a>¿Qué es Application Insights?
Application Insights es un servicio de Application Performance Management (APM) extensible para desarrolladores web en varias plataformas. Usar toomonitor la aplicación web en directo. Se detectarán automáticamente las anomalías de rendimiento. Incluye análisis eficaces herramientas toohelp que diagnosticar problemas y toounderstand lleva a cabo lo que los usuarios con la aplicación.  Se ha diseñado toohelp continuamente mejorar el rendimiento y facilidad de uso. Funciona para las aplicaciones en una amplia variedad de plataformas como. NET, Node.js y J2EE, hospedado en local o en la nube de Hola. Se integra con el proceso de devOps y tiene puntos de conexión tooa gran variedad de herramientas de desarrollo.

![Cree un gráfico de estadísticas de la actividad del usuario o explore en profundidad eventos específicos.](./media/app-insights-overview/00-sample.png)

[Eche un vistazo a la animación de introducción de hello](https://www.youtube.com/watch?v=fX2NtGrh-Y0).

## <a name="how-does-application-insights-work"></a>¿Cómo funciona Application Insights?
Instalar un paquete pequeño instrumentación en la aplicación y configurar un recurso de Application Insights en el portal de Microsoft Azure Hola. instrumentación de Hello supervisa la aplicación y envía el portal de toohello de datos de telemetría. (aplicación hello puede ejecutar desde cualquier lugar; no tiene toobe hospedado en Azure.)

Puede instrumentar la aplicación de servicio web de hello no solo, sino también todos los componentes de fondo y Hola JavaScript en páginas web de Hola por sí mismos. 

![Instrumentación de visión de aplicación de la aplicación envía telemetría tooyour recursos de Application Insights.](./media/app-insights-overview/01-scheme.png)


Además, puede insertar telemetría de los entornos de host de hello como contadores de rendimiento, diagnósticos de Azure o registros de Docker. También puede configurar las pruebas web que envían periódicamente solicitudes sintéticas tooyour servicio de web.

Todas estas secuencias de telemetría se integran en Hola portal de Azure, donde puede aplicar eficaz analíticos y datos sin procesar de toohello de herramientas de búsqueda.


### <a name="whats-hello-overhead"></a>¿Qué es la sobrecarga de hello?
impacto de Hello en el rendimiento de la aplicación es muy pequeña. Las llamadas de seguimiento no suponen ningún tipo de bloqueo y se agrupan por lotes y se envían en un subproceso aparte.

## <a name="what-does-application-insights-monitor"></a>¿Qué supervisa Application Insights?

Application Insights está dirigido al equipo de desarrollo de hello, toohelp comprender el rendimiento de la aplicación y cómo se usa. Supervisa:

* **Tasas de solicitud, tiempos de respuesta y tasas de error** - Averigüe qué páginas que son las más conocidas, en qué momento del día y dónde están los usuarios. Vea qué páginas presentan mejor rendimiento. Si los tiempos de respuesta y las tasas de error aumentan cuando hay más solicitudes, quizás tiene un problema de recursos. 
* **Tasas de dependencia, tiempos de respuesta y tasa de error** - Averigüe si los servicios externos le ralentizan.
* **Excepciones** : analizar Hola agregado las estadísticas, o seleccionar instancias concretas y profundizar en seguimiento de la pila de Hola y las solicitudes relacionadas. Se notifican tanto las excepciones de servidor como las de explorador.
* **Vistas de página y rendimiento de carga** - Notificados por los exploradores de los usuarios.
* **Llamadas AJAX** desde páginas web - Tasas, tiempos de respuesta y tasas de error.
* **Número de usuarios y sesiones**.
* **Contadores de rendimiento** de las máquinas de servidor de Windows o Linux, como CPU, memoria y uso de la red. 
* **Diagnóstico de host** de Docker o Azure. 
* **Registros de seguimiento de diagnóstico** de la aplicación - De esta forma puede correlacionar eventos de seguimiento con las solicitudes.
* **Eventos personalizados y las métricas** que ha escrito en código de cliente o servidor de hello, tootrack eventos empresariales como elementos venden o juegos ganadas.

## <a name="where-do-i-see-my-telemetry"></a>¿Dónde veo la telemetría?

Hay de muchas maneras tooexplore los datos. Consulte estos artículos:

|  |  |
| --- | --- |
| [**Detección inteligente y alertas manuales**](app-insights-proactive-diagnostics.md)<br/>Alertas automáticas adaptan patrones normal de la aplicación tooyour de telemetría y se desencadena cuando hay algún fuera patrón habitual de Hola. También puede [establecer alertas](app-insights-alerts.md) sobre niveles concretos de métricas estándares o personalizadas. |![Ejemplo de alerta](./media/app-insights-overview/alerts-tn.png) |
| [**Mapa de aplicación**](app-insights-app-map.md)<br/>componentes de saludo de la aplicación, con alertas y las métricas clave. |![Mapa de aplicación](./media/app-insights-overview/appmap-tn.png)  |
| [**Generador de perfiles**](app-insights-profiler.md)<br/>Inspeccionar los perfiles de ejecución de Hola de solicitudes muestreadas. |![Generador de perfiles](./media/app-insights-overview/profiler.png) |
| [**Análisis de uso**](app-insights-usage-overview.md)<br/>Analice la segmentación y la retención de usuarios.|![Herramienta Retención](./media/app-insights-overview/retention.png) |
| [**Búsqueda de diagnóstico para datos de instancia**](app-insights-diagnostic-search.md)<br/>Busque y filtre eventos como solicitudes, excepciones, llamadas de dependencia, seguimientos de registro y vistas de páginas.  |![Buscar telemetría](./media/app-insights-overview/search-tn.png) |
| [**Explorador de métricas para datos agregados**](app-insights-metrics-explorer.md)<br/>Explore, filtre y segmente datos agregados, como los índices de solicitudes, errores y excepciones; los tiempos de respuesta y los tiempos de carga de página. |![Métricas](./media/app-insights-overview/metrics-tn.png) |
| [**Paneles**](app-insights-dashboards.md#dashboards)<br/>Combine datos de varios recursos y compártalos con otros. Ideal para aplicaciones de varios componentes y para su presentación continua en la sala de reuniones de Hola. |![Ejemplo de paneles](./media/app-insights-overview/dashboard-tn.png) |
| [**Secuencia de métricas en directo**](app-insights-live-stream.md)<br/>Cuando se implementa una nueva compilación, vea estos toomake de indicadores de rendimiento en tiempo casi real seguro de que todo funciona según lo previsto. |![Ejemplo de métricas en directo](./media/app-insights-overview/live-metrics-tn.png) |
| [**Análisis**](app-insights-analytics.md)<br/>Responda preguntas complejas acerca del uso y el rendimiento de su aplicación mediante este eficaz lenguaje de consulta. |![Ejemplo de análisis](./media/app-insights-overview/analytics-tn.png) |
| [**Visual Studio**](app-insights-visual-studio.md)<br/>Ver datos de rendimiento en el código de hello. Vaya toocode de seguimientos de pila.|![Visual Studio](./media/app-insights-overview/visual-studio-tn.png) |
| [**Depurador de instantáneas**](app-insights-snapshot-debugger.md)<br/>Depure instantáneas muestreadas desde operaciones en directo, con valores de parámetro.|![Visual Studio](./media/app-insights-overview/snapshot.png) |
| [**Power BI**](app-insights-export-power-bi.md)<br/>Integre métricas de uso con otra inteligencia empresarial.| ![Power BI](./media/app-insights-overview/power-bi.png)|
| [**API DE REST**](https://dev.applicationinsights.io/)<br/>Escribir código toorun consultas sobre las métricas y los datos sin procesar.| ![API de REST](./media/app-insights-overview/rest-tn.png) |
| [**Exportación continua**](app-insights-export-telemetry.md)<br/>Exportación masiva de datos sin procesar toostorage tan pronto como llegan. |![Exportación](./media/app-insights-overview/export-tn.png) |

## <a name="how-do-i-use-application-insights"></a>¿Cómo uso Application Insights?

### <a name="monitor"></a>Supervisión
Instale Application Insights en la aplicación web, configure las [pruebas web de disponibilidad](app-insights-monitor-web-app-availability.md) y:

* Configurar un [panel](app-insights-dashboards.md) para su tookeep de salón de equipo un ojo de carga, la capacidad de respuesta y rendimiento de Hola de sus dependencias, página cargas y llamadas de AJAX.
* Detectar que son más lentas de Hola y de la mayoría de las solicitudes de error.
* Inspección [secuencia en directo](app-insights-live-stream.md) cuando se implementa una nueva versión, tooknow inmediatamente sobre una degradación.

### <a name="detect-diagnose"></a>Detección y diagnóstico
Cuando reciba una alerta o detecte un problema:

* Evalúe cuántos usuarios se ven afectados.
* Correlacione los errores con las excepciones, las llamadas de dependencia y los seguimientos.
* Examine el generador de perfiles, las instantáneas, los volcados de pila y los registros de seguimiento.

### <a name="build-measure-learn"></a>Compilación, medición y aprendizaje
[Medir la efectividad de hello](app-insights-usage-overview.md) de cada característica nueva que se implementa.

* Planear toomeasure cómo utilizan los clientes UX nueva o funciones de negocio.
* Escriba datos de telemetría personalizados en el código.
* Ciclo de desarrollo siguiente Hola base en la evidencia de disco duro de la telemetría.

## <a name="get-started"></a>Primeros pasos
Visión de la aplicación es uno de los muchos servicios hospedados en Microsoft Azure y telemetría es enviado para su análisis y presentación de Hola. Por lo que antes de hacer nada más, necesitará una suscripción demasiado[Microsoft Azure](http://azure.com). Es libre toosign y si elige Hola básica [plan de precios](https://azure.microsoft.com/pricing/details/application-insights/) de Application Insights, no hay cargo alguno hasta que la aplicación ha crecido toohave sustancial uso. Si su organización ya tiene una suscripción, podría agregar su tooit de cuenta de Microsoft.

Hay varias maneras de tooget iniciado. Comience con la que más se ajuste a sus necesidades. Puede agregar otros hello más tarde.

* **En tiempo de ejecución: instrumentar la aplicación web en el servidor de Hola.** Evita que cualquier código de toohello de actualización. Necesita el servidor de tooyour de acceso de administrador.
  * [**IIS local o en una máquina virtual**](app-insights-monitor-performance-live-website-now.md)
  * [**Máquina virtual o aplicación web de Azure**](app-insights-monitor-performance-live-website-now.md)
  * [**J2EE**](app-insights-java-live.md)
* **En tiempo de desarrollo: agregar código de tooyour Application Insights.** Le permite toowrite telemetría y tooinstrument back-end y escritorio aplicaciones personalizadas.
  * [Visual Studio](app-insights-asp-net.md) 2013, actualización 2 o superior.
  * Java en [Eclipse](app-insights-java-eclipse.md) u [otras herramientas](app-insights-java-get-started.md)
  * [Node.js](app-insights-nodejs.md)
  * [Otras plataformas](app-insights-platforms.md)
* **[Instrumente sus páginas web](app-insights-javascript.md)** para la vista de la página, AJAX y otros datos de telemetría del lado cliente.
* **[Pruebas de disponibilidad](app-insights-monitor-web-app-availability.md)** : haga ping a su sitio web de manera regular desde nuestros servidores.


## <a name="next-steps"></a>Pasos siguientes
Comience en el tiempo de ejecución con:

* [Servidor IIS](app-insights-monitor-performance-live-website-now.md)
* [Servidor de J2EE](app-insights-java-live.md)

Comience en el tiempo de desarrollo con:

* [ASP.NET](app-insights-asp-net.md)
* [Java](app-insights-java-get-started.md)
* [Node.js](app-insights-nodejs.md)

## <a name="support-and-feedback"></a>Soporte y comentarios
* Preguntas y problemas:
  * [Solución de problemas][qna]
  * [Foro de MSDN](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=ApplicationInsights)
  * [Stackoverflow](http://stackoverflow.com/questions/tagged/ms-application-insights)
* Sus sugerencias:
  * [UserVoice](https://visualstudio.uservoice.com/forums/357324)
* Blog:
  * [Blog de Application Insights](https://azure.microsoft.com/blog/tag/application-insights)

## <a name="videos"></a>Vídeos

[![Introducción animada](./media/app-insights-overview/video-front-1.png)](https://www.youtube.com/watch?v=fX2NtGrh-Y0)

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

<!--Link references-->

[android]: https://github.com/Microsoft/ApplicationInsights-Android
[azure]: ../insights-perf-analytics.md
[client]: app-insights-javascript.md
[desktop]: app-insights-windows-desktop.md
[detect]: app-insights-detect-triage-diagnose.md
[greenbrown]: app-insights-asp-net.md
[ios]: https://github.com/Microsoft/ApplicationInsights-iOS
[java]: app-insights-java-get-started.md
[knowUsers]: app-insights-web-track-usage.md
[platforms]: app-insights-platforms.md
[portal]: http://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
