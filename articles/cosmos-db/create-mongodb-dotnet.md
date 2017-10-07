---
title: "Azure Cosmos DB: Compilar una aplicación web con .NET y Hola MongoDB API | Documentos de Microsoft"
description: "Presenta un ejemplo de código de .NET puede usar tooconnect tooand consulta hello Azure Cosmos DB MongoDB API"
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
ms.openlocfilehash: c85cc47f772a19aaa7181611b75a8acaedbc4c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-hello-azure-portal"></a><span data-ttu-id="d4525-103">Azure Cosmos DB: Compilar una aplicación web de API de MongoDB con .NET y Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="d4525-103">Azure Cosmos DB: Build a MongoDB API web app with .NET and hello Azure portal</span></span>

<span data-ttu-id="d4525-104">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d4525-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="d4525-105">Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente.</span><span class="sxs-lookup"><span data-stu-id="d4525-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="d4525-106">Este inicio rápido muestra cómo toocreate una cuenta de base de datos de Azure Cosmos, la base de datos de documento y la colección mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4525-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="d4525-107">A continuación, podrá compilar e implementar una aplicación de web de lista de tareas integrada en hello [controlador MongoDB .NET](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span><span class="sxs-lookup"><span data-stu-id="d4525-107">You'll then build and deploy a tasks list web app built on hello [MongoDB .NET driver](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d4525-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d4525-108">Prerequisites</span></span>

