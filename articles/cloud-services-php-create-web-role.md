---
title: "Creación de roles web y de trabajo de Azure para PHP | Microsoft Docs"
description: "Una guía para crear roles web y de trabajo de PHP en un servicio en la nube de Azure y configurar el tiempo en ejecución de PHP."
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
ms.openlocfilehash: 214fdcfe20f3fa4ebcbe41308404f8b7e7d15310
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-php-web-and-worker-roles"></a><span data-ttu-id="ac769-103">Creación de roles de trabajo y web de PHP</span><span class="sxs-lookup"><span data-stu-id="ac769-103">How to create PHP web and worker roles</span></span>
## <a name="overview"></a><span data-ttu-id="ac769-104">Información general</span><span class="sxs-lookup"><span data-stu-id="ac769-104">Overview</span></span>
<span data-ttu-id="ac769-105">En esta guía se explica cómo crear roles de trabajo o web de PHP en un entorno de desarrollo de Windows, elegir una versión específica de PHP de versiones "integradas" disponibles, cambiar la configuración de PHP, habilitar extensiones y, por último, implementar en Azure.</span><span class="sxs-lookup"><span data-stu-id="ac769-105">This guide will show you how to create PHP web or worker roles in a Windows development environment, choose a specific version of PHP from the "built-in" versions available, change the PHP configuration, enable extensions, and finally, deploy to Azure.</span></span> <span data-ttu-id="ac769-106">También se describe cómo configurar un rol web o de trabajo para usar un tiempo de ejecución de PHP (con las extensiones y la configuración personalizada) proporcionado por el usuario.</span><span class="sxs-lookup"><span data-stu-id="ac769-106">It also describes how to configure a web or worker role to use a PHP runtime (with custom configuration and extensions) that you provide.</span></span>

## <a name="what-are-php-web-and-worker-roles"></a><span data-ttu-id="ac769-107">¿Qué son los roles web y de trabajo de PHP?</span><span class="sxs-lookup"><span data-stu-id="ac769-107">What are PHP web and worker roles?</span></span>
<span data-ttu-id="ac769-108">Azure ofrece tres modelos de proceso para la ejecución de aplicaciones: Servicio de aplicaciones de Azure, Máquinas virtuales de Azure y Servicios en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac769-108">Azure provides three compute models for running applications: Azure App Service, Azure Virtual Machines, and Azure Cloud Services.</span></span> <span data-ttu-id="ac769-109">Los tres modelos admiten PHP.</span><span class="sxs-lookup"><span data-stu-id="ac769-109">All three models support PHP.</span></span> <span data-ttu-id="ac769-110">Servicios en la nube, que incluye roles web y de trabajo, ofrece el modelo *Plataforma como servicio (PaaS)*.</span><span class="sxs-lookup"><span data-stu-id="ac769-110">Cloud Services, which includes web and worker roles, provides *platform as a service (PaaS)*.</span></span> <span data-ttu-id="ac769-111">Dentro de un servicio en la nube, un rol web proporciona un servidor web de Internet Information Services (IIS) dedicado para hospedar aplicaciones web front-end.</span><span class="sxs-lookup"><span data-stu-id="ac769-111">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server to host front-end web applications.</span></span> <span data-ttu-id="ac769-112">Un rol de trabajo puede ejecutar tareas asincrónicas, de ejecución prolongada o perpetuas, independientes de la entrada o la interacción del usuario.</span><span class="sxs-lookup"><span data-stu-id="ac769-112">A worker role can run asynchronous, long-running or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="ac769-113">Para más información sobre estas opciones, consulte [Cálculo de las opciones de hospedaje proporcionadas por Azure](cloud-services/cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="ac769-113">For more information about these options, see [Compute hosting options provided by Azure](cloud-services/cloud-services-choose-me.md).</span></span>

