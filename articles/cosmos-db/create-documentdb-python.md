---
title: "Azure Cosmos DB: Compilar una aplicación con Python y Hola API de documentos | Documentos de Microsoft"
description: "Presenta un ejemplo de código de Python que puede usar tooconnect tooand consulta Hola API de documentos de base de datos de Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 51c11be2-af6d-425f-a86a-39cbfe61da29
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 05/13/2017
ms.author: mimig
ms.openlocfilehash: e66965ab493c6ef693e88a3767a401d39e1bde2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-hello-azure-portal"></a><span data-ttu-id="d591c-103">Azure Cosmos DB: Compilar una aplicación de API de documentos con Python y Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="d591c-103">Azure Cosmos DB: Build a DocumentDB API app with Python and hello Azure portal</span></span>

<span data-ttu-id="d591c-104">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d591c-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="d591c-105">Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente.</span><span class="sxs-lookup"><span data-stu-id="d591c-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="d591c-106">Este inicio rápido muestra cómo toocreate una cuenta de base de datos de Azure Cosmos, la base de datos de documento y la colección mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d591c-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="d591c-107">A continuación, compilar y ejecutar una aplicación de consola compilada en hello [documentos Python API](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="d591c-107">You then build and run a console app built on hello [DocumentDB Python API](documentdb-sdk-python.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d591c-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d591c-108">Prerequisites</span></span>

