---
title: "aaaHow toomanage simultánea escribe tooresources en búsqueda de Azure"
description: "Utilice conflictos de simultaneidad optimista tooavoid aire intermedio en índices de búsqueda de actualizaciones o eliminaciones tooAzure, los indizadores, orígenes de datos."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 
ms.service: search
ms.devlang: 
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/21/2017
ms.author: heidist
ms.openlocfilehash: c061d2b5c4d2dbd0fd5633405b01ab2912fbc754
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-concurrency-in-azure-search"></a><span data-ttu-id="34893-103">¿Cómo toomanage simultaneidad en búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="34893-103">How toomanage concurrency in Azure Search</span></span>

<span data-ttu-id="34893-104">Al administrar recursos de búsqueda de Azure, como índices y orígenes de datos, es importante tooupdate recursos de forma segura, especialmente si se tiene acceso a recursos al mismo tiempo por diferentes componentes de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="34893-104">When managing Azure Search resources such as indexes and data sources, it's important tooupdate resources safely, especially if resources are accessed concurrently by different components of your application.</span></span> <span data-ttu-id="34893-105">Cuando dos clientes actualizan simultáneamente un recurso sin ninguna coordinación, es posible que se produzcan condiciones de carrera.</span><span class="sxs-lookup"><span data-stu-id="34893-105">When two clients concurrently update a resource without coordination, race conditions are possible.</span></span> <span data-ttu-id="34893-106">tooprevent, ofertas de búsqueda de Azure un *modelo de simultaneidad optimista*.</span><span class="sxs-lookup"><span data-stu-id="34893-106">tooprevent this, Azure Search offers an *optimistic concurrency model*.</span></span> <span data-ttu-id="34893-107">No hay ningún bloqueo en un recurso,</span><span class="sxs-lookup"><span data-stu-id="34893-107">There are no locks on a resource.</span></span> <span data-ttu-id="34893-108">En su lugar, hay un valor ETag para sobrescriben todos los recursos que identifica la versión de recursos de Hola para que se pueden crear las solicitudes que evitar accidental.</span><span class="sxs-lookup"><span data-stu-id="34893-108">Instead, there is an ETag for every resource that identifies hello resource version so that you can craft requests that avoid accidental overwrites.</span></span>

