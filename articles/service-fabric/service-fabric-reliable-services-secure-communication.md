---
title: "aaaHelp una comunicación segura para los servicios de Azure Service Fabric | Documentos de Microsoft"
description: "Información general sobre cómo toohelp proteger la comunicación de servicios de confianza que se ejecutan en un clúster de Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: vturecek
ms.assetid: fc129c1a-fbe4-4339-83ae-0e69a41654e0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: 15201eb503322b17db329b319f1f42860b0f0c6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="152f5-103">Ayuda para garantizar la comunicación de los servicios de Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="152f5-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="152f5-104">C# en Windows</span><span class="sxs-lookup"><span data-stu-id="152f5-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="152f5-105">Java en Linux</span><span class="sxs-lookup"><span data-stu-id="152f5-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

<span data-ttu-id="152f5-106">La seguridad es uno de los aspectos más importantes de Hola de comunicación.</span><span class="sxs-lookup"><span data-stu-id="152f5-106">Security is one of hello most important aspects of communication.</span></span> <span data-ttu-id="152f5-107">marco de aplicación de servicios de confianza de Hello proporciona unos pilas de la comunicación creada previamente y herramientas que puede utilizar la seguridad tooimprove.</span><span class="sxs-lookup"><span data-stu-id="152f5-107">hello Reliable Services application framework provides a few prebuilt communication stacks and tools that you can use tooimprove security.</span></span> <span data-ttu-id="152f5-108">En este artículo se habla acerca de cómo tooimprove seguridad cuando se usa servicios de comunicación remota y Hola pila de comunicación de Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="152f5-108">This article talks about how tooimprove security when you're using service remoting and hello Windows Communication Foundation (WCF) communication stack.</span></span>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="152f5-109">Ayuda para garantizar un servicio cuando usa la comunicación remota para los servicios</span><span class="sxs-lookup"><span data-stu-id="152f5-109">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="152f5-110">Estamos usando una existente [ejemplo](service-fabric-reliable-services-communication-remoting.md) que explica cómo tooset el acceso remoto para servicios de confianza.</span><span class="sxs-lookup"><span data-stu-id="152f5-110">We are using an existing [example](service-fabric-reliable-services-communication-remoting.md) that explains how tooset up remoting for reliable services.</span></span> <span data-ttu-id="152f5-111">toohelp proteger un servicio cuando se utiliza la comunicación remota de servicio, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="152f5-111">toohelp secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="152f5-112">Crear una interfaz, `IHelloWorldStateful`, que define los métodos de Hola que estarán disponibles para una llamada a procedimiento remoto en su servicio.</span><span class="sxs-lookup"><span data-stu-id="152f5-112">Create an interface, `IHelloWorldStateful`, that defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="152f5-113">El servicio va a usar `FabricTransportServiceRemotingListener`, que se declara en hello `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="152f5-113">Your service will use `FabricTransportServiceRemotingListener`, which is declared in hello `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` namespace.</span></span> <span data-ttu-id="152f5-114">Se trata de una implementación de `ICommunicationListener` que ofrece capacidades de comunicación remota.</span><span class="sxs-lookup"><span data-stu-id="152f5-114">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span>

    ```csharp
    public interface IHelloWorldStateful : IService
    {
        Task<string> GetHelloWorld();
    }

    internal class HelloWorldStateful : StatefulService, IHelloWorldStateful
    {
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]{
                    new ServiceReplicaListener(
                        (context) => new FabricTransportServiceRemotingListener(context,this))};
        }

        public Task<string> GetHelloWorld()
        {
            return Task.FromResult("Hello World!");
        }
    }
    ```
