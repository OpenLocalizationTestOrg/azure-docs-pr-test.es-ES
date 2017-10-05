---
title: "Aplicación de API de Node.js en Azure App Service | Microsoft Docs"
description: "Aprenda a crear una API de RESTful de Node.js e implementarla en una aplicación de API en Azure App Service."
services: app-service\api
documentationcenter: node
author: bradygaster
manager: erikre
editor: 
ms.assetid: a820e400-06af-4852-8627-12b3db4a8e70
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: get-started-article
ms.date: 06/13/2017
ms.author: rachelap
ms.openlocfilehash: 806585edd43b9d2d678bfa41523e4d9d40af8cba
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-nodejs-restful-api-and-deploy-it-to-an-api-app-in-azure"></a><span data-ttu-id="a75cc-103">Creación de una API de RESTful de Node.js e implementación en una aplicación de API de Azure</span><span class="sxs-lookup"><span data-stu-id="a75cc-103">Build a Node.js RESTful API and deploy it to an API app in Azure</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="a75cc-104">En este tutorial de inicio rápido se muestra cómo crear una API de REST, escrita con Node.js [Express](http://expressjs.com/), mediante una definición [Swagger](http://swagger.io/) y cómo implementarla como una [aplicación de API](app-service-api-apps-why-best-platform.md) en Azure.</span><span class="sxs-lookup"><span data-stu-id="a75cc-104">This quickstart shows how to create a REST API, written with Node.js [Express](http://expressjs.com/), using a [Swagger](http://swagger.io/) definition and deploying it as an [API app](app-service-api-apps-why-best-platform.md) on Azure.</span></span> <span data-ttu-id="a75cc-105">Creará la aplicación mediante herramientas de línea de comandos, configurará los recursos con la [CLI de Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) e implementará la aplicación mediante Git.</span><span class="sxs-lookup"><span data-stu-id="a75cc-105">You create the app using command-line tools, configure resources with the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and deploy the app using Git.</span></span>  <span data-ttu-id="a75cc-106">Cuando haya terminado, tendrá una API de REST funcional de ejemplo que se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="a75cc-106">When you've finished, you have a working sample REST API running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a75cc-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a75cc-107">Prerequisites</span></span>

