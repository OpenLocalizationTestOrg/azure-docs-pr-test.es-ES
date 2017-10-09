---
title: "aaa \"cargar datos (API de REST - búsqueda de Azure) | Documentos de Microsoft\""
description: "Obtenga información acerca de cómo el índice de tooan tooupload datos en búsqueda de Azure con Hola API de REST."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: 8d0749fb-6e08-4a17-8cd3-1a215138abc6
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 6ba1336012d1f0f6d6d6c933e16aa879afb9b824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-rest-api"></a>Carga datos tooAzure búsqueda mediante Hola API de REST
> [!div class="op_single_selector"]
>
> * [Información general](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
>
>

En este artículo le mostrará cómo hello toouse [API de REST de búsqueda de Azure](https://docs.microsoft.com/rest/api/searchservice/) tooimport datos en un índice de búsqueda de Azure.

Antes de comenzar este tutorial, debe haber [creado ya un índice de Búsqueda de Azure](search-what-is-an-index.md).

En documentos de toopush de orden en el índice mediante API de REST de hello, emitirá el punto de conexión de dirección URL de HTTP POST solicitud tooyour de un índice. cuerpo de Hola de hello solicitud HTTP cuerpo es un objeto JSON que contiene documentos de hello toobe agregado, modificado o eliminado.

## <a name="identify-your-azure-search-services-admin-api-key"></a>Identificación de la clave de API de administración del servicio de Búsqueda de Azure
Cuando se emite solicitudes HTTP en su servicio mediante las API de REST, hello *cada* solicitud de API debe incluir Hola clave de api que se generó Hola aprovisionar el servicio de búsqueda. Tener una clave válida establece la confianza, por cada solicitud, entre Hola aplicación enviando Hola solicitud y el servicio de Hola que los controle.

1. toofind claves de api de su servicio, puede iniciar sesión en toohello [portal de Azure](https://portal.azure.com/)
2. Vaya hoja del servicio de búsqueda de Azure tooyour
3. Haga clic en hello icono "Claves"

El servicio tendrá *claves de administración* y *claves de consulta*.

* El principal y secundaria *claves de administración* conceder derechos completos tooall operaciones, incluido el servicio de hello capacidad toomanage hello, crear y eliminar índices, los indizadores y orígenes de datos. Existen dos claves para que pueda continuar la clave secundaria de hello toouse si decide tooregenerate Hola primary key y viceversa.
* Su *claves de consulta* conceder acceso de solo lectura tooindexes y documentos, y son aplicaciones tooclient normalmente distribuida que emiten solicitudes de búsqueda.

Por motivos de saludo de la importación de datos en un índice, puede usar su clave de administración principal o secundaria.

## <a name="decide-which-indexing-action-toouse"></a>Decidir qué indización toouse de acción
Cuando se utiliza la API de REST de Hola, se van a emitir solicitudes HTTP POST con la dirección URL del extremo del índice JSON solicitud cuerpos tooyour búsqueda de Azure. objeto JSON de Hello en el cuerpo de la solicitud HTTP contiene una matriz JSON con el nombre "value" que contiene los objetos JSON que representa los documentos que le gustaría tooadd tooyour índice, actualizar o eliminar.

Cada objeto JSON de matriz de "value" hello representa un toobe documento indizado. Cada uno de estos objetos contiene la clave del documento de Hola y especifica la acción de indización de hello deseado (carga, merge, delete, etcetera). Dependiendo de cuál de hello debajo de acciones que elija, se deben incluidos para cada documento solo algunos de los campos:

| @search.action | Descripción | Campos necesarios para cada documento | Notas |
| --- | --- | --- | --- |
| `upload` |Un `upload` acción es similar tooan "upsert" donde se insertan si es nuevo y actualiza/reemplaza si existe el documento de Hola. |clave, además de cualquier otro campo que se va a toodefine |Al actualizar o reemplazar un documento existente, cualquier campo que no se especifica en la solicitud de hello tendrá su campo establecido demasiado`null`. Esto sucede incluso si el campo Hola anteriormente se estableció un valor no null tooa. |
| `merge` |Las actualizaciones existentes de documentos con hello especifican campos. Si el documento de hello no existe en el índice de hello, se producirá un error en la mezcla de Hola. |clave, además de cualquier otro campo que se va a toodefine |Cualquier campo que se especifica en una combinación reemplazará el campo existente de hello en el documento de Hola. Aquí se incluyen los campos de tipo `Collection(Edm.String)`. Por ejemplo, si hello documento contiene un campo `tags` con valor `["budget"]` y ejecutar una combinación con el valor `["economy", "pool"]` para `tags`, Hola valor final de hello `tags` campo será `["economy", "pool"]`. No será `["budget", "economy", "pool"]`. |
| `mergeOrUpload` |Esta acción se comporta como `merge` si un documento con hello clave dada ya existe en el índice de Hola. Si el documento de hello no existe, se comporta como `upload` con un nuevo documento. |clave, además de cualquier otro campo que se va a toodefine |- |
| `delete` |Quita del documento especificado Hola Hola índice de. |solo la clave |Los campos que especifique aparte de campo de clave de Hola se pasará por alto. Si desea tooremove un campo individual de un documento, use `merge` en su lugar y simplemente establezca explícitamente campo hello toonull. |

## <a name="construct-your-http-request-and-request-body"></a>Construcción de la solicitud HTTP y el cuerpo de la solicitud
Ahora que ha recopilado los valores de campo necesarios de Hola para las acciones de índice, es solicitudes HTTP real de tooconstruct listo hello y JSON solicitar cuerpo tooimport los datos.

#### <a name="request-and-request-headers"></a>Solicitudes y encabezados de solicitud
En dirección URL de hello, deberá tooprovide el nombre del servicio, el nombre del índice ("hoteles" en este caso), así como la versión adecuada de API de hello (es la versión actual de la API de hello `2016-09-01` en tiempo de hello sobre la publicación de este documento). Necesitará hello toodefine `Content-Type` y `api-key` encabezados de solicitud. Para Hola este último, use una de las claves de administración de su servicio.

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a>Cuerpo de la solicitud
```JSON
{
    "value": [
        {
            "@search.action": "upload",
            "hotelId": "1",
            "baseRate": 199.0,
            "description": "Best hotel in town",
            "description_fr": "Meilleur hôtel en ville",
            "hotelName": "Fancy Stay",
            "category": "Luxury",
            "tags": ["pool", "view", "wifi", "concierge"],
            "parkingIncluded": false,
            "smokingAllowed": false,
            "lastRenovationDate": "2010-06-27T00:00:00Z",
            "rating": 5,
            "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
            "@search.action": "upload",
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags": ["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
            "@search.action": "mergeOrUpload",
            "hotelId": "3",
            "baseRate": 129.99,
            "description": "Close tootown hall and hello river"
        },
        {
            "@search.action": "delete",
            "hotelId": "6"
        }
    ]
}
```

En este caso, estamos usando `upload`, `mergeOrUpload` y `delete` como acciones de búsqueda.

Se supone que este índice "hoteles" de ejemplo ya está relleno con varios documentos. Tenga en cuenta cómo no se tenía toospecify todos los campos de documento posibles Hola al usar `mergeOrUpload` y cómo se puede especificar sólo clave de documento de hello (`hotelId`) cuando se usa `delete`.

Además, tenga en cuenta que solo pueden incluir documentos too1000 (o 16 MB) en una sola solicitud de indización.

## <a name="understand-your-http-response-code"></a>Descripción del código de respuesta HTTP
#### <a name="200"></a>200
Después de enviar una solicitud de indexación correcta recibirá una respuesta HTTP con código de estado de `200 OK`. Hola cuerpo JSON de hello respuesta HTTP será la siguiente:

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": true,
            "errorMessage": null
        },
        ...
    ]
}
```

#### <a name="207"></a>207
Se devolverá un código de estado de `207` solo con que un elemento no se indexe correctamente. Hola cuerpo JSON de la respuesta HTTP de hello contendrá información sobre Hola incorrecta o los documentos.

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": false,
            "errorMessage": "hello search service is too busy tooprocess this document. Please try again later."
        },
        ...
    ]
}
```

