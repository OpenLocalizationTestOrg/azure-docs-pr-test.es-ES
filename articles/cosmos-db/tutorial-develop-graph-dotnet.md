---
title: 'Azure Cosmos DB: desarrollo con API Graph en .NET | Microsoft Docs'
description: "Obtenga información sobre cómo desarrollar con la API de DocumentDB de Azure Cosmos DB con .NET"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: cc8df0be-672b-493e-95a4-26dd52632261
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.custom: mvc
ms.openlocfilehash: eeaa0c4f84a408815371742334d2ba7ce600b72f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-develop-with-the-graph-api-in-net"></a><span data-ttu-id="fd863-103">Azure Cosmos DB: desarrollo con API Graph en .NET</span><span class="sxs-lookup"><span data-stu-id="fd863-103">Azure Cosmos DB: Develop with the Graph API in .NET</span></span>
<span data-ttu-id="fd863-104">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fd863-104">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="fd863-105">Puede crear rápidamente bases de datos de documentos, clave-valor y grafos y realizar consultas en ellas. Todas las bases de datos se beneficiarán de las funcionalidades de distribución global y escala horizontal en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fd863-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="fd863-106">En este tutorial se muestra cómo crear una cuenta de Azure Cosmos DB con Azure Portal y cómo crear un contenedor y una base de datos de grafo.</span><span class="sxs-lookup"><span data-stu-id="fd863-106">This tutorial demonstrates how to create an Azure Cosmos DB account using the Azure portal and how to create a graph database and container.</span></span> <span data-ttu-id="fd863-107">Luego, la aplicación crea una red social sencilla con cuatro personas con la [API Graph](graph-sdk-dotnet.md) (versión preliminar) y después cruza y consulta el grafo con Gremlin.</span><span class="sxs-lookup"><span data-stu-id="fd863-107">The application then creates a simple social network with four people using the [Graph API](graph-sdk-dotnet.md) (preview), then traverses and queries the graph using Gremlin.</span></span>

<span data-ttu-id="fd863-108">En este tutorial se describen las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="fd863-108">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fd863-109">Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fd863-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="fd863-110">Creación de un contenedor y una base de datos de grafo</span><span class="sxs-lookup"><span data-stu-id="fd863-110">Create a graph database and container</span></span>
> * <span data-ttu-id="fd863-111">Serialización de vértices y bordes en objetos .NET</span><span class="sxs-lookup"><span data-stu-id="fd863-111">Serialize vertices and edges to .NET objects</span></span>
> * <span data-ttu-id="fd863-112">Incorporación de vértices y bordes</span><span class="sxs-lookup"><span data-stu-id="fd863-112">Add vertices and edges</span></span>
> * <span data-ttu-id="fd863-113">Consulta del grafo con Gremlin</span><span class="sxs-lookup"><span data-stu-id="fd863-113">Query the graph using Gremlin</span></span>

