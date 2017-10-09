---
title: "Hola a aaaBuild una aplicación .NET de base de datos de Azure Cosmos con API Graph | Documentos de Microsoft"
description: "Presenta un ejemplo de código de .NET puede usar tooconnect tooand consultar la base de datos de Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/28/2017
ms.author: denlee
ms.openlocfilehash: f28790fcb8c9f57c7bb3d844d8276fa04abcc39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-graph-api"></a><span data-ttu-id="b5ff8-103">Azure Cosmos DB: Crear una aplicación de .NET mediante Hola API Graph</span><span class="sxs-lookup"><span data-stu-id="b5ff8-103">Azure Cosmos DB: Build a .NET application using hello Graph API</span></span>

<span data-ttu-id="b5ff8-104">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="b5ff8-105">Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="b5ff8-106">Este inicio rápido muestra cómo toocreate una cuenta de base de datos de Azure Cosmos, la base de datos y el gráfico (contenedor) utilizando Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, database, and graph (container) using hello Azure portal.</span></span> <span data-ttu-id="b5ff8-107">A continuación, compilar y ejecutar una aplicación de consola compilada en hello [API Graph](graph-sdk-dotnet.md) (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="b5ff8-107">You then build and run a console app built on hello [Graph API](graph-sdk-dotnet.md) (preview).</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="b5ff8-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b5ff8-108">Prerequisites</span></span>

<span data-ttu-id="b5ff8-109">Si aún no tiene Visual Studio de 2017 instalado, puede descargar y usar hello **libre** [2017 Community Edition de Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="b5ff8-109">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="b5ff8-110">Asegúrese de que habilitar **desarrollo Azure** durante la instalación de Visual Studio Hola.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-110">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="b5ff8-111">Creación de una cuenta de base de datos</span><span class="sxs-lookup"><span data-stu-id="b5ff8-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="b5ff8-112">Agregar un grafo</span><span class="sxs-lookup"><span data-stu-id="b5ff8-112">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="b5ff8-113">Clonar aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="b5ff8-113">Clone hello sample application</span></span>

<span data-ttu-id="b5ff8-114">Ahora vamos a clonar una API de Graph aplicación de github, establezca la cadena de conexión de Hola y ejecútelo.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-114">Now let's clone a Graph API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="b5ff8-115">Podrá ver lo fácil que es toowork con datos mediante programación.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-115">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="b5ff8-116">Abra una ventana de terminal de git, como git bash, y `cd` tooa directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-116">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="b5ff8-117">Ejecute hello después de repositorio de ejemplo de comando tooclone Hola.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-117">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-dotnet-getting-started.git
    ```

3. <span data-ttu-id="b5ff8-118">A continuación, abra Visual Studio y el archivo de solución de hello abierto.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-118">Then open Visual Studio and open hello solution file.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="b5ff8-119">Revise el código de hello</span><span class="sxs-lookup"><span data-stu-id="b5ff8-119">Review hello code</span></span>

<span data-ttu-id="b5ff8-120">Vamos a hacer una revisión rápida de lo que sucede en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-120">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="b5ff8-121">Archivo de hello abra Program.cs y encontrará que estas líneas de código crean Hola recursos de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-121">Open hello Program.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="b5ff8-122">Hola DocumentClient se inicializa.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-122">hello DocumentClient is initialized.</span></span> <span data-ttu-id="b5ff8-123">En la vista previa de hello, agregamos una extensión de graph API de cliente de base de datos de Azure Cosmos Hola.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-123">In hello preview, we added a graph extension API on hello Azure Cosmos DB client.</span></span> <span data-ttu-id="b5ff8-124">Estamos trabajando en un cliente de graph independiente desacoplado de recursos y el cliente de base de datos de Azure Cosmos Hola.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-124">We are working on a standalone graph client decoupled from hello Azure Cosmos DB client and resources.</span></span>

    ```csharp
    using (DocumentClient client = new DocumentClient(
        new Uri(endpoint),
        authKey,
        new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp }))
    ```

* <span data-ttu-id="b5ff8-125">Se crea una base de datos.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-125">A new database is created.</span></span>

    ```csharp
    Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" });
    ```

* <span data-ttu-id="b5ff8-126">Se crea un grafo.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-126">A new graph is created.</span></span>

    ```csharp
    DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync(
        UriFactory.CreateDatabaseUri("graphdb"),
        new DocumentCollection { Id = "graph" },
        new RequestOptions { OfferThroughput = 1000 });
    ```
* <span data-ttu-id="b5ff8-127">Una serie de pasos de Gremlin se ejecutan utilizando hello `CreateGremlinQuery` método.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-127">A series of Gremlin steps are executed using hello `CreateGremlinQuery` method.</span></span>

    ```csharp
    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, "g.V().count()");
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="b5ff8-128">Actualizar la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="b5ff8-128">Update your connection string</span></span>

