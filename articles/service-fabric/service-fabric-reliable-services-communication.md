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
# <a name="how-toouse-hello-reliable-services-communication-apis"></a>¿Cómo toouse Hola APIs de comunicación de servicios de confianza
Azure Service Fabric como una plataforma es completamente independiente de la comunicación entre los servicios. Todos los protocolos y las pilas son aceptables, de tooHTTP UDP. Es una toohello servicio programador toochoose cómo servicios se deben comunicar. marco de aplicación de servicios de confianza de Hello proporciona comunicaciones predefinidas de pilas, así como las API que se puede usar toobuild los componentes de comunicación personalizada.

## <a name="set-up-service-communication"></a>Configuración de la comunicación del servicio
Hola confiable de servicios de API usa una interfaz sencilla para la comunicación de servicio. tooopen un extremo para el servicio, simplemente se implementa esta interfaz:

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

Luego puede agregar su implementación del agente de escucha de comunicación devolviéndolo en una invalidación del método de clase basado en el servicio.

Para servicios sin estado:

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

Para servicios con estado:

> [!NOTE]
> Las instancias con estado de Reliable Services aún no se admiten en Java.
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

En ambos casos, devuelve una colección de agentes de escucha. Esto permite que el servicio toolisten en varios puntos de conexión utilicen diferentes protocolos, mediante el uso de varios agentes de escucha. Por ejemplo, puede tener un agente de escucha HTTP y un agente de escucha de WebSocket independiente. Cada agente de escucha recibe un nombre y la colección resultante de Hola de *nombre: dirección* pares se representan como un objeto JSON cuando un cliente solicita direcciones de escucha de Hola para una instancia de servicio o una partición.

En un servicio sin estado, la invalidación de hello devuelve una colección de ServiceInstanceListeners. A `ServiceInstanceListener` contiene una función toocreate un `ICommunicationListener(C#) / CommunicationListener(Java)` y le asigna un nombre. Para los servicios con estado, la invalidación de hello devuelve una colección de ServiceReplicaListeners. Esto es ligeramente diferente de su homólogo sin estado, porque un `ServiceReplicaListener` tiene una opción tooopen un `ICommunicationListener` en las réplicas secundarias. No solo puede usar varios agentes de escucha de comunicación en un servicio, sino también especificar cuáles aceptan solicitudes en réplicas secundarias y cuáles escuchan solo en las réplicas principales.

Por ejemplo, puede tener una clase ServiceRemotingListener que realice llamadas RPC solo en las réplicas principales, y un segundo agente de escucha personalizado que lea solicitudes en réplicas secundarias a través de HTTP:

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
> Cuando se crean varios agentes de escucha para un servicio, se **debe** asignar a cada uno un nombre único.
>
>

Por último, se describen los puntos de conexión de Hola que son necesarios para el servicio de Hola Hola [manifiesto del servicio](service-fabric-application-model.md) en la sección de hello en los puntos de conexión.

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

agente de escucha de comunicación de Hello puede tener acceso a recursos de punto de conexión de hello asignados tooit de hello `CodePackageActivationContext` en hello `ServiceContext`. agente de escucha de Hello puede, a continuación, empiece a escuchar las solicitudes cuando se abre.

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> Recursos de punto de conexión son paquetes de servicio completo toohello comunes y se asignan por Service Fabric cuando se activa el paquete de servicio de Hola. Varias réplicas de servicio hospedadas en hello puede compartir el mismo ServiceHost Hola mismo puerto. Esto significa que ese agente de escucha de comunicación de hello debe admitir el uso compartido de puertos. Hola recomienda forma de hacerlo es para hello comunicación del agente de escucha toouse Hola partición identificador y el identificador de réplica/instancia cuando genera la dirección de escucha de Hola.
>
>

### <a name="service-address-registration"></a>Registro de dirección de servicio
Llama a un servicio de sistema hello *Naming Service* se ejecuta en clústeres de Service Fabric. Hola Naming Service es un registrador para los servicios y sus direcciones que escucha cada instancia o una réplica del servicio de Hola. Cuando Hola `OpenAsync(C#) / openAsync(Java)` método de una `ICommunicationListener(C#) / CommunicationListener(Java)` completa, devolver un valor valor obtiene registrado en hello Naming Service. Esto devuelve el valor que obtiene publicados en hello Naming Service es una cadena cuyo valor puede ser cualquier cosa en absoluto. Este valor de cadena es lo que ven los clientes cuando le solicite una dirección de servicio de hello en hello Naming Service.

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

