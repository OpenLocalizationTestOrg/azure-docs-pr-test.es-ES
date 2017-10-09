---
title: "tutorial de retransmisión de WCF de Service Bus aaaAzure | Documentos de Microsoft"
description: "Cree un servicio y una aplicación cliente de Service Bus con Relay WCF."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 53dfd236-97f1-4778-b376-be91aa14b842
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: sethm
ms.openlocfilehash: 78cd52ef51e9fcfcda2f13ec54bde3af50d76476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-tutorial"></a>Tutorial de Azure WCF Relay

Este tutorial describe cómo toobuild WCF simple de retransmisión aplicación de cliente y el servicio utiliza la retransmisión de Azure. Para ver un tutorial parecido donde se usa [mensajería de Service Bus](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), consulte [Introducción a las colas de Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).

Trabajar a través de este tutorial le ofrece una descripción de pasos de hello toocreate requiere una aplicación de cliente y el servicio de retransmisión de WCF. Como sus homólogos WCF originales, un servicio es una construcción que expone uno o varios puntos de conexión, cada uno de los cuales expone una o varias operaciones de servicio. extremo de Hola de un servicio especifica una dirección donde se puede encontrar el servicio de hello, un enlace que contiene información de Hola que un cliente debe comunicar con el servicio de Hola y un contrato que define la funcionalidad de hello proporcionada por los clientes de hello servicio tooits. Hola principal diferencia entre WCF y de retransmisión de WCF es que ese extremo Hola se expone en la nube de hello en lugar de localmente en el equipo.

Después de trabajar a través de la secuencia de Hola de temas en este tutorial, tendrá un servicio en ejecución y un cliente que se puede invocar operaciones de hello del servicio de Hola. Hola primer tema describe cómo tooset una cuenta. se describen los pasos de Hello cómo toodefine un servicio que usa un contrato, cómo tooimplement Hola servicio y cómo tooconfigure Hola servicio en código. También se describe cómo servicio hello toohost y ejecución. Hello servicio que se crea se hospeda a sí mismo y cliente de Hola y el servicio se ejecutan en hello mismo equipo. Puede configurar el servicio de hello mediante código o un archivo de configuración.

pasos de tres final Hola describen cómo configurar la aplicación de cliente de hello, toocreate una aplicación cliente y crear y utilizar a un cliente que puede tener acceso a la funcionalidad de Hola de host de Hola.

## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial, necesitará Hola siguientes:

* [Microsoft Visual Studio 2015 o una versión superior](http://visualstudio.com). En este tutorial se usa Visual Studio 2017.
* Una cuenta de Azure activa. En caso de no tener ninguna, puede crear una cuenta gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/free/).

## <a name="create-a-service-namespace"></a>Creación de un espacio de nombres de servicio

Hola primer paso es un espacio de nombres toocreate y tooobtain una [firma de acceso compartido (SAS)](../service-bus-messaging/service-bus-sas.md) clave. Un espacio de nombres proporciona un límite de aplicación para cada aplicación que se exponen a través del servicio de retransmisión de Hola. Una clave SAS se genera automáticamente por el sistema de hello cuando se crea un espacio de nombres de servicio. combinación de Hola de espacio de nombres de servicio y la clave SAS proporciona credenciales de Hola para aplicación de Azure tooauthenticate access tooan. Siga hello [instrucciones a continuación](relay-create-namespace-portal.md) toocreate un espacio de nombres de retransmisión.

## <a name="define-a-wcf-service-contract"></a>Definición de un contrato de servicio de WCF

contrato de servicio de Hello especifica qué operaciones (Hola terminología del servicio web de funciones o métodos) Hola servicio admite. Los contratos se crean mediante la definición de una interfaz de C++, C# o Visual Basic. Cada método de interfaz de hello corresponde tooa operación del servicio concreta. Cada interfaz debe tener hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) atributo aplicado tooit y cada operación debe tener hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) tooit de atributo que se aplica. Si un método en una interfaz que tiene hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) atributo no tiene hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) atributo, que no se expone el método. código de Hello para estas tareas se proporciona en el ejemplo de Hola Hola procedimiento. Para obtener una descripción completa de contratos y servicios, vea [diseñar e implementar servicios](https://msdn.microsoft.com/library/ms729746.aspx) Hola documentación de WCF.

