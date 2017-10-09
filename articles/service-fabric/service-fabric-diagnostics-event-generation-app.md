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
# <a name="application-and-service-level-event-and-log-generation"></a><span data-ttu-id="01280-103">Generación de eventos y registros de nivel de aplicación y servicio</span><span class="sxs-lookup"><span data-stu-id="01280-103">Application and service level event and log generation</span></span>

## <a name="instrumenting-hello-code-with-custom-events"></a><span data-ttu-id="01280-104">Instrumentación de código de hello con eventos personalizados</span><span class="sxs-lookup"><span data-stu-id="01280-104">Instrumenting hello code with custom events</span></span>

<span data-ttu-id="01280-105">Instrumentación de código de hello es la base de hello para la mayoría de los demás aspectos de la supervisión de los servicios.</span><span class="sxs-lookup"><span data-stu-id="01280-105">Instrumenting hello code is hello basis for most other aspects of monitoring your services.</span></span> <span data-ttu-id="01280-106">La instrumentación es una única manera de hello que puede saber que algo no funciona correctamente y toodiagnose lo que debe toobe fijo.</span><span class="sxs-lookup"><span data-stu-id="01280-106">Instrumentation is hello only way you can know that something is wrong, and toodiagnose what needs toobe fixed.</span></span> <span data-ttu-id="01280-107">Aunque es técnicamente posible tooconnect depurador tooa producción es aquel, no es una práctica común.</span><span class="sxs-lookup"><span data-stu-id="01280-107">Although technically it's possible tooconnect a debugger tooa production service, it's not a common practice.</span></span> <span data-ttu-id="01280-108">Por lo tanto, es importante disponer de datos de instrumentación detallados.</span><span class="sxs-lookup"><span data-stu-id="01280-108">So, having detailed instrumentation data is important.</span></span>

<span data-ttu-id="01280-109">Algunos productos instrumentan el código automáticamente.</span><span class="sxs-lookup"><span data-stu-id="01280-109">Some products automatically instrument your code.</span></span> <span data-ttu-id="01280-110">Aunque estas soluciones pueden funcionar bien, casi siempre se necesita instrumentación manual.</span><span class="sxs-lookup"><span data-stu-id="01280-110">Although these solutions can work well, manual instrumentation is almost always required.</span></span> <span data-ttu-id="01280-111">Final de hello, debe tener suficiente información tooforensically depurar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="01280-111">In hello end, you must have enough information tooforensically debug hello application.</span></span> <span data-ttu-id="01280-112">Este documento describen diferentes enfoques tooinstrumenting el código, y cuando se enfocan toochoose uno frente a otro.</span><span class="sxs-lookup"><span data-stu-id="01280-112">This document describes different approaches tooinstrumenting your code, and when toochoose one approach over another.</span></span>