## <a name="download-the-azure-sdk-for-php"></a><span data-ttu-id="ac769-114">Descarga del SDK de Azure para PHP</span><span class="sxs-lookup"><span data-stu-id="ac769-114">Download the Azure SDK for PHP</span></span>
<span data-ttu-id="ac769-115">El [SDK de Azure para PHP] tiene varios componentes.</span><span class="sxs-lookup"><span data-stu-id="ac769-115">The [Azure SDK for PHP] consists of several components.</span></span> <span data-ttu-id="ac769-116">Este artículo usará dos de ellos: los emuladores de Azure PowerShell y de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac769-116">This article will use two of them: Azure PowerShell and the Azure emulators.</span></span> <span data-ttu-id="ac769-117">Estos dos componentes se pueden instalar a través del instalador de la plataforma web de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ac769-117">These two components can be installed via the Microsoft Web Platform Installer.</span></span> <span data-ttu-id="ac769-118">Para obtener más información, consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ac769-118">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="create-a-cloud-services-project"></a><span data-ttu-id="ac769-119">de un proyecto de servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="ac769-119">Create a Cloud Services project</span></span>
<span data-ttu-id="ac769-120">El primer paso para crear un rol web o de trabajo de PHP es crear un proyecto del servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac769-120">The first step in creating a PHP web or worker role is to create an Azure Service project.</span></span> <span data-ttu-id="ac769-121">El primer paso para crear un rol web o de trabajo de PHP es crear un proyecto del servicio de Azure. Un proyecto del servicio de Azure sirve como un contenedor lógico para roles web y de trabajo y contiene los archivos de [definición del servicio (.csdef)] y [configuración del servicio (.cscfg)] del proyecto.</span><span class="sxs-lookup"><span data-stu-id="ac769-121">an Azure Service project serves as a logical container for web and worker roles, and it contains the project's [service definition (.csdef)] and [service configuration (.cscfg)] files.</span></span>

<span data-ttu-id="ac769-122">Para crear un proyecto nuevo del servicio de Azure, ejecute Azure PowerShell como administrador y, a continuación, ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac769-122">To create a new Azure Service project, run Azure PowerShell as an administrator, and execute the following command:</span></span>

    PS C:\>New-AzureServiceProject myProject

<span data-ttu-id="ac769-123">Este comando creará un directorio nuevo (`myProject`) al que puede agregar roles web y de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ac769-123">This command will create a new directory (`myProject`) to which you can add web and worker roles.</span></span>

## <a name="add-php-web-or-worker-roles"></a><span data-ttu-id="ac769-124">de roles web y de trabajo de PHP</span><span class="sxs-lookup"><span data-stu-id="ac769-124">Add PHP web or worker roles</span></span>
<span data-ttu-id="ac769-125">Para agregar un rol web de PHP a un proyecto, ejecute el siguiente comando desde el directorio raíz del proyecto:</span><span class="sxs-lookup"><span data-stu-id="ac769-125">To add a PHP web role to a project, run the following command from within the project's root directory:</span></span>

    PS C:\myProject> Add-AzurePHPWebRole roleName

<span data-ttu-id="ac769-126">Para un rol de trabajo, use este comando:</span><span class="sxs-lookup"><span data-stu-id="ac769-126">For a worker role, use this command:</span></span>

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> <span data-ttu-id="ac769-127">El `roleName` es opcional.</span><span class="sxs-lookup"><span data-stu-id="ac769-127">The `roleName` parameter is optional.</span></span> <span data-ttu-id="ac769-128">Si se omite, el nombre de rol se generará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="ac769-128">If it is omitted, the role name will be automatically generated.</span></span> <span data-ttu-id="ac769-129">El primer rol web creado será `WebRole1`, el segundo será `WebRole2` y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="ac769-129">The first web role created will be `WebRole1`, the second will be `WebRole2`, and so on.</span></span> <span data-ttu-id="ac769-130">El primer rol de trabajo creado será `WorkerRole1`, el segundo será `WorkerRole2` y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="ac769-130">The first worker role created will be `WorkerRole1`, the second will be `WorkerRole2`, and so on.</span></span>
>
>

## <a name="specify-the-built-in-php-version"></a><span data-ttu-id="ac769-131">de la versión de PHP integrada</span><span class="sxs-lookup"><span data-stu-id="ac769-131">Specify the built-in PHP version</span></span>
<span data-ttu-id="ac769-132">Al agregar un rol web o de trabajo de PHP a un proyecto, los archivos de configuración del proyecto se modifican para que PHP se instale en cada instancia de trabajo o web de la aplicación cuando se implementa.</span><span class="sxs-lookup"><span data-stu-id="ac769-132">When you add a PHP web or worker role to a project, the project's configuration files are modified so that PHP will be installed on each web or worker instance of your application when it is deployed.</span></span> <span data-ttu-id="ac769-133">Para ver la versión de PHP que se instalará de forma predeterminada, ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac769-133">To see the version of PHP that will be installed by default, run the following command:</span></span>

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

