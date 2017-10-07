---
title: "aaaDashboards y navegación en hello Azure Application Insights | Documentos de Microsoft"
description: "Cree vistas de los gráficos APM y consultas principales."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 39b0701b-2fec-4683-842a-8a19424f67bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 58811388205643bb672e0405b3226f12d0f447a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="navigation-and-dashboards-in-hello-application-insights-portal"></a>Navegación y paneles en el portal de Application Insights Hola
Una vez haya [configurar Application Insights en el proyecto](app-insights-overview.md), los datos de telemetría acerca del rendimiento y el uso de la aplicación aparecerá en el recurso del proyecto Application Insights en hello [portal de Azure](https://portal.azure.com).

## <a name="find-your-telemetry"></a>Encontrar la telemetría
Inicie sesión en toohello [portal de Azure](https://portal.azure.com) y navegar por los recursos de Application Insights toohello que creó para la aplicación.

![Haga clic en Examinar, seleccione Application Insights y, después, seleccione su aplicación.](./media/app-insights-dashboards/00-start.png)

hoja de información general de Hello (página) para la aplicación muestra un resumen de hello diagnóstico las métricas clave de la aplicación y es una puerta de enlace toohello otras características del portal de Hola.

![Las principales rutas tooview la telemetría](./media/app-insights-dashboards/010-oview.png)

Puede personalizar cualquiera de las cuadrículas y gráficos de Hola y anclarlos tooa panel. De este modo, se puede reunir telemetría clave Hola de diferentes aplicaciones en el panel central.

## <a name="dashboards"></a>Paneles
Hello lo primero que verá después de iniciar sesión en toohello [portal de Microsoft Azure](https://portal.azure.com) es un panel. A continuación, se pueden reunir los gráficos de Hola que son más importante tooyou en todos los recursos de Azure, incluida la telemetría de [Azure Application Insights](app-insights-overview.md).

![Panel personalizado.](./media/app-insights-dashboards/31.png)

1. **Navegar por los recursos toospecific** como la aplicación en Application Insights: barra izquierda Hola de uso.
2. **Panel actual devuelto toohello**, o cambia las vistas reciente tooother: uso Hola menú desplegable situado en la esquina superior izquierda.
3. **Cambiar paneles**: Use Hola menú desplegable situado en el título del panel de Hola
4. **Crear, editar y compartir paneles** en la barra de herramientas del panel Hola.
5. **Modificar el panel de Hola**: mantenga el mouse sobre un icono y, a continuación, utilizar su top barra toomove, personalizar o quitarlo.

## <a name="add-tooa-dashboard"></a>Agregar panel tooa
Cuando se ve una hoja o un conjunto de gráficos que es especialmente interesante, puede anclar una copia del mismo panel toohello. Lo verá la próxima vez que regrese.

![toopin un gráfico, mantenga el mouse sobre él y, a continuación, haga clic en "..." en el encabezado de Hola.](./media/app-insights-dashboards/33.png)

1. Anclar toodashboard de gráfico. Aparece una copia del gráfico de hello en el panel de Hola.
2. Panel de PIN Hola hoja todo toohello - aparece en panel Hola como un icono que puede hacer clic en.
3. Haga clic en hello esquina superior izquierda tooreturn toohello del panel actual. A continuación, puede usar Hola menú desplegable tooreturn toohello la vista actual.

Observe que los gráficos se agrupan en iconos: un icono puede contener más de un gráfico. Anclar Hola todo icono toohello o panel.

gráfico de Hola se actualiza automáticamente con una frecuencia que depende de intervalo de tiempo del gráfico de hello:

* Tiempo de intervalo de hora too1: actualizar cada 5 minutos
* Intervalo de tiempo de 1 a 24 horas: actualizar cada 15 minutos
* Tiempo de intervalo superior a 24 horas: (intervalo de tiempo)/60.

### <a name="pin-any-query-in-analytics"></a>Ancle cualquier consulta en Analytics
También puede [anclar análisis](app-insights-analytics-using.md#pin-to-dashboard) gráficos tooa [compartido](#share-dashboards-with-your-team) panel. Esto le permite tooadd gráficos de cualquier consulta arbitraria junto con las métricas estándar de Hola. 

Los resultados se recalculan automáticamente cada hora. Haga clic en icono de actualización de hello en hello gráfico toorecalculate inmediatamente. (Cuando el explorador se actualiza, no se recalculan los resultados).

## <a name="adjust-a-tile-on-hello-dashboard"></a>Ajustar un icono en el panel de Hola
Una vez un icono en el panel de hello, ajústela.

![Mantenga el mouse sobre un gráfico en orden tooedit.](./media/app-insights-dashboards/36.png)

1. Agregar un icono de toohello gráfico.
2. Establecer la métrica de hello, agrupar por dimensión y el estilo (tabla, gráfico) de un gráfico.
3. Arrastre Hola diagrama toozoom Haga clic en hello deshacer botón tooreset Hola timespan; establecer propiedades del filtro de gráficos de hello en mosaico Hola.
4. Establezca el título del icono.

Los iconos anclados desde hojas del explorador de métricas tienen más opciones de edición que los iconos anclados desde una hoja de información general.

icono original de Hola que haya anclado no se ve afectado por los cambios.

## <a name="switch-between-dashboards"></a>Cambio entre paneles
Puede guardar más de un panel y cambiar de uno a otro. Al anclar un gráfico o la hoja, estas se agregan toohello del panel actual.

![tooswitch entre paneles, haga clic en el panel y seleccione un panel guardado. toocreate y guardar un nuevo panel, haga clic en nuevo. toorearrange, haga clic en Editar.](./media/app-insights-dashboards/32.png)

Por ejemplo, podría tener un panel para mostrar la pantalla completa en la sala de reuniones de hello y otro para el desarrollo general.

En el panel de hello, una hoja aparece como un icono: haga clic en él toogo toohello hoja. Un gráfico de replica gráfico hello en su ubicación original.

![Haga clic en una hoja de hello tooopen de icono que representa](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a>Uso compartido de paneles
Cuando haya creado un panel, puede compartirlo con otros usuarios.

![En el encabezado del panel hello, haga clic en recurso compartido](./media/app-insights-dashboards/41.png)

Aprenda más acerca de [Roles y control de acceso](app-insights-resources-roles-access-control.md).

## <a name="app-navigation"></a>Navegación en la aplicación
hoja de información general de Hello es la información de toomore de puerta de enlace de hello de la aplicación.

* **Cualquier icono o gráfico** : haga clic en cualquier icono o gráfico toosee información más detallada sobre lo que muestra.

### <a name="overview-blade-buttons"></a>Botones de la hoja de información general
![Barra de navegación superior de hoja de información general](./media/app-insights-dashboards/app-overview-top-nav.png)

* [**Explorador de métricas**](app-insights-metrics-explorer.md): cree sus propios gráficos de rendimiento y uso.
* [**Búsqueda**](app-insights-diagnostic-search.md): investigue casos específicos de eventos como solicitudes, excepciones o seguimientos de registro.
* [**Analytics**](app-insights-analytics.md): consultas eficaces sobre los datos de telemetría.
* **El intervalo de tiempo** -ajustar el intervalo de hello muestra todos los gráficos de hello en hoja Hola.
* **Eliminar** -eliminar el recurso de Application Insights de Hola para esta aplicación. Debe también quitar paquetes de Application Insights Hola de código de la aplicación, o editar hello [clave de instrumentación](app-insights-create-new-resource.md#copy-the-instrumentation-key) en su aplicación toodirect telemetría tooa otro recurso de Application Insights.

### <a name="essentials-tab"></a>Pestaña Essentials
* [Clave de instrumentación](app-insights-create-new-resource.md#copy-the-instrumentation-key): identifica este recurso de la aplicación.
* Precios: hacen que las características estén disponibles y establecen límites de volumen.

### <a name="app-navigation-bar"></a>Barra de navegación de la aplicación
![Barra de navegación izquierda](./media/app-insights-dashboards/app-left-nav-bar.png)

* **Información general sobre** -hoja de información general sobre la aplicación toohello devuelto.
* **Registro de actividad**: alertas y eventos administrativos de Azure.
* [**Control de acceso** ](app-insights-resources-roles-access-control.md) -proporcionar acceso a los miembros de tooteam y otros.
* [**Etiquetas** ](../azure-resource-manager/resource-group-using-tags.md) -Use etiquetas toogroup la aplicación con otras personas.

INVESTIGAR

* [**Asignación de la aplicación** ](app-insights-app-map.md) -Active mapa que muestra los componentes de saludo de la aplicación, se deriva de la información de dependencia de Hola.
* [**Detección inteligente**](app-insights-proactive-diagnostics.md): revise las alertas recientes de rendimiento.
* [**Stream en vivo**](app-insights-live-stream.md): un conjunto fijo de métricas casi instantáneas, útiles al implementar una nueva compilación o depurar.
* [**Disponibilidad / Web pruebas** ](app-insights-monitor-web-app-availability.md) -envío solicitudes regular tooyour aplicación web de alrededor de hello world.*
* [**Errores y rendimiento** ](app-insights-web-monitor-performance.md) -excepciones, las tasas de errores y respuesta el tiempo de espera para las solicitudes tooyour aplicación y para las solicitudes de la aplicación demasiado[dependencias](app-insights-asp-net-dependencies.md).
* [**Rendimiento**](app-insights-web-monitor-performance.md): tiempo de respuesta, tiempos de respuesta de dependencia.
* [Servidores](app-insights-web-monitor-performance.md) : contadores de rendimiento. Está disponible si se [instala el Monitor de estado](app-insights-monitor-performance-live-website-now.md).
* **Explorador** : vista de página y rendimiento de AJAX. Está disponible si se [instrumentan las páginas web](app-insights-javascript.md).
* **Uso** : vista de página, recuentos de usuarios y sesiones. Está disponible si se [instrumentan las páginas web](app-insights-javascript.md).

CONFIGURAR

* **Introducción** : tutorial en línea.
* **Propiedades** : clave de instrumentación, suscripción e identificador de recursos.
* [Alertas](app-insights-alerts.md) : configuración de alertas de métricas.
* [Exportación continua](app-insights-export-telemetry.md) -configurar la exportación de almacenamiento de información de telemetría tooAzure.
* [Pruebas de rendimiento](app-insights-monitor-web-app-availability.md#performance-tests) : configuración de una carga simétrica en el sitio web.
* [Cuotas y precios](app-insights-pricing.md) y [muestreo de ingesta](app-insights-sampling.md).
* **El acceso de API** -crear [anotaciones de la versión](app-insights-annotations.md) y para hello API de acceso a datos.
* [**Los elementos de trabajo** ](app-insights-diagnostic-search.md#create-work-item) -conectarse al sistema de seguimiento para que pueda crear errores al inspeccionar la telemetría de trabajo de tooa.

CONFIGURACIÓN

* [**Bloqueos**](../azure-resource-manager/resource-group-lock-resources.md): bloquee recursos de Azure.
* [**Script de automatización** ](app-insights-powershell.md) -exportar una definición de hello recursos de Azure para que se puede usar como un toocreate nuevos recursos de plantilla.


## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Pasos siguientes

|  |  |
| --- | --- |
| [Explorador de métricas](app-insights-metrics-explorer.md)<br/>Filtre y segmente las métricas |![Ejemplo de búsqueda](./media/app-insights-dashboards/64.png) |
| [Búsqueda de diagnóstico](app-insights-diagnostic-search.md)<br/>Busque y examine eventos y eventos relacionados, y cree errores. |![Ejemplo de búsqueda](./media/app-insights-dashboards/61.png) |
| [Analytics](app-insights-analytics.md)<br/>Lenguaje de consulta eficaz |![Ejemplo de búsqueda](./media/app-insights-dashboards/63.png) |