* <span data-ttu-id="d591c-109">Para poder ejecutar este ejemplo, debe tener Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="d591c-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
    * <span data-ttu-id="d591c-110">[Visual Studio 2015](http://www.visualstudio.com/) o posterior.</span><span class="sxs-lookup"><span data-stu-id="d591c-110">[Visual Studio 2015](http://www.visualstudio.com/) or higher.</span></span>
    * <span data-ttu-id="d591c-111">Herramientas de Python para Visual Studio desde [GitHub](http://microsoft.github.io/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="d591c-111">Python Tools for Visual Studio from [GitHub](http://microsoft.github.io/PTVS/).</span></span> <span data-ttu-id="d591c-112">En este tutorial se usan las herramientas de Python para VS 2015.</span><span class="sxs-lookup"><span data-stu-id="d591c-112">This tutorial uses Python Tools for VS 2015.</span></span>
    * <span data-ttu-id="d591c-113">Python 2.7 en [python.org](https://www.python.org/downloads/release/python-2712/)</span><span class="sxs-lookup"><span data-stu-id="d591c-113">Python 2.7 from [python.org](https://www.python.org/downloads/release/python-2712/)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="d591c-114">Creación de una cuenta de base de datos</span><span class="sxs-lookup"><span data-stu-id="d591c-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="d591c-115">Incorporación de una colección</span><span class="sxs-lookup"><span data-stu-id="d591c-115">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="d591c-116">Clonar aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="d591c-116">Clone hello sample application</span></span>

<span data-ttu-id="d591c-117">Ahora vamos a clonar una API de documentos de aplicación de github, establezca la cadena de conexión de Hola y ejecútelo.</span><span class="sxs-lookup"><span data-stu-id="d591c-117">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="d591c-118">Vea lo fácil que es toowork con datos mediante programación.</span><span class="sxs-lookup"><span data-stu-id="d591c-118">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="d591c-119">Abra una ventana de terminal de git, como git bash, y `cd` tooa directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="d591c-119">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="d591c-120">Ejecute hello después de repositorio de ejemplo de comando tooclone Hola.</span><span class="sxs-lookup"><span data-stu-id="d591c-120">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-hello-code"></a><span data-ttu-id="d591c-121">Revise el código de hello</span><span class="sxs-lookup"><span data-stu-id="d591c-121">Review hello code</span></span>

<span data-ttu-id="d591c-122">Vamos a hacer una revisión rápida de lo que sucede en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d591c-122">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="d591c-123">Archivo de DocumentDBGetStarted.py de hello abierto y encontrará que estas líneas de código crean Hola recursos de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d591c-123">Open hello DocumentDBGetStarted.py file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 


* <span data-ttu-id="d591c-124">Hola DocumentClient se inicializa.</span><span class="sxs-lookup"><span data-stu-id="d591c-124">hello DocumentClient is initialized.</span></span>

    ```python
    # Initialize hello Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* <span data-ttu-id="d591c-125">Se crea una base de datos.</span><span class="sxs-lookup"><span data-stu-id="d591c-125">A new database is created.</span></span>

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* <span data-ttu-id="d591c-126">Se crea una colección.</span><span class="sxs-lookup"><span data-stu-id="d591c-126">A new collection is created.</span></span>

    ```python
    # Create collection options
    options = {
        'offerEnableRUPerMinuteThroughput': True,
        'offerVersion': "V2",
        'offerThroughput': 400
    }

    # Create a collection
    collection = client.CreateCollection(db['_self'], { 'id': config['DOCUMENTDB_COLLECTION'] }, options)
    ```

* <span data-ttu-id="d591c-127">Se crean algunos documentos.</span><span class="sxs-lookup"><span data-stu-id="d591c-127">Some documents are created.</span></span>

    ```python
    # Create some documents
    document1 = client.CreateDocument(collection['_self'],
        { 
            'id': 'server1',
            'Web Site': 0,
            'Cloud Service': 0,
            'Virtual Machine': 0,
            'name': 'some' 
        })
    ```

* <span data-ttu-id="d591c-128">Se realiza una consulta con SQL.</span><span class="sxs-lookup"><span data-stu-id="d591c-128">A query is performed using SQL</span></span>

    ```python
    # Query them in SQL
    query = { 'query': 'SELECT * FROM server s' }    
            
    options = {} 
    options['enableCrossPartitionQuery'] = True
    options['maxItemCount'] = 2

    result_iterable = client.QueryDocuments(collection['_self'], query, options)
    results = list(result_iterable);

    print(results)
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="d591c-129">Actualizar la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="d591c-129">Update your connection string</span></span>

<span data-ttu-id="d591c-130">Ahora vuelva atrás toohello tooget portal Azure la información de la cadena de conexión y se copia en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d591c-130">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="d591c-131">Hola [portal de Azure](http://portal.azure.com/), en la base de datos de Azure Cosmos account, Hola barra de navegación izquierda, haga clic en **claves**y, a continuación, haga clic en **claves de lectura y escritura**.</span><span class="sxs-lookup"><span data-stu-id="d591c-131">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="d591c-132">Usará Hola copia botones en hello derecha de hello toocopy de pantalla Hola URI y la clave principal en hello `DocumentDBGetStarted.py` archivo en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="d591c-132">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello `DocumentDBGetStarted.py` file in hello next step.</span></span>

    ![Ver y copiar una clave de acceso en hello portal de Azure, hoja de claves](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="d591c-134">Abra Hola `DocumentDBGetStarted.py` archivo.</span><span class="sxs-lookup"><span data-stu-id="d591c-134">In Open hello `DocumentDBGetStarted.py` file.</span></span> 

3. <span data-ttu-id="d591c-135">Copie el valor URI de portal hello (mediante el botón Copiar de Hola) y hacerla Hola valor de clave de punto de conexión de hello en `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="d591c-135">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in `DocumentDBGetStarted.py`.</span></span> 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="d591c-136">A continuación, copie el valor de clave principal del portal de Hola y hacerla Hola valo hello `config.MASTERKEY` en `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="d591c-136">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello `config.MASTERKEY` in `DocumentDBGetStarted.py`.</span></span> <span data-ttu-id="d591c-137">Ahora ha actualizado la aplicación con toda la información de hello debe toocommunicate con base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d591c-137">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-hello-app"></a><span data-ttu-id="d591c-138">Ejecutar aplicación hello</span><span class="sxs-lookup"><span data-stu-id="d591c-138">Run hello app</span></span>
1. <span data-ttu-id="d591c-139">En Visual Studio, haga doble clic en el proyecto de hello en **el Explorador de soluciones**, seleccione el entorno actual de Python de Hola y luego haga clic en.</span><span class="sxs-lookup"><span data-stu-id="d591c-139">In Visual Studio, right-click on hello project in **Solution Explorer**, select hello current Python environment, then right click.</span></span>

2. <span data-ttu-id="d591c-140">Seleccione Instalar paquete de Python y, después, escriba **pydocumentdb**.</span><span class="sxs-lookup"><span data-stu-id="d591c-140">Select Install Python Package, then type in **pydocumentdb**</span></span>

3. <span data-ttu-id="d591c-141">Ejecute la aplicación de hello toorun F5.</span><span class="sxs-lookup"><span data-stu-id="d591c-141">Run F5 toorun hello application.</span></span> <span data-ttu-id="d591c-142">La aplicación se muestra en el explorador.</span><span class="sxs-lookup"><span data-stu-id="d591c-142">Your app displays in your browser.</span></span> 

<span data-ttu-id="d591c-143">Ahora puede volver atrás tooData explorador y vea la consulta, modificar y trabajar con nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="d591c-143">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="d591c-144">Revise los SLA de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="d591c-144">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="d591c-145">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="d591c-145">Clean up resources</span></span>

<span data-ttu-id="d591c-146">Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial rápido de hello portal de Azure con hello pasos:</span><span class="sxs-lookup"><span data-stu-id="d591c-146">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="d591c-147">En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="d591c-147">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="d591c-148">En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="d591c-148">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d591c-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d591c-149">Next steps</span></span>

<span data-ttu-id="d591c-150">En este tutorial, ha aprendido cómo crear una colección mediante Hola Explorador de datos toocreate una cuenta de base de datos de Azure Cosmos y ejecutar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="d591c-150">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="d591c-151">Ahora puede importar la cuenta de base de datos de Cosmos tooyour datos adicionales.</span><span class="sxs-lookup"><span data-stu-id="d591c-151">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="d591c-152">Importar datos en la base de datos de Azure Cosmos para hello API de documentos</span><span class="sxs-lookup"><span data-stu-id="d591c-152">Import data into Azure Cosmos DB for hello DocumentDB API</span></span>](import-data.md)


