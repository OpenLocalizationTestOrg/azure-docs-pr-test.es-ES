---
title: "aplicación de aaaWeb con almacenamiento de tabla (Node.js) | Documentos de Microsoft"
description: "Un tutorial que se basa en hello Web App con Express tutorial agregando hello módulo de Azure y servicios de almacenamiento de Azure."
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
ms.openlocfilehash: 4eba16f09f8b69cbc135d097e6ca71e08b33733c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="0d421-103">Aplicación web Node.js con almacenamiento</span><span class="sxs-lookup"><span data-stu-id="0d421-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="0d421-104">Información general</span><span class="sxs-lookup"><span data-stu-id="0d421-104">Overview</span></span>
<span data-ttu-id="0d421-105">En este tutorial, se ampliará la aplicación hello creada en el [aplicación Web de Node.js con Express] tutorial mediante el uso de bibliotecas de cliente de hello Microsoft Azure para Node.js toowork con servicios de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="0d421-105">In this tutorial, you will extend hello application created in the [Node.js Web Application using Express] tutorial by using hello Microsoft Azure Client Libraries for Node.js toowork with data management services.</span></span> <span data-ttu-id="0d421-106">Una aplicación de lista de tareas basada en web que puede implementar tooAzure extenderá el toocreate de aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d421-106">You will extend your application toocreate a web-based task-list application that you can deploy tooAzure.</span></span> <span data-ttu-id="0d421-107">lista de tareas de Hello permite a un usuario recuperar tareas, agregar nuevas tareas y marcar una tarea como completada.</span><span class="sxs-lookup"><span data-stu-id="0d421-107">hello task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="0d421-108">elementos de tarea de Hola se almacenan en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="0d421-108">hello task items are stored in Azure Storage.</span></span> <span data-ttu-id="0d421-109">El almacenamiento de Azure ofrece almacenamiento de datos no estructurados que es tolerante a errores y tiene una alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="0d421-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="0d421-110">Almacenamiento de Azure incluye varias estructuras de datos donde puede almacenar y obtener acceso a datos y se pueden aprovechar los servicios de almacenamiento de Hola de hello las API que se incluyen en hello Azure SDK para Node.js o a través de las API de REST.</span><span class="sxs-lookup"><span data-stu-id="0d421-110">Azure Storage includes several data structures where you can store and access data, and you can leverage hello storage services from hello APIs included in hello Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="0d421-111">Para más información, consulte [Almacenamiento de Azure].</span><span class="sxs-lookup"><span data-stu-id="0d421-111">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="0d421-112">Este tutorial se supone que ha completado hello [aplicación Web Node.js] y [Node.js con Express][aplicación Web de Node.js con Express] tutoriales.</span><span class="sxs-lookup"><span data-stu-id="0d421-112">This tutorial assumes that you have completed hello [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="0d421-113">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="0d421-113">You will learn:</span></span>

* <span data-ttu-id="0d421-114">¿Cómo toowork con Hola motor de plantillas Jade</span><span class="sxs-lookup"><span data-stu-id="0d421-114">How toowork with hello Jade template engine</span></span>
* <span data-ttu-id="0d421-115">¿Cómo toowork con servicios de administración de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="0d421-115">How toowork with Azure Data Management services</span></span>

<span data-ttu-id="0d421-116">Una captura de pantalla de la aplicación hello completado es menor que:</span><span class="sxs-lookup"><span data-stu-id="0d421-116">A screenshot of hello completed application is below:</span></span>

![Hola completado la página web en internet explorer](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="0d421-118">Establecimiento de las credenciales de almacenamiento en Web.Config</span><span class="sxs-lookup"><span data-stu-id="0d421-118">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="0d421-119">tooaccess almacenamiento de Azure, deberá toopass en las credenciales de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0d421-119">tooaccess Azure Storage, you need toopass in storage credentials.</span></span> <span data-ttu-id="0d421-120">toodo esto, use la configuración de la aplicación de web.config.</span><span class="sxs-lookup"><span data-stu-id="0d421-120">toodo this, you utilize web.config application settings.</span></span>
<span data-ttu-id="0d421-121">Esos valores se pasarán como tooNode de variables de entorno, que, a continuación, se leen por hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="0d421-121">Those settings will be passed as environment variables tooNode, which are then read by hello Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="0d421-122">Solo se usan las credenciales de almacenamiento cuando la aplicación hello es tooAzure implementado.</span><span class="sxs-lookup"><span data-stu-id="0d421-122">Storage credentials are only used when hello application is deployed tooAzure.</span></span> <span data-ttu-id="0d421-123">Cuando se ejecuta en el emulador de hello, aplicación hello utilizará el emulador de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d421-123">When running in hello emulator, hello application will use hello storage emulator.</span></span>
>
>

<span data-ttu-id="0d421-124">Realizar Hola después de credenciales de la cuenta de almacenamiento de información de pasos tooretrieve hello y agregarlas toohello la configuración de web.config:</span><span class="sxs-lookup"><span data-stu-id="0d421-124">Perform hello following steps tooretrieve hello storage account credentials and add them toohello web.config settings:</span></span>

1. <span data-ttu-id="0d421-125">Si no está ya abierto, inicie hello Azure PowerShell de hello **iniciar** menú expandiendo **todos los programas, Azure**, haga clic en **Azure PowerShell**y, a continuación, seleccione  **Ejecutar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="0d421-125">If it is not already open, start hello Azure PowerShell from hello **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="0d421-126">Cambiar la carpeta de toohello directorios que contiene la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d421-126">Change directories toohello folder containing your application.</span></span> <span data-ttu-id="0d421-127">Por ejemplo, C:\\nodo\\tasklist\\WebRole1.</span><span class="sxs-lookup"><span data-stu-id="0d421-127">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="0d421-128">Desde la ventana de Powershell de Azure de hello escriba Hola siguiendo la información de la cuenta de almacenamiento de cmdlet tooretrieve hello:</span><span class="sxs-lookup"><span data-stu-id="0d421-128">From hello Azure Powershell window enter hello following cmdlet tooretrieve hello storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="0d421-129">Esto recupera la lista de Hola de cuentas de almacenamiento y la cuenta de claves asociada con el servicio hospedado.</span><span class="sxs-lookup"><span data-stu-id="0d421-129">This retrieves hello list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0d421-130">Puesto que Hola SDK de Azure crea una cuenta de almacenamiento al implementar un servicio, debe existir una cuenta de almacenamiento de la implementación de la aplicación en las guías de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="0d421-130">Since hello Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in hello previous guides.</span></span>
   >
   >
4. <span data-ttu-id="0d421-131">Abra hello **ServiceDefinition.csdef** archivo que contiene la configuración del entorno de Hola que se utiliza cuando la aplicación hello es tooAzure implementado:</span><span class="sxs-lookup"><span data-stu-id="0d421-131">Open hello **ServiceDefinition.csdef** file containing hello environment settings that are used when hello application is deployed tooAzure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="0d421-132">Hola del inserción siguiente bloque en **entorno** elemento, sustituyendo la {cuenta de almacenamiento de} y {clave de acceso de almacenamiento} con el nombre de la cuenta de hello y la clave principal de Hola Hola cuenta de almacenamiento que desee toouse para la implementación:</span><span class="sxs-lookup"><span data-stu-id="0d421-132">Insert hello following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with hello account name and hello primary key for hello storage account you want toouse for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![contenido del archivo Hello web.cloud.config](./media/storage-nodejs-use-table-storage-cloud-service-app/node37.png)

6. <span data-ttu-id="0d421-134">Guarde el archivo hello y cierre el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="0d421-134">Save hello file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="0d421-135">Instalar módulos adicionales</span><span class="sxs-lookup"><span data-stu-id="0d421-135">Install additional modules</span></span>
1. <span data-ttu-id="0d421-136">Hola de uso después de comando tooinstall hello [azure], [nodo-uuid], [nconf] y [asincrónica] módulos localmente, así como toosave una entrada para ellos toohello **package.json** archivo:</span><span class="sxs-lookup"><span data-stu-id="0d421-136">Use hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules locally as well as toosave an entry for them toohello **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="0d421-137">salida de Hello de este comando debe aparecer toohello similar a continuación:</span><span class="sxs-lookup"><span data-stu-id="0d421-137">hello output of this command should appear similar toohello following:</span></span>

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

## <a name="using-hello-table-service-in-a-node-application"></a><span data-ttu-id="0d421-138">Usar servicio de la tabla de hello en una aplicación de nodo</span><span class="sxs-lookup"><span data-stu-id="0d421-138">Using hello Table service in a node application</span></span>
<span data-ttu-id="0d421-139">En esta sección se ampliará la aplicación básica de hello creada por hello **express** comando mediante la adición de un **task.js** archivo que contiene el modelo de Hola para sus tareas.</span><span class="sxs-lookup"><span data-stu-id="0d421-139">In this section you will extend hello basic application created by hello **express** command by adding a **task.js** file which contains hello model for your tasks.</span></span> <span data-ttu-id="0d421-140">Además, modificará Hola existente **app.js** y crear un nuevo **tasklist.js** archivo que usa el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d421-140">You will also modify hello existing **app.js** and create a new **tasklist.js** file that uses hello model.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="0d421-141">Crear modelo Hola</span><span class="sxs-lookup"><span data-stu-id="0d421-141">Create hello model</span></span>
1. <span data-ttu-id="0d421-142">Hola **WebRole1** directorio, cree un nuevo directorio denominado **modelos**.</span><span class="sxs-lookup"><span data-stu-id="0d421-142">In hello **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="0d421-143">Hola **modelos** directorio, cree un nuevo archivo denominado **task.js**.</span><span class="sxs-lookup"><span data-stu-id="0d421-143">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="0d421-144">Este archivo contendrá el modelo de Hola para las tareas de hello creadas por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d421-144">This file will contain hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="0d421-145">En principio Hola de hello **task.js** , agregue Hola siguiendo las bibliotecas de código tooreference necesario:</span><span class="sxs-lookup"><span data-stu-id="0d421-145">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="0d421-146">A continuación, agregará código toodefine y exportar el objeto de tarea de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d421-146">Next, you will add code toodefine and export hello Task object.</span></span> <span data-ttu-id="0d421-147">Este objeto es responsable de la conexión toohello tabla.</span><span class="sxs-lookup"><span data-stu-id="0d421-147">This object is responsible for connecting toohello table.</span></span>

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

5. <span data-ttu-id="0d421-148">A continuación, agregue Hola siguiendo métodos adicionales de código toodefine en el objeto de tarea de hello, que permiten la interacción con los datos almacenados en la tabla de hello:</span><span class="sxs-lookup"><span data-stu-id="0d421-148">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>

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
    ```

6. <span data-ttu-id="0d421-149">Guarde y cierre hello **task.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="0d421-149">Save and close hello **task.js** file.</span></span>

### <a name="create-hello-controller"></a><span data-ttu-id="0d421-150">Crear controlador Hola</span><span class="sxs-lookup"><span data-stu-id="0d421-150">Create hello controller</span></span>
1. <span data-ttu-id="0d421-151">Hola **WebRole1/rutas** directorio, cree un nuevo archivo denominado **tasklist.js** y ábralo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="0d421-151">In hello **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="0d421-152">Agregar Hola sigue código demasiado**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="0d421-152">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="0d421-153">Esto carga los módulos de hello azure y asincrónicas, que son usados por **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="0d421-153">This loads hello azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="0d421-154">Esto también define hello **TaskList** función, que se pasa una instancia de hello **tarea** objeto definimos anteriormente:</span><span class="sxs-lookup"><span data-stu-id="0d421-154">This also defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="0d421-155">Continúe agregando toohello **tasklist.js** archivo mediante la adición de métodos de hello usa demasiado**showTasks**, **addTask**, y **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="0d421-155">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks**, **addTask**, and **completeTasks**:</span></span>

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

4. <span data-ttu-id="0d421-156">Guardar hello **tasklist.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="0d421-156">Save hello **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="0d421-157">Modificar app.js</span><span class="sxs-lookup"><span data-stu-id="0d421-157">Modify app.js</span></span>
1. <span data-ttu-id="0d421-158">Hola **WebRole1** Hola de directorio, abra **app.js** archivo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="0d421-158">In hello **WebRole1** directory, open hello **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="0d421-159">En principio de Hola de archivo hello, agregue Hola después de módulo de hello azure tooload y definir la clave de nombre y la partición de tabla de hello:</span><span class="sxs-lookup"><span data-stu-id="0d421-159">At hello beginning of hello file, add hello following tooload hello azure module and set hello table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="0d421-160">En el archivo de app.js hello, desplácese hacia abajo toowhere verá Hola línea siguiente:</span><span class="sxs-lookup"><span data-stu-id="0d421-160">In hello app.js file, scroll down toowhere you see hello following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="0d421-161">Reemplace Hola por encima de las líneas con el código de hello que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="0d421-161">Replace hello above lines with hello code shown below.</span></span> <span data-ttu-id="0d421-162">Esto inicializará en una instancia de <strong>tarea</strong> con una cuenta de almacenamiento de conexión tooyour.</span><span class="sxs-lookup"><span data-stu-id="0d421-162">This will initialize an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="0d421-163">Este argumento se pasa toohello <strong>TaskList</strong>, que usará toocommunicate con hello servicio tabla:</span><span class="sxs-lookup"><span data-stu-id="0d421-163">This is passed toohello <strong>TaskList</strong>, which will use it toocommunicate with hello Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="0d421-164">Guardar hello **app.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="0d421-164">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="0d421-165">Modificar la vista de índice Hola</span><span class="sxs-lookup"><span data-stu-id="0d421-165">Modify hello index view</span></span>
1. <span data-ttu-id="0d421-166">Cambie los directorios toohello **vistas** Hola de directorio y abra **index.jade** archivo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="0d421-166">Change directories toohello **views** directory and open hello **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="0d421-167">Reemplazar contenido Hola de hello **index.jade** archivo con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="0d421-167">Replace hello contents of hello **index.jade** file with hello code below.</span></span> <span data-ttu-id="0d421-168">Esto define la vista de Hola para mostrar las tareas existentes, así como un formulario para agregar nuevas tareas y marcar los existentes como completada.</span><span class="sxs-lookup"><span data-stu-id="0d421-168">This defines hello view for displaying existing tasks, as well as a form for adding new tasks and marking existing ones as completed.</span></span>

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

3. <span data-ttu-id="0d421-169">Guarde y cierre el archivo **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="0d421-169">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="0d421-170">Modificar diseño global Hola</span><span class="sxs-lookup"><span data-stu-id="0d421-170">Modify hello global layout</span></span>
<span data-ttu-id="0d421-171">Hola **layout.jade** archivo Hola **vistas** directory se utiliza como plantilla global para otro **.jade** archivos.</span><span class="sxs-lookup"><span data-stu-id="0d421-171">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="0d421-172">En este paso, modificará toouse [Bootstrap Twitter](https://github.com/twbs/bootstrap), que es un Kit de herramientas que hace más fácil toodesign un sitio Web de aspecto "nice".</span><span class="sxs-lookup"><span data-stu-id="0d421-172">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span>

1. <span data-ttu-id="0d421-173">Descargue y extraiga los archivos de Hola para [Bootstrap Twitter](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="0d421-173">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="0d421-174">Hola copia **bootstrap.min.css** archivo de hello **arranque\\dist\\css** carpeta toohello **pública\\hojas de estilos** directorio de la aplicación de la lista de tareas.</span><span class="sxs-lookup"><span data-stu-id="0d421-174">Copy hello **bootstrap.min.css** file from hello **bootstrap\\dist\\css** folder toohello **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="0d421-175">De hello **vistas** carpeta, abra hello **layout.jade** en el contenido de hello texto editor y reemplazar con siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="0d421-175">From hello **views** folder, open hello **layout.jade** in your text editor and replace hello contents with hello following:</span></span>

    <span data-ttu-id="0d421-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span><span class="sxs-lookup"><span data-stu-id="0d421-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="0d421-177">Guardar hello **layout.jade** archivo.</span><span class="sxs-lookup"><span data-stu-id="0d421-177">Save hello **layout.jade** file.</span></span>

### <a name="running-hello-application-in-hello-emulator"></a><span data-ttu-id="0d421-178">Ejecutar aplicación Hola Hola emulador</span><span class="sxs-lookup"><span data-stu-id="0d421-178">Running hello Application in hello Emulator</span></span>
<span data-ttu-id="0d421-179">Usar hello tras la aplicación de hello toostart de comando en el emulador de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d421-179">Use hello following command toostart hello application in hello emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="0d421-180">Explorador de Hola se abrirá y muestra hello después de la página:</span><span class="sxs-lookup"><span data-stu-id="0d421-180">hello browser will open and displays hello following page:</span></span>

![Un servidor web paginado titulada mi lista de tareas con una tabla que contiene las tareas y los campos tooadd una nueva tarea.](./media/storage-nodejs-use-table-storage-cloud-service-app/node44.png)

<span data-ttu-id="0d421-182">Use tooadd elementos de formulario de hello, o quite los elementos existentes marcando como completada.</span><span class="sxs-lookup"><span data-stu-id="0d421-182">Use hello form tooadd items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="0d421-183">Publicación tooAzure de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="0d421-183">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="0d421-184">En la ventana de Windows PowerShell de hello, llame a Hola siguiente cmdlet tooredeploy su tooAzure servicio hospedado.</span><span class="sxs-lookup"><span data-stu-id="0d421-184">In hello Windows PowerShell window, call hello following cmdlet tooredeploy your hosted service tooAzure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="0d421-185">Reemplace **myuniquename** por un nombre único para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d421-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="0d421-186">Reemplace **datacentername** con el nombre de Hola de un centro de datos de Azure, como **West US**.</span><span class="sxs-lookup"><span data-stu-id="0d421-186">Replace **datacentername** with hello name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="0d421-187">Una vez completada la implementación de hello, debería ver un siguiente toohello similar de respuesta:</span><span class="sxs-lookup"><span data-stu-id="0d421-187">After hello deployment is complete, you should see a response similar toohello following:</span></span>

```
  PS C:\node\tasklist> publish-azureserviceproject -servicename tasklist -location "West US"
  WARNING: Publishing tasklist tooMicrosoft Azure. This may take several minutes...
  WARNING: 2:18:42 PM - Preparing runtime deployment for service 'tasklist'
  WARNING: 2:18:42 PM - Verifying storage account 'tasklist'...
  WARNING: 2:18:43 PM - Preparing deployment for tasklist with Subscription ID: 65a1016d-0f67-45d2-b838-b8f373d6d52e...
  WARNING: 2:19:01 PM - Connecting...
  WARNING: 2:19:02 PM - Uploading Package toostorage service larrystore...
  WARNING: 2:19:40 PM - Upgrading...
  WARNING: 2:22:48 PM - Created Deployment ID: b7134ab29b1249ff84ada2bd157f296a.
  WARNING: 2:22:48 PM - Initializing...
  WARNING: 2:22:49 PM - Instance WebRole1_IN_0 of role WebRole1 is ready.
  WARNING: 2:22:50 PM - Created Website URL: http://tasklist.cloudapp.net/.
```

<span data-ttu-id="0d421-188">Al igual que antes, porque se especificó hello **-iniciar** opción, Explorador de Hola se abre y muestra la aplicación que se ejecuta en Azure cuando se completa la publicación.</span><span class="sxs-lookup"><span data-stu-id="0d421-188">As before, because you specified hello **-launch** option, hello browser opens and displays your application running in Azure when publishing is completed.</span></span>

![Mostrar la página de mi lista de tareas de Hola una ventana del explorador.](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="0d421-191">Detención y eliminación de su aplicación</span><span class="sxs-lookup"><span data-stu-id="0d421-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="0d421-192">Después de implementar la aplicación, puede que desee toodisable por lo que puede evitar los costos o compilar e implementar otras aplicaciones dentro de Hola libre período de prueba.</span><span class="sxs-lookup"><span data-stu-id="0d421-192">After deploying your application, you may want toodisable it so you can avoid costs or build and deploy other applications within hello free trial time period.</span></span>

<span data-ttu-id="0d421-193">Azure factura las instancias de rol web por hora consumida de tiempo de servidor.</span><span class="sxs-lookup"><span data-stu-id="0d421-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="0d421-194">Hora del servidor se consume una vez implementada la aplicación, incluso si las instancias no se están ejecutando y están en estado de hello detenido.</span><span class="sxs-lookup"><span data-stu-id="0d421-194">Server time is consumed once your application is deployed, even if the instances are not running and are in hello stopped state.</span></span>

<span data-ttu-id="0d421-195">Hello pasos siguientes muestran cómo toostop y eliminar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d421-195">hello following steps show you how toostop and delete your application.</span></span>

1. <span data-ttu-id="0d421-196">En la ventana de Windows PowerShell de hello, detener la implementación de servicio de hello creado en la sección anterior de hello con hello siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="0d421-196">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="0d421-197">Deteniendo el servicio de hello puede tardar varios minutos.</span><span class="sxs-lookup"><span data-stu-id="0d421-197">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="0d421-198">Cuando se detiene el servicio de hello, recibirá un mensaje que indica que se ha detenido.</span><span class="sxs-lookup"><span data-stu-id="0d421-198">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="0d421-199">servicio de hello toodelete, Hola llamada siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="0d421-199">toodelete hello service, call hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="0d421-200">Cuando se le solicite, escriba **Y** toodelete servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d421-200">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="0d421-201">Eliminando el servicio de hello puede tardar varios minutos.</span><span class="sxs-lookup"><span data-stu-id="0d421-201">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="0d421-202">Después de que se ha eliminado el servicio de hello recibirá un mensaje que indica que el servicio de Hola se eliminó.</span><span class="sxs-lookup"><span data-stu-id="0d421-202">After hello service has been deleted you receive a message indicating that hello service was deleted.</span></span>

[aplicación Web de Node.js con Express]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[Almacenamiento de Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[aplicación Web Node.js]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


