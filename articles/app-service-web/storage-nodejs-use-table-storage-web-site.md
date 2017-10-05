---
title: "Aplicación web Node.js utilizando el servicio Tabla de Azure"
description: "Este tutorial le enseña a usar el servicio Tabla de Azure para almacenar datos desde una aplicación Node.js hospedada en Aplicaciones web del Servicio de aplicaciones de Azure."
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
ms.openlocfilehash: 3252914934c1084a165fa39ee983d3039e04d567
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="nodejs-web-app-using-the-azure-table-service"></a><span data-ttu-id="4253d-103">Aplicación web Node.js utilizando el servicio Tabla de Azure</span><span class="sxs-lookup"><span data-stu-id="4253d-103">Node.js web app using the Azure Table Service</span></span>
## <a name="overview"></a><span data-ttu-id="4253d-104">Información general</span><span class="sxs-lookup"><span data-stu-id="4253d-104">Overview</span></span>
<span data-ttu-id="4253d-105">En este tutorial aprenderá a usar Table service que proporciona la administración de datos de Azure para almacenar y tener acceso a los datos desde una aplicación [node] hospedada en [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span><span class="sxs-lookup"><span data-stu-id="4253d-105">This tutorial shows you how to use Table service provided by Azure Data Management to store and access data from a [node] application hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="4253d-106">En este tutorial se asume que tiene alguna experiencia anterior en el uso de Node y [Git].</span><span class="sxs-lookup"><span data-stu-id="4253d-106">This tutorial assumes that you have some prior experience using node and [Git].</span></span>

<span data-ttu-id="4253d-107">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="4253d-107">You will learn:</span></span>

* <span data-ttu-id="4253d-108">Usar npm (administrador de paquetes de Node) para instalar los módulos de Node</span><span class="sxs-lookup"><span data-stu-id="4253d-108">How to use npm (node package manager) to install the node modules</span></span>
* <span data-ttu-id="4253d-109">Trabajar con el servicio Tabla de Azure</span><span class="sxs-lookup"><span data-stu-id="4253d-109">How to work with the Azure Table service</span></span>
* <span data-ttu-id="4253d-110">Uso de la CLI de Azure para crear una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="4253d-110">How to use the Azure CLI to create a web app.</span></span>

<span data-ttu-id="4253d-111">Al seguir este tutorial, podrá compilar una aplicación de "lista de tareas pendientes" basadas en web sencilla que permite crear, recuperar y completar tareas.</span><span class="sxs-lookup"><span data-stu-id="4253d-111">By following this tutorial, you will build a simple web-based "to-do list" application that allows creating, retrieving and completing tasks.</span></span> <span data-ttu-id="4253d-112">Las tareas se almacenan en el servicio Tabla.</span><span class="sxs-lookup"><span data-stu-id="4253d-112">The tasks are stored in the Table service.</span></span>

<span data-ttu-id="4253d-113">Esta es la aplicación completada:</span><span class="sxs-lookup"><span data-stu-id="4253d-113">Here is the completed application:</span></span>

![Página web que muestra una lista de tareas vacía][node-table-finished]

> [!NOTE]
> <span data-ttu-id="4253d-115">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de suscribirse para abrir una cuenta de Azure, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4253d-115">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="4253d-116">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="4253d-116">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="4253d-117">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4253d-117">Prerequisites</span></span>
<span data-ttu-id="4253d-118">Antes de seguir las instrucciones del presente artículo, asegúrese de tener instalados los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="4253d-118">Before following the instructions in this article, ensure that you have the following installed:</span></span>

* <span data-ttu-id="4253d-119">[node] versión 0.10.24 o superior</span><span class="sxs-lookup"><span data-stu-id="4253d-119">[node] version 0.10.24 or higher</span></span>
* <span data-ttu-id="4253d-120">[Git]</span><span class="sxs-lookup"><span data-stu-id="4253d-120">[Git]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a><span data-ttu-id="4253d-121">Crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="4253d-121">Create a storage account</span></span>
<span data-ttu-id="4253d-122">Cree una cuenta de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="4253d-122">Create an Azure storage account.</span></span> <span data-ttu-id="4253d-123">La aplicación usará esta cuenta para almacenar los elementos de tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="4253d-123">The app will use this account to store the to-do items.</span></span>

1. <span data-ttu-id="4253d-124">Inicie sesión en el [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4253d-124">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4253d-125">Haga clic en el icono **Nuevo** situado en la parte inferior izquierda del portal y haga clic en **Datos y almacenamiento** > **Almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="4253d-125">Click the **New** icon on the bottom left of the portal, then click **Data + Storage** > **Storage**.</span></span> <span data-ttu-id="4253d-126">Asigne un nombre único a la cuenta de almacenamiento y cree un [grupo de recursos](../azure-resource-manager/resource-group-overview.md) nuevo para ella.</span><span class="sxs-lookup"><span data-stu-id="4253d-126">Give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Botón Nuevo](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    <span data-ttu-id="4253d-128">Una vez creada la cuenta de almacenamiento, el botón **Notificaciones** emitirá el mensaje **CORRECTO** en color verde y la hoja de la cuenta de almacenamiento se abrirá para mostrar que pertenece al nuevo grupo de recursos que ha creado.</span><span class="sxs-lookup"><span data-stu-id="4253d-128">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span></span>
3. <span data-ttu-id="4253d-129">En la hoja de la cuenta de almacenamiento, haga clic en **Configuración** > **Claves**.</span><span class="sxs-lookup"><span data-stu-id="4253d-129">In the storage account's blade, click **Settings** > **Keys**.</span></span> <span data-ttu-id="4253d-130">Copie la clave de acceso principal en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="4253d-130">Copy the primary access key to the clipboard.</span></span>
   
    ![Clave de acceso][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a><span data-ttu-id="4253d-132">Instalación de módulos y generación de scaffolding</span><span class="sxs-lookup"><span data-stu-id="4253d-132">Install modules and generate scaffolding</span></span>
<span data-ttu-id="4253d-133">En esta sección podrá crear una nueva aplicación Node y usar npm para agregar paquetes de módulos.</span><span class="sxs-lookup"><span data-stu-id="4253d-133">In this section you will create a new Node application and use npm to add module packages.</span></span> <span data-ttu-id="4253d-134">Para esta aplicación, usará los módulos [Express] y [Azure].</span><span class="sxs-lookup"><span data-stu-id="4253d-134">For this application you will use the [Express] and [Azure] modules.</span></span> <span data-ttu-id="4253d-135">El módulo Express proporciona un marco de controlador de vista de modelo para Node, mientras que los módulos de Azure proporcionan conectividad al servicio Tabla.</span><span class="sxs-lookup"><span data-stu-id="4253d-135">The Express module provides a Model View Controller framework for node, while the Azure modules provides connectivity to the Table service.</span></span>

### <a name="install-express-and-generate-scaffolding"></a><span data-ttu-id="4253d-136">Instalar Express y generar scaffolding</span><span class="sxs-lookup"><span data-stu-id="4253d-136">Install express and generate scaffolding</span></span>
1. <span data-ttu-id="4253d-137">Desde la línea de comandos, cree un nuevo directorio denominado **tasklist** y cambie a ese directorio.</span><span class="sxs-lookup"><span data-stu-id="4253d-137">From the command line, create a new directory named **tasklist** and switch to that directory.</span></span>  
2. <span data-ttu-id="4253d-138">Escriba el siguiente comando para instalar el módulo Express.</span><span class="sxs-lookup"><span data-stu-id="4253d-138">Enter the following command to install the Express module.</span></span>
   
        npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="4253d-139">En función del sistema operativo, puede ser necesario poner 'sudo' antes del comando:</span><span class="sxs-lookup"><span data-stu-id="4253d-139">Depending on the operating system, you may need to put 'sudo' before the command:</span></span>
   
        sudo npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="4253d-140">El resultado es similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4253d-140">The output appears similar to the following example:</span></span>
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > <span data-ttu-id="4253d-141">El parámetro '-g' instala el módulo globalmente.</span><span class="sxs-lookup"><span data-stu-id="4253d-141">The '-g' parameter installs the module globally.</span></span> <span data-ttu-id="4253d-142">De este modo, podemos utilizar **express** para generar el scaffolding de la aplicación web sin tener que escribir información de ruta adicional.</span><span class="sxs-lookup"><span data-stu-id="4253d-142">That way, we can use **express** to generate web app scaffolding without having to type in additional path information.</span></span>
   > 
   > 
3. <span data-ttu-id="4253d-143">Para crear el scaffolding para la aplicación, escriba el comando **express** :</span><span class="sxs-lookup"><span data-stu-id="4253d-143">To create the scaffolding for the application, enter the **express** command:</span></span>
   
        express
   
    <span data-ttu-id="4253d-144">El resultado de este comando es similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4253d-144">The output of this command appears similar to the following example:</span></span>
   
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
   
           run the app:
             $ DEBUG=my-application ./bin/www
   
    <span data-ttu-id="4253d-145">Ahora debe tener varios directorios y archivos nuevos en el directorio **tasklist** .</span><span class="sxs-lookup"><span data-stu-id="4253d-145">You now have several new directories and files in the **tasklist** directory.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="4253d-146">Instalar módulos adicionales</span><span class="sxs-lookup"><span data-stu-id="4253d-146">Install additional modules</span></span>
<span data-ttu-id="4253d-147">Uno de los archivos que crea **express** es **package.json**.</span><span class="sxs-lookup"><span data-stu-id="4253d-147">One of the files that **express** creates is **package.json**.</span></span> <span data-ttu-id="4253d-148">Este archivo contiene una lista de dependencias de módulo.</span><span class="sxs-lookup"><span data-stu-id="4253d-148">This file contains a list of module dependencies.</span></span> <span data-ttu-id="4253d-149">Posteriormente, cuando implemente esta aplicación en Aplicaciones web del Servicio de aplicaciones, este archivo determinará los módulos que se deben instalar en Azure.</span><span class="sxs-lookup"><span data-stu-id="4253d-149">Later, when you deploy the application to App Service Web Apps, this file determines which modules need to be installed on Azure.</span></span>

<span data-ttu-id="4253d-150">En la línea de comandos, escriba el siguiente comando para instalar los módulos que se describen en el archivo **package.json**.</span><span class="sxs-lookup"><span data-stu-id="4253d-150">From the command-line, enter the following command to install the modules described in the **package.json** file.</span></span> <span data-ttu-id="4253d-151">Puede que necesite usar 'sudo'.</span><span class="sxs-lookup"><span data-stu-id="4253d-151">You may need to use 'sudo'.</span></span>

    npm install

<span data-ttu-id="4253d-152">El resultado de este comando es similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4253d-152">The output of this command appears similar to the following example:</span></span>

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


<span data-ttu-id="4253d-153">A continuación, escriba el siguiente comando para instalar los módulos [azure], [node-uuid], [nconf] y [async]:</span><span class="sxs-lookup"><span data-stu-id="4253d-153">Next, enter the following command to install the [azure], [node-uuid], [nconf] and [async] modules:</span></span>

    npm install azure-storage node-uuid async nconf --save

<span data-ttu-id="4253d-154">La marca **--save** agrega entradas para estos módulos en el archivo **package.json**.</span><span class="sxs-lookup"><span data-stu-id="4253d-154">The **--save** flag adds entries for these modules to the **package.json** file.</span></span>

<span data-ttu-id="4253d-155">El resultado de este comando es similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4253d-155">The output of this command appears similar to the following example:</span></span>

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-the-application"></a><span data-ttu-id="4253d-156">Creación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="4253d-156">Create the application</span></span>
<span data-ttu-id="4253d-157">Ahora estamos listos para compilar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4253d-157">Now we're ready to build the application.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="4253d-158">Crear un modelo</span><span class="sxs-lookup"><span data-stu-id="4253d-158">Create a model</span></span>
<span data-ttu-id="4253d-159">Un *modelo* es un objeto que representa los datos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4253d-159">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="4253d-160">Para la aplicación, el modelo solo es un objeto de tarea, que representa un elemento en la lista de tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="4253d-160">For the application, the only model is a task object, which represents an item in the to-do list.</span></span> <span data-ttu-id="4253d-161">Las tareas tienen los siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="4253d-161">Tasks will have the following fields:</span></span>

* <span data-ttu-id="4253d-162">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="4253d-162">PartitionKey</span></span>
* <span data-ttu-id="4253d-163">RowKey</span><span class="sxs-lookup"><span data-stu-id="4253d-163">RowKey</span></span>
* <span data-ttu-id="4253d-164">name (string)</span><span class="sxs-lookup"><span data-stu-id="4253d-164">name (string)</span></span>
* <span data-ttu-id="4253d-165">category (string)</span><span class="sxs-lookup"><span data-stu-id="4253d-165">category (string)</span></span>
* <span data-ttu-id="4253d-166">completed (Boolean)</span><span class="sxs-lookup"><span data-stu-id="4253d-166">completed (Boolean)</span></span>

<span data-ttu-id="4253d-167">Table service usa **PartitionKey** y **RowKey** como claves de tabla.</span><span class="sxs-lookup"><span data-stu-id="4253d-167">**PartitionKey** and **RowKey** are used by the Table Service as table keys.</span></span> <span data-ttu-id="4253d-168">Para obtener más información, consulte [Introducción al modelo de datos del servicio Tabla](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="4253d-168">For more information, see [Understanding the Table Service data model](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

1. <span data-ttu-id="4253d-169">En el directorio **tasklist**, cree un directorio nuevo con el nombre **models**.</span><span class="sxs-lookup"><span data-stu-id="4253d-169">In the **tasklist** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="4253d-170">En el directorio **models**, cree un archivo nuevo con el nombre **task.js**.</span><span class="sxs-lookup"><span data-stu-id="4253d-170">In the **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="4253d-171">Este archivo contendrá el modelo para las tareas que se crean con su aplicación.</span><span class="sxs-lookup"><span data-stu-id="4253d-171">This file will contain the model for the tasks created by your application.</span></span>
3. <span data-ttu-id="4253d-172">Al comienzo del archivo **task.js** , agregue el siguiente código para hacer referencia a las bibliotecas requeridas:</span><span class="sxs-lookup"><span data-stu-id="4253d-172">At the beginning of the **task.js** file, add the following code to reference required libraries:</span></span>
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. <span data-ttu-id="4253d-173">Agregue el código siguiente para definir y exportar el objeto Task.</span><span class="sxs-lookup"><span data-stu-id="4253d-173">Add the following code to define and export the Task object.</span></span> <span data-ttu-id="4253d-174">Este objeto es el responsable de la conexión a la tabla.</span><span class="sxs-lookup"><span data-stu-id="4253d-174">This object is responsible for connecting to the table.</span></span>
   
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
5. <span data-ttu-id="4253d-175">Agregue el siguiente código para definir métodos adicionales en el objeto Task, que permite interacciones con los datos almacenados en la tabla:</span><span class="sxs-lookup"><span data-stu-id="4253d-175">Add the following code to define additional methods on the Task object, which allow interactions with data stored in the table:</span></span>
   
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
            // use entityGenerator to set types
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
6. <span data-ttu-id="4253d-176">Guarde y cierre el archivo **task.js** .</span><span class="sxs-lookup"><span data-stu-id="4253d-176">Save and close the **task.js** file.</span></span>

### <a name="create-a-controller"></a><span data-ttu-id="4253d-177">Creación de un controlador</span><span class="sxs-lookup"><span data-stu-id="4253d-177">Create a controller</span></span>
<span data-ttu-id="4253d-178">Un *controlador* administra las solicitudes HTTP y procesa la respuesta HTML.</span><span class="sxs-lookup"><span data-stu-id="4253d-178">A *controller* handles HTTP requests and renders the HTML response.</span></span>

1. <span data-ttu-id="4253d-179">En el directorio **tasklist/routes**, cree un archivo nuevo con el nombre **tasklist.js** y ábralo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="4253d-179">In the **tasklist/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="4253d-180">Agregue el siguiente código a **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="4253d-180">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="4253d-181">De este modo se cargan los módulos azure y async, que utiliza **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="4253d-181">This loads the azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="4253d-182">También define la función **TaskList**, que pasa a una instancia del objeto **Task** que definimos anteriormente:</span><span class="sxs-lookup"><span data-stu-id="4253d-182">This also defines the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. <span data-ttu-id="4253d-183">Defina un objeto **TaskList** .</span><span class="sxs-lookup"><span data-stu-id="4253d-183">Define a **TaskList** object.</span></span>
   
        function TaskList(task) {
          this.task = task;
        }
4. <span data-ttu-id="4253d-184">Agregue los siguientes métodos a **TaskList**:</span><span class="sxs-lookup"><span data-stu-id="4253d-184">Add the following methods to **TaskList**:</span></span>
   
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

### <a name="modify-appjs"></a><span data-ttu-id="4253d-185">Modificar app.js</span><span class="sxs-lookup"><span data-stu-id="4253d-185">Modify app.js</span></span>
1. <span data-ttu-id="4253d-186">En el directorio **tasklist**, abra el archivo **app.js**.</span><span class="sxs-lookup"><span data-stu-id="4253d-186">From the **tasklist** directory, open the **app.js** file.</span></span> <span data-ttu-id="4253d-187">Este archivo se creó anteriormente al ejecutar el comando **express** .</span><span class="sxs-lookup"><span data-stu-id="4253d-187">This file was created earlier by running the **express** command.</span></span>
2. <span data-ttu-id="4253d-188">Al principio del archivo, agregue lo siguiente para cargar el módulo azure, configurar el nombre de la tabla, la clave de partición y las credenciales de almacenamiento utilizadas en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4253d-188">At the beginning of the file, add the following to load the azure module, set the table name, partition key, and set the storage credentials used by this example:</span></span>
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > <span data-ttu-id="4253d-189">nconf cargará los valores de configuración desde las variables de entorno o el archivo **config.json** , que crearemos más adelante.</span><span class="sxs-lookup"><span data-stu-id="4253d-189">nconf will load the configuration values from either environment variables or the **config.json** file, which we will create later.</span></span>
   > 
   > 
3. <span data-ttu-id="4253d-190">En el archivo app.js, desplácese hacia abajo hasta ver la siguiente línea:</span><span class="sxs-lookup"><span data-stu-id="4253d-190">In the app.js file, scroll down to where you see the following line:</span></span>
   
        app.use('/', routes);
        app.use('/users', users);
   
    <span data-ttu-id="4253d-191">Sustituya las líneas anteriores por el código que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="4253d-191">Replace the above lines with the code shown below.</span></span> <span data-ttu-id="4253d-192">De este modo se inicializará una instancia de <strong>Task</strong> con una conexión a su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4253d-192">This will initialize an instance of <strong>Task</strong> with a connection to your storage account.</span></span> <span data-ttu-id="4253d-193">Esto se pasa a la <strong>TaskList</strong>, que lo utilizará para comunicarse con el servicio Tabla:</span><span class="sxs-lookup"><span data-stu-id="4253d-193">This is passed to the <strong>TaskList</strong>, which will use it to communicate with the Table service:</span></span>
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. <span data-ttu-id="4253d-194">Guarde el archivo **app.js** .</span><span class="sxs-lookup"><span data-stu-id="4253d-194">Save the **app.js** file.</span></span>

### <a name="modify-the-index-view"></a><span data-ttu-id="4253d-195">Modificar la vista de índice</span><span class="sxs-lookup"><span data-stu-id="4253d-195">Modify the index view</span></span>
1. <span data-ttu-id="4253d-196">Abra el archivo **tasklist/views/index.jade** en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="4253d-196">Open the **tasklist/views/index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="4253d-197">Reemplace todo el contenido del archivo con el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="4253d-197">Replace the entire contents of the file with the following code.</span></span> <span data-ttu-id="4253d-198">De esta manera se define una vista para mostrar las tareas existentes y se incluye un formulario para agregar tareas nuevas y marcar las existentes como terminadas.</span><span class="sxs-lookup"><span data-stu-id="4253d-198">This defines a view that displays existing tasks and includes a form for adding new tasks and marking existing ones as completed.</span></span>
   
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
3. <span data-ttu-id="4253d-199">Guarde y cierre el archivo **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="4253d-199">Save and close **index.jade** file.</span></span>

### <a name="modify-the-global-layout"></a><span data-ttu-id="4253d-200">Modificar el diseño global</span><span class="sxs-lookup"><span data-stu-id="4253d-200">Modify the global layout</span></span>
<span data-ttu-id="4253d-201">El archivo **layout.jade** del directorio **views** es una plantilla global para otros archivos **.jade**.</span><span class="sxs-lookup"><span data-stu-id="4253d-201">The **layout.jade** file in the **views** directory is a global template for other **.jade** files.</span></span> <span data-ttu-id="4253d-202">En este paso podrá modificarlo para utilizar [Twitter Bootstrap](https://github.com/twbs/bootstrap), un kit de herramientas que facilita el diseño de una aplicación web atractiva.</span><span class="sxs-lookup"><span data-stu-id="4253d-202">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking web app.</span></span>

<span data-ttu-id="4253d-203">Descargue y extraiga los archivos para [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="4253d-203">Download and extract the files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="4253d-204">Copie el archivo **bootstrap.min.css** desde la carpeta Bootstrap **css** al directorio **public\stylesheets** de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="4253d-204">Copy the **bootstrap.min.css** file from the Bootstrap **css** folder into the **public/stylesheets** directory of your application.</span></span>

<span data-ttu-id="4253d-205">En la carpeta **views**, abra **layout.jade** y reemplace todo el contenido por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4253d-205">From the **views** folder, open **layout.jade** and replace the entire contents with the following:</span></span>

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

### <a name="create-a-config-file"></a><span data-ttu-id="4253d-206">Creación de un archivo de configuración</span><span class="sxs-lookup"><span data-stu-id="4253d-206">Create a config file</span></span>
<span data-ttu-id="4253d-207">Para ejecutar la aplicación localmente, pondremos credenciales de Almacenamiento de Azure en un archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="4253d-207">To run the app locally, we'll put Azure Storage credentials into a config file.</span></span> <span data-ttu-id="4253d-208">Cree un archivo denominado **config.json** con el siguiente código JSON:</span><span class="sxs-lookup"><span data-stu-id="4253d-208">Create a file named **config.json* *with the following JSON:</span></span>

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="4253d-209">Reemplace **nombre de cuenta de almacenamiento** por el nombre de la cuenta de almacenamiento creada anteriormente y **clave de acceso de almacenamiento** por la clave de acceso principal de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4253d-209">Replace **storage account name** with the name of the storage account you created earlier, and replace **storage access key** with the primary access key for your storage account.</span></span> <span data-ttu-id="4253d-210">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4253d-210">For example:</span></span>

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="4253d-211">Guarde este archivo en *un nivel de directorio más alto* que el directorio **tasklist** , similar a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4253d-211">Save this file *one directory level higher* than the **tasklist** directory, like this:</span></span>

    parent/
      |-- config.json
      |-- tasklist/

<span data-ttu-id="4253d-212">La razón para hacer esto es evitar la comprobación del archivo de configuración en el control de código fuente, donde puede ser público.</span><span class="sxs-lookup"><span data-stu-id="4253d-212">The reason for doing this is to avoid checking the config file into source control, where it might become public.</span></span> <span data-ttu-id="4253d-213">Cuando se implementa la aplicación en Azure, usaremos las variables de entorno en lugar de un archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="4253d-213">When we deploy the app to Azure, we will use environment variables instead of a config file.</span></span>

## <a name="run-the-application-locally"></a><span data-ttu-id="4253d-214">Ejecución de la aplicación de forma local</span><span class="sxs-lookup"><span data-stu-id="4253d-214">Run the application locally</span></span>
<span data-ttu-id="4253d-215">Lleve a cabo los siguientes pasos para probar la aplicación en su máquina local:</span><span class="sxs-lookup"><span data-stu-id="4253d-215">To test the application on your local machine, perform the following steps:</span></span>

1. <span data-ttu-id="4253d-216">En la línea de comandos, cambie de directorio al directorio **tasklist** .</span><span class="sxs-lookup"><span data-stu-id="4253d-216">From the command-line, change directories to the **tasklist** directory.</span></span>
2. <span data-ttu-id="4253d-217">Utilice el siguiente comando para iniciar localmente la aplicación:</span><span class="sxs-lookup"><span data-stu-id="4253d-217">Use the following command to launch the application locally:</span></span>
   
        npm start
3. <span data-ttu-id="4253d-218">Abra el explorador y navegue a http://127.0.0.1:3000.</span><span class="sxs-lookup"><span data-stu-id="4253d-218">Open a web browser and navigate to http://127.0.0.1:3000.</span></span>
   
    <span data-ttu-id="4253d-219">Aparecerá una página web similar a la del ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="4253d-219">A web page similar to the following example appears.</span></span>
   
    ![Página web que muestra una lista de tareas vacía][node-table-finished]
4. <span data-ttu-id="4253d-221">Para crear un nuevo elemento de tarea pendiente, escriba un nombre y una categoría y haga clic en **Agregar elemento**.</span><span class="sxs-lookup"><span data-stu-id="4253d-221">To create a new to-do item, enter a name and category and click **Add Item**.</span></span> 
5. <span data-ttu-id="4253d-222">Para marcar una tarea como completa, marque **Completado** y haga clic en **Actualizar tareas**.</span><span class="sxs-lookup"><span data-stu-id="4253d-222">To mark a task as complete, check **Complete** and click **Update Tasks**.</span></span>
   
    ![Imagen del elemento nuevo en la lista de tareas][node-table-list-items]

<span data-ttu-id="4253d-224">Aunque la aplicación se ejecuta localmente, almacena los datos en el servicio Tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="4253d-224">Even though the application is running locally, it is storing the data in the Azure Table service.</span></span>

## <a name="deploy-your-application-to-azure"></a><span data-ttu-id="4253d-225">Implementación de su aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="4253d-225">Deploy your application to Azure</span></span>
<span data-ttu-id="4253d-226">En los pasos de esta sección se usan las herramientas de línea de comandos de Azure para crear una nueva aplicación web en el Servicio de aplicaciones y después implementar la aplicación mediante Git.</span><span class="sxs-lookup"><span data-stu-id="4253d-226">The steps in this section use the Azure command-line tools to create a new web app in App Service, and then use Git to deploy your application.</span></span> <span data-ttu-id="4253d-227">Para realizar estos pasos debe tener una suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="4253d-227">To perform these steps you must have an Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="4253d-228">Estos pasos también pueden llevarse a cabo usando el [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4253d-228">These steps can also be performed by using the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="4253d-229">Consulte [Compilación e implementación de una aplicación web de Node.js en el Servicio de aplicaciones de Azure].</span><span class="sxs-lookup"><span data-stu-id="4253d-229">See [Build and deploy a Node.js web app in Azure App Service].</span></span>
> 
> <span data-ttu-id="4253d-230">Si esta es la primera aplicación web que crea, debe usar el Portal de Azure para implementarla.</span><span class="sxs-lookup"><span data-stu-id="4253d-230">If this is the first web app you have created, you must use the Azure Portal to deploy this application.</span></span>
> 
> 

<span data-ttu-id="4253d-231">Para empezar, instale la [CLI de Azure] escribiendo el siguiente comando desde la línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="4253d-231">To get started, install the [Azure CLI] by entering the following command from the command line:</span></span>

    npm install azure-cli -g

### <a name="import-publishing-settings"></a><span data-ttu-id="4253d-232">Importación de la configuración de publicación</span><span class="sxs-lookup"><span data-stu-id="4253d-232">Import publishing settings</span></span>
<span data-ttu-id="4253d-233">En este paso, descargará un archivo que contiene información acerca de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="4253d-233">In this step, you will download a file containing information about your subscription.</span></span>

1. <span data-ttu-id="4253d-234">Escriba el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="4253d-234">Enter the following command:</span></span>
   
        azure login
   
    <span data-ttu-id="4253d-235">Este comando inicia un explorador y se desplaza a la página de descarga.</span><span class="sxs-lookup"><span data-stu-id="4253d-235">This command launches a browser and navigates to the download page.</span></span> <span data-ttu-id="4253d-236">Si se le solicita, inicie sesión con la cuenta asociada a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4253d-236">If prompted, log in with the account associated with your Azure subscription.</span></span>
   
    <!-- ![The download page][download-publishing-settings] -->
   
    <span data-ttu-id="4253d-237">La descarga del archivo se inicia automáticamente; si esto no ocurre, puede hacer clic en el vínculo al comienzo de la página para descargar el archivo manualmente.</span><span class="sxs-lookup"><span data-stu-id="4253d-237">The file download begins automatically; if it does not, you can click the link at the beginning of the page to manually download the file.</span></span> <span data-ttu-id="4253d-238">Guarde el archivo y anote la ruta de acceso del archivo.</span><span class="sxs-lookup"><span data-stu-id="4253d-238">Save the file and note the file path.</span></span>
2. <span data-ttu-id="4253d-239">Escriba el siguiente comando para importar la configuración.</span><span class="sxs-lookup"><span data-stu-id="4253d-239">Enter the following command to import the settings:</span></span>
   
        azure account import <path-to-file>
   
    <span data-ttu-id="4253d-240">Especifique la ruta y el nombre de archivo del archivo de configuración de publicación que descargó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="4253d-240">Specify the path and file name of the publishing settings file you downloaded in the previous step.</span></span>
3. <span data-ttu-id="4253d-241">Después de importar la configuración, elimine el archivo de configuración de publicación.</span><span class="sxs-lookup"><span data-stu-id="4253d-241">After the settings are imported, delete the publish settings file.</span></span> <span data-ttu-id="4253d-242">Ya no es necesario y contiene información confidencial relacionada con su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4253d-242">It is no longer needed, and contains sensitive information regarding your Azure subscription.</span></span>

### <a name="create-an-app-service-web-app"></a><span data-ttu-id="4253d-243">Crear una aplicación web del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="4253d-243">Create an App Service web app</span></span>
1. <span data-ttu-id="4253d-244">En la línea de comandos, cambie de directorio al directorio **tasklist** .</span><span class="sxs-lookup"><span data-stu-id="4253d-244">From the command-line, change directories to the **tasklist** directory.</span></span>
2. <span data-ttu-id="4253d-245">Utilice el comando siguiente para crear una nueva aplicación web.</span><span class="sxs-lookup"><span data-stu-id="4253d-245">Use the following command to create a new web app.</span></span>
   
        azure site create --git
   
    <span data-ttu-id="4253d-246">Se le pedirá que especifique el nombre de la aplicación web y la ubicación.</span><span class="sxs-lookup"><span data-stu-id="4253d-246">You will be prompted for the web app name and location.</span></span> <span data-ttu-id="4253d-247">Proporcione un nombre único y seleccione la misma ubicación geográfica que la cuenta de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="4253d-247">Provide a unique name and select the same geographical location as your Azure Storage account.</span></span>
   
    <span data-ttu-id="4253d-248">El parámetro `--git` crea un repositorio Git en Azure para esta aplicación web.</span><span class="sxs-lookup"><span data-stu-id="4253d-248">The `--git` parameter creates a Git repository on Azure for this web app.</span></span> <span data-ttu-id="4253d-249">También inicializa un repositorio Git en el directorio actual si no existe y agrega un [Git remoto] denominado 'azure', que se usa para publicar la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="4253d-249">It also initializes a Git repository in the current directory if none exists, and adds a [Git remote] named 'azure', which is used to publish the application to Azure.</span></span> <span data-ttu-id="4253d-250">Finalmente, crea un archivo **web.config** , que contiene la configuración usada por Azure para hospedar aplicaciones Node.</span><span class="sxs-lookup"><span data-stu-id="4253d-250">Finally, it creates a **web.config** file, which contains settings used by Azure to host node applications.</span></span> <span data-ttu-id="4253d-251">Si se omite el parámetro `--git` , pero el directorio contiene un repositorio de Git, el comando creará el “azure” remoto.</span><span class="sxs-lookup"><span data-stu-id="4253d-251">If you omit the `--git` parameter but the directory contains a Git repository, the command will still create the 'azure' remote.</span></span>
   
    <span data-ttu-id="4253d-252">Después de que este comando se haya completado, verá un resultado similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="4253d-252">Once this command has completed, you will see output similar to the following.</span></span> <span data-ttu-id="4253d-253">Observe que la línea que comienza por **Website created at** contiene la dirección URL de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="4253d-253">Note that the line beginning with **Website created at** contains the URL for the web app.</span></span>
   
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
   > <span data-ttu-id="4253d-254">Si esta es la primera aplicación web del Servicio de aplicaciones de su suscripción, se le pedirá que use el Portal de Azure para crear la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="4253d-254">If this is the first App Service web app for your subscription, you will be instructed to use the Azure Portal to create the web app.</span></span> <span data-ttu-id="4253d-255">Para obtener más información, consulte [Compilación e implementación de una aplicación web de Node.js en el Servicio de aplicaciones de Azure].</span><span class="sxs-lookup"><span data-stu-id="4253d-255">For more information, see [Build and deploy a Node.js web app in Azure App Service].</span></span>
   > 
   > 

### <a name="set-environment-variables"></a><span data-ttu-id="4253d-256">Establecimiento de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="4253d-256">Set environment variables</span></span>
<span data-ttu-id="4253d-257">En este paso, agregará las variables de entorno a la configuración de la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="4253d-257">In this step, you will add environment variables to your web app configuration on Azure.</span></span>
<span data-ttu-id="4253d-258">En la línea de comandos, escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4253d-258">From the command line, enter the following:</span></span>

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


<span data-ttu-id="4253d-259">Reemplace **<storage account name>** por el nombre de la cuenta de almacenamiento creada anteriormente y **<storage access key>** por la clave de acceso principal para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4253d-259">Replace **<storage account name>** with the name of the storage account you created earlier, and replace **<storage access key>** with the primary access key for your storage account.</span></span> <span data-ttu-id="4253d-260">(Utilice los mismos valores que el archivo config.json que creó anteriormente).</span><span class="sxs-lookup"><span data-stu-id="4253d-260">(Use the same values as the config.json file that you created earlier.)</span></span>

<span data-ttu-id="4253d-261">También puede establecer las variables de entorno en el [Azure Portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="4253d-261">Alternatively, you can set environment variables in the [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="4253d-262">Abra la hoja de la aplicación web haciendo clic en **Examinar** > **Web Apps** > el nombre de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="4253d-262">Open the web app's blade by clicking **Browse** > **Web Apps** > your web app name.</span></span>
2. <span data-ttu-id="4253d-263">En la hoja de la aplicación web, haga clic en **All Settings** (Toda la configuración)  > **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="4253d-263">In your web app's blade, click **All Settings** > **Application Settings**.</span></span>
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. <span data-ttu-id="4253d-264">Desplácese hacia abajo hasta la sección **Configuración de la aplicación** y agregue los pares clave/valor.</span><span class="sxs-lookup"><span data-stu-id="4253d-264">Scroll down to the **App settings** section and add the key/value pairs.</span></span>
   
     ![Configuración de la aplicación](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. <span data-ttu-id="4253d-266">Haga clic en **GUARDAR**.</span><span class="sxs-lookup"><span data-stu-id="4253d-266">Click **SAVE**.</span></span>

### <a name="publish-the-application"></a><span data-ttu-id="4253d-267">Publicación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="4253d-267">Publish the application</span></span>
<span data-ttu-id="4253d-268">Para publicar la aplicación, confirme los archivos de código en Git y, a continuación, inserte en azure/master.</span><span class="sxs-lookup"><span data-stu-id="4253d-268">To publish the app, commit the code files to Git and then push to azure/master.</span></span>

1. <span data-ttu-id="4253d-269">Restablezca las credenciales de implementación.</span><span class="sxs-lookup"><span data-stu-id="4253d-269">Set your deployment credentials.</span></span>
   
        azure site deployment user set <name> <password>
2. <span data-ttu-id="4253d-270">Agregue y confirme los archivos de aplicación.</span><span class="sxs-lookup"><span data-stu-id="4253d-270">Add and commit your application files.</span></span>
   
        git add .
        git commit -m "adding files"
3. <span data-ttu-id="4253d-271">Inserte la confirmación en la aplicación web del Servicio de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="4253d-271">Push the commit to the App Service web app:</span></span>
   
        git push azure master
   
    <span data-ttu-id="4253d-272">Utilice **master** como bifurcación de destino.</span><span class="sxs-lookup"><span data-stu-id="4253d-272">Use **master** as the target branch.</span></span> <span data-ttu-id="4253d-273">Al final de la implementación se verá una instrucción similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="4253d-273">At the end of the deployment, you see a statement similar to the following example:</span></span>
   
        To https://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. <span data-ttu-id="4253d-274">Después de que se haya completado la operación de inserción, diríjase a la URL de la aplicación web que se devolvió anteriormente usando el comando `azure create site` para ver su aplicación.</span><span class="sxs-lookup"><span data-stu-id="4253d-274">Once the push operation has completed, browse to the web app URL returned previously by the `azure create site` command to view your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4253d-275">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4253d-275">Next steps</span></span>
<span data-ttu-id="4253d-276">Si bien los pasos de este artículo describen el uso de Tabla service para almacenar información, puede también usar [MongoDB](https://mlab.com/azure/).</span><span class="sxs-lookup"><span data-stu-id="4253d-276">While the steps in this article describe using the Table Service to store information, you can also use [MongoDB](https://mlab.com/azure/).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4253d-277">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="4253d-277">Additional resources</span></span>
<span data-ttu-id="4253d-278">[CLI de Azure]</span><span class="sxs-lookup"><span data-stu-id="4253d-278">[Azure CLI]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="4253d-279">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="4253d-279">What's changed</span></span>
* <span data-ttu-id="4253d-280">Para obtener una guía del cambio de Sitios web a Servicio de aplicaciones, consulte: [Servicio de aplicaciones de Azure y su impacto en los servicios de Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="4253d-280">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- URLs -->

<span data-ttu-id="4253d-281">[Compilación e implementación de una aplicación web de Node.js en el Servicio de aplicaciones de Azure]: app-service-web-get-started-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="4253d-281">[Build and deploy a Node.js web app in Azure App Service]: app-service-web-get-started-nodejs.md</span></span>
[Azure Developer Center]: /develop/nodejs/

<span data-ttu-id="4253d-282">[node]: http://nodejs.org</span><span class="sxs-lookup"><span data-stu-id="4253d-282">[node]: http://nodejs.org</span></span>
<span data-ttu-id="4253d-283">[Git]: http://git-scm.com</span><span class="sxs-lookup"><span data-stu-id="4253d-283">[Git]: http://git-scm.com</span></span>
<span data-ttu-id="4253d-284">[Express]: http://expressjs.com</span><span class="sxs-lookup"><span data-stu-id="4253d-284">[Express]: http://expressjs.com</span></span>
[for free]: http://windowsazure.com
<span data-ttu-id="4253d-285">[Git remoto]: http://git-scm.com/docs/git-remote</span><span class="sxs-lookup"><span data-stu-id="4253d-285">[Git remote]: http://git-scm.com/docs/git-remote</span></span>

<span data-ttu-id="4253d-286">[CLI de Azure]:../cli-install-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="4253d-286">[Azure CLI]:../cli-install-nodejs.md</span></span>

<span data-ttu-id="4253d-287">[azure]: https://github.com/Azure/azure-sdk-for-node</span><span class="sxs-lookup"><span data-stu-id="4253d-287">[azure]: https://github.com/Azure/azure-sdk-for-node</span></span>
<span data-ttu-id="4253d-288">[node-uuid]: https://www.npmjs.com/package/node-uuid</span><span class="sxs-lookup"><span data-stu-id="4253d-288">[node-uuid]: https://www.npmjs.com/package/node-uuid</span></span>
<span data-ttu-id="4253d-289">[nconf]: https://www.npmjs.com/package/nconf</span><span class="sxs-lookup"><span data-stu-id="4253d-289">[nconf]: https://www.npmjs.com/package/nconf</span></span>
<span data-ttu-id="4253d-290">[async]: https://www.npmjs.com/package/async</span><span class="sxs-lookup"><span data-stu-id="4253d-290">[async]: https://www.npmjs.com/package/async</span></span>

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application to an Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
