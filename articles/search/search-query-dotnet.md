---
title: "Consulte de un índice (API de .NET - Azure Search) | Microsoft Docs"
description: "Cree una consulta de búsqueda en Búsqueda de Azure y use los parámetros de búsqueda para filtrar y ordenar los resultados de búsqueda."
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
ms.openlocfilehash: 52bd0fd4cf70401dcf881c7f28d5cd91397bb059
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="query-your-azure-search-index-using-the-net-sdk"></a><span data-ttu-id="0c376-103">Consultas del índice de Búsqueda de Azure con el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="0c376-103">Query your Azure Search index using the .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0c376-104">Información general</span><span class="sxs-lookup"><span data-stu-id="0c376-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="0c376-105">Portal</span><span class="sxs-lookup"><span data-stu-id="0c376-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="0c376-106">.NET</span><span class="sxs-lookup"><span data-stu-id="0c376-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="0c376-107">REST</span><span class="sxs-lookup"><span data-stu-id="0c376-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="0c376-108">En este artículo se muestra cómo realizar una consulta en un índice con el [SDK de .NET de Búsqueda de Azure](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="0c376-108">This article will show you how to query an index using the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span>

<span data-ttu-id="0c376-109">Antes de comenzar este tutorial, debe haber [creado ya un índice de Azure Search](search-what-is-an-index.md) y [haberlo rellenado con datos](search-what-is-data-import.md).</span><span class="sxs-lookup"><span data-stu-id="0c376-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0c376-110">Todo el código de ejemplo de este artículo está escrito en C#.</span><span class="sxs-lookup"><span data-stu-id="0c376-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="0c376-111">El código fuente completo se puede encontrar [en GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="0c376-111">You can find the full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="0c376-112">Consulte el [SDK de Azure Search para .NET](search-howto-dotnet-sdk.md) para ver un tutorial más detallado sobre el código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0c376-112">You can also read about the [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of the sample code.</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="0c376-113">Identificación de la clave de API de consulta del servicio de Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="0c376-113">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="0c376-114">Ahora que ha creado un índice de Búsqueda de Azure, está casi listo para emitir consultas mediante el SDK de .NET.</span><span class="sxs-lookup"><span data-stu-id="0c376-114">Now that you have created an Azure Search index, you are almost ready to issue queries using the .NET SDK.</span></span> <span data-ttu-id="0c376-115">En primer lugar, debe obtener una de las claves de API de consulta que se generaron para aprovisionar el servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="0c376-115">First, you will need to obtain one of the query api-keys that was generated for the search service you provisioned.</span></span> <span data-ttu-id="0c376-116">El SDK para .NET enviará esta clave de API en cada solicitud al servicio.</span><span class="sxs-lookup"><span data-stu-id="0c376-116">The .NET SDK will send this api-key on every request to your service.</span></span> <span data-ttu-id="0c376-117">Tener una clave válida genera la confianza, solicitud a solicitud, entre la aplicación que envía la solicitud y el servicio que se encarga de ella.</span><span class="sxs-lookup"><span data-stu-id="0c376-117">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="0c376-118">Para buscar las claves de API del servicio, puede iniciar sesión en [Azure Portal](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="0c376-118">To find your service's api-keys you can sign in to the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="0c376-119">Vaya a la hoja de servicio de Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="0c376-119">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="0c376-120">Haga clic en el icono "Claves"</span><span class="sxs-lookup"><span data-stu-id="0c376-120">Click on the "Keys" icon</span></span>

