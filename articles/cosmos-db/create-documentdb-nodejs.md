---
title: "Azure Cosmos DB: Compilar una aplicación con Node.js y la API DocumentDB | Microsoft Docs"
description: "En este tema se presenta un ejemplo de código de Node.js que se puede usar para conectarse a la API DocumentDB de Azure Cosmos DB y realizar consultas."
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
ms.openlocfilehash: 26e3548bf6aacbc60c4c46a5cc88749ca14cec01
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-the-azure-portal"></a><span data-ttu-id="06c99-103">Azure Cosmos DB: Compilar una aplicación de API DocumentDB con Node.js y Azure Portal</span><span class="sxs-lookup"><span data-stu-id="06c99-103">Azure Cosmos DB: Build a DocumentDB API app with Node.js and the Azure portal</span></span>

<span data-ttu-id="06c99-104">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="06c99-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="06c99-105">Puede crear rápidamente bases de datos de documentos, clave-valor y grafos, y realizar consultas en ellas. Todas las bases de datos se beneficiarán de las funcionalidades de distribución global y escalado horizontal en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="06c99-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="06c99-106">En esta guía de inicio rápido se muestra cómo crear una cuenta, una base de datos de documentos y una colección de Azure Cosmos DB mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="06c99-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="06c99-107">Después, compilará y ejecutará una aplicación de consola compilada en la [API DocumentDB de Node.js](documentdb-sdk-node.md).</span><span class="sxs-lookup"><span data-stu-id="06c99-107">You then build and run a console app built on the [DocumentDB Node.js API](documentdb-sdk-node.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06c99-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="06c99-108">Prerequisites</span></span>

