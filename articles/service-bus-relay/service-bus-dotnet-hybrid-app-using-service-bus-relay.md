---
title: "aplicación de en-local o una nube híbrida de retransmisión de WCF (. NET) aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de la aplicación de toocreate una .NET en local y la nube híbrida mediante retransmisión de WCF de Azure."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9ed02f7c-ebfb-4f39-9c97-b7dc15bcb4c1
ms.service: service-bus-relay
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: sethm
ms.openlocfilehash: aab8b1dbdc85c4edf7b0ccef0921b69524b2d306
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a>Aplicación híbrida en la nube o local de .NET con la retransmisión de WCF de Azure
## <a name="introduction"></a>Introducción

Este artículo muestra cómo toobuild un híbrido en la nube de aplicación con Microsoft Azure y Visual Studio. tutorial de Hola se da por supuesto que no tiene ninguna experiencia previa con Azure. En menos de 30 minutos, tendrá una aplicación que utilice varios recursos de Azure y ejecutar en la nube de Hola.

Aprenderá a:

* ¿Cómo toocreate o adaptar un servicio web existente para su uso por una solución web.
* Cómo toouse Hola tooshare datos del servicio de retransmisión de WCF de Azure entre una aplicación de Azure y un servicio web había hospedado en otro lugar.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a>Cómo ayuda Relay de Azure con soluciones híbridas

Soluciones empresariales suelen constar de una combinación de código personalizado escrito tootackle nueva y requisitos empresariales únicos y funcionalidad existente proporcionada por las soluciones y los sistemas que ya están instalados.

Arquitectos de soluciones están comenzando en la nube toouse hello para el control sea más fácil de los requisitos de escala y menores costos operativos. Si lo hace, estos clientes encuentran que activos existentes de servicio que les gustaría usar tooleverage como bloques de creación para sus soluciones están dentro del firewall corporativo de Hola y de fácil obtener acceso para el acceso si solución hello en la nube. No se generan o se hospeda de forma que puede exponer fácilmente en el perímetro de la red corporativa de hello muchos servicios internos.

