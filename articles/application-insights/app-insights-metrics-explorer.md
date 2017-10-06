---
title: "aaaExploring las métricas de visión de la aplicación de Azure | Documentos de Microsoft"
description: "Cómo toointerpret gráficos en el Explorador de métrica y cómo toocustomize hojas de métrica del explorador."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: bwren
ms.openlocfilehash: b77ae227ae61e800ad6f3af8a05cd123ea1d69e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-metrics-in-application-insights"></a>Exploración de métricas en Application Insights
Las métricas de [Application Insights][start] son valores medidos y recuentos de eventos que se envían en telemetría desde la aplicación. Ayudar a detectar problemas de rendimiento y a observar las tendencias sobre cómo se utiliza la aplicación. Hay una amplia gama de métricas estándar y también se pueden crear los propios eventos y métricas personalizados.

Los recuentos de métricas y eventos se muestran en los gráficos de valores agregados, como sumas, promedios o recuentos.

A continuación encontrará un conjunto de ejemplo de gráficos:

![](./media/app-insights-metrics-explorer/01-overview.png)

Buscar en todas partes gráficos de métricas en el portal de Application Insights Hola. En la mayoría de los casos, puede personalizarse y puede agregar más hoja toohello de gráficos. En la hoja de información general de hello, haga clic en a través de toomore detallada gráficos (que tienen también como "Servidores"), o haga clic en **Explorer métricas** tooopen una nueva hoja donde puede crear gráficos personalizados.

## <a name="time-range"></a>Intervalo de tiempo
Puede cambiar Hola cubierto por los gráficos de Hola o cuadrículas en cualquier hoja de intervalo de tiempo.

![Hoja de información general de hello abierta de la aplicación Hola portal de Azure](./media/app-insights-metrics-explorer/03-range.png)

Si espera algunos datos que no ha aparecido todavía, haga clic en Actualizar. Gráficos actualización por sí mismas a intervalos, pero los intervalos de hello son más largos para los intervalos de tiempo mayor. Puede tardar unos instantes para toocome de datos a través de la canalización de análisis de hello en un gráfico.

toozoom en parte de un gráfico, arrastre sobre él:

![Arrastre por parte de un gráfico.](./media/app-insights-metrics-explorer/12-drag.png)

Haga clic en toorestore botón Deshacer Zoom de Hola.

## <a name="granularity-and-point-values"></a>Valores de granularidad y punto
Mantenga el mouse sobre los valores de hello gráfico toodisplay Hola de métricas de hello en ese momento.

![Mantenga el mouse de hello sobre un gráfico](./media/app-insights-metrics-explorer/02-focus.png)

valor de Hola de métrica de hello en un momento determinado se agrega en hello precede el intervalo de muestreo.

intervalo de muestreo de Hola o "granularidad" se muestra en la parte superior de Hola de hoja de Hola.

![encabezado de Hola de una hoja.](./media/app-insights-metrics-explorer/11-grain.png)

Puede ajustar la granularidad de hello en la hoja de intervalo de tiempo de hello:

![encabezado de Hola de una hoja.](./media/app-insights-metrics-explorer/grain.png)

granularidades Hola disponibles dependen de intervalo de tiempo de Hola que seleccione. granularidades explícita Hola son toohello "automático" granularidad de alternativas para el intervalo de tiempo de Hola.


## <a name="editing-charts-and-grids"></a>Edición de gráficos y cuadrículas
tooadd una nueva hoja de gráfico toohello:

![En el Explorador de métricas, elija Agregar gráfico](./media/app-insights-metrics-explorer/04-add.png)

Seleccione **editar** en un tooedit de gráfico nuevo o existente lo que muestra:

![Seleccionar una o más métricas](./media/app-insights-metrics-explorer/08-select.png)

Puede mostrar más de una métrica en un gráfico, aunque hay restricciones sobre las combinaciones de Hola que se pueden mostrar juntos. En cuanto elija una métrica, algunos de hello que otros están deshabilitados.

Si se codificó [métricas personalizadas] [ track] en la aplicación (llamadas tooTrackMetric y TrackEvent) se mostrarán aquí.

## <a name="segment-your-data"></a>Segmentación de los datos
Puede dividir una métrica al propiedad: por ejemplo, toocompare las vistas de página en los clientes con sistemas operativos diferentes.

Seleccione un diagrama o cuadrícula, cambie de agrupación y elegir un toogroup de propiedad por:

![Seleccionar Agrupación en, seleccione una propiedad en Agrupar por](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> Cuando se usa la agrupación, tipos de gráfico de barras y de área de hello proporcionan una presentación apilada. Esto es conveniente donde el método de agregación de hello es suma. Pero en su tipo de agregación de hello es promedio, elegir los tipos de pantalla de línea o una cuadrícula de Hola.
>
>

Si se codificó [métricas personalizadas] [ track] en su aplicación e incluyen los valores de propiedad, podrá tooselect capaz de propiedad de hello en lista de Hola.

¿Es demasiado pequeño para los datos segmentados gráfico Hola? Ajuste el alto:

![Ajustar el control deslizante de Hola](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a>Tipos de agregación
leyenda de Hello en el lado de Hola de forma predeterminada muestra normalmente Hola agregado valor período de Hola de gráfico de Hola. Si mantiene el mouse sobre el gráfico de hello, muestra el valor de hello en ese momento.

Cada punto de datos en el gráfico de hello es un agregado Hola de valores de datos recibidos en hello anterior "granularidad" o intervalo de muestreo. granularidad de Hola se muestra en la parte superior de Hola de hoja de Hola y varía en función de hello escala temporal global del gráfico de Hola.

Se agregan métricas diferentes de distintas maneras:

* **Recuento de** es un recuento de eventos de hello recibidos en el intervalo de muestreo de saludo. Se usa para eventos como las solicitudes. Variaciones en el alto de Hola de hello gráfico indica las variaciones de tasa de hello en el que se producen eventos de Hola. Pero tenga en cuenta que el valor numérico de Hola cambia cuando se cambia el intervalo de muestreo de Hola.
* **Suma** suma los valores de hello de todos los puntos de datos de hello recibidos a través de intervalo de muestreo de hello, o un período de hello del gráfico de Hola.
* **Promedio** divide Hola suma por número de Hola de puntos de datos recibidos a través de intervalo de saludo.
* **únicos** se usan para los recuentos de usuarios y cuentas. En el intervalo de muestreo de Hola o durante el período de hello del gráfico de hello, figura hello muestra el recuento de Hola de distintos usuarios que ve en ese momento.
* **%**: solo se usan versiones porcentuales de cada agregación con gráficos segmentados. Hola total siempre agrega too100% y gráfico de hello muestra la contribución relativa de Hola de diferentes componentes de un total.

    ![Agregación porcentual](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-hello-aggregation-type"></a>Cambiar el tipo de agregación de Hola

![Editar gráfico de hello y, a continuación, seleccione agregación](./media/app-insights-metrics-explorer/05-aggregation.png)

método de Hello predeterminado para cada métrica se muestra cuando se crea un nuevo gráfico o cuando se anula la selección de todas las métricas:

![Anule la selección de todos los valores predeterminados de Hola de toosee de métricas](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a>Anclado del eje Y 
De forma predeterminada un gráfico muestra los valores de eje empezando desde cero hasta valores máximos de rango de datos de hello, toogive una representación visual de quantum de valores de hello. Pero en algunos casos más de quantum Hola podría ser interesante toovisually inspeccionar cambios menores en valores. Para las personalizaciones como este uso Hola intervalo edición característica toopin Hola eje y mínimo o máximo valor del eje y en el lugar deseado.
Haga clic en "Configuración avanzada" casilla de verificación toobring seguridad Hola intervalo del eje y configuración

![Haga clic en Configuración avanzada, seleccione Intervalo personalizado y especifique los valores máximo y mínimo](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a>Filtrado de los datos
métricas de hello simplemente toosee para un conjunto de valores de propiedad seleccionado:

![Hacer clic en Filtro, expanda una propiedad y comprobar algunos valores](./media/app-insights-metrics-explorer/19-filter.png)

Si no selecciona ningún valor para una propiedad determinada, se Hola igual que la selección de todas ellas: no hay ningún filtro en esa propiedad.

Hola Observe los recuentos de eventos junto a cada valor de propiedad. Al seleccionar valores de una propiedad, Hola cuenta junto con otros valores se ajustan derechos de propiedad.

Los filtros aplican los gráficos de hello tooall en una hoja. Si desea que los gráficos de toodifferent diferentes filtros aplicados, cree y guarde las hojas de métricas diferentes. Si lo desea, puede anclar gráficos en el panel de toohello módulos diferentes, para que se puedan ver junto a entre sí.

### <a name="remove-bot-and-web-test-traffic"></a>Supresión de bots y de tráfico de prueba web
Usar el filtro de hello **tráfico Real o sintético** y compruebe **Real**.

También puede filtrar por **Origen del tráfico sintético**.

### <a name="tooadd-properties-toohello-filter-list"></a>lista de filtros de tooadd propiedades toohello
¿Le gustaría toofilter telemetría en una categoría de su elección? Por ejemplo, quizás divida los usuarios en distintas categorías y quiera segmentar los datos por estas categorías.

[Cree su propia propiedad](app-insights-api-custom-events-metrics.md#properties). Establézcalo un [telemetría inicializador](app-insights-api-custom-events-metrics.md#defaults) toohave aparecen en todos los telemetría - incluidos telemetría estándar Hola envían por módulos diferentes de SDK.

## <a name="edit-hello-chart-type"></a>Editar el tipo de gráfico de Hola
Observe que puede cambiar entre cuadrículas y gráficos:

![Seleccionar una cuadrícula o gráfico y elegir un tipo de gráfico](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a>Almacenamiento de la hoja de métricas
Cuando haya creado algunos gráficos, guárdelos como favorito. Puede elegir si tooshare con otros miembros del equipo, si utiliza una cuenta profesional.

![Elegir un favorito](./media/app-insights-metrics-explorer/21-favorite-save.png)

nuevo, la hoja de Hola de toosee **hoja de información general de toohello vaya** y abrir favoritos:

![En la hoja de información general de hello, elija Favoritos](./media/app-insights-metrics-explorer/22-favorite-get.png)

Si opta por intervalo de tiempo relativo al guardar, hoja de Hola se actualizará con las métricas de hello más recientes. Si opta por intervalo de tiempo absoluto, aparecerá Hola los mismos datos cada vez.

## <a name="reset-hello-blade"></a>Restablecimiento de hello hoja
Si edita una hoja pero, a continuación, le gustaría tener tooget atrás toohello original guardan conjunto, haga clic en Restablecer.

![En los botones de hello en parte superior de hello del explorador de métrica](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a>Live Metrics Stream

Para obtener una vista mucho más inmediata de la telemetría, abra [Live Stream](app-insights-live-stream.md). La mayoría de las métricas tardar tooappear unos minutos, a causa de proceso de Hola de agregación. Por el contrario, las métricas activas están optimizadas para conseguir una latencia baja. 

## <a name="set-alerts"></a>Establecer alertas
toobe una notificación por correo electrónico de los valores inusuales de cualquier métrica, agregar una alerta. Puede elegir los administradores de cuentas de toosend Hola correo electrónico toohello o direcciones de correo electrónico toospecific.

![En el Explorador de métricas, elija Reglas de alertas, Agregar alerta](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

[Obtenga más información sobre alertas][alerts].


## <a name="continuous-export"></a>Exportación continua
Si quiere que los datos se exporten continuamente para procesarlos externamente, puede usar la [Exportación continua](app-insights-export-telemetry.md).

### <a name="power-bi"></a>Power BI
Si desea que las vistas incluso más completa de los datos, puede [exportar tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).

## <a name="analytics"></a>Análisis
[Análisis de](app-insights-analytics.md) es un tooanalyze de manera más versátil la telemetría mediante un lenguaje de consulta eficaces. Utilícelo si desea toocombine o los resultados de las métricas de proceso o realizar una exploración exhaustiva de rendimiento reciente de la aplicación. 

En un gráfico de métricas, puede hacer clic en hello análisis icono tooget directamente toohello equivalente consulta de análisis.

## <a name="troubleshooting"></a>Solución de problemas
*No veo ningún dato en el gráfico.*

* Los filtros aplican los gráficos de hello tooall en hoja Hola. Asegúrese de que, mientras que desea concentrarse en un gráfico, no ha configurado un filtro que excluye todos los datos de hello en otro.

    Si desea tooset filtros diferentes en distintos gráficos, crearlos en módulos diferentes, guárdelos independientes como favoritos. Si lo desea, puede anclarlos toohello panel para que se puedan ver junto a entre sí.
* Si un gráfico se agrupa por una propiedad que no está definida en la métrica de hello, a continuación, habrá nada en el gráfico de Hola. Intente borrar "Agrupar por" o elija una propiedad de agrupación diferente.
* Los datos de rendimiento (CPU, velocidad de E/S, etc.) están disponibles para servicios web de Java, aplicaciones de escritorio de Windows, [servicios y aplicaciones web IIS si instala el Monitor de estado](app-insights-monitor-performance-live-website-now.md) y [Azure Cloud Services](app-insights-azure.md). No están disponible para los sitios web de Azure.

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Pasos siguientes
* [Supervisión del uso con Application Insights](app-insights-web-track-usage.md)
* [Uso de la Búsqueda de diagnóstico](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
