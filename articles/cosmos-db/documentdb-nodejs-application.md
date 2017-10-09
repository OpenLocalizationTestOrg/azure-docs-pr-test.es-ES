---
title: "una aplicación web de Node.js para la base de datos de Azure Cosmos aaaBuild | Documentos de Microsoft"
description: "Este tutorial Node.js explora cómo toouse datos de base de datos de Microsoft Azure Cosmos toostore y acceso desde una aplicación web de Node.js Express se hospeda en sitios Web de Azure."
keywords: "Desarrollo de aplicaciones, tutorial de base de datos, información sobre node.js, tutorial de node.js"
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 9da9e63b-e76a-434e-96dd-195ce2699ef3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: mimig
ms.openlocfilehash: 31194dccf37eef69d2219b0d8328a88d434f79b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="_Toc395783175"></a>Creación de una aplicación web de Node.js con Azure Cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

Este tutorial Node.js muestra cómo se hospedan hello documentos API toostore y datos de acceso desde una aplicación de Node.js Express y toouse base de datos de Azure Cosmos en sitios Web de Azure. Compile una aplicación de administración de tareas basadas en web sencilla, una aplicación ToDo, que permite crear, recuperar y completar tareas. tareas de Hola se almacenan como documentos JSON en la base de datos de Azure Cosmos. Este tutorial le guía a través de la creación de hello y la implementación de la aplicación hello y explica lo que sucede en cada fragmento de código.

![Captura de pantalla de aplicación de mi lista de tareas creada en este tutorial Node.js Hola](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

¿No tener tiempo toocomplete Hola tutorial y simplemente desea solución completa de hello tooget? No hay problema, puede obtener la solución de ejemplo completo de Hola desde [GitHub][GitHub]. Tan solo los lee hello [Léame](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) archivo para obtener instrucciones sobre cómo toorun Hola aplicación.

## <a name="_Toc395783176"></a>Requisitos previos
> [!TIP]
> En este tutorial de Node.js se presupone que tiene experiencia previa con el uso de Node.js y los sitios web de Azure.
> 
> 

Antes de seguir las instrucciones de hello en este artículo, debe asegurarse de que tiene Hola siguientes:

* Una cuenta de Azure activa. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).

   OR

   Una instalación local de hello [emulador de base de datos de Azure Cosmos](local-emulator.md) (sólo Windows).
