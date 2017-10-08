---
title: "aplicación de aaaNode.js API de servicio de aplicaciones de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una API de REST de Node.js e implementarlo tooan API de aplicación de servicio de aplicaciones de Azure."
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
ms.openlocfilehash: 3b3229c1453b6ca4d06bef26f476e92afda4e244
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-restful-api-and-deploy-it-tooan-api-app-in-azure"></a><span data-ttu-id="703a8-103">Generar una API de REST de Node.js e implementarlo tooan API aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="703a8-103">Build a Node.js RESTful API and deploy it tooan API app in Azure</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="703a8-104">Este tutorial rápido muestra cómo toocreate una API de REST, escrita con Node.js [Express](http://expressjs.com/), utilizando un [Swagger](http://swagger.io/) definición e implementarlos como un [aplicación de API](app-service-api-apps-why-best-platform.md) en Azure.</span><span class="sxs-lookup"><span data-stu-id="703a8-104">This quickstart shows how toocreate a REST API, written with Node.js [Express](http://expressjs.com/), using a [Swagger](http://swagger.io/) definition and deploying it as an [API app](app-service-api-apps-why-best-platform.md) on Azure.</span></span> <span data-ttu-id="703a8-105">Crear una aplicación de hello usando herramientas de línea de comandos, configurar los recursos con hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)e implementar la aplicación hello mediante Git.</span><span class="sxs-lookup"><span data-stu-id="703a8-105">You create hello app using command-line tools, configure resources with hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and deploy hello app using Git.</span></span>  <span data-ttu-id="703a8-106">Cuando haya terminado, tendrá una API de REST funcional de ejemplo que se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="703a8-106">When you've finished, you have a working sample REST API running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="703a8-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="703a8-107">Prerequisites</span></span>