* [<span data-ttu-id="a75cc-108">Git</span><span class="sxs-lookup"><span data-stu-id="a75cc-108">Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="a75cc-109">Node.js y NPM</span><span class="sxs-lookup"><span data-stu-id="a75cc-109">Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a75cc-110">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="a75cc-110">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a75cc-111">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="a75cc-111">Run `az --version` to find the version.</span></span> <span data-ttu-id="a75cc-112">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a75cc-112">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-your-environment"></a><span data-ttu-id="a75cc-113">Preparación del entorno</span><span class="sxs-lookup"><span data-stu-id="a75cc-113">Prepare your environment</span></span>

1. <span data-ttu-id="a75cc-114">En una ventana de terminal, ejecute el siguiente comando para clonar el ejemplo en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="a75cc-114">In a terminal window, run the following command to clone the sample to your local machine.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. <span data-ttu-id="a75cc-115">Cambie al directorio que contiene el código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a75cc-115">Change to the directory that contains the sample code.</span></span>

    ```bash
    cd app-service-api-node-contact-list
    ```

3. <span data-ttu-id="a75cc-116">Instalar [Swaggerize](https://www.npmjs.com/package/swaggerize-express) en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="a75cc-116">Install [Swaggerize](https://www.npmjs.com/package/swaggerize-express) on your local machine.</span></span> <span data-ttu-id="a75cc-117">Swaggerize es una herramienta que genera código Node.js para la API de REST desde una definición de Swagger.</span><span class="sxs-lookup"><span data-stu-id="a75cc-117">Swaggerize is a tool that generates Node.js code for your REST API from a Swagger definition.</span></span>

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a><span data-ttu-id="a75cc-118">Generar código Node.js</span><span class="sxs-lookup"><span data-stu-id="a75cc-118">Generate Node.js code</span></span> 

<span data-ttu-id="a75cc-119">En esta sección del tutorial se modela un flujo de trabajo de desarrollo de API en el que primero crea los metadatos de Swagger y los usa para aplicar la técnica scaffolding (generación automática) al código del servidor para la API.</span><span class="sxs-lookup"><span data-stu-id="a75cc-119">This section of the tutorial models an API development workflow in which you create Swagger metadata first and use that to scaffold (auto-generate) server code for the API.</span></span> 

<span data-ttu-id="a75cc-120">Cambie el directorio a la carpeta *inicio* y, a continuación, ejecute `yo swaggerize`.</span><span class="sxs-lookup"><span data-stu-id="a75cc-120">Change directory to the *start* folder, then run `yo swaggerize`.</span></span> <span data-ttu-id="a75cc-121">Swaggerize crea un proyecto de Node.js para la API desde la definición de Swagger en *api.json*.</span><span class="sxs-lookup"><span data-stu-id="a75cc-121">Swaggerize creates a Node.js project for your API from the Swagger definition in *api.json*.</span></span>

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

<span data-ttu-id="a75cc-122">Cuando Swaggerize le solicite un nombre de proyecto, use *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="a75cc-122">When Swaggerize asks for a project name, use *ContactList*.</span></span>
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like to call this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-the-project-code"></a><span data-ttu-id="a75cc-123">Personalizar el código del proyecto</span><span class="sxs-lookup"><span data-stu-id="a75cc-123">Customize the project code</span></span>

1. <span data-ttu-id="a75cc-124">Copie la carpeta *lib* en la carpeta *ContactList* creada por `yo swaggerize` y, a continuación, cambie el directorio a *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="a75cc-124">Copy the *lib* folder into the *ContactList* folder created by `yo swaggerize`, then change directory into *ContactList*.</span></span>

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. <span data-ttu-id="a75cc-125">Instale el `jsonpath` y `swaggerize-ui` los módulos NPM.</span><span class="sxs-lookup"><span data-stu-id="a75cc-125">Install the `jsonpath` and `swaggerize-ui` NPM modules.</span></span> 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. <span data-ttu-id="a75cc-126">Reemplace el código del archivo *handlers/contacts.js* por el siguiente:</span><span class="sxs-lookup"><span data-stu-id="a75cc-126">Replace the code in the *handlers/contacts.js* with the following code:</span></span> 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    <span data-ttu-id="a75cc-127">Este código usa los datos JSON almacenados en *lib/contacts.json* proporcionado por *lib/contactRepository.js*.</span><span class="sxs-lookup"><span data-stu-id="a75cc-127">This code uses the JSON data stored in *lib/contacts.json* served by *lib/contactRepository.js*.</span></span> <span data-ttu-id="a75cc-128">El nuevo código *contacts.js* devuelve todos los contactos en el repositorio como una carga JSON.</span><span class="sxs-lookup"><span data-stu-id="a75cc-128">The new *contacts.js* code returns all contacts in the repository as a JSON payload.</span></span> 

4. <span data-ttu-id="a75cc-129">Reemplace el código del archivo **handlers/contacts/{id}.js** por el siguiente:</span><span class="sxs-lookup"><span data-stu-id="a75cc-129">Replace the code in the **handlers/contacts/{id}.js** file with the following code:</span></span>

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    <span data-ttu-id="a75cc-130">Este código permite usar una variable de ruta de acceso para devolver únicamente el contacto con un identificador especificado.</span><span class="sxs-lookup"><span data-stu-id="a75cc-130">This code lets you use a path variable to return only the contact with a given ID.</span></span>

5. <span data-ttu-id="a75cc-131">Reemplace el código de **server.js** por el siguiente:</span><span class="sxs-lookup"><span data-stu-id="a75cc-131">Replace the code in **server.js** with the following code:</span></span>

    ```javascript
    'use strict';

    var port = process.env.PORT || 8000; 

    var http = require('http');
    var express = require('express');
    var bodyParser = require('body-parser');
    var swaggerize = require('swaggerize-express');
    var swaggerUi = require('swaggerize-ui'); 
    var path = require('path');
    var fs = require("fs");
    
    fs.existsSync = fs.existsSync || require('path').existsSync;

    var app = express();

    var server = http.createServer(app);

    app.use(bodyParser.json());

    app.use(swaggerize({
        api: path.resolve('./config/swagger.json'),
        handlers: path.resolve('./handlers'),
        docspath: '/swagger' 
    }));

    // change four
    app.use('/docs', swaggerUi({
        docs: '/swagger'  
    }));

    server.listen(port, function () { 
    });
    ```   

    <span data-ttu-id="a75cc-132">Este código hace algunos pequeños cambios que le permiten trabajar con Azure App Service y expone una interfaz web interactiva para la API.</span><span class="sxs-lookup"><span data-stu-id="a75cc-132">This code makes some small changes to let it work with Azure App Service and exposes an interactive web interface for your API.</span></span>

### <a name="test-the-api-locally"></a><span data-ttu-id="a75cc-133">Prueba de la API en local</span><span class="sxs-lookup"><span data-stu-id="a75cc-133">Test the API locally</span></span>

1. <span data-ttu-id="a75cc-134">Iniciar la aplicación Node.js</span><span class="sxs-lookup"><span data-stu-id="a75cc-134">Start up the Node.js app</span></span>
    ```bash
    npm start
    ```
    
2. <span data-ttu-id="a75cc-135">Vaya a http://localhost:8000/contacts para ver el archivo JSON de toda la lista de contactos.</span><span class="sxs-lookup"><span data-stu-id="a75cc-135">Browse to http://localhost:8000/contacts to view the JSON for the entire contact list.</span></span>
   
   ```json
    {
        "id": 1,
        "name": "Barney Poland",
        "email": "barney@contoso.com"
    },
    {
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    },
    {
        "id": 3,
        "name": "Lora Riggs",
        "email": "lora@contoso.com"
    }
   ```

3. <span data-ttu-id="a75cc-136">Vaya a http://localhost:8000/contacts/2 para ver el contacto con un `id` de dos.</span><span class="sxs-lookup"><span data-stu-id="a75cc-136">Browse to http://localhost:8000/contacts/2 to view the contact with an `id` of two.</span></span>
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. <span data-ttu-id="a75cc-137">Pruebe la API con la interfaz web de Swagger en http://localhost:8000/docs.</span><span class="sxs-lookup"><span data-stu-id="a75cc-137">Test the API using the Swagger web interface at http://localhost:8000/docs.</span></span>
   
    ![Interfaz web de Swagger](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <span data-ttu-id="a75cc-139"><a id="createapiapp"></a>Crear una aplicación de API</span><span class="sxs-lookup"><span data-stu-id="a75cc-139"><a id="createapiapp"></a> Create an API App</span></span>

<span data-ttu-id="a75cc-140">En esta sección, se usa la CLI de Azure 2.0 para crear los recursos para hospedar la API en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="a75cc-140">In this section, you use the Azure CLI 2.0 to create the resources to host the API on Azure App Service.</span></span> 

1.  <span data-ttu-id="a75cc-141">Inicie sesión en la suscripción de Azure con el comando [az login](/cli/azure/#login) y siga las instrucciones de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="a75cc-141">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

    ```azurecli-interactive
    az login
    ```

2. <span data-ttu-id="a75cc-142">Si tiene varias suscripciones de Azure, cambie la suscripción predeterminada a la que desee.</span><span class="sxs-lookup"><span data-stu-id="a75cc-142">If you have multiple Azure subscriptions, change the default subscription to the desired one.</span></span>

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-the-api-with-git"></a><span data-ttu-id="a75cc-143">Implementación de la API con Git</span><span class="sxs-lookup"><span data-stu-id="a75cc-143">Deploy the API with Git</span></span>

<span data-ttu-id="a75cc-144">Implemente el código en la aplicación de API insertando confirmaciones desde el repositorio de Git local en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="a75cc-144">Deploy your code to the API app by pushing commits from your local Git repository to Azure App Service.</span></span>

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. <span data-ttu-id="a75cc-145">Inicialice un nuevo repositorio en el directorio *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="a75cc-145">Initialize a new repo in the *ContactList* directory.</span></span> 

    ```bash
    git init .
    ```

3. <span data-ttu-id="a75cc-146">Excluya el directorio *node_modules* creado por npm en un paso anterior del tutorial desde Git.</span><span class="sxs-lookup"><span data-stu-id="a75cc-146">Exclude the *node_modules* directory created by npm in an earlier step in the tutorial from Git.</span></span> <span data-ttu-id="a75cc-147">Cree un nuevo archivo `.gitignore` en el directorio actual y agregue el siguiente texto en una nueva línea en cualquier lugar en el archivo.</span><span class="sxs-lookup"><span data-stu-id="a75cc-147">Create a new `.gitignore` file in the current directory and add the following text on a new line anywhere in the file.</span></span>

    ```
    node_modules/
    ```
    <span data-ttu-id="a75cc-148">Confirme que la carpeta `node_modules` está siendo ignorada con `git status`.</span><span class="sxs-lookup"><span data-stu-id="a75cc-148">Confirm the `node_modules` folder is being ignored with  `git status`.</span></span>

4. <span data-ttu-id="a75cc-149">Confirme los cambios en el repositorio.</span><span class="sxs-lookup"><span data-stu-id="a75cc-149">Commit the changes to the repo.</span></span>
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push to Azure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-the-api--in-azure"></a><span data-ttu-id="a75cc-150">Prueba de la API en Azure</span><span class="sxs-lookup"><span data-stu-id="a75cc-150">Test the API  in Azure</span></span>

1. <span data-ttu-id="a75cc-151">Abra un explorador en http://app_name.azurewebsites.net/contacts.</span><span class="sxs-lookup"><span data-stu-id="a75cc-151">Open a browser to http://app_name.azurewebsites.net/contacts.</span></span> <span data-ttu-id="a75cc-152">Verá que devuelve el mismo JSON que cuando se realizó la solicitud localmente anteriormente en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="a75cc-152">You see the same JSON returned as when you made the request locally earlier in the tutorial.</span></span>

   ```json
   {
       "id": 1,
       "name": "Barney Poland",
       "email": "barney@contoso.com"
   },
   {
       "id": 2,
       "name": "Lacy Barrera",
       "email": "lacy@contoso.com"
   },
   {
       "id": 3,
       "name": "Lora Riggs",
       "email": "lora@contoso.com"
   }
   ```

2. <span data-ttu-id="a75cc-153">En un explorador, vaya al punto de conexión `http://app_name.azurewebsites.net/docs` para probar la interfaz de usuario de Swagger ejecutándose en Azure.</span><span class="sxs-lookup"><span data-stu-id="a75cc-153">In a browser, go to the `http://app_name.azurewebsites.net/docs` endpoint to try out the Swagger UI running on Azure.</span></span>

    ![Swagger Ii](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    <span data-ttu-id="a75cc-155">Ahora puede implementar actualizaciones a la API de ejemplo en Azure simplemente enviando confirmaciones al repositorio Git de Azure.</span><span class="sxs-lookup"><span data-stu-id="a75cc-155">You can now deploy updates to the sample API to Azure simply by pushing commits to the Azure Git repository.</span></span>

## <a name="clean-up"></a><span data-ttu-id="a75cc-156">Limpieza</span><span class="sxs-lookup"><span data-stu-id="a75cc-156">Clean up</span></span>

<span data-ttu-id="a75cc-157">Para limpiar los recursos creados en esta guía de inicio rápido, ejecute el siguiente comando de la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="a75cc-157">To clean up the resources created in this quickstart, run the following Azure CLI command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a><span data-ttu-id="a75cc-158">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="a75cc-158">Next step</span></span> 
> [!div class="nextstepaction"]
> [<span data-ttu-id="a75cc-159">Utilizar aplicaciones de API desde clientes JavaScript con CORS</span><span class="sxs-lookup"><span data-stu-id="a75cc-159">Consume API apps from JavaScript clients with CORS</span></span>](app-service-api-cors-consume-javascript.md)

