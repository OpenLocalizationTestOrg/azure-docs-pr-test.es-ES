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
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-hello-azure-portal"></a><span data-ttu-id="9d7e0-103">Azure Cosmos DB: Crear una base de datos de documentos mediante Java y Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9d7e0-103">Azure Cosmos DB: Create a document database using Java and hello Azure portal</span></span>

<span data-ttu-id="9d7e0-104">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="9d7e0-105">Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="9d7e0-106">Este tutorial crea un documento de base de datos mediante Hola herramientas del portal Azure para la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-106">This quickstart creates a document database using hello Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="9d7e0-107">Este tutorial rápido muestra también cómo tooquickly crear una aplicación de consola de Java con hello [API de Java de DocumentDB](documentdb-sdk-java.md).</span><span class="sxs-lookup"><span data-stu-id="9d7e0-107">This quickstart also shows you how tooquickly create a Java console app using hello [DocumentDB Java API](documentdb-sdk-java.md).</span></span> <span data-ttu-id="9d7e0-108">instrucciones de Hello en este tutorial rápido se pueden aplicar en cualquier sistema operativo que sea capaz de ejecutar Java.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-108">hello instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="9d7e0-109">Al completar este tutorial rápido estará familiarizado con la creación y modificación de los recursos de base de datos de documento en hello interfaz de usuario o mediante programación, lo que sea su preferencia.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-109">By completing this quickstart you'll be familiar with creating and modifying document database resources in either hello UI or programatically, whichever is your preference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d7e0-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9d7e0-110">Prerequisites</span></span>

