---
title: "aplicación de aaaWeb con almacenamiento de tabla (Node.js) | Documentos de Microsoft"
description: "Un tutorial que se basa en hello Web App con Express tutorial agregando hello módulo de Azure y servicios de almacenamiento de Azure."
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: e90959a2-4cb2-4b19-9bfb-aede15b18b1c
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 7eefc09baab61cf44c98183135abe572b11812e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="bd994-103">Aplicación web Node.js con almacenamiento</span><span class="sxs-lookup"><span data-stu-id="bd994-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="bd994-104">Información general</span><span class="sxs-lookup"><span data-stu-id="bd994-104">Overview</span></span>
<span data-ttu-id="bd994-105">En este tutorial, Hola aplicación que creó en el [aplicación Web de Node.js con Express] tutorial se ha ampliado con bibliotecas de cliente de hello Microsoft Azure para Node.js toowork con servicios de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="bd994-105">In this tutorial, hello application you created in the [Node.js Web Application using Express] tutorial is extended using hello Microsoft Azure Client Libraries for Node.js toowork with data management services.</span></span> <span data-ttu-id="bd994-106">Extender la aplicación mediante la creación de una aplicación de lista de tareas basada en web que puede implementar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bd994-106">You extend your application by creating a web-based task-list application that you can deploy tooAzure.</span></span> <span data-ttu-id="bd994-107">lista de tareas de Hello permite a un usuario recuperar tareas, agregar nuevas tareas y marcar una tarea como completada.</span><span class="sxs-lookup"><span data-stu-id="bd994-107">hello task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="bd994-108">elementos de tarea de Hola se almacenan en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd994-108">hello task items are stored in Azure Storage.</span></span> <span data-ttu-id="bd994-109">El almacenamiento de Azure ofrece almacenamiento de datos no estructurados que es tolerante a errores y tiene una alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="bd994-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="bd994-110">Azure Storage incluye varias estructuras de datos donde puede almacenar y tener acceso a datos.</span><span class="sxs-lookup"><span data-stu-id="bd994-110">Azure Storage includes several data structures where you can store and access data.</span></span> <span data-ttu-id="bd994-111">Puede usar servicios de almacenamiento de Hola de hello las API que se incluyen en hello Azure SDK para Node.js o a través de las API de REST.</span><span class="sxs-lookup"><span data-stu-id="bd994-111">You can use hello storage services from hello APIs included in hello Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="bd994-112">Para más información, consulte [Almacenamiento de Azure].</span><span class="sxs-lookup"><span data-stu-id="bd994-112">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="bd994-113">Este tutorial se supone que ha completado hello [aplicación Web Node.js] y [Node.js con Express][aplicación Web de Node.js con Express] tutoriales.</span><span class="sxs-lookup"><span data-stu-id="bd994-113">This tutorial assumes that you have completed hello [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="bd994-114">Contiene Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="bd994-114">It contains hello following information:</span></span>

* <span data-ttu-id="bd994-115">¿Cómo toowork con Hola motor de plantillas Jade</span><span class="sxs-lookup"><span data-stu-id="bd994-115">How toowork with hello Jade template engine</span></span>
* <span data-ttu-id="bd994-116">¿Cómo toowork con servicios de administración de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="bd994-116">How toowork with Azure Data Management services</span></span>

<span data-ttu-id="bd994-117">Hola siguiente captura de pantalla muestra la aplicación hello completado:</span><span class="sxs-lookup"><span data-stu-id="bd994-117">hello following screenshot shows hello completed application:</span></span>

