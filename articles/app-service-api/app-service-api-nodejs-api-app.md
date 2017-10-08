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
# <a name="build-a-nodejs-restful-api-and-deploy-it-tooan-api-app-in-azure"></a>Generar una API de REST de Node.js e implementarlo tooan API aplicación en Azure
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

Este tutorial rápido muestra cómo toocreate una API de REST, escrita con Node.js [Express](http://expressjs.com/), utilizando un [Swagger](http://swagger.io/) definición e implementarlos como un [aplicación de API](app-service-api-apps-why-best-platform.md) en Azure. Crear una aplicación de hello usando herramientas de línea de comandos, configurar los recursos con hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)e implementar la aplicación hello mediante Git.  Cuando haya terminado, tendrá una API de REST funcional de ejemplo que se ejecuta en Azure.

## <a name="prerequisites"></a>Requisitos previos

* [Git](https://git-scm.com/)
* [Node.js y NPM](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="prepare-your-environment"></a>Preparación del entorno

1. En una ventana de terminal, ejecute hello después de la máquina local tooyour del ejemplo de Hola de comando tooclone.

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. Cambie el directorio toohello que contiene código de ejemplo de Hola.

    ```bash
    cd app-service-api-node-contact-list
    ```

3. Instalar [Swaggerize](https://www.npmjs.com/package/swaggerize-express) en el equipo local. Swaggerize es una herramienta que genera código Node.js para la API de REST desde una definición de Swagger.

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a>Generar código Node.js 

Esta sección del tutorial de hello modela un flujo de trabajo de desarrollo API en el que primero crea metadatos de Swagger y usa ese tooscaffold (Autogenerar) código de servidor de API de Hola. 

Cambiar directorio toohello *iniciar* carpeta, a continuación, ejecute `yo swaggerize`. Swaggerize crea un proyecto de Node.js de la API de definición de Swagger de hello en *api.json*.

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

Cuando Swaggerize le solicite un nombre de proyecto, use *ContactList*.
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like toocall this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-hello-project-code"></a>Personalizar el código del proyecto Hola

1. Hola de copia *lib* carpeta en hello *Listadecontactos* carpeta creada por `yo swaggerize`, a continuación, cambie el directorio a *Listadecontactos*.

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. Instalar hello `jsonpath` y `swaggerize-ui` módulos NPM. 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. Reemplace el código de hello en hello *handlers/contacts.js* con hello siguiente código: 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    Este código usa los datos JSON Hola almacenados en *lib/contacts.json* atendido por *lib/contactRepository.js*. Hola nueva *contacts.js* código devuelve todos los contactos en el repositorio de hello como una carga JSON. 

4. Reemplace el código de hello en hello **handlers/contacts/{id}.js** archivo con el siguiente código de hello:

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    Este código le permite usar un contacto de hello solo tooreturn variable de ruta de acceso con un identificador especificado.

5. Reemplace el código de hello en **server.js** con hello siguiente código:

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

    Este código hace que algunos toolet pequeños cambios funciona con el servicio de aplicación de Azure y expone una interfaz web interactivas de la API.

### <a name="test-hello-api-locally"></a>Hola API de pruebas localmente

1. Iniciar una aplicación de hello Node.js
    ```bash
    npm start
    ```
    
2. Examinar toohttp://localhost:8000 / tooview Hola JSON se pone en contacto para lista de contactos de hello todo.
   
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

3. Examinar toohttp://localhost:8000/contactos/2 tooview Hola contacto con un `id` de dos.
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. API de Hola de prueba mediante la interfaz web de Swagger de hello en http://localhost: 8000/documentos.
   
    ![Interfaz web de Swagger](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <a id="createapiapp"></a>Crear una aplicación de API

En esta sección, use hello Azure CLI 2.0 toocreate Hola recursos toohost Hola API de servicio de aplicaciones de Azure. 

1.  Inicie sesión en la suscripción de Azure con hello tooyour [inicio de sesión de az](/cli/azure/#login) comando y siga hello en pantalla instrucciones.

    ```azurecli-interactive
    az login
    ```

2. Si tiene varias suscripciones de Azure, cambio Hola predeterminado suscripción toohello había deseado uno.

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-hello-api-with-git"></a>Implementar la API de hello con Git

Implementar la aplicación de API de toohello de código mediante la inserción de confirmaciones de su tooAzure de repositorio de Git local servicio de aplicaciones.

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. Inicializar un nuevo repositorio en hello *Listadecontactos* directory. 

    ```bash
    git init .
    ```

3. Excluir hello *node_modules* directorio creado por npm en un paso anterior en el tutorial Hola desde Git. Crear un nuevo `.gitignore` un archivo en el directorio actual de Hola y agregue Hola después de texto en una nueva línea en cualquier lugar en el archivo hello.

    ```
    node_modules/
    ```
    Confirmar hello `node_modules` carpeta omitirá con `git status`.

4. Confirmar Hola cambios toohello repositorio.
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push tooAzure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-hello-api--in-azure"></a>Hola de prueba API en Azure

1. Abra un explorador toohttp://app_name.azurewebsites.net/contacts. Vea Hola que JSON mismo formando cuando realiza la solicitud de hello localmente anteriormente en el tutorial de Hola.

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

2. En un explorador, vaya toohello `http://app_name.azurewebsites.net/docs` tootry de punto de conexión espera Hola UI Swagger que se ejecuta en Azure.

    ![Swagger Ii](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    Ahora puede implementar actualizaciones toohello ejemplo API tooAzure insertando confirmaciones toohello Azure Git repositorio.

## <a name="clean-up"></a>Limpieza

tooclean los recursos de hello creado en este tutorial rápido, ejecute hello siguiente comando de CLI de Azure:

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a>Paso siguiente 
> [!div class="nextstepaction"]
> [Utilizar aplicaciones de API desde clientes JavaScript con CORS](app-service-api-cors-consume-javascript.md)

