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
# <a name="nodejs-web-app-using-hello-azure-table-service"></a>Aplicación web de Node.js con hello servicio tabla de Azure
## <a name="overview"></a>Información general
Este tutorial muestra cómo se proporciona el servicio de tabla de toouse datos de administración de datos de Azure toostore y acceso de un [nodo] aplicación hospedada en [servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) aplicaciones Web. En este tutorial se asume que tiene alguna experiencia anterior en el uso de Node y [Git].

Aprenderá a:

* ¿Cómo toouse npm (Administrador de paquetes de nodo) tooinstall Hola módulos de nodo
* ¿Cómo toowork con Hola servicio tabla de Azure
* ¿Cómo toouse Hola toocreate de CLI de Azure de una aplicación web.

Al seguir este tutorial, podrá compilar una aplicación de "lista de tareas pendientes" basadas en web sencilla que permite crear, recuperar y completar tareas. tareas de Hola se almacenan en hello servicio tabla.

Esta es la aplicación hello completado:

![Página web que muestra una lista de tareas vacía][node-table-finished]

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## <a name="prerequisites"></a>Requisitos previos
Antes de seguir las instrucciones de hello en este artículo, asegúrese de que tiene instalado el siguiente hello:

* [nodo] versión 0.10.24 o superior
* [Git]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a>Crear una cuenta de almacenamiento
Cree una cuenta de Azure Storage. aplicación Hello usará este elementos pendientes de cuenta toostore Hola.

