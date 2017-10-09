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
# <a name="upload-data-tooazure-search-using-hello-net-sdk"></a>Carga datos tooAzure búsqueda mediante Hola SDK para .NET
> [!div class="op_single_selector"]
> * [Información general](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
> 
> 

En este artículo le mostrará cómo hello toouse [SDK de .NET de búsqueda de Azure](https://aka.ms/search-sdk) tooimport datos en un índice de búsqueda de Azure.

Antes de comenzar este tutorial, debe haber [creado ya un índice de Búsqueda de Azure](search-what-is-an-index.md). En este artículo también se da por supuesto que ya ha creado un `SearchServiceClient` de objeto, como se muestra en [crear un índice de búsqueda de Azure con .NET SDK hello](search-create-index-dotnet.md#CreateSearchServiceClient).

> [!NOTE]
> Todo el código de ejemplo de este artículo está escrito en C#. Puede encontrar el código fuente completo hello [en GitHub](http://aka.ms/search-dotnet-howto). También puede leer sobre hello [SDK de .NET de búsqueda de Azure](search-howto-dotnet-sdk.md) para un tutorial más detallado del código de ejemplo de Hola.

En los documentos de toopush de orden en el índice mediante Hola .NET SDK, necesitará:

1. Crear un `SearchIndexClient` índice de búsqueda de objeto tooconnect tooyour.
2. Crear un `IndexBatch` que contiene Hola documentos toobe agregado, modificado o eliminado.
3. Llamar a hello `Documents.Index` método de su `SearchIndexClient` toosend hello `IndexBatch` tooyour índice de búsqueda.

## <a name="create-an-instance-of-hello-searchindexclient-class"></a>Cree una instancia de hello SearchIndexClient (clase)
tooimport datos en el índice utilizando Hola SDK de .NET de búsqueda de Azure, necesitará toocreate una instancia de hello `SearchIndexClient` clase. Puede construir esta instancia usted mismo, pero es más fácil si ya tiene un `SearchServiceClient` instancia toocall su `Indexes.GetClient` método. Por ejemplo, mostramos cómo que obtendría un `SearchIndexClient` para índice de hello denominado "hoteles" desde un `SearchServiceClient` denominado `serviceClient`:

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> En una aplicación de búsqueda típica, el llenado y la administración de índices se controlan mediante un componente independiente de las consultas de búsqueda. `Indexes.GetClient`es conveniente para rellenar un índice porque ahorra Hola problemas de proporcionar otro `SearchCredentials`. Esto hace pasar clave de administración de Hola que Hola de toocreate usado se `SearchServiceClient` toohello nueva `SearchIndexClient`. Sin embargo, en la parte de saludo de la aplicación ejecuta consultas, es mejor hello toocreate `SearchIndexClient` directamente para que pueda pasar de una clave de consulta en lugar de una clave de administración. Esto es coherente con hello [principio de privilegios mínimos](https://en.wikipedia.org/wiki/Principle_of_least_privilege) y que le ayudará a toomake la aplicación más segura. Puede encontrar más información sobre las claves de administración y las claves de consulta en hello [referencia de API de REST de búsqueda de Azure](https://docs.microsoft.com/rest/api/searchservice/).
> 
> 

`SearchIndexClient` tiene una propiedad `Documents`. Esta propiedad proporciona todos los métodos de hello necesarios tooadd, modificar, eliminar o consultar documentos en el índice.

## <a name="decide-which-indexing-action-toouse"></a>Decidir qué indización toouse de acción
datos de tooimport mediante Hola .NET SDK, deberá toopackage seguridad de los datos en un `IndexBatch` objeto. Un `IndexBatch` encapsula una colección de `IndexAction` objetos, cada uno de los cuales contiene un documento y una propiedad que indica qué tooperform de acción de búsqueda de Azure en el documento (carga, merge, delete, etcetera). Dependiendo de cuál de hello debajo de acciones que elija, se deben incluidos para cada documento solo algunos de los campos:

| Acción | Description | Campos necesarios para cada documento | Notas |
| --- | --- | --- | --- |
| `Upload` |Un `Upload` acción es similar tooan "upsert" donde se insertan si es nuevo y actualiza/reemplaza si existe el documento de Hola. |clave, además de cualquier otro campo que se va a toodefine |Al actualizar o reemplazar un documento existente, cualquier campo que no se especifica en la solicitud de hello tendrá su campo establecido demasiado`null`. Esto sucede incluso si el campo Hola anteriormente se estableció un valor no null tooa. |
| `Merge` |Las actualizaciones existentes de documentos con hello especifican campos. Si el documento de hello no existe en el índice de hello, se producirá un error en la mezcla de Hola. |clave, además de cualquier otro campo que se va a toodefine |Cualquier campo que se especifica en una combinación reemplazará el campo existente de hello en el documento de Hola. Aquí se incluyen los campos de tipo `DataType.Collection(DataType.String)`. Por ejemplo, si hello documento contiene un campo `tags` con valor `["budget"]` y ejecutar una combinación con el valor `["economy", "pool"]` para `tags`, Hola valor final de hello `tags` campo será `["economy", "pool"]`. No será `["budget", "economy", "pool"]`. |
| `MergeOrUpload` |Esta acción se comporta como `Merge` si un documento con hello clave dada ya existe en el índice de Hola. Si el documento de hello no existe, se comporta como `Upload` con un nuevo documento. |clave, además de cualquier otro campo que se va a toodefine |- |
| `Delete` |Quita del documento especificado Hola Hola índice de. |solo la clave |Los campos que especifique aparte de campo de clave de Hola se pasará por alto. Si desea tooremove un campo individual de un documento, use `Merge` en su lugar y simplemente establezca explícitamente campo hello toonull. |

También puede especificar qué acción desea toouse con Hola varios métodos estáticos de hello `IndexBatch` y `IndexAction` clases, como se muestra en la siguiente sección de Hola.

## <a name="construct-your-indexbatch"></a>Construcción de IndexBatch
Ahora que sabe qué tooperform acciones en los documentos, está listo tooconstruct Hola `IndexBatch`. Hola de ejemplo siguiente se muestra cómo toocreate un lote con algunas acciones diferentes. Tenga en cuenta que este ejemplo usa una clase personalizada denominada `Hotel` que asigna tooa documento en el índice de "hoteles" Hola.

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

En este caso, usamos `Upload`, `MergeOrUpload`, y `Delete` como nuestras acciones de búsqueda, tal y como especifica métodos de hello llamados en hello `IndexAction` clase.

Se supone que este índice "hoteles" de ejemplo ya está relleno con varios documentos. Tenga en cuenta cómo no se tenía toospecify todos los campos de documento posibles Hola al usar `MergeOrUpload` y cómo se puede especificar sólo clave de documento de hello (`HotelId`) cuando se usa `Delete`.

Además, tenga en cuenta que solo pueden incluir documentos too1000 en una sola solicitud de indización.

> [!NOTE]
> En este ejemplo, estamos aplicando documentos de toodifferent acciones diferentes. Si deseara tooperform Hola mismas acciones en todos los documentos en el lote de hello, en lugar de llamar `IndexBatch.New`, podría utilizar Hola otros métodos estáticos de `IndexBatch`. Por ejemplo, podría crear lotes mediante una llamada a `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` o `IndexBatch.Delete`. Estos métodos toman una colección de documentos (objetos del tipo `Hotel` en este ejemplo), en lugar de objetos `IndexAction`.
> 
> 

## <a name="import-data-toohello-index"></a>Índice de toohello de datos de importación
Ahora que tiene un inicializado `IndexBatch` objeto, puede enviarlo toohello índice mediante una llamada a `Documents.Index` en su `SearchIndexClient` objeto. Hola siguiente ejemplo se muestra cómo toocall `Index`, así como algunos pasos adicionales que deberá tooperform:

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

Hola Nota `try` / `catch` que rodean Hola llamada toohello `Index` método. bloque catch de Hello controla un caso de error importante para la indización. Si se produce un error en el servicio de búsqueda de Azure tooindex algunos de hello documentos en el lote de hello, un `IndexBatchException` producida por `Documents.Index`. Esto puede suceder si indiza documentos mientras el servicio está sobrecargado. **Recomendamos encarecidamente controlar este caso de forma explícita en el código.** Puede retrasar y, a continuación, vuelva a intentar indización documentos Hola que generaron errores o puede iniciar sesión y continuar como ejemplo de Hola o puede hacer algo más según los requisitos de coherencia de datos de su aplicación.

Por último, código de hello en el ejemplo de Hola anterior retrasos en dos segundos. Indización realiza de forma asincrónica en el servicio de búsqueda de Azure, por lo que necesita de aplicación de ejemplo de Hola toowait un tooensure de hora corta que están disponibles para la búsqueda de documentos de Hola. Retrasos así solo suelen ser necesarios en las pruebas, demostraciones y aplicaciones de ejemplo.

<a name="HotelClass"></a>

### <a name="how-hello-net-sdk-handles-documents"></a>Cómo Hola SDK para .NET controla los documentos
Quizás se pregunte cómo Hola SDK de .NET de búsqueda de Azure es las instancias de tooupload capaz de una clase definida por el usuario como `Hotel` toohello índice. toohelp respondamos esa pregunta, echemos un vistazo a hello `Hotel` (clase), que se asigna el esquema de índice toohello definido en [crear un índice de búsqueda de Azure con .NET SDK Hola](search-create-index-dotnet.md#DefineIndex):

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

Hola lo primero que toonotice es que cada propiedad pública de `Hotel` corresponde tooa campo en la definición del índice hello, pero con una diferencia fundamental: nombre de Hola de cada campo empieza por una letra minúscula ("mayúsculas y minúsculas camel"), al nombre de hello cada público propiedad de `Hotel` comienza con una letra mayúscula ("caso Pascal"). Se trata de un escenario común en las aplicaciones de .NET que realizar el enlace de datos donde esquema de destino de hello es control hello fuera del desarrollador de la aplicación hello. En lugar de tener .NET de hello tooviolate las directrices de nomenclatura mediante la realización de los nombres de propiedad y minúscula camel, puede indicar Hola SDK toomap Hola propiedad nombres toocamel caso automáticamente con hello `[SerializePropertyNamesAsCamelCase]` atributo.

> [!NOTE]
> Hola SDK de .NET de búsqueda de Azure usa hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize de biblioteca y deserializar los tooand de objetos de modelos personalizados de JSON. Puede personalizar esta serialización si es necesario. Puede encontrar más información en [Serialización personalizada con JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet). Un ejemplo de esto es el uso de Hola de hello `[JsonProperty]` atributo hello `DescriptionFr` propiedad en el código de ejemplo de Hola anterior.
> 
> 

segunda cosa importante Hola sobre hello `Hotel` clase son tipos de datos de hello propiedades públicas de Hola. tipos de .NET de Hola de estas propiedades asignan tootheir tipos de campo equivalente en la definición del índice Hola. Por ejemplo, hello `Category` propiedad de cadena asigna toohello `category` campo, que es de tipo `DataType.String`. Se dan asignaciones de tipos similares entre `bool?` y `DataType.Boolean`, `DateTimeOffset?` y `DataType.DateTimeOffset`, y así sucesivamente. reglas específicas de Hello para la asignación de tipo hello están documentadas con hello `Documents.Get` método Hola [referencia de SDK de .NET de búsqueda de Azure](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).

Esta capacidad toouse sus propias clases como documentos funciona en ambas direcciones; También puede recuperar los resultados de la búsqueda y tener Hola SDK automáticamente deserializar ellos tooa tipo de su elección, como se muestra en hello [siguiente artículo](search-query-dotnet.md).

> [!NOTE]
> Hola SDK de .NET de búsqueda de Azure también admite documentos dinámicamente tipada utilizando hello `Document` (clase), que es una asignación de clave/valor de los valores de toofield de nombres de campo. Esto es útil en escenarios donde no conoce el esquema de índice de hello en tiempo de diseño, o donde sería clases del modelo de toospecific toobind supone un inconveniente. Todos los métodos de Hola Hola SDK que se encargan de documentos tienen sobrecargas que funcionan con hello `Document` clase, así como fuertemente tipados sobrecargas que toman un parámetro de tipo genérico. Solo Hola este último se utilizan en el código de ejemplo de Hola en este artículo.
> 
> 

**¿Por qué debería usar tipos de datos que aceptan valores null?**

Al diseñar su propio índice modelo clases toomap tooan búsqueda de Azure, se recomienda declarar propiedades de tipos de valor como `bool` y `int` toobe que aceptan valores null (por ejemplo, `bool?` en lugar de `bool`). Si utiliza una propiedad que no acepta valores NULL, tienen también**garantizar** ningún documentos en el índice que contienen un valor nulo para el campo correspondiente Hola. Hola SDK ni Hola servicio Búsqueda de Azure le ayudará a tooenforce esto.

Esto no es simplemente un problema hipotético: Imagine un escenario donde agrega un nuevo índice existente de campo tooan que es de tipo `DataType.Int32`. Después de actualizar la definición del índice hello, todos los documentos tendrá un valor null para ese campo nuevo (ya que todos los tipos admiten valores NULL en la búsqueda de Azure). Si, a continuación, usa una clase de modelo con un acepta valores NULL `int` propiedad para ese campo, obtendrá un `JsonSerializationException` similar a éste al tratar de tooretrieve documentos:

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

Por este motivo, recomendamos utilizar tipos que aceptan valores NULL en las clases de modelo como procedimiento recomendado.

## <a name="next-steps"></a>Pasos siguientes
Después de rellenar el índice de búsqueda de Azure, estará listo toostart emitir toosearch de las consultas para los documentos. Para más información, vea [Consultas en Búsqueda de Azure](search-query-overview.md) .

