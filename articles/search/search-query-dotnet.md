---
title: "aaa \"consultar un índice (API de .NET - búsqueda de Azure) | Documentos de Microsoft\""
description: "Crear una consulta de búsqueda en búsqueda de Azure y usar resultados de búsqueda de toofilter y de ordenación de los parámetros de búsqueda."
services: search
manager: jhubbard
documentationcenter: 
author: brjohnstmsft
ms.assetid: 12c3efba-ea99-4187-9d2d-f63b5ec7040d
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/19/2017
ms.author: brjohnst
ms.openlocfilehash: 8b3ba1cd1270aad038fb48d9053fcff35d243e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-net-sdk"></a><span data-ttu-id="b3e4e-103">Consultar el índice de búsqueda de Azure con hello SDK para .NET</span><span class="sxs-lookup"><span data-stu-id="b3e4e-103">Query your Azure Search index using hello .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b3e4e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="b3e4e-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="b3e4e-105">Portal</span><span class="sxs-lookup"><span data-stu-id="b3e4e-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="b3e4e-106">.NET</span><span class="sxs-lookup"><span data-stu-id="b3e4e-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="b3e4e-107">REST</span><span class="sxs-lookup"><span data-stu-id="b3e4e-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="b3e4e-108">En este artículo le mostrará cómo tooquery un índice utilizando Hola [SDK de .NET de búsqueda de Azure](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="b3e4e-108">This article will show you how tooquery an index using hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span>

<span data-ttu-id="b3e4e-109">Antes de comenzar este tutorial, debe haber [creado ya un índice de Azure Search](search-what-is-an-index.md) y [haberlo rellenado con datos](search-what-is-data-import.md).</span><span class="sxs-lookup"><span data-stu-id="b3e4e-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b3e4e-110">Todo el código de ejemplo de este artículo está escrito en C#.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="b3e4e-111">Puede encontrar el código fuente completo hello [en GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="b3e4e-111">You can find hello full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="b3e4e-112">También puede leer sobre hello [SDK de .NET de búsqueda de Azure](search-howto-dotnet-sdk.md) para un tutorial más detallado del código de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-112">You can also read about hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of hello sample code.</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="b3e4e-113">Identificación de la clave de API de consulta del servicio de Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="b3e4e-113">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="b3e4e-114">Ahora que ha creado un índice de búsqueda de Azure, son consultas tooissue casi listo con hello .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-114">Now that you have created an Azure Search index, you are almost ready tooissue queries using hello .NET SDK.</span></span> <span data-ttu-id="b3e4e-115">En primer lugar, necesitará tooobtain uno Hola consulta claves de api que se generó para aprovisionar el servicio de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-115">First, you will need tooobtain one of hello query api-keys that was generated for hello search service you provisioned.</span></span> <span data-ttu-id="b3e4e-116">Hola .NET SDK enviará esta clave de api en cada servicio de tooyour de solicitud.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-116">hello .NET SDK will send this api-key on every request tooyour service.</span></span> <span data-ttu-id="b3e4e-117">Tener una clave válida establece la confianza, por cada solicitud, entre Hola aplicación enviando Hola solicitud y el servicio de Hola que los controle.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-117">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="b3e4e-118">toofind puede iniciar sesión en toohello de claves de api de su servicio [portal de Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="b3e4e-118">toofind your service's api-keys you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="b3e4e-119">Vaya hoja del servicio de búsqueda de Azure tooyour</span><span class="sxs-lookup"><span data-stu-id="b3e4e-119">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="b3e4e-120">Haga clic en hello icono "Claves"</span><span class="sxs-lookup"><span data-stu-id="b3e4e-120">Click on hello "Keys" icon</span></span>

