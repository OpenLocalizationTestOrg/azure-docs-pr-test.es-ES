---
title: "aaaAzure nivel de supervisión de aplicaciones de tejido de servicio | Documentos de Microsoft"
description: "Obtenga información acerca de la aplicación y registros de eventos de nivel de servicio utilizan toomonitor y diagnosticar clústeres Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 4f4da1eaad4b88428eaa3a2100ac25c8a285a727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-level-event-and-log-generation"></a>Generación de eventos y registros de nivel de aplicación y servicio

## <a name="instrumenting-hello-code-with-custom-events"></a>Instrumentación de código de hello con eventos personalizados

Instrumentación de código de hello es la base de hello para la mayoría de los demás aspectos de la supervisión de los servicios. La instrumentación es una única manera de hello que puede saber que algo no funciona correctamente y toodiagnose lo que debe toobe fijo. Aunque es técnicamente posible tooconnect depurador tooa producción es aquel, no es una práctica común. Por lo tanto, es importante disponer de datos de instrumentación detallados.

Algunos productos instrumentan el código automáticamente. Aunque estas soluciones pueden funcionar bien, casi siempre se necesita instrumentación manual. Final de hello, debe tener suficiente información tooforensically depurar la aplicación hello. Este documento describen diferentes enfoques tooinstrumenting el código, y cuando se enfocan toochoose uno frente a otro.

## <a name="eventsource"></a>EventSource
Cuando se crea una solución de Service Fabric a partir de una plantilla en Visual Studio, se genera una clase derivada de **EventSource** (**ServiceEventSource** o **ActorEventSource**). Se crea una plantilla en la que podrá agregar eventos para la aplicación o el servicio. Hola **EventSource** nombre **debe** ser único y debe cambiarse el nombre de cadena de plantilla predeterminado de hello MyCompany -&lt;solución&gt; - &lt; proyecto&gt;. Con varias **EventSource** definiciones que usan Hola mismo causas de nombre un problema en tiempo de ejecución. Cada evento definido debe tener un identificador único. Si el identificador no es único, se produce un error en tiempo de ejecución. Algunas organizaciones asignar previamente los intervalos de valores para los conflictos de identificadores tooavoid entre los equipos de desarrollo independiente. Para obtener más información, consulte [blog de Vance](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) o hello [la documentación de MSDN](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).

### <a name="using-structured-eventsource-events"></a>Uso de eventos EventSource estructurados

Cada uno de los eventos de hello en los ejemplos de código de hello en esta sección se definen para un caso concreto, por ejemplo, cuando se registra un tipo de servicio. Al definir mensajes por caso de uso, datos que se pueden empaquetar con texto hello de error de Hola y puede más fácil buscar y filtro basado en los nombres de Hola o valores de hello las propiedades especificadas. Estructurar la salida de la instrumentación de hello resulta más fácil tooconsume, pero requiere más la reflexión y una hora toodefine un nuevo evento en cada caso de uso. Algunas definiciones de eventos se pueden compartir en toda la aplicación hello. Por ejemplo, el evento de inicio o detención de un método se podría reutilizar en muchos servicios de una aplicación. Un servicio específico de dominio, como un sistema de pedidos, puede tener un evento **CreateOrder** con su propio evento único. Este enfoque genera a menudo una gran cantidad de eventos y puede necesitar la coordinación de los identificadores entre los equipos de proyecto. 

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello instance constructor is private tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        // hello ServiceTypeRegistered event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceTypeRegisteredEventId = 3;
        [Event(ServiceTypeRegisteredEventId, Level = EventLevel.Informational, Message = "Service host process {0} registered service type {1}", Keywords = Keywords.ServiceInitialization)]
        public void ServiceTypeRegistered(int hostProcessId, string serviceType)
        {
            WriteEvent(ServiceTypeRegisteredEventId, hostProcessId, serviceType);
        }

        // hello ServiceHostInitializationFailed event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceHostInitializationFailedEventId = 4;
        [Event(ServiceHostInitializationFailedEventId, Level = EventLevel.Error, Message = "Service host initialization failed", Keywords = Keywords.ServiceInitialization)]
        public void ServiceHostInitializationFailed(string exception)
        {
            WriteEvent(ServiceHostInitializationFailedEventId, exception);
        }
```

### <a name="using-eventsource-generically"></a>Uso de EventSource genéricamente

Dado que la definición de eventos específicos puede resultar difícil, muchas personas definen algunos con un conjunto común de parámetros que por lo general generan la información saliente como cadena. Gran parte del aspecto de hello estructurado se pierde y es más difícil de resultados de hello toosearch y filtro. En este enfoque, se definen algunos de los eventos que normalmente se corresponden los niveles de registro de toohello. Hola siguiente fragmento de código define un mensaje de error y de depuración:

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello Instance constructor is private, tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        private const int DebugEventId = 10;
        [Event(DebugEventId, Level = EventLevel.Verbose, Message = "{0}")]
        public void Debug(string msg)
        {
            WriteEvent(DebugEventId, msg);
        }

        private const int ErrorEventId = 11;
        [Event(ErrorEventId, Level = EventLevel.Error, Message = "Error: {0} - {1}")]
        public void Error(string error, string msg)
        {
            WriteEvent(ErrorEventId, error, msg);
        }
```

El uso de instrumentación híbrida (estructurada y genérica) también puede funcionar. La instrumentación estructurada se usa para informar sobre errores y métricas. Eventos genéricos pueden usarse para hello detallada registro que es utilizado por los ingenieros para solucionar el problema.

