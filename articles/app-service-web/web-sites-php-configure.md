---
title: "aaaConfigure PHP en aplicaciones de Web del servicio de aplicación de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure Hola instalación de PHP predeterminado o agregar una instalación de PHP personalizada para las aplicaciones Web en el servicio de aplicación de Azure."
services: app-service
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 95c4072b-8570-496b-9c48-ee21a223fb60
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 2e461e4a269a4ce5614f5f05560f38bc53066251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-php-in-azure-app-service-web-apps"></a><span data-ttu-id="f4927-103">Configuración de PHP en Aplicaciones web del Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="f4927-103">Configure PHP in Azure App Service Web Apps</span></span>
## <a name="introduction"></a><span data-ttu-id="f4927-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="f4927-104">Introduction</span></span>
<span data-ttu-id="f4927-105">Esta guía le mostrará cómo tooconfigure Hola integrado en tiempo de ejecución PHP para las aplicaciones Web en [servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714), proporcione un tiempo de ejecución PHP personalizado y habilitar las extensiones.</span><span class="sxs-lookup"><span data-stu-id="f4927-105">This guide will show you how tooconfigure hello built-in PHP runtime for Web Apps in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), provide a custom PHP runtime, and enable extensions.</span></span> <span data-ttu-id="f4927-106">toouse servicio de aplicaciones, regístrese para hello [evaluación gratuita].</span><span class="sxs-lookup"><span data-stu-id="f4927-106">toouse App Service, sign up for hello [free trial].</span></span> <span data-ttu-id="f4927-107">Hola tooget más de esta guía, primero debe crear una aplicación web PHP en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f4927-107">tooget hello most from this guide, you should first create a PHP web app in App Service.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-hello-built-in-php-version"></a><span data-ttu-id="f4927-108">Cómo: cambiar versión PHP de integrados de Hola</span><span class="sxs-lookup"><span data-stu-id="f4927-108">How to: Change hello built-in PHP version</span></span>
<span data-ttu-id="f4927-109">PHP 5.5 está instalado de forma predeterminada y está disponible para utilizarse inmediatamente después de crear una aplicación web de App Service.</span><span class="sxs-lookup"><span data-stu-id="f4927-109">By default, PHP 5.5 is installed and immediately available for use when you create an App Service web app.</span></span> <span data-ttu-id="f4927-110">Hola mejor manera toosee Hola versión disponible "revisión", su configuración predeterminada, y extensiones habilitadas hello es un script que llame hello toodeploy [phpinfo()] (función).</span><span class="sxs-lookup"><span data-stu-id="f4927-110">hello best way toosee hello available release revision, its default configuration, and hello enabled extensions is toodeploy a script that calls hello [phpinfo()] function.</span></span>

<span data-ttu-id="f4927-111">Las versiones de PHP 5.6 y PHP 7.0 también están disponibles, pero no están habilitadas de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f4927-111">PHP 5.6 and PHP 7.0 versions are also available, but not enabled by default.</span></span> <span data-ttu-id="f4927-112">Hola tooupdate versión PHP, siga uno de estos métodos:</span><span class="sxs-lookup"><span data-stu-id="f4927-112">tooupdate hello PHP version, follow one of these methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="f4927-113">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f4927-113">Azure Portal</span></span>
1. <span data-ttu-id="f4927-114">Examinar la aplicación web de tooyour en hello [Portal de Azure](https://portal.azure.com) y haga clic en hello **configuración** botón.</span><span class="sxs-lookup"><span data-stu-id="f4927-114">Browse tooyour web app in hello [Azure Portal](https://portal.azure.com) and click on hello **Settings** button.</span></span>
   
    ![Configuración de aplicaciones web][settings-button]
2. <span data-ttu-id="f4927-116">De hello **configuración** seleccione hoja **configuración de la aplicación** y elija la nueva versión PHP Hola.</span><span class="sxs-lookup"><span data-stu-id="f4927-116">From hello **Settings** blade select **Application Settings** and choose hello new PHP version.</span></span>
   
    ![Configuración de la aplicación][application-settings]
3. <span data-ttu-id="f4927-118">Haga clic en hello **guardar** situado en la parte superior de Hola de hello **configuración de aplicación Web** hoja.</span><span class="sxs-lookup"><span data-stu-id="f4927-118">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Guardar la configuración][save-button]

