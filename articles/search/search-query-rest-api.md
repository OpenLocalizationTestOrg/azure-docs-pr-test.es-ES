---
title: "aaa \"consultar un índice (API de REST - búsqueda de Azure) | Documentos de Microsoft\""
description: "Crear una consulta de búsqueda en búsqueda de Azure y usar resultados de búsqueda de toofilter y de ordenación de los parámetros de búsqueda."
services: search
documentationcenter: 
manager: jhubbard
author: ashmaka
ms.assetid: 8b3ca890-2f5f-44b6-a140-6cb676fc2c9c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/12/2017
ms.author: ashmaka
ms.openlocfilehash: 2f12238b8f4b045f536489cfc8766fb68307bbe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-rest-api"></a>Consultar el índice de búsqueda de Azure con hello API de REST
> [!div class="op_single_selector"]
>
> * [Información general](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
>
>

Este artículo muestra cómo tooquery un índice utilizando Hola [API de REST de búsqueda de Azure](https://docs.microsoft.com/rest/api/searchservice/).

Antes de comenzar este tutorial, debe haber [creado ya un índice de Azure Search](search-what-is-an-index.md) y [haberlo rellenado con datos](search-what-is-data-import.md). Para información preliminar, vea [Cómo funciona la búsqueda de texto completo en Azure Search](search-lucene-query-architecture.md).

## <a name="identify-your-azure-search-services-query-api-key"></a>Identificación de la clave de API de consulta del servicio de Búsqueda de Azure
Un componente clave de cada operación de búsqueda contra Hola API de REST de búsqueda de Azure es hello *clave de api* que se ha generado para el servicio de hello ha aprovisionado. Tener una clave válida establece la confianza, por cada solicitud, entre Hola aplicación enviando Hola solicitud y el servicio de Hola que los controle.

1. toofind claves de api de su servicio, puede iniciar sesión en toohello [portal de Azure](https://portal.azure.com/)
2. Vaya hoja del servicio de búsqueda de Azure tooyour
3. Haga clic en el icono de "Claves" Hola

El servicio tiene *claves de administración* y *claves de consulta*.

* El principal y secundaria *claves de administración* conceder derechos completos tooall operaciones, incluido el servicio de hello capacidad toomanage hello, crear y eliminar índices, los indizadores y orígenes de datos. Existen dos claves para que pueda continuar la clave secundaria de hello toouse si decide tooregenerate Hola primary key y viceversa.
* Su *claves de consulta* conceder acceso de solo lectura tooindexes y documentos, y son aplicaciones tooclient normalmente distribuida que emiten solicitudes de búsqueda.

Para fines de Hola de consultar un índice, puede usar una de las claves de consulta. Las claves de administración también pueden usarse para las consultas, pero debe usar una clave de consulta en el código de aplicación de manera esto mejor hello [principio de privilegios mínimos](https://en.wikipedia.org/wiki/Principle_of_least_privilege).

## <a name="formulate-your-query"></a>Formulación de la consulta
Hay dos maneras de[buscar el índice mediante la API de REST de hello](https://docs.microsoft.com/rest/api/searchservice/Search-Documents). Una manera es tooissue una solicitud HTTP POST donde se definen los parámetros de consulta en un objeto JSON en el cuerpo de la solicitud de saludo. Hola otra manera es tooissue una solicitud HTTP GET donde se definen los parámetros de consulta de dirección URL de solicitud de saludo. POST tiene más [relajado límites](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) en tamaño de Hola de los parámetros de consulta que no son GET. Por este motivo, se recomienda usar la solicitud POST a menos que haya circunstancias especiales en las que utilizar la solicitud GET sea más adecuado.

Para POST y GET, deberá tooprovide el *nombre del servicio*, *nombre del índice*, hello apropiado y *versión de API* (es la versión actual de la API de hello `2016-09-01` en tiempo de Hola sobre la publicación de este documento) en hello URL de solicitud. Para GET, Hola *cadena de consulta* en hello final de la dirección URL de hello es donde se deben proporcionar parámetros de consulta de Hola. Vea a continuación para el formato de dirección URL de hello:

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

Hola formato para POST se Hola mismo, pero con solo api-version en parámetros de cadena de consulta de Hola.

#### <a name="example-queries"></a>Consultas de ejemplo
Presentamos algunas consultas de ejemplo en un índice llamado "hoteles". Estas consultas se muestran en el formato de las solicitudes GET y POST.

Buscar todo índice de Hola Hola término 'presupuesto' y devolver solo hello `hotelName` campo:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

Aplicar un hoteles de toohello índice toofind de filtro más económico que 150 dólares por la noche y devolver hello `hotelId` y `description`:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

Todo índice de búsqueda hello, ordenar por un campo específico (`lastRenovationDate`) en orden descendente, toman dos primeros resultados de Hola y mostrar sólo `hotelName` y `lastRenovationDate`:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$top=2&$orderby=lastRenovationDate desc&$select=hotelName,lastRenovationDate&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "orderby": "lastRenovationDate desc",
    "select": "hotelName,lastRenovationDate",
    "top": 2
}
```

## <a name="submit-your-http-request"></a>Envío de la solicitud HTTP
Ahora que ha formulado la consulta como parte de la dirección URL de la solicitud HTTP (para GET) o del cuerpo de la solicitud (para POST), puede definir los encabezados de solicitud y enviar la consulta.

#### <a name="request-and-request-headers"></a>Solicitudes y encabezados de solicitud
Debe definir dos encabezados de solicitud para GET o tres para POST:

1. Hola `api-key` encabezado debe establecerse toohello clave de consulta que encontró en el paso anterior. También puede usar una clave de administración como hello `api-key` encabezado, pero se recomienda usar una clave de consulta como exclusivamente concede acceso de solo lectura tooindexes y documentos.
2. Hola `Accept` encabezado debe establecerse demasiado`application/json`.
3. Para registrar sólo Hola `Content-Type` encabezado también debe estar establecido demasiado`application/json`.

Vea a continuación un HTTP GET solicitud toosearch Hola "hoteles" índice mediante Hola API de REST de búsqueda de Azure, mediante una consulta simple que se busca Hola término "motel":

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

Aquí es Hola misma consulta de ejemplo, esta vez utilizando HTTP POST:

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

Una solicitud de consulta correcta producirá un código de estado `200 OK` y resultados de la búsqueda de Hola se devuelven como JSON en el cuerpo de respuesta de Hola. Aquí es qué hello como resultado de hello por encima de la consulta tenga el aspecto, suponiendo que el índice de hoteles"Hola" se rellena con datos de ejemplo de Hola en [Hola de importación de datos en búsqueda de Azure con API de REST](search-import-data-rest-api.md) (tenga en cuenta que Hola JSON se ha formateado para mayor claridad).

```JSON
{
    "value": [
        {
            "@search.score": 0.59600675,
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags":["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": {
                "type": "Point",
                "coordinates": [-122.131577, 49.678581],
                "crs": {
                    "type":"name",
                    "properties": {
                        "name": "EPSG:4326"
                    }
                }
            }
        }
    ]
}
```

toolearn más información, visite sección de "Respuesta" hello de [buscar documentos](https://docs.microsoft.com/rest/api/searchservice/Search-Documents). Para más información sobre otros códigos de estado HTTP que se devuelven en caso de error, consulte [Códigos de estado HTTP (Búsqueda de Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).
