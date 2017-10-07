---
title: aaaCreate Azure roles web y de trabajo para PHP | Documentos de Microsoft
description: "Una guía toocreating PHP roles web y de trabajo en un servicio de nube de Azure y la configuración en tiempo de ejecución PHP de Hola."
services: 
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9f7ccda0-bd96-4f7b-a7af-fb279a9e975b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 04a6e8c9c379cb0f854645941b6bc7d614bb91f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-php-web-and-worker-roles"></a><span data-ttu-id="3eefa-103">¿Cómo toocreate roles de web y de trabajo PHP</span><span class="sxs-lookup"><span data-stu-id="3eefa-103">How toocreate PHP web and worker roles</span></span>
## <a name="overview"></a><span data-ttu-id="3eefa-104">Información general</span><span class="sxs-lookup"><span data-stu-id="3eefa-104">Overview</span></span>
<span data-ttu-id="3eefa-105">Esta guía le mostrará cómo los roles de trabajador o web PHP toocreate en un entorno de desarrollo de Windows, elegir una versión específica de PHP Hola "integradas" versiones disponibles, cambiar la configuración de PHP hello, habilitar extensiones y por último, implementar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="3eefa-105">This guide will show you how toocreate PHP web or worker roles in a Windows development environment, choose a specific version of PHP from hello "built-in" versions available, change hello PHP configuration, enable extensions, and finally, deploy tooAzure.</span></span> <span data-ttu-id="3eefa-106">También se describe cómo tooconfigure un rol web o trabajo toouse un tiempo de ejecución PHP (con configuración personalizada y extensiones) proporcionada por usted.</span><span class="sxs-lookup"><span data-stu-id="3eefa-106">It also describes how tooconfigure a web or worker role toouse a PHP runtime (with custom configuration and extensions) that you provide.</span></span>