### <a name="create-a-relay-contract-with-an-interface"></a>Creación de un contrato de retransmisión con una interfaz

1. Abra Visual Studio como administrador haciendo clic en el programa Hola Hola **iniciar** menú y seleccionando **ejecutar como administrador**.
2. Cree un nuevo proyecto de aplicación de consola. Haga clic en hello **archivo** menú y seleccione **New**, a continuación, haga clic en **proyecto**. Hola **nuevo proyecto** cuadro de diálogo, haga clic en **Visual C#** (si **Visual C#** no aparece, mire debajo **otros lenguajes**). Haga clic en hello **aplicación de consola (.NET Framework)** plantilla y asígnele el nombre **EchoService**. Haga clic en **Aceptar** proyecto de hello toocreate.

    ![][2]

3. Instalar paquete NuGet de Bus de servicio de Hola. Este paquete agrega automáticamente referencias toohello Service Bus bibliotecas, así como Hola WCF **System.ServiceModel**. [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) es el espacio de nombres de Hola que habilita características básicas Hola de tooprogrammatically acceso de WCF. Bus de servicio usa muchos de los objetos de Hola y atributos de contratos de servicio WCF toodefine.

    En el Explorador de soluciones, haga clic en proyecto de hello y, a continuación, haga clic en **administrar paquetes de NuGet...** . Haga clic en hello **examinar** y, después, busque `Microsoft Azure Service Bus`. Ese nombre de proyecto Hola está seleccionado en hello **versiones** cuadro. Haga clic en **instalar**y acepte los términos de Hola de uso.

    ![][3]
4. En el Explorador de soluciones, haga doble clic en tooopen de archivo Program.cs hello en el editor de hello, si aún no está abrir.
5. Agregue Hola siguientes instrucciones using al principio de hello del archivo de Hola:

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. Cambiar el nombre del espacio de nombres de Hola de su nombre predeterminado de **EchoService** demasiado**Microsoft.ServiceBus.Samples**.

   > [!IMPORTANT]
   > Este tutorial utiliza el espacio de nombres de hello C# **Microsoft.ServiceBus.Samples**, que es el espacio de nombres de Hola de hello basadas en contratos de tipo que se utiliza en el archivo de configuración de Hola Hola administrado [cliente de WCF configurar hello](#configure-the-wcf-client) paso. Puede especificar cualquier espacio de nombres que desee al compilar este ejemplo; Sin embargo, el tutorial de hello no funcionará a menos que, a continuación, modifique Hola espacios de nombres de servicio y contrato de hello en consecuencia, en el archivo de configuración de aplicación Hola. espacio de nombres de Hello especificado en hello App.config debe ser archivo mismo Hola como espacio de nombres de hello especificado en los archivos de C#.
   >
   >
