---
title: "Cómo depurar una aplicación web de Node.js en el Servicio de aplicaciones de Azure"
description: "Aprenda a depurar una aplicación web de Node.js en el Servicio de aplicaciones de Azure."
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
ms.openlocfilehash: 5e302a4c58a171d40e43a22c34c724e868019ec8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-debug-a-nodejs-web-app-in-azure-app-service"></a><span data-ttu-id="d43c2-103">Cómo depurar una aplicación web de Node.js en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="d43c2-103">How to debug a Node.js web app in Azure App Service</span></span>
<span data-ttu-id="d43c2-104">Azure proporciona diagnósticos integrados para ayudar a depurar aplicaciones Node.js hospedadas en aplicaciones web del [Servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) .</span><span class="sxs-lookup"><span data-stu-id="d43c2-104">Azure provides built-in diagnostics to assist with debugging Node.js applications hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="d43c2-105">En este artículo aprenderá a habilitar el registro de stdout y stderr, mostrar información de error en el explorador y a descargar y ver los archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="d43c2-105">In this article, you will learn how to enable logging of stdout and stderr, display error information in the browser, and how to download and view log files.</span></span>

<span data-ttu-id="d43c2-106">El diagnóstico de las aplicaciones Node.js hospedadas en Azure lo proporciona [IISNode].</span><span class="sxs-lookup"><span data-stu-id="d43c2-106">Diagnostics for Node.js applications hosted on Azure is provided by [IISNode].</span></span> <span data-ttu-id="d43c2-107">Si bien este artículo analiza la configuración más común para recopilar información de diagnóstico, no proporciona una referencia completa para trabajar con IISNode.</span><span class="sxs-lookup"><span data-stu-id="d43c2-107">While this article discusses the most common settings for gathering diagnostics information, it does not provide a complete reference for working with IISNode.</span></span> <span data-ttu-id="d43c2-108">Para obtener más información sobre el trabajo con IISNode, consulte el archivo [léame de IISNode] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="d43c2-108">For more information on working with IISNode, see the [IISNode Readme] on GitHub.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="d43c2-109">Habilitación del registro</span><span class="sxs-lookup"><span data-stu-id="d43c2-109">Enable logging</span></span>
<span data-ttu-id="d43c2-110">De manera predeterminada, una aplicación web del Servicio de aplicaciones solo captura información de diagnóstico sobre las implementaciones, como cuando se realiza la implementación de un sitio web con Git.</span><span class="sxs-lookup"><span data-stu-id="d43c2-110">By default, an App Service web app only captures diagnostic information about deployments, such as when you deploy a web app using Git.</span></span> <span data-ttu-id="d43c2-111">Esta información es útil si está teniendo problemas durante la implementación, como un error al instalar un módulo al que se hace referencia en **package.json**o si va a usar un script de implementación personalizado.</span><span class="sxs-lookup"><span data-stu-id="d43c2-111">This information is useful if you are having problems during deployment, such as a failure when installing a module referenced in **package.json**, or if you are using a custom deployment script.</span></span>

<span data-ttu-id="d43c2-112">Para habilitar el registro de las secuencias stdout y stderr, debe crear un archivo **IISNode.yml** en la raíz de su aplicación Node.js y agregar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d43c2-112">To enable the logging of stdout and stderr streams, you must create an **IISNode.yml** file at the root of your Node.js application and add the following:</span></span>

    loggingEnabled: true

<span data-ttu-id="d43c2-113">Esto permite el registro de stderr y stdout desde su aplicación Node.js.</span><span class="sxs-lookup"><span data-stu-id="d43c2-113">This enables the logging of stderr and stdout from your Node.js application.</span></span>

<span data-ttu-id="d43c2-114">El archivo **IISNode.yml** puede usarse también para controlar si los errores descriptivos o del desarrollador se devuelven al explorador cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="d43c2-114">The **IISNode.yml** file can also be used to control whether friendly errors or developer errors are returned to the browser when a failure occurs.</span></span> <span data-ttu-id="d43c2-115">Para habilitar los errores del desarrollador, agregue la siguiente línea al archivo **IISNode.yml** :</span><span class="sxs-lookup"><span data-stu-id="d43c2-115">To enable developer errors, add the following line to the **IISNode.yml** file:</span></span>

    devErrorsEnabled: true

<span data-ttu-id="d43c2-116">Después de que se habilita esta opción, IISNode devolverá los últimos 64 K de información que se enviaron a stderr en vez de un error descriptivo como "se produjo un error de servidor interno".</span><span class="sxs-lookup"><span data-stu-id="d43c2-116">Once this option is enabled, IISNode will return the last 64K of information sent to stderr instead of a friendly error such as "an internal server error occurred".</span></span>

