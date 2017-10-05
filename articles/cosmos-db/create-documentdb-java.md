---
title: "Creación de una base de datos de documentos de Azure Cosmos DB con Java | Microsoft Docs | de Microsoft Docs"
description: "En este tema se presenta un ejemplo de código de Java que se puede usar para conectarse a la API DocumentDB de Azure Cosmos DB y realizar consultas."
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
ms.openlocfilehash: df1a25d703a7b8082bdabb4f7d593cb005d416fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-the-azure-portal"></a><span data-ttu-id="05ebe-103">Azure Cosmos DB: creación una base de datos de documentos mediante Java y Azure Portal</span><span class="sxs-lookup"><span data-stu-id="05ebe-103">Azure Cosmos DB: Create a document database using Java and the Azure portal</span></span>

<span data-ttu-id="05ebe-104">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="05ebe-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="05ebe-105">Puede crear rápidamente bases de datos de documentos, clave-valor y grafos, y realizar consultas en ellas. Todas las bases de datos se beneficiarán de las funcionalidades de distribución global y escala horizontal en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="05ebe-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="05ebe-106">Este tutorial rápido crea una base de datos de documentos mediante las herramientas de Azure Portal para Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="05ebe-106">This quickstart creates a document database using the Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="05ebe-107">Este tutorial rápido también muestra cómo crear rápidamente una aplicación de consola Java mediante la [API de Java DocumentDB](documentdb-sdk-java.md).</span><span class="sxs-lookup"><span data-stu-id="05ebe-107">This quickstart also shows you how to quickly create a Java console app using the [DocumentDB Java API](documentdb-sdk-java.md).</span></span> <span data-ttu-id="05ebe-108">Las instrucciones que se indican en este tutorial rápido se pueden seguir en cualquier sistema operativo que sea capaz de ejecutar Java.</span><span class="sxs-lookup"><span data-stu-id="05ebe-108">The instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="05ebe-109">Al completar este tutorial rápido aprenderá a crear y modificar los recursos de base de datos de documentos en la interfaz de usuario o mediante programación, lo que prefiera.</span><span class="sxs-lookup"><span data-stu-id="05ebe-109">By completing this quickstart you'll be familiar with creating and modifying document database resources in either the UI or programatically, whichever is your preference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05ebe-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="05ebe-110">Prerequisites</span></span>

