---
title: "tutorial de REST de Bus de aaaService mediante retransmisión de Azure | Documentos de Microsoft"
description: "Cree una sencilla aplicación host de Azure Service Bus Relay que expone una interfaz basada en REST."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1312b2db-94c4-4a48-b815-c5deb5b77a6a
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2017
ms.author: sethm
ms.openlocfilehash: b68650993a0390e7cef891ccb4236095cd86d4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a>Tutorial de REST de Azure WCF Relay

Este tutorial describe cómo toobuild una retransmisión de Azure simple hospedar la aplicación que expone una interfaz basada en REST. REST permite que un cliente web, como un explorador web, hello tooaccess solicitudes de API de Bus de servicio a través de HTTP.

tutorial de Hello usa tooconstruct modelo programación Hola REST de Windows Communication Foundation (WCF) un servicio REST en el Bus de servicio. Para obtener más información, consulte [el modelo de programación de REST de WCF](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) y [diseñar e implementar servicios](/dotnet/framework/wcf/designing-and-implementing-services) Hola documentación de WCF.

## <a name="step-1-create-a-namespace"></a>Paso 1: Crear un espacio de nombres

usar toobegin Hola características de retransmisión en Azure, primero debe crear un espacio de nombres de servicio. Un espacio de nombres proporciona un contenedor con un ámbito para el desvío de recursos de Azure en la aplicación. Siga hello [instrucciones a continuación](relay-create-namespace-portal.md) toocreate un espacio de nombres de retransmisión.

## <a name="step-2-define-a-rest-based-wcf-service-contract-toouse-with-azure-relay"></a>Paso 2: Definir una toouse de contrato de servicio WCF basado en REST con retransmisión de Azure

Cuando se crea un servicio basado en REST WCF, debe definir el contrato de Hola. contrato de Hello especifica qué operaciones Hola admite el host. Una operación de servicio puede considerarse como un método de servicio web. Los contratos se crean mediante la definición de una interfaz de C++, C# o Visual Basic. Cada método de interfaz de hello corresponde tooa operación del servicio concreta. Hola [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) atributo debe ser interfaz tooeach aplicados y Hola [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) atributo debe ser una operación tooeach aplicada. Si un método en una interfaz que tiene hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) no tiene hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), que no se expone el método. código de Hello utilizado para estas tareas se muestra en el ejemplo de Hola Hola procedimiento.

