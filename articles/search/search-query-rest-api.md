---
title: "Consulta de un índice (API de REST - Azure Search) | Microsoft Docs"
description: "Cree una consulta de búsqueda en Búsqueda de Azure y use los parámetros de búsqueda para filtrar y ordenar los resultados de búsqueda."
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
ms.openlocfilehash: 49062bec233ad35cd457f9665fa94c1855343582
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="query-your-azure-search-index-using-the-rest-api"></a><span data-ttu-id="acebd-103">Realización de una consulta al índice de Búsqueda de Azure con la API de REST</span><span class="sxs-lookup"><span data-stu-id="acebd-103">Query your Azure Search index using the REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="acebd-104">Información general</span><span class="sxs-lookup"><span data-stu-id="acebd-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="acebd-105">Portal</span><span class="sxs-lookup"><span data-stu-id="acebd-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="acebd-106">.NET</span><span class="sxs-lookup"><span data-stu-id="acebd-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="acebd-107">REST</span><span class="sxs-lookup"><span data-stu-id="acebd-107">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="acebd-108">Este artículo muestra cómo realizar consultas en un índice con la [API de REST de Azure Search](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="acebd-108">This article shows you how to query an index using the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

<span data-ttu-id="acebd-109">Antes de comenzar este tutorial, debe haber [creado ya un índice de Azure Search](search-what-is-an-index.md) y [haberlo rellenado con datos](search-what-is-data-import.md).</span><span class="sxs-lookup"><span data-stu-id="acebd-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span> <span data-ttu-id="acebd-110">Para información preliminar, vea [Cómo funciona la búsqueda de texto completo en Azure Search](search-lucene-query-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="acebd-110">For background information, see [How full text search works in Azure Search](search-lucene-query-architecture.md).</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="acebd-111">Identificación de la clave de API de consulta del servicio de Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="acebd-111">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="acebd-112">Un componente clave de cada operación de búsqueda en la API de REST de Búsqueda de Azure es la *clave de API* que se generó para el servicio que ha aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="acebd-112">A key component of every search operation against the Azure Search REST API is the *api-key* that was generated for the service you provisioned.</span></span> <span data-ttu-id="acebd-113">Tener una clave válida genera la confianza, solicitud a solicitud, entre la aplicación que envía la solicitud y el servicio que se encarga de ella.</span><span class="sxs-lookup"><span data-stu-id="acebd-113">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="acebd-114">Para buscar las claves de API del servicio, puede iniciar sesión en [Azure Portal](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="acebd-114">To find your service's api-keys, you can sign in to the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="acebd-115">Vaya a la hoja de servicio de Azure Search</span><span class="sxs-lookup"><span data-stu-id="acebd-115">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="acebd-116">Haga clic en el icono "Claves"</span><span class="sxs-lookup"><span data-stu-id="acebd-116">Click the "Keys" icon</span></span>

