---
title: "Preguntas más frecuentes sobre tecnologías de código abierto para Azure Web Apps | Microsoft Docs"
description: "Conozca las respuestas a las preguntas más frecuentes sobre las tecnologías de código abierto en la característica Web Apps de Azure App Service."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: d37b53242c0b231d83425a59ecbe50216216a95b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a><span data-ttu-id="0455d-103">Preguntas más frecuentes sobre tecnologías de código abierto para Web Apps en Azure</span><span class="sxs-lookup"><span data-stu-id="0455d-103">Open-source technologies FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="0455d-104">En este artículo se proporcionan las respuestas a las preguntas más frecuentes sobre los problemas relacionados con las tecnologías de código abierto en la [característica Web Apps de Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="0455d-104">This article has answers to frequently asked questions (FAQs) about issues with open-source technologies for the [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a><span data-ttu-id="0455d-105">Mi base de datos ClearDB está inactiva.</span><span class="sxs-lookup"><span data-stu-id="0455d-105">My ClearDB database is down.</span></span> <span data-ttu-id="0455d-106">¿Cómo se resuelve este problema?</span><span class="sxs-lookup"><span data-stu-id="0455d-106">How do I resolve this?</span></span>

<span data-ttu-id="0455d-107">Si tiene algún problema relacionado con la base de datos, póngase en contacto con el [soporte técnico de ClearDB](https://www.cleardb.com/developers/help/support).</span><span class="sxs-lookup"><span data-stu-id="0455d-107">For database-related issues, contact [ClearDB support](https://www.cleardb.com/developers/help/support).</span></span> 

<span data-ttu-id="0455d-108">Para obtener respuestas a preguntas habituales sobre ClearDB, vea las [preguntas más frecuentes sobre ClearDB](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="0455d-108">For answers to common questions about ClearDB, see [ClearDB FAQs](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-isnt-my-cleardb-database-listed-in-the-portal"></a><span data-ttu-id="0455d-109">¿Por qué no aparece mi base de datos ClearDB en el portal?</span><span class="sxs-lookup"><span data-stu-id="0455d-109">Why isn't my ClearDB database listed in the portal?</span></span>

<span data-ttu-id="0455d-110">Si crea una base de datos ClearDB en [Azure Portal](http://portal.azure.com/), la base de datos no aparecerá en el [Portal de Azure clásico](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="0455d-110">If you create a ClearDB database in the [Azure portal](http://portal.azure.com/), the database doesn't appear in the [Azure classic portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="0455d-111">Para solucionarlo, vincule la base de datos manualmente con la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="0455d-111">To work around this, you can manually link your database to the web app.</span></span>

<span data-ttu-id="0455d-112">Del mismo modo, si crea una base de datos ClearDB en el [Portal de Azure clásico](http://manage.windowsazure.com/), la base de datos no aparecerá en [Azure Portal](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0455d-112">Similarly, if you create a ClearDB database in the [Azure classic portal](http://manage.windowsazure.com/),  you won't see your database in the [Azure portal](http://portal.azure.com/).</span></span> <span data-ttu-id="0455d-113">En este caso, no existe ninguna solución alternativa.</span><span class="sxs-lookup"><span data-stu-id="0455d-113">In this case, no workaround is available.</span></span> 

<span data-ttu-id="0455d-114">Para obtener más información, vea [P+F sobre bases de datos MySQL ClearDB con Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="0455d-114">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a><span data-ttu-id="0455d-115">¿Por qué no se ha migrado mi base de datos ClearDB durante la migración de mi suscripción?</span><span class="sxs-lookup"><span data-stu-id="0455d-115">Why wasn't my ClearDB database migrated during my subscription migration?</span></span>

<span data-ttu-id="0455d-116">Al realizar una migración de recursos entre suscripciones, se aplican algunas limitaciones.</span><span class="sxs-lookup"><span data-stu-id="0455d-116">When you perform resource migration across subscriptions, some limitations apply.</span></span> <span data-ttu-id="0455d-117">Una base de datos MySQL ClearDB es un servicio de terceros y no se migra durante la migración de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="0455d-117">A ClearDB MySQL database is a third-party service and is not migrated during an Azure subscription migration.</span></span>

<span data-ttu-id="0455d-118">Si no administra la migración de su base de datos MySQL antes de migrar los recursos de Azure, es posible que la base de datos MySQL ClearDB no esté disponible.</span><span class="sxs-lookup"><span data-stu-id="0455d-118">If you don't manage the migration of your MySQL database before you migrate your Azure resources, your ClearDB MySQL database might be unavailable.</span></span> <span data-ttu-id="0455d-119">Para evitar esto, primero migre manualmente la base de datos ClearDB y, después, migre la suscripción de Azure para su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="0455d-119">To avoid this, first, manually migrate your ClearDB database, and then migrate the Azure subscription for your web app.</span></span>

<span data-ttu-id="0455d-120">Para obtener más información, vea [P+F sobre bases de datos MySQL ClearDB con Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="0455d-120">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="how-do-i-turn-on-php-logging-to-troubleshoot-php-issues"></a><span data-ttu-id="0455d-121">¿Cómo se activa el registro PHP para solucionar problemas de PHP?</span><span class="sxs-lookup"><span data-stu-id="0455d-121">How do I turn on PHP logging to troubleshoot PHP issues?</span></span>

<span data-ttu-id="0455d-122">Para activar el registro de PHP:</span><span class="sxs-lookup"><span data-stu-id="0455d-122">To turn on PHP logging:</span></span>

1. <span data-ttu-id="0455d-123">Inicie sesión en su [sitio web de Kudu](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="0455d-123">Sign in to your [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="0455d-124">En el menú superior, elija **Consola de depuración** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="0455d-124">In the top menu, select **Debug Console** > **CMD**.</span></span>
3. <span data-ttu-id="0455d-125">Seleccione la carpeta **Sitio**.</span><span class="sxs-lookup"><span data-stu-id="0455d-125">Select the **Site** folder.</span></span>
4. <span data-ttu-id="0455d-126">Seleccione la carpeta **wwwroot**.</span><span class="sxs-lookup"><span data-stu-id="0455d-126">Select the **wwwroot** folder.</span></span>
5. <span data-ttu-id="0455d-127">Seleccione el icono **+** y, después, **Nuevo archivo**.</span><span class="sxs-lookup"><span data-stu-id="0455d-127">Select the **+** icon, and then select **New File**.</span></span>
6. <span data-ttu-id="0455d-128">Establezca el nombre del archivo en **.user.ini**.</span><span class="sxs-lookup"><span data-stu-id="0455d-128">Set the file name to **.user.ini**.</span></span>
7. <span data-ttu-id="0455d-129">Seleccione el icono de lápiz situado junto a **.user.ini**.</span><span class="sxs-lookup"><span data-stu-id="0455d-129">Select the pencil icon next to **.user.ini**.</span></span>
8. <span data-ttu-id="0455d-130">En el archivo, agregue este código: `log_errors=on`</span><span class="sxs-lookup"><span data-stu-id="0455d-130">In the file, add this code: `log_errors=on`</span></span>
9. <span data-ttu-id="0455d-131">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0455d-131">Select **Save**.</span></span>
10. <span data-ttu-id="0455d-132">Seleccione el icono de lápiz situado junto a **wp-config.php**.</span><span class="sxs-lookup"><span data-stu-id="0455d-132">Select the pencil icon next to **wp-config.php**.</span></span>
11. <span data-ttu-id="0455d-133">Cambie el texto por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="0455d-133">Change the text to the following code:</span></span>
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging to /wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings to screendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors to screenini_set('display_errors', 0);
   ```
12. <span data-ttu-id="0455d-134">En Azure Portal, en el menú de la aplicación web, reinicie la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0455d-134">In the Azure portal, in the web app menu, restart your web app.</span></span>

<span data-ttu-id="0455d-135">Para obtener más información, vea [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/) (Habilitar los registros de errores de WordPress).</span><span class="sxs-lookup"><span data-stu-id="0455d-135">For more information, see [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a><span data-ttu-id="0455d-136">¿Cómo se pueden registrar errores de aplicaciones de Python en las aplicaciones hospedadas en App Service?</span><span class="sxs-lookup"><span data-stu-id="0455d-136">How do I log Python application errors in apps that are hosted in App Service?</span></span>

<span data-ttu-id="0455d-137">Para capturar errores de aplicaciones Python:</span><span class="sxs-lookup"><span data-stu-id="0455d-137">To capture Python application errors:</span></span>

1. <span data-ttu-id="0455d-138">En Azure Portal, en la aplicación web, seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="0455d-138">In the Azure portal, in your web app, select **Settings**.</span></span>
2. <span data-ttu-id="0455d-139">En la pestaña **Configuración**, seleccione **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="0455d-139">On the **Settings** tab, select **Application settings**.</span></span>
3. <span data-ttu-id="0455d-140">En **Configuración de la aplicación**, escriba el siguiente par clave-valor:</span><span class="sxs-lookup"><span data-stu-id="0455d-140">Under **App settings**, enter the following key/value pair:</span></span>
    * <span data-ttu-id="0455d-141">Clave: WSGI_LOG</span><span class="sxs-lookup"><span data-stu-id="0455d-141">Key : WSGI_LOG</span></span>
    * <span data-ttu-id="0455d-142">Valor: D:\home\site\wwwroot\logs.txt (escriba el nombre de archivo que elija)</span><span class="sxs-lookup"><span data-stu-id="0455d-142">Value : D:\home\site\wwwroot\logs.txt (enter your choice of file name)</span></span>

<span data-ttu-id="0455d-143">Ahora debería ver los errores en el archivo logs.txt en la carpeta wwwroot.</span><span class="sxs-lookup"><span data-stu-id="0455d-143">You should now see errors in the logs.txt file in the wwwroot folder.</span></span>

## <a name="how-do-i-change-the-version-of-the-nodejs-application-that-is-hosted-in-app-service"></a><span data-ttu-id="0455d-144">¿Cómo se cambia la versión de la aplicación Node.js que se hospeda en App Service?</span><span class="sxs-lookup"><span data-stu-id="0455d-144">How do I change the version of the Node.js application that is hosted in App Service?</span></span>

<span data-ttu-id="0455d-145">Para cambiar la versión de la aplicación Node.js, puede usar una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="0455d-145">To change the version of the Node.js application, you can use one of the following options:</span></span>

*   <span data-ttu-id="0455d-146">En Azure Portal, use **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="0455d-146">In the Azure portal, use **App settings**.</span></span>
    1. <span data-ttu-id="0455d-147">En Azure Portal, vaya a la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="0455d-147">In the Azure portal, go to your web app.</span></span>
    2. <span data-ttu-id="0455d-148">En la hoja **Configuración**, seleccione **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="0455d-148">On the **Settings** blade, select **Application settings**.</span></span>
    3. <span data-ttu-id="0455d-149">En **Configuración de la aplicación**, puede incluir WEBSITE_NODE_DEFAULT_VERSION como clave y la versión de Node.js que quiera como valor.</span><span class="sxs-lookup"><span data-stu-id="0455d-149">In **App settings**, you can include WEBSITE_NODE_DEFAULT_VERSION as the key, and the version of Node.js you want as the value.</span></span>
    4. <span data-ttu-id="0455d-150">Vaya a la [consola Kudu](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="0455d-150">Go to your [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
    5. <span data-ttu-id="0455d-151">Para comprobar la versión de Node.js, escriba el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0455d-151">To check the Node.js version, enter the following command:</span></span>  
   ```
   node -v
   ```
*   <span data-ttu-id="0455d-152">Modifique el archivo iisnode.yml.</span><span class="sxs-lookup"><span data-stu-id="0455d-152">Modify the iisnode.yml file.</span></span> <span data-ttu-id="0455d-153">Si cambia la versión de Node.js en el archivo iisnode.yml, solo establecerá el entorno en tiempo de ejecución que usa iisnode.</span><span class="sxs-lookup"><span data-stu-id="0455d-153">Changing the Node.js version in the iisnode.yml file only sets the runtime environment that iisnode uses.</span></span> <span data-ttu-id="0455d-154">El comando de Kudu y otros comandos seguirán usando la versión de Node.js que esté establecida en **Configuración de la aplicación** en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0455d-154">Your Kudu cmd and others still use the Node.js version that is set in **App settings** in the Azure portal.</span></span>

    <span data-ttu-id="0455d-155">Para establecer manualmente iisnode.yml, cree un archivo iisnode.yml en la carpeta raíz de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0455d-155">To set the iisnode.yml manually, create an iisnode.yml file in your app root folder.</span></span> <span data-ttu-id="0455d-156">En el archivo, incluya la línea siguiente:</span><span class="sxs-lookup"><span data-stu-id="0455d-156">In the file, include the following line:</span></span>
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   <span data-ttu-id="0455d-157">Establezca el archivo iisnode.yml mediante package.json durante la implementación de control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="0455d-157">Set the iisnode.yml file by using package.json during source control deployment.</span></span>
    <span data-ttu-id="0455d-158">El proceso de implementación de control de código fuente de Azure sigue estos pasos:</span><span class="sxs-lookup"><span data-stu-id="0455d-158">The Azure source control deployment process involves the following steps:</span></span>
    1. <span data-ttu-id="0455d-159">Mueve el contenido a la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="0455d-159">Moves content to the Azure web app.</span></span>
    2. <span data-ttu-id="0455d-160">Crea un script de implementación predeterminado, si todavía no hay ninguno (archivos deploy.cmd o .deployment) en la carpeta raíz de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="0455d-160">Creates a default deployment script, if there isn’t one (deploy.cmd, .deployment files) in the web app root folder.</span></span>
    3. <span data-ttu-id="0455d-161">Ejecuta un script de implementación en el que crea un archivo iisnode.yml si hace referencia a la versión de Node.js en el archivo package.json > motor `"engines": {"node": "5.9.1","npm": "3.7.3"}`</span><span class="sxs-lookup"><span data-stu-id="0455d-161">Runs a deployment script in which it creates an iisnode.yml file if you mention the Node.js version in the package.json file > engine `"engines": {"node": "5.9.1","npm": "3.7.3"}`</span></span>
    4. <span data-ttu-id="0455d-162">El archivo iisnode.yml tiene la siguiente línea de código:</span><span class="sxs-lookup"><span data-stu-id="0455d-162">The iisnode.yml file has the following line of code:</span></span>
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-the-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a><span data-ttu-id="0455d-163">Veo el mensaje "Error al establecer una conexión de base de datos" en mi aplicación de WordPress que está hospedada en App Service.</span><span class="sxs-lookup"><span data-stu-id="0455d-163">I see the message "Error establishing a database connection" in my WordPress app that's hosted in App Service.</span></span> <span data-ttu-id="0455d-164">¿Cómo se soluciona este problema?</span><span class="sxs-lookup"><span data-stu-id="0455d-164">How do I troubleshoot this?</span></span>

<span data-ttu-id="0455d-165">Si ve este error en la aplicación de WordPress de Azure, para habilitar php_errors.log y debug.log, complete los pasos que se indican en [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/) (Habilitar los registros de errores de WordPress).</span><span class="sxs-lookup"><span data-stu-id="0455d-165">If you see this error in your Azure WordPress app, to enable php_errors.log and debug.log, complete the steps detailed in [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

<span data-ttu-id="0455d-166">Cuando los registros estén habilitados, reproduzca el error y compruebe los registros para ver si se está quedando sin conexiones:</span><span class="sxs-lookup"><span data-stu-id="0455d-166">When the logs are enabled, reproduce the error, and then check the logs to see if you are running out of connections:</span></span>
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded the ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

<span data-ttu-id="0455d-167">Si ve este error en los archivos debug.log o php_errors.log, significa que la aplicación supera el número de conexiones.</span><span class="sxs-lookup"><span data-stu-id="0455d-167">If you see this error in your debug.log or php_errors.log files, your app is exceeding the number of connections.</span></span> <span data-ttu-id="0455d-168">Si está hospedando en ClearDB, compruebe el número de conexiones que están disponibles en su [plan de servicio](https://www.cleardb.com/pricing.view).</span><span class="sxs-lookup"><span data-stu-id="0455d-168">If you’re hosting on ClearDB, verify the number of connections that are available in your [service plan](https://www.cleardb.com/pricing.view).</span></span>

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a><span data-ttu-id="0455d-169">¿Cómo se puede depurar una aplicación Node.js hospedada en App Service?</span><span class="sxs-lookup"><span data-stu-id="0455d-169">How do I debug a Node.js app that's hosted in App Service?</span></span>

1.  <span data-ttu-id="0455d-170">Vaya a la [consola Kudu](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span><span class="sxs-lookup"><span data-stu-id="0455d-170">Go to your [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span></span>
2.  <span data-ttu-id="0455d-171">Vaya a la carpeta de registros de aplicación (D:\home\LogFiles\Application).</span><span class="sxs-lookup"><span data-stu-id="0455d-171">Go to your application logs folder (D:\home\LogFiles\Application).</span></span>
3.  <span data-ttu-id="0455d-172">En el archivo logging_errors.txt, busque el contenido.</span><span class="sxs-lookup"><span data-stu-id="0455d-172">In the logging_errors.txt file, check for content.</span></span>

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a><span data-ttu-id="0455d-173">¿Cómo se instalan módulos nativos de Python en una aplicación web de App Service o una aplicación de API?</span><span class="sxs-lookup"><span data-stu-id="0455d-173">How do I install native Python modules in an App Service web app or API app?</span></span>

<span data-ttu-id="0455d-174">Algunos paquetes podrían no instalarse si se usa pip en Azure.</span><span class="sxs-lookup"><span data-stu-id="0455d-174">Some packages might not install by using pip in Azure.</span></span> <span data-ttu-id="0455d-175">El paquete podría no estar disponible en el índice de paquetes de Python o podría requerirse un compilador (no hay ningún compilador disponible en el equipo que ejecuta la aplicación web en App Service).</span><span class="sxs-lookup"><span data-stu-id="0455d-175">The package might not be available on the Python Package Index, or a compiler might be required (a compiler is not available on the computer that is running the web app in App Service).</span></span> <span data-ttu-id="0455d-176">Para obtener información sobre cómo instalar módulos nativos en aplicaciones web de App Service y aplicaciones de API, vea [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/) (Instalar módulos de Python en App Service).</span><span class="sxs-lookup"><span data-stu-id="0455d-176">For information about installing native modules in App Service web apps and API apps, see [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span></span>

## <a name="how-do-i-deploy-a-django-app-to-app-service-by-using-git-and-the-new-version-of-python"></a><span data-ttu-id="0455d-177">¿Cómo se implementa una aplicación de Django en App Service mediante GIT y la nueva versión de Python?</span><span class="sxs-lookup"><span data-stu-id="0455d-177">How do I deploy a Django app to App Service by using Git and the new version of Python?</span></span>

<span data-ttu-id="0455d-178">Para obtener información sobre cómo instalar Django, vea [Deploying a Django app to App Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/) (Implementar una aplicación de Django en App Service).</span><span class="sxs-lookup"><span data-stu-id="0455d-178">For information about installing Django, see [Deploying a Django app to App Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span></span>

## <a name="where-are-the-tomcat-log-files-located"></a><span data-ttu-id="0455d-179">¿Dónde se encuentran los archivos de registro de Tomcat?</span><span class="sxs-lookup"><span data-stu-id="0455d-179">Where are the Tomcat log files located?</span></span>

<span data-ttu-id="0455d-180">En Azure Marketplace e implementaciones personalizadas:</span><span class="sxs-lookup"><span data-stu-id="0455d-180">For Azure Marketplace and custom deployments:</span></span>

* <span data-ttu-id="0455d-181">Ubicación de la carpeta: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span><span class="sxs-lookup"><span data-stu-id="0455d-181">Folder location: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span></span>
* <span data-ttu-id="0455d-182">Archivos de interés:</span><span class="sxs-lookup"><span data-stu-id="0455d-182">Files of interest:</span></span>
    * <span data-ttu-id="0455d-183">catalina.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="0455d-183">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="0455d-184">host-manager.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="0455d-184">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="0455d-185">localhost.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="0455d-185">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="0455d-186">manager.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="0455d-186">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="0455d-187">site_access_log.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="0455d-187">site_access_log.*yyyy-mm-dd*.log</span></span>


<span data-ttu-id="0455d-188">Para implementaciones de **configuración de la aplicación** en el portal:</span><span class="sxs-lookup"><span data-stu-id="0455d-188">For portal **App settings** deployments:</span></span>

* <span data-ttu-id="0455d-189">Ubicación de la carpeta: D:\home\LogFiles</span><span class="sxs-lookup"><span data-stu-id="0455d-189">Folder location: D:\home\LogFiles</span></span>
* <span data-ttu-id="0455d-190">Archivos de interés:</span><span class="sxs-lookup"><span data-stu-id="0455d-190">Files of interest:</span></span>
    * <span data-ttu-id="0455d-191">catalina.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="0455d-191">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="0455d-192">host-manager.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="0455d-192">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="0455d-193">localhost.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="0455d-193">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="0455d-194">manager.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="0455d-194">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="0455d-195">site_access_log.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="0455d-195">site_access_log.*yyyy-mm-dd*.log</span></span>

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a><span data-ttu-id="0455d-196">¿Cómo se solucionan los errores de conexión de JDBC Driver?</span><span class="sxs-lookup"><span data-stu-id="0455d-196">How do I troubleshoot JDBC driver connection errors?</span></span>

<span data-ttu-id="0455d-197">Es posible que vea el mensaje siguiente en los registros de Tomcat:</span><span class="sxs-lookup"><span data-stu-id="0455d-197">You might see the following message in your Tomcat logs:</span></span>

```
The web application[ROOT] registered the JDBC driver [com.mysql.jdbc.Driver] but failed to unregister it when the web application was stopped. To prevent a memory leak,the JDBC Driver has been forcibly unregistered
```

<span data-ttu-id="0455d-198">Para resolver el error:</span><span class="sxs-lookup"><span data-stu-id="0455d-198">To resolve the error:</span></span>

1. <span data-ttu-id="0455d-199">Quite el archivo sqljdbc*.jar de la carpeta de app/lib.</span><span class="sxs-lookup"><span data-stu-id="0455d-199">Remove the sqljdbc*.jar file from your app/lib folder.</span></span>
2. <span data-ttu-id="0455d-200">Si está usando el servidor web de Tomcat personalizado o el servidor web de Tomcat de Azure Marketplace, copie este archivo .jar en la carpeta lib de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="0455d-200">If you are using the custom Tomcat or Azure Marketplace Tomcat web server, copy this .jar file to the Tomcat lib folder.</span></span>
3. <span data-ttu-id="0455d-201">Si va a habilitar Java desde Azure Portal (seleccione **Java 1.8** > **Servidor de Tomcat**), copie el archivo sqljdbc.*jar en la carpeta que sea paralela a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0455d-201">If you are enabling Java from the Azure portal (select **Java 1.8** > **Tomcat server**), copy the sqljdbc.* jar file in the folder that's parallel to your app.</span></span> <span data-ttu-id="0455d-202">Después, agregue la siguiente configuración de Classpath en el archivo web.config:</span><span class="sxs-lookup"><span data-stu-id="0455d-202">Then, add the following classpath setting to the web.config file:</span></span>

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path to the sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-to-copy-live-log-files"></a><span data-ttu-id="0455d-203">¿Por qué veo errores al intentar copiar archivos de registro activos?</span><span class="sxs-lookup"><span data-stu-id="0455d-203">Why do I see errors when I attempt to copy live log files?</span></span>

<span data-ttu-id="0455d-204">Si intenta copiar archivos de registro activos para una aplicación de Java (por ejemplo, Tomcat), verá este error de FTP:</span><span class="sxs-lookup"><span data-stu-id="0455d-204">If you try to copy live log files for a Java app (for example, Tomcat), you might see this FTP error:</span></span>

```
Error transferring file [filename] Copying files from remote side failed.
    
The process cannot access the file because it is being used by another process.
```

<span data-ttu-id="0455d-205">El mensaje de error podría variar, en función del cliente FTP.</span><span class="sxs-lookup"><span data-stu-id="0455d-205">The error message might vary, depending on the FTP client.</span></span>

<span data-ttu-id="0455d-206">Todas las aplicaciones de Java tienen este problema de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="0455d-206">All Java apps have this locking issue.</span></span> <span data-ttu-id="0455d-207">Kudu solo permite descargar este archivo mientras se ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0455d-207">Only Kudu supports downloading this file while the app is running.</span></span>

<span data-ttu-id="0455d-208">Si detiene la aplicación, permite el acceso FTP a estos archivos.</span><span class="sxs-lookup"><span data-stu-id="0455d-208">Stopping the app allows FTP access to these files.</span></span>

<span data-ttu-id="0455d-209">Otra solución alternativa consiste en escribir un trabajo web que se ejecute según una programación y que copie estos archivos en un directorio diferente.</span><span class="sxs-lookup"><span data-stu-id="0455d-209">Another workaround is to write a WebJob that runs on a schedule and copies these files to a different directory.</span></span> <span data-ttu-id="0455d-210">Para obtener un proyecto de ejemplo, vea el proyecto [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob).</span><span class="sxs-lookup"><span data-stu-id="0455d-210">For a sample project, see the [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) project.</span></span>

## <a name="where-do-i-find-the-log-files-for-jetty"></a><span data-ttu-id="0455d-211">¿Dónde se encuentran los archivos de registro de Jetty?</span><span class="sxs-lookup"><span data-stu-id="0455d-211">Where do I find the log files for Jetty?</span></span>

<span data-ttu-id="0455d-212">En el caso de Marketplace e implementaciones personalizadas, el archivo de registro está en la carpeta D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs.</span><span class="sxs-lookup"><span data-stu-id="0455d-212">For Marketplace and custom deployments, the log file is in the D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs folder.</span></span> <span data-ttu-id="0455d-213">Tenga en cuenta que la ubicación de la carpeta depende de la versión de Jetty que use.</span><span class="sxs-lookup"><span data-stu-id="0455d-213">Note that the folder location depends on the version of Jetty you are using.</span></span> <span data-ttu-id="0455d-214">Por ejemplo, la ruta de acceso que se proporciona aquí es para Jetty 9.1.2.</span><span class="sxs-lookup"><span data-stu-id="0455d-214">For example, the path provided here is for Jetty 9.1.2.</span></span> <span data-ttu-id="0455d-215">Busque jetty_*AAAA_MM_DD*.stderrout.log.</span><span class="sxs-lookup"><span data-stu-id="0455d-215">Look for jetty_*YYYY_MM_DD*.stderrout.log.</span></span>

<span data-ttu-id="0455d-216">En el caso de implementaciones de configuración de la aplicación en el portal, el archivo de registro está en D:\home\LogFiles.</span><span class="sxs-lookup"><span data-stu-id="0455d-216">For portal App Setting deployments, the log file is in D:\home\LogFiles.</span></span> <span data-ttu-id="0455d-217">Busque jetty_*AAAA_MM_DD*.stderrout.log.</span><span class="sxs-lookup"><span data-stu-id="0455d-217">Look for jetty_*YYYY_MM_DD*.stderrout.log</span></span>

## <a name="can-i-send-email-from-my-azure-web-app"></a><span data-ttu-id="0455d-218">¿Puedo enviar correo electrónico desde la aplicación web de Azure?</span><span class="sxs-lookup"><span data-stu-id="0455d-218">Can I send email from my Azure web app?</span></span>

<span data-ttu-id="0455d-219">App Service no tiene una característica integrada de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="0455d-219">App Service doesn't have a built-in email feature.</span></span> <span data-ttu-id="0455d-220">Para conocer algunas alternativas adecuadas para enviar correo electrónico desde la aplicación, vea este [debate de Stack Overflow](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span><span class="sxs-lookup"><span data-stu-id="0455d-220">For some good alternatives for sending email from your app, see this [Stack Overflow discussion](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span></span>

## <a name="why-does-my-wordpress-site-redirect-to-another-url"></a><span data-ttu-id="0455d-221">¿Por qué mi sitio de WordPress redirige a otra dirección URL?</span><span class="sxs-lookup"><span data-stu-id="0455d-221">Why does my WordPress site redirect to another URL?</span></span>

<span data-ttu-id="0455d-222">Si ha migrado recientemente a Azure, WordPress podría redirigir a la URL de dominio anterior.</span><span class="sxs-lookup"><span data-stu-id="0455d-222">If you have recently migrated to Azure, WordPress might redirect to the old domain URL.</span></span> <span data-ttu-id="0455d-223">Esto se debe a una opción de configuración de la base de datos MySQL.</span><span class="sxs-lookup"><span data-stu-id="0455d-223">This is caused by a setting in the MySQL database.</span></span>

<span data-ttu-id="0455d-224">WordPress Buddy+ es una extensión de sitio de Azure que se puede usar para actualizar la dirección URL de redireccionamiento directamente en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="0455d-224">WordPress Buddy+ is an Azure Site Extension that you can use to update the redirection URL directly in the database.</span></span> <span data-ttu-id="0455d-225">Para obtener más información sobre el uso de WordPress Buddy+, vea [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (Herramientas de WordPress y migración de MySQL con WordPress Buddy+).</span><span class="sxs-lookup"><span data-stu-id="0455d-225">For more information about using WordPress Buddy+, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

<span data-ttu-id="0455d-226">Como alternativa, si prefiere actualizar manualmente la URL de redireccionamiento mediante el uso de consultas SQL o PHPMyAdmin, vea [WordPress: Redirecting to wrong URL](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/) (WordPress: redireccionamiento a una URL incorrecta).</span><span class="sxs-lookup"><span data-stu-id="0455d-226">Alternatively, if you prefer to manually update the redirection URL by using SQL queries or PHPMyAdmin, see [WordPress: Redirecting to wrong URL](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span></span>

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a><span data-ttu-id="0455d-227">¿Cómo se cambia la contraseña de inicio de sesión de WordPress?</span><span class="sxs-lookup"><span data-stu-id="0455d-227">How do I change my WordPress sign-in password?</span></span>

<span data-ttu-id="0455d-228">Si ha olvidado su contraseña de inicio de sesión de WordPress, puede usar WordPress Buddy+ para actualizarla.</span><span class="sxs-lookup"><span data-stu-id="0455d-228">If you have forgotten your WordPress sign-in password, you can use WordPress Buddy+ to update it.</span></span> <span data-ttu-id="0455d-229">Para restablecer la contraseña, instale la extensión de sitio de Azure WordPress Buddy+ y, después, lleve a cabo los pasos que se describen en [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (Herramientas de WordPress y migración de MySQL con WordPress Buddy+).</span><span class="sxs-lookup"><span data-stu-id="0455d-229">To reset your password, install the WordPress Buddy+ Azure Site Extension, and then complete the steps described in [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="i-cant-sign-in-to-wordpress-how-do-i-resolve-this"></a><span data-ttu-id="0455d-230">No puedo iniciar sesión en WordPress.</span><span class="sxs-lookup"><span data-stu-id="0455d-230">I can't sign in to WordPress.</span></span> <span data-ttu-id="0455d-231">¿Cómo se resuelve este problema?</span><span class="sxs-lookup"><span data-stu-id="0455d-231">How do I resolve this?</span></span>

<span data-ttu-id="0455d-232">Si está bloqueado y no puede entrar en WordPress después de instalar recientemente un complemento, dicho complemento podría ser defectuoso.</span><span class="sxs-lookup"><span data-stu-id="0455d-232">If you find yourself locked out of WordPress after recently installing a plugin, you might have a faulty plugin.</span></span> <span data-ttu-id="0455d-233">WordPress Buddy+ es una extensión de sitio de Azure que permite deshabilitar complementos en WordPress.</span><span class="sxs-lookup"><span data-stu-id="0455d-233">WordPress Buddy+ is an Azure Site Extension that can help you disable plugins in WordPress.</span></span> <span data-ttu-id="0455d-234">Para obtener más información, vea [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (Herramientas de WordPress y migración de MySQL con WordPress Buddy+).</span><span class="sxs-lookup"><span data-stu-id="0455d-234">For more information, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="how-do-i-migrate-my-wordpress-database"></a><span data-ttu-id="0455d-235">¿Cómo puedo migrar mi base de datos de WordPress?</span><span class="sxs-lookup"><span data-stu-id="0455d-235">How do I migrate my WordPress database?</span></span>

<span data-ttu-id="0455d-236">Tiene varias opciones para migrar la base de datos MySQL conectada a su sitio web de WordPress:</span><span class="sxs-lookup"><span data-stu-id="0455d-236">You have multiple options for migrating the MySQL database that's connected to your WordPress website:</span></span>

* <span data-ttu-id="0455d-237">Los desarrolladores deben usar el [símbolo del sistema o PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/).</span><span class="sxs-lookup"><span data-stu-id="0455d-237">Developers: Use the [command prompt or PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span></span>
* <span data-ttu-id="0455d-238">Los usuarios que no son desarrolladores deben usar [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="0455d-238">Non-developers: Use [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span></span>

## <a name="how-do-i-help-make-wordpress-more-secure"></a><span data-ttu-id="0455d-239">¿Cómo puedo conseguir que WordPress sea más seguro?</span><span class="sxs-lookup"><span data-stu-id="0455d-239">How do I help make WordPress more secure?</span></span>

<span data-ttu-id="0455d-240">Para obtener información sobre los procedimientos de seguridad recomendados para WordPress, vea [Best practices for WordPress security in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/) (Procedimientos recomendados para la seguridad de WordPress en Azure).</span><span class="sxs-lookup"><span data-stu-id="0455d-240">To learn about security best practices for WordPress, see [Best practices for WordPress security in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span></span>

## <a name="i-am-trying-to-use-phpmyadmin-and-i-see-the-message-access-denied-how-do-i-resolve-this"></a><span data-ttu-id="0455d-241">Estoy intentando usar PHPMyAdmin y aparece el mensaje "Acceso denegado".</span><span class="sxs-lookup"><span data-stu-id="0455d-241">I am trying to use PHPMyAdmin, and I see the message “Access denied.”</span></span> <span data-ttu-id="0455d-242">¿Cómo se resuelve este problema?</span><span class="sxs-lookup"><span data-stu-id="0455d-242">How do I resolve this?</span></span>

<span data-ttu-id="0455d-243">Puede experimentar este problema si la característica de MySQL en aplicación todavía no se está ejecutando en esta instancia de App Service.</span><span class="sxs-lookup"><span data-stu-id="0455d-243">You might experience this issue if the MySQL in-app feature isn't running yet in this App Service instance.</span></span> <span data-ttu-id="0455d-244">Para resolver el problema, intente obtener acceso a su sitio web.</span><span class="sxs-lookup"><span data-stu-id="0455d-244">To resolve the issue, try to access your website.</span></span> <span data-ttu-id="0455d-245">De este modo se inician los procesos necesarios, incluido el proceso de MySQL en aplicación.</span><span class="sxs-lookup"><span data-stu-id="0455d-245">This starts the required processes, including the MySQL in-app process.</span></span> <span data-ttu-id="0455d-246">Para comprobar que MySQL en la aplicación se está ejecutando, asegúrese de que mysqld.exe aparece en los procesos que se muestran en el Explorador de procesos.</span><span class="sxs-lookup"><span data-stu-id="0455d-246">To verify that MySQL in-app is running, in Process Explorer, ensure that mysqld.exe is listed in the processes.</span></span>

<span data-ttu-id="0455d-247">Después de asegurarse de que MySQL en la aplicación se está ejecutando, pruebe a usar PHPMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="0455d-247">After you ensure that MySQL in-app is running, try to use PHPMyAdmin.</span></span>

## <a name="i-get-an-http-403-error-when-i-try-to-import-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a><span data-ttu-id="0455d-248">Obtengo un error HTTP 403 cuando intento importar o exportar mi base de datos de MySQL en la aplicación mediante el uso de PHPMyadmin.</span><span class="sxs-lookup"><span data-stu-id="0455d-248">I get an HTTP 403 error when I try to import or export my MySQL in-app database by using PHPMyadmin.</span></span> <span data-ttu-id="0455d-249">¿Cómo se resuelve este problema?</span><span class="sxs-lookup"><span data-stu-id="0455d-249">How do I resolve this?</span></span>

<span data-ttu-id="0455d-250">Si usa una versión antigua de Chrome, podría tratarse de un problema conocido.</span><span class="sxs-lookup"><span data-stu-id="0455d-250">If you are using an older version of Chrome, you might be experiencing a known bug.</span></span> <span data-ttu-id="0455d-251">Para resolver el problema, actualice a una versión más reciente de Chrome.</span><span class="sxs-lookup"><span data-stu-id="0455d-251">To resolve the issue, upgrade to a newer version of Chrome.</span></span> <span data-ttu-id="0455d-252">También puede intentar usar un explorador diferente, como Internet Explorer o Edge, en los que el problema no se produce.</span><span class="sxs-lookup"><span data-stu-id="0455d-252">Also try using a different browser, like Internet Explorer or Edge, where the issue does not occur.</span></span>