> [!NOTE]
> <span data-ttu-id="d43c2-117">Si bien devErrorsEnabled es útil para diagnosticar los problemas que se producen durante el desarrollo, su habilitación en un entorno de producción puede tener como resultado que se envíen errores de desarrollo a los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="d43c2-117">While devErrorsEnabled is useful when diagnosing problems during development, enabling it in a production environment may result in development errors being sent to end users.</span></span>
> 
> 

<span data-ttu-id="d43c2-118">Si el archivo **IISNode.yml** no existía ya en su aplicación, debe reiniciar la aplicación web después de publicar la aplicación actualizada.</span><span class="sxs-lookup"><span data-stu-id="d43c2-118">If the **IISNode.yml** file did not already exist within your application, you must restart your web app after publishing the updated application.</span></span> <span data-ttu-id="d43c2-119">Si solamente va a cambiar la configuración de un archivo **IISNode.yml** existente que ya se publicó anteriormente, no es necesario reiniciar.</span><span class="sxs-lookup"><span data-stu-id="d43c2-119">If you are simply changing settings in an existing **IISNode.yml** file that has previously been published, no restart is required.</span></span>

> [!NOTE]
> <span data-ttu-id="d43c2-120">Si aplicación web se creó usando las herramientas de línea de comandos de Azure o los cmdlets de Azure PowerShell, automáticamente se crea un archivo predeterminado **IISNode.yml** .</span><span class="sxs-lookup"><span data-stu-id="d43c2-120">If your web app was created using the Azure Command-Line Tools or Azure PowerShell Cmdlets, a default **IISNode.yml** file is automatically created.</span></span>
> 
> 