7. Directamente después de hello `Microsoft.ServiceBus.Samples` declaración de espacio de nombres, pero dentro del espacio de nombres de hello, defina una nueva interfaz denominada `IEchoContract` y aplicar hello `ServiceContractAttribute` interfaz toohello de atributo con un valor de espacio de nombres de `http://samples.microsoft.com/ServiceModel/Relay/`. valor de espacio de nombres de Hello difiere del espacio de nombres de Hola que utilizas en ámbito de hello del código. En su lugar, valor de espacio de nombres de Hola se utiliza como un identificador único para este contrato. Especificar explícitamente el espacio de nombres de hello, impide que valor de espacio de nombres predeterminado de Hola se agreguen toohello el nombre del contrato. Pegue Hola siguiente código después de la declaración de espacio de nombres de hello:

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > Normalmente, el espacio de nombres del contrato de servicio de hello contiene un esquema de nomenclatura que incluya la información de versión. Incluida la información de versión en el espacio de nombres del contrato de servicio de hello permite cambios importantes de servicios tooisolate definiendo un nuevo contrato de servicio con un nuevo espacio de nombres y exponerlo en un nuevo extremo. De esta manera, los clientes pueden seguir contrato de servicio anterior toouse Hola sin necesidad de toobe actualizado. La información de versión puede constar de una fecha o un número de compilación. Para obtener más información, vea [Control de versiones del servicio](http://go.microsoft.com/fwlink/?LinkID=180498). Para fines de Hola de este tutorial, Hola esquema del espacio de nombres del contrato de servicio de Hola de nombre no contiene información de versión.
   >
   >
8. Dentro de hello `IEchoContract` de la interfaz, declare un método para Hola Hola de operación único `IEchoContract` contrato expone Hola interfaz y aplique hello `OperationContractAttribute` método toohello de atributo que desea tooexpose como parte de Hola pública retransmisión de WCF contrato, como se indica a continuación:

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. Directamente después de hello `IEchoContract` definición de la interfaz, declare un canal que herede tanto `IEchoContract` y también toohello `IClientChannel` interfaz, como se muestra aquí:

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    Un canal es objeto WCF de Hola a través del cual cliente y el host de hello pasan información tooeach otras. Más tarde, escribirá el código de información de tooecho Hola canal entre dos aplicaciones de Hola.
10. De hello **generar** menú, haga clic en **generar solución** o presione **Ctrl + Mayús + B** precisión de hello tooconfirm de su trabajo hasta ahora.

### <a name="example"></a>Ejemplo

Hola siguiente código muestra una interfaz básica que define un contrato de retransmisión de WCF.

```csharp
using System;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

Hello interfaz está creada, puede implementar interfaz Hola.

## <a name="implement-hello-wcf-contract"></a>Contrato de WCF implemente Hola

Crear una retransmisión de Azure requiere que cree primero el contrato de hello, que se define mediante una interfaz. Para obtener más información acerca de cómo crear la interfaz de hello, vea el paso anterior de Hola. Hola siguiente paso es interfaz de hello tooimplement. Esto implica la creación de una clase denominada `EchoService` que implementa Hola definido por el usuario `IEchoContract` interfaz. Después de implementar la interfaz de hello, a continuación, configurar interfaz hello mediante un archivo de configuración App.config. archivo de configuración de Hello contiene información necesaria para la aplicación hello, como nombre de hello del servicio de hello, nombre de hello del contrato de Hola y tipo de Hola de protocolo que está toocommunicate usado con el servicio de retransmisión de Hola. código de Hello utilizado para estas tareas se proporciona en el ejemplo de Hola Hola procedimiento. Para obtener información más general acerca de cómo tooimplement un servicio de contrato, consulte [implementar contratos de servicio](https://msdn.microsoft.com/library/ms733764.aspx) Hola documentación de WCF.

1. Crear una nueva clase denominada `EchoService` directamente después de la definición de Hola de hello `IEchoContract` interfaz. Hola `EchoService` clase implementa hello `IEchoContract` interfaz.

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    Implementaciones de interfaz tooother similar, puede implementar definición hello en un archivo diferente. Sin embargo, para este tutorial, la implementación de hello está ubicada en hello mismo archivo como definición de interfaz de Hola y Hola `Main` método.
2. Aplicar hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) atributo toohello `IEchoContract` interfaz. atributo de Hello especifica el espacio de nombres y nombre del servicio Hola. Una vez hecho esto, Hola `EchoService` clase aparece como sigue:

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. Hola implemente `Echo` método definido en hello `IEchoContract` interfaz Hola `EchoService` clase.

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. Haga clic en **generar**, a continuación, haga clic en **generar solución** precisión de hello tooconfirm de su trabajo.

### <a name="define-hello-configuration-for-hello-service-host"></a>Definir configuración de hello para el host del servicio de Hola

1. archivo de configuración de Hello es el archivo de configuración de WCF tooa muy similar. Se incluye el nombre del servicio Hola, endpoint (es decir, ubicación de Hola que Azure retransmisión expone para que los clientes y hosts toocommunicate entre sí) y Hola enlace (Hola el tipo de protocolo que se usa toocommunicate). Hello diferencia principal es que este punto de conexión de servicio configurado hace referencia tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) enlace, que no forma parte del programa Hola a .NET Framework. [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) es uno de los enlaces de hello definidos por el servicio de Hola.
2. En **el Explorador de soluciones**, haga doble clic en el archivo tooopen de hello App.config en el editor de Visual Studio Hola.
3. Hola `<appSettings>` elemento, reemplace los marcadores de posición de Hola por nombre de Hola de su espacio de nombres de servicio y Hola clave SAS que copió en el paso anterior.
4. Dentro de hello `<system.serviceModel>` etiquetas, agregue un `<services>` elemento. Puede definir varias aplicaciones de retransmisión en un único archivo de configuración. Sin embargo, este tutorial solo define una.

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. Dentro de hello `<services>` elemento, agregue un `<service>` nombre del servicio Hola Hola de toodefine de elemento.

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. Dentro de hello `<service>` elemento, definir Hola ubicación del contrato de extremo de Hola y Hola también tipo de enlace de punto de conexión de Hola.

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    punto de conexión de Hola define dónde debe buscar cliente hello para la aplicación de host de Hola. Más adelante, el tutorial de hello usa este toocreate paso un URI que exponga completamente el host de Hola a través de retransmisión de Azure. enlace de Hello declara que estamos usando TCP como Hola toocommunicate de protocolo con el servicio de retransmisión de Hola.
7. De hello **generar** menú, haga clic en **generar solución** precisión de hello tooconfirm de su trabajo.

### <a name="example"></a>Ejemplo

Hello código siguiente muestra implementación Hola Hola del contrato de servicio.

```csharp
[ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]

    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }
