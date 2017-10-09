---
title: aplicaciones de aaaDebugging en un contenedor de Docker local | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomodify una aplicación que se ejecuta en un contenedor de Docker local, actualizar el contenedor de Hola a través de la edición y la actualización y establecer puntos de interrupción de depuración"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/22/2016
ms.author: mlearned
ms.openlocfilehash: ff64e62fbb93901a29b5496bd5e17d2c4ea5ca99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-apps-in-a-local-docker-container"></a><span data-ttu-id="347fe-103">Depuración de aplicaciones en un contenedor de Docker local</span><span class="sxs-lookup"><span data-stu-id="347fe-103">Debugging apps in a local Docker container</span></span>
## <a name="overview"></a><span data-ttu-id="347fe-104">Información general</span><span class="sxs-lookup"><span data-stu-id="347fe-104">Overview</span></span>
<span data-ttu-id="347fe-105">Hola Visual Studio Tools para Docker proporciona un toodevelop de forma coherente en y validar la aplicación localmente en un contenedor Linux Docker.</span><span class="sxs-lookup"><span data-stu-id="347fe-105">hello Visual Studio Tools for Docker provides a consistent way toodevelop in and validate your application locally in a Linux Docker container.</span></span>
<span data-ttu-id="347fe-106">No tiene el contenedor de hello toorestart cada vez que realice un código de cambiar.</span><span class="sxs-lookup"><span data-stu-id="347fe-106">You don't have toorestart hello container each time you make a code change.</span></span>
<span data-ttu-id="347fe-107">Este artículo explica cómo toouse Hola "Editar y actualizar" característica toostart una aplicación Web de ASP.NET Core en un contenedor de Docker local, realice los cambios necesarios y, después, actualizar Hola explorador toosee esos cambios.</span><span class="sxs-lookup"><span data-stu-id="347fe-107">This article illustrates how toouse hello "Edit and Refresh" feature toostart an ASP.NET Core Web app in a local Docker container, make any necessary changes, and then refresh hello browser toosee those changes.</span></span>
<span data-ttu-id="347fe-108">Este artículo también muestra cómo tooset los puntos de interrupción para la depuración.</span><span class="sxs-lookup"><span data-stu-id="347fe-108">This article also shows you how tooset breakpoints for debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="347fe-109">La compatibilidad con el contenedor de Windows estará disponible en una versión futura</span><span class="sxs-lookup"><span data-stu-id="347fe-109">Windows Container support will be coming in a future release</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="347fe-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="347fe-110">Prerequisites</span></span>
<span data-ttu-id="347fe-111">Hola después herramientas debe estar instalado.</span><span class="sxs-lookup"><span data-stu-id="347fe-111">hello following tools must be installed.</span></span>

