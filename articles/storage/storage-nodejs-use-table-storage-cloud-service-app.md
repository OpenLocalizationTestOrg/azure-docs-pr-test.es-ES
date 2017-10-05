---
title: "Aplicación web con Table Storage (Node.js) | Microsoft Docs"
description: "Un tutorial que se agrega a la aplicación web con el tutorial Express añadiendo servicios Almacenamiento de Azure y el módulo de Azure."
services: cloud-services, storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e90959a2-4cb2-4b19-9bfb-aede15b18b1c
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 5d7ee2f529b5127ee60ec8b4f5acaa49e75ddf39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="bc944-103">Aplicación web Node.js con almacenamiento</span><span class="sxs-lookup"><span data-stu-id="bc944-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="bc944-104">Información general</span><span class="sxs-lookup"><span data-stu-id="bc944-104">Overview</span></span>
<span data-ttu-id="bc944-105">En este tutorial, podrá ampliar la aplicación creada en el tutorial [Aplicación web Node.js con Express] mediante el uso de las bibliotecas de cliente de Microsoft Azure para Node.js a fin de trabajar con los servicios de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="bc944-105">In this tutorial, you will extend the application created in the [Node.js Web Application using Express] tutorial by using the Microsoft Azure Client Libraries for Node.js to work with data management services.</span></span> <span data-ttu-id="bc944-106">Va a ampliar su aplicación para crear una aplicación de lista de tareas basada en web que se puede implementar en Azure.</span><span class="sxs-lookup"><span data-stu-id="bc944-106">You will extend your application to create a web-based task-list application that you can deploy to Azure.</span></span> <span data-ttu-id="bc944-107">La lista de tareas permite al usuario recuperar tareas, agregar tareas nuevas y marcar tareas como completadas.</span><span class="sxs-lookup"><span data-stu-id="bc944-107">The task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="bc944-108">Los elementos de tarea se almacenan en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="bc944-108">The task items are stored in Azure Storage.</span></span> <span data-ttu-id="bc944-109">El almacenamiento de Azure ofrece almacenamiento de datos no estructurados que es tolerante a errores y tiene una alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="bc944-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="bc944-110">El almacenamiento de Azure incluye varias estructuras de datos donde puede almacenar datos y tener acceso a ellos, además de aprovechar los servicios de almacenamiento de las API que se incluyen en el SDK de Azure para Node.js o mediante las API de REST.</span><span class="sxs-lookup"><span data-stu-id="bc944-110">Azure Storage includes several data structures where you can store and access data, and you can leverage the storage services from the APIs included in the Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="bc944-111">Para más información, consulte [Almacenamiento de Azure].</span><span class="sxs-lookup"><span data-stu-id="bc944-111">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="bc944-112">En este tutorial se supone que ha completado los tutoriales de [Aplicación web Node.js] y [Node.js con Express][Aplicación web Node.js con Express].</span><span class="sxs-lookup"><span data-stu-id="bc944-112">This tutorial assumes that you have completed the [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="bc944-113">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="bc944-113">You will learn:</span></span>

* <span data-ttu-id="bc944-114">Trabajar con el motor de plantillas Jade</span><span class="sxs-lookup"><span data-stu-id="bc944-114">How to work with the Jade template engine</span></span>
* <span data-ttu-id="bc944-115">Trabajar con los servicios de administración de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="bc944-115">How to work with Azure Data Management services</span></span>

<span data-ttu-id="bc944-116">Captura de pantalla de la aplicación completa:</span><span class="sxs-lookup"><span data-stu-id="bc944-116">A screenshot of the completed application is below:</span></span>

