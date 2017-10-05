---
title: "Información general sobre la comunicación de Reliable Services | Microsoft Docs"
description: "Información general sobre el modelo de comunicación de Reliable Services, incluidos los agentes de escucha de apertura en los servicios, la resolución de puntos de conexión y la comunicación entre servicios."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: 36217988-420e-409d-b0a4-e0e875b6eac8
ms.service: service-fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: b418904f50b772c12bfcdbb95beb9312c8b9fb00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-reliable-services-communication-apis"></a><span data-ttu-id="a0d97-103">Uso de las API de comunicación de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="a0d97-103">How to use the Reliable Services communication APIs</span></span>
<span data-ttu-id="a0d97-104">Azure Service Fabric como una plataforma es completamente independiente de la comunicación entre los servicios.</span><span class="sxs-lookup"><span data-stu-id="a0d97-104">Azure Service Fabric as a platform is completely agnostic about communication between services.</span></span> <span data-ttu-id="a0d97-105">Todos los protocolos y las pilas son aceptables, desde UDP hasta HTTP.</span><span class="sxs-lookup"><span data-stu-id="a0d97-105">All protocols and stacks are acceptable, from UDP to HTTP.</span></span> <span data-ttu-id="a0d97-106">El desarrollador del servicio es quien debe elegir cómo deberían comunicarse los servicios.</span><span class="sxs-lookup"><span data-stu-id="a0d97-106">It's up to the service developer to choose how services should communicate.</span></span> <span data-ttu-id="a0d97-107">El marco de trabajo de aplicaciones de Reliable Services ofrece pilas de comunicación integradas, además de varias API que puede usar para compilar los componentes de comunicación personalizados.</span><span class="sxs-lookup"><span data-stu-id="a0d97-107">The Reliable Services application framework provides built-in communication stacks as well as APIs that you can use to build your custom communication components.</span></span>

## <a name="set-up-service-communication"></a><span data-ttu-id="a0d97-108">Configuración de la comunicación del servicio</span><span class="sxs-lookup"><span data-stu-id="a0d97-108">Set up service communication</span></span>
<span data-ttu-id="a0d97-109">La API de Reliable Services usa una interfaz simple para la comunicación del servicio.</span><span class="sxs-lookup"><span data-stu-id="a0d97-109">The Reliable Services API uses a simple interface for service communication.</span></span> <span data-ttu-id="a0d97-110">Para abrir un punto de conexión para el servicio, solo tiene que implementar esta interfaz:</span><span class="sxs-lookup"><span data-stu-id="a0d97-110">To open an endpoint for your service, simply implement this interface:</span></span>

```csharp

public interface ICommunicationListener
{
    Task<string> OpenAsync(CancellationToken cancellationToken);

    Task CloseAsync(CancellationToken cancellationToken);

    void Abort();
}

```

```java
public interface CommunicationListener {
    CompletableFuture<String> openAsync(CancellationToken cancellationToken);

    CompletableFuture<?> closeAsync(CancellationToken cancellationToken);

    void abort();
}
```

<span data-ttu-id="a0d97-111">Luego puede agregar su implementación del agente de escucha de comunicación devolviéndolo en una invalidación del método de clase basado en el servicio.</span><span class="sxs-lookup"><span data-stu-id="a0d97-111">You can then add your communication listener implementation by returning it in a service-based class method override.</span></span>

<span data-ttu-id="a0d97-112">Para servicios sin estado:</span><span class="sxs-lookup"><span data-stu-id="a0d97-112">For stateless services:</span></span>

```csharp
class MyStatelessService : StatelessService
{
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        ...
    }
    ...
}
```
```java
public class MyStatelessService extends StatelessService {

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ...
    }
    ...
}
```

<span data-ttu-id="a0d97-113">Para servicios con estado:</span><span class="sxs-lookup"><span data-stu-id="a0d97-113">For stateful services:</span></span>

> [!NOTE]
> <span data-ttu-id="a0d97-114">Las instancias con estado de Reliable Services aún no se admiten en Java.</span><span class="sxs-lookup"><span data-stu-id="a0d97-114">Stateful reliable services are not supported in Java yet.</span></span>
>
>

```csharp
class MyStatefulService : StatefulService
{
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        ...
    }
    ...
}
```

