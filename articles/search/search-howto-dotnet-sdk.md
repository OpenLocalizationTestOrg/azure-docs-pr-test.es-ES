---
title: "aaaHow toouse búsqueda de Azure desde una aplicación .NET | Documentos de Microsoft"
description: "Cómo toouse Azure buscar desde una aplicación .NET"
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
ms.openlocfilehash: 8e13fbe5549547d65941b856ce5a90611261388f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-search-from-a-net-application"></a>Cómo toouse Azure buscar desde una aplicación .NET
Este artículo es un tutorial tooget, activos y en funcionamiento con hello [SDK de .NET de búsqueda de Azure](https://aka.ms/search-sdk). Puede usar Hola .NET SDK tooimplement una rica experiencia de búsqueda en la aplicación con búsqueda de Azure.

## <a name="whats-in-hello-azure-search-sdk"></a>¿Qué es Hola búsqueda de Azure SDK
Hello SDK está formado por una biblioteca de cliente, `Microsoft.Azure.Search`. Permite toomanage los índices, los orígenes de datos y los indizadores, así como cargar y administrar documentos y ejecutar las consultas, todo ello sin necesidad de toodeal con detalles de Hola de HTTP y JSON.

biblioteca de cliente de Hello define clases como `Index`, `Field`, y `Document`, así como las operaciones como `Indexes.Create` y `Documents.Search` en hello `SearchServiceClient` y `SearchIndexClient` clases. Estas clases se organizan en hello después de los espacios de nombres:

* [Microsoft.Azure.Search](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [Microsoft.Azure.Search.Models](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

versión actual de Hola de hello SDK de .NET de búsqueda de Azure ahora es disponible con carácter general. Si desea que tooprovide comentarios nos tooincorporate en la versión siguiente de hello, visite nuestro [página de comentarios](https://feedback.azure.com/forums/263029-azure-search/).

Hola .NET SDK es compatible con la versión `2016-09-01` de hello [API de REST de búsqueda de Azure](https://docs.microsoft.com/rest/api/searchservice/). Esta versión incluye ahora compatibilidad con analizadores personalizados y con el indexador de Azure Blob y Azure Table. Obtener una vista previa de características que están *no* parte de esta versión, como la posibilidad de indizar archivos CSV y JSON, que se encuentran en [vista previa](search-api-2015-02-28-preview.md) y están disponibles a través de hello anterior [versión 2.0-versión preliminar de hello SDK para .NET ](https://aka.ms/search-sdk-preview).

Este SDK no admite [operaciones de administración](https://docs.microsoft.com/rest/api/searchmanagement/) como la creación y el escalado de servicios de Search y las claves de API de administración. Si necesita toomanage los recursos de búsqueda desde una aplicación. NET, puede usar hello [.NET SDK de administración de búsqueda de Azure](https://aka.ms/search-mgmt-sdk).

## <a name="upgrading-toohello-latest-version-of-hello-sdk"></a>Actualización de versión más reciente de toohello de hello SDK
Si ya está usando una versión anterior de hello SDK de .NET de búsqueda de Azure y le gustaría tooupgrade toohello versión disponible con carácter general nueva, [este artículo](search-dotnet-sdk-migration.md) explica cómo.

## <a name="requirements-for-hello-sdk"></a>Requisitos para hello SDK
1. Visual Studio 2017.
2. Su propio servicio Búsqueda de Azure. Hola de orden toouse SDK, necesitará nombre hello del servicio y una o varias claves de API. [Crear un servicio en el portal de hello](search-create-service-portal.md) le ayudará a través de estos pasos.
3. Descargar SDK de .NET de búsqueda de Azure de hello [paquete NuGet](http://www.nuget.org/packages/Microsoft.Azure.Search) mediante el uso de "Administrar paquetes de NuGet" en Visual Studio. Busque el nombre del paquete de hello `Microsoft.Azure.Search` en NuGet.org.

Hola SDK de .NET de búsqueda de Azure es compatible con las aplicaciones dirigidas a .NET Framework 4.6 hello y .NET Core.

## <a name="core-scenarios"></a>Escenarios principales
Hay varias cosas que debe toodo en la aplicación de búsqueda. En este tutorial, hablaremos sobre estos escenarios básicos:

* Creación de un índice
* Rellenar índice Hola con documentos
* Búsqueda de documentos mediante filtros y búsqueda de texto completo

código de ejemplo de Hola que sigue muestra cada uno de ellos. Sentirse fragmentos de código de hello toouse disponible en su propia aplicación.

### <a name="overview"></a>Información general
Hola se le pueden explorar de aplicación de ejemplo crea un nuevo índice con el nombre "hoteles", se rellena con algunos documentos, a continuación, ejecuta algunas consultas de búsqueda. Este es el programa principal hello, que muestra Hola flujo general:

```csharp
// This sample shows how toodelete, create, upload documents and query an index
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

    Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> Puede encontrar el código fuente completo de Hola de aplicación de ejemplo de Hola utilizado en este tutorial en [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).
> 
>

Lo recorreremos paso a paso. Primero necesitamos toocreate un nuevo `SearchServiceClient`. Este objeto permite toomanage índices. En orden tooconstruct uno, debe tooprovide el nombre del servicio de búsqueda de Azure, así como una clave de API de administración. Puede escribir esta información en hello `appsettings.json` archivo de hello [aplicación de ejemplo](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).

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
> Si proporciona una clave incorrecta (por ejemplo, una clave de consulta donde se requiere una clave de administración), Hola `SearchServiceClient` producirá un `CloudException` con hello "Prohibido" del mensaje de error Hola primera vez llame a un método de operación en él, como `Indexes.Create`. Si esto ocurre tooyou, comprueba la clave de API.
> 
> 

Hello siguientes líneas llamar a métodos toocreate un índice con el nombre "hoteles" eliminar primero si ya existe. Describiremos estos métodos más adelante.

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

A continuación, es necesario toobe rellena el índice de Hola. toodo, necesitamos un `SearchIndexClient`. Hay dos tooobtain formas uno: mediante la creación de él, o mediante una llamada a `Indexes.GetClient` en hello `SearchServiceClient`. Utilizamos Hola este último para su comodidad.

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> En una aplicación de búsqueda típica, el llenado y la administración de índices se controlan mediante un componente independiente de las consultas de búsqueda. `Indexes.GetClient`es conveniente para rellenar un índice porque ahorra Hola problemas de proporcionar otro `SearchCredentials`. Esto hace pasar clave de administración de Hola que Hola de toocreate usado se `SearchServiceClient` toohello nueva `SearchIndexClient`. Sin embargo, en la parte de saludo de la aplicación ejecuta consultas, es mejor hello toocreate `SearchIndexClient` directamente para que pueda pasar de una clave de consulta en lugar de una clave de administración. Esto es coherente con el principio de Hola de privilegios mínimos y ayudará toomake la aplicación más segura. Puede encontrar más información acerca de las claves de administración y consulta [aquí](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).
> 
> 

Ahora que tenemos un `SearchIndexClient`, se puede rellenar índice Hola. Para ello utilizaremos otro método que tratamos más adelante.

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

Por último, se ejecutan algunas consultas de búsqueda y mostrar los resultados de Hola. Esta vez usamos otro `SearchIndexClient`:

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

Echaremos un vistazo al hello `RunQueries` método más adelante. Aquí es Hola Hola de toocreate de código nuevo `SearchIndexClient`:

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

Esta vez se utilice una clave de consulta debido a que no necesitamos índice toohello de acceso de escritura. Puede escribir esta información en hello `appsettings.json` archivo de hello [aplicación de ejemplo](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).

Si ejecuta esta aplicación con un nombre de servicio válido y las claves de API, el resultado de hello debería tener este aspecto:

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents toobe indexed...
    
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
    
    Complete.  Press any key tooend application...

se proporciona código fuente completo de Hola de aplicación hello final Hola de este artículo.

A continuación, tomaremos aproximación a cada uno de los métodos de hello llamados por `Main`.

### <a name="creating-an-index"></a>Creación de un índice
Después de crear un `SearchServiceClient`, novedad de hello `Main` does es index delete Hola "hoteles" Si ya existe. Que se realiza mediante Hola siguiente método:

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

Este método usa Hola dado `SearchServiceClient` toocheck si existe un índice de Hola y elimínelo.

> [!NOTE]
> código de ejemplo de Hola en este artículo utiliza métodos sincrónicos de Hola de hello SDK de .NET de búsqueda de Azure para simplificar el trabajo. Le recomendamos que use métodos asincrónicos de hello en su propio tookeep aplicaciones escalables y con capacidad de respuesta. Por ejemplo, podría utilizar el método anterior se Hola `ExistsAsync` y `DeleteAsync` en lugar de `Exists` y `Delete`.
> 
> 

A continuación, `Main` crea un nuevo índice "hotels" mediante una llamada a este método:

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

Este método crea un nuevo `Index` objeto con una lista de `Field` objetos que define el esquema de Hola de nuevo índice de Hola. Cada campo tiene un nombre, un tipo de datos y varios atributos que definen su comportamiento de búsqueda. Hola `FieldBuilder` clase utiliza reflexión toocreate una lista de `Field` objetos para el índice de hello examinando Hola propiedades públicas y los atributos de hello dado `Hotel` clase de modelo. Redirigirse a una aproximación a hello `Hotel` clase más adelante.

> [!NOTE]
> Siempre puede crear lista de Hola de `Field` objetos directamente en lugar de usar `FieldBuilder` si es necesario. Por ejemplo, puede que no desee toouse una clase de modelo o puede que necesite toouse una clase de modelo existente que no desea toomodify mediante la adición de atributos.
>
> 

Además toofields, también puede agregar perfiles de puntuación, proveedores de sugerencias o toohello de opciones de CORS índice (se omiten de ejemplo de Hola por razones de brevedad). Puede encontrar más información sobre objetos de índice de Hola y sus partes constituyentes en hello [referencia SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), así como en hello [referencia de API de REST de búsqueda de Azure](https://docs.microsoft.com/rest/api/searchservice/).

### <a name="populating-hello-index"></a>Rellenar índice Hola
paso siguiente de Hello en `Main` es toopopulate Hola recién creado índice. Esto se hace en hello siguiente método:

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
            Description = "Close tootown hall and hello river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

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
}
```

Este método tiene cuatro partes. Hola, primero crea una matriz de `Hotel` objetos que servirá como nuestro índice de toohello tooupload de datos de entrada. Estos datos están incluidos en el código por motivos de simplicidad. En su propia aplicación, los datos provendrán normalmente de un origen de datos externo, como una base de datos SQL.

Hola segunda parte se crea un `IndexBatch` que contienen documentos Hola. Se especifica que desea tooapply toohello lote Hola crearlo, en este caso mediante una llamada de operación de hello `IndexBatch.Upload`. Hello lote está cargado toohello búsqueda de Azure indexar por hello `Documents.Index` método.

> [!NOTE]
> En este ejemplo nos limitamos a cargar documentos. Si deseara toomerge cambios en los documentos existentes o eliminar documentos, puede crear lotes mediante una llamada a `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, o `IndexBatch.Delete` en su lugar. También puede mezclar operaciones diferentes en un único lote mediante una llamada a `IndexBatch.New`, que toma una colección de `IndexAction` objetos, cada uno de los cuales indica una operación determinada en un documento a tooperform de búsqueda de Azure. Puede crear cada uno de ellos `IndexAction` con su propia operación llamando al método correspondiente de hello como `IndexAction.Merge`, `IndexAction.Upload`, y así sucesivamente.
> 
> 

Hola tercera parte de este método es un bloque catch que controla un caso de error importante para la indización. Si se produce un error en el servicio de búsqueda de Azure tooindex algunos de hello documentos en el lote de hello, un `IndexBatchException` producida por `Documents.Index`. Esto puede suceder si indiza documentos mientras el servicio está sobrecargado. **Recomendamos encarecidamente controlar este caso de forma explícita en el código.** Puede retrasar y, a continuación, vuelva a intentar indización documentos Hola que generaron errores o puede iniciar sesión y continuar como ejemplo de Hola o puede hacer algo más según los requisitos de coherencia de datos de su aplicación.

> [!NOTE]
> Puede usar hello `FindFailedActionsToRetry` tooconstruct método un lote nuevo que contenga solo Hola acciones que dieron error en una llamada anterior demasiado`Index`. método Hello está documentado [aquí](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) y no hay una explicación de cómo usa tooproperly [en StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).
>
>

Por último, Hola `UploadDocuments` retrasos de método en dos segundos. Indización realiza de forma asincrónica en el servicio de búsqueda de Azure, por lo que necesita de aplicación de ejemplo de Hola toowait un tooensure de hora corta que están disponibles para la búsqueda de documentos de Hola. Retrasos así solo suelen ser necesarios en las pruebas, demostraciones y aplicaciones de ejemplo.

#### <a name="how-hello-net-sdk-handles-documents"></a>Cómo Hola SDK para .NET controla los documentos
Quizás se pregunte cómo Hola SDK de .NET de búsqueda de Azure es las instancias de tooupload capaz de una clase definida por el usuario como `Hotel` toohello índice. toohelp respondamos esa pregunta, echemos un vistazo a hello `Hotel` clase:

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// hello SerializePropertyNamesAsCamelCase attribute is defined in hello Azure Search .NET SDK.
// It ensures that Pascal-case property names in hello model class are mapped toocamel-case
// field names in hello index.
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

Hola lo primero que toonotice es que cada propiedad pública de `Hotel` corresponde tooa campo en la definición del índice hello, pero con una diferencia fundamental: nombre de Hola de cada campo empieza por una letra minúscula ("mayúsculas y minúsculas camel"), al nombre de hello cada público propiedad de `Hotel` comienza con una letra mayúscula ("caso Pascal"). Se trata de un escenario común en las aplicaciones de .NET que realizar el enlace de datos donde esquema de destino de hello es control hello fuera del desarrollador de la aplicación hello. En lugar de tener .NET de hello tooviolate las directrices de nomenclatura mediante la realización de los nombres de propiedad y minúscula camel, puede indicar Hola SDK toomap Hola propiedad nombres toocamel caso automáticamente con hello `[SerializePropertyNamesAsCamelCase]` atributo.

> [!NOTE]
> Hola SDK de .NET de búsqueda de Azure usa hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize de biblioteca y deserializar los tooand de objetos de modelos personalizados de JSON. Puede personalizar esta serialización si es necesario. Para obtener más información, consulte [Serialización personalizada con JSON.NET](#JsonDotNet).
> 
> 

Hello segundo toonotice lo son Hola atributos como `IsFilterable`, `IsSearchable`, `Key`, y `Analyzer` que decoran cada propiedad pública. Estos atributos asignan directamente toohello [atributos correspondientes del índice de búsqueda de Azure de hello](https://docs.microsoft.com/rest/api/searchservice/create-index#request). Hola `FieldBuilder` clase usa estas definiciones de campo de tooconstruct para índice Hola.

importante tercer Hola sobre hello `Hotel` clase son tipos de datos de hello propiedades públicas de Hola. tipos de .NET de Hola de estas propiedades asignan tootheir tipos de campo equivalente en la definición del índice Hola. Por ejemplo, hello `Category` propiedad de cadena asigna toohello `category` campo, que es de tipo `Edm.String`. Hay asignaciones de tipos similares entre `bool?` y `Edm.Boolean`, `DateTimeOffset?` y `Edm.DateTimeOffset`, reglas específicas de hello etc. para asignación de tipo hello están documentadas con hello `Documents.Get` método Hola [SDK de .NET de búsqueda de Azure referencia](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_). Hola `FieldBuilder` clase se encarga de esta asignación para usted, pero todavía puede ser útil toounderstand por si tuviera tootroubleshoot los problemas de serialización.

Esta capacidad toouse sus propias clases como documentos funciona en ambas direcciones; También puede recuperar los resultados de la búsqueda y tener Hola SDK automáticamente deserializar ellos tooa tipo de su elección, como se verá en la siguiente sección de Hola.

> [!NOTE]
> Hola SDK de .NET de búsqueda de Azure también admite documentos dinámicamente tipada utilizando hello `Document` (clase), que es una asignación de clave/valor de los valores de toofield de nombres de campo. Esto es útil en escenarios donde no conoce el esquema de índice de hello en tiempo de diseño, o donde sería clases del modelo de toospecific toobind supone un inconveniente. Todos los métodos de Hola Hola SDK que se encargan de documentos tienen sobrecargas que funcionan con hello `Document` clase, así como fuertemente tipados sobrecargas que toman un parámetro de tipo genérico. Solo Hola este último se utilizan en el código de ejemplo de Hola en este tutorial. Hola `Document` clase hereda de `Dictionary<string, object>`. Puede encontrar otros detalles [aquí](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).
> 
> 

**¿Por qué debería usar tipos de datos que aceptan valores null?**

Al diseñar su propio índice modelo clases toomap tooan búsqueda de Azure, se recomienda declarar propiedades de tipos de valor como `bool` y `int` toobe que aceptan valores null (por ejemplo, `bool?` en lugar de `bool`). Si utiliza una propiedad que no acepta valores NULL, tienen también**garantizar** ningún documentos en el índice que contienen un valor nulo para el campo correspondiente Hola. Hola SDK ni Hola servicio Búsqueda de Azure le ayudará a tooenforce esto.

Esto no es simplemente un problema hipotético: Imagine un escenario donde agrega un nuevo índice existente de campo tooan que es de tipo `Edm.Int32`. Después de actualizar la definición del índice hello, todos los documentos tendrá un valor null para ese campo nuevo (ya que todos los tipos admiten valores NULL en la búsqueda de Azure). Si, a continuación, usa una clase de modelo con un acepta valores NULL `int` propiedad para ese campo, obtendrá un `JsonSerializationException` similar a éste al tratar de tooretrieve documentos:

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

Por este motivo, recomendamos utilizar tipos que aceptan valores NULL en las clases de modelo como procedimiento recomendado.

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a>Serialización personalizada con JSON.NET
Hola SDK usa JSON.NET para serializar y deserializar documentos. Puede personalizar la serialización y deserialización si necesita definir su propio `JsonConverter` o `IContractResolver` (vea hello [JSON.NET documentación](http://www.newtonsoft.com/json/help/html/Introduction.htm) para obtener más detalles). Esto puede ser útil cuando desee tooadapt una clase de modelo existente de la aplicación para su uso con búsqueda de Azure y otros escenarios más avanzados. Por ejemplo, con la serialización personalizada, puede:

* Incluir o excluir determinadas propiedades de la clase de modelo para que se almacenen como campos del documento.
* Asignar entre los nombres de propiedad del código y los nombres de campo del índice.
* Crear atributos personalizados que pueden usarse para la asignación de campos de propiedades toodocument.

Puede encontrar ejemplos de implementación de serialización personalizada en pruebas unitarias de Hola para hello SDK de .NET de búsqueda de Azure en GitHub. [Esta carpeta](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models) es un buen punto de partida. Contiene clases que se utilizan las pruebas de serialización personalizada hello.

### <a name="searching-for-documents-in-hello-index"></a>Buscar documentos en el índice de Hola
Hola último paso en la aplicación de ejemplo de Hola es toosearch para algunos documentos del índice de Hola. Hola siguiendo el método para ello:

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
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
}
```

Cada vez que ejecuta una consulta, este método crea primero un nuevo objeto `SearchParameters`. Se trata de opciones adicionales de toospecify usado para consulta de hello, como la ordenación, filtrado, paginación y facetas. En este método, estamos estableciendo hello `Filter`, `Select`, `OrderBy`, y `Top` propiedad para consultas diferentes. Hola todos los `SearchParameters` las propiedades están documentadas [aquí](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).

Hola siguiente paso es tooactually Ejecutar consulta de búsqueda de Hola. Esto se realiza mediante hello `Documents.Search` método. Para cada consulta, pasamos toouse de texto de búsqueda de hello como una cadena (o `"*"` si no hay ningún texto de búsqueda), además de hello buscar parámetros que creó anteriormente. También especificamos `Hotel` como parámetro de tipo hello para `Documents.Search`, que indica a documentos de toodeserialize del SDK de hello en los resultados de búsqueda de Hola en objetos de tipo `Hotel`.

> [!NOTE]
> También puede encontrar más información acerca de la sintaxis de expresiones de consulta de búsqueda de Hola [aquí](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).
> 
> 

Finalmente, después de cada consulta este método recorre en iteración todas las coincidencias de hello en resultados de búsqueda de hello, imprimir cada consola de toohello de documento:

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

Echemos un vistazo más de cerca a cada una de las consultas de Hola a su vez. Ésta es Hola código tooexecute Hola primera consulta:

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

En este caso, estamos buscando hoteles que coinciden con la palabra Hola "budget", y queremos tooget volver solo Hola hotel nombres, tal y como especifica hello `Select` parámetro. Estos son los resultados de hello:

    Name: Roach Motel

A continuación, se desea hoteles de hello toofind con una tasa por la noche de menos de 150 $ y devuelven solo el identificador de hotel de Hola y descripción:

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

Esta consulta utiliza una OData `$filter` expresión, `baseRate lt 150`, toofilter documentos de hello en el índice de Hola. Puede encontrar más información sobre sintaxis de OData que admite búsqueda de Azure de hello [aquí](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).

Estos son los resultados de Hola de consulta de hello:

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river

A continuación, queremos toofind Hola superior dos hoteles que se hayan renovado más recientemente y muestran el nombre del hotel hello y última fecha de renovación. Este es el código de hello. 

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

En este caso, usamos nuevo Hola de OData sintaxis toospecify `OrderBy` parámetro como `lastRenovationDate desc`. También establecemos `Top` too2 tooensure sólo obtenemos documentos de dos primeras Hola. Como antes, establecemos `Select` toospecify los campos que se deben devolver.

Estos son los resultados de hello:

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

Por último, queremos toofind todos los hoteles que coinciden con la palabra Hola "motel":

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

Y estos son los resultados de hello, que incluyen todos los campos porque no especificamos hello `Select` propiedad:

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

Este paso completa el tutorial de hello, pero no se detenga aquí. **pasos siguientes** proporcionan recursos adicionales para obtener más información acerca de Búsqueda de Azure.

## <a name="next-steps"></a>Pasos siguientes
* Examinar las referencias de Hola para hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) y [API de REST](https://docs.microsoft.com/rest/api/searchservice/).
* Profundice en sus conocimientos por medio de [vídeos y otros ejemplos y tutoriales](search-video-demo-tutorial-list.md).
* Revisión [convenciones de nomenclatura](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) reglas de hello toolearn para asignar nombres a varios objetos.
* Consulte los [tipos de datos admitidos](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) en Búsqueda de Azure.
