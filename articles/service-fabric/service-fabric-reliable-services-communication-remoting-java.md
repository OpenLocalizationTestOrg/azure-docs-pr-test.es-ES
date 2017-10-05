---
title: "Comunicación remota en Azure Service Fabric | Microsoft Docs"
description: "La comunicación remota de Service Fabric permite a los clientes y servicios comunicarse con los servicios mediante la llamada a procedimiento remoto."
services: service-fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/30/2017
ms.author: pakunapa
ms.openlocfilehash: dc4a362b5737bb424ca2c196c85f4c51b6ee5e30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="22621-103">Comunicación remota de servicio con Reliable Services</span><span class="sxs-lookup"><span data-stu-id="22621-103">Service remoting with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="22621-104">C# en Windows</span><span class="sxs-lookup"><span data-stu-id="22621-104">C# on Windows</span></span>](service-fabric-reliable-services-communication-remoting.md)
> * [<span data-ttu-id="22621-105">Java en Linux</span><span class="sxs-lookup"><span data-stu-id="22621-105">Java on Linux</span></span>](service-fabric-reliable-services-communication-remoting-java.md)
>
>

<span data-ttu-id="22621-106">La plataforma Reliable Services proporciona un mecanismo de comunicación remota para configurar de un modo rápido y sencillo la llamada a procedimiento remoto para los servicios.</span><span class="sxs-lookup"><span data-stu-id="22621-106">The Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="22621-107">Configurar la comunicación remota en un servicio</span><span class="sxs-lookup"><span data-stu-id="22621-107">Set up remoting on a service</span></span>
<span data-ttu-id="22621-108">La configuración de la comunicación remota para un servicio se realiza en dos sencillos pasos:</span><span class="sxs-lookup"><span data-stu-id="22621-108">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="22621-109">Cree una interfaz para que la implemente su servicio.</span><span class="sxs-lookup"><span data-stu-id="22621-109">Create an interface for your service to implement.</span></span> <span data-ttu-id="22621-110">Esta interfaz define los métodos que están disponibles para la llamada a procedimiento remoto en el servicio.</span><span class="sxs-lookup"><span data-stu-id="22621-110">This interface defines the methods that are available for a remote procedure call on your service.</span></span> <span data-ttu-id="22621-111">Los métodos deben ser métodos asincrónicos que devuelven tareas.</span><span class="sxs-lookup"><span data-stu-id="22621-111">The methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="22621-112">La interfaz debe implementar `microsoft.serviceFabric.services.remoting.Service` para indicar que el servicio tiene una interfaz de comunicación remota.</span><span class="sxs-lookup"><span data-stu-id="22621-112">The interface must implement `microsoft.serviceFabric.services.remoting.Service` to signal that the service has a remoting interface.</span></span>
2. <span data-ttu-id="22621-113">Utilice un agente de escucha de comunicación remota en su servicio.</span><span class="sxs-lookup"><span data-stu-id="22621-113">Use a remoting listener in your service.</span></span> <span data-ttu-id="22621-114">Se trata de una implementación de `CommunicationListener` que ofrece capacidades de comunicación remota.</span><span class="sxs-lookup"><span data-stu-id="22621-114">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="22621-115">`FabricTransportServiceRemotingListener` puede utilizarse para crear un agente de escucha de comunicación remota con el protocolo de transporte de comunicación remota predeterminado.</span><span class="sxs-lookup"><span data-stu-id="22621-115">`FabricTransportServiceRemotingListener` can be used to create a remoting listener using the default remoting transport protocol.</span></span>

<span data-ttu-id="22621-116">Por ejemplo, el siguiente servicio sin estado expone un método único para obtener "Hello World" a través de la llamada a procedimiento remoto:</span><span class="sxs-lookup"><span data-stu-id="22621-116">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span></span>