> [!Tip]
> <span data-ttu-id="34893-109">El código conceptual de una [solución de C# de ejemplo](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) explica el funcionamiento del control de simultaneidad en Azure Search.</span><span class="sxs-lookup"><span data-stu-id="34893-109">Conceptual code in a [sample C# solution](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) explains how concurrency control works in Azure Search.</span></span> <span data-ttu-id="34893-110">código de Hello crea condiciones que invocación el control de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="34893-110">hello code creates conditions that invoke concurrency control.</span></span> <span data-ttu-id="34893-111">Hola de lectura [fragmento de código siguiente](#samplecode) es probablemente suficiente para la mayoría de los desarrolladores, pero si desea toorun, nombre de servicio de edición appSettings.JSON que se tooadd hello y una clave de api de administración.</span><span class="sxs-lookup"><span data-stu-id="34893-111">Reading hello [code fragment below](#samplecode) is probably sufficient for most developers, but if you want toorun it, edit appsettings.json tooadd hello service name and an admin api-key.</span></span> <span data-ttu-id="34893-112">Dada una dirección URL del servicio de `http://myservice.search.windows.net`, el nombre del servicio de hello es `myservice`.</span><span class="sxs-lookup"><span data-stu-id="34893-112">Given a service URL of `http://myservice.search.windows.net`, hello service name is `myservice`.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="34893-113">Cómo funciona</span><span class="sxs-lookup"><span data-stu-id="34893-113">How it works</span></span>

<span data-ttu-id="34893-114">Optimista de simultaneidad se implementa a través del acceso condición comprueba en las llamadas de API escribir tooindexes, los indizadores, orígenes de datos y recursos de synonymMap.</span><span class="sxs-lookup"><span data-stu-id="34893-114">Optimistic concurrency is implemented through access condition checks in API calls writing tooindexes, indexers, datasources, and synonymMap resources.</span></span> 

<span data-ttu-id="34893-115">Todos los recursos tienen una [*etiqueta de entidad (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) que proporciona información sobre la versión del objeto.</span><span class="sxs-lookup"><span data-stu-id="34893-115">All resources have an [*entity tag (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) that provides object version information.</span></span> <span data-ttu-id="34893-116">Comprobando Hola ETag en primer lugar, puede evitar las actualizaciones simultáneas en un flujo de trabajo típico (get, modificarlo localmente, actualice) asegurándose de coincidencias de ETag del recurso de hello su copia local.</span><span class="sxs-lookup"><span data-stu-id="34893-116">By checking hello ETag first, you can avoid concurrent updates in a typical workflow (get, modify locally, update) by ensuring hello resource's ETag matches your local copy.</span></span> 

+ <span data-ttu-id="34893-117">Hello REST API usa un [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) en el encabezado de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="34893-117">hello REST API uses an [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on hello request header.</span></span>
+ <span data-ttu-id="34893-118">Hola .NET SDK establece Hola ETag a través de un objeto accessCondition, establecer hello [If-Match | Encabezado If-Match-ninguno](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) en recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="34893-118">hello .NET SDK sets hello ETag through an accessCondition object, setting hello [If-Match | If-Match-None header](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on hello resource.</span></span> <span data-ttu-id="34893-119">Todos los objetos heredados de [IResourceWithETag (SDK de .NET)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) tienen un objeto accessCondition.</span><span class="sxs-lookup"><span data-stu-id="34893-119">Any object inheriting from [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) has an accessCondition object.</span></span>

<span data-ttu-id="34893-120">Cada vez que actualice un recurso, la etiqueta ETag correspondiente cambiará de forma automática.</span><span class="sxs-lookup"><span data-stu-id="34893-120">Every time you update a resource, its ETag changes automatically.</span></span> <span data-ttu-id="34893-121">Al implementar la administración de simultaneidad, lo único que está haciendo es sinónimo de poner una condición previa en la solicitud de actualización de Hola que requiere el recurso remoto hello toohave Hola ETag mismo como copia de Hola Hola del recurso de que ha modificado en el cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="34893-121">When you implement concurrency management, all you're doing is putting a precondition on hello update request that requires hello remote resource toohave hello same ETag as hello copy of hello resource that you modified on hello client.</span></span> <span data-ttu-id="34893-122">Si un proceso simultáneo ya ha cambiado recurso remoto hello, Hola ETag no coincidirán condición previa de Hola y se producirá un error de solicitud de hello HTTP 412.</span><span class="sxs-lookup"><span data-stu-id="34893-122">If a concurrent process has changed hello remote resource already, hello ETag will not match hello precondition and hello request will fail with HTTP 412.</span></span> <span data-ttu-id="34893-123">Si usas Hola .NET SDK, esto se manifiesta como un `CloudException` donde Hola `IsAccessConditionFailed()` método de extensión devuelve true.</span><span class="sxs-lookup"><span data-stu-id="34893-123">If you're using hello .NET SDK, this manifests as a `CloudException` where hello `IsAccessConditionFailed()` extension method returns true.</span></span>

> [!Note]
> <span data-ttu-id="34893-124">Solo hay un mecanismo para la simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="34893-124">There is only one mechanism for concurrency.</span></span> <span data-ttu-id="34893-125">Se usa siempre con independencia de la API que se use para las actualizaciones de recursos.</span><span class="sxs-lookup"><span data-stu-id="34893-125">It's always used regardless of which API is used for resource updates.</span></span> 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a><span data-ttu-id="34893-126">Casos de uso y código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="34893-126">Use cases and sample code</span></span>

<span data-ttu-id="34893-127">Hola siguiente código muestra accessCondition comprueba para las operaciones de actualización de clave:</span><span class="sxs-lookup"><span data-stu-id="34893-127">hello following code demonstrates accessCondition checks for key update operations:</span></span>

+ <span data-ttu-id="34893-128">Producirá un error en una actualización si ya no existe el recurso de Hola</span><span class="sxs-lookup"><span data-stu-id="34893-128">Fail an update if hello resource no longer exists</span></span>
+ <span data-ttu-id="34893-129">Producirá un error en una actualización si cambia la versión de Hola de recursos</span><span class="sxs-lookup"><span data-stu-id="34893-129">Fail an update if hello resource version changes</span></span>

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a><span data-ttu-id="34893-130">Código de ejemplo del [programa DotNetETagsExplainer](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span><span class="sxs-lookup"><span data-stu-id="34893-130">Sample code from [DotNetETagsExplainer program](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span></span>

```
    class Program
    {
        // This sample shows how ETags work by performing conditional updates and deletes
        // on an Azure Search index.
        static void Main(string[] args)
        {
            IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
            IConfigurationRoot configuration = builder.Build();

            SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

            Console.WriteLine("Deleting index...\n");
            DeleteTestIndexIfExists(serviceClient);

            // Every top-level resource in Azure Search has an associated ETag that keeps track of which version
            // of hello resource you're working on. When you first create a resource such as an index, its ETag is
            // empty.
            Index index = DefineTestIndex();
            Console.WriteLine(
                $"Test index hasn't been created yet, so its ETag should be blank. ETag: '{index.ETag}'");

            // Once hello resource exists in Azure Search, its ETag will be populated. Make sure toouse hello object
            // returned by hello SearchServiceClient! Otherwise, you will still have hello old object with the
            // blank ETag.
            Console.WriteLine("Creating index...\n");
            index = serviceClient.Indexes.Create(index);
            
            Console.WriteLine($"Test index created; Its ETag should be populated. ETag: '{index.ETag}'");

            // ETags let you do some useful things you couldn't do otherwise. For example, by using an If-Match
            // condition, we can update an index using CreateOrUpdate and be guaranteed that hello update will only
            // succeed if hello index already exists.
            index.Fields.Add(new Field("name", AnalyzerName.EnMicrosoft));
            index =
                serviceClient.Indexes.CreateOrUpdate(
                    index,
                    accessCondition: AccessCondition.GenerateIfExistsCondition());

            Console.WriteLine(
                $"Test index updated; Its ETag should have changed since it was created. ETag: '{index.ETag}'");

            // More importantly, ETags protect you from concurrent updates toohello same resource. If another
            // client tries tooupdate hello resource, it will fail as long as all clients are using hello right
            // access conditions.
            Index indexForClient1 = index;
            Index indexForClient2 = serviceClient.Indexes.Get("test");

            Console.WriteLine("Simulating concurrent update. toostart, both clients see hello same ETag.");
            Console.WriteLine($"Client 1 ETag: '{indexForClient1.ETag}' Client 2 ETag: '{indexForClient2.ETag}'");

            // Client 1 successfully updates hello index.
            indexForClient1.Fields.Add(new Field("a", DataType.Int32));
            indexForClient1 =
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient1,
                    accessCondition: AccessCondition.IfNotChanged(indexForClient1));

            Console.WriteLine($"Test index updated by client 1; ETag: '{indexForClient1.ETag}'");

            // Client 2 tries tooupdate hello index, but fails, thanks toohello ETag check.
            try
            {
                indexForClient2.Fields.Add(new Field("b", DataType.Boolean));
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient2, 
                    accessCondition: AccessCondition.IfNotChanged(indexForClient2));

                Console.WriteLine("Whoops; This shouldn't happen");
                Environment.Exit(1);
            }
            catch (CloudException e) when (e.IsAccessConditionFailed())
            {
                Console.WriteLine("Client 2 failed tooupdate hello index, as expected.");
            }

            // You can also use access conditions with Delete operations. For example, you can implement an
            // atomic version of hello DeleteTestIndexIfExists method from this sample like this:
            Console.WriteLine("Deleting index...\n");
            serviceClient.Indexes.Delete("test", accessCondition: AccessCondition.GenerateIfExistsCondition());

            // This is slightly better than using hello Exists method since it makes only one round trip to
            // Azure Search instead of potentially two. It also avoids an extra Delete request in cases where
            // hello resource is deleted concurrently, but this doesn't matter much since resource deletion in
            // Azure Search is idempotent.

            // And we're done! Bye!
            Console.WriteLine("Complete.  Press any key tooend application...\n");
            Console.ReadKey();
        }

        private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
        {
            string searchServiceName = configuration["SearchServiceName"];
            string adminApiKey = configuration["SearchServiceAdminApiKey"];

            SearchServiceClient serviceClient =
                new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
            return serviceClient;
        }

        private static void DeleteTestIndexIfExists(SearchServiceClient serviceClient)
        {
            if (serviceClient.Indexes.Exists("test"))
            {
                serviceClient.Indexes.Delete("test");
            }
        }

        private static Index DefineTestIndex() =>
            new Index()
            {
                Name = "test",
                Fields = new[] { new Field("id", DataType.String) { IsKey = true } }
            };
    }
}
```

## <a name="design-pattern"></a><span data-ttu-id="34893-131">Modelo de diseño</span><span class="sxs-lookup"><span data-stu-id="34893-131">Design pattern</span></span>

<span data-ttu-id="34893-132">Un modelo de diseño para implementar simultaneidad optimista debe incluir un bucle que se reintenta la comprobación de condición de acceso de hello, una prueba de la condición de acceso de hello y, opcionalmente, se recupera un recurso actualizado antes de intentar toore-Hola aplicarlos.</span><span class="sxs-lookup"><span data-stu-id="34893-132">A design pattern for implementing optimistic concurrency should include a loop that retries hello access condition check, a test for hello access condition, and optionally retrieves an updated resource before attempting toore-apply hello changes.</span></span> 

<span data-ttu-id="34893-133">Este fragmento de código muestra la suma de Hola de un índice de tooan synonymMap que ya existe.</span><span class="sxs-lookup"><span data-stu-id="34893-133">This code snippet illustrates hello addition of a synonymMap tooan index that already exists.</span></span> <span data-ttu-id="34893-134">Este código está tomado hello [tutorial sinónimo (vista previa) de C# para la búsqueda de Azure](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span><span class="sxs-lookup"><span data-stu-id="34893-134">This code is from hello [Synonym (preview) C# tutorial for Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span></span> 

<span data-ttu-id="34893-135">fragmento de código de Hello obtiene índice hoteles"hello", comprueba la versión del objeto hello en una operación de actualización, produce una excepción si se produce un error en la condición de hello y, a continuación, reintentos Hola operación (arriba toothree horas), a partir de la recuperación de índice de Hola Hola de tooget de servidor más reciente Versión.</span><span class="sxs-lookup"><span data-stu-id="34893-135">hello snippet gets hello "hotels" index, checks hello object version on an update operation, throws an exception if hello condition fails, and then retries hello operation (up toothree times), starting with index retrieval from hello server tooget hello latest version.</span></span>

        private static void EnableSynonymsInHotelsIndexSafely(SearchServiceClient serviceClient)
        {
            int MaxNumTries = 3;

            for (int i = 0; i < MaxNumTries; ++i)
            {
                try
                {
                    Index index = serviceClient.Indexes.Get("hotels");
                    index = AddSynonymMapsToFields(index);

                    // hello IfNotChanged condition ensures that hello index is updated only if hello ETags match.
                    serviceClient.Indexes.CreateOrUpdate(index, accessCondition: AccessCondition.IfNotChanged(index));

                    Console.WriteLine("Updated hello index successfully.\n");
                    break;
                }
                catch (CloudException e) when (e.IsAccessConditionFailed())
                {
                    Console.WriteLine($"Index update failed : {e.Message}. Attempt({i}/{MaxNumTries}).\n");
                }
            }
        }
        
        private static Index AddSynonymMapsToFields(Index index)
        {
            index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
            index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };
            return index;
        }


## <a name="next-steps"></a><span data-ttu-id="34893-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="34893-136">Next steps</span></span>

<span data-ttu-id="34893-137">Hola de revisión [ejemplo sinónimos C#](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) para el contexto más cómo toosafely actualizar un índice existente.</span><span class="sxs-lookup"><span data-stu-id="34893-137">Review hello [synonyms C# sample](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) for more context on how toosafely update an existing index.</span></span>

<span data-ttu-id="34893-138">Intente modificar cualquiera de los siguientes Hola muestrea tooinclude ETags o AccessCondition objetos.</span><span class="sxs-lookup"><span data-stu-id="34893-138">Try modifying either of hello following samples tooinclude ETags or AccessCondition objects.</span></span>

+ [<span data-ttu-id="34893-139">Ejemplo de API de REST en Github</span><span class="sxs-lookup"><span data-stu-id="34893-139">REST API sample on Github</span></span>](https://github.com/Azure-Samples/search-rest-api-getting-started) 
+ <span data-ttu-id="34893-140">[Ejemplo de SDK para .NET en Github](https://github.com/Azure-Samples/search-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="34893-140">[.NET SDK sample on Github](https://github.com/Azure-Samples/search-dotnet-getting-started).</span></span> <span data-ttu-id="34893-141">Esta solución incluye proyectos de "DotNetEtagsExplainer" hello que contiene código de hello presentado en este artículo.</span><span class="sxs-lookup"><span data-stu-id="34893-141">This solution includes hello "DotNetEtagsExplainer" project containing hello code presented in this article.</span></span>

## <a name="see-also"></a><span data-ttu-id="34893-142">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="34893-142">See also</span></span>

  <span data-ttu-id="34893-143">[Common HTTP request and response headers](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)   (Encabezados de solicitud y respuesta HTTP comunes)</span><span class="sxs-lookup"><span data-stu-id="34893-143">[Common HTTP request and response headers](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span></span>  
  <span data-ttu-id="34893-144">[HTTP status codes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) (Códigos de estado HTTP) [Index operations (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations) (Operaciones de índice (API de REST))</span><span class="sxs-lookup"><span data-stu-id="34893-144">[HTTP status codes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [Index operations (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span></span>