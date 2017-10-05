---
title: 'Azure Cosmos DB: desarrollo con la API de DocumentDB en .NET | Microsoft Docs'
description: "Obtenga información sobre cómo desarrollar con la API de DocumentDB de Azure Cosmos DB con .NET"
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
ms.openlocfilehash: 2eed74ae9bd173b0944ec190dfe5d9a4bdc54c37
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmosdb-develop-with-the-documentdb-api-in-net"></a><span data-ttu-id="e5c0b-103">Azure Cosmos DB: desarrollo con la API de DocumentDB en .NET</span><span class="sxs-lookup"><span data-stu-id="e5c0b-103">Azure CosmosDB: Develop with the DocumentDB API in .NET</span></span>

<span data-ttu-id="e5c0b-104">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="e5c0b-105">Puede crear rápidamente bases de datos de documentos, clave-valor y grafos y realizar consultas en ellas. Todas las bases de datos se beneficiarán de las funcionalidades de distribución global y escala horizontal en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="e5c0b-106">En este tutorial se muestra cómo crear una cuenta de Azure Cosmos DB con Azure Portal y, luego, crear una colección y base de datos de documentos con una [clave de partición](documentdb-partition-data.md#partition-keys) mediante la [API de .NET de DocumentDB](documentdb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e5c0b-106">This tutorial demonstrates how to create an Azure Cosmos DB account using the Azure portal, and then create a document database and collection with a [partition key](documentdb-partition-data.md#partition-keys) using the [DocumentDB .NET API](documentdb-introduction.md).</span></span> <span data-ttu-id="e5c0b-107">Si define una clave de partición en el momento de crear una colección, la aplicación está preparada para escalar fácilmente a medida que aumentan los datos.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-107">By defining a partition key when you create a collection, your application is prepared to scale effortlessly as your data grows.</span></span> 

<span data-ttu-id="e5c0b-108">En este tutorial se describen las siguientes tareas mediante el uso de la [API de .NET de DocumentDB](documentdb-sdk-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="e5c0b-108">This tutorial covers the following tasks by using the [DocumentDB .NET API](documentdb-sdk-dotnet.md):</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e5c0b-109">Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e5c0b-109">Create an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="e5c0b-110">Creación de una base de datos y colección con una clave de partición</span><span class="sxs-lookup"><span data-stu-id="e5c0b-110">Create a database and collection with a partition key</span></span>
> * <span data-ttu-id="e5c0b-111">Creación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="e5c0b-111">Create JSON documents</span></span>
> * <span data-ttu-id="e5c0b-112">Actualización de un documento</span><span class="sxs-lookup"><span data-stu-id="e5c0b-112">Update a document</span></span>
> * <span data-ttu-id="e5c0b-113">Consulta de colecciones con particiones</span><span class="sxs-lookup"><span data-stu-id="e5c0b-113">Query partitioned collections</span></span>
> * <span data-ttu-id="e5c0b-114">Ejecución de procedimientos almacenados</span><span class="sxs-lookup"><span data-stu-id="e5c0b-114">Run stored procedures</span></span>
> * <span data-ttu-id="e5c0b-115">Eliminar un documento</span><span class="sxs-lookup"><span data-stu-id="e5c0b-115">Delete a document</span></span>
> * <span data-ttu-id="e5c0b-116">Eliminación de una base de datos</span><span class="sxs-lookup"><span data-stu-id="e5c0b-116">Delete a database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5c0b-117">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e5c0b-117">Prerequisites</span></span>
<span data-ttu-id="e5c0b-118">Asegúrese de que dispone de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e5c0b-118">Please make sure you have the following:</span></span>

* <span data-ttu-id="e5c0b-119">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-119">An active Azure account.</span></span> <span data-ttu-id="e5c0b-120">Si no tiene una, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="e5c0b-120">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="e5c0b-121">De manera alternativa, puede usar el [emulador de Azure Cosmos DB](local-emulator.md) para este tutorial si quisiera usar un entorno local que emule el servicio de Azure DocumentDB con fines de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-121">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial if you'd like to use a local environment that emulates the Azure DocumentDB service for development purposes.</span></span>
* <span data-ttu-id="e5c0b-122">[Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="e5c0b-122">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="e5c0b-123">Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e5c0b-123">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="e5c0b-124">Para comenzar, creemos una cuenta de Azure Cosmos DB en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-124">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>

> [!TIP]
> * <span data-ttu-id="e5c0b-125">¿Ya tiene una cuenta de Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="e5c0b-125">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="e5c0b-126">Si es así, vaya a [Configuración de la solución de Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="e5c0b-126">If so, skip ahead to [Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="e5c0b-127">¿Ya tenía una cuenta de Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="e5c0b-127">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="e5c0b-128">Si es así, ahora es una cuenta de Azure Cosmos DB, por lo que puede ir directamente a [Configuración de la solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="e5c0b-128">If so, your account is now an Azure Cosmos DB account and you can skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="e5c0b-129">Si usa el Emulador de Azure Cosmos DB, siga los pasos que se indican en [Emulador de Azure Cosmos DB](local-emulator.md) para configurar el emulador y vaya directamente a [Configuración de la solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="e5c0b-129">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="e5c0b-130"><a id="SetupVS"></a>Configuración de la solución de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e5c0b-130"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="e5c0b-131">Abra **Visual Studio** en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-131">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="e5c0b-132">En el menú **Archivo**, seleccione **Nuevo** y elija **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-132">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="e5c0b-133">En el cuadro de diálogo **Nuevo proyecto**, seleccione **Plantillas** / **Visual C#** / **Aplicación de consola (.NET Framework)**, asigne un nombre al proyecto y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-133">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="e5c0b-134">![Captura de pantalla de la ventana Nuevo proyecto](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="e5c0b-134">![Screen shot of the New Project window](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span></span>

4. <span data-ttu-id="e5c0b-135">En el **Explorador de soluciones**, haga clic con el botón derecho en la nueva aplicación de la consola, que se encuentra en la solución de Visual Studio y, a continuación, haga clic en **Administrar paquetes NuGet...**</span><span class="sxs-lookup"><span data-stu-id="e5c0b-135">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Captura de pantalla del menú contextual del proyecto](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="e5c0b-137">En la pestaña **NuGet**, haga clic en **Examinar** y escriba **documentdb** en el cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-137">In the **NuGet** tab, click **Browse**, and type **documentdb** in the search box.</span></span>
<!---stopped here--->
6. <span data-ttu-id="e5c0b-138">En los resultados, busque **Microsoft.Azure.DocumentDB** y haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-138">Within the results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="e5c0b-139">El identificador del paquete de la biblioteca de cliente de Azure Cosmos DB es [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="e5c0b-139">The package ID for the Azure Cosmos DB Client Library is [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span></span>
   <span data-ttu-id="e5c0b-140">![Captura de pantalla del menú NuGet para encontrar el SDK de cliente de Azure Cosmos DB](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="e5c0b-140">![Screen shot of the NuGet Menu for finding Azure Cosmos DB Client SDK](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="e5c0b-141">Si recibe un mensaje sobre cómo revisar los cambios en la solución, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-141">If you get a message about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="e5c0b-142">Si recibe un mensaje acerca de la aceptación de licencia, haga clic en **Acepto**.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-142">If you get a message about license acceptance, click **I accept**.</span></span>

## <span data-ttu-id="e5c0b-143"><a id="Connect"></a>Incorporación de referencias en el proyecto</span><span class="sxs-lookup"><span data-stu-id="e5c0b-143"><a id="Connect"></a>Add references to your project</span></span>
<span data-ttu-id="e5c0b-144">Los pasos restantes de este tutorial proporciona los fragmentos de código de la API de DocumentDB que se requieren para crear y actualizar los recursos de Azure Cosmos DB en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-144">The remaining steps in this tutorial provide the DocumentDB API code snippets required to create and update Azure Cosmos DB resources in your project.</span></span>

<span data-ttu-id="e5c0b-145">En primer lugar, agregue estas referencias a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-145">First, add these references to your application.</span></span>
<!---These aren't added by default when you install the pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <span data-ttu-id="e5c0b-146"><a id="add-references"></a>Conexión de la aplicación</span><span class="sxs-lookup"><span data-stu-id="e5c0b-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="e5c0b-147">A continuación, agregue estas dos constantes y la variable *client* en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-147">Next, add these two constants and your *client* variable in your application.</span></span>

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

<span data-ttu-id="e5c0b-148">A continuación, vuelva a [Azure Portal](https://portal.azure.com) para recuperar la dirección URL del punto de conexión y la clave principal.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-148">Then, head back to the [Azure portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="e5c0b-149">La dirección URL del punto de conexión y la clave principal son necesarias para que la aplicación sepa a dónde debe conectarse y para que Azure Cosmos DB confíe en la conexión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-149">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="e5c0b-150">En Azure Portal, vaya a la cuenta de Azure Cosmos DB, haga clic en **Claves** y, luego, en **Claves de lectura y escritura**.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-150">In the Azure portal, navigate to your Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span>

<span data-ttu-id="e5c0b-151">Copie el URI desde el portal y péguelo en `<your endpoint URL>` en el archivo program.cs.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-151">Copy the URI from the portal and paste it over `<your endpoint URL>` in the program.cs file.</span></span> <span data-ttu-id="e5c0b-152">Después, copie la CLAVE PRINCIPAL del portal y péguelo en `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-152">Then copy the PRIMARY KEY from the portal and paste it over `<your primary key>`.</span></span> <span data-ttu-id="e5c0b-153">Asegúrese de quitar `<` y `>` de los valores.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-153">Be sure to remove the `<` and `>` from your values.</span></span>

![Captura de pantalla de Azure Portal, usado por el tutorial de NoSQL para crear una aplicación de consola de C#.](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <span data-ttu-id="e5c0b-156"><a id="instantiate"></a>Creación de instancia de DocumentClient</span><span class="sxs-lookup"><span data-stu-id="e5c0b-156"><a id="instantiate"></a>Instantiate the DocumentClient</span></span>

<span data-ttu-id="e5c0b-157">Ahora, cree una instancia nueva de **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-157">Now, create a new instance of the **DocumentClient**.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <span data-ttu-id="e5c0b-158"><a id="create-database"></a>Creación de una base de datos</span><span class="sxs-lookup"><span data-stu-id="e5c0b-158"><a id="create-database"></a>Create a database</span></span>

<span data-ttu-id="e5c0b-159">A continuación, cree una [base de datos](documentdb-resources.md#databases) de Azure Cosmos DB con el método [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) o el método [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) de la clase **DocumentClient** desde el [SDK de .NET de DocumentDB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="e5c0b-159">Next, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class from the [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="e5c0b-160">Una base de datos es un contenedor lógico de almacenamiento de documentos JSON particionado en recopilaciones.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-160">A database is the logical container of JSON document storage partitioned across collections.</span></span>

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a><span data-ttu-id="e5c0b-161">Decisión sobre una clave de partición</span><span class="sxs-lookup"><span data-stu-id="e5c0b-161">Decide on a partition key</span></span> 

<span data-ttu-id="e5c0b-162">Las colecciones son contenedores para almacenar documentos.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-162">Collections are containers for storing documents.</span></span> <span data-ttu-id="e5c0b-163">Son recursos lógicos y pueden [abarcar una o varias particiones físicas](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="e5c0b-163">They are logical resources and can [span one or more physical partitions](partition-data.md).</span></span> <span data-ttu-id="e5c0b-164">Una [clave de partición](documentdb-partition-data.md) es una propiedad (o ruta de acceso) dentro de los documentos que se usa para distribuir los datos entre los servidores o las particiones.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-164">A [partition key](documentdb-partition-data.md) is a property (or path) within your documents that is used to distribute your data among the servers or partitions.</span></span> <span data-ttu-id="e5c0b-165">Todos los documentos que tengan la misma clave de partición se almacenan en la misma partición.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-165">All documents with the same partition key are stored in the same partition.</span></span> 

<span data-ttu-id="e5c0b-166">Determinar una clave de partición es una decisión importante de tomar antes de crear una colección.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-166">Determining a partition key is an important decision to make before you create a collection.</span></span> <span data-ttu-id="e5c0b-167">Las claves de partición son una propiedad (o ruta de acceso) dentro de los documentos que puede usar Azure Cosmos DB para distribuir los datos entre los distintos servidores o particiones.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-167">Partition keys are a property (or path) within your documents that can be used by Azure Cosmos DB to distribute your data among multiple servers or partitions.</span></span> <span data-ttu-id="e5c0b-168">Cosmos DB aplica un algoritmo hash al valor de clave de partición y usa el resultado al que se ha aplicado un algoritmo hash para determinar en qué partición se va a almacenar el documento.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-168">Cosmos DB hashes the partition key value and uses the hashed result to determine the partition in which to store the document.</span></span> <span data-ttu-id="e5c0b-169">Todos los documentos que tengan la clave de partición se almacenan en la misma partición y las claves de partición no se pueden modificar una vez que se crea una colección.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-169">All documents with the same partition key are stored in the same partition, and partition keys cannot be changed once a collection is created.</span></span> 

<span data-ttu-id="e5c0b-170">En este tutorial se establecerá la clave de partición en `/deviceId`, para que todos los datos de un único dispositivo se almacenen en una sola partición.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-170">For this tutorial, we're going to set the partition key to `/deviceId` so that the all the data for a single device is stored in a single partition.</span></span> <span data-ttu-id="e5c0b-171">Desea elegir una clave de partición con una gran cantidad de valores, cada uno de los cuales se usa casi con la misma frecuencia para garantizar que Cosmos DB puede equilibrar la carga a medida que aumentan los datos para alcanzar el rendimiento total de la colección.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-171">You want to choose a partition key that has a large number of values, each of which are used at about the same frequency to ensure Cosmos DB can load balance as your data grows and achieve the full throughput of the collection.</span></span> 

<span data-ttu-id="e5c0b-172">Para más información sobre la creación de particiones, consulte [Partición y escala en Azure Cosmos DB](partition-data.md)</span><span class="sxs-lookup"><span data-stu-id="e5c0b-172">For more information about partitioning, see [How to partition and scale in Azure Cosmos DB?](partition-data.md)</span></span> 

## <span data-ttu-id="e5c0b-173"><a id="CreateColl"></a>Creación de una colección</span><span class="sxs-lookup"><span data-stu-id="e5c0b-173"><a id="CreateColl"></a>Create a collection</span></span> 

<span data-ttu-id="e5c0b-174">Ahora que conocemos la clave de partición, `/deviceId`, vamos a crear una [colección](documentdb-resources.md#collections) a través del método [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) o el método [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) de la clase **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-174">Now that we know our partition key, `/deviceId`, lets create a [collection](documentdb-resources.md#collections) by using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="e5c0b-175">Una colección es un contenedor de documentos JSON y cualquier lógica de aplicación JavaScript asociada.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-175">A collection is a container of JSON documents and any associated JavaScript application logic.</span></span> 

> [!WARNING]
> <span data-ttu-id="e5c0b-176">Crear una colección implica precios, debido a que reserva rendimiento para que la aplicación se comunique con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-176">Creating a collection has pricing implications, as you are reserving throughput for the application to communicate with Azure Cosmos DB.</span></span> <span data-ttu-id="e5c0b-177">Para más detalles, visite la [página sobre precios](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="e5c0b-177">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

```csharp
// Collection for device telemetry. Here the JSON property deviceId is used  
// as the partition key to spread across partitions. Configured for 2500 RU/s  
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

<span data-ttu-id="e5c0b-178">Este método realiza una llamada API de REST a Azure Cosmos DB y el servicio aprovisiona una cantidad de particiones según el rendimiento que se solicite.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-178">This method makes a REST API call to Azure Cosmos DB, and the service provisions a number of partitions based on the requested throughput.</span></span> <span data-ttu-id="e5c0b-179">Puede cambiar el rendimiento de una colección a medida que evolucionan las necesidades de rendimiento con el SDK o [Azure Portal](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="e5c0b-179">You can change the throughput of a collection as your performance needs evolve using the SDK or the [Azure portal](set-throughput.md).</span></span>

## <span data-ttu-id="e5c0b-180"><a id="CreateDoc"></a>Creación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="e5c0b-180"><a id="CreateDoc"></a>Create JSON documents</span></span>
<span data-ttu-id="e5c0b-181">Vamos a insertar algunos documentos JSON en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-181">Let's insert some JSON documents into Azure Cosmos DB.</span></span> <span data-ttu-id="e5c0b-182">Un [documento](documentdb-resources.md#documents) puede crearse mediante el método [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) de la clase **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-182">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="e5c0b-183">Los documentos son contenido JSON definido por el usuario (arbitrario).</span><span class="sxs-lookup"><span data-stu-id="e5c0b-183">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="e5c0b-184">Esta clase de ejemplo contiene una lectura de dispositivo y una llamada a CreateDocumentAsync para insertar una nueva lectura de dispositivo en una colección.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-184">This sample class contains a device reading, and a call to CreateDocumentAsync to insert a new device reading into a collection.</span></span>

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

// Create a document. Here the partition key is extracted 
// as "XMS-0001" based on the collection definition
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
## <a name="read-data"></a><span data-ttu-id="e5c0b-185">Lectura de datos</span><span class="sxs-lookup"><span data-stu-id="e5c0b-185">Read data</span></span>

<span data-ttu-id="e5c0b-186">Leamos el documento según su clave de partición e identificador con el método ReadDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-186">Let's read the document by its partition key and Id using the ReadDocumentAsync method.</span></span> <span data-ttu-id="e5c0b-187">Tenga en cuenta que las lecturas incluyen un valor PartitionKey (correspondiente al encabezado de solicitud `x-ms-documentdb-partitionkey` de la API de REST).</span><span class="sxs-lookup"><span data-stu-id="e5c0b-187">Note that the reads include a PartitionKey value (corresponding to the `x-ms-documentdb-partitionkey` request header in the REST API).</span></span>

```csharp
// Read document. Needs the partition key and the Id to be specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a><span data-ttu-id="e5c0b-188">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="e5c0b-188">Update data</span></span>

<span data-ttu-id="e5c0b-189">Ahora actualizaremos algunos datos con el método ReplaceDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-189">Now let's update some data using the ReplaceDocumentAsync method.</span></span>

```csharp
// Update the document. Partition key is not required, again extracted from the document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a><span data-ttu-id="e5c0b-190">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="e5c0b-190">Delete data</span></span>

<span data-ttu-id="e5c0b-191">Ahora eliminaremos un documento por clave de partición e identificador con el método DeleteDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-191">Now lets delete a document by partition key and id by using the DeleteDocumentAsync method.</span></span>

```csharp
// Delete a document. The partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a><span data-ttu-id="e5c0b-192">Consulta de colecciones con particiones</span><span class="sxs-lookup"><span data-stu-id="e5c0b-192">Query partitioned collections</span></span>

<span data-ttu-id="e5c0b-193">Al consultar datos en las colecciones particionadas, Azure Cosmos DB enruta automáticamente la consulta a las particiones correspondientes a los valores de clave de partición especificados en el filtro (en caso de que los haya).</span><span class="sxs-lookup"><span data-stu-id="e5c0b-193">When you query data in partitioned collections, Azure Cosmos DB automatically routes the query to the partitions corresponding to the partition key values specified in the filter (if there are any).</span></span> <span data-ttu-id="e5c0b-194">Por ejemplo, esta consulta se enruta únicamente a la partición cuya clave es "XMS-0001".</span><span class="sxs-lookup"><span data-stu-id="e5c0b-194">For example, this query is routed to just the partition containing the partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="e5c0b-195">La consulta siguiente no tiene filtro en la clave de partición (DeviceId) y por ello se despliega por todas las particiones, en las que se ejecuta según el índice de la partición.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-195">The following query does not have a filter on the partition key (DeviceId) and is fanned out to all partitions where it is executed against the partition's index.</span></span> <span data-ttu-id="e5c0b-196">Tenga en cuenta que debe especificar EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` en la API de REST) para que el SDK ejecute una consulta en todas las particiones.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-196">Note that you have to specify the EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in the REST API) to have the SDK to execute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

## <a name="parallel-query-execution"></a><span data-ttu-id="e5c0b-197">Ejecución de consultas en paralelo</span><span class="sxs-lookup"><span data-stu-id="e5c0b-197">Parallel query execution</span></span>
<span data-ttu-id="e5c0b-198">Los SDK de DocumentDB de Azure Cosmos DB de la versión 1.9.0 y posterior admiten opciones de ejecución de consultas en paralelo, que permiten realizar consultas de baja latencia en colecciones con particiones, incluso cuando tienen que acceder a un gran número de particiones.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-198">The Azure Cosmos DB DocumentDB SDKs 1.9.0 and above support parallel query execution options, which allow you to perform low latency queries against partitioned collections, even when they need to touch a large number of partitions.</span></span> <span data-ttu-id="e5c0b-199">Por ejemplo, la siguiente consulta está configurada para ejecutarse en paralelo en particiones.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-199">For example, the following query is configured to run in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="e5c0b-200">Puede administrar la ejecución de consultas en paralelo ajustando los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="e5c0b-200">You can manage parallel query execution by tuning the following parameters:</span></span>

* <span data-ttu-id="e5c0b-201">Al establecer `MaxDegreeOfParallelism`, puede controlar el grado de paralelismo; es decir, el número máximo de conexiones de red simultáneas en las particiones de la colección.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-201">By setting `MaxDegreeOfParallelism`, you can control the degree of parallelism i.e., the maximum number of simultaneous network connections to the collection's partitions.</span></span> <span data-ttu-id="e5c0b-202">Si lo establece en -1, el grado de paralelismo lo administra el SDK.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-202">If you set this to -1, the degree of parallelism is managed by the SDK.</span></span> <span data-ttu-id="e5c0b-203">Si el parámetro `MaxDegreeOfParallelism` no se especifica o está establecido en 0, que es el valor predeterminado, habrá una única conexión de red a las particiones de la colección.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-203">If the `MaxDegreeOfParallelism` is not specified or set to 0, which is the default value, there will be a single network connection to the collection's partitions.</span></span>
* <span data-ttu-id="e5c0b-204">Al establecer `MaxBufferedItemCount`, puede compensar el uso de memoria por parte del cliente y la latencia en las consultas.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-204">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="e5c0b-205">Si se omite este parámetro o lo establece en -1, el número de elementos almacenados en búfer durante la ejecución de consultas en paralelo lo administrará el SDK.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-205">If you omit this parameter or set this to -1, the number of items buffered during parallel query execution is managed by the SDK.</span></span>

<span data-ttu-id="e5c0b-206">Como se trata del mismo estado de la colección, una consulta en paralelo devolverá resultados en el mismo orden que la ejecución en serie.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-206">Given the same state of the collection, a parallel query will return results in the same order as in serial execution.</span></span> <span data-ttu-id="e5c0b-207">Al realizar una consulta entre particiones que incluye la ordenación (ORDER BY o TOP), el SDK de DocumentDB emite la consulta en paralelo en las particiones y combina los resultados ordenados parcialmente en el lado del cliente para generar resultados ordenados globalmente.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-207">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), the DocumentDB SDK issues the query in parallel across partitions and merges partially sorted results in the client side to produce globally ordered results.</span></span>

## <a name="execute-stored-procedures"></a><span data-ttu-id="e5c0b-208">Ejecución de procedimientos almacenados</span><span class="sxs-lookup"><span data-stu-id="e5c0b-208">Execute stored procedures</span></span>
<span data-ttu-id="e5c0b-209">Por último, puede ejecutar transacciones atómicas en relación con documentos con el mismo identificador de dispositivo, por ejemplo, si desea mantener los agregados o el estado más reciente de un dispositivo en un único documento. Para ello, agregue el código siguiente al proyecto.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-209">Lastly, you can execute atomic transactions against documents with the same device ID, e.g. if you're maintaining aggregates or the latest state of a device in a single document by adding the following code to your project.</span></span>

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

<span data-ttu-id="e5c0b-210">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-210">And that's it!</span></span> <span data-ttu-id="e5c0b-211">Estos son los componentes principales de una aplicación Azure Cosmos DB que usa una clave de partición para escalar de manera eficaz la distribución de datos entre las distintas particiones.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-211">those are the main components of an Azure Cosmos DB application that uses a partition key to efficiently scale data distribution across partitions.</span></span>  

## <a name="clean-up-resources"></a><span data-ttu-id="e5c0b-212">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="e5c0b-212">Clean up resources</span></span>

<span data-ttu-id="e5c0b-213">Si no va a seguir usando esta aplicación, siga estos pasos para eliminar todos los recursos creados en este tutorial en Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="e5c0b-213">If you're not going to continue to use this app, delete all resources created by this tutorial in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="e5c0b-214">En el menú de la izquierda de Azure Portal, haga clic en **Grupos de recursos** y en el nombre único del recurso que creó.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-214">From the left-hand menu in the Azure portal, click **Resource groups** and then click the unique name of the resource you created.</span></span> 
2. <span data-ttu-id="e5c0b-215">En la página del grupo de recursos, haga clic en **Eliminar**, escriba en el cuadro de texto el nombre del recurso que quiere eliminar y haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-215">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5c0b-216">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e5c0b-216">Next steps</span></span>

<span data-ttu-id="e5c0b-217">En este tutorial, ha hecho lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e5c0b-217">In this tutorial, you've done the following:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="e5c0b-218">Se creó una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e5c0b-218">Created an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="e5c0b-219">Se creó una base de datos y una colección con una clave de partición</span><span class="sxs-lookup"><span data-stu-id="e5c0b-219">Created a database and collection with a partition key</span></span>
> * <span data-ttu-id="e5c0b-220">Se crearon documentos JSON</span><span class="sxs-lookup"><span data-stu-id="e5c0b-220">Created JSON documents</span></span>
> * <span data-ttu-id="e5c0b-221">Se actualizó un documento</span><span class="sxs-lookup"><span data-stu-id="e5c0b-221">Updated a document</span></span>
> * <span data-ttu-id="e5c0b-222">Se consultaron colecciones con particiones</span><span class="sxs-lookup"><span data-stu-id="e5c0b-222">Queried partitioned collections</span></span>
> * <span data-ttu-id="e5c0b-223">Se ejecutó un procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="e5c0b-223">Ran a stored procedure</span></span>
> * <span data-ttu-id="e5c0b-224">Se eliminó un documento</span><span class="sxs-lookup"><span data-stu-id="e5c0b-224">Deleted a document</span></span>
> * <span data-ttu-id="e5c0b-225">Se eliminó una base de datos</span><span class="sxs-lookup"><span data-stu-id="e5c0b-225">Deleted a database</span></span>

<span data-ttu-id="e5c0b-226">Ahora puede pasar al tutorial siguiente e importar datos adicionales a su cuenta de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e5c0b-226">You can now proceed to the next tutorial and import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="e5c0b-227">Importación de datos a Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e5c0b-227">Import data into Azure Cosmos DB</span></span>](import-data.md)
