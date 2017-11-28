---
title: "comunicación remota de aaaService de Service Fabric | Documentos de Microsoft"
description: "Comunicación remota de Service Fabric permite a los clientes y servicios toocommunicate con los servicios mediante una llamada a procedimiento remoto."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: abfaf430-fea0-4974-afba-cfc9f9f2354b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: vturecek
ms.openlocfilehash: 14682cf8671a85e04144eccf97803ab67c258875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="418cf-103">Comunicación remota de servicio con Reliable Services</span><span class="sxs-lookup"><span data-stu-id="418cf-103">Service remoting with Reliable Services</span></span>
<span data-ttu-id="418cf-104">Para los servicios que no están vinculados tooa protocolo de comunicación determinada o pila, por ejemplo, WebAPI, Windows Communication Foundation (WCF) u otras personas, el marco de trabajo de hello Services confiable proporciona un tooquickly del mecanismo de comunicación remota y configurar fácilmente la llamada a procedimiento remoto para los servicios.</span><span class="sxs-lookup"><span data-stu-id="418cf-104">For services that are not tied tooa particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, hello Reliable Services framework provides a remoting mechanism tooquickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="418cf-105">Configurar la comunicación remota en un servicio</span><span class="sxs-lookup"><span data-stu-id="418cf-105">Set up remoting on a service</span></span>
<span data-ttu-id="418cf-106">La configuración de la comunicación remota para un servicio se realiza en dos sencillos pasos:</span><span class="sxs-lookup"><span data-stu-id="418cf-106">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="418cf-107">Crear una interfaz para el servicio tooimplement.</span><span class="sxs-lookup"><span data-stu-id="418cf-107">Create an interface for your service tooimplement.</span></span> <span data-ttu-id="418cf-108">Esta interfaz define métodos de Hola que estarán disponibles para una llamada a procedimiento remoto en su servicio.</span><span class="sxs-lookup"><span data-stu-id="418cf-108">This interface defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="418cf-109">métodos de Hello deben ser de devolución de tarea métodos asincrónicos.</span><span class="sxs-lookup"><span data-stu-id="418cf-109">hello methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="418cf-110">debe implementar la interfaz de Hello `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal que Hola servicio tiene una interfaz de comunicación remota.</span><span class="sxs-lookup"><span data-stu-id="418cf-110">hello interface must implement `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal that hello service has a remoting interface.</span></span>
2. <span data-ttu-id="418cf-111">Utilice un agente de escucha de comunicación remota en su servicio.</span><span class="sxs-lookup"><span data-stu-id="418cf-111">Use a remoting listener in your service.</span></span> <span data-ttu-id="418cf-112">Se trata de una implementación de `ICommunicationListener` que ofrece capacidades de comunicación remota.</span><span class="sxs-lookup"><span data-stu-id="418cf-112">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="418cf-113">Hola `Microsoft.ServiceFabric.Services.Remoting.Runtime` espacio de nombres contiene un método de extensión,`CreateServiceRemotingListener` para sin estado y con estado de servicios que puede toocreate usa un agente de escucha de comunicación remota usar protocolo de transporte de comunicación remota de Hola de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="418cf-113">hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contains an extension method,`CreateServiceRemotingListener` for both stateless and stateful services that can be used toocreate a remoting listener using hello default remoting transport protocol.</span></span>

<span data-ttu-id="418cf-114">Nota: Hola `Remoting` espacio de nombres está disponible como un paquete de nuget independiente denominado`Microsoft.ServiceFabric.Services.Remoting`</span><span class="sxs-lookup"><span data-stu-id="418cf-114">Note: hello `Remoting` namespace is available as a seperate nuget package called `Microsoft.ServiceFabric.Services.Remoting`</span></span> 

<span data-ttu-id="418cf-115">Por ejemplo, hello siguiente sin estado servicio expone un único método tooget "¡Hello World" a través de una llamada a procedimiento remoto.</span><span class="sxs-lookup"><span data-stu-id="418cf-115">For example, hello following stateless service exposes a single method tooget "Hello World" over a remote procedure call.</span></span>

