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
# <a name="build-a-nodejs-restful-api-and-deploy-it-to-an-api-app-in-azure"></a>Creación de una API de RESTful de Node.js e implementación en una aplicación de API de Azure
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

En este tutorial de inicio rápido se muestra cómo crear una API de REST, escrita con Node.js [Express](http://expressjs.com/), mediante una definición [Swagger](http://swagger.io/) y cómo implementarla como una [aplicación de API](app-service-api-apps-why-best-platform.md) en Azure. Creará la aplicación mediante herramientas de línea de comandos, configurará los recursos con la [CLI de Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) e implementará la aplicación mediante Git.  Cuando haya terminado, tendrá una API de REST funcional de ejemplo que se ejecuta en Azure.

## <a name="prerequisites"></a>Requisitos previos

* [Git](https://git-scm.com/)
* [Node.js y NPM](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior. Ejecute `az --version` para encontrar la versión. Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="prepare-your-environment"></a>Preparación del entorno

1. En una ventana de terminal, ejecute el siguiente comando para clonar el ejemplo en el equipo local.

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. Cambie al directorio que contiene el código de ejemplo.

    ```bash
    cd app-service-api-node-contact-list
    ```

3. Instalar [Swaggerize](https://www.npmjs.com/package/swaggerize-express) en el equipo local. Swaggerize es una herramienta que genera código Node.js para la API de REST desde una definición de Swagger.

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a>Generar código Node.js 

En esta sección del tutorial se modela un flujo de trabajo de desarrollo de API en el que primero crea los metadatos de Swagger y los usa para aplicar la técnica scaffolding (generación automática) al código del servidor para la API. 

Cambie el directorio a la carpeta *inicio* y, a continuación, ejecute `yo swaggerize`. Swaggerize crea un proyecto de Node.js para la API desde la definición de Swagger en *api.json*.

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

Cuando Swaggerize le solicite un nombre de proyecto, use *ContactList*.
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like to call this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-the-project-code"></a>Personalizar el código del proyecto

1. Copie la carpeta *lib* en la carpeta *ContactList* creada por `yo swaggerize` y, a continuación, cambie el directorio a *ContactList*.

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. Instale el `jsonpath` y `swaggerize-ui` los módulos NPM. 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. Reemplace el código del archivo *handlers/contacts.js* por el siguiente: 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    Este código usa los datos JSON almacenados en *lib/contacts.json* proporcionado por *lib/contactRepository.js*. El nuevo código *contacts.js* devuelve todos los contactos en el repositorio como una carga JSON. 

4. Reemplace el código del archivo **handlers/contacts/{id}.js** por el siguiente:

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    Este código permite usar una variable de ruta de acceso para devolver únicamente el contacto con un identificador especificado.

5. Reemplace el código de **server.js** por el siguiente:

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

    Este código hace algunos pequeños cambios que le permiten trabajar con Azure App Service y expone una interfaz web interactiva para la API.

### <a name="test-the-api-locally"></a>Prueba de la API en local

1. Iniciar la aplicación Node.js
    ```bash
    npm start
    ```
    
2. Vaya a http://localhost:8000/contacts para ver el archivo JSON de toda la lista de contactos.
   
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

3. Vaya a http://localhost:8000/contacts/2 para ver el contacto con un `id` de dos.
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. Pruebe la API con la interfaz web de Swagger en http://localhost:8000/docs.
   
    ![Interfaz web de Swagger](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <a id="createapiapp"></a>Crear una aplicación de API

En esta sección, se usa la CLI de Azure 2.0 para crear los recursos para hospedar la API en Azure App Service. 

1.  Inicie sesión en la suscripción de Azure con el comando [az login](/cli/azure/#login) y siga las instrucciones de la pantalla.

    ```azurecli-interactive
    az login
    ```

2. Si tiene varias suscripciones de Azure, cambie la suscripción predeterminada a la que desee.

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-the-api-with-git"></a>Implementación de la API con Git

Implemente el código en la aplicación de API insertando confirmaciones desde el repositorio de Git local en Azure App Service.

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. Inicialice un nuevo repositorio en el directorio *ContactList*. 

    ```bash
    git init .
    ```

3. Excluya el directorio *node_modules* creado por npm en un paso anterior del tutorial desde Git. Cree un nuevo archivo `.gitignore` en el directorio actual y agregue el siguiente texto en una nueva línea en cualquier lugar en el archivo.

    ```
    node_modules/
    ```
    Confirme que la carpeta `node_modules` está siendo ignorada con `git status`.

4. Confirme los cambios en el repositorio.
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push to Azure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-the-api--in-azure"></a>Prueba de la API en Azure

1. Abra un explorador en http://app_name.azurewebsites.net/contacts. Verá que devuelve el mismo JSON que cuando se realizó la solicitud localmente anteriormente en el tutorial.

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

2. En un explorador, vaya al punto de conexión `http://app_name.azurewebsites.net/docs` para probar la interfaz de usuario de Swagger ejecutándose en Azure.

    ![Swagger Ii](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    Ahora puede implementar actualizaciones a la API de ejemplo en Azure simplemente enviando confirmaciones al repositorio Git de Azure.

## <a name="clean-up"></a>Limpieza

Para limpiar los recursos creados en esta guía de inicio rápido, ejecute el siguiente comando de la CLI de Azure:

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a>Paso siguiente 
> [!div class="nextstepaction"]
> [Utilizar aplicaciones de API desde clientes JavaScript con CORS](app-service-api-cors-consume-javascript.md)

