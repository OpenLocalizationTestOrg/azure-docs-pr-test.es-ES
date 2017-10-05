---
title: 'Tutorial de NoSQL: API de DocumentDB para el SDK de Java para Azure Cosmos DB | Microsoft Docs'
description: "Un tutorial de NoSQL que crea una base de datos en línea y la aplicación de consola de Java mediante la API de DocumentDB para Azure Cosmos DB. Azure DocumentDB es una base de datos NoSQL para JSON."
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
ms.openlocfilehash: 5c4bcda308f001572e1c34e991616fc209250a02
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a><span data-ttu-id="22241-105">Tutorial de NoSQL: Creación de una aplicación de consola de Java para la API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="22241-105">NoSQL tutorial: Build a DocumentDB API Java console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="22241-106">.NET</span><span class="sxs-lookup"><span data-stu-id="22241-106">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="22241-107">.NET Core</span><span class="sxs-lookup"><span data-stu-id="22241-107">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="22241-108">Node.js para MongoDB</span><span class="sxs-lookup"><span data-stu-id="22241-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="22241-109">Node.js</span><span class="sxs-lookup"><span data-stu-id="22241-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="22241-110">Java</span><span class="sxs-lookup"><span data-stu-id="22241-110">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="22241-111">C++</span><span class="sxs-lookup"><span data-stu-id="22241-111">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="22241-112">Bienvenido al tutorial de NoSQL sobre la API de DocumentDB para el SDK de Java para Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="22241-112">Welcome to the NoSQL tutorial for the DocumentDB API for Azure Cosmos DB Java SDK!</span></span> <span data-ttu-id="22241-113">Después de seguir este tutorial, tendrá una aplicación de consola que crea recursos de Azure Cosmos DB y los consulta.</span><span class="sxs-lookup"><span data-stu-id="22241-113">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="22241-114">Trataremos los siguientes temas:</span><span class="sxs-lookup"><span data-stu-id="22241-114">We cover:</span></span>

* <span data-ttu-id="22241-115">Creación de una cuenta de Azure Cosmos DB y conexión a ella</span><span class="sxs-lookup"><span data-stu-id="22241-115">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="22241-116">Configuración de la solución de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="22241-116">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="22241-117">Creación de una base de datos en línea</span><span class="sxs-lookup"><span data-stu-id="22241-117">Creating an online database</span></span>
* <span data-ttu-id="22241-118">Creación de una colección</span><span class="sxs-lookup"><span data-stu-id="22241-118">Creating a collection</span></span>
* <span data-ttu-id="22241-119">Creación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="22241-119">Creating JSON documents</span></span>
* <span data-ttu-id="22241-120">Consulta de la colección</span><span class="sxs-lookup"><span data-stu-id="22241-120">Querying the collection</span></span>
* <span data-ttu-id="22241-121">Creación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="22241-121">Creating JSON documents</span></span>
* <span data-ttu-id="22241-122">Consulta de la colección</span><span class="sxs-lookup"><span data-stu-id="22241-122">Querying the collection</span></span>
* <span data-ttu-id="22241-123">Sustitución de un documento</span><span class="sxs-lookup"><span data-stu-id="22241-123">Replacing a document</span></span>
* <span data-ttu-id="22241-124">Eliminación de un documento</span><span class="sxs-lookup"><span data-stu-id="22241-124">Deleting a document</span></span>
* <span data-ttu-id="22241-125">Eliminación de la base de datos</span><span class="sxs-lookup"><span data-stu-id="22241-125">Deleting the database</span></span>

<span data-ttu-id="22241-126">Comencemos.</span><span class="sxs-lookup"><span data-stu-id="22241-126">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22241-127">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="22241-127">Prerequisites</span></span>
<span data-ttu-id="22241-128">Asegúrese de que dispone de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="22241-128">Make sure you have the following:</span></span>

