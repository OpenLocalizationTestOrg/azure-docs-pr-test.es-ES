---
title: "Aplicación híbrida en la nube/local (.NET) de Azure WCF Relay | Microsoft Docs"
description: "Aprenda a crear una aplicación híbrida en la nube o local de .NET con la retransmisión de WCF de Azure."
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
ms.openlocfilehash: 366922a083b9d18ef50e04eb8b459d2725315e1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a><span data-ttu-id="673ef-103">Aplicación híbrida en la nube o local de .NET con la retransmisión de WCF de Azure</span><span class="sxs-lookup"><span data-stu-id="673ef-103">.NET on-premises/cloud hybrid application using Azure WCF Relay</span></span>
## <a name="introduction"></a><span data-ttu-id="673ef-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="673ef-104">Introduction</span></span>

<span data-ttu-id="673ef-105">En este artículo se muestra cómo compilar una aplicación de nube híbrida con Microsoft Azure y Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="673ef-105">This article shows how to build a hybrid cloud application with Microsoft Azure and Visual Studio.</span></span> <span data-ttu-id="673ef-106">Se supone que no tiene ninguna experiencia previa con Azure.</span><span class="sxs-lookup"><span data-stu-id="673ef-106">The tutorial assumes you have no prior experience using Azure.</span></span> <span data-ttu-id="673ef-107">En menos de 30 minutos, dispondrá de una aplicación que utiliza varios recursos de Azure funcionando en la nube.</span><span class="sxs-lookup"><span data-stu-id="673ef-107">In less than 30 minutes, you will have an application that uses multiple Azure resources up and running in the cloud.</span></span>

<span data-ttu-id="673ef-108">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="673ef-108">You will learn:</span></span>

* <span data-ttu-id="673ef-109">Crear o adaptar un servicio web existente para su consumo por una solución web.</span><span class="sxs-lookup"><span data-stu-id="673ef-109">How to create or adapt an existing web service for consumption by a web solution.</span></span>
* <span data-ttu-id="673ef-110">Utilizar la retransmisión de WCF de Azure Service Bus para compartir datos entre una aplicación de Azure y un servicio web hospedado en otra parte.</span><span class="sxs-lookup"><span data-stu-id="673ef-110">How to use the Azure WCF Relay service to share data between an Azure application and a web service hosted elsewhere.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a><span data-ttu-id="673ef-111">Cómo ayuda Relay de Azure con soluciones híbridas</span><span class="sxs-lookup"><span data-stu-id="673ef-111">How Azure Relay helps with hybrid solutions</span></span>

<span data-ttu-id="673ef-112">Las soluciones de negocio por lo general están compuestas por una combinación de código personalizado escrito para afrontar los nuevos y exclusivos requisitos empresariales, así como la funcionalidad existente proporcionada por soluciones y sistemas que ya están instalados.</span><span class="sxs-lookup"><span data-stu-id="673ef-112">Business solutions are typically composed of a combination of custom code written to tackle new and unique business requirements and existing functionality provided by solutions and systems that are already in place.</span></span>

<span data-ttu-id="673ef-113">Los arquitectos de soluciones están comenzando a utilizar la nube para abordar con más facilidad los requisitos de escala y reducir los costes operativos.</span><span class="sxs-lookup"><span data-stu-id="673ef-113">Solution architects are starting to use the cloud for easier handling of scale requirements and lower operational costs.</span></span> <span data-ttu-id="673ef-114">De esta manera, se dan cuenta de que los activos de servicio existentes que les gustaría aprovechar como base de sus soluciones se encuentran dentro del firewall corporativo y no resulta sencillo para la solución en la nube el acceso a ellos.</span><span class="sxs-lookup"><span data-stu-id="673ef-114">In doing so, they find that existing service assets they'd like to leverage as building blocks for their solutions are inside the corporate firewall and out of easy reach for access by the cloud solution.</span></span> <span data-ttu-id="673ef-115">Muchos de los servicios internos no están construidos ni hospedados de una forma que se puedan exponer fácilmente en los servidores perimetrales de la red corporativa.</span><span class="sxs-lookup"><span data-stu-id="673ef-115">Many internal services are not built or hosted in a way that they can be easily exposed at the corporate network edge.</span></span>