* [<span data-ttu-id="9d7e0-111">Kit de desarrollo de Java (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="9d7e0-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="9d7e0-112">En Ubuntu, ejecute `apt-get install default-jdk` tooinstall Hola JDK.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-112">On Ubuntu, run `apt-get install default-jdk` tooinstall hello JDK.</span></span>
    * <span data-ttu-id="9d7e0-113">Ser seguro tooset Hola JAVA_HOME entorno variable toopoint toohello carpeta donde está instalado Hola JDK.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-113">Be sure tooset hello JAVA_HOME environment variable toopoint toohello folder where hello JDK is installed.</span></span>
* <span data-ttu-id="9d7e0-114">[Descargar](http://maven.apache.org/download.cgi) e [instalar](http://maven.apache.org/install.html) un archivo binario de [Maven](http://maven.apache.org/)</span><span class="sxs-lookup"><span data-stu-id="9d7e0-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="9d7e0-115">En Ubuntu, se pueden ejecutar `apt-get install maven` tooinstall Maven.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-115">On Ubuntu, you can run `apt-get install maven` tooinstall Maven.</span></span>
* [<span data-ttu-id="9d7e0-116">Git</span><span class="sxs-lookup"><span data-stu-id="9d7e0-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="9d7e0-117">En Ubuntu, se pueden ejecutar `sudo apt-get install git` tooinstall Git.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-117">On Ubuntu, you can run `sudo apt-get install git` tooinstall Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="9d7e0-118">Creación de una cuenta de base de datos</span><span class="sxs-lookup"><span data-stu-id="9d7e0-118">Create a database account</span></span>

<span data-ttu-id="9d7e0-119">Antes de poder crear una base de datos de documento, debe toocreate una cuenta de base de datos SQL (documentos) con la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-119">Before you can create a document database, you need toocreate a SQL (DocumentDB) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="9d7e0-120">Incorporación de una colección</span><span class="sxs-lookup"><span data-stu-id="9d7e0-120">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="9d7e0-121">Agregar datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="9d7e0-121">Add sample data</span></span>

<span data-ttu-id="9d7e0-122">Ahora puede agregar datos tooyour nueva colección mediante el Explorador de datos.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-122">You can now add data tooyour new collection using Data Explorer.</span></span>

1. <span data-ttu-id="9d7e0-123">En el Explorador de datos, base de datos nueva Hola aparece en panel de colecciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-123">In Data Explorer, hello new database appears in hello Collections pane.</span></span> <span data-ttu-id="9d7e0-124">Expanda hello **tareas** la base de datos, expanda hello **elementos** colección, haga clic en **documentos**y, a continuación, haga clic en **nuevos documentos**.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-124">Expand hello **Tasks** database, expand hello **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Crear nuevos documentos en el Explorador de datos en hello portal de Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="9d7e0-126">Ahora puede agregar una colección de toohello de documento con hello siguiendo la estructura.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-126">Now add a document toohello collection with hello following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="9d7e0-127">Una vez que haya agregado Hola json toohello **documentos** , haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-127">Once you've added hello json toohello **Documents** tab, click **Save**.</span></span>

    ![Copiar datos de json y haga clic en Guardar en el Explorador de datos en hello portal de Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="9d7e0-129">Crear y guardar un documento más donde insertar un valor único para hello `id` propiedad y cambio Hola otras propiedades como considere oportuno.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-129">Create and save one more document where you insert a unique value for hello `id` property, and change hello other properties as you see fit.</span></span> <span data-ttu-id="9d7e0-130">Los nuevos documentos pueden tener la estructura que quiera, ya que Azure Cosmos DB no impone ningún esquema en los datos.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-130">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="9d7e0-131">Ahora use consultas en Explorador de datos tooretrieve los datos haciendo clic en hello puede **Editar filtro** y **aplicar filtro** botones.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-131">You can now use queries in Data Explorer tooretrieve your data by clicking hello **Edit Filter** and **Apply Filter** buttons.</span></span> <span data-ttu-id="9d7e0-132">De forma predeterminada, usa el Explorador de datos `SELECT * FROM c` tooretrieve todos los documentos en la colección de hello, pero puede cambiar ese tooa diferentes [consulta SQL](documentdb-sql-query.md), como `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn todos los documentos de hello en orden descendente en función de su marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-132">By default, Data Explorer uses `SELECT * FROM c` tooretrieve all documents in hello collection, but you can change that tooa different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn all hello documents in descending order based on their timestamp.</span></span> 
 
     <span data-ttu-id="9d7e0-133">También puede usar procedimientos de explorador de datos toocreate almacenado, UDF y lógica de negocios de servidor de tooperform de desencadenadores, así como el rendimiento de escala.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-133">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="9d7e0-134">Explorador de datos expone todo acceso a los datos de mediante programación integrada Hola disponible en las API de hello, pero proporciona un acceso sencillo tooyour datos Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-134">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="9d7e0-135">Clonar aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="9d7e0-135">Clone hello sample application</span></span>

<span data-ttu-id="9d7e0-136">Ahora vamos a cambiar tooworking con el código.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-136">Now let's switch tooworking with code.</span></span> <span data-ttu-id="9d7e0-137">Vamos a clonar una aplicación de API de documentos de GitHub, establezca la cadena de conexión de Hola y ejecútelo.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-137">Let's clone a DocumentDB API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="9d7e0-138">Vea lo fácil que es toowork con datos mediante programación.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-138">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="9d7e0-139">Abra una ventana de terminal de git, como git bash, y `CD` tooa directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-139">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="9d7e0-140">Ejecute hello después de repositorio de ejemplo de comando tooclone Hola.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-140">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="9d7e0-141">Revise el código de hello</span><span class="sxs-lookup"><span data-stu-id="9d7e0-141">Review hello code</span></span>

<span data-ttu-id="9d7e0-142">Vamos a hacer una revisión rápida de lo que sucede en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-142">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="9d7e0-143">Abra hello `Program.java` archivo de hello \src\GetStarted carpeta y busque estas líneas de código que cree Hola recursos de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-143">Open hello `Program.java` file from hello \src\GetStarted folder, and find these lines of code that create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="9d7e0-144">Hola `DocumentClient` se inicializa.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-144">hello `DocumentClient` is initialized.</span></span>

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* <span data-ttu-id="9d7e0-145">Se crea una base de datos.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-145">A new database is created.</span></span>

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* <span data-ttu-id="9d7e0-146">Se crea una colección.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-146">A new collection is created.</span></span>

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* <span data-ttu-id="9d7e0-147">Se crean algunos documentos.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-147">Some documents are created.</span></span>

    ```java
    // Any Java object within your code can be serialized into JSON and written tooAzure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* <span data-ttu-id="9d7e0-148">Se realiza una consulta SQL en JSON.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-148">A SQL query over JSON is performed.</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="9d7e0-149">Actualizar la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="9d7e0-149">Update your connection string</span></span>

<span data-ttu-id="9d7e0-150">Ahora vuelva atrás toohello tooget portal Azure la información de la cadena de conexión y se copia en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-150">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span> <span data-ttu-id="9d7e0-151">Esto le permitirá la toocommunicate de aplicación con la base de datos hospedado.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-151">This will enable your app toocommunicate with your hosted database.</span></span>

1. <span data-ttu-id="9d7e0-152">Hola [portal de Azure](http://portal.azure.com/), en la base de datos de Azure Cosmos account, Hola barra de navegación izquierda, haga clic en **claves**y, a continuación, haga clic en **claves de lectura y escritura**.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-152">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="9d7e0-153">Usará Hola copia botones en hello derecha de hello toocopy de pantalla Hola URI y la clave principal en hello `Program.java` archivo en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-153">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and PRIMARY KEY into hello `Program.java` file in hello next step.</span></span>

    ![Ver y copiar una clave de acceso en hello portal de Azure, hoja de claves](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="9d7e0-155">Hola abierto `Program.java` de archivos, copie el valor URI de portal hello (mediante el botón Copiar de hello) y hacerla Hola valor del constructor de hello extremo toohello DocumentClient en `Program.java`.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-155">In hello open `Program.java` file, copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint toohello DocumentClient constructor in `Program.java`.</span></span> 

    `"https://FILLME.documents.azure.com"`

4. <span data-ttu-id="9d7e0-156">A continuación, copie el valor de clave principal del portal de Hola y péguela sobre "FILLME", lo que Hola segundo parámetro de constructor de DocumentClient Hola.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-156">Then copy your PRIMARY KEY value from hello portal and paste it over “FILLME”, making it hello second parameter in hello DocumentClient constructor.</span></span> <span data-ttu-id="9d7e0-157">Ahora ha actualizado la aplicación con toda la información de hello debe toocommunicate con base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-157">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-app"></a><span data-ttu-id="9d7e0-158">Ejecutar aplicación hello</span><span class="sxs-lookup"><span data-stu-id="9d7e0-158">Run hello app</span></span>

1. <span data-ttu-id="9d7e0-159">En la ventana de terminal de git hello, `cd` toohello azure-cosmos-db-documentdb-java-getting-started carpeta.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-159">In hello git terminal window, `cd` toohello azure-cosmos-db-documentdb-java-getting-started folder.</span></span>

2. <span data-ttu-id="9d7e0-160">En la ventana de terminal de git hello, escriba `mvn package` tooinstall Hola necesario paquetes de Java.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-160">In hello git terminal window, type `mvn package` tooinstall hello required Java packages.</span></span>

3. <span data-ttu-id="9d7e0-161">En la ventana de terminal de git hello, ejecute `mvn exec:java -D exec.mainClass=GetStarted.Program` en Hola ventana de terminal toostart la aplicación de Java.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-161">In hello git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in hello terminal window toostart your Java application.</span></span>

    <span data-ttu-id="9d7e0-162">En la ventana de terminal de hello, recibirá una notificación que Hola FamilyDB se creó la base de datos y toopress un toocontinue clave.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-162">In hello terminal window, you'll receive notification that hello FamilyDB database was created, and toopress a key toocontinue.</span></span> <span data-ttu-id="9d7e0-163">Presione una base de datos de clave toocreate hello, enciéndala toohello Explorador de datos y verá que ahora contiene una base de datos de FamilyDB.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-163">Press a key toocreate hello database, then switch toohello Data Explorer and you'll see that it now contains a FamilyDB database.</span></span> <span data-ttu-id="9d7e0-164">Continuar toopress claves toocreate Hola hello y colección de documentos y, a continuación, realizar una consulta.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-164">Continue toopress keys toocreate hello collection and hello documents and then perform a query.</span></span> <span data-ttu-id="9d7e0-165">Cuando se completa el proyecto de hello, recursos de Hola se eliminan de su cuenta.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-165">When hello project completes, hello resources are deleted from your account.</span></span> 

    ![Ver y copiar una clave de acceso en hello portal de Azure, hoja de claves](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="9d7e0-167">Revise los SLA de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9d7e0-167">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="9d7e0-168">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="9d7e0-168">Clean up resources</span></span>

<span data-ttu-id="9d7e0-169">Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial rápido de hello portal de Azure con hello pasos:</span><span class="sxs-lookup"><span data-stu-id="9d7e0-169">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="9d7e0-170">En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-170">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="9d7e0-171">En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-171">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d7e0-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9d7e0-172">Next steps</span></span>

<span data-ttu-id="9d7e0-173">En este tutorial, ha aprendido cómo toocreate una cuenta de base de datos de Azure Cosmos, la base de datos de documento y la colección mediante Hola Explorador de datos y ejecutar una aplicación toodo Hola lo mismo mediante programación.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-173">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, document database, and collection using hello Data Explorer, and run an app toodo hello same thing programmatically.</span></span> <span data-ttu-id="9d7e0-174">Ahora puede importar la cuenta de base de datos de Cosmos tooyour datos adicionales.</span><span class="sxs-lookup"><span data-stu-id="9d7e0-174">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="9d7e0-175">Importación de datos a Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9d7e0-175">Import data into Azure Cosmos DB</span></span>](import-data.md)