<span data-ttu-id="a0d97-115">En ambos casos, devuelve una colección de agentes de escucha.</span><span class="sxs-lookup"><span data-stu-id="a0d97-115">In both cases, you return a collection of listeners.</span></span> <span data-ttu-id="a0d97-116">Esto permite que el servicio escuche en varios puntos de conexión, que posiblemente usen distintos protocolos, mediante el uso de varios agentes de escucha.</span><span class="sxs-lookup"><span data-stu-id="a0d97-116">This allows your service to listen on multiple endpoints, potentially using different protocols, by using multiple listeners.</span></span> <span data-ttu-id="a0d97-117">Por ejemplo, puede tener un agente de escucha HTTP y un agente de escucha de WebSocket independiente.</span><span class="sxs-lookup"><span data-stu-id="a0d97-117">For example, you may have an HTTP listener and a separate WebSocket listener.</span></span> <span data-ttu-id="a0d97-118">Cada agente de escucha recibe un nombre y la colección resultante de los pares *nombre : dirección* se representan como un objeto JSON cuando un cliente solicita las direcciones de escucha para una partición o instancia de servicio.</span><span class="sxs-lookup"><span data-stu-id="a0d97-118">Each listener gets a name, and the resulting collection of *name : address* pairs are represented as a JSON object when a client requests the listening addresses for a service instance or a partition.</span></span>

<span data-ttu-id="a0d97-119">En un servicio sin estado, la invalidación devuelve una colección de ServiceInstanceListeners.</span><span class="sxs-lookup"><span data-stu-id="a0d97-119">In a stateless service, the override returns a collection of ServiceInstanceListeners.</span></span> <span data-ttu-id="a0d97-120">Un elemento `ServiceInstanceListener` contiene una función para crear un `ICommunicationListener(C#) / CommunicationListener(Java)` y le asigna un nombre.</span><span class="sxs-lookup"><span data-stu-id="a0d97-120">A `ServiceInstanceListener` contains a function to create an `ICommunicationListener(C#) / CommunicationListener(Java)` and gives it a name.</span></span> <span data-ttu-id="a0d97-121">Para servicios con estado, la invalidación devuelve una colección de ServiceReplicaListeners.</span><span class="sxs-lookup"><span data-stu-id="a0d97-121">For stateful services, the override returns a collection of ServiceReplicaListeners.</span></span> <span data-ttu-id="a0d97-122">Difiere ligeramente de su homólogo sin estado, porque elemento `ServiceReplicaListener` tiene una opción de abrir un elemento `ICommunicationListener` en las réplicas secundarias.</span><span class="sxs-lookup"><span data-stu-id="a0d97-122">This is slightly different from its stateless counterpart, because a `ServiceReplicaListener` has an option to open an `ICommunicationListener` on secondary replicas.</span></span> <span data-ttu-id="a0d97-123">No solo puede usar varios agentes de escucha de comunicación en un servicio, sino también especificar cuáles aceptan solicitudes en réplicas secundarias y cuáles escuchan solo en las réplicas principales.</span><span class="sxs-lookup"><span data-stu-id="a0d97-123">Not only can you use multiple communication listeners in a service, but you can also specify which listeners accept requests on secondary replicas and which ones listen only on primary replicas.</span></span>