* [<span data-ttu-id="703a8-108">Git</span><span class="sxs-lookup"><span data-stu-id="703a8-108">Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="703a8-109">Node.js y NPM</span><span class="sxs-lookup"><span data-stu-id="703a8-109">Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="703a8-110">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="703a8-110">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="703a8-111">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="703a8-111">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="703a8-112">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="703a8-112">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-your-environment"></a><span data-ttu-id="703a8-113">Preparación del entorno</span><span class="sxs-lookup"><span data-stu-id="703a8-113">Prepare your environment</span></span>

1. <span data-ttu-id="703a8-114">En una ventana de terminal, ejecute hello después de la máquina local tooyour del ejemplo de Hola de comando tooclone.</span><span class="sxs-lookup"><span data-stu-id="703a8-114">In a terminal window, run hello following command tooclone hello sample tooyour local machine.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. <span data-ttu-id="703a8-115">Cambie el directorio toohello que contiene código de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="703a8-115">Change toohello directory that contains hello sample code.</span></span>

    ```bash
    cd app-service-api-node-contact-list
    ```

3. <span data-ttu-id="703a8-116">Instalar [Swaggerize](https://www.npmjs.com/package/swaggerize-express) en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="703a8-116">Install [Swaggerize](https://www.npmjs.com/package/swaggerize-express) on your local machine.</span></span> <span data-ttu-id="703a8-117">Swaggerize es una herramienta que genera código Node.js para la API de REST desde una definición de Swagger.</span><span class="sxs-lookup"><span data-stu-id="703a8-117">Swaggerize is a tool that generates Node.js code for your REST API from a Swagger definition.</span></span>

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a><span data-ttu-id="703a8-118">Generar código Node.js</span><span class="sxs-lookup"><span data-stu-id="703a8-118">Generate Node.js code</span></span> 

<span data-ttu-id="703a8-119">Esta sección del tutorial de hello modela un flujo de trabajo de desarrollo API en el que primero crea metadatos de Swagger y usa ese tooscaffold (Autogenerar) código de servidor de API de Hola.</span><span class="sxs-lookup"><span data-stu-id="703a8-119">This section of hello tutorial models an API development workflow in which you create Swagger metadata first and use that tooscaffold (auto-generate) server code for hello API.</span></span> 

<span data-ttu-id="703a8-120">Cambiar directorio toohello *iniciar* carpeta, a continuación, ejecute `yo swaggerize`.</span><span class="sxs-lookup"><span data-stu-id="703a8-120">Change directory toohello *start* folder, then run `yo swaggerize`.</span></span> <span data-ttu-id="703a8-121">Swaggerize crea un proyecto de Node.js de la API de definición de Swagger de hello en *api.json*.</span><span class="sxs-lookup"><span data-stu-id="703a8-121">Swaggerize creates a Node.js project for your API from hello Swagger definition in *api.json*.</span></span>

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

<span data-ttu-id="703a8-122">Cuando Swaggerize le solicite un nombre de proyecto, use *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="703a8-122">When Swaggerize asks for a project name, use *ContactList*.</span></span>
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like toocall this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-hello-project-code"></a><span data-ttu-id="703a8-123">Personalizar el código del proyecto Hola</span><span class="sxs-lookup"><span data-stu-id="703a8-123">Customize hello project code</span></span>

1. <span data-ttu-id="703a8-124">Hola de copia *lib* carpeta en hello *Listadecontactos* carpeta creada por `yo swaggerize`, a continuación, cambie el directorio a *Listadecontactos*.</span><span class="sxs-lookup"><span data-stu-id="703a8-124">Copy hello *lib* folder into hello *ContactList* folder created by `yo swaggerize`, then change directory into *ContactList*.</span></span>

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. <span data-ttu-id="703a8-125">Instalar hello `jsonpath` y `swaggerize-ui` módulos NPM.</span><span class="sxs-lookup"><span data-stu-id="703a8-125">Install hello `jsonpath` and `swaggerize-ui` NPM modules.</span></span> 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. <span data-ttu-id="703a8-126">Reemplace el código de hello en hello *handlers/contacts.js* con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="703a8-126">Replace hello code in hello *handlers/contacts.js* with hello following code:</span></span> 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    <span data-ttu-id="703a8-127">Este código usa los datos JSON Hola almacenados en *lib/contacts.json* atendido por *lib/contactRepository.js*.</span><span class="sxs-lookup"><span data-stu-id="703a8-127">This code uses hello JSON data stored in *lib/contacts.json* served by *lib/contactRepository.js*.</span></span> <span data-ttu-id="703a8-128">Hola nueva *contacts.js* código devuelve todos los contactos en el repositorio de hello como una carga JSON.</span><span class="sxs-lookup"><span data-stu-id="703a8-128">hello new *contacts.js* code returns all contacts in hello repository as a JSON payload.</span></span> 

4. <span data-ttu-id="703a8-129">Reemplace el código de hello en hello **handlers/contacts/{id}.js** archivo con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="703a8-129">Replace hello code in hello **handlers/contacts/{id}.js** file with hello following code:</span></span>

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    <span data-ttu-id="703a8-130">Este código le permite usar un contacto de hello solo tooreturn variable de ruta de acceso con un identificador especificado.</span><span class="sxs-lookup"><span data-stu-id="703a8-130">This code lets you use a path variable tooreturn only hello contact with a given ID.</span></span>

5. <span data-ttu-id="703a8-131">Reemplace el código de hello en **server.js** con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="703a8-131">Replace hello code in **server.js** with hello following code:</span></span>

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

    <span data-ttu-id="703a8-132">Este código hace que algunos toolet pequeños cambios funciona con el servicio de aplicación de Azure y expone una interfaz web interactivas de la API.</span><span class="sxs-lookup"><span data-stu-id="703a8-132">This code makes some small changes toolet it work with Azure App Service and exposes an interactive web interface for your API.</span></span>

### <a name="test-hello-api-locally"></a><span data-ttu-id="703a8-133">Hola API de pruebas localmente</span><span class="sxs-lookup"><span data-stu-id="703a8-133">Test hello API locally</span></span>

1. <span data-ttu-id="703a8-134">Iniciar una aplicación de hello Node.js</span><span class="sxs-lookup"><span data-stu-id="703a8-134">Start up hello Node.js app</span></span>
    ```bash
    npm start
    ```
    
2. <span data-ttu-id="703a8-135">Examinar toohttp://localhost:8000 / tooview Hola JSON se pone en contacto para lista de contactos de hello todo.</span><span class="sxs-lookup"><span data-stu-id="703a8-135">Browse toohttp://localhost:8000/contacts tooview hello JSON for hello entire contact list.</span></span>
   
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

3. <span data-ttu-id="703a8-136">Examinar toohttp://localhost:8000/contactos/2 tooview Hola contacto con un `id` de dos.</span><span class="sxs-lookup"><span data-stu-id="703a8-136">Browse toohttp://localhost:8000/contacts/2 tooview hello contact with an `id` of two.</span></span>
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. <span data-ttu-id="703a8-137">API de Hola de prueba mediante la interfaz web de Swagger de hello en http://localhost: 8000/documentos.</span><span class="sxs-lookup"><span data-stu-id="703a8-137">Test hello API using hello Swagger web interface at http://localhost:8000/docs.</span></span>
   
    ![Interfaz web de Swagger](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <span data-ttu-id="703a8-139"><a id="createapiapp"></a>Crear una aplicación de API</span><span class="sxs-lookup"><span data-stu-id="703a8-139"><a id="createapiapp"></a> Create an API App</span></span>

<span data-ttu-id="703a8-140">En esta sección, use hello Azure CLI 2.0 toocreate Hola recursos toohost Hola API de servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="703a8-140">In this section, you use hello Azure CLI 2.0 toocreate hello resources toohost hello API on Azure App Service.</span></span> 

1.  <span data-ttu-id="703a8-141">Inicie sesión en la suscripción de Azure con hello tooyour [inicio de sesión de az](/cli/azure/#login) comando y siga hello en pantalla instrucciones.</span><span class="sxs-lookup"><span data-stu-id="703a8-141">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

    ```azurecli-interactive
    az login
    ```

2. <span data-ttu-id="703a8-142">Si tiene varias suscripciones de Azure, cambio Hola predeterminado suscripción toohello había deseado uno.</span><span class="sxs-lookup"><span data-stu-id="703a8-142">If you have multiple Azure subscriptions, change hello default subscription toohello desired one.</span></span>

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-hello-api-with-git"></a><span data-ttu-id="703a8-143">Implementar la API de hello con Git</span><span class="sxs-lookup"><span data-stu-id="703a8-143">Deploy hello API with Git</span></span>

<span data-ttu-id="703a8-144">Implementar la aplicación de API de toohello de código mediante la inserción de confirmaciones de su tooAzure de repositorio de Git local servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="703a8-144">Deploy your code toohello API app by pushing commits from your local Git repository tooAzure App Service.</span></span>

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. <span data-ttu-id="703a8-145">Inicializar un nuevo repositorio en hello *Listadecontactos* directory.</span><span class="sxs-lookup"><span data-stu-id="703a8-145">Initialize a new repo in hello *ContactList* directory.</span></span> 

    ```bash
    git init .
    ```

3. <span data-ttu-id="703a8-146">Excluir hello *node_modules* directorio creado por npm en un paso anterior en el tutorial Hola desde Git.</span><span class="sxs-lookup"><span data-stu-id="703a8-146">Exclude hello *node_modules* directory created by npm in an earlier step in hello tutorial from Git.</span></span> <span data-ttu-id="703a8-147">Crear un nuevo `.gitignore` un archivo en el directorio actual de Hola y agregue Hola después de texto en una nueva línea en cualquier lugar en el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="703a8-147">Create a new `.gitignore` file in hello current directory and add hello following text on a new line anywhere in hello file.</span></span>

    ```
    node_modules/
    ```
    <span data-ttu-id="703a8-148">Confirmar hello `node_modules` carpeta omitirá con `git status`.</span><span class="sxs-lookup"><span data-stu-id="703a8-148">Confirm hello `node_modules` folder is being ignored with  `git status`.</span></span>

4. <span data-ttu-id="703a8-149">Confirmar Hola cambios toohello repositorio.</span><span class="sxs-lookup"><span data-stu-id="703a8-149">Commit hello changes toohello repo.</span></span>
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push tooAzure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-hello-api--in-azure"></a><span data-ttu-id="703a8-150">Hola de prueba API en Azure</span><span class="sxs-lookup"><span data-stu-id="703a8-150">Test hello API  in Azure</span></span>

1. <span data-ttu-id="703a8-151">Abra un explorador toohttp://app_name.azurewebsites.net/contacts.</span><span class="sxs-lookup"><span data-stu-id="703a8-151">Open a browser toohttp://app_name.azurewebsites.net/contacts.</span></span> <span data-ttu-id="703a8-152">Vea Hola que JSON mismo formando cuando realiza la solicitud de hello localmente anteriormente en el tutorial de Hola.</span><span class="sxs-lookup"><span data-stu-id="703a8-152">You see hello same JSON returned as when you made hello request locally earlier in hello tutorial.</span></span>

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

2. <span data-ttu-id="703a8-153">En un explorador, vaya toohello `http://app_name.azurewebsites.net/docs` tootry de punto de conexión espera Hola UI Swagger que se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="703a8-153">In a browser, go toohello `http://app_name.azurewebsites.net/docs` endpoint tootry out hello Swagger UI running on Azure.</span></span>

    ![Swagger Ii](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    <span data-ttu-id="703a8-155">Ahora puede implementar actualizaciones toohello ejemplo API tooAzure insertando confirmaciones toohello Azure Git repositorio.</span><span class="sxs-lookup"><span data-stu-id="703a8-155">You can now deploy updates toohello sample API tooAzure simply by pushing commits toohello Azure Git repository.</span></span>

## <a name="clean-up"></a><span data-ttu-id="703a8-156">Limpieza</span><span class="sxs-lookup"><span data-stu-id="703a8-156">Clean up</span></span>

<span data-ttu-id="703a8-157">tooclean los recursos de hello creado en este tutorial rápido, ejecute hello siguiente comando de CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="703a8-157">tooclean up hello resources created in this quickstart, run hello following Azure CLI command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a><span data-ttu-id="703a8-158">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="703a8-158">Next step</span></span> 
> [!div class="nextstepaction"]
> [<span data-ttu-id="703a8-159">Utilizar aplicaciones de API desde clientes JavaScript con CORS</span><span class="sxs-lookup"><span data-stu-id="703a8-159">Consume API apps from JavaScript clients with CORS</span></span>](app-service-api-cors-consume-javascript.md)

