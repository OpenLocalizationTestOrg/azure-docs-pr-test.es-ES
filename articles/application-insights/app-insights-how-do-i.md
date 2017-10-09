---
title: aaaHow puedo... en Azure Application Insights | Documentos de Microsoft
description: P+F en Application Insights.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 48b2b644-92e4-44c3-bc14-068f1bbedd22
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: bwren
ms.openlocfilehash: 89294c3583b7c4e7998143be6d359f2deb3c8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-i--in-application-insights"></a>¿Cómo ... en Application Insights?
## <a name="get-an-email-when-"></a>Recibir un correo electrónico cuando...
### <a name="email-if-my-site-goes-down"></a>Enviar un correo electrónico si mi sitio deja de funcionar
Establecer una [prueba web de disponibilidad](app-insights-monitor-web-app-availability.md).

### <a name="email-if-my-site-is-overloaded"></a>Enviar un correo electrónico si mi sitio está sobrecargado
Establecer una [alerta](app-insights-alerts.md) en **Tiempo de respuesta del servidor**. Un umbral entre 1 y 2 segundos debería funcionar.

![](./media/app-insights-how-do-i/030-server.png)

La aplicación también podría mostrar señales de esfuerzo al devolver códigos de error. Establezca una alerta en **Solicitudes con error**.

Si desea tooset una alerta en **excepciones de servidor**, es posible que tenga toodo [alguna configuración adicional](app-insights-asp-net-exceptions.md) datos de pedidos toosee.

### <a name="email-on-exceptions"></a>Envío de excepciones por correo electrónico
1. [Configurar supervisión de excepciones](app-insights-asp-net-exceptions.md)
2. [Establecer una alerta](app-insights-alerts.md) en hello excepción contar métrica

### <a name="email-on-an-event-in-my-app"></a>Enviar un correo electrónico sobre un evento en mi aplicación
Supongamos que le gustaría tooget un correo electrónico cuando se produce un evento específico. Application Insights no ofrece esta función directamente, pero puede [enviar una alerta cuando una métrica sobrepasa un umbral](app-insights-alerts.md).

