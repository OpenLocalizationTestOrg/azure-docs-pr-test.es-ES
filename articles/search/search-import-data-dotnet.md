---
title: "aaa \"cargar datos (. NET - búsqueda de Azure) | Documentos de Microsoft\""
description: "Obtenga información acerca de cómo índice de tooan tooupload datos en búsqueda de Azure con Hola .NET SDK."
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: 
ms.assetid: 0e0e7e7b-7178-4c26-95c6-2fd1e8015aca
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/13/2017
ms.author: brjohnst
ms.openlocfilehash: 78ddbefb522884d1f61cb275c25c091487aee639
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-net-sdk"></a><span data-ttu-id="3beec-103">Carga datos tooAzure búsqueda mediante Hola SDK para .NET</span><span class="sxs-lookup"><span data-stu-id="3beec-103">Upload data tooAzure Search using hello .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3beec-104">Información general</span><span class="sxs-lookup"><span data-stu-id="3beec-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="3beec-105">.NET</span><span class="sxs-lookup"><span data-stu-id="3beec-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="3beec-106">REST</span><span class="sxs-lookup"><span data-stu-id="3beec-106">REST</span></span>](search-import-data-rest-api.md)
> 
> 

<span data-ttu-id="3beec-107">En este artículo le mostrará cómo hello toouse [SDK de .NET de búsqueda de Azure](https://aka.ms/search-sdk) tooimport datos en un índice de búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="3beec-107">This article will show you how toouse hello [Azure Search .NET SDK](https://aka.ms/search-sdk) tooimport data into an Azure Search index.</span></span>

<span data-ttu-id="3beec-108">Antes de comenzar este tutorial, debe haber [creado ya un índice de Búsqueda de Azure](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="3beec-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span> <span data-ttu-id="3beec-109">En este artículo también se da por supuesto que ya ha creado un `SearchServiceClient` de objeto, como se muestra en [crear un índice de búsqueda de Azure con .NET SDK hello](search-create-index-dotnet.md#CreateSearchServiceClient).</span><span class="sxs-lookup"><span data-stu-id="3beec-109">This article also assumes that you have already created a `SearchServiceClient` object, as shown in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span></span>

> [!NOTE]
> <span data-ttu-id="3beec-110">Todo el código de ejemplo de este artículo está escrito en C#.</span><span class="sxs-lookup"><span data-stu-id="3beec-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="3beec-111">Puede encontrar el código fuente completo hello [en GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="3beec-111">You can find hello full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="3beec-112">También puede leer sobre hello [SDK de .NET de búsqueda de Azure](search-howto-dotnet-sdk.md) para un tutorial más detallado del código de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3beec-112">You can also read about hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of hello sample code.</span></span>

<span data-ttu-id="3beec-113">En los documentos de toopush de orden en el índice mediante Hola .NET SDK, necesitará:</span><span class="sxs-lookup"><span data-stu-id="3beec-113">In order toopush documents into your index using hello .NET SDK, you will need to:</span></span>

1. <span data-ttu-id="3beec-114">Crear un `SearchIndexClient` índice de búsqueda de objeto tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="3beec-114">Create a `SearchIndexClient` object tooconnect tooyour search index.</span></span>
2. <span data-ttu-id="3beec-115">Crear un `IndexBatch` que contiene Hola documentos toobe agregado, modificado o eliminado.</span><span class="sxs-lookup"><span data-stu-id="3beec-115">Create an `IndexBatch` containing hello documents toobe added, modified, or deleted.</span></span>
3. <span data-ttu-id="3beec-116">Llamar a hello `Documents.Index` método de su `SearchIndexClient` toosend hello `IndexBatch` tooyour índice de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="3beec-116">Call hello `Documents.Index` method of your `SearchIndexClient` toosend hello `IndexBatch` tooyour search index.</span></span>

## <a name="create-an-instance-of-hello-searchindexclient-class"></a><span data-ttu-id="3beec-117">Cree una instancia de hello SearchIndexClient (clase)</span><span class="sxs-lookup"><span data-stu-id="3beec-117">Create an instance of hello SearchIndexClient class</span></span>
<span data-ttu-id="3beec-118">tooimport datos en el índice utilizando Hola SDK de .NET de búsqueda de Azure, necesitará toocreate una instancia de hello `SearchIndexClient` clase.</span><span class="sxs-lookup"><span data-stu-id="3beec-118">tooimport data into your index using hello Azure Search .NET SDK, you will need toocreate an instance of hello `SearchIndexClient` class.</span></span> <span data-ttu-id="3beec-119">Puede construir esta instancia usted mismo, pero es más fácil si ya tiene un `SearchServiceClient` instancia toocall su `Indexes.GetClient` método.</span><span class="sxs-lookup"><span data-stu-id="3beec-119">You can construct this instance yourself, but it's easier if you already have a `SearchServiceClient` instance toocall its `Indexes.GetClient` method.</span></span> <span data-ttu-id="3beec-120">Por ejemplo, mostramos cómo que obtendría un `SearchIndexClient` para índice de hello denominado "hoteles" desde un `SearchServiceClient` denominado `serviceClient`:</span><span class="sxs-lookup"><span data-stu-id="3beec-120">For example, here is how you would obtain a `SearchIndexClient` for hello index named "hotels" from a `SearchServiceClient` named `serviceClient`:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="3beec-121">En una aplicación de búsqueda típica, el llenado y la administración de índices se controlan mediante un componente independiente de las consultas de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="3beec-121">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="3beec-122">`Indexes.GetClient`es conveniente para rellenar un índice porque ahorra Hola problemas de proporcionar otro `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="3beec-122">`Indexes.GetClient` is convenient for populating an index because it saves you hello trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="3beec-123">Esto hace pasar clave de administración de Hola que Hola de toocreate usado se `SearchServiceClient` toohello nueva `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="3beec-123">It does this by passing hello admin key that you used toocreate hello `SearchServiceClient` toohello new `SearchIndexClient`.</span></span> <span data-ttu-id="3beec-124">Sin embargo, en la parte de saludo de la aplicación ejecuta consultas, es mejor hello toocreate `SearchIndexClient` directamente para que pueda pasar de una clave de consulta en lugar de una clave de administración.</span><span class="sxs-lookup"><span data-stu-id="3beec-124">However, in hello part of your application that executes queries, it is better toocreate hello `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="3beec-125">Esto es coherente con hello [principio de privilegios mínimos](https://en.wikipedia.org/wiki/Principle_of_least_privilege) y que le ayudará a toomake la aplicación más segura.</span><span class="sxs-lookup"><span data-stu-id="3beec-125">This is consistent with hello [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) and will help toomake your application more secure.</span></span> <span data-ttu-id="3beec-126">Puede encontrar más información sobre las claves de administración y las claves de consulta en hello [referencia de API de REST de búsqueda de Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="3beec-126">You can find out more about admin keys and query keys in hello [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
> 
> 

<span data-ttu-id="3beec-127">`SearchIndexClient` tiene una propiedad `Documents`.</span><span class="sxs-lookup"><span data-stu-id="3beec-127">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="3beec-128">Esta propiedad proporciona todos los métodos de hello necesarios tooadd, modificar, eliminar o consultar documentos en el índice.</span><span class="sxs-lookup"><span data-stu-id="3beec-128">This property provides all hello methods you need tooadd, modify, delete, or query documents in your index.</span></span>

## <a name="decide-which-indexing-action-toouse"></a><span data-ttu-id="3beec-129">Decidir qué indización toouse de acción</span><span class="sxs-lookup"><span data-stu-id="3beec-129">Decide which indexing action toouse</span></span>
<span data-ttu-id="3beec-130">datos de tooimport mediante Hola .NET SDK, deberá toopackage seguridad de los datos en un `IndexBatch` objeto.</span><span class="sxs-lookup"><span data-stu-id="3beec-130">tooimport data using hello .NET SDK, you will need toopackage up your data into an `IndexBatch` object.</span></span> <span data-ttu-id="3beec-131">Un `IndexBatch` encapsula una colección de `IndexAction` objetos, cada uno de los cuales contiene un documento y una propiedad que indica qué tooperform de acción de búsqueda de Azure en el documento (carga, merge, delete, etcetera).</span><span class="sxs-lookup"><span data-stu-id="3beec-131">An `IndexBatch` encapsulates a collection of `IndexAction` objects, each of which contains a document and a property that tells Azure Search what action tooperform on that document (upload, merge, delete, etc).</span></span> <span data-ttu-id="3beec-132">Dependiendo de cuál de hello debajo de acciones que elija, se deben incluidos para cada documento solo algunos de los campos:</span><span class="sxs-lookup"><span data-stu-id="3beec-132">Depending on which of hello below actions you choose, only certain fields must be included for each document:</span></span>

| <span data-ttu-id="3beec-133">Acción</span><span class="sxs-lookup"><span data-stu-id="3beec-133">Action</span></span> | <span data-ttu-id="3beec-134">Description</span><span class="sxs-lookup"><span data-stu-id="3beec-134">Description</span></span> | <span data-ttu-id="3beec-135">Campos necesarios para cada documento</span><span class="sxs-lookup"><span data-stu-id="3beec-135">Necessary fields for each document</span></span> | <span data-ttu-id="3beec-136">Notas</span><span class="sxs-lookup"><span data-stu-id="3beec-136">Notes</span></span> |
| --- | --- | --- | --- |
| `Upload` |<span data-ttu-id="3beec-137">Un `Upload` acción es similar tooan "upsert" donde se insertan si es nuevo y actualiza/reemplaza si existe el documento de Hola.</span><span class="sxs-lookup"><span data-stu-id="3beec-137">An `Upload` action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="3beec-138">clave, además de cualquier otro campo que se va a toodefine</span><span class="sxs-lookup"><span data-stu-id="3beec-138">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="3beec-139">Al actualizar o reemplazar un documento existente, cualquier campo que no se especifica en la solicitud de hello tendrá su campo establecido demasiado`null`.</span><span class="sxs-lookup"><span data-stu-id="3beec-139">When updating/replacing an existing document, any field that is not specified in hello request will have its field set too`null`.</span></span> <span data-ttu-id="3beec-140">Esto sucede incluso si el campo Hola anteriormente se estableció un valor no null tooa.</span><span class="sxs-lookup"><span data-stu-id="3beec-140">This occurs even when hello field was previously set tooa non-null value.</span></span> |
| `Merge` |<span data-ttu-id="3beec-141">Las actualizaciones existentes de documentos con hello especifican campos.</span><span class="sxs-lookup"><span data-stu-id="3beec-141">Updates an existing document with hello specified fields.</span></span> <span data-ttu-id="3beec-142">Si el documento de hello no existe en el índice de hello, se producirá un error en la mezcla de Hola.</span><span class="sxs-lookup"><span data-stu-id="3beec-142">If hello document does not exist in hello index, hello merge will fail.</span></span> |<span data-ttu-id="3beec-143">clave, además de cualquier otro campo que se va a toodefine</span><span class="sxs-lookup"><span data-stu-id="3beec-143">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="3beec-144">Cualquier campo que se especifica en una combinación reemplazará el campo existente de hello en el documento de Hola.</span><span class="sxs-lookup"><span data-stu-id="3beec-144">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="3beec-145">Aquí se incluyen los campos de tipo `DataType.Collection(DataType.String)`.</span><span class="sxs-lookup"><span data-stu-id="3beec-145">This includes fields of type `DataType.Collection(DataType.String)`.</span></span> <span data-ttu-id="3beec-146">Por ejemplo, si hello documento contiene un campo `tags` con valor `["budget"]` y ejecutar una combinación con el valor `["economy", "pool"]` para `tags`, Hola valor final de hello `tags` campo será `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="3beec-146">For example, if hello document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, hello final value of hello `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="3beec-147">No será `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="3beec-147">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `MergeOrUpload` |<span data-ttu-id="3beec-148">Esta acción se comporta como `Merge` si un documento con hello clave dada ya existe en el índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="3beec-148">This action behaves like `Merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="3beec-149">Si el documento de hello no existe, se comporta como `Upload` con un nuevo documento.</span><span class="sxs-lookup"><span data-stu-id="3beec-149">If hello document does not exist, it behaves like `Upload` with a new document.</span></span> |<span data-ttu-id="3beec-150">clave, además de cualquier otro campo que se va a toodefine</span><span class="sxs-lookup"><span data-stu-id="3beec-150">key, plus any other fields you wish toodefine</span></span> |- |
| `Delete` |<span data-ttu-id="3beec-151">Quita del documento especificado Hola Hola índice de.</span><span class="sxs-lookup"><span data-stu-id="3beec-151">Removes hello specified document from hello index.</span></span> |<span data-ttu-id="3beec-152">solo la clave</span><span class="sxs-lookup"><span data-stu-id="3beec-152">key only</span></span> |<span data-ttu-id="3beec-153">Los campos que especifique aparte de campo de clave de Hola se pasará por alto.</span><span class="sxs-lookup"><span data-stu-id="3beec-153">Any fields you specify other than hello key field will be ignored.</span></span> <span data-ttu-id="3beec-154">Si desea tooremove un campo individual de un documento, use `Merge` en su lugar y simplemente establezca explícitamente campo hello toonull.</span><span class="sxs-lookup"><span data-stu-id="3beec-154">If you want tooremove an individual field from a document, use `Merge` instead and simply set hello field explicitly toonull.</span></span> |

<span data-ttu-id="3beec-155">También puede especificar qué acción desea toouse con Hola varios métodos estáticos de hello `IndexBatch` y `IndexAction` clases, como se muestra en la siguiente sección de Hola.</span><span class="sxs-lookup"><span data-stu-id="3beec-155">You can specify what action you want toouse with hello various static methods of hello `IndexBatch` and `IndexAction` classes, as shown in hello next section.</span></span>

## <a name="construct-your-indexbatch"></a><span data-ttu-id="3beec-156">Construcción de IndexBatch</span><span class="sxs-lookup"><span data-stu-id="3beec-156">Construct your IndexBatch</span></span>
<span data-ttu-id="3beec-157">Ahora que sabe qué tooperform acciones en los documentos, está listo tooconstruct Hola `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="3beec-157">Now that you know which actions tooperform on your documents, you are ready tooconstruct hello `IndexBatch`.</span></span> <span data-ttu-id="3beec-158">Hola de ejemplo siguiente se muestra cómo toocreate un lote con algunas acciones diferentes.</span><span class="sxs-lookup"><span data-stu-id="3beec-158">hello example below shows how toocreate a batch with a few different actions.</span></span> <span data-ttu-id="3beec-159">Tenga en cuenta que este ejemplo usa una clase personalizada denominada `Hotel` que asigna tooa documento en el índice de "hoteles" Hola.</span><span class="sxs-lookup"><span data-stu-id="3beec-159">Note that our example uses a custom class called `Hotel` that maps tooa document in hello "hotels" index.</span></span>

```csharp
var actions =
    new IndexAction<Hotel>[]
    {
        IndexAction.Upload(
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
            }),
        IndexAction.Upload(
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
            }),
        IndexAction.MergeOrUpload(
            new Hotel()
            {
                HotelId = "3",
                BaseRate = 129.99,
                Description = "Close tootown hall and hello river"
            }),
        IndexAction.Delete(new Hotel() { HotelId = "6" })
    };

