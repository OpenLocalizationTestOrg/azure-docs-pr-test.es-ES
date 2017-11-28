---
title: "Azure Cosmos DB: Compilar una aplicación web con .NET y la API DocumentDB | Microsoft Docs"
description: "En este tema se presenta un ejemplo de código de .NET que se puede usar para conectarse a la API DocumentDB de Azure Cosmos DB y realizar consultas."
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
ms.openlocfilehash: 9bb863261da64c97f99757d4a0cb3474a7755591
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-the-azure-portal"></a><span data-ttu-id="a67e3-103">Azure Cosmos DB: Compilar una aplicación web de API DocumentDB con .NET y Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a67e3-103">Azure Cosmos DB: Build a DocumentDB API web app with .NET and the Azure portal</span></span>

<span data-ttu-id="a67e3-104">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a67e3-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="a67e3-105">Puede crear rápidamente bases de datos de documentos, clave-valor y grafos, y realizar consultas en ellas. Todas las bases de datos se beneficiarán de las funcionalidades de distribución global y escalado horizontal en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a67e3-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="a67e3-106">En esta guía de inicio rápido se muestra cómo crear una cuenta, una base de datos de documentos y una colección de Azure Cosmos DB mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a67e3-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="a67e3-107">Después, compilará e implementará una aplicación de web de lista de tareas pendientes integrada en la [API DocumentDB de .NET](documentdb-sdk-dotnet.md), tal como se muestra en la captura de pantalla siguiente.</span><span class="sxs-lookup"><span data-stu-id="a67e3-107">You'll then build and deploy a todo list web app built on the [DocumentDB .NET API](documentdb-sdk-dotnet.md), as shown in the following screenshot.</span></span> 

