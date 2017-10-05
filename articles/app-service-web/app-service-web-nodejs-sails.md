---
title: "Implementación de una aplicación web Sails.js en Azure App Service | Microsoft Docs"
description: "Obtenga información sobre cómo implementar una aplicación Node.js en el Servicio de aplicaciones de Azure. En este tutorial se muestra cómo implementar una aplicación web Sails.js."
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
ms.openlocfilehash: e36fc5f5273f98c3cca91973db9910f32443ec7c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-a-sailsjs-web-app-to-azure-app-service"></a><span data-ttu-id="5979c-104">Implementación de una aplicación web Sails.js en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="5979c-104">Deploy a Sails.js web app to Azure App Service</span></span>
<span data-ttu-id="5979c-105">En este tutorial se muestra cómo implementar una aplicación Sails.js en el Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="5979c-105">This tutorial shows you how to deploy a Sails.js app to Azure App Service.</span></span> <span data-ttu-id="5979c-106">En el proceso, obtendrá conocimientos generales sobre cómo configurar la aplicación Node.js de modo que se ejecute en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="5979c-106">In the process, you can glean some general knowledge on how to configure your Node.js app to run in App Service.</span></span>

<span data-ttu-id="5979c-107">En este artículo, adquirirá destrezas útiles, como las siguientes:</span><span class="sxs-lookup"><span data-stu-id="5979c-107">Here, you will learn useful skills like:</span></span>

