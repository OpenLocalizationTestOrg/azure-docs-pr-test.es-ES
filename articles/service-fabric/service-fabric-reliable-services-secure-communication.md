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
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a>Ayuda para garantizar la comunicación de los servicios de Azure Service Fabric
> [!div class="op_single_selector"]
> * [C# en Windows](service-fabric-reliable-services-secure-communication.md)
> * [Java en Linux](service-fabric-reliable-services-secure-communication-java.md)
>
>

La seguridad es uno de los aspectos más importantes de Hola de comunicación. marco de aplicación de servicios de confianza de Hello proporciona unos pilas de la comunicación creada previamente y herramientas que puede utilizar la seguridad tooimprove. En este artículo se habla acerca de cómo tooimprove seguridad cuando se usa servicios de comunicación remota y Hola pila de comunicación de Windows Communication Foundation (WCF).

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a>Ayuda para garantizar un servicio cuando usa la comunicación remota para los servicios
Estamos usando una existente [ejemplo](service-fabric-reliable-services-communication-remoting.md) que explica cómo tooset el acceso remoto para servicios de confianza. toohelp proteger un servicio cuando se utiliza la comunicación remota de servicio, siga estos pasos:

1. Crear una interfaz, `IHelloWorldStateful`, que define los métodos de Hola que estarán disponibles para una llamada a procedimiento remoto en su servicio. El servicio va a usar `FabricTransportServiceRemotingListener`, que se declara en hello `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` espacio de nombres. Se trata de una implementación de `ICommunicationListener` que ofrece capacidades de comunicación remota.

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
2. Agregue la configuración de escucha y las credenciales de seguridad.

    Asegúrese de que ese certificado de Hola que quiere que la comunicación del servicio está instalada en todos los nodos Hola Hola clúster segura toohelp de toouse. Hay dos formas de proporcionar la configuración de escucha y las credenciales de seguridad:

   1. Proporcione directamente en el código del servicio de hello:

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
   2. Proporcionarlas utilizando un [paquete de configuración](service-fabric-application-model.md):

       Agregar un `TransportSettings` sección en el archivo de hello settings.xml.

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

       En este caso, Hola `CreateServiceReplicaListeners` método tendrá un aspecto similar al siguiente:

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

        Si agrega un `TransportSettings` sección en el archivo de hello settings.xml, `FabricTransportRemotingListenerSettings ` cargará todas las configuraciones de Hola de esta sección de forma predeterminada.

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        En este caso, Hola `CreateServiceReplicaListeners` método tendrá un aspecto similar al siguiente:

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
3. Cuando se llama a métodos en un servicio seguro mediante el uso de pila de comunicación remota de hello, en lugar de usar hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` clase toocreate un proxy de servicio, utilice `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`. Pase `FabricTransportRemotingSettings`, que contiene `SecurityCredentials`.

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

    Si el código de cliente de Hola se ejecuta como parte de un servicio, puede cargar `FabricTransportRemotingSettings` de archivo de hello settings.xml. Cree una sección de HelloWorldClientTransportSettings que es el código del servicio toohello similares, como se muestra anteriormente. Asegúrese de hello después el código de cliente de toohello de cambios:

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    Si no se está ejecutando el cliente de hello como parte de un servicio, puede crear un archivo client_name.settings.xml en Hola misma ubicación donde haya client_name.exe Hola. A continuación, cree una sección TransportSettings en ese archivo.

    Servicio toohello similar, si agrega un `TransportSettings` sección de cliente settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` carga todos los valores de configuración de Hola de esta sección de forma predeterminada.

    En ese caso, hello anterior se aún más simplifica el código:  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a>Ayuda para garantizar un servicio cuando se utiliza una pila de comunicación basada en WCF
Estamos usando una existente [ejemplo](service-fabric-reliable-services-communication-wcf.md) que explica cómo tooset la una comunicación basada en WCF pila para servicios de confianza. toohelp proteger un servicio cuando se usa una pila de comunicación basada en WCF, siga estos pasos:

1. Para el servicio de hello, necesita el agente de escucha de toohelp Hola segura WCF comunicación (`WcfCommunicationListener`) creados por usted. toodo, modificar hello `CreateServiceReplicaListeners` método.

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
2. En el cliente de hello, Hola `WcfCommunicationClient` clase creada en hello anterior [ejemplo](service-fabric-reliable-services-communication-wcf.md) permanece sin cambios. Pero debe hello toooverride `CreateClientAsync` método `WcfCommunicationClientFactory`:

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

    Use `SecureWcfCommunicationClientFactory` toocreate un cliente de comunicación de WCF (`WcfCommunicationClient`). Usar métodos de servicio de hello cliente tooinvoke.

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

## <a name="next-steps"></a>Pasos siguientes
* [Web API con OWIN en Reliable Services](service-fabric-reliable-services-communication-webapi.md)
