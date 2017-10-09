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
# <a name="service-remoting-with-reliable-services"></a>Comunicación remota de servicio con Reliable Services
> [!div class="op_single_selector"]
> * [C# en Windows](service-fabric-reliable-services-communication-remoting.md)
> * [Java en Linux](service-fabric-reliable-services-communication-remoting-java.md)
>
>

el marco de trabajo de Hello Services confiable proporciona un tooquickly del mecanismo de comunicación remota y configurar fácilmente la llamada a procedimiento remoto para los servicios.

## <a name="set-up-remoting-on-a-service"></a>Configurar la comunicación remota en un servicio
La configuración de la comunicación remota para un servicio se realiza en dos sencillos pasos:

1. Crear una interfaz para el servicio tooimplement. Esta interfaz define métodos de Hola que están disponibles para una llamada a procedimiento remoto en su servicio. métodos de Hello deben ser de devolución de tarea métodos asincrónicos. debe implementar la interfaz de Hello `microsoft.serviceFabric.services.remoting.Service` toosignal que Hola servicio tiene una interfaz de comunicación remota.
2. Utilice un agente de escucha de comunicación remota en su servicio. Se trata de una implementación de `CommunicationListener` que ofrece capacidades de comunicación remota. `FabricTransportServiceRemotingListener`puede ser toocreate usa un agente de escucha de comunicación remota con protocolo de transporte de comunicación remota de Hola de forma predeterminada.

Por ejemplo, hello siguiente sin estado servicio expone un único método tooget "¡Hello World" a través de una llamada a procedimiento remoto.

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
> Hola y argumentos de hello devuelven tipos de interfaz de servicio de hello pueden ser cualquier tipo simple, compleja o personalizada, pero deben ser serializables.
>
>

## <a name="call-remote-service-methods"></a>Llamar a métodos de servicio remoto
Llamadas a métodos en un servicio mediante el uso de la pila de comunicación remota de Hola se realiza mediante un servicio de toohello de proxy local a través de hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` clase. Hola `ServiceProxyBase` método crea un proxy local mediante el uso de hello implementa la misma interfaz que Hola servicio. Con ese proxy, se puede simplemente llamar a métodos en la interfaz de hello remotamente.

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

el marco de trabajo de Hello remoting propaga las excepciones producidas en el cliente del servicio toohello de Hola. Lógica de control de excepciones por lo que en el cliente de hello mediante el uso de `ServiceProxyBase` directamente puede controlar las excepciones que Hola servicio inicia.

## <a name="service-proxy-lifetime"></a>Duración del proxy de servicio
La creación de ServiceProxy es una operación ligera, por lo que el usuario puede crearla todas las veces que lo necesite. El proxy de servicio puede volver a usarse siempre que el usuario lo necesite. Usuario pueda volver a utilizar Hola mismo proxy en el caso de excepción. Cada ServiceProxy contiene mensajes de toosend de cliente que se utiliza de comunicación a través de la conexión de Hola. Al invocar la API, tenemos toosee comprobación interna si el cliente de comunicación que se utiliza es válido. En función de ese resultado, se vuelva a crea a cliente de comunicación de Hola. Por lo tanto, el usuario no es necesario toorecreate serviceproxy en caso de excepción.

### <a name="serviceproxyfactory-lifetime"></a>Duración de ServiceProxyFactory
[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) es un tejido que crea un proxy para distintas interfaces remotas. Si usa la API `ServiceProxyBase.create` para crear el proxy, el marco crea un `FabricServiceProxyFactory`.
Resulta útil toocreate uno manualmente cuando necesite toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) propiedades.
Factory es una operación costosa. `FabricServiceProxyFactory` mantiene la memoria caché de los clientes de comunicación.
Procedimiento recomendado es toocache `FabricServiceProxyFactory` tanto como sea posible.

## <a name="remoting-exception-handling"></a>Control de excepciones remota
Todos los Hola remoto excepción API del servicio, se envían como RuntimeException o FabricException toohello back-cliente.

ServiceProxy controlar todas las excepciones de conmutación por error para la partición de servicio de Hola se crea para. Volver a resuelve los puntos de conexión de hello si hay Failover Exceptions(Non-Transient Exceptions) y reintentos llamada Hola con punto de conexión correcto Hola. El número de reintentos para la excepción de conmutación por error es indefinido.
En el caso de TransientExceptions, solo reintenta llamada Hola.

[OperationRetrySettings] proporciona los parámetros de reintento predeterminados. (https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) Usuario puede configurar estos valores pasando OperationRetrySettings objeto tooServiceProxyFactory constructor.

## <a name="next-steps"></a>Pasos siguientes
* [Protección de la comunicación para Reliable Services](service-fabric-reliable-services-secure-communication.md)
