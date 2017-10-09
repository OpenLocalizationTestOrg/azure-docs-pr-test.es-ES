---
title: "aaaUse .NET Core en la aplicación Web en Linux | Documentos de Microsoft"
description: Use .NET Core en Web App en Linux.
keywords: "azure app service, aplic. web, dotnet, núcleo, linux, oss"
services: app-service
documentationCenter: 
authors: michimune, rachelappel
manager: erikre
editor: 
ms.assetid: c02959e6-7220-496a-a417-9b2147638e2e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: aelnably;wesmc;mikono;rachelap
ms.openlocfilehash: 9b7fb7185dff2c99ed88e7937d455177504937b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a><span data-ttu-id="6acc9-104">Uso de .NET Core en una instancia de Azure Web App en Linux</span><span class="sxs-lookup"><span data-stu-id="6acc9-104">Use .NET Core in an Azure web app on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="6acc9-105">[Aplicación Web](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) en Linux proporciona un servicio de hospedaje web muy escalables y aplicación de revisiones automáticamente con el sistema operativo de Linux de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acc9-105">[Web App](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) on Linux provides a highly scalable, self-patching web hosting service using hello Linux operating system.</span></span> <span data-ttu-id="6acc9-106">Este tutorial contiene instrucciones paso a paso que muestra cómo toocreate una [.NET Core](https://docs.microsoft.com/aspnet/core/) aplicación en la aplicación web de Azure en Linux.</span><span class="sxs-lookup"><span data-stu-id="6acc9-106">This tutorial contains step-by-step instructions showing how toocreate a [.NET Core](https://docs.microsoft.com/aspnet/core/) app on Azure web app on Linux.</span></span> 

![Aplicación web en Linux][10]

<span data-ttu-id="6acc9-108">Puede seguir pasos de hello siguientes a través de un equipo Mac, Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="6acc9-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6acc9-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6acc9-109">Prerequisites</span></span> ##

<span data-ttu-id="6acc9-110">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="6acc9-110">toocomplete this tutorial:</span></span> 

