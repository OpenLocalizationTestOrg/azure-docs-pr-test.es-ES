---
title: "información general de la comunicación de servicios de aaaReliable | Documentos de Microsoft"
description: "Información general del modelo de comunicación de servicios de confianza hello, incluidos los agentes de escucha de apertura en servicios, resuelve los puntos de conexión y la comunicación entre servicios."
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
ms.openlocfilehash: 93a7017b50df0822969daa5ad78302c73e8ba641
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-reliable-services-communication-apis"></a><span data-ttu-id="ee727-103">¿Cómo toouse Hola APIs de comunicación de servicios de confianza</span><span class="sxs-lookup"><span data-stu-id="ee727-103">How toouse hello Reliable Services communication APIs</span></span>
<span data-ttu-id="ee727-104">Azure Service Fabric como una plataforma es completamente independiente de la comunicación entre los servicios.</span><span class="sxs-lookup"><span data-stu-id="ee727-104">Azure Service Fabric as a platform is completely agnostic about communication between services.</span></span> <span data-ttu-id="ee727-105">Todos los protocolos y las pilas son aceptables, de tooHTTP UDP.</span><span class="sxs-lookup"><span data-stu-id="ee727-105">All protocols and stacks are acceptable, from UDP tooHTTP.</span></span> <span data-ttu-id="ee727-106">Es una toohello servicio programador toochoose cómo servicios se deben comunicar.</span><span class="sxs-lookup"><span data-stu-id="ee727-106">It's up toohello service developer toochoose how services should communicate.</span></span> <span data-ttu-id="ee727-107">marco de aplicación de servicios de confianza de Hello proporciona comunicaciones predefinidas de pilas, así como las API que se puede usar toobuild los componentes de comunicación personalizada.</span><span class="sxs-lookup"><span data-stu-id="ee727-107">hello Reliable Services application framework provides built-in communication stacks as well as APIs that you can use toobuild your custom communication components.</span></span>

## <a name="set-up-service-communication"></a><span data-ttu-id="ee727-108">Configuración de la comunicación del servicio</span><span class="sxs-lookup"><span data-stu-id="ee727-108">Set up service communication</span></span>
<span data-ttu-id="ee727-109">Hola confiable de servicios de API usa una interfaz sencilla para la comunicación de servicio.</span><span class="sxs-lookup"><span data-stu-id="ee727-109">hello Reliable Services API uses a simple interface for service communication.</span></span> <span data-ttu-id="ee727-110">tooopen un extremo para el servicio, simplemente se implementa esta interfaz:</span><span class="sxs-lookup"><span data-stu-id="ee727-110">tooopen an endpoint for your service, simply implement this interface:</span></span>

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

<span data-ttu-id="ee727-111">Luego puede agregar su implementación del agente de escucha de comunicación devolviéndolo en una invalidación del método de clase basado en el servicio.</span><span class="sxs-lookup"><span data-stu-id="ee727-111">You can then add your communication listener implementation by returning it in a service-based class method override.</span></span>

<span data-ttu-id="ee727-112">Para servicios sin estado:</span><span class="sxs-lookup"><span data-stu-id="ee727-112">For stateless services:</span></span>

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

<span data-ttu-id="ee727-113">Para servicios con estado:</span><span class="sxs-lookup"><span data-stu-id="ee727-113">For stateful services:</span></span>

> [!NOTE]
> <span data-ttu-id="ee727-114">Las instancias con estado de Reliable Services aún no se admiten en Java.</span><span class="sxs-lookup"><span data-stu-id="ee727-114">Stateful reliable services are not supported in Java yet.</span></span>
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

