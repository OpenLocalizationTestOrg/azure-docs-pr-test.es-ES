---
title: referencia de aaaApplicationInsights.config - Azure | Documentos de Microsoft
description: "Habilitación o deshabilitación de los módulos de recopilación de datos e incorporación de contadores de rendimiento y otros parámetros."
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
editor: alancameronwills
manager: carmonm
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 76cb11349d87dfc508ec8b1c454259a0b079c48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-hello-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a>Configurar Hola Application Insights SDK con ApplicationInsights.config o .xml
Hola Application Insights .NET SDK está formado por un número de paquetes de NuGet. El [paquete core](http://www.nuget.org/packages/Microsoft.ApplicationInsights) proporciona API de Hola para enviar telemetría a saludos Application Insights. Los [paquetes adicionales](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) proporcionan *módulos* e *inicializadores* de telemetría para hacer un seguimiento automático de la aplicación y su contexto. Ajustando el archivo de configuración de hello, puede habilitar o deshabilitar inicializadores y módulos de telemetría y establecer los parámetros para algunos de ellos.

se denomina archivo de configuración de Hello `ApplicationInsights.config` o `ApplicationInsights.xml`, según el tipo de saludo de la aplicación. Se agrega automáticamente tooyour proyecto cuando se [instalar la mayoría de las versiones de SDK de hello][start]. También se agrega tooa aplicación web [Monitor de estado en un servidor IIS][redfield], o cuando se selecciona la visión de la aplicación de hello [extensión para un sitio Web de Azure o la máquina virtual](app-insights-azure-web-apps.md).

No hay un Hola de toocontrol archivo equivalente [SDK en una página web][client].

Este documento describe secciones Hola que verá en la configuración de Hola de archivos, cómo controlan los componentes de Hola de hello SDK, y los paquetes de NuGet cargar esos componentes.

## <a name="telemetry-modules-aspnet"></a>Módulos de telemetría (ASP.NET)
Cada módulo de telemetría recopila un tipo específico de datos y la usa core Hola datos de API toosend Hola. Hola módulos se instalan diferentes paquetes de NuGet, que también agrega el archivo .config de hello líneas requeridas toohello.

Hay un nodo en el archivo de configuración de Hola para cada módulo. toodisable un módulo, eliminar nodo de Hola o márquelo como comentario fuera.

### <a name="dependency-tracking"></a>Seguimiento de dependencia
[Seguimiento de dependencias](app-insights-asp-net-dependencies.md) recopila telemetría acerca de las llamadas que la aplicación realiza toodatabases y servicios externos y las bases de datos. tooallow toowork de este módulo en un servidor IIS, necesita demasiado[instalar el Monitor de estado][redfield]. toouse en aplicaciones web de Azure o máquinas virtuales, [Seleccionar extensión de Application Insights hello](app-insights-azure-web-apps.md).

También puede escribir su propio código utilizando Hola de seguimiento de dependencias [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) .

### <a name="performance-collector"></a>Recopilador de rendimiento
[Recopila contadores de rendimiento del sistema](app-insights-performance-counters.md) como CPU, memoria y carga de la red desde instalaciones de IIS. Puede especificar qué toocollect contadores, incluidos los contadores de rendimiento que se ha configurado manualmente.

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* [Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) .

### <a name="application-insights-diagnostics-telemetry"></a>Telemetría de diagnósticos de Application Insights
Hola `DiagnosticsTelemetryModule` informa de errores en el propio código de instrumentación Application Insights Hola. Por ejemplo, si el código de hello no puede tener acceso a los contadores de rendimiento o un `ITelemetryInitializer` produce una excepción. Realiza un seguimiento por este módulo de telemetría de seguimiento aparece en hello [búsqueda diagnóstico][diagnostic]. Envía datos de diagnóstico toodc.services.vsallin.net.

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* [Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) . Si instala solo este paquete, archivo de hello ApplicationInsights.config no se crea automáticamente.

### <a name="developer-mode"></a>Modo de programador
`DeveloperModeWithDebuggerAttachedTelemetryModule`fuerza Hola Application Insights `TelemetryChannel` toosend datos inmediatamente, elemento de telemetría de uno a la vez, cuando un depurador adjuntarán toohello proceso de la aplicación. Esto reduce la cantidad de Hola de tiempo entre el momento de hello cuando la aplicación realiza un seguimiento de telemetría y cuando aparece en el portal de Application Insights Hola. Esto provoca una sobrecarga considerable en la CPU y el ancho de banda.

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* [Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/)

### <a name="web-request-tracking"></a>Seguimiento de solicitud web
Hola informes [código de tiempo y el resultado de la respuesta](app-insights-asp-net.md) de solicitudes HTTP.

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web)

