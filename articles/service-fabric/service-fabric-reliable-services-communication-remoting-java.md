---
title: acceso remoto de aaaService en Azure Service Fabric | Documentos de Microsoft
description: "Comunicación remota de Service Fabric permite a los clientes y servicios toocommunicate con los servicios mediante una llamada a procedimiento remoto."
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
ms.openlocfilehash: 1177a5ede91352dc61422f2df7424b0d5645147d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="913ee-103">Comunicación remota de servicio con Reliable Services</span><span class="sxs-lookup"><span data-stu-id="913ee-103">Service remoting with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="913ee-104">C# en Windows</span><span class="sxs-lookup"><span data-stu-id="913ee-104">C# on Windows</span></span>](service-fabric-reliable-services-communication-remoting.md)
> * [<span data-ttu-id="913ee-105">Java en Linux</span><span class="sxs-lookup"><span data-stu-id="913ee-105">Java on Linux</span></span>](service-fabric-reliable-services-communication-remoting-java.md)
>
>

<span data-ttu-id="913ee-106">el marco de trabajo de Hello Services confiable proporciona un tooquickly del mecanismo de comunicación remota y configurar fácilmente la llamada a procedimiento remoto para los servicios.</span><span class="sxs-lookup"><span data-stu-id="913ee-106">hello Reliable Services framework provides a remoting mechanism tooquickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="913ee-107">Configurar la comunicación remota en un servicio</span><span class="sxs-lookup"><span data-stu-id="913ee-107">Set up remoting on a service</span></span>
<span data-ttu-id="913ee-108">La configuración de la comunicación remota para un servicio se realiza en dos sencillos pasos:</span><span class="sxs-lookup"><span data-stu-id="913ee-108">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="913ee-109">Crear una interfaz para el servicio tooimplement.</span><span class="sxs-lookup"><span data-stu-id="913ee-109">Create an interface for your service tooimplement.</span></span> <span data-ttu-id="913ee-110">Esta interfaz define métodos de Hola que están disponibles para una llamada a procedimiento remoto en su servicio.</span><span class="sxs-lookup"><span data-stu-id="913ee-110">This interface defines hello methods that are available for a remote procedure call on your service.</span></span> <span data-ttu-id="913ee-111">métodos de Hello deben ser de devolución de tarea métodos asincrónicos.</span><span class="sxs-lookup"><span data-stu-id="913ee-111">hello methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="913ee-112">debe implementar la interfaz de Hello `microsoft.serviceFabric.services.remoting.Service` toosignal que Hola servicio tiene una interfaz de comunicación remota.</span><span class="sxs-lookup"><span data-stu-id="913ee-112">hello interface must implement `microsoft.serviceFabric.services.remoting.Service` toosignal that hello service has a remoting interface.</span></span>
2. <span data-ttu-id="913ee-113">Utilice un agente de escucha de comunicación remota en su servicio.</span><span class="sxs-lookup"><span data-stu-id="913ee-113">Use a remoting listener in your service.</span></span> <span data-ttu-id="913ee-114">Se trata de una implementación de `CommunicationListener` que ofrece capacidades de comunicación remota.</span><span class="sxs-lookup"><span data-stu-id="913ee-114">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="913ee-115">`FabricTransportServiceRemotingListener`puede ser toocreate usa un agente de escucha de comunicación remota con protocolo de transporte de comunicación remota de Hola de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="913ee-115">`FabricTransportServiceRemotingListener` can be used toocreate a remoting listener using hello default remoting transport protocol.</span></span>