<span data-ttu-id="ee727-115">En ambos casos, devuelve una colección de agentes de escucha.</span><span class="sxs-lookup"><span data-stu-id="ee727-115">In both cases, you return a collection of listeners.</span></span> <span data-ttu-id="ee727-116">Esto permite que el servicio toolisten en varios puntos de conexión utilicen diferentes protocolos, mediante el uso de varios agentes de escucha.</span><span class="sxs-lookup"><span data-stu-id="ee727-116">This allows your service toolisten on multiple endpoints, potentially using different protocols, by using multiple listeners.</span></span> <span data-ttu-id="ee727-117">Por ejemplo, puede tener un agente de escucha HTTP y un agente de escucha de WebSocket independiente.</span><span class="sxs-lookup"><span data-stu-id="ee727-117">For example, you may have an HTTP listener and a separate WebSocket listener.</span></span> <span data-ttu-id="ee727-118">Cada agente de escucha recibe un nombre y la colección resultante de Hola de *nombre: dirección* pares se representan como un objeto JSON cuando un cliente solicita direcciones de escucha de Hola para una instancia de servicio o una partición.</span><span class="sxs-lookup"><span data-stu-id="ee727-118">Each listener gets a name, and hello resulting collection of *name : address* pairs are represented as a JSON object when a client requests hello listening addresses for a service instance or a partition.</span></span>

<span data-ttu-id="ee727-119">En un servicio sin estado, la invalidación de hello devuelve una colección de ServiceInstanceListeners.</span><span class="sxs-lookup"><span data-stu-id="ee727-119">In a stateless service, hello override returns a collection of ServiceInstanceListeners.</span></span> <span data-ttu-id="ee727-120">A `ServiceInstanceListener` contiene una función toocreate un `ICommunicationListener(C#) / CommunicationListener(Java)` y le asigna un nombre.</span><span class="sxs-lookup"><span data-stu-id="ee727-120">A `ServiceInstanceListener` contains a function toocreate an `ICommunicationListener(C#) / CommunicationListener(Java)` and gives it a name.</span></span> <span data-ttu-id="ee727-121">Para los servicios con estado, la invalidación de hello devuelve una colección de ServiceReplicaListeners.</span><span class="sxs-lookup"><span data-stu-id="ee727-121">For stateful services, hello override returns a collection of ServiceReplicaListeners.</span></span> <span data-ttu-id="ee727-122">Esto es ligeramente diferente de su homólogo sin estado, porque un `ServiceReplicaListener` tiene una opción tooopen un `ICommunicationListener` en las réplicas secundarias.</span><span class="sxs-lookup"><span data-stu-id="ee727-122">This is slightly different from its stateless counterpart, because a `ServiceReplicaListener` has an option tooopen an `ICommunicationListener` on secondary replicas.</span></span> <span data-ttu-id="ee727-123">No solo puede usar varios agentes de escucha de comunicación en un servicio, sino también especificar cuáles aceptan solicitudes en réplicas secundarias y cuáles escuchan solo en las réplicas principales.</span><span class="sxs-lookup"><span data-stu-id="ee727-123">Not only can you use multiple communication listeners in a service, but you can also specify which listeners accept requests on secondary replicas and which ones listen only on primary replicas.</span></span>

<span data-ttu-id="ee727-124">Por ejemplo, puede tener una clase ServiceRemotingListener que realice llamadas RPC solo en las réplicas principales, y un segundo agente de escucha personalizado que lea solicitudes en réplicas secundarias a través de HTTP:</span><span class="sxs-lookup"><span data-stu-id="ee727-124">For example, you can have a ServiceRemotingListener that takes RPC calls only on primary replicas, and a second, custom listener that takes read requests on secondary replicas over HTTP:</span></span>

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
> <span data-ttu-id="ee727-125">Cuando se crean varios agentes de escucha para un servicio, se **debe** asignar a cada uno un nombre único.</span><span class="sxs-lookup"><span data-stu-id="ee727-125">When creating multiple listeners for a service, each listener **must** be given a unique name.</span></span>
>
>

<span data-ttu-id="ee727-126">Por último, se describen los puntos de conexión de Hola que son necesarios para el servicio de Hola Hola [manifiesto del servicio](service-fabric-application-model.md) en la sección de hello en los puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="ee727-126">Finally, describe hello endpoints that are required for hello service in hello [service manifest](service-fabric-application-model.md) under hello section on endpoints.</span></span>

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

