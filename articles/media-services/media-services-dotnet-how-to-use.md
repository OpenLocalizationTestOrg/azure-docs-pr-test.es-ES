---
title: aaaHow tooSet equipo para el desarrollo de servicios multimedia con .NET
description: "Obtenga información sobre los requisitos previos de Hola para servicios multimedia con hello SDK de servicios multimedia para. NET. También aprenderá cómo toocreate una aplicación de Visual Studio."
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
ms.openlocfilehash: a5a2af3211d8156fd7dea99831fb769df4130d41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-development-with-net"></a><span data-ttu-id="0038c-104">Desarrollo de Servicios multimedia con .NET</span><span class="sxs-lookup"><span data-stu-id="0038c-104">Media Services development with .NET</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="0038c-105">Este tema describe cómo de servicios multimedia de desarrollo de toostart aplicaciones con. NET.</span><span class="sxs-lookup"><span data-stu-id="0038c-105">This topic discusses how toostart developing Media Services applications using .NET.</span></span>

<span data-ttu-id="0038c-106">Hola **Azure Media Services .NET SDK** biblioteca le permite tooprogram en servicios multimedia con. NET.</span><span class="sxs-lookup"><span data-stu-id="0038c-106">hello **Azure Media Services .NET SDK** library enables you tooprogram against Media Services using .NET.</span></span> <span data-ttu-id="0038c-107">toomake incluso más fácil toodevelop con. NET, hello **Azure Media Services .NET SDK Extensions** se proporciona la biblioteca.</span><span class="sxs-lookup"><span data-stu-id="0038c-107">toomake it even easier toodevelop with .NET, hello **Azure Media Services .NET SDK Extensions** library is provided.</span></span> <span data-ttu-id="0038c-108">Esta biblioteca contiene un conjunto de métodos de extensión y funciones auxiliares que simplifican el código de .NET.</span><span class="sxs-lookup"><span data-stu-id="0038c-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span></span> <span data-ttu-id="0038c-109">Las dos bibliotecas están disponibles a través de **NuGet** y **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="0038c-109">Both libraries are available through **NuGet** and **GitHub**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0038c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0038c-110">Prerequisites</span></span>
* <span data-ttu-id="0038c-111">Una cuenta de Servicios multimedia en una suscripción de Azure nueva o existente.</span><span class="sxs-lookup"><span data-stu-id="0038c-111">A Media Services account in a new or existing Azure subscription.</span></span> <span data-ttu-id="0038c-112">Vea el tema de hello [cómo tooCreate una cuenta de servicios multimedia](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="0038c-112">See hello topic [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="0038c-113">Sistemas operativos: Windows 10, Windows 7, Windows 2008 R2 o Windows 8.</span><span class="sxs-lookup"><span data-stu-id="0038c-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="0038c-114">.NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="0038c-114">.NET Framework 4.5.</span></span>
* <span data-ttu-id="0038c-115">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0038c-115">Visual Studio.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="0038c-116">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0038c-116">Create and configure a Visual Studio project</span></span>
<span data-ttu-id="0038c-117">Esta sección muestra cómo toocreate un proyecto en Visual Studio y configurarla para el desarrollo de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="0038c-117">This section shows you how toocreate a project in Visual Studio and set it up for Media Services development.</span></span>  <span data-ttu-id="0038c-118">En este caso, proyecto de hello es una aplicación de consola de Windows en C#, pero hello mismos pasos de configuración se muestra aquí aplican tooother tipos de proyectos que puede crear para las aplicaciones de servicios multimedia (por ejemplo, una aplicación de formularios Windows Forms o una aplicación Web ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="0038c-118">In this case, hello project is a C# Windows console application, but hello same setup steps shown here apply tooother types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span></span>

<span data-ttu-id="0038c-119">Esta sección se muestra cómo toouse **NuGet** tooadd Media Services .NET SDK extensions y otras bibliotecas dependientes.</span><span class="sxs-lookup"><span data-stu-id="0038c-119">This section shows how toouse **NuGet** tooadd Media Services .NET SDK extensions and other dependent libraries.</span></span>

<span data-ttu-id="0038c-120">Como alternativa, puede obtener los bits más recientes de SDK de .NET de servicios multimedia de Hola desde GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) o [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), compilar soluciones de Hola y Agregar proyecto de cliente de hello referencias toohello.</span><span class="sxs-lookup"><span data-stu-id="0038c-120">Alternatively, you can get hello latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build hello solution, and add hello references toohello client project.</span></span> <span data-ttu-id="0038c-121">Todas las dependencias necesarias de hello obtengan descargadas y extraídas automáticamente.</span><span class="sxs-lookup"><span data-stu-id="0038c-121">All hello necessary dependencies get downloaded and extracted automatically.</span></span>

1. <span data-ttu-id="0038c-122">Cree una aplicación de consola en C# mediante Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0038c-122">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="0038c-123">Escriba hello **nombre**, **ubicación**, y **nombre de la solución**y, a continuación, haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="0038c-123">Enter hello **Name**, **Location**, and **Solution name**, and then click OK.</span></span>
2. <span data-ttu-id="0038c-124">Compile la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="0038c-124">Build hello solution.</span></span>
3. <span data-ttu-id="0038c-125">Use **NuGet** tooinstall y agregue **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span><span class="sxs-lookup"><span data-stu-id="0038c-125">Use **NuGet** tooinstall and add **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span></span> <span data-ttu-id="0038c-126">Al instalar este paquete, también se instala el **SDK de Servicios multimedia para .NET** y agrega todas las demás dependencias necesarias.</span><span class="sxs-lookup"><span data-stu-id="0038c-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span></span>
   
    <span data-ttu-id="0038c-127">Asegúrese de que tiene la versión más reciente de Hola de NuGet instalada.</span><span class="sxs-lookup"><span data-stu-id="0038c-127">Ensure that you have hello newest version of NuGet installed.</span></span> <span data-ttu-id="0038c-128">Para más información e instrucciones de instalación, consulte [NuGet](http://nuget.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="0038c-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span></span>
4. <span data-ttu-id="0038c-129">En el Explorador de soluciones, haga clic en nombre de hello del proyecto de Hola y elija Administrar paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="0038c-129">In Solution Explorer, right-click hello name of hello project and choose Manage NuGet packages.</span></span>
   
    <span data-ttu-id="0038c-130">aparece el cuadro de diálogo Administrar paquetes de NuGet Hola.</span><span class="sxs-lookup"><span data-stu-id="0038c-130">hello Manage NuGet Packages dialog box appears.</span></span>
5. <span data-ttu-id="0038c-131">En la galería en línea de hello, busque las extensiones de MediaServices de Azure, elija Azure Media Services .NET SDK Extensions y, a continuación, haga clic en botón de instalar Hola.</span><span class="sxs-lookup"><span data-stu-id="0038c-131">In hello Online gallery, search for Azure MediaServices Extensions, choose Azure Media Services .NET SDK Extensions, and then click hello Install button.</span></span>
   
    <span data-ttu-id="0038c-132">proyecto de Hola se modifica y hace referencia a toohello Media Services .NET SDK Extensions, Media Services .NET SDK, y se agregan otros ensamblados dependientes.</span><span class="sxs-lookup"><span data-stu-id="0038c-132">hello project is modified and references toohello Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span></span>
6. <span data-ttu-id="0038c-133">toopromote un entorno de desarrollo más limpio, considere la posibilidad de habilitar la restauración de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="0038c-133">toopromote a cleaner development environment, consider enabling NuGet Package Restore.</span></span> <span data-ttu-id="0038c-134">Para obtener más información, consulte [Restauración de paquetes de NuGet](http://docs.nuget.org/consume/package-restore).</span><span class="sxs-lookup"><span data-stu-id="0038c-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span></span>
7. <span data-ttu-id="0038c-135">Agregue una referencia demasiado**System.Configuration** ensamblado.</span><span class="sxs-lookup"><span data-stu-id="0038c-135">Add a reference too**System.Configuration** assembly.</span></span> <span data-ttu-id="0038c-136">Este ensamblado contiene Hola System.Configuration. **ConfigurationManager** clase que es tooaccess usa archivos de configuración (por ejemplo, App.config).</span><span class="sxs-lookup"><span data-stu-id="0038c-136">This assembly contains hello System.Configuration.**ConfigurationManager** class that is used tooaccess configuration files (for example, App.config).</span></span>
   
    <span data-ttu-id="0038c-137">referencias de tooadd mediante el cuadro de diálogo de administrar referencias de hello, haga clic en el nombre del proyecto hello en el Explorador de soluciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="0038c-137">tooadd references using hello Manage References dialog, right-click hello project name in hello Solution Explorer.</span></span> <span data-ttu-id="0038c-138">A continuación, seleccione Agregar y Referencias.</span><span class="sxs-lookup"><span data-stu-id="0038c-138">Then, select Add and References.</span></span>
   
    <span data-ttu-id="0038c-139">aparece el cuadro de diálogo de administrar referencias de Hola.</span><span class="sxs-lookup"><span data-stu-id="0038c-139">hello Manage References dialog appears.</span></span>
8. <span data-ttu-id="0038c-140">En los ensamblados de .NET framework, buscar y seleccionar ensamblado System.Configuration de Hola y haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="0038c-140">Under .NET framework assemblies, find and select hello System.Configuration assembly and press OK.</span></span>
9. <span data-ttu-id="0038c-141">Abra el archivo App.config de hello y agregue un *appSettings* archivo toohello de sección.</span><span class="sxs-lookup"><span data-stu-id="0038c-141">Open hello App.config file and add an *appSettings* section toohello file.</span></span>     
   
    <span data-ttu-id="0038c-142">Establecer valores de hello que son necesarios tooconnect toohello API de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="0038c-142">Set hello values that are needed tooconnect toohello Media Services API.</span></span> <span data-ttu-id="0038c-143">Para obtener más información, consulte [Hola acceso API de servicios multimedia de Azure con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="0038c-143">For more information, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

    <span data-ttu-id="0038c-144">Si utilizas [autenticación de usuario](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) el archivo de configuración tendrá probablemente valores para el dominio del inquilino de Azure AD y Hola extremo de la API de REST de AMS.</span><span class="sxs-lookup"><span data-stu-id="0038c-144">If you are using [user authentication](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) your config file will probably have values for your Azure AD tenant domain and hello AMS REST API endpoint.</span></span>
    
    >[!Important]
    ><span data-ttu-id="0038c-145">La mayoría de ejemplos de código de hello documentación de servicios multimedia de Azure establecido, utilice un tipo de autenticación tooconnect toohello AMS API (interactiva) de usuario.</span><span class="sxs-lookup"><span data-stu-id="0038c-145">Most code samples in hello Azure Media Services documentation set, use a user (interactive) type of authentication tooconnect toohello AMS API.</span></span> <span data-ttu-id="0038c-146">Este método de autenticación funcionará bien para administrar o supervisar aplicaciones nativas: aplicaciones móviles, aplicaciones Windows y aplicaciones de consola.</span><span class="sxs-lookup"><span data-stu-id="0038c-146">This authentication method will work well for management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="0038c-147">Este método de autenticación no es adecuado para los tipos de aplicaciones de servidor, servicios web ni tipo de API.</span><span class="sxs-lookup"><span data-stu-id="0038c-147">This authentication method is not suitable for server, web services, APIs type of applications.</span></span>  <span data-ttu-id="0038c-148">Para obtener más información, consulte [Hola AMS API de acceso con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="0038c-148">For more information, see [Access hello AMS API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. <span data-ttu-id="0038c-149">Sobrescribir Hola existente **con** al principio de hello las instrucciones del archivo Program.cs de hello con hello siguiente código.</span><span class="sxs-lookup"><span data-stu-id="0038c-149">Overwrite hello existing **using** statements at hello beginning of hello Program.cs file with hello following code.</span></span>
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

<span data-ttu-id="0038c-150">En este punto, está listo toostart desarrollar una aplicación de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="0038c-150">At this point, you are ready toostart developing a Media Services application.</span></span>    

## <a name="example"></a><span data-ttu-id="0038c-151">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="0038c-151">Example</span></span>

<span data-ttu-id="0038c-152">Este es un pequeño ejemplo que se conecta toohello AMS API y enumera todos los procesadores de medios disponibles.</span><span class="sxs-lookup"><span data-stu-id="0038c-152">Here is a small example that connects toohello AMS API and lists all available Media Processors.</span></span>
    
    class Program
    {
        // Read values from hello App.config file.
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

##<a name="next-steps"></a><span data-ttu-id="0038c-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0038c-153">Next steps</span></span>

<span data-ttu-id="0038c-154">Ahora [puede conectarse toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md) e iniciar [desarrollar](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0038c-154">Now [you can connect toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md) and start [developing](media-services-dotnet-get-started.md).</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="0038c-155">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="0038c-155">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0038c-156">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="0038c-156">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