<span data-ttu-id="a0d97-124">Por ejemplo, puede tener una clase ServiceRemotingListener que realice llamadas RPC solo en las réplicas principales, y un segundo agente de escucha personalizado que lea solicitudes en réplicas secundarias a través de HTTP:</span><span class="sxs-lookup"><span data-stu-id="a0d97-124">For example, you can have a ServiceRemotingListener that takes RPC calls only on primary replicas, and a second, custom listener that takes read requests on secondary replicas over HTTP:</span></span>

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[]
    {
        new ServiceReplicaListener(context =>
            new MyCustomHttpListener(context),
            "HTTPReadonlyEndpoint",
            true),

        new ServiceReplicaListener(context =>
            this.CreateServiceRemotingListener(context),
            "rpcPrimaryEndpoint",
            false)
    };
}
```

> [!NOTE]
> <span data-ttu-id="a0d97-125">Cuando se crean varios agentes de escucha para un servicio, se **debe** asignar a cada uno un nombre único.</span><span class="sxs-lookup"><span data-stu-id="a0d97-125">When creating multiple listeners for a service, each listener **must** be given a unique name.</span></span>
>
>

<span data-ttu-id="a0d97-126">Por último, describa los puntos de conexión que se requieren para el servicio en el [manifiesto de servicio](service-fabric-application-model.md) en la sección que trata sobre los puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="a0d97-126">Finally, describe the endpoints that are required for the service in the [service manifest](service-fabric-application-model.md) under the section on endpoints.</span></span>

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

<span data-ttu-id="a0d97-127">El agente de escucha de comunicación puede acceder a los recursos de puntos de conexión asignados a él desde `CodePackageActivationContext` en `ServiceContext`.</span><span class="sxs-lookup"><span data-stu-id="a0d97-127">The communication listener can access the endpoint resources allocated to it from the `CodePackageActivationContext` in the `ServiceContext`.</span></span> <span data-ttu-id="a0d97-128">El agente de escucha luego puede empezar a escuchar las solicitudes cuando se abre.</span><span class="sxs-lookup"><span data-stu-id="a0d97-128">The listener can then start listening for requests when it is opened.</span></span>

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> <span data-ttu-id="a0d97-129">Los recursos de los puntos de conexión son comunes para el paquete de servicio completo y los asigna Service Fabric cuando se activa el paquete de servicio.</span><span class="sxs-lookup"><span data-stu-id="a0d97-129">Endpoint resources are common to the entire service package, and they are allocated by Service Fabric when the service package is activated.</span></span> <span data-ttu-id="a0d97-130">Es posible que varias réplicas hospedadas en el mismo ServiceHost compartan el mismo puerto.</span><span class="sxs-lookup"><span data-stu-id="a0d97-130">Multiple service replicas hosted in the same ServiceHost may share the same port.</span></span> <span data-ttu-id="a0d97-131">Esto significa que el agente de escucha de comunicación debe admitir el uso compartido de puertos.</span><span class="sxs-lookup"><span data-stu-id="a0d97-131">This means that the communication listener should support port sharing.</span></span> <span data-ttu-id="a0d97-132">La manera recomendada de hacerlo es que el agente de escucha de comunicación utilice el identificador de partición y el identificador de instancia o de réplica cuando genera la dirección de escucha.</span><span class="sxs-lookup"><span data-stu-id="a0d97-132">The recommended way of doing this is for the communication listener to use the partition ID and replica/instance ID when it generates the listen address.</span></span>
>
>

### <a name="service-address-registration"></a><span data-ttu-id="a0d97-133">Registro de dirección de servicio</span><span class="sxs-lookup"><span data-stu-id="a0d97-133">Service address registration</span></span>
<span data-ttu-id="a0d97-134">Un servicio del sistema denominado *servicio de nomenclatura* se ejecuta en clústeres de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a0d97-134">A system service called the *Naming Service* runs on Service Fabric clusters.</span></span> <span data-ttu-id="a0d97-135">El servicio de nomenclatura es un registrador de los servicios y sus direcciones que cada instancia o réplica del servicio escucha.</span><span class="sxs-lookup"><span data-stu-id="a0d97-135">The Naming Service is a registrar for services and their addresses that each instance or replica of the service is listening on.</span></span> <span data-ttu-id="a0d97-136">Cuando el método `OpenAsync(C#) / openAsync(Java)` de una interfaz `ICommunicationListener(C#) / CommunicationListener(Java)` se completa, el valor devuelto se registra en el servicio de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="a0d97-136">When the `OpenAsync(C#) / openAsync(Java)` method of an `ICommunicationListener(C#) / CommunicationListener(Java)` completes, its return value gets registered in the Naming Service.</span></span> <span data-ttu-id="a0d97-137">Este valor devuelto que se publica en el servicio de nomenclatura es una cadena que puede no tener ningún valor.</span><span class="sxs-lookup"><span data-stu-id="a0d97-137">This return value that gets published in the Naming Service is a string whose value can be anything at all.</span></span> <span data-ttu-id="a0d97-138">Este valor de cadena es lo que ven los clientes cuando solicitan una dirección para el servicio desde el servicio de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="a0d97-138">This string value is what clients see when they ask for an address for the service from the Naming Service.</span></span>

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.CodePackageActivationContext.GetEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.Port;

    this.listeningAddress = string.Format(
                CultureInfo.InvariantCulture,
                "http://+:{0}/",
                port);

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

    // the string returned here will be published in the Naming Service.
    return Task.FromResult(this.publishAddress);
}
```
```java
public CompletableFuture<String> openAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.getCodePackageActivationContext.getEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.getPort();

    this.publishAddress = String.format("http://%s:%d/", FabricRuntime.getNodeContext().getIpAddressOrFQDN(), port);

    this.webApp = new WebApp(port);
    this.webApp.start();

    /* the string returned here will be published in the Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

<span data-ttu-id="a0d97-139">Service Fabric ofrece varias API que permiten que los clientes y otros servicios soliciten esta dirección por nombre de servicio.</span><span class="sxs-lookup"><span data-stu-id="a0d97-139">Service Fabric provides APIs that allow clients and other services to then ask for this address by service name.</span></span> <span data-ttu-id="a0d97-140">Esto es importante porque la dirección del servicio no es estática.</span><span class="sxs-lookup"><span data-stu-id="a0d97-140">This is important because the service address is not static.</span></span> <span data-ttu-id="a0d97-141">Los servicios se mueven en el clúster para fines de disponibilidad y equilibrio de recursos.</span><span class="sxs-lookup"><span data-stu-id="a0d97-141">Services are moved around in the cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="a0d97-142">Este mecanismo permite a los clientes resolver la dirección de escucha de un servicio.</span><span class="sxs-lookup"><span data-stu-id="a0d97-142">This is the mechanism that allow clients to resolve the listening address for a service.</span></span>

> [!NOTE]
> <span data-ttu-id="a0d97-143">Para ver un tutorial completo sobre cómo escribir un agente de escucha de comunicación, consulte el artículo sobre los [servicios de la API web de Service Fabric con autohospedaje OWIN](service-fabric-reliable-services-communication-webapi.md) para C#, mientras que para Java puede escribir su propia implementación del servidor HTTP; consulte el ejemplo de aplicación de EchoServer en https://github.com/Azure-Samples/service-fabric-java-getting-started.</span><span class="sxs-lookup"><span data-stu-id="a0d97-143">For a complete walk-through of how to write a communication listener, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md) for C#, whereas for Java you can write your own HTTP server implementation, see EchoServer application example at https://github.com/Azure-Samples/service-fabric-java-getting-started.</span></span>
>
>

## <a name="communicating-with-a-service"></a><span data-ttu-id="a0d97-144">Comunicación con un servicio</span><span class="sxs-lookup"><span data-stu-id="a0d97-144">Communicating with a service</span></span>
<span data-ttu-id="a0d97-145">La API de Reliable Services proporciona las bibliotecas siguientes para la escritura de clientes que se comunican con los servicios.</span><span class="sxs-lookup"><span data-stu-id="a0d97-145">The Reliable Services API provides the following libraries to write clients that communicate with services.</span></span>

### <a name="service-endpoint-resolution"></a><span data-ttu-id="a0d97-146">Resolución del punto de conexión de servicio</span><span class="sxs-lookup"><span data-stu-id="a0d97-146">Service endpoint resolution</span></span>
<span data-ttu-id="a0d97-147">El primer paso para la comunicación con un servicio consiste en resolver una dirección de punto de conexión de la partición o la instancia del servicio con el que quiere comunicarse.</span><span class="sxs-lookup"><span data-stu-id="a0d97-147">The first step to communication with a service is to resolve an endpoint address of the partition or instance of the service you want to talk to.</span></span> <span data-ttu-id="a0d97-148">La clase de utilidad `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` es un tipo primitivo básico que ayuda a los clientes a determinar el punto de conexión de un servicio en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="a0d97-148">The `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` utility class is a basic primitive that helps clients determine the endpoint of a service at runtime.</span></span> <span data-ttu-id="a0d97-149">En la terminología de Service Fabric, el proceso de determinar el punto de conexión de un servicio se denomina *resolución de punto de conexión de servicio*.</span><span class="sxs-lookup"><span data-stu-id="a0d97-149">In Service Fabric terminology, the process of determining the endpoint of a service is referred to as the *service endpoint resolution*.</span></span>

<span data-ttu-id="a0d97-150">Para conectarse a servicios en un mismo clúster, se puede crear ServicePartitionResolver con la configuración predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a0d97-150">To connect to services within a cluster, ServicePartitionResolver can be created using default settings.</span></span> <span data-ttu-id="a0d97-151">Este es el uso recomendado para la mayoría de las situaciones:</span><span class="sxs-lookup"><span data-stu-id="a0d97-151">This is the recommended usage for most situations:</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

<span data-ttu-id="a0d97-152">Para conectarse a servicios en otro clúster, se puede crear ServicePartitionResolver con un conjunto de puntos de conexión de puerta de enlace del clúster.</span><span class="sxs-lookup"><span data-stu-id="a0d97-152">To connect to services in a different cluster, a ServicePartitionResolver can be created with a set of cluster gateway endpoints.</span></span> <span data-ttu-id="a0d97-153">Tenga en cuenta que los puntos de conexión de puerta de enlace son solo distintos puntos de conexión para conectarse al mismo clúster.</span><span class="sxs-lookup"><span data-stu-id="a0d97-153">Note that gateway endpoints are just different endpoints for connecting to the same cluster.</span></span> <span data-ttu-id="a0d97-154">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a0d97-154">For example:</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

<span data-ttu-id="a0d97-155">Como alternativa, puede asignarse una función a `ServicePartitionResolver` para crear un objeto `FabricClient` para uso interno:</span><span class="sxs-lookup"><span data-stu-id="a0d97-155">Alternatively, `ServicePartitionResolver` can be given a function for creating a `FabricClient` to use internally:</span></span>

```csharp
public delegate FabricClient CreateFabricClientDelegate();
```
```java
public FabricServicePartitionResolver(CreateFabricClient createFabricClient) {
...
}

public interface CreateFabricClient {
    public FabricClient getFabricClient();
}
```

<span data-ttu-id="a0d97-156">`FabricClient` es el objeto que se utiliza para comunicarse con el clúster de Service Fabric para realizar diversas operaciones de administración en el clúster.</span><span class="sxs-lookup"><span data-stu-id="a0d97-156">`FabricClient` is the object that is used to communicate with the Service Fabric cluster for various management operations on the cluster.</span></span> <span data-ttu-id="a0d97-157">Esto resulta útil cuando se desea tener más control sobre cómo interactúa la resolución de la partición del servicio con el clúster.</span><span class="sxs-lookup"><span data-stu-id="a0d97-157">This is useful when you want more control over how a service partition resolver interacts with your cluster.</span></span> <span data-ttu-id="a0d97-158">`FabricClient` realiza el almacenamiento en caché internamente y, por lo general, su creación es más costosa, por lo que es importante reutilizar instancias de `FabricClient` tantas veces como sea posible.</span><span class="sxs-lookup"><span data-stu-id="a0d97-158">`FabricClient` performs caching internally and is generally expensive to create, so it is important to reuse `FabricClient` instances as much as possible.</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

<span data-ttu-id="a0d97-159">Luego se usa un método de resolución para recuperar la dirección de un servicio o una partición de servicio en el caso de los servicios con particiones.</span><span class="sxs-lookup"><span data-stu-id="a0d97-159">A resolve method is then used to retrieve the address of a service or a service partition for partitioned services.</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();

ResolvedServicePartition partition =
    await resolver.ResolveAsync(new Uri("fabric:/MyApp/MyService"), new ServicePartitionKey(), cancellationToken);
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();

CompletableFuture<ResolvedServicePartition> partition =
    resolver.resolveAsync(new URI("fabric:/MyApp/MyService"), new ServicePartitionKey());
```

<span data-ttu-id="a0d97-160">Una dirección de servicio se puede resolver fácilmente con una clase ServicePartitionResolver, pero se requiere más trabajo para garantizar que la dirección resuelta puede usarse correctamente.</span><span class="sxs-lookup"><span data-stu-id="a0d97-160">A service address can be resolved easily using a ServicePartitionResolver, but more work is required to ensure the resolved address can be used correctly.</span></span> <span data-ttu-id="a0d97-161">El cliente tiene que detectar si el intento de conexión no se realizó debido a un error transitorio y se puede volver a intentar (por ejemplo, el servicio se movió o no está disponible temporalmente) o se debe a un error permanente (por ejemplo, el servicio se eliminó o el recurso solicitado ya no existe).</span><span class="sxs-lookup"><span data-stu-id="a0d97-161">Your client needs to detect whether the connection attempt failed because of a transient error and can be retried (e.g., service moved or is temporarily unavailable), or a permanent error (e.g., service was deleted or the requested resource no longer exists).</span></span> <span data-ttu-id="a0d97-162">Las instancias o réplicas de servicio pueden moverse siempre de un nodo a otro por varios motivos.</span><span class="sxs-lookup"><span data-stu-id="a0d97-162">Service instances or replicas can move around from node to node at any time for multiple reasons.</span></span> <span data-ttu-id="a0d97-163">La dirección de servicio que se resuelve a través de ServicePartitionResolver puede estar obsoleta en el momento en que el código de cliente intenta conectarse.</span><span class="sxs-lookup"><span data-stu-id="a0d97-163">The service address resolved through ServicePartitionResolver may be stale by the time your client code attempts to connect.</span></span> <span data-ttu-id="a0d97-164">En ese caso, el cliente tiene que volver a resolver la dirección.</span><span class="sxs-lookup"><span data-stu-id="a0d97-164">In that case again the client needs to re-resolve the address.</span></span> <span data-ttu-id="a0d97-165">Al proporcionar la clase `ResolvedServicePartition` anterior, se indica que es necesario volver a intentar la resolución en lugar de simplemente recuperar una dirección en caché.</span><span class="sxs-lookup"><span data-stu-id="a0d97-165">Providing the previous `ResolvedServicePartition` indicates that the resolver needs to try again rather than simply retrieve a cached address.</span></span>

<span data-ttu-id="a0d97-166">Normalmente, el código de cliente no necesita trabajar directamente con ServicePartitionResolver.</span><span class="sxs-lookup"><span data-stu-id="a0d97-166">Typically, the client code need not work with the ServicePartitionResolver directly.</span></span> <span data-ttu-id="a0d97-167">Se crea y se pasa a otras fábricas de cliente de comunicación en la API de Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="a0d97-167">It is created and passed on to communication client factories in the Reliable Services API.</span></span> <span data-ttu-id="a0d97-168">Las fábricas usan la resolución internamente para generar un objeto de cliente que puede utilizarse para comunicarse con servicios.</span><span class="sxs-lookup"><span data-stu-id="a0d97-168">The factories use the resolver internally to generate a client object that can be used to communicate with services.</span></span>

### <a name="communication-clients-and-factories"></a><span data-ttu-id="a0d97-169">Fábricas y clientes de comunicación</span><span class="sxs-lookup"><span data-stu-id="a0d97-169">Communication clients and factories</span></span>
<span data-ttu-id="a0d97-170">La biblioteca de fábrica de comunicación implementa un patrón de reintento típico de control de errores que simplifica el reintento de conexiones en puntos de conexión de servicio resueltos.</span><span class="sxs-lookup"><span data-stu-id="a0d97-170">The communication factory library implements a typical fault-handling retry pattern that makes retrying connections to resolved service endpoints easier.</span></span> <span data-ttu-id="a0d97-171">La biblioteca de fábrica proporciona el mecanismo de reintento, mientras que usted proporciona los controladores de errores.</span><span class="sxs-lookup"><span data-stu-id="a0d97-171">The factory library provides the retry mechanism while you provide the error handlers.</span></span>

<span data-ttu-id="a0d97-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` define la interfaz base que implementa una fábrica de cliente de comunicación que genera clientes que pueden comunicarse con un servicio de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a0d97-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` defines the base interface implemented by a communication client factory that produces clients that can talk to a Service Fabric service.</span></span> <span data-ttu-id="a0d97-173">La implementación de CommunicationClientFactory depende de la pila de comunicación que el servicio de Service Fabric utiliza donde el cliente desea comunicarse.</span><span class="sxs-lookup"><span data-stu-id="a0d97-173">The implementation of the CommunicationClientFactory depends on the communication stack used by the Service Fabric service where the client wants to communicate.</span></span> <span data-ttu-id="a0d97-174">La API de Reliable Services ofrece una instancia de `CommunicationClientFactoryBase<TCommunicationClient>`.</span><span class="sxs-lookup"><span data-stu-id="a0d97-174">The Reliable Services API provides a `CommunicationClientFactoryBase<TCommunicationClient>`.</span></span> <span data-ttu-id="a0d97-175">Esto proporciona una implementación base de la interfaz CommunicationClientFactory y realiza tareas comunes a todas las pilas de comunicación.</span><span class="sxs-lookup"><span data-stu-id="a0d97-175">This provides a base implementation of the CommunicationClientFactory interface and performs tasks that are common to all the communication stacks.</span></span> <span data-ttu-id="a0d97-176">(Estas tareas incluyen el uso de un ServicePartitionResolver para determinar el punto de conexión de servicio).</span><span class="sxs-lookup"><span data-stu-id="a0d97-176">(These tasks include using a ServicePartitionResolver to determine the service endpoint).</span></span> <span data-ttu-id="a0d97-177">Normalmente, los clientes implementan la clase CommunicationClientFactoryBase abstracta para controlar la lógica específica de la pila de comunicación.</span><span class="sxs-lookup"><span data-stu-id="a0d97-177">Clients usually implement the abstract CommunicationClientFactoryBase class to handle logic that is specific to the communication stack.</span></span>

<span data-ttu-id="a0d97-178">El cliente de comunicación solo recibe una dirección y la usa para conectarse a un servicio.</span><span class="sxs-lookup"><span data-stu-id="a0d97-178">The communication client just receives an address and uses it to connect to a service.</span></span> <span data-ttu-id="a0d97-179">El cliente puede utilizar el protocolo que quiera.</span><span class="sxs-lookup"><span data-stu-id="a0d97-179">The client can use whatever protocol it wants.</span></span>

```csharp
class MyCommunicationClient : ICommunicationClient
{
    public ResolvedServiceEndpoint Endpoint { get; set; }

    public string ListenerName { get; set; }

    public ResolvedServicePartition ResolvedServicePartition { get; set; }
}
```
```java
public class MyCommunicationClient implements CommunicationClient {

    private ResolvedServicePartition resolvedServicePartition;
    private String listenerName;
    private ResolvedServiceEndpoint endPoint;

    /*
     * Getters and Setters
     */
}
```

<span data-ttu-id="a0d97-180">La fábrica de cliente es la principal responsable de crear clientes de comunicación.</span><span class="sxs-lookup"><span data-stu-id="a0d97-180">The client factory is primarily responsible for creating communication clients.</span></span> <span data-ttu-id="a0d97-181">En el caso de los clientes que no mantienen una conexión persistente, como un cliente HTTP, la fábrica solo tiene que crear y devolver el cliente.</span><span class="sxs-lookup"><span data-stu-id="a0d97-181">For clients that don't maintain a persistent connection, such as an HTTP client, the factory only needs to create and return the client.</span></span> <span data-ttu-id="a0d97-182">La fábrica también debe validar otros protocolos que mantienen una conexión persistente, como algunos de los protocolos binarios, para determinar si la conexión debe volver a crearse.</span><span class="sxs-lookup"><span data-stu-id="a0d97-182">Other protocols that maintain a persistent connection, such as some binary protocols, should also be validated by the factory to determine whether the connection needs to be re-created.</span></span>  

```csharp
public class MyCommunicationClientFactory : CommunicationClientFactoryBase<MyCommunicationClient>
{
    protected override void AbortClient(MyCommunicationClient client)
    {
    }

