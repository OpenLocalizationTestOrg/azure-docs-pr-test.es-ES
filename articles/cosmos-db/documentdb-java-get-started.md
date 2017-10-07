---
title: 'Tutorial de NoSQL: API de DocumentDB para el SDK de Java para Azure Cosmos DB | Microsoft Docs'
description: "Tutorial de NoSQL que crea una base de datos en línea y la aplicación de consola de Java con hello API de documentos para la base de datos de Azure Cosmos. Azure DocumentDB es una base de datos NoSQL para JSON."
keywords: "tutorial de nosql, base de datos en línea, aplicación de consola de java"
services: cosmos-db
documentationcenter: Java
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 75a9efa1-7edd-4fed-9882-c0177274cbb2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 05/22/2017
ms.author: arramac
ms.openlocfilehash: 1a298a15ab911d140b9df30ad52cfe0fa07c55b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a>Tutorial de NoSQL: Creación de una aplicación de consola de Java para la API de DocumentDB
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js para MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Bienvenido toohello NoSQL tutorial para hello API de documentos de SDK de Java de base de datos de Azure Cosmos. Después de seguir este tutorial, tendrá una aplicación de consola que crea recursos de Azure Cosmos DB y los consulta.

Trataremos los siguientes temas:

* Creación y conexión de cuenta de base de datos de Azure Cosmos tooan
* Configuración de la solución de Visual Studio
* Creación de una base de datos en línea
* Creación de una colección
* Creación de documentos JSON
* Consultar la colección de Hola
* Creación de documentos JSON
* Consultar la colección de Hola
* Sustitución de un documento
* Eliminación de un documento
* Eliminar base de datos de Hola

Comencemos.

## <a name="prerequisites"></a>Requisitos previos
Asegúrese de que tiene Hola siguientes:

