---
title: "<span data-ttu-id=\"ff51b-101\">Comunicación remota de servicio en Service Fabric | Microsoft Docs</span><span class=\"sxs-lookup\"><span data-stu-id=\"ff51b-101\">Service remoting in Service Fabric | Microsoft Docs</span></span>"
description: "<span data-ttu-id=\"ff51b-102\">La comunicación remota de Service Fabric permite a los clientes y servicios comunicarse con los servicios mediante la llamada a procedimiento remoto.</span><span class=\"sxs-lookup\"><span data-stu-id=\"ff51b-102\">Service Fabric remoting allows clients and services to communicate with services by using a remote procedure call.</span></span>"
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
ms.openlocfilehash: 92a8894f24c234fbf38eda086531b524cceccfc1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="ff51b-103">Comunicación remota de servicio con Reliable Services</span><span class="sxs-lookup"><span data-stu-id="ff51b-103">Service remoting with Reliable Services</span></span>
<span data-ttu-id="ff51b-104">Para los servicios que no están vinculados a una pila o un protocolo de comunicación concretos, como WebAPI, Windows Communication Foundation (WCF) u otros, el marco de trabajo de Reliable Services ofrece un mecanismo de comunicación remota para configurar de manera rápida y sencilla una llamada a procedimiento remoto para servicios.</span><span class="sxs-lookup"><span data-stu-id="ff51b-104">For services that are not tied to a particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, the Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="ff51b-105">Configurar la comunicación remota en un servicio</span><span class="sxs-lookup"><span data-stu-id="ff51b-105">Set up remoting on a service</span></span>
<span data-ttu-id="ff51b-106">La configuración de la comunicación remota para un servicio se realiza en dos sencillos pasos:</span><span class="sxs-lookup"><span data-stu-id="ff51b-106">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="ff51b-107">Cree una interfaz para que la implemente su servicio.</span><span class="sxs-lookup"><span data-stu-id="ff51b-107">Create an interface for your service to implement.</span></span> <span data-ttu-id="ff51b-108">Esta interfaz define los métodos que estarán disponibles para la llamada a procedimiento remoto en su servicio.</span><span class="sxs-lookup"><span data-stu-id="ff51b-108">This interface defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="ff51b-109">Los métodos deben ser métodos asincrónicos que devuelven tareas.</span><span class="sxs-lookup"><span data-stu-id="ff51b-109">The methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="ff51b-110">La interfaz debe implementar `Microsoft.ServiceFabric.Services.Remoting.IService` para indicar que el servicio tiene una interfaz de comunicación remota.</span><span class="sxs-lookup"><span data-stu-id="ff51b-110">The interface must implement `Microsoft.ServiceFabric.Services.Remoting.IService` to signal that the service has a remoting interface.</span></span>
2. <span data-ttu-id="ff51b-111">Utilice un agente de escucha de comunicación remota en su servicio.</span><span class="sxs-lookup"><span data-stu-id="ff51b-111">Use a remoting listener in your service.</span></span> <span data-ttu-id="ff51b-112">Se trata de una implementación de `ICommunicationListener` que ofrece capacidades de comunicación remota.</span><span class="sxs-lookup"><span data-stu-id="ff51b-112">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="ff51b-113">El espacio de nombres `Microsoft.ServiceFabric.Services.Remoting.Runtime` contiene un método de extensión, `CreateServiceRemotingListener`, para los servicios con y sin estado que pueden utilizarse para crear un agente de escucha de comunicación remota mediante el protocolo de transporte de comunicación remota predeterminado.</span><span class="sxs-lookup"><span data-stu-id="ff51b-113">The `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contains an extension method,`CreateServiceRemotingListener` for both stateless and stateful services that can be used to create a remoting listener using the default remoting transport protocol.</span></span>

<span data-ttu-id="ff51b-114">Nota: El espacio de nombres `Remoting` está disponible como un paquete NuGet independiente denominado `Microsoft.ServiceFabric.Services.Remoting`</span><span class="sxs-lookup"><span data-stu-id="ff51b-114">Note: The `Remoting` namespace is available as a seperate nuget package called `Microsoft.ServiceFabric.Services.Remoting`</span></span> 

<span data-ttu-id="ff51b-115">Por ejemplo, el siguiente servicio sin estado expone un método único para obtener "Hello World" a través de la llamada a procedimiento remoto:</span><span class="sxs-lookup"><span data-stu-id="ff51b-115">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span></span>

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
> <span data-ttu-id="ff51b-116">Los argumentos y los tipos devueltos en la interfaz de servicio pueden ser cualquier tipo simple, complejo o personalizado, pero deben ser serializables por .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff51b-116">The arguments and the return types in the service interface can be any simple, complex, or custom types, but they must be serializable by the .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="ff51b-117">Llamar a métodos de servicio remoto</span><span class="sxs-lookup"><span data-stu-id="ff51b-117">Call remote service methods</span></span>
<span data-ttu-id="ff51b-118">La llamada a métodos en un servicio con la pila de comunicación remota se realiza mediante un proxy local al servicio a través de la clase `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` .</span><span class="sxs-lookup"><span data-stu-id="ff51b-118">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class.</span></span> <span data-ttu-id="ff51b-119">El método `ServiceProxy` crea un proxy local con la misma interfaz que implementa el servicio.</span><span class="sxs-lookup"><span data-stu-id="ff51b-119">The `ServiceProxy` method creates a local proxy by using the same interface that the service implements.</span></span> <span data-ttu-id="ff51b-120">Con ese proxy, puede llamar simplemente a los métodos en la interfaz de forma remota.</span><span class="sxs-lookup"><span data-stu-id="ff51b-120">With that proxy, you can simply call methods on the interface remotely.</span></span>

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

<span data-ttu-id="ff51b-121">El marco de trabajo de comunicación remota propaga las excepciones generadas en el servicio al cliente.</span><span class="sxs-lookup"><span data-stu-id="ff51b-121">The remoting framework propagates exceptions thrown at the service to the client.</span></span> <span data-ttu-id="ff51b-122">Por lo tanto, la lógica de control de excepciones en el cliente mediante `ServiceProxy` puede controlar excepciones directamente que el servicio genera.</span><span class="sxs-lookup"><span data-stu-id="ff51b-122">So exception-handling logic at the client by using `ServiceProxy` can directly handle exceptions that the service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="ff51b-123">Duración del proxy de servicio</span><span class="sxs-lookup"><span data-stu-id="ff51b-123">Service Proxy Lifetime</span></span>
<span data-ttu-id="ff51b-124">La creación de ServiceProxy es una operación ligera, por lo que el usuario puede crearla todas las veces que lo necesite.</span><span class="sxs-lookup"><span data-stu-id="ff51b-124">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="ff51b-125">El proxy de servicio puede volver a usarse siempre que el usuario lo necesite.</span><span class="sxs-lookup"><span data-stu-id="ff51b-125">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="ff51b-126">El usuario puede volver a usar el mismo proxy en caso de excepción.</span><span class="sxs-lookup"><span data-stu-id="ff51b-126">User can re-use the same proxy in case of Exception.</span></span> <span data-ttu-id="ff51b-127">Cada ServiceProxy contiene un cliente de comunicación que se usa para enviar mensajes a través de la conexión.</span><span class="sxs-lookup"><span data-stu-id="ff51b-127">Each ServiceProxy contains communciation client used to send messages over the wire.</span></span> <span data-ttu-id="ff51b-128">Al invocar la API, se establece una comprobación interna para ver si el cliente de comunicación usado es válido.</span><span class="sxs-lookup"><span data-stu-id="ff51b-128">While invoking API, we have internal check to see if communication client used is valid.</span></span> <span data-ttu-id="ff51b-129">En función de ese resultado, volvemos a crear el cliente de comunicación.</span><span class="sxs-lookup"><span data-stu-id="ff51b-129">Based on that result, we re-create the communication client.</span></span> <span data-ttu-id="ff51b-130">Por lo tanto, el usuario no tiene que volver a crear serviceproxy en caso de excepción.</span><span class="sxs-lookup"><span data-stu-id="ff51b-130">Hence user do not need to recreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="ff51b-131">Duración de ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="ff51b-131">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="ff51b-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) es una fábrica que crea un proxy para interfaces remotas diferentes.</span><span class="sxs-lookup"><span data-stu-id="ff51b-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="ff51b-133">Si utiliza ServiceProxy.Create de la API para crear un proxy, el marco de trabajo crea el singelton ServiceProxyFactory.</span><span class="sxs-lookup"><span data-stu-id="ff51b-133">If you use API ServiceProxy.Create for creating proxy, then framework creates the singelton ServiceProxyFactory.</span></span>
<span data-ttu-id="ff51b-134">Es útil crear uno manualmente cuando necesite invalidar las propiedades [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory).</span><span class="sxs-lookup"><span data-stu-id="ff51b-134">It is useful to create one manually when you need to override [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) properties.</span></span>
<span data-ttu-id="ff51b-135">Factory es una operación costosa.</span><span class="sxs-lookup"><span data-stu-id="ff51b-135">Factory is an expensive operation.</span></span> <span data-ttu-id="ff51b-136">ServiceProxyFactory mantiene la memoria caché del cliente de comunicación.</span><span class="sxs-lookup"><span data-stu-id="ff51b-136">ServiceProxyFactory maintains cache of communication client.</span></span>
<span data-ttu-id="ff51b-137">El procedimiento recomendado consiste en almacenar en caché ServiceProxyFactory tanto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="ff51b-137">Best practice is to cache ServiceProxyFactory for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="ff51b-138">Control de excepciones remota</span><span class="sxs-lookup"><span data-stu-id="ff51b-138">Remoting Exception Handling</span></span>
<span data-ttu-id="ff51b-139">Toda la excepción remota generada por la API de servicio se vuelve a enviar al cliente como AggregateException.</span><span class="sxs-lookup"><span data-stu-id="ff51b-139">All the remote exception thrown by service API, are sent back to the client as AggregateException.</span></span> <span data-ttu-id="ff51b-140">RemoteExceptions debe ser DataContract Serializable, en caso contrario, se genera [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) en la API del proxy con el error de serialización en ella.</span><span class="sxs-lookup"><span data-stu-id="ff51b-140">RemoteExceptions should be DataContract Serializable otherwise [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) is thrown to the proxy API with the serialization error in it.</span></span>

<span data-ttu-id="ff51b-141">ServiceProxy controla todas las excepciones de conmutación por error para la partición de servicio para la que se crea.</span><span class="sxs-lookup"><span data-stu-id="ff51b-141">ServiceProxy does handle all Failover Exception for the service partition it  is created for.</span></span> <span data-ttu-id="ff51b-142">Vuelve a resolver los puntos de conexión si existen excepciones de conmutación por error (excepciones no transitorias) y recupera la llamada con el punto de conexión correcto.</span><span class="sxs-lookup"><span data-stu-id="ff51b-142">It re-resolves the endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries the call with the correct endpoint.</span></span> <span data-ttu-id="ff51b-143">El número de reintentos para la excepción de conmutación por error es indefinido.</span><span class="sxs-lookup"><span data-stu-id="ff51b-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="ff51b-144">En el caso de TransientExceptions, solo recupera la llamada.</span><span class="sxs-lookup"><span data-stu-id="ff51b-144">In case of TransientExceptions, it only retries the call.</span></span>

<span data-ttu-id="ff51b-145">[OperationRetrySettings] proporciona los parámetros de reintento predeterminados.</span><span class="sxs-lookup"><span data-stu-id="ff51b-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="ff51b-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) El usuario puede configurar estos valores pasando el objeto OperationRetrySettings al constructor ServiceProxyFactory.</span><span class="sxs-lookup"><span data-stu-id="ff51b-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) User can configure these values by passing OperationRetrySettings object to ServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff51b-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ff51b-147">Next steps</span></span>
* [<span data-ttu-id="ff51b-148">Web API con OWIN en Reliable Services</span><span class="sxs-lookup"><span data-stu-id="ff51b-148">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="ff51b-149">Comunicación WCF con Reliable Services</span><span class="sxs-lookup"><span data-stu-id="ff51b-149">WCF communication with Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* [<span data-ttu-id="ff51b-150">Protección de la comunicación para Reliable Services</span><span class="sxs-lookup"><span data-stu-id="ff51b-150">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
