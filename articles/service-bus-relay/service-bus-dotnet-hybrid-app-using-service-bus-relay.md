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
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a><span data-ttu-id="26513-103">Aplicación híbrida en la nube o local de .NET con la retransmisión de WCF de Azure</span><span class="sxs-lookup"><span data-stu-id="26513-103">.NET on-premises/cloud hybrid application using Azure WCF Relay</span></span>
## <a name="introduction"></a><span data-ttu-id="26513-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="26513-104">Introduction</span></span>

<span data-ttu-id="26513-105">Este artículo muestra cómo toobuild un híbrido en la nube de aplicación con Microsoft Azure y Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26513-105">This article shows how toobuild a hybrid cloud application with Microsoft Azure and Visual Studio.</span></span> <span data-ttu-id="26513-106">tutorial de Hola se da por supuesto que no tiene ninguna experiencia previa con Azure.</span><span class="sxs-lookup"><span data-stu-id="26513-106">hello tutorial assumes you have no prior experience using Azure.</span></span> <span data-ttu-id="26513-107">En menos de 30 minutos, tendrá una aplicación que utilice varios recursos de Azure y ejecutar en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="26513-107">In less than 30 minutes, you will have an application that uses multiple Azure resources up and running in hello cloud.</span></span>

<span data-ttu-id="26513-108">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="26513-108">You will learn:</span></span>

* <span data-ttu-id="26513-109">¿Cómo toocreate o adaptar un servicio web existente para su uso por una solución web.</span><span class="sxs-lookup"><span data-stu-id="26513-109">How toocreate or adapt an existing web service for consumption by a web solution.</span></span>
* <span data-ttu-id="26513-110">Cómo toouse Hola tooshare datos del servicio de retransmisión de WCF de Azure entre una aplicación de Azure y un servicio web había hospedado en otro lugar.</span><span class="sxs-lookup"><span data-stu-id="26513-110">How toouse hello Azure WCF Relay service tooshare data between an Azure application and a web service hosted elsewhere.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a><span data-ttu-id="26513-111">Cómo ayuda Relay de Azure con soluciones híbridas</span><span class="sxs-lookup"><span data-stu-id="26513-111">How Azure Relay helps with hybrid solutions</span></span>

<span data-ttu-id="26513-112">Soluciones empresariales suelen constar de una combinación de código personalizado escrito tootackle nueva y requisitos empresariales únicos y funcionalidad existente proporcionada por las soluciones y los sistemas que ya están instalados.</span><span class="sxs-lookup"><span data-stu-id="26513-112">Business solutions are typically composed of a combination of custom code written tootackle new and unique business requirements and existing functionality provided by solutions and systems that are already in place.</span></span>

<span data-ttu-id="26513-113">Arquitectos de soluciones están comenzando en la nube toouse hello para el control sea más fácil de los requisitos de escala y menores costos operativos.</span><span class="sxs-lookup"><span data-stu-id="26513-113">Solution architects are starting toouse hello cloud for easier handling of scale requirements and lower operational costs.</span></span> <span data-ttu-id="26513-114">Si lo hace, estos clientes encuentran que activos existentes de servicio que les gustaría usar tooleverage como bloques de creación para sus soluciones están dentro del firewall corporativo de Hola y de fácil obtener acceso para el acceso si solución hello en la nube.</span><span class="sxs-lookup"><span data-stu-id="26513-114">In doing so, they find that existing service assets they'd like tooleverage as building blocks for their solutions are inside hello corporate firewall and out of easy reach for access by hello cloud solution.</span></span> <span data-ttu-id="26513-115">No se generan o se hospeda de forma que puede exponer fácilmente en el perímetro de la red corporativa de hello muchos servicios internos.</span><span class="sxs-lookup"><span data-stu-id="26513-115">Many internal services are not built or hosted in a way that they can be easily exposed at hello corporate network edge.</span></span>

