---
title: aaaInstall .NET en las funciones de servicios de nube de Azure | Documentos de Microsoft
description: "En este artículo se describe cómo toomanually instalar .NET Framework hello en los roles de web y de trabajo de servicio de nube"
services: cloud-services
documentationcenter: .net
author: thraka
manager: timlt
editor: 
ms.assetid: 8d1243dc-879c-4d1f-9ed0-eecd1f6a6653
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: adegeo
ms.openlocfilehash: 45f0f30221292f98c591511b091b02ebe1c1272c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-net-on-azure-cloud-services-roles"></a><span data-ttu-id="36189-103">Instalación de .NET en roles de Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="36189-103">Install .NET on Azure Cloud Services roles</span></span>
<span data-ttu-id="36189-104">Este artículo describe cómo tooinstall las versiones de .NET Framework que no vienen con Hola SO invitado de Azure.</span><span class="sxs-lookup"><span data-stu-id="36189-104">This article describes how tooinstall versions of .NET Framework that don't come with hello Azure Guest OS.</span></span> <span data-ttu-id="36189-105">Puede usar .NET en hello SO invitado tooconfigure sus roles web y de trabajo del servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="36189-105">You can use .NET on hello Guest OS tooconfigure your cloud service web and worker roles.</span></span>

<span data-ttu-id="36189-106">Por ejemplo, puede instalar .NET 4.6.1 en hello familia del SO invitado 4, que no procede con cualquier versión de .NET 4.6.</span><span class="sxs-lookup"><span data-stu-id="36189-106">For example, you can install .NET 4.6.1 on hello Guest OS family 4, which doesn't come with any release of .NET 4.6.</span></span> <span data-ttu-id="36189-107">(Hola familia del SO invitado 5 incluyen .NET 4.6). Para obtener información más reciente de hello en hello versiones SO invitado de Azure, consulte hello [noticias de la versión de SO invitado de Azure](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="36189-107">(hello Guest OS family 5 does come with .NET 4.6.) For hello latest information on hello Azure Guest OS releases, see hello [Azure Guest OS release news](cloud-services-guestos-update-matrix.md).</span></span> 

