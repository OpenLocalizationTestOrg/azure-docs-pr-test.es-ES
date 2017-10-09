---
title: "aaaSynonyms obtener una vista previa de tutorial en búsqueda de Azure | Documentos de Microsoft"
description: "Agregar el índice tooan característica de hello sinónimos vista previa en búsqueda de Azure."
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
ms.openlocfilehash: 055c1cbafb945823a3dc4da0c522db236b1d192c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="synonym-preview-c-tutorial-for-azure-search"></a><span data-ttu-id="a21c3-103">Tutorial C# de sinónimos (versión preliminar) para Azure Search</span><span class="sxs-lookup"><span data-stu-id="a21c3-103">Synonym (preview) C# tutorial for Azure Search</span></span>

<span data-ttu-id="a21c3-104">Sinónimos expandir una consulta que coincida en términos que se considera como término de entrada toohello semánticamente equivalente.</span><span class="sxs-lookup"><span data-stu-id="a21c3-104">Synonyms expand a query by matching on terms considered semantically equivalent toohello input term.</span></span> <span data-ttu-id="a21c3-105">Por ejemplo, conviene documentos de toomatch "car" que contiene términos Hola "automóvil" o "vehicle".</span><span class="sxs-lookup"><span data-stu-id="a21c3-105">For example, you might want "car" toomatch documents containing hello terms "automobile" or "vehicle".</span></span>

<span data-ttu-id="a21c3-106">En Azure Search, los sinónimos se definen en un *mapa de sinónimos* a través de *reglas de asignación* que permiten asociar términos equivalentes.</span><span class="sxs-lookup"><span data-stu-id="a21c3-106">In Azure Search, synonyms are defined in a *synonym map*, through *mapping rules* that associate equivalent terms.</span></span> <span data-ttu-id="a21c3-107">Puede crear varias asignaciones de sinónimo, registrarlos como un índice de tooany disponible de recursos de todo el servicio y, a continuación, hacer referencia a qué un toouse nivel de campo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a21c3-107">You can create multiple synonym maps, post them as a service-wide resource available tooany index, and then reference which one toouse at hello field level.</span></span> <span data-ttu-id="a21c3-108">En el momento de la consulta, además toosearching un índice, búsqueda de Azure realiza una búsqueda en un mapa de sinónimo, si se especifica en los campos usados en consultas de Hola.</span><span class="sxs-lookup"><span data-stu-id="a21c3-108">At query time, in addition toosearching an index, Azure Search does a lookup in a synonym map, if one is specified on fields used in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="a21c3-109">sinónimos de Hello característica está actualmente en vista previa y solo es compatible en Hola última versión preliminar de API y las versiones del SDK (api-version = 2016-09-01-versión preliminar, versión SDK 4.x-vista previa).</span><span class="sxs-lookup"><span data-stu-id="a21c3-109">hello synonyms feature is currently in preview and only supported in hello latest preview API and SDK versions (api-version=2016-09-01-Preview, SDK version 4.x-preview).</span></span> <span data-ttu-id="a21c3-110">En este momento no es compatible con Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a21c3-110">There is no Azure portal support at this time.</span></span> <span data-ttu-id="a21c3-111">La versión preliminar de las API no se someten a las condiciones del Acuerdo de Nivel de Servicio y sus características pueden cambiar, por lo que no se recomienda su uso en aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="a21c3-111">Preview APIs are not under SLA and preview features may change, so we do not recommend using them in production applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a21c3-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a21c3-112">Prerequisites</span></span>

<span data-ttu-id="a21c3-113">Requisitos del tutorial Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="a21c3-113">Tutorial requirements include hello following:</span></span>