Hello diferencia principal entre un contrato de WCF y un contrato basado en REST es adición de Hola de una propiedad toohello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx). Esta propiedad permite toomap un método en el método de interfaz tooa en hello otro lado de la interfaz de Hola. En este caso, usaremos [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink un tooHTTP método GET. Esto permite que el Bus de servicio tooaccurately recuperar e interpretar comandos enviados toohello interfaz.

### <a name="toocreate-a-contract-with-an-interface"></a>toocreate un contrato con una interfaz

1. Abra Visual Studio como administrador: programa Hola de menú contextual en hello **iniciar** menú y, a continuación, haga clic en **ejecutar como administrador**.
2. Cree un nuevo proyecto de aplicación de consola. Haga clic en hello **archivo** menú y seleccione **New**, a continuación, seleccione **proyecto**. Hola **nuevo proyecto** cuadro de diálogo, haga clic en **Visual C#**, seleccione hello **aplicación de consola** plantilla y asígnele el nombre **ImageListener**. Usar valor predeterminado de hello **ubicación**. Haga clic en **Aceptar** proyecto de hello toocreate.
3. Para un proyecto de C#, Visual Studio crea un archivo `Program.cs`. Esta clase contiene vacío `Main()` método, necesario para un toobuild de proyecto de aplicación de consola correctamente.
4. Agregar referencias tooService Bus y **System.ServiceModel.dll** toohello proyecto mediante la instalación de paquetes de NuGet de Bus de servicio de Hola. Este paquete agrega automáticamente referencias toohello Service Bus bibliotecas, así como Hola WCF **System.ServiceModel**. En el Explorador de soluciones, haga clic en hello **ImageListener** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet**. Haga clic en hello **examinar** y, después, busque `Microsoft Azure Service Bus`. Haga clic en **instalar**y acepte los términos de Hola de uso.
5. Debe agregar explícitamente una referencia**System.ServiceModel.Web.dll** toohello proyecto:
   
    a. En el Explorador de soluciones, haga clic en hello **referencias** carpeta bajo la carpeta del proyecto de hello y, a continuación, haga clic en **Agregar referencia**.
   
    b. Hola **Agregar referencia** diálogo cuadro, haga clic en hello **Framework** pestaña en el lado izquierdo de Hola y Hola **búsqueda** , escriba **System.ServiceModel.Web** . Seleccione hello **System.ServiceModel.Web** casilla de verificación, a continuación, haga clic en **Aceptar**.
6. Agregue los siguiente hello `using` las instrucciones en la parte superior de hello del archivo Program.cs de Hola.
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) es el espacio de nombres de Hola que habilita el acceso mediante programación toobasic características de WCF. Retransmisión de WCF usa muchos de los objetos de Hola y atributos de contratos de servicio WCF toodefine. Usará este espacio de nombres en la mayoría de las aplicaciones de Relay. De forma similar, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) ayuda a define canal hello, que es objeto de Hola a través del cual se comunica con el explorador web del cliente hello y retransmisión de Azure. Por último, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contiene tipos de Hola que le permiten aplicaciones basadas en web de toocreate.
7. Cambiar el nombre de hello `ImageListener` espacio de nombres demasiado**Microsoft.ServiceBus.Samples**.
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. Directamente después de hello Abrir llave de apertura de la declaración de espacio de nombres de hello, defina una nueva interfaz denominada **IImageContract** y aplicar hello **ServiceContractAttribute** interfaz toohello de atributo con un valor de `http://samples.microsoft.com/ServiceModel/Relay/`. valor de espacio de nombres de Hello difiere del espacio de nombres de Hola que utilizas en ámbito de hello del código. valor de espacio de nombres de Hola se utiliza como un identificador único para este contrato y debe tener información de versión. Para obtener más información, vea [Control de versiones del servicio](http://go.microsoft.com/fwlink/?LinkID=180498). Especificar explícitamente el espacio de nombres de hello, impide que valor de espacio de nombres predeterminado de Hola se agreguen toohello el nombre del contrato.
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. Dentro de hello `IImageContract` de la interfaz, declare un método para Hola Hola de operación único `IImageContract` contrato expone Hola interfaz y aplique hello `OperationContractAttribute` atributo método toohello que desea tooexpose como parte de hello público Service Bus contrato.
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. Hola **OperationContract** atributo, agregue hello **WebGet** valor.
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    Si lo hace, habilita Hola tooroute de servicio de retransmisión HTTP GET solicita demasiado`GetImage`, hello tootranslate devolver valores de y `GetImage` en una respuesta GETRESPONSE de HTTP. Más adelante en el tutorial de hello, utilizará un tooaccess de explorador web este método y la imagen de toodisplay hello en el Explorador de Hola.
11. Directamente después de hello `IImageContract` definición, declare un canal que herede de ambos hello `IImageContract` y `IClientChannel` interfaces.
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    Un canal es objeto WCF de Hola a través del cual cliente y servicio de hello pasan información tooeach otras. Más adelante, creará el canal de hello en la aplicación host. Retransmisión de Azure, a continuación, utiliza este canal toopass hello las solicitudes HTTP GET desde Hola explorador tooyour **GetImage** implementación. retransmisión de Hello también utiliza Hola Hola de tootake canal **GetImage** valor devuelto y lo traduce a un GETRESPONSE de HTTP para el explorador del cliente de Hola.
12. De hello **generar** menú, haga clic en **generar solución** precisión de hello tooconfirm de su trabajo hasta ahora.

### <a name="example"></a>Ejemplo
Hola siguiente código muestra una interfaz básica que define un contrato de retransmisión de WCF.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="step-3-implement-a-rest-based-wcf-service-contract-toouse-service-bus"></a>Paso 3: Implementar un contrato de servicio WCF basado en REST toouse Bus de servicio
Crear un servicio de retransmisión de WCF basado en REST requiere crear primero el contrato de hello, que se define mediante una interfaz. Hola siguiente paso es interfaz de hello tooimplement. Esto implica la creación de una clase denominada **ImageService** que implementa Hola definido por el usuario **IImageContract** interfaz. Después de implementar el contrato de hello, a continuación, configurar interfaz hello mediante un archivo App.config. archivo de configuración de Hello contiene información necesaria para la aplicación hello, como nombre de hello del servicio de hello, nombre de hello del contrato de Hola y tipo de Hola de protocolo que está toocommunicate usado con el servicio de retransmisión de Hola. código de Hello utilizado para estas tareas se proporciona en el ejemplo de Hola Hola procedimiento.

Como con los pasos anteriores de hello, hay muy pocas diferencias entre implementar un contrato basado en REST y un contrato de retransmisión de WCF.

### <a name="tooimplement-a-rest-style-service-bus-contract"></a>contrato de Bus de servicio de tooimplement un estilo de REST
1. Crear una nueva clase denominada **ImageService** directamente después de la definición de Hola de hello **IImageContract** interfaz. Hola **ImageService** clase implementa hello **IImageContract** interfaz.
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    Implementaciones de interfaz tooother similar, puede implementar definición hello en un archivo diferente. Sin embargo, para este tutorial, la implementación de hello aparece en hello mismo archivo como definición de interfaz de Hola y `Main()` método.
2. Aplicar hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) atributo toohello **IImageService** tooindicate de clase que Hola clase es una implementación de un contrato de WCF.
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    Como se mencionó anteriormente, este espacio de nombres no es un espacio de nombres tradicional. En su lugar, es parte de la arquitectura WCF que identifica el contrato de Hola Hola. Para obtener más información, vea hello [nombres de contrato de datos](https://msdn.microsoft.com/library/ms731045.aspx) tema Hola documentación de WCF.
3. Agregue un proyecto de tooyour de imagen JPG.  
   
    Se trata de una imagen que muestra los servicios de hello en Hola recibir explorador. Haga clic con el botón derecho en el proyecto y, después, haga clic en **Agregar**. A continuación, haga clic en **Elemento existente**. Hola de uso **Agregar elemento existente** tooan de toobrowse del cuadro de diálogo procede .jpg y, a continuación, haga clic en **agregar**.
   
    Al agregar el archivo hello, asegúrese de que **todos los archivos** está seleccionado en hello lista desplegable siguiente toohello **nombre de archivo:** campo. resto de Hola de este tutorial se da por supuesto que Hola nombre de imagen de hello es "image.jpg". Si tiene un archivo diferente, se dispone de toorename Hola imagen o cambiar su toocompensate de código.
4. seguro que Hola ejecutando el servicio puede encontrar el archivo de imagen de hello, en toomake **el Explorador de soluciones** haga clic en archivo de imagen de hello, a continuación, haga clic en **propiedades**. Hola **propiedades** panel, establezca **copiar tooOutput directorio** demasiado**copiar si es posterior**.
5. Agregar una referencia toohello **System.Drawing.dll** toohello ensamblado del proyecto y agregue siguiente Hola asociados `using` instrucciones.  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. Hola **ImageService** clase, agregue Hola después de constructor que carga Hola mapa de bits y prepara toosend se toohello explorador del cliente.
   
    ```csharp
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";
   
        Image bitmap;
   
        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }
    }
    ```
7. Directamente después de código anterior, hello, agregue Hola siguiente **GetImage** método Hola **ImageService** mensaje tooreturn HTTP de clase que contiene la imagen de Hola.
   
    ```csharp
    public Stream GetImage()
    {
        MemoryStream stream = new MemoryStream();
        this.bitmap.Save(stream, ImageFormat.Jpeg);
   
        stream.Position = 0;
        WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";
   
        return stream;
    }
    ```
   
    Esta implementación usa **MemoryStream** tooretrieve Hola imagen y prepararlo para la transmisión por secuencias toohello explorador. Inicia la posición de la secuencia de hello en la posición cero, declara el contenido de la transmisión de hello como jpeg y transmite la información de Hola.
8. De hello **generar** menú, haga clic en **generar solución**.

### <a name="toodefine-hello-configuration-for-running-hello-web-service-on-service-bus"></a>configuración de hello toodefine para ejecutar el servicio web de hello en el Bus de servicio
1. En **el Explorador de soluciones**, haga doble clic en **App.config** tooopen en el editor de Visual Studio Hola.
   
    Hola **App.config** archivo incluye el nombre del servicio hello, extremo (es decir, la ubicación de hello Azure retransmisión expone para que los clientes y hosts toocommunicate entre sí) y (Hola el tipo de protocolo que se usa toocommunicate) de enlace. Hello principal diferencia reside en ese punto de conexión de servicio de hello configurado hace referencia tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) enlace.
