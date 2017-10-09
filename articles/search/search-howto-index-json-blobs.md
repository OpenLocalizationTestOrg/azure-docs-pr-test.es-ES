---
title: "BLOB JSON de aaaIndexing con el indizador de búsqueda de Azure blob"
description: "Indexación de blobs JSON con el indexador de blobs de Azure Search"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 57e32e51-9286-46da-9d59-31884650ba99
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: 269968714358cd40ea66863b4dbb97766e1d77e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-json-blobs-with-azure-search-blob-indexer"></a>Indexación de blobs JSON con el indexador de blobs de Azure Search
Este artículo muestra cómo tooconfigure búsqueda de Azure blob indizador tooextract estructura el contenido de blobs que contienen JSON.

## <a name="scenarios"></a>Escenarios
De forma predeterminada, el [indexador de blobs de Azure Search](search-howto-indexing-azure-blob-storage.md) analiza los blobs JSON como un único fragmento de texto. A menudo, desea toopreserve estructura de Hola de documentos JSON. Por ejemplo, dado el documento JSON de Hola

    {
        "article" : {
             "text" : "A hopefully useful article explaining how tooparse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

puede ser conveniente tooparse en una búsqueda de Azure con "text", "datePublished" y "etiquetas" campos de documento.

O bien, cuando los blobs contienen un **matriz de objetos JSON**, puede que desee cada elemento de matriz de hello toobecome un documento de búsqueda de Azure independiente. Por ejemplo, en un blob con este JSON:  

    [
        { "id" : "1", "text" : "example 1" },
        { "id" : "2", "text" : "example 2" },
        { "id" : "3", "text" : "example 3" }
    ]

puede rellenar el índice de Azure Search con tres documentos independientes, cada uno de ellos con los campos "id" y "text".

> [!IMPORTANT]
> matriz JSON de Hello funcionalidad de análisis está actualmente en vista previa. Está disponible únicamente en la API de REST de hello mediante versión **vista previa 2015-02-28**. Recuerde que las versiones preliminares de las API están pensadas para realizar pruebas y evaluaciones, y no deben usarse en entornos de producción.
>
>

## <a name="setting-up-json-indexing"></a>Configuración de la indexación de JSON
Indización de blobs JSON es la extracción de documento normal toohello similar. En primer lugar, cree el origen de datos de hello exactamente como lo haría normalmente: 

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "optional, my-folder" }
    }   

A continuación, crear índice de búsqueda de destino de hello si aún no tiene uno. 

Por último, cree un indizador y establezca hello `parsingMode` parámetro demasiado`json` (tooindex cada blob como un solo documento) o `jsonArray` (si los blobs contienen matrices JSON y necesita que cada elemento de un toobe de matriz que se trata como un documento independiente):

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } }
    }

Si es necesario, utilice **campo asignaciones** toopick Hola propiedades de hello origen JSON documento que se usó toopopulate al índice de búsqueda de destino, tal y como se muestra en la siguiente sección de Hola.

> [!IMPORTANT]
> Cuando se usa el modo de análisis de `json` o `jsonArray`, Azure Search da por hecho que todos los blobs en el origen de datos contienen JSON. Si necesita toosupport una combinación de JSON y JSON no blobs de hello mismo origen de datos, hacernos saber en [nuestro sitio UserVoice](https://feedback.azure.com/forums/263029-azure-search).
>
>

## <a name="using-field-mappings-toobuild-search-documents"></a>Uso de documentos de búsqueda de toobuild de asignaciones de campo
Actualmente, Azure Search no puede indexar documentos JSON arbitrarios directamente, ya que admite solo tipos de datos primitivos, matrices de cadenas y puntos de GeoJSON. Sin embargo, puede usar **campo asignaciones** toopick partes de la JSON documentar y "elevación" ellos en campos de nivel superior del documento de búsqueda de Hola. toolearn sobre aspectos básicos de las asignaciones de campo, vea [asignaciones de campos de indizador de búsqueda de Azure salvar las diferencias de hello entre orígenes de datos y los índices de búsqueda](search-indexer-field-mappings.md).

Próximamente nuevo documento JSON de ejemplo de tooour:

    {
        "article" : {
             "text" : "A hopefully useful article explaining how tooparse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

Supongamos que tiene un índice de búsqueda con hello siguientes campos: `text` de tipo `Edm.String`, `date` de tipo `Edm.DateTimeOffset`, y `tags` de tipo `Collection(Edm.String)`. toomap su JSON en hello deseado forma, use Hola siguiendo las asignaciones de campos:

    "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
      ]

Hello nombres de campo de origen de asignaciones de Hola se especifican utilizando hello [JSON puntero](http://tools.ietf.org/html/rfc6901) notación. Empezar con una raíz de barra diagonal toorefer toohello del documento JSON y luego elija una propiedad de hello deseado (en el nivel arbitrario de anidamiento) con ruta de acceso separadas por barra diagonal hacia delante.

También puede hacer referencia a elementos de la matriz de tooindividual mediante el uso de un índice de base cero. Por ejemplo, el primer elemento de Hola de toopick de Hola "etiquetas" matriz de Hola por encima de ejemplo, usar una asignación de campo como el siguiente:

    { "sourceFieldName" : "/article/tags/0", "targetFieldName" : "firstTag" }

> [!NOTE]
> Si un nombre de campo de origen en una ruta de acceso de asignación de campo hace referencia la propiedad tooa que no existe en JSON, se omite esa asignación sin indicar un error. Esto se realiza, por lo que podemos admitir documentos con un esquema diferente (que es un caso de uso frecuente). Porque no hay ninguna validación, debe errores tipográficos tooavoid de atención de tootake en la especificación de asignaciones de campo.
>
>

Si sus documentos JSON solo contienen propiedades simples de nivel superior, es posible que no necesite asignaciones de campo. Por ejemplo, si su JSON es similar a este, propiedades de nivel superior de Hola "text", "datePublished" y "etiquetas" directamente asigna toohello correspondientes campos de índice de búsqueda de hello:

    {
       "text" : "A hopefully useful article explaining how tooparse JSON blobs",
       "datePublished" : "2016-04-13"
       "tags" : [ "search", "storage", "howto" ]    
     }

Esta es una carga completa del indexador con asignaciones de campos:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } },
      "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
        ]
    }

## <a name="indexing-nested-json-arrays"></a>Indexación de matrices anidadas JSON
¿Qué ocurre si desea tooindex una matriz de objetos JSON, pero esa matriz se anida en algún lugar dentro del documento de Hola? Puede elegir qué propiedad contiene matriz hello mediante hello `documentRoot` propiedad de configuración. Por ejemplo, si los blobs tienen el siguiente aspecto:

    {
        "level1" : {
            "level2" : [
                { "id" : "1", "text" : "Use hello documentRoot property" },
                { "id" : "2", "text" : "toopluck hello array you want tooindex" },
                { "id" : "3", "text" : "even if it's nested inside hello document" }  
            ]
        }
    }

Utilice esta matriz de hello tooindex de configuración contenida en hello `level2` propiedad:

    {
        "name" : "my-json-array-indexer",
        ... other indexer properties
        "parameters" : { "configuration" : { "parsingMode" : "jsonArray", "documentRoot" : "/level1/level2" } }
    }

## <a name="help-us-make-azure-search-better"></a>Ayúdenos a mejorar Búsqueda de Azure
Si dispone de las solicitudes de características o ideas para mejoras, acérquese toous en nuestra [sitio UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
