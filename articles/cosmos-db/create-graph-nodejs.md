---
title: "aaaBuild una aplicación de Azure Cosmos DB Node.js mediante el uso de API Graph | Documentos de Microsoft"
description: "Presenta un ejemplo de código de Node.js puede usar tooconnect tooand consultar la base de datos de Azure Cosmos"
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
ms.openlocfilehash: 1445755842bc4e4a84ca2b2f789aadde8467e190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-nodejs-application-by-using-graph-api"></a><span data-ttu-id="38b35-103">Azure Cosmos DB: compilación de una aplicación de Node.js mediante API Graph</span><span class="sxs-lookup"><span data-stu-id="38b35-103">Azure Cosmos DB: Build a Node.js application by using Graph API</span></span>

<span data-ttu-id="38b35-104">Base de datos de Azure Cosmos es servicio de base de datos de varios modelos de hello globalmente distribuida de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="38b35-104">Azure Cosmos DB is hello globally distributed multi-model database service from Microsoft.</span></span> <span data-ttu-id="38b35-105">Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente.</span><span class="sxs-lookup"><span data-stu-id="38b35-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="38b35-106">Este artículo de inicio rápido muestra cómo toocreate una base de datos de Azure Cosmos cuenta para API Graph (versión preliminar), de gráfico y de base de datos a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="38b35-106">This quick-start article demonstrates how toocreate an Azure Cosmos DB account for Graph API (preview), database, and graph by using hello Azure portal.</span></span> <span data-ttu-id="38b35-107">A continuación, compilar y ejecutar una aplicación de consola mediante el uso de código abierto de hello [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) controlador.</span><span class="sxs-lookup"><span data-stu-id="38b35-107">You then build and run a console app by using hello open-source [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) driver.</span></span>  

