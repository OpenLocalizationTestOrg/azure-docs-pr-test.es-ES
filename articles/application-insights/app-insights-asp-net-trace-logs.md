---
title: los registros de seguimiento de .NET de aaaExplore en Application Insights
description: Busque registros generados con Seguimiento, NLog o Log4Net.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0c2a084f-6e71-467b-a6aa-4ab222f17153
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 6bfcd9e5751c3656236d7eb2fc09321740171a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a>Exploración de registros de seguimiento de .NET en Application Insights
Si usa NLog, log4Net o System.Diagnostics.Trace para el seguimiento de diagnóstico en la aplicación de ASP.NET, puede que los registros que se envían demasiado[Azure Application Insights][start], donde puede explorar y buscar ellos. Los registros se combinará con hello otro telemetría procedentes de la aplicación, para que pueda identificar Hola seguimientos asociados con cada solicitud del usuario de mantenimiento y ponerlos en correlación con eventos e informes de excepción.

> [!NOTE]
> ¿Necesita que el módulo de captura de registro de hello? Es un adaptador útil para registradores de terceros, pero si aún no está usando NLog, log4Net o System.Diagnostics.Trace, considere la posibilidad de llamar directamente a [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) .
>
>

## <a name="install-logging-on-your-app"></a>Instalación del registro en la aplicación
Instale el marco de registro elegido en su proyecto. Esto debería producir una entrada en app.config o web.config.

Si usas System.Diagnostics.Trace, deberá tooadd un tooweb.config de entrada:

```XML

    <configuration>
     <system.diagnostics>
       <trace autoflush="false" indentsize="4">
         <listeners>
           <add name="myListener"
             type="System.Diagnostics.TextWriterTraceListener"
             initializeData="TextWriterOutput.log" />
           <remove name="Default" />
         </listeners>
       </trace>
     </system.diagnostics>
   </configuration>
```
## <a name="configure-application-insights-toocollect-logs"></a>Configurar registros de toocollect Application Insights
**[Agregar proyecto de Application Insights tooyour](app-insights-asp-net.md)**  si aún no lo ha hecho todavía. Verá un compilador de registros de opción tooinclude Hola.

O **configure Application Insights** haciendo clic con el botón derecho en el proyecto en el Explorador de soluciones. Seleccione la opción de hello demasiado**configurar la recopilación de seguimiento**.

*¿No aparece ningún menú de Application Insights ni una opción de compilador de registros?* Pruebe la [solución de problemas](#troubleshooting).

## <a name="manual-installation"></a>Instalación manual
Utilice este método si el tipo de proyecto no es compatible con el instalador de Application Insights hello (por ejemplo un proyecto escritorio de Windows).

1. Si tiene previsto toouse log4Net o NLog, instálelo en el proyecto.
2. En el Explorador de soluciones, haga clic con el botón derecho en el proyecto y seleccione **Administrar paquetes de NuGet**.
3. Busque "Application Insights"
4. Seleccione el paquete adecuado de hello - uno de:

   * Microsoft.ApplicationInsights.TraceListener (llamadas a System.Diagnostics.Trace toocapture)
   * Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource eventos)
   * Microsoft.ApplicationInsights.EtwListener (toocapture los eventos ETW)
   * Microsoft.ApplicationInsights.NLogTarget
   * Microsoft.ApplicationInsights.Log4NetAppender

paquete de NuGet Hola instala a los ensamblados necesarios de Hola y también modifica el archivo web.config o app.config.

## <a name="insert-diagnostic-log-calls"></a>Insertar llamadas de registro de diagnóstico
Si usa System.Diagnostics.Trace, una llamada típica sería:

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

Si prefiere log4net o NLog:

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a>Uso de eventos EventSource
Puede configurar [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) tooApplication de toobe enviado eventos visión como seguimientos. En primer lugar, instale hello `Microsoft.ApplicationInsights.EventSourceListener` paquete NuGet. A continuación, edite `TelemetryModules` sección de hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) archivo.

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

Para cada origen, puede establecer Hola parámetros siguientes:
 * `Name`Especifica el nombre de Hola de hello EventSource toocollect.
 * `Level`Especifica hello toocollect de nivel de registro. Puede ser `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose` o `Warning`.
 * `Keywords`(Opcional) especifica el valor entero hello toouse de combinaciones de palabras clave.

## <a name="using-diagnosticsource-events"></a>Uso de eventos de DiagnosticSource
Puede configurar [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) tooApplication de toobe enviado eventos visión como seguimientos. En primer lugar, instale hello [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) paquete NuGet. A continuación, edite hello `TelemetryModules` sección de hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) archivo.

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

Para cada DiagnosticSource desea tootrace, agregue una entrada con hello `Name` toohello nombre de su DiagnosticSource del conjunto de atributos.

## <a name="using-etw-events"></a>Uso de eventos ETW
Puede configurar toobe de eventos ETW enviado tooApplication visión como seguimientos. En primer lugar, instale hello `Microsoft.ApplicationInsights.EtwCollector` paquete NuGet. A continuación, edite `TelemetryModules` sección de hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) archivo.

> [!NOTE] 
> Solo se pueden recopilar eventos ETW si Hola Hola de hospedaje de proceso SDK se está ejecutando bajo una identidad que sea miembro de "Usuarios del registro de rendimiento" o los administradores.

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

