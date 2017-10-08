---
title: "aaaSet el análisis de aplicación web de ASP.NET con Azure Application Insights | Documentos de Microsoft"
description: "Configure el análisis del rendimiento, la disponibilidad y el uso de un sitio web de ASP.NET, hospedado localmente o en Azure."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d0eee3c0-b328-448f-8123-f478052751db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 61a3cdce68da48bfb9450b1d296acc1535f50a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a>Configuración de Application Insights para un sitio web de ASP.NET

Este procedimiento configura su toohello de telemetría ASP.NET web app toosend [Azure Application Insights](app-insights-overview.md) servicio. Funciona para las aplicaciones ASP.NET que se hospedan en su propio servidor IIS o en hello en la nube. Obtener gráficos y un lenguaje de consulta eficaces que le ayudarán a comprender el rendimiento de saludo de la aplicación y cómo las personas usan, más alertas automáticas en errores o problemas de rendimiento. Muchos desarrolladores consideran estas características excelente tal y como están, pero también puede ampliar y personalizar la telemetría de hello si necesita.

Su instalación se realiza desde Visual Studio con unos pocos clics. Tener cargos de hello opción tooavoid limitando el volumen de Hola de telemetría. Esto le permite tooexperiment y depuración o toomonitor un sitio con no muchos usuarios. Si decide que desea toogo con antelación y supervisar su sitio de producción, es fácil tooraise límite de hello más adelante.

## <a name="before-you-start"></a>Antes de comenzar
Necesita:

* Visual Studio 2013, actualización 3 o superior. Es mejor que sea superior.
* Una suscripción demasiado[Microsoft Azure](http://azure.com). Si su equipo u organización tiene una suscripción de Azure, propietario de hello puede agregarle tooit, mediante el uso de la [cuenta de Microsoft](http://live.com).

Existen temas alternativo toolook en si está interesado en:

* [Instrumentación de aplicaciones web en tiempo de ejecución con Application Insights](app-insights-monitor-performance-live-website-now.md)
* [Servicios en la nube de Azure](app-insights-cloudservices.md)

## <a name="ide"></a>Paso 1: Agregar Hola Application Insights SDK

Haga clic con el botón derecho en su proyecto de aplicación web en el Explorador de soluciones y elija **Agregar** > **Telemetría de Application Insights...**  o **Configurar Application Insights**.

![Captura de pantalla del Explorador de soluciones, con Agregar telemetría de Application Insights resaltado](./media/app-insights-asp-net/appinsights-03-addExisting.png)

(En Visual Studio 2015, también hay una opción tooadd Application Insights en el cuadro de diálogo de proyecto nuevo de Hola.)

Continuar la página de configuración de Application Insights toohello:

![Captura de pantalla de la página Registre la aplicación en Application Insights](./media/app-insights-asp-net/visual-studio-register-dialog.png)

**a.** Seleccione la cuenta de hello y suscripción que usar tooaccess Azure.

**b.** Seleccione el recurso de hello en donde desea que toosee Hola datos desde la aplicación de Azure. Por lo general:

* Use un [único recurso para diferentes componentes](app-insights-monitor-multi-role-apps.md) de una sola aplicación. 
* Cree recursos independientes para las aplicaciones no relacionadas.
 
Si desea tooset Hola Hola o grupo de ubicación de recursos donde se almacenan los datos, haga clic en **configurar**. Grupos de recursos son utilizados toocontrol acceso toodata. Por ejemplo, si tiene varias aplicaciones que forman parte de Hola mismo sistema, puede poner sus datos de Application Insights Hola el mismo grupo de recursos.

**c.** Establecer un límite en límite de volumen de datos gratuito hello, tooavoid cargos. Application Insights está libere tooa cierto volumen de telemetría. Una vez creado el recurso de hello, puede cambiar la selección en el portal de hello abriendo **características + precios** > **administración del volumen de datos** > **diario límite de volumen**.

**d.** Haga clic en **registrar** toogo con antelación y configurar Application Insights para su aplicación web. Telemetría se enviarán toohello [portal de Azure](https://portal.azure.com), durante la depuración y después de publicar la aplicación.

**e.** Si no desea portal toohello de toosend telemetría durante la depuración, sólo tiene que agregar aplicación de hello Application Insights SDK tooyour pero no configura un recurso en el portal de Hola. Es posible que pueda toosee telemetría en Visual Studio mientras está depurando. Posteriormente, puede devolver la página de configuración de toothis, o puede esperar hasta después de haber implementado la aplicación y [cambiar datos de telemetría en tiempo de ejecución](app-insights-monitor-performance-live-website-now.md).


## <a name="run"></a>Paso 2: Ejecute la aplicación
Ejecute la aplicación con F5. Abra distintas páginas toogenerate algunos telemetría.

En Visual Studio, verá un recuento de eventos de Hola que se han registrado.

![Captura de pantalla de Visual Studio. botón de Application Insights de Hello muestra durante la depuración.](./media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a>Paso 3: Vea su telemetría
Puede ver la telemetría en Visual Studio o en el portal web de hello Application Insights. Buscar la telemetría en Visual Studio toohelp depurar la aplicación. Supervisar el rendimiento y uso en el portal web de hello cuando el sistema está activo. 

### <a name="see-your-telemetry-in-visual-studio"></a>Visualización de datos de telemetría en Visual Studio

En Visual Studio, abra la ventana de Application Insights hello. Haga clic en hello **Application Insights** botón, o haga clic en el proyecto en el Explorador de soluciones, seleccione **Application Insights**y, a continuación, haga clic en **telemetría Live Search**.

En la ventana de búsqueda de información de aplicación de Visual Studio de hello, vea hello **datos de sesión de depuración** vista de telemetría generado en el lado del servidor hello de la aplicación. Experimentar con filtros de Hola y haga clic en cualquier evento toosee más detalle.

![Captura de pantalla de Hola ver los datos de la sesión de depuración en la ventana de Application Insights de hello.](./media/app-insights-asp-net/55.png)

> [!NOTE]
> Si no ve los datos, asegúrese de que el intervalo de tiempo de hello es correcto y haga clic en el icono de búsqueda de Hola.

[Más información acerca de las herramientas de Application Insights en Visual Studio](app-insights-visual-studio.md).

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a>Visualización de datos de telemetría en el portal web

También puede ver la telemetría en el portal web de Application Insights de hello (a menos que elija tooinstall solo Hola SDK). portal de Hello tiene más vistas de varios componentes de Visual Studio, herramientas analíticas y gráficos. portal de Hello también proporciona alertas.

Abra el recurso de Application Insights. Una sesión toohello [portal de Azure](https://portal.azure.com/) encontró allí, o el proyecto de Hola de menú contextual en Visual Studio y dejar que le lleva allí.

![Captura de pantalla de Visual Studio, que muestra cómo tooopen Hola portal de Application Insights](./media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> Si se produce un error de acceso: ¿tiene más de un conjunto de credenciales de Microsoft y están firmados con un conjunto Hola erróneo? En el portal de hello, cierre la sesión e iniciarla de nuevo.

Hola portal se abrirá en una vista de telemetría de Hola desde la aplicación.

![Captura de pantalla de la página de información general de Application Insights](./media/app-insights-asp-net/66.png)

En el portal de hello, haga clic en cualquier icono o un gráfico toosee más detalle.

[Más información acerca del uso de Application Insights en hello portal de Azure](app-insights-dashboards.md).

## <a name="step-4-publish-your-app"></a>Paso 4: Publique la aplicación
Publicar el servidor IIS de aplicación tooyour o tooAzure. Inspección [secuencia en directo de métricas](app-insights-metrics-explorer.md#live-metrics-stream) toomake que todo está ejecutándose sin problemas.

La telemetría se acumula en el portal de Application Insights hello, donde puede supervisar las métricas, buscar la telemetría y configurar [paneles](app-insights-dashboards.md). También puede usar hello eficaz [lenguaje de consulta de análisis de registros](https://docs.loganalytics.io/) eventos específicos de uso y rendimiento o toofind tooanalyze.

También puede seguir tooanalyze la telemetría en [Visual Studio](app-insights-visual-studio.md), con herramientas tales como la búsqueda de diagnóstico y [tendencias](app-insights-visual-studio-trends.md).

> [!NOTE]
> Si la aplicación envía suficiente Hola de telemetría tooapproach [limitación de peticiones límites](app-insights-pricing.md#limits-summary)automático [muestreo](app-insights-sampling.md) activa. Muestreo reduce la cantidad de Hola de telemetría enviado desde su aplicación, al tiempo que conserva los datos correlacionados con fines de diagnóstico.
>
>

## <a name="land"></a>Ya está listo

¡Enhorabuena! Instalar paquete de Application Insights de hello en la aplicación y configurar el servicio de toosend telemetría toohello Application Insights en Azure.

![Diagrama del movimiento de la telemetría](./media/app-insights-asp-net/01-scheme.png)

Hola recursos de Azure que recibe la telemetría de la aplicación se identifica mediante un *clave de instrumentación*. Encontrará esta clave en el archivo ApplicationInsights.config de hello.


## <a name="upgrade-toofuture-sdk-versions"></a>Actualizar las versiones SDK de toofuture
tooupgrade tooa [nueva versión de hello SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), abra hello **Administrador de paquetes de NuGet** nuevo y el filtro de paquetes instalados. Seleccione **Microsoft.ApplicationInsights.Web** y elija **Actualizar**.

Si ha realizado cualquier tooApplicationInsights.config personalizaciones, guarde una copia del mismo antes de actualizar. A continuación, combinar los cambios en la nueva versión de hello.

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Pasos siguientes

### <a name="more-telemetry"></a>Más telemetría

* **[Datos de carga de página y explorador](app-insights-javascript.md)**: inserte un fragmento de código en las páginas web.
* **[Obtenga una supervisión más detallada de las dependencias y excepciones](app-insights-monitor-performance-live-website-now.md)**: instale el Monitor de estado en el servidor.
* **[Eventos personalizados de código](app-insights-api-custom-events-metrics.md)**  toocount, hora o medir las acciones del usuario.
* **[Obtenga datos del registro](app-insights-asp-net-trace-logs.md)**: ponga en correlación los datos del registro con la telemetría.

### <a name="analysis"></a>Análisis

* **[Trabajo con Application Insights en Visual Studio](app-insights-visual-studio.md)**<br/>Incluye información sobre la depuración con la telemetría, búsqueda de diagnóstico y obtención de detalles toocode.
* **[Trabajar con el portal de Application Insights Hola](app-insights-dashboards.md)**<br/> Incluye información acerca de los paneles, eficaces herramientas de diagnóstico y análisis, alertas, un mapa activo de dependencias de la aplicación y exportación de la telemetría.
* **[Análisis de](app-insights-analytics-tour.md)**  -Hola lenguaje de consulta eficaces.

### <a name="alerts"></a>Alertas

* [Pruebas de disponibilidad](app-insights-monitor-web-app-availability.md): crear pruebas de que el sitio esté visible en la web de hello toomake.
* [Diagnósticos de Smart](app-insights-proactive-diagnostics.md): estas pruebas se ejecutan automáticamente, por lo que no tiene toodo nada tooset su seguridad. Le indican si la aplicación tiene una tasa de solicitudes con error inusual.
* [Alertas de métrica](app-insights-alerts.md): establecer estos toowarn si una métrica supera un umbral. Puede establecerlas en las métricas personalizadas que codifique en la aplicación.

### <a name="automation"></a>Automation

* [Creación de recursos de Application Insights mediante PowerShell](app-insights-powershell.md)
