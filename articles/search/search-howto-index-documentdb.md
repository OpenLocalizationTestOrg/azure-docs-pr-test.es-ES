---
title: "aaaIndexing un origen de datos de la base de datos de Cosmos para búsqueda de Azure | Documentos de Microsoft"
description: "Este artículo muestra cómo toocreate un indizador de búsqueda de Azure con la base de datos de Cosmos como un origen de datos."
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: search
ms.date: 08/10/2017
ms.author: eugenesh
ms.openlocfilehash: 195c9bc026ee1591679dc425ef083a32a3c86be6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-cosmos-db-with-azure-search-using-indexers"></a>Conexión de Cosmos DB con Azure Search mediante indexadores

Si desea tooimplement una búsqueda excelente experiencia sobre los datos de la base de datos de Cosmos, puede usar un datos toopull de indizador de búsqueda de Azure en un índice de búsqueda de Azure. En este artículo, le mostraremos cómo toointegrate base de datos de Azure Cosmos con búsqueda de Azure sin necesidad de toowrite cualquier infraestructura de indización de código toomaintain.

tooset de un indizador de Cosmos DB, debe tener un [servicio Búsqueda de Azure](search-create-service-portal.md)y crear un índice, origen de datos y por último Hola indizador. Puede crear estos objetos mediante hello [portal](search-import-data-portal.md), [.NET SDK](/dotnet/api/microsoft.azure.search), o [API de REST](/rest/api/searchservice/) para todos los lenguajes de .NET que no sean. 

Si se opta por el portal de hello, Hola [Asistente para importar datos](search-import-data-portal.md) le guía a través de la creación de hello de todos estos recursos.

> [!NOTE]
> COSMOS DB es hello siguiente generación de documentos. Aunque se cambia el nombre de producto de hello, sintaxis es Hola mismo que antes. Continúe toospecify `documentdb` como se indica en este artículo de indizador. 

> [!TIP]
> Puede iniciar hello **importar datos** Asistente de Hola DB Cosmos panel toosimplify la indización para ese origen de datos. En la navegación de la izquierda, vaya demasiado**colecciones** > **Agregar búsqueda de Azure** tooget iniciado.

<a name="Concepts"></a>
## <a name="azure-search-indexer-concepts"></a>Conceptos del indexador de Azure Search
Azure admite la búsqueda Hola creación y administración de orígenes de datos (como la base de datos de Cosmos) e indizadores que funcionan con los orígenes de datos.

A **origen de datos** especifica tooindex de datos de Hola, credenciales y directivas para identificar cambios en los datos de hello (por ejemplo, modificados o eliminados los documentos dentro de la colección). origen de datos de Hola se define como un recurso independiente de modo que se puede utilizar por varios indizadores.

Un **indizador** describe cómo fluyen los datos de Hola desde el origen de datos en un índice de búsqueda de destino. Los indexadores se pueden utilizar para:

* Realizar una copia única de hello datos toopopulate un índice.
* Sincronizar un índice con cambios en el origen de datos de hello según una programación. programación de Hello es parte de la definición de indizador de Hola.
* Invoque el índice de actualizaciones a petición tooan según sea necesario.

<a name="CreateDataSource"></a>
## <a name="step-1-create-a-data-source"></a>Paso 1: Creación de un origen de datos
toocreate un origen de datos, realice una entrada de blog:

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId", "query": null },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        }
    }

cuerpo de saludo de solicitud de hello contiene definición de origen de datos de hello, que debe incluir Hola siguientes campos:

* **nombre**: elija cualquier toorepresent de nombre de la base de datos de la base de datos de Cosmos.
* **type**: debe ser `documentdb`.
* **credenciales**:
  
  * **connectionString**: obligatorio. Especificar la base de datos de la base de datos de Azure Cosmos de tooyour de hello conexión información Hola siguiendo el formato:`AccountEndpoint=<Cosmos DB endpoint url>;AccountKey=<Cosmos DB auth key>;Database=<Cosmos DB database id>`
* **contenedor**:
  
  * **nombre**: obligatorio. Especifique el identificador de Hola de Hola DB Cosmos colección toobe indizado.
  * **consulta**: opcional. Puede especificar un tooflatten consulta un documento JSON arbitrario en un esquema sin formato que se puede indizar la búsqueda de Azure.