Para cada origen, puede establecer Hola parámetros siguientes:
 * `ProviderName`es el nombre de Hola de toocollect de proveedor ETW de Hola.
 * `ProviderGuid`Especifica Hola GUID de hello toocollect de proveedor ETW, se puede utilizar en lugar de `ProviderName`.
 * `Level`establece hello toocollect de nivel de registro. Puede ser `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose` o `Warning`.
 * `Keywords`Valor entero de la palabra clave combinaciones toouse Hola a conjuntos (opcionales).

## <a name="using-hello-trace-api-directly"></a>Directamente con la API de seguimiento de Hola
Puede llamar directamente a API de seguimiento de hello Application Insights. los adaptadores de registro de Hello utilizan esta API.

Por ejemplo:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

La ventaja de TrackTrace es que puede colocar datos relativamente largos en mensajes de bienvenida. Por ejemplo, aquí podría codificar datos POST.

Además, puede agregar un mensaje de tooyour de nivel de gravedad. Y, al igual que otros telemetría, puede agregar valores de propiedad que se puede utilizar toohelp filtrar o buscar para diferentes conjuntos de seguimientos. Por ejemplo:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

Esto permitiría que, en [búsqueda][diagnostic], tooeasily filtrar todos los mensajes de saludo de un nivel de gravedad determinado relacionados con la base de datos determinada tooa.

## <a name="explore-your-logs"></a>Explorar los registros
Ejecute la aplicación, ya sea en modo de depuración o mediante su implementación para que esté activa.

En la hoja de información general de la aplicación en [portal de Application Insights hello][portal], elija [búsqueda][diagnostic].

![En Application Insights, elija Buscar.](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Búsqueda](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

Por ejemplo, puede:

* Filtrar por seguimientos de registro, o por elementos con determinadas propiedades
* Inspeccionar un elemento específico en detalle
* Buscar otra telemetría relacionada con toohello misma solicitud de usuario (es decir, con Hola mismo OperationId)
* Guardar configuración de Hola de esta página como favorito

> [!NOTE]
> **Muestreo.** Si la aplicación envía una gran cantidad de datos y utilizas Hola Application Insights SDK para ASP.NET versión 2.0.0-beta3 o posterior, característica de muestreo adaptativo de hello puede operar y enviar solamente un porcentaje de la telemetría. [Aprenda más sobre el muestreo.](app-insights-sampling.md)
>
>

## <a name="next-steps"></a>Pasos siguientes
[Diagnóstico de errores y excepciones en ASP.NET][exceptions]

[Aprenda más sobre la búsqueda][diagnostic].

## <a name="troubleshooting"></a>Solución de problemas
### <a name="how-do-i-do-this-for-java"></a>¿Cómo se puede hacer para Java?
Hola de uso [adaptadores de registro de Java](app-insights-java-trace-logs.md).

### <a name="theres-no-application-insights-option-on-hello-project-context-menu"></a>No hay ninguna opción de Application Insights en el menú contextual del proyecto Hola
* Compruebe si las herramientas de Application Insights están instaladas en este equipo de desarrollo. En el menú Herramientas de Visual Studio, en Extensiones y actualizaciones, busque Herramientas de Application Insights. Si no se encuentra en la ficha de hello instalado, abra hello en línea pestaña e instálelo.
* Podría tratarse de un tipo de proyecto no admitido por las herramientas de Application Insights. Use la [instalación manual](#manual-installation).

### <a name="no-log-adapter-option-in-hello-configuration-tool"></a>Ninguna opción de adaptador de registro en la herramienta de configuración de Hola
* En primer lugar debe marco de registro de hello tooinstall.
* Si usa System.Diagnostics.Trace, asegúrese de que lo ha [configurado en `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).
* ¿Tengo versión más reciente de Hola de Application Insights? En Visual Studio **herramientas** menú, elija **extensiones y actualizaciones**, abra hello y **actualizaciones** ficha. Si hay herramientas de análisis de desarrollador, haga clic en tooupdate se.

### <a name="emptykey"></a>Aparece el mensaje de error "La clave de instrumentación no puede estar vacía".
Parece que instaló Hola registro paquete Nuget de adaptador sin tener que instalar Application Insights.

En el Explorador de soluciones, haga clic con el botón derecho en `ApplicationInsights.config` y elija **Actualizar Application Insights**. Obtendrá un cuadro de diálogo que le invita toosign en tooAzure y cree un recurso de Application Insights, o volver a utilizar uno existente. Esto debería solucionarlo.

### <a name="i-can-see-traces-in-diagnostic-search-but-not-hello-other-events"></a>Puedo ver seguimientos en la búsqueda de diagnóstico, pero no Hola otros eventos
A veces puede tardar unos instantes para todos los tooget Hola de eventos y las solicitudes a través de la canalización de Hola.

### <a name="limits"></a>¿Qué cantidad de datos se conserva?
Varios factores afectan a cantidad Hola de los datos almacenados. Vea hello [límites](app-insights-api-custom-events-metrics.md#limits) sección de página de las métricas de eventos de cliente de Hola para obtener más información. 

### <a name="im-not-seeing-some-of-hello-log-entries-that-i-expect"></a>No veo algunas entradas del registro de hello que espero
Si la aplicación envía una gran cantidad de datos y utilizas Hola Application Insights SDK para ASP.NET versión 2.0.0-beta3 o posterior, característica de muestreo adaptativo de hello puede operar y enviar solamente un porcentaje de la telemetría. [Aprenda más sobre el muestreo.](app-insights-sampling.md)

## <a name="add"></a>Pasos siguientes
* [Configuración de pruebas de disponibilidad y de capacidad de respuesta][availability]
* [Solución de problemas][qna]

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