> [!NOTE]
> Esto suele significar que esa carga de hello en la búsqueda de su servicio está alcanzando un punto donde las solicitudes de indización comenzarán tooreturn `503` las respuestas. En este caso, es muy recomendable que interrumpa el código de cliente y espere antes de volver a intentarlo. Esto le dará sistema Hola algunos toorecover tiempo, aumentar las posibilidades de Hola que se realizará correctamente las solicitudes futuras. Rápidamente volver a intentar su solicitud únicamente prolongará la situación de Hola.
>
>

#### <a name="429"></a>429
Un código de estado `429` se devolverán cuando se ha excedido la cuota Hola número de documentos por índice.

#### <a name="503"></a>503
Un código de estado `503` se devolverá si ninguno de los elementos de hello en solicitud de saludo se indizaron correctamente. Este error significa que Hola sistema está sometido a mucha carga y no se puede procesar su solicitud en este momento.

> [!NOTE]
> En este caso, es muy recomendable que interrumpa el código de cliente y espere antes de volver a intentarlo. Esto le dará sistema Hola algunos toorecover tiempo, aumentar las posibilidades de Hola que se realizará correctamente las solicitudes futuras. Rápidamente volver a intentar su solicitud únicamente prolongará la situación de Hola.
>
>

Para más información sobre las acciones de documentos y las respuestas de éxito o error, consulte [Agregar, actualizar o eliminar documentos](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents). Para más información sobre otros códigos de estado HTTP que se devuelven en caso de error, consulte [Códigos de estado HTTP (Búsqueda de Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).

## <a name="next-steps"></a>Pasos siguientes
Después de rellenar el índice de búsqueda de Azure, estará listo toostart emitir toosearch de las consultas para los documentos. Para más información, vea [Consultas en Búsqueda de Azure](search-query-overview.md) .