<span data-ttu-id="673ef-116">[Azure Relay](https://azure.microsoft.com/services/service-bus/) está diseñada para el caso de uso en que se toman los servicios web de Windows Communication Foundation (WCF) existentes y se permite el acceso seguro a los mismos a las soluciones que residen fuera del perímetro corporativo, sin necesidad de realizar cambios molestos en la infraestructura de la red corporativa.</span><span class="sxs-lookup"><span data-stu-id="673ef-116">[Azure Relay](https://azure.microsoft.com/services/service-bus/) is designed for the use-case of taking existing Windows Communication Foundation (WCF) web services and making those services securely accessible to solutions that reside outside the corporate perimeter without requiring intrusive changes to the corporate network infrastructure.</span></span> <span data-ttu-id="673ef-117">Dichos servicios de retransmisión aún se hospedan en el entorno existente, pero delegan la escucha de sesiones y solicitudes de entrada en el servicio de relé hospedado en la nube.</span><span class="sxs-lookup"><span data-stu-id="673ef-117">Such relay services are still hosted inside their existing environment, but they delegate listening for incoming sessions and requests to the cloud-hosted relay service.</span></span> <span data-ttu-id="673ef-118">Azure Relay también protege dichos servicios del acceso no autorizado mediante el uso de la autenticación de [Firma de acceso compartido (SAS)](../service-bus-messaging/service-bus-sas.md).</span><span class="sxs-lookup"><span data-stu-id="673ef-118">Azure Relay also protects those services from unauthorized access by using [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) authentication.</span></span>

## <a name="solution-scenario"></a><span data-ttu-id="673ef-119">Escenario de la solución</span><span class="sxs-lookup"><span data-stu-id="673ef-119">Solution scenario</span></span>
<span data-ttu-id="673ef-120">En este tutorial, creará un sitio web de ASP.NET que le permitirá ver una lista de productos en la página del inventario de productos.</span><span class="sxs-lookup"><span data-stu-id="673ef-120">In this tutorial, you will create an ASP.NET website that enables you to see a list of products on the product inventory page.</span></span>

![][0]

<span data-ttu-id="673ef-121">En este tutorial se asume que la información de los productos se encuentra en un sistema local y se usa Relay de Azure para obtener acceso a dicho sistema.</span><span class="sxs-lookup"><span data-stu-id="673ef-121">The tutorial assumes that you have product information in an existing on-premises system, and uses Azure Relay to reach into that system.</span></span> <span data-ttu-id="673ef-122">Esto lo simula un servicio web que se ejecuta en una aplicación de consola simple y el respaldo lo proporciona un conjunto de productos en memoria.</span><span class="sxs-lookup"><span data-stu-id="673ef-122">This is simulated by a web service that runs in a simple console application and is backed by an in-memory set of products.</span></span> <span data-ttu-id="673ef-123">Dicha aplicación de consola se puede ejecutar en el equipo propio y el rol web se puede implementar en Azure.</span><span class="sxs-lookup"><span data-stu-id="673ef-123">You will be able to run this console application on your own computer and deploy the web role into Azure.</span></span> <span data-ttu-id="673ef-124">Al hacerlo, observará que el rol web que se ejecuta en el centro de datos de Azure llamará a su equipo, aunque casi seguro que este residirá al menos detrás de un firewall y una capa de traducción de direcciones de red (NAT).</span><span class="sxs-lookup"><span data-stu-id="673ef-124">By doing so, you will see how the web role running in the Azure datacenter will indeed call into your computer, even though your computer will almost certainly reside behind at least one firewall and a network address translation (NAT) layer.</span></span>

## <a name="set-up-the-development-environment"></a><span data-ttu-id="673ef-125">Configuración del entorno de desarrollo</span><span class="sxs-lookup"><span data-stu-id="673ef-125">Set up the development environment</span></span>

<span data-ttu-id="673ef-126">Antes de comenzar a desarrollar aplicaciones de Azure, obtenga las herramientas y configure el entorno de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="673ef-126">Before you can begin developing Azure applications, download the tools and set up your development environment:</span></span>

1. <span data-ttu-id="673ef-127">Instale el SDK de Azure para .NET desde la [página de descargas](https://azure.microsoft.com/downloads/) del SDK.</span><span class="sxs-lookup"><span data-stu-id="673ef-127">Install the Azure SDK for .NET from the SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="673ef-128">En la columna **.NET**, haga clic en la versión de [Visual Studio](http://www.visualstudio.com) que está usando.</span><span class="sxs-lookup"><span data-stu-id="673ef-128">In the **.NET** column, click the version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="673ef-129">Los pasos de este tutorial utilizan Visual Studio 2015, pero también funcionan con Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="673ef-129">The steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="673ef-130">Cuando se le solicite ejecutar o guardar el programa de instalación, haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="673ef-130">When prompted to run or save the installer, click **Run**.</span></span>
4. <span data-ttu-id="673ef-131">En el **instalador de plataforma web**, haga clic en **Instalar** y continúe con la instalación.</span><span class="sxs-lookup"><span data-stu-id="673ef-131">In the **Web Platform Installer**, click **Install** and proceed with the installation.</span></span>
5. <span data-ttu-id="673ef-132">Cuando la instalación se complete, dispondrá de todo lo necesario para iniciar el desarrollo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="673ef-132">Once the installation is complete, you will have everything necessary to start to develop the app.</span></span> <span data-ttu-id="673ef-133">El SDK incluye las herramientas que le permiten desarrollar fácilmente aplicaciones Azure en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="673ef-133">The SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="673ef-134">Creación de un espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="673ef-134">Create a namespace</span></span>

<span data-ttu-id="673ef-135">Para comenzar a usar las características de Relay en Azure, primero debe crear un espacio de nombres de servicio.</span><span class="sxs-lookup"><span data-stu-id="673ef-135">To begin using the relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="673ef-136">Un espacio de nombres proporciona un contenedor con un ámbito para el desvío de recursos de Azure en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="673ef-136">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="673ef-137">Siga las [instrucciones a continuación](relay-create-namespace-portal.md) para crear un espacio de nombres de Relay.</span><span class="sxs-lookup"><span data-stu-id="673ef-137">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="create-an-on-premises-server"></a><span data-ttu-id="673ef-138">Creación de un servidor local</span><span class="sxs-lookup"><span data-stu-id="673ef-138">Create an on-premises server</span></span>

<span data-ttu-id="673ef-139">En primer lugar, cree un sistema de catálogo de productos local (ficticio).</span><span class="sxs-lookup"><span data-stu-id="673ef-139">First, you will build a (mock) on-premises product catalog system.</span></span> <span data-ttu-id="673ef-140">Será bastante simple; puede considerar que representa un sistema de catálogo de productos local real con una superficie de servicio completa que se intenta integrar.</span><span class="sxs-lookup"><span data-stu-id="673ef-140">It will be fairly simple; you can see this as representing an actual on-premises product catalog system with a complete service surface that we're trying to integrate.</span></span>

<span data-ttu-id="673ef-141">Este proyecto es una aplicación de consola de Visual Studio y emplea el [paquete NuGet de Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) para incluir las bibliotecas y los valores de configuración de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="673ef-141">This project is a Visual Studio console application, and uses the [Azure Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) to include the Service Bus libraries and configuration settings.</span></span>

### <a name="create-the-project"></a><span data-ttu-id="673ef-142">Creación del proyecto</span><span class="sxs-lookup"><span data-stu-id="673ef-142">Create the project</span></span>

1. <span data-ttu-id="673ef-143">Inicie Microsoft Visual Studio con privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="673ef-143">Using administrator privileges, start Microsoft Visual Studio.</span></span> <span data-ttu-id="673ef-144">Para hacerlo, haga clic con el botón derecho en el icono del programa Visual Studio y, luego, haga clic en **Ejecutar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="673ef-144">To do so, right-click the Visual Studio program icon, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="673ef-145">En Visual Studio, en el menú **Archivo**, haga clic en **Nuevo** y, a continuación, en **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="673ef-145">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="673ef-146">En **Plantillas instaladas**, en **Visual C#**, haga clic en **Aplicación de consola (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="673ef-146">From **Installed Templates**, under **Visual C#**, click **Console App (.NET Framework)**.</span></span> <span data-ttu-id="673ef-147">En el cuadro **Nombre**, escriba el nombre **ProductsServer**:</span><span class="sxs-lookup"><span data-stu-id="673ef-147">In the **Name** box, type the name **ProductsServer**:</span></span>

   ![][11]
4. <span data-ttu-id="673ef-148">Haga clic en **Aceptar** para crear el proyecto **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="673ef-148">Click **OK** to create the **ProductsServer** project.</span></span>
5. <span data-ttu-id="673ef-149">Si ya ha instalado el administrador del paquete NuGet para Visual Studio, vaya al paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="673ef-149">If you have already installed the NuGet package manager for Visual Studio, skip to the next step.</span></span> <span data-ttu-id="673ef-150">De lo contrario, visite [NuGet][NuGet] y haga clic en [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) (Instalar NuGet).</span><span class="sxs-lookup"><span data-stu-id="673ef-150">Otherwise, visit [NuGet][NuGet] and click [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span></span> <span data-ttu-id="673ef-151">Siga las indicaciones para instalar el administrador del paquete NuGet y, a continuación, reinicie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="673ef-151">Follow the prompts to install the NuGet package manager, then re-start Visual Studio.</span></span>
6. <span data-ttu-id="673ef-152">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **ProductsServer** y luego haga clic en **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="673ef-152">In Solution Explorer, right-click the **ProductsServer** project, then click **Manage NuGet Packages**.</span></span>
7. <span data-ttu-id="673ef-153">Haga clic en la pestaña **Examinar** y luego busque `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="673ef-153">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="673ef-154">Seleccione el paquete **WindowsAzure.ServiceBus**.</span><span class="sxs-lookup"><span data-stu-id="673ef-154">Select the **WindowsAzure.ServiceBus** package.</span></span>
8. <span data-ttu-id="673ef-155">Haga clic en **Instalar**y acepte las condiciones de uso.</span><span class="sxs-lookup"><span data-stu-id="673ef-155">Click **Install**, and accept the terms of use.</span></span>

   ![][13]

   <span data-ttu-id="673ef-156">Tenga en cuenta que ahora se hace referencia a los ensamblados del cliente requeridos.</span><span class="sxs-lookup"><span data-stu-id="673ef-156">Note that the required client assemblies are now referenced.</span></span>
8. <span data-ttu-id="673ef-157">Agregue una clase nueva para el contrato de su producto.</span><span class="sxs-lookup"><span data-stu-id="673ef-157">Add a new class for your product contract.</span></span> <span data-ttu-id="673ef-158">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **ProductsServer**, a continuación en **Agregar** y, por último, en **Clase**.</span><span class="sxs-lookup"><span data-stu-id="673ef-158">In Solution Explorer, right-click the **ProductsServer** project and click **Add**, and then click **Class**.</span></span>
9. <span data-ttu-id="673ef-159">En el cuadro **Name**, escriba el nombre **ProductsContract.cs**.</span><span class="sxs-lookup"><span data-stu-id="673ef-159">In the **Name** box, type the name **ProductsContract.cs**.</span></span> <span data-ttu-id="673ef-160">A continuación, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="673ef-160">Then click **Add**.</span></span>
10. <span data-ttu-id="673ef-161">En **ProductsContract.cs**, sustituya la definición del espacio de nombres por el siguiente código, que define el contrato del servicio.</span><span class="sxs-lookup"><span data-stu-id="673ef-161">In **ProductsContract.cs**, replace the namespace definition with the following code, which defines the contract for the service.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define the data contract for the service
        [DataContract]
        // Declare the serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define the service contract.
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
11. <span data-ttu-id="673ef-162">En Program.cs, sustituya la definición del espacio de nombres por el siguiente código, que agrega el servicio de perfil y su host:</span><span class="sxs-lookup"><span data-stu-id="673ef-162">In Program.cs, replace the namespace definition with the following code, which adds the profile service and the host for it.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement the IProducts interface.
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

            // Display a message in the service console application
            // when the list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define the Main() function in the service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER to close");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. <span data-ttu-id="673ef-163">En el Explorador de soluciones, haga doble clic en el archivo **App.config** para abrirlo en el editor de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="673ef-163">In Solution Explorer, double-click the **App.config** file to open it in the Visual Studio editor.</span></span> <span data-ttu-id="673ef-164">En la parte inferior del elemento `<system.ServiceModel>` (pero aún dentro de `<system.ServiceModel>`), agregue el siguiente código XML.</span><span class="sxs-lookup"><span data-stu-id="673ef-164">At the bottom of the `<system.ServiceModel>` element (but still within `<system.ServiceModel>`), add the following XML code.</span></span> <span data-ttu-id="673ef-165">Asegúrese de reemplazar *yourServiceNamespace* por el nombre de su espacio de nombres y *yourKey* por la clave SAS que recuperó anteriormente en el portal:</span><span class="sxs-lookup"><span data-stu-id="673ef-165">Be sure to replace *yourServiceNamespace* with the name of your namespace, and *yourKey* with the SAS key you retrieved earlier from the portal:</span></span>

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
13. <span data-ttu-id="673ef-166">Aún en App.config, en el elemento `<appSettings>`, reemplace el valor de la cadena de conexión por la cadena de conexión que obtuvo antes en el portal.</span><span class="sxs-lookup"><span data-stu-id="673ef-166">Still in App.config, in the `<appSettings>` element, replace the connection string value with the connection string you previously obtained from the portal.</span></span>

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. <span data-ttu-id="673ef-167">Presione **Ctrl+Mayús+B**, o bien, en el menú **Compilar**, haga clic en **Compilar solución** para compilar la aplicación y comprobar la exactitud del trabajo hasta el momento.</span><span class="sxs-lookup"><span data-stu-id="673ef-167">Press **Ctrl+Shift+B** or from the **Build** menu, click **Build Solution** to build the application and verify the accuracy of your work so far.</span></span>

## <a name="create-an-aspnet-application"></a><span data-ttu-id="673ef-168">Creación de una aplicación ASP.NET</span><span class="sxs-lookup"><span data-stu-id="673ef-168">Create an ASP.NET application</span></span>

<span data-ttu-id="673ef-169">En esta sección se creará una aplicación ASP.NET simple que mostrará los datos recuperados del servicio de producto.</span><span class="sxs-lookup"><span data-stu-id="673ef-169">In this section you will build a simple ASP.NET application that displays data retrieved from your product service.</span></span>

### <a name="create-the-project"></a><span data-ttu-id="673ef-170">Creación del proyecto</span><span class="sxs-lookup"><span data-stu-id="673ef-170">Create the project</span></span>

1. <span data-ttu-id="673ef-171">Asegúrese de que se está ejecutando Visual Studio con privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="673ef-171">Ensure that Visual Studio is running with administrator privileges.</span></span>
2. <span data-ttu-id="673ef-172">En Visual Studio, en el menú **Archivo**, haga clic en **Nuevo** y, a continuación, en **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="673ef-172">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="673ef-173">En **Plantillas instaladas**, en **Visual C#**, haga clic en **Aplicación web ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="673ef-173">From **Installed Templates**, under **Visual C#**, click **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="673ef-174">Asigne al proyecto el nombre **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="673ef-174">Name the project **ProductsPortal**.</span></span> <span data-ttu-id="673ef-175">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="673ef-175">Then click **OK**.</span></span>

   ![][15]

4. <span data-ttu-id="673ef-176">En la lista de **plantillas ASP.NET** del cuadro de diálogo **Nueva aplicación web ASP.NET**, haga clic en **MVC**.</span><span class="sxs-lookup"><span data-stu-id="673ef-176">From the **ASP.NET Templates** list in the **New ASP.NET Web Application** dialog, click **MVC**.</span></span>

   ![][16]

6. <span data-ttu-id="673ef-177">Haga clic en el botón **Cambiar autenticación**.</span><span class="sxs-lookup"><span data-stu-id="673ef-177">Click the **Change Authentication** button.</span></span> <span data-ttu-id="673ef-178">En el cuadro de diálogo **Cambiar autenticación**, asegúrese de que esté seleccionada la opción **Sin autenticación** y luego haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="673ef-178">In the **Change Authentication** dialog box, ensure that **No Authentication** is selected, and then click **OK**.</span></span> <span data-ttu-id="673ef-179">En este tutorial, va a implementar una aplicación que no necesita un inicio de sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="673ef-179">For this tutorial, you're deploying an app that does not need a user login.</span></span>

    ![][18]

7. <span data-ttu-id="673ef-180">De vuelta en el cuadro de diálogo **Nueva aplicación web ASP.NET**, haga clic en **Aceptar** para crear la aplicación de MVC.</span><span class="sxs-lookup"><span data-stu-id="673ef-180">Back in the **New ASP.NET Web Application** dialog, click **OK** to create the MVC app.</span></span>
8. <span data-ttu-id="673ef-181">Ahora debe configurar recursos de Azure para una aplicación web nueva.</span><span class="sxs-lookup"><span data-stu-id="673ef-181">Now you must configure Azure resources for a new web app.</span></span> <span data-ttu-id="673ef-182">Siga los pasos de la [sección Publicación en Azure de este artículo](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="673ef-182">Follow the steps in the [Publish to Azure section of this article](../app-service-web/app-service-web-get-started-dotnet.md).</span></span> <span data-ttu-id="673ef-183">A continuación, vuelva a este tutorial y continúe con el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="673ef-183">Then, return to this tutorial and proceed to the next step.</span></span>
10. <span data-ttu-id="673ef-184">En el Explorador de soluciones, haga clic con el botón derecho en **Modelos** y, luego, en **Agregar** y, por último, en **Clase**.</span><span class="sxs-lookup"><span data-stu-id="673ef-184">In Solution Explorer, right-click **Models** and then click **Add**, then click **Class**.</span></span> <span data-ttu-id="673ef-185">En el cuadro **Name**, escriba el nombre **Product.cs**.</span><span class="sxs-lookup"><span data-stu-id="673ef-185">In the **Name** box, type the name **Product.cs**.</span></span> <span data-ttu-id="673ef-186">A continuación, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="673ef-186">Then click **Add**.</span></span>

    ![][17]

### <a name="modify-the-web-application"></a><span data-ttu-id="673ef-187">Modificación de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="673ef-187">Modify the web application</span></span>

1. <span data-ttu-id="673ef-188">En el archivo Product.cs en Visual Studio, sustituya la definición del espacio de nombres existente por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="673ef-188">In the Product.cs file in Visual Studio, replace the existing namespace definition with the following code.</span></span>

   ```csharp
    // Declare properties for the products inventory.
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
2. <span data-ttu-id="673ef-189">En el Explorador de soluciones, expanda la carpeta **Controladores** y luego haga doble clic en el archivo **HomeController.cs** para abrirlo en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="673ef-189">In Solution Explorer, expand the **Controllers** folder, then double-click the **HomeController.cs** file to open it in Visual Studio.</span></span>
3. <span data-ttu-id="673ef-190">En el archivo **HomeController.cs**, sustituya la definición de espacio de nombres existente por el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="673ef-190">In **HomeController.cs**, replace the existing namespace definition with the following code.</span></span>

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of the products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. <span data-ttu-id="673ef-191">En el Explorador de soluciones, expanda la carpeta Views\Shared y luego haga doble clic en **_Layout.cshtml** para abrirlo en el Editor de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="673ef-191">In Solution Explorer, expand the Views\Shared folder, then double-click **_Layout.cshtml** to open it in the Visual Studio editor.</span></span>
5. <span data-ttu-id="673ef-192">Cambie todas las ocurrencias de **My ASP.NET Application** por **Productos de LITWARE**.</span><span class="sxs-lookup"><span data-stu-id="673ef-192">Change all occurrences of **My ASP.NET Application** to **LITWARE's Products**.</span></span>
6. <span data-ttu-id="673ef-193">Quite los vínculos **Página principal**, **Acerca de** y **Contacto**.</span><span class="sxs-lookup"><span data-stu-id="673ef-193">Remove the **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="673ef-194">En el siguiente ejemplo, elimine el código resaltado.</span><span class="sxs-lookup"><span data-stu-id="673ef-194">In the following example, delete the highlighted code.</span></span>

    ![][41]

7. <span data-ttu-id="673ef-195">En el Explorador de soluciones, expanda la carpeta Views\Home y luego haga doble clic en **Index.cshtml** para abrirlo en el Editor de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="673ef-195">In Solution Explorer, expand the Views\Home folder, then double-click **Index.cshtml** to open it in the Visual Studio editor.</span></span> <span data-ttu-id="673ef-196">Reemplace todo el contenido del archivo con el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="673ef-196">Replace the entire contents of the file with the following code.</span></span>

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
8. <span data-ttu-id="673ef-197">Para comprobar la precisión del trabajo realizado hasta el momento, puede presionar **Ctrl+Mayús+B** para compilar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="673ef-197">To verify the accuracy of your work so far, you can press **Ctrl+Shift+B** to build the project.</span></span>

### <a name="run-the-app-locally"></a><span data-ttu-id="673ef-198">Ejecución de la aplicación de forma local</span><span class="sxs-lookup"><span data-stu-id="673ef-198">Run the app locally</span></span>

<span data-ttu-id="673ef-199">Ejecute la aplicación para comprobar que funciona.</span><span class="sxs-lookup"><span data-stu-id="673ef-199">Run the application to verify that it works.</span></span>

1. <span data-ttu-id="673ef-200">Asegúrese de que **ProductsPortal** es el proyecto activo.</span><span class="sxs-lookup"><span data-stu-id="673ef-200">Ensure that **ProductsPortal** is the active project.</span></span> <span data-ttu-id="673ef-201">Haga clic con el botón derecho en el nombre del proyecto en el Explorador de soluciones y seleccione **Establecer como proyecto de inicio**.</span><span class="sxs-lookup"><span data-stu-id="673ef-201">Right-click the project name in Solution Explorer and select **Set As Startup Project**.</span></span>
2. <span data-ttu-id="673ef-202">En Visual Studio, presione **F5**.</span><span class="sxs-lookup"><span data-stu-id="673ef-202">In Visual Studio, press **F5**.</span></span>
3. <span data-ttu-id="673ef-203">La aplicación debería aparecer ejecutándose en un explorador.</span><span class="sxs-lookup"><span data-stu-id="673ef-203">Your application should appear, running in a browser.</span></span>

   ![][21]

## <a name="put-the-pieces-together"></a><span data-ttu-id="673ef-204">Combinación de todos los componentes</span><span class="sxs-lookup"><span data-stu-id="673ef-204">Put the pieces together</span></span>

<span data-ttu-id="673ef-205">El siguiente paso es conectar el servidor de productos local con la aplicación ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="673ef-205">The next step is to hook up the on-premises products server with the ASP.NET application.</span></span>

1. <span data-ttu-id="673ef-206">Si no está abierto, vuelva a abrir en Visual Studio el proyecto **ProductsPortal** que ha creado en la sección [Creación de una aplicación ASP.NET](#create-an-aspnet-application).</span><span class="sxs-lookup"><span data-stu-id="673ef-206">If it is not already open, in Visual Studio re-open the **ProductsPortal** project you created in the [Create an ASP.NET application](#create-an-aspnet-application) section.</span></span>
2. <span data-ttu-id="673ef-207">Agregue el paquete NuGet a las referencias del proyecto de forma similar al paso de la sección "Creación de un servidor local".</span><span class="sxs-lookup"><span data-stu-id="673ef-207">Similar to the step in the "Create an On-Premises Server" section, add the NuGet package to the project references.</span></span> <span data-ttu-id="673ef-208">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **ProductsPortal** y luego haga clic en **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="673ef-208">In Solution Explorer, right-click the **ProductsPortal** project, then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="673ef-209">Busque "Service Bus" y seleccione el elemento **WindowsAzure.ServiceBus**.</span><span class="sxs-lookup"><span data-stu-id="673ef-209">Search for "Service Bus" and select the **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="673ef-210">Después finalice la instalación y cierre este cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="673ef-210">Then complete the installation and close this dialog box.</span></span>
4. <span data-ttu-id="673ef-211">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **ProductsPortal** y, a continuación, haga clic en **Agregar** y, finalmente, en **Elemento existente**.</span><span class="sxs-lookup"><span data-stu-id="673ef-211">In Solution Explorer, right-click the **ProductsPortal** project, then click **Add**, then **Existing Item**.</span></span>
5. <span data-ttu-id="673ef-212">Desplácese al archivo **ProductsContract.cs** desde el proyecto de consola **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="673ef-212">Navigate to the **ProductsContract.cs** file from the **ProductsServer** console project.</span></span> <span data-ttu-id="673ef-213">Haga clic para resaltar ProductsContract.cs.</span><span class="sxs-lookup"><span data-stu-id="673ef-213">Click to highlight ProductsContract.cs.</span></span> <span data-ttu-id="673ef-214">Haga clic en la flecha abajo situada junto a **Agregar** y, a continuación, haga clic en **Agregar como vínculo**.</span><span class="sxs-lookup"><span data-stu-id="673ef-214">Click the down arrow next to **Add**, then click **Add as Link**.</span></span>

   ![][24]

6. <span data-ttu-id="673ef-215">Ahora abra el archivo **HomeController.cs** en el editor de Visual Studio y sustituya la definición del espacio de nombres por el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="673ef-215">Now open the **HomeController.cs** file in the Visual Studio editor and replace the namespace definition with the following code.</span></span> <span data-ttu-id="673ef-216">Asegúrese de reemplazar *yourServiceNamespace* por el nombre de su espacio de nombres de servicio y *yourKey* por su clave de SAS.</span><span class="sxs-lookup"><span data-stu-id="673ef-216">Be sure to replace *yourServiceNamespace* with the name of your service namespace, and *yourKey* with your SAS key.</span></span> <span data-ttu-id="673ef-217">Esto permitirá que el cliente llame al servicio local y que se devuelva el resultado de la llamada.</span><span class="sxs-lookup"><span data-stu-id="673ef-217">This will enable the client to call the on-premises service, returning the result of the call.</span></span>

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
           // Declare the channel factory.
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
                   // Return a view of the products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. <span data-ttu-id="673ef-218">En el Explorador de soluciones, haga clic con el botón derecho en la solución **ProductsPortal** (asegúrese de que hace clic en la solución, no en el proyecto).</span><span class="sxs-lookup"><span data-stu-id="673ef-218">In Solution Explorer, right-click the **ProductsPortal** solution (make sure to right-click the solution, not the project).</span></span> <span data-ttu-id="673ef-219">Haga clic en **Agregar** y, a continuación, en **Proyecto existente**.</span><span class="sxs-lookup"><span data-stu-id="673ef-219">Click **Add**, then click **Existing Project**.</span></span>
8. <span data-ttu-id="673ef-220">Desplácese al proyecto **ProductsServer** y haga doble clic en la solución **ProductsServer.csproj** para agregarla.</span><span class="sxs-lookup"><span data-stu-id="673ef-220">Navigate to the **ProductsServer** project, then double-click the **ProductsServer.csproj** solution file to add it.</span></span>
9. <span data-ttu-id="673ef-221">**ProductsServer** debe estar en ejecución para mostrar los datos en **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="673ef-221">**ProductsServer** must be running in order to display the data on **ProductsPortal**.</span></span> <span data-ttu-id="673ef-222">En el Explorador de soluciones, haga clic con el botón derecho en la solución **ProductsPortal** y, a continuación, haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="673ef-222">In Solution Explorer, right-click the **ProductsPortal** solution and click **Properties**.</span></span> <span data-ttu-id="673ef-223">Se muestra el cuadro de diálogo **Páginas de propiedades**.</span><span class="sxs-lookup"><span data-stu-id="673ef-223">The **Property Pages** dialog box is displayed.</span></span>
10. <span data-ttu-id="673ef-224">A la izquierda, haga clic en **Proyecto de inicio**.</span><span class="sxs-lookup"><span data-stu-id="673ef-224">On the left side, click **Startup Project**.</span></span> <span data-ttu-id="673ef-225">A la derecha, haga clic en **Proyectos de inicio múltiples**.</span><span class="sxs-lookup"><span data-stu-id="673ef-225">On the right side, click **Multiple startup projects**.</span></span> <span data-ttu-id="673ef-226">Asegúrese de que aparezcan **ProductsServer** y **ProductsPortal** en ese orden y que la acción **Iniciar** esté establecida para ambos.</span><span class="sxs-lookup"><span data-stu-id="673ef-226">Ensure that **ProductsServer** and **ProductsPortal** appear, in that order, with **Start** set as the action for both.</span></span>

      ![][25]

11. <span data-ttu-id="673ef-227">Aún en el cuadro de diálogo **Propiedades**, haga clic en **Dependencias del proyecto** a la izquierda.</span><span class="sxs-lookup"><span data-stu-id="673ef-227">Still in the **Properties** dialog box, click **Project Dependencies** on the left side.</span></span>
12. <span data-ttu-id="673ef-228">En la lista **Proyectos**, haga clic en **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="673ef-228">In the **Projects** list, click **ProductsServer**.</span></span> <span data-ttu-id="673ef-229">Asegúrese de que la opción **ProductsPortal** no esté seleccionada.</span><span class="sxs-lookup"><span data-stu-id="673ef-229">Ensure that **ProductsPortal** is not selected.</span></span>
13. <span data-ttu-id="673ef-230">En la lista **Proyectos**, haga clic en **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="673ef-230">In the **Projects** list, click **ProductsPortal**.</span></span> <span data-ttu-id="673ef-231">Asegúrese de que **ProductsServer** esté seleccionado.</span><span class="sxs-lookup"><span data-stu-id="673ef-231">Ensure that **ProductsServer** is selected.</span></span>

    ![][26]

14. <span data-ttu-id="673ef-232">En el cuadro de diálogo **Páginas de propiedades**, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="673ef-232">Click **OK** in the **Property Pages** dialog box.</span></span>

## <a name="run-the-project-locally"></a><span data-ttu-id="673ef-233">Ejecución del proyecto de forma local</span><span class="sxs-lookup"><span data-stu-id="673ef-233">Run the project locally</span></span>

<span data-ttu-id="673ef-234">Para probar la aplicación localmente, en Visual Studio, presione **F5**.</span><span class="sxs-lookup"><span data-stu-id="673ef-234">To test the application locally, in Visual Studio press **F5**.</span></span> <span data-ttu-id="673ef-235">El servidor local (**ProductsServer**) se debe iniciar primero y luego la aplicación **ProductsPortal** se debe iniciar en una ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="673ef-235">The on-premises server (**ProductsServer**) should start first, then the **ProductsPortal** application should start in a browser window.</span></span> <span data-ttu-id="673ef-236">Esta vez verá que el inventario de productos muestra los datos recuperados del sistema local del servicio de productos.</span><span class="sxs-lookup"><span data-stu-id="673ef-236">This time, you will see that the product inventory lists data retrieved from the product service on-premises system.</span></span>

![][10]

<span data-ttu-id="673ef-237">Presione **Actualizar** en la página **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="673ef-237">Press **Refresh** on the **ProductsPortal** page.</span></span> <span data-ttu-id="673ef-238">Cada vez que actualice la página, verá que la aplicación de servidor muestra un mensaje cuando se llama a `GetProducts()` desde **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="673ef-238">Each time you refresh the page, you'll see the server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

<span data-ttu-id="673ef-239">Cierre ambas aplicaciones antes de continuar con el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="673ef-239">Close both applications before proceeding to the next step.</span></span>

## <a name="deploy-the-productsportal-project-to-an-azure-web-app"></a><span data-ttu-id="673ef-240">Implementación del proyecto ProductsPortal en una aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="673ef-240">Deploy the ProductsPortal project to an Azure web app</span></span>

<span data-ttu-id="673ef-241">El siguiente paso consiste en volver a publicar el front-end **ProductsPortal** de la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="673ef-241">The next step is to republish the Azure Web app **ProductsPortal** frontend.</span></span> <span data-ttu-id="673ef-242">Haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="673ef-242">Do the following:</span></span>

1. <span data-ttu-id="673ef-243">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **ProductsPortal** y haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="673ef-243">In Solution Explorer, right-click the **ProductsPortal** project, and click **Publish**.</span></span> <span data-ttu-id="673ef-244">A continuación, haga clic en **Publicar** en la página **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="673ef-244">Then, click **Publish** on the **Publish** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="673ef-245">Puede que vea un mensaje de error en la ventana del explorador cuando el proyecto web **ProductsPortal** se inicie automáticamente después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="673ef-245">You may see an error message in the browser window when the **ProductsPortal** web project is automatically launched after the deployment.</span></span> <span data-ttu-id="673ef-246">Esto es normal y se produce porque la aplicación **ProductsServer** no se está ejecutando todavía.</span><span class="sxs-lookup"><span data-stu-id="673ef-246">This is expected, and occurs because the **ProductsServer** application isn't running yet.</span></span>
>
>

2. <span data-ttu-id="673ef-247">Copie la dirección URL de la aplicación web implementada, la necesitará en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="673ef-247">Copy the URL of the deployed web app, as you will need the URL in the next step.</span></span> <span data-ttu-id="673ef-248">También puede obtener esta dirección URL de la ventana de actividad del Servicio de aplicaciones de Azure en Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="673ef-248">You can also obtain this URL from the Azure App Service Activity window in Visual Studio:</span></span>

  ![][9]

3. <span data-ttu-id="673ef-249">Cierre la ventana del explorador para detener la aplicación en ejecución.</span><span class="sxs-lookup"><span data-stu-id="673ef-249">Close the browser window to stop the running application.</span></span>

### <a name="set-productsportal-as-web-app"></a><span data-ttu-id="673ef-250">Establecimiento de ProductsPortal como aplicación web</span><span class="sxs-lookup"><span data-stu-id="673ef-250">Set ProductsPortal as web app</span></span>

<span data-ttu-id="673ef-251">Antes de ejecutar la aplicación en la nube, debe asegurarse de que **ProductsPortal** se inicie desde dentro de Visual Studio como una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="673ef-251">Before running the application in the cloud, you must ensure that **ProductsPortal** is launched from within Visual Studio as a web app.</span></span>

1. <span data-ttu-id="673ef-252">En Visual Studio, haga clic con el botón derecho en el proyecto **ProductsPortal** y luego haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="673ef-252">In Visual Studio, right-click the **ProductsPortal** project and then click **Properties**.</span></span>
2. <span data-ttu-id="673ef-253">En la columna izquierda, haga clic en **Web**.</span><span class="sxs-lookup"><span data-stu-id="673ef-253">In the left-hand column, click **Web**.</span></span>
3. <span data-ttu-id="673ef-254">En la sección **Acción de inicio**, haga clic en el botón **Dirección URL de inicio** y, en el cuadro de texto, escriba la dirección URL de la aplicación web anteriormente implementada, por ejemplo `http://productsportal1234567890.azurewebsites.net/`.</span><span class="sxs-lookup"><span data-stu-id="673ef-254">In the **Start Action** section, click the **Start URL** button, and in the text box enter the URL for your previously deployed web app; for example, `http://productsportal1234567890.azurewebsites.net/`.</span></span>

    ![][27]

4. <span data-ttu-id="673ef-255">En el menú **Archivo** de Visual Studio, haga clic en **Guardar todo**.</span><span class="sxs-lookup"><span data-stu-id="673ef-255">From the **File** menu in Visual Studio, click **Save All**.</span></span>
5. <span data-ttu-id="673ef-256">En el menú Compilar de Visual Studio, haga clic en **Recompilar solución**.</span><span class="sxs-lookup"><span data-stu-id="673ef-256">From the Build menu in Visual Studio, click **Rebuild Solution**.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="673ef-257">Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="673ef-257">Run the application</span></span>

1. <span data-ttu-id="673ef-258">Presione F5 para compilar y ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="673ef-258">Press F5 to build and run the application.</span></span> <span data-ttu-id="673ef-259">Primero debe iniciarse el servidor local (la aplicación de consola **ProductsServer**) y luego la aplicación **ProductsPortal** en una ventana de explorador, tal como se muestra en la captura de pantalla siguiente.</span><span class="sxs-lookup"><span data-stu-id="673ef-259">The on-premises server (the **ProductsServer** console application) should start first, then the **ProductsPortal** application should start in a browser window, as shown in the following screen shot.</span></span> <span data-ttu-id="673ef-260">Observe de nuevo que el inventario de productos muestra los datos recuperados del sistema local del servicio de productos y muestra esos datos en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="673ef-260">Notice again that the product inventory lists data retrieved from the product service on-premises system, and displays that data in the web app.</span></span> <span data-ttu-id="673ef-261">Compruebe la dirección URL para asegurarse de que **ProductsPortal** se ejecuta en la nube como una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="673ef-261">Check the URL to make sure that **ProductsPortal** is running in the cloud, as an Azure web app.</span></span>

   ![][1]

   > [!IMPORTANT]
   > <span data-ttu-id="673ef-262">La aplicación de consola **ProductsServer** se debe estar ejecutando y debe poder suministrar los datos a la aplicación **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="673ef-262">The **ProductsServer** console application must be running and able to serve the data to the **ProductsPortal** application.</span></span> <span data-ttu-id="673ef-263">Si el explorador muestra un error, espere unos segundos a que **ProductsServer** se cargue y muestre el siguiente mensaje.</span><span class="sxs-lookup"><span data-stu-id="673ef-263">If the browser displays an error, wait a few more seconds for **ProductsServer** to load and display the following message.</span></span> <span data-ttu-id="673ef-264">A continuación, presione **Actualizar** en el explorador.</span><span class="sxs-lookup"><span data-stu-id="673ef-264">Then press **Refresh** in the browser.</span></span>
   >
   >

   ![][37]
2. <span data-ttu-id="673ef-265">En el explorador, presione **Actualizar** en la página **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="673ef-265">Back in the browser, press **Refresh** on the **ProductsPortal** page.</span></span> <span data-ttu-id="673ef-266">Cada vez que actualice la página, verá que la aplicación de servidor muestra un mensaje cuando se llama a `GetProducts()` desde **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="673ef-266">Each time you refresh the page, you'll see the server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

    ![][38]

## <a name="next-steps"></a><span data-ttu-id="673ef-267">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="673ef-267">Next steps</span></span>

<span data-ttu-id="673ef-268">Para más información sobre Relay de Azure, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="673ef-268">To learn more about Azure Relay, see the following resources:</span></span>  

* [<span data-ttu-id="673ef-269">¿Qué es Relay de Azure?</span><span class="sxs-lookup"><span data-stu-id="673ef-269">What is Azure Relay?</span></span>](relay-what-is-it.md)  
* [<span data-ttu-id="673ef-270">Uso de Relay</span><span class="sxs-lookup"><span data-stu-id="673ef-270">How to use Relay</span></span>](service-bus-dotnet-how-to-use-relay.md)  

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
