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
# <a name="synonym-preview-c-tutorial-for-azure-search"></a>Tutorial C# de sinónimos (versión preliminar) para Azure Search

Sinónimos expandir una consulta que coincida en términos que se considera como término de entrada toohello semánticamente equivalente. Por ejemplo, conviene documentos de toomatch "car" que contiene términos Hola "automóvil" o "vehicle".

En Azure Search, los sinónimos se definen en un *mapa de sinónimos* a través de *reglas de asignación* que permiten asociar términos equivalentes. Puede crear varias asignaciones de sinónimo, registrarlos como un índice de tooany disponible de recursos de todo el servicio y, a continuación, hacer referencia a qué un toouse nivel de campo de Hola. En el momento de la consulta, además toosearching un índice, búsqueda de Azure realiza una búsqueda en un mapa de sinónimo, si se especifica en los campos usados en consultas de Hola.

> [!NOTE]
> sinónimos de Hello característica está actualmente en vista previa y solo es compatible en Hola última versión preliminar de API y las versiones del SDK (api-version = 2016-09-01-versión preliminar, versión SDK 4.x-vista previa). En este momento no es compatible con Azure Portal. La versión preliminar de las API no se someten a las condiciones del Acuerdo de Nivel de Servicio y sus características pueden cambiar, por lo que no se recomienda su uso en aplicaciones de producción.

## <a name="prerequisites"></a>Requisitos previos

Requisitos del tutorial Hola siguientes:

* [Visual Studio](https://www.visualstudio.com/downloads/)
* [Un servicio de Azure Search](search-create-service-portal.md)
* [Versión preliminar de la biblioteca Microsoft.Azure.Search .NET](https://aka.ms/search-sdk-preview)
* [Cómo toouse Azure buscar desde una aplicación .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a>Información general

Las consultas de antes y después muestra el valor de Hola de sinónimos. En este tutorial, usamos una aplicación de ejemplo que ejecuta consultas y devuelve los resultados en un índice de ejemplo. aplicación de ejemplo de Hola crea un índice pequeño denominado "hoteles" rellenados con dos documentos. aplicación Hello ejecuta consultas de búsqueda con los términos y frases que no aparecen en el índice de hello, habilita la característica de sinónimos de hello, a continuación, problemas de Hola mismas búsquedas de nuevo. código de Hello siguiente muestra hello flujo general.

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
Hola toocreate de pasos y rellenar índice de ejemplo de Hola se explican en [cómo toouse Azure buscar desde una aplicación .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).

## <a name="before-queries"></a>Consultas "antes de"

En `RunQueriesWithNonExistentTermsInIndex`, se emiten consultas de búsqueda con "five star", "internet" y "economy AND hotel".
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
Ninguno de los documentos indizados dos Hola contienen términos de hello, por lo que obtenemos siguiente de hello resultado de hello primero `RunQueriesWithNonExistentTermsInIndex`.
~~~
Search hello entire index for hello phrase "five star":

no document matched

Search hello entire index for hello term 'internet':

no document matched

Search hello entire index for hello terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a>Habilitación de sinónimos

La habilitación de sinónimos es un proceso de dos pasos. Se primero se definen y cargar reglas del sinónimo y, a continuación, configurar campos toouse ellos. proceso de Hola se resume en `UploadSynonyms` y `EnableSynonymsInHotelsIndex`.

1. Agregar un servicio de búsqueda de tooyour de asignación de sinónimo. En `UploadSynonyms`, definimos cuatro reglas en el mapa de sinónimo 'desc synonymmap' y cargar el servicio toohello.
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
Un mapa de sinónimo debe cumplir el estándar de código abierto de toohello `solr` formato. formato de Hola se explica en [sinónimos en búsqueda de Azure](search-synonyms.md) en la sección de hello `Apache Solr synonym format`.

2. Configurar asignación de campos de búsqueda toouse Hola sinónimo en la definición del índice Hola. En `EnableSynonymsInHotelsIndex`, se permiten sinónimos en dos campos `category` y `tags` por establecer hello `synonymMaps` toohello nombre de propiedad Hola recién cargado mapa de sinónimo.
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
Al agregar un mapa de sinónimos, no son necesarias las recompilaciones de índices. Puede agregar un servicio de tooyour de asignación de sinónimo y, a continuación, modificar las definiciones de campo existentes en cualquier índice toouse Hola nuevo sinónimo mapa. Adición de Hola de nuevos atributos no influye en la disponibilidad del índice. Hola que esto mismo se aplica en deshabilitar sinónimos para un campo. Simplemente establezca hello `synonymMaps` lista vacía de tooan de propiedad.
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a>Consultas "después de"

Después de que se carga el mapa de sinónimo de Hola y el índice de hello es mapa de sinónimo de hello toouse actualizado, en segundo lugar Hola `RunQueriesWithNonExistentTermsInIndex` llamada genera siguiente hello:

~~~
Search hello entire index for hello phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
consulta primera Hola busca Hola documento de regla de hello `five star=>luxury`. segunda consulta de Hola expande Hola búsqueda mediante `internet,wifi` y hello en tercer lugar usa ambos `hotel, motel` y `economy,inexpensive=>budget` en Buscar documentos de Hola comparan.

Agregar sinónimos completamente cambia la experiencia de búsqueda de Hola. En este tutorial, consultas de hello original no pudo resultados significativos tooreturn incluso si los documentos de hello en nuestro índice están relevantes. Al habilitar sinónimos, podemos expandir un tooinclude índice términos de uso común, con ningún dato de toounderlying cambios en el índice de Hola.

## <a name="sample-application-source-code"></a>Código fuente de aplicación de ejemplo
Puede encontrar el código fuente completo de Hola de aplicación de ejemplo de Hola utilizado en este tutorial en [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).

## <a name="next-steps"></a>Pasos siguientes

* Revisión [cómo toouse sinónimos en búsqueda de Azure](search-synonyms.md)
* Revise la [documentación sobre el uso de sinónimos con la API de REST](https://aka.ms/rgm6rq)
* Examinar las referencias de Hola para hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) y [API de REST](https://docs.microsoft.com/rest/api/searchservice/).