## <a name="graphs-in-azure-cosmos-db"></a><span data-ttu-id="fd863-114">Grafos en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fd863-114">Graphs in Azure Cosmos DB</span></span>
<span data-ttu-id="fd863-115">Puede usar Azure Cosmos DB para crear, actualizar y consultar grafos con la biblioteca [Microsoft.Azure.Graphs](graph-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="fd863-115">You can use Azure Cosmos DB to create, update, and query graphs using the [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) library.</span></span> <span data-ttu-id="fd863-116">La biblioteca Microsoft.Azure.Graph proporciona un método de extensión único `CreateGremlinQuery<T>` además de la clase `DocumentClient` para ejecutas consultas Gremlin.</span><span class="sxs-lookup"><span data-stu-id="fd863-116">The Microsoft.Azure.Graph library provides a single extension method `CreateGremlinQuery<T>` on top of the `DocumentClient` class to execute Gremlin queries.</span></span>

<span data-ttu-id="fd863-117">Gremlin es un lenguaje de programación funcional que admite operaciones de escritura (DML) y operaciones de consulta y cruce.</span><span class="sxs-lookup"><span data-stu-id="fd863-117">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="fd863-118">En este artículo describiremos algunos ejemplos para que comience a trabajar con Gremlin.</span><span class="sxs-lookup"><span data-stu-id="fd863-118">We cover a few examples in this article to get your started with Gremlin.</span></span> <span data-ttu-id="fd863-119">Consulte las [consultas de Gremlin](gremlin-support.md) para un tutorial detallado de las funcionalidades de Gremlin disponibles en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fd863-119">See [Gremlin queries](gremlin-support.md) for a detailed walkthrough of Gremlin capabilities available in Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fd863-120">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fd863-120">Prerequisites</span></span>
<span data-ttu-id="fd863-121">Asegúrese de que dispone de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fd863-121">Please make sure you have the following:</span></span>

* <span data-ttu-id="fd863-122">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="fd863-122">An active Azure account.</span></span> <span data-ttu-id="fd863-123">Si no tiene una, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="fd863-123">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="fd863-124">Como alternativa, puede usar el [Emulador de Azure DocumentDB](local-emulator.md) en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="fd863-124">Alternatively, you can use the [Azure DocumentDB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="fd863-125">[Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="fd863-125">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-database-account"></a><span data-ttu-id="fd863-126">Creación de una cuenta de base de datos</span><span class="sxs-lookup"><span data-stu-id="fd863-126">Create database account</span></span>

<span data-ttu-id="fd863-127">Para comenzar, creemos una cuenta de Azure Cosmos DB en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="fd863-127">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="fd863-128">¿Ya tiene una cuenta de Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="fd863-128">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="fd863-129">Si es así, vaya a [Configuración de la solución de Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="fd863-129">If so, skip ahead to [Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="fd863-130">¿Ya tenía una cuenta de Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="fd863-130">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="fd863-131">Si es así, ahora es una cuenta de Azure Cosmos DB, por lo que puede ir directamente a [Configuración de la solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="fd863-131">If so, your account is now an Azure Cosmos DB account and you can skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="fd863-132">Si usa el Emulador de Azure Cosmos DB, siga los pasos que se indican en [Emulador de Azure Cosmos DB](local-emulator.md) para configurar el emulador y vaya directamente a [Configuración de la solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="fd863-132">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <span data-ttu-id="fd863-133"><a id="SetupVS"></a>Configuración de la solución de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fd863-133"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="fd863-134">Abra **Visual Studio** en el equipo.</span><span class="sxs-lookup"><span data-stu-id="fd863-134">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="fd863-135">En el menú **Archivo**, seleccione **Nuevo** y elija **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="fd863-135">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="fd863-136">En el cuadro de diálogo **Nuevo proyecto**, seleccione **Plantillas** / **Visual C#** / **Aplicación de consola (.NET Framework)**, asigne un nombre al proyecto y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fd863-136">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
4. <span data-ttu-id="fd863-137">En el **Explorador de soluciones**, haga clic con el botón derecho en la nueva aplicación de la consola, que se encuentra en la solución de Visual Studio y, a continuación, haga clic en **Administrar paquetes NuGet...**</span><span class="sxs-lookup"><span data-stu-id="fd863-137">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
5. <span data-ttu-id="fd863-138">En la pestaña **NuGet**, haga clic en **Examinar** y escriba **Microsoft.Azure.Graphs** en el cuadro de búsqueda y active la opción **Incluir versiones preliminares**.</span><span class="sxs-lookup"><span data-stu-id="fd863-138">In the **NuGet** tab, click **Browse**, and type **Microsoft.Azure.Graphs** in the search box, and check the **Include prerelease versions**.</span></span>
6. <span data-ttu-id="fd863-139">En los resultados, busque **Microsoft.Azure.Graphs** y haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="fd863-139">Within the results, find **Microsoft.Azure.Graphs** and click **Install**.</span></span>
   
   <span data-ttu-id="fd863-140">Si recibe un mensaje sobre cómo revisar los cambios en la solución, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fd863-140">If you get a message about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="fd863-141">Si recibe un mensaje acerca de la aceptación de licencia, haga clic en **Acepto**.</span><span class="sxs-lookup"><span data-stu-id="fd863-141">If you get a message about license acceptance, click **I accept**.</span></span>
   
    <span data-ttu-id="fd863-142">La biblioteca `Microsoft.Azure.Graphs` proporciona un método de extensión único `CreateGremlinQuery<T>` para ejecutar operaciones de Gremlin.</span><span class="sxs-lookup"><span data-stu-id="fd863-142">The `Microsoft.Azure.Graphs` library provides a single extension method `CreateGremlinQuery<T>` for executing Gremlin operations.</span></span> <span data-ttu-id="fd863-143">Gremlin es un lenguaje de programación funcional que admite operaciones de escritura (DML) y operaciones de consulta y cruce.</span><span class="sxs-lookup"><span data-stu-id="fd863-143">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="fd863-144">En este artículo describiremos algunos ejemplos para que comience a trabajar con Gremlin.</span><span class="sxs-lookup"><span data-stu-id="fd863-144">We cover a few examples in this article to get your started with Gremlin.</span></span> <span data-ttu-id="fd863-145">El artículo sobre las [consultas de Gremlin](gremlin-support.md) ofrece un tutorial detallado de las funcionalidades de Gremlin en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fd863-145">[Gremlin queries](gremlin-support.md) has a detailed walkthrough of Gremlin capabilities in Azure Cosmos DB.</span></span>

## <span data-ttu-id="fd863-146"><a id="add-references"></a>Conexión de la aplicación</span><span class="sxs-lookup"><span data-stu-id="fd863-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="fd863-147">Agregue estas dos constantes y la variable *client* en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fd863-147">Add these two constants and your *client* variable in your application.</span></span> 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
<span data-ttu-id="fd863-148">A continuación, vuelva a [Azure Portal](https://portal.azure.com) para recuperar la dirección URL del punto de conexión y la clave principal.</span><span class="sxs-lookup"><span data-stu-id="fd863-148">Next, head back to the [Azure portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="fd863-149">La dirección URL del punto de conexión y la clave principal son necesarias para que la aplicación sepa a dónde debe conectarse y para que Azure Cosmos DB confíe en la conexión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fd863-149">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span> 

<span data-ttu-id="fd863-150">En Azure Portal, vaya a la cuenta de Azure Cosmos DB, haga clic en **Claves** y, luego, en **Claves de lectura y escritura**.</span><span class="sxs-lookup"><span data-stu-id="fd863-150">In the Azure portal, navigate to your Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span> 

<span data-ttu-id="fd863-151">Copie el URI desde el portal y péguelo en `Endpoint` en la propiedad de punto de conexión anterior.</span><span class="sxs-lookup"><span data-stu-id="fd863-151">Copy the URI from the portal and paste it over `Endpoint` in the endpoint property above.</span></span> <span data-ttu-id="fd863-152">Luego copie la CLAVE PRINCIPAL del portal y péguela en la propiedad `AuthKey` anterior.</span><span class="sxs-lookup"><span data-stu-id="fd863-152">Then copy the PRIMARY KEY from the portal and paste it into the `AuthKey` property above.</span></span> 

<span data-ttu-id="fd863-153">![Captura de pantalla de Azure Portal usada por el tutorial para crear una aplicación de C#.</span><span class="sxs-lookup"><span data-stu-id="fd863-153">![Screen shot of the Azure portal used by the tutorial to create a C# application.</span></span> <span data-ttu-id="fd863-154">Muestra una cuenta de Azure Cosmos DB, con el botón CLAVES resaltado en la navegación de Azure Cosmos DB y los valores de URI y PRIMARY KEY resaltados en la hoja Claves][claves]</span><span class="sxs-lookup"><span data-stu-id="fd863-154">Shows an Azure Cosmos DB account the KEYS button highlighted on the Azure Cosmos DB navigation , and the URI and PRIMARY KEY values highlighted on the Keys blade][keys]</span></span> 
 
## <span data-ttu-id="fd863-155"><a id="instantiate"></a>Creación de instancia de DocumentClient</span><span class="sxs-lookup"><span data-stu-id="fd863-155"><a id="instantiate"></a>Instantiate the DocumentClient</span></span> 
<span data-ttu-id="fd863-156">A continuación, cree una instancia nueva de **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="fd863-156">Next, create a new instance of the **DocumentClient**.</span></span>  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <span data-ttu-id="fd863-157"><a id="create-database"></a>Creación de una base de datos</span><span class="sxs-lookup"><span data-stu-id="fd863-157"><a id="create-database"></a>Create a database</span></span> 

<span data-ttu-id="fd863-158">Ahora cree una [base de datos](documentdb-resources.md#databases) de Azure Cosmos DB con el método [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) o el método [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) de la clase **DocumentClient** desde el [SDK de .NET de DocumentDB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="fd863-158">Now, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class from the [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span>  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a><span data-ttu-id="fd863-159">Creación de un grafo</span><span class="sxs-lookup"><span data-stu-id="fd863-159">Create a graph</span></span> 

<span data-ttu-id="fd863-160">A continuación, cree un contenedor de grafos a través del método [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) o el método [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) de la clase **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="fd863-160">Next, create a graph container by using the using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="fd863-161">Una colección es un contenedor de entidades de grafo.</span><span class="sxs-lookup"><span data-stu-id="fd863-161">A collection is a container of graph entities.</span></span> 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <span data-ttu-id="fd863-162"><a id="serializing"></a>Serialización de vértices y bordes en objetos .NET</span><span class="sxs-lookup"><span data-stu-id="fd863-162"><a id="serializing"></a>Serialize vertices and edges to .NET objects</span></span>
<span data-ttu-id="fd863-163">Azure Cosmos DB usa el [formato GraphSON](gremlin-support.md), que define un esquema JSON para los vértices, los bordes y las propiedades.</span><span class="sxs-lookup"><span data-stu-id="fd863-163">Azure Cosmos DB uses the [GraphSON wire format](gremlin-support.md), which defines a JSON schema for vertices, edges, and properties.</span></span> <span data-ttu-id="fd863-164">El SDK de .NET de Azure Cosmos DB incluye JSON.NET como dependencia, lo que nos permite serializar/deserializar GraphSON en objetos .NET con los que podemos trabajar en el código.</span><span class="sxs-lookup"><span data-stu-id="fd863-164">The Azure Cosmos DB .NET SDK includes JSON.NET as a dependency, and this allows us to serialize/deserialize GraphSON into .NET objects that we can work with in code.</span></span>

<span data-ttu-id="fd863-165">Como ejemplo, vamos a trabajar con una red social sencilla con cuatro personas.</span><span class="sxs-lookup"><span data-stu-id="fd863-165">As an example, let's work with a simple social network with four people.</span></span> <span data-ttu-id="fd863-166">Veremos cómo crear vértices `Person`, agregar relaciones `Knows` entre ellos y, luego, consultar y cruzar el grafo para encontrar relaciones "de amigos de amigos".</span><span class="sxs-lookup"><span data-stu-id="fd863-166">We look at how to create `Person` vertices, add `Knows` relationships between them, then query and traverse the graph to find "friend of friend" relationships.</span></span> 

<span data-ttu-id="fd863-167">El espacio de nombres `Microsoft.Azure.Graphs.Elements` proporciona las clases `Vertex`, `Edge`, `Property` y `VertexProperty` para deserializar las respuestas de GraphSON en objetos .NET bien definidos.</span><span class="sxs-lookup"><span data-stu-id="fd863-167">The `Microsoft.Azure.Graphs.Elements` namespace provides `Vertex`, `Edge`, `Property` and `VertexProperty` classes for deserializing GraphSON responses to well-defined .NET objects.</span></span>

## <a name="run-gremlin-using-creategremlinquery"></a><span data-ttu-id="fd863-168">Ejecución de Gremlin con CreateGremlinQuery</span><span class="sxs-lookup"><span data-stu-id="fd863-168">Run Gremlin using CreateGremlinQuery</span></span>
<span data-ttu-id="fd863-169">Al igual que SQL, Gremlin admite operaciones de lectura, escritura y consulta.</span><span class="sxs-lookup"><span data-stu-id="fd863-169">Gremlin, like SQL, supports read, write, and query operations.</span></span> <span data-ttu-id="fd863-170">Por ejemplo, el siguiente fragmento de código muestra cómo crear vértices y bordes; haga algunas consultas de ejemplo con `CreateGremlinQuery<T>` e itere de manera asincrónica en estos resultados con `ExecuteNextAsync` y \`HasMoreResults.</span><span class="sxs-lookup"><span data-stu-id="fd863-170">For example, the following snippet shows how to create vertices, edges, perform some sample queries using `CreateGremlinQuery<T>`, and asynchronously iterate through these results using `ExecuteNextAsync` and \`HasMoreResults.</span></span>

```cs
Dictionary<string, string> gremlinQueries = new Dictionary<string, string>
{
    { "Cleanup",        "g.V().drop()" },
    { "AddVertex 1",    "g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44)" },
    { "AddVertex 2",    "g.addV('person').property('id', 'mary').property('firstName', 'Mary').property('lastName', 'Andersen').property('age', 39)" },
    { "AddVertex 3",    "g.addV('person').property('id', 'ben').property('firstName', 'Ben').property('lastName', 'Miller')" },
    { "AddVertex 4",    "g.addV('person').property('id', 'robin').property('firstName', 'Robin').property('lastName', 'Wakefield')" },
    { "AddEdge 1",      "g.V('thomas').addE('knows').to(g.V('mary'))" },
    { "AddEdge 2",      "g.V('thomas').addE('knows').to(g.V('ben'))" },
    { "AddEdge 3",      "g.V('ben').addE('knows').to(g.V('robin'))" },
    { "UpdateVertex",   "g.V('thomas').property('age', 44)" },
    { "CountVertices",  "g.V().count()" },
    { "Filter Range",   "g.V().hasLabel('person').has('age', gt(40))" },
    { "Project",        "g.V().hasLabel('person').values('firstName')" },
    { "Sort",           "g.V().hasLabel('person').order().by('firstName', decr)" },
    { "Traverse",       "g.V('thomas').outE('knows').inV().hasLabel('person')" },
    { "Traverse 2x",    "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')" },
    { "Loop",           "g.V('thomas').repeat(out()).until(has('id', 'robin')).path()" },
    { "DropEdge",       "g.V('thomas').outE('knows').where(inV().has('id', 'mary')).drop()" },
    { "CountEdges",     "g.E().count()" },
    { "DropVertex",     "g.V('thomas').drop()" },
};

foreach (KeyValuePair<string, string> gremlinQuery in gremlinQueries)
{
    Console.WriteLine($"Running {gremlinQuery.Key}: {gremlinQuery.Value}");

    // The CreateGremlinQuery method extensions allow you to execute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, gremlinQuery.Value);
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    Console.WriteLine();
}
```

## <a name="add-vertices-and-edges"></a><span data-ttu-id="fd863-171">Incorporación de vértices y bordes</span><span class="sxs-lookup"><span data-stu-id="fd863-171">Add vertices and edges</span></span>

<span data-ttu-id="fd863-172">Analicemos más detalladamente las instrucciones Gremlin mostradas en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="fd863-172">Let's look at the Gremlin statements shown in the preceding section more detail.</span></span> <span data-ttu-id="fd863-173">En primer lugar, creamos algunos vértices con el método `addV` de Gremlin.</span><span class="sxs-lookup"><span data-stu-id="fd863-173">First we some vertices using Gremlin's `addV` method.</span></span> <span data-ttu-id="fd863-174">Por ejemplo, el fragmento de código siguiente crea un vértice "Thomas Andersen" de tipo "Persona", con propiedades como nombre, apellido y edad.</span><span class="sxs-lookup"><span data-stu-id="fd863-174">For example, the following snippet creates a "Thomas Andersen" vertex of type "Person", with properties for first name, last name, and age.</span></span>

```cs
// Create a vertex
IDocumentQuery<Vertex> createVertexQuery = client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.addV('person').property('firstName', 'Thomas')");

while (createVertexQuery.HasMoreResults)
{
    Vertex thomas = (await create.ExecuteNextAsync<Vertex>()).First();
}
```

<span data-ttu-id="fd863-175">Luego cree algunos bordes entre estos vértices con el método `addE` de Gremlin.</span><span class="sxs-lookup"><span data-stu-id="fd863-175">Then we create some edges between these vertices using Gremlin's `addE` method.</span></span> 

```cs
// Add a "knows" edge
IDocumentQuery<Edge> createEdgeQuery = client.CreateGremlinQuery<Edge>(
    graphCollection, 
    "g.V('thomas').addE('knows').to(g.V('mary'))");

while (create.HasMoreResults)
{
    Edge thomasKnowsMaryEdge = (await create.ExecuteNextAsync<Edge>()).First();
}
```

<span data-ttu-id="fd863-176">Podemos usar el paso `properties` en Gremlin para actualizar un vértice existente.</span><span class="sxs-lookup"><span data-stu-id="fd863-176">We can update an existing vertex by using `properties` step in Gremlin.</span></span> <span data-ttu-id="fd863-177">Omitimos la llamada para ejecutar la consulta vía `HasMoreResults` y `ExecuteNextAsync` para el resto de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="fd863-177">We skip the call to execute the query via `HasMoreResults` and `ExecuteNextAsync` for the rest of the examples.</span></span>

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

<span data-ttu-id="fd863-178">Puede quitar bordes y vértices con el paso `drop` de Gremlin.</span><span class="sxs-lookup"><span data-stu-id="fd863-178">You can drop edges and vertices using Gremlin's `drop` step.</span></span> <span data-ttu-id="fd863-179">El siguiente es un fragmento de código que muestra cómo eliminar un vértice y un borde.</span><span class="sxs-lookup"><span data-stu-id="fd863-179">Here's a snippet that shows how to delete a vertex and an edge.</span></span> <span data-ttu-id="fd863-180">Tenga en cuenta que eliminar un vértice genera una reacción en cadena de eliminaciones de los bordes asociados.</span><span class="sxs-lookup"><span data-stu-id="fd863-180">Note that dropping a vertex performs a cascading delete of the associated edges.</span></span>

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-the-graph"></a><span data-ttu-id="fd863-181">Consulta del grafo</span><span class="sxs-lookup"><span data-stu-id="fd863-181">Query the graph</span></span>

<span data-ttu-id="fd863-182">Puede realizar consultas y cruces también con Gremlin.</span><span class="sxs-lookup"><span data-stu-id="fd863-182">You can perform queries and traversals also using Gremlin.</span></span> <span data-ttu-id="fd863-183">Por ejemplo, en el siguiente fragmento de código se muestra cómo contar el número de vértices del grafo:</span><span class="sxs-lookup"><span data-stu-id="fd863-183">For example, the following snippet shows how to count the number of vertices in the graph:</span></span>

```cs
// Run a query to count vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
<span data-ttu-id="fd863-184">Puede aplicar filtros mediante los pasos `has` y `hasLabel` de Gremlin y combinarlos con `and`, `or` y `not` para crear filtros más complejos:</span><span class="sxs-lookup"><span data-stu-id="fd863-184">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` to build more complex filters:</span></span>

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

<span data-ttu-id="fd863-185">Puede proyectar determinadas propiedades en los resultados de la consulta mediante el paso `values`:</span><span class="sxs-lookup"><span data-stu-id="fd863-185">You can project certain properties in the query results using the `values` step:</span></span>

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

<span data-ttu-id="fd863-186">Hasta ahora, solo hemos visto operadores de consulta que funcionan en cualquier base de datos.</span><span class="sxs-lookup"><span data-stu-id="fd863-186">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="fd863-187">Los grafos son rápidos y eficientes para operaciones de cruce seguro si tiene que ir a bordes y vértices relacionados.</span><span class="sxs-lookup"><span data-stu-id="fd863-187">Graphs are fast and efficient for traversal operations when you need to navigate to related edges and vertices.</span></span> <span data-ttu-id="fd863-188">Encontremos a todos los amigos de Thomas.</span><span class="sxs-lookup"><span data-stu-id="fd863-188">Let's find all friends of Thomas.</span></span> <span data-ttu-id="fd863-189">Lo hacemos usando el paso `outE` de Gremlin para encontrar todos los bordes exteriores de Thomas y atravesando a continuación por los vértices interiores de esos bordes mediante el paso `inV` de Gremlin:</span><span class="sxs-lookup"><span data-stu-id="fd863-189">We do this by using Gremlin's `outE` step to find all the out-edges from Thomas, then traversing to the in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="fd863-190">La siguiente consulta realiza dos saltos para encontrar a todos los "amigos de los amigos" de Thomas, llamando a `outE` y `inV` dos veces.</span><span class="sxs-lookup"><span data-stu-id="fd863-190">The next query performs two hops to find all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="fd863-191">Puede crear consultas más complejas e implementar una lógica de cruce seguro del grafo eficaz con Gremlin, incluidas la combinación de expresiones de filtro, la realización de bucles mediante el paso `loop` y la implementación de la navegación condicional mediante el paso `choose`.</span><span class="sxs-lookup"><span data-stu-id="fd863-191">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using the `loop` step, and implementing conditional navigation using the `choose` step.</span></span> <span data-ttu-id="fd863-192">Obtenga más información sobre lo que puede hacer con [Compatibilidad con Gremlin](gremlin-support.md).</span><span class="sxs-lookup"><span data-stu-id="fd863-192">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

<span data-ttu-id="fd863-193">Eso es todo. Ya completó el tutorial de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fd863-193">That's it, this Azure Cosmos DB tutorial is complete!</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="fd863-194">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="fd863-194">Clean up resources</span></span>

<span data-ttu-id="fd863-195">Si no va a seguir usando esta aplicación, use los pasos siguientes para borrar todos los recursos que se crearon en este tutorial en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="fd863-195">If you're not going to continue to use this app, use the following steps to delete all resources created by this tutorial in the Azure portal.</span></span>  

1. <span data-ttu-id="fd863-196">En el menú de la izquierda de Azure Portal, haga clic en **Grupos de recursos** y en el nombre del recurso que creó.</span><span class="sxs-lookup"><span data-stu-id="fd863-196">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="fd863-197">En la página del grupo de recursos, haga clic en **Eliminar**, escriba en el cuadro de texto el nombre del recurso que quiere eliminar y haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="fd863-197">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd863-198">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fd863-198">Next Steps</span></span>

<span data-ttu-id="fd863-199">En este tutorial, ha hecho lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fd863-199">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fd863-200">Se creó una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fd863-200">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="fd863-201">Se creó un contenedor y una base de datos de grafo</span><span class="sxs-lookup"><span data-stu-id="fd863-201">Created a graph database and container</span></span>
> * <span data-ttu-id="fd863-202">Se serializaron vértices y bordes en objetos .NET</span><span class="sxs-lookup"><span data-stu-id="fd863-202">Serialized vertices and edges to .NET objects</span></span>
> * <span data-ttu-id="fd863-203">Se agregaron vértices y bordes</span><span class="sxs-lookup"><span data-stu-id="fd863-203">Added vertices and edges</span></span>
> * <span data-ttu-id="fd863-204">Se consultó el grafo con Gremlin</span><span class="sxs-lookup"><span data-stu-id="fd863-204">Queried the graph using Gremlin</span></span>

<span data-ttu-id="fd863-205">Ahora puede crear consultas más complejas e implementar con Gremlin una lógica de cruce seguro del grafo eficaz.</span><span class="sxs-lookup"><span data-stu-id="fd863-205">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="fd863-206">Consulta mediante Gremlin</span><span class="sxs-lookup"><span data-stu-id="fd863-206">Query using Gremlin</span></span>](tutorial-query-graph.md)
