---
title: una base de datos de documentos de base de datos de Azure Cosmos con Java aaaCreate | Documentos de Microsoft | Documentos de Microsoft
description: "Presenta un ejemplo de código de Java se puede usar tooconnect tooand consulta Hola API de documentos de base de datos de Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 08/02/2017
ms.author: mimig
ms.openlocfilehash: 400c9e7780034d3e28d749e734786e950edad22f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-hello-azure-portal"></a>Azure Cosmos DB: Crear una base de datos de documentos mediante Java y Hola portal de Azure

Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft. Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente. 

Este tutorial crea un documento de base de datos mediante Hola herramientas del portal Azure para la base de datos de Azure Cosmos. Este tutorial rápido muestra también cómo tooquickly crear una aplicación de consola de Java con hello [API de Java de DocumentDB](documentdb-sdk-java.md). instrucciones de Hello en este tutorial rápido se pueden aplicar en cualquier sistema operativo que sea capaz de ejecutar Java. Al completar este tutorial rápido estará familiarizado con la creación y modificación de los recursos de base de datos de documento en hello interfaz de usuario o mediante programación, lo que sea su preferencia.

## <a name="prerequisites"></a>Requisitos previos

* [Kit de desarrollo de Java (JDK) 1.7+](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * En Ubuntu, ejecute `apt-get install default-jdk` tooinstall Hola JDK.
    * Ser seguro tooset Hola JAVA_HOME entorno variable toopoint toohello carpeta donde está instalado Hola JDK.
* [Descargar](http://maven.apache.org/download.cgi) e [instalar](http://maven.apache.org/install.html) un archivo binario de [Maven](http://maven.apache.org/)
    * En Ubuntu, se pueden ejecutar `apt-get install maven` tooinstall Maven.
* [Git](https://www.git-scm.com/)
    * En Ubuntu, se pueden ejecutar `sudo apt-get install git` tooinstall Git.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Creación de una cuenta de base de datos

Antes de poder crear una base de datos de documento, debe toocreate una cuenta de base de datos SQL (documentos) con la base de datos de Azure Cosmos.

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Incorporación de una colección

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a>Agregar datos de ejemplo

Ahora puede agregar datos tooyour nueva colección mediante el Explorador de datos.

1. En el Explorador de datos, base de datos nueva Hola aparece en panel de colecciones de Hola. Expanda hello **tareas** la base de datos, expanda hello **elementos** colección, haga clic en **documentos**y, a continuación, haga clic en **nuevos documentos**. 

   ![Crear nuevos documentos en el Explorador de datos en hello portal de Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. Ahora puede agregar una colección de toohello de documento con hello siguiendo la estructura.

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. Una vez que haya agregado Hola json toohello **documentos** , haga clic en **guardar**.

    ![Copiar datos de json y haga clic en Guardar en el Explorador de datos en hello portal de Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  Crear y guardar un documento más donde insertar un valor único para hello `id` propiedad y cambio Hola otras propiedades como considere oportuno. Los nuevos documentos pueden tener la estructura que quiera, ya que Azure Cosmos DB no impone ningún esquema en los datos.

     Ahora use consultas en Explorador de datos tooretrieve los datos haciendo clic en hello puede **Editar filtro** y **aplicar filtro** botones. De forma predeterminada, usa el Explorador de datos `SELECT * FROM c` tooretrieve todos los documentos en la colección de hello, pero puede cambiar ese tooa diferentes [consulta SQL](documentdb-sql-query.md), como `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn todos los documentos de hello en orden descendente en función de su marca de tiempo. 
 
     También puede usar procedimientos de explorador de datos toocreate almacenado, UDF y lógica de negocios de servidor de tooperform de desencadenadores, así como el rendimiento de escala. Explorador de datos expone todo acceso a los datos de mediante programación integrada Hola disponible en las API de hello, pero proporciona un acceso sencillo tooyour datos Hola portal de Azure.

## <a name="clone-hello-sample-application"></a>Clonar aplicación de ejemplo de Hola

Ahora vamos a cambiar tooworking con el código. Vamos a clonar una aplicación de API de documentos de GitHub, establezca la cadena de conexión de Hola y ejecútelo. Vea lo fácil que es toowork con datos mediante programación. 

1. Abra una ventana de terminal de git, como git bash, y `CD` tooa directorio de trabajo.  

2. Ejecute hello después de repositorio de ejemplo de comando tooclone Hola. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-hello-code"></a>Revise el código de hello

Vamos a hacer una revisión rápida de lo que sucede en la aplicación hello. Abra hello `Program.java` archivo de hello \src\GetStarted carpeta y busque estas líneas de código que cree Hola recursos de base de datos de Azure Cosmos. 

* Hola `DocumentClient` se inicializa.

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* Se crea una base de datos.

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* Se crea una colección.

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* Se crean algunos documentos.

    ```java
    // Any Java object within your code can be serialized into JSON and written tooAzure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* Se realiza una consulta SQL en JSON.

    ```java
    FeedOptions queryOptions = new FeedOptions();
    queryOptions.setPageSize(-1);
    queryOptions.setEnableCrossPartitionQuery(true);

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    FeedResponse<Document> queryResults = this.client.queryDocuments(
        collectionLink,
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", queryOptions);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }
    ```    

## <a name="update-your-connection-string"></a>Actualizar la cadena de conexión

Ahora vuelva atrás toohello tooget portal Azure la información de la cadena de conexión y se copia en la aplicación hello. Esto le permitirá la toocommunicate de aplicación con la base de datos hospedado.

1. Hola [portal de Azure](http://portal.azure.com/), en la base de datos de Azure Cosmos account, Hola barra de navegación izquierda, haga clic en **claves**y, a continuación, haga clic en **claves de lectura y escritura**. Usará Hola copia botones en hello derecha de hello toocopy de pantalla Hola URI y la clave principal en hello `Program.java` archivo en el paso siguiente de saludo.

    ![Ver y copiar una clave de acceso en hello portal de Azure, hoja de claves](./media/create-documentdb-dotnet/keys.png)

2. Hola abierto `Program.java` de archivos, copie el valor URI de portal hello (mediante el botón Copiar de hello) y hacerla Hola valor del constructor de hello extremo toohello DocumentClient en `Program.java`. 

    `"https://FILLME.documents.azure.com"`

4. A continuación, copie el valor de clave principal del portal de Hola y péguela sobre "FILLME", lo que Hola segundo parámetro de constructor de DocumentClient Hola. Ahora ha actualizado la aplicación con toda la información de hello debe toocommunicate con base de datos de Azure Cosmos. 
    
## <a name="run-hello-app"></a>Ejecutar aplicación hello

1. En la ventana de terminal de git hello, `cd` toohello azure-cosmos-db-documentdb-java-getting-started carpeta.

2. En la ventana de terminal de git hello, escriba `mvn package` tooinstall Hola necesario paquetes de Java.

3. En la ventana de terminal de git hello, ejecute `mvn exec:java -D exec.mainClass=GetStarted.Program` en Hola ventana de terminal toostart la aplicación de Java.

    En la ventana de terminal de hello, recibirá una notificación que Hola FamilyDB se creó la base de datos y toopress un toocontinue clave. Presione una base de datos de clave toocreate hello, enciéndala toohello Explorador de datos y verá que ahora contiene una base de datos de FamilyDB. Continuar toopress claves toocreate Hola hello y colección de documentos y, a continuación, realizar una consulta. Cuando se completa el proyecto de hello, recursos de Hola se eliminan de su cuenta. 

    ![Ver y copiar una clave de acceso en hello portal de Azure, hoja de claves](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-hello-azure-portal"></a>Revise los SLA de hello portal de Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial rápido de hello portal de Azure con hello pasos:

1. En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó. 
2. En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo toocreate una cuenta de base de datos de Azure Cosmos, la base de datos de documento y la colección mediante Hola Explorador de datos y ejecutar una aplicación toodo Hola lo mismo mediante programación. Ahora puede importar la cuenta de base de datos de Cosmos tooyour datos adicionales. 

> [!div class="nextstepaction"]
> [Importación de datos a Azure Cosmos DB](import-data.md)