## <a name="eventsource"></a><span data-ttu-id="01280-113">EventSource</span><span class="sxs-lookup"><span data-stu-id="01280-113">EventSource</span></span>
<span data-ttu-id="01280-114">Cuando se crea una solución de Service Fabric a partir de una plantilla en Visual Studio, se genera una clase derivada de **EventSource** (**ServiceEventSource** o **ActorEventSource**).</span><span class="sxs-lookup"><span data-stu-id="01280-114">When you create a Service Fabric solution from a template in Visual Studio, an **EventSource**-derived class (**ServiceEventSource** or **ActorEventSource**) is generated.</span></span> <span data-ttu-id="01280-115">Se crea una plantilla en la que podrá agregar eventos para la aplicación o el servicio.</span><span class="sxs-lookup"><span data-stu-id="01280-115">A template is created, in which you can add events for your application or service.</span></span> <span data-ttu-id="01280-116">Hola **EventSource** nombre **debe** ser único y debe cambiarse el nombre de cadena de plantilla predeterminado de hello MyCompany -&lt;solución&gt; - &lt; proyecto&gt;.</span><span class="sxs-lookup"><span data-stu-id="01280-116">hello **EventSource** name **must** be unique, and should be renamed from hello default template string MyCompany-&lt;solution&gt;-&lt;project&gt;.</span></span> <span data-ttu-id="01280-117">Con varias **EventSource** definiciones que usan Hola mismo causas de nombre un problema en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="01280-117">Having multiple **EventSource** definitions that use hello same name causes an issue at run time.</span></span> <span data-ttu-id="01280-118">Cada evento definido debe tener un identificador único.</span><span class="sxs-lookup"><span data-stu-id="01280-118">Each defined event must have a unique identifier.</span></span> <span data-ttu-id="01280-119">Si el identificador no es único, se produce un error en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="01280-119">If an identifier is not unique, a runtime failure occurs.</span></span> <span data-ttu-id="01280-120">Algunas organizaciones asignar previamente los intervalos de valores para los conflictos de identificadores tooavoid entre los equipos de desarrollo independiente.</span><span class="sxs-lookup"><span data-stu-id="01280-120">Some organizations preassign ranges of values for identifiers tooavoid conflicts between separate development teams.</span></span> <span data-ttu-id="01280-121">Para obtener más información, consulte [blog de Vance](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) o hello [la documentación de MSDN](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span><span class="sxs-lookup"><span data-stu-id="01280-121">For more information, see [Vance's blog](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) or hello [MSDN documentation](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span></span>

### <a name="using-structured-eventsource-events"></a><span data-ttu-id="01280-122">Uso de eventos EventSource estructurados</span><span class="sxs-lookup"><span data-stu-id="01280-122">Using structured EventSource events</span></span>

<span data-ttu-id="01280-123">Cada uno de los eventos de hello en los ejemplos de código de hello en esta sección se definen para un caso concreto, por ejemplo, cuando se registra un tipo de servicio.</span><span class="sxs-lookup"><span data-stu-id="01280-123">Each of hello events in hello code examples in this section are defined for a specific case, for example, when a service type is registered.</span></span> <span data-ttu-id="01280-124">Al definir mensajes por caso de uso, datos que se pueden empaquetar con texto hello de error de Hola y puede más fácil buscar y filtro basado en los nombres de Hola o valores de hello las propiedades especificadas.</span><span class="sxs-lookup"><span data-stu-id="01280-124">When you define messages by use case, data can be packaged with hello text of hello error, and you can more easily search and filter based on hello names or values of hello specified properties.</span></span> <span data-ttu-id="01280-125">Estructurar la salida de la instrumentación de hello resulta más fácil tooconsume, pero requiere más la reflexión y una hora toodefine un nuevo evento en cada caso de uso.</span><span class="sxs-lookup"><span data-stu-id="01280-125">Structuring hello instrumentation output makes it easier tooconsume, but requires more thought and time toodefine a new event for each use case.</span></span> <span data-ttu-id="01280-126">Algunas definiciones de eventos se pueden compartir en toda la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="01280-126">Some event definitions can be shared across hello entire application.</span></span> <span data-ttu-id="01280-127">Por ejemplo, el evento de inicio o detención de un método se podría reutilizar en muchos servicios de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="01280-127">For example, a method start or stop event would be reused across many services within an application.</span></span> <span data-ttu-id="01280-128">Un servicio específico de dominio, como un sistema de pedidos, puede tener un evento **CreateOrder** con su propio evento único.</span><span class="sxs-lookup"><span data-stu-id="01280-128">A domain-specific service, like an order system, might have a **CreateOrder** event, which has its own unique event.</span></span> <span data-ttu-id="01280-129">Este enfoque genera a menudo una gran cantidad de eventos y puede necesitar la coordinación de los identificadores entre los equipos de proyecto.</span><span class="sxs-lookup"><span data-stu-id="01280-129">This approach might generate many events, and potentially require coordination of identifiers across project teams.</span></span> 

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

### <a name="using-eventsource-generically"></a><span data-ttu-id="01280-130">Uso de EventSource genéricamente</span><span class="sxs-lookup"><span data-stu-id="01280-130">Using EventSource generically</span></span>

<span data-ttu-id="01280-131">Dado que la definición de eventos específicos puede resultar difícil, muchas personas definen algunos con un conjunto común de parámetros que por lo general generan la información saliente como cadena.</span><span class="sxs-lookup"><span data-stu-id="01280-131">Because defining specific events can be difficult, many people define a few events with a common set of parameters that generally output their information as a string.</span></span> <span data-ttu-id="01280-132">Gran parte del aspecto de hello estructurado se pierde y es más difícil de resultados de hello toosearch y filtro.</span><span class="sxs-lookup"><span data-stu-id="01280-132">Much of hello structured aspect is lost, and it's more difficult toosearch and filter hello results.</span></span> <span data-ttu-id="01280-133">En este enfoque, se definen algunos de los eventos que normalmente se corresponden los niveles de registro de toohello.</span><span class="sxs-lookup"><span data-stu-id="01280-133">In this approach, a few events that usually correspond toohello logging levels are defined.</span></span> <span data-ttu-id="01280-134">Hola siguiente fragmento de código define un mensaje de error y de depuración:</span><span class="sxs-lookup"><span data-stu-id="01280-134">hello following snippet defines a debug and error message:</span></span>

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

<span data-ttu-id="01280-135">El uso de instrumentación híbrida (estructurada y genérica) también puede funcionar.</span><span class="sxs-lookup"><span data-stu-id="01280-135">Using a hybrid of structured and generic instrumentation also can work well.</span></span> <span data-ttu-id="01280-136">La instrumentación estructurada se usa para informar sobre errores y métricas.</span><span class="sxs-lookup"><span data-stu-id="01280-136">Structured instrumentation is used for reporting errors and metrics.</span></span> <span data-ttu-id="01280-137">Eventos genéricos pueden usarse para hello detallada registro que es utilizado por los ingenieros para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="01280-137">Generic events can be used for hello detailed logging that is consumed by engineers for troubleshooting.</span></span>

## <a name="aspnet-core-logging"></a><span data-ttu-id="01280-138">Registro de ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="01280-138">ASP.NET Core logging</span></span>

<span data-ttu-id="01280-139">Su toocarefully importante planear cómo se instrumentar el código.</span><span class="sxs-lookup"><span data-stu-id="01280-139">It's important toocarefully plan how you will instrument your code.</span></span> <span data-ttu-id="01280-140">plan de Hello Instrumental derecho puede ayudarle a evitar potencialmente desestabilizar el código base y, a continuación, necesidad de código de hello tooreinstrument.</span><span class="sxs-lookup"><span data-stu-id="01280-140">hello right instrumentation plan can help you avoid potentially destabilizing your code base, and then needing tooreinstrument hello code.</span></span> <span data-ttu-id="01280-141">tooreduce riesgo, puede elegir una biblioteca de instrumentación como [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), que forma parte de Microsoft ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="01280-141">tooreduce risk, you can choose an instrumentation library like [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), which is part of Microsoft ASP.NET Core.</span></span> <span data-ttu-id="01280-142">ASP.NET Core tiene un [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interfaz que puede usar con el proveedor de Hola de su elección, y reduce su efecto de hello en código existente.</span><span class="sxs-lookup"><span data-stu-id="01280-142">ASP.NET Core has an [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface that you can use with hello provider of your choice, while minimizing hello effect on existing code.</span></span> <span data-ttu-id="01280-143">Puede utilizar el código de hello en ASP.NET Core en Windows y Linux y Hola completa de .NET Framework, por lo que el código de instrumentación está normalizado.</span><span class="sxs-lookup"><span data-stu-id="01280-143">You can use hello code in ASP.NET Core on Windows and Linux, and in hello full .NET Framework, so your instrumentation code is standardized.</span></span> <span data-ttu-id="01280-144">Esto se trata con más detalle a continuación:</span><span class="sxs-lookup"><span data-stu-id="01280-144">This is further explored below:</span></span>

### <a name="using-microsoftextensionslogging-in-service-fabric"></a><span data-ttu-id="01280-145">Uso de Microsoft.Extensions.Logging en Service Fabric</span><span class="sxs-lookup"><span data-stu-id="01280-145">Using Microsoft.Extensions.Logging in Service Fabric</span></span>

1. <span data-ttu-id="01280-146">Agregar hello Microsoft.Extensions.Logging NuGet paquete toohello proyecto desea tooinstrument.</span><span class="sxs-lookup"><span data-stu-id="01280-146">Add hello Microsoft.Extensions.Logging NuGet package toohello project you want tooinstrument.</span></span> <span data-ttu-id="01280-147">Además, agregue los paquetes de proveedor (para un paquete de aplicaciones de terceros, vea el siguiente ejemplo de Hola).</span><span class="sxs-lookup"><span data-stu-id="01280-147">Also, add any provider packages (for a third-party package, see hello following example).</span></span> <span data-ttu-id="01280-148">Consulte el artículo sobre el [registro de ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging) para más información.</span><span class="sxs-lookup"><span data-stu-id="01280-148">For more information, see [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span></span>
2. <span data-ttu-id="01280-149">Agregar un **con** la directiva para el archivo de servicio de Microsoft.Extensions.Logging tooyour.</span><span class="sxs-lookup"><span data-stu-id="01280-149">Add a **using** directive for Microsoft.Extensions.Logging tooyour service file.</span></span>
3. <span data-ttu-id="01280-150">Defina una variable privada dentro de la clase de servicio.</span><span class="sxs-lookup"><span data-stu-id="01280-150">Define a private variable within your service class.</span></span>

  ```csharp
  private ILogger _logger = null;

  ```
4. <span data-ttu-id="01280-151">En el constructor de saludo de la clase de servicio, agregue este código:</span><span class="sxs-lookup"><span data-stu-id="01280-151">In hello constructor of your service class, add this code:</span></span>

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. <span data-ttu-id="01280-152">Inicie la instrumentación del código en los métodos.</span><span class="sxs-lookup"><span data-stu-id="01280-152">Start instrumenting your code in your methods.</span></span> <span data-ttu-id="01280-153">Estos son algunos ejemplos:</span><span class="sxs-lookup"><span data-stu-id="01280-153">Here are a few samples:</span></span>

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and hello duration of hello request.
  // Later in hello article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a><span data-ttu-id="01280-154">Uso de otros proveedores de registro</span><span class="sxs-lookup"><span data-stu-id="01280-154">Using other logging providers</span></span>

<span data-ttu-id="01280-155">Algunos proveedores de terceros utilizan enfoque de hello descrito en hello anterior sección, incluidos los [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), y [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span><span class="sxs-lookup"><span data-stu-id="01280-155">Some third-party providers use hello approach described in hello preceding section, including [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), and [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span></span> <span data-ttu-id="01280-156">Puede conectarlos al registro de ASP.NET Core o utilizarlos por separado.</span><span class="sxs-lookup"><span data-stu-id="01280-156">You can plug each of these into ASP.NET Core logging, or you can use them separately.</span></span> <span data-ttu-id="01280-157">Serilog tiene una característica que enriquece todos los mensajes enviados desde un registrador.</span><span class="sxs-lookup"><span data-stu-id="01280-157">Serilog has a feature that enriches all messages sent from a logger.</span></span> <span data-ttu-id="01280-158">Esta característica puede ser el nombre del servicio de toooutput útil hello, tipo e información de la partición.</span><span class="sxs-lookup"><span data-stu-id="01280-158">This feature can be useful toooutput hello service name, type, and partition information.</span></span> <span data-ttu-id="01280-159">toouse esta capacidad en hello infraestructura básica de ASP.NET, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="01280-159">toouse this capability in hello ASP.NET Core infrastructure, do these steps:</span></span>

1. <span data-ttu-id="01280-160">Agregue hello Serilog, Serilog.Extensions.Logging, y paquetes de Serilog.Sinks.Observable NuGet toohello proyecto.</span><span class="sxs-lookup"><span data-stu-id="01280-160">Add hello Serilog, Serilog.Extensions.Logging, and Serilog.Sinks.Observable NuGet packages toohello project.</span></span> <span data-ttu-id="01280-161">En el siguiente ejemplo de Hola, agregar Serilog.Sinks.Literate.</span><span class="sxs-lookup"><span data-stu-id="01280-161">For hello next example, also add Serilog.Sinks.Literate.</span></span> <span data-ttu-id="01280-162">Más adelante en este artículo se muestra un mejor enfoque.</span><span class="sxs-lookup"><span data-stu-id="01280-162">A better approach is shown later in this article.</span></span>
2. <span data-ttu-id="01280-163">En Serilog, cree una instancia del registrador hello y LoggerConfiguration.</span><span class="sxs-lookup"><span data-stu-id="01280-163">In Serilog, create a LoggerConfiguration and hello logger instance.</span></span>

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. <span data-ttu-id="01280-164">Agregue un constructor de servicio de Serilog.ILogger argumento toohello y pasar Hola recién creado registrador.</span><span class="sxs-lookup"><span data-stu-id="01280-164">Add a Serilog.ILogger argument toohello service constructor, and pass hello newly created logger.</span></span>

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. <span data-ttu-id="01280-165">En el constructor del servicio de hello, agregar Hola después de código, que crea hello enrichers de propiedad para hello **ServiceTypeName**, **ServiceName**, **PartitionId**y  **InstanceId** propiedades del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="01280-165">In hello service constructor, add hello following code, which creates hello property enrichers for hello **ServiceTypeName**, **ServiceName**, **PartitionId**, and **InstanceId** properties of hello service.</span></span> <span data-ttu-id="01280-166">También agrega un toohello de enricher propiedad generador de registro de ASP.NET Core, por lo que puede usar Microsoft.Extensions.Logging.ILogger en el código.</span><span class="sxs-lookup"><span data-stu-id="01280-166">It also adds a property enricher toohello ASP.NET Core logging factory, so you can use Microsoft.Extensions.Logging.ILogger in your code.</span></span>

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

5. <span data-ttu-id="01280-167">Código de hello instrumento Hola mismo como si estuviera utilizando ASP.NET Core sin Serilog.</span><span class="sxs-lookup"><span data-stu-id="01280-167">Instrument hello code hello same as if you were using ASP.NET Core without Serilog.</span></span>

  >[!NOTE]
  ><span data-ttu-id="01280-168">Se recomienda que no use Hola estático Log.Logger con el anterior ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="01280-168">We recommend that you don't use hello static Log.Logger with hello preceding example.</span></span> <span data-ttu-id="01280-169">Tejido de servicio puede alojar varias instancias de hello del mismo servicio tipo dentro de un único proceso.</span><span class="sxs-lookup"><span data-stu-id="01280-169">Service Fabric can host multiple instances of hello same service type within a single process.</span></span> <span data-ttu-id="01280-170">Si usas Hola Log.Logger estático, último writer de Hola de enrichers de propiedad Hola mostrará los valores para todas las instancias que se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="01280-170">If you use hello static Log.Logger, hello last writer of hello property enrichers will show values for all instances that are running.</span></span> <span data-ttu-id="01280-171">Se trata de una de las razones por qué variable de hello _logger es una variable de miembro privado de la clase de servicio de hello.</span><span class="sxs-lookup"><span data-stu-id="01280-171">This is one reason why hello _logger variable is a private member variable of hello service class.</span></span> <span data-ttu-id="01280-172">Además, debe realizar el código de hello _logger toocommon disponibles, lo que podría utilizarse a través de servicios.</span><span class="sxs-lookup"><span data-stu-id="01280-172">Also, you must make hello _logger available toocommon code, which might be used across services.</span></span>

## <a name="choosing-a-logging-provider"></a><span data-ttu-id="01280-173">Elección de un proveedor de registro</span><span class="sxs-lookup"><span data-stu-id="01280-173">Choosing a logging provider</span></span>

<span data-ttu-id="01280-174">Si la aplicación depende del alto rendimiento, **EventSource** suele ser el mejor enfoque.</span><span class="sxs-lookup"><span data-stu-id="01280-174">If your application relies on high performance, **EventSource** is usually a good approach.</span></span> <span data-ttu-id="01280-175">**EventSource** *generalmente* utiliza menos recursos y proporciona mejor rendimiento que el registro de ASP.NET Core o cualquiera de las soluciones de terceros disponibles Hola.</span><span class="sxs-lookup"><span data-stu-id="01280-175">**EventSource** *generally* uses fewer resources and performs better than ASP.NET Core logging or any of hello available third-party solutions.</span></span>  <span data-ttu-id="01280-176">Esto no supone un problema para muchos servicios, pero si está orientado al rendimiento, **EventSource** sería una opción mejor.</span><span class="sxs-lookup"><span data-stu-id="01280-176">This isn't an issue for many services, but if your service is performance-oriented, using **EventSource** might be a better choice.</span></span> <span data-ttu-id="01280-177">Sin embargo, tooget en que estas ventajas de estructura de registro, **EventSource** requiere una mayor inversión desde el equipo de ingeniería.</span><span class="sxs-lookup"><span data-stu-id="01280-177">However, tooget these benefits of structured logging, **EventSource** requires a larger investment from your engineering team.</span></span> <span data-ttu-id="01280-178">Si es posible, no un prototipo rápido de algunas opciones de registro y, a continuación, elija Hola que mejor se adapte a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="01280-178">If possible, do a quick prototype of a few logging options, and then choose hello one that best meets your needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01280-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="01280-179">Next steps</span></span>

<span data-ttu-id="01280-180">Una vez haya elegido la tooinstrument de proveedor de registro de las aplicaciones y servicios, los registros y eventos necesitan toobe agrega antes de que se puede enviar tooany plataforma de análisis.</span><span class="sxs-lookup"><span data-stu-id="01280-180">Once you have chosen your logging provider tooinstrument your applications and services, your logs and events need toobe aggregated before they can be sent tooany analysis platform.</span></span> <span data-ttu-id="01280-181">Obtenga información sobre [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) y [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter comprender algunas de hello opciones recomendada.</span><span class="sxs-lookup"><span data-stu-id="01280-181">Read about [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) and [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter understand some of hello recommended options.</span></span>
