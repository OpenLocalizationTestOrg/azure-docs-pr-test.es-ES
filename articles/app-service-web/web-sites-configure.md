---
title: "Configuración de aplicaciones web en el Servicio de aplicaciones de Azure"
description: "Cómo configurar una aplicación web en servicios de aplicaciones de Azure"
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9af8a367-7d39-4399-9941-b80cbc5f39a0
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cacbcf879555907f81d824dc1069b05579dca010
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a><span data-ttu-id="ed529-103">Configuración de aplicaciones web en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="ed529-103">Configure web apps in Azure App Service</span></span>
<span data-ttu-id="ed529-104">En este tema se explica cómo configurar una aplicación web con el [Portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="ed529-104">This topic explains how to configure a web app using the [Azure Portal].</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a><span data-ttu-id="ed529-105">Configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="ed529-105">Application settings</span></span>
1. <span data-ttu-id="ed529-106">En el [Portal de Azure], abra la hoja de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ed529-106">In the [Azure Portal], open the blade for the web app.</span></span>
2. <span data-ttu-id="ed529-107">Haga clic en **Toda la configuración**.</span><span class="sxs-lookup"><span data-stu-id="ed529-107">Click **All Settings**.</span></span>
3. <span data-ttu-id="ed529-108">Haga clic en **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="ed529-108">Click **Application Settings**.</span></span>

![Configuración de la aplicación][configure01]

<span data-ttu-id="ed529-110">La hoja **Configuración de la aplicación** tiene configuraciones agrupadas en varias categorías.</span><span class="sxs-lookup"><span data-stu-id="ed529-110">The **Application settings** blade has settings grouped under several categories.</span></span>

### <a name="general-settings"></a><span data-ttu-id="ed529-111">Configuración general</span><span class="sxs-lookup"><span data-stu-id="ed529-111">General settings</span></span>
<span data-ttu-id="ed529-112">**Versiones del marco**.</span><span class="sxs-lookup"><span data-stu-id="ed529-112">**Framework versions**.</span></span> <span data-ttu-id="ed529-113">Configure estas opciones si su aplicación utiliza cualquiera de estos marcos:</span><span class="sxs-lookup"><span data-stu-id="ed529-113">Set these options if your app uses any these frameworks:</span></span> 

* <span data-ttu-id="ed529-114">**.NET Framework**: configure la versión de .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="ed529-114">**.NET Framework**: Set the .NET framework version.</span></span> 
* <span data-ttu-id="ed529-115">**PHP**: defina la versión de PHP, o bien seleccione **DESACTIVADO** para deshabilitar PHP.</span><span class="sxs-lookup"><span data-stu-id="ed529-115">**PHP**: Set the PHP version, or **OFF** to disable PHP.</span></span> 
* <span data-ttu-id="ed529-116">**Java**: seleccione la versión de Java o **DESACTIVADO** para deshabilitar Java.</span><span class="sxs-lookup"><span data-stu-id="ed529-116">**Java**: Select the Java version or **OFF** to disable Java.</span></span> <span data-ttu-id="ed529-117">Utilice la opción **Contenedor web** para elegir entre las versiones Tomcat y Jetty.</span><span class="sxs-lookup"><span data-stu-id="ed529-117">Use the **Web Container** option to choose between Tomcat and Jetty versions.</span></span>
* <span data-ttu-id="ed529-118">**Python**: seleccione la versión de Python o seleccione **DESACTIVADO** para deshabilitar Python.</span><span class="sxs-lookup"><span data-stu-id="ed529-118">**Python**: Select the Python version, or **OFF** to disable Python.</span></span>

<span data-ttu-id="ed529-119">Por razones técnicas, si se habilita Java para la aplicación, se deshabilitan las opciones .NET, PHP y Python.</span><span class="sxs-lookup"><span data-stu-id="ed529-119">For technical reasons, enabling Java for your app disables the .NET, PHP, and Python options.</span></span>

<span data-ttu-id="ed529-120"><a name="platform"></a>
**Plataforma**.</span><span class="sxs-lookup"><span data-stu-id="ed529-120"><a name="platform"></a>
**Platform**.</span></span> <span data-ttu-id="ed529-121">Seleccione si su aplicación web se ejecuta en un entorno de 32 o 64 bits.</span><span class="sxs-lookup"><span data-stu-id="ed529-121">Selects whether your web app runs in a 32-bit or 64-bit environment.</span></span> <span data-ttu-id="ed529-122">El entorno de 64 bits requiere el modo básico o estándar.</span><span class="sxs-lookup"><span data-stu-id="ed529-122">The 64-bit environment requires Basic or Standard mode.</span></span> <span data-ttu-id="ed529-123">Los modos libre y compartido siempre se ejecutan en un entorno de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="ed529-123">Free and Shared modes always run in a 32-bit environment.</span></span>

<span data-ttu-id="ed529-124">**Sockets web**.</span><span class="sxs-lookup"><span data-stu-id="ed529-124">**Web Sockets**.</span></span> <span data-ttu-id="ed529-125">Seleccione **ACTIVADO** para habilitar el protocolo WebSocket; por ejemplo, si el sitio web utiliza [ASP.NET SignalR] o [socket.io].</span><span class="sxs-lookup"><span data-stu-id="ed529-125">Set **ON** to enable the WebSocket protocol; for example, if your web app uses [ASP.NET SignalR] or [socket.io].</span></span>

<span data-ttu-id="ed529-126"><a name="alwayson"></a>
**AlwaysOn**.</span><span class="sxs-lookup"><span data-stu-id="ed529-126"><a name="alwayson"></a>
**Always On**.</span></span> <span data-ttu-id="ed529-127">De forma predeterminada, las aplicaciones web se descargan si están inactivas durante algún tiempo.</span><span class="sxs-lookup"><span data-stu-id="ed529-127">By default, web apps are unloaded if they are idle for some period of time.</span></span> <span data-ttu-id="ed529-128">Esto permite que el sistema conserve recursos.</span><span class="sxs-lookup"><span data-stu-id="ed529-128">This lets the system conserve resources.</span></span> <span data-ttu-id="ed529-129">En el modo básico o estándar puede habilitar **Siempre disponible** para mantener el sitio cargado continuamente.</span><span class="sxs-lookup"><span data-stu-id="ed529-129">In Basic or Standard mode, you can enable **Always On** to keep the app loaded all the time.</span></span> <span data-ttu-id="ed529-130">Si su aplicación ejecuta WebJobs continuos o WebJobs activados mediante una expresión CRON, debe habilitar **AlwaysOn** o los trabajos web no se ejecutarán de forma fiable.</span><span class="sxs-lookup"><span data-stu-id="ed529-130">If your app runs continuous WebJobs or runs WebJobs triggered using a CRON expression, you should enable **Always On**, or the web jobs may not run reliably.</span></span>

<span data-ttu-id="ed529-131">**Versión de canalización administrada**.</span><span class="sxs-lookup"><span data-stu-id="ed529-131">**Managed Pipeline Version**.</span></span> <span data-ttu-id="ed529-132">Configura el [modo de canalización]IIS.</span><span class="sxs-lookup"><span data-stu-id="ed529-132">Sets the IIS [pipeline mode].</span></span> <span data-ttu-id="ed529-133">Deje este valor en Integrado (el valor predeterminado) a no ser que tenga una aplicación web heredada que requiera una versión anterior de IIS.</span><span class="sxs-lookup"><span data-stu-id="ed529-133">Leave this set to Integrated (the default) unless you have a legacy app that requires an older version of IIS.</span></span>

<span data-ttu-id="ed529-134">**Intercambio automático**.</span><span class="sxs-lookup"><span data-stu-id="ed529-134">**Auto Swap**.</span></span> <span data-ttu-id="ed529-135">Si habilita el Intercambio automático de una ranura de implementación, el servicio de aplicación intercambiará automáticamente la aplicación web en producción cuando inserte una actualización para esa zona.</span><span class="sxs-lookup"><span data-stu-id="ed529-135">If you enable Auto Swap for a deployment slot, App Service will automatically swap the web app into production when you push an update to that slot.</span></span> <span data-ttu-id="ed529-136">Para obtener más información, consulte [Implementación en ranuras de ensayo para las aplicaciones web en el servicio de aplicaciones de Azure](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="ed529-136">For more information, see [Deploy to staging slots for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span>

### <a name="debugging"></a><span data-ttu-id="ed529-137">Depuración</span><span class="sxs-lookup"><span data-stu-id="ed529-137">Debugging</span></span>
<span data-ttu-id="ed529-138">**Depuración remota**.</span><span class="sxs-lookup"><span data-stu-id="ed529-138">**Remote Debugging**.</span></span> <span data-ttu-id="ed529-139">Habilita la depuración remota.</span><span class="sxs-lookup"><span data-stu-id="ed529-139">Enables remote debugging.</span></span> <span data-ttu-id="ed529-140">Cuando esté habilitada, puede usar la depuración remota en Visual Studio para conectarse directamente a su aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="ed529-140">When enabled, you can use the remote debugger in Visual Studio to connect directly to your web app.</span></span> <span data-ttu-id="ed529-141">La depuración remota permanecerá habilitada durante 48 horas.</span><span class="sxs-lookup"><span data-stu-id="ed529-141">Remote debugging will remain enabled for 48 hours.</span></span> 

### <a name="app-settings"></a><span data-ttu-id="ed529-142">Configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="ed529-142">App settings</span></span>
<span data-ttu-id="ed529-143">Esta sección contiene las parejas de nombre y valor que la aplicación web cargará al inicio.</span><span class="sxs-lookup"><span data-stu-id="ed529-143">This section contains name/value pairs that you web app will load on start up.</span></span> 

* <span data-ttu-id="ed529-144">En las aplicaciones .NET, estas configuraciones se insertarán en la sección de la configuración de .NET `AppSettings` en tiempo de ejecución y reemplazará la configuración existente.</span><span class="sxs-lookup"><span data-stu-id="ed529-144">For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings.</span></span> 
* <span data-ttu-id="ed529-145">Las aplicaciones PHP, Python, Java y Node pueden acceder a estas configuraciones como variables de entorno en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="ed529-145">PHP, Python, Java and Node applications can access these settings as environment variables at runtime.</span></span> <span data-ttu-id="ed529-146">En cada configuración de aplicación se crean dos variables de entorno; una con el nombre especificado en el entrada de configuración de la aplicación y otra con el prefijo APPSETTING_.</span><span class="sxs-lookup"><span data-stu-id="ed529-146">For each app setting, two environment variables are created; one with the name specified by the app setting entry, and another with a prefix of APPSETTING_.</span></span> <span data-ttu-id="ed529-147">Ambas contienen el mismo valor.</span><span class="sxs-lookup"><span data-stu-id="ed529-147">Both contain the same value.</span></span>

### <a name="connection-strings"></a><span data-ttu-id="ed529-148">Cadenas de conexión</span><span class="sxs-lookup"><span data-stu-id="ed529-148">Connection strings</span></span>
<span data-ttu-id="ed529-149">Cadenas de conexión para los recursos vinculados.</span><span class="sxs-lookup"><span data-stu-id="ed529-149">Connection strings for linked resources.</span></span> 

<span data-ttu-id="ed529-150">En las aplicaciones .NET, estas cadenas de conexión se insertan en la sección `connectionStrings` de la configuración de .NET en tiempo de ejecución y reemplazan las entradas existentes en las que la clave sea igual que el nombre de la base de datos vinculada.</span><span class="sxs-lookup"><span data-stu-id="ed529-150">For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where the key equals the linked database name.</span></span> 

<span data-ttu-id="ed529-151">En las aplicaciones PHP, Python, Java y Node, estas configuraciones estarán disponibles como variables de entorno en tiempo de ejecución, con el tipo de conexión como prefijo.</span><span class="sxs-lookup"><span data-stu-id="ed529-151">For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with the connection type.</span></span> <span data-ttu-id="ed529-152">Los prefijos de variable de entorno son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="ed529-152">The environment variable prefixes are as follows:</span></span> 

* <span data-ttu-id="ed529-153">SQL Server: `SQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="ed529-153">SQL Server: `SQLCONNSTR_`</span></span>
* <span data-ttu-id="ed529-154">MySQL: `MYSQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="ed529-154">MySQL: `MYSQLCONNSTR_`</span></span>
* <span data-ttu-id="ed529-155">Base de datos SQL: `SQLAZURECONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="ed529-155">SQL Database: `SQLAZURECONNSTR_`</span></span>
* <span data-ttu-id="ed529-156">Personalizado: `CUSTOMCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="ed529-156">Custom: `CUSTOMCONNSTR_`</span></span>

<span data-ttu-id="ed529-157">Por ejemplo, si una cadena de conexión de MySQL recibió el nombre de  `connectionstring1`, se obtendrá acceso a ella a través de la variable de entorno `MYSQLCONNSTR_connectionString1`.</span><span class="sxs-lookup"><span data-stu-id="ed529-157">For example, if a MySql connection string were named `connectionstring1`, it would be accessed through the environment variable `MYSQLCONNSTR_connectionString1`.</span></span>

### <a name="default-documents"></a><span data-ttu-id="ed529-158">Documentos predeterminados</span><span class="sxs-lookup"><span data-stu-id="ed529-158">Default documents</span></span>
<span data-ttu-id="ed529-159">El documento predeterminado es la página web que se muestra en la dirección URL raíz de un sitio web.</span><span class="sxs-lookup"><span data-stu-id="ed529-159">The default document is the web page that is displayed at the root URL for a website.</span></span>  <span data-ttu-id="ed529-160">Se usa el primer archivo coincidente en la lista.</span><span class="sxs-lookup"><span data-stu-id="ed529-160">The first matching file in the list is used.</span></span> 

<span data-ttu-id="ed529-161">Es posible que las aplicaciones utilicen módulos que enruten en base a la URL, en lugar de ofrecer funcionalidad a contenido estático, en cuyo caso no existe realmente un documento predeterminado.</span><span class="sxs-lookup"><span data-stu-id="ed529-161">Web apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.</span></span>    

### <a name="handler-mappings"></a><span data-ttu-id="ed529-162">Asignaciones de controlador</span><span class="sxs-lookup"><span data-stu-id="ed529-162">Handler mappings</span></span>
<span data-ttu-id="ed529-163">Utilice esta zona para agregar procesadores de script personalizados para controlar solicitudes de extensiones de archivo específicas.</span><span class="sxs-lookup"><span data-stu-id="ed529-163">Use this area to add custom script processors to handle requests for specific file extensions.</span></span> 

* <span data-ttu-id="ed529-164">**Extensión**.</span><span class="sxs-lookup"><span data-stu-id="ed529-164">**Extension**.</span></span> <span data-ttu-id="ed529-165">La extensión de archivo que se va a gestionar, por ejemplo, *.php o handler.fcgi.</span><span class="sxs-lookup"><span data-stu-id="ed529-165">The file extension to be handled, such as *.php or handler.fcgi.</span></span> 
* <span data-ttu-id="ed529-166">**Ruta de acceso del procesador de script**.</span><span class="sxs-lookup"><span data-stu-id="ed529-166">**Script Processor Path**.</span></span> <span data-ttu-id="ed529-167">La ruta absoluta del procesador de script.</span><span class="sxs-lookup"><span data-stu-id="ed529-167">The absolute path of the script processor.</span></span> <span data-ttu-id="ed529-168">El procesador de script procesará las solicitudes a archivos que coincidan con esta extensión de archivo.</span><span class="sxs-lookup"><span data-stu-id="ed529-168">Requests to files that match the file extension will be processed by the script processor.</span></span> <span data-ttu-id="ed529-169">Utilice la ruta de acceso `D:\home\site\wwwroot` para hacer referencia al directorio raíz de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ed529-169">Use the path `D:\home\site\wwwroot` to refer to your app's root directory.</span></span>
* <span data-ttu-id="ed529-170">**Argumentos adicionales**.</span><span class="sxs-lookup"><span data-stu-id="ed529-170">**Additional Arguments**.</span></span> <span data-ttu-id="ed529-171">Argumentos opcionales de la línea de comandos para el procesador de script</span><span class="sxs-lookup"><span data-stu-id="ed529-171">Optional command-line arguments for the script processor</span></span> 

### <a name="virtual-applications-and-directories"></a><span data-ttu-id="ed529-172">Directorios y aplicaciones virtuales</span><span class="sxs-lookup"><span data-stu-id="ed529-172">Virtual applications and directories</span></span>
<span data-ttu-id="ed529-173">Para configurar las aplicaciones y los directorios virtuales, especifique cada directorio virtual y su ruta de acceso física correspondiente en relación con la raíz del sitio web.</span><span class="sxs-lookup"><span data-stu-id="ed529-173">To configure virtual applications and directories, specify each virtual directory and its corresponding physical path relative to the website root.</span></span> <span data-ttu-id="ed529-174">De manera opcional, puede activar la casilla **Aplicación** para marcar un directorio virtual como una aplicación.</span><span class="sxs-lookup"><span data-stu-id="ed529-174">Optionally, you can select the **Application** checkbox to mark a virtual directory as an application.</span></span>

## <a name="enabling-diagnostic-logs"></a><span data-ttu-id="ed529-175">Habilitación de registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="ed529-175">Enabling diagnostic logs</span></span>
<span data-ttu-id="ed529-176">Para habilitar registros de diagnóstico:</span><span class="sxs-lookup"><span data-stu-id="ed529-176">To enable diagnostic logs:</span></span>

1. <span data-ttu-id="ed529-177">En la hoja de la aplicación web, haga clic en **Toda la configuración**.</span><span class="sxs-lookup"><span data-stu-id="ed529-177">In the blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="ed529-178">Haga clic en **Registros de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="ed529-178">Click **Diagnostic logs**.</span></span> 

<span data-ttu-id="ed529-179">Opciones para escribir registros de diagnóstico de una aplicación web que admita el registro:</span><span class="sxs-lookup"><span data-stu-id="ed529-179">Options for writing diagnostic logs from a web application that supports logging:</span></span> 

* <span data-ttu-id="ed529-180">**Registro de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ed529-180">**Application Logging**.</span></span> <span data-ttu-id="ed529-181">Escribe registros de aplicación en el sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="ed529-181">Writes application logs to the file system.</span></span> <span data-ttu-id="ed529-182">El registro dura un período de 12 horas.</span><span class="sxs-lookup"><span data-stu-id="ed529-182">Logging lasts for a period of 12 hours.</span></span> 

<span data-ttu-id="ed529-183">**Nivel**.</span><span class="sxs-lookup"><span data-stu-id="ed529-183">**Level**.</span></span> <span data-ttu-id="ed529-184">Cuando el registro de aplicaciones está habilitado, esta opción especifica la cantidad de información que se registrará (Error, Advertencia, Información o Detalle).</span><span class="sxs-lookup"><span data-stu-id="ed529-184">When application logging is enabled, this option specifies the amount of information that will be recorded (Error, Warning, Information, or Verbose).</span></span>

<span data-ttu-id="ed529-185">**Registro del servidor web**.</span><span class="sxs-lookup"><span data-stu-id="ed529-185">**Web server logging**.</span></span> <span data-ttu-id="ed529-186">Los registros se guardan con formato de archivo de registro W3C extendido.</span><span class="sxs-lookup"><span data-stu-id="ed529-186">Logs are saved in the W3C extended log file format.</span></span> 

<span data-ttu-id="ed529-187">**Mensajes de error detallados**.</span><span class="sxs-lookup"><span data-stu-id="ed529-187">**Detailed error messages**.</span></span> <span data-ttu-id="ed529-188">Guarda archivos .htm de mensajes de error detallados.</span><span class="sxs-lookup"><span data-stu-id="ed529-188">Saves detailed error messages .htm files.</span></span> <span data-ttu-id="ed529-189">Los archivos se guardan en /LogFiles/DetailedErrors.</span><span class="sxs-lookup"><span data-stu-id="ed529-189">The files are saved under /LogFiles/DetailedErrors.</span></span> 

<span data-ttu-id="ed529-190">**Seguimiento de solicitudes erróneas**.</span><span class="sxs-lookup"><span data-stu-id="ed529-190">**Failed request tracing**.</span></span> <span data-ttu-id="ed529-191">Registra solicitudes erróneas en archivos XML.</span><span class="sxs-lookup"><span data-stu-id="ed529-191">Logs failed requests to XML files.</span></span> <span data-ttu-id="ed529-192">Los archivos se guardan en /LogFiles/W3SVC*xxx*, donde xxx es un identificador único.</span><span class="sxs-lookup"><span data-stu-id="ed529-192">The files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier.</span></span> <span data-ttu-id="ed529-193">Esta carpeta contiene un archivo XSL y uno o varios archivos XML.</span><span class="sxs-lookup"><span data-stu-id="ed529-193">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="ed529-194">Asegúrese de descargar el archivo XSL porque proporciona funcionalidad para dar formato y filtrar los contenidos de los archivos XML.</span><span class="sxs-lookup"><span data-stu-id="ed529-194">Make sure to download the XSL file, because it provides functionality for formatting and filtering the contents of the XML files.</span></span>

<span data-ttu-id="ed529-195">Para ver los archivos de registro, debe crear las credenciales FTP, de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="ed529-195">To view the log files, you must create FTP credentials, as follows:</span></span>

1. <span data-ttu-id="ed529-196">En la hoja de la aplicación web, haga clic en **Toda la configuración**.</span><span class="sxs-lookup"><span data-stu-id="ed529-196">In the blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="ed529-197">Haga clic en **Credenciales de implementación**.</span><span class="sxs-lookup"><span data-stu-id="ed529-197">Click **Deployment credentials**.</span></span>
3. <span data-ttu-id="ed529-198">Escriba un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="ed529-198">Enter a user name and password.</span></span>
4. <span data-ttu-id="ed529-199">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ed529-199">Click **Save**.</span></span>

![Configurar credenciales de implementación][configure03]

<span data-ttu-id="ed529-201">El nombre de usuario de FTP completo es "app\nombreusuario", donde *app* es el nombre de su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ed529-201">The full FTP user name is “app\username” where *app* is the name of your web app.</span></span> <span data-ttu-id="ed529-202">El nombre de usuario se indica en la tarjeta única de la aplicación web, en **Essentials**</span><span class="sxs-lookup"><span data-stu-id="ed529-202">The username is listed in the web app blade, under **Essentials**.</span></span>  

![Credenciales de implementación de FTP][configure02]

## <a name="other-configuration-tasks"></a><span data-ttu-id="ed529-204">Otras tareas de configuración</span><span class="sxs-lookup"><span data-stu-id="ed529-204">Other configuration tasks</span></span>
### <a name="ssl"></a><span data-ttu-id="ed529-205">SSL</span><span class="sxs-lookup"><span data-stu-id="ed529-205">SSL</span></span>
<span data-ttu-id="ed529-206">En modo básico o estándar puede cargar certificados SSL para un dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="ed529-206">In Basic or Standard mode, you can upload SSL certificates for a custom domain.</span></span> <span data-ttu-id="ed529-207">Para más información, consulte [Habilitación de HTTPS para una aplicación web].</span><span class="sxs-lookup"><span data-stu-id="ed529-207">For more information, see [Enable HTTPS for a web app].</span></span> 

<span data-ttu-id="ed529-208">Para ver los certificados cargados, haga clic en **Toda la configuración** > **Dominios personalizados y SSL**.</span><span class="sxs-lookup"><span data-stu-id="ed529-208">To view your uploaded certificates, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="domain-names"></a><span data-ttu-id="ed529-209">Nombres de dominio</span><span class="sxs-lookup"><span data-stu-id="ed529-209">Domain names</span></span>
<span data-ttu-id="ed529-210">Agregue nombres de dominio personalizados para su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ed529-210">Add custom domain names for your web app.</span></span> <span data-ttu-id="ed529-211">Para más información, consulte [Configuración de un nombre de dominio personalizado para una aplicación web en el servicio de aplicaciones de Azure].</span><span class="sxs-lookup"><span data-stu-id="ed529-211">For more information, see [Configure a custom domain name for a web app in Azure App Service].</span></span>

<span data-ttu-id="ed529-212">Para ver los nombres de dominios, haga clic en **Toda la configuración** > **Dominios personalizados y SSL**.</span><span class="sxs-lookup"><span data-stu-id="ed529-212">To view your domain names, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="deployments"></a><span data-ttu-id="ed529-213">Implementaciones</span><span class="sxs-lookup"><span data-stu-id="ed529-213">Deployments</span></span>
* <span data-ttu-id="ed529-214">Configure la implementación continua.</span><span class="sxs-lookup"><span data-stu-id="ed529-214">Set up continuous deployment.</span></span> <span data-ttu-id="ed529-215">Consulte el artículo sobre el [uso de Git para implementar aplicaciones web en Azure App Service](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ed529-215">See [Using Git to deploy Web Apps in Azure App Service](web-sites-deploy.md).</span></span>
* <span data-ttu-id="ed529-216">Ranuras de implementación.</span><span class="sxs-lookup"><span data-stu-id="ed529-216">Deployment slots.</span></span> <span data-ttu-id="ed529-217">Consulte [Configuración de entornos de ensayo para aplicaciones web en el Servicio de aplicaciones de Azure].</span><span class="sxs-lookup"><span data-stu-id="ed529-217">See [Deploy to Staging Environments for Web Apps in Azure App Service].</span></span>

<span data-ttu-id="ed529-218">Para ver las ranuras de implementación, haga clic en **Toda la configuración** > **Ranuras de implementación**.</span><span class="sxs-lookup"><span data-stu-id="ed529-218">To view your deployment slots, click **All Settings** > **Deployment slots**.</span></span>

### <a name="monitoring"></a><span data-ttu-id="ed529-219">Supervisión</span><span class="sxs-lookup"><span data-stu-id="ed529-219">Monitoring</span></span>
<span data-ttu-id="ed529-220">En modo estándar o básico, pruebe la disponibilidad de los puntos de conexión HTTP o HTTPS desde ubicaciones geodistribuidas.</span><span class="sxs-lookup"><span data-stu-id="ed529-220">In Basic or Standard mode, you can  test the availability of HTTP or HTTPS endpoints, from up to three geo-distributed locations.</span></span> <span data-ttu-id="ed529-221">Una prueba de supervisión da error si el código de respuesta HTTP es un error (4xx o 5xx) o si la respuesta se retrasa más de 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="ed529-221">A monitoring test fails if the HTTP response code is an error (4xx or 5xx) or the response takes more than 30 seconds.</span></span> <span data-ttu-id="ed529-222">Un extremo se considera disponible si sus pruebas de supervisión se realizan correctamente desde todas las ubicaciones especificadas.</span><span class="sxs-lookup"><span data-stu-id="ed529-222">An endpoint is considered available if the monitoring tests succeed from all the specified locations.</span></span> 

<span data-ttu-id="ed529-223">Para obtener más información, consulte [Supervisión de estado de extremo web].</span><span class="sxs-lookup"><span data-stu-id="ed529-223">For more information, see [How to: Monitor web endpoint status].</span></span>

> [!NOTE]
> <span data-ttu-id="ed529-224">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de inscribirse para abrir una cuenta de Azure, vaya a [Prueba del Servicio de aplicaciones], donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ed529-224">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ed529-225">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="ed529-225">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ed529-226">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ed529-226">Next steps</span></span>
* <span data-ttu-id="ed529-227">[Configuración de un nombre de dominio personalizado en el Servicio de aplicaciones de Azure]</span><span class="sxs-lookup"><span data-stu-id="ed529-227">[Configure a custom domain name in Azure App Service]</span></span>
* <span data-ttu-id="ed529-228">[Habilitación de HTTPS para una aplicación en el servicio de aplicaciones de Azure]</span><span class="sxs-lookup"><span data-stu-id="ed529-228">[Enable HTTPS for an app in Azure App Service]</span></span>
* <span data-ttu-id="ed529-229">[Escalación de una aplicación web en el Servicio de aplicaciones de Azure]</span><span class="sxs-lookup"><span data-stu-id="ed529-229">[Scale a web app in Azure App Service]</span></span>
* <span data-ttu-id="ed529-230">[Aspectos básicos de supervisión para las aplicaciones web en Servicio de aplicaciones de Azure]</span><span class="sxs-lookup"><span data-stu-id="ed529-230">[Monitoring basics for Web Apps in Azure App Service]</span></span>

<!-- URL List -->

<span data-ttu-id="ed529-231">[ASP.NET SignalR]: http://www.asp.net/signalr</span><span class="sxs-lookup"><span data-stu-id="ed529-231">[ASP.NET SignalR]: http://www.asp.net/signalr</span></span>
<span data-ttu-id="ed529-232">[Portal de Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="ed529-232">[Azure Portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="ed529-233">[Configuración de un nombre de dominio personalizado en el Servicio de aplicaciones de Azure]: ./app-service-web-tutorial-custom-domain.md</span><span class="sxs-lookup"><span data-stu-id="ed529-233">[Configure a custom domain name in Azure App Service]: ./app-service-web-tutorial-custom-domain.md</span></span>
<span data-ttu-id="ed529-234">[Configuración de entornos de ensayo para aplicaciones web en el Servicio de aplicaciones de Azure]: ./web-sites-staged-publishing.md</span><span class="sxs-lookup"><span data-stu-id="ed529-234">[Deploy to Staging Environments for Web Apps in Azure App Service]: ./web-sites-staged-publishing.md</span></span>
<span data-ttu-id="ed529-235">[Habilitación de HTTPS para una aplicación en el servicio de aplicaciones de Azure]: ./app-service-web-tutorial-custom-ssl.md</span><span class="sxs-lookup"><span data-stu-id="ed529-235">[Enable HTTPS for an app in Azure App Service]: ./app-service-web-tutorial-custom-ssl.md</span></span>
<span data-ttu-id="ed529-236">[Supervisión de estado de extremo web]: http://go.microsoft.com/fwLink/?LinkID=279906</span><span class="sxs-lookup"><span data-stu-id="ed529-236">[How to: Monitor web endpoint status]: http://go.microsoft.com/fwLink/?LinkID=279906</span></span>
<span data-ttu-id="ed529-237">[Aspectos básicos de supervisión para las aplicaciones web en Servicio de aplicaciones de Azure]: ./web-sites-monitor.md</span><span class="sxs-lookup"><span data-stu-id="ed529-237">[Monitoring basics for Web Apps in Azure App Service]: ./web-sites-monitor.md</span></span>
<span data-ttu-id="ed529-238">[modo de canalización]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application</span><span class="sxs-lookup"><span data-stu-id="ed529-238">[pipeline mode]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application</span></span>
<span data-ttu-id="ed529-239">[Escalación de una aplicación web en el Servicio de aplicaciones de Azure]: ./web-sites-scale.md</span><span class="sxs-lookup"><span data-stu-id="ed529-239">[Scale a web app in Azure App Service]: ./web-sites-scale.md</span></span>
<span data-ttu-id="ed529-240">[socket.io]: ./web-sites-nodejs-chat-app-socketio.md</span><span class="sxs-lookup"><span data-stu-id="ed529-240">[socket.io]: ./web-sites-nodejs-chat-app-socketio.md</span></span>
<span data-ttu-id="ed529-241">[Prueba del Servicio de aplicaciones]: https://azure.microsoft.com/try/app-service/</span><span class="sxs-lookup"><span data-stu-id="ed529-241">[Try App Service]: https://azure.microsoft.com/try/app-service/</span></span>

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
