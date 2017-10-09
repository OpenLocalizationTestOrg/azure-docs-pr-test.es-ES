---
title: "aaaCreate su primera aplicación de Service Fabric en C# | Documentos de Microsoft"
description: "Introducción toocreating una aplicación de Microsoft Azure Service Fabric con servicios y sin estado."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d9b44d75-e905-468e-b867-2190ce97379a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: vturecek
ms.openlocfilehash: e95e67cc84be1b83c936b250cae9112ddc77b963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="8d25e-103">Introducción a los servicios de confianza</span><span class="sxs-lookup"><span data-stu-id="8d25e-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8d25e-104">C# en Windows</span><span class="sxs-lookup"><span data-stu-id="8d25e-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="8d25e-105">Java en Linux</span><span class="sxs-lookup"><span data-stu-id="8d25e-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
> 
> 

<span data-ttu-id="8d25e-106">Una aplicación de Service Fabric de Azure contiene uno o varios servicios que ejecutan su código.</span><span class="sxs-lookup"><span data-stu-id="8d25e-106">An Azure Service Fabric application contains one or more services that run your code.</span></span> <span data-ttu-id="8d25e-107">Esta guía le mostrará cómo toocreate sin estado y con estado las aplicaciones de Service Fabric con [servicios confiables](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8d25e-107">This guide shows you how toocreate both stateless and stateful Service Fabric applications with [Reliable Services](service-fabric-reliable-services-introduction.md).</span></span>  <span data-ttu-id="8d25e-108">Este vídeo de Microsoft Virtual Academy también muestra cómo toocreate un servicio confiable sin estado:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span><span class="sxs-lookup"><span data-stu-id="8d25e-108">This Microsoft Virtual Academy video also shows you how toocreate a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a><span data-ttu-id="8d25e-109">Conceptos básicos</span><span class="sxs-lookup"><span data-stu-id="8d25e-109">Basic concepts</span></span>
<span data-ttu-id="8d25e-110">tooget a trabajar con servicios de confianza, solo se necesita toounderstand algunos conceptos básicos:</span><span class="sxs-lookup"><span data-stu-id="8d25e-110">tooget started with Reliable Services, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="8d25e-111">**Tipo de servicio**: se trata de la implementación del servicio.</span><span class="sxs-lookup"><span data-stu-id="8d25e-111">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="8d25e-112">Se define mediante la clase hello escribir que extiende `StatelessService` y cualquier otro código o a las dependencias que se usan en él, junto con un nombre y un número de versión.</span><span class="sxs-lookup"><span data-stu-id="8d25e-112">It is defined by hello class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="8d25e-113">**Con el nombre de instancia de servicio**: toorun su servicio, crear instancias con nombre de su tipo de servicio, mucho como crear instancias de objeto de un tipo de clase.</span><span class="sxs-lookup"><span data-stu-id="8d25e-113">**Named service instance**: toorun your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="8d25e-114">Una instancia de servicio tiene un nombre en forma de Hola de identificadores URI utilizando Hola "fabric: /" esquema, como "fabric: / MyApp/MyService".</span><span class="sxs-lookup"><span data-stu-id="8d25e-114">A service instance has a name in hello form of a URI using hello "fabric:/" scheme, such as "fabric:/MyApp/MyService".</span></span>
* <span data-ttu-id="8d25e-115">**Host de servicio**: Hola instancias de servicio crear necesidad toorun dentro de un proceso de host con nombre.</span><span class="sxs-lookup"><span data-stu-id="8d25e-115">**Service host**: hello named service instances you create need toorun inside a host process.</span></span> <span data-ttu-id="8d25e-116">host de servicio de Hello es simplemente un proceso donde se pueden ejecutar instancias de su servicio.</span><span class="sxs-lookup"><span data-stu-id="8d25e-116">hello service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="8d25e-117">**Registro de servicio**: el registro incluye todos los elementos.</span><span class="sxs-lookup"><span data-stu-id="8d25e-117">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="8d25e-118">Hello service type debe estar registrado con hello Service Fabric en tiempo de ejecución en un servicio de instancias de host tooallow Service Fabric toocreate del mismo toorun.</span><span class="sxs-lookup"><span data-stu-id="8d25e-118">hello service type must be registered with hello Service Fabric runtime in a service host tooallow Service Fabric toocreate instances of it toorun.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="8d25e-119">Creación de un servicio sin estado</span><span class="sxs-lookup"><span data-stu-id="8d25e-119">Create a stateless service</span></span>
<span data-ttu-id="8d25e-120">Un servicio sin estado es un tipo de servicio que se encuentra actualmente norm hello en aplicaciones de nube.</span><span class="sxs-lookup"><span data-stu-id="8d25e-120">A stateless service is a type of service that is currently hello norm in cloud applications.</span></span> <span data-ttu-id="8d25e-121">Se considera sin estado porque el propio servicio hello no contiene datos que es necesario toobe almacenada de forma confiable u ofrezca alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="8d25e-121">It is considered stateless because hello service itself does not contain data that needs toobe stored reliably or made highly available.</span></span> <span data-ttu-id="8d25e-122">Si se cierra una instancia de un servicio sin estado, todo su estado interno se pierde.</span><span class="sxs-lookup"><span data-stu-id="8d25e-122">If an instance of a stateless service shuts down, all of its internal state is lost.</span></span> <span data-ttu-id="8d25e-123">En este tipo de servicio, el estado debe ser almacén externo de tooan persistente, como tablas de Azure o una base de datos SQL, para él toobe realizados altamente disponible y confiable.</span><span class="sxs-lookup"><span data-stu-id="8d25e-123">In this type of service, state must be persisted tooan external store, such as Azure Tables or a SQL database, for it toobe made highly available and reliable.</span></span>

<span data-ttu-id="8d25e-124">Inicie Visual Studio 2015 o Visual Studio 2017 como administrador y cree un nuevo proyecto de aplicación de Service Fabric denominado *HelloWorld*:</span><span class="sxs-lookup"><span data-stu-id="8d25e-124">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project named *HelloWorld*:</span></span>

![Usar toocreate de cuadro de diálogo de hello nuevo proyecto una nueva aplicación de Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

<span data-ttu-id="8d25e-126">Después, cree un proyecto de servicio sin estado denominado *HelloWorldStateless*:</span><span class="sxs-lookup"><span data-stu-id="8d25e-126">Then create a stateless service project named *HelloWorldStateless*:</span></span>

![En el segundo cuadro de diálogo hello, cree un proyecto de servicio sin estado](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

<span data-ttu-id="8d25e-128">La solución contiene ahora dos proyectos:</span><span class="sxs-lookup"><span data-stu-id="8d25e-128">Your solution now contains two projects:</span></span>

* <span data-ttu-id="8d25e-129">*HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="8d25e-129">*HelloWorld*.</span></span> <span data-ttu-id="8d25e-130">Se trata de hello *aplicación* proyecto que contiene su *services*.</span><span class="sxs-lookup"><span data-stu-id="8d25e-130">This is hello *application* project that contains your *services*.</span></span> <span data-ttu-id="8d25e-131">También contiene el manifiesto de aplicación Hola que describe la aplicación hello, así como un número de secuencias de comandos de PowerShell que le ayudarán a toodeploy la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8d25e-131">It also contains hello application manifest that describes hello application, as well as a number of PowerShell scripts that help you toodeploy your application.</span></span>
* <span data-ttu-id="8d25e-132">*HelloWorldStateless*.</span><span class="sxs-lookup"><span data-stu-id="8d25e-132">*HelloWorldStateless*.</span></span> <span data-ttu-id="8d25e-133">Se trata de un proyecto de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d25e-133">This is hello service project.</span></span> <span data-ttu-id="8d25e-134">Que contiene la implementación de servicio sin estado Hola.</span><span class="sxs-lookup"><span data-stu-id="8d25e-134">It contains hello stateless service implementation.</span></span>

## <a name="implement-hello-service"></a><span data-ttu-id="8d25e-135">Implementar el servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="8d25e-135">Implement hello service</span></span>
<span data-ttu-id="8d25e-136">Abra hello **HelloWorldStateless.cs** archivo de proyecto de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d25e-136">Open hello **HelloWorldStateless.cs** file in hello service project.</span></span> <span data-ttu-id="8d25e-137">En Service Fabric, un servicio puede ejecutar cualquier lógica de negocios.</span><span class="sxs-lookup"><span data-stu-id="8d25e-137">In Service Fabric, a service can run any business logic.</span></span> <span data-ttu-id="8d25e-138">API de servicio de Hello proporciona dos puntos de entrada para el código:</span><span class="sxs-lookup"><span data-stu-id="8d25e-138">hello service API provides two entry points for your code:</span></span>

* <span data-ttu-id="8d25e-139">Llama a un método de punto de entrada abierto denominado " *RunAsync*" donde puede comenzar la ejecución de cualquier carga de trabajo que desee, como cargas de trabajo de proceso de larga duración.</span><span class="sxs-lookup"><span data-stu-id="8d25e-139">An open-ended entry point method, called *RunAsync*, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* <span data-ttu-id="8d25e-140">Un punto de entrada de comunicación en el que puede conectar su pila de comunicación preferida, como ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="8d25e-140">A communication entry point where you can plug in your communication stack of choice, such as ASP.NET Core.</span></span> <span data-ttu-id="8d25e-141">Aquí es donde puede empezar a recibir las solicitudes de usuarios y otros servicios.</span><span class="sxs-lookup"><span data-stu-id="8d25e-141">This is where you can start receiving requests from users and other services.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

<span data-ttu-id="8d25e-142">En este tutorial, nos centraremos en hello `RunAsync()` método de punto de entrada.</span><span class="sxs-lookup"><span data-stu-id="8d25e-142">In this tutorial, we will focus on hello `RunAsync()` entry point method.</span></span> <span data-ttu-id="8d25e-143">Aquí es donde puede comenzar a ejecutar el código de inmediato.</span><span class="sxs-lookup"><span data-stu-id="8d25e-143">This is where you can immediately start running your code.</span></span>
<span data-ttu-id="8d25e-144">plantilla de proyecto de Hello incluye una implementación de ejemplo `RunAsync()` que incrementa un recuento gradual.</span><span class="sxs-lookup"><span data-stu-id="8d25e-144">hello project template includes a sample implementation of `RunAsync()` that increments a rolling count.</span></span>

> [!NOTE]
> <span data-ttu-id="8d25e-145">Para obtener más información acerca de cómo la pila toowork con una comunicación, vea [servicios de API Web del servicio tejido con OWIN hospeda a sí mismo](service-fabric-reliable-services-communication-webapi.md)</span><span class="sxs-lookup"><span data-stu-id="8d25e-145">For details about how toowork with a communication stack, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md)</span></span>
> 
> 

### <a name="runasync"></a><span data-ttu-id="8d25e-146">RunAsync</span><span class="sxs-lookup"><span data-stu-id="8d25e-146">RunAsync</span></span>
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    long iterations = 0;

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        ServiceEventSource.Current.ServiceMessage(this, "Working-{0}", ++iterations);

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

<span data-ttu-id="8d25e-147">plataforma de Hello llama a este método cuando una instancia de un servicio es tooexecute colocado y listo.</span><span class="sxs-lookup"><span data-stu-id="8d25e-147">hello platform calls this method when an instance of a service is placed and ready tooexecute.</span></span> <span data-ttu-id="8d25e-148">Para un servicio sin estado, que simplemente significa que cuando se abre la instancia de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d25e-148">For a stateless service, that simply means when hello service instance is opened.</span></span> <span data-ttu-id="8d25e-149">Un token de cancelación se proporciona toocoordinate cuando la instancia de servicio necesita toobe cerrado.</span><span class="sxs-lookup"><span data-stu-id="8d25e-149">A cancellation token is provided toocoordinate when your service instance needs toobe closed.</span></span> <span data-ttu-id="8d25e-150">En Service Fabric, este ciclo de apertura y cierre de una instancia de servicio puede producir varias veces más vida Hola Hola como un todo.</span><span class="sxs-lookup"><span data-stu-id="8d25e-150">In Service Fabric, this open/close cycle of a service instance can occur many times over hello lifetime of hello service as a whole.</span></span> <span data-ttu-id="8d25e-151">Esto puede ocurrir por diversos motivos, incluidos los siguientes:</span><span class="sxs-lookup"><span data-stu-id="8d25e-151">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="8d25e-152">sistema de Hello mueve las instancias de servicio para equilibrar los recursos.</span><span class="sxs-lookup"><span data-stu-id="8d25e-152">hello system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="8d25e-153">Se producen errores en el código.</span><span class="sxs-lookup"><span data-stu-id="8d25e-153">Faults occur in your code.</span></span>
* <span data-ttu-id="8d25e-154">se actualiza la aplicación Hello o sistema.</span><span class="sxs-lookup"><span data-stu-id="8d25e-154">hello application or system is upgraded.</span></span>
* <span data-ttu-id="8d25e-155">hardware subyacente Hola experimenta una interrupción inesperada.</span><span class="sxs-lookup"><span data-stu-id="8d25e-155">hello underlying hardware experiences an outage.</span></span>

<span data-ttu-id="8d25e-156">Esta orquestación está administrada por hello sistema tookeep el servicio de alta disponibilidad y equilibrado correctamente.</span><span class="sxs-lookup"><span data-stu-id="8d25e-156">This orchestration is managed by hello system tookeep your service highly available and properly balanced.</span></span>

<span data-ttu-id="8d25e-157">`RunAsync()` no debe bloquearse de forma sincrónica.</span><span class="sxs-lookup"><span data-stu-id="8d25e-157">`RunAsync()` should not block synchronously.</span></span> <span data-ttu-id="8d25e-158">La implementación de Coredispatcher debe devolver una tarea o await en cualquier toocontinue de tiempo de ejecución de las operaciones de ejecución prolongada o de bloqueo tooallow Hola.</span><span class="sxs-lookup"><span data-stu-id="8d25e-158">Your implementation of RunAsync should return a Task or await on any long-running or blocking operations tooallow hello runtime toocontinue.</span></span> <span data-ttu-id="8d25e-159">Tenga en cuenta en hello `while(true)` bucle en el ejemplo anterior de hello, una devolución de tarea `await Task.Delay()` se utiliza.</span><span class="sxs-lookup"><span data-stu-id="8d25e-159">Note in hello `while(true)` loop in hello previous example, a Task-returning `await Task.Delay()` is used.</span></span> <span data-ttu-id="8d25e-160">Si la carga de trabajo debe bloquearse de forma sincrónica, debería programar una nueva tarea con `Task.Run()` en la implementación de `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="8d25e-160">If your workload must block synchronously, you should schedule a new Task with `Task.Run()` in your `RunAsync` implementation.</span></span>

<span data-ttu-id="8d25e-161">Cancelación de la carga de trabajo es un esfuerzo cooperativo organizado Hola proporcionada el token de cancelación.</span><span class="sxs-lookup"><span data-stu-id="8d25e-161">Cancellation of your workload is a cooperative effort orchestrated by hello provided cancellation token.</span></span> <span data-ttu-id="8d25e-162">Hola sistema esperará la tarea tooend (de realización correcta, cancelación o error) antes de que pase.</span><span class="sxs-lookup"><span data-stu-id="8d25e-162">hello system will wait for your task tooend (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="8d25e-163">Es importante toohonor Hola cancelación token, finalizar cualquier trabajo y salir `RunAsync()` lo más rápido posible al sistema de hello solicita la cancelación.</span><span class="sxs-lookup"><span data-stu-id="8d25e-163">It is important toohonor hello cancellation token, finish any work, and exit `RunAsync()` as quickly as possible when hello system requests cancellation.</span></span>

<span data-ttu-id="8d25e-164">En este ejemplo de servicio sin estado, el recuento de Hola se almacena en una variable local.</span><span class="sxs-lookup"><span data-stu-id="8d25e-164">In this stateless service example, hello count is stored in a local variable.</span></span> <span data-ttu-id="8d25e-165">Pero porque se trata de un servicio sin estado, valor de Hola que se almacena solamente existe por hello ciclo de vida actual de su instancia de servicio.</span><span class="sxs-lookup"><span data-stu-id="8d25e-165">But because this is a stateless service, hello value that's stored exists only for hello current lifecycle of its service instance.</span></span> <span data-ttu-id="8d25e-166">Cuando el servicio de Hola se mueve o se reinicia, el valor de Hola se pierde.</span><span class="sxs-lookup"><span data-stu-id="8d25e-166">When hello service moves or restarts, hello value is lost.</span></span>

## <a name="create-a-stateful-service"></a><span data-ttu-id="8d25e-167">Creación de un servicio con estado</span><span class="sxs-lookup"><span data-stu-id="8d25e-167">Create a stateful service</span></span>
<span data-ttu-id="8d25e-168">Service Fabric presenta un nuevo tipo de servicio que es con estado.</span><span class="sxs-lookup"><span data-stu-id="8d25e-168">Service Fabric introduces a new kind of service that is stateful.</span></span> <span data-ttu-id="8d25e-169">Un servicio con estado puede mantener el estado confiable dentro Hola propio servicio, colocado con código de hello que lo está usando.</span><span class="sxs-lookup"><span data-stu-id="8d25e-169">A stateful service can maintain state reliably within hello service itself, co-located with hello code that's using it.</span></span> <span data-ttu-id="8d25e-170">Estado ofrezca alta disponibilidad por Service Fabric sin almacén externo de hello necesidad toopersist estado tooan.</span><span class="sxs-lookup"><span data-stu-id="8d25e-170">State is made highly available by Service Fabric without hello need toopersist state tooan external store.</span></span>

<span data-ttu-id="8d25e-171">tooconvert un valor de contador de toohighly sin estado disponible y persistente, incluso cuando el servicio de Hola se mueve o se reinicia, se necesita un servicio con estado.</span><span class="sxs-lookup"><span data-stu-id="8d25e-171">tooconvert a counter value from stateless toohighly available and persistent, even when hello service moves or restarts, you need a stateful service.</span></span>

<span data-ttu-id="8d25e-172">En Hola mismo *HelloWorld* aplicación, puede agregar un nuevo servicio con el botón secundario en referencias de servicios de hello en el proyecto de aplicación de Hola y seleccionando **Agregar -> nuevo servicio de Fabric**.</span><span class="sxs-lookup"><span data-stu-id="8d25e-172">In hello same *HelloWorld* application, you can add a new service by right-clicking on hello Services references in hello application project and selecting **Add ->  New Service Fabric Service**.</span></span>

![Agregar una aplicación de Service Fabric tooyour de servicio](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

<span data-ttu-id="8d25e-174">Seleccione **Servicio con estado** y asígnele el nombre *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="8d25e-174">Select **Stateful Service** and name it *HelloWorldStateful*.</span></span> <span data-ttu-id="8d25e-175">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="8d25e-175">Click **OK**.</span></span>

![Usar toocreate de cuadro de diálogo de hello nuevo proyecto un nuevo servicio con estado de Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

<span data-ttu-id="8d25e-177">La aplicación ahora debería tener dos servicios: Hola servicio sin estado *HelloWorldStateless* y el servicio con estado hello *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="8d25e-177">Your application should now have two services: hello stateless service *HelloWorldStateless* and hello stateful service *HelloWorldStateful*.</span></span>

<span data-ttu-id="8d25e-178">Un servicio con estado tiene Hola mismos puntos de entrada como un servicio sin estado.</span><span class="sxs-lookup"><span data-stu-id="8d25e-178">A stateful service has hello same entry points as a stateless service.</span></span> <span data-ttu-id="8d25e-179">Hola principal diferencia es disponibilidad Hola de un *proveedor de estado* estado que puede almacenar de forma confiable.</span><span class="sxs-lookup"><span data-stu-id="8d25e-179">hello main difference is hello availability of a *state provider* that can store state reliably.</span></span> <span data-ttu-id="8d25e-180">Tejido de servicio incluye una implementación de proveedor de estado llama [colecciones confiable](service-fabric-reliable-services-reliable-collections.md), que le permite crear estructuras de datos replicados mediante Hola confiable Administrador de estado.</span><span class="sxs-lookup"><span data-stu-id="8d25e-180">Service Fabric comes with a state provider implementation called [Reliable Collections](service-fabric-reliable-services-reliable-collections.md), which lets you create replicated data structures through hello Reliable State Manager.</span></span> <span data-ttu-id="8d25e-181">Un servicio de confianza con estado usa este proveedor de estado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="8d25e-181">A stateful Reliable Service uses this state provider by default.</span></span>

<span data-ttu-id="8d25e-182">Abra **HelloWorldStateful.cs** en *HelloWorldStateful*, que contiene Hola sigue Coredispatcher método:</span><span class="sxs-lookup"><span data-stu-id="8d25e-182">Open **HelloWorldStateful.cs** in *HelloWorldStateful*, which contains hello following RunAsync method:</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");

            ServiceEventSource.Current.ServiceMessage(this, "Current Counter Value: {0}",
                result.HasValue ? result.Value.ToString() : "Value does not exist.");

            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, hello transaction aborts, all changes are
            // discarded, and nothing is saved toohello secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a><span data-ttu-id="8d25e-183">RunAsync</span><span class="sxs-lookup"><span data-stu-id="8d25e-183">RunAsync</span></span>
<span data-ttu-id="8d25e-184">`RunAsync()` funciona de forma similar en los servicios con y sin estado.</span><span class="sxs-lookup"><span data-stu-id="8d25e-184">`RunAsync()` operates similarly in stateful and stateless services.</span></span> <span data-ttu-id="8d25e-185">Sin embargo, en un servicio con estado, plataforma Hola realiza un trabajo adicional en su nombre antes de ejecutar `RunAsync()`.</span><span class="sxs-lookup"><span data-stu-id="8d25e-185">However, in a stateful service, hello platform performs additional work on your behalf before it executes `RunAsync()`.</span></span> <span data-ttu-id="8d25e-186">Este trabajo puede incluir asegurarse de que el Administrador de estado confiable de Hola y confiable de colecciones son toouse listo.</span><span class="sxs-lookup"><span data-stu-id="8d25e-186">This work can include ensuring that hello Reliable State Manager and Reliable Collections are ready toouse.</span></span>

### <a name="reliable-collections-and-hello-reliable-state-manager"></a><span data-ttu-id="8d25e-187">Confiable hello el Administrador de estado confiable y colecciones</span><span class="sxs-lookup"><span data-stu-id="8d25e-187">Reliable Collections and hello Reliable State Manager</span></span>
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

<span data-ttu-id="8d25e-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) es una implementación de diccionario que puede usar tooreliably almacenar el estado de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d25e-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) is a dictionary implementation that you can use tooreliably store state in hello service.</span></span> <span data-ttu-id="8d25e-189">Con Service Fabric y confiable de las colecciones, puede almacenar los datos directamente en el servicio sin necesidad de Hola de un almacén persistente externo.</span><span class="sxs-lookup"><span data-stu-id="8d25e-189">With Service Fabric and Reliable Collections, you can store data directly in your service without hello need for an external persistent store.</span></span> <span data-ttu-id="8d25e-190">Gracias a Reliable Collections, los datos tendrán una alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="8d25e-190">Reliable Collections make your data highly available.</span></span> <span data-ttu-id="8d25e-191">Service Fabric realiza esta tarea creando y administrando automáticamente varias *réplicas* de su servicio.</span><span class="sxs-lookup"><span data-stu-id="8d25e-191">Service Fabric accomplishes this by creating and managing multiple *replicas* of your service for you.</span></span> <span data-ttu-id="8d25e-192">También proporciona una API que abstrae las complejidades de hello alejada de la administración de las réplicas y sus transiciones de estado.</span><span class="sxs-lookup"><span data-stu-id="8d25e-192">It also provides an API that abstracts away hello complexities of managing those replicas and their state transitions.</span></span>

<span data-ttu-id="8d25e-193">Reliable Collections puede almacenar cualquier tipo de .NET, incluidos los tipos personalizados, con un par de advertencias:</span><span class="sxs-lookup"><span data-stu-id="8d25e-193">Reliable Collections can store any .NET type, including your custom types, with a couple of caveats:</span></span>

* <span data-ttu-id="8d25e-194">Tejido de servicio hace que el estado de la alta disponibilidad *replicar* estado entre nodos y colecciones confiable almacenar el disco de toolocal de datos en cada réplica.</span><span class="sxs-lookup"><span data-stu-id="8d25e-194">Service Fabric makes your state highly available by *replicating* state across nodes, and Reliable Collections store your data toolocal disk on each replica.</span></span> <span data-ttu-id="8d25e-195">Es decir, todo lo que se almacena en Reliable Collections debe ser *serializable*.</span><span class="sxs-lookup"><span data-stu-id="8d25e-195">This means that everything that is stored in Reliable Collections must be *serializable*.</span></span> <span data-ttu-id="8d25e-196">De forma predeterminada, se usan colecciones confiable [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) para la serialización, por lo que es importante toomake seguro de que los tipos son [admite Hola serializador de contratos de datos](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) cuando se usa de forma predeterminada Hola serializador.</span><span class="sxs-lookup"><span data-stu-id="8d25e-196">By default, Reliable Collections use [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) for serialization, so it's important toomake sure that your types are [supported by hello Data Contract Serializer](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) when you use hello default serializer.</span></span>
* <span data-ttu-id="8d25e-197">Los objetos se replican para obtener una alta disponibilidad cuando se confirman transacciones en Reliable Collections.</span><span class="sxs-lookup"><span data-stu-id="8d25e-197">Objects are replicated for high availability when you commit transactions on Reliable Collections.</span></span> <span data-ttu-id="8d25e-198">Los objetos almacenados en Reliable Collections se mantienen en la memoria local en el servicio.</span><span class="sxs-lookup"><span data-stu-id="8d25e-198">Objects stored in Reliable Collections are kept in local memory in your service.</span></span> <span data-ttu-id="8d25e-199">Esto significa que tiene un objeto de toohello de referencia local.</span><span class="sxs-lookup"><span data-stu-id="8d25e-199">This means that you have a local reference toohello object.</span></span>
  
   <span data-ttu-id="8d25e-200">Es importante que no modifica las instancias locales de esos objetos sin realizar una operación de actualización en la colección confiable de hello en una transacción.</span><span class="sxs-lookup"><span data-stu-id="8d25e-200">It is important that you do not mutate local instances of those objects without performing an update operation on hello reliable collection in a transaction.</span></span> <span data-ttu-id="8d25e-201">Esto es porque cambios toolocal instancias de objetos no se replicarán automáticamente.</span><span class="sxs-lookup"><span data-stu-id="8d25e-201">This is because changes toolocal instances of objects will not be replicated automatically.</span></span> <span data-ttu-id="8d25e-202">Debe volver a insertar el objeto de hello en el diccionario de Hola o utilizar uno de hello *actualizar* métodos en el diccionario de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d25e-202">You must re-insert hello object back into hello dictionary or use one of hello *update* methods on hello dictionary.</span></span>

<span data-ttu-id="8d25e-203">Hola, Administrador de estado confiable administra colecciones confiable en su nombre.</span><span class="sxs-lookup"><span data-stu-id="8d25e-203">hello Reliable State Manager manages Reliable Collections for you.</span></span> <span data-ttu-id="8d25e-204">Puede simplemente pedir Hola confiable Administrador de Estados para una colección de confianza por su nombre en cualquier momento y en cualquier lugar en el servicio.</span><span class="sxs-lookup"><span data-stu-id="8d25e-204">You can simply ask hello Reliable State Manager for a reliable collection by name at any time and at any place in your service.</span></span> <span data-ttu-id="8d25e-205">Hola, Administrador de estado confiable garantiza que se recibe una referencia.</span><span class="sxs-lookup"><span data-stu-id="8d25e-205">hello Reliable State Manager ensures that you get a reference back.</span></span> <span data-ttu-id="8d25e-206">No recomendamos guardar referencias de instancias de la colección de tooreliable en variables de miembro de clase o propiedades.</span><span class="sxs-lookup"><span data-stu-id="8d25e-206">We don't recommended that you save references tooreliable collection instances in class member variables or properties.</span></span> <span data-ttu-id="8d25e-207">Debe tener especial cuidado tooensure que se establece la referencia de hello instancia tooan en todo momento en el ciclo de vida de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d25e-207">Special care must be taken tooensure that hello reference is set tooan instance at all times in hello service lifecycle.</span></span> <span data-ttu-id="8d25e-208">Hola el Administrador de estado confiable administra este trabajo automáticamente, y está optimizado para la repetición de visitas.</span><span class="sxs-lookup"><span data-stu-id="8d25e-208">hello Reliable State Manager handles this work for you, and it's optimized for repeat visits.</span></span>

### <a name="transactional-and-asynchronous-operations"></a><span data-ttu-id="8d25e-209">Operaciones transaccionales y asincrónicas</span><span class="sxs-lookup"><span data-stu-id="8d25e-209">Transactional and asynchronous operations</span></span>
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

<span data-ttu-id="8d25e-210">Colecciones confiables tienen muchas Hola mismas operaciones que sus `System.Collections.Generic` y `System.Collections.Concurrent` homólogos, excepto LINQ.</span><span class="sxs-lookup"><span data-stu-id="8d25e-210">Reliable Collections have many of hello same operations that their `System.Collections.Generic` and `System.Collections.Concurrent` counterparts do, except LINQ.</span></span> <span data-ttu-id="8d25e-211">Sin embargo, las operaciones relacionadas con Reliable Collections son asincrónicas.</span><span class="sxs-lookup"><span data-stu-id="8d25e-211">Operations on Reliable Collections are asynchronous.</span></span> <span data-ttu-id="8d25e-212">Esto es porque las operaciones de escritura con colecciones de confianza realizan tooreplicate de las operaciones de E/S y conservan datos toodisk.</span><span class="sxs-lookup"><span data-stu-id="8d25e-212">This is because write operations with Reliable Collections perform I/O operations tooreplicate and persist data toodisk.</span></span>

<span data-ttu-id="8d25e-213">Las operaciones de Reliable Collections son *transaccionales*, de modo que el estado puede mantenerse de forma coherente entre varias operaciones y colecciones Reliable Collections.</span><span class="sxs-lookup"><span data-stu-id="8d25e-213">Reliable Collection operations are *transactional*, so that you can keep state consistent across multiple Reliable Collections and operations.</span></span> <span data-ttu-id="8d25e-214">Por ejemplo, puede quitar de la cola un elemento de trabajo de una cola confiable, realizar una operación en él y guardar el resultado de hello en un diccionario confiable, todo dentro de una sola transacción.</span><span class="sxs-lookup"><span data-stu-id="8d25e-214">For example, you may dequeue a work item from a Reliable Queue, perform an operation on it, and save hello result in a Reliable Dictionary, all within a single transaction.</span></span> <span data-ttu-id="8d25e-215">Se trata como una operación atómica, y garantiza que se realizará correctamente la operación completa de Hola o se revertirá la operación completa de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d25e-215">This is treated as an atomic operation, and it guarantees that either hello entire operation will succeed or hello entire operation will roll back.</span></span> <span data-ttu-id="8d25e-216">Si se produce un error después de dequeue elemento Hola pero antes de guardar el resultado de hello, se revierte la transacción entera de Hola y elemento de hello permanece en la cola de Hola para su procesamiento.</span><span class="sxs-lookup"><span data-stu-id="8d25e-216">If an error occurs after you dequeue hello item but before you save hello result, hello entire transaction is rolled back and hello item remains in hello queue for processing.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="8d25e-217">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="8d25e-217">Run hello application</span></span>
<span data-ttu-id="8d25e-218">Devolvemos ahora toohello *HelloWorld* aplicación.</span><span class="sxs-lookup"><span data-stu-id="8d25e-218">We now return toohello *HelloWorld* application.</span></span> <span data-ttu-id="8d25e-219">Ahora puede compilar e implementar sus servicios.</span><span class="sxs-lookup"><span data-stu-id="8d25e-219">You can now build and deploy your services.</span></span> <span data-ttu-id="8d25e-220">Cuando se presiona **F5**, la aplicación será el clúster local tooyour compilado e implementado.</span><span class="sxs-lookup"><span data-stu-id="8d25e-220">When you press **F5**, your application will be built and deployed tooyour local cluster.</span></span>

<span data-ttu-id="8d25e-221">Después de hello de servicios de inicio que se ejecuta, puede ver Hola genera eventos de seguimiento de eventos para Windows (ETW) en un **eventos de diagnóstico** ventana.</span><span class="sxs-lookup"><span data-stu-id="8d25e-221">After hello services start running, you can view hello generated Event Tracing for Windows (ETW) events in a **Diagnostic Events** window.</span></span> <span data-ttu-id="8d25e-222">Tenga en cuenta que los eventos de hello muestra del servicio sin estado de Hola y Hola servicio con estado en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="8d25e-222">Note that hello events displayed are from both hello stateless service and hello stateful service in hello application.</span></span> <span data-ttu-id="8d25e-223">Puede pausar flujo Hola haciendo clic en hello **pausar** botón.</span><span class="sxs-lookup"><span data-stu-id="8d25e-223">You can pause hello stream by clicking hello **Pause** button.</span></span> <span data-ttu-id="8d25e-224">A continuación, puede examinar detalles Hola de un mensaje al expandir ese mensaje.</span><span class="sxs-lookup"><span data-stu-id="8d25e-224">You can then examine hello details of a message by expanding that message.</span></span>

> [!NOTE]
> <span data-ttu-id="8d25e-225">Antes de ejecutar la aplicación hello, asegúrese de que tiene un clúster de desarrollo local que se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="8d25e-225">Before you run hello application, make sure that you have a local development cluster running.</span></span> <span data-ttu-id="8d25e-226">Extraer del repositorio hello [Guía de introducción](service-fabric-get-started.md) para obtener información sobre cómo configurar su entorno local.</span><span class="sxs-lookup"><span data-stu-id="8d25e-226">Check out hello [getting started guide](service-fabric-get-started.md) for information on setting up your local environment.</span></span>
> 
> 

![Ver eventos de diagnóstico en Visual Studio](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a><span data-ttu-id="8d25e-228">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8d25e-228">Next steps</span></span>
[<span data-ttu-id="8d25e-229">Depuración de la aplicación del Service Fabric en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8d25e-229">Debug your Service Fabric application in Visual Studio</span></span>](service-fabric-debugging-your-application.md)

[<span data-ttu-id="8d25e-230">Introducción a los servicios de la API web de Microsoft Azure Service Fabric con autohospedaje OWIN</span><span class="sxs-lookup"><span data-stu-id="8d25e-230">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>](service-fabric-reliable-services-communication-webapi.md)

[<span data-ttu-id="8d25e-231">Obtenga más información acerca de las colecciones fiables</span><span class="sxs-lookup"><span data-stu-id="8d25e-231">Learn more about Reliable Collections</span></span>](service-fabric-reliable-services-reliable-collections.md)

[<span data-ttu-id="8d25e-232">Implementar una aplicación</span><span class="sxs-lookup"><span data-stu-id="8d25e-232">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[<span data-ttu-id="8d25e-233">Actualización de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="8d25e-233">Application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="8d25e-234">Referencia para desarrolladores de servicios confiables</span><span class="sxs-lookup"><span data-stu-id="8d25e-234">Developer reference for Reliable Services</span></span>](https://msdn.microsoft.com/library/azure/dn706529.aspx)