* [Node.js][Node.js] versión v0.10.29 o superior.
* [Express Generator](http://www.expressjs.com/starter/generator.html) (puede instalarlo mediante `npm install express-generator -g`)
* [Git][Git].

## <a name="_Toc395637761"></a>Paso 1: Creación de una cuenta de base de datos de Azure Cosmos DB
Para comenzar, creemos una cuenta de Azure Cosmos DB. Si ya tiene una cuenta o si usas Hola emulador de base de datos de Azure Cosmos para este tutorial, puede omitir demasiado[paso 2: crear una nueva aplicación de Node.js](#_Toc395783178).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <a name="_Toc395783178"></a>Paso 2: Creación de una aplicación Node.js
Ahora vamos a aprender toocreate un proyecto básico de Hello World Node.js con hello [Express](http://expressjs.com/) framework.

1. Abra su terminal favorito, como símbolo de hello Node.js.
2. Navegue directorio toohello en el que desea nueva aplicación de toostore Hola.
3. Usar Hola generador express toogenerate llama a una nueva aplicación **tareas**.
   
        express todo
4. Abra el nuevo directorio **todo** e instale las dependencias.
   
        cd todo
        npm install
5. Ejecute la nueva aplicación.
   
        npm start
6. Puede ver la nueva aplicación llevando el explorador demasiado[http://localhost:3000](http://localhost:3000).
   
    ![Obtenga información acerca de Node.js - captura de pantalla de hello aplicación Hola a todos en una ventana del explorador](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    A continuación, toostop Hola aplicación, presione CTRL+C en la ventana de terminal de hello y, a continuación, haga clic en **y** proceso por lotes de tooterminate Hola.

## <a name="_Toc395783179"></a>Paso 3: Instalación de módulos adicionales
Hola **package.json** archivo es uno de los archivos de hello creados en hello raíz del proyecto de Hola. Este archivo contiene una lista de módulos adicionales necesarios para una aplicación Node.js. Más adelante, cuando se implementa esta tooAzure aplicación sitios Web, este archivo es utilizado toodetermine qué toobe de necesidad de módulos instalados en Azure toosupport la aplicación. Se sigue necesitan tooinstall dos más paquetes para este tutorial.

1. Nuevo en hello terminal, instalar hello **async** módulo a través de npm.
   
        npm install async --save
2. Instalar hello **documentdb** módulo a través de npm. Se trata de módulo de Hola donde ocurre mágico de base de datos de Azure Cosmos Hola todos los.
   
        npm install documentdb --save
3. Una comprobación rápida de hello **package.json** archivo de aplicación hello debe mostrar hello módulos adicionales. Este archivo se indican qué toodownload paquetes de Azure e instalar cuando se ejecuta la aplicación. Debe parecerse al siguiente ejemplo de Hola.
   
        {
          "name": "todo",
          "version": "0.0.0",
          "private": true,
          "scripts": {
            "start": "node ./bin/www"
          },
          "dependencies": {
            "async": "^2.1.4",
            "body-parser": "~1.15.2",
            "cookie-parser": "~1.4.3",
            "debug": "~2.2.0",
            "documentdb": "^1.10.0",
            "express": "~4.14.0",
            "jade": "~1.11.0",
            "morgan": "~1.7.0",
            "serve-favicon": "~2.3.0"
          }
        }
   
    Esto indica a Node (y a Azure más tarde) que la aplicación depende de estos módulos adicionales.

## <a name="_Toc395783180"></a>Paso 4: Usar el servicio de base de datos de Azure Cosmos hello en una aplicación de nodo
Que encarga de todo el programa de instalación inicial de Hola y la configuración, ahora vamos a get hacia abajo toowhy estamos aquí y se toowrite algunos programe con la base de datos de Azure Cosmos.

### <a name="create-hello-model"></a>Crear modelo Hola
1. En el directorio del proyecto hello, cree un directorio denominado **modelos** Hola mismo directorio que el archivo de hello package.json.
2. Hola **modelos** directorio, cree un nuevo archivo denominado **taskDao.js**. Este archivo contendrá el modelo de Hola para las tareas de hello creadas por la aplicación.
3. En Hola mismo **modelos** directorio, cree otro nuevo archivo denominado **docdbUtils.js**. Este archivo contendrá código útil y reutilizable que se utilizará en toda nuestra aplicación. 
4. Código de copia Hola siguiente en demasiado**docdbUtils.js**
   
        var DocumentDBClient = require('documentdb').DocumentClient;
   
        var DocDBUtils = {
            getOrCreateDatabase: function (client, databaseId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id= @id',
                    parameters: [{
                        name: '@id',
                        value: databaseId
                    }]
                };
   
                client.queryDatabases(querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        if (results.length === 0) {
                            var databaseSpec = {
                                id: databaseId
                            };
   
                            client.createDatabase(databaseSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            },
   
            getOrCreateCollection: function (client, databaseLink, collectionId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id=@id',
                    parameters: [{
                        name: '@id',
                        value: collectionId
                    }]
                };               
   
                client.queryCollections(databaseLink, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {        
                        if (results.length === 0) {
                            var collectionSpec = {
                                id: collectionId
                            };
   
                            client.createCollection(databaseLink, collectionSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            }
        };
   
        module.exports = DocDBUtils;
   
5. Guarde y cierre hello **docdbUtils.js** archivo.
6. En principio Hola de hello **taskDao.js** , agregue Hola después Hola de código tooreference **DocumentDBClient** hello y **docdbUtils.js** hemos creado anteriormente:
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. A continuación, agregará código toodefine y exportar el objeto de tarea de Hola. Esto es responsable de inicializar el objeto de tarea y la configuración de hello base de datos y la colección de documentos que se usará.
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. A continuación, agregue Hola siguiendo métodos adicionales de código toodefine en el objeto de tarea de hello, que permiten la interacción con los datos almacenados en la base de datos de Azure Cosmos.
   
        TaskDao.prototype = {
            init: function (callback) {
                var self = this;
   
                docdbUtils.getOrCreateDatabase(self.client, self.databaseId, function (err, db) {
                    if (err) {
                        callback(err);
                    } else {
                        self.database = db;
                        docdbUtils.getOrCreateCollection(self.client, self.database._self, self.collectionId, function (err, coll) {
                            if (err) {
                                callback(err);
   
                            } else {
                                self.collection = coll;
                            }
                        });
                    }
                });
            },
   
            find: function (querySpec, callback) {
                var self = this;
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results);
                    }
                });
            },
   
            addItem: function (item, callback) {
                var self = this;
   
                item.date = Date.now();
                item.completed = false;
   
                self.client.createDocument(self.collection._self, item, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, doc);
                    }
                });
            },
   
            updateItem: function (itemId, callback) {
                var self = this;
   
                self.getItem(itemId, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        doc.completed = true;
   
                        self.client.replaceDocument(doc._self, doc, function (err, replaced) {
                            if (err) {
                                callback(err);
   
                            } else {
                                callback(null, replaced);
                            }
                        });
                    }
                });
            },
   
            getItem: function (itemId, callback) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id = @id',
                    parameters: [{
                        name: '@id',
                        value: itemId
                    }]
                };
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results[0]);
                    }
                });
            }
        };