> [!NOTE]
> <span data-ttu-id="38b35-108">módulo de npm Hello `gremlin-secure` es una versión modificada de `gremlin` módulo, compatible con SSL y SASL necesaria para conectar con base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="38b35-108">hello npm module `gremlin-secure` is a modified version of `gremlin` module, with support for SSL and SASL required for connecting with Azure Cosmos DB.</span></span> <span data-ttu-id="38b35-109">El código fuente está disponible en [GitHub](https://github.com/CosmosDB/gremlin-javascript).</span><span class="sxs-lookup"><span data-stu-id="38b35-109">Source code is available on [GitHub](https://github.com/CosmosDB/gremlin-javascript).</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="38b35-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="38b35-110">Prerequisites</span></span>

<span data-ttu-id="38b35-111">Para poder ejecutar este ejemplo, debe tener Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="38b35-111">Before you can run this sample, you must have hello following prerequisites:</span></span>
* <span data-ttu-id="38b35-112">[Node.js](https://nodejs.org/en/) versión v0.10.29 o posterior</span><span class="sxs-lookup"><span data-stu-id="38b35-112">[Node.js](https://nodejs.org/en/) version v0.10.29 or later</span></span>
* [<span data-ttu-id="38b35-113">Git</span><span class="sxs-lookup"><span data-stu-id="38b35-113">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="38b35-114">Creación de una cuenta de base de datos</span><span class="sxs-lookup"><span data-stu-id="38b35-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="38b35-115">Agregar un grafo</span><span class="sxs-lookup"><span data-stu-id="38b35-115">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="38b35-116">Clonar aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="38b35-116">Clone hello sample application</span></span>

<span data-ttu-id="38b35-117">Ahora vamos a clonar una API de Graph aplicación de GitHub, establezca la cadena de conexión de Hola y ejecútelo.</span><span class="sxs-lookup"><span data-stu-id="38b35-117">Now let's clone a Graph API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="38b35-118">Podrá ver lo fácil que es toowork con datos mediante programación.</span><span class="sxs-lookup"><span data-stu-id="38b35-118">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="38b35-119">Abra una ventana de terminal de Git, como Git Bash y cambie (a través de `cd` comando) tooa directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="38b35-119">Open a Git terminal window, such as Git Bash, and change (via `cd` command) tooa working directory.</span></span>  

2. <span data-ttu-id="38b35-120">Ejecute hello después de repositorio de ejemplo de comando tooclone Hola.</span><span class="sxs-lookup"><span data-stu-id="38b35-120">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-nodejs-getting-started.git
    ```

3. <span data-ttu-id="38b35-121">Abra el archivo de solución de hello en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="38b35-121">Open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="38b35-122">Revise el código de hello</span><span class="sxs-lookup"><span data-stu-id="38b35-122">Review hello code</span></span>

<span data-ttu-id="38b35-123">Vamos a hacer una revisión rápida de lo que sucede en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="38b35-123">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="38b35-124">Abra hello `app.js` archivo y encontrará Hola siguientes líneas de código.</span><span class="sxs-lookup"><span data-stu-id="38b35-124">Open hello `app.js` file, and you'll find hello following lines of code.</span></span> 

* <span data-ttu-id="38b35-125">se crea el cliente de Gremlin Hola.</span><span class="sxs-lookup"><span data-stu-id="38b35-125">hello Gremlin client is created.</span></span>

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

  <span data-ttu-id="38b35-126">Hello configuraciones están en `config.js`, lo que podemos editar Hola pasos de la sección.</span><span class="sxs-lookup"><span data-stu-id="38b35-126">hello configurations are all in `config.js`, which we edit in hello following section.</span></span>

* <span data-ttu-id="38b35-127">Una serie de pasos de Gremlin se ejecutan con hello `client.execute` método.</span><span class="sxs-lookup"><span data-stu-id="38b35-127">A series of Gremlin steps are executed with hello `client.execute` method.</span></span>

    ```nodejs
    console.log('Running Count'); 
    client.execute("g.V().count()", { }, (err, results) => {
        if (err) return console.error(err);
        console.log(JSON.stringify(results));
        console.log();
    });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="38b35-128">Actualizar la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="38b35-128">Update your connection string</span></span>

1. <span data-ttu-id="38b35-129">Archivo de config.js de hello abierto.</span><span class="sxs-lookup"><span data-stu-id="38b35-129">Open hello config.js file.</span></span> 

2. <span data-ttu-id="38b35-130">En config.js, rellene la clave de config.endpoint Hola con hello **Gremlin URI** valor de hello **información general sobre** página del programa Hola a portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="38b35-130">In config.js, fill in hello config.endpoint key with hello **Gremlin URI** value from hello **Overview** page of hello Azure portal.</span></span> 

    `config.endpoint = "GRAPHENDPOINT";`

    ![Ver y copiar una clave de acceso en hello portal de Azure, hoja de claves](./media/create-graph-nodejs/gremlin-uri.png)

   <span data-ttu-id="38b35-132">Si hello **Gremlin URI** valor está en blanco, puede generar el valor de Hola de hello **claves** página del portal de hello, con hello **URI** valor eliminación https:// y el cambio toographs de documentos.</span><span class="sxs-lookup"><span data-stu-id="38b35-132">If hello **Gremlin URI** value is blank, you can generate hello value from hello **Keys** page in hello portal, using hello **URI** value, removing https://, and changing documents toographs.</span></span>

   <span data-ttu-id="38b35-133">el punto de conexión de Hello Gremlin debe ser único nombre de host de hello sin número de puerto y protocolo de hello, como `mygraphdb.graphs.azure.com` (no `https://mygraphdb.graphs.azure.com` o `mygraphdb.graphs.azure.com:433`).</span><span class="sxs-lookup"><span data-stu-id="38b35-133">hello Gremlin endpoint must be only hello host name without hello protocol/port number, like `mygraphdb.graphs.azure.com` (not `https://mygraphdb.graphs.azure.com` or `mygraphdb.graphs.azure.com:433`).</span></span>

3. <span data-ttu-id="38b35-134">En config.js, rellene el valor de config.primaryKey Hola con hello **Primary Key** valor de hello **claves** página del programa Hola a portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="38b35-134">In config.js, fill in hello config.primaryKey value in with hello **Primary Key** value from hello **Keys** page of hello Azure portal.</span></span> 

    `config.primaryKey = "PRIMARYKEY";`

   ![Hola portal Azure, hoja de claves](./media/create-graph-nodejs/keys.png)

4. <span data-ttu-id="38b35-136">Escriba el nombre de la base de datos de Hola y el nombre del gráfico (contenedor) para el valor de Hola de config.database y config.collection.</span><span class="sxs-lookup"><span data-stu-id="38b35-136">Enter hello database name, and graph (container) name for hello value of config.database and config.collection.</span></span> 

<span data-ttu-id="38b35-137">Este es un ejemplo del aspecto que debería tener el archivo config.js completado:</span><span class="sxs-lookup"><span data-stu-id="38b35-137">Here is an example of what your completed config.js file should look like:</span></span>

```nodejs
var config = {}

// Note that this must not have HTTPS or hello port number
config.endpoint = "testgraphacct.graphs.azure.com";
config.primaryKey = "Pams6e7LEUS7LJ2Qk0fjZf3eGo65JdMWHmyn65i52w8ozPX2oxY3iP0yu05t9v1WymAHNcMwPIqNAEv3XDFsEg==";
config.database = "graphdb"
config.collection = "Persons"

module.exports = config;
```

## <a name="run-hello-console-app"></a><span data-ttu-id="38b35-138">Ejecutar la aplicación de consola de hello</span><span class="sxs-lookup"><span data-stu-id="38b35-138">Run hello console app</span></span>

1. <span data-ttu-id="38b35-139">Abra una ventana de terminal y cambie (a través de `cd` comando) directorio de instalación de toohello de archivo package.json hello que se incluye en el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="38b35-139">Open a terminal window and change (via `cd` command) toohello installation directory for hello package.json file that's included in hello project.</span></span>  

2. <span data-ttu-id="38b35-140">Ejecutar `npm install` tooinstall Hola necesario módulos npm, incluido `gremlin-secure`.</span><span class="sxs-lookup"><span data-stu-id="38b35-140">Run `npm install` tooinstall hello required npm modules, including `gremlin-secure`.</span></span>

3. <span data-ttu-id="38b35-141">Ejecutar `node app.js` en un terminal toostart la aplicación de nodo.</span><span class="sxs-lookup"><span data-stu-id="38b35-141">Run `node app.js` in a terminal toostart your node application.</span></span>

## <a name="browse-with-data-explorer"></a><span data-ttu-id="38b35-142">Examinar con el Explorador de datos</span><span class="sxs-lookup"><span data-stu-id="38b35-142">Browse with Data Explorer</span></span>

<span data-ttu-id="38b35-143">Ahora puede volver atrás tooData Explorer Hola tooview de portal de Azure, consultar, modificar y trabajar con los nuevos datos de gráfico.</span><span class="sxs-lookup"><span data-stu-id="38b35-143">You can now go back tooData Explorer in hello Azure portal tooview, query, modify, and work with your new graph data.</span></span>

<span data-ttu-id="38b35-144">En el Explorador de datos, base de datos nueva Hola aparece en hello **gráficos** panel.</span><span class="sxs-lookup"><span data-stu-id="38b35-144">In Data Explorer, hello new database appears in hello **Graphs** pane.</span></span> <span data-ttu-id="38b35-145">Expanda la base de datos de hello, seguido por la colección de hello, a continuación, haga clic en **gráfico**.</span><span class="sxs-lookup"><span data-stu-id="38b35-145">Expand hello database, followed by hello collection, then click **Graph**.</span></span>

<span data-ttu-id="38b35-146">datos de Hello generados por la aplicación de ejemplo de Hola se muestran en panel siguiente de hello en hello **gráfico** ficha al hacer clic en **aplicar filtro**.</span><span class="sxs-lookup"><span data-stu-id="38b35-146">hello data generated by hello sample app is displayed in hello next pane within hello **Graph** tab when you click **Apply Filter**.</span></span>

<span data-ttu-id="38b35-147">Intente completar `g.V()` con `.has('firstName', 'Thomas')` tootest filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="38b35-147">Try completing `g.V()` with `.has('firstName', 'Thomas')` tootest hello filter.</span></span> <span data-ttu-id="38b35-148">Tenga en cuenta que el valor de hello distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="38b35-148">Do note that hello value is case sensitive.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="38b35-149">Revise los SLA de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="38b35-149">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-your-resources"></a><span data-ttu-id="38b35-150">Limpiar los recursos</span><span class="sxs-lookup"><span data-stu-id="38b35-150">Clean up your resources</span></span>

<span data-ttu-id="38b35-151">Si no tiene previsto toocontinue usar esta aplicación, eliminar todos los recursos que ha creado en este artículo haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="38b35-151">If you do not plan toocontinue using this app, delete all resources that you created in this article by doing hello following:</span></span> 

1. <span data-ttu-id="38b35-152">Hola portal de Azure, en el menú de navegación izquierdo de hello, haga clic en **grupos de recursos**y, a continuación, haga clic en nombre de hello del recurso de Hola que ha creado.</span><span class="sxs-lookup"><span data-stu-id="38b35-152">In hello Azure portal, on hello left navigation menu, click **Resource groups**, and then click hello name of hello resource that you created.</span></span> 
2. <span data-ttu-id="38b35-153">En la página del grupo de recursos, haga clic en **eliminar**, escriba nombre Hola de hello recursos toobe eliminar y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="38b35-153">On your resource group page, click **Delete**, type hello name of hello resource toobe deleted, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38b35-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="38b35-154">Next steps</span></span>

<span data-ttu-id="38b35-155">En este artículo, ha aprendido cómo crear un gráfico mediante el Explorador de datos toocreate una cuenta de base de datos de Azure Cosmos y ejecutar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="38b35-155">In this article, you've learned how toocreate an Azure Cosmos DB account, create a graph by using Data Explorer, and run an app.</span></span> <span data-ttu-id="38b35-156">Ahora puede usar Gremlin para implementar una lógica de recorrido del grafo eficaz y crear consultas más complejas.</span><span class="sxs-lookup"><span data-stu-id="38b35-156">You can now build more complex queries and implement powerful graph traversal logic by using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="38b35-157">Consulta mediante Gremlin</span><span class="sxs-lookup"><span data-stu-id="38b35-157">Query using Gremlin</span></span>](tutorial-query-graph.md)
