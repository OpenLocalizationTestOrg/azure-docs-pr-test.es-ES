---
title: "aaaUpgrading toohello versión 1.1 del SDK de .NET de búsqueda de Azure | Documentos de Microsoft"
description: "Actualizar toohello versión 1.1 del SDK de .NET de búsqueda de Azure"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 66f89958-a320-4a24-87f9-69315848909f
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 291ae5731546e47b3c22c721d3552a79bdea80c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-net-sdk-version-3"></a>Actualizar toohello .NET de búsqueda de Azure SDK versión 3
Si está utilizando la versión preview de 2.0 o anterior de hello [SDK de .NET de búsqueda de Azure](https://aka.ms/search-sdk), este artículo le ayudará a actualizar la versión de toouse aplicación 3.

Para ver un tutorial más general de hello SDK incluidos ejemplos, vea [cómo toouse Azure buscar desde una aplicación .NET](search-howto-dotnet-sdk.md).

Versión 3 de hello SDK de .NET de búsqueda de Azure contiene algunos cambios de versiones anteriores. La mayoría son de menor importancia, por lo que cambiar el código solo precisará del mínimo esfuerzo. Vea [tooupgrade pasos](#UpgradeSteps) para obtener instrucciones sobre cómo toochange su código toouse Hola nueva versión del SDK.

> [!NOTE]
> Si está usando la versión 1.0.2-preview o anterior, debe actualizar tooversion 1.1 en primer lugar y, a continuación, actualizar tooversion 3. Vea [Apéndice: pasos tooupgrade tooversion 1.1](#UpgradeStepsV1) para obtener instrucciones.
>
> La instancia de servicio de búsqueda de Azure es compatible con varias versiones de API de REST, incluidas hello más reciente. Puede continuar toouse una versión cuando ya no es Hola más reciente, pero se recomienda que migre la versión más reciente de código toouse Hola. Cuando se utiliza la API de REST de Hola, debe especificar versión de API de hello en cada solicitud realizada a través del parámetro de versión de la api de Hola. Cuando se usa Hola .NET SDK, versión de Hola de hello SDK usa determina versión correspondiente de Hola de hello API de REST. Si usas un SDK anterior, puede continuar toorun ese código sin cambios aunque servicio hello es la versión de toosupport actualizada una API más recientes.

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a>Novedades de la versión 3
Versión 3 de Hola de destinos de SDK de .NET de búsqueda de Azure de hello última versión disponible con carácter general de hello API de REST de búsqueda de Azure, específicamente 2016-09-01. Esto hace posible toouse muchas características nuevas de búsqueda de Azure desde una aplicación. NET, incluidos Hola siguientes:

* [Analizadores personalizados](https://aka.ms/customanalyzers)
* Compatibilidad del indexador de [Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) y [Azure Table Storage](search-howto-indexing-azure-tables.md)
* Personalización de indizador mediante [asignaciones de campos](search-indexer-field-mappings.md)
* ETags admite la actualización simultánea seguro tooenable de orígenes de datos, los indizadores y las definiciones de índice
* Compatibilidad para generar definiciones de campo de índice mediante declaración al decorar la clase de modelo y con hello nuevo `FieldBuilder` clase.
* Compatibilidad con .NET Core y .NET Portable Profile 111

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a>Tooupgrade de pasos
En primer lugar, actualice la referencia de NuGet para `Microsoft.Azure.Search` utilizando cualquier consola de administrador de paquetes de NuGet de Hola o por el botón secundario en las referencias del proyecto y seleccione "Administrar... de paquetes de NuGet" en Visual Studio.

Una vez que haya descargado NuGet Hola nuevos paquetes y sus dependencias, recompile el proyecto. Dependiendo de cómo se estructura el código, se podrá volver a compilar correctamente. Si es así, está listo toogo.

Si se produce un error en la compilación, verá un error de compilación como Hola siguiente:

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' too'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

paso siguiente Hello es toofix este error de compilación. Vea [cambios importantes en la versión 3](#ListOfChanges) para obtener más información acerca de las causas de error de Hola y cómo toofix lo.

Es posible que vea compilación adicionales relacionados con advertencias tooobsolete métodos o propiedades. advertencias de Hola incluyen instrucciones sobre qué toouse en su lugar de hello característica en desuso. Por ejemplo, si la aplicación utiliza hello `IndexingParameters.Base64EncodeKeys` propiedad, recibirá una advertencia que indica que`"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`

Una vez que haya solucionado los errores de compilación, puede realizar cambios tooyour aplicación tootake aprovechar las nuevas funcionalidades si lo desea. Nuevas características de hello SDK se detallan en [cuáles son las novedades en la versión 3](#WhatsNew).

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a>Cambios importantes en la versión 3
No existe un número reducido de cambios importantes en la versión 3 que requieran código cambia además toorebuilding la aplicación.

### <a name="indexesgetclient-return-type"></a>Tipo de valor devuelto de Indexes.GetClient
Hola `Indexes.GetClient` método tiene un nuevo tipo de valor devuelto. Anteriormente devolvía `SearchIndexClient`, pero esto se cambió demasiado`ISearchIndexClient` en vista previa versión 2.0 lo que conlleva cambios sobre tooversion 3. Se trata de los clientes de toosupport que desea toomock hello `GetClient` método para las pruebas unitarias mediante la devolución de una implementación ficticia del `ISearchIndexClient`.

#### <a name="example"></a>Ejemplo
Si el código tiene el siguiente aspecto:

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

Se puede cambiar toothis toofix cualquier error de compilación:

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-toostrings"></a>AnalyzerName, tipo de datos u otros datos ya no son toostrings implícitamente convertibles
Hay muchos tipos de hello SDK de .NET de búsqueda de Azure que derivan de `ExtensibleEnum`. Anteriormente, estos tipos eran tootype convertirse implícitamente todos los `string`. Sin embargo, se ha detectado un error en hello `Object.Equals` implementación de estas clases y corregir errores de hello necesario deshabilitar esta conversión implícita. Conversión explícita demasiado`string` todavía se permiten.

#### <a name="example"></a>Ejemplo
Si el código tiene el siguiente aspecto:

```csharp
var customTokenizerName = TokenizerName.Create("my_tokenizer"); 
var customTokenFilterName = TokenFilterName.Create("my_tokenfilter"); 
var customCharFilterName = CharFilterName.Create("my_charfilter"); 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        customTokenizerName,  
        new[] { customTokenFilterName },  
        new[] { customCharFilterName }), 
}; 
```

Se puede cambiar toothis toofix cualquier error de compilación:

```csharp
const string CustomTokenizerName = "my_tokenizer"; 
const string CustomTokenFilterName = "my_tokenfilter"; 
const string CustomCharFilterName = "my_charfilter"; 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        CustomTokenizerName,  
        new TokenFilterName[] { CustomTokenFilterName },  
        new CharFilterName[] { CustomCharFilterName })
}; 
```

### <a name="removed-obsolete-members"></a>Miembros obsoletos quitados

Puede que vea toomethods relacionados de errores de compilación o propiedades que se han marcado como obsoleto en la versión 2.0-vista previa y posteriormente, se elimina con la versión 3. Si se producen estos errores, mostramos cómo tooresolve ellos:

- Si usaba este constructor: `ScoringParameter(string name, string value)`, utilice en su lugar este: `ScoringParameter(string name, IEnumerable<string> values)`
- Si usaba hello `ScoringParameter.Value` propiedad, utilice hello `ScoringParameter.Values` propiedad o hello `ToString` método en su lugar.
- Si usaba hello `SearchRequestOptions.RequestId` propiedad, utilice hello `ClientRequestId` propiedad en su lugar.

### <a name="removed-preview-features"></a>Características quitadas de la versión preliminar

Si va a actualizar desde la versión 2.0-versión preliminar tooversion 3, tenga en cuenta que JSON y análisis de compatibilidad para los indizadores de Blob CSV se ha quitado ya que estas características están aún en la vista previa. En concreto, Hola siguiendo métodos de hello `IndexingParametersExtensions` clase se han quitado:

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

Si la aplicación tiene una dependencia fuerte acerca de estas características, no será capaz de tooupgrade tooversion 3 de hello SDK de .NET de búsqueda de Azure. Puede continuar toouse versión 2.0-vista previa. Sin embargo, tenga en cuenta que **no se recomienda usar SDK de versión preliminar en aplicaciones de producción**. Las características de versión preliminar son solo para evaluación y pueden cambiar.

## <a name="conclusion"></a>Conclusión
Si necesita más detalles sobre el uso de hello SDK de .NET de búsqueda de Azure, consulte nuestro actualizados recientemente [procedimientos](search-howto-dotnet-sdk.md).

Le agradecemos sus comentarios en hello SDK. Si tiene problemas, puede tooask libre nos para obtener ayuda sobre hello [foro de MSDN de búsqueda de Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch). Si encuentra un error, puede registrar un problema en hello [repositorio de GitHub de SDK de Azure .NET](https://github.com/Azure/azure-sdk-for-net/issues). Asegúrese de que tooprefix el título del problema con "SDK de búsqueda:".

Gracias por usar Búsqueda de Azure.

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-tooupgrade-tooversion-11"></a>Apéndice: Pasos tooupgrade tooversion 1.1
> [!NOTE]
> En esta sección se aplica solo toousers de hello .NET de búsqueda de Azure SDK versión 1.0.2-preview y anteriores.
> 
> 

En primer lugar, actualice la referencia de NuGet para `Microsoft.Azure.Search` utilizando cualquier consola de administrador de paquetes de NuGet de Hola o por el botón secundario en las referencias del proyecto y seleccione "Administrar... de paquetes de NuGet" en Visual Studio.

Una vez que haya descargado NuGet Hola nuevos paquetes y sus dependencias, recompile el proyecto.

Si estuviera previamente mediante versión 1.0.0-preview, 1.0.1-preview o 1.0.2-preview, compilación Hola debe ejecutarse correctamente y está listo toogo!

Si antes usaba versión 0.13.0-preview o anterior, verá errores como Hola siguiente compilación:

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: hello type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

Hola siguiente paso es errores de compilación de hello toofix uno por uno. La mayor parte requerirán cambiar algunos nombres de clase y método cuyo nombre ha cambiado en hello SDK. [lista de cambios importantes de la versión 1.1](#ListOfChangesV1) contiene una lista de estos cambios de nombre.

Si usa las clases personalizadas toomodel los documentos y las clases tienen propiedades de tipos primitivos que no aceptan valores null (por ejemplo, `int` o `bool` en C#), hay una corrección de errores en la versión de Hola 1.1 del SDK de Hola de los cuales debe tener en cuenta. Para obtener más información, consulte la sección [Correcciones de errores en la versión 1.1](#BugFixesV1) .

Por último, una vez que haya solucionado los errores de compilación, puede realizar cambios tooyour aplicación tootake aprovechar las nuevas funcionalidades si lo desea.

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a>lista de cambios importantes de la versión 1.1
Hello siguiente lista se ordena por probabilidad de Hola que cambio de hello afectará el código de aplicación.

#### <a name="indexbatch-and-indexaction-changes"></a>Cambios de IndexBatch e IndexAction
`IndexBatch.Create`se ha cambiado el nombre demasiado`IndexBatch.New` y ya no tiene un `params` argumento. Puede usar `IndexBatch.New` para los lotes que mezclan distintos tipos de acciones (combinaciones, eliminaciones, etc.). Además, existen nuevos métodos estáticos para crear lotes donde todas las acciones de Hola se Hola igual: `Delete`, `Merge`, `MergeOrUpload`, y `Upload`.

`IndexAction` ya no tiene constructores públicos y sus propiedades ahora son inmutables. Debe usar métodos estáticos de hello nueva para la creación de acciones para propósitos diferentes: `Delete`, `Merge`, `MergeOrUpload`, y `Upload`. `IndexAction.Create` se ha quitado. Si utiliza la sobrecarga de Hola que toma solo un documento, asegúrese de toouse seguro `Upload` en su lugar.

##### <a name="example"></a>Ejemplo
Si el código tiene el siguiente aspecto:

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

Se puede cambiar toothis toofix cualquier error de compilación:

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

Si lo desea, se puede simplificar aún más lo toothis:

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a>Cambios de IndexBatchException
Hola `IndexBatchException.IndexResponse` propiedad ha cambiado de nombre demasiado`IndexingResults`, y su tipo es ahora `IList<IndexingResult>`.

##### <a name="example"></a>Ejemplo
Si el código tiene el siguiente aspecto:

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

Se puede cambiar toothis toofix cualquier error de compilación:

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a>Cambios del método de operación
Cada operación de hello SDK de .NET de búsqueda de Azure se expone como un conjunto de sobrecargas de método para los autores de llamadas sincrónicas y asincrónicas. Hello las firmas y la factorización de estas sobrecargas de método ha cambiado en la versión 1.1.

Por ejemplo, hello operación "Obtener estadísticas de índices" en versiones anteriores de hello SDK expone estas firmas:

En `IIndexOperations`:

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

En `IndexOperationsExtensions`:

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

firmas de métodos de Hola Hola misma operación en la versión 1.1 este aspecto:

En `IIndexesOperations`:

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

En `IndexesOperationsExtensions`:

    // Simplified asynchronous operation
    public static Task<IndexGetStatisticsResult> GetStatisticsAsync(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        CancellationToken cancellationToken = default(CancellationToken));

    // Simplified synchronous operation
    public static IndexGetStatisticsResult GetStatistics(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions));

A partir de la versión 1.1, Hola SDK de .NET de búsqueda de Azure organiza métodos de operación de manera diferente:

* Los parámetros opcionales ahora se modelan como predeterminados en lugar de como sobrecargas de método adicionales. Esto reduce número Hola de sobrecargas del método, en ocasiones drásticamente.
* métodos de extensión de Hello ocultan ahora muchos detalles extraños Hola de HTTP desde el llamador de Hola. Por ejemplo, las versiones anteriores de hello SDK devuelve un objeto de respuesta con un código de estado HTTP, que a menudo no necesitan toocheck debido a que los métodos de operación producen `CloudException` para cualquier código de estado que indica un error. Hola nuevos objetos del modelo de valor devuelto de métodos de extensión, ahorrar Hola problema de tener toounwrap ellas en el código.
* Por el contrario, hello interfaces principales ahora exponen métodos que ofrecen un mayor control en el nivel de hello HTTP si lo necesita. Ahora puede pasar en toobe de encabezados HTTP personalizado incluido en las solicitudes y Hola nueva `AzureOperationResponse<T>` devolver tipo da acceso directo toohello `HttpRequestMessage` y `HttpResponseMessage` para la operación de Hola. `AzureOperationResponse`se define en hello `Microsoft.Rest.Azure` espacio de nombres y reemplaza `Hyak.Common.OperationResponse`.

#### <a name="scoringparameters-changes"></a>Cambios de ScoringParameters
Una nueva clase denominada `ScoringParameter` ha sido agregado en hello toomake SDK más reciente sea más fácil tooprovide parámetros tooscoring los perfiles en una consulta de búsqueda. Hola anteriormente `ScoringProfiles` propiedad de hello `SearchParameters` clase se ha escrito como `IList<string>`; Ahora se ha escrito como `IList<ScoringParameter>`.

##### <a name="example"></a>Ejemplo
Si el código tiene el siguiente aspecto:

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

Se puede cambiar toothis toofix cualquier error de compilación: 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a>Cambios de la clase de modelo
Debido a cambios de firma de toohello descritos en [cambios de método de operación](#OperationMethodChanges), muchas clases de hello `Microsoft.Azure.Search.Models` espacio de nombres se han cambiado de nombre o eliminado. Por ejemplo:

* `IndexDefinitionResponse` se ha reemplazado por `AzureOperationResponse<Index>`
* `DocumentSearchResponse`se ha cambiado el nombre demasiado`DocumentSearchResult`
* `IndexResult`se ha cambiado el nombre demasiado`IndexingResult`
* `Documents.Count()`ahora devuelve un `long` con recuento de documentos de hello en lugar de un`DocumentCountResponse`
* `IndexGetStatisticsResponse`se ha cambiado el nombre demasiado`IndexGetStatisticsResult`
* `IndexListResponse`se ha cambiado el nombre demasiado`IndexListResult`

toosummarize, `OperationResponse`-las clases derivadas que existían solo toowrap un objeto de modelo se han quitado. Hello clases restantes han tenido su sufijo cambió de `Response` demasiado`Result`.

##### <a name="example"></a>Ejemplo
Si el código tiene el siguiente aspecto:

    IndexerGetStatusResponse statusResponse = null;

    try
    {
        statusResponse = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = statusResponse.ExecutionInfo.LastResult;

Se puede cambiar toothis toofix cualquier error de compilación:

    IndexerExecutionInfo status = null;

    try
    {
        status = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = status.LastResult;

##### <a name="response-classes-and-ienumerable"></a>Clases de respuesta e IEnumerable
Un cambio adicional que puede afectar a su código es que las clases de respuesta que contienen colecciones ya no implementan `IEnumerable<T>`. En su lugar, puede tener acceso la propiedad de colección Hola directamente. Por ejemplo, si el código tiene el siguiente aspecto:

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

Se puede cambiar toothis toofix cualquier error de compilación:

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a>Caso especial para aplicaciones web
Si tiene una aplicación web que serializa `DocumentSearchResponse` directamente los resultados de búsqueda de toosend toohello explorador, deberá toochange el código o los resultados de hello no serializará correctamente. Por ejemplo, si el código tiene el siguiente aspecto:

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

Puede cambiarlo obteniendo hello `.Results` propiedad de la representación de resultados de búsqueda de hello búsqueda respuesta toofix:

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

Habrá toolook para estos casos en el código por sí mismo; **compilador hello no le avisará** porque `JsonResult.Data` es de tipo `object`.

#### <a name="cloudexception-changes"></a>Cambios de CloudException
Hola `CloudException` clase ha pasado de hello `Hyak.Common` toohello de espacio de nombres `Microsoft.Rest.Azure` espacio de nombres. Además, su `Error` propiedad ha cambiado de nombre demasiado`Body`.

#### <a name="searchserviceclient-and-searchindexclient-changes"></a>Cambios de SearchServiceClient y SearchIndexClient
Hola tipo de hello `Credentials` propiedad ha cambiado respecto de `SearchCredentials` tooits de la clase base `ServiceClientCredentials`. Si necesita hello tooaccess `SearchCredentials` de un `SearchIndexClient` o `SearchServiceClient`, use Hola nuevo `SearchCredentials` propiedad.

En versiones anteriores de hello SDK, `SearchServiceClient` y `SearchIndexClient` tenía constructores que tuvieron un `HttpClient` parámetro. Estos se han reemplazado con constructores que obtienen `HttpClientHandler` y una matriz de objetos `DelegatingHandler`. Esto hace más fácil tooinstall controladores personalizados toopre proceso las solicitudes HTTP si es necesario.

Por último, Hola constructores que tardan una `Uri` y `SearchCredentials` han cambiado. Por ejemplo, si tiene código con este aspecto:

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

Se puede cambiar toothis toofix cualquier error de compilación:

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

También tenga en cuenta que el tipo hello de hello credenciales parámetro ha cambiado demasiado`ServiceClientCredentials`. Esto es improbable tooaffect su código desde `SearchCredentials` se deriva de `ServiceClientCredentials`.

#### <a name="passing-a-request-id"></a>Transferir un identificador de solicitud
En versiones anteriores de hello SDK, puede establecer un identificador de solicitud en hello `SearchServiceClient` o `SearchIndexClient` y se incluiría en cada toohello de solicitud API de REST. Esto es útil para solucionar problemas con el servicio de búsqueda si necesita compatibilidad con toocontact. Sin embargo, resulta más útil tooset un identificador único de la solicitud para cada operación en lugar de toouse Hola mismo identificador para todas las operaciones. Por esta razón, Hola `SetClientRequestId` métodos de `SearchServiceClient` y `SearchIndexClient` se han quitado. En su lugar, puede pasar un método de operación de tooeach de Id. de solicitud a través de hello opcional `SearchRequestOptions` parámetro.

> [!NOTE]
> En una futura versión de SDK de hello, agregaremos un nuevo mecanismo para establecer un identificador de solicitud global en el cliente de hello objetos que es coherente con el enfoque de hello utilizado por otros SDK de Azure.
> 
> 

#### <a name="example"></a>Ejemplo
Si tiene código con este aspecto:

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

Se puede cambiar toothis toofix cualquier error de compilación:

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a>Cambios de nombre de interfaz
nombres de interfaz de Hello operación grupo tienen todos los toobe modificados coherente con sus nombres de propiedad correspondientes:

* Hola tipo de `ISearchServiceClient.Indexes` se ha cambiado de `IIndexOperations` demasiado`IIndexesOperations`.
* Hola tipo de `ISearchServiceClient.Indexers` se ha cambiado de `IIndexerOperations` demasiado`IIndexersOperations`.
* Hola tipo de `ISearchServiceClient.DataSources` se ha cambiado de `IDataSourceOperations` demasiado`IDataSourcesOperations`.
* Hola tipo de `ISearchIndexClient.Documents` se ha cambiado de `IDocumentOperations` demasiado`IDocumentsOperations`.

Este cambio es poco probable que tooaffect su código a menos que cree las simulaciones de estas interfaces para fines de prueba.

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a>Correcciones de errores en la versión 1.1
Se produjo un error en las versiones anteriores de hello SDK de .NET de búsqueda de Azure relacionado tooserialization de clases de modelos personalizados. Error de Hello puede producirse si ha creado una clase de modelo personalizado con una propiedad de un tipo de valor no acepta valores NULL.

#### <a name="steps-tooreproduce"></a>Tooreproduce de pasos
Cree una clase de modelo personalizado con una propiedad de tipo de valor que no acepta valores NULL. Por ejemplo, agregue una propiedad `UnitCount` pública de tipo `int` en lugar de `int?`.

Si se puede indizar un documento con el valor predeterminado de Hola de ese tipo (por ejemplo, 0 para `int`), campo Hola será null en la búsqueda de Azure. Si posteriormente desea buscar ese documento, Hola `Search` llamada producirá `JsonSerializationException` quejan de que no se puede convertir `null` demasiado`int`.

Además, los filtros no funcionen según lo esperado desde que null se escribió toohello índice en lugar de valor de hello diseñado.

#### <a name="fix-details"></a>Detalles de corrección
Este problema se ha corregido en la versión 1.1 de hello SDK. Ahora, si tiene una clase de modelo similar a la siguiente:

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

y establece `IntValue` too0, que valor es ahora correctamente serializado como 0 en el cable de Hola y almacenado como 0 en el índice de Hola. El recorrido de ida y vuelta también funciona según lo previsto.

Hay un toobe problema potencial en cuenta con este enfoque: si usa un tipo de modelo con una propiedad que no acepta valores NULL, tienen también**garantizar** ningún documentos en el índice que contienen un valor nulo para el campo correspondiente Hola. Hola SDK ni Hola API de REST de búsqueda de Azure le ayudará a tooenforce esto.

Esto no es simplemente un problema hipotético: Imagine un escenario donde agrega un nuevo índice existente de campo tooan que es de tipo `Edm.Int32`. Después de actualizar la definición del índice hello, todos los documentos tendrá un valor null para ese campo nuevo (ya que todos los tipos admiten valores NULL en la búsqueda de Azure). Si, a continuación, usa una clase de modelo con un acepta valores NULL `int` propiedad para ese campo, obtendrá un `JsonSerializationException` similar a éste al tratar de tooretrieve documentos:

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

Por este motivo, recomendamos utilizar tipos que aceptan valores null en las clases de modelo como procedimiento recomendado.

Para obtener más detalles sobre esta corrección hello y errores, vea [este problema en GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).

