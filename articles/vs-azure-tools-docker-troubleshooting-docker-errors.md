---
title: los errores de cliente de Docker de aaaTroubleshooting en Windows con Visual Studio | Documentos de Microsoft
description: Solucionar problemas que producirse al usar Visual Studio toocreate e implementar tooDocker de aplicaciones web en Windows con Visual Studio.
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 346f70b9-7b52-4688-a8e8-8f53869618d3
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 7421ae8e044d58fc412d748fb870da4c9b2fdb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-visual-studio-docker-development"></a><span data-ttu-id="7cf61-103">Solución de problemas de desarrollo de Docker en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7cf61-103">Troubleshoot Visual Studio Docker development</span></span>

<span data-ttu-id="7cf61-104">Cuando se trabaja con Visual Studio Tools para la vista previa de Docker, puede encontrar algunos problemas debido a la naturaleza de Hola de vista previa de Hola.</span><span class="sxs-lookup"><span data-stu-id="7cf61-104">When you're working with Visual Studio Tools for Docker Preview, you may encounter some problems because of hello nature of hello preview.</span></span>
<span data-ttu-id="7cf61-105">Estos son algunos problemas frecuentes y sus soluciones.</span><span class="sxs-lookup"><span data-stu-id="7cf61-105">Following are some common issues and resolutions.</span></span>  

## <a name="visual-studio-2017-rc"></a><span data-ttu-id="7cf61-106">Visual Studio 2017 RC</span><span class="sxs-lookup"><span data-stu-id="7cf61-106">Visual Studio 2017 RC</span></span>

### <a name="linux-containers"></a><span data-ttu-id="7cf61-107">**Contenedores de Linux**</span><span class="sxs-lookup"><span data-stu-id="7cf61-107">**Linux containers**</span></span>

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a><span data-ttu-id="7cf61-108">Se producen errores de compilación cuando se depura una aplicación de consola o web de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="7cf61-108">Build errors occur when debugging a .NET Core web or console application</span></span>  

<span data-ttu-id="7cf61-109">Esto podría ser toonot relacionado comparten unidad de Hola donde reside el proyecto de hello con Docker para Windows.</span><span class="sxs-lookup"><span data-stu-id="7cf61-109">This could be related toonot sharing hello drive where hello project resides with Docker for Windows.</span></span>  <span data-ttu-id="7cf61-110">Puede recibir un error similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="7cf61-110">You may receive an error like hello following:</span></span>

