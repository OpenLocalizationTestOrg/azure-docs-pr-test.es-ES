---
title: "aaaHow toodebug una aplicación web de Node.js en el servicio de aplicación de Azure"
description: "Obtenga información acerca de cómo toodebug una Node.js web aplicación de servicio de aplicaciones de Azure."
tags: azure-portal
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: a48f906c-1a3e-43bc-ae84-7d2dde175b15
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 888ec5c3f92cfc3aeea4ea86005b9b6a0d1306ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-a-nodejs-web-app-in-azure-app-service"></a><span data-ttu-id="09dd2-103">Cómo toodebug una Node.js web aplicación de servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="09dd2-103">How toodebug a Node.js web app in Azure App Service</span></span>
<span data-ttu-id="09dd2-104">Azure proporciona diagnósticos integrados tooassist con la depuración de aplicaciones Node.js hospedadas en [servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) aplicaciones Web.</span><span class="sxs-lookup"><span data-stu-id="09dd2-104">Azure provides built-in diagnostics tooassist with debugging Node.js applications hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="09dd2-105">En este artículo, aprenderá cómo tooenable registro de stdout y stderr, mostrar información de error en el Explorador de hello, y cómo toodownload y ver archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="09dd2-105">In this article, you will learn how tooenable logging of stdout and stderr, display error information in hello browser, and how toodownload and view log files.</span></span>

<span data-ttu-id="09dd2-106">El diagnóstico de las aplicaciones Node.js hospedadas en Azure lo proporciona [IISNode].</span><span class="sxs-lookup"><span data-stu-id="09dd2-106">Diagnostics for Node.js applications hosted on Azure is provided by [IISNode].</span></span> <span data-ttu-id="09dd2-107">Aunque este artículo describe la configuración más común de Hola para recopilar información de diagnóstico, no proporciona una referencia completa para trabajar con IISNode.</span><span class="sxs-lookup"><span data-stu-id="09dd2-107">While this article discusses hello most common settings for gathering diagnostics information, it does not provide a complete reference for working with IISNode.</span></span> <span data-ttu-id="09dd2-108">Para obtener más información sobre cómo trabajar con IISNode, vea hello [IISNode Readme] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="09dd2-108">For more information on working with IISNode, see hello [IISNode Readme] on GitHub.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="09dd2-109">Habilitación del registro</span><span class="sxs-lookup"><span data-stu-id="09dd2-109">Enable logging</span></span>
<span data-ttu-id="09dd2-110">De manera predeterminada, una aplicación web del Servicio de aplicaciones solo captura información de diagnóstico sobre las implementaciones, como cuando se realiza la implementación de un sitio web con Git.</span><span class="sxs-lookup"><span data-stu-id="09dd2-110">By default, an App Service web app only captures diagnostic information about deployments, such as when you deploy a web app using Git.</span></span> <span data-ttu-id="09dd2-111">Esta información es útil si está teniendo problemas durante la implementación, como un error al instalar un módulo al que se hace referencia en **package.json**o si va a usar un script de implementación personalizado.</span><span class="sxs-lookup"><span data-stu-id="09dd2-111">This information is useful if you are having problems during deployment, such as a failure when installing a module referenced in **package.json**, or if you are using a custom deployment script.</span></span>

<span data-ttu-id="09dd2-112">Hola tooenable registro de secuencias de stdout y stderr, debe crear un **IISNode.yml** de archivos en la raíz de saludo de la aplicación Node.js y agregue Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="09dd2-112">tooenable hello logging of stdout and stderr streams, you must create an **IISNode.yml** file at hello root of your Node.js application and add hello following:</span></span>

    loggingEnabled: true

<span data-ttu-id="09dd2-113">Esto habilita el registro de hello de stderr y stdout de la aplicación Node.js.</span><span class="sxs-lookup"><span data-stu-id="09dd2-113">This enables hello logging of stderr and stdout from your Node.js application.</span></span>

<span data-ttu-id="09dd2-114">Hola **IISNode.yml** archivo también puede ser usado toocontrol si errores descriptivos o errores de desarrollador se devuelven toohello explorador cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="09dd2-114">hello **IISNode.yml** file can also be used toocontrol whether friendly errors or developer errors are returned toohello browser when a failure occurs.</span></span> <span data-ttu-id="09dd2-115">errores del desarrollador tooenable, agregar Hola después línea toohello **IISNode.yml** archivo:</span><span class="sxs-lookup"><span data-stu-id="09dd2-115">tooenable developer errors, add hello following line toohello **IISNode.yml** file:</span></span>

    devErrorsEnabled: true

