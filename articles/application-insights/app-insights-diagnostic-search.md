---
title: "Búsqueda de Azure Application Insights aaaUsing | Documentos de Microsoft"
description: "Busque y filtre los datos de telemetría sin procesar que envía la aplicación web."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2a437555-8043-45ec-937a-225c9bf0066b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: df2b0eb017ad48bcdc6ef57d8dff207d120143b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-search-in-application-insights"></a>Uso de Búsqueda en Application Insights
Búsqueda es una característica de [Application Insights](app-insights-overview.md) usar toofind y explorar los elementos de telemetría individuales, como las vistas de página, excepciones o solicitudes web. Y puede ver los seguimientos de registros y eventos que haya codificado.

(Para consultas más complejas sobre los datos, use [Analytics](app-insights-analytics-tour.md)).

## <a name="where-do-you-see-search"></a>¿Dónde verá Búsqueda?
### <a name="in-hello-azure-portal"></a>Hola portal de Azure
Puede abrir búsqueda diagnóstico explícitamente desde la hoja de información general de visión de aplicación Hola de la aplicación:

![Open diagnostic search](./media/app-insights-diagnostic-search/01-open-Diagnostic.png)

También se abre al hacer clic a través de algunos gráficos y elementos de la cuadrícula. En este caso, sus filtros están establecidos previamente toofocus en el tipo de saludo del elemento seleccionado. 

Por ejemplo, en la hoja de información general de hello, es un gráfico de barras de solicitudes clasificados por tiempo de respuesta. Haga clic en un toosee de intervalo de rendimiento una lista de las solicitudes individuales en ese intervalo de tiempo de respuesta:

![Recorrido mediante clic del rendimiento de la solicitud](./media/app-insights-diagnostic-search/07-open-from-filters.png)

Hola cuerpo principal de búsqueda de diagnóstico es una lista de elementos de telemetría - solicitudes de servidor, la página vistas, los eventos personalizados que ha incluido y así sucesivamente. En hello parte superior de la lista de hello es un gráfico de resumen que muestran recuentos de eventos con el tiempo.

Haga clic en actualización tooget nuevos eventos.

### <a name="in-visual-studio"></a>En Visual Studio

En Visual Studio, también hay una ventana de Búsqueda de Application Insights. Es muy útil para mostrar eventos de telemetría generados por aplicación hello que está depurando. Pero también puede mostrar los eventos de hello recopilados desde la aplicación publicada en hello portal de Azure.

Abra la ventana de búsqueda de hello en Visual Studio:

![Búsqueda de Application Insights abierta en Visual Studio](./media/app-insights-diagnostic-search/32.png)

ventana de búsqueda de Hello tiene portal de características similares toohello web:

![Ventana de búsqueda de Application Insights en Visual Studio](./media/app-insights-diagnostic-search/34.png)

pestaña de la operación de seguimiento de Hello está disponible al abrir una solicitud o una vista de página. Una "operación" es una secuencia de eventos que está asociada a la vista única de solicitud o la página tooa. Por ejemplo, llamadas de dependencia, excepciones, registros de seguimiento y eventos personalizados pueden ser parte de una única operación. Hola operación de seguimiento ficha muestra gráficamente Hola tiempo y la duración de estos eventos en la vista de solicitud o la página de toohello de relación. 

## <a name="inspect-individual-items"></a>Inspección de elementos individuales
Seleccione los campos de clave de telemetría elemento toosee y elementos relacionados. Si desea que el conjunto completo de hello toosee de campos, haga clic en "...". 