* **dataChangeDetectionPolicy**: se recomienda. Consulte la sección [Indexación de documentos modificados](#DataChangeDetectionPolicy).
* **dataDeletionDetectionPolicy**: opcional. Consulte la sección [Indexación de documentos eliminados](#DataDeletionDetectionPolicy).

### <a name="using-queries-tooshape-indexed-data"></a>Usar consultas tooshape indizar datos
Puede especificar un tooflatten de consulta de base de datos de Cosmos anidadas propiedades o matrices, proyectar las propiedades JSON y filtrar Hola datos toobe indizado. 

Documento de ejemplo:

    {
        "userId": 10001,
        "contact": {
            "firstName": "andy",
            "lastName": "hoh"
        },
        "company": "microsoft",
        "tags": ["azure", "documentdb", "search"]
    }

Consulta de filtro:

    SELECT * FROM c WHERE c.company = "microsoft" and c._ts >= @HighWaterMark ORDER BY c._ts

Consulta sin formato:

    SELECT c.id, c.userId, c.contact.firstName, c.contact.lastName, c.company, c._ts FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts
    
    
Consulta de proyección:

    SELECT VALUE { "id":c.id, "Name":c.contact.firstName, "Company":c.company, "_ts":c._ts } FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts


Consulta sin formato de matriz:

    SELECT c.id, c.userId, tag, c._ts FROM c JOIN tag IN c.tags WHERE c._ts >= @HighWaterMark ORDER BY c._ts

<a name="CreateIndex"></a>
## <a name="step-2-create-an-index"></a>Paso 2: Creación de un índice
Si aún no tiene un índice de Búsqueda de Azure de destino, créelo. Puede crear un índice mediante hello [UI del portal de Azure](search-create-index-portal.md), hello [crear API de REST de índice](/rest/api/searchservice/create-index) o [Index (clase)](/dotnet/api/microsoft.azure.search.models.index).

Hola de ejemplo siguiente crea un índice con un campo de identificador y la descripción:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
       "name": "mysearchindex",
       "fields": [{
         "name": "id",
         "type": "Edm.String",
         "key": true,
         "searchable": false
       }, {
         "name": "description",
         "type": "Edm.String",
         "filterable": false,
         "sortable": false,
         "facetable": false,
         "suggestions": true
       }]
     }

Asegúrese de que Hola esquema de su índice de destino es compatible con el esquema de Hola Hola JSON de documentos de origen o la salida de hello de la proyección de consulta personalizada.

> [!NOTE]
> Para las colecciones particionadas, clave de documento de hello predeterminada es de Cosmos DB `_rid` propiedad, que le cambia el nombre demasiado`rid` en búsqueda de Azure. Además, los valores `_rid` de Cosmos DB contienen caracteres que no son válidos en las claves de Azure Search. Por esta razón, Hola `_rid` valores están codificados con Base64.
> 
> 

### <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>asignación entre tipos de datos de JSON y de Búsqueda de Azure
| TIPO DE DATOS DE JSON | TIPOS DE CAMPOS DE ÍNDICE DE DESTINO COMPATIBLES |
| --- | --- |
| Booleano |Edm.Boolean, Edm.String |
| Números que parecen enteros |Edm.Int32, Edm.Int64, Edm.String |
| Números que parecen puntos flotantes |Edm.Double, Edm.String |
| Cadena |Edm.String |
| Matrices de tipos primitivos, por ejemplo ["a", "b", "c"] |Collection(Edm.String) |
| Cadenas que parecen fechas |Edm.DateTimeOffset, Edm.String |
| Objetos GeoJSON, por ejemplo, {"tipo": "Punto", "coordenadas": [long, lat]} |Edm.GeographyPoint |
| Otros objetos JSON |N/D |

<a name="CreateIndexer"></a>
## <a name="step-3-create-an-indexer"></a>Paso 3: Creación de un indexador

Una vez que se han creado el origen de datos e índices de hello, está listo toocreate indizador de hello:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "mydocdbindexer",
      "dataSourceName" : "mydocdbdatasource",
      "targetIndexName" : "mysearchindex",
      "schedule" : { "interval" : "PT2H" }
    }

Este indizador se ejecuta cada dos horas (intervalo de programación se establece demasiado "PT2H"). toorun un indizador cada 30 minutos, establezca el intervalo de saludo demasiado "PT30M". intervalo admitido de Hello más corta es 5 minutos. Hola programación es opcional: si se omite, un indizador que se ejecuta solo una vez cuando se crea. Sin embargo, puede ejecutarlo a petición en cualquier momento.   

