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
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a><span data-ttu-id="55b64-103">Compilación de una aplicación web Node.js y MongoDB en Azure</span><span class="sxs-lookup"><span data-stu-id="55b64-103">Build a Node.js and MongoDB web app in Azure</span></span>

<span data-ttu-id="55b64-104">Azure Web Apps proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.</span><span class="sxs-lookup"><span data-stu-id="55b64-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="55b64-105">Este tutorial muestra cómo toocreate una Node.js web de aplicación en Azure y conectar tooa base de datos de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="55b64-105">This tutorial shows how toocreate a Node.js web app in Azure and connect it tooa MongoDB database.</span></span> <span data-ttu-id="55b64-106">Cuando haya terminado, tendrá una aplicación MEAN (MongoDB, Express, AngularJS y Node.js) que se ejecuta en [Azure App Service](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="55b64-106">When you're done, you'll have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running in [Azure App Service](app-service-web-overview.md).</span></span> <span data-ttu-id="55b64-107">Por simplicidad, la aplicación de ejemplo de Hola utiliza hello [el marco de trabajo de MEAN.js web](http://meanjs.org/).</span><span class="sxs-lookup"><span data-stu-id="55b64-107">For simplicity, hello sample application uses hello [MEAN.js web framework](http://meanjs.org/).</span></span>