    protected override Task<MyCommunicationClient> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
    {
    }

    protected override bool ValidateClient(MyCommunicationClient clientChannel)
    {
    }

    protected override bool ValidateClient(string endpoint, MyCommunicationClient client)
    {
    }
}
```
```java
public class MyCommunicationClientFactory extends CommunicationClientFactoryBase<MyCommunicationClient> {

    @Override
    protected boolean validateClient(MyCommunicationClient clientChannel) {
    }

    @Override
    protected boolean validateClient(String endpoint, MyCommunicationClient client) {
    }

    @Override
    protected CompletableFuture<MyCommunicationClient> createClientAsync(String endpoint) {
    }

    @Override
    protected void abortClient(MyCommunicationClient client) {
    }
}
```

<span data-ttu-id="a0d97-183">Por último, un controlador de excepciones es responsable de determinar la acción que hay que realizar cuando se produce una excepción.</span><span class="sxs-lookup"><span data-stu-id="a0d97-183">Finally, an exception handler is responsible for determining what action to take when an exception occurs.</span></span> <span data-ttu-id="a0d97-184">Las excepciones se dividen en dos categorías, las que **se pueden volver a intentar** y las que **no se pueden volver a intentar**.</span><span class="sxs-lookup"><span data-stu-id="a0d97-184">Exceptions are categorized into **retryable** and **non retryable**.</span></span>

* <span data-ttu-id="a0d97-185">Las que **se pueden volver a intentar** simplemente se reenvían al autor de la llamada.</span><span class="sxs-lookup"><span data-stu-id="a0d97-185">**Non retryable** exceptions simply get rethrown back to the caller.</span></span>
* <span data-ttu-id="a0d97-186">Las excepciones que **se pueden volver a intentar** se clasifican a su vez en **transitorias** y **no transitorias**.</span><span class="sxs-lookup"><span data-stu-id="a0d97-186">**retryable** exceptions are further categorized into **transient** and **non-transient**.</span></span>
  * <span data-ttu-id="a0d97-187">**transitorias** son las que pueden reintentarse sin volver a resolver la dirección del punto de conexión de servicio.</span><span class="sxs-lookup"><span data-stu-id="a0d97-187">**Transient** exceptions are those that can simply be retried without re-resolving the service endpoint address.</span></span> <span data-ttu-id="a0d97-188">Entre estas últimas se incluyen los problemas transitorios de red o las respuestas de error de servicio que no sean las que indican que la dirección de punto de conexión de servicio no existe.</span><span class="sxs-lookup"><span data-stu-id="a0d97-188">These will include transient network problems or service error responses other than those that indicate the service endpoint address does not exist.</span></span>
  * <span data-ttu-id="a0d97-189">**Non-transient** son las que requieren que se vuelva a resolver la dirección de punto de conexión de servicio.</span><span class="sxs-lookup"><span data-stu-id="a0d97-189">**Non-transient** exceptions are those that require the service endpoint address to be re-resolved.</span></span> <span data-ttu-id="a0d97-190">Entre estas se incluyen las excepciones que indican que no se pudo llegar al punto de conexión de servicio, lo que indica que el servicio se movió a otro nodo.</span><span class="sxs-lookup"><span data-stu-id="a0d97-190">These include exceptions that indicate the service endpoint could not be reached, indicating the service has moved to a different node.</span></span>

<span data-ttu-id="a0d97-191">El método `TryHandleException` toma una decisión sobre una excepción determinada.</span><span class="sxs-lookup"><span data-stu-id="a0d97-191">The `TryHandleException` makes a decision about a given exception.</span></span> <span data-ttu-id="a0d97-192">Si **no sabe** qué decisiones tomar sobre una excepción, debe devolver **false**.</span><span class="sxs-lookup"><span data-stu-id="a0d97-192">If it **does not know** what decisions to make about an exception, it should return **false**.</span></span> <span data-ttu-id="a0d97-193">Cuando **sí sabe** qué decisión tomar, debe establecer el resultado según corresponda y devolver **true**.</span><span class="sxs-lookup"><span data-stu-id="a0d97-193">If it **does know** what decision to make, it should set the result accordingly and return **true**.</span></span>

```csharp
class MyExceptionHandler : IExceptionHandler
{
    public bool TryHandleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings, out ExceptionHandlingResult result)
    {
        // if exceptionInformation.Exception is known and is transient (can be retried without re-resolving)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, true, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;


        // if exceptionInformation.Exception is known and is not transient (indicates a new service endpoint address must be resolved)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, false, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;

        // if exceptionInformation.Exception is unknown (let the next IExceptionHandler attempt to handle it)
        result = null;
        return false;
    }
}
```
```java
public class MyExceptionHandler implements ExceptionHandler {