```

Hello código siguiente muestra hello formato básico del archivo App.config de hello asociado al host de servicio de Hola.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceBus.Samples.EchoService">
        <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding" />
      </service>
    </services>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="host-and-run-a-basic-web-service-tooregister-with-hello-relay-service"></a>Hospedar y ejecutar un tooregister de servicio web básico con el servicio de retransmisión de Hola

Este paso describe cómo toorun un Azure retransmisión servicio.

### <a name="create-hello-relay-credentials"></a>Crear credenciales de retransmisión de Hola

1. En `Main()`, cree dos variables en qué espacio de nombres de toostore Hola y Hola clave SAS que se leen desde la ventana de la consola de Hola.

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    clave SAS de Hello será usado tooaccess más adelante el proyecto. espacio de nombres de Hola se pasa como un parámetro demasiado`CreateServiceUri` toocreate un URI de servicio.
2. Con un [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) objeto, declare que va a usar una clave SAS como tipo de credencial de Hola. Agregar Hola después el código directamente después de código de hello agregado en el último paso de Hola.

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-hello-service"></a>Crear una dirección base para el servicio de Hola

Después de código de hello agregado en el último paso de hello, cree un `Uri` instancia para la dirección base Hola del servicio de Hola. Este URI especifica el esquema de Bus de servicio de hello, espacio de nombres de Hola y ruta de acceso de Hola de interfaz de servicio de Hola.

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

"sb" es una abreviatura para el esquema de Bus de servicio de Hola e indica que estamos usando TCP como protocolo de Hola. Esto se ha indicado anteriormente en el archivo de configuración de hello, cuando [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) se especificó como enlace Hola.

Para este tutorial, hello URI es `sb://putServiceNamespaceHere.windows.net/EchoService`.

### <a name="create-and-configure-hello-service-host"></a>Crear y configurar el host del servicio de Hola