<span data-ttu-id="913ee-116">Por ejemplo, hello siguiente sin estado servicio expone un único método tooget "¡Hello World" a través de una llamada a procedimiento remoto.</span><span class="sxs-lookup"><span data-stu-id="913ee-116">For example, hello following stateless service exposes a single method tooget "Hello World" over a remote procedure call.</span></span>

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
> <span data-ttu-id="913ee-117">Hola y argumentos de hello devuelven tipos de interfaz de servicio de hello pueden ser cualquier tipo simple, compleja o personalizada, pero deben ser serializables.</span><span class="sxs-lookup"><span data-stu-id="913ee-117">hello arguments and hello return types in hello service interface can be any simple, complex, or custom types, but they must be serializable.</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="913ee-118">Llamar a métodos de servicio remoto</span><span class="sxs-lookup"><span data-stu-id="913ee-118">Call remote service methods</span></span>
<span data-ttu-id="913ee-119">Llamadas a métodos en un servicio mediante el uso de la pila de comunicación remota de Hola se realiza mediante un servicio de toohello de proxy local a través de hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` clase.</span><span class="sxs-lookup"><span data-stu-id="913ee-119">Calling methods on a service by using hello remoting stack is done by using a local proxy toohello service through hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span></span> <span data-ttu-id="913ee-120">Hola `ServiceProxyBase` método crea un proxy local mediante el uso de hello implementa la misma interfaz que Hola servicio.</span><span class="sxs-lookup"><span data-stu-id="913ee-120">hello `ServiceProxyBase` method creates a local proxy by using hello same interface that hello service implements.</span></span> <span data-ttu-id="913ee-121">Con ese proxy, se puede simplemente llamar a métodos en la interfaz de hello remotamente.</span><span class="sxs-lookup"><span data-stu-id="913ee-121">With that proxy, you can simply call methods on hello interface remotely.</span></span>

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

<span data-ttu-id="913ee-122">el marco de trabajo de Hello remoting propaga las excepciones producidas en el cliente del servicio toohello de Hola.</span><span class="sxs-lookup"><span data-stu-id="913ee-122">hello remoting framework propagates exceptions thrown at hello service toohello client.</span></span> <span data-ttu-id="913ee-123">Lógica de control de excepciones por lo que en el cliente de hello mediante el uso de `ServiceProxyBase` directamente puede controlar las excepciones que Hola servicio inicia.</span><span class="sxs-lookup"><span data-stu-id="913ee-123">So exception-handling logic at hello client by using `ServiceProxyBase` can directly handle exceptions that hello service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="913ee-124">Duración del proxy de servicio</span><span class="sxs-lookup"><span data-stu-id="913ee-124">Service Proxy Lifetime</span></span>
<span data-ttu-id="913ee-125">La creación de ServiceProxy es una operación ligera, por lo que el usuario puede crearla todas las veces que lo necesite.</span><span class="sxs-lookup"><span data-stu-id="913ee-125">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="913ee-126">El proxy de servicio puede volver a usarse siempre que el usuario lo necesite.</span><span class="sxs-lookup"><span data-stu-id="913ee-126">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="913ee-127">Usuario pueda volver a utilizar Hola mismo proxy en el caso de excepción.</span><span class="sxs-lookup"><span data-stu-id="913ee-127">User can re-use hello same proxy in case of Exception.</span></span> <span data-ttu-id="913ee-128">Cada ServiceProxy contiene mensajes de toosend de cliente que se utiliza de comunicación a través de la conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="913ee-128">Each ServiceProxy contains communication client used toosend messages over hello wire.</span></span> <span data-ttu-id="913ee-129">Al invocar la API, tenemos toosee comprobación interna si el cliente de comunicación que se utiliza es válido.</span><span class="sxs-lookup"><span data-stu-id="913ee-129">While invoking API, we have internal check toosee if communication client used is valid.</span></span> <span data-ttu-id="913ee-130">En función de ese resultado, se vuelva a crea a cliente de comunicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="913ee-130">Based on that result, we re-create hello communication client.</span></span> <span data-ttu-id="913ee-131">Por lo tanto, el usuario no es necesario toorecreate serviceproxy en caso de excepción.</span><span class="sxs-lookup"><span data-stu-id="913ee-131">Hence user do not need toorecreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="913ee-132">Duración de ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="913ee-132">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="913ee-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) es un tejido que crea un proxy para distintas interfaces remotas.</span><span class="sxs-lookup"><span data-stu-id="913ee-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="913ee-134">Si usa la API `ServiceProxyBase.create` para crear el proxy, el marco crea un `FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="913ee-134">If you use API `ServiceProxyBase.create` for creating proxy, then framework creates a `FabricServiceProxyFactory`.</span></span>
<span data-ttu-id="913ee-135">Resulta útil toocreate uno manualmente cuando necesite toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) propiedades.</span><span class="sxs-lookup"><span data-stu-id="913ee-135">It is useful toocreate one manually when you need toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) properties.</span></span>
<span data-ttu-id="913ee-136">Factory es una operación costosa.</span><span class="sxs-lookup"><span data-stu-id="913ee-136">Factory is an expensive operation.</span></span> <span data-ttu-id="913ee-137">`FabricServiceProxyFactory` mantiene la memoria caché de los clientes de comunicación.</span><span class="sxs-lookup"><span data-stu-id="913ee-137">`FabricServiceProxyFactory` maintains cache of communication clients.</span></span>
<span data-ttu-id="913ee-138">Procedimiento recomendado es toocache `FabricServiceProxyFactory` tanto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="913ee-138">Best practice is toocache `FabricServiceProxyFactory` for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="913ee-139">Control de excepciones remota</span><span class="sxs-lookup"><span data-stu-id="913ee-139">Remoting Exception Handling</span></span>
<span data-ttu-id="913ee-140">Todos los Hola remoto excepción API del servicio, se envían como RuntimeException o FabricException toohello back-cliente.</span><span class="sxs-lookup"><span data-stu-id="913ee-140">All hello remote exception thrown by service API, are sent back toohello client either as RuntimeException or FabricException.</span></span>

<span data-ttu-id="913ee-141">ServiceProxy controlar todas las excepciones de conmutación por error para la partición de servicio de Hola se crea para.</span><span class="sxs-lookup"><span data-stu-id="913ee-141">ServiceProxy does handle all Failover Exception for hello service partition it  is created for.</span></span> <span data-ttu-id="913ee-142">Volver a resuelve los puntos de conexión de hello si hay Failover Exceptions(Non-Transient Exceptions) y reintentos llamada Hola con punto de conexión correcto Hola.</span><span class="sxs-lookup"><span data-stu-id="913ee-142">It re-resolves hello endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries hello call with hello correct endpoint.</span></span> <span data-ttu-id="913ee-143">El número de reintentos para la excepción de conmutación por error es indefinido.</span><span class="sxs-lookup"><span data-stu-id="913ee-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="913ee-144">En el caso de TransientExceptions, solo reintenta llamada Hola.</span><span class="sxs-lookup"><span data-stu-id="913ee-144">In case of TransientExceptions, it only retries hello call.</span></span>

<span data-ttu-id="913ee-145">[OperationRetrySettings] proporciona los parámetros de reintento predeterminados.</span><span class="sxs-lookup"><span data-stu-id="913ee-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="913ee-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) Usuario puede configurar estos valores pasando OperationRetrySettings objeto tooServiceProxyFactory constructor.</span><span class="sxs-lookup"><span data-stu-id="913ee-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) User can configure these values by passing OperationRetrySettings object tooServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="913ee-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="913ee-147">Next steps</span></span>
* [<span data-ttu-id="913ee-148">Protección de la comunicación para Reliable Services</span><span class="sxs-lookup"><span data-stu-id="913ee-148">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