* <span data-ttu-id="06c99-109">Antes de ejecutar este ejemplo, debe cumplir los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="06c99-109">Before you can run this sample, you must have the following prerequisites:</span></span>
    * <span data-ttu-id="06c99-110">[Node.js](https://nodejs.org/en/) versión v0.10.29 o superior</span><span class="sxs-lookup"><span data-stu-id="06c99-110">[Node.js](https://nodejs.org/en/) version v0.10.29 or higher</span></span>
    * [<span data-ttu-id="06c99-111">Git</span><span class="sxs-lookup"><span data-stu-id="06c99-111">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="06c99-112">Creación de una cuenta de base de datos</span><span class="sxs-lookup"><span data-stu-id="06c99-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="06c99-113">Incorporación de una colección</span><span class="sxs-lookup"><span data-stu-id="06c99-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="06c99-114">Clonación de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="06c99-114">Clone the sample application</span></span>

<span data-ttu-id="06c99-115">Ahora vamos a clonar una aplicación de API DocumentDB desde GitHub, establecer la cadena de conexión y ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="06c99-115">Now let's clone a DocumentDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="06c99-116">Verá lo fácil que es trabajar con datos mediante programación.</span><span class="sxs-lookup"><span data-stu-id="06c99-116">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="06c99-117">Abra una ventana de terminal de Git, como Git Bash, y `CD` en un directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="06c99-117">Open a git terminal window, such as git bash, and `CD` to a working directory.</span></span>  

2. <span data-ttu-id="06c99-118">Ejecute el comando siguiente para clonar el repositorio de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="06c99-118">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-the-code"></a><span data-ttu-id="06c99-119">Revisar el código</span><span class="sxs-lookup"><span data-stu-id="06c99-119">Review the code</span></span>

<span data-ttu-id="06c99-120">Vamos a revisar rápidamente lo que sucede en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="06c99-120">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="06c99-121">Abra el archivo `app.js` y observe que estas líneas de código crean los recursos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="06c99-121">Open the `app.js` file and you find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="06c99-122">Se inicializa `documentClient`.</span><span class="sxs-lookup"><span data-stu-id="06c99-122">The `documentClient` is initialized.</span></span>

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* <span data-ttu-id="06c99-123">Se crea una base de datos.</span><span class="sxs-lookup"><span data-stu-id="06c99-123">A new database is created.</span></span>

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="06c99-124">Se crea una colección.</span><span class="sxs-lookup"><span data-stu-id="06c99-124">A new collection is created.</span></span>

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="06c99-125">Se crean algunos documentos.</span><span class="sxs-lookup"><span data-stu-id="06c99-125">Some documents are created.</span></span>

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="06c99-126">Se realiza una consulta SQL en JSON.</span><span class="sxs-lookup"><span data-stu-id="06c99-126">A SQL query over JSON is performed.</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="06c99-127">Actualizar la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="06c99-127">Update your connection string</span></span>

<span data-ttu-id="06c99-128">Ahora vuelva a Azure Portal para obtener la información de la cadena de conexión y cópiela en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="06c99-128">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="06c99-129">En [Azure Portal](http://portal.azure.com/), en la cuenta de Azure Cosmos DB, en el panel de navegación izquierdo, haga clic en **Claves** y en **Claves de lectura y escritura**.</span><span class="sxs-lookup"><span data-stu-id="06c99-129">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="06c99-130">Deberá usar los botones de copia del lado derecho de la pantalla para copiar el URI y la clave principal en el archivo `config.js` en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="06c99-130">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the `config.js` file in the next step.</span></span>

    ![Visualización y copia de una clave de acceso en Azure Portal, hoja Claves](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="06c99-132">Abra el archivo `config.js`.</span><span class="sxs-lookup"><span data-stu-id="06c99-132">In Open the `config.js` file.</span></span> 

3. <span data-ttu-id="06c99-133">Copie el valor del URI del portal (con el botón de copia) y conviértalo en el valor de la clave de punto de conexión en `config.js`.</span><span class="sxs-lookup"><span data-stu-id="06c99-133">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in `config.js`.</span></span> 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="06c99-134">Después, copie el valor de la clave principal del portal y conviértalo en el valor de `config.primaryKey` en `config.js`.</span><span class="sxs-lookup"><span data-stu-id="06c99-134">Then copy your PRIMARY KEY value from the portal and make it the value of the `config.primaryKey` in `config.js`.</span></span> <span data-ttu-id="06c99-135">Ya ha actualizado la aplicación con toda la información que necesita para comunicarse con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="06c99-135">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

    `config.primaryKey "FILLME"`
    
## <a name="run-the-app"></a><span data-ttu-id="06c99-136">Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="06c99-136">Run the app</span></span>
1. <span data-ttu-id="06c99-137">Ejecute `npm install` en un terminal para instalar los módulos de NPM necesarios.</span><span class="sxs-lookup"><span data-stu-id="06c99-137">Run `npm install` in a terminal to install required npm modules</span></span>

2. <span data-ttu-id="06c99-138">Ejecute `node app.js` en un terminal para iniciar la aplicación de nodo.</span><span class="sxs-lookup"><span data-stu-id="06c99-138">Run `node app.js` in a terminal to start your node application.</span></span>

<span data-ttu-id="06c99-139">Ahora puede volver al Explorador de datos y ver, consultar, modificar y trabajar con estos nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="06c99-139">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="06c99-140">Revisión de los SLA en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="06c99-140">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="06c99-141">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="06c99-141">Clean up resources</span></span>

<span data-ttu-id="06c99-142">Si no va a seguir usando esta aplicación, siga estos pasos para eliminar todos los recursos creados en esta guía de inicio rápido en Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="06c99-142">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="06c99-143">En el menú de la izquierda de Azure Portal, haga clic en **Grupos de recursos** y en el nombre del recurso que creó.</span><span class="sxs-lookup"><span data-stu-id="06c99-143">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="06c99-144">En la página del grupo de recursos, haga clic en **Eliminar**, escriba en el cuadro de texto el nombre del recurso que quiere eliminar y haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="06c99-144">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06c99-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="06c99-145">Next steps</span></span>

<span data-ttu-id="06c99-146">En esta guía de inicio rápido, ha aprendido a crear una cuenta de Azure Cosmos DB, crear una colección mediante el Explorador de datos y ejecutar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="06c99-146">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run an app.</span></span> <span data-ttu-id="06c99-147">Ahora puede importar datos adicionales en la cuenta de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="06c99-147">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="06c99-148">Importación de datos a Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="06c99-148">Import data into Azure Cosmos DB</span></span>](import-data.md)


