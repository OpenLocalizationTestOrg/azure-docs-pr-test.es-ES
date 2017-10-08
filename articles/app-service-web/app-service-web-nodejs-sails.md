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
# <a name="deploy-a-sailsjs-web-app-tooazure-app-service"></a>Implementar una aplicación de web Sails.js tooAzure servicio de aplicaciones
Este tutorial muestra cómo toodeploy una tooAzure de aplicación de Sails.js servicio de aplicaciones. En el proceso de hello, puede recopilar algunos conocimientos generales sobre cómo tooconfigure su toorun de aplicación Node.js en el servicio de aplicaciones.

En este artículo, adquirirá destrezas útiles, como las siguientes:

* Configurar una aplicación Sails.js que se ejecute en App Service.
* Implementar un tooApp servicio de aplicación de línea de comandos de Hola.
* Stdout y stderr lectura registra tootroubleshoot los problemas de implementación.
* Almacenar las variables de entorno fuera del control de código fuente.
* Acceder a las variables de entorno de Azure desde su aplicación.
* Conectar la base de datos de tooa (MongoDB).

Debe tener conocimientos prácticos de Sails.js. Este tutorial no está previsto toohelp con problemas relacionados con toorunning Sail.js en general.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello

Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

- [Azure 1.0 de CLI](app-service-web-nodejs-sails-cli-nodejs.md) – nuestro CLI para modelos de implementación de administración de recursos y clásico Hola
- [Azure 2.0 CLI](app-service-web-nodejs-sails.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola

## <a name="prerequisites"></a>Requisitos previos
* [Node.js](https://nodejs.org/)
* [Sails.js](http://sailsjs.org/get-started)
* [Git](http://www.git-scm.com/downloads)
* [CLI de Azure 2.0](/cli/azure/install-az-cli2)
* Una cuenta de Microsoft Azure. Si aún no tiene ninguna, puede [registrarse para una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) o [activar las ventajas de suscriptor de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> También puede [probar App Service](https://azure.microsoft.com/try/app-service/) sin una cuenta de Azure. Crear una aplicación de inicio y trabajar con él para la hora de tooan--ninguna tarjeta de crédito necesario, sin compromisos.
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a>Paso 1: Creación y configuración de una aplicación de Sails.js localmente
En primer lugar, cree rápidamente una aplicación Sails.js en su entorno de desarrollo con estos pasos:

1. Terminal de línea de comandos de hello abierto de su elección y `CD` tooa directorio de trabajo.
2. Cree una nueva Sails.js y ejecútela:

        sails new <app_name>
        cd <app_name>
        sails lift

    Asegúrese de que puede navegar por página de inicio predeterminada de toohello en http://localhost:1377.

1. Después, habilite el registro para Azure. En el directorio raíz, cree un archivo denominado `iisnode.yml` y agregue Hola después de dos líneas:

        loggingEnabled: true
        logDirectory: iisnode

    Registro ahora está habilitado para hello [iisnode](https://github.com/tjanczuk/iisnode) que el servicio de aplicaciones de Azure usa toorun Node.js aplicaciones de servidor. 
    Para obtener más información sobre su funcionamiento, consulte [cómo toodebug una Node.js web aplicación de servicio de aplicaciones de Azure](web-sites-nodejs-debug.md).

2. A continuación, configure las variables de entorno de Azure de hello Sails.js aplicación toouse. Abra config/env/production.js tooconfigure el entorno de producción y establezca `port` y `hookTimeout`:

        module.exports = {

            // Use process.env.port toohandle web requests toohello default HTTP port
            port: process.env.port,
            // Increase hooks timout too30 seconds
            // This avoids hello Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    Encontrará documentación sobre estas opciones de configuración en la [documentación de Sails.js](http://sailsjs.org/documentation/reference/configuration/sails-config).

4. Después, codificar hello Node.js versión que desea toouse. En package.json, agregue el siguiente hello `engines` propiedad tooset hello Node.js versión tooone que queremos.

        "engines": {
            "node": "6.9.1"
        },

5. Por último, inicialice un repositorio Git y valide los archivos. En el Hola raíz de la aplicación (donde es package.json), ejecute hello siguientes comandos de Git:

        git init
        git add .
        git commit -m "<your commit message>"

El código está listo toobe implementado. 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a>Paso 2: Creación de una aplicación de Azure e implementación de Sails.js

A continuación, cree Hola recurso del servicio de aplicación en Azure e implemente su tooit de aplicación Sails.js.

1. inicio de sesión tooAzure de este modo:

        az login

    Siga el inicio de sesión de hello toocontinue prompt hello en un explorador con una cuenta de Microsoft que tenga su suscripción de Azure.

3. Establecer usuario de implementación de hello para el servicio de aplicaciones. Posteriormente implementará el código mediante estas credenciales.
   
        az appservice web deployment user set --user-name <username> --password <password>

3. Cree un [grupo de recursos](../azure-resource-manager/resource-group-overview.md) con un nombre. Para este tutorial Node.js, no necesita realmente tooknow qué es.

        az group create --location "<location>" --name my-sailsjs-app-group

    toosee los posibles valores pueden usar para `<location>`, usar hello `az appservice list-locations` comando de CLI.

3. Cree "GRATIS" un [plan de App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) con un nombre. Para este tutorial de node.js, solo es preciso saber que en este plan no se cobrarán las aplicaciones web.

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. Cree una nueva aplicación web con un nombre único en `<app_name>`.

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a>Paso 3: Configuración e implementación de la aplicación Sails.js

1. Configurar implementación de Git local para su nueva aplicación web con hello siguiente comando:

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    Obtendrá una salida JSON como este, lo que significa que está configurado dicho repositorio de Git remoto hello:

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. Agregar dirección URL de Hola Hola JSON como un Git remoto para el repositorio local (llamado `azure` para simplificar el trabajo).

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. Implementar la toohello del código de ejemplo `azure` Git remoto. Cuando se le pida, use las credenciales de implementación de Hola que configuró anteriormente.

        git push azure master

7. Por último, simplemente inicie la aplicación de Azure en vivo en el Explorador de hello:

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    Ahora debería ver Hola la misma página de inicio de Sails.js.

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a>Solución de problemas de la implementación
Si se produce un error en la aplicación Sails.js por algún motivo en el servicio de aplicaciones, encontrar Hola stderr registros toohelp solucionar sus problemas.
Para obtener más información, consulte [cómo toodebug una Node.js web aplicación de servicio de aplicaciones de Azure](web-sites-nodejs-debug.md).
Si la aplicación hello ha iniciado correctamente, registro de hello stdout debe muestran mensajes de bienvenida del familiar:

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

Puede controlar la granularidad de los registros de stdout Hola Hola [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) archivo.

## <a name="connect-tooa-database-in-azure"></a>Conectar tooa base de datos de Azure
base de datos de tooconnect tooa en Azure, se crea la base de datos de Hola de su elección en Azure, por ejemplo, la base de datos de Azure SQL, MySQL, MongoDB, caché de Azure (Redis), etc. y usar Hola correspondiente [adaptador de almacén de datos](https://github.com/balderdashy/sails#compatibility) tooconnect tooit. Hello pasos de esta sección muestran cómo tooconnect tooMongoDB mediante el uso de un [base de datos de Azure Cosmos](../documentdb/documentdb-protocol-mongodb.md) base de datos que puede admitir las conexiones de cliente de MongoDB.

1. [Cree una cuenta de Cosmos DB que admita el protocolo de MongoDB](../documentdb/documentdb-create-mongodb-account.md).
2. [Cree una colección y una base de datos Cosmos DB](../documentdb/documentdb-create-collection.md). Hola nombre de colección de hello no importa, pero necesita Hola nombre de base de datos de hello cuando se conecta desde Sails.js.
3. [Buscar información de conexión de hello para la base de datos de la base de datos de Cosmos](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).
2. Desde el línea de comandos terminal, instalar a adaptador de MongoDB hello:

        npm install sails-mongo --save

3. Abra config/connections.js y agregue Hola conexión objeto toohello lista siguiente:

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
    > Hola `ssl: true` opción es importante porque [lo requiere la base de datos de Cosmos](../cosmos-db/connect-mongodb-account.md#connection-string-requirements). 
    >
    >

4. Para cada variable de entorno (`process.env.*`), deberá tooset en el servicio de aplicaciones. toodo, ejecución Hola siguientes comandos de su terminal. Use la información de conexión de hello para la base de datos de Cosmos.

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    Si coloca la configuración en la configuración de la aplicación de Azure mantendrá los datos confidenciales fuera del control de código fuente (Git). A continuación, configurará el desarrollo de su entorno toouse Hola la misma información de conexión.
5. Abra config/local.js y agregue Hola después el objeto de conexiones:

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    Esta configuración invalida la configuración de hello en el archivo config/connections.js para entorno local de Hola. Este archivo está excluido por hello .gitignore de forma predeterminada en el proyecto, por lo que no se almacenarán en Git. Ahora, está base de datos de tooconnect puede tooyour Cosmos DB (MongoDB) desde la aplicación web de Azure y de su entorno de desarrollo local.
6. Abra config/env/production.js tooconfigure el entorno de producción y agregue Hola siguiente `models` objeto:

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. Abra config/env/development.js tooconfigure el entorno de desarrollo y agregue el siguiente de hello `models` objeto:

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    `migrate: 'alter'`le permite utilizar toocreate de características de migración de base de datos y actualizar fácilmente las colecciones de base de datos o tablas. Sin embargo, `migrate: 'safe'` se usa en su entorno de Azure (producción) porque Sails.js no permite toouse `migrate: 'alter'` en un entorno de producción (consulte [Sails.js documentación](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).
8. De hello terminal, [generar](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) una Sails.js [plano API](http://sailsjs.org/documentation/concepts/blueprints) como normalmente, a continuación, ejecutaría `sails lift` crear base de datos de hello con la migración de base de datos de Sails.js. Por ejemplo:

         sails generate api mywidget
         sails lift

    Hola `mywidget` modelo generado por este comando está vacío, pero se puede usar tooshow contamos con conectividad de base de datos.
    Al ejecutar `sails lift`, crea colecciones que faltan de Hola y tablas para hello modelos usa su aplicación.
9. Acceso a la API de plano Hola que acaba de crear en el Explorador de Hola. Por ejemplo:

        http://localhost:1337/mywidget/create

    Hola API debe devolver tooyou atrás de entrada de hello creado en la ventana del explorador hello, lo que significa que la colección se creó correctamente.

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. Ahora, su tooAzure cambios de inserción y examinar tooyour aplicación toomake que todavía funciona.

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. Hola plano API de acceso de la aplicación web de Azure. Por ejemplo:

         http://<appname>.azurewebsites.net/mywidget/create

     Si Hola API devuelve otra entrada nueva, la aplicación web de Azure está hablando de base de datos de tooyour DB Cosmos (MongoDB).

## <a name="more-resources"></a>Más recursos
* [Introducción a las aplicaciones web Node.js en el Servicio de aplicaciones de Azure](app-service-web-get-started-nodejs.md)
* [Uso de módulos Node.js con aplicaciones de Azure](../nodejs-use-node-modules-azure-apps.md)
