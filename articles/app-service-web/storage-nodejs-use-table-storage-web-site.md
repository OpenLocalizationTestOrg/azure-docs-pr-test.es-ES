---
title: "aplicación web de aaaNode.js con hello servicio tabla de Azure"
description: "Este tutorial le enseña cómo toouse hello Azure Table service toostore datos desde una aplicación Node.js que se hospeda en aplicaciones de Web del servicio de aplicación de Azure."
tags: azure-portal
services: app-service\web, storage
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 029e6f46-f586-4309-adbf-71c7b8d537d4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: f6e08335b4c7f62f7b3994287edd586860cb7135
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-using-hello-azure-table-service"></a><span data-ttu-id="a5afe-103">Aplicación web de Node.js con hello servicio tabla de Azure</span><span class="sxs-lookup"><span data-stu-id="a5afe-103">Node.js web app using hello Azure Table Service</span></span>
## <a name="overview"></a><span data-ttu-id="a5afe-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a5afe-104">Overview</span></span>
<span data-ttu-id="a5afe-105">Este tutorial muestra cómo se proporciona el servicio de tabla de toouse datos de administración de datos de Azure toostore y acceso de un [nodo] aplicación hospedada en [servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) aplicaciones Web.</span><span class="sxs-lookup"><span data-stu-id="a5afe-105">This tutorial shows you how toouse Table service provided by Azure Data Management toostore and access data from a [node] application hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="a5afe-106">En este tutorial se asume que tiene alguna experiencia anterior en el uso de Node y [Git].</span><span class="sxs-lookup"><span data-stu-id="a5afe-106">This tutorial assumes that you have some prior experience using node and [Git].</span></span>

<span data-ttu-id="a5afe-107">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="a5afe-107">You will learn:</span></span>

* <span data-ttu-id="a5afe-108">¿Cómo toouse npm (Administrador de paquetes de nodo) tooinstall Hola módulos de nodo</span><span class="sxs-lookup"><span data-stu-id="a5afe-108">How toouse npm (node package manager) tooinstall hello node modules</span></span>
* <span data-ttu-id="a5afe-109">¿Cómo toowork con Hola servicio tabla de Azure</span><span class="sxs-lookup"><span data-stu-id="a5afe-109">How toowork with hello Azure Table service</span></span>
* <span data-ttu-id="a5afe-110">¿Cómo toouse Hola toocreate de CLI de Azure de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="a5afe-110">How toouse hello Azure CLI toocreate a web app.</span></span>

<span data-ttu-id="a5afe-111">Al seguir este tutorial, podrá compilar una aplicación de "lista de tareas pendientes" basadas en web sencilla que permite crear, recuperar y completar tareas.</span><span class="sxs-lookup"><span data-stu-id="a5afe-111">By following this tutorial, you will build a simple web-based "to-do list" application that allows creating, retrieving and completing tasks.</span></span> <span data-ttu-id="a5afe-112">tareas de Hola se almacenan en hello servicio tabla.</span><span class="sxs-lookup"><span data-stu-id="a5afe-112">hello tasks are stored in hello Table service.</span></span>

<span data-ttu-id="a5afe-113">Esta es la aplicación hello completado:</span><span class="sxs-lookup"><span data-stu-id="a5afe-113">Here is hello completed application:</span></span>

![Página web que muestra una lista de tareas vacía][node-table-finished]

> [!NOTE]
> <span data-ttu-id="a5afe-115">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a5afe-115">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a5afe-116">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="a5afe-116">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="a5afe-117">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a5afe-117">Prerequisites</span></span>
<span data-ttu-id="a5afe-118">Antes de seguir las instrucciones de hello en este artículo, asegúrese de que tiene instalado el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="a5afe-118">Before following hello instructions in this article, ensure that you have hello following installed:</span></span>

* <span data-ttu-id="a5afe-119">[nodo] versión 0.10.24 o superior</span><span class="sxs-lookup"><span data-stu-id="a5afe-119">[node] version 0.10.24 or higher</span></span>
* <span data-ttu-id="a5afe-120">[Git]</span><span class="sxs-lookup"><span data-stu-id="a5afe-120">[Git]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a><span data-ttu-id="a5afe-121">Crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="a5afe-121">Create a storage account</span></span>
<span data-ttu-id="a5afe-122">Cree una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="a5afe-122">Create an Azure storage account.</span></span> <span data-ttu-id="a5afe-123">aplicación Hello usará este elementos pendientes de cuenta toostore Hola.</span><span class="sxs-lookup"><span data-stu-id="a5afe-123">hello app will use this account toostore hello to-do items.</span></span>

