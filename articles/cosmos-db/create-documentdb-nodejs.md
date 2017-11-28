---
title: "Azure Cosmos DB: Compilar una aplicación con Node.js y Hola API de documentos | Documentos de Microsoft"
description: "Presenta un ejemplo de código de Node.js puede usar tooconnect tooand consulta Hola API de documentos de base de datos de Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 9c0f033c-240e-4fee-8421-08907231087f
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 287d860c7d6f788f05a397b238ef0f841c3c30ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-hello-azure-portal"></a><span data-ttu-id="975f4-103">Azure Cosmos DB: Compilar una aplicación de API de documentos con Node.js y Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="975f4-103">Azure Cosmos DB: Build a DocumentDB API app with Node.js and hello Azure portal</span></span>

<span data-ttu-id="975f4-104">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="975f4-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="975f4-105">Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente.</span><span class="sxs-lookup"><span data-stu-id="975f4-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="975f4-106">Este inicio rápido muestra cómo toocreate una cuenta de base de datos de Azure Cosmos, la base de datos de documento y la colección mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="975f4-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="975f4-107">A continuación, compilar y ejecutar una aplicación de consola compilada en hello [DocumentDB Node.js API](documentdb-sdk-node.md).</span><span class="sxs-lookup"><span data-stu-id="975f4-107">You then build and run a console app built on hello [DocumentDB Node.js API](documentdb-sdk-node.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="975f4-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="975f4-108">Prerequisites</span></span>

