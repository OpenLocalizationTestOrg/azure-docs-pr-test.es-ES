---
title: "aaaHelp una comunicación segura para los servicios de Azure Service Fabric | Documentos de Microsoft"
description: "Información general sobre cómo toohelp proteger la comunicación de servicios de confianza que se ejecutan en un clúster de Azure Service Fabric."
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
ms.openlocfilehash: 14db54d50c35478c1f2c156de0dba36f1427c8cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a>Ayuda para garantizar la comunicación de los servicios de Azure Service Fabric
> [!div class="op_single_selector"]
> * [C# en Windows](service-fabric-reliable-services-secure-communication.md)
> * [Java en Linux](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a>Ayuda para garantizar un servicio cuando usa la comunicación remota para los servicios
Usaremos una existente [ejemplo](service-fabric-reliable-services-communication-remoting-java.md) que explica cómo tooset el acceso remoto para servicios de confianza. toohelp proteger un servicio cuando se utiliza la comunicación remota de servicio, siga estos pasos:

1. Crear una interfaz, `HelloWorldStateless`, que define los métodos de Hola que estarán disponibles para una llamada a procedimiento remoto en su servicio. El servicio va a usar `FabricTransportServiceRemotingListener`, que se declara en hello `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` paquete. Se trata de una implementación de `CommunicationListener` que ofrece capacidades de comunicación remota.

    ```java
    public interface HelloWorldStateless extends Service {
        CompletableFuture<String> getHelloWorld();
    }

    class HelloWorldStatelessImpl extends StatelessService implements HelloWorldStateless {
        @Override
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
        return listeners;
        }

        public CompletableFuture<String> getHelloWorld() {
            return CompletableFuture.completedFuture("Hello World!");
        }
    }
    ```
2. Agregue la configuración de escucha y las credenciales de seguridad.

    Asegúrese de que ese certificado de Hola que quiere que la comunicación del servicio está instalada en todos los nodos Hola Hola clúster segura toohelp de toouse. Hay dos formas de proporcionar la configuración de escucha y las credenciales de seguridad:

   1. Proporcionarlas utilizando un [paquete de configuración](service-fabric-application-model.md):

       Agregar un `TransportSettings` sección en el archivo de hello settings.xml.

       ```xml
       <!--Section name should always end with "TransportSettings".-->
       <!--Here we are using a prefix "HelloWorldStateless".-->
        <Section Name="HelloWorldStatelessTransportSettings">
            <Parameter Name="MaxMessageSize" Value="10000000" />
            <Parameter Name="SecurityCredentialsType" Value="X509_2" />
            <Parameter Name="CertificatePath" Value="/path/to/cert/BD1C71E248B8C6834C151174DECDBDC02DE1D954.crt" />
            <Parameter Name="CertificateProtectionLevel" Value="EncryptandSign" />
            <Parameter Name="CertificateRemoteThumbprints" Value="BD1C71E248B8C6834C151174DECDBDC02DE1D954" />
        </Section>

       ```

       En este caso, Hola `createServiceInstanceListeners` método tendrá un aspecto similar al siguiente:

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        Si agrega un `TransportSettings` sección hello settings.xml archivo sin ningún prefijo `FabricTransportListenerSettings` cargará todas las configuraciones de Hola de esta sección de forma predeterminada.

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        En este caso, Hola `CreateServiceInstanceListeners` método tendrá un aspecto similar al siguiente:

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. Cuando se llama a métodos en un servicio seguro mediante el uso de pila de comunicación remota de hello, en lugar de usar hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` clase toocreate un proxy de servicio, utilice `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.

    Si el código de cliente de Hola se ejecuta como parte de un servicio, puede cargar `FabricTransportSettings` de archivo de hello settings.xml. Cree una sección de TransportSettings que es el código del servicio toohello similares, como se muestra anteriormente. Asegúrese de hello después el código de cliente de toohello de cambios:

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