* [<span data-ttu-id="05ebe-111">Kit de desarrollo de Java (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="05ebe-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="05ebe-112">En Ubuntu, ejecute `apt-get install default-jdk` para instalar el JDK.</span><span class="sxs-lookup"><span data-stu-id="05ebe-112">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span></span>
    * <span data-ttu-id="05ebe-113">Asegúrese de establecer la variable de entorno JAVA_HOME para que apunte a la carpeta donde está instalado el JDK.</span><span class="sxs-lookup"><span data-stu-id="05ebe-113">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span></span>
* <span data-ttu-id="05ebe-114">[Descargar](http://maven.apache.org/download.cgi) e [instalar](http://maven.apache.org/install.html) un archivo binario de [Maven](http://maven.apache.org/)</span><span class="sxs-lookup"><span data-stu-id="05ebe-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="05ebe-115">En Ubuntu, puede ejecutar `apt-get install maven` para instalar Maven.</span><span class="sxs-lookup"><span data-stu-id="05ebe-115">On Ubuntu, you can run `apt-get install maven` to install Maven.</span></span>
* [<span data-ttu-id="05ebe-116">Git</span><span class="sxs-lookup"><span data-stu-id="05ebe-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="05ebe-117">En Ubuntu, puede ejecutar `sudo apt-get install git` para instalar Git.</span><span class="sxs-lookup"><span data-stu-id="05ebe-117">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="05ebe-118">Creación de una cuenta de base de datos</span><span class="sxs-lookup"><span data-stu-id="05ebe-118">Create a database account</span></span>

<span data-ttu-id="05ebe-119">Para poder crear una base de datos de documentos, debe crear una cuenta de SQL Database (DocumentDB) con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="05ebe-119">Before you can create a document database, you need to create a SQL (DocumentDB) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="05ebe-120">Incorporación de una colección</span><span class="sxs-lookup"><span data-stu-id="05ebe-120">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="05ebe-121">Agregar datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="05ebe-121">Add sample data</span></span>

<span data-ttu-id="05ebe-122">Ahora puede agregar datos a la nueva colección mediante el Explorador de datos.</span><span class="sxs-lookup"><span data-stu-id="05ebe-122">You can now add data to your new collection using Data Explorer.</span></span>

1. <span data-ttu-id="05ebe-123">En el Explorador de datos, la nueva base de datos aparece en el panel Colecciones.</span><span class="sxs-lookup"><span data-stu-id="05ebe-123">In Data Explorer, the new database appears in the Collections pane.</span></span> <span data-ttu-id="05ebe-124">Expanda la base de datos **Tareas**, expanda la colección **Elementos**, haga clic en **Documentos** y, después, haga clic en **Nuevos documentos**.</span><span class="sxs-lookup"><span data-stu-id="05ebe-124">Expand the **Tasks** database, expand the **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Creación de documentos en el Explorador de datos en Azure Portal](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="05ebe-126">Ahora agregue un documento a la colección con la estructura siguiente.</span><span class="sxs-lookup"><span data-stu-id="05ebe-126">Now add a document to the collection with the following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="05ebe-127">Cuando haya agregado el archivo JSON a la pestaña **Documentos**, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="05ebe-127">Once you've added the json to the **Documents** tab, click **Save**.</span></span>

    ![Copiar los datos JSON y hacer clic en Guardar en el Explorador de datos en Azure Portal](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="05ebe-129">Cree y guarde un documento más donde insertará un valor único para la propiedad `id` y cambie las demás propiedades como corresponda.</span><span class="sxs-lookup"><span data-stu-id="05ebe-129">Create and save one more document where you insert a unique value for the `id` property, and change the other properties as you see fit.</span></span> <span data-ttu-id="05ebe-130">Los nuevos documentos pueden tener la estructura que quiera, ya que Azure Cosmos DB no impone ningún esquema en los datos.</span><span class="sxs-lookup"><span data-stu-id="05ebe-130">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="05ebe-131">Ahora puede usar consultas en el Explorador de datos para recuperar los datos haciendo clic en los botones **Editar filtro** y **Aplicar filtro**.</span><span class="sxs-lookup"><span data-stu-id="05ebe-131">You can now use queries in Data Explorer to retrieve your data by clicking the **Edit Filter** and **Apply Filter** buttons.</span></span> <span data-ttu-id="05ebe-132">De forma predeterminada, el Explorador de datos usa `SELECT * FROM c` para recuperar todos los documentos de la colección, pero puede cambiarlo por una [consulta SQL](documentdb-sql-query.md) diferente, como `SELECT * FROM c ORDER BY c._ts DESC`, para devolver todos los documentos en orden descendente en función de su marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="05ebe-132">By default, Data Explorer uses `SELECT * FROM c` to retrieve all documents in the collection, but you can change that to a different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, to return all the documents in descending order based on their timestamp.</span></span> 
 
     <span data-ttu-id="05ebe-133">También puede usar el Explorador de datos para crear procedimientos almacenados, UDF y desencadenadores para realizar la lógica de negocios del servidor, así como escalar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="05ebe-133">You can also use Data Explorer to create stored procedures, UDFs, and triggers to perform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="05ebe-134">El Explorador de datos expone todo el acceso a datos mediante programación integrado que está disponible en las API, pero permite un acceso fácil a los datos de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="05ebe-134">Data Explorer exposes all of the built-in programmatic data access available in the APIs, but provides easy access to your data in the Azure portal.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="05ebe-135">Clonación de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="05ebe-135">Clone the sample application</span></span>

<span data-ttu-id="05ebe-136">Ahora vamos a empezar a trabajar con el código.</span><span class="sxs-lookup"><span data-stu-id="05ebe-136">Now let's switch to working with code.</span></span> <span data-ttu-id="05ebe-137">Vamos a clonar una aplicación de API DocumentDB desde GitHub, a establecer la cadena de conexión y a ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="05ebe-137">Let's clone a DocumentDB API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="05ebe-138">Verá lo fácil que es trabajar con datos mediante programación.</span><span class="sxs-lookup"><span data-stu-id="05ebe-138">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="05ebe-139">Abra una ventana de terminal de Git, como Git Bash, y `CD` en un directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="05ebe-139">Open a git terminal window, such as git bash, and `CD` to a working directory.</span></span>  

2. <span data-ttu-id="05ebe-140">Ejecute el comando siguiente para clonar el repositorio de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="05ebe-140">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-the-code"></a><span data-ttu-id="05ebe-141">Revisar el código</span><span class="sxs-lookup"><span data-stu-id="05ebe-141">Review the code</span></span>

<span data-ttu-id="05ebe-142">Vamos a revisar rápidamente lo que sucede en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="05ebe-142">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="05ebe-143">Abra el archivo `Program.java` y, en la carpeta \src\GetStarted, busque las líneas de código que crean los recursos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="05ebe-143">Open the `Program.java` file from the \src\GetStarted folder, and find these lines of code that create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="05ebe-144">Se inicializa `DocumentClient`.</span><span class="sxs-lookup"><span data-stu-id="05ebe-144">The `DocumentClient` is initialized.</span></span>

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* <span data-ttu-id="05ebe-145">Se crea una base de datos.</span><span class="sxs-lookup"><span data-stu-id="05ebe-145">A new database is created.</span></span>

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* <span data-ttu-id="05ebe-146">Se crea una colección.</span><span class="sxs-lookup"><span data-stu-id="05ebe-146">A new collection is created.</span></span>

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* <span data-ttu-id="05ebe-147">Se crean algunos documentos.</span><span class="sxs-lookup"><span data-stu-id="05ebe-147">Some documents are created.</span></span>

    ```java
    // Any Java object within your code can be serialized into JSON and written to Azure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* <span data-ttu-id="05ebe-148">Se realiza una consulta SQL en JSON.</span><span class="sxs-lookup"><span data-stu-id="05ebe-148">A SQL query over JSON is performed.</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="05ebe-149">Actualizar la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="05ebe-149">Update your connection string</span></span>

<span data-ttu-id="05ebe-150">Ahora vuelva a Azure Portal para obtener la información de la cadena de conexión y cópiela en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="05ebe-150">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span> <span data-ttu-id="05ebe-151">Esto permitirá que la aplicación se comunique con la base de datos hospedada.</span><span class="sxs-lookup"><span data-stu-id="05ebe-151">This will enable your app to communicate with your hosted database.</span></span>

1. <span data-ttu-id="05ebe-152">En [Azure Portal](http://portal.azure.com/), en la cuenta de Azure Cosmos DB, en el panel de navegación izquierdo, haga clic en **Claves** y en **Claves de lectura y escritura**.</span><span class="sxs-lookup"><span data-stu-id="05ebe-152">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="05ebe-153">Deberá usar los botones de copia del lado derecho de la pantalla para copiar el valor de URI y de PRIMARY KEY (clave principal) en el archivo `Program.java` en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="05ebe-153">You'll use the copy buttons on the right side of the screen to copy the URI and PRIMARY KEY into the `Program.java` file in the next step.</span></span>

    ![Visualización y copia de una clave de acceso en Azure Portal, hoja Claves](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="05ebe-155">En el archivo `Program.java`, copie el valor del URI desde el portal (con el botón de copia) y conviértalo en el valor del punto de conexión al constructor DocumentClient en `Program.java`.</span><span class="sxs-lookup"><span data-stu-id="05ebe-155">In the open `Program.java` file, copy your URI value from the portal (using the copy button) and make it the value of the endpoint to the DocumentClient constructor in `Program.java`.</span></span> 

    `"https://FILLME.documents.azure.com"`

4. <span data-ttu-id="05ebe-156">A continuación, copie el valor de PRIMARY KEY del portal y péguelo sobre "FILLME", convirtiéndolo en el segundo parámetro del constructor DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="05ebe-156">Then copy your PRIMARY KEY value from the portal and paste it over “FILLME”, making it the second parameter in the DocumentClient constructor.</span></span> <span data-ttu-id="05ebe-157">Ya ha actualizado la aplicación con toda la información que necesita para comunicarse con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="05ebe-157">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-the-app"></a><span data-ttu-id="05ebe-158">Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="05ebe-158">Run the app</span></span>

1. <span data-ttu-id="05ebe-159">En la ventana del terminal de git, use `cd` para cambiar a la carpeta azure-cosmos-db-documentdb-java-getting-started.</span><span class="sxs-lookup"><span data-stu-id="05ebe-159">In the git terminal window, `cd` to the azure-cosmos-db-documentdb-java-getting-started folder.</span></span>

2. <span data-ttu-id="05ebe-160">En la ventana del terminal de git, escriba `mvn package` para instalar los paquetes Java necesarios.</span><span class="sxs-lookup"><span data-stu-id="05ebe-160">In the git terminal window, type `mvn package` to install the required Java packages.</span></span>

3. <span data-ttu-id="05ebe-161">En la ventana del terminal de git, ejecute `mvn exec:java -D exec.mainClass=GetStarted.Program` para iniciar la aplicación de Java.</span><span class="sxs-lookup"><span data-stu-id="05ebe-161">In the git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in the terminal window to start your Java application.</span></span>

    <span data-ttu-id="05ebe-162">En la ventana del terminal, recibirá la notificación de que se creó la base de datos FamilyDB y se le pedirá que presione una tecla para continuar.</span><span class="sxs-lookup"><span data-stu-id="05ebe-162">In the terminal window, you'll receive notification that the FamilyDB database was created, and to press a key to continue.</span></span> <span data-ttu-id="05ebe-163">Presione una tecla para crear la base de datos, a continuación cambie al Explorador de datos y verá que ahora contiene una base de datos FamilyDB.</span><span class="sxs-lookup"><span data-stu-id="05ebe-163">Press a key to create the database, then switch to the Data Explorer and you'll see that it now contains a FamilyDB database.</span></span> <span data-ttu-id="05ebe-164">Continúe presionando las teclas para crear la colección y los documentos y, a continuación, realizar una consulta.</span><span class="sxs-lookup"><span data-stu-id="05ebe-164">Continue to press keys to create the collection and the documents and then perform a query.</span></span> <span data-ttu-id="05ebe-165">Cuando se complete el proyecto, se eliminan los recursos de su cuenta.</span><span class="sxs-lookup"><span data-stu-id="05ebe-165">When the project completes, the resources are deleted from your account.</span></span> 

    ![Visualización y copia de una clave de acceso en Azure Portal, hoja Claves](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="05ebe-167">Revisar los SLA en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="05ebe-167">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="05ebe-168">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="05ebe-168">Clean up resources</span></span>

<span data-ttu-id="05ebe-169">Si no va a seguir usando esta aplicación, siga estos pasos para eliminar todos los recursos creados en esta guía de inicio rápido en Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="05ebe-169">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="05ebe-170">En el menú de la izquierda de Azure Portal, haga clic en **Grupos de recursos** y en el nombre del recurso que creó.</span><span class="sxs-lookup"><span data-stu-id="05ebe-170">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="05ebe-171">En la página del grupo de recursos, haga clic en **Eliminar**, escriba en el cuadro de texto el nombre del recurso que quiere eliminar y haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="05ebe-171">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05ebe-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="05ebe-172">Next steps</span></span>

<span data-ttu-id="05ebe-173">En esta guía de inicio rápido, ha aprendido a crear una cuenta de Azure Cosmos DB, una base de datos de documentos y una colección mediante el Explorador de datos, así como a ejecutar una aplicación para que haga lo mismo mediante programación.</span><span class="sxs-lookup"><span data-stu-id="05ebe-173">In this quickstart, you've learned how to create an Azure Cosmos DB account, document database, and collection using the Data Explorer, and run an app to do the same thing programmatically.</span></span> <span data-ttu-id="05ebe-174">Ahora puede importar datos adicionales en la cuenta de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="05ebe-174">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="05ebe-175">Importación de datos a Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="05ebe-175">Import data into Azure Cosmos DB</span></span>](import-data.md)