![Aplicación de tareas pendientes con datos de ejemplo](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a><span data-ttu-id="a67e3-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a67e3-109">Prerequisites</span></span>

<span data-ttu-id="a67e3-110">Si aún no tiene Visual Studio de 2017 instalado, puede descargar y usar la versión **gratis** de [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a67e3-110">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="a67e3-111">Asegúrese de que habilita **Desarrollo de Azure** durante la instalación de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a67e3-111">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="a67e3-112">Creación de una cuenta de base de datos</span><span class="sxs-lookup"><span data-stu-id="a67e3-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
## <a name="add-a-collection"></a><span data-ttu-id="a67e3-113">Agregar una colección</span><span class="sxs-lookup"><span data-stu-id="a67e3-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="a67e3-114">Agregar datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a67e3-114">Add sample data</span></span>

<span data-ttu-id="a67e3-115">Ahora puede agregar datos a la nueva colección mediante el Explorador de datos.</span><span class="sxs-lookup"><span data-stu-id="a67e3-115">You can now add data to your new collection using Data Explorer.</span></span>

1. <span data-ttu-id="a67e3-116">En el Explorador de datos, la nueva base de datos aparece en el panel Colecciones.</span><span class="sxs-lookup"><span data-stu-id="a67e3-116">In Data Explorer, the new database appears in the Collections pane.</span></span> <span data-ttu-id="a67e3-117">Expanda la base de datos **Tareas**, expanda la colección **Elementos**, haga clic en **Documentos** y, después, haga clic en **Nuevos documentos**.</span><span class="sxs-lookup"><span data-stu-id="a67e3-117">Expand the **Tasks** database, expand the **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Creación de documentos en el Explorador de datos en Azure Portal](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="a67e3-119">Ahora agregue un documento a la colección con la estructura siguiente.</span><span class="sxs-lookup"><span data-stu-id="a67e3-119">Now add a document to the collection with the following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="a67e3-120">Cuando haya agregado el archivo JSON a la pestaña **Documentos**, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a67e3-120">Once you've added the json to the **Documents** tab, click **Save**.</span></span>

    ![Copiar los datos JSON y hacer clic en Guardar en el Explorador de datos en Azure Portal](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="a67e3-122">Cree y guarde un documento más donde insertará un valor único para la propiedad `id` y cambie las demás propiedades como corresponda.</span><span class="sxs-lookup"><span data-stu-id="a67e3-122">Create and save one more document where you insert a unique value for the `id` property, and change the other properties as you see fit.</span></span> <span data-ttu-id="a67e3-123">Los nuevos documentos pueden tener la estructura que quiera, ya que Azure Cosmos DB no impone ningún esquema en los datos.</span><span class="sxs-lookup"><span data-stu-id="a67e3-123">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="a67e3-124">Ahora puede usar consultas en el Explorador de datos para recuperar los datos.</span><span class="sxs-lookup"><span data-stu-id="a67e3-124">You can now use queries in Data Explorer to retrieve your data.</span></span> <span data-ttu-id="a67e3-125">De forma predeterminada, el Explorador de datos usa `SELECT * FROM c` para recuperar todos los documentos de la colección, pero puede cambiarlo por una [consulta SQL](documentdb-sql-query.md) diferente, como `SELECT * FROM c ORDER BY c._ts DESC`, para devolver todos los documentos en orden descendente en función de su marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="a67e3-125">By default, Data Explorer uses `SELECT * FROM c` to retrieve all documents in the collection, but you can change that to a different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, to return all the documents in descending order based on their timestamp.</span></span>
 
     <span data-ttu-id="a67e3-126">También puede usar el Explorador de datos para crear procedimientos almacenados, UDF y desencadenadores para realizar la lógica de negocios del servidor, así como escalar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="a67e3-126">You can also use Data Explorer to create stored procedures, UDFs, and triggers to perform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="a67e3-127">El Explorador de datos expone todo el acceso a datos mediante programación integrado que está disponible en las API, pero permite un acceso fácil a los datos de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a67e3-127">Data Explorer exposes all of the built-in programmatic data access available in the APIs, but provides easy access to your data in the Azure portal.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="a67e3-128">Clonación de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a67e3-128">Clone the sample application</span></span>

<span data-ttu-id="a67e3-129">Ahora vamos a empezar a trabajar con el código.</span><span class="sxs-lookup"><span data-stu-id="a67e3-129">Now let's switch to working with code.</span></span> <span data-ttu-id="a67e3-130">Vamos a clonar una aplicación de API DocumentDB desde GitHub, a establecer la cadena de conexión y a ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="a67e3-130">Let's clone a DocumentDB API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="a67e3-131">Verá lo fácil que es trabajar con datos mediante programación.</span><span class="sxs-lookup"><span data-stu-id="a67e3-131">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="a67e3-132">Abra una ventana de terminal de Git, como Git Bash, y `CD` en un directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="a67e3-132">Open a git terminal window, such as git bash, and `CD` to a working directory.</span></span>  

2. <span data-ttu-id="a67e3-133">Ejecute el comando siguiente para clonar el repositorio de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a67e3-133">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. <span data-ttu-id="a67e3-134">Después, abra el archivo de solución de tareas pendientes en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a67e3-134">Then open the todo solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="a67e3-135">Revisión del código</span><span class="sxs-lookup"><span data-stu-id="a67e3-135">Review the code</span></span>

<span data-ttu-id="a67e3-136">Vamos a revisar rápidamente lo que sucede en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a67e3-136">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="a67e3-137">Abra el archivo DocumentDBRepository.cs y observe que estas líneas de código crean los recursos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a67e3-137">Open the DocumentDBRepository.cs file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="a67e3-138">DocumentClient se inicializa en la línea 73.</span><span class="sxs-lookup"><span data-stu-id="a67e3-138">The DocumentClient is initialized on line 73.</span></span>

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* <span data-ttu-id="a67e3-139">Se crea una nueva base de datos en la línea 88.</span><span class="sxs-lookup"><span data-stu-id="a67e3-139">A new database is created on line 88.</span></span>

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* <span data-ttu-id="a67e3-140">Se crea una nueva colección en la línea 107.</span><span class="sxs-lookup"><span data-stu-id="a67e3-140">A new collection is created on line 107.</span></span>

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="a67e3-141">Actualización de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="a67e3-141">Update your connection string</span></span>

<span data-ttu-id="a67e3-142">Ahora vuelva a Azure Portal para obtener la información de la cadena de conexión y cópiela en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a67e3-142">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="a67e3-143">En [Azure Portal](http://portal.azure.com/), en la cuenta de Azure Cosmos DB, en el panel de navegación izquierdo, haga clic en **Claves** y en **Claves de lectura y escritura**.</span><span class="sxs-lookup"><span data-stu-id="a67e3-143">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="a67e3-144">Deberá usar los botones de copia del lado derecho de la pantalla para copiar el URI y la clave principal en el archivo web.config en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="a67e3-144">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the web.config file in the next step.</span></span>

    ![Visualización y copia de una clave de acceso en Azure Portal, hoja Claves](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="a67e3-146">En Visual Studio 2017, abra el archivo web.config.</span><span class="sxs-lookup"><span data-stu-id="a67e3-146">In Visual Studio 2017, open the web.config file.</span></span> 

3. <span data-ttu-id="a67e3-147">Copie el valor del URI del portal (con el botón de copia) y conviértalo en el valor de la clave de punto de conexión en web.config.</span><span class="sxs-lookup"><span data-stu-id="a67e3-147">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in web.config.</span></span> 

    `<add key="endpoint" value="FILLME" />`

4. <span data-ttu-id="a67e3-148">Después, copie el valor de la clave principal del portal y conviértalo en el valor de la clave de autenticación en web.config. Ya ha actualizado la aplicación con toda la información que necesita para comunicarse con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a67e3-148">Then copy your PRIMARY KEY value from the portal and make it the value of the authKey in web.config. You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-the-web-app"></a><span data-ttu-id="a67e3-149">Ejecución de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="a67e3-149">Run the web app</span></span>
1. <span data-ttu-id="a67e3-150">En Visual Studio, haga clic con el botón derecho en el proyecto en el **Explorador de soluciones** y, después, haga clic en **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a67e3-150">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="a67e3-151">En el cuadro **Examinar** de NuGet, escriba *DocumentDB*.</span><span class="sxs-lookup"><span data-stu-id="a67e3-151">In the NuGet **Browse** box, type *DocumentDB*.</span></span>

3. <span data-ttu-id="a67e3-152">En los resultados, instale la biblioteca **Microsoft.Azure.DocumentDB**.</span><span class="sxs-lookup"><span data-stu-id="a67e3-152">From the results, install the **Microsoft.Azure.DocumentDB** library.</span></span> <span data-ttu-id="a67e3-153">De este modo, se instalan el paquete Microsoft.Azure.DocumentDB y todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="a67e3-153">This installs the Microsoft.Azure.DocumentDB package as well as all dependencies.</span></span>

4. <span data-ttu-id="a67e3-154">Presione Ctrl+F5 para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a67e3-154">Click CTRL + F5 to run the application.</span></span> <span data-ttu-id="a67e3-155">La aplicación se muestra en el explorador.</span><span class="sxs-lookup"><span data-stu-id="a67e3-155">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="a67e3-156">Haga clic en **Crear nuevo** en el explorador y cree algunas tareas en la aplicación de tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="a67e3-156">Click **Create New** in the browser and create a few new tasks in your to-do app.</span></span>

   ![Aplicación de tareas pendientes con datos de ejemplo](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

<span data-ttu-id="a67e3-158">Ahora puede volver al Explorador de datos y ver, consultar, modificar y trabajar con estos nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="a67e3-158">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="a67e3-159">Revisión de los SLA en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a67e3-159">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="a67e3-160">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="a67e3-160">Clean up resources</span></span>

<span data-ttu-id="a67e3-161">Si no va a seguir usando esta aplicación, siga estos pasos para eliminar todos los recursos creados en esta guía de inicio rápido en Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="a67e3-161">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="a67e3-162">En el menú de la izquierda de Azure Portal, haga clic en **Grupos de recursos** y en el nombre del recurso que creó.</span><span class="sxs-lookup"><span data-stu-id="a67e3-162">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="a67e3-163">En la página del grupo de recursos, haga clic en **Eliminar**, escriba en el cuadro de texto el nombre del recurso que quiere eliminar y haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="a67e3-163">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a67e3-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a67e3-164">Next steps</span></span>

<span data-ttu-id="a67e3-165">En esta guía de inicio rápido, ha aprendido a crear una cuenta de Azure Cosmos DB, crear una colección mediante el Explorador de datos y ejecutar una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="a67e3-165">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run a web app.</span></span> <span data-ttu-id="a67e3-166">Ahora puede importar datos adicionales en la cuenta de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a67e3-166">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="a67e3-167">Importación de datos a Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a67e3-167">Import data into Azure Cosmos DB</span></span>](import-data.md)