<span data-ttu-id="09dd2-116">Una vez habilitada esta opción, IISNode devolverá Hola última 64K de información que se envía toostderr en lugar de un error descriptivo, como "se produjo un error interno del servidor".</span><span class="sxs-lookup"><span data-stu-id="09dd2-116">Once this option is enabled, IISNode will return hello last 64K of information sent toostderr instead of a friendly error such as "an internal server error occurred".</span></span>

> [!NOTE]
> <span data-ttu-id="09dd2-117">Aunque devErrorsEnabled es útil cuando se diagnostican problemas durante el desarrollo, habilitarla en un entorno de producción puede provocar errores de programación que se envían los usuarios de tooend.</span><span class="sxs-lookup"><span data-stu-id="09dd2-117">While devErrorsEnabled is useful when diagnosing problems during development, enabling it in a production environment may result in development errors being sent tooend users.</span></span>
> 
> 

<span data-ttu-id="09dd2-118">Si hello **IISNode.yml** archivo ya no existe en la aplicación, debe reiniciar la aplicación web después de publicar la aplicación hello actualizado.</span><span class="sxs-lookup"><span data-stu-id="09dd2-118">If hello **IISNode.yml** file did not already exist within your application, you must restart your web app after publishing hello updated application.</span></span> <span data-ttu-id="09dd2-119">Si solamente va a cambiar la configuración de un archivo **IISNode.yml** existente que ya se publicó anteriormente, no es necesario reiniciar.</span><span class="sxs-lookup"><span data-stu-id="09dd2-119">If you are simply changing settings in an existing **IISNode.yml** file that has previously been published, no restart is required.</span></span>

> [!NOTE]
> <span data-ttu-id="09dd2-120">Si la aplicación web se creó mediante herramientas de línea de comandos de Azure de Hola o los PowerShell Cmdlets de Azure, valor predeterminado es **IISNode.yml** archivo se crea automáticamente.</span><span class="sxs-lookup"><span data-stu-id="09dd2-120">If your web app was created using hello Azure Command-Line Tools or Azure PowerShell Cmdlets, a default **IISNode.yml** file is automatically created.</span></span>
> 
> 

<span data-ttu-id="09dd2-121">toorestart hello web aplicación, una aplicación web de seleccione Hola Hola [Portal de Azure](https://portal.azure.com)y, a continuación, haga clic en **reiniciar** botón:</span><span class="sxs-lookup"><span data-stu-id="09dd2-121">toorestart hello web app, select hello web app in hello [Azure Portal](https://portal.azure.com), and then click **RESTART** button:</span></span>

![Botón de reinicio][restart-button]

<span data-ttu-id="09dd2-123">Si se instalan herramientas de línea de comandos de Azure de hello en el entorno de desarrollo, puede usar Hola después de la aplicación web de comando toorestart hello:</span><span class="sxs-lookup"><span data-stu-id="09dd2-123">If hello Azure Command-Line Tools are installed in your development environment, you can use hello following command toorestart hello web app:</span></span>

    azure site restart [sitename]

> [!NOTE]
> <span data-ttu-id="09dd2-124">Aunque loggingEnabled y devErrorsEnabled son opciones de configuración de IISNode.yml Hola suelen usada para capturar información de diagnóstico, IISNode.yml puede ser usado tooconfigure una variedad de opciones para el entorno de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="09dd2-124">While loggingEnabled and devErrorsEnabled are hello most commonly used IISNode.yml configuration options for capturing diagnostic information, IISNode.yml can be used tooconfigure a variety of options for your hosting environment.</span></span> <span data-ttu-id="09dd2-125">Para obtener una lista completa de opciones de configuración de hello, vea hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) archivo.</span><span class="sxs-lookup"><span data-stu-id="09dd2-125">For a full list of hello configuration options, see hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.</span></span>
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a><span data-ttu-id="09dd2-126">Acceso a los registros</span><span class="sxs-lookup"><span data-stu-id="09dd2-126">Accessing logs</span></span>
<span data-ttu-id="09dd2-127">Pueden tener acceso a registros de diagnóstico de tres maneras; Usa Hola archivo de protocolo de transferencia (FTP), descargar un archivo Zip, o como activo actualiza el flujo de registro de hello (también conocido como una cola).</span><span class="sxs-lookup"><span data-stu-id="09dd2-127">Diagnostic logs can be accessed in three ways; Using hello File Transfer Protocol (FTP), downloading a Zip archive, or as a live updated stream of hello log (also known as a tail).</span></span> <span data-ttu-id="09dd2-128">Descargar el archivo Zip de Hola Hola de archivos de registro o ver la secuencia en directo de hello requieren herramientas de línea de comandos de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="09dd2-128">Downloading hello Zip archive of hello log files or viewing hello live stream require hello Azure Command-Line Tools.</span></span> <span data-ttu-id="09dd2-129">Estos pueden instalarse mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="09dd2-129">These can be installed by using hello following command:</span></span>

    npm install azure-cli -g

