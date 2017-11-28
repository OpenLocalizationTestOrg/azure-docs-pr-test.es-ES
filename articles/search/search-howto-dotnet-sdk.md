---
title: "aaaHow toouse búsqueda de Azure desde una aplicación .NET | Documentos de Microsoft"
description: "Cómo toouse Azure buscar desde una aplicación .NET"
services: search
documentationcenter: 
author: brjohnstmsft
manager: jlembicz
editor: 
ms.assetid: 93653341-c05f-4cfd-be45-bb877f964fcb
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 8e13fbe5549547d65941b856ce5a90611261388f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-search-from-a-net-application"></a><span data-ttu-id="72f02-103">Cómo toouse Azure buscar desde una aplicación .NET</span><span class="sxs-lookup"><span data-stu-id="72f02-103">How toouse Azure Search from a .NET Application</span></span>
<span data-ttu-id="72f02-104">Este artículo es un tutorial tooget, activos y en funcionamiento con hello [SDK de .NET de búsqueda de Azure](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="72f02-104">This article is a walkthrough tooget you up and running with hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span> <span data-ttu-id="72f02-105">Puede usar Hola .NET SDK tooimplement una rica experiencia de búsqueda en la aplicación con búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="72f02-105">You can use hello .NET SDK tooimplement a rich search experience in your application using Azure Search.</span></span>

## <a name="whats-in-hello-azure-search-sdk"></a><span data-ttu-id="72f02-106">¿Qué es Hola búsqueda de Azure SDK</span><span class="sxs-lookup"><span data-stu-id="72f02-106">What's in hello Azure Search SDK</span></span>
<span data-ttu-id="72f02-107">Hello SDK está formado por una biblioteca de cliente, `Microsoft.Azure.Search`.</span><span class="sxs-lookup"><span data-stu-id="72f02-107">hello SDK consists of a client library, `Microsoft.Azure.Search`.</span></span> <span data-ttu-id="72f02-108">Permite toomanage los índices, los orígenes de datos y los indizadores, así como cargar y administrar documentos y ejecutar las consultas, todo ello sin necesidad de toodeal con detalles de Hola de HTTP y JSON.</span><span class="sxs-lookup"><span data-stu-id="72f02-108">It enables you toomanage your indexes, data sources, and indexers, as well as upload and manage documents, and execute queries, all without having toodeal with hello details of HTTP and JSON.</span></span>

<span data-ttu-id="72f02-109">biblioteca de cliente de Hello define clases como `Index`, `Field`, y `Document`, así como las operaciones como `Indexes.Create` y `Documents.Search` en hello `SearchServiceClient` y `SearchIndexClient` clases.</span><span class="sxs-lookup"><span data-stu-id="72f02-109">hello client library defines classes like `Index`, `Field`, and `Document`, as well as operations like `Indexes.Create` and `Documents.Search` on hello `SearchServiceClient` and `SearchIndexClient` classes.</span></span> <span data-ttu-id="72f02-110">Estas clases se organizan en hello después de los espacios de nombres:</span><span class="sxs-lookup"><span data-stu-id="72f02-110">These classes are organized into hello following namespaces:</span></span>

* [<span data-ttu-id="72f02-111">Microsoft.Azure.Search</span><span class="sxs-lookup"><span data-stu-id="72f02-111">Microsoft.Azure.Search</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [<span data-ttu-id="72f02-112">Microsoft.Azure.Search.Models</span><span class="sxs-lookup"><span data-stu-id="72f02-112">Microsoft.Azure.Search.Models</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

<span data-ttu-id="72f02-113">versión actual de Hola de hello SDK de .NET de búsqueda de Azure ahora es disponible con carácter general.</span><span class="sxs-lookup"><span data-stu-id="72f02-113">hello current version of hello Azure Search .NET SDK is now generally available.</span></span> <span data-ttu-id="72f02-114">Si desea que tooprovide comentarios nos tooincorporate en la versión siguiente de hello, visite nuestro [página de comentarios](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="72f02-114">If you would like tooprovide feedback for us tooincorporate in hello next version, please visit our [feedback page](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

<span data-ttu-id="72f02-115">Hola .NET SDK es compatible con la versión `2016-09-01` de hello [API de REST de búsqueda de Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="72f02-115">hello .NET SDK supports version `2016-09-01` of hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span> <span data-ttu-id="72f02-116">Esta versión incluye ahora compatibilidad con analizadores personalizados y con el indexador de Azure Blob y Azure Table.</span><span class="sxs-lookup"><span data-stu-id="72f02-116">This version now includes support for custom analyzers and Azure Blob and Azure Table indexer support.</span></span> <span data-ttu-id="72f02-117">Obtener una vista previa de características que están *no* parte de esta versión, como la posibilidad de indizar archivos CSV y JSON, que se encuentran en [vista previa](search-api-2015-02-28-preview.md) y están disponibles a través de hello anterior [versión 2.0-versión preliminar de hello SDK para .NET ](https://aka.ms/search-sdk-preview).</span><span class="sxs-lookup"><span data-stu-id="72f02-117">Preview features that are *not* part of this version, such as support for indexing JSON and CSV files, are in [preview](search-api-2015-02-28-preview.md) and available via hello older [2.0-preview version of hello .NET SDK](https://aka.ms/search-sdk-preview).</span></span>

<span data-ttu-id="72f02-118">Este SDK no admite [operaciones de administración](https://docs.microsoft.com/rest/api/searchmanagement/) como la creación y el escalado de servicios de Search y las claves de API de administración.</span><span class="sxs-lookup"><span data-stu-id="72f02-118">This SDK does not support [Management Operations](https://docs.microsoft.com/rest/api/searchmanagement/) such as creating and scaling Search services and managing API keys.</span></span> <span data-ttu-id="72f02-119">Si necesita toomanage los recursos de búsqueda desde una aplicación. NET, puede usar hello [.NET SDK de administración de búsqueda de Azure](https://aka.ms/search-mgmt-sdk).</span><span class="sxs-lookup"><span data-stu-id="72f02-119">If you need toomanage your Search resources from a .NET application, you can use hello [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span></span>

## <a name="upgrading-toohello-latest-version-of-hello-sdk"></a><span data-ttu-id="72f02-120">Actualización de versión más reciente de toohello de hello SDK</span><span class="sxs-lookup"><span data-stu-id="72f02-120">Upgrading toohello latest version of hello SDK</span></span>
<span data-ttu-id="72f02-121">Si ya está usando una versión anterior de hello SDK de .NET de búsqueda de Azure y le gustaría tooupgrade toohello versión disponible con carácter general nueva, [este artículo](search-dotnet-sdk-migration.md) explica cómo.</span><span class="sxs-lookup"><span data-stu-id="72f02-121">If you're already using an older version of hello Azure Search .NET SDK and you'd like tooupgrade toohello new generally available version, [this article](search-dotnet-sdk-migration.md) explains how.</span></span>

## <a name="requirements-for-hello-sdk"></a><span data-ttu-id="72f02-122">Requisitos para hello SDK</span><span class="sxs-lookup"><span data-stu-id="72f02-122">Requirements for hello SDK</span></span>
1. <span data-ttu-id="72f02-123">Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="72f02-123">Visual Studio 2017.</span></span>
2. <span data-ttu-id="72f02-124">Su propio servicio Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="72f02-124">Your own Azure Search service.</span></span> <span data-ttu-id="72f02-125">Hola de orden toouse SDK, necesitará nombre hello del servicio y una o varias claves de API.</span><span class="sxs-lookup"><span data-stu-id="72f02-125">In order toouse hello SDK, you will need hello name of your service and one or more API keys.</span></span> <span data-ttu-id="72f02-126">[Crear un servicio en el portal de hello](search-create-service-portal.md) le ayudará a través de estos pasos.</span><span class="sxs-lookup"><span data-stu-id="72f02-126">[Create a service in hello portal](search-create-service-portal.md) will help you through these steps.</span></span>
3. <span data-ttu-id="72f02-127">Descargar SDK de .NET de búsqueda de Azure de hello [paquete NuGet](http://www.nuget.org/packages/Microsoft.Azure.Search) mediante el uso de "Administrar paquetes de NuGet" en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="72f02-127">Download hello Azure Search .NET SDK [NuGet package](http://www.nuget.org/packages/Microsoft.Azure.Search) by using "Manage NuGet Packages" in Visual Studio.</span></span> <span data-ttu-id="72f02-128">Busque el nombre del paquete de hello `Microsoft.Azure.Search` en NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="72f02-128">Just search for hello package name `Microsoft.Azure.Search` on NuGet.org.</span></span>

<span data-ttu-id="72f02-129">Hola SDK de .NET de búsqueda de Azure es compatible con las aplicaciones dirigidas a .NET Framework 4.6 hello y .NET Core.</span><span class="sxs-lookup"><span data-stu-id="72f02-129">hello Azure Search .NET SDK supports applications targeting hello .NET Framework 4.6 and .NET Core.</span></span>

## <a name="core-scenarios"></a><span data-ttu-id="72f02-130">Escenarios principales</span><span class="sxs-lookup"><span data-stu-id="72f02-130">Core scenarios</span></span>
<span data-ttu-id="72f02-131">Hay varias cosas que debe toodo en la aplicación de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="72f02-131">There are several things you'll need toodo in your search application.</span></span> <span data-ttu-id="72f02-132">En este tutorial, hablaremos sobre estos escenarios básicos:</span><span class="sxs-lookup"><span data-stu-id="72f02-132">In this tutorial, we'll cover these core scenarios:</span></span>

* <span data-ttu-id="72f02-133">Creación de un índice</span><span class="sxs-lookup"><span data-stu-id="72f02-133">Creating an index</span></span>
* <span data-ttu-id="72f02-134">Rellenar índice Hola con documentos</span><span class="sxs-lookup"><span data-stu-id="72f02-134">Populating hello index with documents</span></span>
* <span data-ttu-id="72f02-135">Búsqueda de documentos mediante filtros y búsqueda de texto completo</span><span class="sxs-lookup"><span data-stu-id="72f02-135">Searching for documents using full-text search and filters</span></span>

<span data-ttu-id="72f02-136">código de ejemplo de Hola que sigue muestra cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="72f02-136">hello sample code that follows illustrates each of these.</span></span> <span data-ttu-id="72f02-137">Sentirse fragmentos de código de hello toouse disponible en su propia aplicación.</span><span class="sxs-lookup"><span data-stu-id="72f02-137">Feel free toouse hello code snippets in your own application.</span></span>

### <a name="overview"></a><span data-ttu-id="72f02-138">Información general</span><span class="sxs-lookup"><span data-stu-id="72f02-138">Overview</span></span>
<span data-ttu-id="72f02-139">Hola se le pueden explorar de aplicación de ejemplo crea un nuevo índice con el nombre "hoteles", se rellena con algunos documentos, a continuación, ejecuta algunas consultas de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="72f02-139">hello sample application we'll be exploring creates a new index named "hotels", populates it with a few documents, then executes some search queries.</span></span> <span data-ttu-id="72f02-140">Este es el programa principal hello, que muestra Hola flujo general:</span><span class="sxs-lookup"><span data-stu-id="72f02-140">Here is hello main program, showing hello overall flow:</span></span>

```csharp
// This sample shows how toodelete, create, upload documents and query an index
static void Main(string[] args)
{
    IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
    IConfigurationRoot configuration = builder.Build();

    SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

    Console.WriteLine("{0}", "Deleting index...\n");
    DeleteHotelsIndexIfExists(serviceClient);

    Console.WriteLine("{0}", "Creating index...\n");
    CreateHotelsIndex(serviceClient);

    ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

    Console.WriteLine("{0}", "Uploading documents...\n");
    UploadDocuments(indexClient);

    ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

    RunQueries(indexClientForQueries);

    Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> <span data-ttu-id="72f02-141">Puede encontrar el código fuente completo de Hola de aplicación de ejemplo de Hola utilizado en este tutorial en [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="72f02-141">You can find hello full source code of hello sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>
> 
>

<span data-ttu-id="72f02-142">Lo recorreremos paso a paso.</span><span class="sxs-lookup"><span data-stu-id="72f02-142">We'll walk through this step by step.</span></span> <span data-ttu-id="72f02-143">Primero necesitamos toocreate un nuevo `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="72f02-143">First we need toocreate a new `SearchServiceClient`.</span></span> <span data-ttu-id="72f02-144">Este objeto permite toomanage índices.</span><span class="sxs-lookup"><span data-stu-id="72f02-144">This object allows you toomanage indexes.</span></span> <span data-ttu-id="72f02-145">En orden tooconstruct uno, debe tooprovide el nombre del servicio de búsqueda de Azure, así como una clave de API de administración.</span><span class="sxs-lookup"><span data-stu-id="72f02-145">In order tooconstruct one, you need tooprovide your Azure Search service name as well as an admin API key.</span></span> <span data-ttu-id="72f02-146">Puede escribir esta información en hello `appsettings.json` archivo de hello [aplicación de ejemplo](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="72f02-146">You can enter this information in hello `appsettings.json` file of hello [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

> [!NOTE]
> <span data-ttu-id="72f02-147">Si proporciona una clave incorrecta (por ejemplo, una clave de consulta donde se requiere una clave de administración), Hola `SearchServiceClient` producirá un `CloudException` con hello "Prohibido" del mensaje de error Hola primera vez llame a un método de operación en él, como `Indexes.Create`.</span><span class="sxs-lookup"><span data-stu-id="72f02-147">If you provide an incorrect key (for example, a query key where an admin key was required), hello `SearchServiceClient` will throw a `CloudException` with hello error message "Forbidden" hello first time you call an operation method on it, such as `Indexes.Create`.</span></span> <span data-ttu-id="72f02-148">Si esto ocurre tooyou, comprueba la clave de API.</span><span class="sxs-lookup"><span data-stu-id="72f02-148">If this happens tooyou, double-check our API key.</span></span>
> 
> 

<span data-ttu-id="72f02-149">Hello siguientes líneas llamar a métodos toocreate un índice con el nombre "hoteles" eliminar primero si ya existe.</span><span class="sxs-lookup"><span data-stu-id="72f02-149">hello next few lines call methods toocreate an index named "hotels", deleting it first if it already exists.</span></span> <span data-ttu-id="72f02-150">Describiremos estos métodos más adelante.</span><span class="sxs-lookup"><span data-stu-id="72f02-150">We will walk through these methods a little later.</span></span>

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

<span data-ttu-id="72f02-151">A continuación, es necesario toobe rellena el índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="72f02-151">Next, hello index needs toobe populated.</span></span> <span data-ttu-id="72f02-152">toodo, necesitamos un `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="72f02-152">toodo this, we will need a `SearchIndexClient`.</span></span> <span data-ttu-id="72f02-153">Hay dos tooobtain formas uno: mediante la creación de él, o mediante una llamada a `Indexes.GetClient` en hello `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="72f02-153">There are two ways tooobtain one: by constructing it, or by calling `Indexes.GetClient` on hello `SearchServiceClient`.</span></span> <span data-ttu-id="72f02-154">Utilizamos Hola este último para su comodidad.</span><span class="sxs-lookup"><span data-stu-id="72f02-154">We use hello latter for convenience.</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="72f02-155">En una aplicación de búsqueda típica, el llenado y la administración de índices se controlan mediante un componente independiente de las consultas de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="72f02-155">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="72f02-156">`Indexes.GetClient`es conveniente para rellenar un índice porque ahorra Hola problemas de proporcionar otro `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="72f02-156">`Indexes.GetClient` is convenient for populating an index because it saves you hello trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="72f02-157">Esto hace pasar clave de administración de Hola que Hola de toocreate usado se `SearchServiceClient` toohello nueva `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="72f02-157">It does this by passing hello admin key that you used toocreate hello `SearchServiceClient` toohello new `SearchIndexClient`.</span></span> <span data-ttu-id="72f02-158">Sin embargo, en la parte de saludo de la aplicación ejecuta consultas, es mejor hello toocreate `SearchIndexClient` directamente para que pueda pasar de una clave de consulta en lugar de una clave de administración.</span><span class="sxs-lookup"><span data-stu-id="72f02-158">However, in hello part of your application that executes queries, it is better toocreate hello `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="72f02-159">Esto es coherente con el principio de Hola de privilegios mínimos y ayudará toomake la aplicación más segura.</span><span class="sxs-lookup"><span data-stu-id="72f02-159">This is consistent with hello principle of least privilege and will help toomake your application more secure.</span></span> <span data-ttu-id="72f02-160">Puede encontrar más información acerca de las claves de administración y consulta [aquí](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span><span class="sxs-lookup"><span data-stu-id="72f02-160">You can find out more about admin keys and query keys [here](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span></span>
> 
> 

<span data-ttu-id="72f02-161">Ahora que tenemos un `SearchIndexClient`, se puede rellenar índice Hola.</span><span class="sxs-lookup"><span data-stu-id="72f02-161">Now that we have a `SearchIndexClient`, we can populate hello index.</span></span> <span data-ttu-id="72f02-162">Para ello utilizaremos otro método que tratamos más adelante.</span><span class="sxs-lookup"><span data-stu-id="72f02-162">This is done by another method that we will walk through later.</span></span>

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

<span data-ttu-id="72f02-163">Por último, se ejecutan algunas consultas de búsqueda y mostrar los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="72f02-163">Finally, we execute a few search queries and display hello results.</span></span> <span data-ttu-id="72f02-164">Esta vez usamos otro `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="72f02-164">This time we use a different `SearchIndexClient`:</span></span>

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

<span data-ttu-id="72f02-165">Echaremos un vistazo al hello `RunQueries` método más adelante.</span><span class="sxs-lookup"><span data-stu-id="72f02-165">We will take a closer look at hello `RunQueries` method later.</span></span> <span data-ttu-id="72f02-166">Aquí es Hola Hola de toocreate de código nuevo `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="72f02-166">Here is hello code toocreate hello new `SearchIndexClient`:</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="72f02-167">Esta vez se utilice una clave de consulta debido a que no necesitamos índice toohello de acceso de escritura.</span><span class="sxs-lookup"><span data-stu-id="72f02-167">This time we use a query key since we do not need write access toohello index.</span></span> <span data-ttu-id="72f02-168">Puede escribir esta información en hello `appsettings.json` archivo de hello [aplicación de ejemplo](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="72f02-168">You can enter this information in hello `appsettings.json` file of hello [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

<span data-ttu-id="72f02-169">Si ejecuta esta aplicación con un nombre de servicio válido y las claves de API, el resultado de hello debería tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="72f02-169">If you run this application with a valid service name and API keys, hello output should look like this:</span></span>

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents toobe indexed...
    
    Search hello entire index for hello term 'budget' and return only hello hotelName field:
    
    Name: Roach Motel
    
    Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello hotelId and description:
    
    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river
    
    Search hello entire index, order by a specific field (lastRenovationDate) in descending order, take hello top two results, and show only hotelName and lastRenovationDate:
    
    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00
    
    Search hello entire index for hello term 'motel':
    
    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
    
    Complete.  Press any key tooend application...

<span data-ttu-id="72f02-170">se proporciona código fuente completo de Hola de aplicación hello final Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="72f02-170">hello full source code of hello application is provided at hello end of this article.</span></span>

<span data-ttu-id="72f02-171">A continuación, tomaremos aproximación a cada uno de los métodos de hello llamados por `Main`.</span><span class="sxs-lookup"><span data-stu-id="72f02-171">Next, we will take a closer look at each of hello methods called by `Main`.</span></span>

### <a name="creating-an-index"></a><span data-ttu-id="72f02-172">Creación de un índice</span><span class="sxs-lookup"><span data-stu-id="72f02-172">Creating an index</span></span>
<span data-ttu-id="72f02-173">Después de crear un `SearchServiceClient`, novedad de hello `Main` does es index delete Hola "hoteles" Si ya existe.</span><span class="sxs-lookup"><span data-stu-id="72f02-173">After creating a `SearchServiceClient`, hello next thing `Main` does is delete hello "hotels" index if it already exists.</span></span> <span data-ttu-id="72f02-174">Que se realiza mediante Hola siguiente método:</span><span class="sxs-lookup"><span data-stu-id="72f02-174">That is done by hello following method:</span></span>

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

<span data-ttu-id="72f02-175">Este método usa Hola dado `SearchServiceClient` toocheck si existe un índice de Hola y elimínelo.</span><span class="sxs-lookup"><span data-stu-id="72f02-175">This method uses hello given `SearchServiceClient` toocheck if hello index exists, and if so, delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="72f02-176">código de ejemplo de Hola en este artículo utiliza métodos sincrónicos de Hola de hello SDK de .NET de búsqueda de Azure para simplificar el trabajo.</span><span class="sxs-lookup"><span data-stu-id="72f02-176">hello example code in this article uses hello synchronous methods of hello Azure Search .NET SDK for simplicity.</span></span> <span data-ttu-id="72f02-177">Le recomendamos que use métodos asincrónicos de hello en su propio tookeep aplicaciones escalables y con capacidad de respuesta.</span><span class="sxs-lookup"><span data-stu-id="72f02-177">We recommend that you use hello asynchronous methods in your own applications tookeep them scalable and responsive.</span></span> <span data-ttu-id="72f02-178">Por ejemplo, podría utilizar el método anterior se Hola `ExistsAsync` y `DeleteAsync` en lugar de `Exists` y `Delete`.</span><span class="sxs-lookup"><span data-stu-id="72f02-178">For example, in hello method above you could use `ExistsAsync` and `DeleteAsync` instead of `Exists` and `Delete`.</span></span>
> 
> 

<span data-ttu-id="72f02-179">A continuación, `Main` crea un nuevo índice "hotels" mediante una llamada a este método:</span><span class="sxs-lookup"><span data-stu-id="72f02-179">Next, `Main` creates a new "hotels" index by calling this method:</span></span>

```csharp
private static void CreateHotelsIndex(SearchServiceClient serviceClient)
{
    var definition = new Index()
    {
        Name = "hotels",
        Fields = FieldBuilder.BuildForType<Hotel>()
    };

    serviceClient.Indexes.Create(definition);
}
```

<span data-ttu-id="72f02-180">Este método crea un nuevo `Index` objeto con una lista de `Field` objetos que define el esquema de Hola de nuevo índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="72f02-180">This method creates a new `Index` object with a list of `Field` objects that defines hello schema of hello new index.</span></span> <span data-ttu-id="72f02-181">Cada campo tiene un nombre, un tipo de datos y varios atributos que definen su comportamiento de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="72f02-181">Each field has a name, data type, and several attributes that define its search behavior.</span></span> <span data-ttu-id="72f02-182">Hola `FieldBuilder` clase utiliza reflexión toocreate una lista de `Field` objetos para el índice de hello examinando Hola propiedades públicas y los atributos de hello dado `Hotel` clase de modelo.</span><span class="sxs-lookup"><span data-stu-id="72f02-182">hello `FieldBuilder` class uses reflection toocreate a list of `Field` objects for hello index by examining hello public properties and attributes of hello given `Hotel` model class.</span></span> <span data-ttu-id="72f02-183">Redirigirse a una aproximación a hello `Hotel` clase más adelante.</span><span class="sxs-lookup"><span data-stu-id="72f02-183">We'll take a closer look at hello `Hotel` class later on.</span></span>

> [!NOTE]
> <span data-ttu-id="72f02-184">Siempre puede crear lista de Hola de `Field` objetos directamente en lugar de usar `FieldBuilder` si es necesario.</span><span class="sxs-lookup"><span data-stu-id="72f02-184">You can always create hello list of `Field` objects directly instead of using `FieldBuilder` if needed.</span></span> <span data-ttu-id="72f02-185">Por ejemplo, puede que no desee toouse una clase de modelo o puede que necesite toouse una clase de modelo existente que no desea toomodify mediante la adición de atributos.</span><span class="sxs-lookup"><span data-stu-id="72f02-185">For example, you may not want toouse a model class or you may need toouse an existing model class that you don't want toomodify by adding attributes.</span></span>
>
> 

<span data-ttu-id="72f02-186">Además toofields, también puede agregar perfiles de puntuación, proveedores de sugerencias o toohello de opciones de CORS índice (se omiten de ejemplo de Hola por razones de brevedad).</span><span class="sxs-lookup"><span data-stu-id="72f02-186">In addition toofields, you can also add scoring profiles, suggesters, or CORS options toohello Index (these are omitted from hello sample for brevity).</span></span> <span data-ttu-id="72f02-187">Puede encontrar más información sobre objetos de índice de Hola y sus partes constituyentes en hello [referencia SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), así como en hello [referencia de API de REST de búsqueda de Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="72f02-187">You can find more information about hello Index object and its constituent parts in hello [SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), as well as in hello [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

### <a name="populating-hello-index"></a><span data-ttu-id="72f02-188">Rellenar índice Hola</span><span class="sxs-lookup"><span data-stu-id="72f02-188">Populating hello index</span></span>
<span data-ttu-id="72f02-189">paso siguiente de Hello en `Main` es toopopulate Hola recién creado índice.</span><span class="sxs-lookup"><span data-stu-id="72f02-189">hello next step in `Main` is toopopulate hello newly-created index.</span></span> <span data-ttu-id="72f02-190">Esto se hace en hello siguiente método:</span><span class="sxs-lookup"><span data-stu-id="72f02-190">This is done in hello following method:</span></span>

```csharp
private static void UploadDocuments(ISearchIndexClient indexClient)
{
    var hotels = new Hotel[]
    {
        new Hotel()
        { 
            HotelId = "1", 
            BaseRate = 199.0, 
            Description = "Best hotel in town",
            DescriptionFr = "Meilleur hôtel en ville",
            HotelName = "Fancy Stay",
            Category = "Luxury", 
            Tags = new[] { "pool", "view", "wifi", "concierge" },
            ParkingIncluded = false, 
            SmokingAllowed = false,
            LastRenovationDate = new DateTimeOffset(2010, 6, 27, 0, 0, 0, TimeSpan.Zero), 
            Rating = 5, 
            Location = GeographyPoint.Create(47.678581, -122.131577)
        },
        new Hotel()
        { 
            HotelId = "2", 
            BaseRate = 79.99,
            Description = "Cheapest hotel in town",
            DescriptionFr = "Hôtel le moins cher en ville",
            HotelName = "Roach Motel",
            Category = "Budget",
            Tags = new[] { "motel", "budget" },
            ParkingIncluded = true,
            SmokingAllowed = true,
            LastRenovationDate = new DateTimeOffset(1982, 4, 28, 0, 0, 0, TimeSpan.Zero),
            Rating = 1,
            Location = GeographyPoint.Create(49.678581, -122.131577)
        },
        new Hotel() 
        { 
            HotelId = "3", 
            BaseRate = 129.99,
            Description = "Close tootown hall and hello river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

    try
    {
        indexClient.Documents.Index(batch);
    }
    catch (IndexBatchException e)
    {
        // Sometimes when your Search service is under load, indexing will fail for some of hello documents in
        // hello batch. Depending on your application, you can take compensating actions like delaying and
        // retrying. For this simple demo, we just log hello failed document keys and continue.
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

    Console.WriteLine("Waiting for documents toobe indexed...\n");
    Thread.Sleep(2000);
}
```

<span data-ttu-id="72f02-191">Este método tiene cuatro partes.</span><span class="sxs-lookup"><span data-stu-id="72f02-191">This method has four parts.</span></span> <span data-ttu-id="72f02-192">Hola, primero crea una matriz de `Hotel` objetos que servirá como nuestro índice de toohello tooupload de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="72f02-192">hello first creates an array of `Hotel` objects that will serve as our input data tooupload toohello index.</span></span> <span data-ttu-id="72f02-193">Estos datos están incluidos en el código por motivos de simplicidad.</span><span class="sxs-lookup"><span data-stu-id="72f02-193">This data is hard-coded for simplicity.</span></span> <span data-ttu-id="72f02-194">En su propia aplicación, los datos provendrán normalmente de un origen de datos externo, como una base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="72f02-194">In your own application, your data will likely come from an external data source such as a SQL database.</span></span>

<span data-ttu-id="72f02-195">Hola segunda parte se crea un `IndexBatch` que contienen documentos Hola.</span><span class="sxs-lookup"><span data-stu-id="72f02-195">hello second part creates an `IndexBatch` containing hello documents.</span></span> <span data-ttu-id="72f02-196">Se especifica que desea tooapply toohello lote Hola crearlo, en este caso mediante una llamada de operación de hello `IndexBatch.Upload`.</span><span class="sxs-lookup"><span data-stu-id="72f02-196">You specify hello operation you want tooapply toohello batch at hello time you create it, in this case by calling `IndexBatch.Upload`.</span></span> <span data-ttu-id="72f02-197">Hello lote está cargado toohello búsqueda de Azure indexar por hello `Documents.Index` método.</span><span class="sxs-lookup"><span data-stu-id="72f02-197">hello batch is then uploaded toohello Azure Search index by hello `Documents.Index` method.</span></span>

> [!NOTE]
> <span data-ttu-id="72f02-198">En este ejemplo nos limitamos a cargar documentos.</span><span class="sxs-lookup"><span data-stu-id="72f02-198">In this example, we are just uploading documents.</span></span> <span data-ttu-id="72f02-199">Si deseara toomerge cambios en los documentos existentes o eliminar documentos, puede crear lotes mediante una llamada a `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, o `IndexBatch.Delete` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="72f02-199">If you wanted toomerge changes into existing documents or delete documents, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete` instead.</span></span> <span data-ttu-id="72f02-200">También puede mezclar operaciones diferentes en un único lote mediante una llamada a `IndexBatch.New`, que toma una colección de `IndexAction` objetos, cada uno de los cuales indica una operación determinada en un documento a tooperform de búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="72f02-200">You can also mix different operations in a single batch by calling `IndexBatch.New`, which takes a collection of `IndexAction` objects, each of which tells Azure Search tooperform a particular operation on a document.</span></span> <span data-ttu-id="72f02-201">Puede crear cada uno de ellos `IndexAction` con su propia operación llamando al método correspondiente de hello como `IndexAction.Merge`, `IndexAction.Upload`, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="72f02-201">You can create each `IndexAction` with its own operation by calling hello corresponding method such as `IndexAction.Merge`, `IndexAction.Upload`, and so on.</span></span>
> 
> 

<span data-ttu-id="72f02-202">Hola tercera parte de este método es un bloque catch que controla un caso de error importante para la indización.</span><span class="sxs-lookup"><span data-stu-id="72f02-202">hello third part of this method is a catch block that handles an important error case for indexing.</span></span> <span data-ttu-id="72f02-203">Si se produce un error en el servicio de búsqueda de Azure tooindex algunos de hello documentos en el lote de hello, un `IndexBatchException` producida por `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="72f02-203">If your Azure Search service fails tooindex some of hello documents in hello batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="72f02-204">Esto puede suceder si indiza documentos mientras el servicio está sobrecargado.</span><span class="sxs-lookup"><span data-stu-id="72f02-204">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="72f02-205">**Recomendamos encarecidamente controlar este caso de forma explícita en el código.**</span><span class="sxs-lookup"><span data-stu-id="72f02-205">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="72f02-206">Puede retrasar y, a continuación, vuelva a intentar indización documentos Hola que generaron errores o puede iniciar sesión y continuar como ejemplo de Hola o puede hacer algo más según los requisitos de coherencia de datos de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="72f02-206">You can delay and then retry indexing hello documents that failed, or you can log and continue like hello sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="72f02-207">Puede usar hello `FindFailedActionsToRetry` tooconstruct método un lote nuevo que contenga solo Hola acciones que dieron error en una llamada anterior demasiado`Index`.</span><span class="sxs-lookup"><span data-stu-id="72f02-207">You can use hello `FindFailedActionsToRetry` method tooconstruct a new batch containing only hello actions that failed in a previous call too`Index`.</span></span> <span data-ttu-id="72f02-208">método Hello está documentado [aquí](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) y no hay una explicación de cómo usa tooproperly [en StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span><span class="sxs-lookup"><span data-stu-id="72f02-208">hello method is documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) and there is a discussion of how tooproperly use it [on StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span></span>
>
>

<span data-ttu-id="72f02-209">Por último, Hola `UploadDocuments` retrasos de método en dos segundos.</span><span class="sxs-lookup"><span data-stu-id="72f02-209">Finally, hello `UploadDocuments` method delays for two seconds.</span></span> <span data-ttu-id="72f02-210">Indización realiza de forma asincrónica en el servicio de búsqueda de Azure, por lo que necesita de aplicación de ejemplo de Hola toowait un tooensure de hora corta que están disponibles para la búsqueda de documentos de Hola.</span><span class="sxs-lookup"><span data-stu-id="72f02-210">Indexing happens asynchronously in your Azure Search service, so hello sample application needs toowait a short time tooensure that hello documents are available for searching.</span></span> <span data-ttu-id="72f02-211">Retrasos así solo suelen ser necesarios en las pruebas, demostraciones y aplicaciones de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="72f02-211">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

#### <a name="how-hello-net-sdk-handles-documents"></a><span data-ttu-id="72f02-212">Cómo Hola SDK para .NET controla los documentos</span><span class="sxs-lookup"><span data-stu-id="72f02-212">How hello .NET SDK handles documents</span></span>
<span data-ttu-id="72f02-213">Quizás se pregunte cómo Hola SDK de .NET de búsqueda de Azure es las instancias de tooupload capaz de una clase definida por el usuario como `Hotel` toohello índice.</span><span class="sxs-lookup"><span data-stu-id="72f02-213">You may be wondering how hello Azure Search .NET SDK is able tooupload instances of a user-defined class like `Hotel` toohello index.</span></span> <span data-ttu-id="72f02-214">toohelp respondamos esa pregunta, echemos un vistazo a hello `Hotel` clase:</span><span class="sxs-lookup"><span data-stu-id="72f02-214">toohelp answer that question, let's look at hello `Hotel` class:</span></span>

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// hello SerializePropertyNamesAsCamelCase attribute is defined in hello Azure Search .NET SDK.
// It ensures that Pascal-case property names in hello model class are mapped toocamel-case
// field names in hello index.
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [System.ComponentModel.DataAnnotations.Key]
    [IsFilterable]
    public string HotelId { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public double? BaseRate { get; set; }

    [IsSearchable]
    public string Description { get; set; }

    [IsSearchable]
    [Analyzer(AnalyzerName.AsString.FrLucene)]
    [JsonProperty("description_fr")]
    public string DescriptionFr { get; set; }

    [IsSearchable, IsFilterable, IsSortable]
    public string HotelName { get; set; }

    [IsSearchable, IsFilterable, IsSortable, IsFacetable]
    public string Category { get; set; }

    [IsSearchable, IsFilterable, IsFacetable]
    public string[] Tags { get; set; }

    [IsFilterable, IsFacetable]
    public bool? ParkingIncluded { get; set; }

    [IsFilterable, IsFacetable]
    public bool? SmokingAllowed { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public DateTimeOffset? LastRenovationDate { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public int? Rating { get; set; }

    [IsFilterable, IsSortable]
    public GeographyPoint Location { get; set; }
}
```

<span data-ttu-id="72f02-215">Hola lo primero que toonotice es que cada propiedad pública de `Hotel` corresponde tooa campo en la definición del índice hello, pero con una diferencia fundamental: nombre de Hola de cada campo empieza por una letra minúscula ("mayúsculas y minúsculas camel"), al nombre de hello cada público propiedad de `Hotel` comienza con una letra mayúscula ("caso Pascal").</span><span class="sxs-lookup"><span data-stu-id="72f02-215">hello first thing toonotice is that each public property of `Hotel` corresponds tooa field in hello index definition, but with one crucial difference: hello name of each field starts with a lower-case letter ("camel case"), while hello name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="72f02-216">Se trata de un escenario común en las aplicaciones de .NET que realizar el enlace de datos donde esquema de destino de hello es control hello fuera del desarrollador de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="72f02-216">This is a common scenario in .NET applications that perform data-binding where hello target schema is outside hello control of hello application developer.</span></span> <span data-ttu-id="72f02-217">En lugar de tener .NET de hello tooviolate las directrices de nomenclatura mediante la realización de los nombres de propiedad y minúscula camel, puede indicar Hola SDK toomap Hola propiedad nombres toocamel caso automáticamente con hello `[SerializePropertyNamesAsCamelCase]` atributo.</span><span class="sxs-lookup"><span data-stu-id="72f02-217">Rather than having tooviolate hello .NET naming guidelines by making property names camel-case, you can tell hello SDK toomap hello property names toocamel-case automatically with hello `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="72f02-218">Hola SDK de .NET de búsqueda de Azure usa hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize de biblioteca y deserializar los tooand de objetos de modelos personalizados de JSON.</span><span class="sxs-lookup"><span data-stu-id="72f02-218">hello Azure Search .NET SDK uses hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library tooserialize and deserialize your custom model objects tooand from JSON.</span></span> <span data-ttu-id="72f02-219">Puede personalizar esta serialización si es necesario.</span><span class="sxs-lookup"><span data-stu-id="72f02-219">You can customize this serialization if needed.</span></span> <span data-ttu-id="72f02-220">Para obtener más información, consulte [Serialización personalizada con JSON.NET](#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="72f02-220">For more details, see [Custom Serialization with JSON.NET](#JsonDotNet).</span></span>
> 
> 

<span data-ttu-id="72f02-221">Hello segundo toonotice lo son Hola atributos como `IsFilterable`, `IsSearchable`, `Key`, y `Analyzer` que decoran cada propiedad pública.</span><span class="sxs-lookup"><span data-stu-id="72f02-221">hello second thing toonotice are hello attributes such as `IsFilterable`, `IsSearchable`, `Key`, and `Analyzer` that decorate each public property.</span></span> <span data-ttu-id="72f02-222">Estos atributos asignan directamente toohello [atributos correspondientes del índice de búsqueda de Azure de hello](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span><span class="sxs-lookup"><span data-stu-id="72f02-222">These attributes map directly toohello [corresponding attributes of hello Azure Search index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span></span> <span data-ttu-id="72f02-223">Hola `FieldBuilder` clase usa estas definiciones de campo de tooconstruct para índice Hola.</span><span class="sxs-lookup"><span data-stu-id="72f02-223">hello `FieldBuilder` class uses these tooconstruct field definitions for hello index.</span></span>

<span data-ttu-id="72f02-224">importante tercer Hola sobre hello `Hotel` clase son tipos de datos de hello propiedades públicas de Hola.</span><span class="sxs-lookup"><span data-stu-id="72f02-224">hello third important thing about hello `Hotel` class are hello data types of hello public properties.</span></span> <span data-ttu-id="72f02-225">tipos de .NET de Hola de estas propiedades asignan tootheir tipos de campo equivalente en la definición del índice Hola.</span><span class="sxs-lookup"><span data-stu-id="72f02-225">hello .NET types of  these properties map tootheir equivalent field types in hello index definition.</span></span> <span data-ttu-id="72f02-226">Por ejemplo, hello `Category` propiedad de cadena asigna toohello `category` campo, que es de tipo `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="72f02-226">For example, hello `Category` string property maps toohello `category` field, which is of type `Edm.String`.</span></span> <span data-ttu-id="72f02-227">Hay asignaciones de tipos similares entre `bool?` y `Edm.Boolean`, `DateTimeOffset?` y `Edm.DateTimeOffset`, reglas específicas de hello etc. para asignación de tipo hello están documentadas con hello `Documents.Get` método Hola [SDK de .NET de búsqueda de Azure referencia](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="72f02-227">There are similar type mappings between `bool?` and `Edm.Boolean`, `DateTimeOffset?` and `Edm.DateTimeOffset`, etc. hello specific rules for hello type mapping are documented with hello `Documents.Get` method in hello [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span> <span data-ttu-id="72f02-228">Hola `FieldBuilder` clase se encarga de esta asignación para usted, pero todavía puede ser útil toounderstand por si tuviera tootroubleshoot los problemas de serialización.</span><span class="sxs-lookup"><span data-stu-id="72f02-228">hello `FieldBuilder` class takes care of this mapping for you, but it can still be helpful toounderstand in case you need tootroubleshoot any serialization issues.</span></span>

<span data-ttu-id="72f02-229">Esta capacidad toouse sus propias clases como documentos funciona en ambas direcciones; También puede recuperar los resultados de la búsqueda y tener Hola SDK automáticamente deserializar ellos tooa tipo de su elección, como se verá en la siguiente sección de Hola.</span><span class="sxs-lookup"><span data-stu-id="72f02-229">This ability toouse your own classes as documents works in both directions; You can also retrieve search results and have hello SDK automatically deserialize them tooa type of your choice, as we will see in hello next section.</span></span>

> [!NOTE]
> <span data-ttu-id="72f02-230">Hola SDK de .NET de búsqueda de Azure también admite documentos dinámicamente tipada utilizando hello `Document` (clase), que es una asignación de clave/valor de los valores de toofield de nombres de campo.</span><span class="sxs-lookup"><span data-stu-id="72f02-230">hello Azure Search .NET SDK also supports dynamically-typed documents using hello `Document` class, which is a key/value mapping of field names toofield values.</span></span> <span data-ttu-id="72f02-231">Esto es útil en escenarios donde no conoce el esquema de índice de hello en tiempo de diseño, o donde sería clases del modelo de toospecific toobind supone un inconveniente.</span><span class="sxs-lookup"><span data-stu-id="72f02-231">This is useful in scenarios where you don't know hello index schema at design-time, or where it would be inconvenient toobind toospecific model classes.</span></span> <span data-ttu-id="72f02-232">Todos los métodos de Hola Hola SDK que se encargan de documentos tienen sobrecargas que funcionan con hello `Document` clase, así como fuertemente tipados sobrecargas que toman un parámetro de tipo genérico.</span><span class="sxs-lookup"><span data-stu-id="72f02-232">All hello methods in hello SDK that deal with documents have overloads that work with hello `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="72f02-233">Solo Hola este último se utilizan en el código de ejemplo de Hola en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="72f02-233">Only hello latter are used in hello sample code in this tutorial.</span></span> <span data-ttu-id="72f02-234">Hola `Document` clase hereda de `Dictionary<string, object>`.</span><span class="sxs-lookup"><span data-stu-id="72f02-234">hello `Document` class inherits from `Dictionary<string, object>`.</span></span> <span data-ttu-id="72f02-235">Puede encontrar otros detalles [aquí](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span><span class="sxs-lookup"><span data-stu-id="72f02-235">You can find other details [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span></span>
> 
> 

<span data-ttu-id="72f02-236">**¿Por qué debería usar tipos de datos que aceptan valores null?**</span><span class="sxs-lookup"><span data-stu-id="72f02-236">**Why you should use nullable data types**</span></span>

<span data-ttu-id="72f02-237">Al diseñar su propio índice modelo clases toomap tooan búsqueda de Azure, se recomienda declarar propiedades de tipos de valor como `bool` y `int` toobe que aceptan valores null (por ejemplo, `bool?` en lugar de `bool`).</span><span class="sxs-lookup"><span data-stu-id="72f02-237">When designing your own model classes toomap tooan Azure Search index, we recommend declaring properties of value types such as `bool` and `int` toobe nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="72f02-238">Si utiliza una propiedad que no acepta valores NULL, tienen también**garantizar** ningún documentos en el índice que contienen un valor nulo para el campo correspondiente Hola.</span><span class="sxs-lookup"><span data-stu-id="72f02-238">If you use a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="72f02-239">Hola SDK ni Hola servicio Búsqueda de Azure le ayudará a tooenforce esto.</span><span class="sxs-lookup"><span data-stu-id="72f02-239">Neither hello SDK nor hello Azure Search service will help you tooenforce this.</span></span>

<span data-ttu-id="72f02-240">Esto no es simplemente un problema hipotético: Imagine un escenario donde agrega un nuevo índice existente de campo tooan que es de tipo `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="72f02-240">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="72f02-241">Después de actualizar la definición del índice hello, todos los documentos tendrá un valor null para ese campo nuevo (ya que todos los tipos admiten valores NULL en la búsqueda de Azure).</span><span class="sxs-lookup"><span data-stu-id="72f02-241">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="72f02-242">Si, a continuación, usa una clase de modelo con un acepta valores NULL `int` propiedad para ese campo, obtendrá un `JsonSerializationException` similar a éste al tratar de tooretrieve documentos:</span><span class="sxs-lookup"><span data-stu-id="72f02-242">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="72f02-243">Por este motivo, recomendamos utilizar tipos que aceptan valores NULL en las clases de modelo como procedimiento recomendado.</span><span class="sxs-lookup"><span data-stu-id="72f02-243">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a><span data-ttu-id="72f02-244">Serialización personalizada con JSON.NET</span><span class="sxs-lookup"><span data-stu-id="72f02-244">Custom Serialization with JSON.NET</span></span>
<span data-ttu-id="72f02-245">Hola SDK usa JSON.NET para serializar y deserializar documentos.</span><span class="sxs-lookup"><span data-stu-id="72f02-245">hello SDK uses JSON.NET for serializing and deserializing documents.</span></span> <span data-ttu-id="72f02-246">Puede personalizar la serialización y deserialización si necesita definir su propio `JsonConverter` o `IContractResolver` (vea hello [JSON.NET documentación](http://www.newtonsoft.com/json/help/html/Introduction.htm) para obtener más detalles).</span><span class="sxs-lookup"><span data-stu-id="72f02-246">You can customize serialization and deserialization if needed by defining your own `JsonConverter` or `IContractResolver` (see hello [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) for more details).</span></span> <span data-ttu-id="72f02-247">Esto puede ser útil cuando desee tooadapt una clase de modelo existente de la aplicación para su uso con búsqueda de Azure y otros escenarios más avanzados.</span><span class="sxs-lookup"><span data-stu-id="72f02-247">This can be useful when you want tooadapt an existing model class from your application for use with Azure Search, and other more advanced scenarios.</span></span> <span data-ttu-id="72f02-248">Por ejemplo, con la serialización personalizada, puede:</span><span class="sxs-lookup"><span data-stu-id="72f02-248">For example, with custom serialization you can:</span></span>

* <span data-ttu-id="72f02-249">Incluir o excluir determinadas propiedades de la clase de modelo para que se almacenen como campos del documento.</span><span class="sxs-lookup"><span data-stu-id="72f02-249">Include or exclude certain properties of your model class from being stored as document fields.</span></span>
* <span data-ttu-id="72f02-250">Asignar entre los nombres de propiedad del código y los nombres de campo del índice.</span><span class="sxs-lookup"><span data-stu-id="72f02-250">Map between property names in your code and field names in your index.</span></span>
* <span data-ttu-id="72f02-251">Crear atributos personalizados que pueden usarse para la asignación de campos de propiedades toodocument.</span><span class="sxs-lookup"><span data-stu-id="72f02-251">Create custom attributes that can be used for mapping properties toodocument fields.</span></span>

<span data-ttu-id="72f02-252">Puede encontrar ejemplos de implementación de serialización personalizada en pruebas unitarias de Hola para hello SDK de .NET de búsqueda de Azure en GitHub.</span><span class="sxs-lookup"><span data-stu-id="72f02-252">You can find examples of implementing custom serialization in hello unit tests for hello Azure Search .NET SDK on GitHub.</span></span> <span data-ttu-id="72f02-253">[Esta carpeta](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models) es un buen punto de partida.</span><span class="sxs-lookup"><span data-stu-id="72f02-253">A good starting point is [this folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span></span> <span data-ttu-id="72f02-254">Contiene clases que se utilizan las pruebas de serialización personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="72f02-254">It contains classes that are used by hello custom serialization tests.</span></span>

### <a name="searching-for-documents-in-hello-index"></a><span data-ttu-id="72f02-255">Buscar documentos en el índice de Hola</span><span class="sxs-lookup"><span data-stu-id="72f02-255">Searching for documents in hello index</span></span>
<span data-ttu-id="72f02-256">Hola último paso en la aplicación de ejemplo de Hola es toosearch para algunos documentos del índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="72f02-256">hello last step in hello sample application is toosearch for some documents in hello index.</span></span> <span data-ttu-id="72f02-257">Hola siguiendo el método para ello:</span><span class="sxs-lookup"><span data-stu-id="72f02-257">hello following method does this:</span></span>

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
    SearchParameters parameters;
    DocumentSearchResult<Hotel> results;

    Console.WriteLine("Search hello entire index for hello term 'budget' and return only hello hotelName field:\n");

    parameters =
        new SearchParameters()
        {
            Select = new[] { "hotelName" }
        };

    results = indexClient.Documents.Search<Hotel>("budget", parameters);

    WriteDocuments(results);

    Console.Write("Apply a filter toohello index toofind hotels cheaper than $150 per night, ");
    Console.WriteLine("and return hello hotelId and description:\n");

    parameters =
        new SearchParameters()
        {
            Filter = "baseRate lt 150",
            Select = new[] { "hotelId", "description" }
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.Write("Search hello entire index, order by a specific field (lastRenovationDate) ");
    Console.Write("in descending order, take hello top two results, and show only hotelName and ");
    Console.WriteLine("lastRenovationDate:\n");

    parameters =
        new SearchParameters()
        {
            OrderBy = new[] { "lastRenovationDate desc" },
            Select = new[] { "hotelName", "lastRenovationDate" },
            Top = 2
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.WriteLine("Search hello entire index for hello term 'motel':\n");

    parameters = new SearchParameters();
    results = indexClient.Documents.Search<Hotel>("motel", parameters);

    WriteDocuments(results);
}
```

<span data-ttu-id="72f02-258">Cada vez que ejecuta una consulta, este método crea primero un nuevo objeto `SearchParameters`.</span><span class="sxs-lookup"><span data-stu-id="72f02-258">Each time it executes a query, this method first creates a new `SearchParameters` object.</span></span> <span data-ttu-id="72f02-259">Se trata de opciones adicionales de toospecify usado para consulta de hello, como la ordenación, filtrado, paginación y facetas.</span><span class="sxs-lookup"><span data-stu-id="72f02-259">This is used toospecify additional options for hello query such as sorting, filtering, paging, and faceting.</span></span> <span data-ttu-id="72f02-260">En este método, estamos estableciendo hello `Filter`, `Select`, `OrderBy`, y `Top` propiedad para consultas diferentes.</span><span class="sxs-lookup"><span data-stu-id="72f02-260">In this method, we're setting hello `Filter`, `Select`, `OrderBy`, and `Top` property for different queries.</span></span> <span data-ttu-id="72f02-261">Hola todos los `SearchParameters` las propiedades están documentadas [aquí](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span><span class="sxs-lookup"><span data-stu-id="72f02-261">All hello `SearchParameters` properties are documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span></span>

<span data-ttu-id="72f02-262">Hola siguiente paso es tooactually Ejecutar consulta de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="72f02-262">hello next step is tooactually execute hello search query.</span></span> <span data-ttu-id="72f02-263">Esto se realiza mediante hello `Documents.Search` método.</span><span class="sxs-lookup"><span data-stu-id="72f02-263">This is done using hello `Documents.Search` method.</span></span> <span data-ttu-id="72f02-264">Para cada consulta, pasamos toouse de texto de búsqueda de hello como una cadena (o `"*"` si no hay ningún texto de búsqueda), además de hello buscar parámetros que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="72f02-264">For each query, we pass hello search text toouse as a string (or `"*"` if there is no search text), plus hello search parameters created earlier.</span></span> <span data-ttu-id="72f02-265">También especificamos `Hotel` como parámetro de tipo hello para `Documents.Search`, que indica a documentos de toodeserialize del SDK de hello en los resultados de búsqueda de Hola en objetos de tipo `Hotel`.</span><span class="sxs-lookup"><span data-stu-id="72f02-265">We also specify `Hotel` as hello type parameter for `Documents.Search`, which tells hello SDK toodeserialize documents in hello search results into objects of type `Hotel`.</span></span>

> [!NOTE]
> <span data-ttu-id="72f02-266">También puede encontrar más información acerca de la sintaxis de expresiones de consulta de búsqueda de Hola [aquí](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="72f02-266">You can find more information about hello search query expression syntax [here](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span></span>
> 
> 

<span data-ttu-id="72f02-267">Finalmente, después de cada consulta este método recorre en iteración todas las coincidencias de hello en resultados de búsqueda de hello, imprimir cada consola de toohello de documento:</span><span class="sxs-lookup"><span data-stu-id="72f02-267">Finally, after each query this method iterates through all hello matches in hello search results, printing each document toohello console:</span></span>

```csharp
private static void WriteDocuments(DocumentSearchResult<Hotel> searchResults)
{
    foreach (SearchResult<Hotel> result in searchResults.Results)
    {
        Console.WriteLine(result.Document);
    }

    Console.WriteLine();
}
```

<span data-ttu-id="72f02-268">Echemos un vistazo más de cerca a cada una de las consultas de Hola a su vez.</span><span class="sxs-lookup"><span data-stu-id="72f02-268">Let's take a closer look at each of hello queries in turn.</span></span> <span data-ttu-id="72f02-269">Ésta es Hola código tooexecute Hola primera consulta:</span><span class="sxs-lookup"><span data-stu-id="72f02-269">Here is hello code tooexecute hello first query:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

<span data-ttu-id="72f02-270">En este caso, estamos buscando hoteles que coinciden con la palabra Hola "budget", y queremos tooget volver solo Hola hotel nombres, tal y como especifica hello `Select` parámetro.</span><span class="sxs-lookup"><span data-stu-id="72f02-270">In this case, we're searching for hotels that match hello word "budget", and we want tooget back only hello hotel names, as specified by hello `Select` parameter.</span></span> <span data-ttu-id="72f02-271">Estos son los resultados de hello:</span><span class="sxs-lookup"><span data-stu-id="72f02-271">Here are hello results:</span></span>

    Name: Roach Motel

<span data-ttu-id="72f02-272">A continuación, se desea hoteles de hello toofind con una tasa por la noche de menos de 150 $ y devuelven solo el identificador de hotel de Hola y descripción:</span><span class="sxs-lookup"><span data-stu-id="72f02-272">Next, we want toofind hello hotels with a nightly rate of less than $150, and return only hello hotel ID and description:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

<span data-ttu-id="72f02-273">Esta consulta utiliza una OData `$filter` expresión, `baseRate lt 150`, toofilter documentos de hello en el índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="72f02-273">This query uses an OData `$filter` expression, `baseRate lt 150`, toofilter hello documents in hello index.</span></span> <span data-ttu-id="72f02-274">Puede encontrar más información sobre sintaxis de OData que admite búsqueda de Azure de hello [aquí](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="72f02-274">You can find out more about hello OData syntax that Azure Search supports [here](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span></span>

<span data-ttu-id="72f02-275">Estos son los resultados de Hola de consulta de hello:</span><span class="sxs-lookup"><span data-stu-id="72f02-275">Here are hello results of hello query:</span></span>

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river

<span data-ttu-id="72f02-276">A continuación, queremos toofind Hola superior dos hoteles que se hayan renovado más recientemente y muestran el nombre del hotel hello y última fecha de renovación.</span><span class="sxs-lookup"><span data-stu-id="72f02-276">Next, we want toofind hello top two hotels that have been most recently renovated, and show hello hotel name and last renovation date.</span></span> <span data-ttu-id="72f02-277">Este es el código de hello.</span><span class="sxs-lookup"><span data-stu-id="72f02-277">Here is hello code:</span></span> 

```csharp
parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

<span data-ttu-id="72f02-278">En este caso, usamos nuevo Hola de OData sintaxis toospecify `OrderBy` parámetro como `lastRenovationDate desc`.</span><span class="sxs-lookup"><span data-stu-id="72f02-278">In this case, we again use OData syntax toospecify hello `OrderBy` parameter as `lastRenovationDate desc`.</span></span> <span data-ttu-id="72f02-279">También establecemos `Top` too2 tooensure sólo obtenemos documentos de dos primeras Hola.</span><span class="sxs-lookup"><span data-stu-id="72f02-279">We also set `Top` too2 tooensure we only get hello top two documents.</span></span> <span data-ttu-id="72f02-280">Como antes, establecemos `Select` toospecify los campos que se deben devolver.</span><span class="sxs-lookup"><span data-stu-id="72f02-280">As before, we set `Select` toospecify which fields should be returned.</span></span>

<span data-ttu-id="72f02-281">Estos son los resultados de hello:</span><span class="sxs-lookup"><span data-stu-id="72f02-281">Here are hello results:</span></span>

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

<span data-ttu-id="72f02-282">Por último, queremos toofind todos los hoteles que coinciden con la palabra Hola "motel":</span><span class="sxs-lookup"><span data-stu-id="72f02-282">Finally, we want toofind all hotels that match hello word "motel":</span></span>

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

<span data-ttu-id="72f02-283">Y estos son los resultados de hello, que incluyen todos los campos porque no especificamos hello `Select` propiedad:</span><span class="sxs-lookup"><span data-stu-id="72f02-283">And here are hello results, which include all fields since we did not specify hello `Select` property:</span></span>

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

<span data-ttu-id="72f02-284">Este paso completa el tutorial de hello, pero no se detenga aquí.</span><span class="sxs-lookup"><span data-stu-id="72f02-284">This step completes hello tutorial, but don't stop here.</span></span> <span data-ttu-id="72f02-285">**pasos siguientes** proporcionan recursos adicionales para obtener más información acerca de Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="72f02-285">**Next steps** provides additional resources for learning more about Azure Search.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72f02-286">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="72f02-286">Next steps</span></span>
* <span data-ttu-id="72f02-287">Examinar las referencias de Hola para hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) y [API de REST](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="72f02-287">Browse hello references for hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
* <span data-ttu-id="72f02-288">Profundice en sus conocimientos por medio de [vídeos y otros ejemplos y tutoriales](search-video-demo-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="72f02-288">Deepen your knowledge through [videos and other samples and tutorials](search-video-demo-tutorial-list.md).</span></span>
* <span data-ttu-id="72f02-289">Revisión [convenciones de nomenclatura](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) reglas de hello toolearn para asignar nombres a varios objetos.</span><span class="sxs-lookup"><span data-stu-id="72f02-289">Review [naming conventions](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) toolearn hello rules for naming various objects.</span></span>
* <span data-ttu-id="72f02-290">Consulte los [tipos de datos admitidos](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) en Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="72f02-290">Review [supported data types](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span></span>