>[!IMPORTANT]
><span data-ttu-id="36189-108">Hello Azure SDK 2.9 contiene una restricción sobre la implementación de .NET 4.6 en la familia de SO invitado de hello 4 o versiones anterior.</span><span class="sxs-lookup"><span data-stu-id="36189-108">hello Azure SDK 2.9 contains a restriction on deploying .NET 4.6 on hello Guest OS family 4 or earlier.</span></span> <span data-ttu-id="36189-109">Corrección de restricción de hello está disponible en hello [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) sitio.</span><span class="sxs-lookup"><span data-stu-id="36189-109">A fix for hello restriction is available on hello [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span></span>

<span data-ttu-id="36189-110">tooinstall .NET en sus roles web y de trabajo, incluye el instalador web de hello .NET como parte de su proyecto de servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="36189-110">tooinstall .NET on your web and worker roles, include hello .NET web installer as part of your cloud service project.</span></span> <span data-ttu-id="36189-111">Inicie el instalador de hello como parte de las tareas de inicio del rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="36189-111">Start hello installer as part of hello role's startup tasks.</span></span> 

## <a name="add-hello-net-installer-tooyour-project"></a><span data-ttu-id="36189-112">Agregar proyecto de tooyour de instalador de .NET de Hola</span><span class="sxs-lookup"><span data-stu-id="36189-112">Add hello .NET installer tooyour project</span></span>
<span data-ttu-id="36189-113">instalador de toodownload hello web Hola .NET Framework, elegir versión de Hola que desea tooinstall:</span><span class="sxs-lookup"><span data-stu-id="36189-113">toodownload hello web installer for hello .NET Framework, choose hello version that you want tooinstall:</span></span>

* [<span data-ttu-id="36189-114">Instalador web de .NET 4.7</span><span class="sxs-lookup"><span data-stu-id="36189-114">.NET 4.7 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=825298)
* [<span data-ttu-id="36189-115">Instalador web de .NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="36189-115">.NET 4.6.1 web installer</span></span>](http://go.microsoft.com/fwlink/?LinkId=671729)

<span data-ttu-id="36189-116">instalador de hello tooadd para un *web* rol:</span><span class="sxs-lookup"><span data-stu-id="36189-116">tooadd hello installer for a *web* role:</span></span>
  1. <span data-ttu-id="36189-117">En el **Explorador de soluciones**, en **Roles** del proyecto de servicio en la nube, haga clic con el botón derecho en el rol *web* y seleccione **Agregar** > **Nueva carpeta**.</span><span class="sxs-lookup"><span data-stu-id="36189-117">In **Solution Explorer**, under **Roles** in your cloud service project, right-click your *web* role and select **Add** > **New Folder**.</span></span> <span data-ttu-id="36189-118">Cree una carpeta llamada **bin**.</span><span class="sxs-lookup"><span data-stu-id="36189-118">Create a folder named **bin**.</span></span>
  2. <span data-ttu-id="36189-119">Haga clic en la carpeta bin de Hola y seleccione **agregar** > **elemento existente**.</span><span class="sxs-lookup"><span data-stu-id="36189-119">Right-click hello bin folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="36189-120">Seleccione el instalador de .NET de Hola y Agregar carpeta bin de toohello.</span><span class="sxs-lookup"><span data-stu-id="36189-120">Select hello .NET installer and add it toohello bin folder.</span></span>
  
<span data-ttu-id="36189-121">instalador de hello tooadd para un *trabajo* rol:</span><span class="sxs-lookup"><span data-stu-id="36189-121">tooadd hello installer for a *worker* role:</span></span>
* <span data-ttu-id="36189-122">Haga clic con el botón derecho en el rol de *trabajo* y seleccione **Agregar** > **Elemento existente**.</span><span class="sxs-lookup"><span data-stu-id="36189-122">Right-click your *worker* role and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="36189-123">Seleccione el instalador de .NET de Hola y agregar rol toohello.</span><span class="sxs-lookup"><span data-stu-id="36189-123">Select hello .NET installer and add it toohello role.</span></span> 

<span data-ttu-id="36189-124">Cuando se agregan archivos en esta carpeta de contenido de rol de manera toohello, estas se agregan automáticamente tooyour paquete de servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="36189-124">When files are added in this way toohello role content folder, they're automatically added tooyour cloud service package.</span></span> <span data-ttu-id="36189-125">Hola archivos pasan a ser implementado tooa ubicación coherente en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="36189-125">hello files are then deployed tooa consistent location on hello virtual machine.</span></span> <span data-ttu-id="36189-126">Repita este proceso para cada rol web y de trabajo en el servicio de nube para que todos los roles tienen una copia del instalador de Hola.</span><span class="sxs-lookup"><span data-stu-id="36189-126">Repeat this process for each web and worker role in your cloud service so that all roles have a copy of hello installer.</span></span>

> [!NOTE]
> <span data-ttu-id="36189-127">Debe instalar .NET 4.6.1 en su rol de servicio en la nube, incluso si la aplicación tiene como destino .NET 4.6.</span><span class="sxs-lookup"><span data-stu-id="36189-127">You should install .NET 4.6.1 on your cloud service role even if your application targets .NET 4.6.</span></span> <span data-ttu-id="36189-128">Hola SO invitado incluye Base de conocimiento de hello [actualizar 3098779](https://support.microsoft.com/kb/3098779) y [actualizar 3097997](https://support.microsoft.com/kb/3097997).</span><span class="sxs-lookup"><span data-stu-id="36189-128">hello Guest OS includes hello Knowledge Base [update 3098779](https://support.microsoft.com/kb/3098779) and [update 3097997](https://support.microsoft.com/kb/3097997).</span></span> <span data-ttu-id="36189-129">Pueden producirse problemas al ejecutar las aplicaciones de .NET si está instalado .NET 4.6 encima de las actualizaciones de Base de conocimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="36189-129">Issues can occur when you run your .NET applications if .NET 4.6 is installed on top of hello Knowledge Base updates.</span></span> <span data-ttu-id="36189-130">tooavoid estos problemas, instale .NET 4.6.1 en lugar de la versión 4.6.</span><span class="sxs-lookup"><span data-stu-id="36189-130">tooavoid these issues, install .NET 4.6.1 rather than version 4.6.</span></span> <span data-ttu-id="36189-131">Para obtener más información, vea hello [el artículo de Knowledge Base 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="36189-131">For more information, see hello [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
> 
> 

![Contenidos de rol con archivos de instalador][1]

## <a name="define-startup-tasks-for-your-roles"></a><span data-ttu-id="36189-133">Definir las tareas de inicio para los roles</span><span class="sxs-lookup"><span data-stu-id="36189-133">Define startup tasks for your roles</span></span>
<span data-ttu-id="36189-134">Puede utilizar operaciones de tooperform de tareas de inicio antes de que se inicia un rol.</span><span class="sxs-lookup"><span data-stu-id="36189-134">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="36189-135">Instalar Hola .NET Framework como parte de la tarea de inicio de hello garantiza framework Hola está instalado antes de que se ejecute cualquier código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="36189-135">Installing hello .NET Framework as part of hello startup task ensures that hello framework is installed before any application code is run.</span></span> <span data-ttu-id="36189-136">Para más información sobre de las tareas de inicio, consulte [Ejecución de tareas de inicio en Azure](cloud-services-startup-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="36189-136">For more information on startup tasks, see [Run startup tasks in Azure](cloud-services-startup-tasks.md).</span></span> 

1. <span data-ttu-id="36189-137">Agregar Hola siguiente contenido toohello el archivo ServiceDefinition.csdef bajo hello **WebRole** o **WorkerRole** nodo para todos los roles:</span><span class="sxs-lookup"><span data-stu-id="36189-137">Add hello following content toohello ServiceDefinition.csdef file under hello **WebRole** or **WorkerRole** node for all roles:</span></span>
   
    ```xml
    <LocalResources>
      <LocalStorage name="NETFXInstall" sizeInMB="1024" cleanOnRoleRecycle="false" />
    </LocalResources>    
    <Startup>
      <Task commandLine="install.cmd" executionContext="elevated" taskType="simple">
        <Environment>
          <Variable name="PathToNETFXInstall">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='NETFXInstall']/@path" />
          </Variable>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
    ```
   
    <span data-ttu-id="36189-138">Hello configuración anterior ejecuta comandos de consola de hello `install.cmd` con tooinstall de privilegios de administrador Hola .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="36189-138">hello preceding configuration runs hello console command `install.cmd` with administrator privileges tooinstall hello .NET Framework.</span></span> <span data-ttu-id="36189-139">configuración de Hello también crea un **LocalStorage** elemento denominado **NETFXInstall**.</span><span class="sxs-lookup"><span data-stu-id="36189-139">hello configuration also creates a **LocalStorage** element named **NETFXInstall**.</span></span> <span data-ttu-id="36189-140">script de inicio de Hello establece toouse de la carpeta temporal de hello este recurso de almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="36189-140">hello startup script sets hello temp folder toouse this local storage resource.</span></span> 
    
    > [!IMPORTANT]
    > <span data-ttu-id="36189-141">tooensure corregir instalación de framework hello, tamaño del conjunto de Hola de este recurso tooat menos 1024 MB.</span><span class="sxs-lookup"><span data-stu-id="36189-141">tooensure correct installation of hello framework, set hello size of this resource tooat least 1,024 MB.</span></span>
    
    <span data-ttu-id="36189-142">Para más información sobre las tareas de inicio, consulte las [tareas de inicio comunes de Azure Cloud Services](cloud-services-startup-tasks-common.md).</span><span class="sxs-lookup"><span data-stu-id="36189-142">For more information about startup tasks, see [Common Azure Cloud Services startup tasks](cloud-services-startup-tasks-common.md).</span></span>

2. <span data-ttu-id="36189-143">Cree un archivo denominado **install.cmd** y agregue la siguiente Hola instala archivos de script toohello.</span><span class="sxs-lookup"><span data-stu-id="36189-143">Create a file named **install.cmd** and add hello following install script toohello file.</span></span>

    <span data-ttu-id="36189-144">script de Hola comprueba si versión especificada de Hola de hello .NET Framework ya está instalado en el equipo de hello consultando el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="36189-144">hello script checks whether hello specified version of hello .NET Framework is already installed on hello machine by querying hello registry.</span></span> <span data-ttu-id="36189-145">Si no está instalada la versión de .NET de hello, se abre el instalador web de .NET de Hola.</span><span class="sxs-lookup"><span data-stu-id="36189-145">If hello .NET version is not installed, then hello .NET web installer is opened.</span></span> <span data-ttu-id="36189-146">toohelp solucionar los problemas, el script de Hola registra todas las actividades toohello archivo startuptasklog-(fecha y hora actuales) .txt que se almacena en **InstallLogs** almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="36189-146">toohelp troubleshoot any issues, hello script logs all activity toohello file startuptasklog-(current date and time).txt that is stored in **InstallLogs** local storage.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="36189-147">Utilice un editor de texto básico como el Bloc de notas de Windows toocreate Hola install.cmd archivo.</span><span class="sxs-lookup"><span data-stu-id="36189-147">Use a basic text editor like Windows Notepad toocreate hello install.cmd file.</span></span> <span data-ttu-id="36189-148">Si utiliza Visual Studio toocreate un archivo de texto y cambie Hola extensión too.cmd, archivo hello todavía podría contener una marca de orden de bytes UTF-8.</span><span class="sxs-lookup"><span data-stu-id="36189-148">If you use Visual Studio toocreate a text file and change hello extension too.cmd, hello file might still contain a UTF-8 byte order mark.</span></span> <span data-ttu-id="36189-149">Esta marca puede producir un error cuando se ejecuta la primera línea del script de Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="36189-149">This mark can cause an error when hello first line of hello script is run.</span></span> <span data-ttu-id="36189-150">tooavoid este error, asegúrese de primera línea de Hola de hello una REM (instrucción) que se puede omitir por el procesamiento de orden de bytes de Hola de secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="36189-150">tooavoid this error, make hello first line of hello script a REM statement that can be skipped by hello byte order processing.</span></span> 
    > 
    >
   
    ```cmd
    REM Set hello value of netfx tooinstall appropriate .NET Framework. 
    REM ***** tooinstall .NET 4.5.2 set hello variable netfx too"NDP452" *****
    REM ***** tooinstall .NET 4.6 set hello variable netfx too"NDP46" *****
    REM ***** tooinstall .NET 4.6.1 set hello variable netfx too"NDP461" *****
    REM ***** tooinstall .NET 4.6.2 set hello variable netfx too"NDP462" *****
    REM ***** tooinstall .NET 4.7 set hello variable netfx too"NDP47" *****
    set netfx="NDP47"

    REM ***** Set script start timestamp *****
    set timehour=%time:~0,2%
    set timestamp=%date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2%
    set "log=install.cmd started %timestamp%."

    REM ***** Exit script if running in Emulator *****
    if %ComputeEmulatorRunning%=="true" goto exit

    REM ***** Needed toocorrectly install .NET 4.6.1, otherwise you may see an out of disk space error *****
    set TMP=%PathToNETFXInstall%
    set TEMP=%PathToNETFXInstall%

    REM ***** Setup .NET filenames and registry keys *****
    if %netfx%=="NDP47" goto NDP47
    if %netfx%=="NDP462" goto NDP462
    if %netfx%=="NDP461" goto NDP461
    if %netfx%=="NDP46" goto NDP46
        set "netfxinstallfile=NDP452-KB2901954-Web.exe"
        set netfxregkey="0x5cbf5"
        goto logtimestamp

    :NDP46
    set "netfxinstallfile=NDP46-KB3045560-Web.exe"
    set netfxregkey="0x6004f"
    goto logtimestamp

    :NDP461
    set "netfxinstallfile=NDP461-KB3102438-Web.exe"
    set netfxregkey="0x6040e"
    goto logtimestamp

    :NDP462
    set "netfxinstallfile=NDP462-KB3151802-Web.exe"
    set netfxregkey="0x60632"

    :NDP47
    set "netfxinstallfile=NDP47-KB3186500-Web.exe"
    set netfxregkey="0x707FE"

    :logtimestamp
    REM ***** Setup LogFile with timestamp *****
    md "%PathToNETFXInstall%\log"
    set startuptasklog="%PathToNETFXInstall%log\startuptasklog-%timestamp%.txt"
    set netfxinstallerlog="%PathToNETFXInstall%log\NetFXInstallerLog-%timestamp%"
    echo %log% >> %startuptasklog%
    echo Logfile generated at: %startuptasklog% >> %startuptasklog%
    echo TMP set to: %TMP% >> %startuptasklog%
    echo TEMP set to: %TEMP% >> %startuptasklog%

    REM ***** Check if .NET is installed *****
    echo Checking if .NET (%netfx%) is installed >> %startuptasklog%
    set /A netfxregkeydecimal=%netfxregkey%
    set foundkey=0
    FOR /F "usebackq skip=2 tokens=1,2*" %%A in (`reg query "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full" /v Release 2^>nul`) do @set /A foundkey=%%C
    echo Minimum required key: %netfxregkeydecimal% -- found key: %foundkey% >> %startuptasklog%
    if %foundkey% GEQ %netfxregkeydecimal% goto installed

    REM ***** Installing .NET *****
    echo Installing .NET with commandline: start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog%  /chainingpackage "CloudService Startup Task" >> %startuptasklog%
    start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog% /chainingpackage "CloudService Startup Task" >> %startuptasklog% 2>>&1
    if %ERRORLEVEL%== 0 goto installed
        echo .NET installer exited with code %ERRORLEVEL% >> %startuptasklog%    
        if %ERRORLEVEL%== 3010 goto restart
        if %ERRORLEVEL%== 1641 goto restart
        echo .NET (%netfx%) install failed with Error Code %ERRORLEVEL%. Further logs can be found in %netfxinstallerlog% >> %startuptasklog%

    :restart
    echo Restarting toocomplete .NET (%netfx%) installation >> %startuptasklog%
    EXIT /B %ERRORLEVEL%

    :installed
    echo .NET (%netfx%) is installed >> %startuptasklog%

    :end
    echo install.cmd completed: %date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2% >> %startuptasklog%

    :exit
    EXIT /B 0
    ```
   
   > [!NOTE]
   > <span data-ttu-id="36189-151">Este script muestra cómo tooinstall .NET 4.5.2 o la versión 4.6 de continuidad, aunque ya está disponible en .NET 4.5.2 Hola SO invitado de Azure.</span><span class="sxs-lookup"><span data-stu-id="36189-151">This script shows how tooinstall .NET 4.5.2 or version 4.6 for continuity, even though .NET 4.5.2 is already available on hello Azure Guest OS.</span></span> <span data-ttu-id="36189-152">Directamente debe instalar .NET 4.6.1 en lugar de la versión 4.6, tal y como se describe en hello [el artículo de Knowledge Base 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="36189-152">You should directly install .NET 4.6.1 rather than version 4.6, as described in hello [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
   > 
   > 

3. <span data-ttu-id="36189-153">Agregar el rol tooeach de hello install.cmd archivos mediante el uso de **agregar** > **elemento existente** en **el Explorador de soluciones** tal como se describe anteriormente en este tema.</span><span class="sxs-lookup"><span data-stu-id="36189-153">Add hello install.cmd file tooeach role by using **Add** > **Existing Item** in **Solution Explorer** as described earlier in this topic.</span></span> 

    <span data-ttu-id="36189-154">Una vez completado este paso, deben tener todos los roles de archivo de instalador de .NET de hello y archivo de hello install.cmd.</span><span class="sxs-lookup"><span data-stu-id="36189-154">After this step is complete, all roles should have hello .NET installer file and hello install.cmd file.</span></span>

   ![Contenidos de rol con todos los archivos][2]

## <a name="configure-diagnostics-tootransfer-startup-logs-tooblob-storage"></a><span data-ttu-id="36189-156">Configurar el almacenamiento de información de diagnóstico tootransfer inicio registros tooBlob</span><span class="sxs-lookup"><span data-stu-id="36189-156">Configure Diagnostics tootransfer startup logs tooBlob storage</span></span>
<span data-ttu-id="36189-157">toosimplify solución de problemas de instalación, puede configurar diagnósticos de Azure tootransfer script o bienvenida almacenamiento de blobs de tooAzure de instalador de .NET a los archivos de registro generados por el inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="36189-157">toosimplify troubleshooting installation issues, you can configure Azure Diagnostics tootransfer any log files generated by hello startup script or hello .NET installer tooAzure Blob storage.</span></span> <span data-ttu-id="36189-158">Con este enfoque, puede ver registros de Hola por descargar archivos de registro de hello desde almacenamiento de blobs, en lugar de tener tooremote escritorio en función de Hola.</span><span class="sxs-lookup"><span data-stu-id="36189-158">By using this approach, you can view hello logs by downloading hello log files from Blob storage rather than having tooremote desktop into hello role.</span></span>

<span data-ttu-id="36189-159">tooconfigure diagnósticos, abra el archivo diagnostics.wadcfgx de hello y agregue Hola siguen contenido en hello **directorios** nodo:</span><span class="sxs-lookup"><span data-stu-id="36189-159">tooconfigure Diagnostics, open hello diagnostics.wadcfgx file and add hello following content under hello **Directories** node:</span></span> 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

<span data-ttu-id="36189-160">Este código XML configura archivos de diagnóstico tootransfer hello en el directorio de registro de hello en hello **NETFXInstall** recurso toohello cuenta de almacenamiento de diagnósticos en hello **netfx install** contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="36189-160">This XML configures Diagnostics tootransfer hello files in hello log directory in hello **NETFXInstall** resource toohello Diagnostics storage account in hello **netfx-install** blob container.</span></span>

## <a name="deploy-your-cloud-service"></a><span data-ttu-id="36189-161">Implementación del servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="36189-161">Deploy your cloud service</span></span>
<span data-ttu-id="36189-162">Al implementar el servicio de nube, las tareas de inicio de Hola instalación Hola .NET Framework si aún no está instalado.</span><span class="sxs-lookup"><span data-stu-id="36189-162">When you deploy your cloud service, hello startup tasks install hello .NET Framework if it's not already installed.</span></span> <span data-ttu-id="36189-163">Los roles de servicio de nube están en hello *ocupado* estado mientras se instala framework Hola.</span><span class="sxs-lookup"><span data-stu-id="36189-163">Your cloud service roles are in hello *busy* state while hello framework is being installed.</span></span> <span data-ttu-id="36189-164">Si la instalación de framework Hola requiere un reinicio, los roles del servicio hello también podrían reiniciarse.</span><span class="sxs-lookup"><span data-stu-id="36189-164">If hello framework installation requires a restart, hello service roles might also restart.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="36189-165">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="36189-165">Additional resources</span></span>
* <span data-ttu-id="36189-166">[Hola instalar .NET Framework][Installing hello .NET Framework]</span><span class="sxs-lookup"><span data-stu-id="36189-166">[Installing hello .NET Framework][Installing hello .NET Framework]</span></span>
* <span data-ttu-id="36189-167">[Determinación de las versiones instaladas de .NET Framework][How to: Determine Which .NET Framework Versions Are Installed]</span><span class="sxs-lookup"><span data-stu-id="36189-167">[Determine which .NET Framework versions are installed][How to: Determine Which .NET Framework Versions Are Installed]</span></span>
* <span data-ttu-id="36189-168">[Solución de problemas en instalaciones de .NET Framework][Troubleshooting .NET Framework Installations]</span><span class="sxs-lookup"><span data-stu-id="36189-168">[Troubleshooting .NET Framework installations][Troubleshooting .NET Framework Installations]</span></span>

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing hello .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
