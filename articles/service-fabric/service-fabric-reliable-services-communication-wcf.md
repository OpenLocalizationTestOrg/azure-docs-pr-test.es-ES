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
# <a name="wcf-based-communication-stack-for-reliable-services"></a>Pila de comunicación basada en WCF de Reliable Services
Hola servicios confiables marco de trabajo permite servicio pila de comunicación de los autores toochoose Hola que deseen toouse para su servicio. Puede conectar en la pila de comunicación de Hola de su elección a través de hello **ICommunicationListener** procedentes de hello [CreateServiceReplicaListeners o CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) métodos. marco de trabajo de Hello proporciona una implementación de pila de comunicaciones de hello en función de hello Windows Communication Foundation (WCF) para los autores de servicio que desee toouse comunicación basada en WCF.

## <a name="wcf-communication-listener"></a>Agente de escucha de comunicación WCF
implementación de Hello específicas de WCF de **ICommunicationListener** proporciona hello **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** clase.

Pongamos que tenemos un contrato de servicio del tipo `ICalculator`

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

Podemos crear un agente de escucha de comunicación de WCF Hola Hola de servicio después de la forma.

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

## <a name="writing-clients-for-hello-wcf-communication-stack"></a>Escribir clientes de pila de comunicación de WCF de Hola
Para escribir clientes proporciona toocommunicate con los servicios mediante WCF, framework hello **WcfClientCommunicationFactory**, que es la implementación de hello específicas de WCF de [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

canal de comunicación de WCF de Hello puede tener acceso desde hello **WcfCommunicationClient** creado por hello **WcfCommunicationClientFactory**.

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

Código de cliente puede usar hello **WcfCommunicationClientFactory** junto con hello **WcfCommunicationClient** que implementa **ServicePartitionClient** toodetermine Hola extremo de servicio y comunicarse con el servicio de Hola.

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
> Hola ServicePartitionResolver, se supone que cliente Hola se está ejecutando en el mismo clúster que el servicio de Hola. Si es no Hola así, cree un objeto ServicePartitionResolver y pasar en los extremos de conexión del clúster de Hola.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* [Llamada a procedimiento remoto con la comunicación remota de Reliable Services](service-fabric-reliable-services-communication-remoting.md)
* [Web API con OWIN en Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Protección de la comunicación para Reliable Services](service-fabric-reliable-services-secure-communication.md)

