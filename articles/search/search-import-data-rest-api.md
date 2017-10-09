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
# <a name="upload-data-tooazure-search-using-hello-rest-api"></a><span data-ttu-id="220ff-103">Carga datos tooAzure búsqueda mediante Hola API de REST</span><span class="sxs-lookup"><span data-stu-id="220ff-103">Upload data tooAzure Search using hello REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="220ff-104">Información general</span><span class="sxs-lookup"><span data-stu-id="220ff-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="220ff-105">.NET</span><span class="sxs-lookup"><span data-stu-id="220ff-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="220ff-106">REST</span><span class="sxs-lookup"><span data-stu-id="220ff-106">REST</span></span>](search-import-data-rest-api.md)
>
>

<span data-ttu-id="220ff-107">En este artículo le mostrará cómo hello toouse [API de REST de búsqueda de Azure](https://docs.microsoft.com/rest/api/searchservice/) tooimport datos en un índice de búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="220ff-107">This article will show you how toouse hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/) tooimport data into an Azure Search index.</span></span>

<span data-ttu-id="220ff-108">Antes de comenzar este tutorial, debe haber [creado ya un índice de Búsqueda de Azure](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="220ff-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span>

<span data-ttu-id="220ff-109">En documentos de toopush de orden en el índice mediante API de REST de hello, emitirá el punto de conexión de dirección URL de HTTP POST solicitud tooyour de un índice.</span><span class="sxs-lookup"><span data-stu-id="220ff-109">In order toopush documents into your index using hello REST API, you will issue an HTTP POST request tooyour index's URL endpoint.</span></span> <span data-ttu-id="220ff-110">cuerpo de Hola de hello solicitud HTTP cuerpo es un objeto JSON que contiene documentos de hello toobe agregado, modificado o eliminado.</span><span class="sxs-lookup"><span data-stu-id="220ff-110">hello body of hello HTTP request body is a JSON object containing hello documents toobe added, modified, or deleted.</span></span>

## <a name="identify-your-azure-search-services-admin-api-key"></a><span data-ttu-id="220ff-111">Identificación de la clave de API de administración del servicio de Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="220ff-111">Identify your Azure Search service's admin api-key</span></span>
<span data-ttu-id="220ff-112">Cuando se emite solicitudes HTTP en su servicio mediante las API de REST, hello *cada* solicitud de API debe incluir Hola clave de api que se generó Hola aprovisionar el servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="220ff-112">When issuing HTTP requests against your service using hello REST API, *each* API request must include hello api-key that was generated for hello Search service you provisioned.</span></span> <span data-ttu-id="220ff-113">Tener una clave válida establece la confianza, por cada solicitud, entre Hola aplicación enviando Hola solicitud y el servicio de Hola que los controle.</span><span class="sxs-lookup"><span data-stu-id="220ff-113">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="220ff-114">toofind claves de api de su servicio, puede iniciar sesión en toohello [portal de Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="220ff-114">toofind your service's api-keys, you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="220ff-115">Vaya hoja del servicio de búsqueda de Azure tooyour</span><span class="sxs-lookup"><span data-stu-id="220ff-115">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="220ff-116">Haga clic en hello icono "Claves"</span><span class="sxs-lookup"><span data-stu-id="220ff-116">Click on hello "Keys" icon</span></span>

<span data-ttu-id="220ff-117">El servicio tendrá *claves de administración* y *claves de consulta*.</span><span class="sxs-lookup"><span data-stu-id="220ff-117">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="220ff-118">El principal y secundaria *claves de administración* conceder derechos completos tooall operaciones, incluido el servicio de hello capacidad toomanage hello, crear y eliminar índices, los indizadores y orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="220ff-118">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="220ff-119">Existen dos claves para que pueda continuar la clave secundaria de hello toouse si decide tooregenerate Hola primary key y viceversa.</span><span class="sxs-lookup"><span data-stu-id="220ff-119">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="220ff-120">Su *claves de consulta* conceder acceso de solo lectura tooindexes y documentos, y son aplicaciones tooclient normalmente distribuida que emiten solicitudes de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="220ff-120">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="220ff-121">Por motivos de saludo de la importación de datos en un índice, puede usar su clave de administración principal o secundaria.</span><span class="sxs-lookup"><span data-stu-id="220ff-121">For hello purposes of importing data into an index, you can use either your primary or secondary admin key.</span></span>

## <a name="decide-which-indexing-action-toouse"></a><span data-ttu-id="220ff-122">Decidir qué indización toouse de acción</span><span class="sxs-lookup"><span data-stu-id="220ff-122">Decide which indexing action toouse</span></span>
<span data-ttu-id="220ff-123">Cuando se utiliza la API de REST de Hola, se van a emitir solicitudes HTTP POST con la dirección URL del extremo del índice JSON solicitud cuerpos tooyour búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="220ff-123">When using hello REST API, you will issue HTTP POST requests with JSON request bodies tooyour Azure Search index's endpoint URL.</span></span> <span data-ttu-id="220ff-124">objeto JSON de Hello en el cuerpo de la solicitud HTTP contiene una matriz JSON con el nombre "value" que contiene los objetos JSON que representa los documentos que le gustaría tooadd tooyour índice, actualizar o eliminar.</span><span class="sxs-lookup"><span data-stu-id="220ff-124">hello JSON object in your HTTP request body will contain a single JSON array named "value" containing JSON objects representing documents you would like tooadd tooyour index, update, or delete.</span></span>

<span data-ttu-id="220ff-125">Cada objeto JSON de matriz de "value" hello representa un toobe documento indizado.</span><span class="sxs-lookup"><span data-stu-id="220ff-125">Each JSON object in hello "value" array represents a document toobe indexed.</span></span> <span data-ttu-id="220ff-126">Cada uno de estos objetos contiene la clave del documento de Hola y especifica la acción de indización de hello deseado (carga, merge, delete, etcetera).</span><span class="sxs-lookup"><span data-stu-id="220ff-126">Each of these objects contains hello document's key and specifies hello desired indexing action (upload, merge, delete, etc).</span></span> <span data-ttu-id="220ff-127">Dependiendo de cuál de hello debajo de acciones que elija, se deben incluidos para cada documento solo algunos de los campos:</span><span class="sxs-lookup"><span data-stu-id="220ff-127">Depending on which of hello below actions you choose, only certain fields must be included for each document:</span></span>

| @search.action | <span data-ttu-id="220ff-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="220ff-128">Description</span></span> | <span data-ttu-id="220ff-129">Campos necesarios para cada documento</span><span class="sxs-lookup"><span data-stu-id="220ff-129">Necessary fields for each document</span></span> | <span data-ttu-id="220ff-130">Notas</span><span class="sxs-lookup"><span data-stu-id="220ff-130">Notes</span></span> |
| --- | --- | --- | --- |
| `upload` |<span data-ttu-id="220ff-131">Un `upload` acción es similar tooan "upsert" donde se insertan si es nuevo y actualiza/reemplaza si existe el documento de Hola.</span><span class="sxs-lookup"><span data-stu-id="220ff-131">An `upload` action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="220ff-132">clave, además de cualquier otro campo que se va a toodefine</span><span class="sxs-lookup"><span data-stu-id="220ff-132">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="220ff-133">Al actualizar o reemplazar un documento existente, cualquier campo que no se especifica en la solicitud de hello tendrá su campo establecido demasiado`null`.</span><span class="sxs-lookup"><span data-stu-id="220ff-133">When updating/replacing an existing document, any field that is not specified in hello request will have its field set too`null`.</span></span> <span data-ttu-id="220ff-134">Esto sucede incluso si el campo Hola anteriormente se estableció un valor no null tooa.</span><span class="sxs-lookup"><span data-stu-id="220ff-134">This occurs even when hello field was previously set tooa non-null value.</span></span> |
| `merge` |<span data-ttu-id="220ff-135">Las actualizaciones existentes de documentos con hello especifican campos.</span><span class="sxs-lookup"><span data-stu-id="220ff-135">Updates an existing document with hello specified fields.</span></span> <span data-ttu-id="220ff-136">Si el documento de hello no existe en el índice de hello, se producirá un error en la mezcla de Hola.</span><span class="sxs-lookup"><span data-stu-id="220ff-136">If hello document does not exist in hello index, hello merge will fail.</span></span> |<span data-ttu-id="220ff-137">clave, además de cualquier otro campo que se va a toodefine</span><span class="sxs-lookup"><span data-stu-id="220ff-137">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="220ff-138">Cualquier campo que se especifica en una combinación reemplazará el campo existente de hello en el documento de Hola.</span><span class="sxs-lookup"><span data-stu-id="220ff-138">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="220ff-139">Aquí se incluyen los campos de tipo `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="220ff-139">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="220ff-140">Por ejemplo, si hello documento contiene un campo `tags` con valor `["budget"]` y ejecutar una combinación con el valor `["economy", "pool"]` para `tags`, Hola valor final de hello `tags` campo será `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="220ff-140">For example, if hello document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, hello final value of hello `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="220ff-141">No será `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="220ff-141">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `mergeOrUpload` |<span data-ttu-id="220ff-142">Esta acción se comporta como `merge` si un documento con hello clave dada ya existe en el índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="220ff-142">This action behaves like `merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="220ff-143">Si el documento de hello no existe, se comporta como `upload` con un nuevo documento.</span><span class="sxs-lookup"><span data-stu-id="220ff-143">If hello document does not exist, it behaves like `upload` with a new document.</span></span> |<span data-ttu-id="220ff-144">clave, además de cualquier otro campo que se va a toodefine</span><span class="sxs-lookup"><span data-stu-id="220ff-144">key, plus any other fields you wish toodefine</span></span> |- |
| `delete` |<span data-ttu-id="220ff-145">Quita del documento especificado Hola Hola índice de.</span><span class="sxs-lookup"><span data-stu-id="220ff-145">Removes hello specified document from hello index.</span></span> |<span data-ttu-id="220ff-146">solo la clave</span><span class="sxs-lookup"><span data-stu-id="220ff-146">key only</span></span> |<span data-ttu-id="220ff-147">Los campos que especifique aparte de campo de clave de Hola se pasará por alto.</span><span class="sxs-lookup"><span data-stu-id="220ff-147">Any fields you specify other than hello key field will be ignored.</span></span> <span data-ttu-id="220ff-148">Si desea tooremove un campo individual de un documento, use `merge` en su lugar y simplemente establezca explícitamente campo hello toonull.</span><span class="sxs-lookup"><span data-stu-id="220ff-148">If you want tooremove an individual field from a document, use `merge` instead and simply set hello field explicitly toonull.</span></span> |

## <a name="construct-your-http-request-and-request-body"></a><span data-ttu-id="220ff-149">Construcción de la solicitud HTTP y el cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="220ff-149">Construct your HTTP request and request body</span></span>
<span data-ttu-id="220ff-150">Ahora que ha recopilado los valores de campo necesarios de Hola para las acciones de índice, es solicitudes HTTP real de tooconstruct listo hello y JSON solicitar cuerpo tooimport los datos.</span><span class="sxs-lookup"><span data-stu-id="220ff-150">Now that you have gathered hello necessary field values for your index actions, you are ready tooconstruct hello actual HTTP request and JSON request body tooimport your data.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="220ff-151">Solicitudes y encabezados de solicitud</span><span class="sxs-lookup"><span data-stu-id="220ff-151">Request and Request Headers</span></span>
<span data-ttu-id="220ff-152">En dirección URL de hello, deberá tooprovide el nombre del servicio, el nombre del índice ("hoteles" en este caso), así como la versión adecuada de API de hello (es la versión actual de la API de hello `2016-09-01` en tiempo de hello sobre la publicación de este documento).</span><span class="sxs-lookup"><span data-stu-id="220ff-152">In hello URL, you will need tooprovide your service name, index name ("hotels" in this case), as well as hello proper API version (hello current API version is `2016-09-01` at hello time of publishing this document).</span></span> <span data-ttu-id="220ff-153">Necesitará hello toodefine `Content-Type` y `api-key` encabezados de solicitud.</span><span class="sxs-lookup"><span data-stu-id="220ff-153">You will need toodefine hello `Content-Type` and `api-key` request headers.</span></span> <span data-ttu-id="220ff-154">Para Hola este último, use una de las claves de administración de su servicio.</span><span class="sxs-lookup"><span data-stu-id="220ff-154">For hello latter, use one of your service's admin keys.</span></span>

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a><span data-ttu-id="220ff-155">Cuerpo de la solicitud</span><span class="sxs-lookup"><span data-stu-id="220ff-155">Request Body</span></span>
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

<span data-ttu-id="220ff-156">En este caso, estamos usando `upload`, `mergeOrUpload` y `delete` como acciones de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="220ff-156">In this case, we are using `upload`, `mergeOrUpload`, and `delete` as our search actions.</span></span>

<span data-ttu-id="220ff-157">Se supone que este índice "hoteles" de ejemplo ya está relleno con varios documentos.</span><span class="sxs-lookup"><span data-stu-id="220ff-157">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="220ff-158">Tenga en cuenta cómo no se tenía toospecify todos los campos de documento posibles Hola al usar `mergeOrUpload` y cómo se puede especificar sólo clave de documento de hello (`hotelId`) cuando se usa `delete`.</span><span class="sxs-lookup"><span data-stu-id="220ff-158">Note how we did not have toospecify all hello possible document fields when using `mergeOrUpload` and how we only specified hello document key (`hotelId`) when using `delete`.</span></span>

<span data-ttu-id="220ff-159">Además, tenga en cuenta que solo pueden incluir documentos too1000 (o 16 MB) en una sola solicitud de indización.</span><span class="sxs-lookup"><span data-stu-id="220ff-159">Also, note that you can only include up too1000 documents (or 16 MB) in a single indexing request.</span></span>

## <a name="understand-your-http-response-code"></a><span data-ttu-id="220ff-160">Descripción del código de respuesta HTTP</span><span class="sxs-lookup"><span data-stu-id="220ff-160">Understand your HTTP response code</span></span>
#### <a name="200"></a><span data-ttu-id="220ff-161">200</span><span class="sxs-lookup"><span data-stu-id="220ff-161">200</span></span>
<span data-ttu-id="220ff-162">Después de enviar una solicitud de indexación correcta recibirá una respuesta HTTP con código de estado de `200 OK`.</span><span class="sxs-lookup"><span data-stu-id="220ff-162">After submitting a successful indexing request you will receive an HTTP response with status code of `200 OK`.</span></span> <span data-ttu-id="220ff-163">Hola cuerpo JSON de hello respuesta HTTP será la siguiente:</span><span class="sxs-lookup"><span data-stu-id="220ff-163">hello JSON body of hello HTTP response will be as follows:</span></span>

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

#### <a name="207"></a><span data-ttu-id="220ff-164">207</span><span class="sxs-lookup"><span data-stu-id="220ff-164">207</span></span>
<span data-ttu-id="220ff-165">Se devolverá un código de estado de `207` solo con que un elemento no se indexe correctamente.</span><span class="sxs-lookup"><span data-stu-id="220ff-165">A status code of `207` will be returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="220ff-166">Hola cuerpo JSON de la respuesta HTTP de hello contendrá información sobre Hola incorrecta o los documentos.</span><span class="sxs-lookup"><span data-stu-id="220ff-166">hello JSON body of hello HTTP response will contain information about hello unsuccessful document(s).</span></span>

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
> <span data-ttu-id="220ff-167">Esto suele significar que esa carga de hello en la búsqueda de su servicio está alcanzando un punto donde las solicitudes de indización comenzarán tooreturn `503` las respuestas.</span><span class="sxs-lookup"><span data-stu-id="220ff-167">This often means that hello load on your search service is reaching a point where indexing requests will begin tooreturn `503` responses.</span></span> <span data-ttu-id="220ff-168">En este caso, es muy recomendable que interrumpa el código de cliente y espere antes de volver a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="220ff-168">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="220ff-169">Esto le dará sistema Hola algunos toorecover tiempo, aumentar las posibilidades de Hola que se realizará correctamente las solicitudes futuras.</span><span class="sxs-lookup"><span data-stu-id="220ff-169">This will give hello system some time toorecover, increasing hello chances that future requests will succeed.</span></span> <span data-ttu-id="220ff-170">Rápidamente volver a intentar su solicitud únicamente prolongará la situación de Hola.</span><span class="sxs-lookup"><span data-stu-id="220ff-170">Rapidly retrying your requests will only prolong hello situation.</span></span>
>
>

#### <a name="429"></a><span data-ttu-id="220ff-171">429</span><span class="sxs-lookup"><span data-stu-id="220ff-171">429</span></span>
<span data-ttu-id="220ff-172">Un código de estado `429` se devolverán cuando se ha excedido la cuota Hola número de documentos por índice.</span><span class="sxs-lookup"><span data-stu-id="220ff-172">A status code of `429` will be returned when you have exceeded your quota on hello number of documents per index.</span></span>

#### <a name="503"></a><span data-ttu-id="220ff-173">503</span><span class="sxs-lookup"><span data-stu-id="220ff-173">503</span></span>
<span data-ttu-id="220ff-174">Un código de estado `503` se devolverá si ninguno de los elementos de hello en solicitud de saludo se indizaron correctamente.</span><span class="sxs-lookup"><span data-stu-id="220ff-174">A status code of `503` will be returned if none of hello items in hello request were successfully indexed.</span></span> <span data-ttu-id="220ff-175">Este error significa que Hola sistema está sometido a mucha carga y no se puede procesar su solicitud en este momento.</span><span class="sxs-lookup"><span data-stu-id="220ff-175">This error means that hello system is under heavy load and your request can't be processed at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="220ff-176">En este caso, es muy recomendable que interrumpa el código de cliente y espere antes de volver a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="220ff-176">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="220ff-177">Esto le dará sistema Hola algunos toorecover tiempo, aumentar las posibilidades de Hola que se realizará correctamente las solicitudes futuras.</span><span class="sxs-lookup"><span data-stu-id="220ff-177">This will give hello system some time toorecover, increasing hello chances that future requests will succeed.</span></span> <span data-ttu-id="220ff-178">Rápidamente volver a intentar su solicitud únicamente prolongará la situación de Hola.</span><span class="sxs-lookup"><span data-stu-id="220ff-178">Rapidly retrying your requests will only prolong hello situation.</span></span>
>
>

<span data-ttu-id="220ff-179">Para más información sobre las acciones de documentos y las respuestas de éxito o error, consulte [Agregar, actualizar o eliminar documentos](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span><span class="sxs-lookup"><span data-stu-id="220ff-179">For more information on document actions and success/error responses, please see [Add, Update, or Delete Documents](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span></span> <span data-ttu-id="220ff-180">Para más información sobre otros códigos de estado HTTP que se devuelven en caso de error, consulte [Códigos de estado HTTP (Búsqueda de Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span><span class="sxs-lookup"><span data-stu-id="220ff-180">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="220ff-181">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="220ff-181">Next steps</span></span>
<span data-ttu-id="220ff-182">Después de rellenar el índice de búsqueda de Azure, estará listo toostart emitir toosearch de las consultas para los documentos.</span><span class="sxs-lookup"><span data-stu-id="220ff-182">After populating your Azure Search index, you will be ready toostart issuing queries toosearch for documents.</span></span> <span data-ttu-id="220ff-183">Para más información, vea [Consultas en Búsqueda de Azure](search-query-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="220ff-183">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>