<span data-ttu-id="b5ff8-129">Ahora vuelva atrás toohello tooget portal Azure la información de la cadena de conexión y se copia en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-129">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="b5ff8-130">En Visual Studio de 2017, abra el archivo App.config de hello.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-130">In Visual Studio 2017, open hello App.config file.</span></span> 

2. <span data-ttu-id="b5ff8-131">Hola portal de Azure, en la cuenta de base de datos de Azure Cosmos, haga clic en **claves** Hola barra de navegación izquierda.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-131">In hello Azure portal, in your Azure Cosmos DB account, click **Keys** in hello left navigation.</span></span> 

    ![Ver y copiar una clave principal en el portal de Azure, en la página de claves de Hola Hola](./media/create-graph-dotnet/keys.png)

3. <span data-ttu-id="b5ff8-133">Copia la **URI** valor desde el portal de Hola y hacerla Hola valor de clave de punto de conexión de hello en el archivo App.config. Puede usar Hola copia botón tal como se muestra en hello anterior captura de pantalla toocopy valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-133">Copy your **URI** value from hello portal and make it hello value of hello Endpoint key in App.config. You can use hello copy button as shown in hello preceding screenshot toocopy hello value.</span></span>

    `<add key="Endpoint" value="https://FILLME.documents.azure.com:443" />`

4. <span data-ttu-id="b5ff8-134">Copia la **PRIMARY KEY** valor desde el portal de Hola y hacerla Hola valor de clave de SFF hello en el archivo App.config, a continuación, guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-134">Copy your **PRIMARY KEY** value from hello portal, and make it hello value of hello AuthKey key in App.config, then save your changes.</span></span> 

    `<add key="AuthKey" value="FILLME" />`

<span data-ttu-id="b5ff8-135">Ahora ha actualizado la aplicación con toda la información de hello debe toocommunicate con base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-135">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="run-hello-console-app"></a><span data-ttu-id="b5ff8-136">Ejecutar la aplicación de consola de hello</span><span class="sxs-lookup"><span data-stu-id="b5ff8-136">Run hello console app</span></span>

1. <span data-ttu-id="b5ff8-137">En Visual Studio, haga doble clic en hello **GraphGetStarted** proyecto **el Explorador de soluciones** y, a continuación, haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-137">In Visual Studio, right-click on hello **GraphGetStarted** project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="b5ff8-138">Hola NuGet **examinar** , escriba *Microsoft.Azure.Graphs* y comprobar hello **incluye versión preliminar** cuadro.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-138">In hello NuGet **Browse** box, type *Microsoft.Azure.Graphs* and check hello **Includes prerelease** box.</span></span> 

3. <span data-ttu-id="b5ff8-139">Desde los resultados de hello, instalar hello **Microsoft.Azure.Graphs** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-139">From hello results, install hello **Microsoft.Azure.Graphs** library.</span></span> <span data-ttu-id="b5ff8-140">Esto instala el paquete de biblioteca de extensión de gráfico de base de datos de Azure Cosmos de Hola y todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-140">This installs hello Azure Cosmos DB graph extension library package and all dependencies.</span></span>

    <span data-ttu-id="b5ff8-141">Si recibe un mensaje acerca de la revisión de la solución de toohello de cambios, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-141">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="b5ff8-142">Si recibe un mensaje acerca de la aceptación de licencia, haga clic en **Acepto**.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-142">If you get a message about license acceptance, click **I accept**.</span></span>

