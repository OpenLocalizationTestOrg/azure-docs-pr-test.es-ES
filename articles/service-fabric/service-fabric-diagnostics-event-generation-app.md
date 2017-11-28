---
title: "Supervisión del nivel de aplicación de Azure Service Fabric | Microsoft Docs"
description: "Obtenga información sobre los eventos y los registros de nivel de servicio y aplicación usados para supervisar y diagnosticar los clústeres de Azure Service Fabric."
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
ms.openlocfilehash: 3c472904641108b7383cd0f1416c47460f8de11a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="application-and-service-level-event-and-log-generation"></a><span data-ttu-id="f86da-103">Generación de eventos y registros de nivel de aplicación y servicio</span><span class="sxs-lookup"><span data-stu-id="f86da-103">Application and service level event and log generation</span></span>

## <a name="instrumenting-the-code-with-custom-events"></a><span data-ttu-id="f86da-104">Instrumentación del código con eventos personalizados</span><span class="sxs-lookup"><span data-stu-id="f86da-104">Instrumenting the code with custom events</span></span>

<span data-ttu-id="f86da-105">La instrumentación del código es la base para la mayoría de los demás aspectos de la supervisión de los servicios.</span><span class="sxs-lookup"><span data-stu-id="f86da-105">Instrumenting the code is the basis for most other aspects of monitoring your services.</span></span> <span data-ttu-id="f86da-106">La instrumentación es la única manera de saber que algo no funciona correctamente y diagnosticar lo que debe solucionarse.</span><span class="sxs-lookup"><span data-stu-id="f86da-106">Instrumentation is the only way you can know that something is wrong, and to diagnose what needs to be fixed.</span></span> <span data-ttu-id="f86da-107">Aunque técnicamente es posible que conectar un depurador a un servicio de producción, no es un procedimiento habitual.</span><span class="sxs-lookup"><span data-stu-id="f86da-107">Although technically it's possible to connect a debugger to a production service, it's not a common practice.</span></span> <span data-ttu-id="f86da-108">Por lo tanto, es importante disponer de datos de instrumentación detallados.</span><span class="sxs-lookup"><span data-stu-id="f86da-108">So, having detailed instrumentation data is important.</span></span>

<span data-ttu-id="f86da-109">Algunos productos instrumentan el código automáticamente.</span><span class="sxs-lookup"><span data-stu-id="f86da-109">Some products automatically instrument your code.</span></span> <span data-ttu-id="f86da-110">Aunque estas soluciones pueden funcionar bien, casi siempre se necesita instrumentación manual.</span><span class="sxs-lookup"><span data-stu-id="f86da-110">Although these solutions can work well, manual instrumentation is almost always required.</span></span> <span data-ttu-id="f86da-111">Al final, debe tener suficiente información para depurar desde la aplicación de manera forense.</span><span class="sxs-lookup"><span data-stu-id="f86da-111">In the end, you must have enough information to forensically debug the application.</span></span> <span data-ttu-id="f86da-112">Este documento describe los distintos enfoques para instrumentar el código y se indica cuándo elegir uno u otro.</span><span class="sxs-lookup"><span data-stu-id="f86da-112">This document describes different approaches to instrumenting your code, and when to choose one approach over another.</span></span>