* <span data-ttu-id="5979c-108">Configurar una aplicación Sails.js que se ejecute en App Service.</span><span class="sxs-lookup"><span data-stu-id="5979c-108">Configure a Sails.js app run in App Service.</span></span>
* <span data-ttu-id="5979c-109">Implementar una aplicación en App Service desde la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="5979c-109">Deploy an app to App Service from the command line.</span></span>
* <span data-ttu-id="5979c-110">Lectura de los registros stderr y stdout para solucionar cualquier problema de implementación.</span><span class="sxs-lookup"><span data-stu-id="5979c-110">Read stderr and stdout logs to troubleshoot any deployment issues.</span></span>
* <span data-ttu-id="5979c-111">Almacenar las variables de entorno fuera del control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="5979c-111">Store environment variables outside of source control.</span></span>
* <span data-ttu-id="5979c-112">Acceder a las variables de entorno de Azure desde su aplicación.</span><span class="sxs-lookup"><span data-stu-id="5979c-112">Access Azure environment variables from your app.</span></span>
* <span data-ttu-id="5979c-113">Conectarse a una base de datos (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="5979c-113">Connect to a database (MongoDB).</span></span>

<span data-ttu-id="5979c-114">Debe tener conocimientos prácticos de Sails.js.</span><span class="sxs-lookup"><span data-stu-id="5979c-114">You should have working knowledge of Sails.js.</span></span> <span data-ttu-id="5979c-115">Este tutorial no tiene como objetivo ayudarle con los problemas relacionados con la ejecución de Sail.js en general.</span><span class="sxs-lookup"><span data-stu-id="5979c-115">This tutorial is not intended to help you with issues related to running Sail.js in general.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="5979c-116">Versiones de la CLI para completar la tarea</span><span class="sxs-lookup"><span data-stu-id="5979c-116">CLI versions to complete the task</span></span>

<span data-ttu-id="5979c-117">Puede completar la tarea mediante una de las siguientes versiones de la CLI:</span><span class="sxs-lookup"><span data-stu-id="5979c-117">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="5979c-118">[CLI de Azure 1.0](app-service-web-nodejs-sails-cli-nodejs.md): la CLI para los modelos de implementación clásico y de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5979c-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span>
- <span data-ttu-id="5979c-119">[CLI de Azure 2.0](app-service-web-nodejs-sails.md): la CLI de última generación para el modelo de implementación de administración de recursos</span><span class="sxs-lookup"><span data-stu-id="5979c-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5979c-120">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5979c-120">Prerequisites</span></span>
* [<span data-ttu-id="5979c-121">Node.js</span><span class="sxs-lookup"><span data-stu-id="5979c-121">Node.js</span></span>](https://nodejs.org/)
* [<span data-ttu-id="5979c-122">Sails.js</span><span class="sxs-lookup"><span data-stu-id="5979c-122">Sails.js</span></span>](http://sailsjs.org/get-started)
* [<span data-ttu-id="5979c-123">Git</span><span class="sxs-lookup"><span data-stu-id="5979c-123">Git</span></span>](http://www.git-scm.com/downloads)
* [<span data-ttu-id="5979c-124">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="5979c-124">Azure CLI 2.0</span></span>](/cli/azure/install-az-cli2)
* <span data-ttu-id="5979c-125">Una cuenta de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5979c-125">A Microsoft Azure account.</span></span> <span data-ttu-id="5979c-126">Si aún no tiene ninguna, puede [registrarse para una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) o [activar las ventajas de suscriptor de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="5979c-126">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="5979c-127">También puede [probar App Service](https://azure.microsoft.com/try/app-service/) sin una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="5979c-127">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="5979c-128">Cree una aplicación de inicio y juegue con ella durante una hora como máximo; no se requiere ninguna tarjeta de crédito ni ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="5979c-128">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a><span data-ttu-id="5979c-129">Paso 1: Creación y configuración de una aplicación de Sails.js localmente</span><span class="sxs-lookup"><span data-stu-id="5979c-129">Step 1: Create and configure a Sails.js app locally</span></span>
<span data-ttu-id="5979c-130">En primer lugar, cree rápidamente una aplicación Sails.js en su entorno de desarrollo con estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5979c-130">First, quickly create a default Sails.js app in your development environment by following these steps:</span></span>

1. <span data-ttu-id="5979c-131">Abra el terminal de línea de comandos de su elección y `CD` en un directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="5979c-131">Open the command-line terminal of your choice and `CD` to a working directory.</span></span>
2. <span data-ttu-id="5979c-132">Cree una nueva Sails.js y ejecútela:</span><span class="sxs-lookup"><span data-stu-id="5979c-132">Create a Sails.js app and run it:</span></span>

        sails new <app_name>
        cd <app_name>
        sails lift

    <span data-ttu-id="5979c-133">Asegúrese de que puede navegar a la página principal predeterminada en http://localhost:1377.</span><span class="sxs-lookup"><span data-stu-id="5979c-133">Make sure you can navigate to the default home page at http://localhost:1377.</span></span>

1. <span data-ttu-id="5979c-134">Después, habilite el registro para Azure.</span><span class="sxs-lookup"><span data-stu-id="5979c-134">Next, enable logging for Azure.</span></span> <span data-ttu-id="5979c-135">En el directorio raíz, cree un archivo denominado `iisnode.yml` y agregue las dos líneas siguientes:</span><span class="sxs-lookup"><span data-stu-id="5979c-135">In your root directory, create a file called `iisnode.yml` and add the following two lines:</span></span>

        loggingEnabled: true
        logDirectory: iisnode

    <span data-ttu-id="5979c-136">Ya se ha habilitado el registro para el servidor [iisnode](https://github.com/tjanczuk/iisnode) que Azure App Service utiliza para ejecutar aplicaciones Node.js.</span><span class="sxs-lookup"><span data-stu-id="5979c-136">Logging is now enabled for the [iisnode](https://github.com/tjanczuk/iisnode) server that Azure App Service uses to run Node.js apps.</span></span> 
    <span data-ttu-id="5979c-137">Para obtener más información sobre su funcionamiento, consulte [Cómo depurar una aplicación web de Node.js en Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="5979c-137">For more information on how this works, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

2. <span data-ttu-id="5979c-138">A continuación, configure la aplicación Sails.js para usar las variables de entorno de Azure.</span><span class="sxs-lookup"><span data-stu-id="5979c-138">Next, configure the Sails.js app to use Azure environment variables.</span></span> <span data-ttu-id="5979c-139">Abra config/env/production.js para configurar el entorno de producción y establezca `port` y `hookTimeout`:</span><span class="sxs-lookup"><span data-stu-id="5979c-139">Open config/env/production.js to configure your production environment, and set `port` and `hookTimeout`:</span></span>

        module.exports = {

            // Use process.env.port to handle web requests to the default HTTP port
            port: process.env.port,
            // Increase hooks timout to 30 seconds
            // This avoids the Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    <span data-ttu-id="5979c-140">Encontrará documentación sobre estas opciones de configuración en la [documentación de Sails.js](http://sailsjs.org/documentation/reference/configuration/sails-config).</span><span class="sxs-lookup"><span data-stu-id="5979c-140">You can find documentation for these configuration settings in the  [Sails.js Documentation](http://sailsjs.org/documentation/reference/configuration/sails-config).</span></span>

4. <span data-ttu-id="5979c-141">A continuación, codifique la versión de Node.js que desea utilizar.</span><span class="sxs-lookup"><span data-stu-id="5979c-141">Next, hardcode the Node.js version you want to use.</span></span> <span data-ttu-id="5979c-142">En package.json, agregue la siguiente propiedad `engines` para establecer la versión de Node.js que quiera.</span><span class="sxs-lookup"><span data-stu-id="5979c-142">In package.json, add the following `engines` property to set the Node.js version to one that we want.</span></span>

        "engines": {
            "node": "6.9.1"
        },

5. <span data-ttu-id="5979c-143">Por último, inicialice un repositorio Git y valide los archivos.</span><span class="sxs-lookup"><span data-stu-id="5979c-143">Finally, initialize a Git repository and commit your files.</span></span> <span data-ttu-id="5979c-144">En la raíz de la aplicación (donde está package.json), ejecute los siguientes comandos de Git:</span><span class="sxs-lookup"><span data-stu-id="5979c-144">In the application root (where package.json is), run the following Git commands:</span></span>

        git init
        git add .
        git commit -m "<your commit message>"

<span data-ttu-id="5979c-145">El código está listo para implementarse.</span><span class="sxs-lookup"><span data-stu-id="5979c-145">Your code is ready to be deployed.</span></span> 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a><span data-ttu-id="5979c-146">Paso 2: Creación de una aplicación de Azure e implementación de Sails.js</span><span class="sxs-lookup"><span data-stu-id="5979c-146">Step 2: Create an Azure app and deploy Sails.js</span></span>

<span data-ttu-id="5979c-147">A continuación, cree el recurso de App Service en Azure e implemente en él la aplicación de Sails.js.</span><span class="sxs-lookup"><span data-stu-id="5979c-147">Next, create the App Service resource in Azure and deploy your Sails.js app to it.</span></span>

1. <span data-ttu-id="5979c-148">Inicie sesión en Azure de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="5979c-148">log in to Azure like so:</span></span>

        az login

    <span data-ttu-id="5979c-149">Siga las indicaciones para continuar el inicio de sesión en un explorador con una cuenta de Microsoft que tenga su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="5979c-149">Follow the prompt to continue the login in a browser with a Microsoft account that has your Azure subscription.</span></span>

3. <span data-ttu-id="5979c-150">Establezca el usuario de implementación de App Service.</span><span class="sxs-lookup"><span data-stu-id="5979c-150">Set the deployment user for App Service.</span></span> <span data-ttu-id="5979c-151">Posteriormente implementará el código mediante estas credenciales.</span><span class="sxs-lookup"><span data-stu-id="5979c-151">You will deploy code using these credentials later.</span></span>
   
        az appservice web deployment user set --user-name <username> --password <password>

3. <span data-ttu-id="5979c-152">Cree un [grupo de recursos](../azure-resource-manager/resource-group-overview.md) con un nombre.</span><span class="sxs-lookup"><span data-stu-id="5979c-152">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with a name.</span></span> <span data-ttu-id="5979c-153">Para este tutorial de node.js, no es preciso saber qué es.</span><span class="sxs-lookup"><span data-stu-id="5979c-153">For this Node.js tutorial, you don't really need to know what it is.</span></span>

        az group create --location "<location>" --name my-sailsjs-app-group

    <span data-ttu-id="5979c-154">Para ver los posibles valores que puede usar para `<location>`, use el comando de la CLI `az appservice list-locations`.</span><span class="sxs-lookup"><span data-stu-id="5979c-154">To see what possible values you can use for `<location>`, use the `az appservice list-locations` CLI command.</span></span>

3. <span data-ttu-id="5979c-155">Cree "GRATIS" un [plan de App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) con un nombre.</span><span class="sxs-lookup"><span data-stu-id="5979c-155">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) with a name.</span></span> <span data-ttu-id="5979c-156">Para este tutorial de node.js, solo es preciso saber que en este plan no se cobrarán las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="5979c-156">For this Node.js tutorial, just know that you won't be charged for web apps in this plan.</span></span>

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. <span data-ttu-id="5979c-157">Cree una nueva aplicación web con un nombre único en `<app_name>`.</span><span class="sxs-lookup"><span data-stu-id="5979c-157">Create a new web app with a unique name in `<app_name>`.</span></span>

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a><span data-ttu-id="5979c-158">Paso 3: Configuración e implementación de la aplicación Sails.js</span><span class="sxs-lookup"><span data-stu-id="5979c-158">Step 3: Configure and deploy your Sails.js app</span></span>

1. <span data-ttu-id="5979c-159">Configure la implementación local de Git para la nueva aplicación web con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="5979c-159">Configure local Git deployment for your new web app with the following command:</span></span>

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="5979c-160">Obtendrá una salida JSON como esta, lo que significa que está configurado el repositorio de Git remoto:</span><span class="sxs-lookup"><span data-stu-id="5979c-160">You will get a JSON output like this, which means that the remote Git repository is configured:</span></span>

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. <span data-ttu-id="5979c-161">Agregue la dirección URL en la salida JSON como un repositorio de Git remoto para el repositorio local (llamado `azure` para mayor claridad).</span><span class="sxs-lookup"><span data-stu-id="5979c-161">Add the URL in the JSON as a Git remote for your local repository (called `azure` for simplicity).</span></span>

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. <span data-ttu-id="5979c-162">Implemente el código de ejemplo para el repositorio de Git remoto `azure`.</span><span class="sxs-lookup"><span data-stu-id="5979c-162">Deploy your sample code to the `azure` Git remote.</span></span> <span data-ttu-id="5979c-163">Cuando se le pida, use las credenciales de implementación que configuró anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5979c-163">When prompted, use the deployment credentials you configured earlier.</span></span>

        git push azure master

7. <span data-ttu-id="5979c-164">Por último, inicie la aplicación de Azure activa en el explorador:</span><span class="sxs-lookup"><span data-stu-id="5979c-164">Finally, just launch your live Azure app in the browser:</span></span>

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="5979c-165">Ahora debería ver la misma página principal de Sails.js.</span><span class="sxs-lookup"><span data-stu-id="5979c-165">You should now see the same Sails.js home page.</span></span>

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a><span data-ttu-id="5979c-166">Solución de problemas de la implementación</span><span class="sxs-lookup"><span data-stu-id="5979c-166">Troubleshoot your deployment</span></span>
<span data-ttu-id="5979c-167">Si la aplicación Sails.js produce un error por algún motivo en el Servicio de aplicaciones, busque los registros stderr como ayuda para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="5979c-167">If your Sails.js application fails for some reason in App Service, find the stderr logs to help troubleshoot it.</span></span>
<span data-ttu-id="5979c-168">Para obtener más información, consulte [Cómo depurar una aplicación web de Node.js en Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="5979c-168">For more information, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>
<span data-ttu-id="5979c-169">Si la aplicación se ha iniciado correctamente, el registro stdout debería mostrar este mensaje conocido:</span><span class="sxs-lookup"><span data-stu-id="5979c-169">If the app has started successfully, the stdout log should show you the familiar message:</span></span>

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
    To see your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    To shut down Sails, press <CTRL> + C at any time.

<span data-ttu-id="5979c-170">Puede controlar la granularidad de los registros de stdout en el archivo [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) .</span><span class="sxs-lookup"><span data-stu-id="5979c-170">You can control granularity of the stdout logs in the [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span></span>

## <a name="connect-to-a-database-in-azure"></a><span data-ttu-id="5979c-171">Conexión a una base de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="5979c-171">Connect to a database in Azure</span></span>
<span data-ttu-id="5979c-172">Para conectarse a una base de datos de Azure, debe crear una base de datos de su elección en Azure, como Azure SQL Database, MySQL, MongoDB, Azure Redis Cache, etc., y usar el [adaptador de almacén de datos](https://github.com/balderdashy/sails#compatibility) correspondiente para conectarse a ella.</span><span class="sxs-lookup"><span data-stu-id="5979c-172">To connect to a database in Azure, you create the database of your choice in Azure, such as Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache, etc., and use the corresponding [datastore adapter](https://github.com/balderdashy/sails#compatibility) to connect to it.</span></span> <span data-ttu-id="5979c-173">En los pasos de esta sección, se indica cómo conectarse a MongoDB mediante una base de datos [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md), que puede admitir conexiones de cliente de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5979c-173">The steps in this section show you how to connect to MongoDB by using an [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, which can support MongoDB client connections.</span></span>

1. <span data-ttu-id="5979c-174">[Cree una cuenta de Cosmos DB que admita el protocolo de MongoDB](../documentdb/documentdb-create-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="5979c-174">[Create a Cosmos DB account with MongoDB protocol support](../documentdb/documentdb-create-mongodb-account.md).</span></span>
2. <span data-ttu-id="5979c-175">[Cree una colección y una base de datos Cosmos DB](../documentdb/documentdb-create-collection.md).</span><span class="sxs-lookup"><span data-stu-id="5979c-175">[Create a Cosmos DB collection and database](../documentdb/documentdb-create-collection.md).</span></span> <span data-ttu-id="5979c-176">El nombre de la colección es irrelevante, pero necesita el nombre de la base de datos al conectase desde Sails.js.</span><span class="sxs-lookup"><span data-stu-id="5979c-176">The name of the collection doesn't matter, but you need the name of the database when you connect from Sails.js.</span></span>
3. <span data-ttu-id="5979c-177">[Busque la información de conexión para la base de datos Cosmos DB](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="5979c-177">[Find the connection information for your Cosmos DB database](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span></span>
2. <span data-ttu-id="5979c-178">Desde el terminal de línea de comandos, instale el adaptador de MongoDB:</span><span class="sxs-lookup"><span data-stu-id="5979c-178">From your command-line terminal, install the MongoDB adapter:</span></span>

        npm install sails-mongo --save

3. <span data-ttu-id="5979c-179">Abra config/connections.js y agregue el siguiente objeto de conexión a la lista:</span><span class="sxs-lookup"><span data-stu-id="5979c-179">Open config/connections.js and add the following connection object to the list:</span></span>

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
    > <span data-ttu-id="5979c-180">La opción `ssl: true` es importante porque [Cosmos DB la necesita](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="5979c-180">The `ssl: true` option is important because [Cosmos DB requires it](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 
    >
    >

4. <span data-ttu-id="5979c-181">Para cada variable de entorno (`process.env.*`), debe establecerlo en App Service.</span><span class="sxs-lookup"><span data-stu-id="5979c-181">For each environment variable (`process.env.*`), you need to set it in App Service.</span></span> <span data-ttu-id="5979c-182">Para ello, ejecute los comandos siguientes desde su terminal:</span><span class="sxs-lookup"><span data-stu-id="5979c-182">To do this, run the following commands from your terminal.</span></span> <span data-ttu-id="5979c-183">Use la información de conexión para la base de datos Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5979c-183">Use the connection information for your Cosmos DB.</span></span>

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="5979c-184">Si coloca la configuración en la configuración de la aplicación de Azure mantendrá los datos confidenciales fuera del control de código fuente (Git).</span><span class="sxs-lookup"><span data-stu-id="5979c-184">Putting your settings in Azure app settings keeps sensitive data out of your source control (Git).</span></span> <span data-ttu-id="5979c-185">A continuación, configurará el entorno de desarrollo para que utilice la misma información de conexión.</span><span class="sxs-lookup"><span data-stu-id="5979c-185">Next, you will configure your development environment to use the same connection information.</span></span>
5. <span data-ttu-id="5979c-186">Abra config/local.js y agregue el siguiente objeto de conexiones:</span><span class="sxs-lookup"><span data-stu-id="5979c-186">Open config/local.js and add the following connections object:</span></span>

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    <span data-ttu-id="5979c-187">Esta configuración invalida la configuración del archivo config/connections.js para el entorno local.</span><span class="sxs-lookup"><span data-stu-id="5979c-187">This configuration overrides the settings in your config/connections.js file for the local environment.</span></span> <span data-ttu-id="5979c-188">El archivo .gitignore predeterminado del proyecto excluirá este archivo, por lo que no se almacenará en Git.</span><span class="sxs-lookup"><span data-stu-id="5979c-188">This file is excluded by the default .gitignore in your project, so it will not be stored in Git.</span></span> <span data-ttu-id="5979c-189">Ahora, ya puede conectarse a la base de datos Cosmos DB (MongoDB) desde la aplicación web de Azure y el entorno de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="5979c-189">Now, you are able to connect to your Cosmos DB (MongoDB) database both from your Azure web app and from your local development environment.</span></span>
6. <span data-ttu-id="5979c-190">Abra config/env/production.js para configurar el entorno de producción y agregue el siguiente objeto `models` :</span><span class="sxs-lookup"><span data-stu-id="5979c-190">Open config/env/production.js to configure your production environment, and add the following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. <span data-ttu-id="5979c-191">Abra config/env/development.js para configurar el entorno de desarrollo y agregue el siguiente objeto `models` :</span><span class="sxs-lookup"><span data-stu-id="5979c-191">Open config/env/development.js to configure your development environment, and add the following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    <span data-ttu-id="5979c-192">`migrate: 'alter'` permite usar las características de migración de base de datos para crear y actualizar fácilmente las tablas o colecciones de base de datos.</span><span class="sxs-lookup"><span data-stu-id="5979c-192">`migrate: 'alter'` lets you use database migration features to create and update database collections or tables easily.</span></span> <span data-ttu-id="5979c-193">Sin embargo, `migrate: 'safe'` se usa para el entorno de Azure (producción) porque Sails.js no permite utilizar `migrate: 'alter'` en un entorno de producción (consulte la [ documentación de Sails.js](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span><span class="sxs-lookup"><span data-stu-id="5979c-193">However, `migrate: 'safe'` is used for your Azure (production) environment because Sails.js does not allow you to use `migrate: 'alter'` in a production environment (see [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span></span>
8. <span data-ttu-id="5979c-194">Desde el terminal, [genere](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) una [API de proyecto](http://sailsjs.org/documentation/concepts/blueprints) de Sails.js como lo haría normalmente y, después, ejecute `sails lift` para crear la base de datos con la migración de la base de datos de Sails.js.</span><span class="sxs-lookup"><span data-stu-id="5979c-194">From the terminal, [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) a Sails.js [blueprint API](http://sailsjs.org/documentation/concepts/blueprints) like you normally would, then run `sails lift` to create the database with Sails.js database migration.</span></span> <span data-ttu-id="5979c-195">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5979c-195">For example:</span></span>

         sails generate api mywidget
         sails lift

    <span data-ttu-id="5979c-196">El modelo `mywidget` generado por este comando está vacío, pero se puede usar para mostrar que tenemos conectividad de base de datos.</span><span class="sxs-lookup"><span data-stu-id="5979c-196">The `mywidget` model generated by this command is empty, but we can use it to show that we have database connectivity.</span></span>
    <span data-ttu-id="5979c-197">Al ejecutar `sails lift`, crea las tablas y colecciones que faltan para los modelos que usa la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5979c-197">When you run `sails lift`, it creates the missing collections and tables for the models your app uses.</span></span>
9. <span data-ttu-id="5979c-198">Acceda a la API de proyecto que acaba de crear en el explorador.</span><span class="sxs-lookup"><span data-stu-id="5979c-198">Access the blueprint API you just created in the browser.</span></span> <span data-ttu-id="5979c-199">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5979c-199">For example:</span></span>

        http://localhost:1337/mywidget/create

    <span data-ttu-id="5979c-200">La API debe devolver la entrada creada en la ventana del explorador, lo que significa que la colección se ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="5979c-200">The API should return the created entry back to you in the browser window, which means that your collection is created  successfully.</span></span>

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. <span data-ttu-id="5979c-201">Ahora, inserte los cambios en Azure y vaya a la aplicación para asegurarse de que sigue funcionando.</span><span class="sxs-lookup"><span data-stu-id="5979c-201">Now, push your changes to Azure, and browse to your app to make sure it still works.</span></span>

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. <span data-ttu-id="5979c-202">Acceda a la API de proyecto de la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="5979c-202">Access the blueprint API of your Azure web app.</span></span> <span data-ttu-id="5979c-203">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5979c-203">For example:</span></span>

         http://<appname>.azurewebsites.net/mywidget/create

     <span data-ttu-id="5979c-204">Si la API devuelve otra entrada nueva, significa que la aplicación web de Azure está comunicándose con la base de datos Cosmos DB (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="5979c-204">If the API returns another new entry, then your Azure web app is talking to your Cosmos DB (MongoDB) database.</span></span>

## <a name="more-resources"></a><span data-ttu-id="5979c-205">Más recursos</span><span class="sxs-lookup"><span data-stu-id="5979c-205">More resources</span></span>
* [<span data-ttu-id="5979c-206">Introducción a las aplicaciones web Node.js en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="5979c-206">Get started with Node.js web apps in Azure App Service</span></span>](app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="5979c-207">Uso de módulos Node.js con aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="5979c-207">Using Node.js Modules with Azure applications</span></span>](../nodejs-use-node-modules-azure-apps.md)