Para obtener más detalles sobre Hola crear API de indizador, visite [crear indizador](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

<a id="RunIndexer"></a>
### <a name="running-indexer-on-demand"></a>Ejecución del indexador a petición
En suma toorunning periódicamente según una programación, un indizador también se puede invocar a petición:

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=2016-09-01
    api-key: [Search service admin key]

> [!NOTE]
> Cuando ejecute API devuelve correctamente, se ha programado la invocación de indizador de Hola, pero el procesamiento real de Hola se produce de forma asincrónica. 

Puede supervisar el estado de indizador de hello en portal de Hola o con hello obtener indizador estado API, que se describen a continuación. 

<a name="GetIndexerStatus"></a>
### <a name="getting-indexer-status"></a>Obtención del estado del indexador
Puede recuperar el historial de estado y la ejecución de Hola de un indizador:

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=2016-09-01
    api-key: [Search service admin key]

respuesta de Hello contiene el estado general del indizador, invocación de indizador último (o en curso) de Hola y Hola el historial reciente invocaciones de indizador.

    {
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
         },
        "executionHistory":[ {
            "status":"success",
             "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        }]
    }

Historial de ejecución contiene la toohello 50 últimas ejecuciones completadas, que se ordenan en orden cronológico inverso (de modo que ocurra ejecución más reciente de Hola en respuesta de hello).

<a name="DataChangeDetectionPolicy"></a>
## <a name="indexing-changed-documents"></a>Indexación de documentos modificados
propósito de Hola de los datos cambia la directiva de detección es tooefficiently identificar elementos de datos que han cambiado. Actualmente, directiva de hello solo admitido es hello `High Water Mark` directiva mediante hello `_ts` propiedad (marca de tiempo) proporcionada por base de datos de Cosmos, que se especifica como sigue:

    {
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "_ts"
    }

Mediante esta directiva es muy recomendable rendimiento de indizador buena tooensure. 

Si está utilizando una consulta personalizada, asegúrese de que ese hello `_ts` propiedad se proyecta mediante la consulta de Hola.

<a name="IncrementalProgress"></a>
### <a name="incremental-progress-and-custom-queries"></a>Progreso incremental y consultas personalizadas
Progreso incremental durante la indización garantiza que si se interrumpe la ejecución de indizador por errores transitorios o límite de tiempo de ejecución, el indizador de hello puede recoger donde se quedó próxima vez se ejecuta, en lugar de tener la colección completa de hello toore índice desde el principio. Esto es especialmente importante cuando se indexan colecciones grandes. 

tooenable el progreso incremental cuando se usa una consulta personalizada, asegúrese de que la consulta ordena los resultados de Hola por hello `_ts` columna. Esto permite periódica comprobación que señala a la que búsqueda de Azure usa el progreso incremental de tooprovide en presencia de Hola de errores.   

En algunos casos, incluso si la consulta contiene un `ORDER BY [collection alias]._ts` cláusula, búsqueda de Azure puede no deducir esa consulta Hola está ordenada por hello `_ts`. Puede indicar que la búsqueda de Azure que los resultados se ordenan mediante el uso de hello `assumeOrderByHighWaterMarkColumn` propiedad de configuración. toospecify esta sugerencia, crear o actualizar el indizador como sigue: 

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "assumeOrderByHighWaterMarkColumn" : true } }
    } 

<a name="DataDeletionDetectionPolicy"></a>
## <a name="indexing-deleted-documents"></a>Indexación de documentos eliminados
Cuando se eliminan filas de la colección de hello, normalmente desea toodelete las filas del índice de búsqueda de hello así. Hola de una directiva de detección de eliminación de datos sirve tooefficiently identificar elementos de datos eliminados. Actualmente, directiva de hello solo admitido es hello `Soft Delete` directiva (eliminación está marcada con una marca de algún tipo), que se especifica como sigue:

    {
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "hello property that specifies whether a document was deleted",
        "softDeleteMarkerValue" : "hello value that identifies a document as deleted"
    }

Si está utilizando una consulta personalizada, asegúrese de que esa propiedad Hola al que hace referencia `softDeleteColumnName` se proyecta mediante la consulta de Hola.

Hola de ejemplo siguiente crea un origen de datos con una directiva de eliminación temporal:

    POST https://[Search service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId" },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        },
        "dataDeletionDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName": "isDeleted",
            "softDeleteMarkerValue": "true"
        }
    }

## <a name="NextSteps"></a>Pasos siguientes
¡Enhorabuena! Ha aprendido cómo toointegrate base de datos de Azure Cosmos con búsqueda de Azure mediante Hola indizador para la base de datos de Cosmos.

* toolearn cómo más información acerca de la base de datos de Cosmos de Azure, vea hello [página de servicio de base de datos de Cosmos](https://azure.microsoft.com/services/documentdb/).
* toolearn cómo más información acerca de la búsqueda de Azure, vea hello [página de servicio de búsqueda](https://azure.microsoft.com/services/search/).