<span data-ttu-id="b3e4e-121">El servicio tendrá *claves de administración* y *claves de consulta*.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-121">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="b3e4e-122">El principal y secundaria *claves de administración* conceder derechos completos tooall operaciones, incluido el servicio de hello capacidad toomanage hello, crear y eliminar índices, los indizadores y orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-122">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="b3e4e-123">Existen dos claves para que pueda continuar la clave secundaria de hello toouse si decide tooregenerate Hola primary key y viceversa.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-123">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="b3e4e-124">Su *claves de consulta* conceder acceso de solo lectura tooindexes y documentos, y son aplicaciones tooclient normalmente distribuida que emiten solicitudes de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-124">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="b3e4e-125">Para fines de Hola de consultar un índice, puede usar una de las claves de consulta.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-125">For hello purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="b3e4e-126">Las claves de administración también pueden usarse para las consultas, pero debe usar una clave de consulta en el código de aplicación de manera esto mejor hello [principio de privilegios mínimos](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="b3e4e-126">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows hello [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="create-an-instance-of-hello-searchindexclient-class"></a><span data-ttu-id="b3e4e-127">Cree una instancia de hello SearchIndexClient (clase)</span><span class="sxs-lookup"><span data-stu-id="b3e4e-127">Create an instance of hello SearchIndexClient class</span></span>
<span data-ttu-id="b3e4e-128">consultas de tooissue con hello SDK de .NET de búsqueda de Azure, deberá toocreate una instancia de Hola `SearchIndexClient` clase.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-128">tooissue queries with hello Azure Search .NET SDK, you will need toocreate an instance of hello `SearchIndexClient` class.</span></span> <span data-ttu-id="b3e4e-129">Esta clase tiene varios constructores.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-129">This class has several constructors.</span></span> <span data-ttu-id="b3e4e-130">Hola uno desea que toma el nombre del servicio de búsqueda, el nombre del índice y un `SearchCredentials` objeto como parámetros.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-130">hello one you want takes your search service name, index name, and a `SearchCredentials` object as parameters.</span></span> <span data-ttu-id="b3e4e-131">`SearchCredentials` incluye su clave de API.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-131">`SearchCredentials` wraps your api-key.</span></span>