Service Fabric proporciona API que permiten a los clientes y otro servicios toothen solicitar esta dirección por nombre de servicio. Esto es importante porque la dirección de servicio de hello no es estático. Servicios se mueven en clúster de Hola para fines de disponibilidad y equilibrio de recursos. Este es el mecanismo de Hola que permiten a los clientes hello tooresolve dirección para un servicio de escucha.

> [!NOTE]
> Para ver un tutorial completo de cómo toowrite un agente de escucha de comunicación, consulte [servicios de API Web del servicio tejido con OWIN hospeda a sí mismo](service-fabric-reliable-services-communication-webapi.md) en C#, mientras que para Java puede escribir su propia implementación de servidor HTTP, vea aplicación EchoServer ejemplo en https://github.com/Azure-Samples/service-fabric-java-getting-started.
>
>

## <a name="communicating-with-a-service"></a>Comunicación con un servicio
Hola confiable de servicios de API proporciona Hola después de los clientes de toowrite de bibliotecas que se comunican con los servicios.

### <a name="service-endpoint-resolution"></a>Resolución del punto de conexión de servicio
Hola primer paso toocommunication con un servicio es una dirección de punto de conexión de partición de Hola o instancia de servicio de Hola que desee tootalk a tooresolve. Hola `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` clase de utilidad es una primitiva básica que ayuda a los clientes a determinar el extremo de Hola de un servicio en tiempo de ejecución. En la terminología de Service Fabric, proceso de Hola de determinar el extremo de Hola de un servicio es hello tooas que se hace referencia *resolución de punto de conexión de servicio*.

tooconnect tooservices dentro de un clúster, ServicePartitionResolver pueden crearse con la configuración predeterminada. Se trata de hello recomendada el uso de la mayoría de los casos:

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

tooconnect tooservices en un clúster distinto, un ServicePartitionResolver puede crearse con un conjunto de puntos de conexión de puerta de enlace de clúster. Tenga en cuenta que los puntos de conexión de puerta de enlace son simplemente diferentes puntos de conexión para conectar toohello mismo clúster. Por ejemplo:

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

O bien, `ServicePartitionResolver` puede indicarse una función para crear un `FabricClient` toouse internamente:

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

`FabricClient`es el objeto hello toocommunicate usado con clúster de Service Fabric Hola para realizar diversas operaciones de administración en clúster de Hola. Esto resulta útil cuando se desea tener más control sobre cómo interactúa la resolución de la partición del servicio con el clúster. `FabricClient`lleva a cabo internamente el almacenamiento en caché y es toocreate suele ser costoso, por lo que es importante tooreuse `FabricClient` instancias tanto como sea posibles.

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

Un método de resolución es, a continuación, usa tooretrieve Hola dirección de un servicio o una partición de servicio para los servicios con particiones.

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

Una dirección de servicio se puede resolver fácilmente utilizando una ServicePartitionResolver, pero se necesita más trabajo tooensure Hola resuelve la dirección se puede usar correctamente. El cliente debe toodetect si el intento de conexión de hello error debido a un error transitorio y se puede recuperar (p. ej., servicio movido o no está disponible temporalmente), o un error permanente (p. ej., servicio se ha eliminado o hello recurso solicitado ya no existe). Instancias de servicio o réplicas pueden moverse del nodo toonode en cualquier momento por distintos motivos. dirección de servicio de Hello resuelven a través de ServicePartitionResolver puede estar obsoleto por tiempo Hola que su código de cliente intenta tooconnect. En ese caso nuevo cliente de hello debe dirección de hello toore se resuelven. Proporcionar Hola anterior `ResolvedServicePartition` indica que Hola tootry de necesidades de resolución de nuevo en lugar de simplemente recuperar una dirección almacenada en caché.

