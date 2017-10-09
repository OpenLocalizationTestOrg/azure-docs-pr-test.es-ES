---
title: "Azure Cosmos DB: Compilar una aplicación web con .NET y Hola API de documentos | Documentos de Microsoft"
description: "Presenta un ejemplo de código de .NET puede usar tooconnect tooand consulta Hola API de documentos de base de datos de Azure Cosmos"
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
ms.openlocfilehash: 35517e35d80c48662a51a99814652ffa1121fc5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-hello-azure-portal"></a><span data-ttu-id="95d5b-103">Azure Cosmos DB: Compilar una aplicación web de API de documentos con .NET y Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="95d5b-103">Azure Cosmos DB: Build a DocumentDB API web app with .NET and hello Azure portal</span></span>

<span data-ttu-id="95d5b-104">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="95d5b-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="95d5b-105">Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente.</span><span class="sxs-lookup"><span data-stu-id="95d5b-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="95d5b-106">Este inicio rápido muestra cómo toocreate una cuenta de base de datos de Azure Cosmos, la base de datos de documento y la colección mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="95d5b-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="95d5b-107">A continuación, podrá compilar e implementar una aplicación de web de lista de tareas integrada en hello [API de .NET de DocumentDB](documentdb-sdk-dotnet.md), tal y como se muestra en la siguiente captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="95d5b-107">You'll then build and deploy a todo list web app built on hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), as shown in hello following screenshot.</span></span> 

