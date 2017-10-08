---
title: "aaaConfigure las aplicaciones web en el servicio de aplicación de Azure"
description: "¿Cómo tooconfigure una aplicación web en servicios de aplicaciones de Azure"
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
ms.openlocfilehash: 8697ab6f21cfeb470e11f0d82c68692d43142fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a><span data-ttu-id="3b0d7-103">Configuración de aplicaciones web en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="3b0d7-103">Configure web apps in Azure App Service</span></span>
<span data-ttu-id="3b0d7-104">Este tema explica cómo Hola tooconfigure una aplicación web con [Portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="3b0d7-104">This topic explains how tooconfigure a web app using hello [Azure Portal].</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a><span data-ttu-id="3b0d7-105">Configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="3b0d7-105">Application settings</span></span>
1. <span data-ttu-id="3b0d7-106">Hola [Portal de Azure], abra hoja hello para la aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-106">In hello [Azure Portal], open hello blade for hello web app.</span></span>
2. <span data-ttu-id="3b0d7-107">Haga clic en **Toda la configuración**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-107">Click **All Settings**.</span></span>
3. <span data-ttu-id="3b0d7-108">Haga clic en **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-108">Click **Application Settings**.</span></span>

![Configuración de la aplicación][configure01]

<span data-ttu-id="3b0d7-110">Hola **configuración de la aplicación** hoja se agrupan en varias categorías de configuración.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-110">hello **Application settings** blade has settings grouped under several categories.</span></span>

### <a name="general-settings"></a><span data-ttu-id="3b0d7-111">Configuración general</span><span class="sxs-lookup"><span data-stu-id="3b0d7-111">General settings</span></span>
<span data-ttu-id="3b0d7-112">**Versiones del marco**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-112">**Framework versions**.</span></span> <span data-ttu-id="3b0d7-113">Configure estas opciones si su aplicación utiliza cualquiera de estos marcos:</span><span class="sxs-lookup"><span data-stu-id="3b0d7-113">Set these options if your app uses any these frameworks:</span></span> 

* <span data-ttu-id="3b0d7-114">**.NET framework**: versión de .NET framework de conjunto Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-114">**.NET Framework**: Set hello .NET framework version.</span></span> 
* <span data-ttu-id="3b0d7-115">**PHP**: versión de PHP de conjunto hello, o **OFF** toodisable PHP.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-115">**PHP**: Set hello PHP version, or **OFF** toodisable PHP.</span></span> 
* <span data-ttu-id="3b0d7-116">**Java**: versión de Java de hello Select o **OFF** toodisable Java.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-116">**Java**: Select hello Java version or **OFF** toodisable Java.</span></span> <span data-ttu-id="3b0d7-117">Hola de uso **contenedor Web** toochoose opción entre las versiones de Tomcat y Jetty.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-117">Use hello **Web Container** option toochoose between Tomcat and Jetty versions.</span></span>
* <span data-ttu-id="3b0d7-118">**Python**: versión de Python seleccione hello, o **OFF** toodisable Python.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-118">**Python**: Select hello Python version, or **OFF** toodisable Python.</span></span>

<span data-ttu-id="3b0d7-119">Por razones técnicas, si se habilita Java para la aplicación, deshabilita las opciones. NET, PHP y Python de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-119">For technical reasons, enabling Java for your app disables hello .NET, PHP, and Python options.</span></span>

<span data-ttu-id="3b0d7-120"><a name="platform"></a>
**Plataforma**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-120"><a name="platform"></a>
**Platform**.</span></span> <span data-ttu-id="3b0d7-121">Seleccione si su aplicación web se ejecuta en un entorno de 32 o 64 bits.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-121">Selects whether your web app runs in a 32-bit or 64-bit environment.</span></span> <span data-ttu-id="3b0d7-122">entorno de 64 bits de Hello requiere el modo básico o estándar.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-122">hello 64-bit environment requires Basic or Standard mode.</span></span> <span data-ttu-id="3b0d7-123">Los modos libre y compartido siempre se ejecutan en un entorno de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-123">Free and Shared modes always run in a 32-bit environment.</span></span>

<span data-ttu-id="3b0d7-124">**Sockets web**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-124">**Web Sockets**.</span></span> <span data-ttu-id="3b0d7-125">Establecer **ON** tooenable Hola protocolo WebSocket; por ejemplo, si su aplicación web usa [ASP.NET SignalR] o [socket.io].</span><span class="sxs-lookup"><span data-stu-id="3b0d7-125">Set **ON** tooenable hello WebSocket protocol; for example, if your web app uses [ASP.NET SignalR] or [socket.io].</span></span>

<span data-ttu-id="3b0d7-126"><a name="alwayson"></a>
**AlwaysOn**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-126"><a name="alwayson"></a>
**Always On**.</span></span> <span data-ttu-id="3b0d7-127">De forma predeterminada, las aplicaciones web se descargan si están inactivas durante algún tiempo.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-127">By default, web apps are unloaded if they are idle for some period of time.</span></span> <span data-ttu-id="3b0d7-128">Esto permite que el sistema de hello conservar los recursos.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-128">This lets hello system conserve resources.</span></span> <span data-ttu-id="3b0d7-129">En el modo básico o estándar, puede habilitar **Always On** tookeep Hola aplicación carga todo el tiempo Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-129">In Basic or Standard mode, you can enable **Always On** tookeep hello app loaded all hello time.</span></span> <span data-ttu-id="3b0d7-130">Si la aplicación ejecuta trabajos Web continuos o se ejecuta trabajos Web desencadena mediante una expresión CRON, debe habilitar **Always On**, o trabajos de hello web no pueden ejecutar de forma confiable.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-130">If your app runs continuous WebJobs or runs WebJobs triggered using a CRON expression, you should enable **Always On**, or hello web jobs may not run reliably.</span></span>

<span data-ttu-id="3b0d7-131">**Versión de canalización administrada**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-131">**Managed Pipeline Version**.</span></span> <span data-ttu-id="3b0d7-132">Conjuntos de Hola IIS [el modo de canalización].</span><span class="sxs-lookup"><span data-stu-id="3b0d7-132">Sets hello IIS [pipeline mode].</span></span> <span data-ttu-id="3b0d7-133">Deje este conjunto tooIntegrated (valor predeterminado de hello) a menos que tenga una aplicación heredada que requiere una versión anterior de IIS.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-133">Leave this set tooIntegrated (hello default) unless you have a legacy app that requires an older version of IIS.</span></span>

<span data-ttu-id="3b0d7-134">**Intercambio automático**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-134">**Auto Swap**.</span></span> <span data-ttu-id="3b0d7-135">Si habilita el intercambio automático de una ranura de implementación, servicio de aplicaciones automáticamente intercambiará aplicación web de hello en producción cuando realice una inserción una ranura de toothat de actualización.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-135">If you enable Auto Swap for a deployment slot, App Service will automatically swap hello web app into production when you push an update toothat slot.</span></span> <span data-ttu-id="3b0d7-136">Para obtener más información, consulte [implementar toostaging ranuras de las aplicaciones web de servicio de aplicaciones de Azure](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="3b0d7-136">For more information, see [Deploy toostaging slots for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span>

### <a name="debugging"></a><span data-ttu-id="3b0d7-137">Depuración</span><span class="sxs-lookup"><span data-stu-id="3b0d7-137">Debugging</span></span>
<span data-ttu-id="3b0d7-138">**Depuración remota**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-138">**Remote Debugging**.</span></span> <span data-ttu-id="3b0d7-139">Habilita la depuración remota.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-139">Enables remote debugging.</span></span> <span data-ttu-id="3b0d7-140">Cuando está habilitada, puede utilizar a depurador remoto hello en Visual Studio tooconnect directamente tooyour aplicación web.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-140">When enabled, you can use hello remote debugger in Visual Studio tooconnect directly tooyour web app.</span></span> <span data-ttu-id="3b0d7-141">La depuración remota permanecerá habilitada durante 48 horas.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-141">Remote debugging will remain enabled for 48 hours.</span></span> 

### <a name="app-settings"></a><span data-ttu-id="3b0d7-142">Configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="3b0d7-142">App settings</span></span>
<span data-ttu-id="3b0d7-143">Esta sección contiene las parejas de nombre y valor que la aplicación web cargará al inicio.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-143">This section contains name/value pairs that you web app will load on start up.</span></span> 

* <span data-ttu-id="3b0d7-144">En las aplicaciones .NET, estas configuraciones se insertarán en la sección de la configuración de .NET `AppSettings` en tiempo de ejecución y reemplazará la configuración existente.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-144">For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings.</span></span> 
* <span data-ttu-id="3b0d7-145">Las aplicaciones PHP, Python, Java y Node pueden acceder a estas configuraciones como variables de entorno en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-145">PHP, Python, Java and Node applications can access these settings as environment variables at runtime.</span></span> <span data-ttu-id="3b0d7-146">Para cada configuración de la aplicación, se crean dos variables de entorno; uno con el nombre de hello especificado por la entrada de configuración de aplicación hello y otro con el prefijo APPSETTING_.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-146">For each app setting, two environment variables are created; one with hello name specified by hello app setting entry, and another with a prefix of APPSETTING_.</span></span> <span data-ttu-id="3b0d7-147">Ambos contienen Hola mismo valor.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-147">Both contain hello same value.</span></span>

### <a name="connection-strings"></a><span data-ttu-id="3b0d7-148">Cadenas de conexión</span><span class="sxs-lookup"><span data-stu-id="3b0d7-148">Connection strings</span></span>
<span data-ttu-id="3b0d7-149">Cadenas de conexión para los recursos vinculados.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-149">Connection strings for linked resources.</span></span> 

<span data-ttu-id="3b0d7-150">Para las aplicaciones. NET, estas cadenas de conexión se insertan en la configuración de .NET `connectionStrings` configuración en tiempo de ejecución, invalidando las entradas existentes que sea igual que la clave de Hola Hola nombre vinculado de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-150">For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where hello key equals hello linked database name.</span></span> 

<span data-ttu-id="3b0d7-151">Para las aplicaciones PHP, Python, Java y Node, esta configuración estará disponible como variables de entorno en tiempo de ejecución, el prefijo con el tipo de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-151">For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with hello connection type.</span></span> <span data-ttu-id="3b0d7-152">prefijos de variable de entorno de Hello son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="3b0d7-152">hello environment variable prefixes are as follows:</span></span> 

* <span data-ttu-id="3b0d7-153">SQL Server: `SQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="3b0d7-153">SQL Server: `SQLCONNSTR_`</span></span>
* <span data-ttu-id="3b0d7-154">MySQL: `MYSQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="3b0d7-154">MySQL: `MYSQLCONNSTR_`</span></span>
* <span data-ttu-id="3b0d7-155">Base de datos SQL: `SQLAZURECONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="3b0d7-155">SQL Database: `SQLAZURECONNSTR_`</span></span>
* <span data-ttu-id="3b0d7-156">Personalizado: `CUSTOMCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="3b0d7-156">Custom: `CUSTOMCONNSTR_`</span></span>

<span data-ttu-id="3b0d7-157">Por ejemplo, si una cadena de conexión de MySql se denomina `connectionstring1`, podría tener acceso a ella a través de la variable de entorno de hello `MYSQLCONNSTR_connectionString1`.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-157">For example, if a MySql connection string were named `connectionstring1`, it would be accessed through hello environment variable `MYSQLCONNSTR_connectionString1`.</span></span>

### <a name="default-documents"></a><span data-ttu-id="3b0d7-158">Documentos predeterminados</span><span class="sxs-lookup"><span data-stu-id="3b0d7-158">Default documents</span></span>
<span data-ttu-id="3b0d7-159">documento predeterminado de Hello es hello web página que se muestra en la dirección URL raíz de Hola para un sitio Web.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-159">hello default document is hello web page that is displayed at hello root URL for a website.</span></span>  <span data-ttu-id="3b0d7-160">se utiliza el primer archivo coincidente Hello en lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-160">hello first matching file in hello list is used.</span></span> 

<span data-ttu-id="3b0d7-161">Es posible que las aplicaciones utilicen módulos que enruten en base a la URL, en lugar de ofrecer funcionalidad a contenido estático, en cuyo caso no existe realmente un documento predeterminado.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-161">Web apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.</span></span>    

### <a name="handler-mappings"></a><span data-ttu-id="3b0d7-162">Asignaciones de controlador</span><span class="sxs-lookup"><span data-stu-id="3b0d7-162">Handler mappings</span></span>
<span data-ttu-id="3b0d7-163">Usar este solicitudes de toohandle de procesadores de script personalizado de área tooadd para determinadas extensiones de archivo.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-163">Use this area tooadd custom script processors toohandle requests for specific file extensions.</span></span> 

* <span data-ttu-id="3b0d7-164">**Extensión**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-164">**Extension**.</span></span> <span data-ttu-id="3b0d7-165">Controla el toobe de extensión de archivo Hello, por ejemplo, *.php o handler.fcgi.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-165">hello file extension toobe handled, such as *.php or handler.fcgi.</span></span> 
* <span data-ttu-id="3b0d7-166">**Ruta de acceso del procesador de script**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-166">**Script Processor Path**.</span></span> <span data-ttu-id="3b0d7-167">Hola ruta de acceso absoluta del procesador de script de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-167">hello absolute path of hello script processor.</span></span> <span data-ttu-id="3b0d7-168">Procesador de script de Hola procesará toofiles las solicitudes que coinciden con la extensión de archivo Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-168">Requests toofiles that match hello file extension will be processed by hello script processor.</span></span> <span data-ttu-id="3b0d7-169">Usar ruta de acceso de hello `D:\home\site\wwwroot` directorio raíz de la aplicación de toorefer tooyour.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-169">Use hello path `D:\home\site\wwwroot` toorefer tooyour app's root directory.</span></span>
* <span data-ttu-id="3b0d7-170">**Argumentos adicionales**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-170">**Additional Arguments**.</span></span> <span data-ttu-id="3b0d7-171">Argumentos de línea de comandos opcionales para el procesador de script de Hola</span><span class="sxs-lookup"><span data-stu-id="3b0d7-171">Optional command-line arguments for hello script processor</span></span> 

### <a name="virtual-applications-and-directories"></a><span data-ttu-id="3b0d7-172">Directorios y aplicaciones virtuales</span><span class="sxs-lookup"><span data-stu-id="3b0d7-172">Virtual applications and directories</span></span>
<span data-ttu-id="3b0d7-173">tooconfigure de aplicaciones virtuales y directorios, especifique cada directorio virtual y su correspondiente raíz del sitio Web de toohello relativa de ruta de acceso física.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-173">tooconfigure virtual applications and directories, specify each virtual directory and its corresponding physical path relative toohello website root.</span></span> <span data-ttu-id="3b0d7-174">Si lo desea, puede seleccionar hello **aplicación** casilla toomark un directorio virtual como una aplicación.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-174">Optionally, you can select hello **Application** checkbox toomark a virtual directory as an application.</span></span>

## <a name="enabling-diagnostic-logs"></a><span data-ttu-id="3b0d7-175">Habilitación de registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="3b0d7-175">Enabling diagnostic logs</span></span>
<span data-ttu-id="3b0d7-176">registros de diagnóstico de tooenable:</span><span class="sxs-lookup"><span data-stu-id="3b0d7-176">tooenable diagnostic logs:</span></span>

1. <span data-ttu-id="3b0d7-177">En la hoja de hello para la aplicación web, haga clic en **toda la configuración de**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-177">In hello blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="3b0d7-178">Haga clic en **Registros de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-178">Click **Diagnostic logs**.</span></span> 

<span data-ttu-id="3b0d7-179">Opciones para escribir registros de diagnóstico de una aplicación web que admita el registro:</span><span class="sxs-lookup"><span data-stu-id="3b0d7-179">Options for writing diagnostic logs from a web application that supports logging:</span></span> 

* <span data-ttu-id="3b0d7-180">**Registro de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-180">**Application Logging**.</span></span> <span data-ttu-id="3b0d7-181">Escribe registros de la aplicación de sistema de archivos de toohello.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-181">Writes application logs toohello file system.</span></span> <span data-ttu-id="3b0d7-182">El registro dura un período de 12 horas.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-182">Logging lasts for a period of 12 hours.</span></span> 

<span data-ttu-id="3b0d7-183">**Nivel**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-183">**Level**.</span></span> <span data-ttu-id="3b0d7-184">Cuando se habilita el registro de aplicación, esta opción especifica la cantidad de Hola de información que será registrados (Error, advertencia, información o detallado).</span><span class="sxs-lookup"><span data-stu-id="3b0d7-184">When application logging is enabled, this option specifies hello amount of information that will be recorded (Error, Warning, Information, or Verbose).</span></span>

<span data-ttu-id="3b0d7-185">**Registro del servidor web**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-185">**Web server logging**.</span></span> <span data-ttu-id="3b0d7-186">Los registros se guardan en formato de archivo de registro extendido W3C de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-186">Logs are saved in hello W3C extended log file format.</span></span> 

<span data-ttu-id="3b0d7-187">**Mensajes de error detallados**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-187">**Detailed error messages**.</span></span> <span data-ttu-id="3b0d7-188">Guarda archivos .htm de mensajes de error detallados.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-188">Saves detailed error messages .htm files.</span></span> <span data-ttu-id="3b0d7-189">Hola archivos se guardan en /LogFiles/DetailedErrors.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-189">hello files are saved under /LogFiles/DetailedErrors.</span></span> 

<span data-ttu-id="3b0d7-190">**Seguimiento de solicitudes erróneas**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-190">**Failed request tracing**.</span></span> <span data-ttu-id="3b0d7-191">Registros de error en las solicitudes tooXML archivos.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-191">Logs failed requests tooXML files.</span></span> <span data-ttu-id="3b0d7-192">Hola se guardan los archivos bajo/LogFiles/W3SVC*xxx*, donde xxx es un identificador único.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-192">hello files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier.</span></span> <span data-ttu-id="3b0d7-193">Esta carpeta contiene un archivo XSL y uno o varios archivos XML.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-193">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="3b0d7-194">Asegúrese de Hola de toodownload seguro archivo XSL, porque proporciona la funcionalidad para dar formato y filtrar el contenido de Hola Hola de archivos de XML.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-194">Make sure toodownload hello XSL file, because it provides functionality for formatting and filtering hello contents of hello XML files.</span></span>

<span data-ttu-id="3b0d7-195">archivos de registro de hello tooview, debe crear las credenciales FTP, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="3b0d7-195">tooview hello log files, you must create FTP credentials, as follows:</span></span>

1. <span data-ttu-id="3b0d7-196">En la hoja de hello para la aplicación web, haga clic en **toda la configuración de**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-196">In hello blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="3b0d7-197">Haga clic en **Credenciales de implementación**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-197">Click **Deployment credentials**.</span></span>
3. <span data-ttu-id="3b0d7-198">Escriba un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-198">Enter a user name and password.</span></span>
4. <span data-ttu-id="3b0d7-199">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-199">Click **Save**.</span></span>

![Configurar credenciales de implementación][configure03]

<span data-ttu-id="3b0d7-201">nombre de usuario FTP completo Hello es "app\username" donde *aplicación* es Hola nombre de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-201">hello full FTP user name is “app\username” where *app* is hello name of your web app.</span></span> <span data-ttu-id="3b0d7-202">Hello nombre de usuario aparece en la hoja de la aplicación hello web, en **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-202">hello username is listed in hello web app blade, under **Essentials**.</span></span>  

![Credenciales de implementación de FTP][configure02]

## <a name="other-configuration-tasks"></a><span data-ttu-id="3b0d7-204">Otras tareas de configuración</span><span class="sxs-lookup"><span data-stu-id="3b0d7-204">Other configuration tasks</span></span>
### <a name="ssl"></a><span data-ttu-id="3b0d7-205">SSL</span><span class="sxs-lookup"><span data-stu-id="3b0d7-205">SSL</span></span>
<span data-ttu-id="3b0d7-206">En modo básico o estándar puede cargar certificados SSL para un dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-206">In Basic or Standard mode, you can upload SSL certificates for a custom domain.</span></span> <span data-ttu-id="3b0d7-207">Para más información, consulte [Habilitación de HTTPS para una aplicación web].</span><span class="sxs-lookup"><span data-stu-id="3b0d7-207">For more information, see [Enable HTTPS for a web app].</span></span> 

<span data-ttu-id="3b0d7-208">tooview los certificados cargados, haga clic en ejecutar **toda la configuración de** > **los dominios personalizados y SSL**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-208">tooview your uploaded certificates, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="domain-names"></a><span data-ttu-id="3b0d7-209">Nombres de dominio</span><span class="sxs-lookup"><span data-stu-id="3b0d7-209">Domain names</span></span>
<span data-ttu-id="3b0d7-210">Agregue nombres de dominio personalizados para su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-210">Add custom domain names for your web app.</span></span> <span data-ttu-id="3b0d7-211">Para más información, consulte [Configuración de un nombre de dominio personalizado para una aplicación web en el servicio de aplicaciones de Azure].</span><span class="sxs-lookup"><span data-stu-id="3b0d7-211">For more information, see [Configure a custom domain name for a web app in Azure App Service].</span></span>

<span data-ttu-id="3b0d7-212">tooview sus nombres de dominio, haga clic en ejecutar **toda la configuración de** > **los dominios personalizados y SSL**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-212">tooview your domain names, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="deployments"></a><span data-ttu-id="3b0d7-213">Implementaciones</span><span class="sxs-lookup"><span data-stu-id="3b0d7-213">Deployments</span></span>
* <span data-ttu-id="3b0d7-214">Configure la implementación continua.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-214">Set up continuous deployment.</span></span> <span data-ttu-id="3b0d7-215">Vea [toodeploy Git usando las aplicaciones Web en el servicio de aplicación de Azure](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="3b0d7-215">See [Using Git toodeploy Web Apps in Azure App Service](web-sites-deploy.md).</span></span>
* <span data-ttu-id="3b0d7-216">Ranuras de implementación.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-216">Deployment slots.</span></span> <span data-ttu-id="3b0d7-217">Vea [implementar entornos de tooStaging para las aplicaciones Web en el servicio de aplicación de Azure].</span><span class="sxs-lookup"><span data-stu-id="3b0d7-217">See [Deploy tooStaging Environments for Web Apps in Azure App Service].</span></span>

<span data-ttu-id="3b0d7-218">tooview las ranuras de implementación, haga clic en ejecutar **toda la configuración de** > **ranuras de implementación**.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-218">tooview your deployment slots, click **All Settings** > **Deployment slots**.</span></span>

### <a name="monitoring"></a><span data-ttu-id="3b0d7-219">Supervisión</span><span class="sxs-lookup"><span data-stu-id="3b0d7-219">Monitoring</span></span>
<span data-ttu-id="3b0d7-220">En el modo básico o estándar, puede probar la disponibilidad Hola de extremos HTTP o HTTPS, desde ubicaciones distribuidas geográficamente de toothree.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-220">In Basic or Standard mode, you can  test hello availability of HTTP or HTTPS endpoints, from up toothree geo-distributed locations.</span></span> <span data-ttu-id="3b0d7-221">Se produce un error en una prueba de supervisión si Hola código de respuesta HTTP es un error (4xx o 5xx) o respuesta de hello tarda más de 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-221">A monitoring test fails if hello HTTP response code is an error (4xx or 5xx) or hello response takes more than 30 seconds.</span></span> <span data-ttu-id="3b0d7-222">Un punto de conexión se considera disponible si pruebas de supervisión de hello sean correctas de todos los Hola especificado ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-222">An endpoint is considered available if hello monitoring tests succeed from all hello specified locations.</span></span> 

<span data-ttu-id="3b0d7-223">Para obtener más información, consulte [Supervisión de estado de extremo web].</span><span class="sxs-lookup"><span data-stu-id="3b0d7-223">For more information, see [How to: Monitor web endpoint status].</span></span>

> [!NOTE]
> <span data-ttu-id="3b0d7-224">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones], donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-224">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="3b0d7-225">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="3b0d7-225">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="3b0d7-226">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3b0d7-226">Next steps</span></span>
* <span data-ttu-id="3b0d7-227">[Configuración de un nombre de dominio personalizado en el Servicio de aplicaciones de Azure]</span><span class="sxs-lookup"><span data-stu-id="3b0d7-227">[Configure a custom domain name in Azure App Service]</span></span>
* <span data-ttu-id="3b0d7-228">[Habilitación de HTTPS para una aplicación en el servicio de aplicaciones de Azure]</span><span class="sxs-lookup"><span data-stu-id="3b0d7-228">[Enable HTTPS for an app in Azure App Service]</span></span>
* <span data-ttu-id="3b0d7-229">[Escalación de una aplicación web en el Servicio de aplicaciones de Azure]</span><span class="sxs-lookup"><span data-stu-id="3b0d7-229">[Scale a web app in Azure App Service]</span></span>
* <span data-ttu-id="3b0d7-230">[Aspectos básicos de supervisión para las aplicaciones web en Servicio de aplicaciones de Azure]</span><span class="sxs-lookup"><span data-stu-id="3b0d7-230">[Monitoring basics for Web Apps in Azure App Service]</span></span>

<!-- URL List -->

[ASP.NET SignalR]: http://www.asp.net/signalr
[Portal de Azure]: https://portal.azure.com/
[Configuración de un nombre de dominio personalizado en el Servicio de aplicaciones de Azure]: ./app-service-web-tutorial-custom-domain.md
[implementar entornos de tooStaging para las aplicaciones Web en el servicio de aplicación de Azure]: ./web-sites-staged-publishing.md
[Habilitación de HTTPS para una aplicación en el servicio de aplicaciones de Azure]: ./app-service-web-tutorial-custom-ssl.md
[Supervisión de estado de extremo web]: http://go.microsoft.com/fwLink/?LinkID=279906
[Aspectos básicos de supervisión para las aplicaciones web en Servicio de aplicaciones de Azure]: ./web-sites-monitor.md
[el modo de canalización]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application
[Escalación de una aplicación web en el Servicio de aplicaciones de Azure]: ./web-sites-scale.md
[socket.io]: ./web-sites-nodejs-chat-app-socketio.md
[pruebe el servicio de aplicaciones]: https://azure.microsoft.com/try/app-service/

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