2. <span data-ttu-id="152f5-115">Agregue la configuración de escucha y las credenciales de seguridad.</span><span class="sxs-lookup"><span data-stu-id="152f5-115">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="152f5-116">Asegúrese de que ese certificado de Hola que quiere que la comunicación del servicio está instalada en todos los nodos Hola Hola clúster segura toohelp de toouse.</span><span class="sxs-lookup"><span data-stu-id="152f5-116">Make sure that hello certificate that you want toouse toohelp secure your service communication is installed on all hello nodes in hello cluster.</span></span> <span data-ttu-id="152f5-117">Hay dos formas de proporcionar la configuración de escucha y las credenciales de seguridad:</span><span class="sxs-lookup"><span data-stu-id="152f5-117">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="152f5-118">Proporcione directamente en el código del servicio de hello:</span><span class="sxs-lookup"><span data-stu-id="152f5-118">Provide them directly in hello service code:</span></span>

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           FabricTransportRemotingListenerSettings  listenerSettings = new FabricTransportRemotingListenerSettings
           {
               MaxMessageSize = 10000000,
               SecurityCredentials = GetSecurityCredentials()
           };
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(context,this,listenerSettings))
           };
       }

       private static SecurityCredentials GetSecurityCredentials()
       {
           // Provide certificate details.
           var x509Credentials = new X509Credentials
           {
               FindType = X509FindType.FindByThumbprint,
               FindValue = "4FEF3950642138446CC364A396E1E881DB76B48C",
               StoreLocation = StoreLocation.LocalMachine,
               StoreName = "My",
               ProtectionLevel = ProtectionLevel.EncryptAndSign
           };
           x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
           x509Credentials.RemoteCertThumbprints.Add("9FEF3950642138446CC364A396E1E881DB76B483");
           return x509Credentials;
       }
       ```
   2. <span data-ttu-id="152f5-119">Proporcionarlas utilizando un [paquete de configuración](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="152f5-119">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="152f5-120">Agregar un `TransportSettings` sección en el archivo de hello settings.xml.</span><span class="sxs-lookup"><span data-stu-id="152f5-120">Add a `TransportSettings` section in hello settings.xml file.</span></span>

       ```xml
       <Section Name="HelloWorldStatefulTransportSettings">
           <Parameter Name="MaxMessageSize" Value="10000000" />
           <Parameter Name="SecurityCredentialsType" Value="X509" />
           <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
           <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
           <Parameter Name="CertificateRemoteThumbprints" Value="9FEF3950642138446CC364A396E1E881DB76B483" />
           <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
           <Parameter Name="CertificateStoreName" Value="My" />
           <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
           <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
       </Section>
       ```

       <span data-ttu-id="152f5-121">En este caso, Hola `CreateServiceReplicaListeners` método tendrá un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="152f5-121">In this case, hello `CreateServiceReplicaListeners` method will look like this:</span></span>

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(
                       context,this,FabricTransportRemotingListenerSettings .LoadFrom("HelloWorldStatefulTransportSettings")))
           };
       }
       ```

        <span data-ttu-id="152f5-122">Si agrega un `TransportSettings` sección en el archivo de hello settings.xml, `FabricTransportRemotingListenerSettings ` cargará todas las configuraciones de Hola de esta sección de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="152f5-122">If you add a `TransportSettings` section in hello settings.xml file , `FabricTransportRemotingListenerSettings ` will load all hello settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="152f5-123">En este caso, Hola `CreateServiceReplicaListeners` método tendrá un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="152f5-123">In this case, hello `CreateServiceReplicaListeners` method will look like this:</span></span>

        ```csharp
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]
            {
                return new[]{
                        new ServiceReplicaListener(
                            (context) => new FabricTransportServiceRemotingListener(context,this))};
            };
        }
        ```