1. Establecer el modo de conectividad de hello demasiado`AutoDetect`.

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    modo de conectividad de Hello describe Hola protocolo Hola servicio usa toocommunicate con servicio de retransmisión de hello; HTTP o TCP. Con configuración predeterminada de hello `AutoDetect`, servicio de hello intenta tooconnect tooAzure retransmisión a través de HTTP y TCP, si está disponible si TCP no está disponible. Tenga en cuenta que esto difiere del servicio de Hola Hola protocolo se especifica para la comunicación de cliente. Dicho protocolo viene determinado por enlace Hola utilizado. Por ejemplo, un servicio puede utilizar hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) enlace, que especifica que el extremo se comunica con los clientes a través de HTTP. Que el mismo servicio podría especificar **ConnectivityMode.AutoDetect** para que el servicio de Hola se comunica con la retransmisión de Azure a través de TCP.
2. Crear el host de servicio de hello, con hello que URI creado anteriormente en esta sección.

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    host de servicio de Hello es objeto WCF de Hola que crea una instancia de servicio de Hola. En este caso, se le pase tipo hello del servicio que desea toocreate (un `EchoService` tipo) y también la dirección del toohello a la que desea que el servicio de Hola de tooexpose.
3. En hello parte superior del archivo de hello Program.cs, agregue referencias demasiado[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) y [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. En `Main()`, configurar el acceso público de hello extremo tooenable.

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    Este paso informa a servicio de retransmisión de Hola que la aplicación se puede encontrar públicamente examinando la fuente ATOM de hello para el proyecto. Si establece **DiscoveryType** demasiado**privada**, un cliente todavía sería capaz de tooaccess servicio de Hola. Sin embargo, el servicio de hello no aparecería cuando busca el espacio de nombres de hello retransmisión. En su lugar, Hola cliente tendría ruta de acceso de punto de conexión de tooknow Hola con antelación.
5. Aplicar credenciales del servicio de hello toohello puntos de conexión de servicio definidos en el archivo App.config de hello:

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    Como se indicó en el paso anterior de hello, podría haberse declarado varios servicios y los puntos de conexión en el archivo de configuración de Hola. Si tuviera, este código recorrería el archivo de configuración de Hola y búsqueda para cada punto de conexión toowhich debería aplicar sus credenciales. Sin embargo, para este tutorial, el archivo de configuración de hello tiene solo un punto de conexión.

### <a name="open-hello-service-host"></a>Host de servicio de hello abierto

1. Abra el servicio de Hola.

    ```csharp
    host.Open();
    ```
2. Informar al usuario de Hola que Hola servicio está en ejecución y explique cómo tooshut servicio Hola.

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. Cuando termine, cierre el host de servicio de Hola.

    ```csharp
    host.Close();
    ```
4. Presione **Ctrl + Mayús + B** proyecto de hello toobuild.

### <a name="example"></a>Ejemplo

El código de servicio completado debería tener el siguiente formato. código de Hello incluye contrato de servicio de Hola y la implementación de los pasos anteriores en el tutorial de Hola y Hola de hosts de servicio en una aplicación de consola.

```csharp
using System;
using System.ServiceModel;
using System.ServiceModel.Description;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Description;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { };

    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {

            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;         

            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS key: ");
            string sasKey = Console.ReadLine();

           // Create hello credentials object for hello endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create hello service URI based on hello service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create hello service host reading hello configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create hello ServiceRegistrySettings behavior for hello endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add hello Relay credentials tooall endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open hello service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            // Close hello service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-hello-service-contract"></a>Crear a un cliente WCF de contrato de servicio de Hola

paso siguiente Hello es toocreate una aplicación cliente y definir Hola contrato de servicio se implementarán en pasos posteriores. Tenga en cuenta que muchos de estos pasos son similares a los pasos de hello usa toocreate un servicio: definir un contrato, editar un archivo App.config de archivos, con el servicio de retransmisión de credenciales tooconnect toohello y así sucesivamente. código de Hello utilizado para estas tareas se proporciona en el ejemplo de Hola Hola procedimiento.

1. Crear un nuevo proyecto de la solución de Visual Studio actual de hello para el cliente de hello haciendo Hola siguiente:

   1. En el Explorador de soluciones, en Hola la misma solución que contiene el servicio de hello, haga clic en la solución actual de hello (no en proyecto de hello) y haga clic en **agregar**. Después, haga clic en **Nuevo proyecto**.
   2. Hola **Agregar nuevo proyecto** cuadro de diálogo, haga clic en **Visual C#** (si **Visual C#** no aparece, mire debajo **otros lenguajes**), seleccione Hola **Aplicación de consola (.NET Framework)** plantilla y asígnele el nombre **EchoClient**.
   3. Haga clic en **Aceptar**.
      <br />
2. En el Explorador de soluciones, haga doble clic en el archivo Program.cs Hola Hola **EchoClient** proyecto tooopen abrir en el editor de hello, si aún no lo está.
3. Cambiar el nombre del espacio de nombres de Hola de su nombre predeterminado de `EchoClient` demasiado`Microsoft.ServiceBus.Samples`.
4. Instalar hello [paquete NuGet de Bus de servicio](https://www.nuget.org/packages/WindowsAzure.ServiceBus): en el Explorador de soluciones, haga clic en hello **EchoClient** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet**. Haga clic en hello **examinar** y, después, busque `Microsoft Azure Service Bus`. Haga clic en **instalar**y acepte los términos de Hola de uso.

    ![][3]
5. Agregar un `using` instrucción para hello [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) espacio de nombres en el archivo Program.cs de Hola.

    ```csharp
    using System.ServiceModel;
    ```
6. Agregar espacio de nombres de hello servicio contrato definición toohello, como se muestra en el siguiente ejemplo de Hola. Tenga en cuenta que esta definición es definición toohello idénticos que se usa en hello **servicio** proyecto. Debe agregar este código en parte superior de Hola de hello `Microsoft.ServiceBus.Samples` espacio de nombres.

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. Presione **Ctrl + Mayús + B** cliente de hello toobuild.

### <a name="example"></a>Ejemplo

Hello código siguiente muestra hello estado actual del archivo Program.cs de Hola Hola **EchoClient** proyecto.

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }


    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="configure-hello-wcf-client"></a>Configurar el cliente WCF de Hola

En este paso, creará un archivo App.config para una aplicación cliente básica que tiene acceso a servicios de hello creado anteriormente en este tutorial. Este archivo App.config define el contrato de hello, enlace y el nombre de punto de conexión de Hola. código de Hello utilizado para estas tareas se proporciona en el ejemplo de Hola Hola procedimiento.

1. En el Explorador de soluciones, en hello **EchoClient** proyecto de equipo y haga doble clic en **App.config** tooopen archivo de hello en el editor de Visual Studio Hola.
2. Hola `<appSettings>` elemento, reemplace los marcadores de posición de Hola por nombre de Hola de su espacio de nombres de servicio y Hola clave SAS que copió en el paso anterior.
3. De elemento de system.serviceModel hello, agregue un `<client>` elemento.

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    En este paso se declara que está definiendo una aplicación cliente de estilo WCF.
4. Dentro de hello `client` elemento, Definir nombre hello, contrato y tipo de enlace de punto de conexión de Hola.

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    Este paso define nombre Hola de punto de conexión de hello, contrato de hello definido en el servicio de Hola y hechos de Hola que aplicación de cliente de hello usa TCP toocommunicate con retransmisión de Azure. Hello nombre de punto de conexión se usa en hello siguiente paso toolink esta configuración de punto de conexión con el URI del servicio de Hola.
5. Haga clic en **Archivo** y luego en **Guardar todo**.

## <a name="example"></a>Ejemplo

Hello código siguiente muestra archivo App.config de hello para el cliente de eco hello.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <client>
      <endpoint name="RelayEndpoint"
                      contract="Microsoft.ServiceBus.Samples.IEchoContract"
                      binding="netTcpRelayBinding"/>
    </client>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="implement-hello-wcf-client"></a>Cliente de WCF implemente Hola
En este paso, se implementa una aplicación cliente básica que tiene acceso a servicios de Hola que creó anteriormente en este tutorial. Servicio toohello similar, el cliente de hello realiza muchas de hello mismo operaciones tooaccess retransmisión de Azure:

1. Establece el modo de conectividad de Hola.
2. Crea el URI que localiza el servicio de host de Hola Hola.
3. Define las credenciales de seguridad de Hola.
4. Se aplica Hola credenciales toohello conexión.
5. Abre la conexión de Hola.
6. Realiza tareas de específicos de la aplicación hello.
7. Cierra la conexión de Hola.

Sin embargo, una de las principales diferencias de hello es que la aplicación de cliente de hello usa un servicio de retransmisión de canal tooconnect toohello, mientras que el servicio de hello utiliza una llamada demasiado**ServiceHost**. código de Hello utilizado para estas tareas se proporciona en el ejemplo de Hola Hola procedimiento.

### <a name="implement-a-client-application"></a>Implementación de una aplicación cliente
1. Establecer el modo de conectividad de hello demasiado**detección automática**. Agregar Hola siguiente código dentro de hello `Main()` método de hello **EchoClient** aplicación.

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. Definir variables toohold Hola valores para el espacio de nombres de servicio de Hola y la clave SAS que se leen desde la consola de Hola.

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. Crear Hola URI que define la ubicación de hello del host de hello en el proyecto de retransmisión.

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. Crear objeto de credencial de hello para el punto de conexión del espacio de nombres de servicio.

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. Crear el generador de canales de Hola que carga la configuración de Hola que se describe en el archivo App.config de hello.

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    Un generador de canales es un objeto WCF que crea un canal a través del cual se comunican las aplicaciones de cliente y servicio de Hola.
6. Aplicar las credenciales de Hola.

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. Crear y abrir el servicio de toohello de canal de Hola.

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. Escribir la interfaz de usuario básica de Hola y funcionalidad de eco hello.

    ```csharp
    Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
    string input = Console.ReadLine();
    while (input != String.Empty)
    {
        try
        {
            Console.WriteLine("Server echoed: {0}", channel.Echo(input));
        }
        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.Message);
        }
        input = Console.ReadLine();
    }
    ```

    Tenga en cuenta que código de hello usa instancia Hola del objeto de canal de Hola como un proxy para el servicio de Hola.
9. Cierre canal hello y generador de hello cerrar.

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a>Ejemplo

El código completado debe aparecer como sigue, que muestra cómo toocreate una aplicación cliente, cómo toocall Hola operaciones del servicio de Hola y cómo tooclose Hola a cliente después de la operación de hello llamar a finaliza.

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;


            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS Key: ");
            string sasKey = Console.ReadLine();



            Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));

            channelFactory.Endpoint.Behaviors.Add(sasCredential);

            IEchoChannel channel = channelFactory.CreateChannel();
            channel.Open();

            Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
            string input = Console.ReadLine();
            while (input != String.Empty)
            {
                try
                {
                    Console.WriteLine("Server echoed: {0}", channel.Echo(input));
                }
                catch (Exception e)
                {
                    Console.WriteLine("Error: " + e.Message);
                }
                input = Console.ReadLine();
            }

            channel.Close();
            channelFactory.Close();

        }
    }
}
```

