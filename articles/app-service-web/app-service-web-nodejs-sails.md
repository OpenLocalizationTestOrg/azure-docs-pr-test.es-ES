---
title: "aaaDeploy una tooAzure de aplicación web de Sails.js servicio de aplicaciones | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodeploy una aplicación Node.js servicio de aplicaciones de Azure. Este tutorial muestra cómo toodeploy una Sails.js web app."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 8877ddc8-1476-45ae-9e7f-3c75917b4564
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: f5b2518b9c87c040845f7268763862be8c15e83e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-sailsjs-web-app-tooazure-app-service"></a><span data-ttu-id="3d038-104">Implementar una aplicación de web Sails.js tooAzure servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="3d038-104">Deploy a Sails.js web app tooAzure App Service</span></span>
<span data-ttu-id="3d038-105">Este tutorial muestra cómo toodeploy una tooAzure de aplicación de Sails.js servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3d038-105">This tutorial shows you how toodeploy a Sails.js app tooAzure App Service.</span></span> <span data-ttu-id="3d038-106">En el proceso de hello, puede recopilar algunos conocimientos generales sobre cómo tooconfigure su toorun de aplicación Node.js en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3d038-106">In hello process, you can glean some general knowledge on how tooconfigure your Node.js app toorun in App Service.</span></span>

<span data-ttu-id="3d038-107">En este artículo, adquirirá destrezas útiles, como las siguientes:</span><span class="sxs-lookup"><span data-stu-id="3d038-107">Here, you will learn useful skills like:</span></span>