* <span data-ttu-id="22241-129">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="22241-129">An active Azure account.</span></span> <span data-ttu-id="22241-130">Si no tiene una, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="22241-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="22241-131">Como alternativa, en este tutorial puede usar el [Emulador de Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="22241-131">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="22241-132">Git</span><span class="sxs-lookup"><span data-stu-id="22241-132">Git</span></span>](https://git-scm.com/downloads)
* <span data-ttu-id="22241-133"><seg>
  [Kit de desarrollo de Java (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</seg></span><span class="sxs-lookup"><span data-stu-id="22241-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* <span data-ttu-id="22241-134">[Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="22241-134">[Maven](http://maven.apache.org/download.cgi).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="22241-135">Paso 1: Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="22241-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="22241-136">Vamos a crear una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="22241-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="22241-137">Si ya tiene una cuenta que desea usar, puede ir directamente a [Clonar el proyecto de GitHub](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="22241-137">If you already have an account you want to use, you can skip ahead to [Clone the GitHub project](#GitClone).</span></span> <span data-ttu-id="22241-138">Si está usando el Emulador de Azure Cosmos DB, siga los pasos que se indican en el [Emulador de Azure Cosmos DB](local-emulator.md) para configurar el emulador y vaya directamente a [Clonar el proyecto de GitHub](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="22241-138">If you are using the Azure Cosmos DB Emulator, follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to set up the emulator and skip ahead to [Clone the GitHub project](#GitClone).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="22241-139"><a id="GitClone"></a>Paso 2: Clonar el proyecto de GitHub</span><span class="sxs-lookup"><span data-stu-id="22241-139"><a id="GitClone"></a>Step 2: Clone the GitHub project</span></span>
<span data-ttu-id="22241-140">En primer lugar, clone el repositorio de GitHub para [empezar a trabajar con Azure Cosmos DB y Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="22241-140">You can get started by cloning the GitHub repository for [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span></span> <span data-ttu-id="22241-141">Por ejemplo, desde un directorio local, ejecute lo siguiente para recuperar el proyecto de ejemplo localmente.</span><span class="sxs-lookup"><span data-stu-id="22241-141">For example, from a local directory run the following to retrieve the sample project locally.</span></span>

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

<span data-ttu-id="22241-142">El directorio contiene un archivo `pom.xml` para el proyecto y una carpeta `src` que contiene el código fuente de Java, incluido `Program.java`, que muestra cómo realizar operaciones sencillas con Azure Cosmos DB, como crear documentos y consultar datos dentro de una colección.</span><span class="sxs-lookup"><span data-stu-id="22241-142">The directory contains a `pom.xml` for the project and a `src` folder containing Java source code including `Program.java` which shows how perform simple operations with Azure Cosmos DB like creating documents and querying data within a collection.</span></span> <span data-ttu-id="22241-143">El archivo `pom.xml` incluye una dependencia en el [SDK de Java para DocumentDB en Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span><span class="sxs-lookup"><span data-stu-id="22241-143">The `pom.xml` includes a dependency on the [DocumentDB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span></span>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <span data-ttu-id="22241-144"><a id="Connect"></a>Paso 3: Conexión a una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="22241-144"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="22241-145">A continuación, vuelva a [Azure Portal](https://portal.azure.com) para recuperar el punto de conexión y la clave maestra principal.</span><span class="sxs-lookup"><span data-stu-id="22241-145">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint and primary master key.</span></span> <span data-ttu-id="22241-146">El punto de conexión y la clave principal de Azure Cosmos DB son necesarios para que la aplicación sepa a dónde debe conectarse y para que Azure Cosmos DB confíe en la conexión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="22241-146">The Azure Cosmos DB endpoint and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="22241-147">En Azure Portal, vaya a la cuenta de Azure Cosmos DB y haga clic en **Claves**.</span><span class="sxs-lookup"><span data-stu-id="22241-147">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span> <span data-ttu-id="22241-148">Copie el URI desde el portal y péguelo en `https://FILLME.documents.azure.com`, en el archivo Program.java.</span><span class="sxs-lookup"><span data-stu-id="22241-148">Copy the URI from the portal and paste it into `https://FILLME.documents.azure.com` in the Program.java file.</span></span> <span data-ttu-id="22241-149">Después, copie la CLAVE PRINCIPAL del Portal y péguela en `FILLME`.</span><span class="sxs-lookup"><span data-stu-id="22241-149">Then copy the PRIMARY KEY from the portal and paste it into `FILLME`.</span></span>

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Captura de pantalla de Azure Portal usado por el tutorial de NoSQL para crear una aplicación de consola de Java.][keys]

## <a name="step-4-create-a-database"></a><span data-ttu-id="22241-152">Paso 4: Creación de una base de datos</span><span class="sxs-lookup"><span data-stu-id="22241-152">Step 4: Create a database</span></span>
<span data-ttu-id="22241-153">Para crear una [base de datos](documentdb-resources.md#databases) de Azure Cosmos DB, puede usar el método [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) de la clase **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="22241-153">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) method of the **DocumentClient** class.</span></span> <span data-ttu-id="22241-154">Una base de datos es un contenedor lógico de almacenamiento de documentos JSON particionado en recopilaciones.</span><span class="sxs-lookup"><span data-stu-id="22241-154">A database is the logical container of JSON document storage partitioned across collections.</span></span>

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <span data-ttu-id="22241-155"><a id="CreateColl"></a>Paso 5: Creación de una colección</span><span class="sxs-lookup"><span data-stu-id="22241-155"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="22241-156">**createCollection** creará una colección con un rendimiento reservado, lo que tiene implicaciones en los precios.</span><span class="sxs-lookup"><span data-stu-id="22241-156">**createCollection** creates a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="22241-157">Para más información, visite nuestra [página de precios](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="22241-157">For more details, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="22241-158">Para crear una [colección](documentdb-resources.md#collections), puede usar el método [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) de la clase **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="22241-158">A [collection](documentdb-resources.md#collections) can be created by using the [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) method of the **DocumentClient** class.</span></span> <span data-ttu-id="22241-159">Una colección es un contenedor de documentos JSON asociado a la lógica de aplicación de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="22241-159">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <span data-ttu-id="22241-160"><a id="CreateDoc"></a>Paso 6: Creación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="22241-160"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="22241-161">Para crear un [documento](documentdb-resources.md#documents), puede usar el método [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) de la clase **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="22241-161">A [document](documentdb-resources.md#documents) can be created by using the [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) method of the **DocumentClient** class.</span></span> <span data-ttu-id="22241-162">Los documentos son contenido JSON definido por el usuario (arbitrario).</span><span class="sxs-lookup"><span data-stu-id="22241-162">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="22241-163">Ahora podemos insertar uno o varios documentos.</span><span class="sxs-lookup"><span data-stu-id="22241-163">We can now insert one or more documents.</span></span> <span data-ttu-id="22241-164">Si ya dispone de datos que desea almacenar en la base de datos, puede usar la [herramienta de migración de datos](import-data.md) de Azure Cosmos DB para importar los datos en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="22241-164">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) to import the data into a database.</span></span>

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

![Diagrama que muestra la relación jerárquica entre la cuenta, la base de datos en línea, la colección y los documentos usados por el tutorial de NoSQL para crear una aplicación de consola de Java.](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="22241-166"><a id="Query"></a>Paso 7: Consulta de los recursos de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="22241-166"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="22241-167">Azure Cosmos DB admite [consultas](documentdb-sql-query.md) enriquecidas en los documentos JSON que se almacenan en las colecciones.</span><span class="sxs-lookup"><span data-stu-id="22241-167">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="22241-168">El código de ejemplo siguiente muestra cómo consultar documentos de Azure Cosmos DB mediante la sintaxis SQL con el método [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments).</span><span class="sxs-lookup"><span data-stu-id="22241-168">The following sample code shows how to query documents in Azure Cosmos DB using SQL syntax with the [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) method.</span></span>

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <span data-ttu-id="22241-169"><a id="ReplaceDocument"></a>Paso 8: Reemplazar un documento JSON</span><span class="sxs-lookup"><span data-stu-id="22241-169"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="22241-170">Azure Cosmos DB permite actualizar documentos JSON con el método [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument).</span><span class="sxs-lookup"><span data-stu-id="22241-170">Azure Cosmos DB supports updating JSON documents using the [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) method.</span></span>

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <span data-ttu-id="22241-171"><a id="DeleteDocument"></a>Paso 9: Eliminar documento JSON</span><span class="sxs-lookup"><span data-stu-id="22241-171"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="22241-172">Análogamente, Azure Cosmos DB permite eliminar documentos JSON con el método [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument).</span><span class="sxs-lookup"><span data-stu-id="22241-172">Similarly, Azure Cosmos DB supports deleting JSON documents using the [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) method.</span></span>  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <span data-ttu-id="22241-173"><a id="DeleteDatabase"></a>Paso 10: Eliminar la base de datos</span><span class="sxs-lookup"><span data-stu-id="22241-173"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="22241-174">La eliminación de la base de datos creada quitará la base de datos y todos los recursos secundarios (colecciones, documentos, etc.).</span><span class="sxs-lookup"><span data-stu-id="22241-174">Deleting the created database removes the database and all children resources (collections, documents, etc.).</span></span>

    this.client.deleteDatabase("/dbs/familydb", null);

## <span data-ttu-id="22241-175"><a id="Run"></a>Paso 11: Ejecutar la aplicación de consola de Java</span><span class="sxs-lookup"><span data-stu-id="22241-175"><a id="Run"></a>Step 11: Run your Java console application all together!</span></span>
<span data-ttu-id="22241-176">Para ejecutar la aplicación desde la consola, navegue hasta la carpeta del proyecto y realice la compilación con Maven:</span><span class="sxs-lookup"><span data-stu-id="22241-176">To run the application from the console, navigate to the project folder and compile using Maven:</span></span>
    
    mvn package

<span data-ttu-id="22241-177">La ejecución de `mvn package` descarga la biblioteca de Azure Cosmos DB más reciente de Maven y genera `GetStarted-0.0.1-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="22241-177">Running `mvn package` downloads the latest Azure Cosmos DB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span></span> <span data-ttu-id="22241-178">A continuación, ejecute la aplicación con:</span><span class="sxs-lookup"><span data-stu-id="22241-178">Then run the app by running:</span></span>

    mvn exec:java -D exec.mainClass=GetStarted.Program

<span data-ttu-id="22241-179">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="22241-179">Congratulations!</span></span> <span data-ttu-id="22241-180">Ha completado este tutorial de NoSQL y tiene una aplicación de consola de Java en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="22241-180">You've completed this NoSQL tutorial and have a working Java console application!</span></span>

## <a name="next-steps"></a><span data-ttu-id="22241-181">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="22241-181">Next steps</span></span>
* <span data-ttu-id="22241-182">¿Desea un tutorial de las aplicaciones web de Java?</span><span class="sxs-lookup"><span data-stu-id="22241-182">Want a Java web app tutorial?</span></span> <span data-ttu-id="22241-183">Consulte [Creación de una aplicación web de Java mediante Azure Cosmos DB](documentdb-java-application.md).</span><span class="sxs-lookup"><span data-stu-id="22241-183">See [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md).</span></span>
* <span data-ttu-id="22241-184">Información acerca de cómo [supervisar una cuenta de Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="22241-184">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="22241-185">Ejecute las consultas en nuestro conjunto de datos de ejemplo en el [área de consultas](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="22241-185">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="22241-186">Obtenga más información sobre el modelo de programación en la sección sobre desarrollo de la [página de documentación de Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="22241-186">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