<span data-ttu-id="26513-116">[Retransmisión Azure](https://azure.microsoft.com/services/service-bus/) está diseñado para Hola casos de uso de seguridad existente servicios web de Windows Communication Foundation (WCF) y hacer que los servicios toosolutions accesible de forma segura que residen perímetro Hola corporativa sin necesidad de infraestructura de red corporativa de cambios intrusivo toohello.</span><span class="sxs-lookup"><span data-stu-id="26513-116">[Azure Relay](https://azure.microsoft.com/services/service-bus/) is designed for hello use-case of taking existing Windows Communication Foundation (WCF) web services and making those services securely accessible toosolutions that reside outside hello corporate perimeter without requiring intrusive changes toohello corporate network infrastructure.</span></span> <span data-ttu-id="26513-117">Dichos servicios de retransmisión todavía están alojadas en su entorno existente, pero delegan la escucha entrantes sesiones y solicitudes toohello hospedada en la nube servicio de retransmisión.</span><span class="sxs-lookup"><span data-stu-id="26513-117">Such relay services are still hosted inside their existing environment, but they delegate listening for incoming sessions and requests toohello cloud-hosted relay service.</span></span> <span data-ttu-id="26513-118">Azure Relay también protege dichos servicios del acceso no autorizado mediante el uso de la autenticación de [Firma de acceso compartido (SAS)](../service-bus-messaging/service-bus-sas.md).</span><span class="sxs-lookup"><span data-stu-id="26513-118">Azure Relay also protects those services from unauthorized access by using [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) authentication.</span></span>

## <a name="solution-scenario"></a><span data-ttu-id="26513-119">Escenario de la solución</span><span class="sxs-lookup"><span data-stu-id="26513-119">Solution scenario</span></span>
<span data-ttu-id="26513-120">En este tutorial, creará un sitio Web ASP.NET que permite toosee una lista de productos en la página de inventario de productos de Hola.</span><span class="sxs-lookup"><span data-stu-id="26513-120">In this tutorial, you will create an ASP.NET website that enables you toosee a list of products on hello product inventory page.</span></span>

![][0]

<span data-ttu-id="26513-121">tutorial de Hola se supone que tiene información de producto en un sistema local existente y usa Azure retransmisión tooreach en ese sistema.</span><span class="sxs-lookup"><span data-stu-id="26513-121">hello tutorial assumes that you have product information in an existing on-premises system, and uses Azure Relay tooreach into that system.</span></span> <span data-ttu-id="26513-122">Esto lo simula un servicio web que se ejecuta en una aplicación de consola simple y el respaldo lo proporciona un conjunto de productos en memoria.</span><span class="sxs-lookup"><span data-stu-id="26513-122">This is simulated by a web service that runs in a simple console application and is backed by an in-memory set of products.</span></span> <span data-ttu-id="26513-123">Se pueden toorun capaz de esta aplicación de consola en su propio equipo e implementar el rol web de hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="26513-123">You will be able toorun this console application on your own computer and deploy hello web role into Azure.</span></span> <span data-ttu-id="26513-124">Al hacerlo, verá cómo los rol de hello web que se ejecuta en hello centro de datos Azure realmente llamará en el equipo, incluso aunque el equipo va a residir casi con toda seguridad detrás de al menos un servidor de seguridad y una capa de traducción (NAT) de la dirección de red.</span><span class="sxs-lookup"><span data-stu-id="26513-124">By doing so, you will see how hello web role running in hello Azure datacenter will indeed call into your computer, even though your computer will almost certainly reside behind at least one firewall and a network address translation (NAT) layer.</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="26513-125">Configurar el entorno de desarrollo de Hola</span><span class="sxs-lookup"><span data-stu-id="26513-125">Set up hello development environment</span></span>

<span data-ttu-id="26513-126">Antes de empezar a desarrollar aplicaciones de Azure, descargue las herramientas de Hola y configurar el entorno de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="26513-126">Before you can begin developing Azure applications, download hello tools and set up your development environment:</span></span>

1. <span data-ttu-id="26513-127">Instalar hello Azure SDK para .NET de hello SDK [página de descargas](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="26513-127">Install hello Azure SDK for .NET from hello SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="26513-128">Hola **.NET** columna, haga clic en la versión de Hola de [Visual Studio](http://www.visualstudio.com) que usa.</span><span class="sxs-lookup"><span data-stu-id="26513-128">In hello **.NET** column, click hello version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="26513-129">Hola los pasos de este tutorial, use Visual Studio 2015, pero también funcionan con Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="26513-129">hello steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="26513-130">Cuando se le pida toorun o guardar el instalador de hello, haga clic en **ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="26513-130">When prompted toorun or save hello installer, click **Run**.</span></span>
4. <span data-ttu-id="26513-131">Hola **instalador de plataforma Web**, haga clic en **instalar** y continuar con la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="26513-131">In hello **Web Platform Installer**, click **Install** and proceed with hello installation.</span></span>
5. <span data-ttu-id="26513-132">Una vez completada la instalación de hello, tendrá todo lo necesario toostart toodevelop Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="26513-132">Once hello installation is complete, you will have everything necessary toostart toodevelop hello app.</span></span> <span data-ttu-id="26513-133">Hola SDK incluye herramientas que le permiten desarrollar fácilmente aplicaciones de Azure en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26513-133">hello SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="26513-134">Creación de un espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="26513-134">Create a namespace</span></span>

<span data-ttu-id="26513-135">usar toobegin Hola características de retransmisión en Azure, primero debe crear un espacio de nombres de servicio.</span><span class="sxs-lookup"><span data-stu-id="26513-135">toobegin using hello relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="26513-136">Un espacio de nombres proporciona un contenedor con un ámbito para el desvío de recursos de Azure en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="26513-136">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="26513-137">Siga hello [instrucciones a continuación](relay-create-namespace-portal.md) toocreate un espacio de nombres de retransmisión.</span><span class="sxs-lookup"><span data-stu-id="26513-137">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="create-an-on-premises-server"></a><span data-ttu-id="26513-138">Creación de un servidor local</span><span class="sxs-lookup"><span data-stu-id="26513-138">Create an on-premises server</span></span>

<span data-ttu-id="26513-139">En primer lugar, cree un sistema de catálogo de productos local (ficticio).</span><span class="sxs-lookup"><span data-stu-id="26513-139">First, you will build a (mock) on-premises product catalog system.</span></span> <span data-ttu-id="26513-140">Es bastante sencillo; puede ver esto representa un sistema de catálogo de producto real de local a una superficie completa del servicio que estamos intentando toointegrate.</span><span class="sxs-lookup"><span data-stu-id="26513-140">It will be fairly simple; you can see this as representing an actual on-premises product catalog system with a complete service surface that we're trying toointegrate.</span></span>

<span data-ttu-id="26513-141">Este proyecto es una aplicación de consola de Visual Studio y usa hello [paquete NuGet de Bus de servicio de Azure](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude Hola bibliotecas de Bus de servicio y la configuración.</span><span class="sxs-lookup"><span data-stu-id="26513-141">This project is a Visual Studio console application, and uses hello [Azure Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello Service Bus libraries and configuration settings.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="26513-142">Crear proyecto de Hola</span><span class="sxs-lookup"><span data-stu-id="26513-142">Create hello project</span></span>

1. <span data-ttu-id="26513-143">Inicie Microsoft Visual Studio con privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="26513-143">Using administrator privileges, start Microsoft Visual Studio.</span></span> <span data-ttu-id="26513-144">por lo tanto, haga clic en el icono de programa de Visual Studio de hello toodo y, a continuación, haga clic en **ejecutar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="26513-144">toodo so, right-click hello Visual Studio program icon, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="26513-145">En Visual Studio, en hello **archivo** menú, haga clic en **New**y, a continuación, haga clic en **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="26513-145">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="26513-146">En **Plantillas instaladas**, en **Visual C#**, haga clic en **Aplicación de consola (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="26513-146">From **Installed Templates**, under **Visual C#**, click **Console App (.NET Framework)**.</span></span> <span data-ttu-id="26513-147">Hola **nombre** cuadro, escriba un nombre hello **ProductsServer**:</span><span class="sxs-lookup"><span data-stu-id="26513-147">In hello **Name** box, type hello name **ProductsServer**:</span></span>

   ![][11]
4. <span data-ttu-id="26513-148">Haga clic en **Aceptar** toocreate hello **ProductsServer** proyecto.</span><span class="sxs-lookup"><span data-stu-id="26513-148">Click **OK** toocreate hello **ProductsServer** project.</span></span>
5. <span data-ttu-id="26513-149">Si ya ha instalado el Administrador de paquetes de NuGet Hola para Visual Studio, omita el paso siguiente toohello.</span><span class="sxs-lookup"><span data-stu-id="26513-149">If you have already installed hello NuGet package manager for Visual Studio, skip toohello next step.</span></span> <span data-ttu-id="26513-150">De lo contrario, visite [NuGet][NuGet] y haga clic en [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) (Instalar NuGet).</span><span class="sxs-lookup"><span data-stu-id="26513-150">Otherwise, visit [NuGet][NuGet] and click [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span></span> <span data-ttu-id="26513-151">Siga el Administrador de paquetes de NuGet de Hola Hola mensajes tooinstall, a continuación, vuelva a iniciar Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26513-151">Follow hello prompts tooinstall hello NuGet package manager, then re-start Visual Studio.</span></span>
6. <span data-ttu-id="26513-152">En el Explorador de soluciones, haga clic en hello **ProductsServer** proyecto, a continuación, haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="26513-152">In Solution Explorer, right-click hello **ProductsServer** project, then click **Manage NuGet Packages**.</span></span>
7. <span data-ttu-id="26513-153">Haga clic en hello **examinar** y, después, busque `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="26513-153">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="26513-154">Seleccione hello **WindowsAzure.ServiceBus** paquete.</span><span class="sxs-lookup"><span data-stu-id="26513-154">Select hello **WindowsAzure.ServiceBus** package.</span></span>
8. <span data-ttu-id="26513-155">Haga clic en **instalar**y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="26513-155">Click **Install**, and accept hello terms of use.</span></span>

   ![][13]

   <span data-ttu-id="26513-156">Tenga en cuenta que Hola ahora ensamblados de cliente al que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="26513-156">Note that hello required client assemblies are now referenced.</span></span>
8. <span data-ttu-id="26513-157">Agregue una clase nueva para el contrato de su producto.</span><span class="sxs-lookup"><span data-stu-id="26513-157">Add a new class for your product contract.</span></span> <span data-ttu-id="26513-158">En el Explorador de soluciones, haga clic en hello **ProductsServer** del proyecto y haga clic en **agregar**y, a continuación, haga clic en **clase**.</span><span class="sxs-lookup"><span data-stu-id="26513-158">In Solution Explorer, right-click hello **ProductsServer** project and click **Add**, and then click **Class**.</span></span>
9. <span data-ttu-id="26513-159">Hola **nombre** cuadro, escriba un nombre hello **ProductsContract.cs**.</span><span class="sxs-lookup"><span data-stu-id="26513-159">In hello **Name** box, type hello name **ProductsContract.cs**.</span></span> <span data-ttu-id="26513-160">A continuación, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="26513-160">Then click **Add**.</span></span>
10. <span data-ttu-id="26513-161">En **ProductsContract.cs**, reemplace la definición de espacio de nombres de hello con hello siguiente código, que define el contrato de hello para el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="26513-161">In **ProductsContract.cs**, replace hello namespace definition with hello following code, which defines hello contract for hello service.</span></span>

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
11. <span data-ttu-id="26513-162">En Program.cs, reemplace la definición de espacio de nombres de hello con hello siguiente código, que agrega el servicio de perfiles de Hola y host de Hola para él.</span><span class="sxs-lookup"><span data-stu-id="26513-162">In Program.cs, replace hello namespace definition with hello following code, which adds hello profile service and hello host for it.</span></span>

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
12. <span data-ttu-id="26513-163">En el Explorador de soluciones, haga doble clic en hello **App.config** tooopen de archivos en el editor de Visual Studio Hola.</span><span class="sxs-lookup"><span data-stu-id="26513-163">In Solution Explorer, double-click hello **App.config** file tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="26513-164">En parte inferior de Hola de hello `<system.ServiceModel>` elemento (pero aún dentro `<system.ServiceModel>`), agregar Hola después el código XML.</span><span class="sxs-lookup"><span data-stu-id="26513-164">At hello bottom of hello `<system.ServiceModel>` element (but still within `<system.ServiceModel>`), add hello following XML code.</span></span> <span data-ttu-id="26513-165">Ser seguro tooreplace *yourServiceNamespace* con nombre hello del espacio de nombres, y *yourKey* con la clave SAS de hello recuperó anteriormente desde el portal de hello:</span><span class="sxs-lookup"><span data-stu-id="26513-165">Be sure tooreplace *yourServiceNamespace* with hello name of your namespace, and *yourKey* with hello SAS key you retrieved earlier from hello portal:</span></span>

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
13. <span data-ttu-id="26513-166">Aún en un archivo App.config, Hola `<appSettings>` elemento, reemplace el valor de cadena de conexión de hello con cadena de conexión de hello obtenido previamente desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="26513-166">Still in App.config, in hello `<appSettings>` element, replace hello connection string value with hello connection string you previously obtained from hello portal.</span></span>

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. <span data-ttu-id="26513-167">Presione **Ctrl + Mayús + B** o de hello **generar** menú, haga clic en **generar solución** toobuild Hola aplicación y compruebe precisión Hola de su trabajo hasta ahora.</span><span class="sxs-lookup"><span data-stu-id="26513-167">Press **Ctrl+Shift+B** or from hello **Build** menu, click **Build Solution** toobuild hello application and verify hello accuracy of your work so far.</span></span>

## <a name="create-an-aspnet-application"></a><span data-ttu-id="26513-168">Creación de una aplicación ASP.NET</span><span class="sxs-lookup"><span data-stu-id="26513-168">Create an ASP.NET application</span></span>

<span data-ttu-id="26513-169">En esta sección se creará una aplicación ASP.NET simple que mostrará los datos recuperados del servicio de producto.</span><span class="sxs-lookup"><span data-stu-id="26513-169">In this section you will build a simple ASP.NET application that displays data retrieved from your product service.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="26513-170">Crear proyecto de Hola</span><span class="sxs-lookup"><span data-stu-id="26513-170">Create hello project</span></span>

1. <span data-ttu-id="26513-171">Asegúrese de que se está ejecutando Visual Studio con privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="26513-171">Ensure that Visual Studio is running with administrator privileges.</span></span>
2. <span data-ttu-id="26513-172">En Visual Studio, en hello **archivo** menú, haga clic en **New**y, a continuación, haga clic en **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="26513-172">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="26513-173">En **Plantillas instaladas**, en **Visual C#**, haga clic en **Aplicación web ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="26513-173">From **Installed Templates**, under **Visual C#**, click **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="26513-174">Proyecto de hello Name **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="26513-174">Name hello project **ProductsPortal**.</span></span> <span data-ttu-id="26513-175">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="26513-175">Then click **OK**.</span></span>

   ![][15]

4. <span data-ttu-id="26513-176">De hello **plantillas ASP.NET** lista Hola **nueva aplicación Web ASP.NET** cuadro de diálogo, haga clic en **MVC**.</span><span class="sxs-lookup"><span data-stu-id="26513-176">From hello **ASP.NET Templates** list in hello **New ASP.NET Web Application** dialog, click **MVC**.</span></span>

   ![][16]

6. <span data-ttu-id="26513-177">Haga clic en hello **Cambiar autenticación** botón.</span><span class="sxs-lookup"><span data-stu-id="26513-177">Click hello **Change Authentication** button.</span></span> <span data-ttu-id="26513-178">Hola **Cambiar autenticación** diálogo cuadro, asegúrese de que **sin autenticación** está seleccionada y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="26513-178">In hello **Change Authentication** dialog box, ensure that **No Authentication** is selected, and then click **OK**.</span></span> <span data-ttu-id="26513-179">En este tutorial, va a implementar una aplicación que no necesita un inicio de sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="26513-179">For this tutorial, you're deploying an app that does not need a user login.</span></span>

    ![][18]

7. <span data-ttu-id="26513-180">Nuevo en hello **nueva aplicación Web ASP.NET** cuadro de diálogo, haga clic en **Aceptar** aplicación MVC de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="26513-180">Back in hello **New ASP.NET Web Application** dialog, click **OK** toocreate hello MVC app.</span></span>
8. <span data-ttu-id="26513-181">Ahora debe configurar recursos de Azure para una aplicación web nueva.</span><span class="sxs-lookup"><span data-stu-id="26513-181">Now you must configure Azure resources for a new web app.</span></span> <span data-ttu-id="26513-182">Siga los pasos de Hola Hola [publicar tooAzure sección de este artículo](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="26513-182">Follow hello steps in hello [Publish tooAzure section of this article](../app-service-web/app-service-web-get-started-dotnet.md).</span></span> <span data-ttu-id="26513-183">A continuación, devolver toothis tutorial y continúe toohello siguiente paso.</span><span class="sxs-lookup"><span data-stu-id="26513-183">Then, return toothis tutorial and proceed toohello next step.</span></span>
10. <span data-ttu-id="26513-184">En el Explorador de soluciones, haga clic con el botón derecho en **Modelos** y, luego, en **Agregar** y, por último, en **Clase**.</span><span class="sxs-lookup"><span data-stu-id="26513-184">In Solution Explorer, right-click **Models** and then click **Add**, then click **Class**.</span></span> <span data-ttu-id="26513-185">Hola **nombre** cuadro, escriba un nombre hello **Product.cs**.</span><span class="sxs-lookup"><span data-stu-id="26513-185">In hello **Name** box, type hello name **Product.cs**.</span></span> <span data-ttu-id="26513-186">A continuación, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="26513-186">Then click **Add**.</span></span>

    ![][17]

### <a name="modify-hello-web-application"></a><span data-ttu-id="26513-187">Modificar la aplicación web de hello</span><span class="sxs-lookup"><span data-stu-id="26513-187">Modify hello web application</span></span>

1. <span data-ttu-id="26513-188">En archivo de Product.cs de hello en Visual Studio, reemplace la definición de espacio de nombres existente de hello con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="26513-188">In hello Product.cs file in Visual Studio, replace hello existing namespace definition with hello following code.</span></span>

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
2. <span data-ttu-id="26513-189">En el Explorador de soluciones, expanda hello **controladores** carpeta, a continuación, haga doble clic en hello **HomeController.cs** tooopen de archivos en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26513-189">In Solution Explorer, expand hello **Controllers** folder, then double-click hello **HomeController.cs** file tooopen it in Visual Studio.</span></span>
3. <span data-ttu-id="26513-190">En **HomeController.cs**, reemplazar la definición de espacio de nombres existente de Hola con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="26513-190">In **HomeController.cs**, replace hello existing namespace definition with hello following code.</span></span>

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
4. <span data-ttu-id="26513-191">En el Explorador de soluciones, expanda la carpeta Views\Shared de hello, a continuación, haga doble clic en **_Layout.cshtml** tooopen en el editor de Visual Studio Hola.</span><span class="sxs-lookup"><span data-stu-id="26513-191">In Solution Explorer, expand hello Views\Shared folder, then double-click **_Layout.cshtml** tooopen it in hello Visual Studio editor.</span></span>
5. <span data-ttu-id="26513-192">Cambie todas las apariciones de **mi aplicación ASP.NET** demasiado**productos de LITWARE**.</span><span class="sxs-lookup"><span data-stu-id="26513-192">Change all occurrences of **My ASP.NET Application** too**LITWARE's Products**.</span></span>
6. <span data-ttu-id="26513-193">Quitar hello **inicio**, **sobre**, y **póngase en contacto con** vínculos.</span><span class="sxs-lookup"><span data-stu-id="26513-193">Remove hello **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="26513-194">En el siguiente ejemplo de Hola, eliminar código de hello resaltado.</span><span class="sxs-lookup"><span data-stu-id="26513-194">In hello following example, delete hello highlighted code.</span></span>

    ![][41]

7. <span data-ttu-id="26513-195">En el Explorador de soluciones, expanda la carpeta Views\Home de hello, a continuación, haga doble clic en **Index.cshtml** tooopen en el editor de Visual Studio Hola.</span><span class="sxs-lookup"><span data-stu-id="26513-195">In Solution Explorer, expand hello Views\Home folder, then double-click **Index.cshtml** tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="26513-196">Reemplace Hola todo contenido de archivo hello con hello siguiente código.</span><span class="sxs-lookup"><span data-stu-id="26513-196">Replace hello entire contents of hello file with hello following code.</span></span>

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
8. <span data-ttu-id="26513-197">precisión de hello tooverify de su trabajo hasta ahora, puede presionar **Ctrl + Mayús + B** proyecto de hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="26513-197">tooverify hello accuracy of your work so far, you can press **Ctrl+Shift+B** toobuild hello project.</span></span>

### <a name="run-hello-app-locally"></a><span data-ttu-id="26513-198">Ejecutar la aplicación hello localmente</span><span class="sxs-lookup"><span data-stu-id="26513-198">Run hello app locally</span></span>

<span data-ttu-id="26513-199">Ejecute tooverify de aplicación Hola que funciona.</span><span class="sxs-lookup"><span data-stu-id="26513-199">Run hello application tooverify that it works.</span></span>

1. <span data-ttu-id="26513-200">Asegúrese de que **ProductsPortal** es Hola de proyecto activo.</span><span class="sxs-lookup"><span data-stu-id="26513-200">Ensure that **ProductsPortal** is hello active project.</span></span> <span data-ttu-id="26513-201">Haga clic en nombre de proyecto de hello en el Explorador de soluciones y seleccione **establecer como proyecto de inicio**.</span><span class="sxs-lookup"><span data-stu-id="26513-201">Right-click hello project name in Solution Explorer and select **Set As Startup Project**.</span></span>
2. <span data-ttu-id="26513-202">En Visual Studio, presione **F5**.</span><span class="sxs-lookup"><span data-stu-id="26513-202">In Visual Studio, press **F5**.</span></span>
3. <span data-ttu-id="26513-203">La aplicación debería aparecer ejecutándose en un explorador.</span><span class="sxs-lookup"><span data-stu-id="26513-203">Your application should appear, running in a browser.</span></span>

   ![][21]

## <a name="put-hello-pieces-together"></a><span data-ttu-id="26513-204">Reunir piezas Hola</span><span class="sxs-lookup"><span data-stu-id="26513-204">Put hello pieces together</span></span>

<span data-ttu-id="26513-205">Hola siguiente paso es toohook servidor de productos de hello en local con hello aplicación ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="26513-205">hello next step is toohook up hello on-premises products server with hello ASP.NET application.</span></span>

1. <span data-ttu-id="26513-206">Si no está ya abierto, en Visual Studio vuelve a abrir hello **ProductsPortal** proyecto que creó en hello [crear una aplicación ASP.NET](#create-an-aspnet-application) sección.</span><span class="sxs-lookup"><span data-stu-id="26513-206">If it is not already open, in Visual Studio re-open hello **ProductsPortal** project you created in hello [Create an ASP.NET application](#create-an-aspnet-application) section.</span></span>
2. <span data-ttu-id="26513-207">Paso de toohello similar en la sección "Crear un servidor local" de hello, agregue referencias de proyecto de toohello de paquete de hello NuGet.</span><span class="sxs-lookup"><span data-stu-id="26513-207">Similar toohello step in hello "Create an On-Premises Server" section, add hello NuGet package toohello project references.</span></span> <span data-ttu-id="26513-208">En el Explorador de soluciones, haga clic en hello **ProductsPortal** proyecto, a continuación, haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="26513-208">In Solution Explorer, right-click hello **ProductsPortal** project, then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="26513-209">La búsqueda de "Bus de servicio" y seleccione hello **WindowsAzure.ServiceBus** elemento.</span><span class="sxs-lookup"><span data-stu-id="26513-209">Search for "Service Bus" and select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="26513-210">A continuación, completar la instalación de Hola y cerrar este cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26513-210">Then complete hello installation and close this dialog box.</span></span>
4. <span data-ttu-id="26513-211">En el Explorador de soluciones, haga clic en hello **ProductsPortal** proyecto, a continuación, haga clic en **agregar**, a continuación, **elemento existente**.</span><span class="sxs-lookup"><span data-stu-id="26513-211">In Solution Explorer, right-click hello **ProductsPortal** project, then click **Add**, then **Existing Item**.</span></span>
5. <span data-ttu-id="26513-212">Navegue toohello **ProductsContract.cs** archivo de hello **ProductsServer** proyecto de consola.</span><span class="sxs-lookup"><span data-stu-id="26513-212">Navigate toohello **ProductsContract.cs** file from hello **ProductsServer** console project.</span></span> <span data-ttu-id="26513-213">Haga clic en toohighlight ProductsContract.cs.</span><span class="sxs-lookup"><span data-stu-id="26513-213">Click toohighlight ProductsContract.cs.</span></span> <span data-ttu-id="26513-214">Haga clic en hello flecha abajo junto demasiado**agregar**, a continuación, haga clic en **agregar como vínculo**.</span><span class="sxs-lookup"><span data-stu-id="26513-214">Click hello down arrow next too**Add**, then click **Add as Link**.</span></span>

   ![][24]

6. <span data-ttu-id="26513-215">Ahora, abra hello **HomeController.cs** un archivo en el editor de Visual Studio de Hola y reemplace la definición de espacio de nombres de hello con hello siguiente código.</span><span class="sxs-lookup"><span data-stu-id="26513-215">Now open hello **HomeController.cs** file in hello Visual Studio editor and replace hello namespace definition with hello following code.</span></span> <span data-ttu-id="26513-216">Ser seguro tooreplace *yourServiceNamespace* con el nombre de Hola de su espacio de nombres de servicio, y *yourKey* con su clave SAS.</span><span class="sxs-lookup"><span data-stu-id="26513-216">Be sure tooreplace *yourServiceNamespace* with hello name of your service namespace, and *yourKey* with your SAS key.</span></span> <span data-ttu-id="26513-217">Esto le permitirá hello toocall Hola local servicio de cliente, devolver el resultado de hello de llamada de Hola.</span><span class="sxs-lookup"><span data-stu-id="26513-217">This will enable hello client toocall hello on-premises service, returning hello result of hello call.</span></span>

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
7. <span data-ttu-id="26513-218">En el Explorador de soluciones, haga clic en hello **ProductsPortal** solución (asegúrese de que tooright y haga clic en Hola solución, no en proyecto de Hola).</span><span class="sxs-lookup"><span data-stu-id="26513-218">In Solution Explorer, right-click hello **ProductsPortal** solution (make sure tooright-click hello solution, not hello project).</span></span> <span data-ttu-id="26513-219">Haga clic en **Agregar** y, a continuación, en **Proyecto existente**.</span><span class="sxs-lookup"><span data-stu-id="26513-219">Click **Add**, then click **Existing Project**.</span></span>
8. <span data-ttu-id="26513-220">Navegue toohello **ProductsServer** proyecto, a continuación, haga doble clic en hello **ProductsServer.csproj** tooadd del archivo de solución.</span><span class="sxs-lookup"><span data-stu-id="26513-220">Navigate toohello **ProductsServer** project, then double-click hello **ProductsServer.csproj** solution file tooadd it.</span></span>
9. <span data-ttu-id="26513-221">**ProductsServer** debe estar ejecutándose en los datos del pedido toodisplay hello en **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="26513-221">**ProductsServer** must be running in order toodisplay hello data on **ProductsPortal**.</span></span> <span data-ttu-id="26513-222">En el Explorador de soluciones, haga clic en hello **ProductsPortal** solución y haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="26513-222">In Solution Explorer, right-click hello **ProductsPortal** solution and click **Properties**.</span></span> <span data-ttu-id="26513-223">Hola **páginas de propiedades** se muestra el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26513-223">hello **Property Pages** dialog box is displayed.</span></span>
10. <span data-ttu-id="26513-224">En el lado izquierdo de hello, haga clic en **proyecto de inicio**.</span><span class="sxs-lookup"><span data-stu-id="26513-224">On hello left side, click **Startup Project**.</span></span> <span data-ttu-id="26513-225">En el lado derecho de hello, haga clic en **proyectos de inicio múltiples**.</span><span class="sxs-lookup"><span data-stu-id="26513-225">On hello right side, click **Multiple startup projects**.</span></span> <span data-ttu-id="26513-226">Asegúrese de que **ProductsServer** y **ProductsPortal** aparecen, en ese orden, con **iniciar** establecer como acción de Hola para ambos.</span><span class="sxs-lookup"><span data-stu-id="26513-226">Ensure that **ProductsServer** and **ProductsPortal** appear, in that order, with **Start** set as hello action for both.</span></span>

      ![][25]

11. <span data-ttu-id="26513-227">Aún en hello **propiedades** cuadro de diálogo, haga clic en **dependencias del proyecto** en hello lado izquierdo.</span><span class="sxs-lookup"><span data-stu-id="26513-227">Still in hello **Properties** dialog box, click **Project Dependencies** on hello left side.</span></span>
12. <span data-ttu-id="26513-228">Hola **proyectos** lista, haga clic en **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="26513-228">In hello **Projects** list, click **ProductsServer**.</span></span> <span data-ttu-id="26513-229">Asegúrese de que la opción **ProductsPortal** no esté seleccionada.</span><span class="sxs-lookup"><span data-stu-id="26513-229">Ensure that **ProductsPortal** is not selected.</span></span>
13. <span data-ttu-id="26513-230">Hola **proyectos** lista, haga clic en **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="26513-230">In hello **Projects** list, click **ProductsPortal**.</span></span> <span data-ttu-id="26513-231">Asegúrese de que **ProductsServer** esté seleccionado.</span><span class="sxs-lookup"><span data-stu-id="26513-231">Ensure that **ProductsServer** is selected.</span></span>

    ![][26]

14. <span data-ttu-id="26513-232">Haga clic en **Aceptar** en hello **páginas de propiedades** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26513-232">Click **OK** in hello **Property Pages** dialog box.</span></span>

## <a name="run-hello-project-locally"></a><span data-ttu-id="26513-233">Ejecutar el proyecto de hello localmente</span><span class="sxs-lookup"><span data-stu-id="26513-233">Run hello project locally</span></span>

<span data-ttu-id="26513-234">aplicación de hello tootest localmente, en Visual Studio presione **F5**.</span><span class="sxs-lookup"><span data-stu-id="26513-234">tootest hello application locally, in Visual Studio press **F5**.</span></span> <span data-ttu-id="26513-235">servidor local de Hello (**ProductsServer**) debe iniciar primero, a continuación, Hola **ProductsPortal** debe iniciarse la aplicación en una ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="26513-235">hello on-premises server (**ProductsServer**) should start first, then hello **ProductsPortal** application should start in a browser window.</span></span> <span data-ttu-id="26513-236">Esta vez, verá que inventario de productos de hello enumera los datos recuperados del sistema de hello producto servicio local.</span><span class="sxs-lookup"><span data-stu-id="26513-236">This time, you will see that hello product inventory lists data retrieved from hello product service on-premises system.</span></span>

![][10]

<span data-ttu-id="26513-237">Presione **actualizar** en hello **ProductsPortal** página.</span><span class="sxs-lookup"><span data-stu-id="26513-237">Press **Refresh** on hello **ProductsPortal** page.</span></span> <span data-ttu-id="26513-238">Cada vez que se actualice la página de hello, verá la aplicación de servidor hello se muestra un mensaje cuando `GetProducts()` de **ProductsServer** se llama.</span><span class="sxs-lookup"><span data-stu-id="26513-238">Each time you refresh hello page, you'll see hello server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

<span data-ttu-id="26513-239">Cierre ambas aplicaciones antes del paso siguiente de toohello de continuar.</span><span class="sxs-lookup"><span data-stu-id="26513-239">Close both applications before proceeding toohello next step.</span></span>

## <a name="deploy-hello-productsportal-project-tooan-azure-web-app"></a><span data-ttu-id="26513-240">Implementar la aplicación web de Azure de hello ProductsPortal proyecto tooan</span><span class="sxs-lookup"><span data-stu-id="26513-240">Deploy hello ProductsPortal project tooan Azure web app</span></span>

<span data-ttu-id="26513-241">Hola siguiente paso es aplicación de Azure Web hello toorepublish **ProductsPortal** front-end.</span><span class="sxs-lookup"><span data-stu-id="26513-241">hello next step is toorepublish hello Azure Web app **ProductsPortal** frontend.</span></span> <span data-ttu-id="26513-242">Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="26513-242">Do hello following:</span></span>

1. <span data-ttu-id="26513-243">En el Explorador de soluciones, haga clic en hello **ProductsPortal** del proyecto y haga clic en **publicar**.</span><span class="sxs-lookup"><span data-stu-id="26513-243">In Solution Explorer, right-click hello **ProductsPortal** project, and click **Publish**.</span></span> <span data-ttu-id="26513-244">A continuación, haga clic en **publicar** en hello **publicar** página.</span><span class="sxs-lookup"><span data-stu-id="26513-244">Then, click **Publish** on hello **Publish** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="26513-245">Puede ver un mensaje de error en la ventana del explorador hello cuando hello **ProductsPortal** proyecto web se inicia automáticamente después de la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="26513-245">You may see an error message in hello browser window when hello **ProductsPortal** web project is automatically launched after hello deployment.</span></span> <span data-ttu-id="26513-246">Esto es normal y se produce porque hello **ProductsServer** aplicación no se está ejecutando todavía.</span><span class="sxs-lookup"><span data-stu-id="26513-246">This is expected, and occurs because hello **ProductsServer** application isn't running yet.</span></span>
>
>

2. <span data-ttu-id="26513-247">Copiar dirección URL de Hola de hello implementa la aplicación web, ya que será necesario URL hello en el paso siguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="26513-247">Copy hello URL of hello deployed web app, as you will need hello URL in hello next step.</span></span> <span data-ttu-id="26513-248">También puede obtener esta dirección URL de la ventana de actividad del servicio de aplicación de Azure de hello en Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="26513-248">You can also obtain this URL from hello Azure App Service Activity window in Visual Studio:</span></span>

  ![][9]

3. <span data-ttu-id="26513-249">Cierre Hola de toostop de ventana hello explorador ejecutando la aplicación.</span><span class="sxs-lookup"><span data-stu-id="26513-249">Close hello browser window toostop hello running application.</span></span>

### <a name="set-productsportal-as-web-app"></a><span data-ttu-id="26513-250">Establecimiento de ProductsPortal como aplicación web</span><span class="sxs-lookup"><span data-stu-id="26513-250">Set ProductsPortal as web app</span></span>

<span data-ttu-id="26513-251">Antes de la aplicación en ejecución hello en la nube de hello, debe asegurarse de que **ProductsPortal** se inicia desde dentro de Visual Studio como una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="26513-251">Before running hello application in hello cloud, you must ensure that **ProductsPortal** is launched from within Visual Studio as a web app.</span></span>

1. <span data-ttu-id="26513-252">En Visual Studio, haga clic en hello **ProductsPortal** del proyecto y, a continuación, haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="26513-252">In Visual Studio, right-click hello **ProductsPortal** project and then click **Properties**.</span></span>
2. <span data-ttu-id="26513-253">En la columna izquierda de hello, haga clic en **Web**.</span><span class="sxs-lookup"><span data-stu-id="26513-253">In hello left-hand column, click **Web**.</span></span>
3. <span data-ttu-id="26513-254">Hola **acción de inicio** sección, haga clic en hello **dirección URL de inicio** botón y, en el cuadro de texto hello escriba Hola URL para la aplicación web implementada anteriormente; por ejemplo, `http://productsportal1234567890.azurewebsites.net/`.</span><span class="sxs-lookup"><span data-stu-id="26513-254">In hello **Start Action** section, click hello **Start URL** button, and in hello text box enter hello URL for your previously deployed web app; for example, `http://productsportal1234567890.azurewebsites.net/`.</span></span>

    ![][27]

4. <span data-ttu-id="26513-255">De hello **archivo** menú en Visual Studio, haga clic en **guardar todo**.</span><span class="sxs-lookup"><span data-stu-id="26513-255">From hello **File** menu in Visual Studio, click **Save All**.</span></span>
5. <span data-ttu-id="26513-256">En el menú de compilación de hello en Visual Studio, haga clic en **volver a generar solución**.</span><span class="sxs-lookup"><span data-stu-id="26513-256">From hello Build menu in Visual Studio, click **Rebuild Solution**.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="26513-257">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="26513-257">Run hello application</span></span>

1. <span data-ttu-id="26513-258">Presione F5 toobuild y ejecute la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="26513-258">Press F5 toobuild and run hello application.</span></span> <span data-ttu-id="26513-259">servidor local de Hello (hello **ProductsServer** aplicación de consola) debe iniciar primero, a continuación, Hola **ProductsPortal** aplicación debe comenzar en una ventana del explorador, como se muestra en hello después de la pantalla captura.</span><span class="sxs-lookup"><span data-stu-id="26513-259">hello on-premises server (hello **ProductsServer** console application) should start first, then hello **ProductsPortal** application should start in a browser window, as shown in hello following screen shot.</span></span> <span data-ttu-id="26513-260">Tenga en cuenta nuevo ese inventario de productos de Hola enumera los datos recuperados del sistema de hello producto servicio local y muestra los datos en la aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="26513-260">Notice again that hello product inventory lists data retrieved from hello product service on-premises system, and displays that data in hello web app.</span></span> <span data-ttu-id="26513-261">Comprobar Hola URL toomake seguro de que **ProductsPortal** se ejecuta en la nube hello, como una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="26513-261">Check hello URL toomake sure that **ProductsPortal** is running in hello cloud, as an Azure web app.</span></span>

   ![][1]

   > [!IMPORTANT]
   > <span data-ttu-id="26513-262">Hola **ProductsServer** aplicación de consola debe estar en ejecución y puede tooserve Hola datos toohello **ProductsPortal** aplicación.</span><span class="sxs-lookup"><span data-stu-id="26513-262">hello **ProductsServer** console application must be running and able tooserve hello data toohello **ProductsPortal** application.</span></span> <span data-ttu-id="26513-263">Si el Explorador de hello muestra un error, espere unos segundos más **ProductsServer** tooload y Hola mostrar después de los mensajes.</span><span class="sxs-lookup"><span data-stu-id="26513-263">If hello browser displays an error, wait a few more seconds for **ProductsServer** tooload and display hello following message.</span></span> <span data-ttu-id="26513-264">A continuación, presione **actualizar** en el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="26513-264">Then press **Refresh** in hello browser.</span></span>
   >
   >

   ![][37]
2. <span data-ttu-id="26513-265">En el Explorador de hello, presione **actualizar** en hello **ProductsPortal** página.</span><span class="sxs-lookup"><span data-stu-id="26513-265">Back in hello browser, press **Refresh** on hello **ProductsPortal** page.</span></span> <span data-ttu-id="26513-266">Cada vez que se actualice la página de hello, verá la aplicación de servidor hello se muestra un mensaje cuando `GetProducts()` de **ProductsServer** se llama.</span><span class="sxs-lookup"><span data-stu-id="26513-266">Each time you refresh hello page, you'll see hello server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

    ![][38]

## <a name="next-steps"></a><span data-ttu-id="26513-267">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="26513-267">Next steps</span></span>

<span data-ttu-id="26513-268">toolearn más información acerca de la retransmisión de Azure, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="26513-268">toolearn more about Azure Relay, see hello following resources:</span></span>  

* [<span data-ttu-id="26513-269">¿Qué es Relay de Azure?</span><span class="sxs-lookup"><span data-stu-id="26513-269">What is Azure Relay?</span></span>](relay-what-is-it.md)  
* [<span data-ttu-id="26513-270">¿Cómo de retransmisión toouse</span><span class="sxs-lookup"><span data-stu-id="26513-270">How toouse Relay</span></span>](service-bus-dotnet-how-to-use-relay.md)  

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