* <span data-ttu-id="3d038-108">Configurar una aplicación Sails.js que se ejecute en App Service.</span><span class="sxs-lookup"><span data-stu-id="3d038-108">Configure a Sails.js app run in App Service.</span></span>
* <span data-ttu-id="3d038-109">Implementar un tooApp servicio de aplicación de línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d038-109">Deploy an app tooApp Service from hello command line.</span></span>
* <span data-ttu-id="3d038-110">Stdout y stderr lectura registra tootroubleshoot los problemas de implementación.</span><span class="sxs-lookup"><span data-stu-id="3d038-110">Read stderr and stdout logs tootroubleshoot any deployment issues.</span></span>
* <span data-ttu-id="3d038-111">Almacenar las variables de entorno fuera del control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="3d038-111">Store environment variables outside of source control.</span></span>
* <span data-ttu-id="3d038-112">Acceder a las variables de entorno de Azure desde su aplicación.</span><span class="sxs-lookup"><span data-stu-id="3d038-112">Access Azure environment variables from your app.</span></span>
* <span data-ttu-id="3d038-113">Conectar la base de datos de tooa (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="3d038-113">Connect tooa database (MongoDB).</span></span>

<span data-ttu-id="3d038-114">Debe tener conocimientos prácticos de Sails.js.</span><span class="sxs-lookup"><span data-stu-id="3d038-114">You should have working knowledge of Sails.js.</span></span> <span data-ttu-id="3d038-115">Este tutorial no está previsto toohelp con problemas relacionados con toorunning Sail.js en general.</span><span class="sxs-lookup"><span data-stu-id="3d038-115">This tutorial is not intended toohelp you with issues related toorunning Sail.js in general.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="3d038-116">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="3d038-116">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="3d038-117">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="3d038-117">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="3d038-118">[Azure 1.0 de CLI](app-service-web-nodejs-sails-cli-nodejs.md) – nuestro CLI para modelos de implementación de administración de recursos y clásico Hola</span><span class="sxs-lookup"><span data-stu-id="3d038-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span>
- <span data-ttu-id="3d038-119">[Azure 2.0 CLI](app-service-web-nodejs-sails.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="3d038-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d038-120">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3d038-120">Prerequisites</span></span>
* [<span data-ttu-id="3d038-121">Node.js</span><span class="sxs-lookup"><span data-stu-id="3d038-121">Node.js</span></span>](https://nodejs.org/)
* [<span data-ttu-id="3d038-122">Sails.js</span><span class="sxs-lookup"><span data-stu-id="3d038-122">Sails.js</span></span>](http://sailsjs.org/get-started)
* [<span data-ttu-id="3d038-123">Git</span><span class="sxs-lookup"><span data-stu-id="3d038-123">Git</span></span>](http://www.git-scm.com/downloads)
* [<span data-ttu-id="3d038-124">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="3d038-124">Azure CLI 2.0</span></span>](/cli/azure/install-az-cli2)
* <span data-ttu-id="3d038-125">Una cuenta de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3d038-125">A Microsoft Azure account.</span></span> <span data-ttu-id="3d038-126">Si aún no tiene ninguna, puede [registrarse para una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) o [activar las ventajas de suscriptor de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="3d038-126">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="3d038-127">También puede [probar App Service](https://azure.microsoft.com/try/app-service/) sin una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="3d038-127">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="3d038-128">Crear una aplicación de inicio y trabajar con él para la hora de tooan--ninguna tarjeta de crédito necesario, sin compromisos.</span><span class="sxs-lookup"><span data-stu-id="3d038-128">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a><span data-ttu-id="3d038-129">Paso 1: Creación y configuración de una aplicación de Sails.js localmente</span><span class="sxs-lookup"><span data-stu-id="3d038-129">Step 1: Create and configure a Sails.js app locally</span></span>
<span data-ttu-id="3d038-130">En primer lugar, cree rápidamente una aplicación Sails.js en su entorno de desarrollo con estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3d038-130">First, quickly create a default Sails.js app in your development environment by following these steps:</span></span>

1. <span data-ttu-id="3d038-131">Terminal de línea de comandos de hello abierto de su elección y `CD` tooa directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3d038-131">Open hello command-line terminal of your choice and `CD` tooa working directory.</span></span>
2. <span data-ttu-id="3d038-132">Cree una nueva Sails.js y ejecútela:</span><span class="sxs-lookup"><span data-stu-id="3d038-132">Create a Sails.js app and run it:</span></span>

        sails new <app_name>
        cd <app_name>
        sails lift

    <span data-ttu-id="3d038-133">Asegúrese de que puede navegar por página de inicio predeterminada de toohello en http://localhost:1377.</span><span class="sxs-lookup"><span data-stu-id="3d038-133">Make sure you can navigate toohello default home page at http://localhost:1377.</span></span>

1. <span data-ttu-id="3d038-134">Después, habilite el registro para Azure.</span><span class="sxs-lookup"><span data-stu-id="3d038-134">Next, enable logging for Azure.</span></span> <span data-ttu-id="3d038-135">En el directorio raíz, cree un archivo denominado `iisnode.yml` y agregue Hola después de dos líneas:</span><span class="sxs-lookup"><span data-stu-id="3d038-135">In your root directory, create a file called `iisnode.yml` and add hello following two lines:</span></span>

        loggingEnabled: true
        logDirectory: iisnode

    <span data-ttu-id="3d038-136">Registro ahora está habilitado para hello [iisnode](https://github.com/tjanczuk/iisnode) que el servicio de aplicaciones de Azure usa toorun Node.js aplicaciones de servidor.</span><span class="sxs-lookup"><span data-stu-id="3d038-136">Logging is now enabled for hello [iisnode](https://github.com/tjanczuk/iisnode) server that Azure App Service uses toorun Node.js apps.</span></span> 
    <span data-ttu-id="3d038-137">Para obtener más información sobre su funcionamiento, consulte [cómo toodebug una Node.js web aplicación de servicio de aplicaciones de Azure](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="3d038-137">For more information on how this works, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

2. <span data-ttu-id="3d038-138">A continuación, configure las variables de entorno de Azure de hello Sails.js aplicación toouse.</span><span class="sxs-lookup"><span data-stu-id="3d038-138">Next, configure hello Sails.js app toouse Azure environment variables.</span></span> <span data-ttu-id="3d038-139">Abra config/env/production.js tooconfigure el entorno de producción y establezca `port` y `hookTimeout`:</span><span class="sxs-lookup"><span data-stu-id="3d038-139">Open config/env/production.js tooconfigure your production environment, and set `port` and `hookTimeout`:</span></span>

        module.exports = {

            // Use process.env.port toohandle web requests toohello default HTTP port
            port: process.env.port,
            // Increase hooks timout too30 seconds
            // This avoids hello Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    <span data-ttu-id="3d038-140">Encontrará documentación sobre estas opciones de configuración en la [documentación de Sails.js](http://sailsjs.org/documentation/reference/configuration/sails-config).</span><span class="sxs-lookup"><span data-stu-id="3d038-140">You can find documentation for these configuration settings in the  [Sails.js Documentation](http://sailsjs.org/documentation/reference/configuration/sails-config).</span></span>

4. <span data-ttu-id="3d038-141">Después, codificar hello Node.js versión que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="3d038-141">Next, hardcode hello Node.js version you want toouse.</span></span> <span data-ttu-id="3d038-142">En package.json, agregue el siguiente hello `engines` propiedad tooset hello Node.js versión tooone que queremos.</span><span class="sxs-lookup"><span data-stu-id="3d038-142">In package.json, add hello following `engines` property tooset hello Node.js version tooone that we want.</span></span>

        "engines": {
            "node": "6.9.1"
        },

5. <span data-ttu-id="3d038-143">Por último, inicialice un repositorio Git y valide los archivos.</span><span class="sxs-lookup"><span data-stu-id="3d038-143">Finally, initialize a Git repository and commit your files.</span></span> <span data-ttu-id="3d038-144">En el Hola raíz de la aplicación (donde es package.json), ejecute hello siguientes comandos de Git:</span><span class="sxs-lookup"><span data-stu-id="3d038-144">In hello application root (where package.json is), run hello following Git commands:</span></span>

        git init
        git add .
        git commit -m "<your commit message>"

<span data-ttu-id="3d038-145">El código está listo toobe implementado.</span><span class="sxs-lookup"><span data-stu-id="3d038-145">Your code is ready toobe deployed.</span></span> 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a><span data-ttu-id="3d038-146">Paso 2: Creación de una aplicación de Azure e implementación de Sails.js</span><span class="sxs-lookup"><span data-stu-id="3d038-146">Step 2: Create an Azure app and deploy Sails.js</span></span>

<span data-ttu-id="3d038-147">A continuación, cree Hola recurso del servicio de aplicación en Azure e implemente su tooit de aplicación Sails.js.</span><span class="sxs-lookup"><span data-stu-id="3d038-147">Next, create hello App Service resource in Azure and deploy your Sails.js app tooit.</span></span>

1. <span data-ttu-id="3d038-148">inicio de sesión tooAzure de este modo:</span><span class="sxs-lookup"><span data-stu-id="3d038-148">log in tooAzure like so:</span></span>

        az login

    <span data-ttu-id="3d038-149">Siga el inicio de sesión de hello toocontinue prompt hello en un explorador con una cuenta de Microsoft que tenga su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3d038-149">Follow hello prompt toocontinue hello login in a browser with a Microsoft account that has your Azure subscription.</span></span>

3. <span data-ttu-id="3d038-150">Establecer usuario de implementación de hello para el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3d038-150">Set hello deployment user for App Service.</span></span> <span data-ttu-id="3d038-151">Posteriormente implementará el código mediante estas credenciales.</span><span class="sxs-lookup"><span data-stu-id="3d038-151">You will deploy code using these credentials later.</span></span>
   
        az appservice web deployment user set --user-name <username> --password <password>

3. <span data-ttu-id="3d038-152">Cree un [grupo de recursos](../azure-resource-manager/resource-group-overview.md) con un nombre.</span><span class="sxs-lookup"><span data-stu-id="3d038-152">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with a name.</span></span> <span data-ttu-id="3d038-153">Para este tutorial Node.js, no necesita realmente tooknow qué es.</span><span class="sxs-lookup"><span data-stu-id="3d038-153">For this Node.js tutorial, you don't really need tooknow what it is.</span></span>

        az group create --location "<location>" --name my-sailsjs-app-group

    <span data-ttu-id="3d038-154">toosee los posibles valores pueden usar para `<location>`, usar hello `az appservice list-locations` comando de CLI.</span><span class="sxs-lookup"><span data-stu-id="3d038-154">toosee what possible values you can use for `<location>`, use hello `az appservice list-locations` CLI command.</span></span>

3. <span data-ttu-id="3d038-155">Cree "GRATIS" un [plan de App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) con un nombre.</span><span class="sxs-lookup"><span data-stu-id="3d038-155">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) with a name.</span></span> <span data-ttu-id="3d038-156">Para este tutorial de node.js, solo es preciso saber que en este plan no se cobrarán las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="3d038-156">For this Node.js tutorial, just know that you won't be charged for web apps in this plan.</span></span>

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. <span data-ttu-id="3d038-157">Cree una nueva aplicación web con un nombre único en `<app_name>`.</span><span class="sxs-lookup"><span data-stu-id="3d038-157">Create a new web app with a unique name in `<app_name>`.</span></span>

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a><span data-ttu-id="3d038-158">Paso 3: Configuración e implementación de la aplicación Sails.js</span><span class="sxs-lookup"><span data-stu-id="3d038-158">Step 3: Configure and deploy your Sails.js app</span></span>

1. <span data-ttu-id="3d038-159">Configurar implementación de Git local para su nueva aplicación web con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="3d038-159">Configure local Git deployment for your new web app with hello following command:</span></span>

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="3d038-160">Obtendrá una salida JSON como este, lo que significa que está configurado dicho repositorio de Git remoto hello:</span><span class="sxs-lookup"><span data-stu-id="3d038-160">You will get a JSON output like this, which means that hello remote Git repository is configured:</span></span>

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. <span data-ttu-id="3d038-161">Agregar dirección URL de Hola Hola JSON como un Git remoto para el repositorio local (llamado `azure` para simplificar el trabajo).</span><span class="sxs-lookup"><span data-stu-id="3d038-161">Add hello URL in hello JSON as a Git remote for your local repository (called `azure` for simplicity).</span></span>

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. <span data-ttu-id="3d038-162">Implementar la toohello del código de ejemplo `azure` Git remoto.</span><span class="sxs-lookup"><span data-stu-id="3d038-162">Deploy your sample code toohello `azure` Git remote.</span></span> <span data-ttu-id="3d038-163">Cuando se le pida, use las credenciales de implementación de Hola que configuró anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3d038-163">When prompted, use hello deployment credentials you configured earlier.</span></span>

        git push azure master

7. <span data-ttu-id="3d038-164">Por último, simplemente inicie la aplicación de Azure en vivo en el Explorador de hello:</span><span class="sxs-lookup"><span data-stu-id="3d038-164">Finally, just launch your live Azure app in hello browser:</span></span>

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="3d038-165">Ahora debería ver Hola la misma página de inicio de Sails.js.</span><span class="sxs-lookup"><span data-stu-id="3d038-165">You should now see hello same Sails.js home page.</span></span>

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a><span data-ttu-id="3d038-166">Solución de problemas de la implementación</span><span class="sxs-lookup"><span data-stu-id="3d038-166">Troubleshoot your deployment</span></span>
<span data-ttu-id="3d038-167">Si se produce un error en la aplicación Sails.js por algún motivo en el servicio de aplicaciones, encontrar Hola stderr registros toohelp solucionar sus problemas.</span><span class="sxs-lookup"><span data-stu-id="3d038-167">If your Sails.js application fails for some reason in App Service, find hello stderr logs toohelp troubleshoot it.</span></span>
<span data-ttu-id="3d038-168">Para obtener más información, consulte [cómo toodebug una Node.js web aplicación de servicio de aplicaciones de Azure](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="3d038-168">For more information, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>
<span data-ttu-id="3d038-169">Si la aplicación hello ha iniciado correctamente, registro de hello stdout debe muestran mensajes de bienvenida del familiar:</span><span class="sxs-lookup"><span data-stu-id="3d038-169">If hello app has started successfully, hello stdout log should show you hello familiar message:</span></span>

                   .-..-.
    
       Sails              <|    .-..-.
       v0.12.11            |\
                          /|.\
                         / || \
                       ,'  |'  \
                    .-'.-==|/_--'
                    `--'-------' 
       __---___--___---___--___---___--___
     ____---___--___---___--___---___--___-__

    Server lifted in `D:\home\site\wwwroot`
    toosee your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    tooshut down Sails, press <CTRL> + C at any time.

<span data-ttu-id="3d038-170">Puede controlar la granularidad de los registros de stdout Hola Hola [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) archivo.</span><span class="sxs-lookup"><span data-stu-id="3d038-170">You can control granularity of hello stdout logs in hello [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span></span>

## <a name="connect-tooa-database-in-azure"></a><span data-ttu-id="3d038-171">Conectar tooa base de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="3d038-171">Connect tooa database in Azure</span></span>
<span data-ttu-id="3d038-172">base de datos de tooconnect tooa en Azure, se crea la base de datos de Hola de su elección en Azure, por ejemplo, la base de datos de Azure SQL, MySQL, MongoDB, caché de Azure (Redis), etc. y usar Hola correspondiente [adaptador de almacén de datos](https://github.com/balderdashy/sails#compatibility) tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="3d038-172">tooconnect tooa database in Azure, you create hello database of your choice in Azure, such as Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache, etc., and use hello corresponding [datastore adapter](https://github.com/balderdashy/sails#compatibility) tooconnect tooit.</span></span> <span data-ttu-id="3d038-173">Hello pasos de esta sección muestran cómo tooconnect tooMongoDB mediante el uso de un [base de datos de Azure Cosmos](../documentdb/documentdb-protocol-mongodb.md) base de datos que puede admitir las conexiones de cliente de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="3d038-173">hello steps in this section show you how tooconnect tooMongoDB by using an [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, which can support MongoDB client connections.</span></span>

1. <span data-ttu-id="3d038-174">[Cree una cuenta de Cosmos DB que admita el protocolo de MongoDB](../documentdb/documentdb-create-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="3d038-174">[Create a Cosmos DB account with MongoDB protocol support](../documentdb/documentdb-create-mongodb-account.md).</span></span>
2. <span data-ttu-id="3d038-175">[Cree una colección y una base de datos Cosmos DB](../documentdb/documentdb-create-collection.md).</span><span class="sxs-lookup"><span data-stu-id="3d038-175">[Create a Cosmos DB collection and database](../documentdb/documentdb-create-collection.md).</span></span> <span data-ttu-id="3d038-176">Hola nombre de colección de hello no importa, pero necesita Hola nombre de base de datos de hello cuando se conecta desde Sails.js.</span><span class="sxs-lookup"><span data-stu-id="3d038-176">hello name of hello collection doesn't matter, but you need hello name of hello database when you connect from Sails.js.</span></span>
3. <span data-ttu-id="3d038-177">[Buscar información de conexión de hello para la base de datos de la base de datos de Cosmos](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="3d038-177">[Find hello connection information for your Cosmos DB database](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span></span>
2. <span data-ttu-id="3d038-178">Desde el línea de comandos terminal, instalar a adaptador de MongoDB hello:</span><span class="sxs-lookup"><span data-stu-id="3d038-178">From your command-line terminal, install hello MongoDB adapter:</span></span>

        npm install sails-mongo --save

3. <span data-ttu-id="3d038-179">Abra config/connections.js y agregue Hola conexión objeto toohello lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="3d038-179">Open config/connections.js and add hello following connection object toohello list:</span></span>

        docDbMongo: {
            adapter: 'sails-mongo',
            user: process.env.dbuser,
            password: process.env.dbpassword,
            host: process.env.dbhost,
            port: process.env.dbport,
            database: process.env.dbname,
            ssl: true
        },

    > [!NOTE] 
    > <span data-ttu-id="3d038-180">Hola `ssl: true` opción es importante porque [lo requiere la base de datos de Cosmos](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="3d038-180">hello `ssl: true` option is important because [Cosmos DB requires it](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 
    >
    >

4. <span data-ttu-id="3d038-181">Para cada variable de entorno (`process.env.*`), deberá tooset en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3d038-181">For each environment variable (`process.env.*`), you need tooset it in App Service.</span></span> <span data-ttu-id="3d038-182">toodo, ejecución Hola siguientes comandos de su terminal.</span><span class="sxs-lookup"><span data-stu-id="3d038-182">toodo this, run hello following commands from your terminal.</span></span> <span data-ttu-id="3d038-183">Use la información de conexión de hello para la base de datos de Cosmos.</span><span class="sxs-lookup"><span data-stu-id="3d038-183">Use hello connection information for your Cosmos DB.</span></span>

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="3d038-184">Si coloca la configuración en la configuración de la aplicación de Azure mantendrá los datos confidenciales fuera del control de código fuente (Git).</span><span class="sxs-lookup"><span data-stu-id="3d038-184">Putting your settings in Azure app settings keeps sensitive data out of your source control (Git).</span></span> <span data-ttu-id="3d038-185">A continuación, configurará el desarrollo de su entorno toouse Hola la misma información de conexión.</span><span class="sxs-lookup"><span data-stu-id="3d038-185">Next, you will configure your development environment toouse hello same connection information.</span></span>
5. <span data-ttu-id="3d038-186">Abra config/local.js y agregue Hola después el objeto de conexiones:</span><span class="sxs-lookup"><span data-stu-id="3d038-186">Open config/local.js and add hello following connections object:</span></span>

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    <span data-ttu-id="3d038-187">Esta configuración invalida la configuración de hello en el archivo config/connections.js para entorno local de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d038-187">This configuration overrides hello settings in your config/connections.js file for hello local environment.</span></span> <span data-ttu-id="3d038-188">Este archivo está excluido por hello .gitignore de forma predeterminada en el proyecto, por lo que no se almacenarán en Git.</span><span class="sxs-lookup"><span data-stu-id="3d038-188">This file is excluded by hello default .gitignore in your project, so it will not be stored in Git.</span></span> <span data-ttu-id="3d038-189">Ahora, está base de datos de tooconnect puede tooyour Cosmos DB (MongoDB) desde la aplicación web de Azure y de su entorno de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="3d038-189">Now, you are able tooconnect tooyour Cosmos DB (MongoDB) database both from your Azure web app and from your local development environment.</span></span>
6. <span data-ttu-id="3d038-190">Abra config/env/production.js tooconfigure el entorno de producción y agregue Hola siguiente `models` objeto:</span><span class="sxs-lookup"><span data-stu-id="3d038-190">Open config/env/production.js tooconfigure your production environment, and add hello following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. <span data-ttu-id="3d038-191">Abra config/env/development.js tooconfigure el entorno de desarrollo y agregue el siguiente de hello `models` objeto:</span><span class="sxs-lookup"><span data-stu-id="3d038-191">Open config/env/development.js tooconfigure your development environment, and add hello following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    <span data-ttu-id="3d038-192">`migrate: 'alter'`le permite utilizar toocreate de características de migración de base de datos y actualizar fácilmente las colecciones de base de datos o tablas.</span><span class="sxs-lookup"><span data-stu-id="3d038-192">`migrate: 'alter'` lets you use database migration features toocreate and update database collections or tables easily.</span></span> <span data-ttu-id="3d038-193">Sin embargo, `migrate: 'safe'` se usa en su entorno de Azure (producción) porque Sails.js no permite toouse `migrate: 'alter'` en un entorno de producción (consulte [Sails.js documentación](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span><span class="sxs-lookup"><span data-stu-id="3d038-193">However, `migrate: 'safe'` is used for your Azure (production) environment because Sails.js does not allow you toouse `migrate: 'alter'` in a production environment (see [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span></span>
8. <span data-ttu-id="3d038-194">De hello terminal, [generar](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) una Sails.js [plano API](http://sailsjs.org/documentation/concepts/blueprints) como normalmente, a continuación, ejecutaría `sails lift` crear base de datos de hello con la migración de base de datos de Sails.js.</span><span class="sxs-lookup"><span data-stu-id="3d038-194">From hello terminal, [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) a Sails.js [blueprint API](http://sailsjs.org/documentation/concepts/blueprints) like you normally would, then run `sails lift` to create hello database with Sails.js database migration.</span></span> <span data-ttu-id="3d038-195">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3d038-195">For example:</span></span>

         sails generate api mywidget
         sails lift

    <span data-ttu-id="3d038-196">Hola `mywidget` modelo generado por este comando está vacío, pero se puede usar tooshow contamos con conectividad de base de datos.</span><span class="sxs-lookup"><span data-stu-id="3d038-196">hello `mywidget` model generated by this command is empty, but we can use it tooshow that we have database connectivity.</span></span>
    <span data-ttu-id="3d038-197">Al ejecutar `sails lift`, crea colecciones que faltan de Hola y tablas para hello modelos usa su aplicación.</span><span class="sxs-lookup"><span data-stu-id="3d038-197">When you run `sails lift`, it creates hello missing collections and tables for hello models your app uses.</span></span>
9. <span data-ttu-id="3d038-198">Acceso a la API de plano Hola que acaba de crear en el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d038-198">Access hello blueprint API you just created in hello browser.</span></span> <span data-ttu-id="3d038-199">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3d038-199">For example:</span></span>

        http://localhost:1337/mywidget/create

    <span data-ttu-id="3d038-200">Hola API debe devolver tooyou atrás de entrada de hello creado en la ventana del explorador hello, lo que significa que la colección se creó correctamente.</span><span class="sxs-lookup"><span data-stu-id="3d038-200">hello API should return hello created entry back tooyou in hello browser window, which means that your collection is created  successfully.</span></span>

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. <span data-ttu-id="3d038-201">Ahora, su tooAzure cambios de inserción y examinar tooyour aplicación toomake que todavía funciona.</span><span class="sxs-lookup"><span data-stu-id="3d038-201">Now, push your changes tooAzure, and browse tooyour app toomake sure it still works.</span></span>

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. <span data-ttu-id="3d038-202">Hola plano API de acceso de la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="3d038-202">Access hello blueprint API of your Azure web app.</span></span> <span data-ttu-id="3d038-203">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3d038-203">For example:</span></span>

         http://<appname>.azurewebsites.net/mywidget/create

     <span data-ttu-id="3d038-204">Si Hola API devuelve otra entrada nueva, la aplicación web de Azure está hablando de base de datos de tooyour DB Cosmos (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="3d038-204">If hello API returns another new entry, then your Azure web app is talking tooyour Cosmos DB (MongoDB) database.</span></span>

## <a name="more-resources"></a><span data-ttu-id="3d038-205">Más recursos</span><span class="sxs-lookup"><span data-stu-id="3d038-205">More resources</span></span>
* [<span data-ttu-id="3d038-206">Introducción a las aplicaciones web Node.js en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="3d038-206">Get started with Node.js web apps in Azure App Service</span></span>](app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="3d038-207">Uso de módulos Node.js con aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="3d038-207">Using Node.js Modules with Azure applications</span></span>](../nodejs-use-node-modules-azure-apps.md)