* [<span data-ttu-id="347fe-112">Versión más reciente de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="347fe-112">Latest version of Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="347fe-113">SDK de Microsoft ASP.NET Core 1.0</span><span class="sxs-lookup"><span data-stu-id="347fe-113">Microsoft ASP.NET Core 1.0 SDK</span></span>](https://go.microsoft.com/fwlink/?LinkID=809122)

<span data-ttu-id="347fe-114">toorun localmente contenedores de Docker, necesitará a un cliente local.</span><span class="sxs-lookup"><span data-stu-id="347fe-114">toorun Docker containers locally, you'll need a local docker client.</span></span>
<span data-ttu-id="347fe-115">Puede usar hello [cuadro de herramientas de Docker](https://www.docker.com/products/docker-toolbox), lo que requiere toobe de Hyper-V deshabilitado, o puede usar [Docker para Windows](https://www.docker.com/get-docker), que usa Hyper-V y requiere Windows 10.</span><span class="sxs-lookup"><span data-stu-id="347fe-115">You can use hello [Docker Toolbox](https://www.docker.com/products/docker-toolbox), which requires Hyper-V toobe disabled, or you can use [Docker for Windows](https://www.docker.com/get-docker), which uses Hyper-V, and requires Windows 10.</span></span>

<span data-ttu-id="347fe-116">Si usa el cuadro de herramientas de Docker, necesitará demasiado[configurar cliente hello](vs-azure-tools-docker-setup.md)</span><span class="sxs-lookup"><span data-stu-id="347fe-116">If using Docker Toolbox, you'll need too[configure hello Docker client](vs-azure-tools-docker-setup.md)</span></span>

## <a name="1-create-a-web-app"></a><span data-ttu-id="347fe-117">1. Creación de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="347fe-117">1. Create a web app</span></span>
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="347fe-118">2. Agregue compatibilidad con Docker</span><span class="sxs-lookup"><span data-stu-id="347fe-118">2. Add Docker support</span></span>
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a><span data-ttu-id="347fe-119">3. Edición del código y actualización</span><span class="sxs-lookup"><span data-stu-id="347fe-119">3. Edit your code and refresh</span></span>
<span data-ttu-id="347fe-120">tooquickly iterar cambios, puede iniciar la aplicación dentro de un contenedor y continuar toomake cambios, verlos como lo haría con IIS Express.</span><span class="sxs-lookup"><span data-stu-id="347fe-120">tooquickly iterate changes, you can start your application within a container, and continue toomake changes, viewing them as you would with IIS Express.</span></span>

1. <span data-ttu-id="347fe-121">Establecer configuración de soluciones de hello demasiado`Debug` y presione  **&lt;CTRL + F5 >** toobuild el docker de la imagen y lo ejecuta localmente.</span><span class="sxs-lookup"><span data-stu-id="347fe-121">Set hello Solution Configuration too`Debug` and press **&lt;CTRL + F5>** toobuild your docker image and run it locally.</span></span>

    <span data-ttu-id="347fe-122">Una vez que la imagen de contenedor de Hola se ha creado y se está ejecutando en un contenedor de Docker, Visual Studio iniciará la aplicación Web de hello en el explorador predeterminado.</span><span class="sxs-lookup"><span data-stu-id="347fe-122">Once hello container image has been built and is running in a Docker container, Visual Studio will launch hello Web app in your default browser.</span></span>
    <span data-ttu-id="347fe-123">Si está utilizando el Explorador de Microsoft Edge Hola o en caso contrario, tiene errores, vea [solución de problemas](vs-azure-tools-docker-troubleshooting-docker-errors.md) sección.</span><span class="sxs-lookup"><span data-stu-id="347fe-123">If you are using hello Microsoft Edge browser or otherwise have errors, see [Troubleshooting](vs-azure-tools-docker-troubleshooting-docker-errors.md) section.</span></span>
2. <span data-ttu-id="347fe-124">Vaya toohello acerca de la página, que es donde veremos toomake los cambios.</span><span class="sxs-lookup"><span data-stu-id="347fe-124">Go toohello About page, which is where we're going toomake our changes.</span></span>
3. <span data-ttu-id="347fe-125">Devolver tooVisual Studio y abra `Views\Home\About.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="347fe-125">Return tooVisual Studio and open `Views\Home\About.cshtml`.</span></span>
4. <span data-ttu-id="347fe-126">Agregar Hola siguiente HTML toohello contenido final de archivo hello y guardar los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="347fe-126">Add hello following HTML content toohello end of hello file and save hello changes.</span></span>

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. <span data-ttu-id="347fe-127">Ver la ventana de salida de hello, cuando se completa Hola compilación de .NET y ver las siguientes líneas, cambiar explorador tooyour atrás y actualizar Hola acerca de la página.</span><span class="sxs-lookup"><span data-stu-id="347fe-127">Viewing hello output window, when hello .NET build is completed and you see these lines, switch back tooyour browser and refresh hello About page.</span></span>

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C tooshut down
   ```
6. <span data-ttu-id="347fe-128">Se han aplicado los cambios.</span><span class="sxs-lookup"><span data-stu-id="347fe-128">Your changes have been applied!</span></span>

## <a name="4-debug-with-breakpoints"></a><span data-ttu-id="347fe-129">4. Depuración con puntos de interrupción</span><span class="sxs-lookup"><span data-stu-id="347fe-129">4. Debug with breakpoints</span></span>
<span data-ttu-id="347fe-130">A menudo, cambios deberán aún más la inspección, aprovechando Hola características de Visual Studio de depuración.</span><span class="sxs-lookup"><span data-stu-id="347fe-130">Often, changes will need further inspection, leveraging hello debugging features of Visual Studio.</span></span>

1. <span data-ttu-id="347fe-131">Devolver tooVisual Studio y abra`Controllers\HomeController.cs`</span><span class="sxs-lookup"><span data-stu-id="347fe-131">Return tooVisual Studio and open `Controllers\HomeController.cs`</span></span>
2. <span data-ttu-id="347fe-132">Reemplace el contenido de hello del método de hello About() con siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="347fe-132">Replace hello contents of hello About() method with hello following:</span></span>

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. <span data-ttu-id="347fe-133">Conjunto toohello de un punto de interrupción a la izquierda de hello `string message`... línea.</span><span class="sxs-lookup"><span data-stu-id="347fe-133">Set a breakpoint toohello left of hello `string message`... line.</span></span>
4. <span data-ttu-id="347fe-134">Aciertos  **&lt;F5 >** toostart depuración.</span><span class="sxs-lookup"><span data-stu-id="347fe-134">Hit **&lt;F5>** toostart debugging.</span></span>
5. <span data-ttu-id="347fe-135">Navegue toohello sobre toohit de página en el punto de interrupción.</span><span class="sxs-lookup"><span data-stu-id="347fe-135">Navigate toohello About page toohit your breakpoint.</span></span>
6. <span data-ttu-id="347fe-136">Conmutador tooVisual Studio tooview Hola punto de interrupción e inspeccionar Hola valor del mensaje.</span><span class="sxs-lookup"><span data-stu-id="347fe-136">Switch tooVisual Studio tooview hello breakpoint, and inspect hello value of message.</span></span>

   ![][2]

## <a name="summary"></a><span data-ttu-id="347fe-137">Resumen</span><span class="sxs-lookup"><span data-stu-id="347fe-137">Summary</span></span>
<span data-ttu-id="347fe-138">Con [Visual Studio 2015 Tools para Docker](https://aka.ms/DockerToolsForVS), puede obtener la productividad de Hola de trabajar de forma local, con realismo de producción de hello de desarrollo dentro de un contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="347fe-138">With [Visual Studio 2015 Tools for Docker](https://aka.ms/DockerToolsForVS), you can get hello productivity of working locally, with hello production realism of developing within a Docker container.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="347fe-139">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="347fe-139">Troubleshooting</span></span>
[<span data-ttu-id="347fe-140">Solución de problemas de desarrollo de Docker en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="347fe-140">Troubleshooting Visual Studio Docker Development</span></span>](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a><span data-ttu-id="347fe-141">Más información acerca de Docker con Visual Studio, Windows y Azure</span><span class="sxs-lookup"><span data-stu-id="347fe-141">More about Docker with Visual Studio, Windows, and Azure</span></span>
* <span data-ttu-id="347fe-142">[Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) : desarrollo de código de .NET Core en un contenedor</span><span class="sxs-lookup"><span data-stu-id="347fe-142">[Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) - Developing your .NET Core code in a container</span></span>
* <span data-ttu-id="347fe-143">[Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) : compilación e implementación de contenedores de Docker</span><span class="sxs-lookup"><span data-stu-id="347fe-143">[Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) - Build and Deploy docker containers</span></span>
* <span data-ttu-id="347fe-144">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) : servicios de lenguaje para editar archivos de Docker, a los que próximamente se incorporarán más escenarios de E2E</span><span class="sxs-lookup"><span data-stu-id="347fe-144">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) - Language services for editing docker files, with more e2e scenarios coming</span></span>
* <span data-ttu-id="347fe-145">[Documentación acerca de los contenedores de Windows](http://aka.ms/containers): información de Windows Server y Nano Server</span><span class="sxs-lookup"><span data-stu-id="347fe-145">[Windows Container Information](http://aka.ms/containers)- Windows Server and Nano Server information</span></span>
* <span data-ttu-id="347fe-146">[Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Contenido de Azure Container Service](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="347fe-146">[Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service Content](http://aka.ms/AzureContainerService)</span></span>
* <span data-ttu-id="347fe-147">Para obtener más ejemplos del uso de Docker, consulte [trabajar con Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) de hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) conectar 2015 [demostración](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="347fe-147">For more examples of working with Docker, see [Working with Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) from hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span> <span data-ttu-id="347fe-148">Encontrará tutoriales más rápidos de demostración de hello HealthClinic.biz, [tutoriales de herramientas de desarrollador de Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="347fe-148">For more quickstarts from hello HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>

## <a name="various-docker-tools"></a><span data-ttu-id="347fe-149">Varias herramientas de Docker</span><span class="sxs-lookup"><span data-stu-id="347fe-149">Various Docker tools</span></span>
<span data-ttu-id="347fe-150">[Some great docker tools (Steve Lasker's blog) (Herramientas excelentes de Docker [blog de Steve])](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)</span><span class="sxs-lookup"><span data-stu-id="347fe-150">[Some great docker tools (Steve Lasker's blog)](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)</span></span>

## <a name="good-articles"></a><span data-ttu-id="347fe-151">Buenos artículos</span><span class="sxs-lookup"><span data-stu-id="347fe-151">Good articles</span></span>
[<span data-ttu-id="347fe-152">Introducción tooMicroservices desde NGINX</span><span class="sxs-lookup"><span data-stu-id="347fe-152">Introduction tooMicroservices from NGINX</span></span>](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a><span data-ttu-id="347fe-153">Presentaciones</span><span class="sxs-lookup"><span data-stu-id="347fe-153">Presentations</span></span>
* [<span data-ttu-id="347fe-154">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e</span><span class="sxs-lookup"><span data-stu-id="347fe-154">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e</span></span>](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [<span data-ttu-id="347fe-155">Introducción tooASP.NET Core @ compilación 2016 - donde se en demostración</span><span class="sxs-lookup"><span data-stu-id="347fe-155">Introduction tooASP.NET Core @ build 2016 - Where You At Demo</span></span>](https://channel9.msdn.com/Events/Build/2016/B810)
* [<span data-ttu-id="347fe-156">Developing .NET apps in containers, Channel 9 (Desarrollo de aplicaciones .NET en contenedores, Channel 9)</span><span class="sxs-lookup"><span data-stu-id="347fe-156">Developing .NET apps in containers, Channel 9</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