## <a name="run-hello-applications"></a>Ejecutar aplicaciones de Hola

1. Presione **Ctrl + Mayús + B** solución de hello toobuild. Esto compila el proyecto de cliente de Hola y el proyecto de servicio de Hola que creó en los pasos anteriores de Hola.
2. Antes de la aplicación cliente en ejecución hello, debe asegurarse de que está ejecutando la aplicación de servicio de Hola. En el Explorador de soluciones en Visual Studio, haga clic en hello **EchoService** solución, a continuación, haga clic en **propiedades**.
3. En el cuadro de diálogo de propiedades de solución de hello, haga clic en **proyecto de inicio**, a continuación, haga clic en hello **proyectos de inicio múltiples** botón. Asegúrese de que **EchoService** aparece en primer lugar en la lista de Hola.
4. Conjunto hello **acción** cuadro para ambos hello **EchoService** y **EchoClient** proyectos demasiado**iniciar**.

    ![][5]
5. Haga clic en **Dependencias del proyecto**. Hola **proyectos** cuadro, seleccione **EchoClient**. Hola **depende de** cuadro, asegúrese de que **EchoService** está activada.

    ![][6]
6. Haga clic en **Aceptar** toodismiss hello **propiedades** cuadro de diálogo.
7. Presione **F5** toorun ambos proyectos.
8. Ambas ventanas de consola abrirse y solicitarle para nombre de espacio de nombres de Hola. Hello servicio debe ejecutarse en primer lugar, por lo que en hello **EchoService** ventana de consola, escriba el espacio de nombres de hello y, a continuación, presione **ENTRAR**.
9. A continuación, se le solicitará su clave de SAS. Escriba la clave SAS de hello y presione ENTRAR.

    Este es el resultado de ejemplo de ventana de consola Hola. Tenga en cuenta que los valores de hello figuran aquí se proporcionan por ejemplo solo con fines.

    `Your Service Namespace: myNamespace``Your SAS Key: <SAS key value>`

    aplicación de servicio de Hello imprime la dirección de Hola la ventana toohello consola en el que está escuchando, tal como se muestra en el siguiente ejemplo de Hola.

    `Service address: sb://mynamespace.servicebus.windows.net/EchoService/``Press [Enter] tooexit`