<span data-ttu-id="ee727-127">agente de escucha de comunicación de Hello puede tener acceso a recursos de punto de conexión de hello asignados tooit de hello `CodePackageActivationContext` en hello `ServiceContext`.</span><span class="sxs-lookup"><span data-stu-id="ee727-127">hello communication listener can access hello endpoint resources allocated tooit from hello `CodePackageActivationContext` in hello `ServiceContext`.</span></span> <span data-ttu-id="ee727-128">agente de escucha de Hello puede, a continuación, empiece a escuchar las solicitudes cuando se abre.</span><span class="sxs-lookup"><span data-stu-id="ee727-128">hello listener can then start listening for requests when it is opened.</span></span>

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> <span data-ttu-id="ee727-129">Recursos de punto de conexión son paquetes de servicio completo toohello comunes y se asignan por Service Fabric cuando se activa el paquete de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee727-129">Endpoint resources are common toohello entire service package, and they are allocated by Service Fabric when hello service package is activated.</span></span> <span data-ttu-id="ee727-130">Varias réplicas de servicio hospedadas en hello puede compartir el mismo ServiceHost Hola mismo puerto.</span><span class="sxs-lookup"><span data-stu-id="ee727-130">Multiple service replicas hosted in hello same ServiceHost may share hello same port.</span></span> <span data-ttu-id="ee727-131">Esto significa que ese agente de escucha de comunicación de hello debe admitir el uso compartido de puertos.</span><span class="sxs-lookup"><span data-stu-id="ee727-131">This means that hello communication listener should support port sharing.</span></span> <span data-ttu-id="ee727-132">Hola recomienda forma de hacerlo es para hello comunicación del agente de escucha toouse Hola partición identificador y el identificador de réplica/instancia cuando genera la dirección de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee727-132">hello recommended way of doing this is for hello communication listener toouse hello partition ID and replica/instance ID when it generates hello listen address.</span></span>
>
>

