---
title: "aplicaciones web de tecnologías de origen aaaOpen preguntas más frecuentes de Azure | Documentos de Microsoft"
description: "Obtener toofrequently respuestas preguntas más frecuentes acerca de las tecnologías de código abierto en función de las aplicaciones Web de Hola de servicio de aplicaciones de Azure."
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
ms.openlocfilehash: 35cff4f322859d25972747cf55aa7c4316381a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a><span data-ttu-id="0bfa7-103">Preguntas más frecuentes sobre tecnologías de código abierto para Web Apps en Azure</span><span class="sxs-lookup"><span data-stu-id="0bfa7-103">Open-source technologies FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="0bfa7-104">Este artículo tiene toofrequently respuestas preguntas frecuentes (P+f) sobre los problemas con las tecnologías de código abierto para hello [característica de las aplicaciones Web de servicio de aplicaciones de Azure](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-104">This article has answers toofrequently asked questions (FAQs) about issues with open-source technologies for hello [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a><span data-ttu-id="0bfa7-105">Mi base de datos ClearDB está inactiva.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-105">My ClearDB database is down.</span></span> <span data-ttu-id="0bfa7-106">¿Cómo se resuelve este problema?</span><span class="sxs-lookup"><span data-stu-id="0bfa7-106">How do I resolve this?</span></span>

<span data-ttu-id="0bfa7-107">Si tiene algún problema relacionado con la base de datos, póngase en contacto con el [soporte técnico de ClearDB](https://www.cleardb.com/developers/help/support).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-107">For database-related issues, contact [ClearDB support](https://www.cleardb.com/developers/help/support).</span></span> 

<span data-ttu-id="0bfa7-108">Para respuestas toocommon preguntas sobre ClearDB, consulte [ClearDB preguntas más frecuentes sobre](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-108">For answers toocommon questions about ClearDB, see [ClearDB FAQs](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-isnt-my-cleardb-database-listed-in-hello-portal"></a><span data-ttu-id="0bfa7-109">¿Por qué no aparece mi base de datos ClearDB en el portal de hello?</span><span class="sxs-lookup"><span data-stu-id="0bfa7-109">Why isn't my ClearDB database listed in hello portal?</span></span>

<span data-ttu-id="0bfa7-110">Si crea una base de datos ClearDB en hello [portal de Azure](http://portal.azure.com/), base de datos de hello no aparece en hello [portal de Azure clásico](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-110">If you create a ClearDB database in hello [Azure portal](http://portal.azure.com/), hello database doesn't appear in hello [Azure classic portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="0bfa7-111">toowork resolver este problema, puede vincular manualmente la aplicación web de toohello de base de datos.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-111">toowork around this, you can manually link your database toohello web app.</span></span>

<span data-ttu-id="0bfa7-112">De forma similar, si crea una base de datos ClearDB en hello [portal de Azure clásico](http://manage.windowsazure.com/), no podrá ver la base de datos en hello [portal de Azure](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-112">Similarly, if you create a ClearDB database in hello [Azure classic portal](http://manage.windowsazure.com/),  you won't see your database in hello [Azure portal](http://portal.azure.com/).</span></span> <span data-ttu-id="0bfa7-113">En este caso, no existe ninguna solución alternativa.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-113">In this case, no workaround is available.</span></span> 

<span data-ttu-id="0bfa7-114">Para obtener más información, vea [P+F sobre bases de datos MySQL ClearDB con Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-114">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a><span data-ttu-id="0bfa7-115">¿Por qué no se ha migrado mi base de datos ClearDB durante la migración de mi suscripción?</span><span class="sxs-lookup"><span data-stu-id="0bfa7-115">Why wasn't my ClearDB database migrated during my subscription migration?</span></span>

<span data-ttu-id="0bfa7-116">Al realizar una migración de recursos entre suscripciones, se aplican algunas limitaciones.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-116">When you perform resource migration across subscriptions, some limitations apply.</span></span> <span data-ttu-id="0bfa7-117">Una base de datos MySQL ClearDB es un servicio de terceros y no se migra durante la migración de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-117">A ClearDB MySQL database is a third-party service and is not migrated during an Azure subscription migration.</span></span>

<span data-ttu-id="0bfa7-118">Si no administra la migración de saludo de la base de datos de MySQL antes de migrar los recursos de Azure, la base de datos ClearDB MySQL podría no estar disponible.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-118">If you don't manage hello migration of your MySQL database before you migrate your Azure resources, your ClearDB MySQL database might be unavailable.</span></span> <span data-ttu-id="0bfa7-119">tooavoid esto, en primer lugar, migrar manualmente la base de datos ClearDB y, a continuación, migrar Hola suscripción de Azure para su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-119">tooavoid this, first, manually migrate your ClearDB database, and then migrate hello Azure subscription for your web app.</span></span>

<span data-ttu-id="0bfa7-120">Para obtener más información, vea [P+F sobre bases de datos MySQL ClearDB con Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-120">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="how-do-i-turn-on-php-logging-tootroubleshoot-php-issues"></a><span data-ttu-id="0bfa7-121">¿Cómo activar PHP registro de problemas PHP tootroubleshoot?</span><span class="sxs-lookup"><span data-stu-id="0bfa7-121">How do I turn on PHP logging tootroubleshoot PHP issues?</span></span>

<span data-ttu-id="0bfa7-122">tooturn registro PHP:</span><span class="sxs-lookup"><span data-stu-id="0bfa7-122">tooturn on PHP logging:</span></span>

1. <span data-ttu-id="0bfa7-123">Inicie sesión en tooyour [sitio Web de Kudu](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-123">Sign in tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="0bfa7-124">En el menú superior de hello, seleccione **consola de depuración** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-124">In hello top menu, select **Debug Console** > **CMD**.</span></span>
3. <span data-ttu-id="0bfa7-125">Seleccione hello **sitio** carpeta.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-125">Select hello **Site** folder.</span></span>
4. <span data-ttu-id="0bfa7-126">Seleccione hello **wwwroot** carpeta.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-126">Select hello **wwwroot** folder.</span></span>
5. <span data-ttu-id="0bfa7-127">Seleccione hello  **+**  icono y, a continuación, seleccione **nuevo archivo**.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-127">Select hello **+** icon, and then select **New File**.</span></span>
6. <span data-ttu-id="0bfa7-128">Establecer nombre de archivo de hello demasiado**. user.ini**.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-128">Set hello file name too**.user.ini**.</span></span>
7. <span data-ttu-id="0bfa7-129">Seleccione a continuación el icono de lápiz Hola demasiado**. user.ini**.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-129">Select hello pencil icon next too**.user.ini**.</span></span>
8. <span data-ttu-id="0bfa7-130">En el archivo hello, agregue este código:`log_errors=on`</span><span class="sxs-lookup"><span data-stu-id="0bfa7-130">In hello file, add this code: `log_errors=on`</span></span>
9. <span data-ttu-id="0bfa7-131">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-131">Select **Save**.</span></span>
10. <span data-ttu-id="0bfa7-132">Seleccione a continuación el icono de lápiz Hola demasiado**wp-config.php**.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-132">Select hello pencil icon next too**wp-config.php**.</span></span>
11. <span data-ttu-id="0bfa7-133">Cambiar Hola texto toohello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="0bfa7-133">Change hello text toohello following code:</span></span>
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging too/wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings tooscreendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors tooscreenini_set('display_errors', 0);
   ```
12. <span data-ttu-id="0bfa7-134">Hola portal de Azure, en el menú de aplicación web de hello, reinicie la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-134">In hello Azure portal, in hello web app menu, restart your web app.</span></span>

<span data-ttu-id="0bfa7-135">Para obtener más información, vea [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/) (Habilitar los registros de errores de WordPress).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-135">For more information, see [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a><span data-ttu-id="0bfa7-136">¿Cómo se pueden registrar errores de aplicaciones de Python en las aplicaciones hospedadas en App Service?</span><span class="sxs-lookup"><span data-stu-id="0bfa7-136">How do I log Python application errors in apps that are hosted in App Service?</span></span>

<span data-ttu-id="0bfa7-137">errores de aplicación de Python toocapture:</span><span class="sxs-lookup"><span data-stu-id="0bfa7-137">toocapture Python application errors:</span></span>

1. <span data-ttu-id="0bfa7-138">Hola portal de Azure, en la aplicación web, seleccione **configuración**.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-138">In hello Azure portal, in your web app, select **Settings**.</span></span>
2. <span data-ttu-id="0bfa7-139">En hello **configuración** ficha, seleccione **configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-139">On hello **Settings** tab, select **Application settings**.</span></span>
3. <span data-ttu-id="0bfa7-140">En **configuración de la aplicación**, escriba Hola siguiendo el par clave/valor:</span><span class="sxs-lookup"><span data-stu-id="0bfa7-140">Under **App settings**, enter hello following key/value pair:</span></span>
    * <span data-ttu-id="0bfa7-141">Clave: WSGI_LOG</span><span class="sxs-lookup"><span data-stu-id="0bfa7-141">Key : WSGI_LOG</span></span>
    * <span data-ttu-id="0bfa7-142">Valor: D:\home\site\wwwroot\logs.txt (escriba el nombre de archivo que elija)</span><span class="sxs-lookup"><span data-stu-id="0bfa7-142">Value : D:\home\site\wwwroot\logs.txt (enter your choice of file name)</span></span>

<span data-ttu-id="0bfa7-143">Ahora debería ver los errores en el archivo de logs.txt hello en la carpeta wwwroot de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-143">You should now see errors in hello logs.txt file in hello wwwroot folder.</span></span>

## <a name="how-do-i-change-hello-version-of-hello-nodejs-application-that-is-hosted-in-app-service"></a><span data-ttu-id="0bfa7-144">¿Cómo se cambia la versión de Hola de hello aplicación Node.js que se hospeda en el servicio de aplicaciones?</span><span class="sxs-lookup"><span data-stu-id="0bfa7-144">How do I change hello version of hello Node.js application that is hosted in App Service?</span></span>

<span data-ttu-id="0bfa7-145">versión de hello toochange de hello aplicación Node.js, puede usar uno de hello siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="0bfa7-145">toochange hello version of hello Node.js application, you can use one of hello following options:</span></span>

*   <span data-ttu-id="0bfa7-146">Hola portal de Azure, use **configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-146">In hello Azure portal, use **App settings**.</span></span>
    1. <span data-ttu-id="0bfa7-147">Hola portal de Azure, vaya tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-147">In hello Azure portal, go tooyour web app.</span></span>
    2. <span data-ttu-id="0bfa7-148">En hello **configuración** hoja, seleccione **configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-148">On hello **Settings** blade, select **Application settings**.</span></span>
    3. <span data-ttu-id="0bfa7-149">En **configuración de la aplicación**, puede incluir WEBSITE_NODE_DEFAULT_VERSION como clave de Hola y Hola versión de Node.js que desee como valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-149">In **App settings**, you can include WEBSITE_NODE_DEFAULT_VERSION as hello key, and hello version of Node.js you want as hello value.</span></span>
    4. <span data-ttu-id="0bfa7-150">Vaya tooyour [consola Kudu](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-150">Go tooyour [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
    5. <span data-ttu-id="0bfa7-151">toocheck Hola versión Node.js, escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="0bfa7-151">toocheck hello Node.js version, enter hello following command:</span></span>  
   ```
   node -v
   ```
*   <span data-ttu-id="0bfa7-152">Modifique el archivo de hello iisnode.yml.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-152">Modify hello iisnode.yml file.</span></span> <span data-ttu-id="0bfa7-153">Versión de Node.js Hola variación en el archivo de hello iisnode.yml solo establece entorno en tiempo de ejecución de Hola que iisnode utiliza.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-153">Changing hello Node.js version in hello iisnode.yml file only sets hello runtime environment that iisnode uses.</span></span> <span data-ttu-id="0bfa7-154">Su cmd Kudu y otros seguir usan la versión Node.js de Hola que se establece en **configuración de la aplicación** Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-154">Your Kudu cmd and others still use hello Node.js version that is set in **App settings** in hello Azure portal.</span></span>

    <span data-ttu-id="0bfa7-155">tooset hello iisnode.yml manualmente, cree un archivo de iisnode.yml en la carpeta raíz de aplicación.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-155">tooset hello iisnode.yml manually, create an iisnode.yml file in your app root folder.</span></span> <span data-ttu-id="0bfa7-156">En el archivo de hello, incluya Hola después de línea:</span><span class="sxs-lookup"><span data-stu-id="0bfa7-156">In hello file, include hello following line:</span></span>
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   <span data-ttu-id="0bfa7-157">Establecer archivo de hello iisnode.yml mediante package.json durante la implementación de control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-157">Set hello iisnode.yml file by using package.json during source control deployment.</span></span>
    <span data-ttu-id="0bfa7-158">Hola proceso de implementación del control de origen de Azure implica Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0bfa7-158">hello Azure source control deployment process involves hello following steps:</span></span>
    1. <span data-ttu-id="0bfa7-159">Mueve la aplicación de toohello contenido web de Azure.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-159">Moves content toohello Azure web app.</span></span>
    2. <span data-ttu-id="0bfa7-160">Crea un script de implementación predeterminado, si no hay uno (deploy.cmd, archivos de implementación.) en la carpeta raíz de hello web app.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-160">Creates a default deployment script, if there isn’t one (deploy.cmd, .deployment files) in hello web app root folder.</span></span>
    3. <span data-ttu-id="0bfa7-161">Ejecuta un script de implementación en el que crea un archivo iisnode.yml si mencionan versión Node.js de hello en el archivo de hello package.json > motor de`"engines": {"node": "5.9.1","npm": "3.7.3"}`</span><span class="sxs-lookup"><span data-stu-id="0bfa7-161">Runs a deployment script in which it creates an iisnode.yml file if you mention hello Node.js version in hello package.json file > engine `"engines": {"node": "5.9.1","npm": "3.7.3"}`</span></span>
    4. <span data-ttu-id="0bfa7-162">archivo de Hello iisnode.yml tiene Hola después de la línea de código:</span><span class="sxs-lookup"><span data-stu-id="0bfa7-162">hello iisnode.yml file has hello following line of code:</span></span>
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-hello-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a><span data-ttu-id="0bfa7-163">Aparece el mensaje de Hola "Error al establecer una conexión de base de datos" en mi aplicación WordPress que se hospeda en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-163">I see hello message "Error establishing a database connection" in my WordPress app that's hosted in App Service.</span></span> <span data-ttu-id="0bfa7-164">¿Cómo se soluciona este problema?</span><span class="sxs-lookup"><span data-stu-id="0bfa7-164">How do I troubleshoot this?</span></span>

<span data-ttu-id="0bfa7-165">Si ve este error en la aplicación de Azure WordPress, tooenable php_errors.log y debug.log, pasos de hello completa se detallan en [registros de errores de WordPress habilitar](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-165">If you see this error in your Azure WordPress app, tooenable php_errors.log and debug.log, complete hello steps detailed in [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

<span data-ttu-id="0bfa7-166">Cuando se habilitan los registros de hello, reproducir el error de hello y, a continuación, comprobar Hola registros toosee si se está quedando sin conexiones:</span><span class="sxs-lookup"><span data-stu-id="0bfa7-166">When hello logs are enabled, reproduce hello error, and then check hello logs toosee if you are running out of connections:</span></span>
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded hello ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

<span data-ttu-id="0bfa7-167">Si ve este error en los archivos debug.log o php_errors.log, la aplicación supera el número Hola de conexiones.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-167">If you see this error in your debug.log or php_errors.log files, your app is exceeding hello number of connections.</span></span> <span data-ttu-id="0bfa7-168">Si está hospedando en ClearDB, compruebe el número de Hola de conexiones que están disponibles en su [plan de servicio](https://www.cleardb.com/pricing.view).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-168">If you’re hosting on ClearDB, verify hello number of connections that are available in your [service plan](https://www.cleardb.com/pricing.view).</span></span>

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a><span data-ttu-id="0bfa7-169">¿Cómo se puede depurar una aplicación Node.js hospedada en App Service?</span><span class="sxs-lookup"><span data-stu-id="0bfa7-169">How do I debug a Node.js app that's hosted in App Service?</span></span>

1.  <span data-ttu-id="0bfa7-170">Vaya tooyour [consola Kudu](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-170">Go tooyour [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span></span>
2.  <span data-ttu-id="0bfa7-171">Carpeta de registros de aplicación de vaya tooyour (D:\home\LogFiles\Application).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-171">Go tooyour application logs folder (D:\home\LogFiles\Application).</span></span>
3.  <span data-ttu-id="0bfa7-172">En el archivo de logging_errors.txt hello, busque el contenido.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-172">In hello logging_errors.txt file, check for content.</span></span>

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a><span data-ttu-id="0bfa7-173">¿Cómo se instalan módulos nativos de Python en una aplicación web de App Service o una aplicación de API?</span><span class="sxs-lookup"><span data-stu-id="0bfa7-173">How do I install native Python modules in an App Service web app or API app?</span></span>

<span data-ttu-id="0bfa7-174">Algunos paquetes podrían no instalarse si se usa pip en Azure.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-174">Some packages might not install by using pip in Azure.</span></span> <span data-ttu-id="0bfa7-175">paquete de Hello podría no estar disponible en el índice del paquete Python Hola o un compilador puede ser necesario (un compilador no está disponible en el equipo de Hola que se ejecuta la aplicación web de hello en servicio de aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-175">hello package might not be available on hello Python Package Index, or a compiler might be required (a compiler is not available on hello computer that is running hello web app in App Service).</span></span> <span data-ttu-id="0bfa7-176">Para obtener información sobre cómo instalar módulos nativos en aplicaciones web de App Service y aplicaciones de API, vea [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/) (Instalar módulos de Python en App Service).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-176">For information about installing native modules in App Service web apps and API apps, see [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span></span>

## <a name="how-do-i-deploy-a-django-app-tooapp-service-by-using-git-and-hello-new-version-of-python"></a><span data-ttu-id="0bfa7-177">¿Cómo implementar un tooApp de aplicación Django servicio mediante Git y Hola nueva versión de Python</span><span class="sxs-lookup"><span data-stu-id="0bfa7-177">How do I deploy a Django app tooApp Service by using Git and hello new version of Python?</span></span>

<span data-ttu-id="0bfa7-178">Para obtener información acerca de cómo instalar Django, consulte [implementar un tooApp de aplicación Django servicio](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-178">For information about installing Django, see [Deploying a Django app tooApp Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span></span>

## <a name="where-are-hello-tomcat-log-files-located"></a><span data-ttu-id="0bfa7-179">¿Dónde están los archivos de registro de Tomcat Hola ubicados?</span><span class="sxs-lookup"><span data-stu-id="0bfa7-179">Where are hello Tomcat log files located?</span></span>

<span data-ttu-id="0bfa7-180">En Azure Marketplace e implementaciones personalizadas:</span><span class="sxs-lookup"><span data-stu-id="0bfa7-180">For Azure Marketplace and custom deployments:</span></span>

* <span data-ttu-id="0bfa7-181">Ubicación de la carpeta: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span><span class="sxs-lookup"><span data-stu-id="0bfa7-181">Folder location: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span></span>
* <span data-ttu-id="0bfa7-182">Archivos de interés:</span><span class="sxs-lookup"><span data-stu-id="0bfa7-182">Files of interest:</span></span>
    * <span data-ttu-id="0bfa7-183">catalina.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="0bfa7-183">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="0bfa7-184">host-manager.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="0bfa7-184">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="0bfa7-185">localhost.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="0bfa7-185">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="0bfa7-186">manager.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="0bfa7-186">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="0bfa7-187">site_access_log.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="0bfa7-187">site_access_log.*yyyy-mm-dd*.log</span></span>


<span data-ttu-id="0bfa7-188">Para implementaciones de **configuración de la aplicación** en el portal:</span><span class="sxs-lookup"><span data-stu-id="0bfa7-188">For portal **App settings** deployments:</span></span>

* <span data-ttu-id="0bfa7-189">Ubicación de la carpeta: D:\home\LogFiles</span><span class="sxs-lookup"><span data-stu-id="0bfa7-189">Folder location: D:\home\LogFiles</span></span>
* <span data-ttu-id="0bfa7-190">Archivos de interés:</span><span class="sxs-lookup"><span data-stu-id="0bfa7-190">Files of interest:</span></span>
    * <span data-ttu-id="0bfa7-191">catalina.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="0bfa7-191">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="0bfa7-192">host-manager.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="0bfa7-192">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="0bfa7-193">localhost.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="0bfa7-193">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="0bfa7-194">manager.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="0bfa7-194">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="0bfa7-195">site_access_log.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="0bfa7-195">site_access_log.*yyyy-mm-dd*.log</span></span>

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a><span data-ttu-id="0bfa7-196">¿Cómo se solucionan los errores de conexión de JDBC Driver?</span><span class="sxs-lookup"><span data-stu-id="0bfa7-196">How do I troubleshoot JDBC driver connection errors?</span></span>

<span data-ttu-id="0bfa7-197">Puede aparecer Hola sigue mensaje en los registros de Tomcat:</span><span class="sxs-lookup"><span data-stu-id="0bfa7-197">You might see hello following message in your Tomcat logs:</span></span>

```
hello web application[ROOT] registered hello JDBC driver [com.mysql.jdbc.Driver] but failed toounregister it when hello web application was stopped. tooprevent a memory leak,hello JDBC Driver has been forcibly unregistered
```

<span data-ttu-id="0bfa7-198">error de Hola tooresolve:</span><span class="sxs-lookup"><span data-stu-id="0bfa7-198">tooresolve hello error:</span></span>

1. <span data-ttu-id="0bfa7-199">Hola sqljdbc*.jar archivo se quitará la carpeta de aplicación/lib.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-199">Remove hello sqljdbc*.jar file from your app/lib folder.</span></span>
2. <span data-ttu-id="0bfa7-200">Si usas Hola Tomcat o Azure Marketplace Tomcat servidor web personalizado, copie esta carpeta .jar archivo toohello Tomcat "lib".</span><span class="sxs-lookup"><span data-stu-id="0bfa7-200">If you are using hello custom Tomcat or Azure Marketplace Tomcat web server, copy this .jar file toohello Tomcat lib folder.</span></span>
3. <span data-ttu-id="0bfa7-201">Si va a habilitar Java de Hola portal de Azure (seleccione **Java 1.8** > **servidor de Tomcat**), archivo de copia hello sqljdbc.* jar en carpeta Hola aplicación tooyour paralelas.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-201">If you are enabling Java from hello Azure portal (select **Java 1.8** > **Tomcat server**), copy hello sqljdbc.* jar file in hello folder that's parallel tooyour app.</span></span> <span data-ttu-id="0bfa7-202">A continuación, agregue Hola classpath el archivo web.config de configuración toohello siguiente:</span><span class="sxs-lookup"><span data-stu-id="0bfa7-202">Then, add hello following classpath setting toohello web.config file:</span></span>

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path toohello sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-toocopy-live-log-files"></a><span data-ttu-id="0bfa7-203">¿Por qué veo errores cuando intente archivos de registro en vivo de toocopy?</span><span class="sxs-lookup"><span data-stu-id="0bfa7-203">Why do I see errors when I attempt toocopy live log files?</span></span>

<span data-ttu-id="0bfa7-204">Si trata de archivos de registro en vivo de toocopy para una aplicación de Java (por ejemplo, Tomcat), puede aparecer este error FTP:</span><span class="sxs-lookup"><span data-stu-id="0bfa7-204">If you try toocopy live log files for a Java app (for example, Tomcat), you might see this FTP error:</span></span>

```
Error transferring file [filename] Copying files from remote side failed.
    
hello process cannot access hello file because it is being used by another process.
```

<span data-ttu-id="0bfa7-205">mensaje de error de Hello puede variar en función de cliente hello FTP.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-205">hello error message might vary, depending on hello FTP client.</span></span>

<span data-ttu-id="0bfa7-206">Todas las aplicaciones de Java tienen este problema de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-206">All Java apps have this locking issue.</span></span> <span data-ttu-id="0bfa7-207">Kudu sólo admite la descarga de este archivo mientras se está ejecutando la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-207">Only Kudu supports downloading this file while hello app is running.</span></span>

<span data-ttu-id="0bfa7-208">Detener aplicación hello permite el acceso FTP archivos toothese.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-208">Stopping hello app allows FTP access toothese files.</span></span>

<span data-ttu-id="0bfa7-209">Otra solución alternativa es toowrite un trabajo Web que se ejecuta según una programación y copia estas tooa otro directorio de archivos.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-209">Another workaround is toowrite a WebJob that runs on a schedule and copies these files tooa different directory.</span></span> <span data-ttu-id="0bfa7-210">Para un proyecto de ejemplo, vea hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) proyecto.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-210">For a sample project, see hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) project.</span></span>

## <a name="where-do-i-find-hello-log-files-for-jetty"></a><span data-ttu-id="0bfa7-211">¿Dónde se puede encontrar los archivos de registro de hello para Jetty?</span><span class="sxs-lookup"><span data-stu-id="0bfa7-211">Where do I find hello log files for Jetty?</span></span>

<span data-ttu-id="0bfa7-212">Marketplace y las implementaciones personalizadas, archivo de registro de hello radica en carpeta de D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs Hola.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-212">For Marketplace and custom deployments, hello log file is in hello D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs folder.</span></span> <span data-ttu-id="0bfa7-213">Tenga en cuenta que la ubicación de la carpeta de hello depende de versión Hola de Jetty que usa.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-213">Note that hello folder location depends on hello version of Jetty you are using.</span></span> <span data-ttu-id="0bfa7-214">Por ejemplo, la ruta de acceso de hello proporcionada aquí sirve de Jetty 9.1.2.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-214">For example, hello path provided here is for Jetty 9.1.2.</span></span> <span data-ttu-id="0bfa7-215">Busque jetty_*AAAA_MM_DD*.stderrout.log.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-215">Look for jetty_*YYYY_MM_DD*.stderrout.log.</span></span>

<span data-ttu-id="0bfa7-216">Para implementaciones de configuración de la aplicación de portal, archivo de registro de hello está en D:\home\LogFiles.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-216">For portal App Setting deployments, hello log file is in D:\home\LogFiles.</span></span> <span data-ttu-id="0bfa7-217">Busque jetty_*AAAA_MM_DD*.stderrout.log.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-217">Look for jetty_*YYYY_MM_DD*.stderrout.log</span></span>

## <a name="can-i-send-email-from-my-azure-web-app"></a><span data-ttu-id="0bfa7-218">¿Puedo enviar correo electrónico desde la aplicación web de Azure?</span><span class="sxs-lookup"><span data-stu-id="0bfa7-218">Can I send email from my Azure web app?</span></span>

<span data-ttu-id="0bfa7-219">App Service no tiene una característica integrada de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-219">App Service doesn't have a built-in email feature.</span></span> <span data-ttu-id="0bfa7-220">Para conocer algunas alternativas adecuadas para enviar correo electrónico desde la aplicación, vea este [debate de Stack Overflow](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-220">For some good alternatives for sending email from your app, see this [Stack Overflow discussion](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span></span>

## <a name="why-does-my-wordpress-site-redirect-tooanother-url"></a><span data-ttu-id="0bfa7-221">¿Por qué mi sitio de WordPress tooanother dirección URL de redireccionamiento?</span><span class="sxs-lookup"><span data-stu-id="0bfa7-221">Why does my WordPress site redirect tooanother URL?</span></span>

<span data-ttu-id="0bfa7-222">Si recientemente ha migrado tooAzure, WordPress podría redirigir la dirección URL del dominio antiguo toohello.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-222">If you have recently migrated tooAzure, WordPress might redirect toohello old domain URL.</span></span> <span data-ttu-id="0bfa7-223">Esto se debe a una configuración de base de datos de MySQL Hola.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-223">This is caused by a setting in hello MySQL database.</span></span>

<span data-ttu-id="0bfa7-224">WordPress amigo + es una extensión de sitio de Azure que puede usar la dirección URL de redirección de hello tooupdate directamente en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-224">WordPress Buddy+ is an Azure Site Extension that you can use tooupdate hello redirection URL directly in hello database.</span></span> <span data-ttu-id="0bfa7-225">Para obtener más información sobre el uso de WordPress Buddy+, vea [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (Herramientas de WordPress y migración de MySQL con WordPress Buddy+).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-225">For more information about using WordPress Buddy+, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

<span data-ttu-id="0bfa7-226">O bien, si prefiere toomanually actualización dirección URL de redirección hello mediante consultas SQL o PHPMyAdmin, consulte [WordPress: redirigir la dirección URL de toowrong](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-226">Alternatively, if you prefer toomanually update hello redirection URL by using SQL queries or PHPMyAdmin, see [WordPress: Redirecting toowrong URL](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span></span>

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a><span data-ttu-id="0bfa7-227">¿Cómo se cambia la contraseña de inicio de sesión de WordPress?</span><span class="sxs-lookup"><span data-stu-id="0bfa7-227">How do I change my WordPress sign-in password?</span></span>

<span data-ttu-id="0bfa7-228">Si ha olvidado su contraseña de inicio de sesión de WordPress, puede usar WordPress amigo + tooupdate lo.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-228">If you have forgotten your WordPress sign-in password, you can use WordPress Buddy+ tooupdate it.</span></span> <span data-ttu-id="0bfa7-229">tooreset su contraseña, instalación Hola WordPress amigo + extensión de sitio de Azure y pasos de hello completa, a continuación, se describen en [WordPress herramientas y la migración de MySQL con WordPress amigo +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-229">tooreset your password, install hello WordPress Buddy+ Azure Site Extension, and then complete hello steps described in [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="i-cant-sign-in-toowordpress-how-do-i-resolve-this"></a><span data-ttu-id="0bfa7-230">No se puede iniciar sesión en tooWordPress.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-230">I can't sign in tooWordPress.</span></span> <span data-ttu-id="0bfa7-231">¿Cómo se resuelve este problema?</span><span class="sxs-lookup"><span data-stu-id="0bfa7-231">How do I resolve this?</span></span>

<span data-ttu-id="0bfa7-232">Si está bloqueado y no puede entrar en WordPress después de instalar recientemente un complemento, dicho complemento podría ser defectuoso.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-232">If you find yourself locked out of WordPress after recently installing a plugin, you might have a faulty plugin.</span></span> <span data-ttu-id="0bfa7-233">WordPress Buddy+ es una extensión de sitio de Azure que permite deshabilitar complementos en WordPress.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-233">WordPress Buddy+ is an Azure Site Extension that can help you disable plugins in WordPress.</span></span> <span data-ttu-id="0bfa7-234">Para obtener más información, vea [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (Herramientas de WordPress y migración de MySQL con WordPress Buddy+).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-234">For more information, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="how-do-i-migrate-my-wordpress-database"></a><span data-ttu-id="0bfa7-235">¿Cómo puedo migrar mi base de datos de WordPress?</span><span class="sxs-lookup"><span data-stu-id="0bfa7-235">How do I migrate my WordPress database?</span></span>

<span data-ttu-id="0bfa7-236">Tiene varias opciones para migrar bases de datos de MySQL de Hola que es el sitio Web de WordPress tooyour conectado:</span><span class="sxs-lookup"><span data-stu-id="0bfa7-236">You have multiple options for migrating hello MySQL database that's connected tooyour WordPress website:</span></span>

* <span data-ttu-id="0bfa7-237">Los desarrolladores: Hola de uso [símbolo del sistema o PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span><span class="sxs-lookup"><span data-stu-id="0bfa7-237">Developers: Use hello [command prompt or PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span></span>
* <span data-ttu-id="0bfa7-238">Los usuarios que no son desarrolladores deben usar [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-238">Non-developers: Use [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span></span>

## <a name="how-do-i-help-make-wordpress-more-secure"></a><span data-ttu-id="0bfa7-239">¿Cómo puedo conseguir que WordPress sea más seguro?</span><span class="sxs-lookup"><span data-stu-id="0bfa7-239">How do I help make WordPress more secure?</span></span>

<span data-ttu-id="0bfa7-240">toolearn sobre prácticas recomendadas de seguridad para WordPress, vea [las prácticas recomendadas para la seguridad de WordPress en Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span><span class="sxs-lookup"><span data-stu-id="0bfa7-240">toolearn about security best practices for WordPress, see [Best practices for WordPress security in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span></span>

## <a name="i-am-trying-toouse-phpmyadmin-and-i-see-hello-message-access-denied-how-do-i-resolve-this"></a><span data-ttu-id="0bfa7-241">Estoy tratando de toouse PHPMyAdmin y aparece el mensaje de Hola "Acceso denegado".</span><span class="sxs-lookup"><span data-stu-id="0bfa7-241">I am trying toouse PHPMyAdmin, and I see hello message “Access denied.”</span></span> <span data-ttu-id="0bfa7-242">¿Cómo se resuelve este problema?</span><span class="sxs-lookup"><span data-stu-id="0bfa7-242">How do I resolve this?</span></span>

<span data-ttu-id="0bfa7-243">Puede experimentar este problema si la característica de hello MySQL en la aplicación no se está ejecutando todavía en esta instancia de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-243">You might experience this issue if hello MySQL in-app feature isn't running yet in this App Service instance.</span></span> <span data-ttu-id="0bfa7-244">tooresolve Hola problema, intente tooaccess su sitio Web.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-244">tooresolve hello issue, try tooaccess your website.</span></span> <span data-ttu-id="0bfa7-245">Esto inicia procesos Hola necesario, por ejemplo el proceso de hello en la aplicación de MySQL.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-245">This starts hello required processes, including hello MySQL in-app process.</span></span> <span data-ttu-id="0bfa7-246">tooverify que MySQL que se está ejecutando en la aplicación, en el Explorador de proceso, asegúrese de que mysqld.exe se muestra en los procesos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-246">tooverify that MySQL in-app is running, in Process Explorer, ensure that mysqld.exe is listed in hello processes.</span></span>

<span data-ttu-id="0bfa7-247">Después de asegurarse de que se está ejecutando en la aplicación de MySQL, intente toouse PHPMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-247">After you ensure that MySQL in-app is running, try toouse PHPMyAdmin.</span></span>

## <a name="i-get-an-http-403-error-when-i-try-tooimport-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a><span data-ttu-id="0bfa7-248">Obtengo un error 403 de HTTP cuando intente tooimport o exportar mi base de datos de MySQL en la aplicación mediante PHPMyadmin.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-248">I get an HTTP 403 error when I try tooimport or export my MySQL in-app database by using PHPMyadmin.</span></span> <span data-ttu-id="0bfa7-249">¿Cómo se resuelve este problema?</span><span class="sxs-lookup"><span data-stu-id="0bfa7-249">How do I resolve this?</span></span>

<span data-ttu-id="0bfa7-250">Si usa una versión antigua de Chrome, podría tratarse de un problema conocido.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-250">If you are using an older version of Chrome, you might be experiencing a known bug.</span></span> <span data-ttu-id="0bfa7-251">problema de hello tooresolve, versión más reciente de actualización tooa de Chrome.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-251">tooresolve hello issue, upgrade tooa newer version of Chrome.</span></span> <span data-ttu-id="0bfa7-252">Intentar usar un explorador diferente, como Internet Explorer o Edge, donde hello problema no ocurre.</span><span class="sxs-lookup"><span data-stu-id="0bfa7-252">Also try using a different browser, like Internet Explorer or Edge, where hello issue does not occur.</span></span>