<span data-ttu-id="0c376-121">El servicio tendrá *claves de administración* y *claves de consulta*.</span><span class="sxs-lookup"><span data-stu-id="0c376-121">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="0c376-122">Sus *claves de administración* principal y secundaria permiten conceder derechos completos para todas las operaciones, incluida la capacidad para administrar el servicio, crear y eliminar índices, indexadores y orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="0c376-122">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="0c376-123">Existen dos claves, de forma que puede usar la clave secundaria si decide volver a generar la clave principal y viceversa.</span><span class="sxs-lookup"><span data-stu-id="0c376-123">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="0c376-124">Las *claves de consulta* conceden acceso de solo lectura a índices y documentos y normalmente se distribuyen entre las aplicaciones cliente que emiten solicitudes de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="0c376-124">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="0c376-125">Para consultar un índice, puede utilizar una de las claves de consulta.</span><span class="sxs-lookup"><span data-stu-id="0c376-125">For the purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="0c376-126">Las claves de administración también se pueden utilizar para las consultas, pero debe utilizar una clave de consulta en el código de aplicación ya que esto se adapta mejor al [principio de privilegios mínimos](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="0c376-126">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows the [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="create-an-instance-of-the-searchindexclient-class"></a><span data-ttu-id="0c376-127">Creación de una instancia de la clase SearchIndexClient</span><span class="sxs-lookup"><span data-stu-id="0c376-127">Create an instance of the SearchIndexClient class</span></span>
<span data-ttu-id="0c376-128">Para emitir consultas con el SDK de .NET de Búsqueda de Azure, necesitará crear una instancia de la clase `SearchIndexClient` .</span><span class="sxs-lookup"><span data-stu-id="0c376-128">To issue queries with the Azure Search .NET SDK, you will need to create an instance of the `SearchIndexClient` class.</span></span> <span data-ttu-id="0c376-129">Esta clase tiene varios constructores.</span><span class="sxs-lookup"><span data-stu-id="0c376-129">This class has several constructors.</span></span> <span data-ttu-id="0c376-130">El que desea tiene el nombre del servicio de búsqueda, el nombre del índice y un objeto `SearchCredentials` como parámetros.</span><span class="sxs-lookup"><span data-stu-id="0c376-130">The one you want takes your search service name, index name, and a `SearchCredentials` object as parameters.</span></span> <span data-ttu-id="0c376-131">`SearchCredentials` incluye su clave de API.</span><span class="sxs-lookup"><span data-stu-id="0c376-131">`SearchCredentials` wraps your api-key.</span></span>

<span data-ttu-id="0c376-132">El código siguiente crea una nueva instancia de `SearchIndexClient` para el índice "hotels" (creado en [Creación de un índice de Azure Search mediante el SDK de .NET](search-create-index-dotnet.md)) con los valores de nombre de servicio de búsqueda y clave de API que se almacenan en el archivo de configuración de la aplicación (`appsettings.json` en el caso de la [aplicación de ejemplo](http://aka.ms/search-dotnet-howto)):</span><span class="sxs-lookup"><span data-stu-id="0c376-132">The code below creates a new `SearchIndexClient` for the "hotels" index (created in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md)) using values for the search service name and api-key that are stored in the application's config file (`appsettings.json` in the case of the [sample application](http://aka.ms/search-dotnet-howto)):</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="0c376-133">`SearchIndexClient` tiene una propiedad `Documents`.</span><span class="sxs-lookup"><span data-stu-id="0c376-133">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="0c376-134">Esta propiedad proporciona todos los métodos que necesita para consultar los índices de Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="0c376-134">This property provides all the methods you need to query Azure Search indexes.</span></span>

## <a name="query-your-index"></a><span data-ttu-id="0c376-135">Consulta del índice</span><span class="sxs-lookup"><span data-stu-id="0c376-135">Query your index</span></span>
<span data-ttu-id="0c376-136">Buscar con el SDK de .NET es tan sencillo como llamar al método `Documents.Search` en su `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="0c376-136">Searching with the .NET SDK is as simple as calling the `Documents.Search` method on your `SearchIndexClient`.</span></span> <span data-ttu-id="0c376-137">Este método usa unos cuantos parámetros, incluido el texto de búsqueda, además de un objeto `SearchParameters` que se puede usar para refinar la consulta.</span><span class="sxs-lookup"><span data-stu-id="0c376-137">This method takes a few parameters, including the search text, along with a `SearchParameters` object that can be used to further refine the query.</span></span>

#### <a name="types-of-queries"></a><span data-ttu-id="0c376-138">Tipos de consultas</span><span class="sxs-lookup"><span data-stu-id="0c376-138">Types of Queries</span></span>
<span data-ttu-id="0c376-139">Los dos [tipos de consultas](search-query-overview.md#types-of-queries) principales que usará son `search` y `filter`.</span><span class="sxs-lookup"><span data-stu-id="0c376-139">The two main [query types](search-query-overview.md#types-of-queries) you will use are `search` and `filter`.</span></span> <span data-ttu-id="0c376-140">Una consulta `search` realiza búsquedas de uno o más términos en todos los campos *habilitados para búsqueda* del índice.</span><span class="sxs-lookup"><span data-stu-id="0c376-140">A `search` query searches for one or more terms in all *searchable* fields in your index.</span></span> <span data-ttu-id="0c376-141">Una consulta `filter` evalúa una expresión booleana en todos los campos *filtrables* de un índice.</span><span class="sxs-lookup"><span data-stu-id="0c376-141">A `filter` query evaluates a boolean expression over all *filterable* fields in an index.</span></span>

<span data-ttu-id="0c376-142">Tanto los filtros como las búsquedas se realizan con el método `Documents.Search` .</span><span class="sxs-lookup"><span data-stu-id="0c376-142">Both searches and filters are performed using the `Documents.Search` method.</span></span> <span data-ttu-id="0c376-143">Se puede pasar una consulta de búsqueda en el parámetro `searchText`, mientras que una expresión de filtro se puede pasar en la propiedad `Filter` de la clase `SearchParameters`.</span><span class="sxs-lookup"><span data-stu-id="0c376-143">A search query can be passed in the `searchText` parameter, while a filter expression can be passed in the `Filter` property of the `SearchParameters` class.</span></span> <span data-ttu-id="0c376-144">Para filtrar sin buscar, solo tiene que pasar `"*"` al parámetro `searchText`.</span><span class="sxs-lookup"><span data-stu-id="0c376-144">To filter without searching, just pass `"*"` for the `searchText` parameter.</span></span> <span data-ttu-id="0c376-145">Para buscar sin filtrar, simplemente deje la propiedad `Filter` sin establecer, o no pase ninguna instancia de `SearchParameters`.</span><span class="sxs-lookup"><span data-stu-id="0c376-145">To search without filtering, just leave the `Filter` property unset, or do not pass in a `SearchParameters` instance at all.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="0c376-146">Consultas de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0c376-146">Example Queries</span></span>
<span data-ttu-id="0c376-147">El código de ejemplo siguiente muestra algunas formas de consultar el índice "hoteles" definido en [Creación de un índice de Búsqueda de Azure con el SDK de .NET](search-create-index-dotnet.md#DefineIndex).</span><span class="sxs-lookup"><span data-stu-id="0c376-147">The following sample code shows a few different ways to query the "hotels" index defined in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#DefineIndex).</span></span> <span data-ttu-id="0c376-148">Tenga en cuenta que los documentos que se devuelven con los resultados de búsqueda son instancias de la clase `Hotel` , que se definió en [Importación de datos en Búsqueda de Azure con el SDK de .NET](search-import-data-dotnet.md#HotelClass).</span><span class="sxs-lookup"><span data-stu-id="0c376-148">Note that the documents returned with the search results are instances of the `Hotel` class, which was defined in [Data Import in Azure Search using the .NET SDK](search-import-data-dotnet.md#HotelClass).</span></span> <span data-ttu-id="0c376-149">El código de ejemplo usa un método `WriteDocuments` para enviar los resultados de búsqueda a la consola.</span><span class="sxs-lookup"><span data-stu-id="0c376-149">The sample code makes use of a `WriteDocuments` method to output the search results to the console.</span></span> <span data-ttu-id="0c376-150">Este método se describe en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="0c376-150">This method is described in the next section.</span></span>

```csharp
SearchParameters parameters;
DocumentSearchResult<Hotel> results;

Console.WriteLine("Search the entire index for the term 'budget' and return only the hotelName field:\n");

parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);

Console.Write("Apply a filter to the index to find hotels cheaper than $150 per night, ");
Console.WriteLine("and return the hotelId and description:\n");

parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);

Console.Write("Search the entire index, order by a specific field (lastRenovationDate) ");
Console.Write("in descending order, take the top two results, and show only hotelName and ");
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

Console.WriteLine("Search the entire index for the term 'motel':\n");

parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

## <a name="handle-search-results"></a><span data-ttu-id="0c376-151">Control de los resultados de la búsqueda</span><span class="sxs-lookup"><span data-stu-id="0c376-151">Handle search results</span></span>
<span data-ttu-id="0c376-152">El método `Documents.Search` devuelve un objeto `DocumentSearchResult` que contiene los resultados de la consulta.</span><span class="sxs-lookup"><span data-stu-id="0c376-152">The `Documents.Search` method returns a `DocumentSearchResult` object that contains the results of the query.</span></span> <span data-ttu-id="0c376-153">En el ejemplo de la sección anterior, se usa un método llamado `WriteDocuments` para enviar los resultados de búsqueda a la consola:</span><span class="sxs-lookup"><span data-stu-id="0c376-153">The example in the previous section used a method called `WriteDocuments` to output the search results to the console:</span></span>

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

<span data-ttu-id="0c376-154">Este es el aspecto de los resultados de las consultas de la sección anterior, suponiendo que el índice "hoteles" contenga los datos de ejemplo de [Importación de datos en Búsqueda de Azure con el SDK de .NET](search-import-data-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="0c376-154">Here is what the results look like for the queries in the previous section, assuming the "hotels" index is populated with the sample data in [Data Import in Azure Search using the .NET SDK](search-import-data-dotnet.md):</span></span>

```
Search the entire index for the term 'budget' and return only the hotelName field:

Name: Roach Motel

Apply a filter to the index to find hotels cheaper than $150 per night, and return the hotelId and description:

ID: 2   Description: Cheapest hotel in town
ID: 3   Description: Close to town hall and the river

Search the entire index, order by a specific field (lastRenovationDate) in descending order, take the top two results, and show only hotelName and lastRenovationDate:

Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

Search the entire index for the term 'motel':

ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
```

<span data-ttu-id="0c376-155">El código de ejemplo anterior envía los resultados de búsqueda a la consola.</span><span class="sxs-lookup"><span data-stu-id="0c376-155">The sample code above uses the console to output search results.</span></span> <span data-ttu-id="0c376-156">Del mismo modo, necesitará mostrar los resultados de búsqueda en su propia aplicación.</span><span class="sxs-lookup"><span data-stu-id="0c376-156">You will likewise need to display search results in your own application.</span></span> <span data-ttu-id="0c376-157">Consulte [este ejemplo en GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) para ver cómo representar los resultados de búsqueda en una aplicación web basada en ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="0c376-157">See [this sample on GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) for an example of how to render search results in an ASP.NET MVC-based web application.</span></span>

