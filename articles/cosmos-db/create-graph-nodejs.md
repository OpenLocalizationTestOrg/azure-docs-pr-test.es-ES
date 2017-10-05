---
title: "Compilación de una aplicación de Node.js de Azure Cosmos DB mediante API Graph | Microsoft Docs"
description: "En este tema se presenta un ejemplo de código Node.js que puede usar para conectarse a Azure Cosmos DB y realizar consultas."
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
ms.date: 07/14/2017
ms.author: denlee
ms.openlocfilehash: 6d14719938af0ce825955389824441e111024869
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-build-a-nodejs-application-by-using-graph-api"></a><span data-ttu-id="46d40-103">Azure Cosmos DB: compilación de una aplicación de Node.js mediante API Graph</span><span class="sxs-lookup"><span data-stu-id="46d40-103">Azure Cosmos DB: Build a Node.js application by using Graph API</span></span>

<span data-ttu-id="46d40-104">Azure Cosmos DB es el servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="46d40-104">Azure Cosmos DB is the globally distributed multi-model database service from Microsoft.</span></span> <span data-ttu-id="46d40-105">Puede crear rápidamente bases de datos de documentos, clave-valor y grafos y realizar consultas en ellas. Todas las bases de datos se beneficiarán de las funcionalidades de distribución global y escala horizontal en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="46d40-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="46d40-106">En este artículo de inicio rápido se muestra cómo crear un grafo, una base de datos y una cuenta de Azure Cosmos DB para API Graph (versión preliminar) mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="46d40-106">This quick-start article demonstrates how to create an Azure Cosmos DB account for Graph API (preview), database, and graph by using the Azure portal.</span></span> <span data-ttu-id="46d40-107">Después, compilará y ejecutará una aplicación de consola con el controlador [Node.js de Gremlin](https://www.npmjs.com/package/gremlin-secure) de código abierto.</span><span class="sxs-lookup"><span data-stu-id="46d40-107">You then build and run a console app by using the open-source [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) driver.</span></span>  

