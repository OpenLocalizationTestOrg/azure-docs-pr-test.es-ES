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
# <a name="nodejs-web-application-using-storage"></a>Aplicación web Node.js con almacenamiento
## <a name="overview"></a>Información general
En este tutorial, Hola aplicación que creó en el [aplicación Web de Node.js con Express] tutorial se ha ampliado con bibliotecas de cliente de hello Microsoft Azure para Node.js toowork con servicios de administración de datos. Extender la aplicación mediante la creación de una aplicación de lista de tareas basada en web que puede implementar tooAzure. lista de tareas de Hello permite a un usuario recuperar tareas, agregar nuevas tareas y marcar una tarea como completada.

elementos de tarea de Hola se almacenan en el almacenamiento de Azure. El almacenamiento de Azure ofrece almacenamiento de datos no estructurados que es tolerante a errores y tiene una alta disponibilidad. Azure Storage incluye varias estructuras de datos donde puede almacenar y tener acceso a datos. Puede usar servicios de almacenamiento de Hola de hello las API que se incluyen en hello Azure SDK para Node.js o a través de las API de REST. Para más información, consulte [Almacenamiento de Azure].

Este tutorial se supone que ha completado hello [aplicación Web Node.js] y [Node.js con Express][aplicación Web de Node.js con Express] tutoriales.

Contiene Hola siguiente información:

* ¿Cómo toowork con Hola motor de plantillas Jade
* ¿Cómo toowork con servicios de administración de datos de Azure

Hola siguiente captura de pantalla muestra la aplicación hello completado:

