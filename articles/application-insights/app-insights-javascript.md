---
title: aplicaciones web de aaaAzure Application Insights para JavaScript | Documentos de Microsoft
description: "Obtenga recuentos de sesiones y vistas de página, además de datos de cliente web, y realice el seguimiento de los patrones de uso. Detecte problemas de rendimiento y excepciones en páginas web de JavaScript."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 3b710d09-6ab4-4004-b26a-4fa840039500
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 986db3c3776471f9f8556f4e09f2d02aad022549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-web-pages"></a>Application Insights para páginas web
Obtenga información sobre el rendimiento de Hola y el uso de su aplicación o página web. Si agrega [Application Insights](app-insights-overview.md) tooyour secuencia de comandos de página, obtendrá los intervalos de carga de página y llamadas de AJAX, recuentos y detalles de excepciones de explorador y errores de AJAX, así como a los usuarios y los recuentos de sesión. Todos estos datos se pueden segmentar por página, sistema operativo del cliente y versión del explorador, geolocalización y otras dimensiones. Puede establecer alertas sobre recuentos de errores o sobre cargas de página lentas. Y mediante la inserción de llamadas de seguimiento en el código de JavaScript, puede realizar un seguimiento cómo se utilizan las diferentes características de saludo de la aplicación de la página web.

Puede utilizar Application Insights con cualquier página web, solo tiene que agregar un pequeño fragmento de JavaScript. Si su servicio web es [Java](app-insights-java-get-started.md) o [ASP.NET](app-insights-asp-net.md), puede integrar datos de telemetría desde el servidor y los clientes.

![En portal.azure.com, abra el recurso de la aplicación y haga clic en el Explorador.](./media/app-insights-javascript/03.png)