* <span data-ttu-id="6acc9-111">Instalar hello [.NET Core SDK](https://www.microsoft.com/net/download/core).</span><span class="sxs-lookup"><span data-stu-id="6acc9-111">Install hello [.NET Core SDK](https://www.microsoft.com/net/download/core).</span></span>
* <span data-ttu-id="6acc9-112">Instale [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="6acc9-112">Install [Git](https://git-scm.com/downloads).</span></span>

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a><span data-ttu-id="6acc9-113">Creación de una aplicación .NET Core local</span><span class="sxs-lookup"><span data-stu-id="6acc9-113">Create a local .NET Core application</span></span> ##

<span data-ttu-id="6acc9-114">Inicie una nueva sesión de terminal.</span><span class="sxs-lookup"><span data-stu-id="6acc9-114">Start a new terminal session.</span></span> <span data-ttu-id="6acc9-115">Cree un directorio denominado `hellodotnetcore`y cambiar hello tooit de directorio actual.</span><span class="sxs-lookup"><span data-stu-id="6acc9-115">Create a directory named `hellodotnetcore`, and change hello current directory tooit.</span></span> <span data-ttu-id="6acc9-116">A continuación, escriba lo siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="6acc9-116">Then type hello following:</span></span> 

```
dotnet new web
``` 

  <span data-ttu-id="6acc9-117">Este comando crea tres archivos (*hellodotnetcore.csproj*, *Program.cs*, y *Startup.cs*) y una carpeta vacía (*wwwroot /*) en el directorio actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acc9-117">This command creates three files (*hellodotnetcore.csproj*, *Program.cs*, and *Startup.cs*) and one empty folder (*wwwroot/*) under hello current directory.</span></span> <span data-ttu-id="6acc9-118">contenido de Hello `.csproj` archivo debe ser similar al siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="6acc9-118">hello content of `.csproj` file should look like hello following:</span></span> 

```xml
  <!-- Empty lines are omitted. -->

  <Project Sdk="Microsoft.NET.Sdk.Web">
        <PropertyGroup>
        <TargetFramework>netcoreapp1.1</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
        <Folder Include="wwwroot\" />
        </ItemGroup>
        <ItemGroup>
        <PackageReference Include="Microsoft.AspNetCore" Version="1.1.2" />
        </ItemGroup>
  </Project>
```

<span data-ttu-id="6acc9-119">Puesto que esta aplicación es una aplicación web, un tooan referencia paquete ASP.NET Core automáticamente fue agregado toohello *hellodotnetcore.csproj* archivo.</span><span class="sxs-lookup"><span data-stu-id="6acc9-119">Since this app is a web application, a reference tooan ASP.NET Core package was automatically added toohello *hellodotnetcore.csproj* file.</span></span> <span data-ttu-id="6acc9-120">número de versión de Hola de paquetes de saludo se establece según toohello elegido framework.</span><span class="sxs-lookup"><span data-stu-id="6acc9-120">hello version number of hello package is set according toohello chosen framework.</span></span> <span data-ttu-id="6acc9-121">Este ejemplo hace referencia a ASP.NET Core versión 1.1.2 porque se usa .NET Core 1.1.</span><span class="sxs-lookup"><span data-stu-id="6acc9-121">This example is referencing ASP.NET Core version 1.1.2 because .NET Core 1.1 is used.</span></span>

## <a name="build-and-test-hello-application-locally"></a><span data-ttu-id="6acc9-122">Compilar y probar la aplicación hello localmente</span><span class="sxs-lookup"><span data-stu-id="6acc9-122">Build and test hello application locally</span></span> ##

<span data-ttu-id="6acc9-123">Puede compilar y ejecutar la aplicación de .NET Core con hello `dotnet restore` comando seguido por hello `dotnet run` de comandos, como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="6acc9-123">You can build and run your .NET Core app with hello `dotnet restore` command followed by hello `dotnet run` command, as shown here:</span></span>

```
dotnet restore
dotnet run
```


<span data-ttu-id="6acc9-124">Cuando se inicia la aplicación hello, muestra un mensaje que indica la aplicación hello escucha las solicitudes de tooincoming en un puerto.</span><span class="sxs-lookup"><span data-stu-id="6acc9-124">When hello application starts, it displays a message indicating hello app is listening tooincoming requests at a port.</span></span> 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C tooshut down.
```

<span data-ttu-id="6acc9-125">Probar examinando demasiado`http://localhost:5000/` con el explorador.</span><span class="sxs-lookup"><span data-stu-id="6acc9-125">Test it by browsing too`http://localhost:5000/` with your browser.</span></span> <span data-ttu-id="6acc9-126">Si todo funciona correctamente, verá "Hello World!" (¡Hola mundo!)</span><span class="sxs-lookup"><span data-stu-id="6acc9-126">If everything works fine, you see "Hello World!"</span></span> <span data-ttu-id="6acc9-127">como texto de resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="6acc9-127">as hello result text.</span></span>

![Prueba con un explorador][7]

## <a name="create-a-net-core-app-in-hello-azure-portal"></a><span data-ttu-id="6acc9-129">Crear una aplicación de .NET Core en hello Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="6acc9-129">Create a .NET Core app in hello Azure Portal</span></span> ##

<span data-ttu-id="6acc9-130">En primer lugar debe toocreate una aplicación web vacía.</span><span class="sxs-lookup"><span data-stu-id="6acc9-130">First you need toocreate an empty web app.</span></span> <span data-ttu-id="6acc9-131">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/) y crear un nuevo [aplicación Web en Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="6acc9-131">Log in toohello [Azure portal](https://portal.azure.com/) and create a new [Web App on Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span></span>

![Creación de una aplicación web][1]

<span data-ttu-id="6acc9-133">Cuando Hola **crear** se abre la página, proporcione detalles acerca de la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="6acc9-133">When hello **Create** page opens, provide details about your web app:</span></span>

![Elección de una pila de tiempo de ejecución .NET Core][2]

<span data-ttu-id="6acc9-135">Use Hola siguiente tabla se como un toofill guía out hello **crear** página, a continuación, seleccione **Aceptar** y **crear** toocreate Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="6acc9-135">Use hello following table as a guide toofill out hello **Create** page, then select **OK** and **Create** toocreate hello app.</span></span>

| <span data-ttu-id="6acc9-136">Configuración</span><span class="sxs-lookup"><span data-stu-id="6acc9-136">Setting</span></span>      | <span data-ttu-id="6acc9-137">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="6acc9-137">Suggested value</span></span>  | <span data-ttu-id="6acc9-138">Descripción</span><span class="sxs-lookup"><span data-stu-id="6acc9-138">Description</span></span>                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| <span data-ttu-id="6acc9-139">Nombre de la aplicación</span><span class="sxs-lookup"><span data-stu-id="6acc9-139">App name</span></span> | <span data-ttu-id="6acc9-140">hellodotnetcore</span><span class="sxs-lookup"><span data-stu-id="6acc9-140">hellodotnetcore</span></span>  | <span data-ttu-id="6acc9-141">nombre de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6acc9-141">hello name of your app.</span></span> <span data-ttu-id="6acc9-142">Este nombre debe ser único.</span><span class="sxs-lookup"><span data-stu-id="6acc9-142">This name must be unique.</span></span> |
| <span data-ttu-id="6acc9-143">La suscripción</span><span class="sxs-lookup"><span data-stu-id="6acc9-143">Subscription</span></span> | <span data-ttu-id="6acc9-144">Elección de una suscripción actual</span><span class="sxs-lookup"><span data-stu-id="6acc9-144">Choose an existing subscription</span></span> | <span data-ttu-id="6acc9-145">Hola suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="6acc9-145">hello Azure subscription.</span></span> |
| <span data-ttu-id="6acc9-146">Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="6acc9-146">Resource Group</span></span> | <span data-ttu-id="6acc9-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6acc9-147">myResourceGroup</span></span> |  <span data-ttu-id="6acc9-148">Hola recursos de Azure grupo toocontain hello web app.</span><span class="sxs-lookup"><span data-stu-id="6acc9-148">hello Azure resource group toocontain hello web app.</span></span> |
| <span data-ttu-id="6acc9-149">Plan de servicio de aplicación</span><span class="sxs-lookup"><span data-stu-id="6acc9-149">App Service Plan</span></span> | <span data-ttu-id="6acc9-150">Nombre del plan de App Service existente</span><span class="sxs-lookup"><span data-stu-id="6acc9-150">Existing App Service Plan name</span></span> |  <span data-ttu-id="6acc9-151">Hola plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6acc9-151">hello App Service plan.</span></span>  |
| <span data-ttu-id="6acc9-152">Configuración del contenedor</span><span class="sxs-lookup"><span data-stu-id="6acc9-152">Configure Container</span></span> | <span data-ttu-id="6acc9-153">.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="6acc9-153">.NET Core 1.1</span></span> | <span data-ttu-id="6acc9-154">tipo de contenedor de esta aplicación web de Hola: registro integrado, Docker o Private.</span><span class="sxs-lookup"><span data-stu-id="6acc9-154">hello type of container for this web app: Built-in, Docker, or Private registry.</span></span> |
| <span data-ttu-id="6acc9-155">Origen de la imagen</span><span class="sxs-lookup"><span data-stu-id="6acc9-155">Image source</span></span>  | <span data-ttu-id="6acc9-156">Característica integrada</span><span class="sxs-lookup"><span data-stu-id="6acc9-156">Built-in</span></span>  |  <span data-ttu-id="6acc9-157">origen de Hola de imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acc9-157">hello source of hello image.</span></span> |
| <span data-ttu-id="6acc9-158">Pila de tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="6acc9-158">Runtime Stack</span></span>  | <span data-ttu-id="6acc9-159">.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="6acc9-159">.NET Core 1.1</span></span>  | <span data-ttu-id="6acc9-160">pila de tiempo de ejecución de Hola y versión.</span><span class="sxs-lookup"><span data-stu-id="6acc9-160">hello runtime stack and version.</span></span>  |

## <a name="deploy-your-application-via-git"></a><span data-ttu-id="6acc9-161">Implementación de la aplicación a través de Git</span><span class="sxs-lookup"><span data-stu-id="6acc9-161">Deploy your application via Git</span></span> ##

<span data-ttu-id="6acc9-162">Usar Git toodeploy Hola .NET Core aplicación tooAzure aplicación Web de servicio de aplicaciones en Linux.</span><span class="sxs-lookup"><span data-stu-id="6acc9-162">Use Git toodeploy hello .NET Core application tooAzure App Service Web App on Linux.</span></span>

<span data-ttu-id="6acc9-163">aplicación web de Azure nuevo de Hello ya tiene configurado de implementación de Git.</span><span class="sxs-lookup"><span data-stu-id="6acc9-163">hello new Azure web app already has Git deployment configured.</span></span> <span data-ttu-id="6acc9-164">Encontrará dirección URL de implementación de Git Hola desplazándose toohello siguiendo la dirección URL después de insertar el nombre de la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="6acc9-164">You will find hello Git deployment URL by navigating toohello following URL after inserting your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

<span data-ttu-id="6acc9-165">Hola dirección URL de Git tiene Hola siguiente formulario basado en el nombre de la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="6acc9-165">hello Git URL has hello following form based on your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

<span data-ttu-id="6acc9-166">Ejecute hello después de la aplicación de comandos toodeploy hello aplicación local tooyour web de Azure:</span><span class="sxs-lookup"><span data-stu-id="6acc9-166">Run hello following commands toodeploy hello local application tooyour Azure web app:</span></span> 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="6acc9-167">No es necesario toopush los archivos en *bin /* o *obj /* directorios dado que la aplicación se basa en la nube de Hola Hola cuando la aplicación los archivos de origen se insertan tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6acc9-167">You don't need toopush any files under *bin/* or *obj/* directories because your application is built in hello cloud when hello application's source files are pushed tooAzure.</span></span> <span data-ttu-id="6acc9-168">Una vez completado el proceso de compilación de hello, archivos binarios se copian en el directorio de la aplicación hello en */principal/sitio/wwwroot/*.</span><span class="sxs-lookup"><span data-stu-id="6acc9-168">After hello build process is complete, binary files are copied into hello application's directory at */home/site/wwwroot/*.</span></span>

<span data-ttu-id="6acc9-169">Confirme que las operaciones de implementación remota de hello informan correcto.</span><span class="sxs-lookup"><span data-stu-id="6acc9-169">Confirm that hello remote deployment operations report success.</span></span> <span data-ttu-id="6acc9-170">Las operaciones de inserción pueden tardar bastante tiempo desde la resolución de paquete y en la nube Hola de proceso de compilación.</span><span class="sxs-lookup"><span data-stu-id="6acc9-170">Push operations may take a while since package resolution and build process run in hello cloud.</span></span> <span data-ttu-id="6acc9-171">Verá varios mensajes de estado, y algunos indican que se han copiado los archivos.</span><span class="sxs-lookup"><span data-stu-id="6acc9-171">You will see several status messages, including ones stating that files have been copied.</span></span> <span data-ttu-id="6acc9-172">salida de Hello debería ser similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="6acc9-172">hello output should look similar toohello following:</span></span>

```bash
/* some output has been removed for brevity */
remote: Copying file: 'System.Net.Websockets.dll' 
remote: Copying file: 'System.Runtime.CompilerServices.Unsafe.dll' 
remote: Copying file: 'System.Runtime.Serialization.Primitives.dll' 
remote: Copying file: 'System.Text.Encodings.Web.dll' 
remote: Copying file: 'hellodotnetcore.deps.json' 
remote: Copying file: 'hellodotnetcore.dll' 
remote: Omitting next output lines...
remote: Finished successfully.
remote: Running post deployment commands...
remote: Deployment successful.
toohttps://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

<span data-ttu-id="6acc9-173">Cuando haya completado la implementación de hello, reinicie la aplicación web con efecto de hello implementación tootake.</span><span class="sxs-lookup"><span data-stu-id="6acc9-173">Once hello deployment has completed, restart your web app for hello deployment tootake effect.</span></span> <span data-ttu-id="6acc9-174">toodo, vaya toohello portal de Azure y navegue toohello **Introducción** página de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="6acc9-174">toodo this, go toohello Azure portal and navigate toohello **Overview** page of your web app.</span></span> <span data-ttu-id="6acc9-175">Seleccione hello **reiniciar** botón en la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="6acc9-175">Select hello **Restart** button in hello page.</span></span> <span data-ttu-id="6acc9-176">Cuando aparezca una ventana emergente, seleccione **Sí** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="6acc9-176">When a popup window shows up, select **Yes** tooconfirm.</span></span> <span data-ttu-id="6acc9-177">A continuación, puede examinar la aplicación web, como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="6acc9-177">You can then browse your web app, as shown here:</span></span>

![Exploración .NET Core implementado tooAzure servicio de aplicaciones en Linux][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="6acc9-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6acc9-179">Next steps</span></span>
* [<span data-ttu-id="6acc9-180">Preguntas más frecuentes sobre Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="6acc9-180">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