Normalmente, los código de cliente de hello no necesita trabajar con hello ServicePartitionResolver directamente. Se crea y se pasan en toocommunication generadores del cliente en hello confiable de servicios de API. generadores de Hello usan resolución Hola internamente toogenerate un objeto de cliente que puede ser utilizado toocommunicate con los servicios.

### <a name="communication-clients-and-factories"></a>Fábricas y clientes de comunicación
biblioteca de fábrica de comunicación de Hello implementa un patrón típico de reintento de control de errores que facilita retrying extremos de servicio de tooresolved de conexiones. biblioteca de fábrica de Hello proporciona mecanismo de reintento de hello mientras proporcionan controladores de errores de Hola.

`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`define la interfaz de base de hello implementada por un generador de cliente de comunicación generadas por los clientes que pueden comunicarse el servicio de Service Fabric tooa. Hola implementación de hello que communicationclientfactory depende de la pila de comunicación de hello utilizado por servicio de Service Fabric de Hola donde el cliente de Hola desde toocommunicate. Hello confiable API Services proporciona un `CommunicationClientFactoryBase<TCommunicationClient>`. Esto proporciona una implementación base de la interfaz de CommunicationClientFactory de Hola y realiza tareas de pilas de comunicación de hello tooall comunes. (Estas tareas incluyen el uso de un extremo de servicio de ServicePartitionResolver toodetermine Hola). Los clientes implementan generalmente Hola abstracta CommunicationClientFactoryBase clase toohandle lógica de pila de comunicación toohello específico.

cliente de comunicación de Hello simplemente recibe una dirección y usa tooconnect tooa servicio. cliente de Hello puede usar cualquier protocolo que desee.

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

Hola client factory es principalmente responsable de la creación de clientes de comunicación. Para los clientes que no mantienen una conexión persistente, por ejemplo, un cliente HTTP, generador de hello solo necesita toocreate y cliente hello devuelto. Otros protocolos que mantienen una conexión persistente, por ejemplo, algunos protocolos binarios, también deben validarse por hello generador toodetermine si es una conexión de hello toobe vuelve a crear.  

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

Por último, un controlador de excepciones es responsable de determinar qué tootake acción cuando se produce una excepción. Las excepciones se dividen en dos categorías, las que **se pueden volver a intentar** y las que **no se pueden volver a intentar**.

* **Irreproducible** excepciones simplemente obtengan vuelve a producir llamador toohello atrás.
* Las excepciones que **se pueden volver a intentar** se clasifican a su vez en **transitorias** y **no transitorias**.
  * **Transitorio** excepciones son aquellos que simplemente se vuelve a intentar sin volver a resolver la dirección del extremo de servicio de Hola. Entre ellos incluyen los problemas de red transitorios o respuestas de error de servicio distintos a los que indican la dirección del extremo de servicio de hello no existe.
  * **No transitorio** excepciones son aquellos que requieren la dirección de punto de conexión de hello servicio toobe volviera a resolver. Esto incluye las excepciones que indican un extremo de servicio de hello no se puede acceder, que indica el servicio de Hola movió tooa otro nodo.

Hola `TryHandleException` toma una decisión sobre una excepción determinada. Si se **no sabe** qué toomake decisiones sobre una excepción, debe devolver **false**. Si se **saber** qué toomake de decisión, debe establecer el resultado de hello en consecuencia y devolver **true**.

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
### <a name="putting-it-all-together"></a>Resumen
Con un `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, y `IExceptionHandler(C#) / ExceptionHandler(Java)` generadas en torno a un protocolo de comunicaciones, un `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` envuelve combina todas estas características y proporciona control de errores de Hola y trazo de resolución de direcciones de partición de servicio alrededor de estos componentes.

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

## <a name="next-steps"></a>Pasos siguientes
* Ver un ejemplo de comunicación HTTP entre los servicios en un [proyecto de ejemplo de C# en GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) o un [proyecto de ejemplo de Java en GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).
* [Llamadas a procedimiento remoto con la comunicación remota de Reliable Services](service-fabric-reliable-services-communication-remoting.md)
* [API web que usa OWIN en Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Comunicación WCF con la utilización de Reliable Services](service-fabric-reliable-services-communication-wcf.md)
