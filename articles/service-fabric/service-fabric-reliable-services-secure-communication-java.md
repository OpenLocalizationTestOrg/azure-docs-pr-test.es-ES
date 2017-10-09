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
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="d3399-103">Ayuda para garantizar la comunicación de los servicios de Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d3399-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3399-104">C# en Windows</span><span class="sxs-lookup"><span data-stu-id="d3399-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="d3399-105">Java en Linux</span><span class="sxs-lookup"><span data-stu-id="d3399-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="d3399-106">Ayuda para garantizar un servicio cuando usa la comunicación remota para los servicios</span><span class="sxs-lookup"><span data-stu-id="d3399-106">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="d3399-107">Usaremos una existente [ejemplo](service-fabric-reliable-services-communication-remoting-java.md) que explica cómo tooset el acceso remoto para servicios de confianza.</span><span class="sxs-lookup"><span data-stu-id="d3399-107">We'll be using an existing [example](service-fabric-reliable-services-communication-remoting-java.md) that explains how tooset up remoting for reliable services.</span></span> <span data-ttu-id="d3399-108">toohelp proteger un servicio cuando se utiliza la comunicación remota de servicio, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d3399-108">toohelp secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="d3399-109">Crear una interfaz, `HelloWorldStateless`, que define los métodos de Hola que estarán disponibles para una llamada a procedimiento remoto en su servicio.</span><span class="sxs-lookup"><span data-stu-id="d3399-109">Create an interface, `HelloWorldStateless`, that defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="d3399-110">El servicio va a usar `FabricTransportServiceRemotingListener`, que se declara en hello `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` paquete.</span><span class="sxs-lookup"><span data-stu-id="d3399-110">Your service will use `FabricTransportServiceRemotingListener`, which is declared in hello `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` package.</span></span> <span data-ttu-id="d3399-111">Se trata de una implementación de `CommunicationListener` que ofrece capacidades de comunicación remota.</span><span class="sxs-lookup"><span data-stu-id="d3399-111">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span>

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
2. <span data-ttu-id="d3399-112">Agregue la configuración de escucha y las credenciales de seguridad.</span><span class="sxs-lookup"><span data-stu-id="d3399-112">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="d3399-113">Asegúrese de que ese certificado de Hola que quiere que la comunicación del servicio está instalada en todos los nodos Hola Hola clúster segura toohelp de toouse.</span><span class="sxs-lookup"><span data-stu-id="d3399-113">Make sure that hello certificate that you want toouse toohelp secure your service communication is installed on all hello nodes in hello cluster.</span></span> <span data-ttu-id="d3399-114">Hay dos formas de proporcionar la configuración de escucha y las credenciales de seguridad:</span><span class="sxs-lookup"><span data-stu-id="d3399-114">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="d3399-115">Proporcionarlas utilizando un [paquete de configuración](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="d3399-115">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="d3399-116">Agregar un `TransportSettings` sección en el archivo de hello settings.xml.</span><span class="sxs-lookup"><span data-stu-id="d3399-116">Add a `TransportSettings` section in hello settings.xml file.</span></span>

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

       <span data-ttu-id="d3399-117">En este caso, Hola `createServiceInstanceListeners` método tendrá un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="d3399-117">In this case, hello `createServiceInstanceListeners` method will look like this:</span></span>

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        <span data-ttu-id="d3399-118">Si agrega un `TransportSettings` sección hello settings.xml archivo sin ningún prefijo `FabricTransportListenerSettings` cargará todas las configuraciones de Hola de esta sección de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d3399-118">If you add a `TransportSettings` section in hello settings.xml file without any prefix, `FabricTransportListenerSettings` will load all hello settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="d3399-119">En este caso, Hola `CreateServiceInstanceListeners` método tendrá un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="d3399-119">In this case, hello `CreateServiceInstanceListeners` method will look like this:</span></span>

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. <span data-ttu-id="d3399-120">Cuando se llama a métodos en un servicio seguro mediante el uso de pila de comunicación remota de hello, en lugar de usar hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` clase toocreate un proxy de servicio, utilice `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="d3399-120">When you call methods on a secured service by using hello remoting stack, instead of using hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class toocreate a service proxy, use `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span></span>

    <span data-ttu-id="d3399-121">Si el código de cliente de Hola se ejecuta como parte de un servicio, puede cargar `FabricTransportSettings` de archivo de hello settings.xml.</span><span class="sxs-lookup"><span data-stu-id="d3399-121">If hello client code is running as part of a service, you can load `FabricTransportSettings` from hello settings.xml file.</span></span> <span data-ttu-id="d3399-122">Cree una sección de TransportSettings que es el código del servicio toohello similares, como se muestra anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d3399-122">Create a TransportSettings section that is similar toohello service code, as shown earlier.</span></span> <span data-ttu-id="d3399-123">Asegúrese de hello después el código de cliente de toohello de cambios:</span><span class="sxs-lookup"><span data-stu-id="d3399-123">Make hello following changes toohello client code:</span></span>

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
