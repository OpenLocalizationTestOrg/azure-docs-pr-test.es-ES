---
title: "Configuración de PHP en Azure App Service Web Apps | Microsoft Docs"
description: "Obtenga información acerca de cómo configurar la instalación de PHP predeterminada o agregar una instalación de PHP personalizada para Aplicaciones web en el Servicio de aplicaciones de Azure."
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
ms.openlocfilehash: 624dd416f37aacdb3d2f6e59afdc2efe646e610b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-php-in-azure-app-service-web-apps"></a><span data-ttu-id="45012-103">Configuración de PHP en Aplicaciones web del Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="45012-103">Configure PHP in Azure App Service Web Apps</span></span>
## <a name="introduction"></a><span data-ttu-id="45012-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="45012-104">Introduction</span></span>
<span data-ttu-id="45012-105">En esta guía se explica cómo configurar el tiempo de ejecución de PHP integrado en Aplicaciones web en el [Servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714), ofrecer un tiempo de ejecución de PHP personalizado y habilitar extensiones.</span><span class="sxs-lookup"><span data-stu-id="45012-105">This guide will show you how to configure the built-in PHP runtime for Web Apps in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), provide a custom PHP runtime, and enable extensions.</span></span> <span data-ttu-id="45012-106">Para utilizar el Servicio de aplicaciones, regístrese para obtener acceso a la [evaluación gratuita].</span><span class="sxs-lookup"><span data-stu-id="45012-106">To use App Service, sign up for the [free trial].</span></span> <span data-ttu-id="45012-107">Para obtener el máximo partido de esta guía, primero debe crear una aplicación web PHP en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="45012-107">To get the most from this guide, you should first create a PHP web app in App Service.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-the-built-in-php-version"></a><span data-ttu-id="45012-108">Cómo: Cambiar la versión de PHP integrada</span><span class="sxs-lookup"><span data-stu-id="45012-108">How to: Change the built-in PHP version</span></span>
<span data-ttu-id="45012-109">PHP 5.5 está instalado de forma predeterminada y está disponible para utilizarse inmediatamente después de crear una aplicación web de App Service.</span><span class="sxs-lookup"><span data-stu-id="45012-109">By default, PHP 5.5 is installed and immediately available for use when you create an App Service web app.</span></span> <span data-ttu-id="45012-110">La mejor forma de ver la revisión publicada disponible, su configuración predeterminada y las extensiones habilitadas es implementando un script que llame a la función [phpinfo()] .</span><span class="sxs-lookup"><span data-stu-id="45012-110">The best way to see the available release revision, its default configuration, and the enabled extensions is to deploy a script that calls the [phpinfo()] function.</span></span>

