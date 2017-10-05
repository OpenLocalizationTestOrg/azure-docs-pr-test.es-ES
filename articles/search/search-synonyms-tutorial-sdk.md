---
title: "Tutorial de la versión preliminar de sinónimos en Azure Search | Microsoft Docs"
description: "Incorporación de la característica de versión preliminar de sinónimos a un índice de Azure Search."
services: search
manager: jhubbard
documentationcenter: 
author: HeidiSteen
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 03/31/2017
ms.author: heidist
ms.openlocfilehash: 014959ed471f796d2184f0f8ff10d15cdc8a2ec6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="synonym-preview-c-tutorial-for-azure-search"></a><span data-ttu-id="eb9dc-103">Tutorial C# de sinónimos (versión preliminar) para Azure Search</span><span class="sxs-lookup"><span data-stu-id="eb9dc-103">Synonym (preview) C# tutorial for Azure Search</span></span>

<span data-ttu-id="eb9dc-104">Los sinónimos amplían una consulta realizando coincidencias con términos que se consideran equivalentes semánticamente al término de entrada.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-104">Synonyms expand a query by matching on terms considered semantically equivalent to the input term.</span></span> <span data-ttu-id="eb9dc-105">Por ejemplo, podría interesarle que "coche" obtenga coincidencias con documentos que contengan los términos "automóvil" o "vehículo".</span><span class="sxs-lookup"><span data-stu-id="eb9dc-105">For example, you might want "car" to match documents containing the terms "automobile" or "vehicle".</span></span>

<span data-ttu-id="eb9dc-106">En Azure Search, los sinónimos se definen en un *mapa de sinónimos* a través de *reglas de asignación* que permiten asociar términos equivalentes.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-106">In Azure Search, synonyms are defined in a *synonym map*, through *mapping rules* that associate equivalent terms.</span></span> <span data-ttu-id="eb9dc-107">Puede crear varios mapas de sinónimos, publicarlos como un recurso de todo el servicio disponible para todos los índices y, a continuación, hacer referencia a cuál desea usar en el nivel de campo.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-107">You can create multiple synonym maps, post them as a service-wide resource available to any index, and then reference which one to use at the field level.</span></span> <span data-ttu-id="eb9dc-108">En el momento de la consulta, además de buscar un índice, Azure Search realiza una búsqueda en un mapa de sinónimos, si se especifica uno en los campos usados en la consulta.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-108">At query time, in addition to searching an index, Azure Search does a lookup in a synonym map, if one is specified on fields used in the query.</span></span>

> [!NOTE]
> <span data-ttu-id="eb9dc-109">La característica de sinónimos está actualmente en versión preliminar y solo se admite en las versiones preliminares más recientes de API y SDK (api-version=2016-09-01-Preview, SDK version 4.x-preview).</span><span class="sxs-lookup"><span data-stu-id="eb9dc-109">The synonyms feature is currently in preview and only supported in the latest preview API and SDK versions (api-version=2016-09-01-Preview, SDK version 4.x-preview).</span></span> <span data-ttu-id="eb9dc-110">En este momento no hay compatibilidad con Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-110">There is no Azure portal support at this time.</span></span> <span data-ttu-id="eb9dc-111">La versión preliminar de las API no se someten a las condiciones del Acuerdo de Nivel de Servicio y sus características pueden cambiar, por lo que no se recomienda su uso en aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-111">Preview APIs are not under SLA and preview features may change, so we do not recommend using them in production applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb9dc-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="eb9dc-112">Prerequisites</span></span>

<span data-ttu-id="eb9dc-113">Los requisitos del tutorial incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="eb9dc-113">Tutorial requirements include the following:</span></span>