<span data-ttu-id="09dd2-130">Una vez instalado, se pueden acceder a herramientas de hello mediante comando hello 'azure'.</span><span class="sxs-lookup"><span data-stu-id="09dd2-130">Once installed, hello tools can be accessed using hello 'azure' command.</span></span> <span data-ttu-id="09dd2-131">Hola herramientas de línea de comandos debe estar configurado toouse su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="09dd2-131">hello command-line tools must first be configured toouse your Azure subscription.</span></span> <span data-ttu-id="09dd2-132">Para obtener información sobre cómo tooaccomplish esta tarea, vea hello **cómo toodownload e importar configuración de publicación** sección de hello [cómo tooUse Hola herramientas de línea de comandos de Azure](../xplat-cli-connect.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="09dd2-132">For information on how tooaccomplish this task, see hello **How toodownload and import publish settings** section of hello [How tooUse hello Azure Command-Line Tools](../xplat-cli-connect.md) article.</span></span>

### <a name="ftp"></a><span data-ttu-id="09dd2-133">FTP</span><span class="sxs-lookup"><span data-stu-id="09dd2-133">FTP</span></span>
<span data-ttu-id="09dd2-134">información de diagnóstico de hello tooaccess a través de FTP, visite hello [Portal de Azure](https://portal.azure.com), seleccione la aplicación web y, a continuación, seleccione hello **panel**.</span><span class="sxs-lookup"><span data-stu-id="09dd2-134">tooaccess hello diagnostic information through FTP, visit hello [Azure Portal](https://portal.azure.com), select your web app, and then select hello **DASHBOARD**.</span></span> <span data-ttu-id="09dd2-135">Hola **vínculos rápidos** sección hello **registros de diagnóstico FTP** y **registros de diagnóstico FTPS** vínculos proporcionan acceso toohello registros mediante el protocolo de hello FTP.</span><span class="sxs-lookup"><span data-stu-id="09dd2-135">In hello **quick links** section, hello **FTP DIAGNOSTIC LOGS** and **FTPS DIAGNOSTIC LOGS** links provide access toohello logs using hello FTP protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="09dd2-136">Si se aún no has configurado el nombre de usuario y la contraseña de FTP o implementación, puede hacerlo desde hello **inicio rápido** página de administración seleccionando **configurar credenciales de implementación**.</span><span class="sxs-lookup"><span data-stu-id="09dd2-136">If you have not previously configured user name and password for FTP or deployment, you can do so from hello **Quickstart** management page by selecting **Set up deployment credentials**.</span></span>
> 
> 

<span data-ttu-id="09dd2-137">Hola direcciones URL de FTP que se devuelven en el panel de hello es para hello **LogFiles** directorio, que incluirá Hola siguientes subdirectorios:</span><span class="sxs-lookup"><span data-stu-id="09dd2-137">hello FTP URL returned in hello dashboard is for hello **LogFiles** directory, which will contain hello following sub-directories:</span></span>

* <span data-ttu-id="09dd2-138">[Método de implementación](web-sites-deploy.md) -si utiliza un método de implementación como Git, un directorio de hello mismo nombre, se creará y contendrá la información relacionada con toodeployments.</span><span class="sxs-lookup"><span data-stu-id="09dd2-138">[Deployment Method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of hello same name will be created and will contain information related toodeployments.</span></span>
* <span data-ttu-id="09dd2-139">nodejs: La información de Stdout y stderr capturada desde todas las instancias de su aplicación (cuando loggingEnabled es verdadero).</span><span class="sxs-lookup"><span data-stu-id="09dd2-139">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="zip-archive"></a><span data-ttu-id="09dd2-140">Archivo Zip</span><span class="sxs-lookup"><span data-stu-id="09dd2-140">Zip archive</span></span>
<span data-ttu-id="09dd2-141">toodownload un archivo Zip de registros de diagnóstico de Hola Hola de uso siguiente comando desde herramientas de línea de comandos de hello Azure:</span><span class="sxs-lookup"><span data-stu-id="09dd2-141">toodownload a Zip archive of hello diagnostic logs, use hello following command from hello Azure Command-Line Tools:</span></span>

    azure site log download [sitename]

<span data-ttu-id="09dd2-142">Se descargará un **diagnostics.zip** en el directorio actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="09dd2-142">This will download a **diagnostics.zip** in hello current directory.</span></span> <span data-ttu-id="09dd2-143">Este archivo contiene Hola siguiendo la estructura de directorios:</span><span class="sxs-lookup"><span data-stu-id="09dd2-143">This archive contains hello following directory structure:</span></span>

* <span data-ttu-id="09dd2-144">deployments: Un registro de información sobre las implementaciones de su aplicación</span><span class="sxs-lookup"><span data-stu-id="09dd2-144">deployments - A log of information about deployments of your application</span></span>
* <span data-ttu-id="09dd2-145">LogFiles</span><span class="sxs-lookup"><span data-stu-id="09dd2-145">LogFiles</span></span>
  
  * <span data-ttu-id="09dd2-146">[Método de implementación](web-sites-deploy.md) -si utiliza un método de implementación como Git, un directorio de hello mismo nombre, se creará y contendrá la información relacionada con toodeployments.</span><span class="sxs-lookup"><span data-stu-id="09dd2-146">[Deployment method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of hello same name will be created and will contain information related toodeployments.</span></span>
  * <span data-ttu-id="09dd2-147">nodejs: La información de Stdout y stderr capturada desde todas las instancias de su aplicación (cuando loggingEnabled es verdadero).</span><span class="sxs-lookup"><span data-stu-id="09dd2-147">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="live-stream-tail"></a><span data-ttu-id="09dd2-148">Secuencia en directo (cola)</span><span class="sxs-lookup"><span data-stu-id="09dd2-148">Live stream (tail)</span></span>
<span data-ttu-id="09dd2-149">tooview una secuencia en directo de la información de registro de diagnóstico, Hola de uso siguiente comando desde herramientas de línea de comandos de hello Azure:</span><span class="sxs-lookup"><span data-stu-id="09dd2-149">tooview a live stream of diagnostic log information, use hello following command from hello Azure Command-Line Tools:</span></span>

    azure site log tail [sitename]

<span data-ttu-id="09dd2-150">Esto devolverá una secuencia de eventos de registro que se actualizan cuando se producen en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="09dd2-150">This will return a stream of log events that are updated as they occur on hello server.</span></span> <span data-ttu-id="09dd2-151">Esta secuencia devolverá información de implementación además de información de stdout y stderr (cuando loggingEnabled es verdadero).</span><span class="sxs-lookup"><span data-stu-id="09dd2-151">This stream will return deployment information as well as stdout and stderr information (when loggingEnabled is true.)</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="09dd2-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="09dd2-152">Next Steps</span></span>
<span data-ttu-id="09dd2-153">En este artículo se habrá aprendido cómo tooenable y acceso a información de diagnóstico de Azure.</span><span class="sxs-lookup"><span data-stu-id="09dd2-153">In this article you learned how tooenable and access diagnostics information for Azure.</span></span> <span data-ttu-id="09dd2-154">Aunque esta información es útil en problemas de descripción que se producen con la aplicación, puede señalar tooa problema con un módulo que está utilizando o esa versión de Hola de Node.js utilizado por las aplicaciones de servicio Web de aplicación es diferente de hello uno usado en la implementación entorno.</span><span class="sxs-lookup"><span data-stu-id="09dd2-154">While this information is useful in understanding problems that occur with your application, it may point tooa problem with a module you are using or that hello version of Node.js used by App Service Web Apps is different than hello one used in your deployment environment.</span></span>

<span data-ttu-id="09dd2-155">Para obtener información sobre el trabajo con módulos en Azure, consulte [Uso de módulos Node.js con aplicaciones de Azure](../nodejs-use-node-modules-azure-apps.md).</span><span class="sxs-lookup"><span data-stu-id="09dd2-155">For information in working with modules on Azure, see [Using Node.js Modules with Azure Applications](../nodejs-use-node-modules-azure-apps.md).</span></span>

<span data-ttu-id="09dd2-156">Para obtener información sobre la especificación de una versión de Node.js para su aplicación, consulte [Especificación de una versión de Node.js en una aplicación de Azure].</span><span class="sxs-lookup"><span data-stu-id="09dd2-156">For information on specifying a Node.js version for your application, see [Specifying a Node.js version in an Azure application].</span></span>

<span data-ttu-id="09dd2-157">Para obtener más información, vea también hello [Centro para desarrolladores de Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="09dd2-157">For more information, see also hello [Node.js Developer Center](/develop/nodejs/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="09dd2-158">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="09dd2-158">What's changed</span></span>
* <span data-ttu-id="09dd2-159">Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="09dd2-159">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="09dd2-160">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="09dd2-160">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="09dd2-161">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="09dd2-161">No credit cards required; no commitments.</span></span>
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme
[How tooUse hello Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[Especificación de una versión de Node.js en una aplicación de Azure]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