### <a name="exception-tracking"></a>Seguimiento de excepciones
`ExceptionTrackingTelemetryModule` realiza excepciones no controladas en la aplicación web. Consulte [Errores y excepciones][exceptions].

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web)
* `Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - Realiza un seguimiento de [excepciones de tareas inadvertidas](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).
* `Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - Realiza un seguimiento de excepciones no controladas para roles de trabajo, servicios de Windows y aplicaciones de consola.
* [Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) .

### <a name="eventsource-tracking"></a>Seguimiento de EventSource
`EventSourceTelemetryModule`le permite tooconfigure EventSource eventos toobe enviado tooApplication visión como seguimientos. Para obtener información sobre el seguimiento de eventos EventSource, vea [Uso de eventos EventSource](app-insights-asp-net-trace-logs.md#using-eventsource-events).

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [Microsoft.ApplicationInsights.EventSourceListener](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a>Seguimiento de eventos ETW
`EtwCollectorTelemetryModule`le permite tooconfigure eventos de ETW proveedores toobe enviado tooApplication visión como seguimientos. Para obtener información sobre el seguimiento de eventos ETW de seguimiento, vea [Uso de eventos ETW](app-insights-asp-net-trace-logs.md#using-etw-events).

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [Microsoft.ApplicationInsights.EtwCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a>Microsoft.ApplicationInsights
paquete de Hola a Microsoft.ApplicationInsights proporciona hello [principales API](https://msdn.microsoft.com/library/mt420197.aspx) de hello SDK. Hello otros módulos de telemetría utilizan y también puede [usar toodefine su propio telemetría](app-insights-api-custom-events-metrics.md).

* No hay entrada en ApplicationInsights.config.
* [Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) . Si solamente instala este NuGet, no se genera ningún archivo .config.

## <a name="telemetry-channel"></a>Canal de telemetría
canal de telemetría de Hello administra el almacenamiento en búfer y transmisión de telemetría toohello servicio Application Insights.

* `Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`es el canal de hello predeterminado para los servicios. Almacena en búfer los datos de la memoria.
* `Microsoft.ApplicationInsights.PersistenceChannel` es una alternativa para aplicaciones de consola. Puede guardar cualquier almacenamiento de datos unflushed toopersistent cuando la aplicación cierra y enviará cuando la aplicación hello se inicia de nuevo.

## <a name="telemetry-initializers-aspnet"></a>Inicializadores de telemetría (ASP.NET)
Los inicializadores de telemetría establecen propiedades de contexto que se envían junto con todos los elementos de telemetría.

También puede [escribir sus propios inicializadores](app-insights-api-filtering-sampling.md#add-properties) tooset las propiedades de contexto.

inicializadores de Hello estándar se configuraron todos haciendo hello Web o WindowsServer NuGet paquetes:

* `AccountIdTelemetryInitializer`establece la propiedad de identificador de cuenta de hello.
* `AuthenticatedUserIdTelemetryInitializer`establece hello AuthenticatedUserId propiedad como conjunto Hola SDK de JavaScript.
* `AzureRoleEnvironmentTelemetryInitializer`Hola actualizaciones `RoleName` y `RoleInstance` propiedades de hello `Device` contexto para todos los elementos de telemetría con la información extraída del entorno de Azure en tiempo de ejecución de Hola.
* `BuildInfoConfigComponentVersionTelemetryInitializer`Hola actualizaciones `Version` propiedad de hello `Component` contexto para todos los elementos de telemetría con valor de hello extraído de hello `BuildInfo.config` archivo generado por MS Build.
* `ClientIpHeaderTelemetryInitializer`actualizaciones `Ip` propiedad de hello `Location` según el contexto de todos los elementos de telemetría hello `X-Forwarded-For` encabezado HTTP de solicitud de saludo.
* `DeviceTelemetryInitializer`Hola de las actualizaciones siguientes propiedades de hello `Device` contexto para todos los elementos de telemetría.
  * `Type`se establece demasiado "PC"
  * `Id`se establece toohello nombre de dominio Hola equipo donde se ejecuta la aplicación web de hello.
  * `OemName`está establecido el valor de toohello extraído de hello `Win32_ComputerSystem.Manufacturer` campo mediante WMI.
  * `Model`está establecido el valor de toohello extraído de hello `Win32_ComputerSystem.Model` campo mediante WMI.
  * `NetworkType`está establecido el valor de toohello extraído de hello `NetworkInterface`.
  * `Language`se establece el nombre toohello de hello `CurrentCulture`.
* `DomainNameRoleInstanceTelemetryInitializer`Hola actualizaciones `RoleInstance` propiedad de hello `Device` contexto para todos los elementos de telemetría con el nombre de dominio de hello del equipo de Hola donde se ejecuta la aplicación web de hello.
* `OperationNameTelemetryInitializer`Hola actualizaciones `Name` propiedad de hello `RequestTelemetry` hello y `Name` propiedad de hello `Operation` contexto de todos los elementos de telemetría basado en método hello HTTP, así como nombres de Hola de tooprocess invocado de acción y controlador de MVC de ASP.NET solicitud.
* `OperationIdTelemetryInitializer`o `OperationCorrelationTelemetryInitializer` Hola actualizaciones `Operation.Id` realiza el seguimiento de propiedad de contexto de todos los elementos de telemetría al controlar una solicitud con hello generada automáticamente `RequestTelemetry.Id`.
* `SessionTelemetryInitializer`Hola actualizaciones `Id` propiedad de hello `Session` contexto para todos los elementos de telemetría con valor extraído de hello `ai_session` cookie generados por hello código de instrumentación ApplicationInsights JavaScript ejecuta en el explorador del usuario de Hola.
* `SyntheticTelemetryInitializer`o `SyntheticUserAgentTelemetryInitializer` Hola actualizaciones `User`, `Session` y `Operation` realiza el seguimiento de propiedades de contextos de todos los elementos de telemetría cuando controla una solicitud de una fuente sintética, como una disponibilidad de prueba o bot de motor de búsqueda. De forma predeterminada, [Explorador de métricas](app-insights-metrics-explorer.md) no muestra telemetría sintética.

    Hola `<Filters>` establece la identificación de propiedades de las solicitudes de Hola.
* `UserAgentTelemetryInitializer`Hola actualizaciones `UserAgent` propiedad de hello `User` según el contexto de todos los elementos de telemetría hello `User-Agent` encabezado HTTP de solicitud de Hola.
* `UserTelemetryInitializer`Hola actualizaciones `Id` y `AcquisitionDate` propiedades de `User` contexto para todos los elementos de telemetría con los valores extraídos de hello `ai_user` cookie generada por código de instrumentación de Application Insights JavaScript Hola ejecutando Hola explorador del usuario.
* `WebTestTelemetryInitializer`conjuntos de Hola Id. de usuario, Id. de sesión y propiedades de origen sintético para solicitudes HTTP que vienen de [pruebas de disponibilidad](app-insights-monitor-web-app-availability.md).
  Hola `<Filters>` establece la identificación de propiedades de las solicitudes de Hola.

Para aplicaciones de .NET que se ejecutan en el tejido de servicio, puede incluir hello `Microsoft.ApplicationInsights.ServiceFabric` paquete NuGet. Este paquete incluye un `FabricTelemetryInitializer`, que agrega elementos de tootelemetry de propiedades de Service Fabric. Para obtener más información, vea hello [página de GitHub](https://go.microsoft.com/fwlink/?linkid=848457) acerca de las propiedades de hello agregadas por este paquete de NuGet.

## <a name="telemetry-processors-aspnet"></a>Procesadores de telemetría (ASP.NET)
Pueden filtrar y modificar cada elemento de telemetría justo antes de que se envía desde el portal de hello SDK toohello procesadores de telemetría.

También puede [escribir sus propios procesadores de telemetría](app-insights-api-filtering-sampling.md#filtering).

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a>Procesador de telemetría de muestreo adaptivo (desde 2.0.0-beta3)
Esta opción está habilitada de manera predeterminada. Si la aplicación envía una gran cantidad de datos de telemetría, este procesador quita algunos de ellos.

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

parámetro Hello proporciona destino Hola Hola algoritmo intenta tooachieve. Cada instancia de hello SDK funciona de forma independiente, por lo que si el servidor es un clúster de varios equipos, el volumen real de Hola de telemetría se multiplicará según corresponda.

[Obtenga más información sobre el muestreo](app-insights-sampling.md).

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a>Procesador de telemetría de muestreo de tasa fija (desde 2.0.0-beta1)
También hay un [procesador de telemetría de muestreo](app-insights-api-filtering-sampling.md) estándar (desde 2.0.1):

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a>Parámetros de canal (Java)
Estos parámetros afectan a cómo debe almacenar y vaciar los datos de telemetría de Hola que recopila Hola SDK de Java.

#### <a name="maxtelemetrybuffercapacity"></a>MaxTelemetryBufferCapacity
número de Hola de elementos de telemetría que pueden almacenarse en el almacenamiento en memoria del SDK de Hola. Cuando se alcanza este número, se vacía el búfer de telemetría de hello: es decir, los elementos de telemetría de Hola se envían toohello servidor de Application Insights.

* Mín: 1
* Máx: 1000
* Valor predeterminado: 500

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a>FlushIntervalInSeconds
Determina la frecuencia con hello datos que están almacenados en el almacenamiento en memoria de Hola deberían estar vació (enviado tooApplication visión).

* Mín: 1
* Máx: 300
* Valor predeterminado: 5

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a>MaxTransmissionStorageCapacityInMB
Determina el tamaño máximo de hello en MB que se asigna a un almacenamiento persistente en el disco local de hello toohello. Este almacenamiento se utiliza para almacenar elementos de telemetría que dieron error toobe transmitida toohello Application Insights extremo. Cuando se ha cumplido el tamaño de almacenamiento de hello, se descartarán los nuevos elementos de telemetría.

* Mín: 1
* Máx: 100
* Valor predeterminado: 10

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a>InstrumentationKey
Esto determina los recursos de Application Insights de hello en el que aparecen los datos. Normalmente se crea un recurso independiente, con una clave independiente, para cada una de las aplicaciones.

Si desea tooset Hola clave dinámicamente: por ejemplo, si desea que los resultados de toosend de sus recursos de aplicación toodifferent - puede omitir clave Hola Hola del archivo de configuración y establecer en el código.

clave de hello tooset para todas las instancias de TelemetryClient, incluidos los módulos de telemetría estándar, Establece clave hello en TelemetryConfiguration.Active. Hágalo en un método de inicialización, como global.aspx.cs, en un servicio de ASP.NET:

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

Si su intención es toosend un conjunto específico de recursos distinto de tooa de eventos, puede establecer clave Hola para un TelemetryClient específica:

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

una nueva clave, tooget [crear un nuevo recurso en el portal de Application Insights hello][new].

## <a name="next-steps"></a>Pasos siguientes
[Obtener más información sobre la API de hello][api].

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