<span data-ttu-id="ac769-134">La salida del comando anterior tendrá un aspecto similar al que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="ac769-134">The output from the command above will look similar to what is shown below.</span></span> <span data-ttu-id="ac769-135">En este ejemplo, la marca `IsDefault` se define en `true` para PHP 5.3.17, indicando que será la versión de PHP instalada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ac769-135">In this example, the `IsDefault` flag is set to `true` for PHP 5.3.17, indicating that it will be the default PHP version installed.</span></span>

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

<span data-ttu-id="ac769-136">Puede definir la versión del tiempo de ejecución de PHP con cualquier versión de PHP de la lista.</span><span class="sxs-lookup"><span data-stu-id="ac769-136">You can set the PHP runtime version to any of the PHP versions that are listed.</span></span> <span data-ttu-id="ac769-137">Por ejemplo, para definir la versión de PHP (para un rol con nombre `roleName`) como 5.4.0, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac769-137">For example, to set the PHP version (for a role with the name `roleName`) to 5.4.0, use the following command:</span></span>

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> <span data-ttu-id="ac769-138">Las versiones PHP disponibles pueden cambiar en el futuro.</span><span class="sxs-lookup"><span data-stu-id="ac769-138">Available PHP versions may change in the future.</span></span>
>
>

## <a name="customize-the-built-in-php-runtime"></a><span data-ttu-id="ac769-139">del tiempo de ejecución de PHP integrado</span><span class="sxs-lookup"><span data-stu-id="ac769-139">Customize the built-in PHP runtime</span></span>
<span data-ttu-id="ac769-140">Tiene el control total de la configuración del tiempo de ejecución de PHO instalado al seguir los pasos anteriores, incluida la modificación de la configuración de `php.ini` y la habilitación de las extensiones.</span><span class="sxs-lookup"><span data-stu-id="ac769-140">You have complete control over the configuration of the PHP runtime that is installed when you follow the steps above, including modification of `php.ini` settings and enabling of extensions.</span></span>

<span data-ttu-id="ac769-141">Para personalizar el tiempo de ejecución de PHP integrado, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ac769-141">To customize the built-in PHP runtime, follow these steps:</span></span>

1. <span data-ttu-id="ac769-142">Agregue una carpeta nueva, con el  nombre `php`, al directorio `bin` del rol web.</span><span class="sxs-lookup"><span data-stu-id="ac769-142">Add a new folder, named `php`, to the `bin` directory of your web role.</span></span> <span data-ttu-id="ac769-143">Si se trata de un rol de trabajo, agréguelo al directorio raíz del rol.</span><span class="sxs-lookup"><span data-stu-id="ac769-143">For a worker role, add it to the role's root directory.</span></span>
2. <span data-ttu-id="ac769-144">En la carpeta `php`, cree otra carpeta denominada `ext`.</span><span class="sxs-lookup"><span data-stu-id="ac769-144">In the `php` folder, create another folder called `ext`.</span></span> <span data-ttu-id="ac769-145">Coloque los archivos de extensión `.dll` (por ejemplo, `php_mongo.dll`) que desee habilitar en esta carpeta.</span><span class="sxs-lookup"><span data-stu-id="ac769-145">Put any `.dll` extension files (e.g., `php_mongo.dll`) that you want to enable in this folder.</span></span>
3. <span data-ttu-id="ac769-146">Agregue un archivo `php.ini` a la carpeta `php`.</span><span class="sxs-lookup"><span data-stu-id="ac769-146">Add a `php.ini` file to the `php` folder.</span></span> <span data-ttu-id="ac769-147">Habilite todas las extensiones personalizadas y defina todas las directivas de PHP en este archivo.</span><span class="sxs-lookup"><span data-stu-id="ac769-147">Enable any custom extensions and set any PHP directives in this file.</span></span> <span data-ttu-id="ac769-148">Por ejemplo, si desea activar `display_errors` y habilitar la extensión `php_mongo.dll`, el contenido del archivo `php.ini` será el siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac769-148">For example, if you wanted to turn `display_errors` on and enable the `php_mongo.dll` extension, the contents of your `php.ini` file would be as follows:</span></span>

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> <span data-ttu-id="ac769-149">Cualquier configuración que no defina explícitamente en el archivo `php.ini` que proporcione se definirá automáticamente con los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="ac769-149">Any settings that you don't explicitly set in the `php.ini` file that you provide will automatically be set to their default values.</span></span> <span data-ttu-id="ac769-150">Sin embargo, tenga en cuenta que puede agregar un archivo `php.ini` completo.</span><span class="sxs-lookup"><span data-stu-id="ac769-150">However, keep in mind that you can add a complete `php.ini` file.</span></span>
>
>

