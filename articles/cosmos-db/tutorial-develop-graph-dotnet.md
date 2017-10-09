---
title: 'Azure Cosmos DB: Desarrollar con hello API Graph en .NET | Documentos de Microsoft'
description: "Obtenga información acerca de cómo toodevelop con la API de documentos de Azure Cosmos DB con .NET"
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
ms.openlocfilehash: 12e435d8169aeee6e818dac4a3b66c7a0ec5f2d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-graph-api-in-net"></a><span data-ttu-id="e01ac-103">Azure Cosmos DB: Desarrollar con hello API Graph en .NET</span><span class="sxs-lookup"><span data-stu-id="e01ac-103">Azure Cosmos DB: Develop with hello Graph API in .NET</span></span>
<span data-ttu-id="e01ac-104">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e01ac-104">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="e01ac-105">Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente.</span><span class="sxs-lookup"><span data-stu-id="e01ac-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="e01ac-106">Este tutorial se muestra cómo toocreate una cuenta de base de datos de Azure Cosmos mediante Hola portal de Azure y cómo toocreate una base de datos de gráfico y el contenedor.</span><span class="sxs-lookup"><span data-stu-id="e01ac-106">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal and how toocreate a graph database and container.</span></span> <span data-ttu-id="e01ac-107">aplicación Hello, a continuación, crea una red social simple con cuatro personas que usan hello [API Graph](graph-sdk-dotnet.md) (vista previa), a continuación, recorre y consultas gráfico de hello utilizando Gremlin.</span><span class="sxs-lookup"><span data-stu-id="e01ac-107">hello application then creates a simple social network with four people using hello [Graph API](graph-sdk-dotnet.md) (preview), then traverses and queries hello graph using Gremlin.</span></span>

<span data-ttu-id="e01ac-108">Este tutorial trata Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="e01ac-108">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e01ac-109">Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e01ac-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="e01ac-110">Creación de un contenedor y una base de datos de grafo</span><span class="sxs-lookup"><span data-stu-id="e01ac-110">Create a graph database and container</span></span>
> * <span data-ttu-id="e01ac-111">Serializar objetos too.NET vértices y bordes</span><span class="sxs-lookup"><span data-stu-id="e01ac-111">Serialize vertices and edges too.NET objects</span></span>
> * <span data-ttu-id="e01ac-112">Incorporación de vértices y bordes</span><span class="sxs-lookup"><span data-stu-id="e01ac-112">Add vertices and edges</span></span>
> * <span data-ttu-id="e01ac-113">Gráfico de consultas hello mediante Gremlin</span><span class="sxs-lookup"><span data-stu-id="e01ac-113">Query hello graph using Gremlin</span></span>

## <a name="graphs-in-azure-cosmos-db"></a><span data-ttu-id="e01ac-114">Grafos en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e01ac-114">Graphs in Azure Cosmos DB</span></span>
<span data-ttu-id="e01ac-115">Puede usar base de datos de Azure Cosmos toocreate, actualización y gráficos de consultas usando hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) biblioteca.</span><span class="sxs-lookup"><span data-stu-id="e01ac-115">You can use Azure Cosmos DB toocreate, update, and query graphs using hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) library.</span></span> <span data-ttu-id="e01ac-116">biblioteca de Hello Microsoft.Azure.Graph proporciona un método de extensión único `CreateGremlinQuery<T>` sobre hello `DocumentClient` clase consultas de Gremlin tooexecute.</span><span class="sxs-lookup"><span data-stu-id="e01ac-116">hello Microsoft.Azure.Graph library provides a single extension method `CreateGremlinQuery<T>` on top of hello `DocumentClient` class tooexecute Gremlin queries.</span></span>

<span data-ttu-id="e01ac-117">Gremlin es un lenguaje de programación funcional que admite operaciones de escritura (DML) y operaciones de consulta y cruce.</span><span class="sxs-lookup"><span data-stu-id="e01ac-117">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="e01ac-118">Trataremos algunos ejemplos en este artículo tooget el que se inició con Gremlin.</span><span class="sxs-lookup"><span data-stu-id="e01ac-118">We cover a few examples in this article tooget your started with Gremlin.</span></span> <span data-ttu-id="e01ac-119">Consulte las [consultas de Gremlin](gremlin-support.md) para un tutorial detallado de las funcionalidades de Gremlin disponibles en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e01ac-119">See [Gremlin queries](gremlin-support.md) for a detailed walkthrough of Gremlin capabilities available in Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e01ac-120">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e01ac-120">Prerequisites</span></span>
<span data-ttu-id="e01ac-121">Asegúrese de que tiene Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="e01ac-121">Please make sure you have hello following:</span></span>

