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
# <a name="query-your-azure-search-index-using-hello-rest-api"></a><span data-ttu-id="4e938-103">Consultar el índice de búsqueda de Azure con hello API de REST</span><span class="sxs-lookup"><span data-stu-id="4e938-103">Query your Azure Search index using hello REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="4e938-104">Información general</span><span class="sxs-lookup"><span data-stu-id="4e938-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="4e938-105">Portal</span><span class="sxs-lookup"><span data-stu-id="4e938-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="4e938-106">.NET</span><span class="sxs-lookup"><span data-stu-id="4e938-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="4e938-107">REST</span><span class="sxs-lookup"><span data-stu-id="4e938-107">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="4e938-108">Este artículo muestra cómo tooquery un índice utilizando Hola [API de REST de búsqueda de Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="4e938-108">This article shows you how tooquery an index using hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

<span data-ttu-id="4e938-109">Antes de comenzar este tutorial, debe haber [creado ya un índice de Azure Search](search-what-is-an-index.md) y [haberlo rellenado con datos](search-what-is-data-import.md).</span><span class="sxs-lookup"><span data-stu-id="4e938-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span> <span data-ttu-id="4e938-110">Para información preliminar, vea [Cómo funciona la búsqueda de texto completo en Azure Search](search-lucene-query-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="4e938-110">For background information, see [How full text search works in Azure Search](search-lucene-query-architecture.md).</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="4e938-111">Identificación de la clave de API de consulta del servicio de Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="4e938-111">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="4e938-112">Un componente clave de cada operación de búsqueda contra Hola API de REST de búsqueda de Azure es hello *clave de api* que se ha generado para el servicio de hello ha aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="4e938-112">A key component of every search operation against hello Azure Search REST API is hello *api-key* that was generated for hello service you provisioned.</span></span> <span data-ttu-id="4e938-113">Tener una clave válida establece la confianza, por cada solicitud, entre Hola aplicación enviando Hola solicitud y el servicio de Hola que los controle.</span><span class="sxs-lookup"><span data-stu-id="4e938-113">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="4e938-114">toofind claves de api de su servicio, puede iniciar sesión en toohello [portal de Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="4e938-114">toofind your service's api-keys, you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="4e938-115">Vaya hoja del servicio de búsqueda de Azure tooyour</span><span class="sxs-lookup"><span data-stu-id="4e938-115">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="4e938-116">Haga clic en el icono de "Claves" Hola</span><span class="sxs-lookup"><span data-stu-id="4e938-116">Click hello "Keys" icon</span></span>

