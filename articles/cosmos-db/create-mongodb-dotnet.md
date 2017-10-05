---
title: "Azure Cosmos DB: Compilar una aplicación web con .NET y la API MongoDB | Microsoft Docs"
description: "En este tema se presenta un ejemplo de código de .NET que se puede usar para conectarse a la API MongoDB de Azure Cosmos DB y realizar consultas."
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
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 2d30bec75d701b1fd55355d1e139350b6d828c9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-the-azure-portal"></a><span data-ttu-id="8b99d-103">Azure Cosmos DB: Compilar una aplicación web de API MongoDB con .NET y Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8b99d-103">Azure Cosmos DB: Build a MongoDB API web app with .NET and the Azure portal</span></span>

<span data-ttu-id="8b99d-104">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8b99d-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="8b99d-105">Puede crear rápidamente bases de datos de documentos, clave-valor y grafos, y realizar consultas en ellas. Todas las bases de datos se beneficiarán de las funcionalidades de distribución global y escalado horizontal en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b99d-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="8b99d-106">En esta guía de inicio rápido se muestra cómo crear una cuenta, una base de datos de documentos y una colección de Azure Cosmos DB mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="8b99d-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="8b99d-107">Después, compilará e implementará una aplicación web de lista de tareas compilada en el [controlador .NET de MongoDB](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span><span class="sxs-lookup"><span data-stu-id="8b99d-107">You'll then build and deploy a tasks list web app built on the [MongoDB .NET driver](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8b99d-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8b99d-108">Prerequisites</span></span>

