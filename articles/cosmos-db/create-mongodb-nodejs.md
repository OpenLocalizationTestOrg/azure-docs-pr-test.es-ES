---
title: "aaaConnect tooAzure de aplicación de MongoDB Cosmos DB mediante el uso de Node.js | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconnect una tooAzure de aplicación Node.js MongoDB Cosmos DB existente"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 06/19/2017
ms.author: mimig
ms.openlocfilehash: 4bc4f17a31d8c18d1ce5e3f002462f4d48eeb1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-migrate-an-existing-nodejs-mongodb-web-app"></a><span data-ttu-id="0ac48-103">Azure Cosmos DB: Migrar una aplicación web MongoDB de Node.js</span><span class="sxs-lookup"><span data-stu-id="0ac48-103">Azure Cosmos DB: Migrate an existing Node.js MongoDB web app</span></span> 

<span data-ttu-id="0ac48-104">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0ac48-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="0ac48-105">Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente.</span><span class="sxs-lookup"><span data-stu-id="0ac48-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="0ac48-106">Este tutorial rápido muestra cómo toouse existente [MongoDB](mongodb-introduction.md) aplicación escrita en Node.js y conéctelo tooyour base de datos de Azure Cosmos base de datos, que es compatible con conexiones de cliente de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0ac48-106">This quickstart demonstrates how toouse an existing [MongoDB](mongodb-introduction.md) app written in Node.js and connect it tooyour Azure Cosmos DB database, which supports MongoDB client connections.</span></span> <span data-ttu-id="0ac48-107">En otras palabras, la aplicación Node.js sólo sabe que se está conectando con MongoDB APIs de base de datos de tooa.</span><span class="sxs-lookup"><span data-stu-id="0ac48-107">In other words, your Node.js application only knows that it's connecting tooa database using MongoDB APIs.</span></span> <span data-ttu-id="0ac48-108">Es transparente toohello aplicación Hola a datos se almacena en la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0ac48-108">It is transparent toohello application that hello data is stored in Azure Cosmos DB.</span></span>