9. Guarde y cierre hello **taskDao.js** archivo. 

### <a name="create-hello-controller"></a>Crear controlador Hola
1. Hola **rutas** directorio del proyecto, cree un nuevo archivo denominado **tasklist.js**. 
2. Agregar Hola sigue código demasiado**tasklist.js**. Esto carga los módulos de hello DocumentDBClient y asincrónicas, que son usados por **tasklist.js**. Esto también define hello **TaskList** función, que se pasa una instancia de hello **tarea** objeto definimos anteriormente:
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. Continúe agregando toohello **tasklist.js** archivo mediante la adición de métodos de hello usa demasiado**showTasks, addTask**, y **completeTasks**:
   
        TaskList.prototype = {
            showTasks: function (req, res) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.completed=@completed',
                    parameters: [{
                        name: '@completed',
                        value: false
                    }]
                };
   
                self.taskDao.find(querySpec, function (err, items) {
                    if (err) {
                        throw (err);
                    }
   
                    res.render('index', {
                        title: 'My ToDo List ',
                        tasks: items
                    });
                });
            },
   
            addTask: function (req, res) {
                var self = this;
                var item = req.body;
   
                self.taskDao.addItem(item, function (err) {
                    if (err) {
                        throw (err);
                    }
   
                    res.redirect('/');
                });
            },
   
            completeTask: function (req, res) {
                var self = this;
                var completedTasks = Object.keys(req.body);
   
                async.forEach(completedTasks, function taskIterator(completedTask, callback) {
                    self.taskDao.updateItem(completedTask, function (err) {
                        if (err) {
                            callback(err);
                        } else {
                            callback(null);
                        }
                    });
                }, function goHome(err) {
                    if (err) {
                        throw err;
                    } else {
                        res.redirect('/');
                    }
                });
            }
        };
4. Guarde y cierre hello **tasklist.js** archivo.

### <a name="add-configjs"></a>Agregar config.js
1. En el directorio del proyecto, cree un nuevo archivo con el nombre **config.js**.
2. Agregue la Hola siguiente demasiado**config.js**. Así se definen las opciones de configuración y los valores necesarios para nuestra aplicación.
   
        var config = {}
   
        config.host = process.env.HOST || "[hello URI value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[hello PRIMARY KEY value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. Hola **config.js** de archivos, valores de hello de actualización de HOST y AUTH_KEY con valores de hello que se encuentran en la hoja de claves de saludo de la cuenta de base de datos de Azure Cosmos en hello [portal de Microsoft Azure](https://portal.azure.com).