<span data-ttu-id="d4525-109">Si aún no tiene Visual Studio de 2017 instalado, puede descargar y usar hello **libre** [2017 Community Edition de Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d4525-109">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="d4525-110">Asegúrese de que habilitar **desarrollo Azure** durante la instalación de Visual Studio Hola.</span><span class="sxs-lookup"><span data-stu-id="d4525-110">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="d4525-111">Creación de una cuenta de base de datos</span><span class="sxs-lookup"><span data-stu-id="d4525-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="d4525-112">Clonar aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="d4525-112">Clone hello sample application</span></span>

<span data-ttu-id="d4525-113">Ahora vamos a clonar una API de MongoDB aplicación de github, establezca la cadena de conexión de Hola y ejecútelo.</span><span class="sxs-lookup"><span data-stu-id="d4525-113">Now let's clone a MongoDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="d4525-114">Podrá ver lo fácil que es toowork con datos mediante programación.</span><span class="sxs-lookup"><span data-stu-id="d4525-114">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="d4525-115">Abra una ventana de terminal de git, como git bash, y `cd` tooa directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="d4525-115">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="d4525-116">Ejecute hello después de repositorio de ejemplo de comando tooclone Hola.</span><span class="sxs-lookup"><span data-stu-id="d4525-116">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. <span data-ttu-id="d4525-117">A continuación, abra el archivo de solución de hello en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d4525-117">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="d4525-118">Revise el código de hello</span><span class="sxs-lookup"><span data-stu-id="d4525-118">Review hello code</span></span>

<span data-ttu-id="d4525-119">Vamos a hacer una revisión rápida de lo que sucede en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d4525-119">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="d4525-120">Abra hello **Dal.cs** archivo bajo hello **DAL** directorio y encontrará que estas líneas de código crean Hola recursos de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d4525-120">Open hello **Dal.cs** file under hello **DAL** directory and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="d4525-121">Inicializar hello Mongo cliente.</span><span class="sxs-lookup"><span data-stu-id="d4525-121">Initialize hello Mongo Client.</span></span>

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

* <span data-ttu-id="d4525-122">Recuperar la base de datos de Hola y colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4525-122">Retrieve hello database and hello collection.</span></span>

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* <span data-ttu-id="d4525-123">Recupere todos los documentos.</span><span class="sxs-lookup"><span data-stu-id="d4525-123">Retrieve all documents.</span></span>

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="d4525-124">Actualizar la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="d4525-124">Update your connection string</span></span>

<span data-ttu-id="d4525-125">Ahora vuelva atrás toohello tooget portal Azure la información de la cadena de conexión y se copia en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d4525-125">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="d4525-126">Hola [portal de Azure](http://portal.azure.com/), en la base de datos de Azure Cosmos account, Hola barra de navegación izquierda, haga clic en **cadena de conexión**y, a continuación, haga clic en **claves de lectura y escritura**.</span><span class="sxs-lookup"><span data-stu-id="d4525-126">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Connection String**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="d4525-127">Deberá usar botones de copia de hello en hello derecha de Hola Hola de toocopy pantalla nombre de usuario, la contraseña y el Host en el archivo Dal.cs de hello en el paso siguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4525-127">You'll use hello copy buttons on hello right side of hello screen toocopy hello Username, Password, and Host into hello Dal.cs file in hello next step.</span></span>

2. <span data-ttu-id="d4525-128">Abra hello **Dal.cs** archivo Hola **DAL** directory.</span><span class="sxs-lookup"><span data-stu-id="d4525-128">Open hello **Dal.cs** file in hello **DAL** directory.</span></span> 

3. <span data-ttu-id="d4525-129">Copia la **nombre de usuario** valor desde portal hello (mediante el botón Copiar de hello) y hacerla Hola valo hello **nombre de usuario** en su **Dal.cs** archivo.</span><span class="sxs-lookup"><span data-stu-id="d4525-129">Copy your **username** value from hello portal (using hello copy button) and make it hello value of hello **username** in your **Dal.cs** file.</span></span> 

4. <span data-ttu-id="d4525-130">A continuación, copie su **host** valor desde el portal de Hola y hacerla Hola valo hello **host** en su **Dal.cs** archivo.</span><span class="sxs-lookup"><span data-stu-id="d4525-130">Then copy your **host** value from hello portal and make it hello value of hello **host** in your **Dal.cs** file.</span></span> 

5. <span data-ttu-id="d4525-131">Por último, copie su **contraseña** valor desde el portal de Hola y hacerla Hola valo hello **contraseña** en su **Dal.cs** archivo.</span><span class="sxs-lookup"><span data-stu-id="d4525-131">Finally copy your **password** value from hello portal and make it hello value of hello **password** in your **Dal.cs** file.</span></span> 

<span data-ttu-id="d4525-132">Ahora ha actualizado la aplicación con toda la información de hello debe toocommunicate con base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d4525-132">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-web-app"></a><span data-ttu-id="d4525-133">Ejecutar la aplicación web de hello</span><span class="sxs-lookup"><span data-stu-id="d4525-133">Run hello web app</span></span>

1. <span data-ttu-id="d4525-134">En Visual Studio, haga doble clic en el proyecto de hello en **el Explorador de soluciones** y, a continuación, haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d4525-134">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="d4525-135">Hola NuGet **examinar** , escriba *MongoDB.Driver*.</span><span class="sxs-lookup"><span data-stu-id="d4525-135">In hello NuGet **Browse** box, type *MongoDB.Driver*.</span></span>

3. <span data-ttu-id="d4525-136">Desde los resultados de hello, instalar hello **MongoDB.Driver** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="d4525-136">From hello results, install hello **MongoDB.Driver** library.</span></span> <span data-ttu-id="d4525-137">Esto instala el paquete de MongoDB.Driver de hello, así como todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="d4525-137">This installs hello MongoDB.Driver package as well as all dependencies.</span></span>

4. <span data-ttu-id="d4525-138">Haga clic en CTRL + F5 aplicación hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="d4525-138">Click CTRL + F5 toorun hello application.</span></span> <span data-ttu-id="d4525-139">La aplicación se muestra en el explorador.</span><span class="sxs-lookup"><span data-stu-id="d4525-139">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="d4525-140">Haga clic en **crear** Hola explorador y crear unas nuevas tareas en la aplicación de la lista de tareas.</span><span class="sxs-lookup"><span data-stu-id="d4525-140">Click **Create** in hello browser and create a few new tasks in your task list app.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="d4525-141">Revise los SLA de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="d4525-141">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="d4525-142">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="d4525-142">Clean up resources</span></span>

<span data-ttu-id="d4525-143">Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial rápido de hello portal de Azure con hello pasos:</span><span class="sxs-lookup"><span data-stu-id="d4525-143">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="d4525-144">En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="d4525-144">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="d4525-145">En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="d4525-145">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4525-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d4525-146">Next steps</span></span>

<span data-ttu-id="d4525-147">En este tutorial, ha aprendido cómo toocreate una cuenta de base de datos de Azure Cosmos y ejecutar una aplicación web con Hola API para MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d4525-147">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and run a web app using hello API for MongoDB.</span></span> <span data-ttu-id="d4525-148">Ahora puede importar la cuenta de base de datos de Cosmos tooyour datos adicionales.</span><span class="sxs-lookup"><span data-stu-id="d4525-148">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="d4525-149">Importar datos en la base de datos de Azure Cosmos para hello API de MongoDB</span><span class="sxs-lookup"><span data-stu-id="d4525-149">Import data into Azure Cosmos DB for hello MongoDB API</span></span>](mongodb-migrate.md)