## <a name="eventsource"></a><span data-ttu-id="f86da-113">EventSource</span><span class="sxs-lookup"><span data-stu-id="f86da-113">EventSource</span></span>
<span data-ttu-id="f86da-114">Cuando se crea una solución de Service Fabric a partir de una plantilla en Visual Studio, se genera una clase derivada de **EventSource** (**ServiceEventSource** o **ActorEventSource**).</span><span class="sxs-lookup"><span data-stu-id="f86da-114">When you create a Service Fabric solution from a template in Visual Studio, an **EventSource**-derived class (**ServiceEventSource** or **ActorEventSource**) is generated.</span></span> <span data-ttu-id="f86da-115">Se crea una plantilla en la que podrá agregar eventos para la aplicación o el servicio.</span><span class="sxs-lookup"><span data-stu-id="f86da-115">A template is created, in which you can add events for your application or service.</span></span> <span data-ttu-id="f86da-116">El nombre de **EventSource** **debe** ser único y debe cambiarse a partir de la cadena de plantilla predeterminada de MyCompany-&lt;solución&gt;-&lt;proyecto&gt;.</span><span class="sxs-lookup"><span data-stu-id="f86da-116">The **EventSource** name **must** be unique, and should be renamed from the default template string MyCompany-&lt;solution&gt;-&lt;project&gt;.</span></span> <span data-ttu-id="f86da-117">El hecho de tener varias definiciones de **EventSource** con el mismo nombre genera un problema en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="f86da-117">Having multiple **EventSource** definitions that use the same name causes an issue at run time.</span></span> <span data-ttu-id="f86da-118">Cada evento definido debe tener un identificador único.</span><span class="sxs-lookup"><span data-stu-id="f86da-118">Each defined event must have a unique identifier.</span></span> <span data-ttu-id="f86da-119">Si el identificador no es único, se produce un error en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="f86da-119">If an identifier is not unique, a runtime failure occurs.</span></span> <span data-ttu-id="f86da-120">En algunas organizaciones se asignan previamente rangos de valores para los identificadores, lo cual evita conflictos entre los equipos de desarrollo independientes.</span><span class="sxs-lookup"><span data-stu-id="f86da-120">Some organizations preassign ranges of values for identifiers to avoid conflicts between separate development teams.</span></span> <span data-ttu-id="f86da-121">Para más información, consulte el [blog de Vance](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) o la [documentación de MSDN](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span><span class="sxs-lookup"><span data-stu-id="f86da-121">For more information, see [Vance's blog](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) or the [MSDN documentation](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span></span>

### <a name="using-structured-eventsource-events"></a><span data-ttu-id="f86da-122">Uso de eventos EventSource estructurados</span><span class="sxs-lookup"><span data-stu-id="f86da-122">Using structured EventSource events</span></span>

<span data-ttu-id="f86da-123">Los eventos de los ejemplos de código de esta sección se definen para un caso concreto, como cuando se registra un tipo de servicio.</span><span class="sxs-lookup"><span data-stu-id="f86da-123">Each of the events in the code examples in this section are defined for a specific case, for example, when a service type is registered.</span></span> <span data-ttu-id="f86da-124">Al definir mensajes por caso de uso, se pueden empaquetar datos con el texto del error, y se puede buscar y filtrar más fácilmente según el nombre o los valores de las propiedades especificadas.</span><span class="sxs-lookup"><span data-stu-id="f86da-124">When you define messages by use case, data can be packaged with the text of the error, and you can more easily search and filter based on the names or values of the specified properties.</span></span> <span data-ttu-id="f86da-125">La estructuración del resultado de la instrumentación facilita su uso, pero se requiere mayor tiempo y reflexión para definir un nuevo evento para cada caso de uso.</span><span class="sxs-lookup"><span data-stu-id="f86da-125">Structuring the instrumentation output makes it easier to consume, but requires more thought and time to define a new event for each use case.</span></span> <span data-ttu-id="f86da-126">Algunas definiciones de eventos se pueden compartir en toda la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f86da-126">Some event definitions can be shared across the entire application.</span></span> <span data-ttu-id="f86da-127">Por ejemplo, el evento de inicio o detención de un método se podría reutilizar en muchos servicios de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="f86da-127">For example, a method start or stop event would be reused across many services within an application.</span></span> <span data-ttu-id="f86da-128">Un servicio específico de dominio, como un sistema de pedidos, puede tener un evento **CreateOrder** con su propio evento único.</span><span class="sxs-lookup"><span data-stu-id="f86da-128">A domain-specific service, like an order system, might have a **CreateOrder** event, which has its own unique event.</span></span> <span data-ttu-id="f86da-129">Este enfoque genera a menudo una gran cantidad de eventos y puede necesitar la coordinación de los identificadores entre los equipos de proyecto.</span><span class="sxs-lookup"><span data-stu-id="f86da-129">This approach might generate many events, and potentially require coordination of identifiers across project teams.</span></span> 

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // The instance constructor is private to enforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        // The ServiceTypeRegistered event contains a unique identifier, an event attribute that defined the event, and the code implementation of the event.
        private const int ServiceTypeRegisteredEventId = 3;
        [Event(ServiceTypeRegisteredEventId, Level = EventLevel.Informational, Message = "Service host process {0} registered service type {1}", Keywords = Keywords.ServiceInitialization)]
        public void ServiceTypeRegistered(int hostProcessId, string serviceType)
        {
            WriteEvent(ServiceTypeRegisteredEventId, hostProcessId, serviceType);
        }

        // The ServiceHostInitializationFailed event contains a unique identifier, an event attribute that defined the event, and the code implementation of the event.
        private const int ServiceHostInitializationFailedEventId = 4;
        [Event(ServiceHostInitializationFailedEventId, Level = EventLevel.Error, Message = "Service host initialization failed", Keywords = Keywords.ServiceInitialization)]
        public void ServiceHostInitializationFailed(string exception)
        {
            WriteEvent(ServiceHostInitializationFailedEventId, exception);
        }
```

### <a name="using-eventsource-generically"></a><span data-ttu-id="f86da-130">Uso de EventSource genéricamente</span><span class="sxs-lookup"><span data-stu-id="f86da-130">Using EventSource generically</span></span>

<span data-ttu-id="f86da-131">Dado que la definición de eventos específicos puede resultar difícil, muchas personas definen algunos con un conjunto común de parámetros que por lo general generan la información saliente como cadena.</span><span class="sxs-lookup"><span data-stu-id="f86da-131">Because defining specific events can be difficult, many people define a few events with a common set of parameters that generally output their information as a string.</span></span> <span data-ttu-id="f86da-132">Gran parte de la estructura se pierde, lo que dificulta la búsqueda y el filtrado de los resultados.</span><span class="sxs-lookup"><span data-stu-id="f86da-132">Much of the structured aspect is lost, and it's more difficult to search and filter the results.</span></span> <span data-ttu-id="f86da-133">Con este enfoque se definen algunos eventos que normalmente corresponden a los niveles de registro.</span><span class="sxs-lookup"><span data-stu-id="f86da-133">In this approach, a few events that usually correspond to the logging levels are defined.</span></span> <span data-ttu-id="f86da-134">El fragmento de código siguiente define un mensaje de error y de depuración:</span><span class="sxs-lookup"><span data-stu-id="f86da-134">The following snippet defines a debug and error message:</span></span>

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // The Instance constructor is private, to enforce singleton semantics.
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

<span data-ttu-id="f86da-135">El uso de instrumentación híbrida (estructurada y genérica) también puede funcionar.</span><span class="sxs-lookup"><span data-stu-id="f86da-135">Using a hybrid of structured and generic instrumentation also can work well.</span></span> <span data-ttu-id="f86da-136">La instrumentación estructurada se usa para informar sobre errores y métricas.</span><span class="sxs-lookup"><span data-stu-id="f86da-136">Structured instrumentation is used for reporting errors and metrics.</span></span> <span data-ttu-id="f86da-137">Los eventos genéricos pueden incluirse en el registro detallado para la solución de problemas por parte de los ingenieros.</span><span class="sxs-lookup"><span data-stu-id="f86da-137">Generic events can be used for the detailed logging that is consumed by engineers for troubleshooting.</span></span>

## <a name="aspnet-core-logging"></a><span data-ttu-id="f86da-138">Registro de ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="f86da-138">ASP.NET Core logging</span></span>

<span data-ttu-id="f86da-139">Es importante planear minuciosamente la instrumentación del código.</span><span class="sxs-lookup"><span data-stu-id="f86da-139">It's important to carefully plan how you will instrument your code.</span></span> <span data-ttu-id="f86da-140">Un plan de instrumentación correcto puede ayudarle a evitar que se desestabilice el código base y sea necesario volver a instrumentarlo.</span><span class="sxs-lookup"><span data-stu-id="f86da-140">The right instrumentation plan can help you avoid potentially destabilizing your code base, and then needing to reinstrument the code.</span></span> <span data-ttu-id="f86da-141">Para reducir el riesgo, puede elegir una biblioteca de instrumentación como [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), componente de Microsoft ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="f86da-141">To reduce risk, you can choose an instrumentation library like [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), which is part of Microsoft ASP.NET Core.</span></span> <span data-ttu-id="f86da-142">ASP.NET Core tiene una interfaz [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) que puede usar con su proveedor preferido al tiempo que reduce al mínimo el efecto sobre el código existente.</span><span class="sxs-lookup"><span data-stu-id="f86da-142">ASP.NET Core has an [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface that you can use with the provider of your choice, while minimizing the effect on existing code.</span></span> <span data-ttu-id="f86da-143">Puede utilizar el código de ASP.NET Core en Windows y Linux, y en .NET Framework completo, por lo que el código de instrumentación es estándar.</span><span class="sxs-lookup"><span data-stu-id="f86da-143">You can use the code in ASP.NET Core on Windows and Linux, and in the full .NET Framework, so your instrumentation code is standardized.</span></span> <span data-ttu-id="f86da-144">Esto se trata con más detalle a continuación:</span><span class="sxs-lookup"><span data-stu-id="f86da-144">This is further explored below:</span></span>

### <a name="using-microsoftextensionslogging-in-service-fabric"></a><span data-ttu-id="f86da-145">Uso de Microsoft.Extensions.Logging en Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f86da-145">Using Microsoft.Extensions.Logging in Service Fabric</span></span>

1. <span data-ttu-id="f86da-146">Agregue el paquete de NuGet Microsoft.Extensions.Logging al proyecto que desee instrumentar.</span><span class="sxs-lookup"><span data-stu-id="f86da-146">Add the Microsoft.Extensions.Logging NuGet package to the project you want to instrument.</span></span> <span data-ttu-id="f86da-147">Además, agregue los paquetes del proveedor (vea el ejemplo siguiente para paquetes de terceros).</span><span class="sxs-lookup"><span data-stu-id="f86da-147">Also, add any provider packages (for a third-party package, see the following example).</span></span> <span data-ttu-id="f86da-148">Consulte el artículo sobre el [registro de ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging) para más información.</span><span class="sxs-lookup"><span data-stu-id="f86da-148">For more information, see [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span></span>
2. <span data-ttu-id="f86da-149">Agregue una directiva **using** para Microsoft.Extensions.Logging al archivo de servicio.</span><span class="sxs-lookup"><span data-stu-id="f86da-149">Add a **using** directive for Microsoft.Extensions.Logging to your service file.</span></span>
3. <span data-ttu-id="f86da-150">Defina una variable privada dentro de la clase de servicio.</span><span class="sxs-lookup"><span data-stu-id="f86da-150">Define a private variable within your service class.</span></span>

  ```csharp
  private ILogger _logger = null;

  ```
4. <span data-ttu-id="f86da-151">En el constructor de la clase de servicio, agregue este código:</span><span class="sxs-lookup"><span data-stu-id="f86da-151">In the constructor of your service class, add this code:</span></span>

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. <span data-ttu-id="f86da-152">Inicie la instrumentación del código en los métodos.</span><span class="sxs-lookup"><span data-stu-id="f86da-152">Start instrumenting your code in your methods.</span></span> <span data-ttu-id="f86da-153">Estos son algunos ejemplos:</span><span class="sxs-lookup"><span data-stu-id="f86da-153">Here are a few samples:</span></span>

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and the duration of the request.
  // Later in the article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a><span data-ttu-id="f86da-154">Uso de otros proveedores de registro</span><span class="sxs-lookup"><span data-stu-id="f86da-154">Using other logging providers</span></span>

<span data-ttu-id="f86da-155">Algunos proveedores de terceros usan el enfoque descrito en la sección anterior, como [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/) y [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span><span class="sxs-lookup"><span data-stu-id="f86da-155">Some third-party providers use the approach described in the preceding section, including [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), and [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span></span> <span data-ttu-id="f86da-156">Puede conectarlos al registro de ASP.NET Core o utilizarlos por separado.</span><span class="sxs-lookup"><span data-stu-id="f86da-156">You can plug each of these into ASP.NET Core logging, or you can use them separately.</span></span> <span data-ttu-id="f86da-157">Serilog tiene una característica que enriquece todos los mensajes enviados desde un registrador.</span><span class="sxs-lookup"><span data-stu-id="f86da-157">Serilog has a feature that enriches all messages sent from a logger.</span></span> <span data-ttu-id="f86da-158">Esta característica puede ser útil para generar el nombre del servicio, el tipo y la información de la partición.</span><span class="sxs-lookup"><span data-stu-id="f86da-158">This feature can be useful to output the service name, type, and partition information.</span></span> <span data-ttu-id="f86da-159">Para utilizar esta funcionalidad en la infraestructura de ASP.NET Core, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f86da-159">To use this capability in the ASP.NET Core infrastructure, do these steps:</span></span>

1. <span data-ttu-id="f86da-160">Agregue los paquetes de NuGet Serilog, Serilog.Extensions.Logging y Serilog.Sinks.Observable al proyecto.</span><span class="sxs-lookup"><span data-stu-id="f86da-160">Add the Serilog, Serilog.Extensions.Logging, and Serilog.Sinks.Observable NuGet packages to the project.</span></span> <span data-ttu-id="f86da-161">En el ejemplo siguiente, agregue también Serilog.Sinks.Literate.</span><span class="sxs-lookup"><span data-stu-id="f86da-161">For the next example, also add Serilog.Sinks.Literate.</span></span> <span data-ttu-id="f86da-162">Más adelante en este artículo se muestra un mejor enfoque.</span><span class="sxs-lookup"><span data-stu-id="f86da-162">A better approach is shown later in this article.</span></span>
2. <span data-ttu-id="f86da-163">Ebn Serilog, cree LoggerConfiguration y la instancia del registrador.</span><span class="sxs-lookup"><span data-stu-id="f86da-163">In Serilog, create a LoggerConfiguration and the logger instance.</span></span>

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. <span data-ttu-id="f86da-164">Agregue un argumento Serilog.ILogger al constructor del servicio y pase el registrador recién creado.</span><span class="sxs-lookup"><span data-stu-id="f86da-164">Add a Serilog.ILogger argument to the service constructor, and pass the newly created logger.</span></span>

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. <span data-ttu-id="f86da-165">En el constructor del servicio, agregue el siguiente código, con lo que se crean la propiedad enrichers para las propiedades **ServiceTypeName**, **ServiceName**, **PartitionId** y **InstanceId** del servicio.</span><span class="sxs-lookup"><span data-stu-id="f86da-165">In the service constructor, add the following code, which creates the property enrichers for the **ServiceTypeName**, **ServiceName**, **PartitionId**, and **InstanceId** properties of the service.</span></span> <span data-ttu-id="f86da-166">Se agrega también una propiedad enricher a la fábrica de registro de ASP.NET Core, por lo que podrá usar Microsoft.Extensions.Logging.ILogger en el código.</span><span class="sxs-lookup"><span data-stu-id="f86da-166">It also adds a property enricher to the ASP.NET Core logging factory, so you can use Microsoft.Extensions.Logging.ILogger in your code.</span></span>

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

5. <span data-ttu-id="f86da-167">Instrumente el código como su estuviera usando ASP.NET Core sin Serilog.</span><span class="sxs-lookup"><span data-stu-id="f86da-167">Instrument the code the same as if you were using ASP.NET Core without Serilog.</span></span>

  >[!NOTE]
  ><span data-ttu-id="f86da-168">No es recomendable usar el Log.Logger estático con el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="f86da-168">We recommend that you don't use the static Log.Logger with the preceding example.</span></span> <span data-ttu-id="f86da-169">Service Fabric puede hospedar varias instancias del mismo tipo de servicio dentro de un único proceso.</span><span class="sxs-lookup"><span data-stu-id="f86da-169">Service Fabric can host multiple instances of the same service type within a single process.</span></span> <span data-ttu-id="f86da-170">Si usa el Log.Logger estático, la última versión de la propiedad enrichers mostrará los valores para todas las instancias en ejecución.</span><span class="sxs-lookup"><span data-stu-id="f86da-170">If you use the static Log.Logger, the last writer of the property enrichers will show values for all instances that are running.</span></span> <span data-ttu-id="f86da-171">Este es uno de los motivos por los cuales la variable _logger es una variable de miembro privada de la clase de servicio.</span><span class="sxs-lookup"><span data-stu-id="f86da-171">This is one reason why the _logger variable is a private member variable of the service class.</span></span> <span data-ttu-id="f86da-172">Además, debe poner _logger a disposición del código común, que podría utilizarse en diferentes servicios.</span><span class="sxs-lookup"><span data-stu-id="f86da-172">Also, you must make the _logger available to common code, which might be used across services.</span></span>

## <a name="choosing-a-logging-provider"></a><span data-ttu-id="f86da-173">Elección de un proveedor de registro</span><span class="sxs-lookup"><span data-stu-id="f86da-173">Choosing a logging provider</span></span>

<span data-ttu-id="f86da-174">Si la aplicación depende del alto rendimiento, **EventSource** suele ser el mejor enfoque.</span><span class="sxs-lookup"><span data-stu-id="f86da-174">If your application relies on high performance, **EventSource** is usually a good approach.</span></span> <span data-ttu-id="f86da-175">*Por lo general*, **EventSource** utiliza menos recursos y su rendimiento es mejor que el del registro de ASP.NET Core o de cualquiera de las soluciones de terceros disponibles.</span><span class="sxs-lookup"><span data-stu-id="f86da-175">**EventSource** *generally* uses fewer resources and performs better than ASP.NET Core logging or any of the available third-party solutions.</span></span>  <span data-ttu-id="f86da-176">Esto no supone un problema para muchos servicios, pero si está orientado al rendimiento, **EventSource** sería una opción mejor.</span><span class="sxs-lookup"><span data-stu-id="f86da-176">This isn't an issue for many services, but if your service is performance-oriented, using **EventSource** might be a better choice.</span></span> <span data-ttu-id="f86da-177">Sin embargo, para obtener las ventajas del registro estructurado, **EventSource** requiere una mayor inversión por parte del equipo de ingeniería.</span><span class="sxs-lookup"><span data-stu-id="f86da-177">However, to get these benefits of structured logging, **EventSource** requires a larger investment from your engineering team.</span></span> <span data-ttu-id="f86da-178">Si es posible, cree un prototipo rápido de algunas opciones de registro y, luego, seleccione la que mejor se adapte a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="f86da-178">If possible, do a quick prototype of a few logging options, and then choose the one that best meets your needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f86da-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f86da-179">Next steps</span></span>

<span data-ttu-id="f86da-180">Una vez que haya elegido el proveedor de registro para instrumentar las aplicaciones y los servicios, los registros y los eventos deben agregarse antes de que se puedan enviar a cualquier plataforma de análisis.</span><span class="sxs-lookup"><span data-stu-id="f86da-180">Once you have chosen your logging provider to instrument your applications and services, your logs and events need to be aggregated before they can be sent to any analysis platform.</span></span> <span data-ttu-id="f86da-181">Obtenga información sobre [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) y [WAD](service-fabric-diagnostics-event-aggregation-wad.md) para entender mejor algunas de las opciones recomendadas.</span><span class="sxs-lookup"><span data-stu-id="f86da-181">Read about [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) and [WAD](service-fabric-diagnostics-event-aggregation-wad.md) to better understand some of the recommended options.</span></span>