* <span data-ttu-id="975f4-109">Para poder ejecutar este ejemplo, debe tener Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="975f4-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
    * <span data-ttu-id="975f4-110">[Node.js](https://nodejs.org/en/) versión v0.10.29 o superior</span><span class="sxs-lookup"><span data-stu-id="975f4-110">[Node.js](https://nodejs.org/en/) version v0.10.29 or higher</span></span>
    * [<span data-ttu-id="975f4-111">Git</span><span class="sxs-lookup"><span data-stu-id="975f4-111">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="975f4-112">Creación de una cuenta de base de datos</span><span class="sxs-lookup"><span data-stu-id="975f4-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="975f4-113">Incorporación de una colección</span><span class="sxs-lookup"><span data-stu-id="975f4-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="975f4-114">Clonar aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="975f4-114">Clone hello sample application</span></span>

<span data-ttu-id="975f4-115">Ahora vamos a clonar una API de documentos de aplicación de github, establezca la cadena de conexión de Hola y ejecútelo.</span><span class="sxs-lookup"><span data-stu-id="975f4-115">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="975f4-116">Vea lo fácil que es toowork con datos mediante programación.</span><span class="sxs-lookup"><span data-stu-id="975f4-116">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="975f4-117">Abra una ventana de terminal de git, como git bash, y `CD` tooa directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="975f4-117">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="975f4-118">Ejecute hello después de repositorio de ejemplo de comando tooclone Hola.</span><span class="sxs-lookup"><span data-stu-id="975f4-118">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="975f4-119">Revise el código de hello</span><span class="sxs-lookup"><span data-stu-id="975f4-119">Review hello code</span></span>

<span data-ttu-id="975f4-120">Vamos a hacer una revisión rápida de lo que sucede en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="975f4-120">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="975f4-121">Abra hello `app.js` archivo y descubre que estas líneas de código crean Hola recursos de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="975f4-121">Open hello `app.js` file and you find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="975f4-122">Hola `documentClient` se inicializa.</span><span class="sxs-lookup"><span data-stu-id="975f4-122">hello `documentClient` is initialized.</span></span>

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* <span data-ttu-id="975f4-123">Se crea una base de datos.</span><span class="sxs-lookup"><span data-stu-id="975f4-123">A new database is created.</span></span>

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="975f4-124">Se crea una colección.</span><span class="sxs-lookup"><span data-stu-id="975f4-124">A new collection is created.</span></span>

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="975f4-125">Se crean algunos documentos.</span><span class="sxs-lookup"><span data-stu-id="975f4-125">Some documents are created.</span></span>

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="975f4-126">Se realiza una consulta SQL en JSON.</span><span class="sxs-lookup"><span data-stu-id="975f4-126">A SQL query over JSON is performed.</span></span>

    ```nodejs
    client.queryDocuments(
        collectionUrl,
        'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
    ).toArray((err, results) => {
        if (err) reject(err)
        else {
            for (var queryResult of results) {
                let resultString = JSON.stringify(queryResult);
                console.log(`\tQuery returned ${resultString}`);
            }
            console.log();
            resolve(results);
        }
    });
    ```    

## <a name="update-your-connection-string"></a><span data-ttu-id="975f4-127">Actualizar la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="975f4-127">Update your connection string</span></span>

<span data-ttu-id="975f4-128">Ahora vuelva atrás toohello tooget portal Azure la información de la cadena de conexión y se copia en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="975f4-128">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="975f4-129">Hola [portal de Azure](http://portal.azure.com/), en la base de datos de Azure Cosmos account, Hola barra de navegación izquierda, haga clic en **claves**y, a continuación, haga clic en **claves de lectura y escritura**.</span><span class="sxs-lookup"><span data-stu-id="975f4-129">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="975f4-130">Usará Hola copia botones en hello derecha de hello toocopy de pantalla Hola URI y la clave principal en hello `config.js` archivo en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="975f4-130">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello `config.js` file in hello next step.</span></span>

    ![Ver y copiar una clave de acceso en hello portal de Azure, hoja de claves](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="975f4-132">Abra Hola `config.js` archivo.</span><span class="sxs-lookup"><span data-stu-id="975f4-132">In Open hello `config.js` file.</span></span> 

3. <span data-ttu-id="975f4-133">Copie el valor URI de portal hello (mediante el botón Copiar de Hola) y hacerla Hola valor de clave de punto de conexión de hello en `config.js`.</span><span class="sxs-lookup"><span data-stu-id="975f4-133">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in `config.js`.</span></span> 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="975f4-134">A continuación, copie el valor de clave principal del portal de Hola y hacerla Hola valo hello `config.primaryKey` en `config.js`.</span><span class="sxs-lookup"><span data-stu-id="975f4-134">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello `config.primaryKey` in `config.js`.</span></span> <span data-ttu-id="975f4-135">Ahora ha actualizado la aplicación con toda la información de hello debe toocommunicate con base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="975f4-135">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `config.primaryKey "FILLME"`
    
## <a name="run-hello-app"></a><span data-ttu-id="975f4-136">Ejecutar aplicación hello</span><span class="sxs-lookup"><span data-stu-id="975f4-136">Run hello app</span></span>
1. <span data-ttu-id="975f4-137">Ejecutar `npm install` en un terminal tooinstall necesario módulos npm</span><span class="sxs-lookup"><span data-stu-id="975f4-137">Run `npm install` in a terminal tooinstall required npm modules</span></span>

2. <span data-ttu-id="975f4-138">Ejecutar `node app.js` en un terminal toostart la aplicación de nodo.</span><span class="sxs-lookup"><span data-stu-id="975f4-138">Run `node app.js` in a terminal toostart your node application.</span></span>

<span data-ttu-id="975f4-139">Ahora puede volver atrás tooData explorador y vea la consulta, modificar y trabajar con nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="975f4-139">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="975f4-140">Revise los SLA de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="975f4-140">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="975f4-141">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="975f4-141">Clean up resources</span></span>

<span data-ttu-id="975f4-142">Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial rápido de hello portal de Azure con hello pasos:</span><span class="sxs-lookup"><span data-stu-id="975f4-142">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="975f4-143">En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="975f4-143">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="975f4-144">En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="975f4-144">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="975f4-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="975f4-145">Next steps</span></span>

<span data-ttu-id="975f4-146">En este tutorial, ha aprendido cómo crear una colección mediante Hola Explorador de datos toocreate una cuenta de base de datos de Azure Cosmos y ejecutar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="975f4-146">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="975f4-147">Ahora puede importar la cuenta de base de datos de Cosmos tooyour datos adicionales.</span><span class="sxs-lookup"><span data-stu-id="975f4-147">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="975f4-148">Importación de datos a Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="975f4-148">Import data into Azure Cosmos DB</span></span>](import-data.md)