3. <span data-ttu-id="152f5-124">Cuando se llama a métodos en un servicio seguro mediante el uso de pila de comunicación remota de hello, en lugar de usar hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` clase toocreate un proxy de servicio, utilice `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="152f5-124">When you call methods on a secured service by using hello remoting stack, instead of using hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class toocreate a service proxy, use `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span></span> <span data-ttu-id="152f5-125">Pase `FabricTransportRemotingSettings`, que contiene `SecurityCredentials`.</span><span class="sxs-lookup"><span data-stu-id="152f5-125">Pass in `FabricTransportRemotingSettings`, which contains `SecurityCredentials`.</span></span>

    ```csharp

    var x509Credentials = new X509Credentials
    {
        FindType = X509FindType.FindByThumbprint,
        FindValue = "9FEF3950642138446CC364A396E1E881DB76B483",
        StoreLocation = StoreLocation.LocalMachine,
        StoreName = "My",
        ProtectionLevel = ProtectionLevel.EncryptAndSign
    };
    x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
    x509Credentials.RemoteCertThumbprints.Add("4FEF3950642138446CC364A396E1E881DB76B48C");

    FabricTransportRemotingSettings transportSettings = new FabricTransportRemotingSettings
    {
        SecurityCredentials = x509Credentials,
    };

    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(transportSettings));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="152f5-126">Si el código de cliente de Hola se ejecuta como parte de un servicio, puede cargar `FabricTransportRemotingSettings` de archivo de hello settings.xml.</span><span class="sxs-lookup"><span data-stu-id="152f5-126">If hello client code is running as part of a service, you can load `FabricTransportRemotingSettings` from hello settings.xml file.</span></span> <span data-ttu-id="152f5-127">Cree una sección de HelloWorldClientTransportSettings que es el código del servicio toohello similares, como se muestra anteriormente.</span><span class="sxs-lookup"><span data-stu-id="152f5-127">Create a HelloWorldClientTransportSettings section that is similar toohello service code, as shown earlier.</span></span> <span data-ttu-id="152f5-128">Asegúrese de hello después el código de cliente de toohello de cambios:</span><span class="sxs-lookup"><span data-stu-id="152f5-128">Make hello following changes toohello client code:</span></span>

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="152f5-129">Si no se está ejecutando el cliente de hello como parte de un servicio, puede crear un archivo client_name.settings.xml en Hola misma ubicación donde haya client_name.exe Hola.</span><span class="sxs-lookup"><span data-stu-id="152f5-129">If hello client is not running as part of a service, you can create a client_name.settings.xml file in hello same location where hello client_name.exe is.</span></span> <span data-ttu-id="152f5-130">A continuación, cree una sección TransportSettings en ese archivo.</span><span class="sxs-lookup"><span data-stu-id="152f5-130">Then create a TransportSettings section in that file.</span></span>

    <span data-ttu-id="152f5-131">Servicio toohello similar, si agrega un `TransportSettings` sección de cliente settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` carga todos los valores de configuración de Hola de esta sección de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="152f5-131">Similar toohello service, if you add a `TransportSettings` section in client settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` loads all hello settings from this section by default.</span></span>

    <span data-ttu-id="152f5-132">En ese caso, hello anterior se aún más simplifica el código:</span><span class="sxs-lookup"><span data-stu-id="152f5-132">In that case, hello earlier code is even further simplified:</span></span>  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a><span data-ttu-id="152f5-133">Ayuda para garantizar un servicio cuando se utiliza una pila de comunicación basada en WCF</span><span class="sxs-lookup"><span data-stu-id="152f5-133">Help secure a service when you're using a WCF-based communication stack</span></span>
<span data-ttu-id="152f5-134">Estamos usando una existente [ejemplo](service-fabric-reliable-services-communication-wcf.md) que explica cómo tooset la una comunicación basada en WCF pila para servicios de confianza.</span><span class="sxs-lookup"><span data-stu-id="152f5-134">We are using an existing [example](service-fabric-reliable-services-communication-wcf.md) that explains how tooset up a WCF-based communication stack for reliable services.</span></span> <span data-ttu-id="152f5-135">toohelp proteger un servicio cuando se usa una pila de comunicación basada en WCF, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="152f5-135">toohelp secure a service when you're using a WCF-based communication stack, follow these steps:</span></span>

1. <span data-ttu-id="152f5-136">Para el servicio de hello, necesita el agente de escucha de toohelp Hola segura WCF comunicación (`WcfCommunicationListener`) creados por usted.</span><span class="sxs-lookup"><span data-stu-id="152f5-136">For hello service, you need toohelp secure hello WCF communication listener (`WcfCommunicationListener`) that you create.</span></span> <span data-ttu-id="152f5-137">toodo, modificar hello `CreateServiceReplicaListeners` método.</span><span class="sxs-lookup"><span data-stu-id="152f5-137">toodo this, modify hello `CreateServiceReplicaListeners` method.</span></span>

    ```csharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        return new[]
        {
            new ServiceReplicaListener(
                this.CreateWcfCommunicationListener)
        };
    }

    private WcfCommunicationListener<ICalculator> CreateWcfCommunicationListener(StatefulServiceContext context)
    {
       var wcfCommunicationListener = new WcfCommunicationListener<ICalculator>(
            serviceContext:context,
            wcfServiceObject:this,
            // For this example, we will be using NetTcpBinding.
            listenerBinding: GetNetTcpBinding(),
            endpointResourceName:"WcfServiceEndpoint");

        // Add certificate details in hello ServiceHost credentials.
        wcfCommunicationListener.ServiceHost.Credentials.ServiceCertificate.SetCertificate(
            StoreLocation.LocalMachine,
            StoreName.My,
            X509FindType.FindByThumbprint,
            "9DC906B169DC4FAFFD1697AC781E806790749D2F");
        return wcfCommunicationListener;
    }

    private static NetTcpBinding GetNetTcpBinding()
    {
        NetTcpBinding b = new NetTcpBinding(SecurityMode.TransportWithMessageCredential);
        b.Security.Message.ClientCredentialType = MessageCredentialType.Certificate;
        return b;
    }
    ```