* Una cuenta de Azure activa. Si no tiene una, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/free/). Como alternativa, puede usar hello [emulador de base de datos de Azure Cosmos](local-emulator.md) para este tutorial.
* [Git](https://git-scm.com/downloads)
* <seg>
  [Kit de desarrollo de Java (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</seg>
* [Maven](http://maven.apache.org/download.cgi).

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Paso 1: Creación de una cuenta de Azure Cosmos DB
Vamos a crear una cuenta de Azure Cosmos DB. Si ya tiene una cuenta que desee toouse, puede pasar demasiado[proyecto GitHub de clon hello](#GitClone). Si usas hello Azure Cosmos DB emulador, siga los pasos de hello en [emulador de base de datos de Azure Cosmos](local-emulator.md) tooset una copia de seguridad emulador hello y pase demasiado[proyecto GitHub de clon hello](#GitClone).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="GitClone"></a>Paso 2: Clonar proyecto de hello GitHub
Puede comenzar a trabajar mediante la clonación de repositorio de GitHub de Hola para [empezar a trabajar con la base de datos de Azure Cosmos y Java](https://github.com/Azure-Samples/documentdb-java-getting-started). Por ejemplo, desde un directorio local ejecute hello siguiendo el proyecto de ejemplo de Hola de tooretrieve localmente.

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

Hola directorio contiene un `pom.xml` proyecto hello y un `src` carpeta que contiene el código de origen de Java incluidos `Program.java` que muestra cómo realiza operaciones sencillas con base de datos de Azure Cosmos como creación de documentos y consultar los datos dentro de un colección. Hola `pom.xml` incluye una dependencia en hello [documentos de SDK de Java en Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <a id="Connect"></a>Paso 3: Conectar la cuenta de base de datos de Azure Cosmos tooan
A continuación, hacer copia de head toohello [Portal de Azure](https://portal.azure.com) tooretrieve el punto de conexión y la clave maestra de la principal. Hello punto de conexión de base de datos de Azure Cosmos y clave principal son necesarios para su aplicación toounderstand donde tooconnect y para la base de datos de Azure Cosmos tootrust conexión de la aplicación.

Hola Portal de Azure, navegar por la cuenta de base de datos de Azure Cosmos tooyour y, a continuación, haga clic en **claves**. Copiar Hola URI desde el portal de Hola y pegarlos en `https://FILLME.documents.azure.com` en el archivo de hello Program.java. A continuación, copia Hola clave principal del portal de Hola y péguelo en `FILLME`.

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Captura de pantalla de hello Portal de Azure usan Hola NoSQL tutorial toocreate una aplicación de consola de Java. Muestra una base de datos de Azure Cosmos cuenta, con centro activo Hola resaltado, Hola resaltado en la hoja de cuenta de base de datos de Azure Cosmos Hola de botón de claves y valores URI, la clave principal y la clave secundaria de hello resaltan en hello hoja de claves][keys]

## <a name="step-4-create-a-database"></a>Paso 4: Creación de una base de datos
La base de datos de Azure Cosmos [base de datos](documentdb-resources.md#databases) pueden crearse mediante el uso de hello [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) método de hello **DocumentClient** clase. Una base de datos es el contenedor lógico de Hola de almacenamiento de documentos JSON particionado entre colecciones.

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <a id="CreateColl"></a>Paso 5: Creación de una colección
> [!WARNING]
> **createCollection** creará una colección con un rendimiento reservado, lo que tiene implicaciones en los precios. Para más información, visite nuestra [página de precios](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

A [colección](documentdb-resources.md#collections) pueden crearse mediante el uso de hello [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) método de hello **DocumentClient** clase. Una colección es un contenedor de documentos JSON asociado a la lógica de aplicación de JavaScript.


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <a id="CreateDoc"></a>Paso 6: Creación de documentos JSON
A [documento](documentdb-resources.md#documents) pueden crearse mediante el uso de hello [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) método de hello **DocumentClient** clase. Los documentos son contenido JSON definido por el usuario (arbitrario). Ahora podemos insertar uno o varios documentos. Si ya tiene datos que le gustaría toostore en la base de datos, puede usar Azure Cosmos DB [herramienta de migración de datos](import-data.md) datos de hello tooimport en una base de datos.

    // Insert your Java objects as documents 
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen")

    // More initialization skipped for brevity. You can have nested references
    andersenFamily.setParents(new Parent[] { parent1, parent2 });
    andersenFamily.setDistrict("WA5");
    Address address = new Address();
    address.setCity("Seattle");
    address.setCounty("King");
    address.setState("WA");

    andersenFamily.setAddress(address);
    andersenFamily.setRegistered(true);

    this.client.createDocument("/dbs/familydb/colls/familycoll", family, new RequestOptions(), true);

![Diagrama que ilustra relación jerárquica Hola entre la cuenta de hello, base de datos en línea hello, colección de Hola y documentos de hello usa Hola NoSQL tutorial toocreate una aplicación de consola de Java](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>Paso 7: Consulta de los recursos de Azure Cosmos DB
Azure Cosmos DB admite [consultas](documentdb-sql-query.md) enriquecidas en los documentos JSON que se almacenan en las colecciones.  Hola siguiendo el ejemplo de código muestra cómo se documentan en la base de datos de Azure Cosmos tooquery utilizando la sintaxis SQL con hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) método.

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <a id="ReplaceDocument"></a>Paso 8: Reemplazar un documento JSON
Base de datos de Azure Cosmos admite actualizables documentos JSON mediante hello [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) método.

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <a id="DeleteDocument"></a>Paso 9: Eliminar documento JSON
De igual forma, base de datos de Azure Cosmos admite eliminar documentos JSON con hello [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) método.  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <a id="DeleteDatabase"></a>Paso 10: Eliminar base de datos de Hola
Eliminar base de datos de hello creado quita la base de datos de Hola y todos los recursos de los elementos secundarios (colecciones, documentos, etcetera).

    this.client.deleteDatabase("/dbs/familydb", null);

## <a id="Run"></a>Paso 11: Ejecutar la aplicación de consola de Java
aplicación de hello toorun desde la consola de hello, desplácese toohello carpeta del proyecto y realizar la compilación mediante Maven:
    
    mvn package

Ejecuta `mvn package` descargas de biblioteca de base de datos de Azure Cosmos más reciente de Hola de Maven y genera `GetStarted-0.0.1-SNAPSHOT.jar`. A continuación, ejecutar la aplicación hello ejecutando:

    mvn exec:java -D exec.mainClass=GetStarted.Program

¡Enhorabuena! Ha completado este tutorial de NoSQL y tiene una aplicación de consola de Java en funcionamiento.

## <a name="next-steps"></a>Pasos siguientes
* ¿Desea un tutorial de las aplicaciones web de Java? Consulte [Creación de una aplicación web de Java mediante Azure Cosmos DB](documentdb-java-application.md).
* Obtenga información acerca de cómo demasiado[supervisar una cuenta de base de datos de Azure Cosmos](monitor-accounts.md).
* Ejecutar consultas en el conjunto de datos de ejemplo de Hola [Query Playground](https://www.documentdb.com/sql/demo).
* Obtener más información sobre el modelo de programación de Hola Hola sección desarrollar de hello [página de documentación de la base de datos de Azure Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
