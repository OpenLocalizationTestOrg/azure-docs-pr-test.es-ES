---
title: 'Azure Cosmos DB: Desarrollar con hello API de documentos en .NET | Documentos de Microsoft'
description: "Obtenga información acerca de cómo toodevelop con la API de documentos de Azure Cosmos DB con .NET"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: 0d3d17afa782054c8fdf3cbac421e5a5d0a6800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmosdb-develop-with-hello-documentdb-api-in-net"></a><span data-ttu-id="c7e20-103">Azure CosmosDB: Desarrollar con hello API de documentos en .NET</span><span class="sxs-lookup"><span data-stu-id="c7e20-103">Azure CosmosDB: Develop with hello DocumentDB API in .NET</span></span>

<span data-ttu-id="c7e20-104">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c7e20-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="c7e20-105">Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente.</span><span class="sxs-lookup"><span data-stu-id="c7e20-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="c7e20-106">Este tutorial muestra cómo toocreate una cuenta de base de datos de Azure Cosmos mediante Hola portal de Azure y, a continuación, crear una base de datos de documento y una colección con un [clave de partición](documentdb-partition-data.md#partition-keys) con hello [API de .NET de DocumentDB](documentdb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c7e20-106">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal, and then create a document database and collection with a [partition key](documentdb-partition-data.md#partition-keys) using hello [DocumentDB .NET API](documentdb-introduction.md).</span></span> <span data-ttu-id="c7e20-107">Mediante la definición de una clave de partición cuando se crea una colección, la aplicación está preparada tooscale sin esfuerzo a medida que aumentan los datos.</span><span class="sxs-lookup"><span data-stu-id="c7e20-107">By defining a partition key when you create a collection, your application is prepared tooscale effortlessly as your data grows.</span></span> 

<span data-ttu-id="c7e20-108">Tareas de continuación Hola tutorial abarca mediante el uso de hello [API de .NET de DocumentDB](documentdb-sdk-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="c7e20-108">This tutorial covers hello following tasks by using hello [DocumentDB .NET API](documentdb-sdk-dotnet.md):</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c7e20-109">Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c7e20-109">Create an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="c7e20-110">Creación de una base de datos y colección con una clave de partición</span><span class="sxs-lookup"><span data-stu-id="c7e20-110">Create a database and collection with a partition key</span></span>
> * <span data-ttu-id="c7e20-111">Creación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="c7e20-111">Create JSON documents</span></span>
> * <span data-ttu-id="c7e20-112">Actualización de un documento</span><span class="sxs-lookup"><span data-stu-id="c7e20-112">Update a document</span></span>
> * <span data-ttu-id="c7e20-113">Consulta de colecciones con particiones</span><span class="sxs-lookup"><span data-stu-id="c7e20-113">Query partitioned collections</span></span>
> * <span data-ttu-id="c7e20-114">Ejecución de procedimientos almacenados</span><span class="sxs-lookup"><span data-stu-id="c7e20-114">Run stored procedures</span></span>
> * <span data-ttu-id="c7e20-115">Eliminar un documento</span><span class="sxs-lookup"><span data-stu-id="c7e20-115">Delete a document</span></span>
> * <span data-ttu-id="c7e20-116">Eliminación de una base de datos</span><span class="sxs-lookup"><span data-stu-id="c7e20-116">Delete a database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7e20-117">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c7e20-117">Prerequisites</span></span>
<span data-ttu-id="c7e20-118">Asegúrese de que tiene Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="c7e20-118">Please make sure you have hello following:</span></span>

* <span data-ttu-id="c7e20-119">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="c7e20-119">An active Azure account.</span></span> <span data-ttu-id="c7e20-120">Si no tiene una, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="c7e20-120">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="c7e20-121">Como alternativa, puede usar hello [emulador de base de datos de Azure Cosmos](local-emulator.md) para este tutorial si desea que toouse un entorno local que emula el servicio de Azure DocumentDB Hola para fines de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="c7e20-121">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial if you'd like toouse a local environment that emulates hello Azure DocumentDB service for development purposes.</span></span>
* <span data-ttu-id="c7e20-122">[Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="c7e20-122">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="c7e20-123">Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c7e20-123">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="c7e20-124">Empecemos creando una cuenta de base de datos de Azure Cosmos Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c7e20-124">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>

> [!TIP]
> * <span data-ttu-id="c7e20-125">¿Ya tiene una cuenta de Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="c7e20-125">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="c7e20-126">Si es así, pasar demasiado[configure su solución de Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="c7e20-126">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="c7e20-127">¿Ya tenía una cuenta de Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="c7e20-127">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="c7e20-128">En caso afirmativo, la cuenta es ahora una cuenta de base de datos de Azure Cosmos y puede saltarse lecciones demasiado[configure su solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="c7e20-128">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="c7e20-129">Si usas hello Azure Cosmos DB emulador, siga los pasos de hello en [emulador de base de datos de Azure Cosmos](local-emulator.md) toosetup Hola emulador y pase demasiado[configurar la solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="c7e20-129">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="c7e20-130"><a id="SetupVS"></a>Configuración de la solución de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c7e20-130"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="c7e20-131">Abra **Visual Studio** en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c7e20-131">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="c7e20-132">En hello **archivo** menú, seleccione **New**y, a continuación, elija **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="c7e20-132">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="c7e20-133">Hola **nuevo proyecto** cuadro de diálogo, seleccione **plantillas** / **Visual C#** / **aplicación de consola (.NET Framework)**, denomine el proyecto y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c7e20-133">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="c7e20-134">![Captura de pantalla de ventana nuevo proyecto de hello](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="c7e20-134">![Screen shot of hello New Project window](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span></span>

4. <span data-ttu-id="c7e20-135">Hola **el Explorador de soluciones**, haga clic con el botón secundario en la nueva aplicación de consola, que se encuentra en la solución de Visual Studio, y, a continuación, haga clic en **administrar paquetes de NuGet...**</span><span class="sxs-lookup"><span data-stu-id="c7e20-135">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Captura de pantalla de hello derecha menú Clicked Hola proyecto](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="c7e20-137">Hola **NuGet** , haga clic en **examinar**y el tipo de **documentdb** en el cuadro de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7e20-137">In hello **NuGet** tab, click **Browse**, and type **documentdb** in hello search box.</span></span>
<!---stopped here--->
6. <span data-ttu-id="c7e20-138">En los resultados de hello, buscar **Microsoft.Azure.DocumentDB** y haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="c7e20-138">Within hello results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="c7e20-139">Id. de paquete de Hola para hello biblioteca de cliente de base de datos de Azure Cosmos es [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="c7e20-139">hello package ID for hello Azure Cosmos DB Client Library is [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span></span>
   <span data-ttu-id="c7e20-140">![Captura de pantalla de hello NuGet menú para buscar el SDK de cliente de base de datos de Azure Cosmos](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="c7e20-140">![Screen shot of hello NuGet Menu for finding Azure Cosmos DB Client SDK](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="c7e20-141">Si recibe un mensaje acerca de la revisión de la solución de toohello de cambios, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c7e20-141">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="c7e20-142">Si recibe un mensaje acerca de la aceptación de licencia, haga clic en **Acepto**.</span><span class="sxs-lookup"><span data-stu-id="c7e20-142">If you get a message about license acceptance, click **I accept**.</span></span>

## <span data-ttu-id="c7e20-143"><a id="Connect"></a>Agregar referencias tooyour proyecto</span><span class="sxs-lookup"><span data-stu-id="c7e20-143"><a id="Connect"></a>Add references tooyour project</span></span>
<span data-ttu-id="c7e20-144">Hola restantes pasos de este tutorial proporcione Hola API de documentos código fragmentos de código toocreate y actualización de base de datos de Azure Cosmos recursos necesarios en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="c7e20-144">hello remaining steps in this tutorial provide hello DocumentDB API code snippets required toocreate and update Azure Cosmos DB resources in your project.</span></span>

<span data-ttu-id="c7e20-145">En primer lugar, agregue estas aplicaciones de tooyour de referencias.</span><span class="sxs-lookup"><span data-stu-id="c7e20-145">First, add these references tooyour application.</span></span>
<!---These aren't added by default when you install hello pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <span data-ttu-id="c7e20-146"><a id="add-references"></a>Conexión de la aplicación</span><span class="sxs-lookup"><span data-stu-id="c7e20-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="c7e20-147">A continuación, agregue estas dos constantes y la variable *client* en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c7e20-147">Next, add these two constants and your *client* variable in your application.</span></span>

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

<span data-ttu-id="c7e20-148">A continuación, hacer copia de head toohello [portal de Azure](https://portal.azure.com) tooretrieve la dirección URL del extremo y la clave principal.</span><span class="sxs-lookup"><span data-stu-id="c7e20-148">Then, head back toohello [Azure portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="c7e20-149">dirección URL del extremo de Hola y clave principal son necesarios para su aplicación toounderstand donde tooconnect y para la base de datos de Azure Cosmos tootrust conexión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c7e20-149">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="c7e20-150">Hola portal de Azure, navegar por la cuenta de base de datos de Azure Cosmos tooyour, haga clic en **claves**y, a continuación, haga clic en **claves de lectura y escritura**.</span><span class="sxs-lookup"><span data-stu-id="c7e20-150">In hello Azure portal, navigate tooyour Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span>

<span data-ttu-id="c7e20-151">Copie Hola URI desde el portal de Hola y péguela sobre `<your endpoint URL>` en el archivo program.cs de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7e20-151">Copy hello URI from hello portal and paste it over `<your endpoint URL>` in hello program.cs file.</span></span> <span data-ttu-id="c7e20-152">A continuación, copiar Hola clave principal del portal de Hola y péguela sobre `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="c7e20-152">Then copy hello PRIMARY KEY from hello portal and paste it over `<your primary key>`.</span></span> <span data-ttu-id="c7e20-153">Estar seguro de hello tooremove `<` y `>` de sus valores.</span><span class="sxs-lookup"><span data-stu-id="c7e20-153">Be sure tooremove hello `<` and `>` from your values.</span></span>

![Captura de pantalla de hello portal de Azure usa Hola NoSQL tutorial toocreate una aplicación de consola de C#.](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <span data-ttu-id="c7e20-156"><a id="instantiate"></a>Crear una instancia de hello DocumentClient</span><span class="sxs-lookup"><span data-stu-id="c7e20-156"><a id="instantiate"></a>Instantiate hello DocumentClient</span></span>

<span data-ttu-id="c7e20-157">Ahora, cree una nueva instancia de hello **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="c7e20-157">Now, create a new instance of hello **DocumentClient**.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <span data-ttu-id="c7e20-158"><a id="create-database"></a>Creación de una base de datos</span><span class="sxs-lookup"><span data-stu-id="c7e20-158"><a id="create-database"></a>Create a database</span></span>

<span data-ttu-id="c7e20-159">A continuación, cree una base de datos de Azure Cosmos [base de datos](documentdb-resources.md#databases) mediante el uso de hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) método o [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) método de hello  **DocumentClient** clase a partir de hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c7e20-159">Next, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class from hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="c7e20-160">Una base de datos es el contenedor lógico de Hola de almacenamiento de documentos JSON particionado entre colecciones.</span><span class="sxs-lookup"><span data-stu-id="c7e20-160">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a><span data-ttu-id="c7e20-161">Decisión sobre una clave de partición</span><span class="sxs-lookup"><span data-stu-id="c7e20-161">Decide on a partition key</span></span> 

<span data-ttu-id="c7e20-162">Las colecciones son contenedores para almacenar documentos.</span><span class="sxs-lookup"><span data-stu-id="c7e20-162">Collections are containers for storing documents.</span></span> <span data-ttu-id="c7e20-163">Son recursos lógicos y pueden [abarcar una o varias particiones físicas](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="c7e20-163">They are logical resources and can [span one or more physical partitions](partition-data.md).</span></span> <span data-ttu-id="c7e20-164">A [clave de partición](documentdb-partition-data.md) es una propiedad (o ruta de acceso) dentro de los documentos que está toodistribute usa los datos entre los servidores de Hola o particiones.</span><span class="sxs-lookup"><span data-stu-id="c7e20-164">A [partition key](documentdb-partition-data.md) is a property (or path) within your documents that is used toodistribute your data among hello servers or partitions.</span></span> <span data-ttu-id="c7e20-165">Hola a todos los documentos con hello misma clave de partición se almacenan en misma partición.</span><span class="sxs-lookup"><span data-stu-id="c7e20-165">All documents with hello same partition key are stored in hello same partition.</span></span> 

<span data-ttu-id="c7e20-166">Determinar una clave de partición es una decisión importante toomake antes de crear una colección.</span><span class="sxs-lookup"><span data-stu-id="c7e20-166">Determining a partition key is an important decision toomake before you create a collection.</span></span> <span data-ttu-id="c7e20-167">Las claves de partición son una propiedad (o la ruta de acceso) en los documentos que pueden ser utilizado por la base de datos de Azure Cosmos toodistribute los datos entre varios servidores o las particiones.</span><span class="sxs-lookup"><span data-stu-id="c7e20-167">Partition keys are a property (or path) within your documents that can be used by Azure Cosmos DB toodistribute your data among multiple servers or partitions.</span></span> <span data-ttu-id="c7e20-168">COSMOS DB aplica un algoritmo hash de valor de clave de partición de Hola y utiliza la partición de Hola de toodetermine de resultado de hello aplica un algoritmo hash en qué documento de hello toostore.</span><span class="sxs-lookup"><span data-stu-id="c7e20-168">Cosmos DB hashes hello partition key value and uses hello hashed result toodetermine hello partition in which toostore hello document.</span></span> <span data-ttu-id="c7e20-169">Hola a todos los documentos con hello misma clave de partición se almacenan en misma partición y las claves de partición no se puede cambiar una vez que se crea una colección.</span><span class="sxs-lookup"><span data-stu-id="c7e20-169">All documents with hello same partition key are stored in hello same partition, and partition keys cannot be changed once a collection is created.</span></span> 

<span data-ttu-id="c7e20-170">Para este tutorial, vamos clave de partición de hello tooset demasiado`/deviceId` así que Hola a todos los datos de Hola para un único dispositivo se almacena en una sola partición.</span><span class="sxs-lookup"><span data-stu-id="c7e20-170">For this tutorial, we're going tooset hello partition key too`/deviceId` so that hello all hello data for a single device is stored in a single partition.</span></span> <span data-ttu-id="c7e20-171">Desea toochoose una clave de partición que tiene un gran número de valores, cada uno de los cuales se usan en sobre hello tooensure de frecuencia mismo Cosmos DB puede equilibrar la carga que los datos aumenta y lograr un rendimiento total de colección de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="c7e20-171">You want toochoose a partition key that has a large number of values, each of which are used at about hello same frequency tooensure Cosmos DB can load balance as your data grows and achieve hello full throughput of hello collection.</span></span> 

<span data-ttu-id="c7e20-172">¿Para obtener más información acerca de las particiones, vea [cómo toopartition y la escala en la base de datos de Azure Cosmos?](partition-data.md)</span><span class="sxs-lookup"><span data-stu-id="c7e20-172">For more information about partitioning, see [How toopartition and scale in Azure Cosmos DB?](partition-data.md)</span></span> 

## <span data-ttu-id="c7e20-173"><a id="CreateColl"></a>Creación de una colección</span><span class="sxs-lookup"><span data-stu-id="c7e20-173"><a id="CreateColl"></a>Create a collection</span></span> 

<span data-ttu-id="c7e20-174">Ahora que sabemos que la clave de partición, `/deviceId`, permite crear un [colección](documentdb-resources.md#collections) mediante el uso de hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) método o [ CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) método de hello **DocumentClient** clase.</span><span class="sxs-lookup"><span data-stu-id="c7e20-174">Now that we know our partition key, `/deviceId`, lets create a [collection](documentdb-resources.md#collections) by using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="c7e20-175">Una colección es un contenedor de documentos JSON y cualquier lógica de aplicación JavaScript asociada.</span><span class="sxs-lookup"><span data-stu-id="c7e20-175">A collection is a container of JSON documents and any associated JavaScript application logic.</span></span> 

> [!WARNING]
> <span data-ttu-id="c7e20-176">Crear una colección tiene precios implicaciones, tal y como está reservando para hello toocommunicate de aplicación con la base de datos de Azure Cosmos rendimiento.</span><span class="sxs-lookup"><span data-stu-id="c7e20-176">Creating a collection has pricing implications, as you are reserving throughput for hello application toocommunicate with Azure Cosmos DB.</span></span> <span data-ttu-id="c7e20-177">Para más detalles, visite la [página sobre precios](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="c7e20-177">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

```csharp
// Collection for device telemetry. Here hello JSON property deviceId is used  
// as hello partition key toospread across partitions. Configured for 2500 RU/s  
// throughput and an indexing policy that supports sorting against any  
// number or string property. .
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 2500 });
```

<span data-ttu-id="c7e20-178">Esto hace que la método una API de REST llamada tooAzure DB Cosmos y Hola un número de particiones según rendimiento solicitado Hola de disposiciones de servicio.</span><span class="sxs-lookup"><span data-stu-id="c7e20-178">This method makes a REST API call tooAzure Cosmos DB, and hello service provisions a number of partitions based on hello requested throughput.</span></span> <span data-ttu-id="c7e20-179">Puede cambiar el rendimiento de una colección Hola según sus necesidades de rendimiento evolucionar utilizando Hola SDK o hello [portal de Azure](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="c7e20-179">You can change hello throughput of a collection as your performance needs evolve using hello SDK or hello [Azure portal](set-throughput.md).</span></span>

## <span data-ttu-id="c7e20-180"><a id="CreateDoc"></a>Creación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="c7e20-180"><a id="CreateDoc"></a>Create JSON documents</span></span>
<span data-ttu-id="c7e20-181">Vamos a insertar algunos documentos JSON en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c7e20-181">Let's insert some JSON documents into Azure Cosmos DB.</span></span> <span data-ttu-id="c7e20-182">A [documento](documentdb-resources.md#documents) pueden crearse mediante el uso de hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) método de hello **DocumentClient** clase.</span><span class="sxs-lookup"><span data-stu-id="c7e20-182">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="c7e20-183">Los documentos son contenido JSON definido por el usuario (arbitrario).</span><span class="sxs-lookup"><span data-stu-id="c7e20-183">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="c7e20-184">Esta clase de ejemplo contiene una lectura de dispositivo y un tooinsert de tooCreateDocumentAsync de llamada a un nuevo dispositivo de lectura en una colección.</span><span class="sxs-lookup"><span data-stu-id="c7e20-184">This sample class contains a device reading, and a call tooCreateDocumentAsync tooinsert a new device reading into a collection.</span></span>

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here hello partition key is extracted 
// as "XMS-0001" based on hello collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```
## <a name="read-data"></a><span data-ttu-id="c7e20-185">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="c7e20-185">Read data</span></span>

<span data-ttu-id="c7e20-186">Vamos a leer documento Hola por su clave de partición y el identificador mediante el método ReadDocumentAsync de hello.</span><span class="sxs-lookup"><span data-stu-id="c7e20-186">Let's read hello document by its partition key and Id using hello ReadDocumentAsync method.</span></span> <span data-ttu-id="c7e20-187">Tenga en cuenta que las lecturas Hola incluyen un valor de PartitionKey (toohello correspondiente `x-ms-documentdb-partitionkey` encabezado de solicitud de hello API de REST).</span><span class="sxs-lookup"><span data-stu-id="c7e20-187">Note that hello reads include a PartitionKey value (corresponding toohello `x-ms-documentdb-partitionkey` request header in hello REST API).</span></span>

```csharp
// Read document. Needs hello partition key and hello Id toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a><span data-ttu-id="c7e20-188">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="c7e20-188">Update data</span></span>

<span data-ttu-id="c7e20-189">Ahora vamos a actualizar algunos datos utilizando el método de hello ReplaceDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="c7e20-189">Now let's update some data using hello ReplaceDocumentAsync method.</span></span>

```csharp
// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a><span data-ttu-id="c7e20-190">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="c7e20-190">Delete data</span></span>

<span data-ttu-id="c7e20-191">Ahora permite eliminar un documento por clave de partición y el identificador mediante el método de hello DeleteDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="c7e20-191">Now lets delete a document by partition key and id by using hello DeleteDocumentAsync method.</span></span>

```csharp
// Delete a document. hello partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a><span data-ttu-id="c7e20-192">Consulta de colecciones con particiones</span><span class="sxs-lookup"><span data-stu-id="c7e20-192">Query partitioned collections</span></span>

<span data-ttu-id="c7e20-193">Al consultar datos en colecciones con particiones, la base de datos de Azure Cosmos automáticamente las rutas Hola particiones toohello de consulta correspondiente a los valores de clave de partición de toohello especificados en el filtro de hello (si hay alguno).</span><span class="sxs-lookup"><span data-stu-id="c7e20-193">When you query data in partitioned collections, Azure Cosmos DB automatically routes hello query toohello partitions corresponding toohello partition key values specified in hello filter (if there are any).</span></span> <span data-ttu-id="c7e20-194">Por ejemplo, esta consulta es la clave de partición Hola de contenedor de partición de hello del toojust enrutado "XMS-0001".</span><span class="sxs-lookup"><span data-stu-id="c7e20-194">For example, this query is routed toojust hello partition containing hello partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="c7e20-195">Hola siguiente consulta no tiene un filtro en la clave de partición de hello (DeviceId) y es en abanico particiones tooall donde se ejecuta en el índice de la partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7e20-195">hello following query does not have a filter on hello partition key (DeviceId) and is fanned out tooall partitions where it is executed against hello partition's index.</span></span> <span data-ttu-id="c7e20-196">Tenga en cuenta que tener hello toospecify EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` Hola API de REST) toohave Hola SDK tooexecute una consulta en particiones.</span><span class="sxs-lookup"><span data-stu-id="c7e20-196">Note that you have toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello REST API) toohave hello SDK tooexecute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

## <a name="parallel-query-execution"></a><span data-ttu-id="c7e20-197">Ejecución de consultas en paralelo</span><span class="sxs-lookup"><span data-stu-id="c7e20-197">Parallel query execution</span></span>
<span data-ttu-id="c7e20-198">Hola SDK de documentos de base de datos de Azure Cosmos 1.9.0 y versiones posteriores admite opciones de ejecución de consultas en paralelo, lo que permite una latencia baja tooperform consultas en colecciones con particiones, incluso cuando los necesitan tootouch un gran número de particiones.</span><span class="sxs-lookup"><span data-stu-id="c7e20-198">hello Azure Cosmos DB DocumentDB SDKs 1.9.0 and above support parallel query execution options, which allow you tooperform low latency queries against partitioned collections, even when they need tootouch a large number of partitions.</span></span> <span data-ttu-id="c7e20-199">Por ejemplo, hello después de consulta es toorun configurado en paralelo en particiones.</span><span class="sxs-lookup"><span data-stu-id="c7e20-199">For example, hello following query is configured toorun in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="c7e20-200">Puede administrar la ejecución de consultas en paralelo ajustando Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="c7e20-200">You can manage parallel query execution by tuning hello following parameters:</span></span>

* <span data-ttu-id="c7e20-201">Estableciendo `MaxDegreeOfParallelism`, puede controlar el grado de Hola de paralelismo es decir, Hola número máximo de particiones de la colección de las toohello de conexiones de red simultáneas.</span><span class="sxs-lookup"><span data-stu-id="c7e20-201">By setting `MaxDegreeOfParallelism`, you can control hello degree of parallelism i.e., hello maximum number of simultaneous network connections toohello collection's partitions.</span></span> <span data-ttu-id="c7e20-202">Si se establece demasiado-1, se administra el grado de paralelismo Hola Hola SDK.</span><span class="sxs-lookup"><span data-stu-id="c7e20-202">If you set this too-1, hello degree of parallelism is managed by hello SDK.</span></span> <span data-ttu-id="c7e20-203">Si hello `MaxDegreeOfParallelism` no se ha especificado o establecer too0, que es el valor predeterminado de hello, habrá particiones de la colección toohello de conexión de red único.</span><span class="sxs-lookup"><span data-stu-id="c7e20-203">If hello `MaxDegreeOfParallelism` is not specified or set too0, which is hello default value, there will be a single network connection toohello collection's partitions.</span></span>
* <span data-ttu-id="c7e20-204">Al establecer `MaxBufferedItemCount`, puede compensar el uso de memoria por parte del cliente y la latencia en las consultas.</span><span class="sxs-lookup"><span data-stu-id="c7e20-204">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="c7e20-205">Si omite este parámetro o se establece demasiado-1, número de Hola de elementos almacenados en búfer durante la ejecución de consultas en paralelo es administrado por hello SDK.</span><span class="sxs-lookup"><span data-stu-id="c7e20-205">If you omit this parameter or set this too-1, hello number of items buffered during parallel query execution is managed by hello SDK.</span></span>

<span data-ttu-id="c7e20-206">Dados Hola mismo estado de recopilación de hello, una consulta en paralelo devolverá resultados Hola mismo pedido como en ejecución en serie.</span><span class="sxs-lookup"><span data-stu-id="c7e20-206">Given hello same state of hello collection, a parallel query will return results in hello same order as in serial execution.</span></span> <span data-ttu-id="c7e20-207">Al realizar una consulta entre particiones que incluye la ordenación (ORDER BY o superior), hello DocumentDB SDK emite consultas hello en paralelo en particiones y combina los resultados ordenados parcialmente en tooproduce de lado cliente hello resultados ordenados globalmente.</span><span class="sxs-lookup"><span data-stu-id="c7e20-207">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), hello DocumentDB SDK issues hello query in parallel across partitions and merges partially sorted results in hello client side tooproduce globally ordered results.</span></span>

## <a name="execute-stored-procedures"></a><span data-ttu-id="c7e20-208">Ejecución de procedimientos almacenados</span><span class="sxs-lookup"><span data-stu-id="c7e20-208">Execute stored procedures</span></span>
<span data-ttu-id="c7e20-209">Por último, puede ejecutar transacciones atómicas con documentos con Hola mismo Id. de dispositivo, por ejemplo, si desea mantener agregados u Hola estado más reciente de un dispositivo en un único documento agregando Hola siguiendo el proyecto de código tooyour.</span><span class="sxs-lookup"><span data-stu-id="c7e20-209">Lastly, you can execute atomic transactions against documents with hello same device ID, e.g. if you're maintaining aggregates or hello latest state of a device in a single document by adding hello following code tooyour project.</span></span>

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

<span data-ttu-id="c7e20-210">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="c7e20-210">And that's it!</span></span> <span data-ttu-id="c7e20-211">esos son componentes principales de Hola de una aplicación de base de datos de Azure Cosmos que utiliza una distribución de datos de escala de tooefficiently clave de partición en particiones.</span><span class="sxs-lookup"><span data-stu-id="c7e20-211">those are hello main components of an Azure Cosmos DB application that uses a partition key tooefficiently scale data distribution across partitions.</span></span>  

## <a name="clean-up-resources"></a><span data-ttu-id="c7e20-212">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="c7e20-212">Clean up resources</span></span>

<span data-ttu-id="c7e20-213">Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial Hola portal de Azure con hello pasos:</span><span class="sxs-lookup"><span data-stu-id="c7e20-213">If you're not going toocontinue toouse this app, delete all resources created by this tutorial in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="c7e20-214">En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en hello único nombre de recurso de Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="c7e20-214">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello unique name of hello resource you created.</span></span> 
2. <span data-ttu-id="c7e20-215">En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="c7e20-215">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7e20-216">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c7e20-216">Next steps</span></span>

<span data-ttu-id="c7e20-217">En este tutorial, ha hecho siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="c7e20-217">In this tutorial, you've done hello following:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="c7e20-218">Se creó una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c7e20-218">Created an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="c7e20-219">Se creó una base de datos y una colección con una clave de partición</span><span class="sxs-lookup"><span data-stu-id="c7e20-219">Created a database and collection with a partition key</span></span>
> * <span data-ttu-id="c7e20-220">Se crearon documentos JSON</span><span class="sxs-lookup"><span data-stu-id="c7e20-220">Created JSON documents</span></span>
> * <span data-ttu-id="c7e20-221">Se actualizó un documento</span><span class="sxs-lookup"><span data-stu-id="c7e20-221">Updated a document</span></span>
> * <span data-ttu-id="c7e20-222">Se consultaron colecciones con particiones</span><span class="sxs-lookup"><span data-stu-id="c7e20-222">Queried partitioned collections</span></span>
> * <span data-ttu-id="c7e20-223">Se ejecutó un procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="c7e20-223">Ran a stored procedure</span></span>
> * <span data-ttu-id="c7e20-224">Se eliminó un documento</span><span class="sxs-lookup"><span data-stu-id="c7e20-224">Deleted a document</span></span>
> * <span data-ttu-id="c7e20-225">Se eliminó una base de datos</span><span class="sxs-lookup"><span data-stu-id="c7e20-225">Deleted a database</span></span>

<span data-ttu-id="c7e20-226">Ahora puede continuar el tutorial siguiente toohello e importar cuenta de base de datos de Cosmos tooyour datos adicionales.</span><span class="sxs-lookup"><span data-stu-id="c7e20-226">You can now proceed toohello next tutorial and import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7e20-227">Importación de datos a Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c7e20-227">Import data into Azure Cosmos DB</span></span>](import-data.md)