* [<span data-ttu-id="eb9dc-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="eb9dc-114">Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="eb9dc-115">Un servicio de Azure Search</span><span class="sxs-lookup"><span data-stu-id="eb9dc-115">Azure Search service</span></span>](search-create-service-portal.md)
* [<span data-ttu-id="eb9dc-116">Versión preliminar de la biblioteca Microsoft.Azure.Search .NET</span><span class="sxs-lookup"><span data-stu-id="eb9dc-116">Preview version of Microsoft.Azure.Search .NET library</span></span>](https://aka.ms/search-sdk-preview)
* [<span data-ttu-id="eb9dc-117">Cómo usar Azure Search desde una aplicación .NET</span><span class="sxs-lookup"><span data-stu-id="eb9dc-117">How to use Azure Search from a .NET Application</span></span>](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a><span data-ttu-id="eb9dc-118">Información general</span><span class="sxs-lookup"><span data-stu-id="eb9dc-118">Overview</span></span>

<span data-ttu-id="eb9dc-119">Las consultas de antes y después del uso de sinónimos muestran el valor de los mismos.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-119">Before-and-after queries demonstrate the value of synonyms.</span></span> <span data-ttu-id="eb9dc-120">En este tutorial, usamos una aplicación de ejemplo que ejecuta consultas y devuelve los resultados en un índice de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-120">In this tutorial, we use a sample application that executes queries and returns results on a sample index.</span></span> <span data-ttu-id="eb9dc-121">La aplicación de ejemplo crea un índice pequeño denominado "hotels" rellenado con dos documentos.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-121">The sample application creates a small index named "hotels" populated with two documents.</span></span> <span data-ttu-id="eb9dc-122">La aplicación ejecuta consultas de búsqueda usando términos y frases que no aparecen en el índice, habilita la característica de sinónimos y vuelve a realizar las mismas búsquedas.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-122">The application executes search queries using terms and phrases that do not appear in the index, enables the synonyms feature, then issues the same searches again.</span></span> <span data-ttu-id="eb9dc-123">El código siguiente muestra el flujo general.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-123">The code below demonstrates the overall flow.</span></span>

```csharp
  static void Main(string[] args)
  {
      SearchServiceClient serviceClient = CreateSearchServiceClient();

      Console.WriteLine("{0}", "Cleaning up resources...\n");
      CleanupResources(serviceClient);

      Console.WriteLine("{0}", "Creating index...\n");
      CreateHotelsIndex(serviceClient);

      ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

      Console.WriteLine("{0}", "Uploading documents...\n");
      UploadDocuments(indexClient);

      ISearchIndexClient indexClientForQueries = CreateSearchIndexClient();

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Adding synonyms...\n");
      UploadSynonyms(serviceClient);
      EnableSynonymsInHotelsIndex(serviceClient);
      Thread.Sleep(10000); // Wait for the changes to propagate

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Complete.  Press any key to end application...\n");

      Console.ReadKey();
  }
```
<span data-ttu-id="eb9dc-124">Se explican los pasos necesarios para crear y rellenar el índice de ejemplo en [Cómo usar Azure Search desde una aplicación .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span><span class="sxs-lookup"><span data-stu-id="eb9dc-124">The steps to create and populate the sample index are explained in [How to use Azure Search from a .NET Application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

## <a name="before-queries"></a><span data-ttu-id="eb9dc-125">Consultas "antes de"</span><span class="sxs-lookup"><span data-stu-id="eb9dc-125">"Before" queries</span></span>

<span data-ttu-id="eb9dc-126">En `RunQueriesWithNonExistentTermsInIndex`, se emiten consultas de búsqueda con "five star", "internet" y "economy AND hotel".</span><span class="sxs-lookup"><span data-stu-id="eb9dc-126">In `RunQueriesWithNonExistentTermsInIndex`, we issue search queries with "five star", "internet", and "economy AND hotel".</span></span>
```csharp
Console.WriteLine("Search the entire index for the phrase \"five star\":\n");
results = indexClient.Documents.Search<Hotel>("\"five star\"", parameters);
WriteDocuments(results);

Console.WriteLine("Search the entire index for the term 'internet':\n");
results = indexClient.Documents.Search<Hotel>("internet", parameters);
WriteDocuments(results);

Console.WriteLine("Search the entire index for the terms 'economy' AND 'hotel':\n");
results = indexClient.Documents.Search<Hotel>("economy AND hotel", parameters);
WriteDocuments(results);
```
<span data-ttu-id="eb9dc-127">Ninguno de los dos documentos indexados contienen los términos, por lo que obtenemos el siguiente resultado del primer `RunQueriesWithNonExistentTermsInIndex`.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-127">Neither of the two indexed documents contain the terms, so we get the following output from the first `RunQueriesWithNonExistentTermsInIndex`.</span></span>
~~~
Search the entire index for the phrase "five star":

no document matched

Search the entire index for the term 'internet':

no document matched

Search the entire index for the terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a><span data-ttu-id="eb9dc-128">Habilitación de sinónimos</span><span class="sxs-lookup"><span data-stu-id="eb9dc-128">Enable synonyms</span></span>

<span data-ttu-id="eb9dc-129">La habilitación de sinónimos es un proceso de dos pasos.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-129">Enabling synonyms is a two-step process.</span></span> <span data-ttu-id="eb9dc-130">Primero se definen y cargan reglas de sinónimos y, a continuación, se configuran los campos para utilizarlos.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-130">We first define and upload synonym rules and then configure fields to use them.</span></span> <span data-ttu-id="eb9dc-131">El proceso se describe en `UploadSynonyms` y `EnableSynonymsInHotelsIndex`.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-131">The process is outlined in `UploadSynonyms` and `EnableSynonymsInHotelsIndex`.</span></span>

1. <span data-ttu-id="eb9dc-132">Agregue un mapa de sinónimos al servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-132">Add a synonym map to your search service.</span></span> <span data-ttu-id="eb9dc-133">En `UploadSynonyms`, definimos cuatro reglas en nuestro mapa de sinónimos 'desc synonymmap' y lo cargamos en el servicio.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-133">In `UploadSynonyms`, we define four rules in our synonym map 'desc-synonymmap' and upload to the service.</span></span>
```csharp
    var synonymMap = new SynonymMap()
    {
        Name = "desc-synonymmap",
        Format = "solr",
        Synonyms = "hotel, motel\n
                    internet,wifi\n
                    five star=>luxury\n
                    economy,inexpensive=>budget"
    };

    serviceClient.SynonymMaps.CreateOrUpdate(synonymMap);
```
<span data-ttu-id="eb9dc-134">Un mapa de sinónimos tiene que cumplir el formato `solr` de estándar de código abierto.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-134">A synonym map must conform to the open source standard `solr` format.</span></span> <span data-ttu-id="eb9dc-135">El formato se explica en [Synonyms in Azure Search](search-synonyms.md) (Sinónimos en Azure Search) en la sección `Apache Solr synonym format`.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-135">The format is explained in [Synonyms in Azure Search](search-synonyms.md) under the section `Apache Solr synonym format`.</span></span>

2. <span data-ttu-id="eb9dc-136">Configure los campos de búsqueda para utilizar el mapa de sinónimos en la definición del índice.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-136">Configure searchable fields to use the synonym map in the index definition.</span></span> <span data-ttu-id="eb9dc-137">En `EnableSynonymsInHotelsIndex`, habilitaremos los sinónimos en dos campos `category` y `tags` estableciendo la propiedad `synonymMaps` en el nombre del mapa de sinónimos recién cargado.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-137">In `EnableSynonymsInHotelsIndex`, we enable synonyms on two fields `category` and `tags` by setting the `synonymMaps` property to the name of the newly uploaded synonym map.</span></span>
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
<span data-ttu-id="eb9dc-138">Al agregar un mapa de sinónimos, no son necesarias las recompilaciones de índices.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-138">When you add a synonym map, index rebuilds are not required.</span></span> <span data-ttu-id="eb9dc-139">Puede agregar un mapa de sinónimos a su servicio y luego modificar las definiciones de campo existentes en los índices para usar el nuevo mapa de sinónimos.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-139">You can add a synonym map to your service, and then amend existing field definitions in any index to use the new synonym map.</span></span> <span data-ttu-id="eb9dc-140">La adición de nuevos atributos no influye en la disponibilidad de los índices.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-140">The addition of new attributes has no impact on index availability.</span></span> <span data-ttu-id="eb9dc-141">Lo mismo se aplica a la deshabilitación de sinónimos para un campo.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-141">The same applies in disabling synonyms for a field.</span></span> <span data-ttu-id="eb9dc-142">Simplemente establezca la propiedad `synonymMaps` en una lista vacía.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-142">You can simply set the `synonymMaps` property to an empty list.</span></span>
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a><span data-ttu-id="eb9dc-143">Consultas "después de"</span><span class="sxs-lookup"><span data-stu-id="eb9dc-143">"After" queries</span></span>

<span data-ttu-id="eb9dc-144">Después cargar el mapa de sinónimos y de actualizar el índice para que use el mapa de sinónimos, la segunda llamada a `RunQueriesWithNonExistentTermsInIndex` genera lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="eb9dc-144">After the synonym map is uploaded and the index is updated to use the synonym map, the second `RunQueriesWithNonExistentTermsInIndex` call outputs the following:</span></span>

~~~
Search the entire index for the phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search the entire index for the term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search the entire index for the terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
<span data-ttu-id="eb9dc-145">La primera consulta busca el documento a partir de la regla `five star=>luxury`.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-145">The first query finds the document from the rule `five star=>luxury`.</span></span> <span data-ttu-id="eb9dc-146">La segunda consulta amplía la búsqueda utilizando `internet,wifi` y la tercera usando `hotel, motel` y `economy,inexpensive=>budget` en la búsqueda de coincidencia en los documentos.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-146">The second query expands the search using `internet,wifi` and the third using both `hotel, motel` and `economy,inexpensive=>budget` in finding the documents they matched.</span></span>

<span data-ttu-id="eb9dc-147">Agregar sinónimos cambia totalmente la experiencia de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-147">Adding synonyms completely changes the search experience.</span></span> <span data-ttu-id="eb9dc-148">En este tutorial, las consultas originales devolvieron resultados significativos, aunque los documentos en nuestro índice eran relevantes.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-148">In this tutorial, the original queries failed to return meaningful results even though the documents in our index were relevant.</span></span> <span data-ttu-id="eb9dc-149">Al habilitar sinónimos, podemos ampliar un índice para incluir los términos de uso común, sin realizar cambios en los datos subyacentes en el índice.</span><span class="sxs-lookup"><span data-stu-id="eb9dc-149">By enabling synonyms, we can expand an index to include terms in common use, with no changes to underlying data in the index.</span></span>

## <a name="sample-application-source-code"></a><span data-ttu-id="eb9dc-150">Código fuente de aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="eb9dc-150">Sample application source code</span></span>
<span data-ttu-id="eb9dc-151">Puede encontrar el código fuente completo de la aplicación de ejemplo usada en este tutorial en [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span><span class="sxs-lookup"><span data-stu-id="eb9dc-151">You can find the full source code of the sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb9dc-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eb9dc-152">Next steps</span></span>

* <span data-ttu-id="eb9dc-153">Revise [cómo utilizar sinónimos en Azure Search](search-synonyms.md)</span><span class="sxs-lookup"><span data-stu-id="eb9dc-153">Review [How to use synonyms in Azure Search](search-synonyms.md)</span></span>
* <span data-ttu-id="eb9dc-154">Revise la [documentación sobre el uso de sinónimos con la API de REST](https://aka.ms/rgm6rq)</span><span class="sxs-lookup"><span data-stu-id="eb9dc-154">Review [Synonyms REST API documentation](https://aka.ms/rgm6rq)</span></span>
* <span data-ttu-id="eb9dc-155">Examine las referencias del [SDK para .NET](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) y la [API de REST](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="eb9dc-155">Browse the references for the [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
