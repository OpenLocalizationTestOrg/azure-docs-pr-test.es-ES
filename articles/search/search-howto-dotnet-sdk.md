---
title: "Uso de Azure Search desde una aplicación .NET | Microsoft Docs"
description: "Cómo usar Búsqueda de Azure desde una aplicación .NET"
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
ms.openlocfilehash: 552a7ab193e12d2e72da494166d774e974c85d47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-search-from-a-net-application"></a><span data-ttu-id="03229-103">Cómo usar Búsqueda de Azure desde una aplicación .NET</span><span class="sxs-lookup"><span data-stu-id="03229-103">How to use Azure Search from a .NET Application</span></span>
<span data-ttu-id="03229-104">Este artículo es un tutorial para empezar a trabajar con el [SDK de Búsqueda de Azure para .NET](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="03229-104">This article is a walkthrough to get you up and running with the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span> <span data-ttu-id="03229-105">Puede utilizar el SDK para .NET para implementar una experiencia de búsqueda enriquecida en la aplicación mediante Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="03229-105">You can use the .NET SDK to implement a rich search experience in your application using Azure Search.</span></span>

## <a name="whats-in-the-azure-search-sdk"></a><span data-ttu-id="03229-106">Qué es el SDK de Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="03229-106">What's in the Azure Search SDK</span></span>
<span data-ttu-id="03229-107">El SDK contiene una biblioteca de cliente, `Microsoft.Azure.Search`.</span><span class="sxs-lookup"><span data-stu-id="03229-107">The SDK consists of a client library, `Microsoft.Azure.Search`.</span></span> <span data-ttu-id="03229-108">Permite administrar los índices, los orígenes de datos y los indizadores, así como cargar y administrar documentos y ejecutar consultas, todo ello sin tener que ocuparse de los detalles de HTTP y JSON.</span><span class="sxs-lookup"><span data-stu-id="03229-108">It enables you to manage your indexes, data sources, and indexers, as well as upload and manage documents, and execute queries, all without having to deal with the details of HTTP and JSON.</span></span>

<span data-ttu-id="03229-109">La biblioteca de cliente define clases como `Index`, `Field` y `Document`, además de operaciones como `Indexes.Create` y `Documents.Search` en las clases `SearchServiceClient` y `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="03229-109">The client library defines classes like `Index`, `Field`, and `Document`, as well as operations like `Indexes.Create` and `Documents.Search` on the `SearchServiceClient` and `SearchIndexClient` classes.</span></span> <span data-ttu-id="03229-110">Estas clases están organizadas en los espacios de nombres siguientes:</span><span class="sxs-lookup"><span data-stu-id="03229-110">These classes are organized into the following namespaces:</span></span>

* [<span data-ttu-id="03229-111">Microsoft.Azure.Search</span><span class="sxs-lookup"><span data-stu-id="03229-111">Microsoft.Azure.Search</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [<span data-ttu-id="03229-112">Microsoft.Azure.Search.Models</span><span class="sxs-lookup"><span data-stu-id="03229-112">Microsoft.Azure.Search.Models</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

<span data-ttu-id="03229-113">La versión actual del SDK de .NET para Búsqueda de Azure ya está disponible con carácter general.</span><span class="sxs-lookup"><span data-stu-id="03229-113">The current version of the Azure Search .NET SDK is now generally available.</span></span> <span data-ttu-id="03229-114">Si desea enviarnos comentarios para que los tengamos en cuenta en próxima versión, visite nuestra [página de comentarios](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="03229-114">If you would like to provide feedback for us to incorporate in the next version, please visit our [feedback page](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

<span data-ttu-id="03229-115">El SDK para .NET es compatible con la versión `2016-09-01` de la [API de REST de Azure Search](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="03229-115">The .NET SDK supports version `2016-09-01` of the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span> <span data-ttu-id="03229-116">Esta versión incluye ahora compatibilidad con analizadores personalizados y con el indexador de Azure Blob y Azure Table.</span><span class="sxs-lookup"><span data-stu-id="03229-116">This version now includes support for custom analyzers and Azure Blob and Azure Table indexer support.</span></span> <span data-ttu-id="03229-117">Existen características de versión preliminar que *no* son parte de esta versión, como la compatibilidad con la indexación de archivos JSON y CSV, que están [disponibles](search-api-2015-02-28-preview.md) mediante la versión [2.0-preview anterior del SDK para .NET](https://aka.ms/search-sdk-preview).</span><span class="sxs-lookup"><span data-stu-id="03229-117">Preview features that are *not* part of this version, such as support for indexing JSON and CSV files, are in [preview](search-api-2015-02-28-preview.md) and available via the older [2.0-preview version of the .NET SDK](https://aka.ms/search-sdk-preview).</span></span>

<span data-ttu-id="03229-118">Este SDK no admite [operaciones de administración](https://docs.microsoft.com/rest/api/searchmanagement/) como la creación y el escalado de servicios de Search y las claves de API de administración.</span><span class="sxs-lookup"><span data-stu-id="03229-118">This SDK does not support [Management Operations](https://docs.microsoft.com/rest/api/searchmanagement/) such as creating and scaling Search services and managing API keys.</span></span> <span data-ttu-id="03229-119">Si necesita administrar los recursos de Search desde una aplicación .NET, puede usar el [SDK de administración para .NET de Azure Search](https://aka.ms/search-mgmt-sdk).</span><span class="sxs-lookup"><span data-stu-id="03229-119">If you need to manage your Search resources from a .NET application, you can use the [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span></span>

## <a name="upgrading-to-the-latest-version-of-the-sdk"></a><span data-ttu-id="03229-120">Actualización a la versión más reciente del SDK</span><span class="sxs-lookup"><span data-stu-id="03229-120">Upgrading to the latest version of the SDK</span></span>
<span data-ttu-id="03229-121">Si ya utiliza una versión anterior del SDK de .NET para Búsqueda de Azure y desea actualizar a la nueva versión disponible, en [este artículo](search-dotnet-sdk-migration.md) se explica el proceso.</span><span class="sxs-lookup"><span data-stu-id="03229-121">If you're already using an older version of the Azure Search .NET SDK and you'd like to upgrade to the new generally available version, [this article](search-dotnet-sdk-migration.md) explains how.</span></span>

## <a name="requirements-for-the-sdk"></a><span data-ttu-id="03229-122">Requisitos para el SDK</span><span class="sxs-lookup"><span data-stu-id="03229-122">Requirements for the SDK</span></span>
1. <span data-ttu-id="03229-123">Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="03229-123">Visual Studio 2017.</span></span>
2. <span data-ttu-id="03229-124">Su propio servicio Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="03229-124">Your own Azure Search service.</span></span> <span data-ttu-id="03229-125">Para usar el SDK, será necesario el nombre del servicio y una o varias claves de API.</span><span class="sxs-lookup"><span data-stu-id="03229-125">In order to use the SDK, you will need the name of your service and one or more API keys.</span></span> <span data-ttu-id="03229-126">[Crear un servicio en el portal](search-create-service-portal.md) le ayudará con estos pasos.</span><span class="sxs-lookup"><span data-stu-id="03229-126">[Create a service in the portal](search-create-service-portal.md) will help you through these steps.</span></span>
3. <span data-ttu-id="03229-127">Descargue el [paquete NuGet](http://www.nuget.org/packages/Microsoft.Azure.Search) del SDK de Búsqueda de Azure para .NET mediante "Administrar paquetes de NuGet" en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="03229-127">Download the Azure Search .NET SDK [NuGet package](http://www.nuget.org/packages/Microsoft.Azure.Search) by using "Manage NuGet Packages" in Visual Studio.</span></span> <span data-ttu-id="03229-128">Solo tiene que buscar el nombre del paquete `Microsoft.Azure.Search` en NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="03229-128">Just search for the package name `Microsoft.Azure.Search` on NuGet.org.</span></span>

<span data-ttu-id="03229-129">El SDK de .NET de Azure Search es compatible con las aplicaciones destinadas a .NET Framework 4.6 y .NET Core.</span><span class="sxs-lookup"><span data-stu-id="03229-129">The Azure Search .NET SDK supports applications targeting the .NET Framework 4.6 and .NET Core.</span></span>

## <a name="core-scenarios"></a><span data-ttu-id="03229-130">Escenarios principales</span><span class="sxs-lookup"><span data-stu-id="03229-130">Core scenarios</span></span>
<span data-ttu-id="03229-131">Hay varias tareas que debe realizar en su aplicación de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="03229-131">There are several things you'll need to do in your search application.</span></span> <span data-ttu-id="03229-132">En este tutorial, hablaremos sobre estos escenarios básicos:</span><span class="sxs-lookup"><span data-stu-id="03229-132">In this tutorial, we'll cover these core scenarios:</span></span>

* <span data-ttu-id="03229-133">Creación de un índice</span><span class="sxs-lookup"><span data-stu-id="03229-133">Creating an index</span></span>
* <span data-ttu-id="03229-134">Llenado del índice con documentos</span><span class="sxs-lookup"><span data-stu-id="03229-134">Populating the index with documents</span></span>
* <span data-ttu-id="03229-135">Búsqueda de documentos mediante filtros y búsqueda de texto completo</span><span class="sxs-lookup"><span data-stu-id="03229-135">Searching for documents using full-text search and filters</span></span>

<span data-ttu-id="03229-136">El código de ejemplo siguiente expone cada una de ellas.</span><span class="sxs-lookup"><span data-stu-id="03229-136">The sample code that follows illustrates each of these.</span></span> <span data-ttu-id="03229-137">No dude en usar los fragmentos de código en su propia aplicación.</span><span class="sxs-lookup"><span data-stu-id="03229-137">Feel free to use the code snippets in your own application.</span></span>

### <a name="overview"></a><span data-ttu-id="03229-138">Información general</span><span class="sxs-lookup"><span data-stu-id="03229-138">Overview</span></span>
<span data-ttu-id="03229-139">La aplicación de ejemplo que vamos a explorar crea un nuevo índice denominado "hotels", lo rellena con varios documentos y, a continuación, ejecuta varias consultas de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="03229-139">The sample application we'll be exploring creates a new index named "hotels", populates it with a few documents, then executes some search queries.</span></span> <span data-ttu-id="03229-140">Este es el programa principal, que muestra el flujo general:</span><span class="sxs-lookup"><span data-stu-id="03229-140">Here is the main program, showing the overall flow:</span></span>

```csharp
// This sample shows how to delete, create, upload documents and query an index
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

    Console.WriteLine("{0}", "Complete.  Press any key to end application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> <span data-ttu-id="03229-141">Puede encontrar el código fuente completo de la aplicación de ejemplo usada en este tutorial en [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="03229-141">You can find the full source code of the sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>
> 
>

<span data-ttu-id="03229-142">Lo recorreremos paso a paso.</span><span class="sxs-lookup"><span data-stu-id="03229-142">We'll walk through this step by step.</span></span> <span data-ttu-id="03229-143">Primero, debemos crear un nuevo `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="03229-143">First we need to create a new `SearchServiceClient`.</span></span> <span data-ttu-id="03229-144">Este objeto le permite administrar índices.</span><span class="sxs-lookup"><span data-stu-id="03229-144">This object allows you to manage indexes.</span></span> <span data-ttu-id="03229-145">Para crear uno, deberá proporcionar el nombre de su servicio Búsqueda de Azure y una clave de API de administración.</span><span class="sxs-lookup"><span data-stu-id="03229-145">In order to construct one, you need to provide your Azure Search service name as well as an admin API key.</span></span> <span data-ttu-id="03229-146">Puede escribir esta información en el archivo `appsettings.json` de la [aplicación de ejemplo](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="03229-146">You can enter this information in the `appsettings.json` file of the [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

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
> <span data-ttu-id="03229-147">Si proporciona una clave incorrecta (por ejemplo, una clave de consulta cuando se requiere una clave de administración), el `SearchServiceClient` producirá un `CloudException` con el mensaje de error "Forbidden" (Prohibido) cuando llame a un método de operación con él, como `Indexes.Create`.</span><span class="sxs-lookup"><span data-stu-id="03229-147">If you provide an incorrect key (for example, a query key where an admin key was required), the `SearchServiceClient` will throw a `CloudException` with the error message "Forbidden" the first time you call an operation method on it, such as `Indexes.Create`.</span></span> <span data-ttu-id="03229-148">Si esto sucede, compruebe la clave de API.</span><span class="sxs-lookup"><span data-stu-id="03229-148">If this happens to you, double-check our API key.</span></span>
> 
> 

<span data-ttu-id="03229-149">Las siguientes líneas llaman a métodos para crear un índice llamado "hotels", eliminándolo antes si ya existe.</span><span class="sxs-lookup"><span data-stu-id="03229-149">The next few lines call methods to create an index named "hotels", deleting it first if it already exists.</span></span> <span data-ttu-id="03229-150">Describiremos estos métodos más adelante.</span><span class="sxs-lookup"><span data-stu-id="03229-150">We will walk through these methods a little later.</span></span>

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

<span data-ttu-id="03229-151">A continuación, el índice debe rellenarse.</span><span class="sxs-lookup"><span data-stu-id="03229-151">Next, the index needs to be populated.</span></span> <span data-ttu-id="03229-152">Para ello, necesitamos un `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="03229-152">To do this, we will need a `SearchIndexClient`.</span></span> <span data-ttu-id="03229-153">Hay dos maneras de obtener uno: se puede crear o se puede llamar a `Indexes.GetClient` en el `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="03229-153">There are two ways to obtain one: by constructing it, or by calling `Indexes.GetClient` on the `SearchServiceClient`.</span></span> <span data-ttu-id="03229-154">Usamos esta última por motivos de comodidad.</span><span class="sxs-lookup"><span data-stu-id="03229-154">We use the latter for convenience.</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="03229-155">En una aplicación de búsqueda típica, el llenado y la administración de índices se controlan mediante un componente independiente de las consultas de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="03229-155">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="03229-156">`Indexes.GetClient` resulta cómodo para rellenar un índice porque evita la molestia de dar otro `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="03229-156">`Indexes.GetClient` is convenient for populating an index because it saves you the trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="03229-157">Con este fin, pasa la clave de administrador que se usó para crear el `SearchServiceClient` al nuevo `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="03229-157">It does this by passing the admin key that you used to create the `SearchServiceClient` to the new `SearchIndexClient`.</span></span> <span data-ttu-id="03229-158">Sin embargo, en la parte de la aplicación que ejecuta consultas, es mejor crear directamente el `SearchIndexClient` para poder pasar una clave de consulta en lugar de una clave de administración.</span><span class="sxs-lookup"><span data-stu-id="03229-158">However, in the part of your application that executes queries, it is better to create the `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="03229-159">Esto está en consonancia con el principio de privilegios mínimos y le ayudará a proteger su aplicación.</span><span class="sxs-lookup"><span data-stu-id="03229-159">This is consistent with the principle of least privilege and will help to make your application more secure.</span></span> <span data-ttu-id="03229-160">Puede encontrar más información acerca de las claves de administración y consulta [aquí](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span><span class="sxs-lookup"><span data-stu-id="03229-160">You can find out more about admin keys and query keys [here](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span></span>
> 
> 

<span data-ttu-id="03229-161">Ahora que tenemos un `SearchIndexClient`, podemos rellenar el índice.</span><span class="sxs-lookup"><span data-stu-id="03229-161">Now that we have a `SearchIndexClient`, we can populate the index.</span></span> <span data-ttu-id="03229-162">Para ello utilizaremos otro método que tratamos más adelante.</span><span class="sxs-lookup"><span data-stu-id="03229-162">This is done by another method that we will walk through later.</span></span>

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

<span data-ttu-id="03229-163">Finalmente, ejecutamos algunas consultas de búsqueda y mostramos los resultados.</span><span class="sxs-lookup"><span data-stu-id="03229-163">Finally, we execute a few search queries and display the results.</span></span> <span data-ttu-id="03229-164">Esta vez usamos otro `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="03229-164">This time we use a different `SearchIndexClient`:</span></span>

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

<span data-ttu-id="03229-165">Echaremos un vistazo al método `RunQueries` más adelante.</span><span class="sxs-lookup"><span data-stu-id="03229-165">We will take a closer look at the `RunQueries` method later.</span></span> <span data-ttu-id="03229-166">Este es el código para crear el nuevo elemento `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="03229-166">Here is the code to create the new `SearchIndexClient`:</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="03229-167">Esta vez usamos una clave de consulta dado que no necesitamos acceso de escritura al índice.</span><span class="sxs-lookup"><span data-stu-id="03229-167">This time we use a query key since we do not need write access to the index.</span></span> <span data-ttu-id="03229-168">Puede escribir esta información en el archivo `appsettings.json` de la [aplicación de ejemplo](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="03229-168">You can enter this information in the `appsettings.json` file of the [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

<span data-ttu-id="03229-169">Si ejecuta esta aplicación con un nombre de servicio válido y claves de API, la salida será parecida a esta:</span><span class="sxs-lookup"><span data-stu-id="03229-169">If you run this application with a valid service name and API keys, the output should look like this:</span></span>

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents to be indexed...
    
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
    
    Complete.  Press any key to end application...

<span data-ttu-id="03229-170">El código fuente completo de la aplicación se proporciona al final de este artículo.</span><span class="sxs-lookup"><span data-stu-id="03229-170">The full source code of the application is provided at the end of this article.</span></span>

<span data-ttu-id="03229-171">A continuación, veremos más de cerca cada uno de los métodos llamados por `Main`.</span><span class="sxs-lookup"><span data-stu-id="03229-171">Next, we will take a closer look at each of the methods called by `Main`.</span></span>

### <a name="creating-an-index"></a><span data-ttu-id="03229-172">Creación de un índice</span><span class="sxs-lookup"><span data-stu-id="03229-172">Creating an index</span></span>
<span data-ttu-id="03229-173">Después de crear un `SearchServiceClient`, lo siguiente que hace `Main` es eliminar el índice "hotels" si ya existe.</span><span class="sxs-lookup"><span data-stu-id="03229-173">After creating a `SearchServiceClient`, the next thing `Main` does is delete the "hotels" index if it already exists.</span></span> <span data-ttu-id="03229-174">Esto se lleva a cabo mediante el método siguiente:</span><span class="sxs-lookup"><span data-stu-id="03229-174">That is done by the following method:</span></span>

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

<span data-ttu-id="03229-175">Este método utiliza el `SearchServiceClient` proporcionado para comprobar si existe el índice y, en ese caso, eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="03229-175">This method uses the given `SearchServiceClient` to check if the index exists, and if so, delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="03229-176">El código de ejemplo de este artículo usa los métodos sincrónicos del SDK de Búsqueda de Azure para .NET por motivos de simplicidad.</span><span class="sxs-lookup"><span data-stu-id="03229-176">The example code in this article uses the synchronous methods of the Azure Search .NET SDK for simplicity.</span></span> <span data-ttu-id="03229-177">En sus propias aplicaciones, recomendamos que use métodos asincrónicos para mantener su escalabilidad y capacidad de respuesta.</span><span class="sxs-lookup"><span data-stu-id="03229-177">We recommend that you use the asynchronous methods in your own applications to keep them scalable and responsive.</span></span> <span data-ttu-id="03229-178">Por ejemplo, en el método anterior podría utilizar `ExistsAsync` y `DeleteAsync` en lugar de `Exists` y `Delete`.</span><span class="sxs-lookup"><span data-stu-id="03229-178">For example, in the method above you could use `ExistsAsync` and `DeleteAsync` instead of `Exists` and `Delete`.</span></span>
> 
> 

<span data-ttu-id="03229-179">A continuación, `Main` crea un nuevo índice "hotels" mediante una llamada a este método:</span><span class="sxs-lookup"><span data-stu-id="03229-179">Next, `Main` creates a new "hotels" index by calling this method:</span></span>

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

<span data-ttu-id="03229-180">Este método crea un nuevo objeto `Index` con una lista de objetos `Field` que define el esquema del nuevo índice.</span><span class="sxs-lookup"><span data-stu-id="03229-180">This method creates a new `Index` object with a list of `Field` objects that defines the schema of the new index.</span></span> <span data-ttu-id="03229-181">Cada campo tiene un nombre, un tipo de datos y varios atributos que definen su comportamiento de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="03229-181">Each field has a name, data type, and several attributes that define its search behavior.</span></span> <span data-ttu-id="03229-182">La clase `FieldBuilder` usa reflexión para crear una lista de objetos `Field` para el índice examinando las propiedades públicas y los atributos de la clase de modelo `Hotel` dada.</span><span class="sxs-lookup"><span data-stu-id="03229-182">The `FieldBuilder` class uses reflection to create a list of `Field` objects for the index by examining the public properties and attributes of the given `Hotel` model class.</span></span> <span data-ttu-id="03229-183">Examinaremos más de cerca la clase `Hotel` más adelante.</span><span class="sxs-lookup"><span data-stu-id="03229-183">We'll take a closer look at the `Hotel` class later on.</span></span>

> [!NOTE]
> <span data-ttu-id="03229-184">En caso necesario, siempre puede crear la lista de objetos `Field` directamente en lugar de usar `FieldBuilder`.</span><span class="sxs-lookup"><span data-stu-id="03229-184">You can always create the list of `Field` objects directly instead of using `FieldBuilder` if needed.</span></span> <span data-ttu-id="03229-185">Por ejemplo, puede que no quiera usar una clase model o que necesite usar una clase model existente que no quiere modificar agregando atributos.</span><span class="sxs-lookup"><span data-stu-id="03229-185">For example, you may not want to use a model class or you may need to use an existing model class that you don't want to modify by adding attributes.</span></span>
>
> 

<span data-ttu-id="03229-186">Además de campos, puede agregar al índice perfiles de puntuación, proveedores de sugerencias u opciones de CORS (se omiten en el ejemplo para mayor brevedad).</span><span class="sxs-lookup"><span data-stu-id="03229-186">In addition to fields, you can also add scoring profiles, suggesters, or CORS options to the Index (these are omitted from the sample for brevity).</span></span> <span data-ttu-id="03229-187">Puede encontrar más información sobre el objeto Index y sus partes constituyentes en la [referencia del SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), así como en la [referencia de la API de REST de Azure Search](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="03229-187">You can find more information about the Index object and its constituent parts in the [SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), as well as in the [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

### <a name="populating-the-index"></a><span data-ttu-id="03229-188">Llenado del índice</span><span class="sxs-lookup"><span data-stu-id="03229-188">Populating the index</span></span>
<span data-ttu-id="03229-189">El siguiente paso en `Main` consiste en rellenar el índice recién creado.</span><span class="sxs-lookup"><span data-stu-id="03229-189">The next step in `Main` is to populate the newly-created index.</span></span> <span data-ttu-id="03229-190">Esto se lleva a cabo mediante el método siguiente:</span><span class="sxs-lookup"><span data-stu-id="03229-190">This is done in the following method:</span></span>

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
            Description = "Close to town hall and the river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

    try
    {
        indexClient.Documents.Index(batch);
    }
    catch (IndexBatchException e)
    {
        // Sometimes when your Search service is under load, indexing will fail for some of the documents in
        // the batch. Depending on your application, you can take compensating actions like delaying and
        // retrying. For this simple demo, we just log the failed document keys and continue.
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

    Console.WriteLine("Waiting for documents to be indexed...\n");
    Thread.Sleep(2000);
}
```

<span data-ttu-id="03229-191">Este método tiene cuatro partes.</span><span class="sxs-lookup"><span data-stu-id="03229-191">This method has four parts.</span></span> <span data-ttu-id="03229-192">La primera crea una matriz de objetos `Hotel` que serán los datos de entrada que cargaremos en el índice.</span><span class="sxs-lookup"><span data-stu-id="03229-192">The first creates an array of `Hotel` objects that will serve as our input data to upload to the index.</span></span> <span data-ttu-id="03229-193">Estos datos están incluidos en el código por motivos de simplicidad.</span><span class="sxs-lookup"><span data-stu-id="03229-193">This data is hard-coded for simplicity.</span></span> <span data-ttu-id="03229-194">En su propia aplicación, los datos provendrán normalmente de un origen de datos externo, como una base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="03229-194">In your own application, your data will likely come from an external data source such as a SQL database.</span></span>

<span data-ttu-id="03229-195">En la segunda parte se crea un `IndexBatch` que contiene los documentos.</span><span class="sxs-lookup"><span data-stu-id="03229-195">The second part creates an `IndexBatch` containing the documents.</span></span> <span data-ttu-id="03229-196">Especifique la operación que desee aplicar al lote en el momento de su creación, en este caso llamando a `IndexBatch.Upload`.</span><span class="sxs-lookup"><span data-stu-id="03229-196">You specify the operation you want to apply to the batch at the time you create it, in this case by calling `IndexBatch.Upload`.</span></span> <span data-ttu-id="03229-197">A continuación, el lote se carga en el índice de Búsqueda de Azure mediante el método `Documents.Index` .</span><span class="sxs-lookup"><span data-stu-id="03229-197">The batch is then uploaded to the Azure Search index by the `Documents.Index` method.</span></span>

> [!NOTE]
> <span data-ttu-id="03229-198">En este ejemplo nos limitamos a cargar documentos.</span><span class="sxs-lookup"><span data-stu-id="03229-198">In this example, we are just uploading documents.</span></span> <span data-ttu-id="03229-199">Si desea combinar los cambios en los documentos existentes o eliminar documentos, puede crear lotes llamando a `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` o `IndexBatch.Delete`.</span><span class="sxs-lookup"><span data-stu-id="03229-199">If you wanted to merge changes into existing documents or delete documents, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete` instead.</span></span> <span data-ttu-id="03229-200">También puede combinar diferentes operaciones en un único lote llamando a `IndexBatch.New`, que selecciona una colección de objetos de `IndexAction`, que indican a Búsqueda de Azure que realice una operación determinada en un documento.</span><span class="sxs-lookup"><span data-stu-id="03229-200">You can also mix different operations in a single batch by calling `IndexBatch.New`, which takes a collection of `IndexAction` objects, each of which tells Azure Search to perform a particular operation on a document.</span></span> <span data-ttu-id="03229-201">Puede crear cada `IndexAction` con su propia operación llamando al método correspondiente, como `IndexAction.Merge`, `IndexAction.Upload`, etc.</span><span class="sxs-lookup"><span data-stu-id="03229-201">You can create each `IndexAction` with its own operation by calling the corresponding method such as `IndexAction.Merge`, `IndexAction.Upload`, and so on.</span></span>
> 
> 

<span data-ttu-id="03229-202">La tercera parte de este método es un bloque catch que controla un caso de error importante para la indización.</span><span class="sxs-lookup"><span data-stu-id="03229-202">The third part of this method is a catch block that handles an important error case for indexing.</span></span> <span data-ttu-id="03229-203">Si su servicio Búsqueda de Azure no logra indizar algunos de los documentos del lote, aparece una `IndexBatchException` producida por `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="03229-203">If your Azure Search service fails to index some of the documents in the batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="03229-204">Esto puede suceder si indiza documentos mientras el servicio está sobrecargado.</span><span class="sxs-lookup"><span data-stu-id="03229-204">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="03229-205">**Recomendamos encarecidamente controlar este caso de forma explícita en el código.**</span><span class="sxs-lookup"><span data-stu-id="03229-205">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="03229-206">Puede retrasar la indización de los documentos que dieron error y volver a intentarlo; puede crear un registro y continuar, como hace el ejemplo, o puede adoptar otro enfoque según los requisitos de coherencia de datos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="03229-206">You can delay and then retry indexing the documents that failed, or you can log and continue like the sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="03229-207">Puede usar el método `FindFailedActionsToRetry` para construir un nuevo lote que contiene solo las acciones que dieron error en una llamada anterior a `Index`.</span><span class="sxs-lookup"><span data-stu-id="03229-207">You can use the `FindFailedActionsToRetry` method to construct a new batch containing only the actions that failed in a previous call to `Index`.</span></span> <span data-ttu-id="03229-208">El método está documentado [aquí](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) y puede encontrar una explicación de cómo se usa correctamente [en StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span><span class="sxs-lookup"><span data-stu-id="03229-208">The method is documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) and there is a discussion of how to properly use it [on StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span></span>
>
>

<span data-ttu-id="03229-209">Por último, el método `UploadDocuments` se retrasa durante dos segundos.</span><span class="sxs-lookup"><span data-stu-id="03229-209">Finally, the `UploadDocuments` method delays for two seconds.</span></span> <span data-ttu-id="03229-210">La indización ocurre de manera asincrónica en el servicio Búsqueda de Azure, por lo que la aplicación de ejemplo debe esperar unos momentos para asegurarse de que los documentos estén disponibles para la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="03229-210">Indexing happens asynchronously in your Azure Search service, so the sample application needs to wait a short time to ensure that the documents are available for searching.</span></span> <span data-ttu-id="03229-211">Retrasos así solo suelen ser necesarios en las pruebas, demostraciones y aplicaciones de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="03229-211">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

#### <a name="how-the-net-sdk-handles-documents"></a><span data-ttu-id="03229-212">Gestión de documentos del SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="03229-212">How the .NET SDK handles documents</span></span>
<span data-ttu-id="03229-213">Quizás se pregunte cómo consigue el SDK de Azure para .NET cargar en el índice las instancias de una clase definida por el usuario como `Hotel` .</span><span class="sxs-lookup"><span data-stu-id="03229-213">You may be wondering how the Azure Search .NET SDK is able to upload instances of a user-defined class like `Hotel` to the index.</span></span> <span data-ttu-id="03229-214">Para responder mejor a esa pregunta, echemos un vistazo a la clase `Hotel` :</span><span class="sxs-lookup"><span data-stu-id="03229-214">To help answer that question, let's look at the `Hotel` class:</span></span>

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// The SerializePropertyNamesAsCamelCase attribute is defined in the Azure Search .NET SDK.
// It ensures that Pascal-case property names in the model class are mapped to camel-case
// field names in the index.
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

<span data-ttu-id="03229-215">Lo primero que debe tener en cuenta es que cada propiedad pública de `Hotel` corresponde a un campo de la definición del índice, pero con una diferencia fundamental: el nombre de cada campo comienza con una letra minúscula ("mayúsculas y minúsculas Camel"), mientras que el nombre de cada propiedad pública de `Hotel` comienza con una letra mayúscula ("mayúsculas y minúsculas Pascal").</span><span class="sxs-lookup"><span data-stu-id="03229-215">The first thing to notice is that each public property of `Hotel` corresponds to a field in the index definition, but with one crucial difference: The name of each field starts with a lower-case letter ("camel case"), while the name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="03229-216">Se trata de un escenario común en las aplicaciones .NET que realizan enlaces de datos cuando el esquema de destino está fuera del control del desarrollador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="03229-216">This is a common scenario in .NET applications that perform data-binding where the target schema is outside the control of the application developer.</span></span> <span data-ttu-id="03229-217">En lugar de tener que infringir las directrices de nomenclatura de .NET utilizando mayúsculas y minúsculas Camel para los nombres de las propiedades, puede usar el atributo `[SerializePropertyNamesAsCamelCase]` para indicar al SDK que asigne los nombres de las propiedades automáticamente a mayúsculas y minúsculas Camel.</span><span class="sxs-lookup"><span data-stu-id="03229-217">Rather than having to violate the .NET naming guidelines by making property names camel-case, you can tell the SDK to map the property names to camel-case automatically with the `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="03229-218">El SDK de .NET para Búsqueda de Azure usa la biblioteca [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) para serializar y deserializar los objetos de modelo personalizados en JSON y de este.</span><span class="sxs-lookup"><span data-stu-id="03229-218">The Azure Search .NET SDK uses the [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library to serialize and deserialize your custom model objects to and from JSON.</span></span> <span data-ttu-id="03229-219">Puede personalizar esta serialización si es necesario.</span><span class="sxs-lookup"><span data-stu-id="03229-219">You can customize this serialization if needed.</span></span> <span data-ttu-id="03229-220">Para obtener más información, consulte [Serialización personalizada con JSON.NET](#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="03229-220">For more details, see [Custom Serialization with JSON.NET](#JsonDotNet).</span></span>
> 
> 

<span data-ttu-id="03229-221">El segundo aspecto que se debe tener en cuenta son los atributos, como `IsFilterable`, `IsSearchable`, `Key` y `Analyzer` que decoran cada propiedad pública.</span><span class="sxs-lookup"><span data-stu-id="03229-221">The second thing to notice are the attributes such as `IsFilterable`, `IsSearchable`, `Key`, and `Analyzer` that decorate each public property.</span></span> <span data-ttu-id="03229-222">Estos atributos se asignan directamente a los [atributos correspondientes del índice de Azure Search](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span><span class="sxs-lookup"><span data-stu-id="03229-222">These attributes map directly to the [corresponding attributes of the Azure Search index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span></span> <span data-ttu-id="03229-223">La clase `FieldBuilder` usa estos para construir definiciones de campo para el índice.</span><span class="sxs-lookup"><span data-stu-id="03229-223">The `FieldBuilder` class uses these to construct field definitions for the index.</span></span>

<span data-ttu-id="03229-224">El segundo aspecto importante sobre la clase `Hotel` son los tipos de datos de las propiedades públicas.</span><span class="sxs-lookup"><span data-stu-id="03229-224">The third important thing about the `Hotel` class are the data types of the public properties.</span></span> <span data-ttu-id="03229-225">Los tipos .NET de estas propiedades se asignan a los tipos de campo equivalentes de la definición del índice.</span><span class="sxs-lookup"><span data-stu-id="03229-225">The .NET types of  these properties map to their equivalent field types in the index definition.</span></span> <span data-ttu-id="03229-226">Por ejemplo, la propiedad de cadena `Category` se asigna al campo `category`, que es de tipo `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="03229-226">For example, the `Category` string property maps to the `category` field, which is of type `Edm.String`.</span></span> <span data-ttu-id="03229-227">Se dan asignaciones de tipos semejantes entre `bool?` y `Edm.Boolean`, `DateTimeOffset?` y `Edm.DateTimeOffset`, etc. Las reglas específicas para la asignación de tipos se documentan con el método `Documents.Get` en la [referencia del SDK de Azure Search para .NET](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="03229-227">There are similar type mappings between `bool?` and `Edm.Boolean`, `DateTimeOffset?` and `Edm.DateTimeOffset`, etc. The specific rules for the type mapping are documented with the `Documents.Get` method in the [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span> <span data-ttu-id="03229-228">Aunque la clase `FieldBuilder` se ocupa de esta asignación, todavía puede ser útil comprenderlo por si necesitara solucionar los problemas de serialización.</span><span class="sxs-lookup"><span data-stu-id="03229-228">The `FieldBuilder` class takes care of this mapping for you, but it can still be helpful to understand in case you need to troubleshoot any serialization issues.</span></span>

<span data-ttu-id="03229-229">Esta posibilidad de usar sus propias clases como documentos funciona en ambas direcciones: también puede recuperar los resultados de la búsqueda y hacer que el SDK los deserialice automáticamente a un tipo de su elección, como veremos en la siguiente sección.</span><span class="sxs-lookup"><span data-stu-id="03229-229">This ability to use your own classes as documents works in both directions; You can also retrieve search results and have the SDK automatically deserialize them to a type of your choice, as we will see in the next section.</span></span>

> [!NOTE]
> <span data-ttu-id="03229-230">El SDK de Búsqueda de Azure para .NET también admite documentos de tipo dinámico mediante la clase `Document`, que es una asignación clave/valor de nombres de campo a valores de campo.</span><span class="sxs-lookup"><span data-stu-id="03229-230">The Azure Search .NET SDK also supports dynamically-typed documents using the `Document` class, which is a key/value mapping of field names to field values.</span></span> <span data-ttu-id="03229-231">Esto es útil en escenarios en los que no se conoce el esquema del índice en el momento del diseño o en los que resulte inconveniente enlazar a clases de modelo específicas.</span><span class="sxs-lookup"><span data-stu-id="03229-231">This is useful in scenarios where you don't know the index schema at design-time, or where it would be inconvenient to bind to specific model classes.</span></span> <span data-ttu-id="03229-232">Todos los métodos del SDK que se ocupan de los documentos tienen sobrecargas que funcionan con la clase `Document` , así como sobrecargas de asignación rigurosa que aceptan un parámetro de tipo genérico.</span><span class="sxs-lookup"><span data-stu-id="03229-232">All the methods in the SDK that deal with documents have overloads that work with the `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="03229-233">En el código de ejemplo de este tutorial solo se utilizan las últimas.</span><span class="sxs-lookup"><span data-stu-id="03229-233">Only the latter are used in the sample code in this tutorial.</span></span> <span data-ttu-id="03229-234">La clase `Document` se hereda de `Dictionary<string, object>`.</span><span class="sxs-lookup"><span data-stu-id="03229-234">The `Document` class inherits from `Dictionary<string, object>`.</span></span> <span data-ttu-id="03229-235">Puede encontrar otros detalles [aquí](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span><span class="sxs-lookup"><span data-stu-id="03229-235">You can find other details [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span></span>
> 
> 

<span data-ttu-id="03229-236">**¿Por qué debería usar tipos de datos que aceptan valores null?**</span><span class="sxs-lookup"><span data-stu-id="03229-236">**Why you should use nullable data types**</span></span>

<span data-ttu-id="03229-237">Al diseñar sus propias clases de modelo para asignar a un índice de Búsqueda de Azure, es recomendable declarar las propiedades de tipos de valor como `bool` y `int` que aceptan valores NULL (por ejemplo: `bool?` en lugar de `bool`).</span><span class="sxs-lookup"><span data-stu-id="03229-237">When designing your own model classes to map to an Azure Search index, we recommend declaring properties of value types such as `bool` and `int` to be nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="03229-238">Si usa un tipo de modelo con una propiedad que no acepta valores NULL, tendrá que **garantizar** que ningún documento del índice contiene un valor NULL para el campo correspondiente.</span><span class="sxs-lookup"><span data-stu-id="03229-238">If you use a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="03229-239">Ni el SDK ni el servicio Búsqueda de Azure le permitirá aplicar esto.</span><span class="sxs-lookup"><span data-stu-id="03229-239">Neither the SDK nor the Azure Search service will help you to enforce this.</span></span>

<span data-ttu-id="03229-240">Esto no es solo una inquietud hipotética: imagine un escenario donde se agrega un nuevo campo a un índice existente que es de tipo `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="03229-240">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="03229-241">Después de actualizar la definición del índice, todos los documentos tendrán un valor null para ese campo nuevo (ya que todos los tipos aceptan valores NULL en Búsqueda de Azure).</span><span class="sxs-lookup"><span data-stu-id="03229-241">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="03229-242">Si después usa una clase de modelo con una propiedad `int` que no acepta valores NULL para ese campo, obtendrá `JsonSerializationException` así al intentar recuperar documentos:</span><span class="sxs-lookup"><span data-stu-id="03229-242">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="03229-243">Por este motivo, recomendamos utilizar tipos que aceptan valores NULL en las clases de modelo como procedimiento recomendado.</span><span class="sxs-lookup"><span data-stu-id="03229-243">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a><span data-ttu-id="03229-244">Serialización personalizada con JSON.NET</span><span class="sxs-lookup"><span data-stu-id="03229-244">Custom Serialization with JSON.NET</span></span>
<span data-ttu-id="03229-245">El SDK usa JSON.NET para serializar y deserializar documentos.</span><span class="sxs-lookup"><span data-stu-id="03229-245">The SDK uses JSON.NET for serializing and deserializing documents.</span></span> <span data-ttu-id="03229-246">Puede personalizar la serialización y deserialización si lo necesita definiendo su propio `JsonConverter` o `IContractResolver` (consulte la [documentación JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) para obtener más detalles).</span><span class="sxs-lookup"><span data-stu-id="03229-246">You can customize serialization and deserialization if needed by defining your own `JsonConverter` or `IContractResolver` (see the [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) for more details).</span></span> <span data-ttu-id="03229-247">Esto puede ser útil cuando desea adaptar una clase de modelo existente de la aplicación para usarla con Búsqueda de Azure y otros escenarios más avanzados.</span><span class="sxs-lookup"><span data-stu-id="03229-247">This can be useful when you want to adapt an existing model class from your application for use with Azure Search, and other more advanced scenarios.</span></span> <span data-ttu-id="03229-248">Por ejemplo, con la serialización personalizada, puede:</span><span class="sxs-lookup"><span data-stu-id="03229-248">For example, with custom serialization you can:</span></span>

* <span data-ttu-id="03229-249">Incluir o excluir determinadas propiedades de la clase de modelo para que se almacenen como campos del documento.</span><span class="sxs-lookup"><span data-stu-id="03229-249">Include or exclude certain properties of your model class from being stored as document fields.</span></span>
* <span data-ttu-id="03229-250">Asignar entre los nombres de propiedad del código y los nombres de campo del índice.</span><span class="sxs-lookup"><span data-stu-id="03229-250">Map between property names in your code and field names in your index.</span></span>
* <span data-ttu-id="03229-251">Cree atributos personalizados que se puedan usar para asignar propiedades a campos de documento.</span><span class="sxs-lookup"><span data-stu-id="03229-251">Create custom attributes that can be used for mapping properties to document fields.</span></span>

<span data-ttu-id="03229-252">Puede encontrar ejemplos de implementación de serialización personalizada en las pruebas unitarias del SDK de .NET para Búsqueda de Azure en GitHub.</span><span class="sxs-lookup"><span data-stu-id="03229-252">You can find examples of implementing custom serialization in the unit tests for the Azure Search .NET SDK on GitHub.</span></span> <span data-ttu-id="03229-253">[Esta carpeta](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models) es un buen punto de partida.</span><span class="sxs-lookup"><span data-stu-id="03229-253">A good starting point is [this folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span></span> <span data-ttu-id="03229-254">Contiene clases que las pruebas de serialización personalizada utilizan.</span><span class="sxs-lookup"><span data-stu-id="03229-254">It contains classes that are used by the custom serialization tests.</span></span>

### <a name="searching-for-documents-in-the-index"></a><span data-ttu-id="03229-255">Búsqueda de documentos en el índice</span><span class="sxs-lookup"><span data-stu-id="03229-255">Searching for documents in the index</span></span>
<span data-ttu-id="03229-256">El último paso de la aplicación de ejemplo es buscar algunos documentos en el índice.</span><span class="sxs-lookup"><span data-stu-id="03229-256">The last step in the sample application is to search for some documents in the index.</span></span> <span data-ttu-id="03229-257">Esto es lo que hace el método siguiente:</span><span class="sxs-lookup"><span data-stu-id="03229-257">The following method does this:</span></span>

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
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
}
```

<span data-ttu-id="03229-258">Cada vez que ejecuta una consulta, este método crea primero un nuevo objeto `SearchParameters`.</span><span class="sxs-lookup"><span data-stu-id="03229-258">Each time it executes a query, this method first creates a new `SearchParameters` object.</span></span> <span data-ttu-id="03229-259">Esto se utiliza para especificar opciones adicionales para la consulta, como el orden, los filtros, la paginación y las facetas.</span><span class="sxs-lookup"><span data-stu-id="03229-259">This is used to specify additional options for the query such as sorting, filtering, paging, and faceting.</span></span> <span data-ttu-id="03229-260">En este método, vamos a establecer la propiedad `Filter`, `Select`, `OrderBy` y `Top` para diferentes consultas.</span><span class="sxs-lookup"><span data-stu-id="03229-260">In this method, we're setting the `Filter`, `Select`, `OrderBy`, and `Top` property for different queries.</span></span> <span data-ttu-id="03229-261">Todas las `SearchParameters`propiedades se documentan [aquí](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span><span class="sxs-lookup"><span data-stu-id="03229-261">All the `SearchParameters` properties are documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span></span>

<span data-ttu-id="03229-262">El siguiente paso consiste en ejecutar la consulta de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="03229-262">The next step is to actually execute the search query.</span></span> <span data-ttu-id="03229-263">Esto se hace mediante el método `Documents.Search`:</span><span class="sxs-lookup"><span data-stu-id="03229-263">This is done using the `Documents.Search` method.</span></span> <span data-ttu-id="03229-264">Para cada consulta, pasamos el texto de búsqueda para usarlo como cadena (o `"*"` si no hay ningún texto de búsqueda), además de los parámetros de búsqueda creados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="03229-264">For each query, we pass the search text to use as a string (or `"*"` if there is no search text), plus the search parameters created earlier.</span></span> <span data-ttu-id="03229-265">También especificamos `Hotel` como el parámetro de tipo para `Documents.Search`, lo que indica al SDK que deserialice los documentos de los resultados de búsqueda en objetos de tipo `Hotel`.</span><span class="sxs-lookup"><span data-stu-id="03229-265">We also specify `Hotel` as the type parameter for `Documents.Search`, which tells the SDK to deserialize documents in the search results into objects of type `Hotel`.</span></span>

> [!NOTE]
> <span data-ttu-id="03229-266">Puede encontrar más información acerca de la sintaxis de expresiones de consulta de búsqueda [aquí](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="03229-266">You can find more information about the search query expression syntax [here](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span></span>
> 
> 

<span data-ttu-id="03229-267">Por último, después de cada consulta este método recorre en iteración todas las coincidencias de los resultados de búsqueda e imprime cada documento en la consola:</span><span class="sxs-lookup"><span data-stu-id="03229-267">Finally, after each query this method iterates through all the matches in the search results, printing each document to the console:</span></span>

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

<span data-ttu-id="03229-268">Examinemos más de cerca cada una de las consultas de una en una.</span><span class="sxs-lookup"><span data-stu-id="03229-268">Let's take a closer look at each of the queries in turn.</span></span> <span data-ttu-id="03229-269">Este es el código para ejecutar la primera consulta:</span><span class="sxs-lookup"><span data-stu-id="03229-269">Here is the code to execute the first query:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

<span data-ttu-id="03229-270">En este caso, estamos buscando hoteles que coincidan con la palabra "presupuesto" y queremos que los resultados solo devuelvan los nombres de hotel, como especifica el parámetro `Select`.</span><span class="sxs-lookup"><span data-stu-id="03229-270">In this case, we're searching for hotels that match the word "budget", and we want to get back only the hotel names, as specified by the `Select` parameter.</span></span> <span data-ttu-id="03229-271">Estos son los resultados:</span><span class="sxs-lookup"><span data-stu-id="03229-271">Here are the results:</span></span>

    Name: Roach Motel

<span data-ttu-id="03229-272">A continuación, queremos encontrar los hoteles con una tarifa por noche inferior a 150 dólares USA y que solo se devuelvan el identificador del hotel y la descripción:</span><span class="sxs-lookup"><span data-stu-id="03229-272">Next, we want to find the hotels with a nightly rate of less than $150, and return only the hotel ID and description:</span></span>

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

<span data-ttu-id="03229-273">Esta consulta usa una expresión `$filter` de OData, `baseRate lt 150`, para filtrar los documentos del índice.</span><span class="sxs-lookup"><span data-stu-id="03229-273">This query uses an OData `$filter` expression, `baseRate lt 150`, to filter the documents in the index.</span></span> <span data-ttu-id="03229-274">Puede encontrar más información acerca de la sintaxis de OData admitida por Búsqueda de Azure [aquí](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="03229-274">You can find out more about the OData syntax that Azure Search supports [here](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span></span>

<span data-ttu-id="03229-275">Estos son los resultados de la consulta:</span><span class="sxs-lookup"><span data-stu-id="03229-275">Here are the results of the query:</span></span>

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close to town hall and the river

<span data-ttu-id="03229-276">Seguidamente, quiere encontrar los dos mejores hoteles que se han renovado más recientemente y mostrar el nombre del hotel y la última fecha de renovación.</span><span class="sxs-lookup"><span data-stu-id="03229-276">Next, we want to find the top two hotels that have been most recently renovated, and show the hotel name and last renovation date.</span></span> <span data-ttu-id="03229-277">Este es el código:</span><span class="sxs-lookup"><span data-stu-id="03229-277">Here is the code:</span></span> 

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

<span data-ttu-id="03229-278">En este caso, usamos de nuevo la sintaxis de OData para especificar el parámetro `OrderBy` como `lastRenovationDate desc`.</span><span class="sxs-lookup"><span data-stu-id="03229-278">In this case, we again use OData syntax to specify the `OrderBy` parameter as `lastRenovationDate desc`.</span></span> <span data-ttu-id="03229-279">También establecemos `Top` en 2 para tener la seguridad de que solo obtenemos los dos documentos principales.</span><span class="sxs-lookup"><span data-stu-id="03229-279">We also set `Top` to 2 to ensure we only get the top two documents.</span></span> <span data-ttu-id="03229-280">Como antes, establecemos `Select` para especificar los campos que se deben devolver.</span><span class="sxs-lookup"><span data-stu-id="03229-280">As before, we set `Select` to specify which fields should be returned.</span></span>

<span data-ttu-id="03229-281">Estos son los resultados:</span><span class="sxs-lookup"><span data-stu-id="03229-281">Here are the results:</span></span>

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

<span data-ttu-id="03229-282">Por último, queremos encontrar todos los hoteles que coinciden con la palabra "motel":</span><span class="sxs-lookup"><span data-stu-id="03229-282">Finally, we want to find all hotels that match the word "motel":</span></span>

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

<span data-ttu-id="03229-283">Y estos son los resultados, que incluyen todos los campos, ya que no se especificó la propiedad `Select`:</span><span class="sxs-lookup"><span data-stu-id="03229-283">And here are the results, which include all fields since we did not specify the `Select` property:</span></span>

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

<span data-ttu-id="03229-284">Este paso finaliza el tutorial, pero no se detenga aquí.</span><span class="sxs-lookup"><span data-stu-id="03229-284">This step completes the tutorial, but don't stop here.</span></span> <span data-ttu-id="03229-285">**pasos siguientes** proporcionan recursos adicionales para obtener más información acerca de Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="03229-285">**Next steps** provides additional resources for learning more about Azure Search.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03229-286">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="03229-286">Next steps</span></span>
* <span data-ttu-id="03229-287">Examine las referencias del [SDK para .NET](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) y la [API de REST](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="03229-287">Browse the references for the [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
* <span data-ttu-id="03229-288">Profundice en sus conocimientos por medio de [vídeos y otros ejemplos y tutoriales](search-video-demo-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="03229-288">Deepen your knowledge through [videos and other samples and tutorials](search-video-demo-tutorial-list.md).</span></span>
* <span data-ttu-id="03229-289">Consulte las [convenciones de nomenclatura](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) para conocer las reglas que deben seguir los nombres de diversos objetos.</span><span class="sxs-lookup"><span data-stu-id="03229-289">Review [naming conventions](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) to learn the rules for naming various objects.</span></span>
* <span data-ttu-id="03229-290">Consulte los [tipos de datos admitidos](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) en Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="03229-290">Review [supported data types](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span></span>