var batch = IndexBatch.New(actions);
```

<span data-ttu-id="3beec-160">En este caso, usamos `Upload`, `MergeOrUpload`, y `Delete` como nuestras acciones de búsqueda, tal y como especifica métodos de hello llamados en hello `IndexAction` clase.</span><span class="sxs-lookup"><span data-stu-id="3beec-160">In this case, we are using `Upload`, `MergeOrUpload`, and `Delete` as our search actions, as specified by hello methods called on hello `IndexAction` class.</span></span>

<span data-ttu-id="3beec-161">Se supone que este índice "hoteles" de ejemplo ya está relleno con varios documentos.</span><span class="sxs-lookup"><span data-stu-id="3beec-161">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="3beec-162">Tenga en cuenta cómo no se tenía toospecify todos los campos de documento posibles Hola al usar `MergeOrUpload` y cómo se puede especificar sólo clave de documento de hello (`HotelId`) cuando se usa `Delete`.</span><span class="sxs-lookup"><span data-stu-id="3beec-162">Note how we did not have toospecify all hello possible document fields when using `MergeOrUpload` and how we only specified hello document key (`HotelId`) when using `Delete`.</span></span>

<span data-ttu-id="3beec-163">Además, tenga en cuenta que solo pueden incluir documentos too1000 en una sola solicitud de indización.</span><span class="sxs-lookup"><span data-stu-id="3beec-163">Also, note that you can only include up too1000 documents in a single indexing request.</span></span>

> [!NOTE]
> <span data-ttu-id="3beec-164">En este ejemplo, estamos aplicando documentos de toodifferent acciones diferentes.</span><span class="sxs-lookup"><span data-stu-id="3beec-164">In this example, we are applying different actions toodifferent documents.</span></span> <span data-ttu-id="3beec-165">Si deseara tooperform Hola mismas acciones en todos los documentos en el lote de hello, en lugar de llamar `IndexBatch.New`, podría utilizar Hola otros métodos estáticos de `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="3beec-165">If you wanted tooperform hello same actions across all documents in hello batch, instead of calling `IndexBatch.New`, you could use hello other static methods of `IndexBatch`.</span></span> <span data-ttu-id="3beec-166">Por ejemplo, podría crear lotes mediante una llamada a `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` o `IndexBatch.Delete`.</span><span class="sxs-lookup"><span data-stu-id="3beec-166">For example, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete`.</span></span> <span data-ttu-id="3beec-167">Estos métodos toman una colección de documentos (objetos del tipo `Hotel` en este ejemplo), en lugar de objetos `IndexAction`.</span><span class="sxs-lookup"><span data-stu-id="3beec-167">These methods take a collection of documents (objects of type `Hotel` in this example) instead of `IndexAction` objects.</span></span>
> 
> 

## <a name="import-data-toohello-index"></a><span data-ttu-id="3beec-168">Índice de toohello de datos de importación</span><span class="sxs-lookup"><span data-stu-id="3beec-168">Import data toohello index</span></span>
<span data-ttu-id="3beec-169">Ahora que tiene un inicializado `IndexBatch` objeto, puede enviarlo toohello índice mediante una llamada a `Documents.Index` en su `SearchIndexClient` objeto.</span><span class="sxs-lookup"><span data-stu-id="3beec-169">Now that you have an initialized `IndexBatch` object, you can send it toohello index by calling `Documents.Index` on your `SearchIndexClient` object.</span></span> <span data-ttu-id="3beec-170">Hola siguiente ejemplo se muestra cómo toocall `Index`, así como algunos pasos adicionales que deberá tooperform:</span><span class="sxs-lookup"><span data-stu-id="3beec-170">hello following example shows how toocall `Index`, as well as some extra steps you will need tooperform:</span></span>

```csharp
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
```

<span data-ttu-id="3beec-171">Hola Nota `try` / `catch` que rodean Hola llamada toohello `Index` método.</span><span class="sxs-lookup"><span data-stu-id="3beec-171">Note hello `try`/`catch` surrounding hello call toohello `Index` method.</span></span> <span data-ttu-id="3beec-172">bloque catch de Hello controla un caso de error importante para la indización.</span><span class="sxs-lookup"><span data-stu-id="3beec-172">hello catch block handles an important error case for indexing.</span></span> <span data-ttu-id="3beec-173">Si se produce un error en el servicio de búsqueda de Azure tooindex algunos de hello documentos en el lote de hello, un `IndexBatchException` producida por `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="3beec-173">If your Azure Search service fails tooindex some of hello documents in hello batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="3beec-174">Esto puede suceder si indiza documentos mientras el servicio está sobrecargado.</span><span class="sxs-lookup"><span data-stu-id="3beec-174">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="3beec-175">**Recomendamos encarecidamente controlar este caso de forma explícita en el código.**</span><span class="sxs-lookup"><span data-stu-id="3beec-175">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="3beec-176">Puede retrasar y, a continuación, vuelva a intentar indización documentos Hola que generaron errores o puede iniciar sesión y continuar como ejemplo de Hola o puede hacer algo más según los requisitos de coherencia de datos de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="3beec-176">You can delay and then retry indexing hello documents that failed, or you can log and continue like hello sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

