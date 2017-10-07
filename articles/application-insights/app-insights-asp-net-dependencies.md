---
title: aaaDependency seguimiento en Azure Application Insights | Documentos de Microsoft
description: "Analice el uso, la disponibilidad y el rendimiento de su aplicación web de Microsoft Azure o local con Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d15c4ca8-4c1a-47ab-a03d-c322b4bb2a9e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: e72f5465462ae8e64363cbbaa62911aff636c504
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a>Configurar Application Insights: seguimiento de dependencias
Una *dependencia* es un componente externo al que llama la aplicación. Suele ser un servicio al que se llama mediante HTTP, una base de datos o un sistema de archivos. [Application Insights](app-insights-overview.md) mide cuánto tiempo espera su aplicación a las dependencias y la frecuencia con que se produce un error en una llamada de dependencia. Puede investigar llamadas específicas y relacionarlos toorequests y excepciones.

![gráficos de ejemplo](./media/app-insights-asp-net-dependencies/10-intro.png)

monitor de dependencia del cuadro de Hello actualmente emite llamadas toothese tipos de dependencias:

* Server
  * Bases de datos SQL
  * Servicios WFC y web de ASP.NET que usan enlaces basados en HTTP
  * Llamadas HTTP locales o remotas
  * Azure Cosmos DB, Table Storage, Blob Storage y Queue Storage
* Páginas web
  * Llamadas AJAX

La supervisión funciona mediante la [instrumentación del código de byte](https://msdn.microsoft.com/library/z9z62c29.aspx) alrededor de los métodos seleccionados. La sobrecarga de rendimiento es mínima.

También puede escribir su propio SDK llama toomonitor otras dependencias, tanto en el código de cliente y servidor hello, con hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).

## <a name="set-up-dependency-monitoring"></a>Configuración de la supervisión de dependencias
Hola recopila automáticamente información de dependencia parcial [Application Insights SDK](app-insights-asp-net.md). tooget completa de los datos, instalar agente adecuado de hello para el servidor de host de Hola.