### <a name="azure-powershell-windows"></a><span data-ttu-id="f4927-120">Azure PowerShell (Windows)</span><span class="sxs-lookup"><span data-stu-id="f4927-120">Azure PowerShell (Windows)</span></span>
1. <span data-ttu-id="f4927-121">Abra PowerShell de Azure y la cuenta de inicio de sesión tooyour:</span><span class="sxs-lookup"><span data-stu-id="f4927-121">Open Azure PowerShell, and login tooyour account:</span></span>
   
        PS C:\> Login-AzureRmAccount
2. <span data-ttu-id="f4927-122">Establezca la versión de PHP de hello para la aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4927-122">Set hello PHP version for hello web app.</span></span>
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. <span data-ttu-id="f4927-123">Ahora se establece la versión de PHP Hola.</span><span class="sxs-lookup"><span data-stu-id="f4927-123">hello PHP version is now set.</span></span> <span data-ttu-id="f4927-124">Puede confirmar esta configuración:</span><span class="sxs-lookup"><span data-stu-id="f4927-124">You can confirm these settings:</span></span>
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a><span data-ttu-id="f4927-125">Interfaz de línea de comandos de Azure (Linux, Mac, Windows)</span><span class="sxs-lookup"><span data-stu-id="f4927-125">Azure Command-Line Interface (Linux, Mac, Windows)</span></span>
<span data-ttu-id="f4927-126">toouse Hola interfaz de línea de comandos de Azure, debe tener **Node.js** instalados en su equipo.</span><span class="sxs-lookup"><span data-stu-id="f4927-126">toouse hello Azure Command-Line Interface, you must have **Node.js** installed on your computer.</span></span>

1. <span data-ttu-id="f4927-127">Abrir Terminal y la cuenta de inicio de sesión tooyour.</span><span class="sxs-lookup"><span data-stu-id="f4927-127">Open Terminal, and login tooyour account.</span></span>
   
        azure login
2. <span data-ttu-id="f4927-128">Establezca la versión de PHP de hello para la aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4927-128">Set hello PHP version for hello web app.</span></span>
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. <span data-ttu-id="f4927-129">Ahora se establece la versión de PHP Hola.</span><span class="sxs-lookup"><span data-stu-id="f4927-129">hello PHP version is now set.</span></span> <span data-ttu-id="f4927-130">Puede confirmar esta configuración:</span><span class="sxs-lookup"><span data-stu-id="f4927-130">You can confirm these settings:</span></span>
   
        azure site show {app-name}