> [!NOTE]
> <span data-ttu-id="46d40-108">El módulo npm `gremlin-secure` es una versión modificada del módulo `gremlin`, compatible con los protocolos SSL y SASL que son necesarios para conectar con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="46d40-108">The npm module `gremlin-secure` is a modified version of `gremlin` module, with support for SSL and SASL required for connecting with Azure Cosmos DB.</span></span> <span data-ttu-id="46d40-109">El código fuente está disponible en [GitHub](https://github.com/CosmosDB/gremlin-javascript).</span><span class="sxs-lookup"><span data-stu-id="46d40-109">Source code is available on [GitHub](https://github.com/CosmosDB/gremlin-javascript).</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="46d40-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="46d40-110">Prerequisites</span></span>

<span data-ttu-id="46d40-111">Antes de ejecutar este ejemplo, debe cumplir los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="46d40-111">Before you can run this sample, you must have the following prerequisites:</span></span>
* <span data-ttu-id="46d40-112">[Node.js](https://nodejs.org/en/) versión v0.10.29 o posterior</span><span class="sxs-lookup"><span data-stu-id="46d40-112">[Node.js](https://nodejs.org/en/) version v0.10.29 or later</span></span>
* [<span data-ttu-id="46d40-113">Git</span><span class="sxs-lookup"><span data-stu-id="46d40-113">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="46d40-114">Creación de una cuenta de base de datos</span><span class="sxs-lookup"><span data-stu-id="46d40-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="46d40-115">Agregar un grafo</span><span class="sxs-lookup"><span data-stu-id="46d40-115">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="46d40-116">Clonación de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="46d40-116">Clone the sample application</span></span>

<span data-ttu-id="46d40-117">Ahora, vamos a clonar una aplicación de API Graph desde GitHub, establecer la cadena de conexión y ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="46d40-117">Now let's clone a Graph API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="46d40-118">Verá lo fácil que es trabajar con datos mediante programación.</span><span class="sxs-lookup"><span data-stu-id="46d40-118">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="46d40-119">Abra una ventana de terminal de Git, como Git Bash, y cambie a un directorio de trabajo (mediante el comando `cd`).</span><span class="sxs-lookup"><span data-stu-id="46d40-119">Open a Git terminal window, such as Git Bash, and change (via `cd` command) to a working directory.</span></span>  

2. <span data-ttu-id="46d40-120">Ejecute el comando siguiente para clonar el repositorio de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="46d40-120">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-nodejs-getting-started.git
    ```

3. <span data-ttu-id="46d40-121">Abra el archivo de solución en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="46d40-121">Open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="46d40-122">Revisar el código</span><span class="sxs-lookup"><span data-stu-id="46d40-122">Review the code</span></span>

<span data-ttu-id="46d40-123">Vamos a revisar rápidamente lo que sucede en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="46d40-123">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="46d40-124">Abra el archivo `app.js` y encontrará las líneas de código siguientes.</span><span class="sxs-lookup"><span data-stu-id="46d40-124">Open the `app.js` file, and you'll find the following lines of code.</span></span> 

* <span data-ttu-id="46d40-125">Se crea el cliente Gremlin.</span><span class="sxs-lookup"><span data-stu-id="46d40-125">The Gremlin client is created.</span></span>

    ```nodejs
    const client = Gremlin.createClient(
        443, 
        config.endpoint, 
        { 
            "session": false, 
            "ssl": true, 
            "user": `/dbs/${config.database}/colls/${config.collection}`,
            "password": config.primaryKey
        });
    ```

  <span data-ttu-id="46d40-126">Las configuraciones están todas en `config.js`, que podemos editar en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="46d40-126">The configurations are all in `config.js`, which we edit in the following section.</span></span>

* <span data-ttu-id="46d40-127">Se ejecuta una serie de pasos de Gremlin con el método `client.execute`.</span><span class="sxs-lookup"><span data-stu-id="46d40-127">A series of Gremlin steps are executed with the `client.execute` method.</span></span>

    ```nodejs
    console.log('Running Count'); 
    client.execute("g.V().count()", { }, (err, results) => {
        if (err) return console.error(err);
        console.log(JSON.stringify(results));
        console.log();
    });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="46d40-128">Actualización de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="46d40-128">Update your connection string</span></span>

1. <span data-ttu-id="46d40-129">Abra el archivo config.js.</span><span class="sxs-lookup"><span data-stu-id="46d40-129">Open the config.js file.</span></span> 

2. <span data-ttu-id="46d40-130">En config.js, rellene la clave config.endpoint con el valor del **Identificador URI de Gremlin** de la página **Información general** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="46d40-130">In config.js, fill in the config.endpoint key with the **Gremlin URI** value from the **Overview** page of the Azure portal.</span></span> 

    `config.endpoint = "GRAPHENDPOINT";`

    ![Visualización y copia de una clave de acceso en Azure Portal, hoja Claves](./media/create-graph-nodejs/gremlin-uri.png)

   <span data-ttu-id="46d40-132">Si el valor de **Identificador URI de Gremlin** está en blanco, puede generar el valor desde la página **Claves** en el portal; para ello, use el valor de **URI**, elimine https:// y cambie documents por graphs.</span><span class="sxs-lookup"><span data-stu-id="46d40-132">If the **Gremlin URI** value is blank, you can generate the value from the **Keys** page in the portal, using the **URI** value, removing https://, and changing documents to graphs.</span></span>

   <span data-ttu-id="46d40-133">El punto de conexión de Gremlin debe ser solo el nombre de host sin el número de puerto y protocolo, como `mygraphdb.graphs.azure.com` (no como `https://mygraphdb.graphs.azure.com` ni `mygraphdb.graphs.azure.com:433`).</span><span class="sxs-lookup"><span data-stu-id="46d40-133">The Gremlin endpoint must be only the host name without the protocol/port number, like `mygraphdb.graphs.azure.com` (not `https://mygraphdb.graphs.azure.com` or `mygraphdb.graphs.azure.com:433`).</span></span>

3. <span data-ttu-id="46d40-134">En config.js, rellene el valor de config.primaryKey con el valor de la **Clave principal** de la página **Claves** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="46d40-134">In config.js, fill in the config.primaryKey value in with the **Primary Key** value from the **Keys** page of the Azure portal.</span></span> 

    `config.primaryKey = "PRIMARYKEY";`

   ![Hoja de claves de Azure Portal](./media/create-graph-nodejs/keys.png)

4. <span data-ttu-id="46d40-136">Escriba el nombre de la base de datos y el nombre del grafo (contenedor) para el valor de config.database y config.collection.</span><span class="sxs-lookup"><span data-stu-id="46d40-136">Enter the database name, and graph (container) name for the value of config.database and config.collection.</span></span> 

<span data-ttu-id="46d40-137">Este es un ejemplo del aspecto que debería tener el archivo config.js completado:</span><span class="sxs-lookup"><span data-stu-id="46d40-137">Here is an example of what your completed config.js file should look like:</span></span>

```nodejs
var config = {}

// Note that this must not have HTTPS or the port number
config.endpoint = "testgraphacct.graphs.azure.com";
config.primaryKey = "Pams6e7LEUS7LJ2Qk0fjZf3eGo65JdMWHmyn65i52w8ozPX2oxY3iP0yu05t9v1WymAHNcMwPIqNAEv3XDFsEg==";
config.database = "graphdb"
config.collection = "Persons"

module.exports = config;
```

## <a name="run-the-console-app"></a><span data-ttu-id="46d40-138">Ejecutar la aplicación de consola</span><span class="sxs-lookup"><span data-stu-id="46d40-138">Run the console app</span></span>

1. <span data-ttu-id="46d40-139">Abra una ventana del terminal y, con el comando `cd`, cambie al directorio de instalación del archivo package.json incluido en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="46d40-139">Open a terminal window and change (via `cd` command) to the installation directory for the package.json file that's included in the project.</span></span>  

2. <span data-ttu-id="46d40-140">Ejecute `npm install` para instalar los módulos npm necesarios, incluido `gremlin-secure`.</span><span class="sxs-lookup"><span data-stu-id="46d40-140">Run `npm install` to install the required npm modules, including `gremlin-secure`.</span></span>

3. <span data-ttu-id="46d40-141">Ejecute `node app.js` en un terminal para iniciar la aplicación de nodo.</span><span class="sxs-lookup"><span data-stu-id="46d40-141">Run `node app.js` in a terminal to start your node application.</span></span>

## <a name="browse-with-data-explorer"></a><span data-ttu-id="46d40-142">Examinar con el Explorador de datos</span><span class="sxs-lookup"><span data-stu-id="46d40-142">Browse with Data Explorer</span></span>

<span data-ttu-id="46d40-143">Ahora puede volver al Explorador de datos en Azure Portal para examinar, consultar, modificar y trabajar con los datos del nuevo grafo.</span><span class="sxs-lookup"><span data-stu-id="46d40-143">You can now go back to Data Explorer in the Azure portal to view, query, modify, and work with your new graph data.</span></span>

<span data-ttu-id="46d40-144">En el Explorador de datos, la nueva base de datos aparece en el panel **Grafos**.</span><span class="sxs-lookup"><span data-stu-id="46d40-144">In Data Explorer, the new database appears in the **Graphs** pane.</span></span> <span data-ttu-id="46d40-145">Expanda la base de datos, luego la colección y haga clic en **Grafo**.</span><span class="sxs-lookup"><span data-stu-id="46d40-145">Expand the database, followed by the collection, then click **Graph**.</span></span>

<span data-ttu-id="46d40-146">Los datos generados por la aplicación de ejemplo se muestran en el panel siguiente dentro de la pestaña **Grafo** al hacer clic en **Aplicar filtro**.</span><span class="sxs-lookup"><span data-stu-id="46d40-146">The data generated by the sample app is displayed in the next pane within the **Graph** tab when you click **Apply Filter**.</span></span>

<span data-ttu-id="46d40-147">Intente completar `g.V()` con `.has('firstName', 'Thomas')` para probar el filtro.</span><span class="sxs-lookup"><span data-stu-id="46d40-147">Try completing `g.V()` with `.has('firstName', 'Thomas')` to test the filter.</span></span> <span data-ttu-id="46d40-148">Tenga en cuenta que el valor distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="46d40-148">Do note that the value is case sensitive.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="46d40-149">Revisar los SLA en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="46d40-149">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-your-resources"></a><span data-ttu-id="46d40-150">Limpiar los recursos</span><span class="sxs-lookup"><span data-stu-id="46d40-150">Clean up your resources</span></span>

<span data-ttu-id="46d40-151">Si no piensa seguir usando la aplicación, haga lo siguiente para eliminar todos los recursos que ha creado en este artículo:</span><span class="sxs-lookup"><span data-stu-id="46d40-151">If you do not plan to continue using this app, delete all resources that you created in this article by doing the following:</span></span> 

1. <span data-ttu-id="46d40-152">En Azure Portal, en el menú de navegación de la izquierda, haga clic en **Grupos de recursos** y, después, en el nombre del recurso que creó.</span><span class="sxs-lookup"><span data-stu-id="46d40-152">In the Azure portal, on the left navigation menu, click **Resource groups**, and then click the name of the resource that you created.</span></span> 
2. <span data-ttu-id="46d40-153">En la página del grupo de recursos, haga clic en **Eliminar**, escriba el nombre del recurso que quiere eliminar y haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="46d40-153">On your resource group page, click **Delete**, type the name of the resource to be deleted, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46d40-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="46d40-154">Next steps</span></span>

<span data-ttu-id="46d40-155">En este artículo, ha obtenido información sobre cómo crear una cuenta de Azure Cosmos DB, crear un grafo mediante el Explorador de datos y ejecutar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="46d40-155">In this article, you've learned how to create an Azure Cosmos DB account, create a graph by using Data Explorer, and run an app.</span></span> <span data-ttu-id="46d40-156">Ahora puede usar Gremlin para implementar una lógica de recorrido del grafo eficaz y crear consultas más complejas.</span><span class="sxs-lookup"><span data-stu-id="46d40-156">You can now build more complex queries and implement powerful graph traversal logic by using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="46d40-157">Consulta mediante Gremlin</span><span class="sxs-lookup"><span data-stu-id="46d40-157">Query using Gremlin</span></span>](tutorial-query-graph.md)