Las alertas se pueden establecer en [métricas personalizadas](app-insights-api-custom-events-metrics.md#trackmetric), aunque no así los eventos no personalizados. Escribir algunas tooincrease código una métrica cuando se produce el evento de hello:

    telemetry.TrackMetric("Alarm", 10);

o:

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

Dado que las alertas tienen dos Estados, deberá toosend un valor bajo cuando considere la posibilidad de alerta de hello toohave finalizado:

    telemetry.TrackMetric("Alarm", 0.5);

Crear un gráfico en [explorer métrica](app-insights-metrics-explorer.md) toosee la alarma:

![](./media/app-insights-how-do-i/010-alarm.png)

Establecer ahora una alerta toofire cuando métrica Hola supera un valor mid durante un breve período:

![](./media/app-insights-how-do-i/020-threshold.png)

Establecer Hola promedio toohello período mínimo.

Verá mensajes de correo electrónico cuando la métrica de hello está por encima y por debajo del umbral de Hola.

Algunos tooconsider puntos:

* Una alerta tiene dos estados ("alerta" y "correcto"). se evalúa el estado de Hello solo cuando se recibe una métrica.
* Se envía un correo electrónico sólo cuando cambia el estado de Hola. Por lo tanto, tendrá que toosend las métricas de alto y bajo valor.
* alerta de hello tooevaluate, promedio de hello queda recogido de valores de hello recibido Hola anterior período. Esto se produce cada vez que se recibe una métrica, por lo que los mensajes de correo electrónico pueden enviarse con más frecuencia que establece el período de Hola.
* Puesto que se envían correos electrónicos de "alerta" y "correcto", puede ser conveniente tooconsider volver a pensar en el evento Monoestable como una condición de dos Estados. Por ejemplo, en lugar de un evento de "trabajo completado", tiene una condición de "trabajo en curso", donde se obtienen mensajes de correo electrónico en hello inicial y final de un trabajo.

### <a name="set-up-alerts-automatically"></a>Configuración de alertas automáticamente
[Usar PowerShell toocreate nuevas alertas](app-insights-alerts.md#automation)

## <a name="use-powershell-toomanage-application-insights"></a>Usar PowerShell tooManage Application Insights
* [Creación de nuevos recursos](app-insights-powershell-script-create-resource.md)
* [Creación de nuevas alertas](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a>Telemetría independiente de diferentes versiones

* Varios roles en una aplicación: usar un único recurso de Application Insights y filtrar por cloud_NombreDelRol. [Más información](app-insights-monitor-multi-role-apps.md)
* Separación de versiones de desarrollo, prueba y publicación: utilizar diferentes recursos de Application Insights. Seleccionar las claves de la instrumentación de Hola de web.config. [Más información](app-insights-separate-resources.md)
* Generación de informes de versiones de compilación: agregar una propiedad usando un inicializador de telemetría. [Más información](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a>Supervisar servidores back-end y aplicaciones de escritorio
[Utilizar el módulo de SDK de Windows Server hello](app-insights-windows-desktop.md).

## <a name="visualize-data"></a>Visualización de datos
#### <a name="dashboard-with-metrics-from-multiple-apps"></a>Panel con métricas de varias aplicaciones
* En el [Explorador de métricas](app-insights-metrics-explorer.md), personalice el gráfico y guárdelo como favorito. Puede anclar toohello panel de Azure.

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a>Panel con datos de otros orígenes y Application Insights
* [Exportar telemetría tooPower BI](app-insights-export-power-bi.md).

O

* Use SharePoint como panel, mostrando los datos en elementos web de SharePoint. [Usar exportación continua y análisis de transmisiones tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).  Usar base de datos de PowerView tooexamine hello y crear un elemento web de SharePoint para PowerView.

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a>Filtrado de usuarios anónimos o autenticados
Si los usuarios inician sesión, puede establecer hello [autenticado Id. de usuario](app-insights-api-custom-events-metrics.md#authenticated-users). (No ocurre automáticamente).

A continuación, puede:

* Buscar identificadores de usuario específicos

![](./media/app-insights-how-do-i/110-search.png)

* Filtrar las métricas tooeither anónimos o autenticados los usuarios

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a>Modificación de valores o nombres de propiedad
Cree un [filtro](app-insights-api-filtering-sampling.md#filtering). Esto le permite modificar o filtrar telemetría antes de que se envíe desde su visión tooApplication de aplicación.

## <a name="list-specific-users-and-their-usage"></a>Enumeración de usuarios específicos y su uso
Si su intención es demasiado[buscar usuarios específicos](#search-specific-users), puede establecer hello [autenticado Id. de usuario](app-insights-api-custom-events-metrics.md#authenticated-users).

Si desea obtener una lista de usuarios con datos como las páginas que ven o la frecuencia con la que inician sesión, tiene dos opciones:

* [Id. de usuario autenticado de conjunto](app-insights-api-custom-events-metrics.md#authenticated-users), [exportar base de datos de tooa](app-insights-code-sample-export-sql-stream-analytics.md) y uso adecuado de herramientas tooanalyze los datos de usuario no existe.
* Si tiene sólo un número reducido de usuarios, envíe eventos personalizados o las métricas, con datos de saludo de interés como Hola valor métrico o el nombre de evento y el Id. de usuario de configuración hello como una propiedad. vistas de página tooanalyze, reemplace las llamadas de trackPageView de JavaScript estándar de Hola. telemetría de servidor tooanalyze, usar una telemetría telemetría inicializador tooadd Hola usuario id tooall server. Puede, a continuación, las métricas de filtro y de segmento y búsquedas en el Id. de usuario de Hola.

## <a name="reduce-traffic-from-my-app-tooapplication-insights"></a>Reducir el tráfico de mi tooApplication de app Insights
* En [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), deshabilite los módulos que no es necesario, tal Recopilador del contador de rendimiento de Hola.
* Use [muestreo y filtrado](app-insights-api-filtering-sampling.md) en hello SDK.
* En las páginas web, limite el número de Hola de llamadas Ajax notificados para cada vista de página. En el fragmento de script de Hola después `instrumentationKey:...` , insertar: `,maxAjaxCallsPerView:3` (o un número adecuado).
* Si usas [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), agregado Hola de lotes de valores de métrica de proceso antes de enviar el resultado de hello. Hay una sobrecarga de TrackMetric() que se proporciona para eso.

Obtenga más información sobre [precios y cuotas](app-insights-pricing.md).

## <a name="disable-telemetry"></a>Deshabilitar la telemetría
demasiado**dinámicamente detener e iniciar** Hola recopilación y transmisión de telemetría de servidor hello:

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



demasiado**deshabilitar los recopiladores estándares seleccionados** : por ejemplo, los contadores de rendimiento, las solicitudes HTTP o dependencias - eliminar o marque como comentario las líneas relevantes de hello en [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). Por ejemplo, podría hacer esto, si desea que toosend sus propios datos TrackRequest.

## <a name="view-system-performance-counters"></a>Visualización de contadores de rendimiento del sistema
Entre hello las métricas que puede mostrar en el Explorador de métricas son un conjunto de contadores de rendimiento del sistema. Hay una hoja predefinida denominada **Servidores** que muestra varios de ellos.

![Abra el recurso de Application Insights y haga clic en Servidores](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a>Si no ve ningún dato de contadores de rendimiento
* **servidor IIS** en su propia máquina o en una VM. [Instale el Monitor de estado](app-insights-monitor-performance-live-website-now.md).
* **Sitio web de Azure** : todavía no se admiten los contadores de rendimiento. Hay varias métricas que se puede obtener como una parte estándar de panel de control de sitio web de Azure Hola.
* **Servidor Unix** - [instale collectd](app-insights-java-collectd.md)

### <a name="toodisplay-more-performance-counters"></a>toodisplay más contadores de rendimiento
* En primer lugar, [agregar un nuevo gráfico](app-insights-metrics-explorer.md) y vea si hello es Hola básica conjunto de contadores que ofrecemos.
* Si no es así, [Agregar conjunto de toohello de hello contadores recopilado por el módulo del contador de rendimiento de hello](app-insights-performance-counters.md).
