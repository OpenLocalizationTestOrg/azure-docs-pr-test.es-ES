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
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a><span data-ttu-id="1ccea-105">Tutorial de NoSQL: Creación de una aplicación de consola de Java para la API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="1ccea-105">NoSQL tutorial: Build a DocumentDB API Java console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1ccea-106">.NET</span><span class="sxs-lookup"><span data-stu-id="1ccea-106">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="1ccea-107">.NET Core</span><span class="sxs-lookup"><span data-stu-id="1ccea-107">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="1ccea-108">Node.js para MongoDB</span><span class="sxs-lookup"><span data-stu-id="1ccea-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="1ccea-109">Node.js</span><span class="sxs-lookup"><span data-stu-id="1ccea-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="1ccea-110">Java</span><span class="sxs-lookup"><span data-stu-id="1ccea-110">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="1ccea-111">C++</span><span class="sxs-lookup"><span data-stu-id="1ccea-111">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="1ccea-112">Bienvenido toohello NoSQL tutorial para hello API de documentos de SDK de Java de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="1ccea-112">Welcome toohello NoSQL tutorial for hello DocumentDB API for Azure Cosmos DB Java SDK!</span></span> <span data-ttu-id="1ccea-113">Después de seguir este tutorial, tendrá una aplicación de consola que crea recursos de Azure Cosmos DB y los consulta.</span><span class="sxs-lookup"><span data-stu-id="1ccea-113">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="1ccea-114">Trataremos los siguientes temas:</span><span class="sxs-lookup"><span data-stu-id="1ccea-114">We cover:</span></span>

* <span data-ttu-id="1ccea-115">Creación y conexión de cuenta de base de datos de Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="1ccea-115">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="1ccea-116">Configuración de la solución de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ccea-116">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="1ccea-117">Creación de una base de datos en línea</span><span class="sxs-lookup"><span data-stu-id="1ccea-117">Creating an online database</span></span>
* <span data-ttu-id="1ccea-118">Creación de una colección</span><span class="sxs-lookup"><span data-stu-id="1ccea-118">Creating a collection</span></span>
* <span data-ttu-id="1ccea-119">Creación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="1ccea-119">Creating JSON documents</span></span>
* <span data-ttu-id="1ccea-120">Consultar la colección de Hola</span><span class="sxs-lookup"><span data-stu-id="1ccea-120">Querying hello collection</span></span>
* <span data-ttu-id="1ccea-121">Creación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="1ccea-121">Creating JSON documents</span></span>
* <span data-ttu-id="1ccea-122">Consultar la colección de Hola</span><span class="sxs-lookup"><span data-stu-id="1ccea-122">Querying hello collection</span></span>
* <span data-ttu-id="1ccea-123">Sustitución de un documento</span><span class="sxs-lookup"><span data-stu-id="1ccea-123">Replacing a document</span></span>
* <span data-ttu-id="1ccea-124">Eliminación de un documento</span><span class="sxs-lookup"><span data-stu-id="1ccea-124">Deleting a document</span></span>
* <span data-ttu-id="1ccea-125">Eliminar base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="1ccea-125">Deleting hello database</span></span>

<span data-ttu-id="1ccea-126">Comencemos.</span><span class="sxs-lookup"><span data-stu-id="1ccea-126">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ccea-127">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1ccea-127">Prerequisites</span></span>
<span data-ttu-id="1ccea-128">Asegúrese de que tiene Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="1ccea-128">Make sure you have hello following:</span></span>