![Aplicación de tareas pendientes con datos de ejemplo](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a><span data-ttu-id="95d5b-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="95d5b-109">Prerequisites</span></span>

<span data-ttu-id="95d5b-110">Si aún no tiene Visual Studio de 2017 instalado, puede descargar y usar hello **libre** [2017 Community Edition de Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="95d5b-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="95d5b-111">Asegúrese de que habilitar **desarrollo Azure** durante la instalación de Visual Studio Hola.</span><span class="sxs-lookup"><span data-stu-id="95d5b-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="95d5b-112">Creación de una cuenta de base de datos</span><span class="sxs-lookup"><span data-stu-id="95d5b-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
## <a name="add-a-collection"></a><span data-ttu-id="95d5b-113">Agregar una colección</span><span class="sxs-lookup"><span data-stu-id="95d5b-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="95d5b-114">Agregar datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="95d5b-114">Add sample data</span></span>

<span data-ttu-id="95d5b-115">Ahora puede agregar datos tooyour nueva colección mediante el Explorador de datos.</span><span class="sxs-lookup"><span data-stu-id="95d5b-115">You can now add data tooyour new collection using Data Explorer.</span></span>

1. <span data-ttu-id="95d5b-116">En el Explorador de datos, base de datos nueva Hola aparece en panel de colecciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="95d5b-116">In Data Explorer, hello new database appears in hello Collections pane.</span></span> <span data-ttu-id="95d5b-117">Expanda hello **tareas** la base de datos, expanda hello **elementos** colección, haga clic en **documentos**y, a continuación, haga clic en **nuevos documentos**.</span><span class="sxs-lookup"><span data-stu-id="95d5b-117">Expand hello **Tasks** database, expand hello **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Crear nuevos documentos en el Explorador de datos en hello portal de Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="95d5b-119">Ahora puede agregar una colección de toohello de documento con hello siguiendo la estructura.</span><span class="sxs-lookup"><span data-stu-id="95d5b-119">Now add a document toohello collection with hello following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="95d5b-120">Una vez que haya agregado Hola json toohello **documentos** , haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="95d5b-120">Once you've added hello json toohello **Documents** tab, click **Save**.</span></span>

    ![Copiar datos de json y haga clic en Guardar en el Explorador de datos en hello portal de Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="95d5b-122">Crear y guardar un documento más donde insertar un valor único para hello `id` propiedad y cambio Hola otras propiedades como considere oportuno.</span><span class="sxs-lookup"><span data-stu-id="95d5b-122">Create and save one more document where you insert a unique value for hello `id` property, and change hello other properties as you see fit.</span></span> <span data-ttu-id="95d5b-123">Los nuevos documentos pueden tener la estructura que quiera, ya que Azure Cosmos DB no impone ningún esquema en los datos.</span><span class="sxs-lookup"><span data-stu-id="95d5b-123">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="95d5b-124">Ahora puede usar consultas en el Explorador de datos tooretrieve los datos.</span><span class="sxs-lookup"><span data-stu-id="95d5b-124">You can now use queries in Data Explorer tooretrieve your data.</span></span> <span data-ttu-id="95d5b-125">De forma predeterminada, usa el Explorador de datos `SELECT * FROM c` tooretrieve todos los documentos en la colección de hello, pero puede cambiar ese tooa diferentes [consulta SQL](documentdb-sql-query.md), como `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn todos los documentos de hello en orden descendente en función de su marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="95d5b-125">By default, Data Explorer uses `SELECT * FROM c` tooretrieve all documents in hello collection, but you can change that tooa different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn all hello documents in descending order based on their timestamp.</span></span>
 
     <span data-ttu-id="95d5b-126">También puede usar procedimientos de explorador de datos toocreate almacenado, UDF y lógica de negocios de servidor de tooperform de desencadenadores, así como el rendimiento de escala.</span><span class="sxs-lookup"><span data-stu-id="95d5b-126">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="95d5b-127">Explorador de datos expone todo acceso a los datos de mediante programación integrada Hola disponible en las API de hello, pero proporciona un acceso sencillo tooyour datos Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="95d5b-127">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="95d5b-128">Clonar aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="95d5b-128">Clone hello sample application</span></span>

<span data-ttu-id="95d5b-129">Ahora vamos a cambiar tooworking con el código.</span><span class="sxs-lookup"><span data-stu-id="95d5b-129">Now let's switch tooworking with code.</span></span> <span data-ttu-id="95d5b-130">Vamos a clonar una aplicación de API de documentos de GitHub, establezca la cadena de conexión de Hola y ejecútelo.</span><span class="sxs-lookup"><span data-stu-id="95d5b-130">Let's clone a DocumentDB API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="95d5b-131">Podrá ver lo fácil que es toowork con datos mediante programación.</span><span class="sxs-lookup"><span data-stu-id="95d5b-131">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="95d5b-132">Abra una ventana de terminal de git, como git bash, y `CD` tooa directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="95d5b-132">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="95d5b-133">Ejecute hello después de repositorio de ejemplo de comando tooclone Hola.</span><span class="sxs-lookup"><span data-stu-id="95d5b-133">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. <span data-ttu-id="95d5b-134">A continuación, abra el archivo de solución de hello tareas en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="95d5b-134">Then open hello todo solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="95d5b-135">Revise el código de hello</span><span class="sxs-lookup"><span data-stu-id="95d5b-135">Review hello code</span></span>

<span data-ttu-id="95d5b-136">Vamos a hacer una revisión rápida de lo que sucede en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="95d5b-136">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="95d5b-137">Archivo de DocumentDBRepository.cs de hello abierto y encontrará que estas líneas de código crean Hola recursos de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="95d5b-137">Open hello DocumentDBRepository.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="95d5b-138">Hola DocumentClient se inicializa en línea 73.</span><span class="sxs-lookup"><span data-stu-id="95d5b-138">hello DocumentClient is initialized on line 73.</span></span>

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* <span data-ttu-id="95d5b-139">Se crea una nueva base de datos en la línea 88.</span><span class="sxs-lookup"><span data-stu-id="95d5b-139">A new database is created on line 88.</span></span>

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* <span data-ttu-id="95d5b-140">Se crea una nueva colección en la línea 107.</span><span class="sxs-lookup"><span data-stu-id="95d5b-140">A new collection is created on line 107.</span></span>

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="95d5b-141">Actualizar la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="95d5b-141">Update your connection string</span></span>

<span data-ttu-id="95d5b-142">Ahora vuelva atrás toohello tooget portal Azure la información de la cadena de conexión y se copia en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="95d5b-142">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="95d5b-143">Hola [portal de Azure](http://portal.azure.com/), en la base de datos de Azure Cosmos account, Hola barra de navegación izquierda, haga clic en **claves**y, a continuación, haga clic en **claves de lectura y escritura**.</span><span class="sxs-lookup"><span data-stu-id="95d5b-143">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="95d5b-144">Deberá usar botones de copia de hello en hello derecha de hello toocopy de pantalla Hola URI y la clave principal en el archivo web.config de hello en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="95d5b-144">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello web.config file in hello next step.</span></span>

    ![Ver y copiar una clave de acceso en hello portal de Azure, hoja de claves](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="95d5b-146">En Visual Studio de 2017, abra el archivo web.config de hello.</span><span class="sxs-lookup"><span data-stu-id="95d5b-146">In Visual Studio 2017, open hello web.config file.</span></span> 

3. <span data-ttu-id="95d5b-147">Copie el valor URI de portal hello (mediante el botón Copiar de Hola) y hacerla Hola valor de clave de punto de conexión de hello en el archivo web.config.</span><span class="sxs-lookup"><span data-stu-id="95d5b-147">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in web.config.</span></span> 

    `<add key="endpoint" value="FILLME" />`

4. <span data-ttu-id="95d5b-148">A continuación, copie el valor de clave principal del portal de Hola y hacerla Hola valo SFF hello en el archivo web.config. Ahora ha actualizado la aplicación con toda la información de hello debe toocommunicate con base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="95d5b-148">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello authKey in web.config. You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-hello-web-app"></a><span data-ttu-id="95d5b-149">Ejecutar la aplicación web de hello</span><span class="sxs-lookup"><span data-stu-id="95d5b-149">Run hello web app</span></span>
1. <span data-ttu-id="95d5b-150">En Visual Studio, haga doble clic en el proyecto de hello en **el Explorador de soluciones** y, a continuación, haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="95d5b-150">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="95d5b-151">Hola NuGet **examinar** , escriba *DocumentDB*.</span><span class="sxs-lookup"><span data-stu-id="95d5b-151">In hello NuGet **Browse** box, type *DocumentDB*.</span></span>

3. <span data-ttu-id="95d5b-152">Desde los resultados de hello, instalar hello **Microsoft.Azure.DocumentDB** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="95d5b-152">From hello results, install hello **Microsoft.Azure.DocumentDB** library.</span></span> <span data-ttu-id="95d5b-153">Esto instala el paquete de Microsoft.Azure.DocumentDB de hello, así como todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="95d5b-153">This installs hello Microsoft.Azure.DocumentDB package as well as all dependencies.</span></span>

4. <span data-ttu-id="95d5b-154">Haga clic en CTRL + F5 aplicación hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="95d5b-154">Click CTRL + F5 toorun hello application.</span></span> <span data-ttu-id="95d5b-155">La aplicación se muestra en el explorador.</span><span class="sxs-lookup"><span data-stu-id="95d5b-155">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="95d5b-156">Haga clic en **crear nuevo** Hola explorador y crear unas cuantas tareas nuevas en la aplicación de tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="95d5b-156">Click **Create New** in hello browser and create a few new tasks in your to-do app.</span></span>

   ![Aplicación de tareas pendientes con datos de ejemplo](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

<span data-ttu-id="95d5b-158">Ahora puede volver atrás tooData explorador y vea la consulta, modificar y trabajar con nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="95d5b-158">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="95d5b-159">Revise los SLA de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="95d5b-159">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="95d5b-160">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="95d5b-160">Clean up resources</span></span>

<span data-ttu-id="95d5b-161">Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial rápido de hello portal de Azure con hello pasos:</span><span class="sxs-lookup"><span data-stu-id="95d5b-161">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="95d5b-162">En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="95d5b-162">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="95d5b-163">En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="95d5b-163">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95d5b-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="95d5b-164">Next steps</span></span>

<span data-ttu-id="95d5b-165">En este tutorial, ha aprendido cómo crear una colección mediante Hola Explorador de datos toocreate una cuenta de base de datos de Azure Cosmos y ejecutar una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="95d5b-165">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run a web app.</span></span> <span data-ttu-id="95d5b-166">Ahora puede importar la cuenta de base de datos de Cosmos tooyour datos adicionales.</span><span class="sxs-lookup"><span data-stu-id="95d5b-166">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="95d5b-167">Importación de datos a Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="95d5b-167">Import data into Azure Cosmos DB</span></span>](import-data.md)