* <span data-ttu-id="e01ac-122">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="e01ac-122">An active Azure account.</span></span> <span data-ttu-id="e01ac-123">Si no tiene una, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="e01ac-123">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="e01ac-124">Como alternativa, puede usar hello [emulador de Azure DocumentDB](local-emulator.md) para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="e01ac-124">Alternatively, you can use hello [Azure DocumentDB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="e01ac-125">[Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="e01ac-125">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-database-account"></a><span data-ttu-id="e01ac-126">Creación de una cuenta de base de datos</span><span class="sxs-lookup"><span data-stu-id="e01ac-126">Create database account</span></span>

<span data-ttu-id="e01ac-127">Empecemos creando una cuenta de base de datos de Azure Cosmos Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e01ac-127">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="e01ac-128">¿Ya tiene una cuenta de Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="e01ac-128">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="e01ac-129">Si es así, pasar demasiado[configure su solución de Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="e01ac-129">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="e01ac-130">¿Ya tenía una cuenta de Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="e01ac-130">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="e01ac-131">En caso afirmativo, la cuenta es ahora una cuenta de base de datos de Azure Cosmos y puede saltarse lecciones demasiado[configure su solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="e01ac-131">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="e01ac-132">Si usas hello Azure Cosmos DB emulador, siga los pasos de hello en [emulador de base de datos de Azure Cosmos](local-emulator.md) toosetup Hola emulador y pase demasiado[configurar la solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="e01ac-132">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <span data-ttu-id="e01ac-133"><a id="SetupVS"></a>Configuración de la solución de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e01ac-133"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="e01ac-134">Abra **Visual Studio** en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e01ac-134">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="e01ac-135">En hello **archivo** menú, seleccione **New**y, a continuación, elija **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="e01ac-135">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="e01ac-136">Hola **nuevo proyecto** cuadro de diálogo, seleccione **plantillas** / **Visual C#** / **aplicación de consola (.NET Framework)**, denomine el proyecto y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e01ac-136">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
4. <span data-ttu-id="e01ac-137">Hola **el Explorador de soluciones**, haga clic con el botón secundario en la nueva aplicación de consola, que se encuentra en la solución de Visual Studio, y, a continuación, haga clic en **administrar paquetes de NuGet...**</span><span class="sxs-lookup"><span data-stu-id="e01ac-137">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
5. <span data-ttu-id="e01ac-138">Hola **NuGet** , haga clic en **examinar**y el tipo de **Microsoft.Azure.Graphs** en el cuadro de búsqueda de Hola y Hola de comprobación **incluyen versiones preliminares**.</span><span class="sxs-lookup"><span data-stu-id="e01ac-138">In hello **NuGet** tab, click **Browse**, and type **Microsoft.Azure.Graphs** in hello search box, and check hello **Include prerelease versions**.</span></span>
6. <span data-ttu-id="e01ac-139">En los resultados de hello, buscar **Microsoft.Azure.Graphs** y haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="e01ac-139">Within hello results, find **Microsoft.Azure.Graphs** and click **Install**.</span></span>
   
   <span data-ttu-id="e01ac-140">Si recibe un mensaje acerca de la revisión de la solución de toohello de cambios, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e01ac-140">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="e01ac-141">Si recibe un mensaje acerca de la aceptación de licencia, haga clic en **Acepto**.</span><span class="sxs-lookup"><span data-stu-id="e01ac-141">If you get a message about license acceptance, click **I accept**.</span></span>
   
    <span data-ttu-id="e01ac-142">Hola `Microsoft.Azure.Graphs` biblioteca proporciona un método de extensión único `CreateGremlinQuery<T>` para ejecutar operaciones de Gremlin.</span><span class="sxs-lookup"><span data-stu-id="e01ac-142">hello `Microsoft.Azure.Graphs` library provides a single extension method `CreateGremlinQuery<T>` for executing Gremlin operations.</span></span> <span data-ttu-id="e01ac-143">Gremlin es un lenguaje de programación funcional que admite operaciones de escritura (DML) y operaciones de consulta y cruce.</span><span class="sxs-lookup"><span data-stu-id="e01ac-143">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="e01ac-144">Trataremos algunos ejemplos en este artículo tooget el que se inició con Gremlin.</span><span class="sxs-lookup"><span data-stu-id="e01ac-144">We cover a few examples in this article tooget your started with Gremlin.</span></span> <span data-ttu-id="e01ac-145">El artículo sobre las [consultas de Gremlin](gremlin-support.md) ofrece un tutorial detallado de las funcionalidades de Gremlin en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e01ac-145">[Gremlin queries](gremlin-support.md) has a detailed walkthrough of Gremlin capabilities in Azure Cosmos DB.</span></span>

## <span data-ttu-id="e01ac-146"><a id="add-references"></a>Conexión de la aplicación</span><span class="sxs-lookup"><span data-stu-id="e01ac-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="e01ac-147">Agregue estas dos constantes y la variable *client* en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e01ac-147">Add these two constants and your *client* variable in your application.</span></span> 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
<span data-ttu-id="e01ac-148">A continuación, hacer copia de head toohello [portal de Azure](https://portal.azure.com) tooretrieve la dirección URL del extremo y la clave principal.</span><span class="sxs-lookup"><span data-stu-id="e01ac-148">Next, head back toohello [Azure portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="e01ac-149">dirección URL del extremo de Hola y clave principal son necesarios para su aplicación toounderstand donde tooconnect y para la base de datos de Azure Cosmos tootrust conexión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e01ac-149">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span> 

<span data-ttu-id="e01ac-150">Hola portal de Azure, navegar por la cuenta de base de datos de Azure Cosmos tooyour, haga clic en **claves**y, a continuación, haga clic en **claves de lectura y escritura**.</span><span class="sxs-lookup"><span data-stu-id="e01ac-150">In hello Azure portal, navigate tooyour Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span> 

<span data-ttu-id="e01ac-151">Copie Hola URI desde el portal de Hola y péguela sobre `Endpoint` en la propiedad de punto de conexión de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="e01ac-151">Copy hello URI from hello portal and paste it over `Endpoint` in hello endpoint property above.</span></span> <span data-ttu-id="e01ac-152">A continuación, copia Hola clave principal del portal de Hola y pegarlos en hello `AuthKey` propiedad anterior.</span><span class="sxs-lookup"><span data-stu-id="e01ac-152">Then copy hello PRIMARY KEY from hello portal and paste it into hello `AuthKey` property above.</span></span> 

<span data-ttu-id="e01ac-153">! [Captura de pantalla de hello portal de Azure usado por toocreate tutorial Hola una aplicación de C#.</span><span class="sxs-lookup"><span data-stu-id="e01ac-153">![Screen shot of hello Azure portal used by hello tutorial toocreate a C# application.</span></span> <span data-ttu-id="e01ac-154">Muestra un saludo de la cuenta de base de datos de Azure Cosmos botón claves resaltado en hello navegación de la base de datos de Azure Cosmos y valores URI y la clave principal de hello resaltan en hello hoja de claves] [keys]</span><span class="sxs-lookup"><span data-stu-id="e01ac-154">Shows an Azure Cosmos DB account hello KEYS button highlighted on hello Azure Cosmos DB navigation , and hello URI and PRIMARY KEY values highlighted on hello Keys blade][keys]</span></span> 
 
## <span data-ttu-id="e01ac-155"><a id="instantiate"></a>Crear una instancia de hello DocumentClient</span><span class="sxs-lookup"><span data-stu-id="e01ac-155"><a id="instantiate"></a>Instantiate hello DocumentClient</span></span> 
<span data-ttu-id="e01ac-156">A continuación, cree una nueva instancia de hello **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="e01ac-156">Next, create a new instance of hello **DocumentClient**.</span></span>  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <span data-ttu-id="e01ac-157"><a id="create-database"></a>Creación de una base de datos</span><span class="sxs-lookup"><span data-stu-id="e01ac-157"><a id="create-database"></a>Create a database</span></span> 

<span data-ttu-id="e01ac-158">A continuación, cree una base de datos de Azure Cosmos [base de datos](documentdb-resources.md#databases) mediante el uso de hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) método o [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) método de hello  **DocumentClient** clase a partir de hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="e01ac-158">Now, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class from hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span>  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a><span data-ttu-id="e01ac-159">Creación de un grafo</span><span class="sxs-lookup"><span data-stu-id="e01ac-159">Create a graph</span></span> 

<span data-ttu-id="e01ac-160">A continuación, crear un contenedor de gráficos mediante hello mediante hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) método o [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) método de hello **DocumentClient**  clase.</span><span class="sxs-lookup"><span data-stu-id="e01ac-160">Next, create a graph container by using hello using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="e01ac-161">Una colección es un contenedor de entidades de grafo.</span><span class="sxs-lookup"><span data-stu-id="e01ac-161">A collection is a container of graph entities.</span></span> 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <span data-ttu-id="e01ac-162"><a id="serializing"></a>Serializar objetos too.NET vértices y bordes</span><span class="sxs-lookup"><span data-stu-id="e01ac-162"><a id="serializing"></a>Serialize vertices and edges too.NET objects</span></span>
<span data-ttu-id="e01ac-163">Base de datos de Azure Cosmos usa hello [GraphSON formato](gremlin-support.md), que define un esquema JSON de vértices, bordes y propiedades.</span><span class="sxs-lookup"><span data-stu-id="e01ac-163">Azure Cosmos DB uses hello [GraphSON wire format](gremlin-support.md), which defines a JSON schema for vertices, edges, and properties.</span></span> <span data-ttu-id="e01ac-164">Hello Azure Cosmos DB .NET SDK incluye JSON.NET como una dependencia, y esto nos permite tooserialize/deserializar GraphSON en objetos .NET que podemos trabajar con en el código.</span><span class="sxs-lookup"><span data-stu-id="e01ac-164">hello Azure Cosmos DB .NET SDK includes JSON.NET as a dependency, and this allows us tooserialize/deserialize GraphSON into .NET objects that we can work with in code.</span></span>

<span data-ttu-id="e01ac-165">Como ejemplo, vamos a trabajar con una red social sencilla con cuatro personas.</span><span class="sxs-lookup"><span data-stu-id="e01ac-165">As an example, let's work with a simple social network with four people.</span></span> <span data-ttu-id="e01ac-166">Veremos cómo toocreate `Person` vértices, agregar `Knows` relaciones entre ellas, a continuación, consultar y recorrer las relaciones de hello gráfico toofind "friend de confianza".</span><span class="sxs-lookup"><span data-stu-id="e01ac-166">We look at how toocreate `Person` vertices, add `Knows` relationships between them, then query and traverse hello graph toofind "friend of friend" relationships.</span></span> 

<span data-ttu-id="e01ac-167">Hola `Microsoft.Azure.Graphs.Elements` espacio de nombres proporciona `Vertex`, `Edge`, `Property` y `VertexProperty` clases para deserializar los objetos de .NET definidos por el toowell de GraphSON las respuestas.</span><span class="sxs-lookup"><span data-stu-id="e01ac-167">hello `Microsoft.Azure.Graphs.Elements` namespace provides `Vertex`, `Edge`, `Property` and `VertexProperty` classes for deserializing GraphSON responses toowell-defined .NET objects.</span></span>

## <a name="run-gremlin-using-creategremlinquery"></a><span data-ttu-id="e01ac-168">Ejecución de Gremlin con CreateGremlinQuery</span><span class="sxs-lookup"><span data-stu-id="e01ac-168">Run Gremlin using CreateGremlinQuery</span></span>
<span data-ttu-id="e01ac-169">Al igual que SQL, Gremlin admite operaciones de lectura, escritura y consulta.</span><span class="sxs-lookup"><span data-stu-id="e01ac-169">Gremlin, like SQL, supports read, write, and query operations.</span></span> <span data-ttu-id="e01ac-170">Por ejemplo, hello fragmento de código siguiente muestra cómo toocreate vértices, bordes, realizan algunas consultas de ejemplo con `CreateGremlinQuery<T>`y asincrónica recorrer en iteración los resultados mediante `ExecuteNextAsync` y ' HasMoreResults.</span><span class="sxs-lookup"><span data-stu-id="e01ac-170">For example, hello following snippet shows how toocreate vertices, edges, perform some sample queries using `CreateGremlinQuery<T>`, and asynchronously iterate through these results using `ExecuteNextAsync` and \`HasMoreResults.</span></span>

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

    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
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

## <a name="add-vertices-and-edges"></a><span data-ttu-id="e01ac-171">Incorporación de vértices y bordes</span><span class="sxs-lookup"><span data-stu-id="e01ac-171">Add vertices and edges</span></span>

<span data-ttu-id="e01ac-172">Echemos un vistazo a las instrucciones de Gremlin Hola que se muestra en la sección anterior de hello más detalle.</span><span class="sxs-lookup"><span data-stu-id="e01ac-172">Let's look at hello Gremlin statements shown in hello preceding section more detail.</span></span> <span data-ttu-id="e01ac-173">En primer lugar, creamos algunos vértices con el método `addV` de Gremlin.</span><span class="sxs-lookup"><span data-stu-id="e01ac-173">First we some vertices using Gremlin's `addV` method.</span></span> <span data-ttu-id="e01ac-174">Por ejemplo, hello fragmento de código siguiente crea un vértice "Thomas Andersen" de tipo "Persona", con las propiedades de nombre, apellido y edad.</span><span class="sxs-lookup"><span data-stu-id="e01ac-174">For example, hello following snippet creates a "Thomas Andersen" vertex of type "Person", with properties for first name, last name, and age.</span></span>

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

<span data-ttu-id="e01ac-175">Luego cree algunos bordes entre estos vértices con el método `addE` de Gremlin.</span><span class="sxs-lookup"><span data-stu-id="e01ac-175">Then we create some edges between these vertices using Gremlin's `addE` method.</span></span> 

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

<span data-ttu-id="e01ac-176">Podemos usar el paso `properties` en Gremlin para actualizar un vértice existente.</span><span class="sxs-lookup"><span data-stu-id="e01ac-176">We can update an existing vertex by using `properties` step in Gremlin.</span></span> <span data-ttu-id="e01ac-177">Se omite la consulta de Hola Hola llamada tooexecute a través de `HasMoreResults` y `ExecuteNextAsync` para el resto de Hola de ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="e01ac-177">We skip hello call tooexecute hello query via `HasMoreResults` and `ExecuteNextAsync` for hello rest of hello examples.</span></span>

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

<span data-ttu-id="e01ac-178">Puede quitar bordes y vértices con el paso `drop` de Gremlin.</span><span class="sxs-lookup"><span data-stu-id="e01ac-178">You can drop edges and vertices using Gremlin's `drop` step.</span></span> <span data-ttu-id="e01ac-179">Este es un fragmento de código que muestra cómo toodelete un vértice y un borde.</span><span class="sxs-lookup"><span data-stu-id="e01ac-179">Here's a snippet that shows how toodelete a vertex and an edge.</span></span> <span data-ttu-id="e01ac-180">Tenga en cuenta que la eliminación de un vértice realiza una eliminación en cascada de hello había asociado bordes.</span><span class="sxs-lookup"><span data-stu-id="e01ac-180">Note that dropping a vertex performs a cascading delete of hello associated edges.</span></span>

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-hello-graph"></a><span data-ttu-id="e01ac-181">Gráfico de consultas Hola</span><span class="sxs-lookup"><span data-stu-id="e01ac-181">Query hello graph</span></span>

<span data-ttu-id="e01ac-182">Puede realizar consultas y cruces también con Gremlin.</span><span class="sxs-lookup"><span data-stu-id="e01ac-182">You can perform queries and traversals also using Gremlin.</span></span> <span data-ttu-id="e01ac-183">Por ejemplo, hello siguiente fragmento de código muestra cómo toocount Hola número de vértices en el gráfico de hello:</span><span class="sxs-lookup"><span data-stu-id="e01ac-183">For example, hello following snippet shows how toocount hello number of vertices in hello graph:</span></span>

```cs
// Run a query toocount vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
<span data-ttu-id="e01ac-184">Puede realizar filtros utilizando del Gremlin `has` y `hasLabel` los pasos y combinarlos con `and`, `or`, y `not` toobuild los filtros más complejos:</span><span class="sxs-lookup"><span data-stu-id="e01ac-184">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` toobuild more complex filters:</span></span>

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

<span data-ttu-id="e01ac-185">Puede proyectar ciertas propiedades de resultados de la consulta de hello mediante hello `values` paso:</span><span class="sxs-lookup"><span data-stu-id="e01ac-185">You can project certain properties in hello query results using hello `values` step:</span></span>

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

<span data-ttu-id="e01ac-186">Hasta ahora, solo hemos visto operadores de consulta que funcionan en cualquier base de datos.</span><span class="sxs-lookup"><span data-stu-id="e01ac-186">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="e01ac-187">Gráficos son rápidos y eficaces para las operaciones de recorrido cuando necesite toonavigate toorelated bordes y vértices.</span><span class="sxs-lookup"><span data-stu-id="e01ac-187">Graphs are fast and efficient for traversal operations when you need toonavigate toorelated edges and vertices.</span></span> <span data-ttu-id="e01ac-188">Encontremos a todos los amigos de Thomas.</span><span class="sxs-lookup"><span data-stu-id="e01ac-188">Let's find all friends of Thomas.</span></span> <span data-ttu-id="e01ac-189">Hacer esto mediante el uso del Gremlin `outE` paso toofind Hola todos los out-bordes de Thomas, a continuación, recorrer toohello vértices respecto a los bordes del Gremlin `inV` paso:</span><span class="sxs-lookup"><span data-stu-id="e01ac-189">We do this by using Gremlin's `outE` step toofind all hello out-edges from Thomas, then traversing toohello in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="e01ac-190">realiza la siguiente consulta de Hello toofind de dos saltos todos "Amigos de amigos" de Thomas, mediante una llamada a `outE` y `inV` dos veces.</span><span class="sxs-lookup"><span data-stu-id="e01ac-190">hello next query performs two hops toofind all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="e01ac-191">Puede crear consultas más complejas e implementar lógica de cruce seguro de gráfico eficaz mediante Gremlin, filtro de combinación incluido Hola de expresiones, realizar el bucle con `loop` paso y la implementación de navegación condicional mediante hello `choose` paso.</span><span class="sxs-lookup"><span data-stu-id="e01ac-191">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using hello `loop` step, and implementing conditional navigation using hello `choose` step.</span></span> <span data-ttu-id="e01ac-192">Obtenga más información sobre lo que puede hacer con [Compatibilidad con Gremlin](gremlin-support.md).</span><span class="sxs-lookup"><span data-stu-id="e01ac-192">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

<span data-ttu-id="e01ac-193">Eso es todo. Ya completó el tutorial de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e01ac-193">That's it, this Azure Cosmos DB tutorial is complete!</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="e01ac-194">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="e01ac-194">Clean up resources</span></span>

<span data-ttu-id="e01ac-195">Si no va toocontinue toouse esta aplicación, utilice Hola después toodelete pasos todos los recursos creados por este tutorial Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e01ac-195">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span>  

1. <span data-ttu-id="e01ac-196">En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="e01ac-196">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="e01ac-197">En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="e01ac-197">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e01ac-198">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e01ac-198">Next Steps</span></span>

<span data-ttu-id="e01ac-199">En este tutorial, ha hecho siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="e01ac-199">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e01ac-200">Se creó una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e01ac-200">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="e01ac-201">Se creó un contenedor y una base de datos de grafo</span><span class="sxs-lookup"><span data-stu-id="e01ac-201">Created a graph database and container</span></span>
> * <span data-ttu-id="e01ac-202">Objetos serializados de too.NET de vértices y bordes</span><span class="sxs-lookup"><span data-stu-id="e01ac-202">Serialized vertices and edges too.NET objects</span></span>
> * <span data-ttu-id="e01ac-203">Se agregaron vértices y bordes</span><span class="sxs-lookup"><span data-stu-id="e01ac-203">Added vertices and edges</span></span>
> * <span data-ttu-id="e01ac-204">Gráfico de hello consultado mediante Gremlin</span><span class="sxs-lookup"><span data-stu-id="e01ac-204">Queried hello graph using Gremlin</span></span>

<span data-ttu-id="e01ac-205">Ahora puede crear consultas más complejas e implementar con Gremlin una lógica eficaz de recorrido del grafo.</span><span class="sxs-lookup"><span data-stu-id="e01ac-205">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="e01ac-206">Consulta mediante Gremlin</span><span class="sxs-lookup"><span data-stu-id="e01ac-206">Query using Gremlin</span></span>](tutorial-query-graph.md)
