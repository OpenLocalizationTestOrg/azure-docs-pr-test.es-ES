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
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-hello-azure-portal"></a><span data-ttu-id="9772a-103">Azure Cosmos DB: Compilar una aplicación de consola de API de MongoDB con Java y Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9772a-103">Azure Cosmos DB: Build a MongoDB API console app with Java and hello Azure portal</span></span>

<span data-ttu-id="9772a-104">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9772a-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="9772a-105">Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente.</span><span class="sxs-lookup"><span data-stu-id="9772a-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="9772a-106">Este inicio rápido muestra cómo toocreate una cuenta de base de datos de Azure Cosmos, la base de datos de documento y la colección mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9772a-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="9772a-107">A continuación, podrá compilar e implementar una aplicación de consola compilada en hello [controlador MongoDB Java](https://docs.mongodb.com/ecosystem/drivers/java/).</span><span class="sxs-lookup"><span data-stu-id="9772a-107">You'll then build and deploy a console app built on hello [MongoDB Java driver](https://docs.mongodb.com/ecosystem/drivers/java/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9772a-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9772a-108">Prerequisites</span></span>

* <span data-ttu-id="9772a-109">Para poder ejecutar este ejemplo, debe tener Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="9772a-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
   * <span data-ttu-id="9772a-110">JDK 1.7+ (ejecute `apt-get install default-jdk` si no tiene JDK)</span><span class="sxs-lookup"><span data-stu-id="9772a-110">JDK 1.7+ (Run `apt-get install default-jdk` if you don't have JDK)</span></span>
   * <span data-ttu-id="9772a-111">Maven (ejecute `apt-get install maven` si no tiene Maven)</span><span class="sxs-lookup"><span data-stu-id="9772a-111">Maven (Run `apt-get install maven` if you don't have Maven)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="9772a-112">Creación de una cuenta de base de datos</span><span class="sxs-lookup"><span data-stu-id="9772a-112">Create a database account</span></span>

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a><span data-ttu-id="9772a-113">Agregar una colección</span><span class="sxs-lookup"><span data-stu-id="9772a-113">Add a collection</span></span>

<span data-ttu-id="9772a-114">Asígnele un nombre a la base de datos nueva (**db**) y a la nueva colección (**coll**).</span><span class="sxs-lookup"><span data-stu-id="9772a-114">Name your new database, **db**, and your new collection, **coll**.</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="9772a-115">Clonar aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="9772a-115">Clone hello sample application</span></span>

<span data-ttu-id="9772a-116">Ahora vamos a clonar una API de MongoDB aplicación de github, establezca la cadena de conexión de Hola y ejecútelo.</span><span class="sxs-lookup"><span data-stu-id="9772a-116">Now let's clone a MongoDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="9772a-117">Podrá ver lo fácil que es toowork con datos mediante programación.</span><span class="sxs-lookup"><span data-stu-id="9772a-117">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="9772a-118">Abra una ventana de terminal de git, como git bash, y `cd` tooa directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="9772a-118">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="9772a-119">Ejecute hello después de repositorio de ejemplo de comando tooclone Hola.</span><span class="sxs-lookup"><span data-stu-id="9772a-119">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. <span data-ttu-id="9772a-120">A continuación, abra el archivo de solución de hello en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9772a-120">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="9772a-121">Revise el código de hello</span><span class="sxs-lookup"><span data-stu-id="9772a-121">Review hello code</span></span>

<span data-ttu-id="9772a-122">Vamos a hacer una revisión rápida de lo que sucede en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9772a-122">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="9772a-123">Abra hello `Program.cs` archivo y encontrará que estas líneas de código crean Hola recursos de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="9772a-123">Open hello `Program.cs` file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="9772a-124">Hola DocumentClient se inicializa.</span><span class="sxs-lookup"><span data-stu-id="9772a-124">hello DocumentClient is initialized.</span></span>

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* <span data-ttu-id="9772a-125">Se crean una base de datos y una colección.</span><span class="sxs-lookup"><span data-stu-id="9772a-125">A new database and collection are created.</span></span>

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* <span data-ttu-id="9772a-126">Se insertan algunos documentos mediante `MongoCollection.insertOne`.</span><span class="sxs-lookup"><span data-stu-id="9772a-126">Some documents are inserted using `MongoCollection.insertOne`</span></span>

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* <span data-ttu-id="9772a-127">Se realizan algunas consultas mediante `MongoCollection.find`.</span><span class="sxs-lookup"><span data-stu-id="9772a-127">Some queries are performed using `MongoCollection.find`</span></span>

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="9772a-128">Actualizar la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="9772a-128">Update your connection string</span></span>

<span data-ttu-id="9772a-129">Ahora vuelva atrás toohello tooget portal Azure la información de la cadena de conexión y se copia en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9772a-129">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="9772a-130">En la cuenta de hello, seleccione **inicio rápido**, seleccione Java y luego copiar Portapapeles de tooyour de cadena de conexión de Hola</span><span class="sxs-lookup"><span data-stu-id="9772a-130">From hello Account, select **Quick Start**, select Java, then copy hello connection string tooyour clipboard</span></span>

2. <span data-ttu-id="9772a-131">Abra hello `Program.java` archivo, reemplace el constructor de hello argumento toohello MongoClientURI con la cadena de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="9772a-131">Open hello `Program.java` file, replace hello argument toohello MongoClientURI constructor with hello connection string.</span></span> <span data-ttu-id="9772a-132">Ahora ha actualizado la aplicación con toda la información de hello debe toocommunicate con base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="9772a-132">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-console-app"></a><span data-ttu-id="9772a-133">Ejecutar la aplicación de consola de hello</span><span class="sxs-lookup"><span data-stu-id="9772a-133">Run hello console app</span></span>

1. <span data-ttu-id="9772a-134">Ejecutar `mvn package` en un terminal tooinstall necesario módulos npm</span><span class="sxs-lookup"><span data-stu-id="9772a-134">Run `mvn package` in a terminal tooinstall required npm modules</span></span>

2. <span data-ttu-id="9772a-135">Ejecutar `mvn exec:java -D exec.mainClass=GetStarted.Program` en un terminal toostart la aplicación de Java.</span><span class="sxs-lookup"><span data-stu-id="9772a-135">Run `mvn exec:java -D exec.mainClass=GetStarted.Program` in a terminal toostart your Java application.</span></span>

<span data-ttu-id="9772a-136">Ahora puede usar [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) tooquery, modificar y trabajar con nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="9772a-136">You can now use [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) tooquery, modify, and work with this new data.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="9772a-137">Revise los SLA de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9772a-137">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="9772a-138">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="9772a-138">Clean up resources</span></span>

<span data-ttu-id="9772a-139">Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial rápido de hello portal de Azure con hello pasos:</span><span class="sxs-lookup"><span data-stu-id="9772a-139">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="9772a-140">En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="9772a-140">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="9772a-141">En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="9772a-141">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9772a-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9772a-142">Next steps</span></span>

<span data-ttu-id="9772a-143">En este tutorial, ha aprendido cómo crear una colección mediante Hola Explorador de datos toocreate una cuenta de base de datos de Azure Cosmos y ejecutar una aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="9772a-143">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run a console app.</span></span> <span data-ttu-id="9772a-144">Ahora puede importar la cuenta de base de datos de Cosmos tooyour datos adicionales.</span><span class="sxs-lookup"><span data-stu-id="9772a-144">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="9772a-145">Importación de datos de MongoDB a Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9772a-145">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)