Necesita una suscripción demasiado[Microsoft Azure](https://azure.com). Si su equipo tiene una suscripción de la organización, pida Hola propietario tooadd su tooit Account de Microsoft. El desarrollo y la utilización a pequeña escala no implica ningún costo.

## <a name="set-up-application-insights-for-your-web-page"></a>Configuración de Application Insights para su página Web
Agregue tooyour las páginas Web Hola cargador código fragmento de código, como sigue.

### <a name="open-or-create-application-insights-resource"></a>Apertura o creación de recurso en Application Insights
Hola recursos de Application Insights es donde se muestran los datos sobre rendimiento y el uso de la página. 

Inicie sesión en [Azure Portal](https://portal.azure.com).

Si ya ha configurado para el servidor de saludo de la aplicación de supervisión, ya dispone de un recurso:

![Seleccione Examinar, Servicios para desarrolladores, Application Insights.](./media/app-insights-javascript/01-find.png)

Si no tiene uno, créelo:

![Seleccione Nuevo, Servicios para desarrolladores, Application Insights.](./media/app-insights-javascript/01-create.png)

*¿Tiene ya alguna pregunta?* [Creación de recursos en Application Insights](app-insights-create-new-resource.md).

### <a name="add-hello-sdk-script-tooyour-app-or-web-pages"></a>Agregar script tooyour aplicación de hello SDK o las páginas web
En Inicio rápido, obtener script de Hola para páginas web:

![En la hoja de información general sobre la aplicación, elija Inicio rápido, obtener código toomonitor las páginas web. Copie el script de Hola.](./media/app-insights-javascript/02-monitor-web-page.png)

Insertar el script de Hola justo antes de hello `</head>` etiqueta de cada página que desee tootrack. Si su sitio Web tiene una página maestra, puede colocar el script de Hola no existe. Por ejemplo:

* En un proyecto de ASP.NET MVC, lo colocaría en `View\Shared\_Layout.cshtml`
* En un sitio de SharePoint, en el panel de control hello, abra [configuración del sitio o página maestra](app-insights-sharepoint.md).

script de Hola contiene la clave de instrumentación de Hola que dirige el recurso de Application Insights de hello datos tooyour. 

([Una explicación más detallada del script de Hola. ](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))

*(Si está usando un marco de página web conocido, mire a ver si encuentra adaptadores de Application Insights). Por ejemplo, hay [un módulo AngularJS](http://ngmodules.org/modules/angular-appinsights).)*

## <a name="detailed-configuration"></a>Configuración detallada
Hay varios [parámetros](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) que puede establecer, aunque en la mayoría de los casos, no es necesario. Por ejemplo, puede deshabilitar o limitar número de Hola de llamadas Ajax notificados por la vista de página (tooreduce tráfico). O bien puede establecer depuración modo toohave telemetría mover rápidamente a través de la canalización de hello sin que se va a procesar por lotes.

tooset estos parámetros, busque esta línea en el fragmento de código de hello y agregar más elementos separados por comas después de él:

    })({
      instrumentationKey: "..."
      // Insert here
    });

Hola [parámetros disponibles](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) incluyen:

    // Send telemetry immediately without batching.
    // Remember tooremove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, tooreduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up tooexecution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <a name="run"></a>Ejecución de la aplicación
Ejecutar la aplicación web, usar un mientras toogenerate telemetría y espera una cuestión de segundos. Puede ejecutar mediante hello **F5** clave en el equipo de desarrollo, o publicarlo y que los usuarios puedan trabajar con él.

Si desea toocheck telemetría de Hola que una aplicación web está enviando información de tooApplication, use herramientas de depuración de su explorador (**F12** en muchos exploradores). Los datos se envían toodc.services.visualstudio.com.

## <a name="explore-your-browser-performance-data"></a>Exploración de los datos de rendimiento del explorador
Hola abra Explorador hoja tooshow agrega los datos de rendimiento desde los exploradores de los usuarios.

![En portal.azure.com, abra el recurso de la aplicación y haga clic en Configuración, Explorador](./media/app-insights-javascript/03.png)

*¿Aún no hay datos? Haga clic en **actualizar** al principio de Hola de página de Hola. ¿Todavía nada? Consulte [Solución de problemas](app-insights-troubleshoot-faq.md).*

Hola explorador hoja es un [hoja de métricas explorador](app-insights-metrics-explorer.md) con filtros predefinidos y elementos a un gráfico. Puede editar intervalo de tiempo de hello, filtros y la configuración de gráfico si desea y guardar el resultado de hello como favorito. Haga clic en **Restaurar valores predeterminados** tooget toohello atrás configuración original de hoja.

## <a name="page-load-performance"></a>Rendimiento de carga de la página
En hello superior es un gráfico segmentado de tiempos de carga de página. alto total de Hola de gráfico de Hola representa páginas de tooload y la presentación de tiempo medio de Hola desde la aplicación en los exploradores de los usuarios. tiempo de Hola se mide desde al explorador de hello envía la solicitud HTTP inicial de hello hasta que la carga sincrónica todos los eventos se han procesado, incluido el diseño y la ejecución de scripts. No incluye las tareas asincrónicas, como la carga de elementos web de las llamadas AJAX.

gráfico de Hello segmentos de tiempo de carga de página total de hello en hello [estándares intervalos definidos por W3C](http://www.w3.org/TR/navigation-timing/#processing-model). 

![](./media/app-insights-javascript/08-client-split.png)

Tenga en cuenta que hello *conectado a la red* tiempo suele ser más lenta de lo que cabría esperar, porque es un promedio a través de todas las solicitudes de servidor de hello explorador toohello. Muchas de las solicitudes individuales tienen un tiempo de conexión de 0 porque ya hay un servidor de toohello conexión activa.

### <a name="slow-loading"></a>¿La carga es lenta?
Una carga de página lenta es una importante fuente de insatisfacción para los usuarios. Gráfico de hello indica la carga de página lenta, resulta fácil toodo cierta investigación de diagnóstico.

gráfico de Hello muestra promedio de Hola de todas las cargas de página en la aplicación. toosee si el problema de Hola limita tooparticular páginas, buscar más hacia abajo de la hoja de hello, donde hay una cuadrícula segmentada por página dirección URL:

![](./media/app-insights-javascript/09-page-perf.png)

Observe el recuento de vistas de página de Hola y la desviación estándar. Si el recuento de páginas de hello es muy baja, a continuación, Hola problema no está afectando a los usuarios mucho. Una desviación estándar alta (promedio de toohello comparables propio) indica una gran cantidad de la variación entre las mediciones individuales.

**Amplíe la información de una dirección URL y una vista de página.** Haga clic en cualquier toosee de nombre de página una hoja de dirección URL del explorador gráficos filtrados toothat simplemente; y, a continuación, en una instancia de una vista de página.

![](./media/app-insights-javascript/35.png)

Haga clic en `...` para obtener una lista completa de propiedades para ese evento, o bien inspeccionar llamadas de Ajax de Hola y eventos relacionados. Llamadas Ajax lentas afectan a Hola tiempo de carga de página global si son sincrónicas. Relacionados con los eventos incluyen solicitudes de servidor para hello misma dirección URL (si ha configurado visión de la aplicación en el servidor web).

**Evolución del rendimiento de la página en el tiempo.** Volver a la hoja de exploradores de hello, cambiar la cuadrícula de tiempo de carga de vista de página de hello en un toosee de gráfico de línea si hubiera picos en momentos concretos:

![Haga clic en el encabezado de Hola de cuadrícula de Hola y seleccione un nuevo tipo de gráfico](./media/app-insights-javascript/10-page-perf-area.png)

**Segmentación mediante otras dimensiones.** ¿Quizás las páginas son tooload más lento en una situación determinada de explorador, el sistema operativo cliente o usuario? Agregar un nuevo gráfico y experimentar con hello **Group by** dimensión.

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a>Rendimiento AJAX
Asegúrese de que las llamadas AJAX en sus páginas web funcionan correctamente. Suelen ser usado toofill partes de la página de forma asincrónica. Aunque hello página general podría cargar rápidamente, los usuarios podrían frustrados por comenzar en elementos web en blanco, esperando datos tooappear en ellos.

Llamadas AJAX realizadas desde la página web se muestran en la hoja de exploradores de hello como dependencias.

Hay gráficos de resumen en la parte superior de Hola de hoja de hello:

![](./media/app-insights-javascript/31.png)

y cuadrículas detalladas más abajo:

![](./media/app-insights-javascript/33.png)

Haga clic en cualquier fila para obtener detalles concretos.

> [!NOTE]
> Si elimina el filtro de exploradores de hello en hoja hello, servidor y las dependencias de AJAX se incluyen en estos gráficos. Haga clic en Restaurar valores predeterminados tooreconfigure Hola filtro.
> 
> 

**toodrill en llamadas Ajax error** desplácese hacia abajo de la cuadrícula de errores de dependencia de toohello y, a continuación, haga clic en una instancia específica de toosee de fila.

![](./media/app-insights-javascript/37.png)


Haga clic en `...` para telemetría completa de Hola para una llamada de Ajax.

### <a name="no-ajax-calls-reported"></a>¿No se han notificado llamadas Ajax?
Llamadas AJAX incluyen las llamadas HTTP/HTTPS realizadas desde script de Hola de la página web. Si no se ven notificado, comprobar ese fragmento de código de hello no ha establecido hello `disableAjaxTracking` o `maxAjaxCallsPerView` [parámetros](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).

## <a name="browser-exceptions"></a>Excepciones de explorador
En la hoja de exploradores de hello, hay un gráfico de resumen de las excepciones y una cuadrícula de tipos de excepción más hacia abajo de la hoja de Hola.

![](./media/app-insights-javascript/39.png)

Si no ve las excepciones de explorador notificadas, comprobar ese fragmento de código de hello no ha establecido hello `disableExceptionTracking` [parámetro](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).

## <a name="inspect-individual-page-view-events"></a>Inspección de eventos de vista de página individuales

Por lo general, Application Insights analiza la telemetría de vista de página y usted solo verá informes acumulativos, cuya media se ha calculado en función de todos los usuarios. Pero a efectos de depuración, también puede ver eventos de vista de página individuales.

En la hoja de búsqueda de diagnóstico de hello, establezca filtros tooPage vista.

![](./media/app-insights-javascript/12-search-pages.png)

Seleccione cualquier toosee de eventos más detallados. En la página de detalles de hello, haga clic en "..." toosee todavía con más detalle.

> [!NOTE]
> Si usa [búsqueda](app-insights-diagnostic-search.md), observe que tiene palabras completas toomatch: "Iene" y "má" no coincide con "About".
> 
> 

También puede usar hello eficaz [lenguaje de consulta de análisis de registros](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch las vistas de página.

### <a name="page-view-properties"></a>Propiedades de la vista de página
* **Duración de vista de página** 
  
  * De forma predeterminada, Hola tiempo toma tooload Hola página, de toofull de solicitud de cliente cargue (incluidos los archivos auxiliares pero excluidas las tareas asincrónicas como las llamadas de Ajax). 
  * Si establece `overridePageViewDuration` en hello [configuración de la página](#detailed-configuration), Hola intervalo entre tooexecution de solicitud de cliente de hello primero `trackPageView`. Si mueve trackPageView desde su posición normal después de la inicialización de Hola de secuencia de comandos de hello, refleja un valor diferente.
  * Si `overridePageViewDuration` establecido y una duración se proporciona un argumento de hello `trackPageView()` llamar, a continuación, el valor del argumento Hola se utiliza en su lugar. 

## <a name="custom-page-counts"></a>Recuentos de página personalizados
De forma predeterminada, un recuento de páginas se produce cada vez que se carga una página nueva en el explorador del cliente de Hola.  Sin embargo, podrían desear toocount vistas de página adicionales. Por ejemplo, una página puede mostrar su contenido en las pestañas y desea toocount una página al usuario de hello cambia pestañas. O código JavaScript en la página de hello podría cargar contenido nuevo sin cambiar la dirección URL del explorador de Hola.

Inserte una llamada de JavaScript similar al siguiente en el punto adecuado de hello en el código de cliente:

    appInsights.trackPageView(myPageName);

nombre de la página de Hello puede contener Hola mismo caracteres como una dirección URL, pero nada después de "#" o "?" se omite.

## <a name="usage-tracking"></a>Seguimiento de uso
¿Desea toofind lo que hacer los usuarios con la aplicación?

* [Obtenga información sobre el seguimiento de uso](app-insights-web-track-usage.md)
* [Más información sobre las API para eventos y métricas personalizados](app-insights-api-custom-events-metrics.md).

## <a name="video"></a> Vídeo


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <a name="next"></a> Pasos siguientes
* [Seguir el uso](app-insights-web-track-usage.md)
* [Eventos y métricas personalizados](app-insights-api-custom-events-metrics.md)
* [Compilación - Métrica - Aprendizaje](app-insights-web-track-usage.md)