## <a name="what-are-php-web-and-worker-roles"></a><span data-ttu-id="3eefa-107">¿Qué son los roles web y de trabajo de PHP?</span><span class="sxs-lookup"><span data-stu-id="3eefa-107">What are PHP web and worker roles?</span></span>
<span data-ttu-id="3eefa-108">Azure ofrece tres modelos de proceso para la ejecución de aplicaciones: Servicio de aplicaciones de Azure, Máquinas virtuales de Azure y Servicios en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="3eefa-108">Azure provides three compute models for running applications: Azure App Service, Azure Virtual Machines, and Azure Cloud Services.</span></span> <span data-ttu-id="3eefa-109">Los tres modelos admiten PHP.</span><span class="sxs-lookup"><span data-stu-id="3eefa-109">All three models support PHP.</span></span> <span data-ttu-id="3eefa-110">Servicios en la nube, que incluye roles web y de trabajo, ofrece el modelo *Plataforma como servicio (PaaS)*.</span><span class="sxs-lookup"><span data-stu-id="3eefa-110">Cloud Services, which includes web and worker roles, provides *platform as a service (PaaS)*.</span></span> <span data-ttu-id="3eefa-111">Dentro de un servicio de nube, un rol web proporciona un sitio web de Internet Information Services (IIS) dedicado las aplicaciones de servidor toohost front-end web.</span><span class="sxs-lookup"><span data-stu-id="3eefa-111">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server toohost front-end web applications.</span></span> <span data-ttu-id="3eefa-112">Un rol de trabajo puede ejecutar tareas asincrónicas, de ejecución prolongada o perpetuas, independientes de la entrada o la interacción del usuario.</span><span class="sxs-lookup"><span data-stu-id="3eefa-112">A worker role can run asynchronous, long-running or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="3eefa-113">Para más información sobre estas opciones, consulte [Cálculo de las opciones de hospedaje proporcionadas por Azure](cloud-services/cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="3eefa-113">For more information about these options, see [Compute hosting options provided by Azure](cloud-services/cloud-services-choose-me.md).</span></span>

## <a name="download-hello-azure-sdk-for-php"></a><span data-ttu-id="3eefa-114">Descargar hello Azure SDK para PHP</span><span class="sxs-lookup"><span data-stu-id="3eefa-114">Download hello Azure SDK for PHP</span></span>
<span data-ttu-id="3eefa-115">Hola [Azure SDK para PHP] consta de varios componentes.</span><span class="sxs-lookup"><span data-stu-id="3eefa-115">hello [Azure SDK for PHP] consists of several components.</span></span> <span data-ttu-id="3eefa-116">Este artículo utiliza dos de ellos: PowerShell de Azure y Hola emuladores de Azure.</span><span class="sxs-lookup"><span data-stu-id="3eefa-116">This article will use two of them: Azure PowerShell and hello Azure emulators.</span></span> <span data-ttu-id="3eefa-117">Estos dos componentes se pueden instalar a través de hello instalador de plataforma Web de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3eefa-117">These two components can be installed via hello Microsoft Web Platform Installer.</span></span> <span data-ttu-id="3eefa-118">Para obtener más información, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3eefa-118">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="create-a-cloud-services-project"></a><span data-ttu-id="3eefa-119">de un proyecto de servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="3eefa-119">Create a Cloud Services project</span></span>
<span data-ttu-id="3eefa-120">Hola primer paso para crear un rol de trabajo o web PHP es toocreate un proyecto de servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="3eefa-120">hello first step in creating a PHP web or worker role is toocreate an Azure Service project.</span></span> <span data-ttu-id="3eefa-121">un proyecto de servicio de Azure actúa como un contenedor lógico para los roles de web y de trabajo y que contiene el proyecto de hello [(.csdef) de la definición del servicio] y [configuración del servicio (.cscfg)] archivos.</span><span class="sxs-lookup"><span data-stu-id="3eefa-121">an Azure Service project serves as a logical container for web and worker roles, and it contains hello project's [service definition (.csdef)] and [service configuration (.cscfg)] files.</span></span>

<span data-ttu-id="3eefa-122">toocreate un nuevo proyecto de servicio de Azure, ejecute Azure PowerShell como administrador y ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="3eefa-122">toocreate a new Azure Service project, run Azure PowerShell as an administrator, and execute hello following command:</span></span>

    PS C:\>New-AzureServiceProject myProject

<span data-ttu-id="3eefa-123">Este comando crea un nuevo directorio (`myProject`) toowhich puede agregar los roles web y de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3eefa-123">This command will create a new directory (`myProject`) toowhich you can add web and worker roles.</span></span>

## <a name="add-php-web-or-worker-roles"></a><span data-ttu-id="3eefa-124">de roles web y de trabajo de PHP</span><span class="sxs-lookup"><span data-stu-id="3eefa-124">Add PHP web or worker roles</span></span>
<span data-ttu-id="3eefa-125">tooadd un proyecto tooa de rol de web PHP, ejecute hello siguiente comando desde dentro del directorio raíz del proyecto de hello:</span><span class="sxs-lookup"><span data-stu-id="3eefa-125">tooadd a PHP web role tooa project, run hello following command from within hello project's root directory:</span></span>

    PS C:\myProject> Add-AzurePHPWebRole roleName

<span data-ttu-id="3eefa-126">Para un rol de trabajo, use este comando:</span><span class="sxs-lookup"><span data-stu-id="3eefa-126">For a worker role, use this command:</span></span>

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> <span data-ttu-id="3eefa-127">Hola `roleName` parámetro es opcional.</span><span class="sxs-lookup"><span data-stu-id="3eefa-127">hello `roleName` parameter is optional.</span></span> <span data-ttu-id="3eefa-128">Si se omite, se generará automáticamente el nombre del rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="3eefa-128">If it is omitted, hello role name will be automatically generated.</span></span> <span data-ttu-id="3eefa-129">primer rol de web Hola creado será `WebRole1`, hello en segundo lugar será `WebRole2`, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="3eefa-129">hello first web role created will be `WebRole1`, hello second will be `WebRole2`, and so on.</span></span> <span data-ttu-id="3eefa-130">primer rol de trabajo Hola creado será `WorkerRole1`, hello en segundo lugar será `WorkerRole2`, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="3eefa-130">hello first worker role created will be `WorkerRole1`, hello second will be `WorkerRole2`, and so on.</span></span>
>
>

## <a name="specify-hello-built-in-php-version"></a><span data-ttu-id="3eefa-131">Especificar versión PHP integrado Hola</span><span class="sxs-lookup"><span data-stu-id="3eefa-131">Specify hello built-in PHP version</span></span>
<span data-ttu-id="3eefa-132">Cuando se agrega un proyecto PHP tooa de rol de trabajo o web, archivos de configuración del proyecto de Hola se modifican para que PHP se instalará en cada instancia de trabajador o web de la aplicación cuando se implementa.</span><span class="sxs-lookup"><span data-stu-id="3eefa-132">When you add a PHP web or worker role tooa project, hello project's configuration files are modified so that PHP will be installed on each web or worker instance of your application when it is deployed.</span></span> <span data-ttu-id="3eefa-133">versión de hello toosee de PHP que se instalará de forma predeterminada, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="3eefa-133">toosee hello version of PHP that will be installed by default, run hello following command:</span></span>

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

<span data-ttu-id="3eefa-134">Hello salida del comando hello anterior tendrá un aspecto similar toowhat se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="3eefa-134">hello output from hello command above will look similar toowhat is shown below.</span></span> <span data-ttu-id="3eefa-135">En este ejemplo, Hola `IsDefault` marca se establece demasiado`true` para PHP 5.3.17, que indica que será versión PHP predeterminado Hola instalada.</span><span class="sxs-lookup"><span data-stu-id="3eefa-135">In this example, hello `IsDefault` flag is set too`true` for PHP 5.3.17, indicating that it will be hello default PHP version installed.</span></span>

```
Runtime Version     PackageUri                      IsDefault
------- -------     ----------                      ---------
Node 0.6.17         http://nodertncu.blob.core...   False
Node 0.6.20         http://nodertncu.blob.core...   True
Node 0.8.4          http://nodertncu.blob.core...   False
IISNode 0.1.21      http://nodertncu.blob.core...   True
Cache 1.8.0         http://nodertncu.blob.core...   True
PHP 5.3.17          http://nodertncu.blob.core...   True
PHP 5.4.0           http://nodertncu.blob.core...   False
```

<span data-ttu-id="3eefa-136">Puede establecer Hola PHP en tiempo de ejecución versión tooany de versiones PHP de Hola que aparecen.</span><span class="sxs-lookup"><span data-stu-id="3eefa-136">You can set hello PHP runtime version tooany of hello PHP versions that are listed.</span></span> <span data-ttu-id="3eefa-137">Por ejemplo, versión de PHP de tooset Hola (para un rol con nombre hello `roleName`) too5.4.0, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="3eefa-137">For example, tooset hello PHP version (for a role with hello name `roleName`) too5.4.0, use hello following command:</span></span>

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> <span data-ttu-id="3eefa-138">Versiones PHP disponibles pueden cambiar en futuras Hola.</span><span class="sxs-lookup"><span data-stu-id="3eefa-138">Available PHP versions may change in hello future.</span></span>
>
>

## <a name="customize-hello-built-in-php-runtime"></a><span data-ttu-id="3eefa-139">Personalizar el tiempo de ejecución de hello integrado PHP</span><span class="sxs-lookup"><span data-stu-id="3eefa-139">Customize hello built-in PHP runtime</span></span>
<span data-ttu-id="3eefa-140">Tiene un control completo sobre la configuración de Hola de en tiempo de ejecución PHP de Hola que se instala al seguir los pasos de hello anteriormente, incluida la modificación de `php.ini` configuración y habilitación de extensiones.</span><span class="sxs-lookup"><span data-stu-id="3eefa-140">You have complete control over hello configuration of hello PHP runtime that is installed when you follow hello steps above, including modification of `php.ini` settings and enabling of extensions.</span></span>

<span data-ttu-id="3eefa-141">toocustomize Hola integrado en tiempo de ejecución PHP, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3eefa-141">toocustomize hello built-in PHP runtime, follow these steps:</span></span>

1. <span data-ttu-id="3eefa-142">Agregar una nueva carpeta denominada `php`, toohello `bin` directorio de su rol web.</span><span class="sxs-lookup"><span data-stu-id="3eefa-142">Add a new folder, named `php`, toohello `bin` directory of your web role.</span></span> <span data-ttu-id="3eefa-143">Para que un rol de trabajo, debe agregarlo directorio de raíz del rol toohello.</span><span class="sxs-lookup"><span data-stu-id="3eefa-143">For a worker role, add it toohello role's root directory.</span></span>
2. <span data-ttu-id="3eefa-144">Hola `php` carpeta, cree otra carpeta denominada `ext`.</span><span class="sxs-lookup"><span data-stu-id="3eefa-144">In hello `php` folder, create another folder called `ext`.</span></span> <span data-ttu-id="3eefa-145">Ponga ningún `.dll` archivos de extensión (p. ej., `php_mongo.dll`) que desea tooenable en esta carpeta.</span><span class="sxs-lookup"><span data-stu-id="3eefa-145">Put any `.dll` extension files (e.g., `php_mongo.dll`) that you want tooenable in this folder.</span></span>
3. <span data-ttu-id="3eefa-146">Agregar un `php.ini` archivo toohello `php` carpeta.</span><span class="sxs-lookup"><span data-stu-id="3eefa-146">Add a `php.ini` file toohello `php` folder.</span></span> <span data-ttu-id="3eefa-147">Habilite todas las extensiones personalizadas y defina todas las directivas de PHP en este archivo.</span><span class="sxs-lookup"><span data-stu-id="3eefa-147">Enable any custom extensions and set any PHP directives in this file.</span></span> <span data-ttu-id="3eefa-148">Por ejemplo, si deseara tooturn `display_errors` en y habilitar hello `php_mongo.dll` extensión, el contenido de Hola de su `php.ini` archivo sería como sigue:</span><span class="sxs-lookup"><span data-stu-id="3eefa-148">For example, if you wanted tooturn `display_errors` on and enable hello `php_mongo.dll` extension, hello contents of your `php.ini` file would be as follows:</span></span>

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> <span data-ttu-id="3eefa-149">Cualquier configuración que no establece explícitamente en hello `php.ini` archivo que proporcione automáticamente will establecerse como valores predeterminados de tootheir.</span><span class="sxs-lookup"><span data-stu-id="3eefa-149">Any settings that you don't explicitly set in hello `php.ini` file that you provide will automatically be set tootheir default values.</span></span> <span data-ttu-id="3eefa-150">Sin embargo, tenga en cuenta que puede agregar un archivo `php.ini` completo.</span><span class="sxs-lookup"><span data-stu-id="3eefa-150">However, keep in mind that you can add a complete `php.ini` file.</span></span>
>
>

## <a name="use-your-own-php-runtime"></a><span data-ttu-id="3eefa-151">del tiempo de ejecución de PHP propio</span><span class="sxs-lookup"><span data-stu-id="3eefa-151">Use your own PHP runtime</span></span>
<span data-ttu-id="3eefa-152">En algunos casos, en lugar de seleccionar un tiempo de ejecución PHP integrado y configurarlo como se describió anteriormente, puede que desee tooprovide su propio tiempo de ejecución PHP.</span><span class="sxs-lookup"><span data-stu-id="3eefa-152">In some cases, instead of selecting a built-in PHP runtime and configuring it as described above, you may want tooprovide your own PHP runtime.</span></span> <span data-ttu-id="3eefa-153">Por ejemplo, puede usar Hola mismo en tiempo de ejecución PHP en un rol web o de trabajo que se utiliza en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="3eefa-153">For example, you can use hello same PHP runtime in a web or worker role that you use in your development environment.</span></span> <span data-ttu-id="3eefa-154">Esto hace más fácil tooensure esa aplicación hello no cambiará el comportamiento en el entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3eefa-154">This makes it easier tooensure that hello application will not change behavior in your production environment.</span></span>

### <a name="configure-a-web-role-toouse-your-own-php-runtime"></a><span data-ttu-id="3eefa-155">Configurar una toouse de rol web en su propio tiempo de ejecución PHP</span><span class="sxs-lookup"><span data-stu-id="3eefa-155">Configure a web role toouse your own PHP runtime</span></span>
<span data-ttu-id="3eefa-156">tooconfigure un toouse de rol web un tiempo de ejecución PHP que proporcione, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3eefa-156">tooconfigure a web role toouse a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="3eefa-157">Cree un proyecto del servicio de Azure y agregue un rol web de PHP según se describe anteriormente en este tema.</span><span class="sxs-lookup"><span data-stu-id="3eefa-157">Create an Azure Service project and add a PHP web role as described previously in this topic.</span></span>
2. <span data-ttu-id="3eefa-158">Crear un `php` carpeta Hola `bin` carpeta que se encuentra en el directorio de raíz del rol web y, a continuación, agregue el toohello de tiempo de ejecución (todos los archivos binarios, archivos de configuración, las subcarpetas, etc.) de PHP `php` carpeta.</span><span class="sxs-lookup"><span data-stu-id="3eefa-158">Create a `php` folder in hello `bin` folder that is in your web role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) toohello `php` folder.</span></span>
3. <span data-ttu-id="3eefa-159">(OPCIONAL) Si el tiempo de ejecución PHP usa hello [Microsoft Drivers for PHP para SQL Server][sqlsrv drivers], necesitará tooconfigure su tooinstall de rol web [SQL Server Native Client 2012] [ sql native client] cuando se aprovisiona.</span><span class="sxs-lookup"><span data-stu-id="3eefa-159">(OPTIONAL) If your PHP runtime uses hello [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need tooconfigure your web role tooinstall [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="3eefa-160">toodo, agregar hello [sqlncli.msi x64 installer] toohello `bin` carpeta en el directorio de raíz del rol web.</span><span class="sxs-lookup"><span data-stu-id="3eefa-160">toodo this, add hello [sqlncli.msi x64 installer] toohello `bin` folder in your web role's root directory.</span></span> <span data-ttu-id="3eefa-161">script de inicio de Hola se describe en el paso siguiente Hola ejecutará en modo silencioso instalador hello cuando se aprovisiona el rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="3eefa-161">hello startup script described in hello next step will silently run hello installer when hello role is provisioned.</span></span> <span data-ttu-id="3eefa-162">Si el tiempo de ejecución PHP no usa Hola Microsoft Drivers for PHP para SQL Server, puede quitar Hola siguientes línea de script de Hola mostrado en el paso siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="3eefa-162">If your PHP runtime does not use hello Microsoft Drivers for PHP for SQL Server, you can remove hello following line from hello script shown in hello next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="3eefa-163">Defina una tarea de inicio que configura [Internet Information Services (IIS)] [ iis.net] toouse solicita su toohandle en tiempo de ejecución PHP para `.php` páginas.</span><span class="sxs-lookup"><span data-stu-id="3eefa-163">Define a startup task that configures [Internet Information Services (IIS)][iis.net] toouse your PHP runtime toohandle requests for `.php` pages.</span></span> <span data-ttu-id="3eefa-164">toodo, abra hello `setup_web.cmd` archivo (Hola `bin` archivo del directorio de raíz del rol web) en un editor de texto y reemplazar su contenido con Hola después de la secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="3eefa-164">toodo this, open hello `setup_web.cmd` file (in hello `bin` file of your web role's root directory) in a text editor and replace its contents with hello following script:</span></span>

    ```cmd
    @ECHO ON
    cd "%~dp0"

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    SET PHP_FULL_PATH=%~dp0php\php-cgi.exe
    SET NEW_PATH=%PATH%;%RoleRoot%\base\x86

    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%',maxInstances='12',idleTimeout='60000',activityTimeout='3600',requestTimeout='60000',instanceMaxRequests='10000',protocol='NamedPipe',flushNamedPipe='False']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PATH',value='%NEW_PATH%']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PHP_FCGI_MAX_REQUESTS',value='10000']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/handlers /+"[name='PHP',path='*.php',verb='GET,HEAD,POST',modules='FastCgiModule',scriptProcessor='%PHP_FULL_PATH%',resourceType='Either',requireAccess='Script']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /"[fullPath='%PHP_FULL_PATH%'].queueLength:50000"
    ```
5. <span data-ttu-id="3eefa-165">Agregue el directorio raíz de aplicación archivos tooyour del rol web.</span><span class="sxs-lookup"><span data-stu-id="3eefa-165">Add your application files tooyour web role's root directory.</span></span> <span data-ttu-id="3eefa-166">Este será el directorio raíz del servidor de hello web.</span><span class="sxs-lookup"><span data-stu-id="3eefa-166">This will be hello web server's root directory.</span></span>
6. <span data-ttu-id="3eefa-167">Publicar su aplicación, como se describe en hello [publicar su aplicación](#publish-your-application) sección más adelante.</span><span class="sxs-lookup"><span data-stu-id="3eefa-167">Publish your application as described in hello [Publish your application](#publish-your-application) section below.</span></span>

> [!NOTE]
> <span data-ttu-id="3eefa-168">Hola `download.ps1` secuencia de comandos (Hola `bin` carpeta del directorio de raíz del rol web Hola) se pueden eliminar después de seguir los pasos de hello descritos anteriormente para usar su propio tiempo de ejecución PHP.</span><span class="sxs-lookup"><span data-stu-id="3eefa-168">hello `download.ps1` script (in hello `bin` folder of hello web role's root directory) can be deleted after you follow hello steps described above for using your own PHP runtime.</span></span>
>
>

### <a name="configure-a-worker-role-toouse-your-own-php-runtime"></a><span data-ttu-id="3eefa-169">Configurar una toouse de rol de trabajo en su propio tiempo de ejecución PHP</span><span class="sxs-lookup"><span data-stu-id="3eefa-169">Configure a worker role toouse your own PHP runtime</span></span>
<span data-ttu-id="3eefa-170">tooconfigure un toouse de rol de trabajo un tiempo de ejecución PHP que proporcione, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3eefa-170">tooconfigure a worker role toouse a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="3eefa-171">Cree un proyecto del servicio de Azure y agregue un rol de trabajo de PHP según se describe anteriormente en este tema.</span><span class="sxs-lookup"><span data-stu-id="3eefa-171">Create an Azure Service project and add a PHP worker role as described previously in this topic.</span></span>
2. <span data-ttu-id="3eefa-172">Crear un `php` carpeta en el directorio de raíz del rol de trabajo de hello y, a continuación, agregue el toohello de tiempo de ejecución (todos los archivos binarios, archivos de configuración, las subcarpetas, etc.) de PHP `php` carpeta.</span><span class="sxs-lookup"><span data-stu-id="3eefa-172">Create a `php` folder in hello worker role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) toohello `php` folder.</span></span>
3. <span data-ttu-id="3eefa-173">(OPCIONAL) Si usa el tiempo de ejecución PHP [Microsoft Drivers for PHP para SQL Server][sqlsrv drivers], necesitará tooconfigure su tooinstall de rol de trabajo [SQL Server Native Client 2012] [ sql native client] cuando se aprovisiona.</span><span class="sxs-lookup"><span data-stu-id="3eefa-173">(OPTIONAL) If your PHP runtime uses [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need tooconfigure your worker role tooinstall [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="3eefa-174">toodo, agregar hello [sqlncli.msi x64 installer] directorio de raíz del rol de trabajo toohello.</span><span class="sxs-lookup"><span data-stu-id="3eefa-174">toodo this, add hello [sqlncli.msi x64 installer] toohello worker role's root directory.</span></span> <span data-ttu-id="3eefa-175">script de inicio de Hola se describe en el paso siguiente Hola ejecutará en modo silencioso instalador hello cuando se aprovisiona el rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="3eefa-175">hello startup script described in hello next step will silently run hello installer when hello role is provisioned.</span></span> <span data-ttu-id="3eefa-176">Si el tiempo de ejecución PHP no usa Hola Microsoft Drivers for PHP para SQL Server, puede quitar Hola siguientes línea de script de Hola mostrado en el paso siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="3eefa-176">If your PHP runtime does not use hello Microsoft Drivers for PHP for SQL Server, you can remove hello following line from hello script shown in hello next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="3eefa-177">Defina una tarea de inicio que agrega el `php.exe` variable de entorno de ruta de acceso del rol de trabajo ejecutable toohello cuando se aprovisiona el rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="3eefa-177">Define a startup task that adds your `php.exe` executable toohello worker role's PATH environment variable when hello role is provisioned.</span></span> <span data-ttu-id="3eefa-178">toodo, abra hello `setup_worker.cmd` de archivos (en el directorio de raíz del rol de trabajo de Hola) en un editor de texto y reemplace su contenido con hello siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="3eefa-178">toodo this, open hello `setup_worker.cmd` file (in hello worker role's root directory) in a text editor and replace its contents with hello following script:</span></span>

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service toohello web root directory...
    icacls ..\ /grant "Network Service":(OI)(CI)W
    if %ERRORLEVEL% neq 0 goto error
    echo OK

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    setx Path "%PATH%;%~dp0php" /M

    if %ERRORLEVEL% neq 0 goto error

    echo SUCCESS
    exit /b 0

    :error

    echo FAILED
    exit /b -1
    ```
5. <span data-ttu-id="3eefa-179">Agregue el directorio raíz de la aplicación archivos tooyour del rol de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3eefa-179">Add your application files tooyour worker role's root directory.</span></span>
6. <span data-ttu-id="3eefa-180">Publicar su aplicación, como se describe en hello [publicar su aplicación](#publish-your-application) sección más adelante.</span><span class="sxs-lookup"><span data-stu-id="3eefa-180">Publish your application as described in hello [Publish your application](#publish-your-application) section below.</span></span>

## <a name="run-your-application-in-hello-compute-and-storage-emulators"></a><span data-ttu-id="3eefa-181">Ejecutar la aplicación en hello emuladores de proceso y almacenamiento</span><span class="sxs-lookup"><span data-stu-id="3eefa-181">Run your application in hello compute and storage emulators</span></span>
<span data-ttu-id="3eefa-182">Hello emuladores de Azure proporcionan un entorno local en el que puede probar la aplicación de Azure antes de implementarla en la nube toohello.</span><span class="sxs-lookup"><span data-stu-id="3eefa-182">hello Azure emulators provide a local environment in which you can test your Azure application before you deploy it toohello cloud.</span></span> <span data-ttu-id="3eefa-183">Hay algunas diferencias entre los emuladores de Hola y Hola entorno de Azure.</span><span class="sxs-lookup"><span data-stu-id="3eefa-183">There are some differences between hello emulators and hello Azure environment.</span></span> <span data-ttu-id="3eefa-184">toounderstand esto mejor, vea [usar el emulador de almacenamiento de Azure de Hola para desarrollo y pruebas](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="3eefa-184">toounderstand this better, see [Use hello Azure storage emulator for development and testing](storage/common/storage-use-emulator.md).</span></span>

<span data-ttu-id="3eefa-185">Tenga en cuenta que debe tener PHP había instalado localmente emulador de proceso de toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="3eefa-185">Note that you must have PHP installed locally toouse hello compute emulator.</span></span> <span data-ttu-id="3eefa-186">emulador de proceso de Hello usará su local toorun de instalación de PHP la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3eefa-186">hello compute emulator will use your local PHP installation toorun your application.</span></span>

<span data-ttu-id="3eefa-187">ejecutar el proyecto en emuladores de hello, de toorun Hola siguiente comando desde el directorio raíz de su proyecto:</span><span class="sxs-lookup"><span data-stu-id="3eefa-187">toorun your project in hello emulators, execute hello following command from your project's root directory:</span></span>

    PS C:\MyProject> Start-AzureEmulator

<span data-ttu-id="3eefa-188">Verá toothis similar de salida:</span><span class="sxs-lookup"><span data-stu-id="3eefa-188">You will see output similar toothis:</span></span>

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

<span data-ttu-id="3eefa-189">Puede ver la aplicación que se ejecuta en el emulador de hello, abra un explorador web y exploración toohello dirección local se muestra en la salida de hello (`http://127.0.0.1:81` en la salida de ejemplo de Hola anterior).</span><span class="sxs-lookup"><span data-stu-id="3eefa-189">You can see your application running in hello emulator by opening a web browser and browsing toohello local address shown in hello output (`http://127.0.0.1:81` in hello example output above).</span></span>

<span data-ttu-id="3eefa-190">emuladores de hello toostop, ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="3eefa-190">toostop hello emulators, execute this command:</span></span>

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a><span data-ttu-id="3eefa-191">Publicación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="3eefa-191">Publish your application</span></span>
<span data-ttu-id="3eefa-192">toopublish la aplicación, necesita toofirst importar la configuración de publicación mediante el uso de hello [importación-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3eefa-192">toopublish your application, you need toofirst import your publish settings by using hello [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span></span> <span data-ttu-id="3eefa-193">A continuación, puede publicar su aplicación mediante el uso de hello [AzureServiceProject publicar](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3eefa-193">Then you can publish your application by using hello [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span></span> <span data-ttu-id="3eefa-194">Para obtener información acerca de la firma, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3eefa-194">For information about signing in, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3eefa-195">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3eefa-195">Next steps</span></span>
<span data-ttu-id="3eefa-196">Para obtener más información, vea hello [Centro para desarrolladores de PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="3eefa-196">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

[Azure SDK para PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[(.csdef) de la definición del servicio]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[configuración del servicio (.cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[sqlncli.msi x64 installer]: http://go.microsoft.com/fwlink/?LinkID=239648