```java
import java.util.ArrayList;
import java.util.concurrent.CompletableFuture;
import java.util.List;
import microsoft.servicefabric.services.communication.runtime.ServiceInstanceListener;
import microsoft.servicefabric.services.remoting.Service;
import microsoft.servicefabric.services.runtime.StatelessService;

public interface MyService extends Service {
    CompletableFuture<String> helloWorldAsync();
}

class MyServiceImpl extends StatelessService implements MyService {
    public MyServiceImpl(StatelessServiceContext context) {
       super(context);
    }

    public CompletableFuture<String> helloWorldAsync() {
        return CompletableFuture.completedFuture("Hello!");
    }

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
        listeners.add(new ServiceInstanceListener((context) -> {
            return new FabricTransportServiceRemotingListener(context,this);
        }));
        return listeners;
    }
}
```

> [!NOTE]
> <span data-ttu-id="22621-117">Los argumentos y los tipos devueltos en la interfaz de servicio pueden ser cualquier tipo simple, complejo o personalizado, pero deben ser serializables.</span><span class="sxs-lookup"><span data-stu-id="22621-117">The arguments and the return types in the service interface can be any simple, complex, or custom types, but they must be serializable.</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="22621-118">Llamar a métodos de servicio remoto</span><span class="sxs-lookup"><span data-stu-id="22621-118">Call remote service methods</span></span>
<span data-ttu-id="22621-119">La llamada a métodos en un servicio con la pila de comunicación remota se realiza mediante un proxy local al servicio a través de la clase `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` .</span><span class="sxs-lookup"><span data-stu-id="22621-119">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span></span> <span data-ttu-id="22621-120">El método `ServiceProxyBase` crea un proxy local con la misma interfaz que implementa el servicio.</span><span class="sxs-lookup"><span data-stu-id="22621-120">The `ServiceProxyBase` method creates a local proxy by using the same interface that the service implements.</span></span> <span data-ttu-id="22621-121">Con ese proxy, puede llamar simplemente a los métodos en la interfaz de forma remota.</span><span class="sxs-lookup"><span data-stu-id="22621-121">With that proxy, you can simply call methods on the interface remotely.</span></span>

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