2. <span data-ttu-id="152f5-138">En el cliente de hello, Hola `WcfCommunicationClient` clase creada en hello anterior [ejemplo](service-fabric-reliable-services-communication-wcf.md) permanece sin cambios.</span><span class="sxs-lookup"><span data-stu-id="152f5-138">In hello client, hello `WcfCommunicationClient` class that was created in hello previous [example](service-fabric-reliable-services-communication-wcf.md) remains unchanged.</span></span> <span data-ttu-id="152f5-139">Pero debe hello toooverride `CreateClientAsync` método `WcfCommunicationClientFactory`:</span><span class="sxs-lookup"><span data-stu-id="152f5-139">But you need toooverride hello `CreateClientAsync` method of `WcfCommunicationClientFactory`:</span></span>

    ```csharp
    public class SecureWcfCommunicationClientFactory<TServiceContract> : WcfCommunicationClientFactory<TServiceContract> where TServiceContract : class
    {
        private readonly Binding clientBinding;
        private readonly object callbackObject;
        public SecureWcfCommunicationClientFactory(
            Binding clientBinding,
            IEnumerable<IExceptionHandler> exceptionHandlers = null,
            IServicePartitionResolver servicePartitionResolver = null,
            string traceId = null,
            object callback = null)
            : base(clientBinding, exceptionHandlers, servicePartitionResolver,traceId,callback)
        {
            this.clientBinding = clientBinding;
            this.callbackObject = callback;
        }

        protected override Task<WcfCommunicationClient<TServiceContract>> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
        {
            var endpointAddress = new EndpointAddress(new Uri(endpoint));
            ChannelFactory<TServiceContract> channelFactory;
            if (this.callbackObject != null)
            {
                channelFactory = new DuplexChannelFactory<TServiceContract>(
                this.callbackObject,
                this.clientBinding,
                endpointAddress);
            }
            else
            {
                channelFactory = new ChannelFactory<TServiceContract>(this.clientBinding, endpointAddress);
            }
            // Add certificate details toohello ChannelFactory credentials.
            // These credentials will be used by hello clients created by
            // SecureWcfCommunicationClientFactory.  
            channelFactory.Credentials.ClientCertificate.SetCertificate(
                StoreLocation.LocalMachine,
                StoreName.My,
                X509FindType.FindByThumbprint,
                "9DC906B169DC4FAFFD1697AC781E806790749D2F");
            var channel = channelFactory.CreateChannel();
            var clientChannel = ((IClientChannel)channel);
            clientChannel.OperationTimeout = this.clientBinding.ReceiveTimeout;
            return Task.FromResult(this.CreateWcfCommunicationClient(channel));
        }
    }
    ```

    <span data-ttu-id="152f5-140">Use `SecureWcfCommunicationClientFactory` toocreate un cliente de comunicación de WCF (`WcfCommunicationClient`).</span><span class="sxs-lookup"><span data-stu-id="152f5-140">Use `SecureWcfCommunicationClientFactory` toocreate a WCF communication client (`WcfCommunicationClient`).</span></span> <span data-ttu-id="152f5-141">Usar métodos de servicio de hello cliente tooinvoke.</span><span class="sxs-lookup"><span data-stu-id="152f5-141">Use hello client tooinvoke service methods.</span></span>

    ```csharp
    IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();

    var wcfClientFactory = new SecureWcfCommunicationClientFactory<ICalculator>(clientBinding: GetNetTcpBinding(), servicePartitionResolver: partitionResolver);

    var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
        wcfClientFactory,
        ServiceUri,
        ServicePartitionKey.Singleton);

    var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
        client => client.Channel.Add(2, 3)).Result;
    ```

## <a name="next-steps"></a><span data-ttu-id="152f5-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="152f5-142">Next steps</span></span>
* [<span data-ttu-id="152f5-143">Web API con OWIN en Reliable Services</span><span class="sxs-lookup"><span data-stu-id="152f5-143">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