1. <span data-ttu-id="a5afe-124">Inicie sesión en hello [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a5afe-124">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a5afe-125">Haga clic en hello **New** icono situado en la parte inferior de hello izquierda del portal de hello, a continuación, haga clic en **datos + almacenamiento** > **almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="a5afe-125">Click hello **New** icon on hello bottom left of hello portal, then click **Data + Storage** > **Storage**.</span></span> <span data-ttu-id="a5afe-126">Asigne un nombre único de cuenta de almacenamiento de Hola y crear un nuevo [grupo de recursos](../azure-resource-manager/resource-group-overview.md) para él.</span><span class="sxs-lookup"><span data-stu-id="a5afe-126">Give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Botón Nuevo](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    <span data-ttu-id="a5afe-128">Cuando se ha creado la cuenta de almacenamiento de hello, Hola **notificaciones** botón parpadeará en un color verde **correcto** y está abierta la hoja de la cuenta de almacenamiento de hello tooshow que pertenece toohello nuevo recurso de grupo, creado.</span><span class="sxs-lookup"><span data-stu-id="a5afe-128">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="a5afe-129">En la hoja de la cuenta de almacenamiento de hello, haga clic en **configuración** > **claves**.</span><span class="sxs-lookup"><span data-stu-id="a5afe-129">In hello storage account's blade, click **Settings** > **Keys**.</span></span> <span data-ttu-id="a5afe-130">Copie el Portapapeles de toohello clave de acceso principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5afe-130">Copy hello primary access key toohello clipboard.</span></span>
   
    ![Clave de acceso][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a><span data-ttu-id="a5afe-132">Instalación de módulos y generación de scaffolding</span><span class="sxs-lookup"><span data-stu-id="a5afe-132">Install modules and generate scaffolding</span></span>
<span data-ttu-id="a5afe-133">En esta sección creará una nueva aplicación de nodo y usar paquetes de npm tooadd módulo.</span><span class="sxs-lookup"><span data-stu-id="a5afe-133">In this section you will create a new Node application and use npm tooadd module packages.</span></span> <span data-ttu-id="a5afe-134">Para esta aplicación usará hello [Express] y [Azure] módulos.</span><span class="sxs-lookup"><span data-stu-id="a5afe-134">For this application you will use hello [Express] and [Azure] modules.</span></span> <span data-ttu-id="a5afe-135">módulo de Hello Express proporciona un marco de Model View Controller de nodo, mientras Hola módulos de Azure proporciona servicio de tabla de toohello de conectividad.</span><span class="sxs-lookup"><span data-stu-id="a5afe-135">hello Express module provides a Model View Controller framework for node, while hello Azure modules provides connectivity toohello Table service.</span></span>

### <a name="install-express-and-generate-scaffolding"></a><span data-ttu-id="a5afe-136">Instalar Express y generar scaffolding</span><span class="sxs-lookup"><span data-stu-id="a5afe-136">Install express and generate scaffolding</span></span>
1. <span data-ttu-id="a5afe-137">Desde la línea de comandos de hello, cree un directorio denominado **tasklist** y directory toothat del conmutador.</span><span class="sxs-lookup"><span data-stu-id="a5afe-137">From hello command line, create a new directory named **tasklist** and switch toothat directory.</span></span>  
2. <span data-ttu-id="a5afe-138">Escriba Hola después de módulo de comando tooinstall Hola Express.</span><span class="sxs-lookup"><span data-stu-id="a5afe-138">Enter hello following command tooinstall hello Express module.</span></span>
   
        npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="a5afe-139">Función de sistema operativo de hello, puede ser necesario tooput 'sudo' antes de que el comando de hello:</span><span class="sxs-lookup"><span data-stu-id="a5afe-139">Depending on hello operating system, you may need tooput 'sudo' before hello command:</span></span>
   
        sudo npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="a5afe-140">salida de Hello aparece similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a5afe-140">hello output appears similar toohello following example:</span></span>
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > <span data-ttu-id="a5afe-141">Hola '-g' parámetro instala el módulo de hello globalmente.</span><span class="sxs-lookup"><span data-stu-id="a5afe-141">hello '-g' parameter installs hello module globally.</span></span> <span data-ttu-id="a5afe-142">De este modo, podemos usar **express** toogenerate scaffolding de aplicación web sin necesidad de tootype en información adicional de la ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="a5afe-142">That way, we can use **express** toogenerate web app scaffolding without having tootype in additional path information.</span></span>
   > 
   > 
3. <span data-ttu-id="a5afe-143">scaffolding de hello toocreate para la aplicación hello, escriba Hola **express** comando:</span><span class="sxs-lookup"><span data-stu-id="a5afe-143">toocreate hello scaffolding for hello application, enter hello **express** command:</span></span>
   
        express
   
    <span data-ttu-id="a5afe-144">salida de Hello de este comando aparece similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a5afe-144">hello output of this command appears similar toohello following example:</span></span>
   
           create : .
           create : ./package.json
           create : ./app.js
           create : ./public
           create : ./public/images
           create : ./routes
           create : ./routes/index.js
           create : ./routes/users.js
           create : ./public/stylesheets
           create : ./public/stylesheets/style.css
           create : ./views
           create : ./views/index.jade
           create : ./views/layout.jade
           create : ./views/error.jade
           create : ./public/javascripts
           create : ./bin
           create : ./bin/www
   
           install dependencies:
             $ cd . && npm install
   
           run hello app:
             $ DEBUG=my-application ./bin/www
   
    <span data-ttu-id="a5afe-145">Ahora tiene varias nuevos directorios y archivos en hello **tasklist** directory.</span><span class="sxs-lookup"><span data-stu-id="a5afe-145">You now have several new directories and files in hello **tasklist** directory.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="a5afe-146">Instalar módulos adicionales</span><span class="sxs-lookup"><span data-stu-id="a5afe-146">Install additional modules</span></span>
<span data-ttu-id="a5afe-147">Uno de hello archivos que **express** crea es **package.json**.</span><span class="sxs-lookup"><span data-stu-id="a5afe-147">One of hello files that **express** creates is **package.json**.</span></span> <span data-ttu-id="a5afe-148">Este archivo contiene una lista de dependencias de módulo.</span><span class="sxs-lookup"><span data-stu-id="a5afe-148">This file contains a list of module dependencies.</span></span> <span data-ttu-id="a5afe-149">Más adelante, cuando se implementa hello tooApp de aplicación Web del servicio de aplicaciones, este archivo determina qué módulos necesitan toobe instalado en Azure.</span><span class="sxs-lookup"><span data-stu-id="a5afe-149">Later, when you deploy hello application tooApp Service Web Apps, this file determines which modules need toobe installed on Azure.</span></span>

<span data-ttu-id="a5afe-150">Desde la línea de comandos de hello, escriba Hola después de módulos de hello tooinstall comando descritos en hello **package.json** archivo.</span><span class="sxs-lookup"><span data-stu-id="a5afe-150">From hello command-line, enter hello following command tooinstall hello modules described in hello **package.json** file.</span></span> <span data-ttu-id="a5afe-151">Puede que necesite toouse 'sudo'.</span><span class="sxs-lookup"><span data-stu-id="a5afe-151">You may need toouse 'sudo'.</span></span>

    npm install

<span data-ttu-id="a5afe-152">salida de Hello de este comando aparece similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a5afe-152">hello output of this command appears similar toohello following example:</span></span>

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


<span data-ttu-id="a5afe-153">A continuación, escriba Hola después comando tooinstall hello [azure], [nodo uuid], [nconf] y [async] módulos:</span><span class="sxs-lookup"><span data-stu-id="a5afe-153">Next, enter hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules:</span></span>

    npm install azure-storage node-uuid async nconf --save

<span data-ttu-id="a5afe-154">Hola **--guardar** marca agrega entradas para estos módulos toohello **package.json** archivo.</span><span class="sxs-lookup"><span data-stu-id="a5afe-154">hello **--save** flag adds entries for these modules toohello **package.json** file.</span></span>

<span data-ttu-id="a5afe-155">salida de Hello de este comando aparece similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a5afe-155">hello output of this command appears similar toohello following example:</span></span>

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-hello-application"></a><span data-ttu-id="a5afe-156">Crear aplicación hello</span><span class="sxs-lookup"><span data-stu-id="a5afe-156">Create hello application</span></span>
<span data-ttu-id="a5afe-157">Ahora estamos aplicación de hello toobuild listo.</span><span class="sxs-lookup"><span data-stu-id="a5afe-157">Now we're ready toobuild hello application.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="a5afe-158">Crear un modelo</span><span class="sxs-lookup"><span data-stu-id="a5afe-158">Create a model</span></span>
<span data-ttu-id="a5afe-159">A *modelo* es un objeto que representa los datos de hello en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5afe-159">A *model* is an object that represents hello data in your application.</span></span> <span data-ttu-id="a5afe-160">Para la aplicación hello, modelo solo hello es un objeto de tarea que representa un elemento de lista de tareas pendientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5afe-160">For hello application, hello only model is a task object, which represents an item in hello to-do list.</span></span> <span data-ttu-id="a5afe-161">Tareas tendrá Hola siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="a5afe-161">Tasks will have hello following fields:</span></span>

* <span data-ttu-id="a5afe-162">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="a5afe-162">PartitionKey</span></span>
* <span data-ttu-id="a5afe-163">RowKey</span><span class="sxs-lookup"><span data-stu-id="a5afe-163">RowKey</span></span>
* <span data-ttu-id="a5afe-164">name (string)</span><span class="sxs-lookup"><span data-stu-id="a5afe-164">name (string)</span></span>
* <span data-ttu-id="a5afe-165">category (string)</span><span class="sxs-lookup"><span data-stu-id="a5afe-165">category (string)</span></span>
* <span data-ttu-id="a5afe-166">completed (Boolean)</span><span class="sxs-lookup"><span data-stu-id="a5afe-166">completed (Boolean)</span></span>

<span data-ttu-id="a5afe-167">**PartitionKey** y **RowKey** Hola servicio tabla sirven como claves de tabla.</span><span class="sxs-lookup"><span data-stu-id="a5afe-167">**PartitionKey** and **RowKey** are used by hello Table Service as table keys.</span></span> <span data-ttu-id="a5afe-168">Para obtener más información, consulte [modelo de datos de servicio de la tabla de descripción hello](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5afe-168">For more information, see [Understanding hello Table Service data model](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

1. <span data-ttu-id="a5afe-169">Hola **tasklist** directorio, cree un nuevo directorio denominado **modelos**.</span><span class="sxs-lookup"><span data-stu-id="a5afe-169">In hello **tasklist** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="a5afe-170">Hola **modelos** directorio, cree un nuevo archivo denominado **task.js**.</span><span class="sxs-lookup"><span data-stu-id="a5afe-170">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="a5afe-171">Este archivo contendrá el modelo de Hola para las tareas de hello creadas por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5afe-171">This file will contain hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="a5afe-172">En principio Hola de hello **task.js** , agregue Hola siguiendo las bibliotecas de código tooreference necesario:</span><span class="sxs-lookup"><span data-stu-id="a5afe-172">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. <span data-ttu-id="a5afe-173">Agregue código toodefine siguiente de Hola y exporta el objeto de tarea de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5afe-173">Add hello following code toodefine and export hello Task object.</span></span> <span data-ttu-id="a5afe-174">Este objeto es responsable de la conexión toohello tabla.</span><span class="sxs-lookup"><span data-stu-id="a5afe-174">This object is responsible for connecting toohello table.</span></span>
   
          module.exports = Task;
   
        function Task(storageClient, tableName, partitionKey) {
          this.storageClient = storageClient;
          this.tableName = tableName;
          this.partitionKey = partitionKey;
          this.storageClient.createTableIfNotExists(tableName, function tableCreated(error) {
            if(error) {
              throw error;
            }
          });
        };
5. <span data-ttu-id="a5afe-175">Agregue Hola siguiendo métodos adicionales de código toodefine en el objeto de tarea de hello, que permiten la interacción con los datos almacenados en la tabla de hello:</span><span class="sxs-lookup"><span data-stu-id="a5afe-175">Add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>
   
        Task.prototype = {
          find: function(query, callback) {
            self = this;
            self.storageClient.queryEntities(this.tableName, query, null, function entitiesQueried(error, result) {
              if(error) {
                callback(error);
              } else {
                callback(null, result.entries);
              }
            });
          },
   
          addItem: function(item, callback) {
            self = this;
            // use entityGenerator tooset types
            // NOTE: RowKey must be a string type, even though
            // it contains a GUID in this example.
            var itemDescriptor = {
              PartitionKey: entityGen.String(self.partitionKey),
              RowKey: entityGen.String(uuid()),
              name: entityGen.String(item.name),
              category: entityGen.String(item.category),
              completed: entityGen.Boolean(false)
            };
            self.storageClient.insertEntity(self.tableName, itemDescriptor, function entityInserted(error) {
              if(error){  
                callback(error);
              }
              callback(null);
            });
          },
   
          updateItem: function(rKey, callback) {
            self = this;
            self.storageClient.retrieveEntity(self.tableName, self.partitionKey, rKey, function entityQueried(error, entity) {
              if(error) {
                callback(error);
              }
              entity.completed._ = true;
              self.storageClient.updateEntity(self.tableName, entity, function entityUpdated(error) {
                if(error) {
                  callback(error);
                }
                callback(null);
              });
            });
          }
        }
6. <span data-ttu-id="a5afe-176">Guarde y cierre hello **task.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="a5afe-176">Save and close hello **task.js** file.</span></span>

### <a name="create-a-controller"></a><span data-ttu-id="a5afe-177">Creación de un controlador</span><span class="sxs-lookup"><span data-stu-id="a5afe-177">Create a controller</span></span>
<span data-ttu-id="a5afe-178">A *controlador* controla las solicitudes HTTP y representa la respuesta de hello HTML.</span><span class="sxs-lookup"><span data-stu-id="a5afe-178">A *controller* handles HTTP requests and renders hello HTML response.</span></span>

1. <span data-ttu-id="a5afe-179">Hola **tasklist/rutas** directorio, cree un nuevo archivo denominado **tasklist.js** y ábralo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="a5afe-179">In hello **tasklist/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="a5afe-180">Agregar Hola sigue código demasiado**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="a5afe-180">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="a5afe-181">Esto carga los módulos de hello azure y asincrónicas, que son usados por **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="a5afe-181">This loads hello azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="a5afe-182">Esto también define hello **TaskList** función, que se pasa una instancia de hello **tarea** objeto definimos anteriormente:</span><span class="sxs-lookup"><span data-stu-id="a5afe-182">This also defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. <span data-ttu-id="a5afe-183">Defina un objeto **TaskList** .</span><span class="sxs-lookup"><span data-stu-id="a5afe-183">Define a **TaskList** object.</span></span>
   
        function TaskList(task) {
          this.task = task;
        }
4. <span data-ttu-id="a5afe-184">Agregar Hola siguiendo métodos demasiado**TaskList**:</span><span class="sxs-lookup"><span data-stu-id="a5afe-184">Add hello following methods too**TaskList**:</span></span>
   
        TaskList.prototype = {
          showTasks: function(req, res) {
            self = this;
            var query = new azure.TableQuery()
              .where('completed eq ?', false);
            self.task.find(query, function itemsFound(error, items) {
              res.render('index',{title: 'My ToDo List ', tasks: items});
            });
          },
   
          addTask: function(req,res) {
            var self = this;
            var item = req.body.item;
            self.task.addItem(item, function itemAdded(error) {
              if(error) {
                throw error;
              }
              res.redirect('/');
            });
          },
   
          completeTask: function(req,res) {
            var self = this;
            var completedTasks = Object.keys(req.body);
            async.forEach(completedTasks, function taskIterator(completedTask, callback) {
              self.task.updateItem(completedTask, function itemsUpdated(error) {
                if(error){
                  callback(error);
                } else {
                  callback(null);
                }
              });
            }, function goHome(error){
              if(error) {
                throw error;
              } else {
               res.redirect('/');
              }
            });
          }
        }

### <a name="modify-appjs"></a><span data-ttu-id="a5afe-185">Modificar app.js</span><span class="sxs-lookup"><span data-stu-id="a5afe-185">Modify app.js</span></span>
1. <span data-ttu-id="a5afe-186">De hello **tasklist** Hola de directorio, abra **app.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="a5afe-186">From hello **tasklist** directory, open hello **app.js** file.</span></span> <span data-ttu-id="a5afe-187">Este archivo se creó anteriormente mediante la ejecución de hello **express** comando.</span><span class="sxs-lookup"><span data-stu-id="a5afe-187">This file was created earlier by running hello **express** command.</span></span>
2. <span data-ttu-id="a5afe-188">En principio de Hola de archivo hello, agregue Hola después de módulo de hello azure tooload, nombre de la tabla de conjunto de Hola, clave de partición y las credenciales de almacenamiento de hello conjunto utilizadas por este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a5afe-188">At hello beginning of hello file, add hello following tooload hello azure module, set hello table name, partition key, and set hello storage credentials used by this example:</span></span>
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > <span data-ttu-id="a5afe-189">nconf cargará los valores de configuración de Hola de variables de entorno o hello **config.json** archivo, que creará más adelante.</span><span class="sxs-lookup"><span data-stu-id="a5afe-189">nconf will load hello configuration values from either environment variables or hello **config.json** file, which we will create later.</span></span>
   > 
   > 
3. <span data-ttu-id="a5afe-190">En el archivo de app.js hello, desplácese hacia abajo toowhere verá Hola línea siguiente:</span><span class="sxs-lookup"><span data-stu-id="a5afe-190">In hello app.js file, scroll down toowhere you see hello following line:</span></span>
   
        app.use('/', routes);
        app.use('/users', users);
   
    <span data-ttu-id="a5afe-191">Reemplace Hola por encima de las líneas con el código de hello que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="a5afe-191">Replace hello above lines with hello code shown below.</span></span> <span data-ttu-id="a5afe-192">Esto inicializará en una instancia de <strong>tarea</strong> con una cuenta de almacenamiento de conexión tooyour.</span><span class="sxs-lookup"><span data-stu-id="a5afe-192">This will initialize an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="a5afe-193">Este argumento se pasa toohello <strong>TaskList</strong>, que usará toocommunicate con hello servicio tabla:</span><span class="sxs-lookup"><span data-stu-id="a5afe-193">This is passed toohello <strong>TaskList</strong>, which will use it toocommunicate with hello Table service:</span></span>
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. <span data-ttu-id="a5afe-194">Guardar hello **app.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="a5afe-194">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="a5afe-195">Modificar la vista de índice Hola</span><span class="sxs-lookup"><span data-stu-id="a5afe-195">Modify hello index view</span></span>
1. <span data-ttu-id="a5afe-196">Abra hello **tasklist/views/index.jade** archivo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="a5afe-196">Open hello **tasklist/views/index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="a5afe-197">Reemplace Hola todo contenido de archivo hello con hello siguiente código.</span><span class="sxs-lookup"><span data-stu-id="a5afe-197">Replace hello entire contents of hello file with hello following code.</span></span> <span data-ttu-id="a5afe-198">De esta manera se define una vista para mostrar las tareas existentes y se incluye un formulario para agregar tareas nuevas y marcar las existentes como terminadas.</span><span class="sxs-lookup"><span data-stu-id="a5afe-198">This defines a view that displays existing tasks and includes a form for adding new tasks and marking existing ones as completed.</span></span>
   
        extends layout
   
        block content
          h1= title
          br
   
          form(action="/completetask", method="post")
            table.table.table-striped.table-bordered
              tr
                td Name
                td Category
                td Date
                td Complete
              if (typeof tasks === "undefined")
                tr
                  td
              else
                each task in tasks
                  tr
                    td #{task.name._}
                    td #{task.category._}
                    - var day   = task.Timestamp._.getDate();
                    - var month = task.Timestamp._.getMonth() + 1;
                    - var year  = task.Timestamp._.getFullYear();
                    td #{month + "/" + day + "/" + year}
                    td
                      input(type="checkbox", name="#{task.RowKey._}", value="#{!task.completed._}", checked=task.completed._)
            button.btn(type="submit") Update tasks
          hr
          form.well(action="/addtask", method="post")
            label Item Name:
            input(name="item[name]", type="textbox")
            label Item Category:
            input(name="item[category]", type="textbox")
            br
            button.btn(type="submit") Add item
3. <span data-ttu-id="a5afe-199">Guarde y cierre el archivo **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="a5afe-199">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="a5afe-200">Modificar diseño global Hola</span><span class="sxs-lookup"><span data-stu-id="a5afe-200">Modify hello global layout</span></span>
<span data-ttu-id="a5afe-201">Hola **layout.jade** archivo Hola **vistas** directory es una plantilla global para otros **.jade** archivos.</span><span class="sxs-lookup"><span data-stu-id="a5afe-201">hello **layout.jade** file in hello **views** directory is a global template for other **.jade** files.</span></span> <span data-ttu-id="a5afe-202">En este paso, modificará toouse [Bootstrap Twitter](https://github.com/twbs/bootstrap), que es un Kit de herramientas que hace más fácil toodesign una aplicación web la claridad "nice".</span><span class="sxs-lookup"><span data-stu-id="a5afe-202">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking web app.</span></span>

<span data-ttu-id="a5afe-203">Descargue y extraiga los archivos de Hola para [Bootstrap Twitter](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="a5afe-203">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="a5afe-204">Hola copia **bootstrap.min.css** archivo de hello Bootstrap **css** carpeta en hello **público/hojas de estilos** directorio de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5afe-204">Copy hello **bootstrap.min.css** file from hello Bootstrap **css** folder into hello **public/stylesheets** directory of your application.</span></span>

<span data-ttu-id="a5afe-205">De hello **vistas** carpeta, abra **layout.jade** y reemplace el contenido completo de hello con siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="a5afe-205">From hello **views** folder, open **layout.jade** and replace hello entire contents with hello following:</span></span>

    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body.app
        nav.navbar.navbar-default
          div.navbar-header
          a.navbar-brand(href='/') My Tasks
        block content

### <a name="create-a-config-file"></a><span data-ttu-id="a5afe-206">Creación de un archivo de configuración</span><span class="sxs-lookup"><span data-stu-id="a5afe-206">Create a config file</span></span>
<span data-ttu-id="a5afe-207">toorun localmente la aplicación de hello, colocamos las credenciales de almacenamiento de Azure en un archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="a5afe-207">toorun hello app locally, we'll put Azure Storage credentials into a config file.</span></span> <span data-ttu-id="a5afe-208">Cree un archivo denominado **config.json* * con hello después JSON:</span><span class="sxs-lookup"><span data-stu-id="a5afe-208">Create a file named **config.json* *with hello following JSON:</span></span>

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="a5afe-209">Reemplace **nombre de la cuenta de almacenamiento** con el nombre de Hola de almacenamiento de hello de la cuenta que creó anteriormente y reemplace **clave de acceso de almacenamiento** con la clave de acceso principal de hello para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a5afe-209">Replace **storage account name** with hello name of hello storage account you created earlier, and replace **storage access key** with hello primary access key for your storage account.</span></span> <span data-ttu-id="a5afe-210">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a5afe-210">For example:</span></span>

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="a5afe-211">Guarde este archivo *nivel de un directorio superior* que hello **tasklist** directorio, similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="a5afe-211">Save this file *one directory level higher* than hello **tasklist** directory, like this:</span></span>

    parent/
      |-- config.json
      |-- tasklist/

<span data-ttu-id="a5afe-212">motivo de Hola para hacer esto es tooavoid comprobando el archivo de configuración de hello en el control de código fuente, donde se puede convertir en público.</span><span class="sxs-lookup"><span data-stu-id="a5afe-212">hello reason for doing this is tooavoid checking hello config file into source control, where it might become public.</span></span> <span data-ttu-id="a5afe-213">Cuando se implementa tooAzure de aplicación Hola, usaremos las variables de entorno en lugar de un archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="a5afe-213">When we deploy hello app tooAzure, we will use environment variables instead of a config file.</span></span>

## <a name="run-hello-application-locally"></a><span data-ttu-id="a5afe-214">Ejecutar la aplicación hello localmente</span><span class="sxs-lookup"><span data-stu-id="a5afe-214">Run hello application locally</span></span>
<span data-ttu-id="a5afe-215">aplicación de hello tootest en el equipo local, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a5afe-215">tootest hello application on your local machine, perform hello following steps:</span></span>

1. <span data-ttu-id="a5afe-216">Desde la línea de comandos de hello, cambiar directorios toohello **tasklist** directory.</span><span class="sxs-lookup"><span data-stu-id="a5afe-216">From hello command-line, change directories toohello **tasklist** directory.</span></span>
2. <span data-ttu-id="a5afe-217">Usar hello tras la aplicación localmente de comando toolaunch hello:</span><span class="sxs-lookup"><span data-stu-id="a5afe-217">Use hello following command toolaunch hello application locally:</span></span>
   
        npm start
3. <span data-ttu-id="a5afe-218">Abra un explorador web y navegue toohttp://127.0.0.1:3000.</span><span class="sxs-lookup"><span data-stu-id="a5afe-218">Open a web browser and navigate toohttp://127.0.0.1:3000.</span></span>
   
    <span data-ttu-id="a5afe-219">Aparece un toohello similar de página web siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a5afe-219">A web page similar toohello following example appears.</span></span>
   
    ![Página web que muestra una lista de tareas vacía][node-table-finished]
4. <span data-ttu-id="a5afe-221">toocreate un nuevo elemento de tarea, escriba un nombre y una categoría y haga clic en **Agregar elemento**.</span><span class="sxs-lookup"><span data-stu-id="a5afe-221">toocreate a new to-do item, enter a name and category and click **Add Item**.</span></span> 
5. <span data-ttu-id="a5afe-222">una tarea como completa, verificación de toomark **completar** y haga clic en **tareas de actualización de**.</span><span class="sxs-lookup"><span data-stu-id="a5afe-222">toomark a task as complete, check **Complete** and click **Update Tasks**.</span></span>
   
    ![Una imagen de hello nuevo elemento de lista de Hola de tareas][node-table-list-items]

<span data-ttu-id="a5afe-224">Aunque la aplicación hello se ejecuta localmente, está almacenando datos de Hola Hola servicio tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="a5afe-224">Even though hello application is running locally, it is storing hello data in hello Azure Table service.</span></span>

## <a name="deploy-your-application-tooazure"></a><span data-ttu-id="a5afe-225">Implementar la aplicación tooAzure</span><span class="sxs-lookup"><span data-stu-id="a5afe-225">Deploy your application tooAzure</span></span>
<span data-ttu-id="a5afe-226">pasos de Hello en esta sección use hello Azure herramientas de línea de comandos toocreate una nueva aplicación web de servicio de aplicaciones y, a continuación, usan Git toodeploy la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5afe-226">hello steps in this section use hello Azure command-line tools toocreate a new web app in App Service, and then use Git toodeploy your application.</span></span> <span data-ttu-id="a5afe-227">tooperform estos pasos debe tener una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a5afe-227">tooperform these steps you must have an Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="a5afe-228">Estos pasos también se pueden realizar mediante el uso de hello [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a5afe-228">These steps can also be performed by using hello [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="a5afe-229">Consulte [Compilación e implementación de una aplicación web de Node.js en el Servicio de aplicaciones de Azure].</span><span class="sxs-lookup"><span data-stu-id="a5afe-229">See [Build and deploy a Node.js web app in Azure App Service].</span></span>
> 
> <span data-ttu-id="a5afe-230">Si se trata de hello primera aplicación web que ha creado, debe usar hello Azure Portal toodeploy esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5afe-230">If this is hello first web app you have created, you must use hello Azure Portal toodeploy this application.</span></span>
> 
> 

<span data-ttu-id="a5afe-231">tooget iniciado, instalar hello [CLI de Azure] escribiendo el siguiente comando desde la línea de comandos de Hola de hello:</span><span class="sxs-lookup"><span data-stu-id="a5afe-231">tooget started, install hello [Azure CLI] by entering hello following command from hello command line:</span></span>

    npm install azure-cli -g

### <a name="import-publishing-settings"></a><span data-ttu-id="a5afe-232">Importación de la configuración de publicación</span><span class="sxs-lookup"><span data-stu-id="a5afe-232">Import publishing settings</span></span>
<span data-ttu-id="a5afe-233">En este paso, descargará un archivo que contiene información acerca de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="a5afe-233">In this step, you will download a file containing information about your subscription.</span></span>

1. <span data-ttu-id="a5afe-234">Escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="a5afe-234">Enter hello following command:</span></span>
   
        azure login
   
    <span data-ttu-id="a5afe-235">Este comando inicia un explorador y desplaza la página de descarga de toohello.</span><span class="sxs-lookup"><span data-stu-id="a5afe-235">This command launches a browser and navigates toohello download page.</span></span> <span data-ttu-id="a5afe-236">Si se le solicita, inicie sesión con la cuenta de hello asociada con su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a5afe-236">If prompted, log in with hello account associated with your Azure subscription.</span></span>
   
    <!-- ![hello download page][download-publishing-settings] -->
   
    <span data-ttu-id="a5afe-237">descarga del archivo Hola se iniciará automáticamente; Si no es así, puede hacer clic Hola vínculo al principio de Hola Hola toomanually descarga Hola del archivo de página.</span><span class="sxs-lookup"><span data-stu-id="a5afe-237">hello file download begins automatically; if it does not, you can click hello link at hello beginning of hello page toomanually download hello file.</span></span> <span data-ttu-id="a5afe-238">Guardar ruta de archivo de Hola de archivo y observe Hola.</span><span class="sxs-lookup"><span data-stu-id="a5afe-238">Save hello file and note hello file path.</span></span>
2. <span data-ttu-id="a5afe-239">Escriba Hola después de la configuración del comando de Hola tooimport:</span><span class="sxs-lookup"><span data-stu-id="a5afe-239">Enter hello following command tooimport hello settings:</span></span>
   
        azure account import <path-to-file>
   
    <span data-ttu-id="a5afe-240">Especifique el nombre de ruta de acceso y de Hola de hello publicar el archivo de configuración que ha descargado en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5afe-240">Specify hello path and file name of hello publishing settings file you downloaded in hello previous step.</span></span>
3. <span data-ttu-id="a5afe-241">Después de importa configuración de hello, eliminar Hola publicar el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="a5afe-241">After hello settings are imported, delete hello publish settings file.</span></span> <span data-ttu-id="a5afe-242">Ya no es necesario y contiene información confidencial relacionada con su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a5afe-242">It is no longer needed, and contains sensitive information regarding your Azure subscription.</span></span>

### <a name="create-an-app-service-web-app"></a><span data-ttu-id="a5afe-243">Crear una aplicación web del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="a5afe-243">Create an App Service web app</span></span>
1. <span data-ttu-id="a5afe-244">Desde la línea de comandos de hello, cambiar directorios toohello **tasklist** directory.</span><span class="sxs-lookup"><span data-stu-id="a5afe-244">From hello command-line, change directories toohello **tasklist** directory.</span></span>
2. <span data-ttu-id="a5afe-245">Usar hello después comando toocreate una nueva aplicación web.</span><span class="sxs-lookup"><span data-stu-id="a5afe-245">Use hello following command toocreate a new web app.</span></span>
   
        azure site create --git
   
    <span data-ttu-id="a5afe-246">Se le pedirá que especifique para la ubicación y el nombre de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="a5afe-246">You will be prompted for hello web app name and location.</span></span> <span data-ttu-id="a5afe-247">Proporcione un nombre único y seleccione Hola misma ubicación geográfica que la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="a5afe-247">Provide a unique name and select hello same geographical location as your Azure Storage account.</span></span>
   
    <span data-ttu-id="a5afe-248">Hola `--git` parámetro crea un repositorio Git en Azure para esta aplicación web.</span><span class="sxs-lookup"><span data-stu-id="a5afe-248">hello `--git` parameter creates a Git repository on Azure for this web app.</span></span> <span data-ttu-id="a5afe-249">También inicializa un repositorio Git en el directorio actual de hello si no existe y agrega un [Git remoto] denominado "azure", que es usado toopublish Hola aplicación tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a5afe-249">It also initializes a Git repository in hello current directory if none exists, and adds a [Git remote] named 'azure', which is used toopublish hello application tooAzure.</span></span> <span data-ttu-id="a5afe-250">Por último, crea un **web.config** archivo, que contiene la configuración utilizada por las aplicaciones de Azure toohost nodo.</span><span class="sxs-lookup"><span data-stu-id="a5afe-250">Finally, it creates a **web.config** file, which contains settings used by Azure toohost node applications.</span></span> <span data-ttu-id="a5afe-251">Si se omite hello `--git` parámetro pero Hola directorio contiene un repositorio Git, comando hello seguirá creando remoto hello 'azure'.</span><span class="sxs-lookup"><span data-stu-id="a5afe-251">If you omit hello `--git` parameter but hello directory contains a Git repository, hello command will still create hello 'azure' remote.</span></span>
   
    <span data-ttu-id="a5afe-252">Cuando haya completado este comando, verá el siguiente toohello similar de salida.</span><span class="sxs-lookup"><span data-stu-id="a5afe-252">Once this command has completed, you will see output similar toohello following.</span></span> <span data-ttu-id="a5afe-253">Tenga en cuenta que Hola línea a partir **sitio Web creado en** contiene la dirección URL de hello para la aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5afe-253">Note that hello line beginning with **Website created at** contains hello URL for hello web app.</span></span>
   
        info:   Executing command site create
        help:   Need a site name
        Name: TableTasklist
        info:   Using location southcentraluswebspace
        info:   Executing `git init`
        info:   Creating default .gitignore file
        info:   Creating a new web site
        info:   Created web site at  tabletasklist.azurewebsites.net
        info:   Initializing repository
        info:   Repository initialized
        info:   Executing `git remote add azure https://username@tabletasklist.azurewebsites.net/TableTasklist.git`
        info:   site create command OK
   
   > [!NOTE]
   > <span data-ttu-id="a5afe-254">Si se trata de hello primer servicio de aplicaciones web app para su suscripción, estará siguiendo las instrucciones toouse Hola Portal de Azure toocreate hello web app.</span><span class="sxs-lookup"><span data-stu-id="a5afe-254">If this is hello first App Service web app for your subscription, you will be instructed toouse hello Azure Portal toocreate hello web app.</span></span> <span data-ttu-id="a5afe-255">Para obtener más información, consulte [Compilación e implementación de una aplicación web de Node.js en el Servicio de aplicaciones de Azure].</span><span class="sxs-lookup"><span data-stu-id="a5afe-255">For more information, see [Build and deploy a Node.js web app in Azure App Service].</span></span>
   > 
   > 

### <a name="set-environment-variables"></a><span data-ttu-id="a5afe-256">Establecimiento de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="a5afe-256">Set environment variables</span></span>
<span data-ttu-id="a5afe-257">En este paso, agregará la configuración de aplicaciones de web de tooyour de variables de entorno en Azure.</span><span class="sxs-lookup"><span data-stu-id="a5afe-257">In this step, you will add environment variables tooyour web app configuration on Azure.</span></span>
<span data-ttu-id="a5afe-258">Desde la línea de comandos de hello, escriba Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="a5afe-258">From hello command line, enter hello following:</span></span>

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


<span data-ttu-id="a5afe-259">Reemplace  **<storage account name>**  con el nombre de Hola de almacenamiento de hello de la cuenta que creó anteriormente y reemplace  **<storage access key>**  con la clave de acceso principal de hello para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a5afe-259">Replace **<storage account name>** with hello name of hello storage account you created earlier, and replace **<storage access key>** with hello primary access key for your storage account.</span></span> <span data-ttu-id="a5afe-260">(Usar Hola mismo valores como archivo config.json hello que creó anteriormente).</span><span class="sxs-lookup"><span data-stu-id="a5afe-260">(Use hello same values as hello config.json file that you created earlier.)</span></span>

<span data-ttu-id="a5afe-261">Como alternativa, puede establecer las variables de entorno en hello [Portal de Azure](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="a5afe-261">Alternatively, you can set environment variables in hello [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="a5afe-262">Abra la hoja de la aplicación hello web haciendo clic en **examinar** > **aplicaciones Web** > el nombre de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="a5afe-262">Open hello web app's blade by clicking **Browse** > **Web Apps** > your web app name.</span></span>
2. <span data-ttu-id="a5afe-263">En la hoja de la aplicación web, haga clic en **All Settings** (Toda la configuración)  > **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="a5afe-263">In your web app's blade, click **All Settings** > **Application Settings**.</span></span>
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. <span data-ttu-id="a5afe-264">Desplácese hacia abajo toohello **configuración de la aplicación** agregar pares de clave/valor de Hola y la sección.</span><span class="sxs-lookup"><span data-stu-id="a5afe-264">Scroll down toohello **App settings** section and add hello key/value pairs.</span></span>
   
     ![Configuración de la aplicación](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. <span data-ttu-id="a5afe-266">Haga clic en **GUARDAR**.</span><span class="sxs-lookup"><span data-stu-id="a5afe-266">Click **SAVE**.</span></span>

### <a name="publish-hello-application"></a><span data-ttu-id="a5afe-267">Publicar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="a5afe-267">Publish hello application</span></span>
<span data-ttu-id="a5afe-268">aplicación de hello toopublish, confirmar tooGit de archivos de código de hello y, a continuación, empújelo tooazure/maestro.</span><span class="sxs-lookup"><span data-stu-id="a5afe-268">toopublish hello app, commit hello code files tooGit and then push tooazure/master.</span></span>

1. <span data-ttu-id="a5afe-269">Restablezca las credenciales de implementación.</span><span class="sxs-lookup"><span data-stu-id="a5afe-269">Set your deployment credentials.</span></span>
   
        azure site deployment user set <name> <password>
2. <span data-ttu-id="a5afe-270">Agregue y confirme los archivos de aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5afe-270">Add and commit your application files.</span></span>
   
        git add .
        git commit -m "adding files"
3. <span data-ttu-id="a5afe-271">Insertar Hola confirmación toohello aplicación de servicio de aplicaciones web:</span><span class="sxs-lookup"><span data-stu-id="a5afe-271">Push hello commit toohello App Service web app:</span></span>
   
        git push azure master
   
    <span data-ttu-id="a5afe-272">Use **maestro** como la bifurcación de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5afe-272">Use **master** as hello target branch.</span></span> <span data-ttu-id="a5afe-273">Al final de Hola de implementación de hello, verá un toohello similar de instrucción siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a5afe-273">At hello end of hello deployment, you see a statement similar toohello following example:</span></span>
   
        toohttps://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. <span data-ttu-id="a5afe-274">Una vez completada la operación de inserción de hello, examinar la URL de la aplicación web toohello devuelta previamente por hello `azure create site` tooview de comandos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5afe-274">Once hello push operation has completed, browse toohello web app URL returned previously by hello `azure create site` command tooview your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5afe-275">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a5afe-275">Next steps</span></span>
<span data-ttu-id="a5afe-276">Mientras pasos hello en este artículo describen el uso de información de toostore de servicio de la tabla de Hola, también puede usar [MongoDB](https://mlab.com/azure/).</span><span class="sxs-lookup"><span data-stu-id="a5afe-276">While hello steps in this article describe using hello Table Service toostore information, you can also use [MongoDB](https://mlab.com/azure/).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a5afe-277">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a5afe-277">Additional resources</span></span>
<span data-ttu-id="a5afe-278">[CLI de Azure]</span><span class="sxs-lookup"><span data-stu-id="a5afe-278">[Azure CLI]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="a5afe-279">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="a5afe-279">What's changed</span></span>
* <span data-ttu-id="a5afe-280">Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="a5afe-280">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- URLs -->

[Compilación e implementación de una aplicación web de Node.js en el Servicio de aplicaciones de Azure]: app-service-web-get-started-nodejs.md
[Azure Developer Center]: /develop/nodejs/

[nodo]: http://nodejs.org
[Git]: http://git-scm.com
[Express]: http://expressjs.com
[for free]: http://windowsazure.com
[Git remoto]: http://git-scm.com/docs/git-remote

[CLI de Azure]:../cli-install-nodejs.md

[azure]: https://github.com/Azure/azure-sdk-for-node
[nodo uuid]: https://www.npmjs.com/package/node-uuid
[nconf]: https://www.npmjs.com/package/nconf
[async]: https://www.npmjs.com/package/async

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application tooan Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