4. Guarde y cierre hello **config.js** archivo.

### <a name="modify-appjs"></a>Modificar app.js
1. En el directorio del proyecto hello, abra hello **app.js** archivo. Este archivo se creó anteriormente cuando se creó la aplicación web de hello Express.
2. Agregar Hola después de la parte superior de toohello de código de **app.js**
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. Este código define toobe de archivo de configuración de hello usa y continúa tooread valores fuera de este archivo en algunas de las variables que se usará pronto.
4. Reemplace Hola después de dos líneas en **app.js** archivo:
   
        app.use('/', index);
        app.use('/users', users); 
   
      con hello siguiente fragmento de código:
   
        var docDbClient = new DocumentDBClient(config.host, {
            masterKey: config.authKey
        });
        var taskDao = new TaskDao(docDbClient, config.databaseId, config.collectionId);
        var taskList = new TaskList(taskDao);
        taskDao.init();
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
        app.set('view engine', 'jade');
5. Estas líneas definen una nueva instancia de nuestro **TaskDao** objeto, con un tooAzure de conexión nueva base de datos de Cosmos (utilizando los valores de hello leído en hello **config.js**), inicializar el objeto de tarea de hello y, a continuación, enlazar las acciones de formulario toomethods en nuestra **TaskList** controlador. 
6. Por último, guarde y cierre hello **app.js** archivo, casi acabamos.