![Hola completado la página web en internet explorer](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a>Establecimiento de las credenciales de almacenamiento en Web.Config
Debe pasar las credenciales de almacenamiento tooaccess almacenamiento de Azure. Esto se realiza mediante el uso de la configuración de la aplicación hello web.config.
configuración de web.config Hola se pasa como tooNode de variables de entorno, que, a continuación, se leen por hello Azure SDK.

> [!NOTE]
> Solo se usan las credenciales de almacenamiento cuando la aplicación hello es tooAzure implementado. Cuando se ejecuta en el emulador de hello, aplicación hello usa el emulador de almacenamiento de Hola.
>
>

Realizar Hola después de credenciales de la cuenta de almacenamiento de información de pasos tooretrieve hello y agregarlas toohello la configuración de web.config:

1. Si no está ya abierto, inicie hello Azure PowerShell de hello **iniciar** menú expandiendo **todos los programas, Azure**, haga clic en **Azure PowerShell**y, a continuación, seleccione  **Ejecutar como administrador**.
2. Cambiar la carpeta de toohello directorios que contiene la aplicación. Por ejemplo, C:\\nodo\\tasklist\\WebRole1.
3. Desde la ventana de Powershell de Azure de hello, escriba Hola siguiendo la información de la cuenta de almacenamiento de cmdlet tooretrieve hello:

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   Hello cmdlet anterior recupera Hola lista de cuentas de almacenamiento y las claves de cuenta asociadas con su servicio hospedado.

   > [!NOTE]
   > Puesto que Hola SDK de Azure crea una cuenta de almacenamiento al implementar un servicio, debe existir una cuenta de almacenamiento de la implementación de la aplicación en las guías de hello anterior.
   >
   >
4. Abra hello **ServiceDefinition.csdef** archivo que contiene la configuración del entorno de Hola que se utiliza cuando la aplicación hello es tooAzure implementado:

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. Hola del inserción siguiente bloque en **entorno** elemento, sustituyendo la {cuenta de almacenamiento de} y {clave de acceso de almacenamiento} con el nombre de la cuenta de hello y la clave principal de Hola Hola cuenta de almacenamiento que desee toouse para la implementación:

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![contenido del archivo Hello web.cloud.config](./media/table-storage-cloud-service-nodejs/node37.png)

6. Guarde el archivo hello y cierre el Bloc de notas.

### <a name="install-additional-modules"></a>Instalar módulos adicionales
1. Hola de uso después de comando tooinstall hello [azure], [nodo-uuid], [nconf] y [asincrónica] módulos localmente, así como toosave una entrada para ellos toohello **package.json** archivo:

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  salida de Hello de este comando debe aparecer toohello similar a continuación:

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

## <a name="using-hello-table-service-in-a-node-application"></a>Usar servicio de la tabla de hello en una aplicación de nodo
En esta sección, Hola básica aplicación creada por hello **express** comandos se extiende mediante la adición de un **task.js** archivo que contiene el modelo de Hola para sus tareas. Modificar existente hello **app.js** de archivos y crear un nuevo **tasklist.js** archivo que usa el modelo de Hola.

### <a name="create-hello-model"></a>Crear modelo Hola
1. Hola **WebRole1** directorio, cree un nuevo directorio denominado **modelos**.
2. Hola **modelos** directorio, cree un nuevo archivo denominado **task.js**. Este archivo contiene el modelo de Hola para las tareas de hello creadas por la aplicación.
3. En principio Hola de hello **task.js** , agregue Hola siguiendo las bibliotecas de código tooreference necesario:

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. A continuación, agregue código toodefine y exportar el objeto de tarea de Hola. objeto de tarea de Hello es responsable de la conexión toohello tabla.

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

5. A continuación, agregue Hola siguiendo métodos adicionales de código toodefine en el objeto de tarea de hello, que permiten la interacción con los datos almacenados en la tabla de hello:

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

6. Guarde y cierre hello **task.js** archivo.

### <a name="create-hello-controller"></a>Crear controlador Hola
1. Hola **WebRole1/rutas** directorio, cree un nuevo archivo denominado **tasklist.js** y ábralo en un editor de texto.
2. Agregar Hola sigue código demasiado**tasklist.js**. Este código carga hello azure y módulos asincrónicos, que son usados por **tasklist.js** y define hello **TaskList** función, que se pasa una instancia de hello **tarea** objeto se definida anteriormente:

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. Continúe agregando toohello **tasklist.js** archivo mediante la adición de métodos de hello usa demasiado**showTasks**, **addTask**, y **completeTasks**:

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

4. Guardar hello **tasklist.js** archivo.

### <a name="modify-appjs"></a>Modificar app.js
1. Hola **WebRole1** Hola de directorio, abra **app.js** archivo en un editor de texto.
2. En principio de Hola de archivo hello, agregue Hola después de módulo de hello azure tooload y definir la clave de nombre y la partición de tabla de hello:

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. En el archivo de app.js hello, desplácese hacia abajo toowhere verá Hola línea siguiente:

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    Reemplace Hola líneas anteriores con el siguiente código de hello. Este código inicializa una instancia de <strong>tarea</strong> con una cuenta de almacenamiento de conexión tooyour. Hola <strong>tarea</strong> se pasa toohello <strong>TaskList</strong>, que utiliza toocommunicate con el servicio de la tabla de hello:

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. Guardar hello **app.js** archivo.

### <a name="modify-hello-index-view"></a>Modificar la vista de índice Hola
1. Cambie los directorios toohello **vistas** Hola de directorio y abra **index.jade** archivo en un editor de texto.
2. Reemplazar contenido Hola de hello **index.jade** archivo con el siguiente código de hello. Este código define la vista de Hola para mostrar las tareas existentes y un formulario para agregar nuevas tareas y marcar los existentes como completada.

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

3. Guarde y cierre el archivo **index.jade** .

### <a name="modify-hello-global-layout"></a>Modificar diseño global Hola
Hola **layout.jade** archivo Hola **vistas** directory se utiliza como plantilla global para otro **.jade** archivos. En este paso, modificará hello **layout.jade** archivo toouse [Bootstrap Twitter](https://github.com/twbs/bootstrap), que es un Kit de herramientas que hace más fácil toodesign un sitio Web de aspecto "nice".

1. Descargue y extraiga los archivos de Hola para [Bootstrap Twitter](http://getbootstrap.com/). Hola copia **bootstrap.min.css** archivo de hello **arranque\\dist\\css** carpeta toohello **pública\\hojas de estilos** directorio de la aplicación de la lista de tareas.
2. De hello **vistas** carpeta, abra hello **layout.jade** un archivo en el editor de texto y reemplace el contenido de hello con siguiente hello:

    doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content

3. Guardar hello **layout.jade** archivo.

### <a name="running-hello-application-in-hello-emulator"></a>Ejecutar aplicación Hola Hola emulador
Usar hello tras la aplicación de hello toostart de comando en el emulador de Hola.

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

Explorador de Hola se abre y muestra hello después de página:

![Un servidor web paginado titulada mi lista de tareas con una tabla que contiene las tareas y los campos tooadd una nueva tarea.](./media/table-storage-cloud-service-nodejs/node44.png)

Use tooadd elementos de formulario de hello, o quite los elementos existentes marcando como completada.

## <a name="publishing-hello-application-tooazure"></a>Publicación tooAzure de aplicación Hola
En la ventana de Windows PowerShell de hello, llame a Hola siguiente cmdlet tooredeploy su tooAzure servicio hospedado.

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

Reemplace **myuniquename** por un nombre único para esta aplicación. Reemplace **datacentername** con el nombre de Hola de un centro de datos de Azure, como **West US**.

Una vez completada la implementación de hello, debería ver un siguiente toohello similar de respuesta:

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

Mediante la especificación de hello **-iniciar** opción en el cmdlet anterior hello, Explorador de Hola se abre y muestra la aplicación que se ejecuta en Azure cuando se completa la publicación.

![Mostrar la página de mi lista de tareas de Hola una ventana del explorador. dirección URL de Hello indica página Hola ahora se hospeda en Azure.](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a>Detención y eliminación de su aplicación
Después de implementar la aplicación, puede que desee toodisable por lo que puede evitar los costos o compilar e implementar otras aplicaciones dentro de Hola libre período de prueba.

Azure factura las instancias de rol web por hora consumida de tiempo de servidor.
Hora del servidor se consume una vez implementada la aplicación, incluso si las instancias no se están ejecutando y están en estado de hello detenido.

Hello pasos siguientes muestran cómo toostop y eliminar la aplicación.

1. En la ventana de Windows PowerShell de hello, detener la implementación de servicio de hello creado en la sección anterior de hello con hello siguiente cmdlet:

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   Deteniendo el servicio de hello puede tardar varios minutos. Cuando se detiene el servicio de hello, recibirá un mensaje que indica que se ha detenido.

2. servicio de hello toodelete, Hola llamada siguiente cmdlet:

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   Cuando se le solicite, escriba **Y** toodelete servicio de Hola.

   Eliminando el servicio de hello puede tardar varios minutos. Después de elimina el servicio de hello, recibirá un mensaje que indica que el servicio de Hola se eliminó.

[aplicación Web de Node.js con Express]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[Almacenamiento de Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[aplicación Web Node.js]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