| Plataforma | Instalación |
| --- | --- |
| Servidor IIS |Cualquier [instalar el Monitor de estado en el servidor](app-insights-monitor-performance-live-website-now.md) o [actualizar el marco de aplicación de too.NET 4.6 o posterior](http://go.microsoft.com/fwlink/?LinkId=528259) e instalar hello [Application Insights SDK](app-insights-asp-net.md) en la aplicación. |
| Aplicación web de Azure |En el panel de control de aplicación web, [hoja de Application Insights Hola abierto en el panel de control de aplicación web](app-insights-azure-web-apps.md) y elija instalar si se le solicita. |
| Servicio en la nube de Azure |[Uso de tarea de inicio](app-insights-cloudservices.md) o [Instalación de .NET Framework 4.6 o versiones posteriores](../cloud-services/cloud-services-dotnet-install-dotnet.md) |

## <a name="where-toofind-dependency-data"></a>Donde los datos de dependencia toofind
* [Asignación de aplicación](#application-map) visualiza las dependencias entre la aplicación y los componentes colindantes.
* Las hojas [Rendimiento, Exploradores y Errores](#performance-and-blades) muestran datos de dependencia del servidor.
* La hoja [Exploradores](#ajax-calls) muestra las llamadas AJAX de los exploradores de los usuarios.
* [Haga clic en a través de solicitudes lentas o con errores](#diagnose-slow-requests) toocheck llama a su dependencia.
* [Análisis de](#analytics) pueden ser datos de dependencia de tooquery usado.

## <a name="application-map"></a>Mapa de aplicación
Asignación de la aplicación actúa como una ayuda visual toodiscovering de dependencias entre componentes de saludo de la aplicación. Se genera automáticamente de telemetría de Hola desde la aplicación. Este ejemplo muestra llamadas de AJAX de las secuencias de comandos del explorador de Hola y las llamadas REST del servidor de hello servicios externos tootwo de aplicación.

![Mapa de aplicación](./media/app-insights-asp-net-dependencies/08.png)

* **Navegar desde los cuadros de hello** toorelevant dependencia y otros gráficos.
* **Mapa de hello PIN** toohello [panel](app-insights-dashboards.md), donde será totalmente funcional.

[Más información](app-insights-app-map.md).

## <a name="performance-and-failure-blades"></a>Hojas Rendimiento y Errores
hoja de rendimiento de Hello muestra la duración de Hola de dependencia las llamadas realizadas por la aplicación de servidor hello. Hay un gráfico de resumen y una tabla segmentada por llamadas.

![Gráficos de dependencia de la hoja Rendimiento](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

Desplazarse por los gráficos de resumen de Hola u Hola tabla elementos toosearch sin procesar las instancias de estas llamadas.

![Instancias de llamadas de dependencia](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

**Número de errores** se muestran en hello **errores** hoja. Un error es cualquier código de retorno que no está en hello intervalo 200-399, o desconocido.

> [!NOTE]
> **¿El porcentaje de errores es 100?** Probablemente, esto signifique que está obteniendo datos de dependencias parciales. Necesita demasiado[configurar tooyour adecuado orientada a servicios de dependencia](#set-up-dependency-monitoring).
>
>

## <a name="ajax-calls"></a>Llamadas AJAX
hoja de exploradores de Hello muestra la duración de Hola y llama a tasa de error de AJAX de [JavaScript en las páginas web](app-insights-javascript.md). Se muestran como dependencias.

## <a name="diagnosis"></a> Diagnóstico de solicitudes lentas
Cada evento de solicitud está asociado a las llamadas de dependencia de hello, excepciones y otros eventos que se realiza el seguimiento mientras se procesa la aplicación Hola solicitud. Por lo que si realización algunas solicitudes incorrecto, puede averiguar si es debido a las respuestas de tooslow de una dependencia.

Veamos un ejemplo.

### <a name="tracing-from-requests-toodependencies"></a>Seguimiento de solicitudes toodependencies
Abra la hoja de rendimiento de Hola y examine cuadrícula Hola de solicitudes:

![Lista de solicitudes con promedios y recuentos](./media/app-insights-asp-net-dependencies/02-reqs.png)

parte superior de Hello uno está tardando mucho. Veamos si podemos descubrimos que transcurre el tiempo de Hola.

Haga clic en ese eventos de solicitud individual de toosee de fila:

![Lista de casos de solicitudes](./media/app-insights-asp-net-dependencies/03-instances.png)

Haga clic en cualquier tooinspect de instancia de ejecución prolongada más y desplácese hacia abajo toohello dependencia remoto llamadas relacionadas toothis solicitud:

![Buscar llamadas tooRemote dependencias, identifique duración inusual](./media/app-insights-asp-net-dependencies/04-dependencies.png)

Parece que la mayor parte del servicio de hora de hello que un servicio local de llamada tooa dedicada a esta solicitud.

Seleccione esa fila tooget obtener más información:

![Haga clic en a través de ese punto de entrada y dependencia remoto tooidentify Hola](./media/app-insights-asp-net-dependencies/05-detail.png)

Parece que esto es donde el problema Hola. Se ha detectado el problema de hello, por lo que ahora le necesario toofind out ¿por qué llamada está tardando tanto.

### <a name="request-timeline"></a>Escala de tiempo de solicitudes
En otro caso, no hay ninguna llamada de dependencia especialmente larga. Pero, al cambiar la vista de escala de tiempo toohello, podemos ver dónde se produjo el retraso de hello en el procesamiento interno:

![Buscar llamadas tooRemote dependencias, identifique duración inusual](./media/app-insights-asp-net-dependencies/04-1.png)

Parece que hay toobe un gran espacio después de hello primera dependencia llamada, por lo que debemos mirar en nuestro toosee de código por qué es decir.

### <a name="profile-your-live-site"></a>Generación de un perfil del sitio activo

¿No sabe dónde va el tiempo de presentación? Hola [el generador de perfiles de Application Insights](app-insights-profiler.md) seguimientos HTTP llama tooyour sitio en vivo y muestra las funciones en el código han tardado hello más largo.

## <a name="failed-requests"></a>Error en las solicitudes
Las solicitudes con error también podrían estar asociadas con errores llamadas toodependencies. Una vez más, podemos desplazarse tootrack problema Hola.

![Haga clic en el gráfico de hello las solicitudes con error](./media/app-insights-asp-net-dependencies/06-fail.png)

Desplazarse por los tooan aparición de una solicitud errónea y examine los eventos asociados.

![Haga clic en un tipo de solicitud, haga clic en hello instancia tooget tooa vista diferente de Hola misma instancia, haga clic en detalles de la excepción de tooget.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a>Análisis
Puede realizar un seguimiento de las dependencias en hello [lenguaje de consulta de análisis de registros](https://docs.loganalytics.io/). Estos son algunos ejemplos.

* Búsqueda de llamadas de dependencia con errores:

```

    dependencies | where success != "True" | take 10
```

* Búsqueda de llamadas AJAX:

```

    dependencies | where client_Type == "Browser" | take 10
```

* Búsqueda de llamadas de dependencia asociadas a solicitudes:

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* Búsqueda de llamadas AJAX asociadas a vistas de página:

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a>Seguimiento de dependencias personalizadas
módulo de seguimiento de dependencias estándar Hola detecta automáticamente las dependencias externas, como las bases de datos y las API de REST. Pero puede que desee trata de algunos componentes adicionales toobe Hola misma manera.

Puede escribir código que envía información de dependencia, utilizando Hola mismo [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) utilizado por los módulos estándares Hola.

Por ejemplo, si compila el código con un ensamblado que no es suyo a usted mismo, podría tiempo todos los tooit de llamadas de hello, toofind out qué contribución dificulta la respuesta de tooyour el tiempo de espera. toohave este datos que se muestran en los gráficos de dependencia de Hola de Application Insights, enviarla a través de `TrackDependency`.

```C#

            var startTime = DateTime.UtcNow;
            var timer = System.Diagnostics.Stopwatch.StartNew();
            try
            {
                success = dependency.Call();
            }
            finally
            {
                timer.Stop();
                telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
            }
```

Si desea tooswitch desactivar el módulo de seguimiento de dependencia estándar de hello, quite tooDependencyTrackingTelemetryModule de referencia de hello en [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).

## <a name="troubleshooting"></a>Solución de problemas
*La marca de éxito de dependencia siempre muestra true o false.*

*La consulta SQL no se muestra en su totalidad.*

* Versión más reciente de actualización toohello de hello SDK. Si la versión de .NET es inferior a la 4.6, siga estos pasos:
  * Host de IIS: instalar [agente de visión de la aplicación](app-insights-monitor-performance-live-website-now.md) en los servidores de host de Hola.
  * Aplicación web de Azure: abrir Application Insights pestaña en el panel de control de aplicación de hello web e instale Application Insights.

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Pasos siguientes
* [Excepciones](app-insights-asp-net-exceptions.md)
* [Datos de página y usuario](app-insights-javascript.md)
* [Disponibilidad](app-insights-monitor-web-app-availability.md)