2. Hola `<system.serviceModel>` XML es un elemento WCF que define uno o varios servicios. En este caso, es punto de conexión y el nombre de servicio de hello toodefine usado. Final Hola de hello `<system.serviceModel>` elemento (pero aún dentro `<system.serviceModel>`), agregue un `<bindings>` elemento que tiene Hola siguen contenido. Esto define los enlaces de hello utilizados en la aplicación hello. Puede definir varios enlaces, pero para este tutorial está definiendo solo uno.
   
    ```xml
    <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
            <binding name="default">
                <security relayClientAuthenticationType="None" />
            </binding>
        </webHttpRelayBinding>
    </bindings>
    ```
   
    código de Hello anterior define una retransmisión de WCF [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) enlace con **relayClientAuthenticationType** establecido demasiado**ninguno**. Este valor indica que un extremo que usa este enlace no requiere una credencial de cliente.
3. Después de hello `<bindings>` elemento, agregue un `<services>` elemento. Enlaces toohello similares, puede definir varios servicios en un único archivo de configuración. Sin embargo, para este tutorial, solo se define uno.
   
    ```xml
    <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
            <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IImageContract"
                    binding="webHttpRelayBinding"
                    bindingConfiguration="default"
                    behaviorConfiguration="sbTokenProvider"
                    address="" />
        </service>
    </services>
    ```
   
    Este paso configura un servicio que utiliza predeterminado Hola definido anteriormente **webHttpRelayBinding**. También se utiliza de forma predeterminada hello **sbTokenProvider**, que se define en el paso siguiente de saludo.