### <a name="service-address-registration"></a><span data-ttu-id="ee727-133">Registro de dirección de servicio</span><span class="sxs-lookup"><span data-stu-id="ee727-133">Service address registration</span></span>
<span data-ttu-id="ee727-134">Llama a un servicio de sistema hello *Naming Service* se ejecuta en clústeres de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ee727-134">A system service called hello *Naming Service* runs on Service Fabric clusters.</span></span> <span data-ttu-id="ee727-135">Hola Naming Service es un registrador para los servicios y sus direcciones que escucha cada instancia o una réplica del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee727-135">hello Naming Service is a registrar for services and their addresses that each instance or replica of hello service is listening on.</span></span> <span data-ttu-id="ee727-136">Cuando Hola `OpenAsync(C#) / openAsync(Java)` método de una `ICommunicationListener(C#) / CommunicationListener(Java)` completa, devolver un valor valor obtiene registrado en hello Naming Service.</span><span class="sxs-lookup"><span data-stu-id="ee727-136">When hello `OpenAsync(C#) / openAsync(Java)` method of an `ICommunicationListener(C#) / CommunicationListener(Java)` completes, its return value gets registered in hello Naming Service.</span></span> <span data-ttu-id="ee727-137">Esto devuelve el valor que obtiene publicados en hello Naming Service es una cadena cuyo valor puede ser cualquier cosa en absoluto.</span><span class="sxs-lookup"><span data-stu-id="ee727-137">This return value that gets published in hello Naming Service is a string whose value can be anything at all.</span></span> <span data-ttu-id="ee727-138">Este valor de cadena es lo que ven los clientes cuando le solicite una dirección de servicio de hello en hello Naming Service.</span><span class="sxs-lookup"><span data-stu-id="ee727-138">This string value is what clients see when they ask for an address for hello service from hello Naming Service.</span></span>

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

    // hello string returned here will be published in hello Naming Service.
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

    /* hello string returned here will be published in hello Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

<span data-ttu-id="ee727-139">Service Fabric proporciona API que permiten a los clientes y otro servicios toothen solicitar esta dirección por nombre de servicio.</span><span class="sxs-lookup"><span data-stu-id="ee727-139">Service Fabric provides APIs that allow clients and other services toothen ask for this address by service name.</span></span> <span data-ttu-id="ee727-140">Esto es importante porque la dirección de servicio de hello no es estático.</span><span class="sxs-lookup"><span data-stu-id="ee727-140">This is important because hello service address is not static.</span></span> <span data-ttu-id="ee727-141">Servicios se mueven en clúster de Hola para fines de disponibilidad y equilibrio de recursos.</span><span class="sxs-lookup"><span data-stu-id="ee727-141">Services are moved around in hello cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="ee727-142">Este es el mecanismo de Hola que permiten a los clientes hello tooresolve dirección para un servicio de escucha.</span><span class="sxs-lookup"><span data-stu-id="ee727-142">This is hello mechanism that allow clients tooresolve hello listening address for a service.</span></span>

> [!NOTE]
> <span data-ttu-id="ee727-143">Para ver un tutorial completo de cómo toowrite un agente de escucha de comunicación, consulte [servicios de API Web del servicio tejido con OWIN hospeda a sí mismo](service-fabric-reliable-services-communication-webapi.md) en C#, mientras que para Java puede escribir su propia implementación de servidor HTTP, vea aplicación EchoServer ejemplo en https://github.com/Azure-Samples/service-fabric-java-getting-started.</span><span class="sxs-lookup"><span data-stu-id="ee727-143">For a complete walk-through of how toowrite a communication listener, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md) for C#, whereas for Java you can write your own HTTP server implementation, see EchoServer application example at https://github.com/Azure-Samples/service-fabric-java-getting-started.</span></span>
>
>

## <a name="communicating-with-a-service"></a><span data-ttu-id="ee727-144">Comunicación con un servicio</span><span class="sxs-lookup"><span data-stu-id="ee727-144">Communicating with a service</span></span>
<span data-ttu-id="ee727-145">Hola confiable de servicios de API proporciona Hola después de los clientes de toowrite de bibliotecas que se comunican con los servicios.</span><span class="sxs-lookup"><span data-stu-id="ee727-145">hello Reliable Services API provides hello following libraries toowrite clients that communicate with services.</span></span>

### <a name="service-endpoint-resolution"></a><span data-ttu-id="ee727-146">Resolución del punto de conexión de servicio</span><span class="sxs-lookup"><span data-stu-id="ee727-146">Service endpoint resolution</span></span>
<span data-ttu-id="ee727-147">Hola primer paso toocommunication con un servicio es una dirección de punto de conexión de partición de Hola o instancia de servicio de Hola que desee tootalk a tooresolve.</span><span class="sxs-lookup"><span data-stu-id="ee727-147">hello first step toocommunication with a service is tooresolve an endpoint address of hello partition or instance of hello service you want tootalk to.</span></span> <span data-ttu-id="ee727-148">Hola `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` clase de utilidad es una primitiva básica que ayuda a los clientes a determinar el extremo de Hola de un servicio en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="ee727-148">hello `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` utility class is a basic primitive that helps clients determine hello endpoint of a service at runtime.</span></span> <span data-ttu-id="ee727-149">En la terminología de Service Fabric, proceso de Hola de determinar el extremo de Hola de un servicio es hello tooas que se hace referencia *resolución de punto de conexión de servicio*.</span><span class="sxs-lookup"><span data-stu-id="ee727-149">In Service Fabric terminology, hello process of determining hello endpoint of a service is referred tooas hello *service endpoint resolution*.</span></span>

<span data-ttu-id="ee727-150">tooconnect tooservices dentro de un clúster, ServicePartitionResolver pueden crearse con la configuración predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ee727-150">tooconnect tooservices within a cluster, ServicePartitionResolver can be created using default settings.</span></span> <span data-ttu-id="ee727-151">Se trata de hello recomendada el uso de la mayoría de los casos:</span><span class="sxs-lookup"><span data-stu-id="ee727-151">This is hello recommended usage for most situations:</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

<span data-ttu-id="ee727-152">tooconnect tooservices en un clúster distinto, un ServicePartitionResolver puede crearse con un conjunto de puntos de conexión de puerta de enlace de clúster.</span><span class="sxs-lookup"><span data-stu-id="ee727-152">tooconnect tooservices in a different cluster, a ServicePartitionResolver can be created with a set of cluster gateway endpoints.</span></span> <span data-ttu-id="ee727-153">Tenga en cuenta que los puntos de conexión de puerta de enlace son simplemente diferentes puntos de conexión para conectar toohello mismo clúster.</span><span class="sxs-lookup"><span data-stu-id="ee727-153">Note that gateway endpoints are just different endpoints for connecting toohello same cluster.</span></span> <span data-ttu-id="ee727-154">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ee727-154">For example:</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

<span data-ttu-id="ee727-155">O bien, `ServicePartitionResolver` puede indicarse una función para crear un `FabricClient` toouse internamente:</span><span class="sxs-lookup"><span data-stu-id="ee727-155">Alternatively, `ServicePartitionResolver` can be given a function for creating a `FabricClient` toouse internally:</span></span>

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

<span data-ttu-id="ee727-156">`FabricClient`es el objeto hello toocommunicate usado con clúster de Service Fabric Hola para realizar diversas operaciones de administración en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee727-156">`FabricClient` is hello object that is used toocommunicate with hello Service Fabric cluster for various management operations on hello cluster.</span></span> <span data-ttu-id="ee727-157">Esto resulta útil cuando se desea tener más control sobre cómo interactúa la resolución de la partición del servicio con el clúster.</span><span class="sxs-lookup"><span data-stu-id="ee727-157">This is useful when you want more control over how a service partition resolver interacts with your cluster.</span></span> <span data-ttu-id="ee727-158">`FabricClient`lleva a cabo internamente el almacenamiento en caché y es toocreate suele ser costoso, por lo que es importante tooreuse `FabricClient` instancias tanto como sea posibles.</span><span class="sxs-lookup"><span data-stu-id="ee727-158">`FabricClient` performs caching internally and is generally expensive toocreate, so it is important tooreuse `FabricClient` instances as much as possible.</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

<span data-ttu-id="ee727-159">Un método de resolución es, a continuación, usa tooretrieve Hola dirección de un servicio o una partición de servicio para los servicios con particiones.</span><span class="sxs-lookup"><span data-stu-id="ee727-159">A resolve method is then used tooretrieve hello address of a service or a service partition for partitioned services.</span></span>

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

<span data-ttu-id="ee727-160">Una dirección de servicio se puede resolver fácilmente utilizando una ServicePartitionResolver, pero se necesita más trabajo tooensure Hola resuelve la dirección se puede usar correctamente.</span><span class="sxs-lookup"><span data-stu-id="ee727-160">A service address can be resolved easily using a ServicePartitionResolver, but more work is required tooensure hello resolved address can be used correctly.</span></span> <span data-ttu-id="ee727-161">El cliente debe toodetect si el intento de conexión de hello error debido a un error transitorio y se puede recuperar (p. ej., servicio movido o no está disponible temporalmente), o un error permanente (p. ej., servicio se ha eliminado o hello recurso solicitado ya no existe).</span><span class="sxs-lookup"><span data-stu-id="ee727-161">Your client needs toodetect whether hello connection attempt failed because of a transient error and can be retried (e.g., service moved or is temporarily unavailable), or a permanent error (e.g., service was deleted or hello requested resource no longer exists).</span></span> <span data-ttu-id="ee727-162">Instancias de servicio o réplicas pueden moverse del nodo toonode en cualquier momento por distintos motivos.</span><span class="sxs-lookup"><span data-stu-id="ee727-162">Service instances or replicas can move around from node toonode at any time for multiple reasons.</span></span> <span data-ttu-id="ee727-163">dirección de servicio de Hello resuelven a través de ServicePartitionResolver puede estar obsoleto por tiempo Hola que su código de cliente intenta tooconnect.</span><span class="sxs-lookup"><span data-stu-id="ee727-163">hello service address resolved through ServicePartitionResolver may be stale by hello time your client code attempts tooconnect.</span></span> <span data-ttu-id="ee727-164">En ese caso nuevo cliente de hello debe dirección de hello toore se resuelven.</span><span class="sxs-lookup"><span data-stu-id="ee727-164">In that case again hello client needs toore-resolve hello address.</span></span> <span data-ttu-id="ee727-165">Proporcionar Hola anterior `ResolvedServicePartition` indica que Hola tootry de necesidades de resolución de nuevo en lugar de simplemente recuperar una dirección almacenada en caché.</span><span class="sxs-lookup"><span data-stu-id="ee727-165">Providing hello previous `ResolvedServicePartition` indicates that hello resolver needs tootry again rather than simply retrieve a cached address.</span></span>

<span data-ttu-id="ee727-166">Normalmente, los código de cliente de hello no necesita trabajar con hello ServicePartitionResolver directamente.</span><span class="sxs-lookup"><span data-stu-id="ee727-166">Typically, hello client code need not work with hello ServicePartitionResolver directly.</span></span> <span data-ttu-id="ee727-167">Se crea y se pasan en toocommunication generadores del cliente en hello confiable de servicios de API.</span><span class="sxs-lookup"><span data-stu-id="ee727-167">It is created and passed on toocommunication client factories in hello Reliable Services API.</span></span> <span data-ttu-id="ee727-168">generadores de Hello usan resolución Hola internamente toogenerate un objeto de cliente que puede ser utilizado toocommunicate con los servicios.</span><span class="sxs-lookup"><span data-stu-id="ee727-168">hello factories use hello resolver internally toogenerate a client object that can be used toocommunicate with services.</span></span>

### <a name="communication-clients-and-factories"></a><span data-ttu-id="ee727-169">Fábricas y clientes de comunicación</span><span class="sxs-lookup"><span data-stu-id="ee727-169">Communication clients and factories</span></span>
<span data-ttu-id="ee727-170">biblioteca de fábrica de comunicación de Hello implementa un patrón típico de reintento de control de errores que facilita retrying extremos de servicio de tooresolved de conexiones.</span><span class="sxs-lookup"><span data-stu-id="ee727-170">hello communication factory library implements a typical fault-handling retry pattern that makes retrying connections tooresolved service endpoints easier.</span></span> <span data-ttu-id="ee727-171">biblioteca de fábrica de Hello proporciona mecanismo de reintento de hello mientras proporcionan controladores de errores de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee727-171">hello factory library provides hello retry mechanism while you provide hello error handlers.</span></span>

<span data-ttu-id="ee727-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`define la interfaz de base de hello implementada por un generador de cliente de comunicación generadas por los clientes que pueden comunicarse el servicio de Service Fabric tooa.</span><span class="sxs-lookup"><span data-stu-id="ee727-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` defines hello base interface implemented by a communication client factory that produces clients that can talk tooa Service Fabric service.</span></span> <span data-ttu-id="ee727-173">Hola implementación de hello que communicationclientfactory depende de la pila de comunicación de hello utilizado por servicio de Service Fabric de Hola donde el cliente de Hola desde toocommunicate.</span><span class="sxs-lookup"><span data-stu-id="ee727-173">hello implementation of hello CommunicationClientFactory depends on hello communication stack used by hello Service Fabric service where hello client wants toocommunicate.</span></span> <span data-ttu-id="ee727-174">Hello confiable API Services proporciona un `CommunicationClientFactoryBase<TCommunicationClient>`.</span><span class="sxs-lookup"><span data-stu-id="ee727-174">hello Reliable Services API provides a `CommunicationClientFactoryBase<TCommunicationClient>`.</span></span> <span data-ttu-id="ee727-175">Esto proporciona una implementación base de la interfaz de CommunicationClientFactory de Hola y realiza tareas de pilas de comunicación de hello tooall comunes.</span><span class="sxs-lookup"><span data-stu-id="ee727-175">This provides a base implementation of hello CommunicationClientFactory interface and performs tasks that are common tooall hello communication stacks.</span></span> <span data-ttu-id="ee727-176">(Estas tareas incluyen el uso de un extremo de servicio de ServicePartitionResolver toodetermine Hola).</span><span class="sxs-lookup"><span data-stu-id="ee727-176">(These tasks include using a ServicePartitionResolver toodetermine hello service endpoint).</span></span> <span data-ttu-id="ee727-177">Los clientes implementan generalmente Hola abstracta CommunicationClientFactoryBase clase toohandle lógica de pila de comunicación toohello específico.</span><span class="sxs-lookup"><span data-stu-id="ee727-177">Clients usually implement hello abstract CommunicationClientFactoryBase class toohandle logic that is specific toohello communication stack.</span></span>

<span data-ttu-id="ee727-178">cliente de comunicación de Hello simplemente recibe una dirección y usa tooconnect tooa servicio.</span><span class="sxs-lookup"><span data-stu-id="ee727-178">hello communication client just receives an address and uses it tooconnect tooa service.</span></span> <span data-ttu-id="ee727-179">cliente de Hello puede usar cualquier protocolo que desee.</span><span class="sxs-lookup"><span data-stu-id="ee727-179">hello client can use whatever protocol it wants.</span></span>

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

<span data-ttu-id="ee727-180">Hola client factory es principalmente responsable de la creación de clientes de comunicación.</span><span class="sxs-lookup"><span data-stu-id="ee727-180">hello client factory is primarily responsible for creating communication clients.</span></span> <span data-ttu-id="ee727-181">Para los clientes que no mantienen una conexión persistente, por ejemplo, un cliente HTTP, generador de hello solo necesita toocreate y cliente hello devuelto.</span><span class="sxs-lookup"><span data-stu-id="ee727-181">For clients that don't maintain a persistent connection, such as an HTTP client, hello factory only needs toocreate and return hello client.</span></span> <span data-ttu-id="ee727-182">Otros protocolos que mantienen una conexión persistente, por ejemplo, algunos protocolos binarios, también deben validarse por hello generador toodetermine si es una conexión de hello toobe vuelve a crear.</span><span class="sxs-lookup"><span data-stu-id="ee727-182">Other protocols that maintain a persistent connection, such as some binary protocols, should also be validated by hello factory toodetermine whether hello connection needs toobe re-created.</span></span>  

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

<span data-ttu-id="ee727-183">Por último, un controlador de excepciones es responsable de determinar qué tootake acción cuando se produce una excepción.</span><span class="sxs-lookup"><span data-stu-id="ee727-183">Finally, an exception handler is responsible for determining what action tootake when an exception occurs.</span></span> <span data-ttu-id="ee727-184">Las excepciones se dividen en dos categorías, las que **se pueden volver a intentar** y las que **no se pueden volver a intentar**.</span><span class="sxs-lookup"><span data-stu-id="ee727-184">Exceptions are categorized into **retryable** and **non retryable**.</span></span>

* <span data-ttu-id="ee727-185">**Irreproducible** excepciones simplemente obtengan vuelve a producir llamador toohello atrás.</span><span class="sxs-lookup"><span data-stu-id="ee727-185">**Non retryable** exceptions simply get rethrown back toohello caller.</span></span>
* <span data-ttu-id="ee727-186">Las excepciones que **se pueden volver a intentar** se clasifican a su vez en **transitorias** y **no transitorias**.</span><span class="sxs-lookup"><span data-stu-id="ee727-186">**retryable** exceptions are further categorized into **transient** and **non-transient**.</span></span>
  * <span data-ttu-id="ee727-187">**Transitorio** excepciones son aquellos que simplemente se vuelve a intentar sin volver a resolver la dirección del extremo de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee727-187">**Transient** exceptions are those that can simply be retried without re-resolving hello service endpoint address.</span></span> <span data-ttu-id="ee727-188">Entre ellos incluyen los problemas de red transitorios o respuestas de error de servicio distintos a los que indican la dirección del extremo de servicio de hello no existe.</span><span class="sxs-lookup"><span data-stu-id="ee727-188">These will include transient network problems or service error responses other than those that indicate hello service endpoint address does not exist.</span></span>
  * <span data-ttu-id="ee727-189">**No transitorio** excepciones son aquellos que requieren la dirección de punto de conexión de hello servicio toobe volviera a resolver.</span><span class="sxs-lookup"><span data-stu-id="ee727-189">**Non-transient** exceptions are those that require hello service endpoint address toobe re-resolved.</span></span> <span data-ttu-id="ee727-190">Esto incluye las excepciones que indican un extremo de servicio de hello no se puede acceder, que indica el servicio de Hola movió tooa otro nodo.</span><span class="sxs-lookup"><span data-stu-id="ee727-190">These include exceptions that indicate hello service endpoint could not be reached, indicating hello service has moved tooa different node.</span></span>

<span data-ttu-id="ee727-191">Hola `TryHandleException` toma una decisión sobre una excepción determinada.</span><span class="sxs-lookup"><span data-stu-id="ee727-191">hello `TryHandleException` makes a decision about a given exception.</span></span> <span data-ttu-id="ee727-192">Si se **no sabe** qué toomake decisiones sobre una excepción, debe devolver **false**.</span><span class="sxs-lookup"><span data-stu-id="ee727-192">If it **does not know** what decisions toomake about an exception, it should return **false**.</span></span> <span data-ttu-id="ee727-193">Si se **saber** qué toomake de decisión, debe establecer el resultado de hello en consecuencia y devolver **true**.</span><span class="sxs-lookup"><span data-stu-id="ee727-193">If it **does know** what decision toomake, it should set hello result accordingly and return **true**.</span></span>

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

        // if exceptionInformation.Exception is unknown (let hello next IExceptionHandler attempt toohandle it)
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

        /* if exceptionInformation.getException() is unknown (let hello next ExceptionHandler attempt toohandle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a><span data-ttu-id="ee727-194">Resumen</span><span class="sxs-lookup"><span data-stu-id="ee727-194">Putting it all together</span></span>
<span data-ttu-id="ee727-195">Con un `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, y `IExceptionHandler(C#) / ExceptionHandler(Java)` generadas en torno a un protocolo de comunicaciones, un `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` envuelve combina todas estas características y proporciona control de errores de Hola y trazo de resolución de direcciones de partición de servicio alrededor de estos componentes.</span><span class="sxs-lookup"><span data-stu-id="ee727-195">With an `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, and `IExceptionHandler(C#) / ExceptionHandler(Java)` built around a communication protocol, a `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` wraps it all together and provides hello fault-handling and service partition address resolution loop around these components.</span></span>

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with hello service using hello client.
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
      /* Communicate with hello service using hello client.
       */
   });

```

## <a name="next-steps"></a><span data-ttu-id="ee727-196">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ee727-196">Next steps</span></span>
* <span data-ttu-id="ee727-197">Ver un ejemplo de comunicación HTTP entre los servicios en un [proyecto de ejemplo de C# en GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) o un [proyecto de ejemplo de Java en GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span><span class="sxs-lookup"><span data-stu-id="ee727-197">See an example of HTTP communication between services in a [C# sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) or [Java sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span></span>
* [<span data-ttu-id="ee727-198">Llamadas a procedimiento remoto con la comunicación remota de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="ee727-198">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="ee727-199">API web que usa OWIN en Reliable Services</span><span class="sxs-lookup"><span data-stu-id="ee727-199">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="ee727-200">Comunicación WCF con la utilización de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="ee727-200">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