## <a name="aspnet-core-logging"></a>Registro de ASP.NET Core

Su toocarefully importante planear cómo se instrumentar el código. plan de Hello Instrumental derecho puede ayudarle a evitar potencialmente desestabilizar el código base y, a continuación, necesidad de código de hello tooreinstrument. tooreduce riesgo, puede elegir una biblioteca de instrumentación como [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), que forma parte de Microsoft ASP.NET Core. ASP.NET Core tiene un [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interfaz que puede usar con el proveedor de Hola de su elección, y reduce su efecto de hello en código existente. Puede utilizar el código de hello en ASP.NET Core en Windows y Linux y Hola completa de .NET Framework, por lo que el código de instrumentación está normalizado. Esto se trata con más detalle a continuación:

### <a name="using-microsoftextensionslogging-in-service-fabric"></a>Uso de Microsoft.Extensions.Logging en Service Fabric

1. Agregar hello Microsoft.Extensions.Logging NuGet paquete toohello proyecto desea tooinstrument. Además, agregue los paquetes de proveedor (para un paquete de aplicaciones de terceros, vea el siguiente ejemplo de Hola). Consulte el artículo sobre el [registro de ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging) para más información.
2. Agregar un **con** la directiva para el archivo de servicio de Microsoft.Extensions.Logging tooyour.
3. Defina una variable privada dentro de la clase de servicio.

  ```csharp
  private ILogger _logger = null;

  ```
4. En el constructor de saludo de la clase de servicio, agregue este código:

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. Inicie la instrumentación del código en los métodos. Estos son algunos ejemplos:

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and hello duration of hello request.
  // Later in hello article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a>Uso de otros proveedores de registro

Algunos proveedores de terceros utilizan enfoque de hello descrito en hello anterior sección, incluidos los [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), y [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging). Puede conectarlos al registro de ASP.NET Core o utilizarlos por separado. Serilog tiene una característica que enriquece todos los mensajes enviados desde un registrador. Esta característica puede ser el nombre del servicio de toooutput útil hello, tipo e información de la partición. toouse esta capacidad en hello infraestructura básica de ASP.NET, siga estos pasos:

1. Agregue hello Serilog, Serilog.Extensions.Logging, y paquetes de Serilog.Sinks.Observable NuGet toohello proyecto. En el siguiente ejemplo de Hola, agregar Serilog.Sinks.Literate. Más adelante en este artículo se muestra un mejor enfoque.
2. En Serilog, cree una instancia del registrador hello y LoggerConfiguration.

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. Agregue un constructor de servicio de Serilog.ILogger argumento toohello y pasar Hola recién creado registrador.

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. En el constructor del servicio de hello, agregar Hola después de código, que crea hello enrichers de propiedad para hello **ServiceTypeName**, **ServiceName**, **PartitionId**y  **InstanceId** propiedades del servicio de Hola. También agrega un toohello de enricher propiedad generador de registro de ASP.NET Core, por lo que puede usar Microsoft.Extensions.Logging.ILogger en el código.

  ```csharp
  public Stateless(StatelessServiceContext context, Serilog.ILogger serilog)
      : base(context)
  {
      PropertyEnricher[] properties = new PropertyEnricher[]
      {
          new PropertyEnricher("ServiceTypeName", context.ServiceTypeName),
          new PropertyEnricher("ServiceName", context.ServiceName),
          new PropertyEnricher("PartitionId", context.PartitionId),
          new PropertyEnricher("InstanceId", context.ReplicaOrInstanceId),
      };

      serilog.ForContext(properties);

      _logger = new LoggerFactory().AddSerilog(serilog.ForContext(properties)).CreateLogger<Stateless>();
  }
  ```

5. Código de hello instrumento Hola mismo como si estuviera utilizando ASP.NET Core sin Serilog.

  >[!NOTE]
  >Se recomienda que no use Hola estático Log.Logger con el anterior ejemplo de Hola. Tejido de servicio puede alojar varias instancias de hello del mismo servicio tipo dentro de un único proceso. Si usas Hola Log.Logger estático, último writer de Hola de enrichers de propiedad Hola mostrará los valores para todas las instancias que se ejecutan. Se trata de una de las razones por qué variable de hello _logger es una variable de miembro privado de la clase de servicio de hello. Además, debe realizar el código de hello _logger toocommon disponibles, lo que podría utilizarse a través de servicios.

## <a name="choosing-a-logging-provider"></a>Elección de un proveedor de registro

Si la aplicación depende del alto rendimiento, **EventSource** suele ser el mejor enfoque. **EventSource** *generalmente* utiliza menos recursos y proporciona mejor rendimiento que el registro de ASP.NET Core o cualquiera de las soluciones de terceros disponibles Hola.  Esto no supone un problema para muchos servicios, pero si está orientado al rendimiento, **EventSource** sería una opción mejor. Sin embargo, tooget en que estas ventajas de estructura de registro, **EventSource** requiere una mayor inversión desde el equipo de ingeniería. Si es posible, no un prototipo rápido de algunas opciones de registro y, a continuación, elija Hola que mejor se adapte a sus necesidades.

## <a name="next-steps"></a>Pasos siguientes

Una vez haya elegido la tooinstrument de proveedor de registro de las aplicaciones y servicios, los registros y eventos necesitan toobe agrega antes de que se puede enviar tooany plataforma de análisis. Obtenga información sobre [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) y [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter comprender algunas de hello opciones recomendada.
