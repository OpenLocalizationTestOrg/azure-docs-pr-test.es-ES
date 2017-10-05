---
title: "Pila comunicación de WCF de Reliable Services | Microsoft Docs"
description: "La pila de comunicación de WCF integrada en Service Fabric ofrece comunicación de WCF del servicio de cliente para Reliable Services."
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
ms.openlocfilehash: 7037620ebdc26a9f18531064bf45d058f5060e39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="wcf-based-communication-stack-for-reliable-services"></a><span data-ttu-id="f0e94-103">Pila de comunicación basada en WCF de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="f0e94-103">WCF-based communication stack for Reliable Services</span></span>
<span data-ttu-id="f0e94-104">El marco de Reliable Services permite a los autores de servicio elegir la pila de comunicación que desean usar para su servicio.</span><span class="sxs-lookup"><span data-stu-id="f0e94-104">The Reliable Services framework allows service authors to choose the communication stack that they want to use for their service.</span></span> <span data-ttu-id="f0e94-105">Pueden conectar la pila de comunicaciones que deseen mediante la clase **ICommunicationListener** devuelta desde los métodos [CreateServiceReplicaListeners o CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) .</span><span class="sxs-lookup"><span data-stu-id="f0e94-105">They can plug in the communication stack of their choice via the **ICommunicationListener** returned from the [CreateServiceReplicaListeners or CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methods.</span></span> <span data-ttu-id="f0e94-106">El marco proporciona una implementación de la pila de comunicación basada en Windows Communication Foundation (WCF) para los autores de servicio que desean usar la comunicación basada en WCF.</span><span class="sxs-lookup"><span data-stu-id="f0e94-106">The framework provides an implementation of the communication stack based on the Windows Communication Foundation (WCF) for service authors who want to use WCF-based communication.</span></span>

## <a name="wcf-communication-listener"></a><span data-ttu-id="f0e94-107">Agente de escucha de comunicación WCF</span><span class="sxs-lookup"><span data-stu-id="f0e94-107">WCF Communication Listener</span></span>
<span data-ttu-id="f0e94-108">La implementación específica de WCF de **ICommunicationListener** la proporciona la clase **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener**.</span><span class="sxs-lookup"><span data-stu-id="f0e94-108">The WCF-specific implementation of **ICommunicationListener** is provided by the **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** class.</span></span>

<span data-ttu-id="f0e94-109">Pongamos que tenemos un contrato de servicio del tipo `ICalculator`</span><span class="sxs-lookup"><span data-stu-id="f0e94-109">Lest say we have a service contract of type `ICalculator`</span></span>

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

<span data-ttu-id="f0e94-110">Podemos crear un agente de escucha de comunicación de WCF en el servicio de la siguiente manera.</span><span class="sxs-lookup"><span data-stu-id="f0e94-110">We can create a WCF communication listener in the service the following manner.</span></span>

```csharp

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[] { new ServiceReplicaListener((context) =>
        new WcfCommunicationListener<ICalculator>(
            wcfServiceObject:this,
            serviceContext:context,
            //
            // The name of the endpoint configured in the ServiceManifest under the Endpoints section
            // that identifies the endpoint that the WCF ServiceHost should listen on.
            //
            endpointResourceName: "WcfServiceEndpoint",

            //
            // Populate the binding information that you want the service to use.
            //
            listenerBinding: WcfUtility.CreateTcpListenerBinding()
        )
    )};
}

```

## <a name="writing-clients-for-the-wcf-communication-stack"></a><span data-ttu-id="f0e94-111">Escritura de clientes para la pila de comunicación de WCF</span><span class="sxs-lookup"><span data-stu-id="f0e94-111">Writing clients for the WCF communication stack</span></span>
<span data-ttu-id="f0e94-112">Para que los clientes de escritura se comuniquen con los servicios mediante WCF, el marco proporciona la clase **WcfClientCommunicationFactory**, que es la implementación específica de WCF de la clase [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="f0e94-112">For writing clients to communicate with services by using WCF, the framework provides **WcfClientCommunicationFactory**, which is the WCF-specific implementation of [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span></span>

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

<span data-ttu-id="f0e94-113">Se puede acceder al canal de comunicación de WCF desde la clase **WcfCommunicationClient** creada por la clase **WcfCommunicationClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="f0e94-113">The WCF communication channel can be accessed from the **WcfCommunicationClient** created by the **WcfCommunicationClientFactory**.</span></span>

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

<span data-ttu-id="f0e94-114">El código de cliente puede usar la clase **WcfCommunicationClientFactor** y junto con **WcfCommunicationClient** que implementa **ServicePartitionClient** para determinar el punto de conexión de servicio y comunicarse con el servicio.</span><span class="sxs-lookup"><span data-stu-id="f0e94-114">Client code can use the **WcfCommunicationClientFactory** along with the **WcfCommunicationClient** which implements **ServicePartitionClient** to determine the service endpoint and communicate with the service.</span></span>

```csharp
// Create binding
Binding binding = WcfUtility.CreateTcpClientBinding();
// Create a partition resolver
IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();
// create a  WcfCommunicationClientFactory object.
var wcfClientFactory = new WcfCommunicationClientFactory<ICalculator>
    (clientBinding: binding, servicePartitionResolver: partitionResolver);

//
// Create a client for communicating with the ICalculator service that has been created with the
// Singleton partition scheme.
//
var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
                wcfClientFactory,
                ServiceUri,
                ServicePartitionKey.Singleton);

//
// Call the service to perform the operation.
//
var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
                client => client.Channel.Add(2, 3)).Result;

```
> [!NOTE]
> <span data-ttu-id="f0e94-115">ServicePartitionResolver asume que el cliente se ejecuta en el mismo clúster que el servicio.</span><span class="sxs-lookup"><span data-stu-id="f0e94-115">The default ServicePartitionResolver assumes that the client is running in same cluster as the service.</span></span> <span data-ttu-id="f0e94-116">Si no es así, cree un objeto ServicePartitionResolver y transfiera los puntos de conexión del clúster.</span><span class="sxs-lookup"><span data-stu-id="f0e94-116">If that is not the case, create a ServicePartitionResolver object and pass in the cluster connection endpoints.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f0e94-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f0e94-117">Next steps</span></span>
* [<span data-ttu-id="f0e94-118">Llamada a procedimiento remoto con la comunicación remota de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="f0e94-118">Remote procedure call with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="f0e94-119">Web API con OWIN en Reliable Services</span><span class="sxs-lookup"><span data-stu-id="f0e94-119">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="f0e94-120">Protección de la comunicación para Reliable Services</span><span class="sxs-lookup"><span data-stu-id="f0e94-120">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)

