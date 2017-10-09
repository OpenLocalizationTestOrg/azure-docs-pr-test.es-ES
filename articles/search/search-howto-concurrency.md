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
# <a name="how-toomanage-concurrency-in-azure-search"></a>¿Cómo toomanage simultaneidad en búsqueda de Azure

Al administrar recursos de búsqueda de Azure, como índices y orígenes de datos, es importante tooupdate recursos de forma segura, especialmente si se tiene acceso a recursos al mismo tiempo por diferentes componentes de la aplicación. Cuando dos clientes actualizan simultáneamente un recurso sin ninguna coordinación, es posible que se produzcan condiciones de carrera. tooprevent, ofertas de búsqueda de Azure un *modelo de simultaneidad optimista*. No hay ningún bloqueo en un recurso, En su lugar, hay un valor ETag para sobrescriben todos los recursos que identifica la versión de recursos de Hola para que se pueden crear las solicitudes que evitar accidental.

> [!Tip]
> El código conceptual de una [solución de C# de ejemplo](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) explica el funcionamiento del control de simultaneidad en Azure Search. código de Hello crea condiciones que invocación el control de simultaneidad. Hola de lectura [fragmento de código siguiente](#samplecode) es probablemente suficiente para la mayoría de los desarrolladores, pero si desea toorun, nombre de servicio de edición appSettings.JSON que se tooadd hello y una clave de api de administración. Dada una dirección URL del servicio de `http://myservice.search.windows.net`, el nombre del servicio de hello es `myservice`.

## <a name="how-it-works"></a>Cómo funciona

Optimista de simultaneidad se implementa a través del acceso condición comprueba en las llamadas de API escribir tooindexes, los indizadores, orígenes de datos y recursos de synonymMap. 

Todos los recursos tienen una [*etiqueta de entidad (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) que proporciona información sobre la versión del objeto. Comprobando Hola ETag en primer lugar, puede evitar las actualizaciones simultáneas en un flujo de trabajo típico (get, modificarlo localmente, actualice) asegurándose de coincidencias de ETag del recurso de hello su copia local. 

+ Hello REST API usa un [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) en el encabezado de solicitud de saludo.
+ Hola .NET SDK establece Hola ETag a través de un objeto accessCondition, establecer hello [If-Match | Encabezado If-Match-ninguno](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) en recursos de Hola. Todos los objetos heredados de [IResourceWithETag (SDK de .NET)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) tienen un objeto accessCondition.

Cada vez que actualice un recurso, la etiqueta ETag correspondiente cambiará de forma automática. Al implementar la administración de simultaneidad, lo único que está haciendo es sinónimo de poner una condición previa en la solicitud de actualización de Hola que requiere el recurso remoto hello toohave Hola ETag mismo como copia de Hola Hola del recurso de que ha modificado en el cliente de Hola. Si un proceso simultáneo ya ha cambiado recurso remoto hello, Hola ETag no coincidirán condición previa de Hola y se producirá un error de solicitud de hello HTTP 412. Si usas Hola .NET SDK, esto se manifiesta como un `CloudException` donde Hola `IsAccessConditionFailed()` método de extensión devuelve true.

> [!Note]
> Solo hay un mecanismo para la simultaneidad. Se usa siempre con independencia de la API que se use para las actualizaciones de recursos. 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a>Casos de uso y código de ejemplo

Hola siguiente código muestra accessCondition comprueba para las operaciones de actualización de clave:

+ Producirá un error en una actualización si ya no existe el recurso de Hola
+ Producirá un error en una actualización si cambia la versión de Hola de recursos

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a>Código de ejemplo del [programa DotNetETagsExplainer](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)

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

## <a name="design-pattern"></a>Modelo de diseño

Un modelo de diseño para implementar simultaneidad optimista debe incluir un bucle que se reintenta la comprobación de condición de acceso de hello, una prueba de la condición de acceso de hello y, opcionalmente, se recupera un recurso actualizado antes de intentar toore-Hola aplicarlos. 

Este fragmento de código muestra la suma de Hola de un índice de tooan synonymMap que ya existe. Este código está tomado hello [tutorial sinónimo (vista previa) de C# para la búsqueda de Azure](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk). 

fragmento de código de Hello obtiene índice hoteles"hello", comprueba la versión del objeto hello en una operación de actualización, produce una excepción si se produce un error en la condición de hello y, a continuación, reintentos Hola operación (arriba toothree horas), a partir de la recuperación de índice de Hola Hola de tooget de servidor más reciente Versión.

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


## <a name="next-steps"></a>Pasos siguientes

Hola de revisión [ejemplo sinónimos C#](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) para el contexto más cómo toosafely actualizar un índice existente.

Intente modificar cualquiera de los siguientes Hola muestrea tooinclude ETags o AccessCondition objetos.

+ [Ejemplo de API de REST en Github](https://github.com/Azure-Samples/search-rest-api-getting-started) 
+ [Ejemplo de SDK para .NET en Github](https://github.com/Azure-Samples/search-dotnet-getting-started). Esta solución incluye proyectos de "DotNetEtagsExplainer" hello que contiene código de hello presentado en este artículo.

## <a name="see-also"></a>Otras referencias

  [Common HTTP request and response headers](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)   (Encabezados de solicitud y respuesta HTTP comunes)  
  [HTTP status codes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) (Códigos de estado HTTP) [Index operations (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations) (Operaciones de índice (API de REST))