## <a name="use-your-own-php-runtime"></a><span data-ttu-id="ac769-151">del tiempo de ejecución de PHP propio</span><span class="sxs-lookup"><span data-stu-id="ac769-151">Use your own PHP runtime</span></span>
<span data-ttu-id="ac769-152">En algunos casos, en lugar de seleccionar un tiempo de ejecución de PHP integrado y configurarlo como se ha descrito anteriormente, puede proporcionar el tiempo de ejecución de PHP propio.</span><span class="sxs-lookup"><span data-stu-id="ac769-152">In some cases, instead of selecting a built-in PHP runtime and configuring it as described above, you may want to provide your own PHP runtime.</span></span> <span data-ttu-id="ac769-153">Por ejemplo, puede usar el mismo tiempo de ejecución de PHP en un rol web o de trabajo que use en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="ac769-153">For example, you can use the same PHP runtime in a web or worker role that you use in your development environment.</span></span> <span data-ttu-id="ac769-154">De esta forma, garantiza de forma más fácil que la aplicación no cambiará su comportamiento en el entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="ac769-154">This makes it easier to ensure that the application will not change behavior in your production environment.</span></span>

### <a name="configure-a-web-role-to-use-your-own-php-runtime"></a><span data-ttu-id="ac769-155">Configuración de un rol web para usar un tiempo de ejecución de PHP propio</span><span class="sxs-lookup"><span data-stu-id="ac769-155">Configure a web role to use your own PHP runtime</span></span>
<span data-ttu-id="ac769-156">Para configurar un rol web para usar un tiempo de ejecución de PHP proporcionado por el usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ac769-156">To configure a web role to use a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="ac769-157">Cree un proyecto del servicio de Azure y agregue un rol web de PHP según se describe anteriormente en este tema.</span><span class="sxs-lookup"><span data-stu-id="ac769-157">Create an Azure Service project and add a PHP web role as described previously in this topic.</span></span>
2. <span data-ttu-id="ac769-158">Cree una carpeta `php` en la carpeta `bin` que se encuentra en el directorio raíz del rol web y, a continuación, agregue el tiempo de ejecución de PHP (todos los binarios, archivos de configuración, subcarpetas, etc.) a la carpeta `php`.</span><span class="sxs-lookup"><span data-stu-id="ac769-158">Create a `php` folder in the `bin` folder that is in your web role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) to the `php` folder.</span></span>
3. <span data-ttu-id="ac769-159">(OPCIONAL) Si el entorno en tiempo de ejecución de PHP usa los [Controladores de Microsoft para PHP en SQL Server][sqlsrv drivers], tendrá que configurar el rol web para instalar [SQL Server Native Client 2012][sql native client] cuando se aprovisione.</span><span class="sxs-lookup"><span data-stu-id="ac769-159">(OPTIONAL) If your PHP runtime uses the [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need to configure your web role to install [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="ac769-160">Para ello, agregue el [instalador sqlncli.msi x64] a la carpeta `bin` en el directorio raíz del rol web.</span><span class="sxs-lookup"><span data-stu-id="ac769-160">To do this, add the [sqlncli.msi x64 installer] to the `bin` folder in your web role's root directory.</span></span> <span data-ttu-id="ac769-161">El script de inicio descrito en el siguiente paso ejecutará el instalador silenciosamente cuando se aprovisione el rol.</span><span class="sxs-lookup"><span data-stu-id="ac769-161">The startup script described in the next step will silently run the installer when the role is provisioned.</span></span> <span data-ttu-id="ac769-162">Si el tiempo de ejecución de PHP no usa los controladores de Microsoft para PHP en SQL Server, puede eliminar la línea siguiente del script que se muestra en el paso siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac769-162">If your PHP runtime does not use the Microsoft Drivers for PHP for SQL Server, you can remove the following line from the script shown in the next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="ac769-163">Defina una tarea de inicio que configura [Internet Information Services (IIS)][iis.net] para que use el entorno en tiempo de ejecución de PHP a fin de que controle las solicitudes para las páginas `.php`.</span><span class="sxs-lookup"><span data-stu-id="ac769-163">Define a startup task that configures [Internet Information Services (IIS)][iis.net] to use your PHP runtime to handle requests for `.php` pages.</span></span> <span data-ttu-id="ac769-164">Para ello, abra el archivo `setup_web.cmd` (en el archivo `bin` del directorio raíz del rol web) en un editor de texto y reemplace su contenido por el script siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac769-164">To do this, open the `setup_web.cmd` file (in the `bin` file of your web role's root directory) in a text editor and replace its contents with the following script:</span></span>

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
5. <span data-ttu-id="ac769-165">Agregue los archivos de la aplicación al directorio raíz del rol web.</span><span class="sxs-lookup"><span data-stu-id="ac769-165">Add your application files to your web role's root directory.</span></span> <span data-ttu-id="ac769-166">Será el directorio raíz del servidor web.</span><span class="sxs-lookup"><span data-stu-id="ac769-166">This will be the web server's root directory.</span></span>
6. <span data-ttu-id="ac769-167">Publique la aplicación como se describe en la sección [Publicación de la aplicación](#publish-your-application) más adelante.</span><span class="sxs-lookup"><span data-stu-id="ac769-167">Publish your application as described in the [Publish your application](#publish-your-application) section below.</span></span>

> [!NOTE]
> <span data-ttu-id="ac769-168">El script `download.ps1` (en la carpeta `bin` del directorio raíz del rol web) se puede eliminar después de completar los pasos descritos anteriormente para usar el tiempo de ejecución de PHP propio.</span><span class="sxs-lookup"><span data-stu-id="ac769-168">The `download.ps1` script (in the `bin` folder of the web role's root directory) can be deleted after you follow the steps described above for using your own PHP runtime.</span></span>
>
>

### <a name="configure-a-worker-role-to-use-your-own-php-runtime"></a><span data-ttu-id="ac769-169">Configuración de un rol de trabajo para usar un tiempo de ejecución de PHP propio</span><span class="sxs-lookup"><span data-stu-id="ac769-169">Configure a worker role to use your own PHP runtime</span></span>
<span data-ttu-id="ac769-170">Para configurar un rol de trabajo para usar un tiempo de ejecución de PHP propio, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ac769-170">To configure a worker role to use a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="ac769-171">Cree un proyecto del servicio de Azure y agregue un rol de trabajo de PHP según se describe anteriormente en este tema.</span><span class="sxs-lookup"><span data-stu-id="ac769-171">Create an Azure Service project and add a PHP worker role as described previously in this topic.</span></span>
2. <span data-ttu-id="ac769-172">Cree una carpeta `php` en el directorio raíz del rol de trabajo y, a continuación, agregue el tiempo de ejecución de PHP (todos los binarios, archivos de configuración, subcarpetas, etc.) a la carpeta `php`.</span><span class="sxs-lookup"><span data-stu-id="ac769-172">Create a `php` folder in the worker role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) to the `php` folder.</span></span>
3. <span data-ttu-id="ac769-173">.(OPCIONAL) Si el entorno en tiempo de ejecución de PHP usa los [Controladores de Microsoft para PHP en SQL Server][sqlsrv drivers], tendrá que configurar el rol de trabajo para instalar [SQL Server Native Client 2012][sql native client] cuando se aprovisione.</span><span class="sxs-lookup"><span data-stu-id="ac769-173">(OPTIONAL) If your PHP runtime uses [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need to configure your worker role to install [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="ac769-174">Para ello, agregue el [instalador sqlncli.msi x64] al directorio raíz del rol de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ac769-174">To do this, add the [sqlncli.msi x64 installer] to the worker role's root directory.</span></span> <span data-ttu-id="ac769-175">El script de inicio descrito en el siguiente paso ejecutará el instalador silenciosamente cuando se aprovisione el rol.</span><span class="sxs-lookup"><span data-stu-id="ac769-175">The startup script described in the next step will silently run the installer when the role is provisioned.</span></span> <span data-ttu-id="ac769-176">Si el tiempo de ejecución de PHP no usa los controladores de Microsoft para PHP en SQL Server, puede eliminar la línea siguiente del script que se muestra en el paso siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac769-176">If your PHP runtime does not use the Microsoft Drivers for PHP for SQL Server, you can remove the following line from the script shown in the next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="ac769-177">Defina una tarea de inicio que agregue el archivo ejecutable `php.exe` a la variable de entorno PATH del rol de trabajo cuando se aprovisiona el rol.</span><span class="sxs-lookup"><span data-stu-id="ac769-177">Define a startup task that adds your `php.exe` executable to the worker role's PATH environment variable when the role is provisioned.</span></span> <span data-ttu-id="ac769-178">Para ello, abra el archivo `setup_worker.cmd` (en el directorio raíz del rol de trabajo) en un editor de texto y reemplace su contenido por el siguiente script:</span><span class="sxs-lookup"><span data-stu-id="ac769-178">To do this, open the `setup_worker.cmd` file (in the worker role's root directory) in a text editor and replace its contents with the following script:</span></span>

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service to the web root directory...
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
5. <span data-ttu-id="ac769-179">Agregue los archivos de la aplicación al directorio raíz del rol de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ac769-179">Add your application files to your worker role's root directory.</span></span>
6. <span data-ttu-id="ac769-180">Publique la aplicación como se describe en la sección [Publicación de la aplicación](#publish-your-application) más adelante.</span><span class="sxs-lookup"><span data-stu-id="ac769-180">Publish your application as described in the [Publish your application](#publish-your-application) section below.</span></span>

## <a name="run-your-application-in-the-compute-and-storage-emulators"></a><span data-ttu-id="ac769-181">Ejecución de la aplicación en los emuladores de proceso y de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="ac769-181">Run your application in the compute and storage emulators</span></span>
<span data-ttu-id="ac769-182">Los emuladores de Azure ofrecen un entorno local en el que puede probar la aplicación de Azure antes de implementarla en la nube.</span><span class="sxs-lookup"><span data-stu-id="ac769-182">The Azure emulators provide a local environment in which you can test your Azure application before you deploy it to the cloud.</span></span> <span data-ttu-id="ac769-183">Existen algunas diferencias entre los emuladores y el entorno de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac769-183">There are some differences between the emulators and the Azure environment.</span></span> <span data-ttu-id="ac769-184">Para comprender esto mejor, consulte [Uso del emulador de almacenamiento de Azure para desarrollo y pruebas](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="ac769-184">To understand this better, see [Use the Azure storage emulator for development and testing](storage/common/storage-use-emulator.md).</span></span>

<span data-ttu-id="ac769-185">Tenga en cuenta que debe tener instalado PHP localmente para usar el emulador de proceso.</span><span class="sxs-lookup"><span data-stu-id="ac769-185">Note that you must have PHP installed locally to use the compute emulator.</span></span> <span data-ttu-id="ac769-186">El emulador de proceso usará la instalación de PHP local para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ac769-186">The compute emulator will use your local PHP installation to run your application.</span></span>

<span data-ttu-id="ac769-187">Para ejecutar el proyecto en los emuladores, ejecute el comando siguiente desde el directorio raíz del proyecto:</span><span class="sxs-lookup"><span data-stu-id="ac769-187">To run your project in the emulators, execute the following command from your project's root directory:</span></span>

    PS C:\MyProject> Start-AzureEmulator

<span data-ttu-id="ac769-188">Verá una salida similar a esto:</span><span class="sxs-lookup"><span data-stu-id="ac769-188">You will see output similar to this:</span></span>

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

<span data-ttu-id="ac769-189">Puede ver la aplicación en ejecución en el emulador; para ello, abra un explorador web y vaya a la dirección local que aparece en la salida (`http://127.0.0.1:81` en la salida del ejemplo anterior).</span><span class="sxs-lookup"><span data-stu-id="ac769-189">You can see your application running in the emulator by opening a web browser and browsing to the local address shown in the output (`http://127.0.0.1:81` in the example output above).</span></span>

<span data-ttu-id="ac769-190">Para detener los emuladores, ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="ac769-190">To stop the emulators, execute this command:</span></span>

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a><span data-ttu-id="ac769-191">Publicación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="ac769-191">Publish your application</span></span>
<span data-ttu-id="ac769-192">Para publicar la aplicación, primero tiene que importar la configuración de la publicación con el cmdlet [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) .</span><span class="sxs-lookup"><span data-stu-id="ac769-192">To publish your application, you need to first import your publish settings by using the [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span></span> <span data-ttu-id="ac769-193">Después, puede publicar la aplicación con el cmdlet [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) .</span><span class="sxs-lookup"><span data-stu-id="ac769-193">Then you can publish your application by using the [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span></span> <span data-ttu-id="ac769-194">Para obtener información sobre cómo iniciar sesión, consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ac769-194">For information about signing in, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac769-195">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ac769-195">Next steps</span></span>
<span data-ttu-id="ac769-196">Para obtener más información, consulte el [Centro para desarrolladores de PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="ac769-196">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

[SDK de Azure para PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[definición del servicio (.csdef)]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[configuración del servicio (.cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[instalador sqlncli.msi x64]: http://go.microsoft.com/fwlink/?LinkID=239648