![La página web completa en Internet Explorer](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="bc944-118">Establecimiento de las credenciales de almacenamiento en Web.Config</span><span class="sxs-lookup"><span data-stu-id="bc944-118">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="bc944-119">Para tener acceso al almacenamiento de Azure, necesita proporcionar credenciales de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="bc944-119">To access Azure Storage, you need to pass in storage credentials.</span></span> <span data-ttu-id="bc944-120">Para ello, utiliza la configuración de aplicación web.config.</span><span class="sxs-lookup"><span data-stu-id="bc944-120">To do this, you utilize web.config application settings.</span></span>
<span data-ttu-id="bc944-121">Estos ajustes pasarán como variables de entorno a Node, que luego son leídos por el SDK de Azure.</span><span class="sxs-lookup"><span data-stu-id="bc944-121">Those settings will be passed as environment variables to Node, which are then read by the Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="bc944-122">Las credenciales de almacenamiento solo se utilizan cuando la aplicación se implementa en Azure.</span><span class="sxs-lookup"><span data-stu-id="bc944-122">Storage credentials are only used when the application is deployed to Azure.</span></span> <span data-ttu-id="bc944-123">Cuando se ejecuta en el emulador, la aplicación utilizará el emulador de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="bc944-123">When running in the emulator, the application will use the storage emulator.</span></span>
>
>

<span data-ttu-id="bc944-124">Siga estos pasos para recuperar las credenciales de la cuenta de almacenamiento y agregarlas a la configuración de web.config:</span><span class="sxs-lookup"><span data-stu-id="bc944-124">Perform the following steps to retrieve the storage account credentials and add them to the web.config settings:</span></span>

1. <span data-ttu-id="bc944-125">Si aún no está abierto, inicie Azure PowerShell desde el menú **Inicio**, expanda **Todos los programas, Azure**, haga clic con el botón derecho en **Azure PowerShell** y seleccione **Ejecutar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="bc944-125">If it is not already open, start the Azure PowerShell from the **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="bc944-126">Cambie los directorios a la carpeta que contiene la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bc944-126">Change directories to the folder containing your application.</span></span> <span data-ttu-id="bc944-127">Por ejemplo, C:\\nodo\\tasklist\\WebRole1.</span><span class="sxs-lookup"><span data-stu-id="bc944-127">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="bc944-128">Desde la ventana de Azure Powershell escriba el siguiente cmdlet para recuperar la información de la cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="bc944-128">From the Azure Powershell window enter the following cmdlet to retrieve the storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="bc944-129">De esta manera se recupera la lista de cuentas de almacenamiento y las claves de cuentas con el servicio hospedado.</span><span class="sxs-lookup"><span data-stu-id="bc944-129">This retrieves the list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bc944-130">Debido a que el SDK de Azure crea una cuenta de almacenamiento al implementar un servicio, ya debe existir una cuenta de almacenamiento procedente de la implementación de la aplicación en las guías anteriores.</span><span class="sxs-lookup"><span data-stu-id="bc944-130">Since the Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in the previous guides.</span></span>
   >
   >
4. <span data-ttu-id="bc944-131">Abra el archivo **ServiceDefinition.csdef** que contiene la configuración del entorno que se usa cuando la aplicación se implementa en Azure:</span><span class="sxs-lookup"><span data-stu-id="bc944-131">Open the **ServiceDefinition.csdef** file containing the environment settings that are used when the application is deployed to Azure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="bc944-132">Inserte el siguiente bloque bajo el elemento **Environment**, reemplace {STORAGE ACCOUNT} y {STORAGE ACCESS KEY} por el nombre de la cuenta y la clave principal de la cuenta de almacenamiento que desea utilizar para la implementación:</span><span class="sxs-lookup"><span data-stu-id="bc944-132">Insert the following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with the account name and the primary key for the storage account you want to use for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![Contenido del archivo web.cloud.config](./media/storage-nodejs-use-table-storage-cloud-service-app/node37.png)

6. <span data-ttu-id="bc944-134">Guarde el archivo y cierre el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="bc944-134">Save the file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="bc944-135">Instalar módulos adicionales</span><span class="sxs-lookup"><span data-stu-id="bc944-135">Install additional modules</span></span>
1. <span data-ttu-id="bc944-136">Use el comando siguiente para instalar los módulos [azure], [node-uuid], [nconf] y [async] localmente y para guardar una entrada de ellos en el archivo **package.json**:</span><span class="sxs-lookup"><span data-stu-id="bc944-136">Use the following command to install the [azure], [node-uuid], [nconf] and [async] modules locally as well as to save an entry for them to the **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="bc944-137">El resultado de este comando debe ser similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="bc944-137">The output of this command should appear similar to the following:</span></span>

  ```
  node-uuid@1.4.1 node_modules\node-uuid

  nconf@0.6.9 node_modules\nconf
  ├── ini@1.1.0
  ├── async@0.2.9
  └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.8)

  azure-storage@0.1.0 node_modules\azure-storage
  ├── extend@1.2.1
  ├── xmlbuilder@0.4.3
  ├── mime@1.2.11
  ├── underscore@1.4.4
  ├── validator@3.1.0
  ├── node-uuid@1.4.1
  ├── xml2js@0.2.7 (sax@0.5.2)
  └── request@2.27.0 (json-stringify-safe@5.0.0, tunnel-agent@0.3.0, aws-sign@0.3.0, forever-agent@0.5.2, qs@0.6.6, oauth-sign@0.3.0, cookie-jar@0.3.0, hawk@1.0.0, form-data@0.1.3, http-signature@0.10.0)
  ```

## <a name="using-the-table-service-in-a-node-application"></a><span data-ttu-id="bc944-138">Uso del servicio Tabla en una aplicación Node</span><span class="sxs-lookup"><span data-stu-id="bc944-138">Using the Table service in a node application</span></span>
<span data-ttu-id="bc944-139">En esta sección extenderá la aplicación básica creada por el comando **express** agregando un archivo **task.js** que contiene el modelo para sus tareas.</span><span class="sxs-lookup"><span data-stu-id="bc944-139">In this section you will extend the basic application created by the **express** command by adding a **task.js** file which contains the model for your tasks.</span></span> <span data-ttu-id="bc944-140">También podrá modificar el archivo **app.js** existente y crear un archivo **tasklist.js** nuevo que utilice el modelo.</span><span class="sxs-lookup"><span data-stu-id="bc944-140">You will also modify the existing **app.js** and create a new **tasklist.js** file that uses the model.</span></span>

### <a name="create-the-model"></a><span data-ttu-id="bc944-141">Crear el modelo</span><span class="sxs-lookup"><span data-stu-id="bc944-141">Create the model</span></span>
1. <span data-ttu-id="bc944-142">En el directorio **WebRole1**, cree el directorio nuevo con el nombre **models**.</span><span class="sxs-lookup"><span data-stu-id="bc944-142">In the **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="bc944-143">En el directorio **models**, cree un archivo nuevo con el nombre **task.js**.</span><span class="sxs-lookup"><span data-stu-id="bc944-143">In the **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="bc944-144">Este archivo contendrá el modelo para las tareas que se crean con su aplicación.</span><span class="sxs-lookup"><span data-stu-id="bc944-144">This file will contain the model for the tasks created by your application.</span></span>
3. <span data-ttu-id="bc944-145">Al comienzo del archivo **task.js** , agregue el siguiente código para hacer referencia a las bibliotecas requeridas:</span><span class="sxs-lookup"><span data-stu-id="bc944-145">At the beginning of the **task.js** file, add the following code to reference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="bc944-146">A continuación, agregará código para definir y exportar el objeto Task.</span><span class="sxs-lookup"><span data-stu-id="bc944-146">Next, you will add code to define and export the Task object.</span></span> <span data-ttu-id="bc944-147">Este objeto es el responsable de la conexión a la tabla.</span><span class="sxs-lookup"><span data-stu-id="bc944-147">This object is responsible for connecting to the table.</span></span>

    ```nodejs
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
    ```

5. <span data-ttu-id="bc944-148">A continuación, agregue el siguiente código para definir métodos adicionales en el objeto Task, que permite las interacciones con los datos almacenados en la tabla:</span><span class="sxs-lookup"><span data-stu-id="bc944-148">Next, add the following code to define additional methods on the Task object, which allow interactions with data stored in the table:</span></span>

    ```nodejs
    Task.prototype = {
      find: function(query, callback) {
        self = this;
        self.storageClient.queryEntities(query, function entitiesQueried(error, result) {
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
    ```

6. <span data-ttu-id="bc944-149">Guarde y cierre el archivo **task.js** .</span><span class="sxs-lookup"><span data-stu-id="bc944-149">Save and close the **task.js** file.</span></span>

### <a name="create-the-controller"></a><span data-ttu-id="bc944-150">Crear el controlador</span><span class="sxs-lookup"><span data-stu-id="bc944-150">Create the controller</span></span>
1. <span data-ttu-id="bc944-151">En el directorio **WebRole1/routes**, cree un archivo nuevo con el nombre **tasklist.js** y ábralo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="bc944-151">In the **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="bc944-152">Agregue el siguiente código a **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="bc944-152">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="bc944-153">De este modo se cargan los módulos azure y async, que utiliza **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="bc944-153">This loads the azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="bc944-154">También define la función **TaskList**, que pasa a una instancia del objeto **Task** que definimos anteriormente:</span><span class="sxs-lookup"><span data-stu-id="bc944-154">This also defines the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="bc944-155">Continúe agregando al archivo **tasklist.js** los métodos usados para **showTasks**, **addTask** y **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="bc944-155">Continue adding to the **tasklist.js** file by adding the methods used to **showTasks**, **addTask**, and **completeTasks**:</span></span>

    ```nodejs
    TaskList.prototype = {
      showTasks: function(req, res) {
        self = this;
        var query = azure.TableQuery()
          .where('completed eq ?', false);
        self.task.find(query, function itemsFound(error, items) {
          res.render('index',{title: 'My ToDo List ', tasks: items});
        });
      },

      addTask: function(req,res) {
        var self = this
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
    ```

4. <span data-ttu-id="bc944-156">Guarde el archivo **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="bc944-156">Save the **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="bc944-157">Modificar app.js</span><span class="sxs-lookup"><span data-stu-id="bc944-157">Modify app.js</span></span>
1. <span data-ttu-id="bc944-158">En el directorio **WebRole1**, abra el archivo **app.js** en el editor de texto.</span><span class="sxs-lookup"><span data-stu-id="bc944-158">In the **WebRole1** directory, open the **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="bc944-159">Al principio del archivo, agregue lo siguiente para cargar el módulo de Azure y establecer el nombre de tabla y la clave de partición:</span><span class="sxs-lookup"><span data-stu-id="bc944-159">At the beginning of the file, add the following to load the azure module and set the table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="bc944-160">En el archivo app.js, desplácese hacia abajo hasta ver la siguiente línea:</span><span class="sxs-lookup"><span data-stu-id="bc944-160">In the app.js file, scroll down to where you see the following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="bc944-161">Sustituya las líneas anteriores por el código que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="bc944-161">Replace the above lines with the code shown below.</span></span> <span data-ttu-id="bc944-162">De este modo se inicializará una instancia de <strong>Task</strong> con una conexión a su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="bc944-162">This will initialize an instance of <strong>Task</strong> with a connection to your storage account.</span></span> <span data-ttu-id="bc944-163">Esto se pasa a la <strong>TaskList</strong>, que lo utilizará para comunicarse con el servicio Tabla:</span><span class="sxs-lookup"><span data-stu-id="bc944-163">This is passed to the <strong>TaskList</strong>, which will use it to communicate with the Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="bc944-164">Guarde el archivo **app.js** .</span><span class="sxs-lookup"><span data-stu-id="bc944-164">Save the **app.js** file.</span></span>

### <a name="modify-the-index-view"></a><span data-ttu-id="bc944-165">Modificar la vista de índice</span><span class="sxs-lookup"><span data-stu-id="bc944-165">Modify the index view</span></span>
1. <span data-ttu-id="bc944-166">Cambie al directorio **views** y abra el archivo **index.jade** en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="bc944-166">Change directories to the **views** directory and open the **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="bc944-167">Reemplace el contenido del archivo **index.jade** por el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="bc944-167">Replace the contents of the **index.jade** file with the code below.</span></span> <span data-ttu-id="bc944-168">De esta manera se define la vista para mostrar las tareas existentes, además de un formulario para agregar tareas nuevas y marcar las existentes como terminadas.</span><span class="sxs-lookup"><span data-stu-id="bc944-168">This defines the view for displaying existing tasks, as well as a form for adding new tasks and marking existing ones as completed.</span></span>

    ```
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
          if tasks != []
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
    ```

3. <span data-ttu-id="bc944-169">Guarde y cierre el archivo **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="bc944-169">Save and close **index.jade** file.</span></span>

### <a name="modify-the-global-layout"></a><span data-ttu-id="bc944-170">Modificar el diseño global</span><span class="sxs-lookup"><span data-stu-id="bc944-170">Modify the global layout</span></span>
<span data-ttu-id="bc944-171">El archivo **layout.jade** del directorio **views** se utiliza como plantilla global para otros archivos **.jade**.</span><span class="sxs-lookup"><span data-stu-id="bc944-171">The **layout.jade** file in the **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="bc944-172">En este paso podrá modificarlo para utilizar [Twitter Bootstrap](https://github.com/twbs/bootstrap), un kit de herramientas que facilita el diseño de un sitio web atractivo.</span><span class="sxs-lookup"><span data-stu-id="bc944-172">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking website.</span></span>

1. <span data-ttu-id="bc944-173">Descargue y extraiga los archivos para [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="bc944-173">Download and extract the files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="bc944-174">Copie el archivo **bootstrap.min.css** desde la carpeta **bootstrap\\dist\\css** en el directorio **public\\stylesheets** de su aplicación de lista de tareas.</span><span class="sxs-lookup"><span data-stu-id="bc944-174">Copy the **bootstrap.min.css** file from the **bootstrap\\dist\\css** folder to the **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="bc944-175">En la carpeta **views**, abra **layout.jade** en el editor de texto y reemplace el contenido por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="bc944-175">From the **views** folder, open the **layout.jade** in your text editor and replace the contents with the following:</span></span>

    <span data-ttu-id="bc944-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span><span class="sxs-lookup"><span data-stu-id="bc944-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="bc944-177">Guarde el archivo **layout.jade**.</span><span class="sxs-lookup"><span data-stu-id="bc944-177">Save the **layout.jade** file.</span></span>

### <a name="running-the-application-in-the-emulator"></a><span data-ttu-id="bc944-178">Ejecución de la aplicación en el emulador</span><span class="sxs-lookup"><span data-stu-id="bc944-178">Running the Application in the Emulator</span></span>
<span data-ttu-id="bc944-179">Use el siguiente comando para iniciar la aplicación en el emulador.</span><span class="sxs-lookup"><span data-stu-id="bc944-179">Use the following command to start the application in the emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="bc944-180">El explorador se abrirá y mostrará la siguiente página:</span><span class="sxs-lookup"><span data-stu-id="bc944-180">The browser will open and displays the following page:</span></span>

![Una página web con el título My Task List con una tabla que contiene las tareas y los campos para agregar una nueva tarea.](./media/storage-nodejs-use-table-storage-cloud-service-app/node44.png)

<span data-ttu-id="bc944-182">Use el formulario para agregar elementos o quitar los elementos existentes marcándolos como completados.</span><span class="sxs-lookup"><span data-stu-id="bc944-182">Use the form to add items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-the-application-to-azure"></a><span data-ttu-id="bc944-183">Publicación de la aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="bc944-183">Publishing the Application to Azure</span></span>
<span data-ttu-id="bc944-184">En la ventana de Windows PowerShell, llame al siguiente cmdlet para volver a implementar el servicio hospedado en Azure.</span><span class="sxs-lookup"><span data-stu-id="bc944-184">In the Windows PowerShell window, call the following cmdlet to redeploy your hosted service to Azure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="bc944-185">Reemplace **myuniquename** por un nombre único para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="bc944-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="bc944-186">Reemplace **datacentername** por el nombre de un centro de datos de Azure, como por ejemplo **Oeste de EE. UU.**</span><span class="sxs-lookup"><span data-stu-id="bc944-186">Replace **datacentername** with the name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="bc944-187">Después de que la implementación se haya completado, debe ver una respuesta similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="bc944-187">After the deployment is complete, you should see a response similar to the following:</span></span>

```
  PS C:\node\tasklist> publish-azureserviceproject -servicename tasklist -location "West US"
  WARNING: Publishing tasklist to Microsoft Azure. This may take several minutes...
  WARNING: 2:18:42 PM - Preparing runtime deployment for service 'tasklist'
  WARNING: 2:18:42 PM - Verifying storage account 'tasklist'...
  WARNING: 2:18:43 PM - Preparing deployment for tasklist with Subscription ID: 65a1016d-0f67-45d2-b838-b8f373d6d52e...
  WARNING: 2:19:01 PM - Connecting...
  WARNING: 2:19:02 PM - Uploading Package to storage service larrystore...
  WARNING: 2:19:40 PM - Upgrading...
  WARNING: 2:22:48 PM - Created Deployment ID: b7134ab29b1249ff84ada2bd157f296a.
  WARNING: 2:22:48 PM - Initializing...
  WARNING: 2:22:49 PM - Instance WebRole1_IN_0 of role WebRole1 is ready.
  WARNING: 2:22:50 PM - Created Website URL: http://tasklist.cloudapp.net/.
```

<span data-ttu-id="bc944-188">Al igual que antes, puesto que ha especificado la opción **-launch**, el explorador se abre y muestra la aplicación que se ejecuta en Azure cuando se completa la publicación.</span><span class="sxs-lookup"><span data-stu-id="bc944-188">As before, because you specified the **-launch** option, the browser opens and displays your application running in Azure when publishing is completed.</span></span>

![Una ventana del explorador muestra la página My Task List.](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="bc944-191">Detención y eliminación de su aplicación</span><span class="sxs-lookup"><span data-stu-id="bc944-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="bc944-192">Después de implementar la aplicación, es posible que desee deshabilitarla a fin de evitar costes o compilar e implementar otras aplicaciones dentro del período de prueba gratuito.</span><span class="sxs-lookup"><span data-stu-id="bc944-192">After deploying your application, you may want to disable it so you can avoid costs or build and deploy other applications within the free trial time period.</span></span>

<span data-ttu-id="bc944-193">Azure factura las instancias de rol web por hora consumida de tiempo de servidor.</span><span class="sxs-lookup"><span data-stu-id="bc944-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="bc944-194">El tiempo de servidor se empieza a consumir una vez implementada su aplicación, incluso si las instancias no se están ejecutando y se encuentran detenidas.</span><span class="sxs-lookup"><span data-stu-id="bc944-194">Server time is consumed once your application is deployed, even if the instances are not running and are in the stopped state.</span></span>

<span data-ttu-id="bc944-195">Los siguientes pasos muestran cómo detener y eliminar su aplicación.</span><span class="sxs-lookup"><span data-stu-id="bc944-195">The following steps show you how to stop and delete your application.</span></span>

1. <span data-ttu-id="bc944-196">En la ventana de Windows PowerShell, detenga la implementación del servicio creado en la sección anterior con el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bc944-196">In the Windows PowerShell window, stop the service deployment created in the previous section with the following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="bc944-197">La detención del servicio puede durar varios minutos.</span><span class="sxs-lookup"><span data-stu-id="bc944-197">Stopping the service may take several minutes.</span></span> <span data-ttu-id="bc944-198">Una vez detenido el servicio, recibirá un mensaje que le avisará de su detención.</span><span class="sxs-lookup"><span data-stu-id="bc944-198">When the service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="bc944-199">Para eliminar el servicio, llame al siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bc944-199">To delete the service, call the following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="bc944-200">Cuando se le solicite, escriba **Y** para eliminar el servicio.</span><span class="sxs-lookup"><span data-stu-id="bc944-200">When prompted, enter **Y** to delete the service.</span></span>

   <span data-ttu-id="bc944-201">La eliminación del servicio puede durar varios minutos.</span><span class="sxs-lookup"><span data-stu-id="bc944-201">Deleting the service may take several minutes.</span></span> <span data-ttu-id="bc944-202">Una vez eliminado el servicio, recibirá un mensaje que le avisará de su eliminación.</span><span class="sxs-lookup"><span data-stu-id="bc944-202">After the service has been deleted you receive a message indicating that the service was deleted.</span></span>

<span data-ttu-id="bc944-203">[Aplicación web Node.js con Express]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/</span><span class="sxs-lookup"><span data-stu-id="bc944-203">[Node.js Web Application using Express]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/</span></span>
<span data-ttu-id="bc944-204">[Almacenamiento de Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx</span><span class="sxs-lookup"><span data-stu-id="bc944-204">[Storing and Accessing Data in Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx</span></span>
<span data-ttu-id="bc944-205">[Aplicación web Node.js]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/</span><span class="sxs-lookup"><span data-stu-id="bc944-205">[Node.js Web Application]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/</span></span>