![Hola completado la página web en internet explorer](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="bd994-119">Establecimiento de las credenciales de almacenamiento en Web.Config</span><span class="sxs-lookup"><span data-stu-id="bd994-119">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="bd994-120">Debe pasar las credenciales de almacenamiento tooaccess almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd994-120">You must pass in storage credentials tooaccess Azure Storage.</span></span> <span data-ttu-id="bd994-121">Esto se realiza mediante el uso de la configuración de la aplicación hello web.config.</span><span class="sxs-lookup"><span data-stu-id="bd994-121">This is done by utilizing hello web.config application settings.</span></span>
<span data-ttu-id="bd994-122">configuración de web.config Hola se pasa como tooNode de variables de entorno, que, a continuación, se leen por hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="bd994-122">hello web.config settings are passed as environment variables tooNode, which are then read by hello Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="bd994-123">Solo se usan las credenciales de almacenamiento cuando la aplicación hello es tooAzure implementado.</span><span class="sxs-lookup"><span data-stu-id="bd994-123">Storage credentials are only used when hello application is deployed tooAzure.</span></span> <span data-ttu-id="bd994-124">Cuando se ejecuta en el emulador de hello, aplicación hello usa el emulador de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd994-124">When running in hello emulator, hello application uses hello storage emulator.</span></span>
>
>

<span data-ttu-id="bd994-125">Realizar Hola después de credenciales de la cuenta de almacenamiento de información de pasos tooretrieve hello y agregarlas toohello la configuración de web.config:</span><span class="sxs-lookup"><span data-stu-id="bd994-125">Perform hello following steps tooretrieve hello storage account credentials and add them toohello web.config settings:</span></span>

1. <span data-ttu-id="bd994-126">Si no está ya abierto, inicie hello Azure PowerShell de hello **iniciar** menú expandiendo **todos los programas, Azure**, haga clic en **Azure PowerShell**y, a continuación, seleccione  **Ejecutar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="bd994-126">If it is not already open, start hello Azure PowerShell from hello **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="bd994-127">Cambiar la carpeta de toohello directorios que contiene la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bd994-127">Change directories toohello folder containing your application.</span></span> <span data-ttu-id="bd994-128">Por ejemplo, C:\\nodo\\tasklist\\WebRole1.</span><span class="sxs-lookup"><span data-stu-id="bd994-128">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="bd994-129">Desde la ventana de Powershell de Azure de hello, escriba Hola siguiendo la información de la cuenta de almacenamiento de cmdlet tooretrieve hello:</span><span class="sxs-lookup"><span data-stu-id="bd994-129">From hello Azure Powershell window, enter hello following cmdlet tooretrieve hello storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="bd994-130">Hello cmdlet anterior recupera Hola lista de cuentas de almacenamiento y las claves de cuenta asociadas con su servicio hospedado.</span><span class="sxs-lookup"><span data-stu-id="bd994-130">hello preceding cmdlet retrieves hello list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bd994-131">Puesto que Hola SDK de Azure crea una cuenta de almacenamiento al implementar un servicio, debe existir una cuenta de almacenamiento de la implementación de la aplicación en las guías de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="bd994-131">Since hello Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in hello previous guides.</span></span>
   >
   >
4. <span data-ttu-id="bd994-132">Abra hello **ServiceDefinition.csdef** archivo que contiene la configuración del entorno de Hola que se utiliza cuando la aplicación hello es tooAzure implementado:</span><span class="sxs-lookup"><span data-stu-id="bd994-132">Open hello **ServiceDefinition.csdef** file containing hello environment settings that are used when hello application is deployed tooAzure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="bd994-133">Hola del inserción siguiente bloque en **entorno** elemento, sustituyendo la {cuenta de almacenamiento de} y {clave de acceso de almacenamiento} con el nombre de la cuenta de hello y la clave principal de Hola Hola cuenta de almacenamiento que desee toouse para la implementación:</span><span class="sxs-lookup"><span data-stu-id="bd994-133">Insert hello following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with hello account name and hello primary key for hello storage account you want toouse for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![contenido del archivo Hello web.cloud.config](./media/table-storage-cloud-service-nodejs/node37.png)

6. <span data-ttu-id="bd994-135">Guarde el archivo hello y cierre el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="bd994-135">Save hello file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="bd994-136">Instalar módulos adicionales</span><span class="sxs-lookup"><span data-stu-id="bd994-136">Install additional modules</span></span>
1. <span data-ttu-id="bd994-137">Hola de uso después de comando tooinstall hello [azure], [nodo-uuid], [nconf] y [asincrónica] módulos localmente, así como toosave una entrada para ellos toohello **package.json** archivo:</span><span class="sxs-lookup"><span data-stu-id="bd994-137">Use hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules locally as well as toosave an entry for them toohello **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="bd994-138">salida de Hello de este comando debe aparecer toohello similar a continuación:</span><span class="sxs-lookup"><span data-stu-id="bd994-138">hello output of this command should appear similar toohello following:</span></span>

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

## <a name="using-hello-table-service-in-a-node-application"></a><span data-ttu-id="bd994-139">Usar servicio de la tabla de hello en una aplicación de nodo</span><span class="sxs-lookup"><span data-stu-id="bd994-139">Using hello Table service in a node application</span></span>
<span data-ttu-id="bd994-140">En esta sección, Hola básica aplicación creada por hello **express** comandos se extiende mediante la adición de un **task.js** archivo que contiene el modelo de Hola para sus tareas.</span><span class="sxs-lookup"><span data-stu-id="bd994-140">In this section, hello basic application created by hello **express** command is extended by adding a **task.js** file containing hello model for your tasks.</span></span> <span data-ttu-id="bd994-141">Modificar existente hello **app.js** de archivos y crear un nuevo **tasklist.js** archivo que usa el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd994-141">Modify hello existing **app.js** file and create a new **tasklist.js** file that uses hello model.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="bd994-142">Crear modelo Hola</span><span class="sxs-lookup"><span data-stu-id="bd994-142">Create hello model</span></span>
1. <span data-ttu-id="bd994-143">Hola **WebRole1** directorio, cree un nuevo directorio denominado **modelos**.</span><span class="sxs-lookup"><span data-stu-id="bd994-143">In hello **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="bd994-144">Hola **modelos** directorio, cree un nuevo archivo denominado **task.js**.</span><span class="sxs-lookup"><span data-stu-id="bd994-144">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="bd994-145">Este archivo contiene el modelo de Hola para las tareas de hello creadas por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bd994-145">This file contains hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="bd994-146">En principio Hola de hello **task.js** , agregue Hola siguiendo las bibliotecas de código tooreference necesario:</span><span class="sxs-lookup"><span data-stu-id="bd994-146">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="bd994-147">A continuación, agregue código toodefine y exportar el objeto de tarea de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd994-147">Next, add code toodefine and export hello Task object.</span></span> <span data-ttu-id="bd994-148">objeto de tarea de Hello es responsable de la conexión toohello tabla.</span><span class="sxs-lookup"><span data-stu-id="bd994-148">hello Task object is responsible for connecting toohello table.</span></span>

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

5. <span data-ttu-id="bd994-149">A continuación, agregue Hola siguiendo métodos adicionales de código toodefine en el objeto de tarea de hello, que permiten la interacción con los datos almacenados en la tabla de hello:</span><span class="sxs-lookup"><span data-stu-id="bd994-149">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>

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

6. <span data-ttu-id="bd994-150">Guarde y cierre hello **task.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="bd994-150">Save and close hello **task.js** file.</span></span>

### <a name="create-hello-controller"></a><span data-ttu-id="bd994-151">Crear controlador Hola</span><span class="sxs-lookup"><span data-stu-id="bd994-151">Create hello controller</span></span>
1. <span data-ttu-id="bd994-152">Hola **WebRole1/rutas** directorio, cree un nuevo archivo denominado **tasklist.js** y ábralo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="bd994-152">In hello **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="bd994-153">Agregar Hola sigue código demasiado**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="bd994-153">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="bd994-154">Este código carga hello azure y módulos asincrónicos, que son usados por **tasklist.js** y define hello **TaskList** función, que se pasa una instancia de hello **tarea** objeto se definida anteriormente:</span><span class="sxs-lookup"><span data-stu-id="bd994-154">This code loads hello azure and async modules, which are used by **tasklist.js** and defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="bd994-155">Continúe agregando toohello **tasklist.js** archivo mediante la adición de métodos de hello usa demasiado**showTasks**, **addTask**, y **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="bd994-155">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks**, **addTask**, and **completeTasks**:</span></span>

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

4. <span data-ttu-id="bd994-156">Guardar hello **tasklist.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="bd994-156">Save hello **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="bd994-157">Modificar app.js</span><span class="sxs-lookup"><span data-stu-id="bd994-157">Modify app.js</span></span>
1. <span data-ttu-id="bd994-158">Hola **WebRole1** Hola de directorio, abra **app.js** archivo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="bd994-158">In hello **WebRole1** directory, open hello **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="bd994-159">En principio de Hola de archivo hello, agregue Hola después de módulo de hello azure tooload y definir la clave de nombre y la partición de tabla de hello:</span><span class="sxs-lookup"><span data-stu-id="bd994-159">At hello beginning of hello file, add hello following tooload hello azure module and set hello table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="bd994-160">En el archivo de app.js hello, desplácese hacia abajo toowhere verá Hola línea siguiente:</span><span class="sxs-lookup"><span data-stu-id="bd994-160">In hello app.js file, scroll down toowhere you see hello following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="bd994-161">Reemplace Hola líneas anteriores con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="bd994-161">Replace hello preceding lines with hello following code.</span></span> <span data-ttu-id="bd994-162">Este código inicializa una instancia de <strong>tarea</strong> con una cuenta de almacenamiento de conexión tooyour.</span><span class="sxs-lookup"><span data-stu-id="bd994-162">This code initializes an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="bd994-163">Hola <strong>tarea</strong> se pasa toohello <strong>TaskList</strong>, que utiliza toocommunicate con el servicio de la tabla de hello:</span><span class="sxs-lookup"><span data-stu-id="bd994-163">hello <strong>Task</strong> is passed toohello <strong>TaskList</strong>, which uses it toocommunicate with hello Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="bd994-164">Guardar hello **app.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="bd994-164">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="bd994-165">Modificar la vista de índice Hola</span><span class="sxs-lookup"><span data-stu-id="bd994-165">Modify hello index view</span></span>
1. <span data-ttu-id="bd994-166">Cambie los directorios toohello **vistas** Hola de directorio y abra **index.jade** archivo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="bd994-166">Change directories toohello **views** directory and open hello **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="bd994-167">Reemplazar contenido Hola de hello **index.jade** archivo con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="bd994-167">Replace hello contents of hello **index.jade** file with hello following code.</span></span> <span data-ttu-id="bd994-168">Este código define la vista de Hola para mostrar las tareas existentes y un formulario para agregar nuevas tareas y marcar los existentes como completada.</span><span class="sxs-lookup"><span data-stu-id="bd994-168">This code defines hello view for displaying existing tasks, and defines a form for adding new tasks and marking existing ones as completed.</span></span>

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

3. <span data-ttu-id="bd994-169">Guarde y cierre el archivo **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="bd994-169">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="bd994-170">Modificar diseño global Hola</span><span class="sxs-lookup"><span data-stu-id="bd994-170">Modify hello global layout</span></span>
<span data-ttu-id="bd994-171">Hola **layout.jade** archivo Hola **vistas** directory se utiliza como plantilla global para otro **.jade** archivos.</span><span class="sxs-lookup"><span data-stu-id="bd994-171">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="bd994-172">En este paso, modificará hello **layout.jade** archivo toouse [Bootstrap Twitter](https://github.com/twbs/bootstrap), que es un Kit de herramientas que hace más fácil toodesign un sitio Web de aspecto "nice".</span><span class="sxs-lookup"><span data-stu-id="bd994-172">In this step, modify hello **layout.jade** file toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span>

1. <span data-ttu-id="bd994-173">Descargue y extraiga los archivos de Hola para [Bootstrap Twitter](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="bd994-173">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="bd994-174">Hola copia **bootstrap.min.css** archivo de hello **arranque\\dist\\css** carpeta toohello **pública\\hojas de estilos** directorio de la aplicación de la lista de tareas.</span><span class="sxs-lookup"><span data-stu-id="bd994-174">Copy hello **bootstrap.min.css** file from hello **bootstrap\\dist\\css** folder toohello **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="bd994-175">De hello **vistas** carpeta, abra hello **layout.jade** un archivo en el editor de texto y reemplace el contenido de hello con siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="bd994-175">From hello **views** folder, open hello **layout.jade** file in your text editor and replace hello contents with hello following:</span></span>

    <span data-ttu-id="bd994-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span><span class="sxs-lookup"><span data-stu-id="bd994-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="bd994-177">Guardar hello **layout.jade** archivo.</span><span class="sxs-lookup"><span data-stu-id="bd994-177">Save hello **layout.jade** file.</span></span>

### <a name="running-hello-application-in-hello-emulator"></a><span data-ttu-id="bd994-178">Ejecutar aplicación Hola Hola emulador</span><span class="sxs-lookup"><span data-stu-id="bd994-178">Running hello Application in hello Emulator</span></span>
<span data-ttu-id="bd994-179">Usar hello tras la aplicación de hello toostart de comando en el emulador de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd994-179">Use hello following command toostart hello application in hello emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="bd994-180">Explorador de Hola se abre y muestra hello después de página:</span><span class="sxs-lookup"><span data-stu-id="bd994-180">hello browser opens and displays hello following page:</span></span>

![Un servidor web paginado titulada mi lista de tareas con una tabla que contiene las tareas y los campos tooadd una nueva tarea.](./media/table-storage-cloud-service-nodejs/node44.png)

<span data-ttu-id="bd994-182">Use tooadd elementos de formulario de hello, o quite los elementos existentes marcando como completada.</span><span class="sxs-lookup"><span data-stu-id="bd994-182">Use hello form tooadd items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="bd994-183">Publicación tooAzure de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="bd994-183">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="bd994-184">En la ventana de Windows PowerShell de hello, llame a Hola siguiente cmdlet tooredeploy su tooAzure servicio hospedado.</span><span class="sxs-lookup"><span data-stu-id="bd994-184">In hello Windows PowerShell window, call hello following cmdlet tooredeploy your hosted service tooAzure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="bd994-185">Reemplace **myuniquename** por un nombre único para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="bd994-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="bd994-186">Reemplace **datacentername** con el nombre de Hola de un centro de datos de Azure, como **West US**.</span><span class="sxs-lookup"><span data-stu-id="bd994-186">Replace **datacentername** with hello name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="bd994-187">Una vez completada la implementación de hello, debería ver un siguiente toohello similar de respuesta:</span><span class="sxs-lookup"><span data-stu-id="bd994-187">After hello deployment is complete, you should see a response similar toohello following:</span></span>

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

<span data-ttu-id="bd994-188">Mediante la especificación de hello **-iniciar** opción en el cmdlet anterior hello, Explorador de Hola se abre y muestra la aplicación que se ejecuta en Azure cuando se completa la publicación.</span><span class="sxs-lookup"><span data-stu-id="bd994-188">By specifying hello **-launch** option in hello previous cmdlet, hello browser opens and displays your application running in Azure when publishing is completed.</span></span>

![Mostrar la página de mi lista de tareas de Hola una ventana del explorador.](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="bd994-191">Detención y eliminación de su aplicación</span><span class="sxs-lookup"><span data-stu-id="bd994-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="bd994-192">Después de implementar la aplicación, puede que desee toodisable por lo que puede evitar los costos o compilar e implementar otras aplicaciones dentro de Hola libre período de prueba.</span><span class="sxs-lookup"><span data-stu-id="bd994-192">After deploying your application, you may want toodisable it so you can avoid costs or build and deploy other applications within hello free trial time period.</span></span>

<span data-ttu-id="bd994-193">Azure factura las instancias de rol web por hora consumida de tiempo de servidor.</span><span class="sxs-lookup"><span data-stu-id="bd994-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="bd994-194">Hora del servidor se consume una vez implementada la aplicación, incluso si las instancias no se están ejecutando y están en estado de hello detenido.</span><span class="sxs-lookup"><span data-stu-id="bd994-194">Server time is consumed once your application is deployed, even if the instances are not running and are in hello stopped state.</span></span>

<span data-ttu-id="bd994-195">Hello pasos siguientes muestran cómo toostop y eliminar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bd994-195">hello following steps show you how toostop and delete your application.</span></span>

1. <span data-ttu-id="bd994-196">En la ventana de Windows PowerShell de hello, detener la implementación de servicio de hello creado en la sección anterior de hello con hello siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bd994-196">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="bd994-197">Deteniendo el servicio de hello puede tardar varios minutos.</span><span class="sxs-lookup"><span data-stu-id="bd994-197">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="bd994-198">Cuando se detiene el servicio de hello, recibirá un mensaje que indica que se ha detenido.</span><span class="sxs-lookup"><span data-stu-id="bd994-198">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="bd994-199">servicio de hello toodelete, Hola llamada siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bd994-199">toodelete hello service, call hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="bd994-200">Cuando se le solicite, escriba **Y** toodelete servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd994-200">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="bd994-201">Eliminando el servicio de hello puede tardar varios minutos.</span><span class="sxs-lookup"><span data-stu-id="bd994-201">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="bd994-202">Después de elimina el servicio de hello, recibirá un mensaje que indica que el servicio de Hola se eliminó.</span><span class="sxs-lookup"><span data-stu-id="bd994-202">After hello service is deleted, you will receive a message indicating that hello service was deleted.</span></span>

[aplicación Web de Node.js con Express]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[Almacenamiento de Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[aplicación Web Node.js]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