10. Hola **EchoClient** ventana de consola, escriba Hola la misma información que especificó anteriormente para la aplicación de servicio de Hola. Siga Hola de hello anteriores pasos tooenter mismo espacio de nombres de servicio y la SAS de valores para la aplicación de cliente de hello de clave.
11. Después de escribir estos valores, cliente hello abre un servicio de toohello de canal y le pide tooenter algún texto tal como se muestra en el siguiente ejemplo de salida de consola de Hola.

    `Enter text tooecho (or [Enter] tooexit):`

    Escriba alguna aplicación de servicio de texto toosend toohello y presione ENTRAR. Este texto se envía el servicio de toohello a través de la operación de servicio eco hello y aparece en la ventana de consola de servicio de hello como en la siguiente salida de ejemplo de Hola.

    `Echoing: My sample text`

    aplicación de cliente de Hello recibe el valor devuelto de Hola de hello `Echo` operación, que es el texto original de Hola y lo imprime tooits ventana de consola. Hola aquí te mostramos la salida de ejemplo de ventana de consola de cliente de Hola.

    `Server echoed: My sample text`
12. Puede continuar enviando mensajes de texto hello toohello servicio del cliente de esta manera. Cuando haya terminado, presione ENTRAR en tooend de windows de consola de cliente y servicio Hola ambas aplicaciones.

## <a name="next-steps"></a>Pasos siguientes

Este tutorial se ha explicado cómo toobuild una aplicación de cliente de retransmisión de Azure y el servicio utilizando Hola capacidades de retransmisión de WCF de Bus de servicio. Para ver un tutorial parecido donde se usa [mensajería de Service Bus](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), consulte [Introducción a las colas de Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).

toolearn más información acerca de la retransmisión de Azure, vea Hola temas siguientes.

* [Información general sobre la arquitectura de Azure Service Bus](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [Introducción a Azure Relay](relay-what-is-it.md)
* [Cómo el servicio con .NET de la retransmisión de hello toouse WCF](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
