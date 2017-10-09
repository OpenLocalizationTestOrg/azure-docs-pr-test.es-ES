---
title: "pila de comunicación de servicios WCF aaaReliable | Documentos de Microsoft"
description: "pila de comunicación de WCF integrado de Hello en Service Fabric proporciona comunicación del servicio de cliente de WCF para servicios de confianza."
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 75516e1e-ee57-4bc7-95fe-71ec42d452b2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/07/2017
ms.author: bharatn
ms.openlocfilehash: 7feebef4d46a6ae66d05129f47f9b5911e82aec9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="wcf-based-communication-stack-for-reliable-services"></a><span data-ttu-id="f37f2-103">Pila de comunicación basada en WCF de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="f37f2-103">WCF-based communication stack for Reliable Services</span></span>
<span data-ttu-id="f37f2-104">Hola servicios confiables marco de trabajo permite servicio pila de comunicación de los autores toochoose Hola que deseen toouse para su servicio.</span><span class="sxs-lookup"><span data-stu-id="f37f2-104">hello Reliable Services framework allows service authors toochoose hello communication stack that they want toouse for their service.</span></span> <span data-ttu-id="f37f2-105">Puede conectar en la pila de comunicación de Hola de su elección a través de hello **ICommunicationListener** procedentes de hello [CreateServiceReplicaListeners o CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) métodos.</span><span class="sxs-lookup"><span data-stu-id="f37f2-105">They can plug in hello communication stack of their choice via hello **ICommunicationListener** returned from hello [CreateServiceReplicaListeners or CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methods.</span></span> <span data-ttu-id="f37f2-106">marco de trabajo de Hello proporciona una implementación de pila de comunicaciones de hello en función de hello Windows Communication Foundation (WCF) para los autores de servicio que desee toouse comunicación basada en WCF.</span><span class="sxs-lookup"><span data-stu-id="f37f2-106">hello framework provides an implementation of hello communication stack based on hello Windows Communication Foundation (WCF) for service authors who want toouse WCF-based communication.</span></span>

## <a name="wcf-communication-listener"></a><span data-ttu-id="f37f2-107">Agente de escucha de comunicación WCF</span><span class="sxs-lookup"><span data-stu-id="f37f2-107">WCF Communication Listener</span></span>
<span data-ttu-id="f37f2-108">implementación de Hello específicas de WCF de **ICommunicationListener** proporciona hello **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** clase.</span><span class="sxs-lookup"><span data-stu-id="f37f2-108">hello WCF-specific implementation of **ICommunicationListener** is provided by hello **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** class.</span></span>

<span data-ttu-id="f37f2-109">Pongamos que tenemos un contrato de servicio del tipo `ICalculator`</span><span class="sxs-lookup"><span data-stu-id="f37f2-109">Lest say we have a service contract of type `ICalculator`</span></span>

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

<span data-ttu-id="f37f2-110">Podemos crear un agente de escucha de comunicación de WCF Hola Hola de servicio después de la forma.</span><span class="sxs-lookup"><span data-stu-id="f37f2-110">We can create a WCF communication listener in hello service hello following manner.</span></span>

```csharp

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[] { new ServiceReplicaListener((context) =>
        new WcfCommunicationListener<ICalculator>(
            wcfServiceObject:this,
            serviceContext:context,
            //
            // hello name of hello endpoint configured in hello ServiceManifest under hello Endpoints section
            // that identifies hello endpoint that hello WCF ServiceHost should listen on.
            //
            endpointResourceName: "WcfServiceEndpoint",

            //
            // Populate hello binding information that you want hello service toouse.
            //
            listenerBinding: WcfUtility.CreateTcpListenerBinding()
        )
    )};
}

```

## <a name="writing-clients-for-hello-wcf-communication-stack"></a><span data-ttu-id="f37f2-111">Escribir clientes de pila de comunicación de WCF de Hola</span><span class="sxs-lookup"><span data-stu-id="f37f2-111">Writing clients for hello WCF communication stack</span></span>
<span data-ttu-id="f37f2-112">Para escribir clientes proporciona toocommunicate con los servicios mediante WCF, framework hello **WcfClientCommunicationFactory**, que es la implementación de hello específicas de WCF de [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="f37f2-112">For writing clients toocommunicate with services by using WCF, hello framework provides **WcfClientCommunicationFactory**, which is hello WCF-specific implementation of [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span></span>

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

<span data-ttu-id="f37f2-113">canal de comunicación de WCF de Hello puede tener acceso desde hello **WcfCommunicationClient** creado por hello **WcfCommunicationClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="f37f2-113">hello WCF communication channel can be accessed from hello **WcfCommunicationClient** created by hello **WcfCommunicationClientFactory**.</span></span>

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

<span data-ttu-id="f37f2-114">Código de cliente puede usar hello **WcfCommunicationClientFactory** junto con hello **WcfCommunicationClient** que implementa **ServicePartitionClient** toodetermine Hola extremo de servicio y comunicarse con el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="f37f2-114">Client code can use hello **WcfCommunicationClientFactory** along with hello **WcfCommunicationClient** which implements **ServicePartitionClient** toodetermine hello service endpoint and communicate with hello service.</span></span>

```csharp
// Create binding
Binding binding = WcfUtility.CreateTcpClientBinding();
// Create a partition resolver
IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();
// create a  WcfCommunicationClientFactory object.
var wcfClientFactory = new WcfCommunicationClientFactory<ICalculator>
    (clientBinding: binding, servicePartitionResolver: partitionResolver);

//
// Create a client for communicating with hello ICalculator service that has been created with the
// Singleton partition scheme.
//
var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
                wcfClientFactory,
                ServiceUri,
                ServicePartitionKey.Singleton);

//
// Call hello service tooperform hello operation.
//
var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
                client => client.Channel.Add(2, 3)).Result;

```
> [!NOTE]
> <span data-ttu-id="f37f2-115">Hola ServicePartitionResolver, se supone que cliente Hola se está ejecutando en el mismo clúster que el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="f37f2-115">hello default ServicePartitionResolver assumes that hello client is running in same cluster as hello service.</span></span> <span data-ttu-id="f37f2-116">Si es no Hola así, cree un objeto ServicePartitionResolver y pasar en los extremos de conexión del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="f37f2-116">If that is not hello case, create a ServicePartitionResolver object and pass in hello cluster connection endpoints.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f37f2-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f37f2-117">Next steps</span></span>
* [<span data-ttu-id="f37f2-118">Llamada a procedimiento remoto con la comunicación remota de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="f37f2-118">Remote procedure call with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="f37f2-119">Web API con OWIN en Reliable Services</span><span class="sxs-lookup"><span data-stu-id="f37f2-119">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="f37f2-120">Protección de la comunicación para Reliable Services</span><span class="sxs-lookup"><span data-stu-id="f37f2-120">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)