## <a name="_Toc395783181"></a>Paso 5: Creación de una interfaz de usuario
Ahora vamos a activar la interfaz de usuario de atención toobuilding Hola para un usuario pueda interactuar realmente con nuestra aplicación. Hola aplicación Express creamos usa **Jade** como motor de vista de Hola. Para obtener más información sobre Jade consulte demasiado[http://jade-lang.com/](http://jade-lang.com/).

1. Hola **layout.jade** archivo Hola **vistas** directory se utiliza como plantilla global para otro **.jade** archivos. En este paso, modificará toouse [Bootstrap Twitter](https://github.com/twbs/bootstrap), que es un Kit de herramientas que hace más fácil toodesign un sitio Web de aspecto "nice". 
2. Abra hello **layout.jade** archivo se encuentra en hello **vistas** carpeta y reemplazar contenido Hola con siguiente hello:

    ```
    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body
        nav.navbar.navbar-inverse.navbar-fixed-top
          div.navbar-header
            a.navbar-brand(href='#') My Tasks
        block content
        script(src='//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js')
        script(src='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js')
    ```

    Esto indica eficazmente hello **Jade** motor toorender algo de HTML para nuestra aplicación y crea un **bloque** llama **contenido** donde poder proporcionar el diseño de Hola para nuestro contenido páginas.

    Guarde y cierre este archivo **layout.jade** .

3. Ahora, abra hello **index.jade** archivo, la vista de Hola que se usará en nuestra aplicación y reemplace el contenido de Hola de archivo hello con siguiente hello:
   
        extends layout
        block content
           h1 #{title}
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
                     td #{task.name}
                     td #{task.category}
                     - var date  = new Date(task.date);
                     - var day   = date.getDate();
                     - var month = date.getMonth() + 1;
                     - var year  = date.getFullYear();
                     td #{month + "/" + day + "/" + year}
                     td
                       input(type="checkbox", name="#{task.id}", value="#{!task.completed}", checked=task.completed)
             button.btn.btn-primary(type="submit") Update tasks
           hr
           form.well(action="/addtask", method="post")
             .form-group
               label(for="name") Item Name:
               input.form-control(name="name", type="textbox")
             .form-group
               label(for="category") Item Category:
               input.form-control(name="category", type="textbox")
             br
             button.btn(type="submit") Add item
   

Esto amplía el diseño y proporciona contenido de hello **contenido** marcador de posición que hemos visto en hello **layout.jade** versiones anteriores de archivos.
   
En este diseño hemos creado dos formularios HTML.

primera forma de Hello contiene una tabla de nuestros datos y un botón que nos permite tooupdate elementos publicando demasiado**/completetask** método de nuestro controlador.
    
segunda forma de Hello contiene dos campos de entrada y un botón que nos permite toocreate un nuevo elemento publicando demasiado**/addtask** método de nuestro controlador.

Debe ser todo lo que necesitamos para nuestro toowork de aplicación.

## <a name="_Toc395783181"></a>Paso 6: Ejecución de la aplicación de forma local
1. aplicación de hello tootest en el equipo local, ejecute `npm start` en Hola terminal toostart la aplicación, a continuación, actualice su [http://localhost:3000](http://localhost:3000) página del explorador. página de Hello debe ser ahora similar a la imagen de Hola a continuación:
   
    ![Captura de pantalla de hello aplicación MyTodo lista en una ventana del explorador](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > Si recibe un error acerca de la sangría de hello en archivos de layout.jade de Hola o hello index.jade, asegúrese de que las dos primeras líneas de hello en los dos archivos está justificado a la izquierda, sin espacios en blanco. Si hay espacios antes que dos primeras las hello, quitarlos, guardar ambos archivos, a continuación, actualice la ventana del explorador. 

2. Hola elemento, el nombre del elemento y la categoría campos tooenter una nueva tarea y, a continuación, haga clic en **Agregar elemento**. Esto crea un documento en Azure Cosmos DB con esas propiedades. 
3. página de Hello debe actualizar hello toodisplay recién creado del elemento de lista de tareas de Hola.
   
    ![Captura de pantalla de la aplicación hello con un nuevo elemento en la lista de tareas de Hola](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. toocomplete una tarea, solo tiene que activar casilla hello en la columna completa de hello y, a continuación, haga clic en **actualizar tareas**. Este documento de hello las actualizaciones que ya haya creado.

5. aplicación de hello toostop, presione CTRL+C en la ventana de terminal de hello y, a continuación, haga clic en **Y** proceso por lotes de tooterminate Hola.

## <a name="_Toc395783182"></a>Paso 7: Implementar el proyecto de desarrollo aplicación tooAzure sitios Web
1. Si todavía no lo ha hecho, habilite un repositorio para el sitio web de Azure. Encontrará instrucciones sobre cómo toodo esto en hello [tooAzure servicio de aplicaciones de la implementación de Git Local](../app-service-web/app-service-deploy-local-git.md) tema.
2. Agregue el sitio web de Azure como un git remoto.
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. Implementar mediante la inserción de toohello remoto.
   
        git push azure master
4. En pocos segundos, git terminará de publicar su aplicación web y ejecutará un explorador donde podrá ver su útil trabajo ejecutándose en Azure.

    ¡Enhorabuena! Acaba de compilar la primera Node.js Express aplicación Web con la base de datos de Azure Cosmos y haberlo publicado tooAzure sitios Web.

    Si desea que toodownload o consulte la aplicación de referencia completa de toohello para este tutorial, se puede descargar desde [GitHub][GitHub].

## <a name="_Toc395637775"></a>Pasos siguientes

* ¿Desea tooperform escala y rendimiento de pruebas con la base de datos de Azure Cosmos? Consulte [Pruebas de escala y rendimiento con Azure Cosmos DB](performance-testing.md)
* Obtenga información acerca de cómo demasiado[supervisar una cuenta de base de datos de Azure Cosmos](monitor-accounts.md).
* Ejecutar consultas en el conjunto de datos de ejemplo de Hola [Query Playground](https://www.documentdb.com/sql/demo).
* Explorar hello [documentación de la base de datos de Azure Cosmos](https://docs.microsoft.com/azure/documentdb/).

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