<span data-ttu-id="45012-111">Las versiones de PHP 5.6 y PHP 7.0 también están disponibles, pero no están habilitadas de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="45012-111">PHP 5.6 and PHP 7.0 versions are also available, but not enabled by default.</span></span> <span data-ttu-id="45012-112">Para actualizar la versión de PHP, siga uno de estos métodos:</span><span class="sxs-lookup"><span data-stu-id="45012-112">To update the PHP version, follow one of these methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="45012-113">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="45012-113">Azure Portal</span></span>
1. <span data-ttu-id="45012-114">Vaya a la aplicación web en el [Portal de Azure](https://portal.azure.com) y haga clic en el botón **Configuración** .</span><span class="sxs-lookup"><span data-stu-id="45012-114">Browse to your web app in the [Azure Portal](https://portal.azure.com) and click on the **Settings** button.</span></span>
   
    ![Configuración de aplicaciones web][settings-button]
2. <span data-ttu-id="45012-116">En la hoja **Configuración**, seleccione **Configuración de la aplicación** y elija la nueva versión de PHP.</span><span class="sxs-lookup"><span data-stu-id="45012-116">From the **Settings** blade select **Application Settings** and choose the new PHP version.</span></span>
   
    ![Configuración de la aplicación][application-settings]
3. <span data-ttu-id="45012-118">Haga clic en el botón **Guardar**, situado en la parte superior de la hoja **Configuración de aplicaciones web**.</span><span class="sxs-lookup"><span data-stu-id="45012-118">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![Guardar la configuración][save-button]

### <a name="azure-powershell-windows"></a><span data-ttu-id="45012-120">Azure PowerShell (Windows)</span><span class="sxs-lookup"><span data-stu-id="45012-120">Azure PowerShell (Windows)</span></span>
1. <span data-ttu-id="45012-121">Abra Azure PowerShell e inicie sesión en su cuenta:</span><span class="sxs-lookup"><span data-stu-id="45012-121">Open Azure PowerShell, and login to your account:</span></span>
   
        PS C:\> Login-AzureRmAccount
2. <span data-ttu-id="45012-122">Establezca la versión PHP para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="45012-122">Set the PHP version for the web app.</span></span>
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. <span data-ttu-id="45012-123">La versión de PHP ya está configurada.</span><span class="sxs-lookup"><span data-stu-id="45012-123">The PHP version is now set.</span></span> <span data-ttu-id="45012-124">Puede confirmar esta configuración:</span><span class="sxs-lookup"><span data-stu-id="45012-124">You can confirm these settings:</span></span>
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a><span data-ttu-id="45012-125">Interfaz de línea de comandos de Azure (Linux, Mac, Windows)</span><span class="sxs-lookup"><span data-stu-id="45012-125">Azure Command-Line Interface (Linux, Mac, Windows)</span></span>
<span data-ttu-id="45012-126">Para usar la interfaz de línea de comandos de Azure, debe tener **Node.js** instalado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="45012-126">To use the Azure Command-Line Interface, you must have **Node.js** installed on your computer.</span></span>

1. <span data-ttu-id="45012-127">Abra Terminal e inicie sesión en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="45012-127">Open Terminal, and login to your account.</span></span>
   
        azure login
2. <span data-ttu-id="45012-128">Establezca la versión PHP para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="45012-128">Set the PHP version for the web app.</span></span>
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. <span data-ttu-id="45012-129">La versión de PHP ya está configurada.</span><span class="sxs-lookup"><span data-stu-id="45012-129">The PHP version is now set.</span></span> <span data-ttu-id="45012-130">Puede confirmar esta configuración:</span><span class="sxs-lookup"><span data-stu-id="45012-130">You can confirm these settings:</span></span>
   
        azure site show {app-name}

> [!NOTE] 
> <span data-ttu-id="45012-131">Estos son los comandos de la [CLI de Azure 2.0](https://github.com/Azure/azure-cli) equivalentes a lo anterior:</span><span class="sxs-lookup"><span data-stu-id="45012-131">The [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands that are equivalent to the above are:</span></span>
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-the-built-in-php-configurations"></a><span data-ttu-id="45012-132">Cómo: Cambiar las configuraciones de PHP integradas</span><span class="sxs-lookup"><span data-stu-id="45012-132">How to: Change the built-in PHP configurations</span></span>
<span data-ttu-id="45012-133">En todos los tiempos de ejecución de PHP integrados es posible cambiar las opciones de configuración siguiendo los pasos que se indican a continuación.</span><span class="sxs-lookup"><span data-stu-id="45012-133">For any built-in PHP runtime, you can change any of the configuration options by following the steps below.</span></span> <span data-ttu-id="45012-134">(Para obtener información acerca de las directivas, consulte la [lista de directivas de php.ini]).</span><span class="sxs-lookup"><span data-stu-id="45012-134">(For information about php.ini directives, see [List of php.ini directives].)</span></span>

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a><span data-ttu-id="45012-135">Cambio de PHP\_INI\_USUARIO, PHP\_INI\_PERDIR, PHP\_INI\_todas LAS opciones de configuración</span><span class="sxs-lookup"><span data-stu-id="45012-135">Changing PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL configuration settings</span></span>
1. <span data-ttu-id="45012-136">Agregue un archivo [.user.ini] al directorio raíz.</span><span class="sxs-lookup"><span data-stu-id="45012-136">Add a [.user.ini] file to your root directory.</span></span>
2. <span data-ttu-id="45012-137">Agregue la configuración al archivo `.user.ini` usando la misma sintaxis que usaría en un archivo `php.ini`.</span><span class="sxs-lookup"><span data-stu-id="45012-137">Add configuration settings to the `.user.ini` file using the same syntax you would use in a `php.ini` file.</span></span> <span data-ttu-id="45012-138">Por ejemplo, si desea activar la configuración `display_errors` y configurar `upload_max_filesize` como 10M, el archivo `.user.ini` debería contener este texto:</span><span class="sxs-lookup"><span data-stu-id="45012-138">For example, if you wanted to turn the `display_errors` setting on and set `upload_max_filesize` setting to 10M, your `.user.ini` file would contain this text:</span></span>
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on to write errors to d:\home\LogFiles\php_errors.log
        ; log_errors=On
3. <span data-ttu-id="45012-139">Implemente la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="45012-139">Deploy your web app.</span></span>
4. <span data-ttu-id="45012-140">Reinicie la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="45012-140">Restart the web app.</span></span> <span data-ttu-id="45012-141">(Es necesario reiniciar porque la frecuencia con la que PHP lee los archivos `.user.ini` depende de la configuración `user_ini.cache_ttl`, que es una configuración a nivel de sistema con un valor predeterminado de 300 segundos (5 minutos).</span><span class="sxs-lookup"><span data-stu-id="45012-141">(Restarting is necessary because the frequency with which PHP reads `.user.ini` files is governed by the `user_ini.cache_ttl` setting, which is a system level setting and is 300 seconds (5 minutes) by default.</span></span> <span data-ttu-id="45012-142">El reinicio de la aplicación web fuerza a PHP a leer la nueva configuración del archivo `.user.ini` ).</span><span class="sxs-lookup"><span data-stu-id="45012-142">Restarting the web app forces PHP to read the new settings in the `.user.ini` file.)</span></span>

<span data-ttu-id="45012-143">Como alternativa al uso de un archivo `.user.ini`, puede usar la función [ini_set()] en los scripts para definir las opciones de configuración que no son directivas a nivel de sistema.</span><span class="sxs-lookup"><span data-stu-id="45012-143">As an alternative to using a `.user.ini` file, you can use the [ini_set()] function in scripts to set configuration options that are not system-level directives.</span></span>

### <a name="changing-phpinisystem-configuration-settings"></a><span data-ttu-id="45012-144">Cambiar la configuración de PHP\_INI\_SYSTEM</span><span class="sxs-lookup"><span data-stu-id="45012-144">Changing PHP\_INI\_SYSTEM configuration settings</span></span>
1. <span data-ttu-id="45012-145">Agregar una configuración de aplicación a la aplicación web con la clave `PHP_INI_SCAN_DIR` y el valor `d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="45012-145">Add an App Setting to your Web App with the key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
2. <span data-ttu-id="45012-146">Cree un archivo `settings.ini` con la consola Kudu (http://&lt;site-nombre&gt;.scm.azurewebsite.net) en el directorio `d:\home\site\ini`.</span><span class="sxs-lookup"><span data-stu-id="45012-146">Create an `settings.ini` file using Kudu Console (http://&lt;site-name&gt;.scm.azurewebsite.net) in the `d:\home\site\ini` directory.</span></span>
3. <span data-ttu-id="45012-147">Agregue la configuración al archivo `settings.ini` , para ello, use la misma sintaxis que usaría en un archivo php.ini.</span><span class="sxs-lookup"><span data-stu-id="45012-147">Add configuration settings to the `settings.ini` file using the same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="45012-148">Por ejemplo, si desea señalar la configuración `curl.cainfo` en un archivo `*.crt` y establecer la configuración de 'wincache.maxfilesize' en 512 KB, su archivo `settings.ini`debería contener este texto:</span><span class="sxs-lookup"><span data-stu-id="45012-148">For example, if you wanted to point the `curl.cainfo` setting to a `*.crt` file and set 'wincache.maxfilesize' setting to 512K, your `settings.ini` file would contain this text:</span></span>
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. <span data-ttu-id="45012-149">Reinicie la aplicación web para cargar los cambios.</span><span class="sxs-lookup"><span data-stu-id="45012-149">Restart your Web App to load the changes.</span></span>

## <a name="how-to-enable-extensions-in-the-default-php-runtime"></a><span data-ttu-id="45012-150">Cómo: Habilitar las extensiones en el tiempo de ejecución predeterminado de PHP</span><span class="sxs-lookup"><span data-stu-id="45012-150">How to: Enable extensions in the default PHP runtime</span></span>
<span data-ttu-id="45012-151">Como se ha mencionado en la sección anterior, la mejor forma de ver la versión de PHP predeterminada, su configuración predeterminada y las extensiones habilitadas es implementar un script que llame a la función [phpinfo()].</span><span class="sxs-lookup"><span data-stu-id="45012-151">As noted in the previous section, the best way to see the default PHP version, its default configuration, and the enabled extensions is to deploy a script that calls [phpinfo()].</span></span> <span data-ttu-id="45012-152">Para habilitar extensiones adicionales, siga los pasos que se detallan a continuación.</span><span class="sxs-lookup"><span data-stu-id="45012-152">To enable additional extensions, follow the steps below:</span></span>

### <a name="configure-via-ini-settings"></a><span data-ttu-id="45012-153">Configurar mediante configuración de ini</span><span class="sxs-lookup"><span data-stu-id="45012-153">Configure via ini settings</span></span>
1. <span data-ttu-id="45012-154">Agregue un directorio `ext` al directorio `d:\home\site`.</span><span class="sxs-lookup"><span data-stu-id="45012-154">Add a `ext` directory to the `d:\home\site` directory.</span></span>
2. <span data-ttu-id="45012-155">Coloque los archivos con extensión `.dll` en el directorio `ext` (por ejemplo, `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="45012-155">Put `.dll` extension files in the `ext` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="45012-156">Asegúrese de que las extensiones sean compatibles con la versión predeterminada de PHP y que sean compatibles con VC9 y no seguras para subprocesos (nts).</span><span class="sxs-lookup"><span data-stu-id="45012-156">Make sure that the extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="45012-157">Agregar una configuración de aplicación a la aplicación web con la clave `PHP_INI_SCAN_DIR` y el valor `d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="45012-157">Add an App Setting to your Web App with the key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
4. <span data-ttu-id="45012-158">Cree un archivo `ini` en `d:\home\site\ini` denominado `extensions.ini`.</span><span class="sxs-lookup"><span data-stu-id="45012-158">Create an `ini` file in `d:\home\site\ini` called `extensions.ini`.</span></span>
5. <span data-ttu-id="45012-159">Agregue la configuración al archivo `extensions.ini` , para ello, use la misma sintaxis que usaría en un archivo php.ini.</span><span class="sxs-lookup"><span data-stu-id="45012-159">Add configuration settings to the `extensions.ini` file using the same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="45012-160">Por ejemplo, si desea habilitar las extensiones de MongoDB y XDebug su archivo `extensions.ini` debería contener este texto:</span><span class="sxs-lookup"><span data-stu-id="45012-160">For example, if you wanted to enable the MongoDB and XDebug extensions, your `extensions.ini` file would contain this text:</span></span>
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. <span data-ttu-id="45012-161">Reinicie la aplicación web para cargar los cambios.</span><span class="sxs-lookup"><span data-stu-id="45012-161">Restart your Web App to load the changes.</span></span>

### <a name="configure-via-app-setting"></a><span data-ttu-id="45012-162">Configurar a través de la configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="45012-162">Configure via App Setting</span></span>
1. <span data-ttu-id="45012-163">Agregue un directorio `bin` al directorio raíz.</span><span class="sxs-lookup"><span data-stu-id="45012-163">Add a `bin` directory to the root directory.</span></span>
2. <span data-ttu-id="45012-164">Coloque los archivos con extensión `.dll` en el directorio `bin` (por ejemplo, `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="45012-164">Put `.dll` extension files in the `bin` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="45012-165">Asegúrese de que las extensiones sean compatibles con la versión predeterminada de PHP y que sean compatibles con VC9 y no seguras para subprocesos (nts).</span><span class="sxs-lookup"><span data-stu-id="45012-165">Make sure that the extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="45012-166">Implemente la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="45012-166">Deploy your web app.</span></span>
4. <span data-ttu-id="45012-167">Vaya a la aplicación web en el Portal de Azure y haga clic en el botón **Configuración** .</span><span class="sxs-lookup"><span data-stu-id="45012-167">Browse to your web app in the Azure Portal and click on the **Settings** button.</span></span>
   
    ![Configuración de aplicaciones web][settings-button]
5. <span data-ttu-id="45012-169">En la hoja **Configuración**, seleccione **Configuración de la aplicación** y desplácese a la sección **Configuración de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="45012-169">From the **Settings** blade select **Application Settings** and scroll to the **App settings** section.</span></span>
6. <span data-ttu-id="45012-170">En la sección **Configuración de aplicaciones**, cree una clave **PHP_EXTENSIONS**.</span><span class="sxs-lookup"><span data-stu-id="45012-170">In the **App settings** section, create a **PHP_EXTENSIONS** key.</span></span> <span data-ttu-id="45012-171">El valor de esta clave es una ruta de acceso relativa a la raíz del sitio web: **bin\your-ext-file**.</span><span class="sxs-lookup"><span data-stu-id="45012-171">The value for this key would be a path relative to website root: **bin\your-ext-file**.</span></span>
   
    ![Habilitar extensiones en app settings][php-extensions]
7. <span data-ttu-id="45012-173">Haga clic en el botón **Guardar**, situado en la parte superior de la hoja **Configuración de aplicaciones web**.</span><span class="sxs-lookup"><span data-stu-id="45012-173">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![Guardar la configuración][save-button]

<span data-ttu-id="45012-175">También se pueden usar las extensiones Zend mediante una clave **PHP_ZENDEXTENSIONS**.</span><span class="sxs-lookup"><span data-stu-id="45012-175">Zend extensions are also supported by using a **PHP_ZENDEXTENSIONS** key.</span></span> <span data-ttu-id="45012-176">Para habilitar varias extensiones, incluya una lista separada por comas de los archivos `.dll` como valor de configuración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="45012-176">To enable multiple extensions, include a comma-separated list of `.dll` files for the app setting value.</span></span>

## <a name="how-to-use-a-custom-php-runtime"></a><span data-ttu-id="45012-177">Cómo: Usar un tiempo de ejecución de PHP personalizado</span><span class="sxs-lookup"><span data-stu-id="45012-177">How to: Use a custom PHP runtime</span></span>
<span data-ttu-id="45012-178">En lugar del tiempo de ejecución de PHP, Aplicaciones web del Servicio de aplicaciones puede usar un tiempo de ejecución de PHP facilitado por el usuario para ejecutar scripts PHP.</span><span class="sxs-lookup"><span data-stu-id="45012-178">Instead of the default PHP runtime, App Service Web Apps can use a PHP runtime that you provide to execute PHP scripts.</span></span> <span data-ttu-id="45012-179">El tiempo de ejecución que facilita se puede configurar mediante un archivo `php.ini` que también usted facilita.</span><span class="sxs-lookup"><span data-stu-id="45012-179">The runtime that you provide can be configured by a `php.ini` file that you also provide.</span></span> <span data-ttu-id="45012-180">Para usar un tiempo de ejecución de PHP personalizado en Aplicaciones web, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="45012-180">To use a custom PHP runtime with Web Apps, follow the steps below.</span></span>

1. <span data-ttu-id="45012-181">Obtenga una versión compatible con VC9 y VC11 no segura para subprocesos de PHP para Windows.</span><span class="sxs-lookup"><span data-stu-id="45012-181">Obtain a non-thread-safe, VC9 or VC11 compatible version of PHP for Windows.</span></span> <span data-ttu-id="45012-182">Las versiones recientes de PHP para Windows se pueden encontrar aquí: [http://windows.php.net/download/].</span><span class="sxs-lookup"><span data-stu-id="45012-182">Recent releases of PHP for Windows can be found here: [http://windows.php.net/download/].</span></span> <span data-ttu-id="45012-183">Las versiones anteriores pueden encontrarse archivadas aquí: [http://windows.php.net/downloads/releases/archives/].</span><span class="sxs-lookup"><span data-stu-id="45012-183">Older releases can be found in the archive here: [http://windows.php.net/downloads/releases/archives/].</span></span>
2. <span data-ttu-id="45012-184">Modifique el archivo `php.ini` para el tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="45012-184">Modify the `php.ini` file for your runtime.</span></span> <span data-ttu-id="45012-185">Tenga en cuenta que Aplicaciones web omitirá cualquier configuración que se corresponda con directivas que sean solo de nivel de sistema.</span><span class="sxs-lookup"><span data-stu-id="45012-185">Note that any configuration settings that are system-level-only directives will be ignored by Web Apps.</span></span> <span data-ttu-id="45012-186">(Para obtener información acerca de las directivas solo a nivel de sistema, consulte la [lista de directivas de php.ini]).</span><span class="sxs-lookup"><span data-stu-id="45012-186">(For information about system-level-only directives, see [List of php.ini directives]).</span></span>
3. <span data-ttu-id="45012-187">También puede agregar extensiones al tiempo de ejecución de PHP y habilitarlas en el archivo `php.ini` .</span><span class="sxs-lookup"><span data-stu-id="45012-187">Optionally, add extensions to your PHP runtime and enable them in the `php.ini` file.</span></span>
4. <span data-ttu-id="45012-188">Agregue un directorio `bin` al directorio raíz y coloque en él el directorio que contiene el tiempo de ejecución de PHP (por ejemplo, `bin\php`).</span><span class="sxs-lookup"><span data-stu-id="45012-188">Add a `bin` directory to your root directory, and put the directory that contains your PHP runtime in it (for example, `bin\php`).</span></span>
5. <span data-ttu-id="45012-189">Implemente la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="45012-189">Deploy your web app.</span></span>
6. <span data-ttu-id="45012-190">Vaya a la aplicación web en el Portal de Azure y haga clic en el botón **Configuración** .</span><span class="sxs-lookup"><span data-stu-id="45012-190">Browse to your web app in the Azure Portal and click on the **Settings** button.</span></span>
   
    ![Configuración de aplicaciones web][settings-button]
7. <span data-ttu-id="45012-192">En la hoja **Configuración**, seleccione **Configuración de aplicaciones** y desplácese a la sección **Asignaciones de controlador**.</span><span class="sxs-lookup"><span data-stu-id="45012-192">From the **Settings** blade select **Application Settings** and scroll to the **Handler mappings** section.</span></span> <span data-ttu-id="45012-193">Agregue `*.php` al campo Extensión y agregue la ruta de acceso al ejecutable `php-cgi.exe`.</span><span class="sxs-lookup"><span data-stu-id="45012-193">Add `*.php` to the Extension field and add the path to the `php-cgi.exe` executable.</span></span> <span data-ttu-id="45012-194">Si coloca el tiempo de ejecución de PHP en el directorio `bin` de la raíz de la aplicación, la ruta de acceso será `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span><span class="sxs-lookup"><span data-stu-id="45012-194">If you put your PHP runtime in the `bin` directory in the root of you application, the path will be `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span></span>
   
    ![Especificar el controlador en hander mappings][handler-mappings]
8. <span data-ttu-id="45012-196">Haga clic en el botón **Guardar**, situado en la parte superior de la hoja **Configuración de aplicaciones web**.</span><span class="sxs-lookup"><span data-stu-id="45012-196">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![Guardar la configuración][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a><span data-ttu-id="45012-198">Procedimiento para habilitar la automatización de Composer en Azure</span><span class="sxs-lookup"><span data-stu-id="45012-198">How to: Enable Composer automation in Azure</span></span>
<span data-ttu-id="45012-199">De forma predeterminada, el Servicio de aplicaciones no responde con composer.json, si tiene uno en el proyecto PHP.</span><span class="sxs-lookup"><span data-stu-id="45012-199">By default, App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="45012-200">Si usa la [implementación de Git](app-service-deploy-local-git.md), puede habilitar el procesamiento de composer.json durante `git push` mediante la habilitación de la extensión de Composer.</span><span class="sxs-lookup"><span data-stu-id="45012-200">If you use [Git deployment](app-service-deploy-local-git.md), you can enable composer.json processing during `git push` by enabling the Composer extension.</span></span>

> [!NOTE]
> <span data-ttu-id="45012-201">Aquí puede [votar por soporte técnico de primera clase para Composer en el Servicio de aplicaciones](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip).</span><span class="sxs-lookup"><span data-stu-id="45012-201">You can [vote for first-class Composer support in App Service here](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span></span>
> 
> 

1. <span data-ttu-id="45012-202">En la hoja de la aplicación web de PHP, en [Azure Portal](https://portal.azure.com), haga clic en **Herramientas** > **Extensiones**.</span><span class="sxs-lookup"><span data-stu-id="45012-202">In your PHP web app's blade in the [Azure portal](https://portal.azure.com), click **Tools** > **Extensions**.</span></span>
   
    ![Hoja de configuración del Portal de Azure para habilitar la automatización de Composer en Azure](./media/web-sites-php-configure/composer-extension-settings.png)
2. <span data-ttu-id="45012-204">Haga clic en **Agregar** y, luego, en **Compositor**.</span><span class="sxs-lookup"><span data-stu-id="45012-204">Click **Add**, then click **Composer**.</span></span>
   
    ![Agregar la extensión Composer para habilitar la automatización de Composer en Azure](./media/web-sites-php-configure/composer-extension-add.png)
3. <span data-ttu-id="45012-206">Haga clic en **Aceptar** para aceptar las condiciones legales.</span><span class="sxs-lookup"><span data-stu-id="45012-206">Click **OK** to accept legal terms.</span></span> <span data-ttu-id="45012-207">Haga clic de nuevo en **Aceptar** para agregar la extensión.</span><span class="sxs-lookup"><span data-stu-id="45012-207">Click **OK** again to add the extension.</span></span>
   
    <span data-ttu-id="45012-208">La hoja **Extensiones instaladas** mostrará ahora la extensión Compositor.</span><span class="sxs-lookup"><span data-stu-id="45012-208">The **Installed extensions** blade will now show the Composer extension.</span></span>  
    <span data-ttu-id="45012-209">![Aceptar los términos legales para habilitar la automatización de Composer en Azure](./media/web-sites-php-configure/composer-extension-view.png)</span><span class="sxs-lookup"><span data-stu-id="45012-209">![Accept legal terms to enable Composer automation in Azure](./media/web-sites-php-configure/composer-extension-view.png)</span></span>
4. <span data-ttu-id="45012-210">Ahora, ejecute `git add`, `git commit` y `git push` como en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="45012-210">Now, perform `git add`, `git commit`, and `git push` like in the previous section.</span></span> <span data-ttu-id="45012-211">Verá que Composer está instalando las dependencias definidas en composer.json.</span><span class="sxs-lookup"><span data-stu-id="45012-211">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Implementación de GIT con la automatización de Composer en Azure](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a><span data-ttu-id="45012-213">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="45012-213">Next steps</span></span>
<span data-ttu-id="45012-214">Para más información, vea el [Centro para desarrolladores de PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="45012-214">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

> [!NOTE]
> <span data-ttu-id="45012-215">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de inscribirse para abrir una cuenta de Azure, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="45012-215">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="45012-216">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="45012-216">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="45012-217">[evaluación gratuita]: https://www.windowsazure.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="45012-217">[free trial]: https://www.windowsazure.com/pricing/free-trial/</span></span>
<span data-ttu-id="45012-218">[phpinfo()]: http://php.net/manual/en/function.phpinfo.php</span><span class="sxs-lookup"><span data-stu-id="45012-218">[phpinfo()]: http://php.net/manual/en/function.phpinfo.php</span></span>
[select-php-version]: ./media/web-sites-php-configure/select-php-version.png
<span data-ttu-id="45012-219">[lista de directivas de php.ini]: http://www.php.net/manual/en/ini.list.php</span><span class="sxs-lookup"><span data-stu-id="45012-219">[List of php.ini directives]: http://www.php.net/manual/en/ini.list.php</span></span>
<span data-ttu-id="45012-220">[.user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php</span><span class="sxs-lookup"><span data-stu-id="45012-220">[.user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php</span></span>
<span data-ttu-id="45012-221">[ini_set()]: http://www.php.net/manual/en/function.ini-set.php</span><span class="sxs-lookup"><span data-stu-id="45012-221">[ini_set()]: http://www.php.net/manual/en/function.ini-set.php</span></span>
[application-settings]: ./media/web-sites-php-configure/application-settings.png
[settings-button]: ./media/web-sites-php-configure/settings-button.png
[save-button]: ./media/web-sites-php-configure/save-button.png
[php-extensions]: ./media/web-sites-php-configure/php-extensions.png
[handler-mappings]: ./media/web-sites-php-configure/handler-mappings.png
<span data-ttu-id="45012-222">[http://windows.php.net/download/]: http://windows.php.net/download/</span><span class="sxs-lookup"><span data-stu-id="45012-222">[http://windows.php.net/download/]: http://windows.php.net/download/</span></span>
<span data-ttu-id="45012-223">[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/</span><span class="sxs-lookup"><span data-stu-id="45012-223">[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/</span></span>
[SETPHPVERCLI]: ./media/web-sites-php-configure/ChangePHPVersion-XPlatCLI.png
[GETPHPVERCLI]: ./media/web-sites-php-configure/ShowPHPVersion-XplatCLI.png
[SETPHPVERPS]: ./media/web-sites-php-configure/ChangePHPVersion-PS.png
[GETPHPVERPS]: ./media/web-sites-php-configure/ShowPHPVersion-PS.png