```csharp
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Remoting;
using Microsoft.ServiceFabric.Services.Remoting.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

public interface IMyService : IService
{
    Task<string> HelloWorldAsync();
}

class MyService : StatelessService, IMyService
{
    public MyService(StatelessServiceContext context)
        : base (context)
    {
    }

    public Task HelloWorldAsync()
    {
        return Task.FromResult("Hello!");
    }

    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] { new ServiceInstanceListener(context =>            this.CreateServiceRemotingListener(context)) };
    }
}
```
> [!NOTE]
> <span data-ttu-id="418cf-116">Hello hello y argumentos devuelven tipos de interfaz de servicio de hello pueden ser cualquier tipo simple, compleja o personalizada, pero deben ser serializables por hello .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="418cf-116">hello arguments and hello return types in hello service interface can be any simple, complex, or custom types, but they must be serializable by hello .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="418cf-117">Llamar a métodos de servicio remoto</span><span class="sxs-lookup"><span data-stu-id="418cf-117">Call remote service methods</span></span>
<span data-ttu-id="418cf-118">Llamadas a métodos en un servicio mediante el uso de la pila de comunicación remota de Hola se realiza mediante un servicio de toohello de proxy local a través de hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` clase.</span><span class="sxs-lookup"><span data-stu-id="418cf-118">Calling methods on a service by using hello remoting stack is done by using a local proxy toohello service through hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class.</span></span> <span data-ttu-id="418cf-119">Hola `ServiceProxy` método crea un proxy local mediante el uso de hello implementa la misma interfaz que Hola servicio.</span><span class="sxs-lookup"><span data-stu-id="418cf-119">hello `ServiceProxy` method creates a local proxy by using hello same interface that hello service implements.</span></span> <span data-ttu-id="418cf-120">Con ese proxy, se puede simplemente llamar a métodos en la interfaz de hello remotamente.</span><span class="sxs-lookup"><span data-stu-id="418cf-120">With that proxy, you can simply call methods on hello interface remotely.</span></span>

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

<span data-ttu-id="418cf-121">el marco de trabajo de Hello remoting propaga las excepciones producidas en el cliente del servicio toohello de Hola.</span><span class="sxs-lookup"><span data-stu-id="418cf-121">hello remoting framework propagates exceptions thrown at hello service toohello client.</span></span> <span data-ttu-id="418cf-122">Lógica de control de excepciones por lo que en el cliente de hello mediante el uso de `ServiceProxy` directamente puede controlar las excepciones que Hola servicio inicia.</span><span class="sxs-lookup"><span data-stu-id="418cf-122">So exception-handling logic at hello client by using `ServiceProxy` can directly handle exceptions that hello service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="418cf-123">Duración del proxy de servicio</span><span class="sxs-lookup"><span data-stu-id="418cf-123">Service Proxy Lifetime</span></span>
<span data-ttu-id="418cf-124">La creación de ServiceProxy es una operación ligera, por lo que el usuario puede crearla todas las veces que lo necesite.</span><span class="sxs-lookup"><span data-stu-id="418cf-124">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="418cf-125">El proxy de servicio puede volver a usarse siempre que el usuario lo necesite.</span><span class="sxs-lookup"><span data-stu-id="418cf-125">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="418cf-126">Usuario pueda volver a utilizar Hola mismo proxy en el caso de excepción.</span><span class="sxs-lookup"><span data-stu-id="418cf-126">User can re-use hello same proxy in case of Exception.</span></span> <span data-ttu-id="418cf-127">Cada ServiceProxy contiene mensajes de toosend de cliente que se utiliza la comunicación a través de la conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="418cf-127">Each ServiceProxy contains communciation client used toosend messages over hello wire.</span></span> <span data-ttu-id="418cf-128">Al invocar la API, tenemos toosee comprobación interna si el cliente de comunicación que se utiliza es válido.</span><span class="sxs-lookup"><span data-stu-id="418cf-128">While invoking API, we have internal check toosee if communication client used is valid.</span></span> <span data-ttu-id="418cf-129">En función de ese resultado, se vuelva a crea a cliente de comunicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="418cf-129">Based on that result, we re-create hello communication client.</span></span> <span data-ttu-id="418cf-130">Por lo tanto, el usuario no es necesario toorecreate serviceproxy en caso de excepción.</span><span class="sxs-lookup"><span data-stu-id="418cf-130">Hence user do not need toorecreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="418cf-131">Duración de ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="418cf-131">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="418cf-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) es una fábrica que crea un proxy para interfaces remotas diferentes.</span><span class="sxs-lookup"><span data-stu-id="418cf-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="418cf-133">Si utilizas API ServiceProxy.Create para crear el proxy, el marco de trabajo crea hello singelton ServiceProxyFactory.</span><span class="sxs-lookup"><span data-stu-id="418cf-133">If you use API ServiceProxy.Create for creating proxy, then framework creates hello singelton ServiceProxyFactory.</span></span>
<span data-ttu-id="418cf-134">Resulta útil toocreate uno manualmente cuando necesite toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) propiedades.</span><span class="sxs-lookup"><span data-stu-id="418cf-134">It is useful toocreate one manually when you need toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) properties.</span></span>
<span data-ttu-id="418cf-135">Factory es una operación costosa.</span><span class="sxs-lookup"><span data-stu-id="418cf-135">Factory is an expensive operation.</span></span> <span data-ttu-id="418cf-136">ServiceProxyFactory mantiene la memoria caché del cliente de comunicación.</span><span class="sxs-lookup"><span data-stu-id="418cf-136">ServiceProxyFactory maintains cache of communication client.</span></span>
<span data-ttu-id="418cf-137">Procedimiento recomendado es toocache ServiceProxyFactory tanto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="418cf-137">Best practice is toocache ServiceProxyFactory for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="418cf-138">Control de excepciones remota</span><span class="sxs-lookup"><span data-stu-id="418cf-138">Remoting Exception Handling</span></span>
<span data-ttu-id="418cf-139">Todos los Hola remoto excepción API del servicio, se envían cliente toohello espera como AggregateException.</span><span class="sxs-lookup"><span data-stu-id="418cf-139">All hello remote exception thrown by service API, are sent back toohello client as AggregateException.</span></span> <span data-ttu-id="418cf-140">RemoteExceptions debe ser Serializable de DataContract en caso contrario, [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) se produce toohello proxy API con error de serialización de hello en ella.</span><span class="sxs-lookup"><span data-stu-id="418cf-140">RemoteExceptions should be DataContract Serializable otherwise [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) is thrown toohello proxy API with hello serialization error in it.</span></span>

<span data-ttu-id="418cf-141">ServiceProxy controlar todas las excepciones de conmutación por error para la partición de servicio de Hola se crea para.</span><span class="sxs-lookup"><span data-stu-id="418cf-141">ServiceProxy does handle all Failover Exception for hello service partition it  is created for.</span></span> <span data-ttu-id="418cf-142">Volver a resuelve los puntos de conexión de hello si hay Failover Exceptions(Non-Transient Exceptions) y reintentos llamada Hola con punto de conexión correcto Hola.</span><span class="sxs-lookup"><span data-stu-id="418cf-142">It re-resolves hello endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries hello call with hello correct endpoint.</span></span> <span data-ttu-id="418cf-143">El número de reintentos para la excepción de conmutación por error es indefinido.</span><span class="sxs-lookup"><span data-stu-id="418cf-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="418cf-144">En el caso de TransientExceptions, solo reintenta llamada Hola.</span><span class="sxs-lookup"><span data-stu-id="418cf-144">In case of TransientExceptions, it only retries hello call.</span></span>

<span data-ttu-id="418cf-145">[OperationRetrySettings] proporciona los parámetros de reintento predeterminados.</span><span class="sxs-lookup"><span data-stu-id="418cf-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="418cf-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) Usuario puede configurar estos valores pasando OperationRetrySettings objeto tooServiceProxyFactory constructor.</span><span class="sxs-lookup"><span data-stu-id="418cf-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) User can configure these values by passing OperationRetrySettings object tooServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="418cf-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="418cf-147">Next steps</span></span>
* [<span data-ttu-id="418cf-148">Web API con OWIN en Reliable Services</span><span class="sxs-lookup"><span data-stu-id="418cf-148">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="418cf-149">Comunicación WCF con Reliable Services</span><span class="sxs-lookup"><span data-stu-id="418cf-149">WCF communication with Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* [<span data-ttu-id="418cf-150">Protección de la comunicación para Reliable Services</span><span class="sxs-lookup"><span data-stu-id="418cf-150">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