<span data-ttu-id="4e938-117">El servicio tiene *claves de administración* y *claves de consulta*.</span><span class="sxs-lookup"><span data-stu-id="4e938-117">Your service has *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="4e938-118">El principal y secundaria *claves de administración* conceder derechos completos tooall operaciones, incluido el servicio de hello capacidad toomanage hello, crear y eliminar índices, los indizadores y orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="4e938-118">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="4e938-119">Existen dos claves para que pueda continuar la clave secundaria de hello toouse si decide tooregenerate Hola primary key y viceversa.</span><span class="sxs-lookup"><span data-stu-id="4e938-119">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="4e938-120">Su *claves de consulta* conceder acceso de solo lectura tooindexes y documentos, y son aplicaciones tooclient normalmente distribuida que emiten solicitudes de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="4e938-120">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="4e938-121">Para fines de Hola de consultar un índice, puede usar una de las claves de consulta.</span><span class="sxs-lookup"><span data-stu-id="4e938-121">For hello purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="4e938-122">Las claves de administración también pueden usarse para las consultas, pero debe usar una clave de consulta en el código de aplicación de manera esto mejor hello [principio de privilegios mínimos](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="4e938-122">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows hello [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="formulate-your-query"></a><span data-ttu-id="4e938-123">Formulación de la consulta</span><span class="sxs-lookup"><span data-stu-id="4e938-123">Formulate your query</span></span>
<span data-ttu-id="4e938-124">Hay dos maneras de[buscar el índice mediante la API de REST de hello](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span><span class="sxs-lookup"><span data-stu-id="4e938-124">There are two ways too[search your index using hello REST API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="4e938-125">Una manera es tooissue una solicitud HTTP POST donde se definen los parámetros de consulta en un objeto JSON en el cuerpo de la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="4e938-125">One way is tooissue an HTTP POST request where your query parameters are defined in a JSON object in hello request body.</span></span> <span data-ttu-id="4e938-126">Hola otra manera es tooissue una solicitud HTTP GET donde se definen los parámetros de consulta de dirección URL de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="4e938-126">hello other way is tooissue an HTTP GET request where your query parameters are defined within hello request URL.</span></span> <span data-ttu-id="4e938-127">POST tiene más [relajado límites](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) en tamaño de Hola de los parámetros de consulta que no son GET.</span><span class="sxs-lookup"><span data-stu-id="4e938-127">POST has more [relaxed limits](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) on hello size of query parameters than GET.</span></span> <span data-ttu-id="4e938-128">Por este motivo, se recomienda usar la solicitud POST a menos que haya circunstancias especiales en las que utilizar la solicitud GET sea más adecuado.</span><span class="sxs-lookup"><span data-stu-id="4e938-128">For this reason, we recommend using POST unless you have special circumstances where using GET would be more convenient.</span></span>

<span data-ttu-id="4e938-129">Para POST y GET, deberá tooprovide el *nombre del servicio*, *nombre del índice*, hello apropiado y *versión de API* (es la versión actual de la API de hello `2016-09-01` en tiempo de Hola sobre la publicación de este documento) en hello URL de solicitud.</span><span class="sxs-lookup"><span data-stu-id="4e938-129">For both POST and GET, you need tooprovide your *service name*, *index name*, and hello proper *API version* (hello current API version is `2016-09-01` at hello time of publishing this document) in hello request URL.</span></span> <span data-ttu-id="4e938-130">Para GET, Hola *cadena de consulta* en hello final de la dirección URL de hello es donde se deben proporcionar parámetros de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e938-130">For GET, hello *query string* at hello end of hello URL is where you provide hello query parameters.</span></span> <span data-ttu-id="4e938-131">Vea a continuación para el formato de dirección URL de hello:</span><span class="sxs-lookup"><span data-stu-id="4e938-131">See below for hello URL format:</span></span>

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

<span data-ttu-id="4e938-132">Hola formato para POST se Hola mismo, pero con solo api-version en parámetros de cadena de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e938-132">hello format for POST is hello same, but with only api-version in hello query string parameters.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="4e938-133">Consultas de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4e938-133">Example Queries</span></span>
<span data-ttu-id="4e938-134">Presentamos algunas consultas de ejemplo en un índice llamado "hoteles".</span><span class="sxs-lookup"><span data-stu-id="4e938-134">Here are a few example queries on an index named "hotels".</span></span> <span data-ttu-id="4e938-135">Estas consultas se muestran en el formato de las solicitudes GET y POST.</span><span class="sxs-lookup"><span data-stu-id="4e938-135">These queries are shown in both GET and POST format.</span></span>

<span data-ttu-id="4e938-136">Buscar todo índice de Hola Hola término 'presupuesto' y devolver solo hello `hotelName` campo:</span><span class="sxs-lookup"><span data-stu-id="4e938-136">Search hello entire index for hello term 'budget' and return only hello `hotelName` field:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

<span data-ttu-id="4e938-137">Aplicar un hoteles de toohello índice toofind de filtro más económico que 150 dólares por la noche y devolver hello `hotelId` y `description`:</span><span class="sxs-lookup"><span data-stu-id="4e938-137">Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello `hotelId` and `description`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

<span data-ttu-id="4e938-138">Todo índice de búsqueda hello, ordenar por un campo específico (`lastRenovationDate`) en orden descendente, toman dos primeros resultados de Hola y mostrar sólo `hotelName` y `lastRenovationDate`:</span><span class="sxs-lookup"><span data-stu-id="4e938-138">Search hello entire index, order by a specific field (`lastRenovationDate`) in descending order, take hello top two results, and show only `hotelName` and `lastRenovationDate`:</span></span>

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

## <a name="submit-your-http-request"></a><span data-ttu-id="4e938-139">Envío de la solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="4e938-139">Submit your HTTP request</span></span>
<span data-ttu-id="4e938-140">Ahora que ha formulado la consulta como parte de la dirección URL de la solicitud HTTP (para GET) o del cuerpo de la solicitud (para POST), puede definir los encabezados de solicitud y enviar la consulta.</span><span class="sxs-lookup"><span data-stu-id="4e938-140">Now that you have formulated your query as part of your HTTP request URL (for GET) or body (for POST), you can define your request headers and submit your query.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="4e938-141">Solicitudes y encabezados de solicitud</span><span class="sxs-lookup"><span data-stu-id="4e938-141">Request and Request Headers</span></span>
<span data-ttu-id="4e938-142">Debe definir dos encabezados de solicitud para GET o tres para POST:</span><span class="sxs-lookup"><span data-stu-id="4e938-142">You must define two request headers for GET, or three for POST:</span></span>

1. <span data-ttu-id="4e938-143">Hola `api-key` encabezado debe establecerse toohello clave de consulta que encontró en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="4e938-143">hello `api-key` header must be set toohello query key you found in step I above.</span></span> <span data-ttu-id="4e938-144">También puede usar una clave de administración como hello `api-key` encabezado, pero se recomienda usar una clave de consulta como exclusivamente concede acceso de solo lectura tooindexes y documentos.</span><span class="sxs-lookup"><span data-stu-id="4e938-144">You can also use an admin key as hello `api-key` header, but it is recommended that you use a query key as it exclusively grants read-only access tooindexes and documents.</span></span>
2. <span data-ttu-id="4e938-145">Hola `Accept` encabezado debe establecerse demasiado`application/json`.</span><span class="sxs-lookup"><span data-stu-id="4e938-145">hello `Accept` header must be set too`application/json`.</span></span>
3. <span data-ttu-id="4e938-146">Para registrar sólo Hola `Content-Type` encabezado también debe estar establecido demasiado`application/json`.</span><span class="sxs-lookup"><span data-stu-id="4e938-146">For POST only, hello `Content-Type` header should also be set too`application/json`.</span></span>

<span data-ttu-id="4e938-147">Vea a continuación un HTTP GET solicitud toosearch Hola "hoteles" índice mediante Hola API de REST de búsqueda de Azure, mediante una consulta simple que se busca Hola término "motel":</span><span class="sxs-lookup"><span data-stu-id="4e938-147">See below for an HTTP GET request toosearch hello "hotels" index using hello Azure Search REST API, using a simple query that searches for hello term "motel":</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

<span data-ttu-id="4e938-148">Aquí es Hola misma consulta de ejemplo, esta vez utilizando HTTP POST:</span><span class="sxs-lookup"><span data-stu-id="4e938-148">Here is hello same example query, this time using HTTP POST:</span></span>

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

<span data-ttu-id="4e938-149">Una solicitud de consulta correcta producirá un código de estado `200 OK` y resultados de la búsqueda de Hola se devuelven como JSON en el cuerpo de respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e938-149">A successful query request will result in a Status Code of `200 OK` and hello search results are returned as JSON in hello response body.</span></span> <span data-ttu-id="4e938-150">Aquí es qué hello como resultado de hello por encima de la consulta tenga el aspecto, suponiendo que el índice de hoteles"Hola" se rellena con datos de ejemplo de Hola en [Hola de importación de datos en búsqueda de Azure con API de REST](search-import-data-rest-api.md) (tenga en cuenta que Hola JSON se ha formateado para mayor claridad).</span><span class="sxs-lookup"><span data-stu-id="4e938-150">Here is what hello results for hello above query look like, assuming hello "hotels" index is populated with hello sample data in [Data Import in Azure Search using hello REST API](search-import-data-rest-api.md) (note that hello JSON has been formatted for clarity).</span></span>

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

<span data-ttu-id="4e938-151">toolearn más información, visite sección de "Respuesta" hello de [buscar documentos](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span><span class="sxs-lookup"><span data-stu-id="4e938-151">toolearn more, please visit hello "Response" section of [Search Documents](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="4e938-152">Para más información sobre otros códigos de estado HTTP que se devuelven en caso de error, consulte [Códigos de estado HTTP (Búsqueda de Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span><span class="sxs-lookup"><span data-stu-id="4e938-152">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>