<span data-ttu-id="8b99d-109">Si aún no tiene Visual Studio de 2017 instalado, puede descargar y usar la versión **gratis** de [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8b99d-109">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="8b99d-110">Asegúrese de que habilita **Desarrollo de Azure** durante la instalación de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8b99d-110">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="8b99d-111">Creación de una cuenta de base de datos</span><span class="sxs-lookup"><span data-stu-id="8b99d-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="8b99d-112">Clonación de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8b99d-112">Clone the sample application</span></span>

<span data-ttu-id="8b99d-113">Ahora vamos a clonar una aplicación de API MongoDB desde GitHub, establecer la cadena de conexión y ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="8b99d-113">Now let's clone a MongoDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="8b99d-114">Verá lo fácil que es trabajar con datos mediante programación.</span><span class="sxs-lookup"><span data-stu-id="8b99d-114">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="8b99d-115">Abra una ventana de terminal de Git, como Git Bash, y `cd` en un directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="8b99d-115">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="8b99d-116">Ejecute el comando siguiente para clonar el repositorio de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="8b99d-116">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. <span data-ttu-id="8b99d-117">Después, abra el archivo de solución en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8b99d-117">Then open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="8b99d-118">Revisión del código</span><span class="sxs-lookup"><span data-stu-id="8b99d-118">Review the code</span></span>

<span data-ttu-id="8b99d-119">Vamos a revisar rápidamente lo que sucede en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8b99d-119">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="8b99d-120">Abra el archivo **Dal.cs** del directorio **DAL** y observe que estas líneas de código crean los recursos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b99d-120">Open the **Dal.cs** file under the **DAL** directory and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="8b99d-121">Inicialice Mongo Client.</span><span class="sxs-lookup"><span data-stu-id="8b99d-121">Initialize the Mongo Client.</span></span>

    ```cs
        MongoClientSettings settings = new MongoClientSettings();
        settings.Server = new MongoServerAddress(host, 10255);
        settings.UseSsl = true;
        settings.SslSettings = new SslSettings();
        settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;

        MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
        MongoIdentityEvidence evidence = new PasswordEvidence(password);

        settings.Credentials = new List<MongoCredential>()
        {
            new MongoCredential("SCRAM-SHA-1", identity, evidence)
        };

        MongoClient client = new MongoClient(settings);
    ```

* <span data-ttu-id="8b99d-122">Recupere la base de datos y la colección.</span><span class="sxs-lookup"><span data-stu-id="8b99d-122">Retrieve the database and the collection.</span></span>

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* <span data-ttu-id="8b99d-123">Recupere todos los documentos.</span><span class="sxs-lookup"><span data-stu-id="8b99d-123">Retrieve all documents.</span></span>

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="8b99d-124">Actualizar la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="8b99d-124">Update your connection string</span></span>

<span data-ttu-id="8b99d-125">Ahora vuelva a Azure Portal para obtener la información de la cadena de conexión y cópiela en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8b99d-125">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="8b99d-126">En [Azure Portal](http://portal.azure.com/), en la cuenta de Azure Cosmos DB, en el panel de navegación izquierdo, haga clic en **Cadena de conexión** y en **Claves de lectura y escritura**.</span><span class="sxs-lookup"><span data-stu-id="8b99d-126">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Connection String**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="8b99d-127">Deberá usar los botones de copia del lado derecho de la pantalla para copiar el nombre de usuario, la contraseña y el host en el archivo Dal.cs en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="8b99d-127">You'll use the copy buttons on the right side of the screen to copy the Username, Password, and Host into the Dal.cs file in the next step.</span></span>

2. <span data-ttu-id="8b99d-128">Abra el archivo **Dal.cs** en el directorio **DAL**.</span><span class="sxs-lookup"><span data-stu-id="8b99d-128">Open the **Dal.cs** file in the **DAL** directory.</span></span> 

3. <span data-ttu-id="8b99d-129">Copie el valor del **nombre de usuario** del portal (con el botón de copia) y conviértalo en el valor del **nombre de usuario** en el archivo **Dal.cs**.</span><span class="sxs-lookup"><span data-stu-id="8b99d-129">Copy your **username** value from the portal (using the copy button) and make it the value of the **username** in your **Dal.cs** file.</span></span> 

4. <span data-ttu-id="8b99d-130">Después, copie el valor del **host** del portal y conviértalo en el valor del **host** en el archivo **Dal.cs**.</span><span class="sxs-lookup"><span data-stu-id="8b99d-130">Then copy your **host** value from the portal and make it the value of the **host** in your **Dal.cs** file.</span></span> 

5. <span data-ttu-id="8b99d-131">Por último, copie el valor de la **contraseña** del portal y conviértalo en el valor de la **contraseña** en el archivo **Dal.cs**.</span><span class="sxs-lookup"><span data-stu-id="8b99d-131">Finally copy your **password** value from the portal and make it the value of the **password** in your **Dal.cs** file.</span></span> 

<span data-ttu-id="8b99d-132">Ya ha actualizado la aplicación con toda la información que necesita para comunicarse con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b99d-132">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-the-web-app"></a><span data-ttu-id="8b99d-133">Ejecución de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="8b99d-133">Run the web app</span></span>

1. <span data-ttu-id="8b99d-134">En Visual Studio, haga clic con el botón derecho en el proyecto en el **Explorador de soluciones** y, después, haga clic en **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="8b99d-134">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="8b99d-135">En el cuadro **Examinar** de NuGet, escriba *MongoDB.Driver*.</span><span class="sxs-lookup"><span data-stu-id="8b99d-135">In the NuGet **Browse** box, type *MongoDB.Driver*.</span></span>

3. <span data-ttu-id="8b99d-136">En los resultados, instale la biblioteca **MongoDB.Driver**.</span><span class="sxs-lookup"><span data-stu-id="8b99d-136">From the results, install the **MongoDB.Driver** library.</span></span> <span data-ttu-id="8b99d-137">De este modo, se instalan el paquete de MongoDB.Driver y todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="8b99d-137">This installs the MongoDB.Driver package as well as all dependencies.</span></span>

4. <span data-ttu-id="8b99d-138">Presione Ctrl+F5 para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8b99d-138">Click CTRL + F5 to run the application.</span></span> <span data-ttu-id="8b99d-139">La aplicación se muestra en el explorador.</span><span class="sxs-lookup"><span data-stu-id="8b99d-139">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="8b99d-140">Haga clic en **Crear** en el explorador y cree algunas tareas en la aplicación de lista de tareas.</span><span class="sxs-lookup"><span data-stu-id="8b99d-140">Click **Create** in the browser and create a few new tasks in your task list app.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="8b99d-141">Revisar los SLA en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8b99d-141">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="8b99d-142">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="8b99d-142">Clean up resources</span></span>

<span data-ttu-id="8b99d-143">Si no va a seguir usando esta aplicación, siga estos pasos para eliminar todos los recursos creados en esta guía de inicio rápido en Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="8b99d-143">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="8b99d-144">En el menú de la izquierda de Azure Portal, haga clic en **Grupos de recursos** y en el nombre del recurso que creó.</span><span class="sxs-lookup"><span data-stu-id="8b99d-144">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="8b99d-145">En la página del grupo de recursos, haga clic en **Eliminar**, escriba en el cuadro de texto el nombre del recurso que quiere eliminar y haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="8b99d-145">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b99d-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8b99d-146">Next steps</span></span>

<span data-ttu-id="8b99d-147">En esta guía de inicio rápido, ha aprendido a crear una cuenta de Azure Cosmos DB y ejecutar una aplicación web con la API para MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8b99d-147">In this quickstart, you've learned how to create an Azure Cosmos DB account and run a web app using the API for MongoDB.</span></span> <span data-ttu-id="8b99d-148">Ahora puede importar datos adicionales en la cuenta de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b99d-148">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="8b99d-149">Importar datos en Azure Cosmos DB para la API MongoDB</span><span class="sxs-lookup"><span data-stu-id="8b99d-149">Import data into Azure Cosmos DB for the MongoDB API</span></span>](mongodb-migrate.md)