> [!NOTE] 
> <span data-ttu-id="f4927-131">Hola [CLI de Azure 2.0](https://github.com/Azure/azure-cli) son comandos que son equivalente toohello anterior:</span><span class="sxs-lookup"><span data-stu-id="f4927-131">hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands that are equivalent toohello above are:</span></span>
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-hello-built-in-php-configurations"></a><span data-ttu-id="f4927-132">Cómo: cambiar las configuraciones de PHP integradas Hola</span><span class="sxs-lookup"><span data-stu-id="f4927-132">How to: Change hello built-in PHP configurations</span></span>
<span data-ttu-id="f4927-133">Para cualquier tiempo de ejecución PHP integrado, puede cambiar cualquiera de las opciones de configuración de hello siguiendo estos pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="f4927-133">For any built-in PHP runtime, you can change any of hello configuration options by following hello steps below.</span></span> <span data-ttu-id="f4927-134">(Para obtener información acerca de las directivas, consulte la [lista de directivas de php.ini]).</span><span class="sxs-lookup"><span data-stu-id="f4927-134">(For information about php.ini directives, see [List of php.ini directives].)</span></span>

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a><span data-ttu-id="f4927-135">Cambio de PHP\_INI\_USUARIO, PHP\_INI\_PERDIR, PHP\_INI\_todas LAS opciones de configuración</span><span class="sxs-lookup"><span data-stu-id="f4927-135">Changing PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL configuration settings</span></span>
1. <span data-ttu-id="f4927-136">Agregar un [. user.ini] directorio raíz del archivo tooyour.</span><span class="sxs-lookup"><span data-stu-id="f4927-136">Add a [.user.ini] file tooyour root directory.</span></span>
2. <span data-ttu-id="f4927-137">Agregar configuración configuración toohello `.user.ini` archivo utilizando Hola la misma sintaxis que se usan en un `php.ini` archivo.</span><span class="sxs-lookup"><span data-stu-id="f4927-137">Add configuration settings toohello `.user.ini` file using hello same syntax you would use in a `php.ini` file.</span></span> <span data-ttu-id="f4927-138">Por ejemplo, si deseara hello tooturn `display_errors` configuración y defina `upload_max_filesize` configuración too10M, su `.user.ini` archivo contendría este texto:</span><span class="sxs-lookup"><span data-stu-id="f4927-138">For example, if you wanted tooturn hello `display_errors` setting on and set `upload_max_filesize` setting too10M, your `.user.ini` file would contain this text:</span></span>
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on toowrite errors tood:\home\LogFiles\php_errors.log
        ; log_errors=On
3. <span data-ttu-id="f4927-139">Implemente la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="f4927-139">Deploy your web app.</span></span>
4. <span data-ttu-id="f4927-140">Reinicie la aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="f4927-140">Restart hello web app.</span></span> <span data-ttu-id="f4927-141">(Es necesario reiniciar debido a que lee de la frecuencia de hello con qué PHP `.user.ini` archivos se rige por hello `user_ini.cache_ttl` configuración, que es una configuración de nivel de sistema y es de 300 segundos (5 minutos) de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f4927-141">(Restarting is necessary because hello frequency with which PHP reads `.user.ini` files is governed by hello `user_ini.cache_ttl` setting, which is a system level setting and is 300 seconds (5 minutes) by default.</span></span> <span data-ttu-id="f4927-142">Reiniciar aplicación web de hello fuerza las nuevas opciones de hello del tooread PHP en hello `.user.ini` archivo.)</span><span class="sxs-lookup"><span data-stu-id="f4927-142">Restarting hello web app forces PHP tooread hello new settings in hello `.user.ini` file.)</span></span>

<span data-ttu-id="f4927-143">Como una alternativa toousing una `.user.ini` archivo, puede usar hello [ini_set()] función en Opciones de configuración de tooset de secuencias de comandos que no son directivas de nivel de sistema.</span><span class="sxs-lookup"><span data-stu-id="f4927-143">As an alternative toousing a `.user.ini` file, you can use hello [ini_set()] function in scripts tooset configuration options that are not system-level directives.</span></span>

### <a name="changing-phpinisystem-configuration-settings"></a><span data-ttu-id="f4927-144">Cambiar la configuración de PHP\_INI\_SYSTEM</span><span class="sxs-lookup"><span data-stu-id="f4927-144">Changing PHP\_INI\_SYSTEM configuration settings</span></span>
1. <span data-ttu-id="f4927-145">Agregar un tooyour de configuración de la aplicación Web App con la clave de hello `PHP_INI_SCAN_DIR` y valor`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="f4927-145">Add an App Setting tooyour Web App with hello key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
2. <span data-ttu-id="f4927-146">Crear un `settings.ini` archivo mediante la consola de Kudu (http://&lt;nombre del sitio&gt;. scm.azurewebsite.net) en hello `d:\home\site\ini` directory.</span><span class="sxs-lookup"><span data-stu-id="f4927-146">Create an `settings.ini` file using Kudu Console (http://&lt;site-name&gt;.scm.azurewebsite.net) in hello `d:\home\site\ini` directory.</span></span>
3. <span data-ttu-id="f4927-147">Agregar configuración configuración toohello `settings.ini` archivo utilizando Hola la misma sintaxis que se usan en un archivo php.ini.</span><span class="sxs-lookup"><span data-stu-id="f4927-147">Add configuration settings toohello `settings.ini` file using hello same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="f4927-148">Por ejemplo, si deseara hello toopoint `curl.cainfo` configuración tooa `*.crt` de archivos y establezca 'wincache.maxfilesize' establecer too512K, su `settings.ini` archivo contendría este texto:</span><span class="sxs-lookup"><span data-stu-id="f4927-148">For example, if you wanted toopoint hello `curl.cainfo` setting tooa `*.crt` file and set 'wincache.maxfilesize' setting too512K, your `settings.ini` file would contain this text:</span></span>
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. <span data-ttu-id="f4927-149">Reinicie los cambios de hello tooload de aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="f4927-149">Restart your Web App tooload hello changes.</span></span>

## <a name="how-to-enable-extensions-in-hello-default-php-runtime"></a><span data-ttu-id="f4927-150">Cómo: habilitar extensiones en tiempo de ejecución PHP Hola predeterminado</span><span class="sxs-lookup"><span data-stu-id="f4927-150">How to: Enable extensions in hello default PHP runtime</span></span>
<span data-ttu-id="f4927-151">Como se indicó en la sección anterior de hello, versión de PHP de hello mejor manera toosee Hola de forma predeterminada, su configuración predeterminada y Hola habilitado las extensiones son toodeploy un script que llame [phpinfo()].</span><span class="sxs-lookup"><span data-stu-id="f4927-151">As noted in hello previous section, hello best way toosee hello default PHP version, its default configuration, and hello enabled extensions is toodeploy a script that calls [phpinfo()].</span></span> <span data-ttu-id="f4927-152">tooenable extensiones adicionales, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="f4927-152">tooenable additional extensions, follow hello steps below:</span></span>

### <a name="configure-via-ini-settings"></a><span data-ttu-id="f4927-153">Configurar mediante configuración de ini</span><span class="sxs-lookup"><span data-stu-id="f4927-153">Configure via ini settings</span></span>
1. <span data-ttu-id="f4927-154">Agregar un `ext` toohello directorio `d:\home\site` directorio.</span><span class="sxs-lookup"><span data-stu-id="f4927-154">Add a `ext` directory toohello `d:\home\site` directory.</span></span>
2. <span data-ttu-id="f4927-155">Colocar `.dll` archivos de extensión de hello `ext` directorio (por ejemplo, `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="f4927-155">Put `.dll` extension files in hello `ext` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="f4927-156">Asegúrese de que las extensiones de hello son compatibles con la versión predeterminada de PHP y son VC9 y compatible no subprocesos (nts).</span><span class="sxs-lookup"><span data-stu-id="f4927-156">Make sure that hello extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="f4927-157">Agregar un tooyour de configuración de la aplicación Web App con la clave de hello `PHP_INI_SCAN_DIR` y valor`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="f4927-157">Add an App Setting tooyour Web App with hello key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
4. <span data-ttu-id="f4927-158">Cree un archivo `ini` en `d:\home\site\ini` denominado `extensions.ini`.</span><span class="sxs-lookup"><span data-stu-id="f4927-158">Create an `ini` file in `d:\home\site\ini` called `extensions.ini`.</span></span>
5. <span data-ttu-id="f4927-159">Agregar configuración configuración toohello `extensions.ini` archivo utilizando Hola la misma sintaxis que se usan en un archivo php.ini.</span><span class="sxs-lookup"><span data-stu-id="f4927-159">Add configuration settings toohello `extensions.ini` file using hello same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="f4927-160">Por ejemplo, si deseara tooenable Hola MongoDB y XDebug las extensiones, su `extensions.ini` archivo contendría este texto:</span><span class="sxs-lookup"><span data-stu-id="f4927-160">For example, if you wanted tooenable hello MongoDB and XDebug extensions, your `extensions.ini` file would contain this text:</span></span>
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. <span data-ttu-id="f4927-161">Reinicie los cambios de hello tooload de aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="f4927-161">Restart your Web App tooload hello changes.</span></span>

### <a name="configure-via-app-setting"></a><span data-ttu-id="f4927-162">Configurar a través de la configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="f4927-162">Configure via App Setting</span></span>
1. <span data-ttu-id="f4927-163">Agregar un `bin` directorio raíz de toohello.</span><span class="sxs-lookup"><span data-stu-id="f4927-163">Add a `bin` directory toohello root directory.</span></span>
2. <span data-ttu-id="f4927-164">Colocar `.dll` archivos de extensión de hello `bin` directorio (por ejemplo, `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="f4927-164">Put `.dll` extension files in hello `bin` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="f4927-165">Asegúrese de que las extensiones de hello son compatibles con la versión predeterminada de PHP y son VC9 y compatible no subprocesos (nts).</span><span class="sxs-lookup"><span data-stu-id="f4927-165">Make sure that hello extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="f4927-166">Implemente la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="f4927-166">Deploy your web app.</span></span>
4. <span data-ttu-id="f4927-167">Aplicación web de tooyour Hola Portal de Azure y haga clic en hello **configuración** botón.</span><span class="sxs-lookup"><span data-stu-id="f4927-167">Browse tooyour web app in hello Azure Portal and click on hello **Settings** button.</span></span>
   
    ![Configuración de aplicaciones web][settings-button]
5. <span data-ttu-id="f4927-169">De hello **configuración** seleccione hoja **configuración de la aplicación** y desplácese toohello **configuración de la aplicación** sección.</span><span class="sxs-lookup"><span data-stu-id="f4927-169">From hello **Settings** blade select **Application Settings** and scroll toohello **App settings** section.</span></span>
6. <span data-ttu-id="f4927-170">Hola **configuración de la aplicación** , debe crearse un **PHP_EXTENSIONS** clave.</span><span class="sxs-lookup"><span data-stu-id="f4927-170">In hello **App settings** section, create a **PHP_EXTENSIONS** key.</span></span> <span data-ttu-id="f4927-171">valor de Hola para esta clave sería una raíz de ruta de acceso relativa toowebsite: **bin\your-ext-file**.</span><span class="sxs-lookup"><span data-stu-id="f4927-171">hello value for this key would be a path relative toowebsite root: **bin\your-ext-file**.</span></span>
   
    ![Habilitar extensiones en app settings][php-extensions]
7. <span data-ttu-id="f4927-173">Haga clic en hello **guardar** situado en la parte superior de Hola de hello **configuración de aplicación Web** hoja.</span><span class="sxs-lookup"><span data-stu-id="f4927-173">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Guardar la configuración][save-button]

<span data-ttu-id="f4927-175">También se pueden usar las extensiones Zend mediante una clave **PHP_ZENDEXTENSIONS**.</span><span class="sxs-lookup"><span data-stu-id="f4927-175">Zend extensions are also supported by using a **PHP_ZENDEXTENSIONS** key.</span></span> <span data-ttu-id="f4927-176">tooenable varias extensiones, incluye una lista separada por comas de `.dll` archivos para el valor de configuración de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="f4927-176">tooenable multiple extensions, include a comma-separated list of `.dll` files for hello app setting value.</span></span>

## <a name="how-to-use-a-custom-php-runtime"></a><span data-ttu-id="f4927-177">Cómo: Usar un tiempo de ejecución de PHP personalizado</span><span class="sxs-lookup"><span data-stu-id="f4927-177">How to: Use a custom PHP runtime</span></span>
<span data-ttu-id="f4927-178">En lugar de hello tiempo de ejecución PHP de forma predeterminada, las aplicaciones de servicio Web de aplicación puede usar un tiempo de ejecución PHP que proporcione tooexecute scripts PHP.</span><span class="sxs-lookup"><span data-stu-id="f4927-178">Instead of hello default PHP runtime, App Service Web Apps can use a PHP runtime that you provide tooexecute PHP scripts.</span></span> <span data-ttu-id="f4927-179">se puede configurar en tiempo de ejecución de Hola que proporcione un `php.ini` archivo también proporcionado.</span><span class="sxs-lookup"><span data-stu-id="f4927-179">hello runtime that you provide can be configured by a `php.ini` file that you also provide.</span></span> <span data-ttu-id="f4927-180">toouse un tiempo de ejecución PHP personalizada con aplicaciones Web, siga estos pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="f4927-180">toouse a custom PHP runtime with Web Apps, follow hello steps below.</span></span>

1. <span data-ttu-id="f4927-181">Obtenga una versión compatible con VC9 y VC11 no segura para subprocesos de PHP para Windows.</span><span class="sxs-lookup"><span data-stu-id="f4927-181">Obtain a non-thread-safe, VC9 or VC11 compatible version of PHP for Windows.</span></span> <span data-ttu-id="f4927-182">Las versiones recientes de PHP para Windows se pueden encontrar aquí: [http://windows.php.net/download/].</span><span class="sxs-lookup"><span data-stu-id="f4927-182">Recent releases of PHP for Windows can be found here: [http://windows.php.net/download/].</span></span> <span data-ttu-id="f4927-183">Las versiones anteriores pueden encontrarse en el archivo de hello aquí: [http://windows.php.net/downloads/releases/archives/].</span><span class="sxs-lookup"><span data-stu-id="f4927-183">Older releases can be found in hello archive here: [http://windows.php.net/downloads/releases/archives/].</span></span>
2. <span data-ttu-id="f4927-184">Modificar hello `php.ini` archivo para el tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="f4927-184">Modify hello `php.ini` file for your runtime.</span></span> <span data-ttu-id="f4927-185">Tenga en cuenta que Aplicaciones web omitirá cualquier configuración que se corresponda con directivas que sean solo de nivel de sistema.</span><span class="sxs-lookup"><span data-stu-id="f4927-185">Note that any configuration settings that are system-level-only directives will be ignored by Web Apps.</span></span> <span data-ttu-id="f4927-186">(Para obtener información acerca de las directivas solo a nivel de sistema, consulte la [lista de directivas de php.ini]).</span><span class="sxs-lookup"><span data-stu-id="f4927-186">(For information about system-level-only directives, see [List of php.ini directives]).</span></span>
3. <span data-ttu-id="f4927-187">Si lo desea, agregar en tiempo de ejecución de las extensiones tooyour PHP y habilitarlas en hello `php.ini` archivo.</span><span class="sxs-lookup"><span data-stu-id="f4927-187">Optionally, add extensions tooyour PHP runtime and enable them in hello `php.ini` file.</span></span>
4. <span data-ttu-id="f4927-188">Agregar un `bin` directorio raíz de tooyour y directorio de hello put que contiene el tiempo de ejecución PHP en él (por ejemplo, `bin\php`).</span><span class="sxs-lookup"><span data-stu-id="f4927-188">Add a `bin` directory tooyour root directory, and put hello directory that contains your PHP runtime in it (for example, `bin\php`).</span></span>
5. <span data-ttu-id="f4927-189">Implemente la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="f4927-189">Deploy your web app.</span></span>
6. <span data-ttu-id="f4927-190">Aplicación web de tooyour Hola Portal de Azure y haga clic en hello **configuración** botón.</span><span class="sxs-lookup"><span data-stu-id="f4927-190">Browse tooyour web app in hello Azure Portal and click on hello **Settings** button.</span></span>
   
    ![Configuración de aplicaciones web][settings-button]
7. <span data-ttu-id="f4927-192">De hello **configuración** seleccione hoja **configuración de la aplicación** y desplácese toohello **asignaciones de controlador** sección.</span><span class="sxs-lookup"><span data-stu-id="f4927-192">From hello **Settings** blade select **Application Settings** and scroll toohello **Handler mappings** section.</span></span> <span data-ttu-id="f4927-193">Agregar `*.php` toohello extensión campo y agregar toohello de ruta de acceso de hello `php-cgi.exe` ejecutable.</span><span class="sxs-lookup"><span data-stu-id="f4927-193">Add `*.php` toohello Extension field and add hello path toohello `php-cgi.exe` executable.</span></span> <span data-ttu-id="f4927-194">Si coloca el tiempo de ejecución PHP en hello `bin` directorio en hello raíz de su aplicación, ruta de acceso de hello será `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span><span class="sxs-lookup"><span data-stu-id="f4927-194">If you put your PHP runtime in hello `bin` directory in hello root of you application, hello path will be `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span></span>
   
    ![Especificar el controlador en hander mappings][handler-mappings]
8. <span data-ttu-id="f4927-196">Haga clic en hello **guardar** situado en la parte superior de Hola de hello **configuración de aplicación Web** hoja.</span><span class="sxs-lookup"><span data-stu-id="f4927-196">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Guardar la configuración][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a><span data-ttu-id="f4927-198">Procedimiento para habilitar la automatización de Composer en Azure</span><span class="sxs-lookup"><span data-stu-id="f4927-198">How to: Enable Composer automation in Azure</span></span>
<span data-ttu-id="f4927-199">De forma predeterminada, el Servicio de aplicaciones no responde con composer.json, si tiene uno en el proyecto PHP.</span><span class="sxs-lookup"><span data-stu-id="f4927-199">By default, App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="f4927-200">Si usa [Git implementación](app-service-deploy-local-git.md), puede habilitar composer.json procesamiento durante `git push` habilitando la extensión de hello compositor.</span><span class="sxs-lookup"><span data-stu-id="f4927-200">If you use [Git deployment](app-service-deploy-local-git.md), you can enable composer.json processing during `git push` by enabling hello Composer extension.</span></span>

> [!NOTE]
> <span data-ttu-id="f4927-201">Aquí puede [votar por soporte técnico de primera clase para Composer en el Servicio de aplicaciones](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip).</span><span class="sxs-lookup"><span data-stu-id="f4927-201">You can [vote for first-class Composer support in App Service here](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span></span>
> 
> 

1. <span data-ttu-id="f4927-202">En su PHP web hoja de la aplicación Hola [portal de Azure](https://portal.azure.com), haga clic en **herramientas** > **extensiones**.</span><span class="sxs-lookup"><span data-stu-id="f4927-202">In your PHP web app's blade in hello [Azure portal](https://portal.azure.com), click **Tools** > **Extensions**.</span></span>
   
    ![Tooenable de hoja de configuración de Portal Azure automatización compositor en Azure](./media/web-sites-php-configure/composer-extension-settings.png)
2. <span data-ttu-id="f4927-204">Haga clic en **Agregar** y, luego, en **Compositor**.</span><span class="sxs-lookup"><span data-stu-id="f4927-204">Click **Add**, then click **Composer**.</span></span>
   
    ![Agregar automatización Compositor de compositor extensión tooenable en Azure](./media/web-sites-php-configure/composer-extension-add.png)
3. <span data-ttu-id="f4927-206">Haga clic en **Aceptar** tooaccept los términos legales.</span><span class="sxs-lookup"><span data-stu-id="f4927-206">Click **OK** tooaccept legal terms.</span></span> <span data-ttu-id="f4927-207">Haga clic en **Aceptar** extensión Hola de tooadd nuevo.</span><span class="sxs-lookup"><span data-stu-id="f4927-207">Click **OK** again tooadd hello extension.</span></span>
   
    <span data-ttu-id="f4927-208">Hola **extensiones instaladas** hoja mostrará ahora la extensión del compositor de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4927-208">hello **Installed extensions** blade will now show hello Composer extension.</span></span>  
    <span data-ttu-id="f4927-209">![Acepte la automatización de Compositor de tooenable condiciones legales en Azure](./media/web-sites-php-configure/composer-extension-view.png)</span><span class="sxs-lookup"><span data-stu-id="f4927-209">![Accept legal terms tooenable Composer automation in Azure](./media/web-sites-php-configure/composer-extension-view.png)</span></span>
4. <span data-ttu-id="f4927-210">Ahora, realizar `git add`, `git commit`, y `git push` al igual que en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4927-210">Now, perform `git add`, `git commit`, and `git push` like in hello previous section.</span></span> <span data-ttu-id="f4927-211">Verá que Composer está instalando las dependencias definidas en composer.json.</span><span class="sxs-lookup"><span data-stu-id="f4927-211">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Implementación de GIT con la automatización de Composer en Azure](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a><span data-ttu-id="f4927-213">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f4927-213">Next steps</span></span>
<span data-ttu-id="f4927-214">Para obtener más información, vea hello [Centro para desarrolladores de PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="f4927-214">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

> [!NOTE]
> <span data-ttu-id="f4927-215">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f4927-215">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f4927-216">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="f4927-216">No credit cards required; no commitments.</span></span>
> 
> 

[evaluación gratuita]: https://www.windowsazure.com/pricing/free-trial/
[phpinfo()]: http://php.net/manual/en/function.phpinfo.php
[select-php-version]: ./media/web-sites-php-configure/select-php-version.png
[lista de directivas de php.ini]: http://www.php.net/manual/en/ini.list.php
[. user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php
[ini_set()]: http://www.php.net/manual/en/function.ini-set.php
[application-settings]: ./media/web-sites-php-configure/application-settings.png
[settings-button]: ./media/web-sites-php-configure/settings-button.png
[save-button]: ./media/web-sites-php-configure/save-button.png
[php-extensions]: ./media/web-sites-php-configure/php-extensions.png
[handler-mappings]: ./media/web-sites-php-configure/handler-mappings.png
[http://windows.php.net/download/]: http://windows.php.net/download/
[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/
[SETPHPVERCLI]: ./media/web-sites-php-configure/ChangePHPVersion-XPlatCLI.png
[GETPHPVERCLI]: ./media/web-sites-php-configure/ShowPHPVersion-XplatCLI.png
[SETPHPVERPS]: ./media/web-sites-php-configure/ChangePHPVersion-PS.png
[GETPHPVERPS]: ./media/web-sites-php-configure/ShowPHPVersion-PS.png