<span data-ttu-id="22621-122">El marco de trabajo de comunicación remota propaga las excepciones generadas en el servicio al cliente.</span><span class="sxs-lookup"><span data-stu-id="22621-122">The remoting framework propagates exceptions thrown at the service to the client.</span></span> <span data-ttu-id="22621-123">Por lo tanto, la lógica de control de excepciones en el cliente mediante `ServiceProxyBase` puede controlar excepciones directamente que el servicio genera.</span><span class="sxs-lookup"><span data-stu-id="22621-123">So exception-handling logic at the client by using `ServiceProxyBase` can directly handle exceptions that the service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="22621-124">Duración del proxy de servicio</span><span class="sxs-lookup"><span data-stu-id="22621-124">Service Proxy Lifetime</span></span>
<span data-ttu-id="22621-125">La creación de ServiceProxy es una operación ligera, por lo que el usuario puede crearla todas las veces que lo necesite.</span><span class="sxs-lookup"><span data-stu-id="22621-125">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="22621-126">El proxy de servicio puede volver a usarse siempre que el usuario lo necesite.</span><span class="sxs-lookup"><span data-stu-id="22621-126">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="22621-127">El usuario puede volver a usar el mismo proxy en caso de excepción.</span><span class="sxs-lookup"><span data-stu-id="22621-127">User can re-use the same proxy in case of Exception.</span></span> <span data-ttu-id="22621-128">Cada ServiceProxy contiene un cliente de comunicación que se usa para enviar mensajes a través de la conexión.</span><span class="sxs-lookup"><span data-stu-id="22621-128">Each ServiceProxy contains communication client used to send messages over the wire.</span></span> <span data-ttu-id="22621-129">Al invocar la API, se establece una comprobación interna para ver si el cliente de comunicación usado es válido.</span><span class="sxs-lookup"><span data-stu-id="22621-129">While invoking API, we have internal check to see if communication client used is valid.</span></span> <span data-ttu-id="22621-130">En función de ese resultado, volvemos a crear el cliente de comunicación.</span><span class="sxs-lookup"><span data-stu-id="22621-130">Based on that result, we re-create the communication client.</span></span> <span data-ttu-id="22621-131">Por lo tanto, el usuario no tiene que volver a crear serviceproxy en caso de excepción.</span><span class="sxs-lookup"><span data-stu-id="22621-131">Hence user do not need to recreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="22621-132">Duración de ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="22621-132">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="22621-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) es un tejido que crea un proxy para distintas interfaces remotas.</span><span class="sxs-lookup"><span data-stu-id="22621-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="22621-134">Si usa la API `ServiceProxyBase.create` para crear el proxy, el marco crea un `FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="22621-134">If you use API `ServiceProxyBase.create` for creating proxy, then framework creates a `FabricServiceProxyFactory`.</span></span>
<span data-ttu-id="22621-135">Resulta útil crear uno manualmente cuando necesite invalidar las propiedades [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory).</span><span class="sxs-lookup"><span data-stu-id="22621-135">It is useful to create one manually when you need to override [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) properties.</span></span>
<span data-ttu-id="22621-136">Factory es una operación costosa.</span><span class="sxs-lookup"><span data-stu-id="22621-136">Factory is an expensive operation.</span></span> <span data-ttu-id="22621-137">`FabricServiceProxyFactory` mantiene la memoria caché de los clientes de comunicación.</span><span class="sxs-lookup"><span data-stu-id="22621-137">`FabricServiceProxyFactory` maintains cache of communication clients.</span></span>
<span data-ttu-id="22621-138">El procedimiento recomendado consiste en almacenar `FabricServiceProxyFactory` en caché lo más posible.</span><span class="sxs-lookup"><span data-stu-id="22621-138">Best practice is to cache `FabricServiceProxyFactory` for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="22621-139">Control de excepciones remota</span><span class="sxs-lookup"><span data-stu-id="22621-139">Remoting Exception Handling</span></span>
<span data-ttu-id="22621-140">Toda la excepción remota generada por la API de servicio se vuelve a enviar al cliente como RuntimeException o como FabricException.</span><span class="sxs-lookup"><span data-stu-id="22621-140">All the remote exception thrown by service API, are sent back to the client either as RuntimeException or FabricException.</span></span>

<span data-ttu-id="22621-141">ServiceProxy controla todas las excepciones de conmutación por error para la partición de servicio para la que se crea.</span><span class="sxs-lookup"><span data-stu-id="22621-141">ServiceProxy does handle all Failover Exception for the service partition it  is created for.</span></span> <span data-ttu-id="22621-142">Vuelve a resolver los puntos de conexión si existen excepciones de conmutación por error (excepciones no transitorias) y recupera la llamada con el punto de conexión correcto.</span><span class="sxs-lookup"><span data-stu-id="22621-142">It re-resolves the endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries the call with the correct endpoint.</span></span> <span data-ttu-id="22621-143">El número de reintentos para la excepción de conmutación por error es indefinido.</span><span class="sxs-lookup"><span data-stu-id="22621-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="22621-144">En el caso de TransientExceptions, solo recupera la llamada.</span><span class="sxs-lookup"><span data-stu-id="22621-144">In case of TransientExceptions, it only retries the call.</span></span>

<span data-ttu-id="22621-145">[OperationRetrySettings] proporciona los parámetros de reintento predeterminados.</span><span class="sxs-lookup"><span data-stu-id="22621-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="22621-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) El usuario puede configurar estos valores pasando el objeto OperationRetrySettings al constructor ServiceProxyFactory.</span><span class="sxs-lookup"><span data-stu-id="22621-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) User can configure these values by passing OperationRetrySettings object to ServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22621-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="22621-147">Next steps</span></span>
* [<span data-ttu-id="22621-148">Protección de la comunicación para Reliable Services</span><span class="sxs-lookup"><span data-stu-id="22621-148">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