* [<span data-ttu-id="a21c3-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a21c3-114">Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="a21c3-115">Un servicio de Azure Search</span><span class="sxs-lookup"><span data-stu-id="a21c3-115">Azure Search service</span></span>](search-create-service-portal.md)
* [<span data-ttu-id="a21c3-116">Versión preliminar de la biblioteca Microsoft.Azure.Search .NET</span><span class="sxs-lookup"><span data-stu-id="a21c3-116">Preview version of Microsoft.Azure.Search .NET library</span></span>](https://aka.ms/search-sdk-preview)
* [<span data-ttu-id="a21c3-117">Cómo toouse Azure buscar desde una aplicación .NET</span><span class="sxs-lookup"><span data-stu-id="a21c3-117">How toouse Azure Search from a .NET Application</span></span>](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a><span data-ttu-id="a21c3-118">Información general</span><span class="sxs-lookup"><span data-stu-id="a21c3-118">Overview</span></span>

<span data-ttu-id="a21c3-119">Las consultas de antes y después muestra el valor de Hola de sinónimos.</span><span class="sxs-lookup"><span data-stu-id="a21c3-119">Before-and-after queries demonstrate hello value of synonyms.</span></span> <span data-ttu-id="a21c3-120">En este tutorial, usamos una aplicación de ejemplo que ejecuta consultas y devuelve los resultados en un índice de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a21c3-120">In this tutorial, we use a sample application that executes queries and returns results on a sample index.</span></span> <span data-ttu-id="a21c3-121">aplicación de ejemplo de Hola crea un índice pequeño denominado "hoteles" rellenados con dos documentos.</span><span class="sxs-lookup"><span data-stu-id="a21c3-121">hello sample application creates a small index named "hotels" populated with two documents.</span></span> <span data-ttu-id="a21c3-122">aplicación Hello ejecuta consultas de búsqueda con los términos y frases que no aparecen en el índice de hello, habilita la característica de sinónimos de hello, a continuación, problemas de Hola mismas búsquedas de nuevo.</span><span class="sxs-lookup"><span data-stu-id="a21c3-122">hello application executes search queries using terms and phrases that do not appear in hello index, enables hello synonyms feature, then issues hello same searches again.</span></span> <span data-ttu-id="a21c3-123">código de Hello siguiente muestra hello flujo general.</span><span class="sxs-lookup"><span data-stu-id="a21c3-123">hello code below demonstrates hello overall flow.</span></span>

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
      Thread.Sleep(10000); // Wait for hello changes toopropagate

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");

      Console.ReadKey();
  }
```
<span data-ttu-id="a21c3-124">Hola toocreate de pasos y rellenar índice de ejemplo de Hola se explican en [cómo toouse Azure buscar desde una aplicación .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span><span class="sxs-lookup"><span data-stu-id="a21c3-124">hello steps toocreate and populate hello sample index are explained in [How toouse Azure Search from a .NET Application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

## <a name="before-queries"></a><span data-ttu-id="a21c3-125">Consultas "antes de"</span><span class="sxs-lookup"><span data-stu-id="a21c3-125">"Before" queries</span></span>

<span data-ttu-id="a21c3-126">En `RunQueriesWithNonExistentTermsInIndex`, se emiten consultas de búsqueda con "five star", "internet" y "economy AND hotel".</span><span class="sxs-lookup"><span data-stu-id="a21c3-126">In `RunQueriesWithNonExistentTermsInIndex`, we issue search queries with "five star", "internet", and "economy AND hotel".</span></span>
```csharp
Console.WriteLine("Search hello entire index for hello phrase \"five star\":\n");
results = indexClient.Documents.Search<Hotel>("\"five star\"", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello term 'internet':\n");
results = indexClient.Documents.Search<Hotel>("internet", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello terms 'economy' AND 'hotel':\n");
results = indexClient.Documents.Search<Hotel>("economy AND hotel", parameters);
WriteDocuments(results);
```
<span data-ttu-id="a21c3-127">Ninguno de los documentos indizados dos Hola contienen términos de hello, por lo que obtenemos siguiente de hello resultado de hello primero `RunQueriesWithNonExistentTermsInIndex`.</span><span class="sxs-lookup"><span data-stu-id="a21c3-127">Neither of hello two indexed documents contain hello terms, so we get hello following output from hello first `RunQueriesWithNonExistentTermsInIndex`.</span></span>
~~~
Search hello entire index for hello phrase "five star":

no document matched

Search hello entire index for hello term 'internet':

no document matched

Search hello entire index for hello terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a><span data-ttu-id="a21c3-128">Habilitación de sinónimos</span><span class="sxs-lookup"><span data-stu-id="a21c3-128">Enable synonyms</span></span>

<span data-ttu-id="a21c3-129">La habilitación de sinónimos es un proceso de dos pasos.</span><span class="sxs-lookup"><span data-stu-id="a21c3-129">Enabling synonyms is a two-step process.</span></span> <span data-ttu-id="a21c3-130">Se primero se definen y cargar reglas del sinónimo y, a continuación, configurar campos toouse ellos.</span><span class="sxs-lookup"><span data-stu-id="a21c3-130">We first define and upload synonym rules and then configure fields toouse them.</span></span> <span data-ttu-id="a21c3-131">proceso de Hola se resume en `UploadSynonyms` y `EnableSynonymsInHotelsIndex`.</span><span class="sxs-lookup"><span data-stu-id="a21c3-131">hello process is outlined in `UploadSynonyms` and `EnableSynonymsInHotelsIndex`.</span></span>

1. <span data-ttu-id="a21c3-132">Agregar un servicio de búsqueda de tooyour de asignación de sinónimo.</span><span class="sxs-lookup"><span data-stu-id="a21c3-132">Add a synonym map tooyour search service.</span></span> <span data-ttu-id="a21c3-133">En `UploadSynonyms`, definimos cuatro reglas en el mapa de sinónimo 'desc synonymmap' y cargar el servicio toohello.</span><span class="sxs-lookup"><span data-stu-id="a21c3-133">In `UploadSynonyms`, we define four rules in our synonym map 'desc-synonymmap' and upload toohello service.</span></span>
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
<span data-ttu-id="a21c3-134">Un mapa de sinónimo debe cumplir el estándar de código abierto de toohello `solr` formato.</span><span class="sxs-lookup"><span data-stu-id="a21c3-134">A synonym map must conform toohello open source standard `solr` format.</span></span> <span data-ttu-id="a21c3-135">formato de Hola se explica en [sinónimos en búsqueda de Azure](search-synonyms.md) en la sección de hello `Apache Solr synonym format`.</span><span class="sxs-lookup"><span data-stu-id="a21c3-135">hello format is explained in [Synonyms in Azure Search](search-synonyms.md) under hello section `Apache Solr synonym format`.</span></span>

2. <span data-ttu-id="a21c3-136">Configurar asignación de campos de búsqueda toouse Hola sinónimo en la definición del índice Hola.</span><span class="sxs-lookup"><span data-stu-id="a21c3-136">Configure searchable fields toouse hello synonym map in hello index definition.</span></span> <span data-ttu-id="a21c3-137">En `EnableSynonymsInHotelsIndex`, se permiten sinónimos en dos campos `category` y `tags` por establecer hello `synonymMaps` toohello nombre de propiedad Hola recién cargado mapa de sinónimo.</span><span class="sxs-lookup"><span data-stu-id="a21c3-137">In `EnableSynonymsInHotelsIndex`, we enable synonyms on two fields `category` and `tags` by setting hello `synonymMaps` property toohello name of hello newly uploaded synonym map.</span></span>
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
<span data-ttu-id="a21c3-138">Al agregar un mapa de sinónimos, no son necesarias las recompilaciones de índices.</span><span class="sxs-lookup"><span data-stu-id="a21c3-138">When you add a synonym map, index rebuilds are not required.</span></span> <span data-ttu-id="a21c3-139">Puede agregar un servicio de tooyour de asignación de sinónimo y, a continuación, modificar las definiciones de campo existentes en cualquier índice toouse Hola nuevo sinónimo mapa.</span><span class="sxs-lookup"><span data-stu-id="a21c3-139">You can add a synonym map tooyour service, and then amend existing field definitions in any index toouse hello new synonym map.</span></span> <span data-ttu-id="a21c3-140">Adición de Hola de nuevos atributos no influye en la disponibilidad del índice.</span><span class="sxs-lookup"><span data-stu-id="a21c3-140">hello addition of new attributes has no impact on index availability.</span></span> <span data-ttu-id="a21c3-141">Hola que esto mismo se aplica en deshabilitar sinónimos para un campo.</span><span class="sxs-lookup"><span data-stu-id="a21c3-141">hello same applies in disabling synonyms for a field.</span></span> <span data-ttu-id="a21c3-142">Simplemente establezca hello `synonymMaps` lista vacía de tooan de propiedad.</span><span class="sxs-lookup"><span data-stu-id="a21c3-142">You can simply set hello `synonymMaps` property tooan empty list.</span></span>
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a><span data-ttu-id="a21c3-143">Consultas "después de"</span><span class="sxs-lookup"><span data-stu-id="a21c3-143">"After" queries</span></span>

<span data-ttu-id="a21c3-144">Después de que se carga el mapa de sinónimo de Hola y el índice de hello es mapa de sinónimo de hello toouse actualizado, en segundo lugar Hola `RunQueriesWithNonExistentTermsInIndex` llamada genera siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="a21c3-144">After hello synonym map is uploaded and hello index is updated toouse hello synonym map, hello second `RunQueriesWithNonExistentTermsInIndex` call outputs hello following:</span></span>

~~~
Search hello entire index for hello phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
<span data-ttu-id="a21c3-145">consulta primera Hola busca Hola documento de regla de hello `five star=>luxury`.</span><span class="sxs-lookup"><span data-stu-id="a21c3-145">hello first query finds hello document from hello rule `five star=>luxury`.</span></span> <span data-ttu-id="a21c3-146">segunda consulta de Hola expande Hola búsqueda mediante `internet,wifi` y hello en tercer lugar usa ambos `hotel, motel` y `economy,inexpensive=>budget` en Buscar documentos de Hola comparan.</span><span class="sxs-lookup"><span data-stu-id="a21c3-146">hello second query expands hello search using `internet,wifi` and hello third using both `hotel, motel` and `economy,inexpensive=>budget` in finding hello documents they matched.</span></span>

<span data-ttu-id="a21c3-147">Agregar sinónimos completamente cambia la experiencia de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="a21c3-147">Adding synonyms completely changes hello search experience.</span></span> <span data-ttu-id="a21c3-148">En este tutorial, consultas de hello original no pudo resultados significativos tooreturn incluso si los documentos de hello en nuestro índice están relevantes.</span><span class="sxs-lookup"><span data-stu-id="a21c3-148">In this tutorial, hello original queries failed tooreturn meaningful results even though hello documents in our index were relevant.</span></span> <span data-ttu-id="a21c3-149">Al habilitar sinónimos, podemos expandir un tooinclude índice términos de uso común, con ningún dato de toounderlying cambios en el índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="a21c3-149">By enabling synonyms, we can expand an index tooinclude terms in common use, with no changes toounderlying data in hello index.</span></span>

## <a name="sample-application-source-code"></a><span data-ttu-id="a21c3-150">Código fuente de aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a21c3-150">Sample application source code</span></span>
<span data-ttu-id="a21c3-151">Puede encontrar el código fuente completo de Hola de aplicación de ejemplo de Hola utilizado en este tutorial en [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span><span class="sxs-lookup"><span data-stu-id="a21c3-151">You can find hello full source code of hello sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a21c3-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a21c3-152">Next steps</span></span>

* <span data-ttu-id="a21c3-153">Revisión [cómo toouse sinónimos en búsqueda de Azure](search-synonyms.md)</span><span class="sxs-lookup"><span data-stu-id="a21c3-153">Review [How toouse synonyms in Azure Search](search-synonyms.md)</span></span>
* <span data-ttu-id="a21c3-154">Revise la [documentación sobre el uso de sinónimos con la API de REST](https://aka.ms/rgm6rq)</span><span class="sxs-lookup"><span data-stu-id="a21c3-154">Review [Synonyms REST API documentation](https://aka.ms/rgm6rq)</span></span>
* <span data-ttu-id="a21c3-155">Examinar las referencias de Hola para hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) y [API de REST](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="a21c3-155">Browse hello references for hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