<span data-ttu-id="acebd-117">El servicio tiene *claves de administración* y *claves de consulta*.</span><span class="sxs-lookup"><span data-stu-id="acebd-117">Your service has *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="acebd-118">Sus *claves de administración* principal y secundaria permiten conceder derechos completos para todas las operaciones, incluida la capacidad para administrar el servicio, crear y eliminar índices, indexadores y orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="acebd-118">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="acebd-119">Existen dos claves, de forma que puede usar la clave secundaria si decide volver a generar la clave principal y viceversa.</span><span class="sxs-lookup"><span data-stu-id="acebd-119">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="acebd-120">Las *claves de consulta* conceden acceso de solo lectura a índices y documentos y normalmente se distribuyen entre las aplicaciones cliente que emiten solicitudes de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="acebd-120">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="acebd-121">Para consultar un índice, puede utilizar una de las claves de consulta.</span><span class="sxs-lookup"><span data-stu-id="acebd-121">For the purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="acebd-122">Las claves de administración también se pueden utilizar para las consultas, pero debe utilizar una clave de consulta en el código de aplicación ya que esto se adapta mejor al [principio de privilegios mínimos](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="acebd-122">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows the [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="formulate-your-query"></a><span data-ttu-id="acebd-123">Formulación de la consulta</span><span class="sxs-lookup"><span data-stu-id="acebd-123">Formulate your query</span></span>
<span data-ttu-id="acebd-124">Hay dos maneras de [realizar búsquedas en el índice mediante la API de REST](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span><span class="sxs-lookup"><span data-stu-id="acebd-124">There are two ways to [search your index using the REST API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="acebd-125">Una de ellas es emitir una solicitud HTTP POST en la que los parámetros de consulta se definen en un objeto JSON del cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="acebd-125">One way is to issue an HTTP POST request where your query parameters are defined in a JSON object in the request body.</span></span> <span data-ttu-id="acebd-126">La otra es emitir una solicitud HTTP GET en la que los parámetros de la consulta se definen en la dirección URL de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="acebd-126">The other way is to issue an HTTP GET request where your query parameters are defined within the request URL.</span></span> <span data-ttu-id="acebd-127">POST tiene unos [límites más flexibles](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) en relación con el tamaño de los parámetros de la consulta que GET.</span><span class="sxs-lookup"><span data-stu-id="acebd-127">POST has more [relaxed limits](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) on the size of query parameters than GET.</span></span> <span data-ttu-id="acebd-128">Por este motivo, se recomienda usar la solicitud POST a menos que haya circunstancias especiales en las que utilizar la solicitud GET sea más adecuado.</span><span class="sxs-lookup"><span data-stu-id="acebd-128">For this reason, we recommend using POST unless you have special circumstances where using GET would be more convenient.</span></span>

<span data-ttu-id="acebd-129">Tanto para la solicitud POST como para la GET, deberá proporcionar el *nombre del servicio*, el *nombre del índice*, así como la *versión adecuada de la API* (la versión actual de la API es `2016-09-01` en el momento de publicar este documento) en la URL de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="acebd-129">For both POST and GET, you need to provide your *service name*, *index name*, and the proper *API version* (the current API version is `2016-09-01` at the time of publishing this document) in the request URL.</span></span> <span data-ttu-id="acebd-130">En el caso de GET, la *cadena de consulta* del final de la dirección URL es donde se proporcionar los parámetros de la consulta.</span><span class="sxs-lookup"><span data-stu-id="acebd-130">For GET, the *query string* at the end of the URL is where you provide the query parameters.</span></span> <span data-ttu-id="acebd-131">Consulte a continuación el formato de dirección URL:</span><span class="sxs-lookup"><span data-stu-id="acebd-131">See below for the URL format:</span></span>

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

<span data-ttu-id="acebd-132">El formato de la solicitud POST es el mismo, pero solo con la versión de API en los parámetros de la cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="acebd-132">The format for POST is the same, but with only api-version in the query string parameters.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="acebd-133">Consultas de ejemplo</span><span class="sxs-lookup"><span data-stu-id="acebd-133">Example Queries</span></span>
<span data-ttu-id="acebd-134">Presentamos algunas consultas de ejemplo en un índice llamado "hoteles".</span><span class="sxs-lookup"><span data-stu-id="acebd-134">Here are a few example queries on an index named "hotels".</span></span> <span data-ttu-id="acebd-135">Estas consultas se muestran en el formato de las solicitudes GET y POST.</span><span class="sxs-lookup"><span data-stu-id="acebd-135">These queries are shown in both GET and POST format.</span></span>

<span data-ttu-id="acebd-136">Busque en todo el índice el término "presupuesto" y devuelva solo el campo `hotelName`:</span><span class="sxs-lookup"><span data-stu-id="acebd-136">Search the entire index for the term 'budget' and return only the `hotelName` field:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

<span data-ttu-id="acebd-137">Aplique un filtro al índice para buscar hoteles con una tarifa inferior a 150 dólares por noche, y devolver `hotelId` y `description`:</span><span class="sxs-lookup"><span data-stu-id="acebd-137">Apply a filter to the index to find hotels cheaper than $150 per night, and return the `hotelId` and `description`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

<span data-ttu-id="acebd-138">Busque en todo el índice, ordene por un campo específico (`lastRenovationDate`) en orden descendente, tome los dos primeros resultados y muestre solo `hotelName` y `lastRenovationDate`:</span><span class="sxs-lookup"><span data-stu-id="acebd-138">Search the entire index, order by a specific field (`lastRenovationDate`) in descending order, take the top two results, and show only `hotelName` and `lastRenovationDate`:</span></span>

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

## <a name="submit-your-http-request"></a><span data-ttu-id="acebd-139">Envío de la solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="acebd-139">Submit your HTTP request</span></span>
<span data-ttu-id="acebd-140">Ahora que ha formulado la consulta como parte de la dirección URL de la solicitud HTTP (para GET) o del cuerpo de la solicitud (para POST), puede definir los encabezados de solicitud y enviar la consulta.</span><span class="sxs-lookup"><span data-stu-id="acebd-140">Now that you have formulated your query as part of your HTTP request URL (for GET) or body (for POST), you can define your request headers and submit your query.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="acebd-141">Solicitudes y encabezados de solicitud</span><span class="sxs-lookup"><span data-stu-id="acebd-141">Request and Request Headers</span></span>
<span data-ttu-id="acebd-142">Debe definir dos encabezados de solicitud para GET o tres para POST:</span><span class="sxs-lookup"><span data-stu-id="acebd-142">You must define two request headers for GET, or three for POST:</span></span>

1. <span data-ttu-id="acebd-143">El encabezado `api-key` se debe establecer en la clave de consulta que encontró anteriormente en el paso I.</span><span class="sxs-lookup"><span data-stu-id="acebd-143">The `api-key` header must be set to the query key you found in step I above.</span></span> <span data-ttu-id="acebd-144">También puede usar una clave de administración como encabezado `api-key`, pero se recomienda usar una clave de consulta, ya que esta concede acceso de solo lectura a los índices y documentos de forma exclusiva.</span><span class="sxs-lookup"><span data-stu-id="acebd-144">You can also use an admin key as the `api-key` header, but it is recommended that you use a query key as it exclusively grants read-only access to indexes and documents.</span></span>
2. <span data-ttu-id="acebd-145">El encabezado `Accept` debe establecerse en `application/json`.</span><span class="sxs-lookup"><span data-stu-id="acebd-145">The `Accept` header must be set to `application/json`.</span></span>
3. <span data-ttu-id="acebd-146">Solo para POST, el encabezado `Content-Type` debe establecerse también en `application/json`.</span><span class="sxs-lookup"><span data-stu-id="acebd-146">For POST only, the `Content-Type` header should also be set to `application/json`.</span></span>

<span data-ttu-id="acebd-147">Consulte a continuación una solicitud HTTP GET creada para buscar en el índice "hotels" mediante la API de REST de Azure Search con una consulta sencilla que busca el término "motel":</span><span class="sxs-lookup"><span data-stu-id="acebd-147">See below for an HTTP GET request to search the "hotels" index using the Azure Search REST API, using a simple query that searches for the term "motel":</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

<span data-ttu-id="acebd-148">Aquí aparece la misma consulta de ejemplo, pero esta vez utilizando HTTP POST:</span><span class="sxs-lookup"><span data-stu-id="acebd-148">Here is the same example query, this time using HTTP POST:</span></span>

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

<span data-ttu-id="acebd-149">Una solicitud de consulta correcta dará como resultado un código de estado de `200 OK` y los resultados de la búsqueda se devuelven como JSON en el cuerpo de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="acebd-149">A successful query request will result in a Status Code of `200 OK` and the search results are returned as JSON in the response body.</span></span> <span data-ttu-id="acebd-150">Aquí se muestra el aspecto de los resultados de la consulta anterior, suponiendo que el índice "hoteles" se ha rellenado con los datos de ejemplo de [Importación de datos en Búsqueda de Azure con la API de REST](search-import-data-rest-api.md) (tenga en cuenta que se ha aplicado formato a JSON para mayor claridad).</span><span class="sxs-lookup"><span data-stu-id="acebd-150">Here is what the results for the above query look like, assuming the "hotels" index is populated with the sample data in [Data Import in Azure Search using the REST API](search-import-data-rest-api.md) (note that the JSON has been formatted for clarity).</span></span>

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

<span data-ttu-id="acebd-151">Para más información, visite la sección "Respuesta" de [Buscar documentos](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span><span class="sxs-lookup"><span data-stu-id="acebd-151">To learn more, please visit the "Response" section of [Search Documents](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="acebd-152">Para más información sobre otros códigos de estado HTTP que se devuelven en caso de error, consulte [Códigos de estado HTTP (Búsqueda de Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span><span class="sxs-lookup"><span data-stu-id="acebd-152">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>