```
hello "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with hello default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
<span data-ttu-id="7cf61-111">tooresolve este problema:</span><span class="sxs-lookup"><span data-stu-id="7cf61-111">tooresolve this issue:</span></span>

1. <span data-ttu-id="7cf61-112">Haga clic en **Docker para Windows** en Hola área de notificación y, a continuación, seleccione **configuración**.</span><span class="sxs-lookup"><span data-stu-id="7cf61-112">Right-click **Docker for Windows** in hello notification area, and then select **Settings**.</span></span>  
2. <span data-ttu-id="7cf61-113">Seleccione **unidades compartidas** y compartir unidad Hola donde reside el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="7cf61-113">Select **Shared Drives** and share hello drive where hello project resides.</span></span>

### <a name="windows-containers"></a><span data-ttu-id="7cf61-114">**Contenedores de Windows**</span><span class="sxs-lookup"><span data-stu-id="7cf61-114">**Windows containers**</span></span>

<span data-ttu-id="7cf61-115">Hello problemas siguientes son aplicaciones de web y la consola de .NET Framework de toodebugging específicos en los contenedores de Windows.</span><span class="sxs-lookup"><span data-stu-id="7cf61-115">hello following issues are specific toodebugging .NET Framework web and console applications in Windows containers.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="7cf61-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7cf61-116">Prerequisites</span></span>

1. <span data-ttu-id="7cf61-117">Visual Studio 2017 RC (o posterior) con Hola .NET Core y carga de trabajo de vista previa de Docker debe estar instalado.</span><span class="sxs-lookup"><span data-stu-id="7cf61-117">Visual Studio 2017 RC (or later) with hello .NET Core and Docker Preview workload must be installed.</span></span>
2. <span data-ttu-id="7cf61-118">Actualización de aniversario de Windows 10 con las revisiones de Windows Update más recientes.</span><span class="sxs-lookup"><span data-stu-id="7cf61-118">Windows 10 Anniversary Update with that latest Windows Update patches.</span></span> <span data-ttu-id="7cf61-119">En concreto, [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) debe estar instalado.</span><span class="sxs-lookup"><span data-stu-id="7cf61-119">Specifically [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) must be installed.</span></span> 
3. <span data-ttu-id="7cf61-120">[Docker para Windows](https://docs.docker.com/docker-for-windows/) (compilación 1.13.0 o posterior) debe estar instalado.</span><span class="sxs-lookup"><span data-stu-id="7cf61-120">[Docker for Windows](https://docs.docker.com/docker-for-windows/) (build 1.13.0 or later) must be installed.</span></span>
4. <span data-ttu-id="7cf61-121">**Cambiar tooWindows contenedores** debe seleccionarse.</span><span class="sxs-lookup"><span data-stu-id="7cf61-121">**Switch tooWindows containers** must be selected.</span></span> <span data-ttu-id="7cf61-122">En el área de notificación de hello, haga clic en **Docker para Windows**y, a continuación, seleccione **cambiar contenedores tooWindows**.</span><span class="sxs-lookup"><span data-stu-id="7cf61-122">In hello notification area, click **Docker for Windows**, and then select **Switch tooWindows containers**.</span></span> <span data-ttu-id="7cf61-123">Una vez reiniciado el equipo de hello, asegúrese de que esta configuración se conserva.</span><span class="sxs-lookup"><span data-stu-id="7cf61-123">After hello machine restarts, ensure that this setting is retained.</span></span>

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a><span data-ttu-id="7cf61-124">La salida de la consola no aparece en la ventana de salida de Visual Studio cuando se depura una aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="7cf61-124">Console output does not appear in Visual Studio's output window while debugging a console application</span></span>

<span data-ttu-id="7cf61-125">Se trata de un problema conocido con el depurador de Visual Studio (msvsmon.exe), de Hola que actualmente no está diseñado para este escenario.</span><span class="sxs-lookup"><span data-stu-id="7cf61-125">This is a known issue with hello Visual Studio debugger (msvsmon.exe), which is currently not designed for this scenario.</span></span> <span data-ttu-id="7cf61-126">En un futuro podría incluirse compatibilidad para este escenario.</span><span class="sxs-lookup"><span data-stu-id="7cf61-126">Support for this scenario might be included in a future release.</span></span> <span data-ttu-id="7cf61-127">resultado de toosee de aplicación de consola de hello en Visual Studio, use **Docker: Iniciar proyecto**, que es equivalente**iniciar sin depurar**.</span><span class="sxs-lookup"><span data-stu-id="7cf61-127">toosee output from hello console application in Visual Studio, use **Docker: Start Project**, which is equivalent too**Start without Debugging**.</span></span>

#### <a name="debugging-web-applications-with-hello-release-configuration-fails-with-403-forbidden-error"></a><span data-ttu-id="7cf61-128">Se produce un error de configuración con error (403) prohibido de la versión de depuración de aplicaciones web con hello</span><span class="sxs-lookup"><span data-stu-id="7cf61-128">Debugging web applications with hello release configuration fails with (403) Forbidden error</span></span>

<span data-ttu-id="7cf61-129">toowork resolver este problema, abra web.release.config de solución de Hola y comente o eliminar Hola siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="7cf61-129">toowork around this issue, open web.release.config in hello solution and comment out or delete hello following lines:</span></span>

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a><span data-ttu-id="7cf61-130">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="7cf61-130">Visual Studio 2015</span></span>

### <a name="linux-containers"></a><span data-ttu-id="7cf61-131">**Contenedores de Linux**</span><span class="sxs-lookup"><span data-stu-id="7cf61-131">**Linux containers**</span></span>

#### <a name="unable-toovalidate-volume-mapping"></a><span data-ttu-id="7cf61-132">Asignación de volúmenes no se puede toovalidate</span><span class="sxs-lookup"><span data-stu-id="7cf61-132">Unable toovalidate volume mapping</span></span>
<span data-ttu-id="7cf61-133">Asignación de volúmenes es necesario tooshare Hola código y archivos binarios de la aplicación con la carpeta de la aplicación hello en el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="7cf61-133">Volume mapping is required tooshare hello source code and binaries of your application with hello app folder in hello container.</span></span>  <span data-ttu-id="7cf61-134">Las asignaciones de volumen específicas se encuentran dentro de los archivos docker-compose.dev.debug.yml y docker-compose.dev.release.yml.</span><span class="sxs-lookup"><span data-stu-id="7cf61-134">Specific volume mappings are contained within docker-compose.dev.debug.yml and docker-compose.dev.release.yml.</span></span> <span data-ttu-id="7cf61-135">Los archivos se cambien en el equipo host, contenedores de hello reflejan estos cambios en una estructura de carpeta similar.</span><span class="sxs-lookup"><span data-stu-id="7cf61-135">As files are changed on your host machine, hello containers reflect these changes in a similar folder structure.</span></span>

<span data-ttu-id="7cf61-136">asignación de volúmenes de tooenable:</span><span class="sxs-lookup"><span data-stu-id="7cf61-136">tooenable volume mapping:</span></span>

1. <span data-ttu-id="7cf61-137">Haga clic en **Moby** en el área de notificación de Hola y seleccione **configuración**.</span><span class="sxs-lookup"><span data-stu-id="7cf61-137">Click **Moby** in hello notification area and select **Settings**.</span></span>
2. <span data-ttu-id="7cf61-138">Seleccione **Shared Drives** (Unidades compartidas).</span><span class="sxs-lookup"><span data-stu-id="7cf61-138">Select **Shared Drives**.</span></span>
3. <span data-ttu-id="7cf61-139">Seleccione la unidad de Hola que hospeda la unidad de hello y el proyecto en el que reside % USERPROFILE %.</span><span class="sxs-lookup"><span data-stu-id="7cf61-139">Select hello drive that hosts your project and hello drive where %USERPROFILE% resides.</span></span>
4. <span data-ttu-id="7cf61-140">Haga clic en **Apply**.</span><span class="sxs-lookup"><span data-stu-id="7cf61-140">Click **Apply**.</span></span>

<span data-ttu-id="7cf61-141">tootest si funciona la asignación de volúmenes, volver a generar y seleccione F5 desde dentro de Visual Studio después de que se han compartido una o varias unidades, o ejecute hello siguiente código desde un símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="7cf61-141">tootest if volume mapping is functioning, Rebuild and select F5 from within Visual Studio after one or more drives have been shared, or run hello following code from a command prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="7cf61-142">En este ejemplo da por supuesto que la carpeta Usuarios se encuentra en la unidad "C" y se ha compartido.</span><span class="sxs-lookup"><span data-stu-id="7cf61-142">This example assumes that your Users folder is located on drive C and that it has been shared.</span></span>
> <span data-ttu-id="7cf61-143">Revise en caso de que haya compartido una unidad diferente.</span><span class="sxs-lookup"><span data-stu-id="7cf61-143">Revise as necessary if you have shared a different drive.</span></span>

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

<span data-ttu-id="7cf61-144">Ejecute hello siguiente código en el contenedor de Linux Hola.</span><span class="sxs-lookup"><span data-stu-id="7cf61-144">Run hello following code in hello Linux container.</span></span>

```
/ # ls
```

<span data-ttu-id="7cf61-145">Debería ver una lista de directorios de Hola a los usuarios y carpetas públicas.</span><span class="sxs-lookup"><span data-stu-id="7cf61-145">You should see a directory listing from hello Users/Public folder.</span></span> <span data-ttu-id="7cf61-146">Si no se muestran archivos y la carpeta /c/Usuarios/Público no está vacía, la asignación de volúmenes no está configurada correctamente.</span><span class="sxs-lookup"><span data-stu-id="7cf61-146">If no files are displayed and your /c/Users/Public folder isn't empty, volume mapping is not configured properly.</span></span>

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

<span data-ttu-id="7cf61-147">Cambiar toohello túnel espacial directory toosee Hola contenido de hello `/c/Users/Public` directorio:</span><span class="sxs-lookup"><span data-stu-id="7cf61-147">Change toohello wormhole directory toosee hello contents of hello `/c/Users/Public` directory:</span></span>

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> <span data-ttu-id="7cf61-148">Cuando se trabaja con máquinas virtuales de Linux, el sistema de archivos del contenedor de hello distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="7cf61-148">When you're working with Linux VMs, hello container file system is case-sensitive.</span></span>

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a><span data-ttu-id="7cf61-149">Compilación: Error inesperado en la tarea "PrepareForBuild".</span><span class="sxs-lookup"><span data-stu-id="7cf61-149">Build: "PrepareForBuild" task failed unexpectedly</span></span>

<span data-ttu-id="7cf61-150">Microsoft.DotNet.Docker.CommandLine.ClientException: Error al tratar de tooconnect.</span><span class="sxs-lookup"><span data-stu-id="7cf61-150">Microsoft.DotNet.Docker.CommandLine.ClientException: An error occurred trying tooconnect.</span></span>

<span data-ttu-id="7cf61-151">Compruebe que ese host de Docker de hello predeterminado se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="7cf61-151">Verify that hello default Docker host is running.</span></span> <span data-ttu-id="7cf61-152">Abra un símbolo del sistema y ejecute:</span><span class="sxs-lookup"><span data-stu-id="7cf61-152">Open a command prompt and execute:</span></span>

```
docker info
```

<span data-ttu-id="7cf61-153">Si se devuelve un error, a continuación, intente hello toostart **Docker para Windows** una aplicación de escritorio.</span><span class="sxs-lookup"><span data-stu-id="7cf61-153">If this returns an error, then attempt toostart hello **Docker for Windows** desktop app.</span></span> <span data-ttu-id="7cf61-154">Si está ejecutando una aplicación de escritorio hello, a continuación, **Moby** debería estar visible en el área de notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="7cf61-154">If hello desktop app is running, then **Moby** should be visible in hello notification area.</span></span> <span data-ttu-id="7cf61-155">Haga clic en **Moby** y abra **Settings** (Configuración).</span><span class="sxs-lookup"><span data-stu-id="7cf61-155">Right-click **Moby** and open **Settings**.</span></span> <span data-ttu-id="7cf61-156">Haga clic en **Reset** (Restablecer) y, a continuación, reinicie Docker.</span><span class="sxs-lookup"><span data-stu-id="7cf61-156">Click **Reset**, and then restart Docker.</span></span>

## <a name="an-error-dialog-occurs-when-attempting-tooadd-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a><span data-ttu-id="7cf61-157">Un cuadro de diálogo de error aparece al intentar tooadd soporte de Docker o depurar una aplicación de ASP.NET Core en un contenedor de (F5)</span><span class="sxs-lookup"><span data-stu-id="7cf61-157">An error dialog occurs when attempting tooadd Docker Support or debug (F5) an ASP.NET Core application in a container</span></span>

<span data-ttu-id="7cf61-158">Después de desinstalar e instalar las extensiones, Hola caché de Managed Extensibility Framework (MEF) en Visual Studio puede resultar dañada.</span><span class="sxs-lookup"><span data-stu-id="7cf61-158">After uninstalling and installing extensions, hello Managed Extensibility Framework (MEF) cache in Visual Studio can become corrupted.</span></span> <span data-ttu-id="7cf61-159">Cuando esto ocurre, puede causar diversos mensajes de error cuando está agregando compatibilidad con Docker o intentar toorun o depurar su aplicación de ASP.NET Core de (F5).</span><span class="sxs-lookup"><span data-stu-id="7cf61-159">When this occurs, it can cause various error messages when you're adding Docker Support and/or attempting toorun or debug (F5) your ASP.NET Core application.</span></span> <span data-ttu-id="7cf61-160">Como solución temporal, use Hola siguiendo los pasos toodelete y regenerate Hola MEF la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="7cf61-160">As a temporary workaround, use hello following steps toodelete and regenerate hello MEF cache.</span></span>

1. <span data-ttu-id="7cf61-161">Cierre todas las instancias de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7cf61-161">Close all instances of Visual Studio.</span></span>
1. <span data-ttu-id="7cf61-162">Abra %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span><span class="sxs-lookup"><span data-stu-id="7cf61-162">Open %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span></span>
1. <span data-ttu-id="7cf61-163">Eliminar Hola siguientes carpetas:</span><span class="sxs-lookup"><span data-stu-id="7cf61-163">Delete hello following folders:</span></span>
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. <span data-ttu-id="7cf61-164">Abra Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7cf61-164">Open Visual Studio.</span></span>
1. <span data-ttu-id="7cf61-165">Vuelva a intentar el escenario de Hola.</span><span class="sxs-lookup"><span data-stu-id="7cf61-165">Attempt hello scenario again.</span></span>
