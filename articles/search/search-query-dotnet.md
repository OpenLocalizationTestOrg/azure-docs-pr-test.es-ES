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
# <a name="query-your-azure-search-index-using-hello-net-sdk"></a>Consultar el índice de búsqueda de Azure con hello SDK para .NET
> [!div class="op_single_selector"]
> * [Información general](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

En este artículo le mostrará cómo tooquery un índice utilizando Hola [SDK de .NET de búsqueda de Azure](https://aka.ms/search-sdk).

Antes de comenzar este tutorial, debe haber [creado ya un índice de Azure Search](search-what-is-an-index.md) y [haberlo rellenado con datos](search-what-is-data-import.md).

> [!NOTE]
> Todo el código de ejemplo de este artículo está escrito en C#. Puede encontrar el código fuente completo hello [en GitHub](http://aka.ms/search-dotnet-howto). También puede leer sobre hello [SDK de .NET de búsqueda de Azure](search-howto-dotnet-sdk.md) para un tutorial más detallado del código de ejemplo de Hola.

## <a name="identify-your-azure-search-services-query-api-key"></a>Identificación de la clave de API de consulta del servicio de Búsqueda de Azure
Ahora que ha creado un índice de búsqueda de Azure, son consultas tooissue casi listo con hello .NET SDK. En primer lugar, necesitará tooobtain uno Hola consulta claves de api que se generó para aprovisionar el servicio de búsqueda de Hola. Hola .NET SDK enviará esta clave de api en cada servicio de tooyour de solicitud. Tener una clave válida establece la confianza, por cada solicitud, entre Hola aplicación enviando Hola solicitud y el servicio de Hola que los controle.

1. toofind puede iniciar sesión en toohello de claves de api de su servicio [portal de Azure](https://portal.azure.com/)
2. Vaya hoja del servicio de búsqueda de Azure tooyour
3. Haga clic en hello icono "Claves"

El servicio tendrá *claves de administración* y *claves de consulta*.

* El principal y secundaria *claves de administración* conceder derechos completos tooall operaciones, incluido el servicio de hello capacidad toomanage hello, crear y eliminar índices, los indizadores y orígenes de datos. Existen dos claves para que pueda continuar la clave secundaria de hello toouse si decide tooregenerate Hola primary key y viceversa.
* Su *claves de consulta* conceder acceso de solo lectura tooindexes y documentos, y son aplicaciones tooclient normalmente distribuida que emiten solicitudes de búsqueda.

Para fines de Hola de consultar un índice, puede usar una de las claves de consulta. Las claves de administración también pueden usarse para las consultas, pero debe usar una clave de consulta en el código de aplicación de manera esto mejor hello [principio de privilegios mínimos](https://en.wikipedia.org/wiki/Principle_of_least_privilege).

## <a name="create-an-instance-of-hello-searchindexclient-class"></a>Cree una instancia de hello SearchIndexClient (clase)
consultas de tooissue con hello SDK de .NET de búsqueda de Azure, deberá toocreate una instancia de Hola `SearchIndexClient` clase. Esta clase tiene varios constructores. Hola uno desea que toma el nombre del servicio de búsqueda, el nombre del índice y un `SearchCredentials` objeto como parámetros. `SearchCredentials` incluye su clave de API.

código de Hello siguiente crea un nuevo `SearchIndexClient` para índice de "hoteles" Hola (creado en [crear un índice de búsqueda de Azure usando Hola .NET SDK](search-create-index-dotnet.md)) con valores para el nombre de servicio de búsqueda de Hola y clave de api que se almacenan en la configuración de la aplicación hello archivo (`appsettings.json` en caso de hello de hello [aplicación de ejemplo](http://aka.ms/search-dotnet-howto)):

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

`SearchIndexClient` tiene una propiedad `Documents`. Esta propiedad proporciona que todos Hola métodos que necesita tooquery índices de búsqueda de Azure.

## <a name="query-your-index"></a>Consulta del índice
Buscar con hello SDK para .NET es tan sencillo como Hola llamada `Documents.Search` método en su `SearchIndexClient`. Este método toma unos parámetros, incluido el texto de búsqueda de hello, junto con un `SearchParameters` objeto que puede ser usado toofurther refine Hola consulta.

#### <a name="types-of-queries"></a>Tipos de consultas
main Hola dos [tipos de consulta](search-query-overview.md#types-of-queries) va a utilizar son `search` y `filter`. Una consulta `search` realiza búsquedas de uno o más términos en todos los campos *habilitados para búsqueda* del índice. Una consulta `filter` evalúa una expresión booleana en todos los campos *filtrables* de un índice.

Búsquedas y filtros se realizan con hello `Documents.Search` método. Puede pasarse a una consulta de búsqueda de hello `searchText` parámetro, mientras que puede pasarse a una expresión de filtro de hello `Filter` propiedad de hello `SearchParameters` clase. toofilter sin buscar, sólo tiene que pasar `"*"` para hello `searchText` parámetro. toosearch sin filtrar, deje hello `Filter` propiedad no se establece, o no pase un `SearchParameters` en absoluto de la instancia.

#### <a name="example-queries"></a>Consultas de ejemplo
Hola siguiente código de ejemplo muestra varias maneras diferentes tooquery Hola "hoteles" índice definido en [crear un índice de búsqueda de Azure con .NET SDK hello](search-create-index-dotnet.md#DefineIndex). Tenga en cuenta que documentos Hola devueltos con los resultados de la búsqueda de hello son instancias de hello `Hotel` (clase), que se ha definido en [Hola de importación de datos en búsqueda de Azure con .NET SDK](search-import-data-dotnet.md#HotelClass). código de ejemplo de Hola hace uso de un `WriteDocuments` consola de toohello de resultados de búsqueda de método toooutput Hola. Este método se describe en la sección siguiente Hola.

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

## <a name="handle-search-results"></a>Control de los resultados de la búsqueda
Hola `Documents.Search` método devuelve un `DocumentSearchResult` objeto que contiene los resultados de Hola de consulta de Hola. ejemplo de Hola en la sección anterior de hello usa un método llamado `WriteDocuments` consola toohello de toooutput Hola búsqueda resultados:

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

Aquí está lo que parecen resultados hello como para las consultas de hello en la sección anterior de hello, suponiendo un índice de hoteles"Hola" se rellena con datos de ejemplo de Hola en [Hola de importación de datos en búsqueda de Azure con .NET SDK](search-import-data-dotnet.md):

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

código de ejemplo de Hola anterior usa resultados de la búsqueda de hello consola toooutput. Del mismo modo, necesitará toodisplay resultados de la búsqueda en su propia aplicación. Vea [en este ejemplo en GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) para obtener un ejemplo de cómo toorender búsqueda da como resultado una aplicación web basada en ASP.NET MVC.