<span data-ttu-id="d43c2-121">Para reiniciar la aplicación web, selecciónela en el [Portal de Azure](https://portal.azure.com)y después haga clic en el botón **REINICIAR** :</span><span class="sxs-lookup"><span data-stu-id="d43c2-121">To restart the web app, select the web app in the [Azure Portal](https://portal.azure.com), and then click **RESTART** button:</span></span>

![Botón de reinicio][restart-button]

<span data-ttu-id="d43c2-123">Si las herramientas de línea de comandos de Azure están instaladas en su entorno de desarrollo, puede usar el siguiente comando para reiniciar la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="d43c2-123">If the Azure Command-Line Tools are installed in your development environment, you can use the following command to restart the web app:</span></span>

    azure site restart [sitename]

> [!NOTE]
> <span data-ttu-id="d43c2-124">Si bien loggingEnabled y devErrorsEnabled son las opciones de configuración de IISNode.yml de uso más común para capturar información de diagnóstico, se puede usar IISNode.yml para configurar diversas opciones para su entorno de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="d43c2-124">While loggingEnabled and devErrorsEnabled are the most commonly used IISNode.yml configuration options for capturing diagnostic information, IISNode.yml can be used to configure a variety of options for your hosting environment.</span></span> <span data-ttu-id="d43c2-125">Para una lista completa de las opciones de configuración, consulte el archivo [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml).</span><span class="sxs-lookup"><span data-stu-id="d43c2-125">For a full list of the configuration options, see the [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.</span></span>
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a><span data-ttu-id="d43c2-126">Acceso a los registros</span><span class="sxs-lookup"><span data-stu-id="d43c2-126">Accessing logs</span></span>
<span data-ttu-id="d43c2-127">Se puede tener acceso a los registros de diagnósticos de tres formas; mediante el protocolo de transferencia de archivos (FTP), la descarga de un archivo Zip o como una secuencia en directo actualizada del registro (lo que se conoce también como cola).</span><span class="sxs-lookup"><span data-stu-id="d43c2-127">Diagnostic logs can be accessed in three ways; Using the File Transfer Protocol (FTP), downloading a Zip archive, or as a live updated stream of the log (also known as a tail).</span></span> <span data-ttu-id="d43c2-128">La descarga del archivo Zip de los archivos de registro o la visualización de la secuencia en directo requieren las herramientas de línea de comandos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d43c2-128">Downloading the Zip archive of the log files or viewing the live stream require the Azure Command-Line Tools.</span></span> <span data-ttu-id="d43c2-129">Estas se pueden instalar usando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="d43c2-129">These can be installed by using the following command:</span></span>

    npm install azure-cli -g

<span data-ttu-id="d43c2-130">Una vez instaladas, se puede tener acceso a ellas mediante el comando 'azure'.</span><span class="sxs-lookup"><span data-stu-id="d43c2-130">Once installed, the tools can be accessed using the 'azure' command.</span></span> <span data-ttu-id="d43c2-131">Primero se deben configurar las herramientas de línea de comandos para usar su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d43c2-131">The command-line tools must first be configured to use your Azure subscription.</span></span> <span data-ttu-id="d43c2-132">Para obtener información sobre cómo llevar a cabo esta tarea, consulte la sección **Descarga e importación de la configuración de publicación** del artículo [Uso de las herramientas de línea de comandos de Azure](../xplat-cli-connect.md) .</span><span class="sxs-lookup"><span data-stu-id="d43c2-132">For information on how to accomplish this task, see the **How to download and import publish settings** section of the [How to Use The Azure Command-Line Tools](../xplat-cli-connect.md) article.</span></span>

### <a name="ftp"></a><span data-ttu-id="d43c2-133">FTP</span><span class="sxs-lookup"><span data-stu-id="d43c2-133">FTP</span></span>
<span data-ttu-id="d43c2-134">Para tener acceso a la información de diagnóstico a través de FTP, visite el [Portal de Azure](https://portal.azure.com), seleccione su aplicación web y luego seleccione el **PANEL**.</span><span class="sxs-lookup"><span data-stu-id="d43c2-134">To access the diagnostic information through FTP, visit the [Azure Portal](https://portal.azure.com), select your web app, and then select the **DASHBOARD**.</span></span> <span data-ttu-id="d43c2-135">En la sección de **vínculos rápidos**, los vínculos **FTP DIAGNOSTIC LOGS** y **FTPS DIAGNOSTIC LOGS** proporcionan acceso a los registros usando el protocolo FTP.</span><span class="sxs-lookup"><span data-stu-id="d43c2-135">In the **quick links** section, the **FTP DIAGNOSTIC LOGS** and **FTPS DIAGNOSTIC LOGS** links provide access to the logs using the FTP protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="d43c2-136">Si no ha configurado antes el nombre de usuario y la contraseña de FTP o la implementación, puede hacerlo desde la página de administración **Inicio rápido** al seleccionar **Configurar las credenciales de implementación**.</span><span class="sxs-lookup"><span data-stu-id="d43c2-136">If you have not previously configured user name and password for FTP or deployment, you can do so from the **Quickstart** management page by selecting **Set up deployment credentials**.</span></span>
> 
> 

<span data-ttu-id="d43c2-137">La URL de FTP devuelta en el panel es para el directorio **LogFiles** , que contendrá los siguientes subdirectorios:</span><span class="sxs-lookup"><span data-stu-id="d43c2-137">The FTP URL returned in the dashboard is for the **LogFiles** directory, which will contain the following sub-directories:</span></span>

* <span data-ttu-id="d43c2-138">[Deployment Method](web-sites-deploy.md) : si usa un método de implementación como Git, se creará un directorio del mismo nombre que contendrá información relacionada con las implementaciones.</span><span class="sxs-lookup"><span data-stu-id="d43c2-138">[Deployment Method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of the same name will be created and will contain information related to deployments.</span></span>
* <span data-ttu-id="d43c2-139">nodejs: La información de Stdout y stderr capturada desde todas las instancias de su aplicación (cuando loggingEnabled es verdadero).</span><span class="sxs-lookup"><span data-stu-id="d43c2-139">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="zip-archive"></a><span data-ttu-id="d43c2-140">Archivo Zip</span><span class="sxs-lookup"><span data-stu-id="d43c2-140">Zip archive</span></span>
<span data-ttu-id="d43c2-141">Para descargar un archivo Zip de los registros de diagnóstico, use el siguiente comando de las herramientas de línea de comandos de Azure:</span><span class="sxs-lookup"><span data-stu-id="d43c2-141">To download a Zip archive of the diagnostic logs, use the following command from the Azure Command-Line Tools:</span></span>

    azure site log download [sitename]

<span data-ttu-id="d43c2-142">De esta manera se descargará un archivo **diagnostics.zip** en el directorio actual.</span><span class="sxs-lookup"><span data-stu-id="d43c2-142">This will download a **diagnostics.zip** in the current directory.</span></span> <span data-ttu-id="d43c2-143">Este archivo contiene la siguiente estructura de directorios:</span><span class="sxs-lookup"><span data-stu-id="d43c2-143">This archive contains the following directory structure:</span></span>

* <span data-ttu-id="d43c2-144">deployments: Un registro de información sobre las implementaciones de su aplicación</span><span class="sxs-lookup"><span data-stu-id="d43c2-144">deployments - A log of information about deployments of your application</span></span>
* <span data-ttu-id="d43c2-145">LogFiles</span><span class="sxs-lookup"><span data-stu-id="d43c2-145">LogFiles</span></span>
  
  * <span data-ttu-id="d43c2-146">[Deployment Method](web-sites-deploy.md) : si usa un método de implementación como Git, se creará un directorio del mismo nombre que contendrá información relacionada con las implementaciones.</span><span class="sxs-lookup"><span data-stu-id="d43c2-146">[Deployment method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of the same name will be created and will contain information related to deployments.</span></span>
  * <span data-ttu-id="d43c2-147">nodejs: La información de Stdout y stderr capturada desde todas las instancias de su aplicación (cuando loggingEnabled es verdadero).</span><span class="sxs-lookup"><span data-stu-id="d43c2-147">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="live-stream-tail"></a><span data-ttu-id="d43c2-148">Secuencia en directo (cola)</span><span class="sxs-lookup"><span data-stu-id="d43c2-148">Live stream (tail)</span></span>
<span data-ttu-id="d43c2-149">Para ver una secuencia en directo de la información de registro de diagnóstico, use el siguiente comando en las herramientas de línea de comandos de Azure:</span><span class="sxs-lookup"><span data-stu-id="d43c2-149">To view a live stream of diagnostic log information, use the following command from the Azure Command-Line Tools:</span></span>

    azure site log tail [sitename]

<span data-ttu-id="d43c2-150">De esta manera se devolverá una secuencia de eventos de registro que se actualizan a medida que se producen en el servidor.</span><span class="sxs-lookup"><span data-stu-id="d43c2-150">This will return a stream of log events that are updated as they occur on the server.</span></span> <span data-ttu-id="d43c2-151">Esta secuencia devolverá información de implementación además de información de stdout y stderr (cuando loggingEnabled es verdadero).</span><span class="sxs-lookup"><span data-stu-id="d43c2-151">This stream will return deployment information as well as stdout and stderr information (when loggingEnabled is true.)</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="d43c2-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d43c2-152">Next Steps</span></span>
<span data-ttu-id="d43c2-153">En este artículo aprendió a habilitar y a tener acceso a información de diagnóstico en Azure.</span><span class="sxs-lookup"><span data-stu-id="d43c2-153">In this article you learned how to enable and access diagnostics information for Azure.</span></span> <span data-ttu-id="d43c2-154">Si bien esta información es útil para comprender los problemas que se producen con su aplicación, puede indicar un problema con un módulo que está usando o que la versión de Node.js que usan las aplicaciones web del Servicio de aplicaciones es diferente a la usada en su entorno de implementación.</span><span class="sxs-lookup"><span data-stu-id="d43c2-154">While this information is useful in understanding problems that occur with your application, it may point to a problem with a module you are using or that the version of Node.js used by App Service Web Apps is different than the one used in your deployment environment.</span></span>

<span data-ttu-id="d43c2-155">Para obtener información sobre el trabajo con módulos en Azure, consulte [Uso de módulos Node.js con aplicaciones de Azure](../nodejs-use-node-modules-azure-apps.md).</span><span class="sxs-lookup"><span data-stu-id="d43c2-155">For information in working with modules on Azure, see [Using Node.js Modules with Azure Applications](../nodejs-use-node-modules-azure-apps.md).</span></span>

<span data-ttu-id="d43c2-156">Para obtener información sobre la especificación de una versión de Node.js para su aplicación, consulte [Especificación de una versión de Node.js en una aplicación de Azure].</span><span class="sxs-lookup"><span data-stu-id="d43c2-156">For information on specifying a Node.js version for your application, see [Specifying a Node.js version in an Azure application].</span></span>

<span data-ttu-id="d43c2-157">Para obtener más información, consulte también el [Centro para desarrolladores de Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="d43c2-157">For more information, see also the [Node.js Developer Center](/develop/nodejs/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="d43c2-158">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="d43c2-158">What's changed</span></span>
* <span data-ttu-id="d43c2-159">Para obtener una guía del cambio de Sitios web a Servicio de aplicaciones, consulte: [Servicio de aplicaciones de Azure y su impacto en los servicios de Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="d43c2-159">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="d43c2-160">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de inscribirse para abrir una cuenta de Azure, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d43c2-160">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d43c2-161">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="d43c2-161">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="d43c2-162">[IISNode]: https://github.com/tjanczuk/iisnode</span><span class="sxs-lookup"><span data-stu-id="d43c2-162">[IISNode]: https://github.com/tjanczuk/iisnode</span></span>
<span data-ttu-id="d43c2-163">[léame de IISNode]: https://github.com/tjanczuk/iisnode#readme</span><span class="sxs-lookup"><span data-stu-id="d43c2-163">[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme</span></span>
[How to Use The Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
<span data-ttu-id="d43c2-164">[Especificación de una versión de Node.js en una aplicación de Azure]: ../nodejs-specify-node-version-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="d43c2-164">[Specifying a Node.js version in an Azure application]: ../nodejs-specify-node-version-azure-apps.md</span></span>

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

