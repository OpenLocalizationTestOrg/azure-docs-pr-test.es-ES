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
# <a name="service-remoting-with-reliable-services"></a>Comunicación remota de servicio con Reliable Services
Para los servicios que no están vinculados tooa protocolo de comunicación determinada o pila, por ejemplo, WebAPI, Windows Communication Foundation (WCF) u otras personas, el marco de trabajo de hello Services confiable proporciona un tooquickly del mecanismo de comunicación remota y configurar fácilmente la llamada a procedimiento remoto para los servicios.

## <a name="set-up-remoting-on-a-service"></a>Configurar la comunicación remota en un servicio
La configuración de la comunicación remota para un servicio se realiza en dos sencillos pasos:

1. Crear una interfaz para el servicio tooimplement. Esta interfaz define métodos de Hola que estarán disponibles para una llamada a procedimiento remoto en su servicio. métodos de Hello deben ser de devolución de tarea métodos asincrónicos. debe implementar la interfaz de Hello `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal que Hola servicio tiene una interfaz de comunicación remota.
2. Utilice un agente de escucha de comunicación remota en su servicio. Se trata de una implementación de `ICommunicationListener` que ofrece capacidades de comunicación remota. Hola `Microsoft.ServiceFabric.Services.Remoting.Runtime` espacio de nombres contiene un método de extensión,`CreateServiceRemotingListener` para sin estado y con estado de servicios que puede toocreate usa un agente de escucha de comunicación remota usar protocolo de transporte de comunicación remota de Hola de forma predeterminada.

Nota: Hola `Remoting` espacio de nombres está disponible como un paquete de nuget independiente denominado`Microsoft.ServiceFabric.Services.Remoting` 

Por ejemplo, hello siguiente sin estado servicio expone un único método tooget "¡Hello World" a través de una llamada a procedimiento remoto.

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
> Hello hello y argumentos devuelven tipos de interfaz de servicio de hello pueden ser cualquier tipo simple, compleja o personalizada, pero deben ser serializables por hello .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).
>
>

## <a name="call-remote-service-methods"></a>Llamar a métodos de servicio remoto
Llamadas a métodos en un servicio mediante el uso de la pila de comunicación remota de Hola se realiza mediante un servicio de toohello de proxy local a través de hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` clase. Hola `ServiceProxy` método crea un proxy local mediante el uso de hello implementa la misma interfaz que Hola servicio. Con ese proxy, se puede simplemente llamar a métodos en la interfaz de hello remotamente.

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

el marco de trabajo de Hello remoting propaga las excepciones producidas en el cliente del servicio toohello de Hola. Lógica de control de excepciones por lo que en el cliente de hello mediante el uso de `ServiceProxy` directamente puede controlar las excepciones que Hola servicio inicia.

## <a name="service-proxy-lifetime"></a>Duración del proxy de servicio
La creación de ServiceProxy es una operación ligera, por lo que el usuario puede crearla todas las veces que lo necesite. El proxy de servicio puede volver a usarse siempre que el usuario lo necesite. Usuario pueda volver a utilizar Hola mismo proxy en el caso de excepción. Cada ServiceProxy contiene mensajes de toosend de cliente que se utiliza la comunicación a través de la conexión de Hola. Al invocar la API, tenemos toosee comprobación interna si el cliente de comunicación que se utiliza es válido. En función de ese resultado, se vuelva a crea a cliente de comunicación de Hola. Por lo tanto, el usuario no es necesario toorecreate serviceproxy en caso de excepción.

### <a name="serviceproxyfactory-lifetime"></a>Duración de ServiceProxyFactory
[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) es una fábrica que crea un proxy para interfaces remotas diferentes. Si utilizas API ServiceProxy.Create para crear el proxy, el marco de trabajo crea hello singelton ServiceProxyFactory.
Resulta útil toocreate uno manualmente cuando necesite toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) propiedades.
Factory es una operación costosa. ServiceProxyFactory mantiene la memoria caché del cliente de comunicación.
Procedimiento recomendado es toocache ServiceProxyFactory tanto como sea posible.

## <a name="remoting-exception-handling"></a>Control de excepciones remota
Todos los Hola remoto excepción API del servicio, se envían cliente toohello espera como AggregateException. RemoteExceptions debe ser Serializable de DataContract en caso contrario, [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) se produce toohello proxy API con error de serialización de hello en ella.

ServiceProxy controlar todas las excepciones de conmutación por error para la partición de servicio de Hola se crea para. Volver a resuelve los puntos de conexión de hello si hay Failover Exceptions(Non-Transient Exceptions) y reintentos llamada Hola con punto de conexión correcto Hola. El número de reintentos para la excepción de conmutación por error es indefinido.
En el caso de TransientExceptions, solo reintenta llamada Hola.

[OperationRetrySettings] proporciona los parámetros de reintento predeterminados. (https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) Usuario puede configurar estos valores pasando OperationRetrySettings objeto tooServiceProxyFactory constructor.

## <a name="next-steps"></a>Pasos siguientes
* [Web API con OWIN en Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Comunicación WCF con Reliable Services](service-fabric-reliable-services-communication-wcf.md)
* [Protección de la comunicación para Reliable Services](service-fabric-reliable-services-secure-communication.md)
