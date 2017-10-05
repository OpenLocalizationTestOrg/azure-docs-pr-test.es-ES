---
title: "Azure Cosmos DB: Compilar una aplicación de consola con Java y la API MongoDB | Microsoft Docs"
description: "En este tema se presenta un ejemplo de código de Java que se puede usar para conectarse a la API MongoDB de Azure Cosmos DB y realizar consultas."
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
ms.openlocfilehash: f84294d7d324f094d173f7a2ec89759266a74210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-the-azure-portal"></a><span data-ttu-id="4f9d4-103">Azure Cosmos DB: Compilar una aplicación de consola de la API MongoDB con Java y Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4f9d4-103">Azure Cosmos DB: Build a MongoDB API console app with Java and the Azure portal</span></span>

<span data-ttu-id="4f9d4-104">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="4f9d4-105">Puede crear rápidamente bases de datos de documentos, clave-valor y grafos, y realizar consultas en ellas. Todas las bases de datos se beneficiarán de las funcionalidades de distribución global y escalado horizontal en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="4f9d4-106">En esta guía de inicio rápido se muestra cómo crear una cuenta, una base de datos de documentos y una colección de Azure Cosmos DB mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="4f9d4-107">Después, compilará e implementará una aplicación de consola compilada en el [controlador Java de MongoDB](https://docs.mongodb.com/ecosystem/drivers/java/).</span><span class="sxs-lookup"><span data-stu-id="4f9d4-107">You'll then build and deploy a console app built on the [MongoDB Java driver](https://docs.mongodb.com/ecosystem/drivers/java/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4f9d4-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4f9d4-108">Prerequisites</span></span>

* <span data-ttu-id="4f9d4-109">Antes de ejecutar este ejemplo, debe cumplir los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="4f9d4-109">Before you can run this sample, you must have the following prerequisites:</span></span>
   * <span data-ttu-id="4f9d4-110">JDK 1.7+ (ejecute `apt-get install default-jdk` si no tiene JDK)</span><span class="sxs-lookup"><span data-stu-id="4f9d4-110">JDK 1.7+ (Run `apt-get install default-jdk` if you don't have JDK)</span></span>
   * <span data-ttu-id="4f9d4-111">Maven (ejecute `apt-get install maven` si no tiene Maven)</span><span class="sxs-lookup"><span data-stu-id="4f9d4-111">Maven (Run `apt-get install maven` if you don't have Maven)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="4f9d4-112">Creación de una cuenta de base de datos</span><span class="sxs-lookup"><span data-stu-id="4f9d4-112">Create a database account</span></span>

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a><span data-ttu-id="4f9d4-113">Agregar una colección</span><span class="sxs-lookup"><span data-stu-id="4f9d4-113">Add a collection</span></span>

<span data-ttu-id="4f9d4-114">Asígnele un nombre a la base de datos nueva (**db**) y a la nueva colección (**coll**).</span><span class="sxs-lookup"><span data-stu-id="4f9d4-114">Name your new database, **db**, and your new collection, **coll**.</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="4f9d4-115">Clonación de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4f9d4-115">Clone the sample application</span></span>

<span data-ttu-id="4f9d4-116">Ahora vamos a clonar una aplicación de API MongoDB desde GitHub, establecer la cadena de conexión y ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-116">Now let's clone a MongoDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="4f9d4-117">Verá lo fácil que es trabajar con datos mediante programación.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-117">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="4f9d4-118">Abra una ventana de terminal de Git, como Git Bash, y `cd` en un directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-118">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="4f9d4-119">Ejecute el comando siguiente para clonar el repositorio de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-119">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. <span data-ttu-id="4f9d4-120">Después, abra el archivo de solución en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-120">Then open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="4f9d4-121">Revisión del código</span><span class="sxs-lookup"><span data-stu-id="4f9d4-121">Review the code</span></span>

<span data-ttu-id="4f9d4-122">Vamos a revisar rápidamente lo que sucede en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-122">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="4f9d4-123">Abra el archivo `Program.cs` y observe que estas líneas de código crean los recursos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-123">Open the `Program.cs` file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="4f9d4-124">Se inicializa DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-124">The DocumentClient is initialized.</span></span>

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* <span data-ttu-id="4f9d4-125">Se crean una base de datos y una colección.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-125">A new database and collection are created.</span></span>

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* <span data-ttu-id="4f9d4-126">Se insertan algunos documentos mediante `MongoCollection.insertOne`.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-126">Some documents are inserted using `MongoCollection.insertOne`</span></span>

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* <span data-ttu-id="4f9d4-127">Se realizan algunas consultas mediante `MongoCollection.find`.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-127">Some queries are performed using `MongoCollection.find`</span></span>

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="4f9d4-128">Actualizar la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="4f9d4-128">Update your connection string</span></span>

<span data-ttu-id="4f9d4-129">Ahora vuelva a Azure Portal para obtener la información de la cadena de conexión y cópiela en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-129">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="4f9d4-130">En la cuenta, seleccione **Inicio rápido**, elija Java y copie la cadena de conexión en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-130">From the Account, select **Quick Start**, select Java, then copy the connection string to your clipboard</span></span>

2. <span data-ttu-id="4f9d4-131">Abra el archivo `Program.java` y reemplace el argumento del constructor MongoClientURI por la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-131">Open the `Program.java` file, replace the argument to the MongoClientURI constructor with the connection string.</span></span> <span data-ttu-id="4f9d4-132">Ya ha actualizado la aplicación con toda la información que necesita para comunicarse con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-132">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-the-console-app"></a><span data-ttu-id="4f9d4-133">Ejecutar la aplicación de consola</span><span class="sxs-lookup"><span data-stu-id="4f9d4-133">Run the console app</span></span>

1. <span data-ttu-id="4f9d4-134">Ejecute `mvn package` en un terminal para instalar los módulos npm necesarios.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-134">Run `mvn package` in a terminal to install required npm modules</span></span>

2. <span data-ttu-id="4f9d4-135">Ejecute `mvn exec:java -D exec.mainClass=GetStarted.Program` en un terminal para iniciar la aplicación de Java.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-135">Run `mvn exec:java -D exec.mainClass=GetStarted.Program` in a terminal to start your Java application.</span></span>

<span data-ttu-id="4f9d4-136">Ahora puede usar [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) para consultar, modificar y trabajar con estos nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-136">You can now use [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) to query, modify, and work with this new data.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="4f9d4-137">Revisar los SLA en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4f9d4-137">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="4f9d4-138">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="4f9d4-138">Clean up resources</span></span>

<span data-ttu-id="4f9d4-139">Si no va a seguir usando esta aplicación, siga estos pasos para eliminar todos los recursos creados en esta guía de inicio rápido en Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="4f9d4-139">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="4f9d4-140">En el menú de la izquierda de Azure Portal, haga clic en **Grupos de recursos** y en el nombre del recurso que creó.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-140">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="4f9d4-141">En la página del grupo de recursos, haga clic en **Eliminar**, escriba en el cuadro de texto el nombre del recurso que quiere eliminar y haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-141">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f9d4-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4f9d4-142">Next steps</span></span>

<span data-ttu-id="4f9d4-143">En esta guía de inicio rápido, ha aprendido a crear una cuenta de Azure Cosmos DB, crear una colección mediante el Explorador de datos y ejecutar una aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-143">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run a console app.</span></span> <span data-ttu-id="4f9d4-144">Ahora puede importar datos adicionales en la cuenta de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4f9d4-144">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="4f9d4-145">Importar datos de MongoDB en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4f9d4-145">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)


