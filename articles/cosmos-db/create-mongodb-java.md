---
title: "Azure Cosmos DB: Compilar una aplicación de consola con Java y Hola MongoDB API | Documentos de Microsoft"
description: "Presenta un ejemplo de código de Java se puede usar tooconnect tooand consulta hello Azure Cosmos DB MongoDB API"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: fbe416f6b20ed2bb83a1d41eb70ffc6e3cee2b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-hello-azure-portal"></a>Azure Cosmos DB: Compilar una aplicación de consola de API de MongoDB con Java y Hola portal de Azure

Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft. Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente. 

Este inicio rápido muestra cómo toocreate una cuenta de base de datos de Azure Cosmos, la base de datos de documento y la colección mediante Hola portal de Azure. A continuación, podrá compilar e implementar una aplicación de consola compilada en hello [controlador MongoDB Java](https://docs.mongodb.com/ecosystem/drivers/java/). 

## <a name="prerequisites"></a>Requisitos previos

* Para poder ejecutar este ejemplo, debe tener Hola siguiendo los requisitos previos:
   * JDK 1.7+ (ejecute `apt-get install default-jdk` si no tiene JDK)
   * Maven (ejecute `apt-get install maven` si no tiene Maven)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Creación de una cuenta de base de datos

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a>Agregar una colección

Asígnele un nombre a la base de datos nueva (**db**) y a la nueva colección (**coll**).

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Clonar aplicación de ejemplo de Hola

Ahora vamos a clonar una API de MongoDB aplicación de github, establezca la cadena de conexión de Hola y ejecútelo. Podrá ver lo fácil que es toowork con datos mediante programación. 

1. Abra una ventana de terminal de git, como git bash, y `cd` tooa directorio de trabajo.  

2. Ejecute hello después de repositorio de ejemplo de comando tooclone Hola. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. A continuación, abra el archivo de solución de hello en Visual Studio. 

## <a name="review-hello-code"></a>Revise el código de hello

Vamos a hacer una revisión rápida de lo que sucede en la aplicación hello. Abra hello `Program.cs` archivo y encontrará que estas líneas de código crean Hola recursos de base de datos de Azure Cosmos. 

* Hola DocumentClient se inicializa.

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* Se crean una base de datos y una colección.

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* Se insertan algunos documentos mediante `MongoCollection.insertOne`.

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* Se realizan algunas consultas mediante `MongoCollection.find`.

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a>Actualizar la cadena de conexión

Ahora vuelva atrás toohello tooget portal Azure la información de la cadena de conexión y se copia en la aplicación hello.

1. En la cuenta de hello, seleccione **inicio rápido**, seleccione Java y luego copiar Portapapeles de tooyour de cadena de conexión de Hola

2. Abra hello `Program.java` archivo, reemplace el constructor de hello argumento toohello MongoClientURI con la cadena de conexión de Hola. Ahora ha actualizado la aplicación con toda la información de hello debe toocommunicate con base de datos de Azure Cosmos. 
    
## <a name="run-hello-console-app"></a>Ejecutar la aplicación de consola de hello

1. Ejecutar `mvn package` en un terminal tooinstall necesario módulos npm

2. Ejecutar `mvn exec:java -D exec.mainClass=GetStarted.Program` en un terminal toostart la aplicación de Java.

Ahora puede usar [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) tooquery, modificar y trabajar con nuevos datos.

## <a name="review-slas-in-hello-azure-portal"></a>Revise los SLA de hello portal de Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial rápido de hello portal de Azure con hello pasos:

1. En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó. 
2. En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo crear una colección mediante Hola Explorador de datos toocreate una cuenta de base de datos de Azure Cosmos y ejecutar una aplicación de consola. Ahora puede importar la cuenta de base de datos de Cosmos tooyour datos adicionales. 

> [!div class="nextstepaction"]
> [Importación de datos de MongoDB a Azure Cosmos DB](mongodb-migrate.md)