<span data-ttu-id="b3e4e-132">código de Hello siguiente crea un nuevo `SearchIndexClient` para índice de "hoteles" Hola (creado en [crear un índice de búsqueda de Azure usando Hola .NET SDK](search-create-index-dotnet.md)) con valores para el nombre de servicio de búsqueda de Hola y clave de api que se almacenan en la configuración de la aplicación hello archivo (`appsettings.json` en caso de hello de hello [aplicación de ejemplo](http://aka.ms/search-dotnet-howto)):</span><span class="sxs-lookup"><span data-stu-id="b3e4e-132">hello code below creates a new `SearchIndexClient` for hello "hotels" index (created in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md)) using values for hello search service name and api-key that are stored in hello application's config file (`appsettings.json` in hello case of hello [sample application](http://aka.ms/search-dotnet-howto)):</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="b3e4e-133">`SearchIndexClient` tiene una propiedad `Documents`.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-133">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="b3e4e-134">Esta propiedad proporciona que todos Hola métodos que necesita tooquery índices de búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-134">This property provides all hello methods you need tooquery Azure Search indexes.</span></span>

## <a name="query-your-index"></a><span data-ttu-id="b3e4e-135">Consulta del índice</span><span class="sxs-lookup"><span data-stu-id="b3e4e-135">Query your index</span></span>
<span data-ttu-id="b3e4e-136">Buscar con hello SDK para .NET es tan sencillo como Hola llamada `Documents.Search` método en su `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-136">Searching with hello .NET SDK is as simple as calling hello `Documents.Search` method on your `SearchIndexClient`.</span></span> <span data-ttu-id="b3e4e-137">Este método toma unos parámetros, incluido el texto de búsqueda de hello, junto con un `SearchParameters` objeto que puede ser usado toofurther refine Hola consulta.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-137">This method takes a few parameters, including hello search text, along with a `SearchParameters` object that can be used toofurther refine hello query.</span></span>

#### <a name="types-of-queries"></a><span data-ttu-id="b3e4e-138">Tipos de consultas</span><span class="sxs-lookup"><span data-stu-id="b3e4e-138">Types of Queries</span></span>
<span data-ttu-id="b3e4e-139">main Hola dos [tipos de consulta](search-query-overview.md#types-of-queries) va a utilizar son `search` y `filter`.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-139">hello two main [query types](search-query-overview.md#types-of-queries) you will use are `search` and `filter`.</span></span> <span data-ttu-id="b3e4e-140">Una consulta `search` realiza búsquedas de uno o más términos en todos los campos *habilitados para búsqueda* del índice.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-140">A `search` query searches for one or more terms in all *searchable* fields in your index.</span></span> <span data-ttu-id="b3e4e-141">Una consulta `filter` evalúa una expresión booleana en todos los campos *filtrables* de un índice.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-141">A `filter` query evaluates a boolean expression over all *filterable* fields in an index.</span></span>

<span data-ttu-id="b3e4e-142">Búsquedas y filtros se realizan con hello `Documents.Search` método.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-142">Both searches and filters are performed using hello `Documents.Search` method.</span></span> <span data-ttu-id="b3e4e-143">Puede pasarse a una consulta de búsqueda de hello `searchText` parámetro, mientras que puede pasarse a una expresión de filtro de hello `Filter` propiedad de hello `SearchParameters` clase.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-143">A search query can be passed in hello `searchText` parameter, while a filter expression can be passed in hello `Filter` property of hello `SearchParameters` class.</span></span> <span data-ttu-id="b3e4e-144">toofilter sin buscar, sólo tiene que pasar `"*"` para hello `searchText` parámetro.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-144">toofilter without searching, just pass `"*"` for hello `searchText` parameter.</span></span> <span data-ttu-id="b3e4e-145">toosearch sin filtrar, deje hello `Filter` propiedad no se establece, o no pase un `SearchParameters` en absoluto de la instancia.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-145">toosearch without filtering, just leave hello `Filter` property unset, or do not pass in a `SearchParameters` instance at all.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="b3e4e-146">Consultas de ejemplo</span><span class="sxs-lookup"><span data-stu-id="b3e4e-146">Example Queries</span></span>
<span data-ttu-id="b3e4e-147">Hola siguiente código de ejemplo muestra varias maneras diferentes tooquery Hola "hoteles" índice definido en [crear un índice de búsqueda de Azure con .NET SDK hello](search-create-index-dotnet.md#DefineIndex).</span><span class="sxs-lookup"><span data-stu-id="b3e4e-147">hello following sample code shows a few different ways tooquery hello "hotels" index defined in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#DefineIndex).</span></span> <span data-ttu-id="b3e4e-148">Tenga en cuenta que documentos Hola devueltos con los resultados de la búsqueda de hello son instancias de hello `Hotel` (clase), que se ha definido en [Hola de importación de datos en búsqueda de Azure con .NET SDK](search-import-data-dotnet.md#HotelClass).</span><span class="sxs-lookup"><span data-stu-id="b3e4e-148">Note that hello documents returned with hello search results are instances of hello `Hotel` class, which was defined in [Data Import in Azure Search using hello .NET SDK](search-import-data-dotnet.md#HotelClass).</span></span> <span data-ttu-id="b3e4e-149">código de ejemplo de Hola hace uso de un `WriteDocuments` consola de toohello de resultados de búsqueda de método toooutput Hola.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-149">hello sample code makes use of a `WriteDocuments` method toooutput hello search results toohello console.</span></span> <span data-ttu-id="b3e4e-150">Este método se describe en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-150">This method is described in hello next section.</span></span>

```csharp
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
```

## <a name="handle-search-results"></a><span data-ttu-id="b3e4e-151">Control de los resultados de la búsqueda</span><span class="sxs-lookup"><span data-stu-id="b3e4e-151">Handle search results</span></span>
<span data-ttu-id="b3e4e-152">Hola `Documents.Search` método devuelve un `DocumentSearchResult` objeto que contiene los resultados de Hola de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-152">hello `Documents.Search` method returns a `DocumentSearchResult` object that contains hello results of hello query.</span></span> <span data-ttu-id="b3e4e-153">ejemplo de Hola en la sección anterior de hello usa un método llamado `WriteDocuments` consola toohello de toooutput Hola búsqueda resultados:</span><span class="sxs-lookup"><span data-stu-id="b3e4e-153">hello example in hello previous section used a method called `WriteDocuments` toooutput hello search results toohello console:</span></span>

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

<span data-ttu-id="b3e4e-154">Aquí está lo que parecen resultados hello como para las consultas de hello en la sección anterior de hello, suponiendo un índice de hoteles"Hola" se rellena con datos de ejemplo de Hola en [Hola de importación de datos en búsqueda de Azure con .NET SDK](search-import-data-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="b3e4e-154">Here is what hello results look like for hello queries in hello previous section, assuming hello "hotels" index is populated with hello sample data in [Data Import in Azure Search using hello .NET SDK](search-import-data-dotnet.md):</span></span>

```
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
```

<span data-ttu-id="b3e4e-155">código de ejemplo de Hola anterior usa resultados de la búsqueda de hello consola toooutput.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-155">hello sample code above uses hello console toooutput search results.</span></span> <span data-ttu-id="b3e4e-156">Del mismo modo, necesitará toodisplay resultados de la búsqueda en su propia aplicación.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-156">You will likewise need toodisplay search results in your own application.</span></span> <span data-ttu-id="b3e4e-157">Vea [en este ejemplo en GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) para obtener un ejemplo de cómo toorender búsqueda da como resultado una aplicación web basada en ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="b3e4e-157">See [this sample on GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) for an example of how toorender search results in an ASP.NET MVC-based web application.</span></span>