[Retransmisión Azure](https://azure.microsoft.com/services/service-bus/) está diseñado para Hola casos de uso de seguridad existente servicios web de Windows Communication Foundation (WCF) y hacer que los servicios toosolutions accesible de forma segura que residen perímetro Hola corporativa sin necesidad de infraestructura de red corporativa de cambios intrusivo toohello. Dichos servicios de retransmisión todavía están alojadas en su entorno existente, pero delegan la escucha entrantes sesiones y solicitudes toohello hospedada en la nube servicio de retransmisión. Azure Relay también protege dichos servicios del acceso no autorizado mediante el uso de la autenticación de [Firma de acceso compartido (SAS)](../service-bus-messaging/service-bus-sas.md).

## <a name="solution-scenario"></a>Escenario de la solución
En este tutorial, creará un sitio Web ASP.NET que permite toosee una lista de productos en la página de inventario de productos de Hola.

![][0]

tutorial de Hola se supone que tiene información de producto en un sistema local existente y usa Azure retransmisión tooreach en ese sistema. Esto lo simula un servicio web que se ejecuta en una aplicación de consola simple y el respaldo lo proporciona un conjunto de productos en memoria. Se pueden toorun capaz de esta aplicación de consola en su propio equipo e implementar el rol web de hello en Azure. Al hacerlo, verá cómo los rol de hello web que se ejecuta en hello centro de datos Azure realmente llamará en el equipo, incluso aunque el equipo va a residir casi con toda seguridad detrás de al menos un servidor de seguridad y una capa de traducción (NAT) de la dirección de red.

## <a name="set-up-hello-development-environment"></a>Configurar el entorno de desarrollo de Hola

Antes de empezar a desarrollar aplicaciones de Azure, descargue las herramientas de Hola y configurar el entorno de desarrollo:

1. Instalar hello Azure SDK para .NET de hello SDK [página de descargas](https://azure.microsoft.com/downloads/).
2. Hola **.NET** columna, haga clic en la versión de Hola de [Visual Studio](http://www.visualstudio.com) que usa. Hola los pasos de este tutorial, use Visual Studio 2015, pero también funcionan con Visual Studio de 2017.
3. Cuando se le pida toorun o guardar el instalador de hello, haga clic en **ejecutar**.
4. Hola **instalador de plataforma Web**, haga clic en **instalar** y continuar con la instalación de Hola.
5. Una vez completada la instalación de hello, tendrá todo lo necesario toostart toodevelop Hola aplicación. Hola SDK incluye herramientas que le permiten desarrollar fácilmente aplicaciones de Azure en Visual Studio.

## <a name="create-a-namespace"></a>Creación de un espacio de nombres

usar toobegin Hola características de retransmisión en Azure, primero debe crear un espacio de nombres de servicio. Un espacio de nombres proporciona un contenedor con un ámbito para el desvío de recursos de Azure en la aplicación. Siga hello [instrucciones a continuación](relay-create-namespace-portal.md) toocreate un espacio de nombres de retransmisión.

## <a name="create-an-on-premises-server"></a>Creación de un servidor local

En primer lugar, cree un sistema de catálogo de productos local (ficticio). Es bastante sencillo; puede ver esto representa un sistema de catálogo de producto real de local a una superficie completa del servicio que estamos intentando toointegrate.

Este proyecto es una aplicación de consola de Visual Studio y usa hello [paquete NuGet de Bus de servicio de Azure](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude Hola bibliotecas de Bus de servicio y la configuración.

### <a name="create-hello-project"></a>Crear proyecto de Hola

1. Inicie Microsoft Visual Studio con privilegios de administrador. por lo tanto, haga clic en el icono de programa de Visual Studio de hello toodo y, a continuación, haga clic en **ejecutar como administrador**.
2. En Visual Studio, en hello **archivo** menú, haga clic en **New**y, a continuación, haga clic en **proyecto**.
3. En **Plantillas instaladas**, en **Visual C#**, haga clic en **Aplicación de consola (.NET Framework)**. Hola **nombre** cuadro, escriba un nombre hello **ProductsServer**:

   ![][11]
4. Haga clic en **Aceptar** toocreate hello **ProductsServer** proyecto.
5. Si ya ha instalado el Administrador de paquetes de NuGet Hola para Visual Studio, omita el paso siguiente toohello. De lo contrario, visite [NuGet][NuGet] y haga clic en [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) (Instalar NuGet). Siga el Administrador de paquetes de NuGet de Hola Hola mensajes tooinstall, a continuación, vuelva a iniciar Visual Studio.
6. En el Explorador de soluciones, haga clic en hello **ProductsServer** proyecto, a continuación, haga clic en **administrar paquetes de NuGet**.
7. Haga clic en hello **examinar** y, después, busque `Microsoft Azure Service Bus`. Seleccione hello **WindowsAzure.ServiceBus** paquete.
8. Haga clic en **instalar**y acepte los términos de Hola de uso.

   ![][13]

   Tenga en cuenta que Hola ahora ensamblados de cliente al que se hace referencia.
8. Agregue una clase nueva para el contrato de su producto. En el Explorador de soluciones, haga clic en hello **ProductsServer** del proyecto y haga clic en **agregar**y, a continuación, haga clic en **clase**.
9. Hola **nombre** cuadro, escriba un nombre hello **ProductsContract.cs**. A continuación, haga clic en **Agregar**.
10. En **ProductsContract.cs**, reemplace la definición de espacio de nombres de hello con hello siguiente código, que define el contrato de hello para el servicio de Hola.

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define hello data contract for hello service
        [DataContract]
        // Declare hello serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define hello service contract.
        [ServiceContract]
        interface IProducts
        {
            [OperationContract]
            IList<ProductData> GetProducts();

        }

        interface IProductsChannel : IProducts, IClientChannel
        {
        }
    }
    ```
11. En Program.cs, reemplace la definición de espacio de nombres de hello con hello siguiente código, que agrega el servicio de perfiles de Hola y host de Hola para él.

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement hello IProducts interface.
        class ProductsService : IProducts
        {

            // Populate array of products for display on website
            ProductData[] products =
                new []
                    {
                        new ProductData{ Id = "1", Name = "Rock",
                                         Quantity = "1"},
                        new ProductData{ Id = "2", Name = "Paper",
                                         Quantity = "3"},
                        new ProductData{ Id = "3", Name = "Scissors",
                                         Quantity = "5"},
                        new ProductData{ Id = "4", Name = "Well",
                                         Quantity = "2500"},
                    };

            // Display a message in hello service console application
            // when hello list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define hello Main() function in hello service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER tooclose");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. En el Explorador de soluciones, haga doble clic en hello **App.config** tooopen de archivos en el editor de Visual Studio Hola. En parte inferior de Hola de hello `<system.ServiceModel>` elemento (pero aún dentro `<system.ServiceModel>`), agregar Hola después el código XML. Ser seguro tooreplace *yourServiceNamespace* con nombre hello del espacio de nombres, y *yourKey* con la clave SAS de hello recuperó anteriormente desde el portal de hello:

    ```xml
    <system.serviceModel>
    ...
      <services>
         <service name="ProductsServer.ProductsService">
           <endpoint address="sb://yourServiceNamespace.servicebus.windows.net/products" binding="netTcpRelayBinding" contract="ProductsServer.IProducts" behaviorConfiguration="products"/>
         </service>
      </services>
      <behaviors>
         <endpointBehaviors>
           <behavior name="products">
             <transportClientEndpointBehavior>
                <tokenProvider>
                   <sharedAccessSignature keyName="RootManageSharedAccessKey" key="yourKey" />
                </tokenProvider>
             </transportClientEndpointBehavior>
           </behavior>
         </endpointBehaviors>
      </behaviors>
    </system.serviceModel>
    ```
13. Aún en un archivo App.config, Hola `<appSettings>` elemento, reemplace el valor de cadena de conexión de hello con cadena de conexión de hello obtenido previamente desde el portal de Hola.

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. Presione **Ctrl + Mayús + B** o de hello **generar** menú, haga clic en **generar solución** toobuild Hola aplicación y compruebe precisión Hola de su trabajo hasta ahora.

## <a name="create-an-aspnet-application"></a>Creación de una aplicación ASP.NET

En esta sección se creará una aplicación ASP.NET simple que mostrará los datos recuperados del servicio de producto.

### <a name="create-hello-project"></a>Crear proyecto de Hola

1. Asegúrese de que se está ejecutando Visual Studio con privilegios de administrador.
2. En Visual Studio, en hello **archivo** menú, haga clic en **New**y, a continuación, haga clic en **proyecto**.
3. En **Plantillas instaladas**, en **Visual C#**, haga clic en **Aplicación web ASP.NET (.NET Framework)**. Proyecto de hello Name **ProductsPortal**. y, a continuación, haga clic en **Aceptar**.

   ![][15]

4. De hello **plantillas ASP.NET** lista Hola **nueva aplicación Web ASP.NET** cuadro de diálogo, haga clic en **MVC**.

   ![][16]

6. Haga clic en hello **Cambiar autenticación** botón. Hola **Cambiar autenticación** diálogo cuadro, asegúrese de que **sin autenticación** está seleccionada y, a continuación, haga clic en **Aceptar**. En este tutorial, va a implementar una aplicación que no necesita un inicio de sesión de usuario.

    ![][18]

7. Nuevo en hello **nueva aplicación Web ASP.NET** cuadro de diálogo, haga clic en **Aceptar** aplicación MVC de hello toocreate.
8. Ahora debe configurar recursos de Azure para una aplicación web nueva. Siga los pasos de Hola Hola [publicar tooAzure sección de este artículo](../app-service-web/app-service-web-get-started-dotnet.md). A continuación, devolver toothis tutorial y continúe toohello siguiente paso.
10. En el Explorador de soluciones, haga clic con el botón derecho en **Modelos** y, luego, en **Agregar** y, por último, en **Clase**. Hola **nombre** cuadro, escriba un nombre hello **Product.cs**. A continuación, haga clic en **Agregar**.

    ![][17]

### <a name="modify-hello-web-application"></a>Modificar la aplicación web de hello

1. En archivo de Product.cs de hello en Visual Studio, reemplace la definición de espacio de nombres existente de hello con el siguiente código de hello.

   ```csharp
    // Declare properties for hello products inventory.
    namespace ProductsWeb.Models
    {
       public class Product
       {
           public string Id { get; set; }
           public string Name { get; set; }
           public string Quantity { get; set; }
       }
    }
    ```
2. En el Explorador de soluciones, expanda hello **controladores** carpeta, a continuación, haga doble clic en hello **HomeController.cs** tooopen de archivos en Visual Studio.
3. En **HomeController.cs**, reemplazar la definición de espacio de nombres existente de Hola con el siguiente código de hello.

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of hello products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. En el Explorador de soluciones, expanda la carpeta Views\Shared de hello, a continuación, haga doble clic en **_Layout.cshtml** tooopen en el editor de Visual Studio Hola.
5. Cambie todas las apariciones de **mi aplicación ASP.NET** demasiado**productos de LITWARE**.
6. Quitar hello **inicio**, **sobre**, y **póngase en contacto con** vínculos. En el siguiente ejemplo de Hola, eliminar código de hello resaltado.

    ![][41]

7. En el Explorador de soluciones, expanda la carpeta Views\Home de hello, a continuación, haga doble clic en **Index.cshtml** tooopen en el editor de Visual Studio Hola. Reemplace Hola todo contenido de archivo hello con hello siguiente código.

   ```html
   @model IEnumerable<ProductsWeb.Models.Product>

   @{
            ViewBag.Title = "Index";
   }

   <h2>Prod Inventory</h2>

   <table>
             <tr>
                 <th>
                     @Html.DisplayNameFor(model => model.Name)
                 </th>
                 <th></th>
                 <th>
                     @Html.DisplayNameFor(model => model.Quantity)
                 </th>
             </tr>

   @foreach (var item in Model) {
             <tr>
                 <td>
                     @Html.DisplayFor(modelItem => item.Name)
                 </td>
                 <td>
                     @Html.DisplayFor(modelItem => item.Quantity)
                 </td>
             </tr>
   }

   </table>
   ```
8. precisión de hello tooverify de su trabajo hasta ahora, puede presionar **Ctrl + Mayús + B** proyecto de hello toobuild.

### <a name="run-hello-app-locally"></a>Ejecutar la aplicación hello localmente

Ejecute tooverify de aplicación Hola que funciona.

1. Asegúrese de que **ProductsPortal** es Hola de proyecto activo. Haga clic en nombre de proyecto de hello en el Explorador de soluciones y seleccione **establecer como proyecto de inicio**.
2. En Visual Studio, presione **F5**.
3. La aplicación debería aparecer ejecutándose en un explorador.

   ![][21]

## <a name="put-hello-pieces-together"></a>Reunir piezas Hola

Hola siguiente paso es toohook servidor de productos de hello en local con hello aplicación ASP.NET.

1. Si no está ya abierto, en Visual Studio vuelve a abrir hello **ProductsPortal** proyecto que creó en hello [crear una aplicación ASP.NET](#create-an-aspnet-application) sección.
2. Paso de toohello similar en la sección "Crear un servidor local" de hello, agregue referencias de proyecto de toohello de paquete de hello NuGet. En el Explorador de soluciones, haga clic en hello **ProductsPortal** proyecto, a continuación, haga clic en **administrar paquetes de NuGet**.
3. La búsqueda de "Bus de servicio" y seleccione hello **WindowsAzure.ServiceBus** elemento. A continuación, completar la instalación de Hola y cerrar este cuadro de diálogo.
4. En el Explorador de soluciones, haga clic en hello **ProductsPortal** proyecto, a continuación, haga clic en **agregar**, a continuación, **elemento existente**.
5. Navegue toohello **ProductsContract.cs** archivo de hello **ProductsServer** proyecto de consola. Haga clic en toohighlight ProductsContract.cs. Haga clic en hello flecha abajo junto demasiado**agregar**, a continuación, haga clic en **agregar como vínculo**.

   ![][24]

6. Ahora, abra hello **HomeController.cs** un archivo en el editor de Visual Studio de Hola y reemplace la definición de espacio de nombres de hello con hello siguiente código. Ser seguro tooreplace *yourServiceNamespace* con el nombre de Hola de su espacio de nombres de servicio, y *yourKey* con su clave SAS. Esto le permitirá hello toocall Hola local servicio de cliente, devolver el resultado de hello de llamada de Hola.

   ```csharp
   namespace ProductsWeb.Controllers
   {
       using System.Linq;
       using System.ServiceModel;
       using System.Web.Mvc;
       using Microsoft.ServiceBus;
       using Models;
       using ProductsServer;

       public class HomeController : Controller
       {
           // Declare hello channel factory.
           static ChannelFactory<IProductsChannel> channelFactory;

           static HomeController()
           {
               // Create shared access signature token credentials for authentication.
               channelFactory = new ChannelFactory<IProductsChannel>(new NetTcpRelayBinding(),
                   "sb://yourServiceNamespace.servicebus.windows.net/products");
               channelFactory.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior {
                   TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                       "RootManageSharedAccessKey", "yourKey") });
           }

           public ActionResult Index()
           {
               using (IProductsChannel channel = channelFactory.CreateChannel())
               {
                   // Return a view of hello products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. En el Explorador de soluciones, haga clic en hello **ProductsPortal** solución (asegúrese de que tooright y haga clic en Hola solución, no en proyecto de Hola). Haga clic en **Agregar** y, a continuación, en **Proyecto existente**.
8. Navegue toohello **ProductsServer** proyecto, a continuación, haga doble clic en hello **ProductsServer.csproj** tooadd del archivo de solución.
9. **ProductsServer** debe estar ejecutándose en los datos del pedido toodisplay hello en **ProductsPortal**. En el Explorador de soluciones, haga clic en hello **ProductsPortal** solución y haga clic en **propiedades**. Hola **páginas de propiedades** se muestra el cuadro de diálogo.
10. En el lado izquierdo de hello, haga clic en **proyecto de inicio**. En el lado derecho de hello, haga clic en **proyectos de inicio múltiples**. Asegúrese de que **ProductsServer** y **ProductsPortal** aparecen, en ese orden, con **iniciar** establecer como acción de Hola para ambos.

      ![][25]

11. Aún en hello **propiedades** cuadro de diálogo, haga clic en **dependencias del proyecto** en hello lado izquierdo.
12. Hola **proyectos** lista, haga clic en **ProductsServer**. Asegúrese de que la opción **ProductsPortal** no esté seleccionada.
13. Hola **proyectos** lista, haga clic en **ProductsPortal**. Asegúrese de que **ProductsServer** esté seleccionado.

    ![][26]

14. Haga clic en **Aceptar** en hello **páginas de propiedades** cuadro de diálogo.

## <a name="run-hello-project-locally"></a>Ejecutar el proyecto de hello localmente

aplicación de hello tootest localmente, en Visual Studio presione **F5**. servidor local de Hello (**ProductsServer**) debe iniciar primero, a continuación, Hola **ProductsPortal** debe iniciarse la aplicación en una ventana del explorador. Esta vez, verá que inventario de productos de hello enumera los datos recuperados del sistema de hello producto servicio local.

![][10]

Presione **actualizar** en hello **ProductsPortal** página. Cada vez que se actualice la página de hello, verá la aplicación de servidor hello se muestra un mensaje cuando `GetProducts()` de **ProductsServer** se llama.

Cierre ambas aplicaciones antes del paso siguiente de toohello de continuar.

## <a name="deploy-hello-productsportal-project-tooan-azure-web-app"></a>Implementar la aplicación web de Azure de hello ProductsPortal proyecto tooan

Hola siguiente paso es aplicación de Azure Web hello toorepublish **ProductsPortal** front-end. Hola siguientes:

1. En el Explorador de soluciones, haga clic en hello **ProductsPortal** del proyecto y haga clic en **publicar**. A continuación, haga clic en **publicar** en hello **publicar** página.

  > [!NOTE]
  > Puede ver un mensaje de error en la ventana del explorador hello cuando hello **ProductsPortal** proyecto web se inicia automáticamente después de la implementación de Hola. Esto es normal y se produce porque hello **ProductsServer** aplicación no se está ejecutando todavía.
>
>

2. Copiar dirección URL de Hola de hello implementa la aplicación web, ya que será necesario URL hello en el paso siguiente de Hola. También puede obtener esta dirección URL de la ventana de actividad del servicio de aplicación de Azure de hello en Visual Studio:

  ![][9]

3. Cierre Hola de toostop de ventana hello explorador ejecutando la aplicación.

### <a name="set-productsportal-as-web-app"></a>Establecimiento de ProductsPortal como aplicación web

Antes de la aplicación en ejecución hello en la nube de hello, debe asegurarse de que **ProductsPortal** se inicia desde dentro de Visual Studio como una aplicación web.

1. En Visual Studio, haga clic en hello **ProductsPortal** del proyecto y, a continuación, haga clic en **propiedades**.
2. En la columna izquierda de hello, haga clic en **Web**.
3. Hola **acción de inicio** sección, haga clic en hello **dirección URL de inicio** botón y, en el cuadro de texto hello escriba Hola URL para la aplicación web implementada anteriormente; por ejemplo, `http://productsportal1234567890.azurewebsites.net/`.

    ![][27]

4. De hello **archivo** menú en Visual Studio, haga clic en **guardar todo**.
5. En el menú de compilación de hello en Visual Studio, haga clic en **volver a generar solución**.

## <a name="run-hello-application"></a>Ejecutar la aplicación hello

1. Presione F5 toobuild y ejecute la aplicación hello. servidor local de Hello (hello **ProductsServer** aplicación de consola) debe iniciar primero, a continuación, Hola **ProductsPortal** aplicación debe comenzar en una ventana del explorador, como se muestra en hello después de la pantalla captura. Tenga en cuenta nuevo ese inventario de productos de Hola enumera los datos recuperados del sistema de hello producto servicio local y muestra los datos en la aplicación web de hello. Comprobar Hola URL toomake seguro de que **ProductsPortal** se ejecuta en la nube hello, como una aplicación web de Azure.

   ![][1]

   > [!IMPORTANT]
   > Hola **ProductsServer** aplicación de consola debe estar en ejecución y puede tooserve Hola datos toohello **ProductsPortal** aplicación. Si el Explorador de hello muestra un error, espere unos segundos más **ProductsServer** tooload y Hola mostrar después de los mensajes. A continuación, presione **actualizar** en el Explorador de Hola.
   >
   >

   ![][37]
2. En el Explorador de hello, presione **actualizar** en hello **ProductsPortal** página. Cada vez que se actualice la página de hello, verá la aplicación de servidor hello se muestra un mensaje cuando `GetProducts()` de **ProductsServer** se llama.

    ![][38]

## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de la retransmisión de Azure, vea Hola recursos siguientes:  

* [¿Qué es Relay de Azure?](relay-what-is-it.md)  
* [¿Cómo de retransmisión toouse](service-bus-dotnet-how-to-use-relay.md)  

[0]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hybrid.png
[1]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[NuGet]: http://nuget.org

[11]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-con-1.png
[13]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-13.png
[15]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-2.png
[16]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-4.png
[17]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-7.png
[18]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-5.png
[9]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-9.png
[10]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App3.png

[21]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App1.png
[24]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-12.png
[25]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-13.png
[26]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-14.png
[27]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-8.png

[36]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[37]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service1.png
[38]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service2.png
[41]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-40.png
[43]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-hybrid-43.png
