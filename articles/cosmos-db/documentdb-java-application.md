---
title: tutorial de desarrollo de aplicaciones aaaJava con la base de datos de Azure Cosmos | Documentos de Microsoft
description: "Este tutorial de aplicación web de Java muestra cómo toouse Hola base de datos de Azure Cosmos Hola toostore de API de documentos y obtener acceso a datos desde una aplicación de Java hospedada en sitios Web de Azure."
keywords: Application development, database tutorial, java application, java web application tutorial, documentdb, azure, Microsoft azure
services: cosmos-db
documentationcenter: java
author: dennyglee
manager: jhubbard
editor: mimig
ms.assetid: 0867a4a2-4bf5-4898-a1f4-44e3868f8725
ms.service: cosmos-db
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 08/22/2017
ms.author: denlee
ms.openlocfilehash: e073de23beb0037ee1e37b48a69e8fe7cdc3fc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-hello-documentdb-api"></a>Compilar una aplicación web de Java con base de datos de Azure Cosmos y Hola API de documentos
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

Este tutorial de aplicación web de Java muestra cómo hello toouse [base de datos de Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) servicio toostore y acceso a los datos desde una aplicación de Java que se hospeda en aplicaciones de Web del servicio de aplicación de Azure. En este tema, aprenderá:

* ¿Cómo toobuild una aplicación básica de JavaServer Pages (JSP) en Eclipse.
* Cómo toowork con base de datos de Azure Cosmos hello service utilizando hello [SDK de Java de base de datos de Azure Cosmos](https://github.com/Azure/azure-documentdb-java).

Este tutorial de la aplicación de Java muestra cómo las tareas de aplicación de administración de tareas de toocreate basada en web que permite marcar, recuperar y se toocreate como completada, tal como se muestra en hello después de la imagen. Cada una de las tareas de hello en la lista de tareas de Hola se almacenan como documentos JSON en la base de datos de Azure Cosmos.

![Aplicación Java My ToDo List](./media/documentdb-java-application/image1.png)

> [!TIP]
> En este tutorial de desarrollo de aplicaciones se supone que tiene experiencia anterior en el uso de Java. Si es nuevo tooJava o hello [herramientas requisitos previos](#Prerequisites), le recomendamos que descargue Hola completa [tareas](https://github.com/Azure-Samples/documentdb-java-todo-app) proyecto desde GitHub y compilarlas mediante [Hola instrucciones final Hola de este artículo](#GetProject). Una vez que se generan, puede revisar una visión general de hello artículo toogain en código de hello en contexto de Hola de proyecto Hola.  
> 
> 

## <a id="Prerequisites"></a>Requisitos previos para este tutorial de aplicación web de Java
Antes de empezar este tutorial de desarrollo de aplicaciones, debe tener el siguiente hello:

* Una cuenta de Azure activa. En caso de no tener cuenta, puede crear una de evaluación gratuita en tan solo unos minutos. Para más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).

    OR

    Una instalación local de hello [emulador de base de datos de Azure Cosmos](local-emulator.md).
* <seg>
  [Kit de desarrollo de Java (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</seg>
* [IDE de Eclipse para desarrolladores de Java EE.](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [Un sitio web de Azure con un entorno de tiempo de ejecución Java (por ejemplo, Tomcat o Jetty) habilitado.](../app-service-web/web-sites-java-get-started.md)

Si va a instalar estas herramientas para hello primera vez, coreservlets.com proporciona un ejemplo paso a paso del proceso de instalación de hello en la sección de inicio rápido de Hola de sus [Tutorial: instalar TomCat7 y su uso con Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) artículo.

## <a id="CreateDB"></a>Paso 1: Creación de una cuenta de Azure Cosmos DB
Para comenzar, creemos una cuenta de Azure Cosmos DB. Si ya tiene una cuenta o si usas Hola emulador de base de datos de Azure Cosmos para este tutorial, puede omitir demasiado[paso 2: crear la aplicación de Java JSP hello](#CreateJSP).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <a id="CreateJSP"></a>Paso 2: Crear la aplicación de Java JSP hello
Hola toocreate aplicación JSP:

1. En primer lugar, empezaremos por la creación de un proyecto Java. Inicie Eclipse, haga clic en **File** (Archivo), haga clic en **New** (Nuevo) y luego haga clic en **Dynamic Web Project** (Proyecto web dinámico). Si no ve **Dynamic Web Project** aparece como proyecto disponible, Hola siguientes: haga clic en **archivo**, haga clic en **New**, haga clic en **proyecto**..., expanda **Web**, haga clic en **Dynamic Web Project**y haga clic en **siguiente**.
   
    ![Desarrollo de aplicaciones Java JSP](./media/documentdb-java-application/image10.png)
2. Escriba un nombre de proyecto en hello **nombre del proyecto** cuadro y en hello **en tiempo de ejecución de destino** menú desplegable, seleccione opcionalmente un valor (por ejemplo, Apache Tomcat v7.0) y, a continuación, haga clic en **finalizar**. Al seleccionar un tiempo de ejecución de destino permite toorun el proyecto de forma local a través de Eclipse.
3. En Eclipse, en la vista de explorador de proyectos de hello, expanda el proyecto. Haga clic con el botón derecho en **WebContent**, haga clic en **New** (Nuevo) y, después, en **JSP File** (Archivo JSP).
4. Hola **New JSP File** cuadro de diálogo, archivo de nombre hello **index.jsp**. Mantenga la carpeta principal de hello como **WebContent**, tal y como se muestra en Hola la siguiente ilustración y, a continuación, haga clic en **siguiente**.
   
    ![Creación de un nuevo archivo JSP - Tutorial de aplicación web de Java](./media/documentdb-java-application/image11.png)
5. Hola **Select JSP Template** cuadro de diálogo, a fin de Hola de este tutorial, seleccione **New JSP File (html)**y, a continuación, haga clic en **finalizar**.
6. Cuando se abre el archivo index.jsp de hello en Eclipse, agregar texto toodisplay **Hola a todos!** dentro de hello existente <body> elemento. Su actualizada <body> contenido debería ser similar a Hola siguiente código:
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. Guarde el archivo index.jsp de hello.
8. Si establece un tiempo de ejecución de destino en el paso 2, haga clic en **proyecto** y, a continuación, **ejecutar** toorun localmente la aplicación JSP:
   
    ![Hello World – Tutorial de aplicación de Java](./media/documentdb-java-application/image12.png)

## <a id="InstallSDK"></a>Paso 3: Instalar Hola SDK de Java de documentos
Hola toopull de manera más fácil de hello SDK de Java de documentos y sus dependencias es a través de [Maven Apache](http://maven.apache.org/).

toodo esto, necesitará tooconvert los proyectos de maven tooa siguiendo los pasos de hello:

1. Haga clic en el proyecto en el Explorador de proyectos de Hola, haga clic en **configurar**, haga clic en **convertir tooMaven proyecto**.
2. Hola **crear nueva POM** ventana, acepte los valores predeterminados de Hola y haga clic en **finalizar**.
3. En **el Explorador de proyectos**, abra archivos de pom.xml Hola.
4. En hello **dependencias** ficha Hola **dependencias** panel, haga clic en **agregar**.
5. Hola **seleccione dependencia** ventana, Hola siguientes:
   
   * Hola **Id. de grupo** cuadro, escriba com.microsoft.azure.
   * Hola **el identificador del artefacto** cuadro, escriba documentos de azure.
   * Hola **versión** cuadro, escriba 1.5.1.
     
   ![Instalación del SDK de la aplicación Java en DocumentDB](./media/documentdb-java-application/image13.png)
     
   * O Agregar dependencia Hola XML para el Id. de grupo y el identificador del artefacto directamente toohello pom.xml a través de un editor de texto:
     
        <dependency><groupId>com.microsoft.azure</groupId><artifactId>azure-documentdb</artifactId><version>1.9.1</version></dependency>
6. Haga clic en **Aceptar** y Maven instalará Hola SDK de Java de documentos.
7. Guarde el archivo de hello pom.xml.

## <a id="UseService"></a>Paso 4: Usar servicio de base de datos de Azure Cosmos hello en una aplicación de Java
1. En primer lugar, vamos a definir objeto TodoItem de hello en TodoItem.java:
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    En este proyecto, usamos [proyecto Lombok](http://projectlombok.org/) toogenerate Hola constructor, captadores, establecedores y un generador. Como alternativa, puede escribir este código manualmente o hacer Hola IDE generarlo.
2. servicio de base de datos de Azure Cosmos de hello tooinvoke, debe crear instancias de un nuevo **DocumentClient**. En general, es mejor hello tooreuse **DocumentClient** : en lugar de construir un nuevo cliente para cada solicitud subsiguiente. Se puede reutilizar cliente hello ajustando cliente hello en un **DocumentClientFactory**. En DocumentClientFactory.java, se necesita el valor de identificador URI y la clave principal de la Hola de toopaste guardó Portapapeles tooyour en [paso 1](#CreateDB). Reemplace [YOUR\_ENDPOINT\_HERE] por el URI y reemplace [YOUR\_KEY\_HERE] por su CLAVE PRINCIPAL.
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. Ahora vamos a crear un tooabstract de objeto de acceso a datos (DAO) conservar nuestro tooAzure de elementos de lista de tareas Cosmos DB.
   
    En orden toosave cuantos elementos colección tooa, Hola debe cliente tooknow qué base de datos y la colección toopersist demasiado (al que hace referencia Self-Link). En general, es mejor base de datos de toocache hello y colección siempre que sea posible base de datos de toohello de tooavoid adicionales de ida y vuelta.
   
    Hello código siguiente muestra cómo tooretrieve nuestra base de datos y la colección, si existe, o cree uno nuevo si no existe:
   
        public class DocDbDao implements TodoDao {
            // hello name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // hello name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // hello Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for hello database object, so we don't have tooquery for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for hello collection object, so we don't have tooquery for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get hello database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache hello database object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create hello database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get hello collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache hello collection object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create hello collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. paso siguiente Hello es toowrite algunos hello de toopersist de código TodoItems en colección toohello. En este ejemplo, usaremos [Gson](https://code.google.com/p/google-gson/) tooserialize y deserializar documentos de tooJSON TodoItem Java objetos estándar (POJOs).
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize hello TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate hello document as a TodoItem for retrieval (so that we can
            // store multiple entity types in hello collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist hello document using hello DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. Al igual que las colecciones y las bases de datos de Azure Cosmos DB, a los documentos también se hace referencia mediante autovínculos. Hola siguientes auxiliar función permite nos recuperar documentos por otro atributo (por ejemplo, "id") en lugar de vínculos propios:
   
        private Document getDocumentById(String id) {
            // Retrieve hello document using hello DocumentClient.
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.id='" + id + "'", null)
                    .getQueryIterable().toList();
   
            if (documentList.size() > 0) {
                return documentList.get(0);
            } else {
                return null;
            }
        }
6. Podemos usar el método de aplicación auxiliar de hello en el paso 5 tooretrieve un documento TodoItem JSON por Id. de y deserializarla tooa POJO:
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve hello document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize hello document in tooa TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. También podemos utilizar hello DocumentClient tooget una colección o lista de TodoItems mediante SQL de DocumentDB:
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve hello TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize hello documents in tooTodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. Un documento con hello DocumentClient no hay tooupdate de muchas maneras. En nuestra aplicación de lista de tareas, queremos toobe capaz de tootoggle si un TodoItem ha finalizado. Esto puede lograrse mediante la actualización de un atributo "completa" en el documento de Hola Hola:
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve hello document from hello database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update hello document as a JSON document directly.
            // For more complex operations - you could de-serialize hello document in
            // tooa POJO, update hello POJO, and then re-serialize hello POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace hello updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. Por último, queremos Hola capacidad toodelete un TodoItem de nuestra lista. toodo, podemos utilizar el método de aplicación auxiliar de hello indicamos anteriormente tooretrieve Hola vínculos propios y, a continuación, indicar Hola cliente toodelete:
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers toodocuments by self link rather than id.
   
            // Query for hello document tooretrieve hello self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete hello document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <a id="Wire"></a>Paso 5: El resto de Hola de Hola de proyecto de desarrollo de aplicaciones de Java cableado juntos
Ahora que hemos terminado fun Hola bits: lo único que queda es toobuild una interfaz de usuario rápida y vincularla tooour DAO.

1. En primer lugar, puede empezar con la creación de un controlador toocall nuestro DAO:
   
        public class TodoItemController {
            public static TodoItemController getInstance() {
                if (todoItemController == null) {
                    todoItemController = new TodoItemController(TodoDaoFactory.getDao());
                }
                return todoItemController;
            }
   
            private static TodoItemController todoItemController;
   
            private final TodoDao todoDao;
   
            TodoItemController(TodoDao todoDao) {
                this.todoDao = todoDao;
            }
   
            public TodoItem createTodoItem(@NonNull String name,
                    @NonNull String category, boolean isComplete) {
                TodoItem todoItem = TodoItem.builder().name(name).category(category)
                        .complete(isComplete).build();
                return todoDao.createTodoItem(todoItem);
            }
   
            public boolean deleteTodoItem(@NonNull String id) {
                return todoDao.deleteTodoItem(id);
            }
   
            public TodoItem getTodoItemById(@NonNull String id) {
                return todoDao.readTodoItem(id);
            }
   
            public List<TodoItem> getTodoItems() {
                return todoDao.readTodoItems();
            }
   
            public TodoItem updateTodoItem(@NonNull String id, boolean isComplete) {
                return todoDao.updateTodoItem(id, isComplete);
            }
        }
   
    En una aplicación más compleja, controlador de hello puede alojar lógica de negocios complicado sobre Hola DAO.
2. A continuación, vamos a crear un controlador de toohello de las solicitudes de servlet tooroute HTTP:
   
        public class TodoServlet extends HttpServlet {
            // API Keys
            public static final String API_METHOD = "method";
   
            // API Methods
            public static final String CREATE_TODO_ITEM = "createTodoItem";
            public static final String GET_TODO_ITEMS = "getTodoItems";
            public static final String UPDATE_TODO_ITEM = "updateTodoItem";
   
            // API Parameters
            public static final String TODO_ITEM_ID = "todoItemId";
            public static final String TODO_ITEM_NAME = "todoItemName";
            public static final String TODO_ITEM_CATEGORY = "todoItemCategory";
            public static final String TODO_ITEM_COMPLETE = "todoItemComplete";
   
            public static final String MESSAGE_ERROR_INVALID_METHOD = "{'error': 'Invalid method'}";
   
            private static final long serialVersionUID = 1L;
            private static final Gson gson = new Gson();
   
            @Override
            protected void doGet(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
   
                String apiResponse = MESSAGE_ERROR_INVALID_METHOD;
   
                TodoItemController todoItemController = TodoItemController
                        .getInstance();
   
                String id = request.getParameter(TODO_ITEM_ID);
                String name = request.getParameter(TODO_ITEM_NAME);
                String category = request.getParameter(TODO_ITEM_CATEGORY);
                boolean isComplete = StringUtils.equalsIgnoreCase("true",
                        request.getParameter(TODO_ITEM_COMPLETE)) ? true : false;
   
                switch (request.getParameter(API_METHOD)) {
                case CREATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.createTodoItem(name,
                            category, isComplete));
                    break;
                case GET_TODO_ITEMS:
                    apiResponse = gson.toJson(todoItemController.getTodoItems());
                    break;
                case UPDATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.updateTodoItem(id,
                            isComplete));
                    break;
                default:
                    break;
                }
   
                response.getWriter().println(apiResponse);
            }
   
            @Override
            protected void doPost(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
                doGet(request, response);
            }
        }
3. Necesitaremos un usuario de toohello web toodisplay de interfaz de usuario. Vamos a volver a escribir hello index.jsp que hemos creado con anterioridad:
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding toobody for fixed nav bar */
            body {
              padding-top: 50px;
            }
          </style>
        </head>
        <body>
          <!-- Nav Bar -->
          <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
            <div class="container">
              <div class="navbar-header">
                <a class="navbar-brand" href="#">My Tasks</a>
              </div>
            </div>
          </div>
   
          <!-- Body -->
          <div class="container">
            <h1>My ToDo List</h1>
   
            <hr/>
   
            <!-- hello ToDo List -->
            <div class = "todoList">
              <table class="table table-bordered table-striped" id="todoItems">
                <thead>
                  <tr>
                    <th>Name</th>
                    <th>Category</th>
                    <th>Complete</th>
                  </tr>
                </thead>
                <tbody>
                </tbody>
              </table>
   
              <!-- Update Button -->
              <div class="todoUpdatePanel">
                <form class="form-horizontal" role="form">
                  <button type="button" class="btn btn-primary">Update Tasks</button>
                </form>
              </div>
   
            </div>
   
            <hr/>
   
            <!-- Item Input Form -->
            <div class="todoForm">
              <form class="form-horizontal" role="form">
                <div class="form-group">
                  <label for="inputItemName" class="col-sm-2">Task Name</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemName" placeholder="Enter name">
                  </div>
                </div>
   
                <div class="form-group">
                  <label for="inputItemCategory" class="col-sm-2">Task Category</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemCategory" placeholder="Enter category">
                  </div>
                </div>
   
                <button type="button" class="btn btn-primary">Add Task</button>
              </form>
            </div>
   
          </div>
   
          <!-- Placed at hello end of hello document so hello pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. Por último, escribir alguna interfaz de usuario web de cliente JavaScript tootie Hola y Hola servlet juntos:
   
        var todoApp = {
          /*
           * API methods toocall Java backend.
           */
          apiEndpoint: "api",
   
          createTodoItem: function(name, category, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "createTodoItem",
                "todoItemName": name,
                "todoItemCategory": category,
                "todoItemComplete": isComplete
              },
              function(data) {
                var todoItem = data;
                todoApp.addTodoItemToTable(todoItem.id, todoItem.name, todoItem.category, todoItem.complete);
              },
              "json");
          },
   
          getTodoItems: function() {
            $.post(todoApp.apiEndpoint, {
                "method": "getTodoItems"
              },
              function(data) {
                var todoItemArr = data;
                $.each(todoItemArr, function(index, value) {
                  todoApp.addTodoItemToTable(value.id, value.name, value.category, value.complete);
                });
              },
              "json");
          },
   
          updateTodoItem: function(id, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "updateTodoItem",
                "todoItemId": id,
                "todoItemComplete": isComplete
              },
              function(data) {},
              "json");
          },
   
          /*
           * UI Methods
           */
          addTodoItemToTable: function(id, name, category, isComplete) {
            var rowColor = isComplete ? "active" : "warning";
   
            todoApp.ui_table().append($("<tr>")
              .append($("<td>").text(name))
              .append($("<td>").text(category))
              .append($("<td>")
                .append($("<input>")
                  .attr("type", "checkbox")
                  .attr("id", id)
                  .attr("checked", isComplete)
                  .attr("class", "isComplete")
                ))
              .addClass(rowColor)
            );
          },
   
          /*
           * UI Bindings
           */
          bindCreateButton: function() {
            todoApp.ui_createButton().click(function() {
              todoApp.createTodoItem(todoApp.ui_createNameInput().val(), todoApp.ui_createCategoryInput().val(), false);
              todoApp.ui_createNameInput().val("");
              todoApp.ui_createCategoryInput().val("");
            });
          },
   
          bindUpdateButton: function() {
            todoApp.ui_updateButton().click(function() {
              // Disable button temporarily.
              var myButton = $(this);
              var originalText = myButton.text();
              $(this).text("Updating...");
              $(this).prop("disabled", true);
   
              // Call api tooupdate todo items.
              $.each(todoApp.ui_updateId(), function(index, value) {
                todoApp.updateTodoItem(value.name, value.value);
                $(value).remove();
              });
   
              // Re-enable button.
              setTimeout(function() {
                myButton.prop("disabled", false);
                myButton.text(originalText);
              }, 500);
            });
          },
   
          bindUpdateCheckboxes: function() {
            todoApp.ui_table().on("click", ".isComplete", function(event) {
              var checkboxElement = $(event.currentTarget);
              var rowElement = $(event.currentTarget).parents('tr');
              var id = checkboxElement.attr('id');
              var isComplete = checkboxElement.is(':checked');
   
              // Toggle table row color
              if (isComplete) {
                rowElement.addClass("active");
                rowElement.removeClass("warning");
              } else {
                rowElement.removeClass("active");
                rowElement.addClass("warning");
              }
   
              // Update hidden inputs for update panel.
              todoApp.ui_updateForm().children("input[name='" + id + "']").remove();
   
              todoApp.ui_updateForm().append($("<input>")
                .attr("type", "hidden")
                .attr("class", "updateComplete")
                .attr("name", id)
                .attr("value", isComplete));
   
            });
          },
   
          /*
           * UI Elements
           */
          ui_createNameInput: function() {
            return $(".todoForm #inputItemName");
          },
   
          ui_createCategoryInput: function() {
            return $(".todoForm #inputItemCategory");
          },
   
          ui_createButton: function() {
            return $(".todoForm button");
          },
   
          ui_table: function() {
            return $(".todoList table tbody");
          },
   
          ui_updateButton: function() {
            return $(".todoUpdatePanel button");
          },
   
          ui_updateForm: function() {
            return $(".todoUpdatePanel form");
          },
   
          ui_updateId: function() {
            return $(".todoUpdatePanel .updateComplete");
          },
   
          /*
           * Install hello TodoApp
           */
          install: function() {
            todoApp.bindCreateButton();
            todoApp.bindUpdateButton();
            todoApp.bindUpdateCheckboxes();
   
            todoApp.getTodoItems();
          }
        };
   
        $(document).ready(function() {
          todoApp.install();
        });
5. ¡Increíble! Ahora todo lo que queda es aplicación de hello tootest. Ejecutar la aplicación hello localmente y agregue algunos elementos de lista de tareas Rellenar en nombre del elemento de hello y una categoría y haciendo clic en **agregar tarea**.
6. Cuando aparezca el elemento de hello, puede actualizar si ha finalizado o desactiva la casilla de verificación de Hola y haciendo clic en **actualizar tareas**.

## <a id="Deploy"></a>Paso 6: Implementar el tooAzure de aplicación de Java sitios Web
Azure WebSites consigue que la implementación de aplicaciones de Java sea tan sencilla como exportar su aplicación como un archivo WAR y cargarla mediante el control de código fuente (por ejemplo, Git) o FTP.

1. tooexport la aplicación como un archivo WAR, haga clic en el proyecto en **el Explorador de proyectos**, haga clic en **exportar**y, a continuación, haga clic en **archivo WAR**.
2. Hola **exportar WAR** ventana, Hola siguientes:
   
   * En el cuadro del proyecto Web hello, escriba azure-documentdb-java-sample.
   * En el cuadro de destino de hello, elija un archivo WAR de destino toosave Hola.
   * Haga clic en **Finalizar**
3. Ahora que tiene a mano en un archivo WAR, puede simplemente cargarlo tooyour sitio Web de Azure **móviles** directory. Para obtener instrucciones acerca de cómo cargar archivo hello, consulte [agregar una tooAzure de aplicación de Java aplicación del servicio de aplicaciones Web](../app-service-web/web-sites-java-add-app.md).
   
    Una vez que el archivo WAR de hello es el directorio de aplicaciones Web de toohello cargado, entorno de tiempo de ejecución de hello detectará que haya agregado y lo cargará automáticamente.
4. tooview el producto acabado, navegue toohttp://YOUR\_sitio\_NAME.azurewebsites.net/azure-java-sample/ y empezar a agregar sus tareas.

## <a id="GetProject"></a>Obtener proyecto Hola desde GitHub
Todos los ejemplos de hello en este tutorial se incluyen en hello [tareas](https://github.com/Azure-Samples/documentdb-java-todo-app) proyecto en GitHub. proyecto de lista de tareas de tooimport hello en Eclipse, asegúrese de tener software de Hola y recursos que aparecen en hello [requisitos previos](#Prerequisites) sección, a continuación, Hola siguientes:

1. Instale [Project Lombok](http://projectlombok.org/). Lombok es toogenerate usado constructores, captadores, establecedores en proyecto de Hola. Una vez que ha descargado el archivo de lombok.jar hello, haga doble clic en él tooinstall, o instalar desde la línea de comandos de Hola.
2. Si Eclipse está abierto, ciérrelo y reinicie tooload Lombok.
3. En Eclipse, en hello **archivo** menú, haga clic en **importación**.
4. Hola **importación** ventana, haga clic en **Git**, haga clic en **proyectos desde Git**y, a continuación, haga clic en **siguiente**.
5. En hello **Seleccionar origen de repositorio** pantalla, haga clic en **clon URI**.
6. En hello **repositorio de código fuente Git** pantalla Hola **URI** cuadro, escriba https://github.com/Azure-Samples/java-todo-app.git y, a continuación, haga clic en **siguiente**.
7. En hello **selección rama** pantalla, asegúrese de que **maestro** está seleccionada y, a continuación, haga clic en **siguiente**.
8. En hello **destino Local** pantalla, haga clic en **examinar** tooselect una carpeta donde se pueden copiar repositorio hello y, a continuación, haga clic en **siguiente**.
9. En hello **seleccionar un toouse del Asistente para importar proyectos** pantalla, asegúrese de que **importar proyectos existentes** está seleccionada y, a continuación, haga clic en **siguiente**.
10. En hello **importar proyectos** pantalla, anule la selección de hello **DocumentDB** del proyecto y, a continuación, haga clic en **finalizar**. proyecto de documentos de Hello contiene hello Azure Cosmos DB SDK de Java, que se agregará como una dependencia en su lugar.
11. En **el Explorador de proyectos**, desplácese tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java y sustituirlos por valores HOST y MASTER_KEY Hola Hola URI y la clave principal para la cuenta de base de datos de Azure Cosmos y, a continuación, guardar el archivo hello. Para obtener más información, consulte el [paso 1. Creación de una cuenta de base de datos de Azure Cosmos DB](#CreateDB).
12. En **el Explorador de proyectos**, haga clic en hello **azure-documentdb-java-sample**, haga clic en **Build Path**y, a continuación, haga clic en **configurar Build Path**.
13. En hello **Java Build Path** pantalla, en el panel derecho de hello, seleccione hello **bibliotecas** ficha y, a continuación, haga clic en **agregar JAR externo**. Navegue toohello ubicación del archivo de lombok.jar hello y haga clic en **abiertos**y, a continuación, haga clic en **Aceptar**.
14. Hola de uso paso 12 tooopen **propiedades** ventana nuevo y, a continuación, en el panel izquierdo de hello haga clic en **tiempos de ejecución de destino**.
15. En hello **tiempos de ejecución de destino** pantalla, haga clic en **New**, seleccione **Apache Tomcat v7.0**y, a continuación, haga clic en **Aceptar**.
16. Hola de uso paso 12 tooopen **propiedades** ventana nuevo y, a continuación, en el panel izquierdo de hello haga clic en **facetas de proyecto**.
17. En hello **proyecto facetas** pantalla, seleccione **módulo Web dinámico** y **Java**y, a continuación, haga clic en **Aceptar**.
18. En hello **servidores** pestaña final Hola de pantalla de bienvenida, haga clic en **Tomcat v7.0 Server en localhost** y, a continuación, haga clic en **agregar y quitar**.
19. En hello **agregar y quitar** ventana, mover **azure-documentdb-java-sample** toohello **configurado** cuadro y, a continuación, haga clic en **finalizar**.
20. Hola **servidores** pestaña, haga clic en **Tomcat v7.0 Server en localhost**y, a continuación, haga clic en **reiniciar**.
21. En un explorador, navegue toohttp://localhost:8080 / azure-documentdb-java-sample / y comenzar a agregar la lista de tareas de tooyour. Tenga en cuenta que si cambia los valores de puerto predeterminado, cambie el valor de toohello de 8080 seleccionado.
22. vea el sitio web de Azure, de proyecto tooan de toodeploy [paso 6. Implementar los sitios Web de aplicación tooAzure](#Deploy).

[1]: media/documentdb-java-application/keys.png
