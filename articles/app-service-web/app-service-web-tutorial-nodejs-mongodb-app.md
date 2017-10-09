---
title: "aaaBuild una aplicación web de Node.js y MongoDB en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooget una aplicación Node.js trabajando en Azure, con conexión tooa Cosmos base de datos de base de datos con una cadena de conexión de MongoDB."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 0b4d7d0e-e984-49a1-a57a-3c0caa955f0e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 532251c51ed6f8513e6e366393e889b67a85e5b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a>Compilación de una aplicación web Node.js y MongoDB en Azure

Azure Web Apps proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático. Este tutorial muestra cómo toocreate una Node.js web de aplicación en Azure y conectar tooa base de datos de MongoDB. Cuando haya terminado, tendrá una aplicación MEAN (MongoDB, Express, AngularJS y Node.js) que se ejecuta en [Azure App Service](app-service-web-overview.md). Por simplicidad, la aplicación de ejemplo de Hola utiliza hello [el marco de trabajo de MEAN.js web](http://meanjs.org/).

![Aplicación MEAN.js que se ejecuta en Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

Temas que se abordarán:

> [!div class="checklist"]
> * Crear una base de datos MongoDB en Azure
> * Conectar un tooMongoDB de aplicación Node.js
> * Implementar Hola aplicación tooAzure
> * Actualizar el modelo de datos de Hola y volver a implementar la aplicación hello
> * Transmitir registros de diagnóstico desde Azure
> * Administrar aplicación Hola Hola portal de Azure

## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial:

1. [Instalación de Git](https://git-scm.com/)
1. [Instalación de Node.js y NPM](https://nodejs.org/)
1. [Instale Gulp.js](http://gulpjs.com/) (necesario para [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))
1. [Descarga y ejecución de MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="test-local-mongodb"></a>Prueba de la base de datos MongoDB local

Ventana de terminal de hello abierto y `cd` toohello `bin` directorio de la instalación de MongoDB. Puede utilizar esta ventana de terminal toorun todos los comandos de hello en este tutorial.

Ejecute `mongo` en el servidor local de MongoDB de hello tooconnect terminal tooyour.

```bash
mongo
```

Si la conexión se realiza correctamente, la base de datos de MongoDB estará ya funcionando. Si no es así, asegúrese de que se ha iniciado la base de datos local de MongoDB siguiendo los pasos de hello en [instalar MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/). A menudo, MongoDB está instalado, pero seguirá necesitando toostart ejecutar `mongod`. 

Cuando haya terminado pruebas de la base de datos de MongoDB, escriba `Ctrl+C` Hola terminal. 

## <a name="create-local-nodejs-app"></a>Creación de una aplicación local Node.js

En este paso, configurar un proyecto Node.js Hola local.

### <a name="clone-hello-sample-application"></a>Clonar aplicación de ejemplo de Hola

En la ventana de terminal de hello, `cd` tooa directorio de trabajo.  

Ejecute hello después de repositorio de ejemplo de comando tooclone Hola. 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

Este repositorio de ejemplo contiene una copia del programa Hola a [MEAN.js repositorio](https://github.com/meanjs/mean). Es toorun modificado en el servicio de aplicaciones (para obtener más información, vea el repositorio de hello MEAN.js [archivo Léame](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).

### <a name="run-hello-application"></a>Ejecutar la aplicación hello

Ejecute hello siguientes comandos tooinstall Hola necesario paquetes e inicie la aplicación hello.

```bash
cd meanjs
npm install
npm start
```

Cuando se ha cargado completamente la aplicación hello, verá algo similar toohello siguiente mensaje:

```
--
MEAN.JS - Development Environment

Environment:     development
Server:          http://0.0.0.0:3000
Database:        mongodb://localhost/mean-dev
App version:     0.5.0
MEAN.JS version: 0.5.0
--
```

Navegue toohttp://localhost:3000 en un explorador. Haga clic en **Sign Up** sesión Hola menú superior y cree un usuario de prueba. 

Hola MEAN.js aplicación de ejemplo almacena los datos de usuario de base de datos de Hola. Si es correcta en la creación de un usuario y la firma, la aplicación está escribiendo la base de datos de MongoDB local de datos toohello.

![MEAN.js se conecta correctamente tooMongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

Seleccione **Administración > Administrar artículos** tooadd algunos artículos.

toostop Node.js en cualquier momento, presione `Ctrl+C` Hola terminal. 

## <a name="create-production-mongodb"></a>Creación de una base de datos de MongoDB de producción

En este paso, creará una base de datos MongoDB en Azure. Cuando la aplicación esté implementada tooAzure, utiliza esta base de datos en la nube.

Para MongoDB, en este tutorial se usa [Azure Cosmos DB](/azure/documentdb/). Cosmos DB admite las conexiones del cliente de MongoDB.

### <a name="log-in-tooazure"></a>Inicie sesión en tooAzure

Hola CLI de Azure 2.0 toocreate Hola recursos necesarios toohost deberá usar la aplicación en Azure. Inicie sesión en la suscripción de Azure con hello tooyour [inicio de sesión de az](/cli/azure/#login) comando y siga hello en pantalla instrucciones.

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a>Crear un grupo de recursos

Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

Hello en el ejemplo siguiente se crea un grupo de recursos en la región de Europa occidental Hola.

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

Hola de uso [az de servicio de aplicaciones enumerar ubicaciones](/cli/azure/appservice#list-locations) ubicaciones disponibles toolist de comandos de CLI de Azure. 

### <a name="create-a-cosmos-db-account"></a>Creación de una cuenta de Cosmos DB

Cree una cuenta de base de datos de Cosmos con hello [crear az cosmosdb](/cli/azure/cosmosdb#create) comando.

En hello siguiente comando, sustitúyalo por un nombre único de la base de datos de Cosmos para hello  *\<cosmosdb_name >* marcador de posición. Este nombre se usa como parte de Hola de punto de conexión de base de datos de Cosmos hello, `https://<cosmosdb_name>.documents.azure.com/`, por lo que el nombre de Hola necesita toobe único a través de todas las cuentas de base de datos de Cosmos en Azure. Hola nombre debe contener solo letras minúsculas, números y caracteres de guión (-) de Hola y debe estar comprendido entre 3 y 50 caracteres.

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

Hola *--MongoDB kind* parámetro habilita las conexiones de cliente de MongoDB.

Cuando se crea la cuenta de base de datos de Cosmos hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:

```json
{
  "consistencyPolicy":
  {
    "defaultConsistencyLevel": "Session",
    "maxIntervalInSeconds": 5,
    "maxStalenessPrefix": 100
  },
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb_name>.documents.azure.com:443/",
  "failoverPolicies": 
  ...
  < Output truncated for readability >
}
```

## <a name="connect-app-tooproduction-mongodb"></a>Conectar aplicaciones tooproduction MongoDB

En este paso, se conectará la MEAN.js ejemplo toohello Cosmos DB base de datos que acaba de crear, mediante una cadena de conexión de MongoDB. 

### <a name="retrieve-hello-database-key"></a>Recuperar la clave de la base de datos de Hola

base de datos de la base de datos de Cosmos del toohello de tooconnect, se necesita la clave de base de datos de Hola. Hola de uso [az cosmosdb lista-claves](/cli/azure/cosmosdb#list-keys) clave principal de comando tooretrieve Hola.

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

Hola CLI de Azure muestra información toohello similar siguiente ejemplo:

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Copiar valor de Hola de `primaryMasterKey`. Necesitará esta información en el paso siguiente de saludo.

<a name="devconfig"></a>
### <a name="configure-hello-connection-string-in-your-nodejs-application"></a>Configurar la cadena de conexión de hello en la aplicación de Node.js

En el repositorio MEAN.js, abra _config/env/production.js_.

Hola `db` objeto, actualice el valor de Hola de `uri`:

* Reemplace Hola dos  *\<cosmosdb_name >* marcadores de posición con el nombre de base de datos de la base de datos de Cosmos.
* Reemplace hello  *\<primary_master_key >* marcador de posición con clave de Hola que copió en el paso anterior de Hola.

Hello código siguiente muestra hello `db` objeto:

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

Hola `ssl=true` opción es necesaria porque [Cosmos DB requiere SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements). 

Guarde los cambios.

### <a name="test-hello-application-in-production-mode"></a>Probar la aplicación hello en modo de producción 

Ejecute hello después comando toominify y agrupación de las secuencias de comandos para el entorno de producción de hello. Este proceso genera archivos de hello necesarios para el entorno de producción de hello.

```bash
gulp prod
```

Hola ejecución después de que configuró en la cadena de conexión comando toouse hello _config/env/production.js_.

```bash
NODE_ENV=production node server.js
```

`NODE_ENV=production`establece la variable de entorno de Hola que dice toorun Node.js en el entorno de producción de hello.  `node server.js`inicia Hola servidor Node.js con `server.js` en la raíz del repositorio. Así es como se carga la aplicación de Node.js en Azure. 

Cuando se carga la aplicación hello, compruebe que está ejecutando en el entorno de producción de hello toomake:

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

Navegue toohttp://localhost:8443 en un explorador. Haga clic en **Sign Up** sesión Hola menú superior y cree un usuario de prueba. Si está creando un usuario correctas e iniciar sesión en, la aplicación está escribiendo datos de base de datos de Cosmos toohello en Azure. 

Hola terminal, detenga Node.js escribiendo `Ctrl+C`. 

## <a name="deploy-app-tooazure"></a>Implementar la aplicación tooAzure

En este paso, implementará la tooAzure de aplicación conectada a MongoDB Node.js servicio de aplicaciones.

### <a name="create-an-app-service-plan"></a>Creación de un plan de App Service

Crear un plan de servicio de aplicaciones con hello [Crear plan de servicio de aplicaciones az](/cli/azure/appservice/plan#create) comando. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Hello en el ejemplo siguiente se crea un plan de servicio de aplicaciones denominado _myAppServicePlan_ con hello **libre** nivel de precios:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

Cuando se crea el plan de servicio de aplicación Hola, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:

```json 
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
```

### <a name="create-a-web-app"></a>Creación de una aplicación web

Crear una aplicación web en hello `myAppServicePlan` plan de servicio de aplicaciones con hello [crear webapp az](/cli/azure/webapp#create) comando. 

Hola web aplicación le ofrece un hospedaje espacio toodeploy el código y proporciona una dirección URL de hello tooview implementado la aplicación. Aplicación web de uso toocreate Hola. 

Hola el siguiente comando, reemplace hello  *\<app_name >* marcador de posición con un nombre de aplicación único. Este nombre se usa como parte de Hola de dirección URL de hello predeterminado para la aplicación web de hello, por lo que el nombre de hello necesita toobe único en todas las aplicaciones de servicio de aplicaciones de Azure. 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Cuando se ha creado la aplicación web de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo: 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-an-environment-variable"></a>Configuración de una variable de entorno

Anteriormente en hello tutorial, se codificado de forma rígida Hola base de datos cadena de conexión en _config/env/production.js_. De acuerdo con el procedimiento recomendado de seguridad, se desean obtener tookeep estos datos confidenciales de su repositorio de Git. Para la aplicación que se ejecuta en Azure, usará una variable de entorno en su lugar.

En el servicio de aplicación, establecer variables de entorno como _configuración de la aplicación_ mediante el uso de hello [actualizar az webapp configuración appsettings](/cli/azure/webapp/config/appsettings#update) comando. 

Hello ejemplo siguiente se configura un `MONGODB_URI` configuración de la aplicación en la aplicación web de Azure. Reemplace hello  *\<app_name >*,  *\<cosmosdb_name >*, y  *\<primary_master_key >* marcadores de posición.

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

En el código de Node.js, accederá a este valor de aplicación con `process.env.MONGODB_URI`, al igual que accedería a cualquier variable de entorno. 

Ahora, deshacer los cambios too_config/env/production.js_ con hello siguiente comando:

```bash
git checkout -- .
```

Vuelva a abrir _config/env/production.js_. Tenga en cuenta esa aplicación de MEAN.js hello predeterminada ya está configurado toouse Hola `MONGODB_URI` variable de entorno que creó.

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a>Configuración de la implementación de Git local 

Hola de uso [conjunto de usuarios de implementación de aplicación Web de az](/cli/azure/webapp/deployment/user#set) toocreate credenciales para la implementación de comandos.

Puede implementar su aplicación tooAzure servicio de aplicaciones de varias maneras, como FTP, Git local, GitHub, Visual Studio Team Services y BitBucket. Para FTP y Git local, es necesario toohave un usuario de implementación configurada en hello server tooauthenticate la implementación. Dicho usuario es el nivel de cuenta y no es la cuenta de la suscripción de Azure. Solo necesita tooconfigure este usuario de implementación una vez.

Hola siguiente comando, reemplace  *\<nombre de usuario >* y  *\<contraseña >* con un nuevo nombre de usuario y una contraseña. nombre de usuario de Hello debe ser único. Hello contraseña debe tener al menos ocho caracteres, con dos Hola después de tres elementos: letras, números y símbolos. Si se produce un ` 'Conflict'. Details: 409` error, el nombre de usuario de cambio Hola. Si se produce un error ` 'Bad Request'. Details: 400`, use una contraseña más segura.

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

Nombre de usuario de registro hello y una contraseña para su uso en pasos posteriores al implementar la aplicación hello.

Hola de uso [origen de implementación de aplicación Web en az config-local-git](/cli/azure/webapp/deployment/source#config-local-git) comando tooconfigure Git acceso toohello Azure la aplicación web local. 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

Cuando se configura el usuario de la implementación de hello, Hola CLI de Azure muestra hello de dirección URL de implementación para la aplicación web de Azure en hello siguiendo el formato:

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

Copie Hola de salida de terminal de hello, ya que se usará en el paso siguiente de Hola. 

### <a name="push-tooazure-from-git"></a>TooAzure de inserción de Git

Agregue un repositorio de Git local de Azure tooyour remoto. 

```bash
git remote add azure <paste_copied_url_here> 
```

Insertar toohello Azure toodeploy remoto aplicaciones Node.js. Se le pedirá para contraseña de Hola que proporcionó anteriormente como parte de la creación de hello de usuario de implementación de Hola. 

```bash
git push azure master
```

Durante la implementación, Azure App Service comunicará su progreso con Git.

```bash
Counting objects: 5, done.
Delta compression using up too4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 489 bytes | 0 bytes/s, done.
Total 5 (delta 3), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '6c7c716eee'.
remote: Running custom deployment command...
remote: Running deployment command...
remote: Handling node.js deployment.
.
.
.
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

Puede observar que se ejecuta el proceso de implementación de hello [Gulp](http://gulpjs.com/) después `npm install`. Servicio de aplicaciones ejecutan tareas Gulp o Grunt durante la implementación, por lo que este repositorio de ejemplo tiene dos adicionales archivos en su tooenable del directorio raíz que: 

- _implementación_ -este archivo indica toorun de servicio de aplicaciones `bash deploy.sh` como script de implementación personalizada de Hola.
- _Deploy.sh_ -Hola script de implementación personalizado. Si examina el archivo hello, verá que se ejecuta `gulp prod` después `npm install` y `bower install`. 

Puede usar este enfoque tooadd cualquier tooyour paso implementación basada en Git. Si reinicia la aplicación web de Azure en cualquier momento, App Service no vuelve a ejecutar estas tareas de automatización.

### <a name="browse-toohello-azure-web-app"></a>Examinar la aplicación web de Azure de toohello 

Examinar toohello implementa la aplicación web mediante el explorador web. 

```bash 
http://<app_name>.azurewebsites.net 
``` 

Haga clic en **Sign Up** sesión Hola menú superior y cree un usuario ficticio. 

Si es correcta y la aplicación hello inicia sesión automáticamente en toohello crea el usuario y, a continuación, la aplicación MEAN.js en Azure tiene base de datos de conectividad toohello MongoDB (Cosmos DB). 

![Aplicación MEAN.js que se ejecuta en Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

Seleccione **Administración > Administrar artículos** tooadd algunos artículos. 

**¡Enhorabuena!** Está ejecutando una aplicación Node.js orientada a datos en Azure App Service.

## <a name="update-data-model-and-redeploy"></a>Actualización del modelo de datos y nueva implementación

En este paso, cambiar hello `article` datos de modelo y publicar su tooAzure de cambio.

### <a name="update-hello-data-model"></a>Modelo de datos de actualización Hola

Abra _modules/articles/server/models/article.server.model.js_.

En `ArticleSchema`, agregue un tipo `String` llamado `comment`. Cuando haya finalizado, su código de esquema tendrá este aspecto:

```javascript
var ArticleSchema = new Schema({
  ...,
  user: {
    type: Schema.ObjectId,
    ref: 'User'
  },
  comment: {
    type: String,
    default: '',
    trim: true
  }
});
```

### <a name="update-hello-articles-code"></a>Actualizar código de hello artículos

Actualizar el resto de Hola de su `articles` código toouse `comment`.

Hay cinco archivos que necesita toomodify: controlador de servidor de Hola y vistas de cliente de hello cuatro. 

Abra _modules/articles/server/controllers/articles.server.controller.js_.

Hola `update` funcione, agregue una asignación de `article.comment`. Hello código siguiente muestra hello completado `update` función:

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

Abra _modules/articles/client/views/view-article.client.view.html_.

Justo encima de cierre de hello `</section>` etiqueta, agregue Hola después línea toodisplay `comment` junto con el resto de Hola de datos del artículo hello:

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

Abra _modules/articles/client/views/list-articles.client.view.html_.

Justo encima de cierre de hello `</a>` etiqueta, agregue Hola después línea toodisplay `comment` junto con el resto de Hola de datos del artículo hello:

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

Abra _modules/articles/client/views/admin/list-articles.client.view.html_.

Hola interior `<div class="list-group">` elemento y justo encima de cierre de hello `</a>` etiqueta, agregue Hola después línea toodisplay `comment` junto con el resto de Hola de datos del artículo hello:

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

Abra _modules/articles/client/views/admin/form-article.client.view.html_.

Buscar hello `<div class="form-group">` elemento que contiene el botón de envío de hello, que tiene el siguiente aspecto:

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

Justo encima de esta etiqueta, agregue otro `<div class="form-group">` elemento que permite a los usuarios editar hello `comment` campo. El nuevo elemento debe ser como este:

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a>Prueba de los cambios localmente

Guarde todos los cambios.

Pruebe de nuevo los cambios en el modo de producción.

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> Recuerde que la _config/env/production.js_ ha revertido y Hola `MONGODB_URI` sólo se establece la variable de entorno en la aplicación web de Azure y no en el equipo local. Si examina el archivo de configuración de hello, buscar ese Hola configuración de producción tiene como valor predeterminado toouse una base de datos local de MongoDB. De esta forma se garantiza que los datos de producción no se tocan al probar los cambios en el código localmente.

Navegue demasiado`http://localhost:8443` en un explorador y asegúrese de que ha iniciado sesión en.

Seleccione **Administración > Administrar artículos**, a continuación, agregar un artículo seleccionando hello  **+**  botón.

Verá que Hola nueva `Comment` ahora el cuadro de texto.

![Comentario añadido campo tooArticles](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

Hola terminal, detenga Node.js escribiendo `Ctrl+C`. 

### <a name="publish-changes-tooazure"></a>Publicar cambios tooAzure

Confirmar los cambios de Git, a continuación, insertar tooAzure de cambios de código de hello.

```bash
git commit -am "added article comment"
git push azure master
```

Una vez Hola `git push` está completa, navegar por la aplicación web de Azure de tooyour y pruebe la nueva funcionalidad de Hola.

![TooAzure publiquen los cambios de modelo y la base de datos](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

Si agregó anteriormente artículos, aún puede verlos. Los datos existentes en Cosmos DB no se pierden. Además, el esquema de datos de las actualizaciones toohello y deja intactos los datos existentes.

## <a name="stream-diagnostic-logs"></a>Transmisión de registros de diagnóstico 

Mientras se ejecuta la aplicación Node.js en el servicio de aplicación de Azure, puede obtener registros de consola hello tooyour canalizada terminal. De este modo, puede obtener Hola mensajes de diagnóstico del mismo toohelp depurar errores de aplicación.

registro toostart transmisión por secuencias, utilice hello [final del registro de aplicación Web az](/cli/azure/webapp/log#tail) comando.

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

Cuando se inicia la transmisión por secuencias de registro, actualizar la aplicación web de Azure en hello explorador tooget cierto tráfico web. Ahora, ver registros de la consola canalizan tooyour terminal.

Para detener las secuencias de registro en cualquier momento, escriba `Ctrl+C`. 

## <a name="manage-your-azure-web-app"></a>Administración de la aplicación web de Azure

Vaya toohello [portal de Azure](https://portal.azure.com) toosee hello web aplicación que creó.

Hola menú izquierdo, haga clic en **servicios de aplicaciones**, a continuación, haga clic en nombre de saludo de la aplicación web de Azure.

![Aplicación de navegación del portal tooAzure web](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

De forma predeterminada, el portal de hello muestra la aplicación web **Introducción** página. Esta página proporciona una visión del funcionamiento de la aplicación. En este caso, también puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar. pestañas: Hola a la izquierda Hola de página Hola páginas de configuración diferente de hello que puede abrir.

![Página de App Service en Azure Portal](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a>Pasos siguientes

¿Qué ha aprendido?

> [!div class="checklist"]
> * Crear una base de datos MongoDB en Azure
> * Conectar un tooMongoDB de aplicación Node.js
> * Implementar Hola aplicación tooAzure
> * Actualizar el modelo de datos de Hola y volver a implementar la aplicación hello
> * Registros de flujo de Azure tooyour terminal
> * Administrar aplicación Hola Hola portal de Azure

Avanzar toohello siguiente tutorial toolearn cómo toomap un DNS personalizado nombre tooyour web app.

> [!div class="nextstepaction"] 
> [Asignar un tooAzure de nombre DNS personalizado existente aplicaciones Web](app-service-web-tutorial-custom-domain.md)