1. Inicie sesión en hello [Portal de Azure](https://portal.azure.com/).
2. Haga clic en hello **New** icono situado en la parte inferior de hello izquierda del portal de hello, a continuación, haga clic en **datos + almacenamiento** > **almacenamiento**. Asigne un nombre único de cuenta de almacenamiento de Hola y crear un nuevo [grupo de recursos](../azure-resource-manager/resource-group-overview.md) para él.
   
      ![Botón Nuevo](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    Cuando se ha creado la cuenta de almacenamiento de hello, Hola **notificaciones** botón parpadeará en un color verde **correcto** y está abierta la hoja de la cuenta de almacenamiento de hello tooshow que pertenece toohello nuevo recurso de grupo, creado.
3. En la hoja de la cuenta de almacenamiento de hello, haga clic en **configuración** > **claves**. Copie el Portapapeles de toohello clave de acceso principal de Hola.
   
    ![Clave de acceso][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a>Instalación de módulos y generación de scaffolding
En esta sección creará una nueva aplicación de nodo y usar paquetes de npm tooadd módulo. Para esta aplicación usará hello [Express] y [Azure] módulos. módulo de Hello Express proporciona un marco de Model View Controller de nodo, mientras Hola módulos de Azure proporciona servicio de tabla de toohello de conectividad.

### <a name="install-express-and-generate-scaffolding"></a>Instalar Express y generar scaffolding
1. Desde la línea de comandos de hello, cree un directorio denominado **tasklist** y directory toothat del conmutador.  
2. Escriba Hola después de módulo de comando tooinstall Hola Express.
   
        npm install express-generator@4.2.0 -g
   
    Función de sistema operativo de hello, puede ser necesario tooput 'sudo' antes de que el comando de hello:
   
        sudo npm install express-generator@4.2.0 -g
   
    salida de Hello aparece similar toohello siguiente ejemplo:
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > Hola '-g' parámetro instala el módulo de hello globalmente. De este modo, podemos usar **express** toogenerate scaffolding de aplicación web sin necesidad de tootype en información adicional de la ruta de acceso.
   > 
   > 
3. scaffolding de hello toocreate para la aplicación hello, escriba Hola **express** comando:
   
        express
   
    salida de Hello de este comando aparece similar toohello siguiente ejemplo:
   
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
   
    Ahora tiene varias nuevos directorios y archivos en hello **tasklist** directory.

### <a name="install-additional-modules"></a>Instalar módulos adicionales
Uno de hello archivos que **express** crea es **package.json**. Este archivo contiene una lista de dependencias de módulo. Más adelante, cuando se implementa hello tooApp de aplicación Web del servicio de aplicaciones, este archivo determina qué módulos necesitan toobe instalado en Azure.

Desde la línea de comandos de hello, escriba Hola después de módulos de hello tooinstall comando descritos en hello **package.json** archivo. Puede que necesite toouse 'sudo'.

    npm install

salida de Hello de este comando aparece similar toohello siguiente ejemplo:

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


A continuación, escriba Hola después comando tooinstall hello [azure], [nodo uuid], [nconf] y [async] módulos:

    npm install azure-storage node-uuid async nconf --save

Hola **--guardar** marca agrega entradas para estos módulos toohello **package.json** archivo.

salida de Hello de este comando aparece similar toohello siguiente ejemplo:

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-hello-application"></a>Crear aplicación hello
Ahora estamos aplicación de hello toobuild listo.

### <a name="create-a-model"></a>Crear un modelo
A *modelo* es un objeto que representa los datos de hello en la aplicación. Para la aplicación hello, modelo solo hello es un objeto de tarea que representa un elemento de lista de tareas pendientes de Hola. Tareas tendrá Hola siguientes campos:

* PartitionKey
* RowKey
* name (string)
* category (string)
* completed (Boolean)

**PartitionKey** y **RowKey** Hola servicio tabla sirven como claves de tabla. Para obtener más información, consulte [modelo de datos de servicio de la tabla de descripción hello](https://msdn.microsoft.com/library/azure/dd179338.aspx).

1. Hola **tasklist** directorio, cree un nuevo directorio denominado **modelos**.
2. Hola **modelos** directorio, cree un nuevo archivo denominado **task.js**. Este archivo contendrá el modelo de Hola para las tareas de hello creadas por la aplicación.
3. En principio Hola de hello **task.js** , agregue Hola siguiendo las bibliotecas de código tooreference necesario:
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. Agregue código toodefine siguiente de Hola y exporta el objeto de tarea de Hola. Este objeto es responsable de la conexión toohello tabla.
   
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
5. Agregue Hola siguiendo métodos adicionales de código toodefine en el objeto de tarea de hello, que permiten la interacción con los datos almacenados en la tabla de hello:
   
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
6. Guarde y cierre hello **task.js** archivo.

### <a name="create-a-controller"></a>Creación de un controlador
A *controlador* controla las solicitudes HTTP y representa la respuesta de hello HTML.

1. Hola **tasklist/rutas** directorio, cree un nuevo archivo denominado **tasklist.js** y ábralo en un editor de texto.
2. Agregar Hola sigue código demasiado**tasklist.js**. Esto carga los módulos de hello azure y asincrónicas, que son usados por **tasklist.js**. Esto también define hello **TaskList** función, que se pasa una instancia de hello **tarea** objeto definimos anteriormente:
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. Defina un objeto **TaskList** .
   
        function TaskList(task) {
          this.task = task;
        }
4. Agregar Hola siguiendo métodos demasiado**TaskList**:
   
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

### <a name="modify-appjs"></a>Modificar app.js
1. De hello **tasklist** Hola de directorio, abra **app.js** archivo. Este archivo se creó anteriormente mediante la ejecución de hello **express** comando.
2. En principio de Hola de archivo hello, agregue Hola después de módulo de hello azure tooload, nombre de la tabla de conjunto de Hola, clave de partición y las credenciales de almacenamiento de hello conjunto utilizadas por este ejemplo:
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > nconf cargará los valores de configuración de Hola de variables de entorno o hello **config.json** archivo, que creará más adelante.
   > 
   > 
3. En el archivo de app.js hello, desplácese hacia abajo toowhere verá Hola línea siguiente:
   
        app.use('/', routes);
        app.use('/users', users);
   
    Reemplace Hola por encima de las líneas con el código de hello que se muestra a continuación. Esto inicializará en una instancia de <strong>tarea</strong> con una cuenta de almacenamiento de conexión tooyour. Este argumento se pasa toohello <strong>TaskList</strong>, que usará toocommunicate con hello servicio tabla:
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. Guardar hello **app.js** archivo.

### <a name="modify-hello-index-view"></a>Modificar la vista de índice Hola
1. Abra hello **tasklist/views/index.jade** archivo en un editor de texto.
2. Reemplace Hola todo contenido de archivo hello con hello siguiente código. De esta manera se define una vista para mostrar las tareas existentes y se incluye un formulario para agregar tareas nuevas y marcar las existentes como terminadas.
   
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
3. Guarde y cierre el archivo **index.jade** .

### <a name="modify-hello-global-layout"></a>Modificar diseño global Hola
Hola **layout.jade** archivo Hola **vistas** directory es una plantilla global para otros **.jade** archivos. En este paso, modificará toouse [Bootstrap Twitter](https://github.com/twbs/bootstrap), que es un Kit de herramientas que hace más fácil toodesign una aplicación web la claridad "nice".

Descargue y extraiga los archivos de Hola para [Bootstrap Twitter](http://getbootstrap.com/). Hola copia **bootstrap.min.css** archivo de hello Bootstrap **css** carpeta en hello **público/hojas de estilos** directorio de la aplicación.

De hello **vistas** carpeta, abra **layout.jade** y reemplace el contenido completo de hello con siguiente de hello:

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

### <a name="create-a-config-file"></a>Creación de un archivo de configuración
toorun localmente la aplicación de hello, colocamos las credenciales de almacenamiento de Azure en un archivo de configuración. Cree un archivo denominado **config.json* * con hello después JSON:

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Reemplace **nombre de la cuenta de almacenamiento** con el nombre de Hola de almacenamiento de hello de la cuenta que creó anteriormente y reemplace **clave de acceso de almacenamiento** con la clave de acceso principal de hello para la cuenta de almacenamiento. Por ejemplo:

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Guarde este archivo *nivel de un directorio superior* que hello **tasklist** directorio, similar al siguiente:

    parent/
      |-- config.json
      |-- tasklist/

motivo de Hola para hacer esto es tooavoid comprobando el archivo de configuración de hello en el control de código fuente, donde se puede convertir en público. Cuando se implementa tooAzure de aplicación Hola, usaremos las variables de entorno en lugar de un archivo de configuración.

## <a name="run-hello-application-locally"></a>Ejecutar la aplicación hello localmente
aplicación de hello tootest en el equipo local, lleve a cabo Hola pasos:

1. Desde la línea de comandos de hello, cambiar directorios toohello **tasklist** directory.
2. Usar hello tras la aplicación localmente de comando toolaunch hello:
   
        npm start
3. Abra un explorador web y navegue toohttp://127.0.0.1:3000.
   
    Aparece un toohello similar de página web siguiente ejemplo.
   
    ![Página web que muestra una lista de tareas vacía][node-table-finished]
4. toocreate un nuevo elemento de tarea, escriba un nombre y una categoría y haga clic en **Agregar elemento**. 
5. una tarea como completa, verificación de toomark **completar** y haga clic en **tareas de actualización de**.
   
    ![Una imagen de hello nuevo elemento de lista de Hola de tareas][node-table-list-items]

Aunque la aplicación hello se ejecuta localmente, está almacenando datos de Hola Hola servicio tabla de Azure.

## <a name="deploy-your-application-tooazure"></a>Implementar la aplicación tooAzure
pasos de Hello en esta sección use hello Azure herramientas de línea de comandos toocreate una nueva aplicación web de servicio de aplicaciones y, a continuación, usan Git toodeploy la aplicación. tooperform estos pasos debe tener una suscripción de Azure.

> [!NOTE]
> Estos pasos también se pueden realizar mediante el uso de hello [Portal de Azure](https://portal.azure.com/). Consulte [Compilación e implementación de una aplicación web de Node.js en el Servicio de aplicaciones de Azure].
> 
> Si se trata de hello primera aplicación web que ha creado, debe usar hello Azure Portal toodeploy esta aplicación.
> 
> 

tooget iniciado, instalar hello [CLI de Azure] escribiendo el siguiente comando desde la línea de comandos de Hola de hello:

    npm install azure-cli -g

### <a name="import-publishing-settings"></a>Importación de la configuración de publicación
En este paso, descargará un archivo que contiene información acerca de su suscripción.

1. Escriba el siguiente comando de hello:
   
        azure login
   
    Este comando inicia un explorador y desplaza la página de descarga de toohello. Si se le solicita, inicie sesión con la cuenta de hello asociada con su suscripción de Azure.
   
    <!-- ![hello download page][download-publishing-settings] -->
   
    descarga del archivo Hola se iniciará automáticamente; Si no es así, puede hacer clic Hola vínculo al principio de Hola Hola toomanually descarga Hola del archivo de página. Guardar ruta de archivo de Hola de archivo y observe Hola.
2. Escriba Hola después de la configuración del comando de Hola tooimport:
   
        azure account import <path-to-file>
   
    Especifique el nombre de ruta de acceso y de Hola de hello publicar el archivo de configuración que ha descargado en el paso anterior de Hola.
3. Después de importa configuración de hello, eliminar Hola publicar el archivo de configuración. Ya no es necesario y contiene información confidencial relacionada con su suscripción de Azure.

### <a name="create-an-app-service-web-app"></a>Crear una aplicación web del Servicio de aplicaciones
1. Desde la línea de comandos de hello, cambiar directorios toohello **tasklist** directory.
2. Usar hello después comando toocreate una nueva aplicación web.
   
        azure site create --git
   
    Se le pedirá que especifique para la ubicación y el nombre de la aplicación hello. Proporcione un nombre único y seleccione Hola misma ubicación geográfica que la cuenta de almacenamiento de Azure.
   
    Hola `--git` parámetro crea un repositorio Git en Azure para esta aplicación web. También inicializa un repositorio Git en el directorio actual de hello si no existe y agrega un [Git remoto] denominado "azure", que es usado toopublish Hola aplicación tooAzure. Por último, crea un **web.config** archivo, que contiene la configuración utilizada por las aplicaciones de Azure toohost nodo. Si se omite hello `--git` parámetro pero Hola directorio contiene un repositorio Git, comando hello seguirá creando remoto hello 'azure'.
   
    Cuando haya completado este comando, verá el siguiente toohello similar de salida. Tenga en cuenta que Hola línea a partir **sitio Web creado en** contiene la dirección URL de hello para la aplicación web de Hola.
   
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
   > Si se trata de hello primer servicio de aplicaciones web app para su suscripción, estará siguiendo las instrucciones toouse Hola Portal de Azure toocreate hello web app. Para obtener más información, consulte [Compilación e implementación de una aplicación web de Node.js en el Servicio de aplicaciones de Azure].
   > 
   > 

### <a name="set-environment-variables"></a>Establecimiento de variables de entorno
En este paso, agregará la configuración de aplicaciones de web de tooyour de variables de entorno en Azure.
Desde la línea de comandos de hello, escriba Hola siguiente:

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


Reemplace  **<storage account name>**  con el nombre de Hola de almacenamiento de hello de la cuenta que creó anteriormente y reemplace  **<storage access key>**  con la clave de acceso principal de hello para la cuenta de almacenamiento. (Usar Hola mismo valores como archivo config.json hello que creó anteriormente).

Como alternativa, puede establecer las variables de entorno en hello [Portal de Azure](https://portal.azure.com/):

1. Abra la hoja de la aplicación hello web haciendo clic en **examinar** > **aplicaciones Web** > el nombre de la aplicación web.
2. En la hoja de la aplicación web, haga clic en **All Settings** (Toda la configuración)  > **Configuración de la aplicación**.
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. Desplácese hacia abajo toohello **configuración de la aplicación** agregar pares de clave/valor de Hola y la sección.
   
     ![Configuración de la aplicación](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. Haga clic en **GUARDAR**.

### <a name="publish-hello-application"></a>Publicar la aplicación hello
aplicación de hello toopublish, confirmar tooGit de archivos de código de hello y, a continuación, empújelo tooazure/maestro.

1. Restablezca las credenciales de implementación.
   
        azure site deployment user set <name> <password>
2. Agregue y confirme los archivos de aplicación.
   
        git add .
        git commit -m "adding files"
3. Insertar Hola confirmación toohello aplicación de servicio de aplicaciones web:
   
        git push azure master
   
    Use **maestro** como la bifurcación de destino de Hola. Al final de Hola de implementación de hello, verá un toohello similar de instrucción siguiente ejemplo:
   
        toohttps://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. Una vez completada la operación de inserción de hello, examinar la URL de la aplicación web toohello devuelta previamente por hello `azure create site` tooview de comandos de la aplicación.

## <a name="next-steps"></a>Pasos siguientes
Mientras pasos hello en este artículo describen el uso de información de toostore de servicio de la tabla de Hola, también puede usar [MongoDB](https://mlab.com/azure/). 

## <a name="additional-resources"></a>Recursos adicionales
[CLI de Azure]

## <a name="whats-changed"></a>Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

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