* <span data-ttu-id="1ccea-129">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="1ccea-129">An active Azure account.</span></span> <span data-ttu-id="1ccea-130">Si no tiene una, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="1ccea-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="1ccea-131">Como alternativa, puede usar hello [emulador de base de datos de Azure Cosmos](local-emulator.md) para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="1ccea-131">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="1ccea-132">Git</span><span class="sxs-lookup"><span data-stu-id="1ccea-132">Git</span></span>](https://git-scm.com/downloads)
* <span data-ttu-id="1ccea-133"><seg>
  [Kit de desarrollo de Java (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</seg></span><span class="sxs-lookup"><span data-stu-id="1ccea-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* <span data-ttu-id="1ccea-134">[Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="1ccea-134">[Maven](http://maven.apache.org/download.cgi).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="1ccea-135">Paso 1: Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1ccea-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="1ccea-136">Vamos a crear una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1ccea-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="1ccea-137">Si ya tiene una cuenta que desee toouse, puede pasar demasiado[proyecto GitHub de clon hello](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="1ccea-137">If you already have an account you want toouse, you can skip ahead too[Clone hello GitHub project](#GitClone).</span></span> <span data-ttu-id="1ccea-138">Si usas hello Azure Cosmos DB emulador, siga los pasos de hello en [emulador de base de datos de Azure Cosmos](local-emulator.md) tooset una copia de seguridad emulador hello y pase demasiado[proyecto GitHub de clon hello](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="1ccea-138">If you are using hello Azure Cosmos DB Emulator, follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) tooset up hello emulator and skip ahead too[Clone hello GitHub project](#GitClone).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="1ccea-139"><a id="GitClone"></a>Paso 2: Clonar proyecto de hello GitHub</span><span class="sxs-lookup"><span data-stu-id="1ccea-139"><a id="GitClone"></a>Step 2: Clone hello GitHub project</span></span>
<span data-ttu-id="1ccea-140">Puede comenzar a trabajar mediante la clonación de repositorio de GitHub de Hola para [empezar a trabajar con la base de datos de Azure Cosmos y Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="1ccea-140">You can get started by cloning hello GitHub repository for [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span></span> <span data-ttu-id="1ccea-141">Por ejemplo, desde un directorio local ejecute hello siguiendo el proyecto de ejemplo de Hola de tooretrieve localmente.</span><span class="sxs-lookup"><span data-stu-id="1ccea-141">For example, from a local directory run hello following tooretrieve hello sample project locally.</span></span>

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

<span data-ttu-id="1ccea-142">Hola directorio contiene un `pom.xml` proyecto hello y un `src` carpeta que contiene el código de origen de Java incluidos `Program.java` que muestra cómo realiza operaciones sencillas con base de datos de Azure Cosmos como creación de documentos y consultar los datos dentro de un colección.</span><span class="sxs-lookup"><span data-stu-id="1ccea-142">hello directory contains a `pom.xml` for hello project and a `src` folder containing Java source code including `Program.java` which shows how perform simple operations with Azure Cosmos DB like creating documents and querying data within a collection.</span></span> <span data-ttu-id="1ccea-143">Hola `pom.xml` incluye una dependencia en hello [documentos de SDK de Java en Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span><span class="sxs-lookup"><span data-stu-id="1ccea-143">hello `pom.xml` includes a dependency on hello [DocumentDB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span></span>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <span data-ttu-id="1ccea-144"><a id="Connect"></a>Paso 3: Conectar la cuenta de base de datos de Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="1ccea-144"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="1ccea-145">A continuación, hacer copia de head toohello [Portal de Azure](https://portal.azure.com) tooretrieve el punto de conexión y la clave maestra de la principal.</span><span class="sxs-lookup"><span data-stu-id="1ccea-145">Next, head back toohello [Azure Portal](https://portal.azure.com) tooretrieve your endpoint and primary master key.</span></span> <span data-ttu-id="1ccea-146">Hello punto de conexión de base de datos de Azure Cosmos y clave principal son necesarios para su aplicación toounderstand donde tooconnect y para la base de datos de Azure Cosmos tootrust conexión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1ccea-146">hello Azure Cosmos DB endpoint and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="1ccea-147">Hola Portal de Azure, navegar por la cuenta de base de datos de Azure Cosmos tooyour y, a continuación, haga clic en **claves**.</span><span class="sxs-lookup"><span data-stu-id="1ccea-147">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span> <span data-ttu-id="1ccea-148">Copiar Hola URI desde el portal de Hola y pegarlos en `https://FILLME.documents.azure.com` en el archivo de hello Program.java.</span><span class="sxs-lookup"><span data-stu-id="1ccea-148">Copy hello URI from hello portal and paste it into `https://FILLME.documents.azure.com` in hello Program.java file.</span></span> <span data-ttu-id="1ccea-149">A continuación, copia Hola clave principal del portal de Hola y péguelo en `FILLME`.</span><span class="sxs-lookup"><span data-stu-id="1ccea-149">Then copy hello PRIMARY KEY from hello portal and paste it into `FILLME`.</span></span>

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Captura de pantalla de hello Portal de Azure usan Hola NoSQL tutorial toocreate una aplicación de consola de Java.][keys]

## <a name="step-4-create-a-database"></a><span data-ttu-id="1ccea-152">Paso 4: Creación de una base de datos</span><span class="sxs-lookup"><span data-stu-id="1ccea-152">Step 4: Create a database</span></span>
<span data-ttu-id="1ccea-153">La base de datos de Azure Cosmos [base de datos](documentdb-resources.md#databases) pueden crearse mediante el uso de hello [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) método de hello **DocumentClient** clase.</span><span class="sxs-lookup"><span data-stu-id="1ccea-153">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="1ccea-154">Una base de datos es el contenedor lógico de Hola de almacenamiento de documentos JSON particionado entre colecciones.</span><span class="sxs-lookup"><span data-stu-id="1ccea-154">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <span data-ttu-id="1ccea-155"><a id="CreateColl"></a>Paso 5: Creación de una colección</span><span class="sxs-lookup"><span data-stu-id="1ccea-155"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="1ccea-156">**createCollection** creará una colección con un rendimiento reservado, lo que tiene implicaciones en los precios.</span><span class="sxs-lookup"><span data-stu-id="1ccea-156">**createCollection** creates a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="1ccea-157">Para más información, visite nuestra [página de precios](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="1ccea-157">For more details, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="1ccea-158">A [colección](documentdb-resources.md#collections) pueden crearse mediante el uso de hello [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) método de hello **DocumentClient** clase.</span><span class="sxs-lookup"><span data-stu-id="1ccea-158">A [collection](documentdb-resources.md#collections) can be created by using hello [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="1ccea-159">Una colección es un contenedor de documentos JSON asociado a la lógica de aplicación de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1ccea-159">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <span data-ttu-id="1ccea-160"><a id="CreateDoc"></a>Paso 6: Creación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="1ccea-160"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="1ccea-161">A [documento](documentdb-resources.md#documents) pueden crearse mediante el uso de hello [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) método de hello **DocumentClient** clase.</span><span class="sxs-lookup"><span data-stu-id="1ccea-161">A [document](documentdb-resources.md#documents) can be created by using hello [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="1ccea-162">Los documentos son contenido JSON definido por el usuario (arbitrario).</span><span class="sxs-lookup"><span data-stu-id="1ccea-162">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="1ccea-163">Ahora podemos insertar uno o varios documentos.</span><span class="sxs-lookup"><span data-stu-id="1ccea-163">We can now insert one or more documents.</span></span> <span data-ttu-id="1ccea-164">Si ya tiene datos que le gustaría toostore en la base de datos, puede usar Azure Cosmos DB [herramienta de migración de datos](import-data.md) datos de hello tooimport en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="1ccea-164">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) tooimport hello data into a database.</span></span>

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

## <span data-ttu-id="1ccea-166"><a id="Query"></a>Paso 7: Consulta de los recursos de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1ccea-166"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="1ccea-167">Azure Cosmos DB admite [consultas](documentdb-sql-query.md) enriquecidas en los documentos JSON que se almacenan en las colecciones.</span><span class="sxs-lookup"><span data-stu-id="1ccea-167">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="1ccea-168">Hola siguiendo el ejemplo de código muestra cómo se documentan en la base de datos de Azure Cosmos tooquery utilizando la sintaxis SQL con hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) método.</span><span class="sxs-lookup"><span data-stu-id="1ccea-168">hello following sample code shows how tooquery documents in Azure Cosmos DB using SQL syntax with hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) method.</span></span>

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <span data-ttu-id="1ccea-169"><a id="ReplaceDocument"></a>Paso 8: Reemplazar un documento JSON</span><span class="sxs-lookup"><span data-stu-id="1ccea-169"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="1ccea-170">Base de datos de Azure Cosmos admite actualizables documentos JSON mediante hello [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) método.</span><span class="sxs-lookup"><span data-stu-id="1ccea-170">Azure Cosmos DB supports updating JSON documents using hello [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) method.</span></span>

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <span data-ttu-id="1ccea-171"><a id="DeleteDocument"></a>Paso 9: Eliminar documento JSON</span><span class="sxs-lookup"><span data-stu-id="1ccea-171"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="1ccea-172">De igual forma, base de datos de Azure Cosmos admite eliminar documentos JSON con hello [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) método.</span><span class="sxs-lookup"><span data-stu-id="1ccea-172">Similarly, Azure Cosmos DB supports deleting JSON documents using hello [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) method.</span></span>  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <span data-ttu-id="1ccea-173"><a id="DeleteDatabase"></a>Paso 10: Eliminar base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="1ccea-173"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="1ccea-174">Eliminar base de datos de hello creado quita la base de datos de Hola y todos los recursos de los elementos secundarios (colecciones, documentos, etcetera).</span><span class="sxs-lookup"><span data-stu-id="1ccea-174">Deleting hello created database removes hello database and all children resources (collections, documents, etc.).</span></span>

    this.client.deleteDatabase("/dbs/familydb", null);

## <span data-ttu-id="1ccea-175"><a id="Run"></a>Paso 11: Ejecutar la aplicación de consola de Java</span><span class="sxs-lookup"><span data-stu-id="1ccea-175"><a id="Run"></a>Step 11: Run your Java console application all together!</span></span>
<span data-ttu-id="1ccea-176">aplicación de hello toorun desde la consola de hello, desplácese toohello carpeta del proyecto y realizar la compilación mediante Maven:</span><span class="sxs-lookup"><span data-stu-id="1ccea-176">toorun hello application from hello console, navigate toohello project folder and compile using Maven:</span></span>
    
    mvn package

<span data-ttu-id="1ccea-177">Ejecuta `mvn package` descargas de biblioteca de base de datos de Azure Cosmos más reciente de Hola de Maven y genera `GetStarted-0.0.1-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="1ccea-177">Running `mvn package` downloads hello latest Azure Cosmos DB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span></span> <span data-ttu-id="1ccea-178">A continuación, ejecutar la aplicación hello ejecutando:</span><span class="sxs-lookup"><span data-stu-id="1ccea-178">Then run hello app by running:</span></span>

    mvn exec:java -D exec.mainClass=GetStarted.Program

<span data-ttu-id="1ccea-179">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="1ccea-179">Congratulations!</span></span> <span data-ttu-id="1ccea-180">Ha completado este tutorial de NoSQL y tiene una aplicación de consola de Java en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="1ccea-180">You've completed this NoSQL tutorial and have a working Java console application!</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ccea-181">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1ccea-181">Next steps</span></span>
* <span data-ttu-id="1ccea-182">¿Desea un tutorial de las aplicaciones web de Java?</span><span class="sxs-lookup"><span data-stu-id="1ccea-182">Want a Java web app tutorial?</span></span> <span data-ttu-id="1ccea-183">Consulte [Creación de una aplicación web de Java mediante Azure Cosmos DB](documentdb-java-application.md).</span><span class="sxs-lookup"><span data-stu-id="1ccea-183">See [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md).</span></span>
* <span data-ttu-id="1ccea-184">Obtenga información acerca de cómo demasiado[supervisar una cuenta de base de datos de Azure Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="1ccea-184">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="1ccea-185">Ejecutar consultas en el conjunto de datos de ejemplo de Hola [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="1ccea-185">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="1ccea-186">Obtener más información sobre el modelo de programación de Hola Hola sección desarrollar de hello [página de documentación de la base de datos de Azure Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="1ccea-186">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
