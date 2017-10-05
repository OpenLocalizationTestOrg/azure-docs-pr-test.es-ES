---
title: "Configuración del equipo para el desarrollo de Servicios multimedia con .NET"
description: "Conozca los requisitos previos de Servicios multimedia usando el SDK de Servicios multimedia para .NET. Aprenda también a crear una aplicación de Visual Studio."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec2804c7-c656-4fbf-b3e4-3f0f78599a7f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: juliako
ms.openlocfilehash: 15828bc74937a036871b26493498232ec7cf6f06
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="media-services-development-with-net"></a><span data-ttu-id="4feee-104">Desarrollo de Servicios multimedia con .NET</span><span class="sxs-lookup"><span data-stu-id="4feee-104">Media Services development with .NET</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="4feee-105">En este tema se explica cómo empezar a desarrollar aplicaciones de Servicios multimedia con .NET.</span><span class="sxs-lookup"><span data-stu-id="4feee-105">This topic discusses how to start developing Media Services applications using .NET.</span></span>

<span data-ttu-id="4feee-106">La **biblioteca del SDK de Azure Media Services para .NET** le permite programar en los Media Services mediante. NET.</span><span class="sxs-lookup"><span data-stu-id="4feee-106">The **Azure Media Services .NET SDK** library enables you to program against Media Services using .NET.</span></span> <span data-ttu-id="4feee-107">Para que el desarrollo con .NET sea aún más fácil, se proporciona la biblioteca **Extensiones del SDK de Azure Media Services para .NET**.</span><span class="sxs-lookup"><span data-stu-id="4feee-107">To make it even easier to develop with .NET, the **Azure Media Services .NET SDK Extensions** library is provided.</span></span> <span data-ttu-id="4feee-108">Esta biblioteca contiene un conjunto de métodos de extensión y funciones auxiliares que simplifican el código de .NET.</span><span class="sxs-lookup"><span data-stu-id="4feee-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span></span> <span data-ttu-id="4feee-109">Las dos bibliotecas están disponibles a través de **NuGet** y **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="4feee-109">Both libraries are available through **NuGet** and **GitHub**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4feee-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4feee-110">Prerequisites</span></span>
* <span data-ttu-id="4feee-111">Una cuenta de Servicios multimedia en una suscripción de Azure nueva o existente.</span><span class="sxs-lookup"><span data-stu-id="4feee-111">A Media Services account in a new or existing Azure subscription.</span></span> <span data-ttu-id="4feee-112">Vea el tema [Cómo crear una cuenta de Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="4feee-112">See the topic [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="4feee-113">Sistemas operativos: Windows 10, Windows 7, Windows 2008 R2 o Windows 8.</span><span class="sxs-lookup"><span data-stu-id="4feee-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="4feee-114">.NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="4feee-114">.NET Framework 4.5.</span></span>
* <span data-ttu-id="4feee-115">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4feee-115">Visual Studio.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="4feee-116">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4feee-116">Create and configure a Visual Studio project</span></span>
<span data-ttu-id="4feee-117">En esta sección se muestra cómo crear un proyecto en Visual Studio y configurarlo para el desarrollo de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="4feee-117">This section shows you how to create a project in Visual Studio and set it up for Media Services development.</span></span>  <span data-ttu-id="4feee-118">En este caso, el proyecto es una aplicación de consola Windows de C#, pero los pasos de configuración que se muestran aquí se aplican a otros tipos de proyectos que puede crear para las aplicaciones de Media Services (por ejemplo, una aplicación de Windows Forms o una aplicación web ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="4feee-118">In this case, the project is a C# Windows console application, but the same setup steps shown here apply to other types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span></span>

<span data-ttu-id="4feee-119">En esta sección se muestra cómo usar **NuGet** para agregar las extensiones del SDK de .NET para Media Services y otras bibliotecas dependientes.</span><span class="sxs-lookup"><span data-stu-id="4feee-119">This section shows how to use **NuGet** to add Media Services .NET SDK extensions and other dependent libraries.</span></span>

<span data-ttu-id="4feee-120">También puede obtener los bits más recientes del SDK de Media Services para .NET en GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) o [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), compilar la solución y agregar las referencias al proyecto de cliente.</span><span class="sxs-lookup"><span data-stu-id="4feee-120">Alternatively, you can get the latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build the solution, and add the references to the client project.</span></span> <span data-ttu-id="4feee-121">Todas las dependencias necesarias se descargan y extraen automáticamente.</span><span class="sxs-lookup"><span data-stu-id="4feee-121">All the necessary dependencies get downloaded and extracted automatically.</span></span>

1. <span data-ttu-id="4feee-122">Cree una aplicación de consola en C# mediante Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4feee-122">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="4feee-123">Escriba el **Nombre**, la **Ubicación** y el **Nombre de la solución** y, a continuación, haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="4feee-123">Enter the **Name**, **Location**, and **Solution name**, and then click OK.</span></span>
2. <span data-ttu-id="4feee-124">Compile la solución.</span><span class="sxs-lookup"><span data-stu-id="4feee-124">Build the solution.</span></span>
3. <span data-ttu-id="4feee-125">Use **NuGet** para instalar y agregar **Extensiones del SDK de .NET para Azure Media Services** (**windowsazure.mediaservices.extensions**).</span><span class="sxs-lookup"><span data-stu-id="4feee-125">Use **NuGet** to install and add **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span></span> <span data-ttu-id="4feee-126">Al instalar este paquete, también se instala el **SDK de Servicios multimedia para .NET** y agrega todas las demás dependencias necesarias.</span><span class="sxs-lookup"><span data-stu-id="4feee-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span></span>
   
    <span data-ttu-id="4feee-127">Asegúrese de que tiene instalada la versión más reciente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="4feee-127">Ensure that you have the newest version of NuGet installed.</span></span> <span data-ttu-id="4feee-128">Para más información e instrucciones de instalación, consulte [NuGet](http://nuget.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="4feee-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span></span>
4. <span data-ttu-id="4feee-129">En el Explorador de soluciones, haga clic con el botón derecho en el nombre del proyecto y elija Administrar paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="4feee-129">In Solution Explorer, right-click the name of the project and choose Manage NuGet packages.</span></span>
   
    <span data-ttu-id="4feee-130">Aparecerá el cuadro de diálogo Administrar paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="4feee-130">The Manage NuGet Packages dialog box appears.</span></span>
5. <span data-ttu-id="4feee-131">En la galería en línea, busque Extensiones de Servicios multimedia de Azure, elija Extensiones del SDK de Servicios multimedia de Azure para .NET y luego haga clic en el botón Instalar.</span><span class="sxs-lookup"><span data-stu-id="4feee-131">In the Online gallery, search for Azure MediaServices Extensions, choose Azure Media Services .NET SDK Extensions, and then click the Install button.</span></span>
   
    <span data-ttu-id="4feee-132">El proyecto se modifica y se agregan referencias a Extensiones del SDK de Media Services para .NET, al SDK de .NET de Media Services y a otros ensamblados dependientes.</span><span class="sxs-lookup"><span data-stu-id="4feee-132">The project is modified and references to the Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span></span>
6. <span data-ttu-id="4feee-133">Para promover un entorno de desarrollo más limpio, considere la posibilidad de habilitar la restauración de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="4feee-133">To promote a cleaner development environment, consider enabling NuGet Package Restore.</span></span> <span data-ttu-id="4feee-134">Para obtener más información, consulte [Restauración de paquetes de NuGet](http://docs.nuget.org/consume/package-restore).</span><span class="sxs-lookup"><span data-stu-id="4feee-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span></span>
7. <span data-ttu-id="4feee-135">Agregue una referencia al ensamblado **System.Configuration** .</span><span class="sxs-lookup"><span data-stu-id="4feee-135">Add a reference to **System.Configuration** assembly.</span></span> <span data-ttu-id="4feee-136">Este ensamblado contiene la clase de Configuración del sistema.**Administrador de configuración** que se usa para tener acceso a los archivos de configuración (por ejemplo, App.config).</span><span class="sxs-lookup"><span data-stu-id="4feee-136">This assembly contains the System.Configuration.**ConfigurationManager** class that is used to access configuration files (for example, App.config).</span></span>
   
    <span data-ttu-id="4feee-137">Para agregar referencias usando el cuadro de diálogo de administración de referencias, haga clic con el botón derecho en el nombre del proyecto en el Explorador de soluciones.</span><span class="sxs-lookup"><span data-stu-id="4feee-137">To add references using the Manage References dialog, right-click the project name in the Solution Explorer.</span></span> <span data-ttu-id="4feee-138">A continuación, seleccione Agregar y Referencias.</span><span class="sxs-lookup"><span data-stu-id="4feee-138">Then, select Add and References.</span></span>
   
    <span data-ttu-id="4feee-139">Aparecerá el cuadro de diálogo Administrar referencias.</span><span class="sxs-lookup"><span data-stu-id="4feee-139">The Manage References dialog appears.</span></span>
8. <span data-ttu-id="4feee-140">En los ensamblados de .NET Framework, busque, seleccione el ensamblado System.Configuration y haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="4feee-140">Under .NET framework assemblies, find and select the System.Configuration assembly and press OK.</span></span>
9. <span data-ttu-id="4feee-141">Abra el archivo App.config y agregue una sección *appSettings* al archivo.</span><span class="sxs-lookup"><span data-stu-id="4feee-141">Open the App.config file and add an *appSettings* section to the file.</span></span>     
   
    <span data-ttu-id="4feee-142">Establezca los valores que se necesitan para conectarse a la API de Media Services.</span><span class="sxs-lookup"><span data-stu-id="4feee-142">Set the values that are needed to connect to the Media Services API.</span></span> <span data-ttu-id="4feee-143">Para más información, consulte [Acceso a Azure Media Services API con la autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="4feee-143">For more information, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

    <span data-ttu-id="4feee-144">Si usa la [autenticación de usuario](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication), el archivo de configuración probablemente tendrá valores para el dominio del inquilino de Azure AD y el punto de conexión de la API de REST de AMS.</span><span class="sxs-lookup"><span data-stu-id="4feee-144">If you are using [user authentication](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) your config file will probably have values for your Azure AD tenant domain and the AMS REST API endpoint.</span></span>
    
    >[!Important]
    ><span data-ttu-id="4feee-145">La mayoría de los ejemplos de código que aparecen en el conjunto de documentación de Azure Media Services usan un tipo de autenticación de usuario (interactivo) para conectarse a la API de AMS.</span><span class="sxs-lookup"><span data-stu-id="4feee-145">Most code samples in the Azure Media Services documentation set, use a user (interactive) type of authentication to connect to the AMS API.</span></span> <span data-ttu-id="4feee-146">Este método de autenticación funcionará bien para administrar o supervisar aplicaciones nativas: aplicaciones móviles, aplicaciones Windows y aplicaciones de consola.</span><span class="sxs-lookup"><span data-stu-id="4feee-146">This authentication method will work well for management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="4feee-147">Este método de autenticación no es adecuado para los tipos de aplicaciones de servidor, servicios web ni tipo de API.</span><span class="sxs-lookup"><span data-stu-id="4feee-147">This authentication method is not suitable for server, web services, APIs type of applications.</span></span>  <span data-ttu-id="4feee-148">Para más información, consulte [Acceso a Azure Media Services API con la autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="4feee-148">For more information, see [Access the AMS API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. <span data-ttu-id="4feee-149">Sobrescriba las instrucciones **using** existentes siguiendo las instrucciones al comienzo del archivo Program.cs con el siguiente código.</span><span class="sxs-lookup"><span data-stu-id="4feee-149">Overwrite the existing **using** statements at the beginning of the Program.cs file with the following code.</span></span>
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

<span data-ttu-id="4feee-150">En este punto, está listo para iniciar el desarrollo de una aplicación de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="4feee-150">At this point, you are ready to start developing a Media Services application.</span></span>    

## <a name="example"></a><span data-ttu-id="4feee-151">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="4feee-151">Example</span></span>

<span data-ttu-id="4feee-152">Este es un pequeño ejemplo en que se establece una conexión a la API de AMS y muestra todos los procesadores de multimedia disponibles.</span><span class="sxs-lookup"><span data-stu-id="4feee-152">Here is a small example that connects to the AMS API and lists all available Media Processors.</span></span>
    
    class Program
    {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
    
        private static CloudMediaContext _context = null;
        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
    
            // List all available Media Processors
            foreach (var mp in _context.MediaProcessors)
            {
                Console.WriteLine(mp.Name);
            }
    
        }

##<a name="next-steps"></a><span data-ttu-id="4feee-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4feee-153">Next steps</span></span>

<span data-ttu-id="4feee-154">Ahora [puede conectarse a la API de AMS](media-services-use-aad-auth-to-access-ams-api.md) y empezar a [desarrollar](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4feee-154">Now [you can connect to the AMS API](media-services-use-aad-auth-to-access-ams-api.md) and start [developing](media-services-dotnet-get-started.md).</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="4feee-155">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="4feee-155">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4feee-156">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="4feee-156">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