4. Después de hello `<services>` elemento, crear una `<behaviors>` elemento con hello siguen contenido, reemplazando "SAS_KEY" con hello *firma de acceso compartido* clave (SAS) que ha obtenido anteriormente de hello [portal de Azure ][Azure portal].
   
    ```xml
    <behaviors>
        <endpointBehaviors>
            <behavior name="sbTokenProvider">
                <transportClientEndpointBehavior>
                    <tokenProvider>
                        <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
                    </tokenProvider>
                </transportClientEndpointBehavior>
            </behavior>
            </endpointBehaviors>
            <serviceBehaviors>
                <behavior name="default">
                    <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
                </behavior>
            </serviceBehaviors>
    </behaviors>
    ```
5. Aún en un archivo App.config, Hola `<appSettings>` elemento, reemplace el valor de cadena de conexión completa de hello con cadena de conexión de hello obtenido previamente desde el portal de Hola. 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. De hello **generar** menú, haga clic en **generar solución** toobuild Hola toda la solución.

### <a name="example"></a>Ejemplo
Hello código siguiente muestra hello contrato e implementación del servicio para un servicio basado en REST que se ejecuta en el Bus de servicio con hello **WebHttpRelayBinding** enlace.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{


    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

Hello en el ejemplo siguiente se muestra archivo App.config de hello asociado con el servicio de Hola.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove hello ones they don't need. -->
            <behaviorExtensions>
                <add name="connectionStatusBehavior"
                    type="Microsoft.ServiceBus.Configuration.ConnectionStatusElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="transportClientEndpointBehavior"
                    type="Microsoft.ServiceBus.Configuration.TransportClientEndpointBehaviorElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="serviceRegistrySettings"
                    type="Microsoft.ServiceBus.Configuration.ServiceRegistrySettingsElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </behaviorExtensions>
            <bindingElementExtensions>
                <add name="netMessagingTransport"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingTransportExtensionElement, Microsoft.ServiceBus,  Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="tcpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.TcpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpsRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpsRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="onewayRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.RelayedOnewayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingElementExtensions>
            <bindingExtensions>
                <add name="basicHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.BasicHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="webHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WebHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="ws2007HttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WS2007HttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netOnewayRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetOnewayRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netEventRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetEventRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netMessagingBinding"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingExtensions>
        </extensions>
      <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
          <binding name="default">
            <security relayClientAuthenticationType="None" />
          </binding>
        </webHttpRelayBinding>
      </bindings>
      <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
          <endpoint name="RelayEndpoint"
                  contract="Microsoft.ServiceBus.Samples.IImageContract"
                  binding="webHttpRelayBinding"
                  bindingConfiguration="default"
                  behaviorConfiguration="sbTokenProvider"
                  address="" />
        </service>
      </services>
      <behaviors>
        <endpointBehaviors>
          <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
              <tokenProvider>
                <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
        <serviceBehaviors>
          <behavior name="default">
            <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
          </behavior>
        </serviceBehaviors>
      </behaviors>
    </system.serviceModel>
    <appSettings>
        <!-- Service Bus specific app setings for messaging connections -->
        <add key="Microsoft.ServiceBus.ConnectionString"
            value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey="YOUR_SAS_KEY"/>
    </appSettings>
</configuration>
```

## <a name="step-4-host-hello-rest-based-wcf-service-toouse-azure-relay"></a>Paso 4: Host Hola WCF basado en REST servicio toouse retransmisión de Azure
Este paso describe cómo toorun una web service con una aplicación de consola con la retransmisión de WCF. Obtener una lista completa del código de hello escrito en este paso se proporciona en el ejemplo de Hola Hola procedimiento.

### <a name="toocreate-a-base-address-for-hello-service"></a>una dirección base para el servicio de hello toocreate
1. Hola `Main()` declaración de función, cree un espacio de nombres de variable toostore Hola del proyecto. Asegúrese de que tooreplace `yourNamespace` con nombre hello del espacio de nombres de retransmisión de Hola que creó anteriormente.
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    Bus de servicio usa nombre Hola de su toocreate de espacio de nombres un URI único.
2. Crear un `Uri` instancia para la dirección base Hola del servicio de Hola que se basa en el espacio de nombres de Hola.
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="toocreate-and-configure-hello-web-service-host"></a>toocreate y configurar el host del servicio web Hola
* Crear el host del servicio web hello, con la dirección URI de hello creada anteriormente en esta sección.
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    host de servicio de Hello es objeto WCF de Hola que crea una instancia de la aplicación de host de Hola. En este ejemplo se pasa el tipo de saludo del host que desea toocreate (un **ImageService**), y también Hola dirección a la que desea que aplicación de host de tooexpose Hola.

### <a name="toorun-hello-web-service-host"></a>host de servicio web de toorun Hola
1. Abra el servicio de Hola.
   
    ```csharp
    host.Open();
    ```
    Ahora se está ejecutando el servicio de Hola.
2. Muestra un mensaje que indica que está ejecutando el servicio de Hola y cómo toostop Hola servicio.
   
    ```csharp
    Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. Cuando termine, cierre el host de servicio de Hola.
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a>Ejemplo
Hola siguiente ejemplo incluye contrato de servicio de Hola y la implementación de los pasos anteriores en el servicio de Hola de hello tutorial y hospeda en una aplicación de consola. Compile Hola siguiente código en un archivo ejecutable denominado ImageListener.exe.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string serviceNamespace = "InsertServiceNamespaceHere";
            Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");

            WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
            host.Open();

            Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-hello-code"></a>Compilar código de hello
Después de compilar la solución de hello, Hola después de la aplicación de hello toorun:

1. Presione **F5**, o busque la ubicación del archivo ejecutable toohello (ImageListener\bin\Debug\ImageListener.exe), servicio de hello toorun. Mantener Hola ejecutando la aplicación, tal y como se requería paso siguiente de tooperform Hola.
2. Copie y pegue la dirección de Hola Hola desde línea de comandos en una imagen de hello toosee de explorador.
3. Cuando haya terminado, presione **ENTRAR** en aplicación Hola de hello símbolo ventana tooclose.

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha creado una aplicación que utiliza el servicio de retransmisión de Bus de servicio de hello, vea Hola siguiendo artículos toolearn más acerca de la retransmisión de Azure:

* [Información general sobre la arquitectura de Azure Service Bus](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [Introducción a Azure Relay](relay-what-is-it.md)
* [Cómo el servicio con .NET de la retransmisión de hello toouse WCF](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