4. <span data-ttu-id="b5ff8-143">Haga clic en CTRL + F5 aplicación hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-143">Click CTRL + F5 toorun hello application.</span></span>

   <span data-ttu-id="b5ff8-144">ventana de la consola de Hello muestra vértices hello y bordes añadidos toohello gráfico.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-144">hello console window displays hello vertexes and edges being added toohello graph.</span></span> <span data-ttu-id="b5ff8-145">Cuando finalice la secuencia de comandos de hello, presione ENTRAR dos veces tooclose Hola ventana de la consola.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-145">When hello script completes, press ENTER twice tooclose hello console window.</span></span> 

## <a name="browse-using-hello-data-explorer"></a><span data-ttu-id="b5ff8-146">Examinar con hello Explorador de datos</span><span class="sxs-lookup"><span data-stu-id="b5ff8-146">Browse using hello Data Explorer</span></span>

<span data-ttu-id="b5ff8-147">Ahora puede volver atrás tooData Explorer Hola portal de Azure y examinar y consultar los datos de gráfico nuevo.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-147">You can now go back tooData Explorer in hello Azure portal and browse and query your new graph data.</span></span>

1. <span data-ttu-id="b5ff8-148">En el Explorador de datos, base de datos nueva Hola aparece en panel de gráficos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-148">In Data Explorer, hello new database appears in hello Graphs pane.</span></span> <span data-ttu-id="b5ff8-149">Expanda **graphdb**, **graphcollz** y, después, haga clic en **Grafo**.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-149">Expand **graphdb**, **graphcollz**, and then click **Graph**.</span></span>

2. <span data-ttu-id="b5ff8-150">Haga clic en hello **aplicar filtro** botón predeterminado de hello toouse consultar tooview todos los verticies de hello en el gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-150">Click hello **Apply Filter** button toouse hello default query tooview all hello verticies in hello graph.</span></span> <span data-ttu-id="b5ff8-151">datos de Hello generados por la aplicación de ejemplo de Hola se muestran en el panel de gráficos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-151">hello data generated by hello sample app is displayed in hello Graphs pane.</span></span>

    <span data-ttu-id="b5ff8-152">Puede acercar la vista dentro y fuera del gráfico de hello, puede ampliar el espacio de presentación de gráfico de hello, agregar verticies adicionales y mover la superficie de presentación de verticies en Hola.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-152">You can zoom in and out of hello graph, you can expand hello graph display space, add additional verticies, and move verticies on hello display surface.</span></span>

    ![Ver el gráfico de hello en el Explorador de datos en hello portal de Azure](./media/create-graph-dotnet/graph-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="b5ff8-154">Revise los SLA de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b5ff8-154">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="b5ff8-155">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="b5ff8-155">Clean up resources</span></span>

<span data-ttu-id="b5ff8-156">Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial rápido de hello portal de Azure con hello pasos:</span><span class="sxs-lookup"><span data-stu-id="b5ff8-156">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="b5ff8-157">En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-157">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="b5ff8-158">En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-158">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5ff8-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b5ff8-159">Next steps</span></span>

<span data-ttu-id="b5ff8-160">En este tutorial, ha aprendido cómo crear un gráfico utilizando Hola Explorador de datos toocreate una cuenta de base de datos de Azure Cosmos y ejecutar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-160">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a graph using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="b5ff8-161">Ahora puede crear consultas más complejas e implementar con Gremlin una lógica eficaz de recorrido del grafo.</span><span class="sxs-lookup"><span data-stu-id="b5ff8-161">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="b5ff8-162">Consulta mediante Gremlin</span><span class="sxs-lookup"><span data-stu-id="b5ff8-162">Query using Gremlin</span></span>](tutorial-query-graph.md)