<span data-ttu-id="3beec-177">Por último, código de hello en el ejemplo de Hola anterior retrasos en dos segundos.</span><span class="sxs-lookup"><span data-stu-id="3beec-177">Finally, hello code in hello example above delays for two seconds.</span></span> <span data-ttu-id="3beec-178">Indización realiza de forma asincrónica en el servicio de búsqueda de Azure, por lo que necesita de aplicación de ejemplo de Hola toowait un tooensure de hora corta que están disponibles para la búsqueda de documentos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3beec-178">Indexing happens asynchronously in your Azure Search service, so hello sample application needs toowait a short time tooensure that hello documents are available for searching.</span></span> <span data-ttu-id="3beec-179">Retrasos así solo suelen ser necesarios en las pruebas, demostraciones y aplicaciones de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3beec-179">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

<a name="HotelClass"></a>

### <a name="how-hello-net-sdk-handles-documents"></a><span data-ttu-id="3beec-180">Cómo Hola SDK para .NET controla los documentos</span><span class="sxs-lookup"><span data-stu-id="3beec-180">How hello .NET SDK handles documents</span></span>
<span data-ttu-id="3beec-181">Quizás se pregunte cómo Hola SDK de .NET de búsqueda de Azure es las instancias de tooupload capaz de una clase definida por el usuario como `Hotel` toohello índice.</span><span class="sxs-lookup"><span data-stu-id="3beec-181">You may be wondering how hello Azure Search .NET SDK is able tooupload instances of a user-defined class like `Hotel` toohello index.</span></span> <span data-ttu-id="3beec-182">toohelp respondamos esa pregunta, echemos un vistazo a hello `Hotel` (clase), que se asigna el esquema de índice toohello definido en [crear un índice de búsqueda de Azure con .NET SDK Hola](search-create-index-dotnet.md#DefineIndex):</span><span class="sxs-lookup"><span data-stu-id="3beec-182">toohelp answer that question, let's look at hello `Hotel` class, which maps toohello index schema defined in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#DefineIndex):</span></span>

```csharp
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [Key]
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

    // ToString() method omitted for brevity...
}
```

<span data-ttu-id="3beec-183">Hola lo primero que toonotice es que cada propiedad pública de `Hotel` corresponde tooa campo en la definición del índice hello, pero con una diferencia fundamental: nombre de Hola de cada campo empieza por una letra minúscula ("mayúsculas y minúsculas camel"), al nombre de hello cada público propiedad de `Hotel` comienza con una letra mayúscula ("caso Pascal").</span><span class="sxs-lookup"><span data-stu-id="3beec-183">hello first thing toonotice is that each public property of `Hotel` corresponds tooa field in hello index definition, but with one crucial difference: hello name of each field starts with a lower-case letter ("camel case"), while hello name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="3beec-184">Se trata de un escenario común en las aplicaciones de .NET que realizar el enlace de datos donde esquema de destino de hello es control hello fuera del desarrollador de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="3beec-184">This is a common scenario in .NET applications that perform data-binding where hello target schema is outside hello control of hello application developer.</span></span> <span data-ttu-id="3beec-185">En lugar de tener .NET de hello tooviolate las directrices de nomenclatura mediante la realización de los nombres de propiedad y minúscula camel, puede indicar Hola SDK toomap Hola propiedad nombres toocamel caso automáticamente con hello `[SerializePropertyNamesAsCamelCase]` atributo.</span><span class="sxs-lookup"><span data-stu-id="3beec-185">Rather than having tooviolate hello .NET naming guidelines by making property names camel-case, you can tell hello SDK toomap hello property names toocamel-case automatically with hello `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="3beec-186">Hola SDK de .NET de búsqueda de Azure usa hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize de biblioteca y deserializar los tooand de objetos de modelos personalizados de JSON.</span><span class="sxs-lookup"><span data-stu-id="3beec-186">hello Azure Search .NET SDK uses hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library tooserialize and deserialize your custom model objects tooand from JSON.</span></span> <span data-ttu-id="3beec-187">Puede personalizar esta serialización si es necesario.</span><span class="sxs-lookup"><span data-stu-id="3beec-187">You can customize this serialization if needed.</span></span> <span data-ttu-id="3beec-188">Puede encontrar más información en [Serialización personalizada con JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="3beec-188">You can find more details in [Custom Serialization with JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span></span> <span data-ttu-id="3beec-189">Un ejemplo de esto es el uso de Hola de hello `[JsonProperty]` atributo hello `DescriptionFr` propiedad en el código de ejemplo de Hola anterior.</span><span class="sxs-lookup"><span data-stu-id="3beec-189">One example of this is hello use of hello `[JsonProperty]` attribute on hello `DescriptionFr` property in hello sample code above.</span></span>
> 
> 

<span data-ttu-id="3beec-190">segunda cosa importante Hola sobre hello `Hotel` clase son tipos de datos de hello propiedades públicas de Hola.</span><span class="sxs-lookup"><span data-stu-id="3beec-190">hello second important thing about hello `Hotel` class are hello data types of hello public properties.</span></span> <span data-ttu-id="3beec-191">tipos de .NET de Hola de estas propiedades asignan tootheir tipos de campo equivalente en la definición del índice Hola.</span><span class="sxs-lookup"><span data-stu-id="3beec-191">hello .NET types of these properties map tootheir equivalent field types in hello index definition.</span></span> <span data-ttu-id="3beec-192">Por ejemplo, hello `Category` propiedad de cadena asigna toohello `category` campo, que es de tipo `DataType.String`.</span><span class="sxs-lookup"><span data-stu-id="3beec-192">For example, hello `Category` string property maps toohello `category` field, which is of type `DataType.String`.</span></span> <span data-ttu-id="3beec-193">Se dan asignaciones de tipos similares entre `bool?` y `DataType.Boolean`, `DateTimeOffset?` y `DataType.DateTimeOffset`, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="3beec-193">There are similar type mappings between `bool?` and `DataType.Boolean`, `DateTimeOffset?` and `DataType.DateTimeOffset`, and so forth.</span></span> <span data-ttu-id="3beec-194">reglas específicas de Hello para la asignación de tipo hello están documentadas con hello `Documents.Get` método Hola [referencia de SDK de .NET de búsqueda de Azure](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="3beec-194">hello specific rules for hello type mapping are documented with hello `Documents.Get` method in hello [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span>

<span data-ttu-id="3beec-195">Esta capacidad toouse sus propias clases como documentos funciona en ambas direcciones; También puede recuperar los resultados de la búsqueda y tener Hola SDK automáticamente deserializar ellos tooa tipo de su elección, como se muestra en hello [siguiente artículo](search-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="3beec-195">This ability toouse your own classes as documents works in both directions; You can also retrieve search results and have hello SDK automatically deserialize them tooa type of your choice, as shown in hello [next article](search-query-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3beec-196">Hola SDK de .NET de búsqueda de Azure también admite documentos dinámicamente tipada utilizando hello `Document` (clase), que es una asignación de clave/valor de los valores de toofield de nombres de campo.</span><span class="sxs-lookup"><span data-stu-id="3beec-196">hello Azure Search .NET SDK also supports dynamically-typed documents using hello `Document` class, which is a key/value mapping of field names toofield values.</span></span> <span data-ttu-id="3beec-197">Esto es útil en escenarios donde no conoce el esquema de índice de hello en tiempo de diseño, o donde sería clases del modelo de toospecific toobind supone un inconveniente.</span><span class="sxs-lookup"><span data-stu-id="3beec-197">This is useful in scenarios where you don't know hello index schema at design-time, or where it would be inconvenient toobind toospecific model classes.</span></span> <span data-ttu-id="3beec-198">Todos los métodos de Hola Hola SDK que se encargan de documentos tienen sobrecargas que funcionan con hello `Document` clase, así como fuertemente tipados sobrecargas que toman un parámetro de tipo genérico.</span><span class="sxs-lookup"><span data-stu-id="3beec-198">All hello methods in hello SDK that deal with documents have overloads that work with hello `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="3beec-199">Solo Hola este último se utilizan en el código de ejemplo de Hola en este artículo.</span><span class="sxs-lookup"><span data-stu-id="3beec-199">Only hello latter are used in hello sample code in this article.</span></span>
> 
> 

<span data-ttu-id="3beec-200">**¿Por qué debería usar tipos de datos que aceptan valores null?**</span><span class="sxs-lookup"><span data-stu-id="3beec-200">**Why you should use nullable data types**</span></span>

<span data-ttu-id="3beec-201">Al diseñar su propio índice modelo clases toomap tooan búsqueda de Azure, se recomienda declarar propiedades de tipos de valor como `bool` y `int` toobe que aceptan valores null (por ejemplo, `bool?` en lugar de `bool`).</span><span class="sxs-lookup"><span data-stu-id="3beec-201">When designing your own model classes toomap tooan Azure Search index, we recommend declaring properties of value types such as `bool` and `int` toobe nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="3beec-202">Si utiliza una propiedad que no acepta valores NULL, tienen también**garantizar** ningún documentos en el índice que contienen un valor nulo para el campo correspondiente Hola.</span><span class="sxs-lookup"><span data-stu-id="3beec-202">If you use a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="3beec-203">Hola SDK ni Hola servicio Búsqueda de Azure le ayudará a tooenforce esto.</span><span class="sxs-lookup"><span data-stu-id="3beec-203">Neither hello SDK nor hello Azure Search service will help you tooenforce this.</span></span>

<span data-ttu-id="3beec-204">Esto no es simplemente un problema hipotético: Imagine un escenario donde agrega un nuevo índice existente de campo tooan que es de tipo `DataType.Int32`.</span><span class="sxs-lookup"><span data-stu-id="3beec-204">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `DataType.Int32`.</span></span> <span data-ttu-id="3beec-205">Después de actualizar la definición del índice hello, todos los documentos tendrá un valor null para ese campo nuevo (ya que todos los tipos admiten valores NULL en la búsqueda de Azure).</span><span class="sxs-lookup"><span data-stu-id="3beec-205">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="3beec-206">Si, a continuación, usa una clase de modelo con un acepta valores NULL `int` propiedad para ese campo, obtendrá un `JsonSerializationException` similar a éste al tratar de tooretrieve documentos:</span><span class="sxs-lookup"><span data-stu-id="3beec-206">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="3beec-207">Por este motivo, recomendamos utilizar tipos que aceptan valores NULL en las clases de modelo como procedimiento recomendado.</span><span class="sxs-lookup"><span data-stu-id="3beec-207">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3beec-208">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3beec-208">Next steps</span></span>
<span data-ttu-id="3beec-209">Después de rellenar el índice de búsqueda de Azure, estará listo toostart emitir toosearch de las consultas para los documentos.</span><span class="sxs-lookup"><span data-stu-id="3beec-209">After populating your Azure Search index, you will be ready toostart issuing queries toosearch for documents.</span></span> <span data-ttu-id="3beec-210">Para más información, vea [Consultas en Búsqueda de Azure](search-query-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="3beec-210">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>