![Aplicación MEAN.js que se ejecuta en Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="55b64-109">Temas que se abordarán:</span><span class="sxs-lookup"><span data-stu-id="55b64-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="55b64-110">Crear una base de datos MongoDB en Azure</span><span class="sxs-lookup"><span data-stu-id="55b64-110">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="55b64-111">Conectar un tooMongoDB de aplicación Node.js</span><span class="sxs-lookup"><span data-stu-id="55b64-111">Connect a Node.js app tooMongoDB</span></span>
> * <span data-ttu-id="55b64-112">Implementar Hola aplicación tooAzure</span><span class="sxs-lookup"><span data-stu-id="55b64-112">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="55b64-113">Actualizar el modelo de datos de Hola y volver a implementar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="55b64-113">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="55b64-114">Transmitir registros de diagnóstico desde Azure</span><span class="sxs-lookup"><span data-stu-id="55b64-114">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="55b64-115">Administrar aplicación Hola Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="55b64-115">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55b64-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="55b64-116">Prerequisites</span></span>

<span data-ttu-id="55b64-117">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="55b64-117">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="55b64-118">Instalación de Git</span><span class="sxs-lookup"><span data-stu-id="55b64-118">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="55b64-119">Instalación de Node.js y NPM</span><span class="sxs-lookup"><span data-stu-id="55b64-119">Install Node.js and NPM</span></span>](https://nodejs.org/)
1. <span data-ttu-id="55b64-120">[Instale Gulp.js](http://gulpjs.com/) (necesario para [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span><span class="sxs-lookup"><span data-stu-id="55b64-120">[Install Gulp.js](http://gulpjs.com/) (required by [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span></span>
1. [<span data-ttu-id="55b64-121">Descarga y ejecución de MongoDB Community Edition</span><span class="sxs-lookup"><span data-stu-id="55b64-121">Install and run MongoDB Community Edition</span></span>](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="55b64-122">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="55b64-122">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="55b64-123">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="55b64-123">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="55b64-124">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="55b64-124">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-mongodb"></a><span data-ttu-id="55b64-125">Prueba de la base de datos MongoDB local</span><span class="sxs-lookup"><span data-stu-id="55b64-125">Test local MongoDB</span></span>

<span data-ttu-id="55b64-126">Ventana de terminal de hello abierto y `cd` toohello `bin` directorio de la instalación de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="55b64-126">Open hello terminal window and `cd` toohello `bin` directory of your MongoDB installation.</span></span> <span data-ttu-id="55b64-127">Puede utilizar esta ventana de terminal toorun todos los comandos de hello en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="55b64-127">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

<span data-ttu-id="55b64-128">Ejecute `mongo` en el servidor local de MongoDB de hello tooconnect terminal tooyour.</span><span class="sxs-lookup"><span data-stu-id="55b64-128">Run `mongo` in hello terminal tooconnect tooyour local MongoDB server.</span></span>

```bash
mongo
```

<span data-ttu-id="55b64-129">Si la conexión se realiza correctamente, la base de datos de MongoDB estará ya funcionando.</span><span class="sxs-lookup"><span data-stu-id="55b64-129">If your connection is successful, then your MongoDB database is already running.</span></span> <span data-ttu-id="55b64-130">Si no es así, asegúrese de que se ha iniciado la base de datos local de MongoDB siguiendo los pasos de hello en [instalar MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span><span class="sxs-lookup"><span data-stu-id="55b64-130">If not, make sure that your local MongoDB database is started by following hello steps at [Install MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span></span> <span data-ttu-id="55b64-131">A menudo, MongoDB está instalado, pero seguirá necesitando toostart ejecutar `mongod`.</span><span class="sxs-lookup"><span data-stu-id="55b64-131">Often, MongoDB is installed, but you still need toostart it by running `mongod`.</span></span> 

<span data-ttu-id="55b64-132">Cuando haya terminado pruebas de la base de datos de MongoDB, escriba `Ctrl+C` Hola terminal.</span><span class="sxs-lookup"><span data-stu-id="55b64-132">When you're done testing your MongoDB database, type `Ctrl+C` in hello terminal.</span></span> 

## <a name="create-local-nodejs-app"></a><span data-ttu-id="55b64-133">Creación de una aplicación local Node.js</span><span class="sxs-lookup"><span data-stu-id="55b64-133">Create local Node.js app</span></span>

<span data-ttu-id="55b64-134">En este paso, configurar un proyecto Node.js Hola local.</span><span class="sxs-lookup"><span data-stu-id="55b64-134">In this step, you set up hello local Node.js project.</span></span>

### <a name="clone-hello-sample-application"></a><span data-ttu-id="55b64-135">Clonar aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="55b64-135">Clone hello sample application</span></span>

<span data-ttu-id="55b64-136">En la ventana de terminal de hello, `cd` tooa directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="55b64-136">In hello terminal window, `cd` tooa working directory.</span></span>  

<span data-ttu-id="55b64-137">Ejecute hello después de repositorio de ejemplo de comando tooclone Hola.</span><span class="sxs-lookup"><span data-stu-id="55b64-137">Run hello following command tooclone hello sample repository.</span></span> 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

<span data-ttu-id="55b64-138">Este repositorio de ejemplo contiene una copia del programa Hola a [MEAN.js repositorio](https://github.com/meanjs/mean).</span><span class="sxs-lookup"><span data-stu-id="55b64-138">This sample repository contains a copy of hello [MEAN.js repository](https://github.com/meanjs/mean).</span></span> <span data-ttu-id="55b64-139">Es toorun modificado en el servicio de aplicaciones (para obtener más información, vea el repositorio de hello MEAN.js [archivo Léame](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span><span class="sxs-lookup"><span data-stu-id="55b64-139">It is modified toorun on App Service (for more information, see hello MEAN.js repository [README file](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span></span>

### <a name="run-hello-application"></a><span data-ttu-id="55b64-140">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="55b64-140">Run hello application</span></span>

<span data-ttu-id="55b64-141">Ejecute hello siguientes comandos tooinstall Hola necesario paquetes e inicie la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="55b64-141">Run hello following commands tooinstall hello required packages and start hello application.</span></span>

```bash
cd meanjs
npm install
npm start
```

<span data-ttu-id="55b64-142">Cuando se ha cargado completamente la aplicación hello, verá algo similar toohello siguiente mensaje:</span><span class="sxs-lookup"><span data-stu-id="55b64-142">When hello app is fully loaded, you see something similar toohello following message:</span></span>

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

<span data-ttu-id="55b64-143">Navegue toohttp://localhost:3000 en un explorador.</span><span class="sxs-lookup"><span data-stu-id="55b64-143">Navigate toohttp://localhost:3000 in a browser.</span></span> <span data-ttu-id="55b64-144">Haga clic en **Sign Up** sesión Hola menú superior y cree un usuario de prueba.</span><span class="sxs-lookup"><span data-stu-id="55b64-144">Click **Sign Up** in hello top menu and create a test user.</span></span> 

<span data-ttu-id="55b64-145">Hola MEAN.js aplicación de ejemplo almacena los datos de usuario de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="55b64-145">hello MEAN.js sample application stores user data in hello database.</span></span> <span data-ttu-id="55b64-146">Si es correcta en la creación de un usuario y la firma, la aplicación está escribiendo la base de datos de MongoDB local de datos toohello.</span><span class="sxs-lookup"><span data-stu-id="55b64-146">If you are successful at creating a user and signing in, then your app is writing data toohello local MongoDB database.</span></span>

![MEAN.js se conecta correctamente tooMongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

<span data-ttu-id="55b64-148">Seleccione **Administración > Administrar artículos** tooadd algunos artículos.</span><span class="sxs-lookup"><span data-stu-id="55b64-148">Select **Admin > Manage Articles** tooadd some articles.</span></span>

<span data-ttu-id="55b64-149">toostop Node.js en cualquier momento, presione `Ctrl+C` Hola terminal.</span><span class="sxs-lookup"><span data-stu-id="55b64-149">toostop Node.js at any time, press `Ctrl+C` in hello terminal.</span></span> 

## <a name="create-production-mongodb"></a><span data-ttu-id="55b64-150">Creación de una base de datos de MongoDB de producción</span><span class="sxs-lookup"><span data-stu-id="55b64-150">Create production MongoDB</span></span>

<span data-ttu-id="55b64-151">En este paso, creará una base de datos MongoDB en Azure.</span><span class="sxs-lookup"><span data-stu-id="55b64-151">In this step, you create a MongoDB database in Azure.</span></span> <span data-ttu-id="55b64-152">Cuando la aplicación esté implementada tooAzure, utiliza esta base de datos en la nube.</span><span class="sxs-lookup"><span data-stu-id="55b64-152">When your app is deployed tooAzure, it uses this cloud database.</span></span>

<span data-ttu-id="55b64-153">Para MongoDB, en este tutorial se usa [Azure Cosmos DB](/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="55b64-153">For MongoDB, this tutorial uses [Azure Cosmos DB](/azure/documentdb/).</span></span> <span data-ttu-id="55b64-154">Cosmos DB admite las conexiones del cliente de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="55b64-154">Cosmos DB supports MongoDB client connections.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="55b64-155">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="55b64-155">Log in tooAzure</span></span>

<span data-ttu-id="55b64-156">Hola CLI de Azure 2.0 toocreate Hola recursos necesarios toohost deberá usar la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="55b64-156">You'll use hello Azure CLI 2.0 toocreate hello resources needed toohost your app in Azure.</span></span> <span data-ttu-id="55b64-157">Inicie sesión en la suscripción de Azure con hello tooyour [inicio de sesión de az](/cli/azure/#login) comando y siga hello en pantalla instrucciones.</span><span class="sxs-lookup"><span data-stu-id="55b64-157">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="55b64-158">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="55b64-158">Create a resource group</span></span>

<span data-ttu-id="55b64-159">Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="55b64-159">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="55b64-160">Hello en el ejemplo siguiente se crea un grupo de recursos en la región de Europa occidental Hola.</span><span class="sxs-lookup"><span data-stu-id="55b64-160">hello following example creates a resource group in hello West Europe region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

<span data-ttu-id="55b64-161">Hola de uso [az de servicio de aplicaciones enumerar ubicaciones](/cli/azure/appservice#list-locations) ubicaciones disponibles toolist de comandos de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="55b64-161">Use hello [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command toolist available locations.</span></span> 

### <a name="create-a-cosmos-db-account"></a><span data-ttu-id="55b64-162">Creación de una cuenta de Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="55b64-162">Create a Cosmos DB account</span></span>

<span data-ttu-id="55b64-163">Cree una cuenta de base de datos de Cosmos con hello [crear az cosmosdb](/cli/azure/cosmosdb#create) comando.</span><span class="sxs-lookup"><span data-stu-id="55b64-163">Create a Cosmos DB account with hello [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="55b64-164">En hello siguiente comando, sustitúyalo por un nombre único de la base de datos de Cosmos para hello  *\<cosmosdb_name >* marcador de posición.</span><span class="sxs-lookup"><span data-stu-id="55b64-164">In hello following command, substitute a unique Cosmos DB name for hello *\<cosmosdb_name>* placeholder.</span></span> <span data-ttu-id="55b64-165">Este nombre se usa como parte de Hola de punto de conexión de base de datos de Cosmos hello, `https://<cosmosdb_name>.documents.azure.com/`, por lo que el nombre de Hola necesita toobe único a través de todas las cuentas de base de datos de Cosmos en Azure.</span><span class="sxs-lookup"><span data-stu-id="55b64-165">This name is used as hello part of hello Cosmos DB endpoint, `https://<cosmosdb_name>.documents.azure.com/`, so hello name needs toobe unique across all Cosmos DB accounts in Azure.</span></span> <span data-ttu-id="55b64-166">Hola nombre debe contener solo letras minúsculas, números y caracteres de guión (-) de Hola y debe estar comprendido entre 3 y 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="55b64-166">hello name must contain only lowercase letters, numbers, and hello hyphen (-) character, and must be between 3 and 50 characters long.</span></span>

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

<span data-ttu-id="55b64-167">Hola *--MongoDB kind* parámetro habilita las conexiones de cliente de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="55b64-167">hello *--kind MongoDB* parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="55b64-168">Cuando se crea la cuenta de base de datos de Cosmos hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="55b64-168">When hello Cosmos DB account is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

## <a name="connect-app-tooproduction-mongodb"></a><span data-ttu-id="55b64-169">Conectar aplicaciones tooproduction MongoDB</span><span class="sxs-lookup"><span data-stu-id="55b64-169">Connect app tooproduction MongoDB</span></span>

<span data-ttu-id="55b64-170">En este paso, se conectará la MEAN.js ejemplo toohello Cosmos DB base de datos que acaba de crear, mediante una cadena de conexión de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="55b64-170">In this step, you connect your MEAN.js sample application toohello Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

### <a name="retrieve-hello-database-key"></a><span data-ttu-id="55b64-171">Recuperar la clave de la base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="55b64-171">Retrieve hello database key</span></span>

<span data-ttu-id="55b64-172">base de datos de la base de datos de Cosmos del toohello de tooconnect, se necesita la clave de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="55b64-172">tooconnect toohello Cosmos DB database, you need hello database key.</span></span> <span data-ttu-id="55b64-173">Hola de uso [az cosmosdb lista-claves](/cli/azure/cosmosdb#list-keys) clave principal de comando tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="55b64-173">Use hello [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command tooretrieve hello primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

<span data-ttu-id="55b64-174">Hola CLI de Azure muestra información toohello similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="55b64-174">hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Copiar valor de Hola de `primaryMasterKey`. <span data-ttu-id="55b64-176">Necesitará esta información en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="55b64-176">You need this information in hello next step.</span></span>

<a name="devconfig"></a>
### <a name="configure-hello-connection-string-in-your-nodejs-application"></a><span data-ttu-id="55b64-177">Configurar la cadena de conexión de hello en la aplicación de Node.js</span><span class="sxs-lookup"><span data-stu-id="55b64-177">Configure hello connection string in your Node.js application</span></span>

<span data-ttu-id="55b64-178">En el repositorio MEAN.js, abra _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="55b64-178">In your MEAN.js repository, open _config/env/production.js_.</span></span>

<span data-ttu-id="55b64-179">Hola `db` objeto, actualice el valor de Hola de `uri`:</span><span class="sxs-lookup"><span data-stu-id="55b64-179">In hello `db` object, update hello value of `uri`:</span></span>

* <span data-ttu-id="55b64-180">Reemplace Hola dos  *\<cosmosdb_name >* marcadores de posición con el nombre de base de datos de la base de datos de Cosmos.</span><span class="sxs-lookup"><span data-stu-id="55b64-180">Replace hello two *\<cosmosdb_name>* placeholders with your Cosmos DB database name.</span></span>
* <span data-ttu-id="55b64-181">Reemplace hello  *\<primary_master_key >* marcador de posición con clave de Hola que copió en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="55b64-181">Replace hello *\<primary_master_key>* placeholder with hello key you copied in hello previous step.</span></span>

<span data-ttu-id="55b64-182">Hello código siguiente muestra hello `db` objeto:</span><span class="sxs-lookup"><span data-stu-id="55b64-182">hello following code shows hello `db` object:</span></span>

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

<span data-ttu-id="55b64-183">Hola `ssl=true` opción es necesaria porque [Cosmos DB requiere SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="55b64-183">hello `ssl=true` option is required because [Cosmos DB requires SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 

<span data-ttu-id="55b64-184">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="55b64-184">Save your changes.</span></span>

### <a name="test-hello-application-in-production-mode"></a><span data-ttu-id="55b64-185">Probar la aplicación hello en modo de producción</span><span class="sxs-lookup"><span data-stu-id="55b64-185">Test hello application in production mode</span></span> 

<span data-ttu-id="55b64-186">Ejecute hello después comando toominify y agrupación de las secuencias de comandos para el entorno de producción de hello.</span><span class="sxs-lookup"><span data-stu-id="55b64-186">Run hello following command toominify and bundle scripts for hello production environment.</span></span> <span data-ttu-id="55b64-187">Este proceso genera archivos de hello necesarios para el entorno de producción de hello.</span><span class="sxs-lookup"><span data-stu-id="55b64-187">This process generates hello files needed by hello production environment.</span></span>

```bash
gulp prod
```

<span data-ttu-id="55b64-188">Hola ejecución después de que configuró en la cadena de conexión comando toouse hello _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="55b64-188">Run hello following command toouse hello connection string you configured in _config/env/production.js_.</span></span>

```bash
NODE_ENV=production node server.js
```

<span data-ttu-id="55b64-189">`NODE_ENV=production`establece la variable de entorno de Hola que dice toorun Node.js en el entorno de producción de hello.</span><span class="sxs-lookup"><span data-stu-id="55b64-189">`NODE_ENV=production` sets hello environment variable that tells Node.js toorun in hello production environment.</span></span>  <span data-ttu-id="55b64-190">`node server.js`inicia Hola servidor Node.js con `server.js` en la raíz del repositorio.</span><span class="sxs-lookup"><span data-stu-id="55b64-190">`node server.js` starts hello Node.js server with `server.js` in your repository root.</span></span> <span data-ttu-id="55b64-191">Así es como se carga la aplicación de Node.js en Azure.</span><span class="sxs-lookup"><span data-stu-id="55b64-191">This is how your Node.js application is loaded in Azure.</span></span> 

<span data-ttu-id="55b64-192">Cuando se carga la aplicación hello, compruebe que está ejecutando en el entorno de producción de hello toomake:</span><span class="sxs-lookup"><span data-stu-id="55b64-192">When hello app is loaded, check toomake sure that it's running in hello production environment:</span></span>

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

<span data-ttu-id="55b64-193">Navegue toohttp://localhost:8443 en un explorador.</span><span class="sxs-lookup"><span data-stu-id="55b64-193">Navigate toohttp://localhost:8443 in a browser.</span></span> <span data-ttu-id="55b64-194">Haga clic en **Sign Up** sesión Hola menú superior y cree un usuario de prueba.</span><span class="sxs-lookup"><span data-stu-id="55b64-194">Click **Sign Up** in hello top menu and create a test user.</span></span> <span data-ttu-id="55b64-195">Si está creando un usuario correctas e iniciar sesión en, la aplicación está escribiendo datos de base de datos de Cosmos toohello en Azure.</span><span class="sxs-lookup"><span data-stu-id="55b64-195">If you are successful creating a user and signing in, then your app is writing data toohello Cosmos DB database in Azure.</span></span> 

<span data-ttu-id="55b64-196">Hola terminal, detenga Node.js escribiendo `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="55b64-196">In hello terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

## <a name="deploy-app-tooazure"></a><span data-ttu-id="55b64-197">Implementar la aplicación tooAzure</span><span class="sxs-lookup"><span data-stu-id="55b64-197">Deploy app tooAzure</span></span>

<span data-ttu-id="55b64-198">En este paso, implementará la tooAzure de aplicación conectada a MongoDB Node.js servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="55b64-198">In this step, you deploy your MongoDB-connected Node.js application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="55b64-199">Creación de un plan de App Service</span><span class="sxs-lookup"><span data-stu-id="55b64-199">Create an App Service plan</span></span>

<span data-ttu-id="55b64-200">Crear un plan de servicio de aplicaciones con hello [Crear plan de servicio de aplicaciones az](/cli/azure/appservice/plan#create) comando.</span><span class="sxs-lookup"><span data-stu-id="55b64-200">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="55b64-201">Hello en el ejemplo siguiente se crea un plan de servicio de aplicaciones denominado _myAppServicePlan_ con hello **libre** nivel de precios:</span><span class="sxs-lookup"><span data-stu-id="55b64-201">hello following example creates an App Service plan named _myAppServicePlan_ using hello **FREE** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="55b64-202">Cuando se crea el plan de servicio de aplicación Hola, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="55b64-202">When hello App Service plan is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-web-app"></a><span data-ttu-id="55b64-203">Creación de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="55b64-203">Create a web app</span></span>

<span data-ttu-id="55b64-204">Crear una aplicación web en hello `myAppServicePlan` plan de servicio de aplicaciones con hello [crear webapp az](/cli/azure/webapp#create) comando.</span><span class="sxs-lookup"><span data-stu-id="55b64-204">Create a web app in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="55b64-205">Hola web aplicación le ofrece un hospedaje espacio toodeploy el código y proporciona una dirección URL de hello tooview implementado la aplicación.</span><span class="sxs-lookup"><span data-stu-id="55b64-205">hello web app gives you a hosting space toodeploy your code and provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="55b64-206">Aplicación web de uso toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="55b64-206">Use  toocreate hello web app.</span></span> 

<span data-ttu-id="55b64-207">Hola el siguiente comando, reemplace hello  *\<app_name >* marcador de posición con un nombre de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="55b64-207">In hello following command, replace hello *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="55b64-208">Este nombre se usa como parte de Hola de dirección URL de hello predeterminado para la aplicación web de hello, por lo que el nombre de hello necesita toobe único en todas las aplicaciones de servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="55b64-208">This name is used as hello part of hello default URL for hello web app, so hello name needs toobe unique across all apps in Azure App Service.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="55b64-209">Cuando se ha creado la aplicación web de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="55b64-209">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-an-environment-variable"></a><span data-ttu-id="55b64-210">Configuración de una variable de entorno</span><span class="sxs-lookup"><span data-stu-id="55b64-210">Configure an environment variable</span></span>

<span data-ttu-id="55b64-211">Anteriormente en hello tutorial, se codificado de forma rígida Hola base de datos cadena de conexión en _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="55b64-211">Earlier in hello tutorial, you hardcoded hello database connection string in _config/env/production.js_.</span></span> <span data-ttu-id="55b64-212">De acuerdo con el procedimiento recomendado de seguridad, se desean obtener tookeep estos datos confidenciales de su repositorio de Git.</span><span class="sxs-lookup"><span data-stu-id="55b64-212">In keeping with security best practice, you want tookeep this sensitive data out of your Git repository.</span></span> <span data-ttu-id="55b64-213">Para la aplicación que se ejecuta en Azure, usará una variable de entorno en su lugar.</span><span class="sxs-lookup"><span data-stu-id="55b64-213">For your app running in Azure, you'll use an environment variable instead.</span></span>

<span data-ttu-id="55b64-214">En el servicio de aplicación, establecer variables de entorno como _configuración de la aplicación_ mediante el uso de hello [actualizar az webapp configuración appsettings](/cli/azure/webapp/config/appsettings#update) comando.</span><span class="sxs-lookup"><span data-stu-id="55b64-214">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings update](/cli/azure/webapp/config/appsettings#update) command.</span></span> 

<span data-ttu-id="55b64-215">Hello ejemplo siguiente se configura un `MONGODB_URI` configuración de la aplicación en la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="55b64-215">hello following example configures a `MONGODB_URI` app setting in your Azure web app.</span></span> <span data-ttu-id="55b64-216">Reemplace hello  *\<app_name >*,  *\<cosmosdb_name >*, y  *\<primary_master_key >* marcadores de posición.</span><span class="sxs-lookup"><span data-stu-id="55b64-216">Replace hello *\<app_name>*, *\<cosmosdb_name>*, and *\<primary_master_key>* placeholders.</span></span>

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

<span data-ttu-id="55b64-217">En el código de Node.js, accederá a este valor de aplicación con `process.env.MONGODB_URI`, al igual que accedería a cualquier variable de entorno.</span><span class="sxs-lookup"><span data-stu-id="55b64-217">In Node.js code, you access this app setting with `process.env.MONGODB_URI`, just like you would access any environment variable.</span></span> 

<span data-ttu-id="55b64-218">Ahora, deshacer los cambios too_config/env/production.js_ con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="55b64-218">Now, undo your changes too_config/env/production.js_ with hello following command:</span></span>

```bash
git checkout -- .
```

<span data-ttu-id="55b64-219">Vuelva a abrir _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="55b64-219">Open _config/env/production.js_ again.</span></span> <span data-ttu-id="55b64-220">Tenga en cuenta esa aplicación de MEAN.js hello predeterminada ya está configurado toouse Hola `MONGODB_URI` variable de entorno que creó.</span><span class="sxs-lookup"><span data-stu-id="55b64-220">Note that hello default MEAN.js app is already configured toouse hello `MONGODB_URI` environment variable that you created.</span></span>

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a><span data-ttu-id="55b64-221">Configuración de la implementación de Git local</span><span class="sxs-lookup"><span data-stu-id="55b64-221">Configure local git deployment</span></span> 

<span data-ttu-id="55b64-222">Hola de uso [conjunto de usuarios de implementación de aplicación Web de az](/cli/azure/webapp/deployment/user#set) toocreate credenciales para la implementación de comandos.</span><span class="sxs-lookup"><span data-stu-id="55b64-222">Use hello [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command toocreate credentials for deployment.</span></span>

<span data-ttu-id="55b64-223">Puede implementar su aplicación tooAzure servicio de aplicaciones de varias maneras, como FTP, Git local, GitHub, Visual Studio Team Services y BitBucket.</span><span class="sxs-lookup"><span data-stu-id="55b64-223">You can deploy your application tooAzure App Service in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="55b64-224">Para FTP y Git local, es necesario toohave un usuario de implementación configurada en hello server tooauthenticate la implementación.</span><span class="sxs-lookup"><span data-stu-id="55b64-224">For FTP and local Git, it is necessary toohave a deployment user configured on hello server tooauthenticate your deployment.</span></span> <span data-ttu-id="55b64-225">Dicho usuario es el nivel de cuenta y no es la cuenta de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="55b64-225">This deployment user is account-level and is different from your Azure subscription account.</span></span> <span data-ttu-id="55b64-226">Solo necesita tooconfigure este usuario de implementación una vez.</span><span class="sxs-lookup"><span data-stu-id="55b64-226">You only need tooconfigure this deployment user once.</span></span>

<span data-ttu-id="55b64-227">Hola siguiente comando, reemplace  *\<nombre de usuario >* y  *\<contraseña >* con un nuevo nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="55b64-227">In hello following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="55b64-228">nombre de usuario de Hello debe ser único.</span><span class="sxs-lookup"><span data-stu-id="55b64-228">hello user name must be unique.</span></span> <span data-ttu-id="55b64-229">Hello contraseña debe tener al menos ocho caracteres, con dos Hola después de tres elementos: letras, números y símbolos.</span><span class="sxs-lookup"><span data-stu-id="55b64-229">hello password must be at least eight characters long, with two of hello following three elements:  letters, numbers, symbols.</span></span> <span data-ttu-id="55b64-230">Si se produce un ` 'Conflict'. Details: 409` error, el nombre de usuario de cambio Hola.</span><span class="sxs-lookup"><span data-stu-id="55b64-230">If you get a ` 'Conflict'. Details: 409` error, change hello username.</span></span> <span data-ttu-id="55b64-231">Si se produce un error ` 'Bad Request'. Details: 400`, use una contraseña más segura.</span><span class="sxs-lookup"><span data-stu-id="55b64-231">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="55b64-232">Nombre de usuario de registro hello y una contraseña para su uso en pasos posteriores al implementar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="55b64-232">Record hello user name and password for use in later steps when you deploy hello app.</span></span>

<span data-ttu-id="55b64-233">Hola de uso [origen de implementación de aplicación Web en az config-local-git](/cli/azure/webapp/deployment/source#config-local-git) comando tooconfigure Git acceso toohello Azure la aplicación web local.</span><span class="sxs-lookup"><span data-stu-id="55b64-233">Use hello [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command tooconfigure local Git access toohello Azure web app.</span></span> 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

<span data-ttu-id="55b64-234">Cuando se configura el usuario de la implementación de hello, Hola CLI de Azure muestra hello de dirección URL de implementación para la aplicación web de Azure en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="55b64-234">When hello deployment user is configured, hello Azure CLI shows hello deployment URL for your Azure web app in hello following format:</span></span>

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

<span data-ttu-id="55b64-235">Copie Hola de salida de terminal de hello, ya que se usará en el paso siguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="55b64-235">Copy hello output from hello terminal, as it will be used in hello next step.</span></span> 

### <a name="push-tooazure-from-git"></a><span data-ttu-id="55b64-236">TooAzure de inserción de Git</span><span class="sxs-lookup"><span data-stu-id="55b64-236">Push tooAzure from Git</span></span>

<span data-ttu-id="55b64-237">Agregue un repositorio de Git local de Azure tooyour remoto.</span><span class="sxs-lookup"><span data-stu-id="55b64-237">Add an Azure remote tooyour local Git repository.</span></span> 

```bash
git remote add azure <paste_copied_url_here> 
```

<span data-ttu-id="55b64-238">Insertar toohello Azure toodeploy remoto aplicaciones Node.js.</span><span class="sxs-lookup"><span data-stu-id="55b64-238">Push toohello Azure remote toodeploy your Node.js application.</span></span> <span data-ttu-id="55b64-239">Se le pedirá para contraseña de Hola que proporcionó anteriormente como parte de la creación de hello de usuario de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="55b64-239">You will be prompted for hello password you supplied earlier as part of hello creation of hello deployment user.</span></span> 

```bash
git push azure master
```

<span data-ttu-id="55b64-240">Durante la implementación, Azure App Service comunicará su progreso con Git.</span><span class="sxs-lookup"><span data-stu-id="55b64-240">During deployment, Azure App Service communicates its progress with Git.</span></span>

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

<span data-ttu-id="55b64-241">Puede observar que se ejecuta el proceso de implementación de hello [Gulp](http://gulpjs.com/) después `npm install`.</span><span class="sxs-lookup"><span data-stu-id="55b64-241">You may notice that hello deployment process runs [Gulp](http://gulpjs.com/) after `npm install`.</span></span> <span data-ttu-id="55b64-242">Servicio de aplicaciones ejecutan tareas Gulp o Grunt durante la implementación, por lo que este repositorio de ejemplo tiene dos adicionales archivos en su tooenable del directorio raíz que:</span><span class="sxs-lookup"><span data-stu-id="55b64-242">App Service does not run Gulp or Grunt tasks during deployment, so this sample repository has two additional files in its root directory tooenable it:</span></span> 

- <span data-ttu-id="55b64-243">_implementación_ -este archivo indica toorun de servicio de aplicaciones `bash deploy.sh` como script de implementación personalizada de Hola.</span><span class="sxs-lookup"><span data-stu-id="55b64-243">_.deployment_ - This file tells App Service toorun `bash deploy.sh` as hello custom deployment script.</span></span>
- <span data-ttu-id="55b64-244">_Deploy.sh_ -Hola script de implementación personalizado.</span><span class="sxs-lookup"><span data-stu-id="55b64-244">_deploy.sh_ - hello custom deployment script.</span></span> <span data-ttu-id="55b64-245">Si examina el archivo hello, verá que se ejecuta `gulp prod` después `npm install` y `bower install`.</span><span class="sxs-lookup"><span data-stu-id="55b64-245">If you review hello file, you will see that it runs `gulp prod` after `npm install` and `bower install`.</span></span> 

<span data-ttu-id="55b64-246">Puede usar este enfoque tooadd cualquier tooyour paso implementación basada en Git.</span><span class="sxs-lookup"><span data-stu-id="55b64-246">You can use this approach tooadd any step tooyour Git-based deployment.</span></span> <span data-ttu-id="55b64-247">Si reinicia la aplicación web de Azure en cualquier momento, App Service no vuelve a ejecutar estas tareas de automatización.</span><span class="sxs-lookup"><span data-stu-id="55b64-247">If you restart your Azure web app at any point, App Service doesn't rerun these automation tasks.</span></span>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="55b64-248">Examinar la aplicación web de Azure de toohello</span><span class="sxs-lookup"><span data-stu-id="55b64-248">Browse toohello Azure web app</span></span> 

<span data-ttu-id="55b64-249">Examinar toohello implementa la aplicación web mediante el explorador web.</span><span class="sxs-lookup"><span data-stu-id="55b64-249">Browse toohello deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
``` 

<span data-ttu-id="55b64-250">Haga clic en **Sign Up** sesión Hola menú superior y cree un usuario ficticio.</span><span class="sxs-lookup"><span data-stu-id="55b64-250">Click **Sign Up** in hello top menu and create a dummy user.</span></span> 

<span data-ttu-id="55b64-251">Si es correcta y la aplicación hello inicia sesión automáticamente en toohello crea el usuario y, a continuación, la aplicación MEAN.js en Azure tiene base de datos de conectividad toohello MongoDB (Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="55b64-251">If you are successful and hello app automatically signs in toohello created user, then your MEAN.js app in Azure has connectivity toohello MongoDB (Cosmos DB) database.</span></span> 

![Aplicación MEAN.js que se ejecuta en Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="55b64-253">Seleccione **Administración > Administrar artículos** tooadd algunos artículos.</span><span class="sxs-lookup"><span data-stu-id="55b64-253">Select **Admin > Manage Articles** tooadd some articles.</span></span> 

<span data-ttu-id="55b64-254">**¡Enhorabuena!**</span><span class="sxs-lookup"><span data-stu-id="55b64-254">**Congratulations!**</span></span> <span data-ttu-id="55b64-255">Está ejecutando una aplicación Node.js orientada a datos en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="55b64-255">You're running a data-driven Node.js app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="55b64-256">Actualización del modelo de datos y nueva implementación</span><span class="sxs-lookup"><span data-stu-id="55b64-256">Update data model and redeploy</span></span>

<span data-ttu-id="55b64-257">En este paso, cambiar hello `article` datos de modelo y publicar su tooAzure de cambio.</span><span class="sxs-lookup"><span data-stu-id="55b64-257">In this step, you change hello `article` data model and publish your change tooAzure.</span></span>

### <a name="update-hello-data-model"></a><span data-ttu-id="55b64-258">Modelo de datos de actualización Hola</span><span class="sxs-lookup"><span data-stu-id="55b64-258">Update hello data model</span></span>

<span data-ttu-id="55b64-259">Abra _modules/articles/server/models/article.server.model.js_.</span><span class="sxs-lookup"><span data-stu-id="55b64-259">Open _modules/articles/server/models/article.server.model.js_.</span></span>

<span data-ttu-id="55b64-260">En `ArticleSchema`, agregue un tipo `String` llamado `comment`.</span><span class="sxs-lookup"><span data-stu-id="55b64-260">In `ArticleSchema`, add a `String` type called `comment`.</span></span> <span data-ttu-id="55b64-261">Cuando haya finalizado, su código de esquema tendrá este aspecto:</span><span class="sxs-lookup"><span data-stu-id="55b64-261">When you're done, your schema code should look like this:</span></span>

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

### <a name="update-hello-articles-code"></a><span data-ttu-id="55b64-262">Actualizar código de hello artículos</span><span class="sxs-lookup"><span data-stu-id="55b64-262">Update hello articles code</span></span>

<span data-ttu-id="55b64-263">Actualizar el resto de Hola de su `articles` código toouse `comment`.</span><span class="sxs-lookup"><span data-stu-id="55b64-263">Update hello rest of your `articles` code toouse `comment`.</span></span>

<span data-ttu-id="55b64-264">Hay cinco archivos que necesita toomodify: controlador de servidor de Hola y vistas de cliente de hello cuatro.</span><span class="sxs-lookup"><span data-stu-id="55b64-264">There are five files you need toomodify: hello server controller and hello four client views.</span></span> 

<span data-ttu-id="55b64-265">Abra _modules/articles/server/controllers/articles.server.controller.js_.</span><span class="sxs-lookup"><span data-stu-id="55b64-265">Open _modules/articles/server/controllers/articles.server.controller.js_.</span></span>

<span data-ttu-id="55b64-266">Hola `update` funcione, agregue una asignación de `article.comment`.</span><span class="sxs-lookup"><span data-stu-id="55b64-266">In hello `update` function, add an assignment for `article.comment`.</span></span> <span data-ttu-id="55b64-267">Hello código siguiente muestra hello completado `update` función:</span><span class="sxs-lookup"><span data-stu-id="55b64-267">hello following code shows hello completed `update` function:</span></span>

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

<span data-ttu-id="55b64-268">Abra _modules/articles/client/views/view-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="55b64-268">Open _modules/articles/client/views/view-article.client.view.html_.</span></span>

<span data-ttu-id="55b64-269">Justo encima de cierre de hello `</section>` etiqueta, agregue Hola después línea toodisplay `comment` junto con el resto de Hola de datos del artículo hello:</span><span class="sxs-lookup"><span data-stu-id="55b64-269">Just above hello closing `</section>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

<span data-ttu-id="55b64-270">Abra _modules/articles/client/views/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="55b64-270">Open _modules/articles/client/views/list-articles.client.view.html_.</span></span>

<span data-ttu-id="55b64-271">Justo encima de cierre de hello `</a>` etiqueta, agregue Hola después línea toodisplay `comment` junto con el resto de Hola de datos del artículo hello:</span><span class="sxs-lookup"><span data-stu-id="55b64-271">Just above hello closing `</a>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

<span data-ttu-id="55b64-272">Abra _modules/articles/client/views/admin/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="55b64-272">Open _modules/articles/client/views/admin/list-articles.client.view.html_.</span></span>

<span data-ttu-id="55b64-273">Hola interior `<div class="list-group">` elemento y justo encima de cierre de hello `</a>` etiqueta, agregue Hola después línea toodisplay `comment` junto con el resto de Hola de datos del artículo hello:</span><span class="sxs-lookup"><span data-stu-id="55b64-273">Inside hello `<div class="list-group">` element and just above hello closing `</a>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

<span data-ttu-id="55b64-274">Abra _modules/articles/client/views/admin/form-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="55b64-274">Open _modules/articles/client/views/admin/form-article.client.view.html_.</span></span>

<span data-ttu-id="55b64-275">Buscar hello `<div class="form-group">` elemento que contiene el botón de envío de hello, que tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="55b64-275">Find hello `<div class="form-group">` element that contains hello submit button, which looks like this:</span></span>

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

<span data-ttu-id="55b64-276">Justo encima de esta etiqueta, agregue otro `<div class="form-group">` elemento que permite a los usuarios editar hello `comment` campo.</span><span class="sxs-lookup"><span data-stu-id="55b64-276">Just above this tag, add another `<div class="form-group">` element that lets people edit hello `comment` field.</span></span> <span data-ttu-id="55b64-277">El nuevo elemento debe ser como este:</span><span class="sxs-lookup"><span data-stu-id="55b64-277">Your new element should look like this:</span></span>

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="55b64-278">Prueba de los cambios localmente</span><span class="sxs-lookup"><span data-stu-id="55b64-278">Test your changes locally</span></span>

<span data-ttu-id="55b64-279">Guarde todos los cambios.</span><span class="sxs-lookup"><span data-stu-id="55b64-279">Save all your changes.</span></span>

<span data-ttu-id="55b64-280">Pruebe de nuevo los cambios en el modo de producción.</span><span class="sxs-lookup"><span data-stu-id="55b64-280">Test your changes in production mode again.</span></span>

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> <span data-ttu-id="55b64-281">Recuerde que la _config/env/production.js_ ha revertido y Hola `MONGODB_URI` sólo se establece la variable de entorno en la aplicación web de Azure y no en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="55b64-281">Remember that your _config/env/production.js_ has been reverted, and hello `MONGODB_URI` environment variable is only set in your Azure web app and not on your local machine.</span></span> <span data-ttu-id="55b64-282">Si examina el archivo de configuración de hello, buscar ese Hola configuración de producción tiene como valor predeterminado toouse una base de datos local de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="55b64-282">If you look at hello config file, you find that hello production configuration defaults toouse a local MongoDB database.</span></span> <span data-ttu-id="55b64-283">De esta forma se garantiza que los datos de producción no se tocan al probar los cambios en el código localmente.</span><span class="sxs-lookup"><span data-stu-id="55b64-283">This makes sure that you don't touch production data when you test your code changes locally.</span></span>

<span data-ttu-id="55b64-284">Navegue demasiado`http://localhost:8443` en un explorador y asegúrese de que ha iniciado sesión en.</span><span class="sxs-lookup"><span data-stu-id="55b64-284">Navigate too`http://localhost:8443` in a browser and make sure that you're signed in.</span></span>

<span data-ttu-id="55b64-285">Seleccione **Administración > Administrar artículos**, a continuación, agregar un artículo seleccionando hello  **+**  botón.</span><span class="sxs-lookup"><span data-stu-id="55b64-285">Select **Admin > Manage Articles**, then add an article by selecting hello **+** button.</span></span>

<span data-ttu-id="55b64-286">Verá que Hola nueva `Comment` ahora el cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="55b64-286">You see hello new `Comment` textbox now.</span></span>

![Comentario añadido campo tooArticles](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

<span data-ttu-id="55b64-288">Hola terminal, detenga Node.js escribiendo `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="55b64-288">In hello terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

### <a name="publish-changes-tooazure"></a><span data-ttu-id="55b64-289">Publicar cambios tooAzure</span><span class="sxs-lookup"><span data-stu-id="55b64-289">Publish changes tooAzure</span></span>

<span data-ttu-id="55b64-290">Confirmar los cambios de Git, a continuación, insertar tooAzure de cambios de código de hello.</span><span class="sxs-lookup"><span data-stu-id="55b64-290">Commit your changes in Git, then push hello code changes tooAzure.</span></span>

```bash
git commit -am "added article comment"
git push azure master
```

<span data-ttu-id="55b64-291">Una vez Hola `git push` está completa, navegar por la aplicación web de Azure de tooyour y pruebe la nueva funcionalidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="55b64-291">Once hello `git push` is complete, navigate tooyour Azure web app and try out hello new functionality.</span></span>

![TooAzure publiquen los cambios de modelo y la base de datos](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

<span data-ttu-id="55b64-293">Si agregó anteriormente artículos, aún puede verlos.</span><span class="sxs-lookup"><span data-stu-id="55b64-293">If you added any articles earlier, you still can see them.</span></span> <span data-ttu-id="55b64-294">Los datos existentes en Cosmos DB no se pierden.</span><span class="sxs-lookup"><span data-stu-id="55b64-294">Existing data in your Cosmos DB is not lost.</span></span> <span data-ttu-id="55b64-295">Además, el esquema de datos de las actualizaciones toohello y deja intactos los datos existentes.</span><span class="sxs-lookup"><span data-stu-id="55b64-295">Also, your updates toohello data schema and leaves your existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="55b64-296">Transmisión de registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="55b64-296">Stream diagnostic logs</span></span> 

<span data-ttu-id="55b64-297">Mientras se ejecuta la aplicación Node.js en el servicio de aplicación de Azure, puede obtener registros de consola hello tooyour canalizada terminal.</span><span class="sxs-lookup"><span data-stu-id="55b64-297">While your Node.js application runs in Azure App Service, you can get hello console logs piped tooyour terminal.</span></span> <span data-ttu-id="55b64-298">De este modo, puede obtener Hola mensajes de diagnóstico del mismo toohelp depurar errores de aplicación.</span><span class="sxs-lookup"><span data-stu-id="55b64-298">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="55b64-299">registro toostart transmisión por secuencias, utilice hello [final del registro de aplicación Web az](/cli/azure/webapp/log#tail) comando.</span><span class="sxs-lookup"><span data-stu-id="55b64-299">toostart log streaming, use hello [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

<span data-ttu-id="55b64-300">Cuando se inicia la transmisión por secuencias de registro, actualizar la aplicación web de Azure en hello explorador tooget cierto tráfico web.</span><span class="sxs-lookup"><span data-stu-id="55b64-300">Once log streaming has started, refresh your Azure web app in hello browser tooget some web traffic.</span></span> <span data-ttu-id="55b64-301">Ahora, ver registros de la consola canalizan tooyour terminal.</span><span class="sxs-lookup"><span data-stu-id="55b64-301">You now see console logs piped tooyour terminal.</span></span>

<span data-ttu-id="55b64-302">Para detener las secuencias de registro en cualquier momento, escriba `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="55b64-302">Stop log streaming at any time by typing `Ctrl+C`.</span></span> 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="55b64-303">Administración de la aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="55b64-303">Manage your Azure web app</span></span>

<span data-ttu-id="55b64-304">Vaya toohello [portal de Azure](https://portal.azure.com) toosee hello web aplicación que creó.</span><span class="sxs-lookup"><span data-stu-id="55b64-304">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span>

<span data-ttu-id="55b64-305">Hola menú izquierdo, haga clic en **servicios de aplicaciones**, a continuación, haga clic en nombre de saludo de la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="55b64-305">From hello left menu, click **App Services**, then click hello name of your Azure web app.</span></span>

![Aplicación de navegación del portal tooAzure web](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

<span data-ttu-id="55b64-307">De forma predeterminada, el portal de hello muestra la aplicación web **Introducción** página.</span><span class="sxs-lookup"><span data-stu-id="55b64-307">By default, hello portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="55b64-308">Esta página proporciona una visión del funcionamiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="55b64-308">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="55b64-309">En este caso, también puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar.</span><span class="sxs-lookup"><span data-stu-id="55b64-309">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="55b64-310">pestañas: Hola a la izquierda Hola de página Hola páginas de configuración diferente de hello que puede abrir.</span><span class="sxs-lookup"><span data-stu-id="55b64-310">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span>

![Página de App Service en Azure Portal](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a><span data-ttu-id="55b64-312">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="55b64-312">Next steps</span></span>

<span data-ttu-id="55b64-313">¿Qué ha aprendido?</span><span class="sxs-lookup"><span data-stu-id="55b64-313">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="55b64-314">Crear una base de datos MongoDB en Azure</span><span class="sxs-lookup"><span data-stu-id="55b64-314">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="55b64-315">Conectar un tooMongoDB de aplicación Node.js</span><span class="sxs-lookup"><span data-stu-id="55b64-315">Connect a Node.js app tooMongoDB</span></span>
> * <span data-ttu-id="55b64-316">Implementar Hola aplicación tooAzure</span><span class="sxs-lookup"><span data-stu-id="55b64-316">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="55b64-317">Actualizar el modelo de datos de Hola y volver a implementar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="55b64-317">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="55b64-318">Registros de flujo de Azure tooyour terminal</span><span class="sxs-lookup"><span data-stu-id="55b64-318">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="55b64-319">Administrar aplicación Hola Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="55b64-319">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="55b64-320">Avanzar toohello siguiente tutorial toolearn cómo toomap un DNS personalizado nombre tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="55b64-320">Advance toohello next tutorial toolearn how toomap a custom DNS name tooyour web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="55b64-321">Asignar un tooAzure de nombre DNS personalizado existente aplicaciones Web</span><span class="sxs-lookup"><span data-stu-id="55b64-321">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