    @Override
    public ExceptionHandlingResult handleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings) {        

        /* if exceptionInformation.getException() is known and is transient (can be retried without re-resolving)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), true, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;


        /* if exceptionInformation.getException() is known and is not transient (indicates a new service endpoint address must be resolved)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), false, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;

        /* if exceptionInformation.getException() is unknown (let the next ExceptionHandler attempt to handle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a><span data-ttu-id="a0d97-194">Resumen</span><span class="sxs-lookup"><span data-stu-id="a0d97-194">Putting it all together</span></span>
<span data-ttu-id="a0d97-195">Con `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` e `IExceptionHandler(C#) / ExceptionHandler(Java)` creadas en torno a un protocolo de comunicaciones, `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` lo encapsula todo y proporciona el bucle de resolución de direcciones de partición de servicio y control de errores en torno a estos componentes.</span><span class="sxs-lookup"><span data-stu-id="a0d97-195">With an `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, and `IExceptionHandler(C#) / ExceptionHandler(Java)` built around a communication protocol, a `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` wraps it all together and provides the fault-handling and service partition address resolution loop around these components.</span></span>

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with the service using the client.
   },
   CancellationToken.None);

```
```java
private MyCommunicationClientFactory myCommunicationClientFactory;
private URI myServiceUri;

FabricServicePartitionClient myServicePartitionClient = new FabricServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

CompletableFuture<?> result = myServicePartitionClient.invokeWithRetryAsync(client -> {
      /* Communicate with the service using the client.
       */
   });

```

## <a name="next-steps"></a><span data-ttu-id="a0d97-196">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a0d97-196">Next steps</span></span>
* <span data-ttu-id="a0d97-197">Ver un ejemplo de comunicación HTTP entre los servicios en un [proyecto de ejemplo de C# en GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) o un [proyecto de ejemplo de Java en GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span><span class="sxs-lookup"><span data-stu-id="a0d97-197">See an example of HTTP communication between services in a [C# sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) or [Java sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span></span>
* [<span data-ttu-id="a0d97-198">Llamadas a procedimiento remoto con la comunicación remota de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="a0d97-198">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="a0d97-199">API web que usa OWIN en Reliable Services</span><span class="sxs-lookup"><span data-stu-id="a0d97-199">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="a0d97-200">Comunicación WCF con la utilización de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="a0d97-200">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