![Haga clic en nuevo elemento de trabajo, editar los campos de hello y, a continuación, haga clic en Aceptar.](./media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a>Filtro de los tipos de evento
Abra la hoja de filtro de Hola y elegir tipos de evento de Hola desea toosee. (Si, más adelante, desea que los filtros de hello toorestore con el que se abrió hoja hello, haga clic en Restablecer).

![Elija Filtrar y seleccione los tipos de telemetría](./media/app-insights-diagnostic-search/02-filter-req.png)

los tipos de evento de Hello son:

* **Seguimiento** - [registros de diagnóstico](app-insights-asp-net-trace-logs.md), como llamadas a TrackTrace, log4Net, NLog y System.Diagnostic.Trace.
* **Solicitud** - solicitudes HTTP recibidas por la aplicación de servidor, como páginas, scripts, imágenes, archivos de estilo y datos. Estos eventos son gráficos de información general de solicitud y respuesta para la Hola de toocreate usado.
* **Vista de página** - [telemetría enviados por el cliente web de hello](app-insights-javascript.md), usa toocreate página Ver informes. 
* **Evento personalizado** : si se insertan llamadas tooTrackEvent() en orden demasiado[supervisar el uso de](app-insights-api-custom-events-metrics.md), puede buscar aquí.
* **Excepción** - no detectada [las excepciones producidas en el servidor de hello](app-insights-asp-net-exceptions.md)y los que inicie sesión con TrackException().
* **Dependencia** - [llamadas desde una aplicación de servidor](app-insights-asp-net-dependencies.md) tooother servicios, tales como las API de REST o bases de datos y llamadas de AJAX desde su [código de cliente](app-insights-javascript.md).
* **Disponibilidad**: resultados de [pruebas de disponibilidad](app-insights-monitor-web-app-availability.md).

## <a name="filter-on-property-values"></a>Filtro de los valores de propiedad
Puede filtrar eventos en los valores de hello de sus propiedades. propiedades disponibles de Hello dependen de los tipos de evento de Hola que seleccionó. 

Por ejemplo, seleccione solicitudes con un código de respuesta específico. 

![Expanda una propiedad y elija un valor](./media/app-insights-diagnostic-search/03-response500.png)

No elegir ningún valor de una propiedad determinada tiene el mismo efecto que elegir todos los valores de hello. Se desactiva el filtrado en esa propiedad.

### <a name="narrow-your-search"></a>Acotación de la búsqueda
Observe que Hola cuenta toohello derecha de los valores de filtro de Hola muestran cuántas repeticiones no existe están en conjunto filtrado de hello actual. 

En este ejemplo, es evidente de que esa solicitud de ' Rpt/empleados' hello hace que la mayoría de los errores de hello '500':

![Expanda una propiedad y elija un valor](./media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-hello-same-property"></a>Buscar eventos con hello misma propiedad
Buscar Hola a todos los elementos con hello mismo valor de propiedad:

![Haga clic con el botón secundario en una propiedad](./media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-hello-data"></a>Datos de saludo de búsqueda

> [!NOTE]
> toowrite consultas más complejas, abra [ **análisis** ](app-insights-analytics-tour.md) de arriba Hola de hoja de la búsqueda de Hola.
> 

Puede buscar términos en cualquiera de los valores de propiedad de Hola. Esto es especialmente útil si ha escrito [eventos personalizados](app-insights-api-custom-events-metrics.md) con valores de propiedad. 

Puede ser conveniente tooset un intervalo de tiempo, como búsquedas en un intervalo más corto son más rápidos. 

![Open diagnostic search](./media/app-insights-diagnostic-search/appinsights-311search.png)

Busque palabras completas, no subcadenas. Usar caracteres especiales de tooenclose entre comillas.

| cadena | is *not* found by | but these do find it |
| --- | --- | --- |
| HomeController.About |home<br/>controller<br/>out | homecontroller<br/>about<br/>"homecontroller.about"|
|Estados Unidos|Uni<br/>ted|united<br/>states<br/>united AND states<br/>"united states"

Estos son expresiones de búsqueda de Hola que puede utilizar:

| Consulta de ejemplo | Efecto |
| --- | --- |
| `apple` |Buscar todos los eventos en intervalo de tiempo de hello cuyos campos incluyen hello palabra "apple" |
| `apple AND banana` |Busca eventos que contienen ambos términos. Utilizar "AND" en mayúsculas, no "and". |
| `apple OR banana`<br/>`apple banana` |Buscar eventos que contengan cualquiera de los dos términos. Usar "OR" no "or".<br/>Forma abreviada. |
| `apple NOT banana` |Buscar eventos que contienen una palabra pero no Hola otro. |



## <a name="sampling"></a>muestreo
Si la aplicación genera una gran cantidad de telemetría (y el uso de hello 2.0.0-beta3 de versión de SDK de ASP.NET o una versión posterior), módulo de muestreo adaptativo de hello automáticamente reduce el volumen de Hola que se envía toohello portal enviando sólo una fracción representativa de eventos. Sin embargo, eventos que están relacionado toohello misma solicitud se selecciona o anula la selección como un grupo, por lo que puede desplazarse entre los eventos relacionados. 

[Más información sobre el muestreo](app-insights-sampling.md).



## <a name="create-work-item"></a>Creación de elemento de trabajo
Puede crear un error en GitHub o Visual Studio Team Services con detalles de Hola desde cualquier elemento de telemetría. 

![Haga clic en nuevo elemento de trabajo, editar los campos de hello y, a continuación, haga clic en Aceptar.](./media/app-insights-diagnostic-search/42.png)

Hello primera vez para ello, deberá tooconfigure un tooyour vínculo Team Services cuenta y del proyecto.

![Rellenar Hola URL del servidor de Team Services y el nombre del proyecto de Hola y haga clic en autorizar](./media/app-insights-diagnostic-search/41.png)

(También puede configurar vínculo hello en la hoja de elementos de trabajo de Hola.)

## <a name="save-your-search"></a>Guardado de la búsqueda
Cuando haya establecido todos los filtros de Hola que desee, puede guardar búsqueda hello como favorito. Si trabaja en una cuenta profesional, puede elegir si tooshare con otros miembros del equipo.

![Haga clic en favorito, establezca nombre de Hola y haga clic en Guardar](./media/app-insights-diagnostic-search/08-favorite-save.png)

de nuevo, la búsqueda de Hola de toosee **hoja de información general de toohello vaya** y abrir favoritos:

![Favoritos](./media/app-insights-diagnostic-search/09-favorite-get.png)

Si ha guardado con el intervalo de tiempo relativo, hoja de volver a abrir hello tiene los datos más recientes de Hola. Si ha guardado con el intervalo de tiempo absoluto, vea Hola mismos datos cada vez. (Si 'Relative' no está disponible cuando se desea toosave un favorito, haga clic en el intervalo de tiempo en el encabezado de Hola y establecer un intervalo de tiempo que no es un intervalo personalizado).

## <a name="send-more-telemetry-tooapplication-insights"></a>Enviar telemetría más tooApplication visión
En la telemetría de suma toohello de cuadro enviado por Application Insights SDK, puede:

* Capturar seguimientos de registros de su plataforma de registro de favoritos en [.NET](app-insights-asp-net-trace-logs.md) o [Java](app-insights-java-trace-logs.md). Esto significa que puede buscar en los seguimientos de registros y correlacionarlos con vistas de página, excepciones y otros eventos. 
* [Escribir código](app-insights-api-custom-events-metrics.md) toosend excepciones, eventos personalizados y vistas de página. 

[Obtenga información acerca de cómo se registra toosend y telemetría personalizada tooApplication visión](app-insights-asp-net-trace-logs.md).

## <a name="questions"></a>Preguntas y respuestas
### <a name="limits"></a>¿Qué cantidad de datos se conserva?

Vea hello [resumen límites](app-insights-pricing.md#limits-summary).

### <a name="how-can-i-see-post-data-in-my-server-requests"></a>¿Cómo puedo ver datos POST en mis solicitudes de servidor?
Automáticamente no registramos datos POST de hello, pero puede usar [TrackTrace o registro llamadas](app-insights-asp-net-trace-logs.md). Colocar los datos de entrada de hello en el parámetro de mensaje de Hola. No se puede filtrar en el mensaje de Hola Hola mismo forma puede filtrar según propiedades, pero el límite de tamaño de hello es más largo.

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="add"></a>Pasos siguientes
* [Escribir consultas complejas en Analytics](app-insights-analytics-tour.md)
* [Enviar registros y telemetría personalizada tooApplication visión](app-insights-asp-net-trace-logs.md)
* [Configuración de pruebas de disponibilidad y de capacidad de respuesta](app-insights-monitor-web-app-availability.md)
* [Solución de problemas](app-insights-troubleshoot-faq.md)