<span data-ttu-id="0ac48-109">Cuando haya terminado, tendrá una aplicación MEAN (MongoDB, Express, AngularJS y Node.js) que se ejecuta en [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="0ac48-109">When you are done, you will have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running on [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> 

![Aplicación MEAN.js que se ejecuta en Azure App Service](./media/create-mongodb-nodejs/meanjs-in-azure.png)


[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0ac48-111">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="0ac48-111">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0ac48-112">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ac48-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="0ac48-113">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0ac48-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0ac48-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0ac48-114">Prerequisites</span></span> 
<span data-ttu-id="0ac48-115">Además tooAzure CLI, necesitará [Node.js](https://nodejs.org/) y [Git](http://www.git-scm.com/downloads) instalado localmente toorun `npm` y `git` comandos.</span><span class="sxs-lookup"><span data-stu-id="0ac48-115">In addition tooAzure CLI, you need [Node.js](https://nodejs.org/) and [Git](http://www.git-scm.com/downloads) installed locally toorun `npm` and `git` commands.</span></span>

<span data-ttu-id="0ac48-116">Debe tener conocimientos prácticos de Node.js.</span><span class="sxs-lookup"><span data-stu-id="0ac48-116">You should have working knowledge of Node.js.</span></span> <span data-ttu-id="0ac48-117">Este tutorial rápido no está previsto toohelp a desarrollar aplicaciones Node.js en general.</span><span class="sxs-lookup"><span data-stu-id="0ac48-117">This quickstart is not intended toohelp you with developing Node.js applications in general.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="0ac48-118">Clonar aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="0ac48-118">Clone hello sample application</span></span>

<span data-ttu-id="0ac48-119">Abra una ventana de terminal de git, como git bash, y `cd` tooa directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0ac48-119">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

<span data-ttu-id="0ac48-120">Ejecute hello después de repositorio de ejemplo de Hola tooclone de comandos.</span><span class="sxs-lookup"><span data-stu-id="0ac48-120">Run hello following commands tooclone hello sample repository.</span></span> <span data-ttu-id="0ac48-121">Este repositorio de ejemplo contiene predeterminado de hello [MEAN.js](http://meanjs.org/) aplicación.</span><span class="sxs-lookup"><span data-stu-id="0ac48-121">This sample repository contains hello default [MEAN.js](http://meanjs.org/) application.</span></span> 

```bash
git clone https://github.com/prashanthmadi/mean
```

## <a name="run-hello-application"></a><span data-ttu-id="0ac48-122">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="0ac48-122">Run hello application</span></span>

<span data-ttu-id="0ac48-123">Instalar paquetes de saludo necesario e inicie la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="0ac48-123">Install hello required packages and start hello application.</span></span>

```bash
cd mean
npm install
npm start
```

## <a name="log-in-tooazure"></a><span data-ttu-id="0ac48-124">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="0ac48-124">Log in tooAzure</span></span>

<span data-ttu-id="0ac48-125">Si está usando una CLI de Azure instalado, inicie sesión en tooyour suscripción de Azure con hello [inicio de sesión de az](/cli/azure/#login) comando y siga hello en pantalla instrucciones.</span><span class="sxs-lookup"><span data-stu-id="0ac48-125">If you are using an installed Azure CLI, log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> <span data-ttu-id="0ac48-126">Puede omitir este paso si usa Hola Shell en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="0ac48-126">You can skip this step if you're using hello Azure Cloud Shell.</span></span>

```azurecli
az login 
``` 
   
## <a name="add-hello-azure-cosmos-db-module"></a><span data-ttu-id="0ac48-127">Agregar el módulo de base de datos de Azure Cosmos Hola</span><span class="sxs-lookup"><span data-stu-id="0ac48-127">Add hello Azure Cosmos DB module</span></span>

<span data-ttu-id="0ac48-128">Si está usando una CLI de Azure instalado, compruebe toosee si hello `cosmosdb` componente ya está instalado, ejecute hello `az` comando.</span><span class="sxs-lookup"><span data-stu-id="0ac48-128">If you are using an installed Azure CLI, check toosee if hello `cosmosdb` component is already installed by running hello `az` command.</span></span> <span data-ttu-id="0ac48-129">Si `cosmosdb` es en lista de comandos de base de Hola, continuar toohello siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="0ac48-129">If `cosmosdb` is in hello list of base commands, proceed toohello next command.</span></span> <span data-ttu-id="0ac48-130">Puede omitir este paso si usa Hola Shell en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="0ac48-130">You can skip this step if you're using hello Azure Cloud Shell.</span></span>

<span data-ttu-id="0ac48-131">Si `cosmosdb` no está en Hola lista de comandos de base, vuelva a instalar [CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0ac48-131">If `cosmosdb` is not in hello list of base commands, reinstall [Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="0ac48-132">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="0ac48-132">Create a resource group</span></span>

<span data-ttu-id="0ac48-133">Crear un [grupo de recursos](../azure-resource-manager/resource-group-overview.md) con hello [crear grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="0ac48-133">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="0ac48-134">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran recursos de Azure como aplicaciones web, bases de datos y cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0ac48-134">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="0ac48-135">Hello en el ejemplo siguiente se crea un grupo de recursos en la región de Europa occidental Hola.</span><span class="sxs-lookup"><span data-stu-id="0ac48-135">hello following example creates a resource group in hello West Europe region.</span></span> <span data-ttu-id="0ac48-136">Elija un nombre único para el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ac48-136">Choose a unique name for hello resource group.</span></span>

<span data-ttu-id="0ac48-137">Si usas el Shell de nube de Azure, haga clic en **inténtelo**, siga toologin de indicaciones en pantalla de Hola y luego copie el comando hello en el símbolo del sistema Hola.</span><span class="sxs-lookup"><span data-stu-id="0ac48-137">If you are using Azure Cloud Shell, click **Try It**, follow hello onscreen prompts toologin, then copy hello command into hello command prompt.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="0ac48-138">Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0ac48-138">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="0ac48-139">Crear una cuenta de base de datos de Azure Cosmos con hello [crear az cosmosdb](/cli/azure/cosmosdb#create) comando.</span><span class="sxs-lookup"><span data-stu-id="0ac48-139">Create an Azure Cosmos DB account with hello [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="0ac48-140">Hola vuelva siguiente comando, sustituya su propio nombre de cuenta de base de datos de Azure Cosmos único donde verá hello `<cosmosdb-name>` marcador de posición.</span><span class="sxs-lookup"><span data-stu-id="0ac48-140">In hello following command, please substitute your own unique Azure Cosmos DB account name where you see hello `<cosmosdb-name>` placeholder.</span></span> <span data-ttu-id="0ac48-141">Este nombre único que se usará como parte de su punto de conexión de base de datos de Azure Cosmos (`https://<cosmosdb-name>.documents.azure.com/`), por lo que el nombre de Hola debe toobe único entre todas las cuentas de base de datos de Azure Cosmos en Azure.</span><span class="sxs-lookup"><span data-stu-id="0ac48-141">This unique name will be used as part of your Azure Cosmos DB endpoint (`https://<cosmosdb-name>.documents.azure.com/`), so hello name needs toobe unique across all Azure Cosmos DB accounts in Azure.</span></span> 

```azurecli-interactive
az cosmosdb create --name <cosmosdb-name> --resource-group myResourceGroup --kind MongoDB
```

<span data-ttu-id="0ac48-142">Hola `--kind MongoDB` parámetro habilita las conexiones de cliente de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0ac48-142">hello `--kind MongoDB` parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="0ac48-143">Cuando se crea la cuenta de base de datos de Azure Cosmos hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0ac48-143">When hello Azure Cosmos DB account is created, hello Azure CLI shows information similar toohello following example.</span></span> 

> [!NOTE]
> <span data-ttu-id="0ac48-144">Este ejemplo usa JSON como formato de salida de hello CLI de Azure, que es el valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ac48-144">This example uses JSON as hello Azure CLI output format, which is hello default.</span></span> <span data-ttu-id="0ac48-145">toouse otro de salida de formato, vea [formatos para los comandos de CLI de Azure 2.0 de salida](https://docs.microsoft.com/cli/azure/format-output-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0ac48-145">toouse another output format, see [Output formats for Azure CLI 2.0 commands](https://docs.microsoft.com/cli/azure/format-output-azure-cli).</span></span>

```json
{
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb-name>.documents.azure.com:443/",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Document
DB/databaseAccounts/<cosmosdb-name>",
  "kind": "MongoDB",
  "location": "West Europe",
  "name": "<cosmosdb-name>",
  "readLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ],
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.DocumentDB/databaseAccounts",
  "writeLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ]
} 
```

## <a name="connect-your-nodejs-application-toohello-database"></a><span data-ttu-id="0ac48-146">Conectarse a la base de datos de toohello de aplicación Node.js</span><span class="sxs-lookup"><span data-stu-id="0ac48-146">Connect your Node.js application toohello database</span></span>

<span data-ttu-id="0ac48-147">En este paso, se conectará la MEAN.js ejemplo tooan base de datos de Azure Cosmos base de datos que acaba de crear, mediante una cadena de conexión de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0ac48-147">In this step, you connect your MEAN.js sample application tooan Azure Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

<a name="devconfig"></a>
## <a name="configure-hello-connection-string-in-your-nodejs-application"></a><span data-ttu-id="0ac48-148">Configurar la cadena de conexión de hello en la aplicación de Node.js</span><span class="sxs-lookup"><span data-stu-id="0ac48-148">Configure hello connection string in your Node.js application</span></span>

<span data-ttu-id="0ac48-149">En el repositorio de MEAN.js, abra `config/env/local-development.js`.</span><span class="sxs-lookup"><span data-stu-id="0ac48-149">In your MEAN.js repository, open `config/env/local-development.js`.</span></span>

<span data-ttu-id="0ac48-150">Reemplace el contenido de Hola de este archivo con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="0ac48-150">Replace hello content of this file with hello following code.</span></span> <span data-ttu-id="0ac48-151">Asegúrese de tooalso reemplazar Hola dos `<cosmosdb-name>` marcadores de posición con el nombre de cuenta de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0ac48-151">Be sure tooalso replace hello two `<cosmosdb-name>` placeholders with your Azure Cosmos DB account name.</span></span>

```javascript
'use strict';

module.exports = {
  db: {
    uri: 'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean-dev?ssl=true&sslverifycertificate=false'
  }
};
```

## <a name="retrieve-hello-key"></a><span data-ttu-id="0ac48-152">Recuperar la clave de Hola</span><span class="sxs-lookup"><span data-stu-id="0ac48-152">Retrieve hello key</span></span>

<span data-ttu-id="0ac48-153">En orden tooconnect tooan base de datos de Azure Cosmos base de datos, se necesita la clave de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ac48-153">In order tooconnect tooan Azure Cosmos DB database, you need hello database key.</span></span> <span data-ttu-id="0ac48-154">Hola de uso [az cosmosdb lista-claves](/cli/azure/cosmosdb#list-keys) clave principal de comando tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="0ac48-154">Use hello [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command tooretrieve hello primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb-name> --resource-group myResourceGroup --query "primaryMasterKey"
```

<span data-ttu-id="0ac48-155">Hola CLI de Azure genera información toohello similar siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0ac48-155">hello Azure CLI outputs information similar toohello following example.</span></span> 

```json
"RUayjYjixJDWG5xTqIiXjC..."
```

<span data-ttu-id="0ac48-156">Copiar valor de Hola de `primaryMasterKey`.</span><span class="sxs-lookup"><span data-stu-id="0ac48-156">Copy hello value of `primaryMasterKey`.</span></span> <span data-ttu-id="0ac48-157">Esto pegar sobre hello `<primary_master_key>` en `local-development.js`.</span><span class="sxs-lookup"><span data-stu-id="0ac48-157">Paste this over hello  `<primary_master_key>` in `local-development.js`.</span></span>

<span data-ttu-id="0ac48-158">Guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="0ac48-158">Save your changes.</span></span>

### <a name="run-hello-application-again"></a><span data-ttu-id="0ac48-159">Ejecute de nuevo la aplicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ac48-159">Run hello application again.</span></span>

<span data-ttu-id="0ac48-160">Vuelva a ejecutar `npm start`.</span><span class="sxs-lookup"><span data-stu-id="0ac48-160">Run `npm start` again.</span></span> 

```bash
npm start
```

<span data-ttu-id="0ac48-161">Un mensaje de consola ahora debe indicar a que ese entorno de desarrollo de hello está en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="0ac48-161">A console message should now tell you that hello development environment is up and running.</span></span> 

<span data-ttu-id="0ac48-162">Navegue demasiado`http://localhost:3000` en un explorador.</span><span class="sxs-lookup"><span data-stu-id="0ac48-162">Navigate too`http://localhost:3000` in a browser.</span></span> <span data-ttu-id="0ac48-163">Haga clic en **Sign Up** en hello toocreate de menú y try superior dos ficticio a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="0ac48-163">Click **Sign Up** in hello top menu and try toocreate two dummy users.</span></span> 

<span data-ttu-id="0ac48-164">Hola MEAN.js aplicación de ejemplo almacena los datos de usuario de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ac48-164">hello MEAN.js sample application stores user data in hello database.</span></span> <span data-ttu-id="0ac48-165">Si es correcta y MEAN.js inicia sesión automáticamente en hello creó el usuario, a continuación, la conexión de base de datos de Azure Cosmos funciona.</span><span class="sxs-lookup"><span data-stu-id="0ac48-165">If you are successful and MEAN.js automatically signs into hello created user, then your Azure Cosmos DB connection is working.</span></span> 

![MEAN.js se conecta correctamente tooMongoDB](./media/create-mongodb-nodejs/mongodb-connect-success.png)

## <a name="view-data-in-data-explorer"></a><span data-ttu-id="0ac48-167">Ver datos en el Explorador de datos</span><span class="sxs-lookup"><span data-stu-id="0ac48-167">View data in Data Explorer</span></span>

<span data-ttu-id="0ac48-168">Datos almacenados por una base de datos de Azure Cosmos están tooview disponible, consulta y ejecución de lógica de negocios en Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0ac48-168">Data stored by an Azure Cosmos DB is available tooview, query, and run business-logic on in hello Azure portal.</span></span>

<span data-ttu-id="0ac48-169">tooview, consultar y trabajar con datos de usuario de hello creados en el paso anterior hello, inicio de sesión toohello [portal de Azure](https://portal.azure.com) en el explorador web.</span><span class="sxs-lookup"><span data-stu-id="0ac48-169">tooview, query, and work with hello user data created in hello previous step, login toohello [Azure portal](https://portal.azure.com) in your web browser.</span></span>

<span data-ttu-id="0ac48-170">En el cuadro de búsqueda superior hello, tipo de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0ac48-170">In hello top Search box, type Azure Cosmos DB.</span></span> <span data-ttu-id="0ac48-171">Cuando se abra la hoja de la cuenta de Cosmos DB, seleccione su cuenta de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0ac48-171">When your Cosmos DB account blade opens, select your Cosmos DB account.</span></span> <span data-ttu-id="0ac48-172">Hola barra de navegación izquierda, haga clic en el Explorador de datos.</span><span class="sxs-lookup"><span data-stu-id="0ac48-172">In hello left navigation, click Data Explorer.</span></span> <span data-ttu-id="0ac48-173">Expanda la colección en el panel colecciones de hello y, a continuación, puede ver documentos Hola de colección de hello, consultar los datos de hello e incluso crear y ejecutar procedimientos almacenados, desencadenadores y UDF.</span><span class="sxs-lookup"><span data-stu-id="0ac48-173">Expand your collection in hello Collections pane, and then you can view hello documents in hello collection, query hello data, and even create and run stored procedures, triggers, and UDFs.</span></span> 

![Explorador de datos en hello portal de Azure](./media/create-mongodb-nodejs/cosmosdb-connect-mongodb-data-explorer.png)


## <a name="deploy-hello-nodejs-application-tooazure"></a><span data-ttu-id="0ac48-175">Implementar la aplicación tooAzure de hello Node.js</span><span class="sxs-lookup"><span data-stu-id="0ac48-175">Deploy hello Node.js application tooAzure</span></span>

<span data-ttu-id="0ac48-176">En este paso, implementará su tooAzure de aplicación Node.js conectado MongoDB Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0ac48-176">In this step, you deploy your MongoDB-connected Node.js application tooAzure Cosmos DB.</span></span>

<span data-ttu-id="0ac48-177">Quizás haya observado es ese archivo de configuración de Hola que cambió anteriormente para el entorno de desarrollo de hello (`/config/env/local-development.js`).</span><span class="sxs-lookup"><span data-stu-id="0ac48-177">You may have noticed that hello configuration file that you changed earlier is for hello development environment (`/config/env/local-development.js`).</span></span> <span data-ttu-id="0ac48-178">Al implementar el servicio de aplicación tooApp, se ejecutará en el entorno de producción de hello de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0ac48-178">When you deploy your application tooApp Service, it will run in hello production environment by default.</span></span> <span data-ttu-id="0ac48-179">Ahora, deberá toomake Hola mismo cambiar toohello archivo de configuración correspondientes.</span><span class="sxs-lookup"><span data-stu-id="0ac48-179">So now, you need toomake hello same change toohello respective configuration file.</span></span>

<span data-ttu-id="0ac48-180">En el repositorio de MEAN.js, abra `config/env/production.js`.</span><span class="sxs-lookup"><span data-stu-id="0ac48-180">In your MEAN.js repository, open `config/env/production.js`.</span></span>

<span data-ttu-id="0ac48-181">Hola `db` objeto, reemplace el valor de Hola de `uri` como presentación en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0ac48-181">In hello `db` object, replace hello value of `uri` as show in hello following example.</span></span> <span data-ttu-id="0ac48-182">Ser seguro tooreplace Hola marcadores de posición como antes.</span><span class="sxs-lookup"><span data-stu-id="0ac48-182">Be sure tooreplace hello placeholders as before.</span></span>

```javascript
'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean?ssl=true&sslverifycertificate=false',
```

> [!NOTE] 
> <span data-ttu-id="0ac48-183">Hola `ssl=true` opción es importante porque [base de datos de Azure Cosmos requiere SSL](connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="0ac48-183">hello `ssl=true` option is important because [Azure Cosmos DB requires SSL](connect-mongodb-account.md#connection-string-requirements).</span></span> 
>
>

<span data-ttu-id="0ac48-184">Hola terminal, confirme todos los cambios en Git.</span><span class="sxs-lookup"><span data-stu-id="0ac48-184">In hello terminal, commit all your changes into Git.</span></span> <span data-ttu-id="0ac48-185">Puede copiar ambos toorun comandos ellos juntos.</span><span class="sxs-lookup"><span data-stu-id="0ac48-185">You can copy both commands toorun them together.</span></span>

```bash
git add .
git commit -m "configured MongoDB connection string"
```
## <a name="clean-up-resources"></a><span data-ttu-id="0ac48-186">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="0ac48-186">Clean up resources</span></span>

<span data-ttu-id="0ac48-187">Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial rápido de hello portal de Azure con hello pasos:</span><span class="sxs-lookup"><span data-stu-id="0ac48-187">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="0ac48-188">En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="0ac48-188">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="0ac48-189">En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="0ac48-189">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ac48-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0ac48-190">Next steps</span></span>

<span data-ttu-id="0ac48-191">En este tutorial, ha aprendido cómo toocreate una base de datos de Azure Cosmos cuenta y cree una colección de MongoDB utilizando Hola Explorador de datos.</span><span class="sxs-lookup"><span data-stu-id="0ac48-191">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and create a MongoDB collection using hello Data Explorer.</span></span> <span data-ttu-id="0ac48-192">Ahora puede migrar su tooAzure de datos de MongoDB Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0ac48-192">You can now migrate your MongoDB data tooAzure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="0ac48-193">Importación de datos de MongoDB a Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0ac48-193">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)
