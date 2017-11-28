---
title: "API de REST del servicio Azure Search versión 2015-02-28-Preview | Microsoft Docs"
description: "La API de REST del Servicio Búsqueda de Azure versión 2015-02-28-Preview incluye funciones experimentales como analizadores de lenguaje Natural y búsquedas moreLikeThis."
services: search
documentationcenter: na
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 3dba3bf8-9c83-42f6-82bc-04727bd11037
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: search
ms.date: 05/01/2017
ms.author: brjohnst
ms.openlocfilehash: e6ad5c964bfa8421be2706cb4015980e01a271b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a><span data-ttu-id="89b28-103">API de REST del Servicio Búsqueda de Azure versión 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="89b28-103">Azure Search Service REST API: Version 2015-02-28-Preview</span></span>
<span data-ttu-id="89b28-104">Este artículo es la documentación de referencia de `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="89b28-104">This article is the reference documentation for `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="89b28-105">Esta vista previa amplía la versión disponible generalmente actual, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), proporcionando las siguientes funciones experimentales:</span><span class="sxs-lookup"><span data-stu-id="89b28-105">This preview extends the current generally available version, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), by providing the following experimental features:</span></span>

* <span data-ttu-id="89b28-106">`moreLikeThis` parámetro de consulta en la API de [Buscar documentos](#SearchDocs) .</span><span class="sxs-lookup"><span data-stu-id="89b28-106">`moreLikeThis` query parameter in the [Search Documents](#SearchDocs) API.</span></span> <span data-ttu-id="89b28-107">Busca otros documentos que sean relevantes para otro documento específico.</span><span class="sxs-lookup"><span data-stu-id="89b28-107">It finds other documents that are relevant to another specific document.</span></span>

<span data-ttu-id="89b28-108">Algunas partes adicionales de la API de REST `2015-02-28-Preview` se documentan por separado.</span><span class="sxs-lookup"><span data-stu-id="89b28-108">A few additional parts of the `2015-02-28-Preview` REST API are documented separately.</span></span> <span data-ttu-id="89b28-109">Entre ellos se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="89b28-109">These include:</span></span>

* [<span data-ttu-id="89b28-110">Perfiles de puntuación</span><span class="sxs-lookup"><span data-stu-id="89b28-110">Scoring Profiles</span></span>](search-api-scoring-profiles-2015-02-28-preview.md)
* [<span data-ttu-id="89b28-111">Indexadores</span><span class="sxs-lookup"><span data-stu-id="89b28-111">Indexers</span></span>](search-api-indexers-2015-02-28-preview.md)

<span data-ttu-id="89b28-112">El servicio de Búsqueda de Azure está disponible en varias versiones.</span><span class="sxs-lookup"><span data-stu-id="89b28-112">Azure Search service is available in multiple versions.</span></span> <span data-ttu-id="89b28-113">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="89b28-113">Please refer to [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details.</span></span>

## <a name="apis-in-this-document"></a><span data-ttu-id="89b28-114">API incluidas en este documento</span><span class="sxs-lookup"><span data-stu-id="89b28-114">APIs in this document</span></span>
<span data-ttu-id="89b28-115">La API del servicio Búsqueda de Azure admite dos sintaxis de URL para operaciones de API: simple y OData (consulte [Compatibilidad con OData (API de Búsqueda de Azure)](http://msdn.microsoft.com/library/azure/dn798932.aspx) para obtener más información).</span><span class="sxs-lookup"><span data-stu-id="89b28-115">Azure Search service API supports two URL syntaxes for API operations: simple and OData (see [Support for OData (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) for details).</span></span> <span data-ttu-id="89b28-116">La lista siguiente muestra la sintaxis simple.</span><span class="sxs-lookup"><span data-stu-id="89b28-116">The following list shows the simple syntax.</span></span>

[<span data-ttu-id="89b28-117">Crear índice</span><span class="sxs-lookup"><span data-stu-id="89b28-117">Create Index</span></span>](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="89b28-118">Actualizar índice</span><span class="sxs-lookup"><span data-stu-id="89b28-118">Update Index</span></span>](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="89b28-119">Obtener índice</span><span class="sxs-lookup"><span data-stu-id="89b28-119">Get Index</span></span>](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="89b28-120">Enumerar índices</span><span class="sxs-lookup"><span data-stu-id="89b28-120">Listing Indexes</span></span>](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="89b28-121">Obtención de estadísticas de índice</span><span class="sxs-lookup"><span data-stu-id="89b28-121">Get Index Statistics</span></span>](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[<span data-ttu-id="89b28-122">Analizador de prueba</span><span class="sxs-lookup"><span data-stu-id="89b28-122">Test Analyzer</span></span>](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[<span data-ttu-id="89b28-123">Eliminar un índice</span><span class="sxs-lookup"><span data-stu-id="89b28-123">Delete an Index</span></span>](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="89b28-124">Agregar, eliminar y actualizar datos en un índice</span><span class="sxs-lookup"><span data-stu-id="89b28-124">Add, Delete, and Update Data within an Index</span></span>](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[<span data-ttu-id="89b28-125">Buscar en documentos</span><span class="sxs-lookup"><span data-stu-id="89b28-125">Search Documents</span></span>](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[<span data-ttu-id="89b28-126">Buscar documento</span><span class="sxs-lookup"><span data-stu-id="89b28-126">Lookup Document</span></span>](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[<span data-ttu-id="89b28-127">Documentos de recuento</span><span class="sxs-lookup"><span data-stu-id="89b28-127">Count Documents</span></span>](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[<span data-ttu-id="89b28-128">Sugerencias</span><span class="sxs-lookup"><span data-stu-id="89b28-128">Suggestions</span></span>](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a><span data-ttu-id="89b28-129">Operaciones de índice</span><span class="sxs-lookup"><span data-stu-id="89b28-129">Index Operations</span></span>
<span data-ttu-id="89b28-130">Puede crear y administrar índices en el servicio de Búsqueda de Azure a través de solicitudes HTTP sencillas (POST, GET, PUT, DELETE) en un recurso de índice determinado.</span><span class="sxs-lookup"><span data-stu-id="89b28-130">You can create and manage indexes in Azure Search service via simple HTTP requests (POST, GET, PUT, DELETE) against a given index resource.</span></span> <span data-ttu-id="89b28-131">Para crear un índice, primero debe PUBLICAR un documento JSON que describa el esquema de índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-131">To create an index, you first POST a JSON document that describes the index schema.</span></span> <span data-ttu-id="89b28-132">El esquema define los campos de índice, sus tipos de datos y cómo pueden utilizarse (por ejemplo, en las búsquedas de texto completo, filtros, ordenación o faceting).</span><span class="sxs-lookup"><span data-stu-id="89b28-132">The schema defines the fields of the index, their data types, and how they can be used (for example, in full-text searches, filters, sorting, or faceting).</span></span> <span data-ttu-id="89b28-133">También define los perfiles de puntuación, los proveedores de sugerencias y otros atributos para configurar el comportamiento del índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-133">It also defines scoring profiles, suggesters and other attributes to configure the behavior of the index.</span></span>

<span data-ttu-id="89b28-134">En el ejemplo siguiente se proporciona una ilustración de un esquema que se utiliza para buscar información sobre hoteles con el campo de descripción definido en dos idiomas.</span><span class="sxs-lookup"><span data-stu-id="89b28-134">The following example provides an illustration of a schema used for searching on hotel information with the Description field defined in two languages.</span></span> <span data-ttu-id="89b28-135">Observe de qué modo controlan los atributos cómo se utiliza el campo.</span><span class="sxs-lookup"><span data-stu-id="89b28-135">Notice how attributes control how the field is used.</span></span> <span data-ttu-id="89b28-136">Por ejemplo, el `hotelId` se utiliza como clave de documento (`"key": true`) y se excluye de búsquedas de texto completo (`"searchable": false`).</span><span class="sxs-lookup"><span data-stu-id="89b28-136">For example the `hotelId` is used as the document key (`"key": true`) and is excluded from full-text searches (`"searchable": false`).</span></span>

    {
    "name": "hotels",  
    "fields": [
      {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
      {"name": "baseRate", "type": "Edm.Double"},
      {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
      {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
      {"name": "hotelName", "type": "Edm.String"},
      {"name": "category", "type": "Edm.String"},
      {"name": "tags", "type": "Collection(Edm.String)"},
      {"name": "parkingIncluded", "type": "Edm.Boolean"},
      {"name": "smokingAllowed", "type": "Edm.Boolean"},
      {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
      {"name": "rating", "type": "Edm.Int32"},
      {"name": "location", "type": "Edm.GeographyPoint"}
     ],
     "suggesters": [
      {
       "name": "sg",
       "searchMode": "analyzingInfixMatching",
       "sourceFields": ["hotelName"]
      }
     ]
    }

<span data-ttu-id="89b28-137">Una vez creado el índice, podrá cargar documentos que rellenen el índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-137">After the index is created, you'll upload documents that populate the index.</span></span> <span data-ttu-id="89b28-138">Consulte [Agregar o actualizar documentos](#AddOrUpdateDocuments) para este siguiente paso.</span><span class="sxs-lookup"><span data-stu-id="89b28-138">See [Add or Update Documents](#AddOrUpdateDocuments) for this next step.</span></span>

<span data-ttu-id="89b28-139">Para obtener una introducción de vídeo sobre la indexación en Búsqueda de Azure, consulte el [episodio de portada de nube del canal 9 en Búsqueda de Azure](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span><span class="sxs-lookup"><span data-stu-id="89b28-139">For a video introduction to indexing in Azure Search, see the [Channel 9 Cloud Cover episode on Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span></span>

<a name="CreateIndex"></a>

## <a name="create-index"></a><span data-ttu-id="89b28-140">Crear índice</span><span class="sxs-lookup"><span data-stu-id="89b28-140">Create Index</span></span>
<span data-ttu-id="89b28-141">Un índice es el medio principal para organizar y buscar documentos en la Búsqueda de Azure, de modo similar a cómo organiza los registros en una base de datos una tabla.</span><span class="sxs-lookup"><span data-stu-id="89b28-141">An index is the primary means of organizing and searching documents in Azure Search, similar to how a table organizes records in a database.</span></span> <span data-ttu-id="89b28-142">Cada índice tiene una colección de documentos que cumplen el esquema de índice (nombres de campo, tipos de datos y propiedades), pero los índices también especifican construcciones adicionales (proveedores de sugerencias, opciones de CORS y perfiles de puntuación) que definen otros comportamientos de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-142">Each index has a collection of documents that all conform to the index schema (field names, data types, and properties), but indexes also specify additional constructs (suggesters, scoring profiles, and CORS options) that define other search behaviors.</span></span>

<span data-ttu-id="89b28-143">Puede crear un índice nuevo dentro de un servicio de Búsqueda de Azure mediante una solicitud HTTP POST o PUT.</span><span class="sxs-lookup"><span data-stu-id="89b28-143">You can create a new index within an Azure Search service using an HTTP POST or PUT request.</span></span> <span data-ttu-id="89b28-144">El cuerpo de la solicitud es un esquema JSON que especifica la información de índice y configuración.</span><span class="sxs-lookup"><span data-stu-id="89b28-144">The body of the request is a JSON schema that specifies the index and configuration information.</span></span>

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="89b28-145">Como alternativa, puede usar PUT y especificar el nombre del índice en el URI.</span><span class="sxs-lookup"><span data-stu-id="89b28-145">Alternatively, you can use PUT and specify the index name on the URI.</span></span> <span data-ttu-id="89b28-146">Si el índice no existe, se creará.</span><span class="sxs-lookup"><span data-stu-id="89b28-146">If the index does not exist, it will be created.</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

<span data-ttu-id="89b28-147">Crear un índice determina la estructura de los documentos almacenados y usados en operaciones de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-147">Creating an index determines the structure of the documents stored and used in search operations.</span></span> <span data-ttu-id="89b28-148">Rellenar el índice es una operación independiente.</span><span class="sxs-lookup"><span data-stu-id="89b28-148">Populating the index is a separate operation.</span></span> <span data-ttu-id="89b28-149">En este paso, puede usar un [indexador](https://msdn.microsoft.com/library/azure/mt183328.aspx) (disponible para orígenes de datos admitidos) o una operación [Agregar, actualizar o eliminar documentos](https://msdn.microsoft.com/library/azure/dn798930.aspx).</span><span class="sxs-lookup"><span data-stu-id="89b28-149">For this step, you can use an [indexer](https://msdn.microsoft.com/library/azure/mt183328.aspx) (available for supported data sources) or an [Add, Update, or Delete Documents](https://msdn.microsoft.com/library/azure/dn798930.aspx) operation.</span></span> <span data-ttu-id="89b28-150">El índice invertido se genera cuando se publican los documentos.</span><span class="sxs-lookup"><span data-stu-id="89b28-150">The inverted index is generated when the documents are posted.</span></span>

<span data-ttu-id="89b28-151">**Nota**: El número máximo de índices permitido varía según el nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="89b28-151">**Note**: The maximum number of indexes allowed varies by pricing tier.</span></span> <span data-ttu-id="89b28-152">El servicio gratuito permite hasta tres índices.</span><span class="sxs-lookup"><span data-stu-id="89b28-152">The free service allows up to 3 indexes.</span></span> <span data-ttu-id="89b28-153">El servicio estándar permite 50 índices por servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-153">Standard service allows 50 indexes per Search service.</span></span> <span data-ttu-id="89b28-154">Consulte [Límites y restricciones](http://msdn.microsoft.com/library/azure/dn798934.aspx) para obtener detalles.</span><span class="sxs-lookup"><span data-stu-id="89b28-154">See [Limits and constraints](http://msdn.microsoft.com/library/azure/dn798934.aspx) for details.</span></span>

<span data-ttu-id="89b28-155">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-155">**Request**</span></span>

<span data-ttu-id="89b28-156">HTTPS es necesario para todas las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-156">HTTPS is required for all service requests.</span></span> <span data-ttu-id="89b28-157">La solicitud **Crear índice** se puede construir con un método POST o PUT.</span><span class="sxs-lookup"><span data-stu-id="89b28-157">The **Create Index** request can be constructed using either a POST or PUT method.</span></span> <span data-ttu-id="89b28-158">Al usar POST, debe proporcionar un nombre de índice en el cuerpo de la solicitud junto con la definición de esquema de índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-158">When using POST, you must provide an index name in the request body along with the index schema definition.</span></span> <span data-ttu-id="89b28-159">Con PUT, el nombre del índice es parte de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="89b28-159">With PUT, the index name is part of the URL.</span></span> <span data-ttu-id="89b28-160">Si el índice no existe, se crea.</span><span class="sxs-lookup"><span data-stu-id="89b28-160">If the index doesn't exist, it is created.</span></span> <span data-ttu-id="89b28-161">Si ya existe, se actualiza a la nueva definición.</span><span class="sxs-lookup"><span data-stu-id="89b28-161">If it already exists, it is updated to the new definition.</span></span>

<span data-ttu-id="89b28-162">El nombre del índice debe estar en minúsculas, comenzar por una letra o un número, no tener ninguna barra o punto y tener menos de 128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="89b28-162">The index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="89b28-163">Después de iniciar el nombre del índice por una letra o un número, el resto del nombre puede incluir cualquier letra, número y guiones, siempre que los guiones no aparezcan de manera consecutiva.</span><span class="sxs-lookup"><span data-stu-id="89b28-163">After starting the index name with a letter or number, the rest of the name can include any letter, number and dashes, as long as the dashes are not consecutive.</span></span>

<span data-ttu-id="89b28-164">`api-version` es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="89b28-164">The `api-version` is required.</span></span> <span data-ttu-id="89b28-165">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener una lista de las versiones disponibles.</span><span class="sxs-lookup"><span data-stu-id="89b28-165">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for a list of available versions.</span></span>

<span data-ttu-id="89b28-166">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-166">**Request Headers**</span></span>

<span data-ttu-id="89b28-167">En la lista siguiente se describen los encabezados de solicitud obligatorios y opcionales.</span><span class="sxs-lookup"><span data-stu-id="89b28-167">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="89b28-168">`Content-Type`: obligatorio.</span><span class="sxs-lookup"><span data-stu-id="89b28-168">`Content-Type`: Required.</span></span> <span data-ttu-id="89b28-169">Establézcalo en `application/json`</span><span class="sxs-lookup"><span data-stu-id="89b28-169">Set this to `application/json`</span></span>
* <span data-ttu-id="89b28-170">`api-key`: obligatorio.</span><span class="sxs-lookup"><span data-stu-id="89b28-170">`api-key`: Required.</span></span> <span data-ttu-id="89b28-171">El `api-key` se usa para</span><span class="sxs-lookup"><span data-stu-id="89b28-171">The `api-key` is used to</span></span>
* <span data-ttu-id="89b28-172">autenticar la solicitud al servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-172">authenticate the request to your Search service.</span></span> <span data-ttu-id="89b28-173">Es un valor de cadena único para el servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-173">It is a string value, unique to your service.</span></span> <span data-ttu-id="89b28-174">La solicitud **Crear índice** debe incluir un encabezado `api-key` establecido en su clave de administración (en lugar de una clave de consulta).</span><span class="sxs-lookup"><span data-stu-id="89b28-174">The **Create Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="89b28-175">También necesitará el nombre del servicio para construir la dirección URL de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="89b28-175">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="89b28-176">Puede obtener el nombre de servicio y `api-key` desde el panel de servicio en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="89b28-176">You can get both the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="89b28-177">Consulte [Crear un servicio de Búsqueda de Azure en el portal](search-create-service-portal.md) para obtener ayuda sobre la navegación en páginas.</span><span class="sxs-lookup"><span data-stu-id="89b28-177">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="89b28-178"><a name="RequestData"></a>
**Sintaxis del cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-178"><a name="RequestData"></a>
**Request Body Syntax**</span></span>

<span data-ttu-id="89b28-179">El cuerpo de la solicitud contiene una definición de esquema, que incluye la lista de campos de datos de los documentos que se introducirán en este índice, tipos de datos, atributos, así como una lista opcional de perfiles de puntuación que se utilizan para puntuar documentos de coincidencias de puntuación en el momento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="89b28-179">The body of the request contains a schema definition, which includes the list of data fields within documents that will be fed into this index, data types, attributes, as well as an optional list of scoring profiles that are used to score matching documents at query time.</span></span>

<span data-ttu-id="89b28-180">Tenga en cuenta que para una solicitud POST, debe especificar el nombre del índice en el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="89b28-180">Note that for a POST request, you must specify the index name in the request body.</span></span>

<span data-ttu-id="89b28-181">Solo puede haber un campo de clave en el índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-181">There can only be one key field in the index.</span></span> <span data-ttu-id="89b28-182">Debe ser un campo de cadena.</span><span class="sxs-lookup"><span data-stu-id="89b28-182">It has to be a string field.</span></span> <span data-ttu-id="89b28-183">Este campo representa el identificador único de cada documento almacenado en el índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-183">This field represents the unique identifier for each document stored within the index.</span></span>

<span data-ttu-id="89b28-184">Las partes principales de un índice son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="89b28-184">The main parts of an index include the following:</span></span>

* `name`
* <span data-ttu-id="89b28-185">`fields` que se introducirán en este índice, incluido el nombre, tipo de datos y propiedades que definen las acciones permitidas en ese campo.</span><span class="sxs-lookup"><span data-stu-id="89b28-185">`fields` that will be fed into this index, including name, data type, and properties that define allowable actions on that field.</span></span>
* <span data-ttu-id="89b28-186">`suggesters` se usa para autocompletar o anticipar la escritura de las consultas.</span><span class="sxs-lookup"><span data-stu-id="89b28-186">`suggesters` used for auto-complete or type-ahead queries.</span></span>
* <span data-ttu-id="89b28-187">`scoringProfiles` se usa para la clasificación de la puntuación de la búsqueda personalizada.</span><span class="sxs-lookup"><span data-stu-id="89b28-187">`scoringProfiles` used for custom search score ranking.</span></span> <span data-ttu-id="89b28-188">Consulte [Agregar perfiles de puntuación](https://msdn.microsoft.com/library/azure/dn798928.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="89b28-188">See [Add scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for details.</span></span>
* <span data-ttu-id="89b28-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` se usa para definir cómo se descomponen los documentos y las consultas en tokens con capacidad de consulta y búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` used to define how your documents/queries are broken into indexable/searchable tokens.</span></span> <span data-ttu-id="89b28-190">Consulte [Análisis en Búsqueda de Azure](https://aka.ms//azsanalysis) para más detalles.</span><span class="sxs-lookup"><span data-stu-id="89b28-190">See [Analysis in Azure Search](https://aka.ms//azsanalysis) for details.</span></span>
* <span data-ttu-id="89b28-191">`defaultScoringProfile` se usa para sobrescribir los comportamientos de puntuación predeterminados.</span><span class="sxs-lookup"><span data-stu-id="89b28-191">`defaultScoringProfile` used to overwrite the default scoring behaviors.</span></span>
* <span data-ttu-id="89b28-192">`corsOptions` para permitir las consultas de origen cruzado en el índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-192">`corsOptions` to allow cross-origin queries against your index.</span></span>

<span data-ttu-id="89b28-193">La sintaxis para estructurar la carga de la solicitud es la siguiente.</span><span class="sxs-lookup"><span data-stu-id="89b28-193">The syntax for structuring the request payload is as follows.</span></span> <span data-ttu-id="89b28-194">En este tema se proporciona una solicitud de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="89b28-194">A sample request is provided further on in this topic.</span></span>

    {
      "name": (optional on PUT; required on POST) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false,              
          "analyzer": "name of the analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of the search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of the indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in the future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies to searchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading to now over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter to be passed in queries to use as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (the distance in kilometers from the reference location where the boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter to be passed in queries to specify list of tags to compare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }

<span data-ttu-id="89b28-195">**Atributos de índice**</span><span class="sxs-lookup"><span data-stu-id="89b28-195">**Index Attributes**</span></span>

<span data-ttu-id="89b28-196">Es posible establecer los siguientes atributos para crear un índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-196">The following attributes can be set when creating an index.</span></span> <span data-ttu-id="89b28-197">Para obtener más información sobre la puntuación y los perfiles de puntuación, consulte [Agregar perfiles de puntuación](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="89b28-197">For details about scoring and scoring profiles, see [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span>

<span data-ttu-id="89b28-198">`name` : establece el nombre del campo.</span><span class="sxs-lookup"><span data-stu-id="89b28-198">`name` - Sets the name of the field.</span></span>

<span data-ttu-id="89b28-199">`type` : establece el tipo de datos del campo.</span><span class="sxs-lookup"><span data-stu-id="89b28-199">`type` - Sets the data type for the field.</span></span>

<span data-ttu-id="89b28-200">`searchable` : marca el campo como de búsqueda de texto completo.</span><span class="sxs-lookup"><span data-stu-id="89b28-200">`searchable` - Marks the field as full-text search-able.</span></span> <span data-ttu-id="89b28-201">Esto significa que se someterá a análisis como la separación de palabras durante la indexación.</span><span class="sxs-lookup"><span data-stu-id="89b28-201">This means it will undergo analysis such as word-breaking during indexing.</span></span> <span data-ttu-id="89b28-202">Si establece un campo `searchable` en un valor como "día soleado", internamente, se dividirá en los tokens individuales "soleado" y "día".</span><span class="sxs-lookup"><span data-stu-id="89b28-202">If you set a `searchable` field to a value like "sunny day", internally it will be split into the individual tokens "sunny" and "day".</span></span> <span data-ttu-id="89b28-203">Esto permite realizar búsquedas de texto completo de estos términos.</span><span class="sxs-lookup"><span data-stu-id="89b28-203">This enables full-text searches for these terms.</span></span> <span data-ttu-id="89b28-204">Los campos de tipo `Edm.String` o `Collection(Edm.String)` son `searchable` de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="89b28-204">Fields of type `Edm.String` or `Collection(Edm.String)` are `searchable` by default.</span></span> <span data-ttu-id="89b28-205">Los campos de otros tipos no pueden ser `searchable`.</span><span class="sxs-lookup"><span data-stu-id="89b28-205">Fields of other types cannot be `searchable`.</span></span>

* <span data-ttu-id="89b28-206">**Nota**: `searchable`los campos consumen espacio adicional en el índice, ya que Azure Search almacenará una versión con tokens adicional del valor del campo para las búsquedas de texto completo.</span><span class="sxs-lookup"><span data-stu-id="89b28-206">**Note**: `searchable` fields consume extra space in your index since Azure Search will store an additional tokenized version of the field value for full-text searches.</span></span> <span data-ttu-id="89b28-207">Si desea ahorrar espacio en el índice y no necesita incluir un campo en las búsquedas, establezca `searchable` en `false`.</span><span class="sxs-lookup"><span data-stu-id="89b28-207">If you want to save space in your index and you don't need a field to be included in searches, set `searchable` to `false`.</span></span>

<span data-ttu-id="89b28-208">`filterable`: permite que se haga referencia al campo en las consultas `$filter`.</span><span class="sxs-lookup"><span data-stu-id="89b28-208">`filterable` - Allows the field to be referenced in `$filter` queries.</span></span> <span data-ttu-id="89b28-209">`filterable` difiere de `searchable` en el modo en que se gestionan las cadenas.</span><span class="sxs-lookup"><span data-stu-id="89b28-209">`filterable` differs from `searchable` in how strings are handled.</span></span> <span data-ttu-id="89b28-210">Los campos de tipo `Edm.String` o `Collection(Edm.String)` que son `filterable` no sufren separación de palabras, por lo que las comparaciones son solo para las coincidencias exactas.</span><span class="sxs-lookup"><span data-stu-id="89b28-210">Fields of type `Edm.String` or `Collection(Edm.String)` that are `filterable` do not undergo word-breaking, so comparisons are for exact matches only.</span></span> <span data-ttu-id="89b28-211">Por ejemplo, si establece este campo `f` en "día soleado", `$filter=f eq 'sunny'` no encontrará ninguna coincidencia, pero `$filter=f eq 'sunny day'` sí.</span><span class="sxs-lookup"><span data-stu-id="89b28-211">For example, if you set such a field `f` to "sunny day", `$filter=f eq 'sunny'` will find no matches, but `$filter=f eq 'sunny day'` will.</span></span> <span data-ttu-id="89b28-212">Todos los campos son `filterable` de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="89b28-212">All fields are `filterable` by default.</span></span>

<span data-ttu-id="89b28-213">`sortable` : de forma predeterminada el sistema ordena los resultados por calificación, pero en muchas experiencias los usuarios desearán ordenar por los campos de los documentos.</span><span class="sxs-lookup"><span data-stu-id="89b28-213">`sortable` - By default the system sorts results by score, but in many experiences users will want to sort by fields in the documents.</span></span> <span data-ttu-id="89b28-214">Los campos de tipo `Collection(Edm.String)` no pueden ser `sortable`.</span><span class="sxs-lookup"><span data-stu-id="89b28-214">Fields of type `Collection(Edm.String)` cannot be `sortable`.</span></span> <span data-ttu-id="89b28-215">El resto de campos son `sortable` de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="89b28-215">All other fields are `sortable` by default.</span></span>

<span data-ttu-id="89b28-216">`facetable`: suele utilizarse en una presentación de resultados de búsqueda que incluya el número de resultados por categoría (por ejemplo, busque cámaras digitales y consulte los resultados divididos por marca, por megapíxeles, por precio, etc.).</span><span class="sxs-lookup"><span data-stu-id="89b28-216">`facetable`- Typically used in a presentation of search results that includes hit count by category (for example, search for digital cameras and see hits by brand, by megapixels, by price, etc.).</span></span> <span data-ttu-id="89b28-217">Esta opción no puede utilizarse con campos de tipo `Edm.GeographyPoint`.</span><span class="sxs-lookup"><span data-stu-id="89b28-217">This option cannot be used with fields of type `Edm.GeographyPoint`.</span></span> <span data-ttu-id="89b28-218">El resto de campos son `facetable` de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="89b28-218">All other fields are `facetable` by default.</span></span>

* <span data-ttu-id="89b28-219">**Nota**: los campos de tipo `Edm.String` que son `filterable`, `sortable` o `facetable` solo pueden ocupar una longitud de 32 KB como máximo.</span><span class="sxs-lookup"><span data-stu-id="89b28-219">**Note**: Fields of type `Edm.String` that are `filterable`, `sortable`, or `facetable` can be at most 32KB in length.</span></span> <span data-ttu-id="89b28-220">Esto se debe a que esos campos se tratan como un término de búsqueda único y la longitud máxima de un término de Búsqueda de Azure es de 32 KB.</span><span class="sxs-lookup"><span data-stu-id="89b28-220">This is because such fields are treated as a single search term, and the maximum length of a term in Azure Search is 32KB.</span></span> <span data-ttu-id="89b28-221">Si necesita almacenar más texto que este en un campo de cadena único, deberá establecer explícitamente `filterable`, `sortable` y `facetable` en `false` en la definición del índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-221">If you need to store more text than this in a single string field, you will need to explicitly set `filterable`, `sortable`, and `facetable` to `false` in your index definition.</span></span>
* <span data-ttu-id="89b28-222">**Nota**: si un campo no tiene ninguno de los atributos anteriores establecidos en `true` (`searchable`, `filterable`, `sortable` o `facetable`) el campo se excluirá eficazmente del índice invertido.</span><span class="sxs-lookup"><span data-stu-id="89b28-222">**Note**: If a field has none of the above attributes set to `true` (`searchable`, `filterable`, `sortable`,  or`facetable`) the field is effectively excluded from the inverted index.</span></span> <span data-ttu-id="89b28-223">Esta opción es útil para los campos que no se utilizan en las consultas, pero que son necesarios en los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-223">This option is useful for fields that are not used in queries, but are needed in search results.</span></span> <span data-ttu-id="89b28-224">La exclusión de esos campos del índice mejora el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="89b28-224">Excluding such fields from the index improves performance.</span></span>

<span data-ttu-id="89b28-225">`key` : marca el campo como que contiene identificadores únicos para los documentos del índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-225">`key` - Marks the field as containing unique identifiers for documents within the index.</span></span> <span data-ttu-id="89b28-226">Es necesario elegir exactamente un campo como campo `key` y debe ser de tipo `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="89b28-226">Exactly one field must be chosen as the `key` field and it must be of type `Edm.String`.</span></span> <span data-ttu-id="89b28-227">Los campos de clave pueden usarse para buscar documentos directamente a través de la [API de búsqueda](#LookupAPI).</span><span class="sxs-lookup"><span data-stu-id="89b28-227">Key fields can be used to look up documents directly via the [Lookup API](#LookupAPI).</span></span>

<span data-ttu-id="89b28-228">`retrievable` : establece si el campo se puede devolver un resultado de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-228">`retrievable` - Sets whether the field can be returned in a search result.</span></span>  <span data-ttu-id="89b28-229">Esto resulta útil cuando desea usar un campo (por ejemplo, margen) como filtro, ordenación o mecanismo de puntuación, pero no desea que el campo sea visible para el usuario final.</span><span class="sxs-lookup"><span data-stu-id="89b28-229">This is useful when you want to use a field (for example, margin) as a filter, sorting, or scoring mechanism but do not want the field to be visible to the end user.</span></span> <span data-ttu-id="89b28-230">Este atributo debe ser `true` for `key` .</span><span class="sxs-lookup"><span data-stu-id="89b28-230">This attribute must be `true` for `key` fields.</span></span>

<span data-ttu-id="89b28-231">`analyzer` : establece el nombre del analizador que se usa para el campo en el momento de la búsqueda y la indexación.</span><span class="sxs-lookup"><span data-stu-id="89b28-231">`analyzer` - Sets the name of the analyzer to use for the field at search time and indexing time.</span></span> <span data-ttu-id="89b28-232">Para conocer el conjunto de valores permitido, consulte [Analizadores](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="89b28-232">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="89b28-233">Esta opción puede utilizarse solo con campos `searchable` y no se puede establecer junto con `searchAnalyzer` o `indexAnalyzer`.</span><span class="sxs-lookup"><span data-stu-id="89b28-233">This option can be used only with `searchable` fields and it can't be set together with either `searchAnalyzer` or `indexAnalyzer`.</span></span>  <span data-ttu-id="89b28-234">Una vez que se elige el analizador, no se podrá cambiar para el campo.</span><span class="sxs-lookup"><span data-stu-id="89b28-234">Once the analyzer is chosen, it cannot be changed for the field.</span></span>

<span data-ttu-id="89b28-235">`searchAnalyzer` : establece el nombre del analizador que se usa en el momento de búsqueda para el campo.</span><span class="sxs-lookup"><span data-stu-id="89b28-235">`searchAnalyzer` - Sets the name of the analyzer used at search time for the field.</span></span> <span data-ttu-id="89b28-236">Para conocer el conjunto de valores permitido, consulte [Analizadores](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="89b28-236">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="89b28-237">Esta opción solo puede utilizarse con campos `searchable` .</span><span class="sxs-lookup"><span data-stu-id="89b28-237">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="89b28-238">Se debe establecer junto con `indexAnalyzer` y no se puede establecer junto con la opción `analyzer`.</span><span class="sxs-lookup"><span data-stu-id="89b28-238">It must be set together with `indexAnalyzer` and it cannot be set together with the `analyzer` option.</span></span> <span data-ttu-id="89b28-239">Este analizador se puede actualizar en un campo existente.</span><span class="sxs-lookup"><span data-stu-id="89b28-239">This analyzer can be updated on an existing field.</span></span>

<span data-ttu-id="89b28-240">`indexAnalyzer` : establece el nombre del analizador que se usa en el momento de la indexación para el campo.</span><span class="sxs-lookup"><span data-stu-id="89b28-240">`indexAnalyzer` - Sets the name of the analyzer used at indexing time for the field.</span></span> <span data-ttu-id="89b28-241">Para conocer el conjunto de valores permitido, consulte [Analizadores](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="89b28-241">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="89b28-242">Esta opción solo puede utilizarse con campos `searchable` .</span><span class="sxs-lookup"><span data-stu-id="89b28-242">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="89b28-243">Se debe establecer junto con `searchAnalyzer` y no se puede establecer junto con la opción `analyzer`.</span><span class="sxs-lookup"><span data-stu-id="89b28-243">It must be set together with `searchAnalyzer` and it cannot be set together with the `analyzer` option.</span></span> <span data-ttu-id="89b28-244">Una vez que se elige el analizador, no se podrá cambiar para el campo.</span><span class="sxs-lookup"><span data-stu-id="89b28-244">Once the analyzer is chosen, it cannot be changed for the field.</span></span>

<span data-ttu-id="89b28-245">`suggesters` : establece el modo de búsqueda y los campos que son el origen del contenido para obtener sugerencias.</span><span class="sxs-lookup"><span data-stu-id="89b28-245">`suggesters` - Sets the search mode and fields that are the source of the content for suggestions.</span></span> <span data-ttu-id="89b28-246">Consulte [Proveedores de sugerencias](#Suggesters) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="89b28-246">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="89b28-247">`scoringProfiles` : define comportamientos de puntuación personalizados que permiten influir en los elementos que aparecen más arriba en los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-247">`scoringProfiles` - Defines custom scoring behaviors that let you influence which items appear higher in search results.</span></span> <span data-ttu-id="89b28-248">Los perfiles de puntuación se componen de ponderaciones de campos y de funciones.</span><span class="sxs-lookup"><span data-stu-id="89b28-248">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="89b28-249">Consulte [Agregar perfiles de puntuación](https://msdn.microsoft.com/library/azure/dn798928.aspx) para obtener más información acerca de los atributos usados en un perfil de puntuación.</span><span class="sxs-lookup"><span data-stu-id="89b28-249">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information about the attributes used in a scoring profile.</span></span>

<span data-ttu-id="89b28-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Compatibilidad con idioma**</span><span class="sxs-lookup"><span data-stu-id="89b28-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Language support**</span></span>

<span data-ttu-id="89b28-251">Los campos localizables se someten a análisis que con frecuencia implican la separación de palabras, la normalización de texto y el filtrado de términos.</span><span class="sxs-lookup"><span data-stu-id="89b28-251">Searchable fields undergo analysis that most frequently involves word-breaking, text normalization, and filtering out terms.</span></span> <span data-ttu-id="89b28-252">De forma predeterminada, los campos localizables de Azure Search se analizan con el [analizador estándar de Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) que divide el texto en elementos siguiendo las reglas de ["Segmentación de texto Unicode"](http://unicode.org/reports/tr29/).</span><span class="sxs-lookup"><span data-stu-id="89b28-252">By default, searchable fields in Azure Search are analyzed with the [Apache Lucene Standard analyzer](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) which breaks text into elements following the["Unicode Text Segmentation"](http://unicode.org/reports/tr29/) rules.</span></span> <span data-ttu-id="89b28-253">Además, el analizador estándar convierte todos los caracteres en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="89b28-253">Additionally, the standard analyzer converts all characters to their lower case form.</span></span> <span data-ttu-id="89b28-254">Los documentos indexados y lo términos de búsqueda son sometidos a análisis durante la indexación y el procesamiento de consultas.</span><span class="sxs-lookup"><span data-stu-id="89b28-254">Both indexed documents and search terms go through the analysis during indexing and query processing.</span></span>

<span data-ttu-id="89b28-255">Búsqueda de Azure admite una variedad de lenguajes.</span><span class="sxs-lookup"><span data-stu-id="89b28-255">Azure Search supports a variety of languages.</span></span> <span data-ttu-id="89b28-256">Cada uno de esos idiomas requiere un analizador de texto no estándar que representa las características de un idioma determinado.</span><span class="sxs-lookup"><span data-stu-id="89b28-256">Each language requires a non-standard text analyzer which accounts for characteristics of a given language.</span></span> <span data-ttu-id="89b28-257">Búsqueda de Azure ofrece dos tipos de analizadores:</span><span class="sxs-lookup"><span data-stu-id="89b28-257">Azure Search offers two types of analyzers:</span></span>

* <span data-ttu-id="89b28-258">35 analizadores respaldados por Lucene.</span><span class="sxs-lookup"><span data-stu-id="89b28-258">35 analyzers backed by Lucene.</span></span>
* <span data-ttu-id="89b28-259">50 analizadores respaldados por la tecnología de procesamiento de lenguaje natural de Microsoft usada en Office y Bing.</span><span class="sxs-lookup"><span data-stu-id="89b28-259">50 analyzers backed by proprietary Microsoft natural language processing technology used in Office and Bing.</span></span>

<span data-ttu-id="89b28-260">Es posible que algunos desarrolladores prefieran la solución más familiar, simple y de código abierto de Lucene.</span><span class="sxs-lookup"><span data-stu-id="89b28-260">Some developers might prefer the more familiar, simple, open-source solution of Lucene.</span></span> <span data-ttu-id="89b28-261">Los analizadores de Lucene son más rápidos, pero los analizadores de Microsoft disponen de capacidades avanzadas, como la lematización, la descomposición de palabras (en idiomas como el alemán, danés, neerlandés, sueco, noruego, estonio, finés, húngaro, eslovaco) y el reconocimiento de entidades (direcciones URL, correos electrónicos, fechas y números).</span><span class="sxs-lookup"><span data-stu-id="89b28-261">Lucene analyzers are faster, but the Microsoft analyzers have advanced capabilities, such as lemmatization, word decompounding (in languages like German, Danish, Dutch, Swedish, Norwegian, Estonian, Finish, Hungarian, Slovak) and entity recognition (URLs, emails, dates, numbers).</span></span> <span data-ttu-id="89b28-262">Si es posible, debe ejecutar las comparaciones de los analizadores de Microsoft y Lucene para decidir cuál es la que se ajusta mejor.</span><span class="sxs-lookup"><span data-stu-id="89b28-262">If possible, you should run comparisons of both the Microsoft and Lucene analyzers to decide which one is a better fit.</span></span>

<span data-ttu-id="89b28-263">***Cómo se comparan***</span><span class="sxs-lookup"><span data-stu-id="89b28-263">***How they compare***</span></span>

<span data-ttu-id="89b28-264">El analizador de Lucene para inglés amplía el analizador estándar.</span><span class="sxs-lookup"><span data-stu-id="89b28-264">The Lucene analyzer for English extends the standard analyzer.</span></span> <span data-ttu-id="89b28-265">Elimina los posesivos (los ’s finales) de las palabras, aplica la lematización conforme al [Algoritmo de lematización Porter](http://tartarus.org/~martin/PorterStemmer/) y elimina las [palabras no significativas](http://en.wikipedia.org/wiki/Stop_words) del inglés.</span><span class="sxs-lookup"><span data-stu-id="89b28-265">It removes possessives (trailing 's) from words, applies stemming as per [Porter Stemming algorithm](http://tartarus.org/~martin/PorterStemmer/), and removes English [stop words](http://en.wikipedia.org/wiki/Stop_words).</span></span>

<span data-ttu-id="89b28-266">En comparación, el analizador de Microsoft realiza la lematización en lugar del stemming.</span><span class="sxs-lookup"><span data-stu-id="89b28-266">In comparison, the Microsoft analyzer performs lemmatization instead of stemming.</span></span> <span data-ttu-id="89b28-267">Significa que puede controlar mucho mejor formas de palabras derivadas e irregulares, lo que da como resultado unos resultados de búsqueda más pertinentes (consulte el módulo 7 de [presentación MVA de Búsqueda de Azure](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) para obtener más detalles).</span><span class="sxs-lookup"><span data-stu-id="89b28-267">It means it can handle inflected and irregular word forms much better what results in more relevant search results (watch module 7 of [Azure Search MVA presentation](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) for more details).</span></span>

<span data-ttu-id="89b28-268">La indexación con analizadores de Microsoft es entre dos y tres veces más lenta de media que sus equivalentes de Lucene en función del idioma.</span><span class="sxs-lookup"><span data-stu-id="89b28-268">Indexing with Microsoft analyzers is on average two to three times slower than their Lucene equivalents, depending on the language.</span></span> <span data-ttu-id="89b28-269">El rendimiento de la búsqueda no debería verse afectado significativamente en las consultas de tamaño medio.</span><span class="sxs-lookup"><span data-stu-id="89b28-269">Search performance should not be significantly affected for average size queries.</span></span>

<span data-ttu-id="89b28-270">***Configuración***</span><span class="sxs-lookup"><span data-stu-id="89b28-270">***Configuration***</span></span>

<span data-ttu-id="89b28-271">Para cada campo de la definición del índice, puede establecer la propiedad `analyzer` en un nombre de analizador que especifica el idioma y el proveedor.</span><span class="sxs-lookup"><span data-stu-id="89b28-271">For each field in the index definition, you can set the `analyzer` property to an analyzer name that specifies which language and vendor.</span></span> <span data-ttu-id="89b28-272">Se aplicará el mismo analizador durante la búsqueda e indización de ese campo.</span><span class="sxs-lookup"><span data-stu-id="89b28-272">The same analyzer will be applied when indexing and searching for that field.</span></span>
<span data-ttu-id="89b28-273">Por ejemplo, puede tener campos separados para descripciones de hoteles en inglés, francés y español que existen en paralelo dentro del mismo índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-273">For example, you can have separate fields for English, French, and Spanish hotel descriptions that exist side-by-side in the same index.</span></span> <span data-ttu-id="89b28-274">Use el [parámetro de consulta "searchFields"](#SearchQueryParameters) para especificar qué campo concreto del lenguaje buscar en las consultas.</span><span class="sxs-lookup"><span data-stu-id="89b28-274">Use the ['searchFields' query parameter](#SearchQueryParameters) to specify which language-specific field to search against in your queries.</span></span> <span data-ttu-id="89b28-275">Puede revisar ejemplos de consultas que incluyan la propiedad `analyzer` en [Buscar documentos](#SearchDocs).</span><span class="sxs-lookup"><span data-stu-id="89b28-275">You can review query examples that include the `analyzer` property in [Search Documents](#SearchDocs).</span></span> 

<span data-ttu-id="89b28-276">***Lista de analizadores***</span><span class="sxs-lookup"><span data-stu-id="89b28-276">***Analyzer list***</span></span>

<span data-ttu-id="89b28-277">A continuación se muestra la lista de idiomas admitidos y los nombres de analizadores Lucene y Microsoft.</span><span class="sxs-lookup"><span data-stu-id="89b28-277">Below is the list of supported languages together with Lucene and Microsoft analyzer names.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="89b28-278">Idioma</span><span class="sxs-lookup"><span data-stu-id="89b28-278">Language</span></span></th>
        <th><span data-ttu-id="89b28-279">Nombre del analizador de Microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-279">Microsoft analyzer name</span></span></th>
        <th><span data-ttu-id="89b28-280">Nombre del analizador de Lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-280">Lucene analyzer name</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-281">Árabe</span><span class="sxs-lookup"><span data-stu-id="89b28-281">Arabic</span></span></td>
        <td><span data-ttu-id="89b28-282">ar.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-282">ar.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-283">ar.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-283">ar.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-284">Armenio</span><span class="sxs-lookup"><span data-stu-id="89b28-284">Armenian</span></span></td>
        <td></td>
        <td><span data-ttu-id="89b28-285">hy.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-285">hy.lucene</span></span></td>
      </tr>
    <tr>
        <td><span data-ttu-id="89b28-286">Bangla</span><span class="sxs-lookup"><span data-stu-id="89b28-286">Bangla</span></span></td>
        <td><span data-ttu-id="89b28-287">bn.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-287">bn.microsoft</span></span></td>
        <td></td>
    </tr>
      <tr>
        <td><span data-ttu-id="89b28-288">Vasco</span><span class="sxs-lookup"><span data-stu-id="89b28-288">Basque</span></span></td>
        <td></td>
        <td><span data-ttu-id="89b28-289">eu.Lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-289">eu.lucene</span></span></td>
    </tr>
      <tr>
         <td><span data-ttu-id="89b28-290">Búlgaro</span><span class="sxs-lookup"><span data-stu-id="89b28-290">Bulgarian</span></span></td>
        <td><span data-ttu-id="89b28-291">bg.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-291">bg.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-292">bg.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-292">bg.lucene</span></span></td>
      </tr>
      <tr>
        <td><span data-ttu-id="89b28-293">Catalán</span><span class="sxs-lookup"><span data-stu-id="89b28-293">Catalan</span></span></td>
        <td><span data-ttu-id="89b28-294">ca.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-294">ca.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-295">ca.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-295">ca.lucene</span></span></td>          
      </tr>
    <tr>
        <td><span data-ttu-id="89b28-296">Chino simplificado</span><span class="sxs-lookup"><span data-stu-id="89b28-296">Chinese Simplified</span></span></td>
        <td><span data-ttu-id="89b28-297">zh-Hans.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-297">zh-Hans.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-298">zh-Hans.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-298">zh-Hans.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-299">Chino tradicional</span><span class="sxs-lookup"><span data-stu-id="89b28-299">Chinese Traditional</span></span></td>
        <td><span data-ttu-id="89b28-300">zh-Hant.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-300">zh-Hant.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-301">zh-Hant.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-301">zh-Hant.lucene</span></span></td>        
    <tr>
    <tr>
        <td><span data-ttu-id="89b28-302">Croata</span><span class="sxs-lookup"><span data-stu-id="89b28-302">Croatian</span></span></td>
        <td><span data-ttu-id="89b28-303">hr.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-303">hr.microsoft</span></span></td>
        <td/></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-304">Checo</span><span class="sxs-lookup"><span data-stu-id="89b28-304">Czech</span></span></td>
        <td><span data-ttu-id="89b28-305">cs.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-305">cs.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-306">cs.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-306">cs.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="89b28-307">Danés</span><span class="sxs-lookup"><span data-stu-id="89b28-307">Danish</span></span></td>
        <td><span data-ttu-id="89b28-308">da.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-308">da.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-309">da.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-309">da.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="89b28-310">Neerlandés</span><span class="sxs-lookup"><span data-stu-id="89b28-310">Dutch</span></span></td>
        <td><span data-ttu-id="89b28-311">nl.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-311">nl.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-312">nl.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-312">nl.lucene</span></span></td>    
    </tr>    
    <tr>
        <td><span data-ttu-id="89b28-313">English</span><span class="sxs-lookup"><span data-stu-id="89b28-313">English</span></span></td>        
        <td><span data-ttu-id="89b28-314">en.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-314">en.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-315">en.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-315">en.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-316">Estonio</span><span class="sxs-lookup"><span data-stu-id="89b28-316">Estonian</span></span></td>
        <td><span data-ttu-id="89b28-317">et.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-317">et.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-318">Finés</span><span class="sxs-lookup"><span data-stu-id="89b28-318">Finnish</span></span></td>
        <td><span data-ttu-id="89b28-319">fi.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-319">fi.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-320">fi.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-320">fi.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="89b28-321">Francés</span><span class="sxs-lookup"><span data-stu-id="89b28-321">French</span></span></td>
        <td><span data-ttu-id="89b28-322">fr.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-322">fr.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-323">fr.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-323">fr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-324">Gallego</span><span class="sxs-lookup"><span data-stu-id="89b28-324">Galician</span></span></td>
        <td></td>
        <td><span data-ttu-id="89b28-325">gl.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-325">gl.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="89b28-326">Alemán</span><span class="sxs-lookup"><span data-stu-id="89b28-326">German</span></span></td>
        <td><span data-ttu-id="89b28-327">de.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-327">de.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-328">de.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-328">de.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-329">Griego</span><span class="sxs-lookup"><span data-stu-id="89b28-329">Greek</span></span></td>
        <td><span data-ttu-id="89b28-330">el.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-330">el.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-331">el.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-331">el.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-332">Gujarati</span><span class="sxs-lookup"><span data-stu-id="89b28-332">Gujarati</span></span></td>
        <td><span data-ttu-id="89b28-333">gu.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-333">gu.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-334">Hebreo</span><span class="sxs-lookup"><span data-stu-id="89b28-334">Hebrew</span></span></td>
        <td><span data-ttu-id="89b28-335">he.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-335">he.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-336">Hindi</span><span class="sxs-lookup"><span data-stu-id="89b28-336">Hindi</span></span></td>
        <td><span data-ttu-id="89b28-337">hi.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-337">hi.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-338">hi.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-338">hi.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-339">Húngaro</span><span class="sxs-lookup"><span data-stu-id="89b28-339">Hungarian</span></span></td>        
        <td><span data-ttu-id="89b28-340">hu.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-340">hu.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-341">hu.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-341">hu.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-342">Islandés</span><span class="sxs-lookup"><span data-stu-id="89b28-342">Icelandic</span></span></td>
        <td><span data-ttu-id="89b28-343">is.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-343">is.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-344">Indonesio (Bahasa)</span><span class="sxs-lookup"><span data-stu-id="89b28-344">Indonesian (Bahasa)</span></span></td>
        <td><span data-ttu-id="89b28-345">id.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-345">id.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-346">id.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-346">id.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-347">Irlandés</span><span class="sxs-lookup"><span data-stu-id="89b28-347">Irish</span></span></td>
        <td></td>
          <td><span data-ttu-id="89b28-348">ga.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-348">ga.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-349">Italiano</span><span class="sxs-lookup"><span data-stu-id="89b28-349">Italian</span></span></td>
        <td><span data-ttu-id="89b28-350">it.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-350">it.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-351">it.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-351">it.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-352">Japonés</span><span class="sxs-lookup"><span data-stu-id="89b28-352">Japanese</span></span></td>
        <td><span data-ttu-id="89b28-353">ja.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-353">ja.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-354">ja.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-354">ja.lucene</span></span></td>

    </tr>
    <tr>
        <td><span data-ttu-id="89b28-355">Kannada</span><span class="sxs-lookup"><span data-stu-id="89b28-355">Kannada</span></span></td>
        <td><span data-ttu-id="89b28-356">ka.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-356">ka.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-357">Coreano</span><span class="sxs-lookup"><span data-stu-id="89b28-357">Korean</span></span></td>
        <td><span data-ttu-id="89b28-358">ko.Microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-358">ko.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-359">ko.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-359">ko.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-360">Letón</span><span class="sxs-lookup"><span data-stu-id="89b28-360">Latvian</span></span></td>        
        <td><span data-ttu-id="89b28-361">lv.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-361">lv.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-362">lv.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-362">lv.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-363">Lituano</span><span class="sxs-lookup"><span data-stu-id="89b28-363">Lithuanian</span></span></td>
        <td><span data-ttu-id="89b28-364">lt.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-364">lt.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-365">Malayalam</span><span class="sxs-lookup"><span data-stu-id="89b28-365">Malayalam</span></span></td>
        <td><span data-ttu-id="89b28-366">ml.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-366">ml.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-367">Malayo (latino)</span><span class="sxs-lookup"><span data-stu-id="89b28-367">Malay (Latin)</span></span></td>
        <td><span data-ttu-id="89b28-368">ms.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-368">ms.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-369">Marathi</span><span class="sxs-lookup"><span data-stu-id="89b28-369">Marathi</span></span></td>
        <td><span data-ttu-id="89b28-370">mr.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-370">mr.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-371">Noruego</span><span class="sxs-lookup"><span data-stu-id="89b28-371">Norwegian</span></span></td>
        <td><span data-ttu-id="89b28-372">nb.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-372">nb.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-373">no.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-373">no.lucene</span></span></td>        
    </tr>
      <tr>
        <td><span data-ttu-id="89b28-374">Persa</span><span class="sxs-lookup"><span data-stu-id="89b28-374">Persian</span></span></td>
        <td></td>
        <td><span data-ttu-id="89b28-375">fa.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-375">fa.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="89b28-376">Polaco</span><span class="sxs-lookup"><span data-stu-id="89b28-376">Polish</span></span></td>
        <td><span data-ttu-id="89b28-377">pl.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-377">pl.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-378">pl.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-378">pl.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-379">Portugués (Brasil)</span><span class="sxs-lookup"><span data-stu-id="89b28-379">Portuguese (Brazil)</span></span></td>
        <td><span data-ttu-id="89b28-380">pt-Br.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-380">pt-Br.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-381">pt-Br.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-381">pt-Br.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-382">Portugués (Portugal)</span><span class="sxs-lookup"><span data-stu-id="89b28-382">Portuguese (Portugal)</span></span></td>
        <td><span data-ttu-id="89b28-383">pt-Pt.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-383">pt-Pt.microsoft</span></span></td>        
        <td><span data-ttu-id="89b28-384">pt-Pt.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-384">pt-Pt.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-385">Punjabi</span><span class="sxs-lookup"><span data-stu-id="89b28-385">Punjabi</span></span></td>
        <td><span data-ttu-id="89b28-386">pa.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-386">pa.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-387">Rumano</span><span class="sxs-lookup"><span data-stu-id="89b28-387">Romanian</span></span></td>
        <td><span data-ttu-id="89b28-388">ro.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-388">ro.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-389">ro.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-389">ro.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-390">Ruso</span><span class="sxs-lookup"><span data-stu-id="89b28-390">Russian</span></span></td>
        <td><span data-ttu-id="89b28-391">ru.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-391">ru.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-392">ru.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-392">ru.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-393">Serbio (cirílico)</span><span class="sxs-lookup"><span data-stu-id="89b28-393">Serbian (Cyrillic)</span></span></td>
        <td><span data-ttu-id="89b28-394">sr-cyrillic.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-394">sr-cyrillic.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-395">Serbio (latino)</span><span class="sxs-lookup"><span data-stu-id="89b28-395">Serbian (Latin)</span></span></td>
        <td><span data-ttu-id="89b28-396">sr-latin.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-396">sr-latin.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-397">Eslovaco</span><span class="sxs-lookup"><span data-stu-id="89b28-397">Slovak</span></span></td>
        <td><span data-ttu-id="89b28-398">sk.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-398">sk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-399">Esloveno</span><span class="sxs-lookup"><span data-stu-id="89b28-399">Slovenian</span></span></td>
        <td><span data-ttu-id="89b28-400">sl.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-400">sl.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-401">Español</span><span class="sxs-lookup"><span data-stu-id="89b28-401">Spanish</span></span></td>
        <td><span data-ttu-id="89b28-402">es.Microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-402">es.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-403">es.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-403">es.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-404">Sueco</span><span class="sxs-lookup"><span data-stu-id="89b28-404">Swedish</span></span></td>
        <td><span data-ttu-id="89b28-405">sv.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-405">sv.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-406">sv.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-406">sv.lucene</span></span></td>
    </tr>

    <tr>
        <td><span data-ttu-id="89b28-407">Tamil</span><span class="sxs-lookup"><span data-stu-id="89b28-407">Tamil</span></span></td>
        <td><span data-ttu-id="89b28-408">ta.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-408">ta.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-409">Telugu</span><span class="sxs-lookup"><span data-stu-id="89b28-409">Telugu</span></span></td>
        <td><span data-ttu-id="89b28-410">te.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-410">te.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-411">Tailandés</span><span class="sxs-lookup"><span data-stu-id="89b28-411">Thai</span></span></td>
        <td><span data-ttu-id="89b28-412">th.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-412">th.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-413">th.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-413">th.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-414">Turco</span><span class="sxs-lookup"><span data-stu-id="89b28-414">Turkish</span></span></td>
        <td><span data-ttu-id="89b28-415">tr.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-415">tr.microsoft</span></span></td>
        <td><span data-ttu-id="89b28-416">tr.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-416">tr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-417">Ucraniano</span><span class="sxs-lookup"><span data-stu-id="89b28-417">Ukrainian</span></span></td>
        <td><span data-ttu-id="89b28-418">uk.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-418">uk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-419">Urdu</span><span class="sxs-lookup"><span data-stu-id="89b28-419">Urdu</span></span></td>
        <td><span data-ttu-id="89b28-420">ur.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-420">ur.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-421">Vietnamita</span><span class="sxs-lookup"><span data-stu-id="89b28-421">Vietnamese</span></span></td>
        <td><span data-ttu-id="89b28-422">vi.microsoft</span><span class="sxs-lookup"><span data-stu-id="89b28-422">vi.microsoft</span></span></td>
        <td></td>
    </tr>
    <td colspan="3"><span data-ttu-id="89b28-423">Además, Búsqueda de Azure proporciona las configuraciones del analizador de lenguaje válido</span><span class="sxs-lookup"><span data-stu-id="89b28-423">Additionally Azure Search provides language-agnostic analyzer configurations</span></span></td>
    <tr>
        <td><span data-ttu-id="89b28-424">Plegamiento de ASCII estándar</span><span class="sxs-lookup"><span data-stu-id="89b28-424">Standard ASCII Folding</span></span></td>
        <td><span data-ttu-id="89b28-425">standardasciifolding.lucene</span><span class="sxs-lookup"><span data-stu-id="89b28-425">standardasciifolding.lucene</span></span></td>
        <td>
        <ul>
            <li><span data-ttu-id="89b28-426">Segmentación de texto Unicode (Tokenizer estándar)</span><span class="sxs-lookup"><span data-stu-id="89b28-426">Unicode text segmentation (Standard Tokenizer)</span></span></li>
            <li><span data-ttu-id="89b28-427">Filtro de plegamiento de ASCII: convierte los caracteres Unicode que no pertenecen al conjunto de los primeros 127 caracteres ASCII en sus valores equivalentes ASCII.</span><span class="sxs-lookup"><span data-stu-id="89b28-427">ASCII folding filter - converts Unicode characters that don't belong to the set of first 127 ASCII characters into their ASCII equivalents.</span></span> <span data-ttu-id="89b28-428">Esto es útil para quitar los signos diacríticos.</span><span class="sxs-lookup"><span data-stu-id="89b28-428">This is useful for removing diacritics.</span></span></li>
        </ul>
        </td>
    </tr>
</table>

<span data-ttu-id="89b28-429">Todos los analizadores con nombres anotados con <i>lucene</i> disponen de tecnología de [analizadores de idioma de Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span><span class="sxs-lookup"><span data-stu-id="89b28-429">All analyzers with names annotated with <i>lucene</i> are powered by [Apache Lucene's language analyzers](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span></span> <span data-ttu-id="89b28-430">Puede encontrar más información sobre el filtro de plegamiento de ASCII [aquí](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span><span class="sxs-lookup"><span data-stu-id="89b28-430">More information about the ASCII folding filter can be found [here](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span></span>

<span data-ttu-id="89b28-431">**Proveedores de sugerencias**</span><span class="sxs-lookup"><span data-stu-id="89b28-431">**Suggesters**</span></span>

<span data-ttu-id="89b28-432">Un `suggester` define qué campos de un índice se utilizan para admitir Autocompletar en las búsquedas.</span><span class="sxs-lookup"><span data-stu-id="89b28-432">A `suggester` defines which fields in an index are used to support auto-complete in searches.</span></span> <span data-ttu-id="89b28-433">Normalmente las cadenas de búsqueda parcial se envían a las [API de sugerencias](#Suggestions) mientras el usuario está escribiendo una consulta de búsqueda y la API devuelve un conjunto de frases sugeridas.</span><span class="sxs-lookup"><span data-stu-id="89b28-433">Typically partial search strings are sent to the [Suggestions API](#Suggestions) while the user is typing a search query, and the API returns a set of suggested phrases.</span></span> <span data-ttu-id="89b28-434">El proveedor de sugerencias que defina en el índice determina qué campos se utilizan para generar los términos de búsqueda de escritura anticipada.</span><span class="sxs-lookup"><span data-stu-id="89b28-434">A suggester that you define in the index determines which fields are used to build the type-ahead search terms.</span></span> <span data-ttu-id="89b28-435">Consulte [Proveedores de sugerencias](#Suggesters) para obtener más detalles sobre la configuración.</span><span class="sxs-lookup"><span data-stu-id="89b28-435">See [Suggesters](#Suggesters) for configuration details.</span></span>

<span data-ttu-id="89b28-436">**Perfiles de puntuación**</span><span class="sxs-lookup"><span data-stu-id="89b28-436">**Scoring profiles**</span></span>

<span data-ttu-id="89b28-437">Un `scoringProfile` define comportamientos de puntuación personalizados que permiten influir en los elementos que aparecen más arriba en los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-437">A `scoringProfile` defines custom scoring behaviors that let you influence which items appear higher in the search results.</span></span> <span data-ttu-id="89b28-438">Los perfiles de puntuación se componen de ponderaciones de campos y de funciones.</span><span class="sxs-lookup"><span data-stu-id="89b28-438">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="89b28-439">Para poder utilizarlos, especifique un perfil por nombre en la cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="89b28-439">To use them, you specify a profile by name on the query string.</span></span>

<span data-ttu-id="89b28-440">El perfil de puntuación predeterminada funciona en segundo plano para calcular un resultado de búsqueda para todos los elementos de un conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="89b28-440">A default scoring profile operates behind the scenes to compute a search score for every item in a result set.</span></span> <span data-ttu-id="89b28-441">Puede usar un perfil de puntuación interno y sin nombre.</span><span class="sxs-lookup"><span data-stu-id="89b28-441">You can use the internal, unnamed scoring profile.</span></span> <span data-ttu-id="89b28-442">Como alternativa, establezca `defaultScoringProfile` para usar un perfil personalizado como valor predeterminado, al que se invoca cuando no se especifica un perfil personalizado en la cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="89b28-442">Alternatively, set `defaultScoringProfile` to use a custom profile as the default, invoked whenever a custom profile is not specified on the query string.</span></span>

<span data-ttu-id="89b28-443">Consulte [Adición de perfiles de puntuación a un índice de búsqueda (API de REST de servicio Búsqueda de Azure)](search-api-scoring-profiles-2015-02-28-preview.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="89b28-443">See [Add scoring profiles to a search index (Azure Search Service REST API)](search-api-scoring-profiles-2015-02-28-preview.md) for details.</span></span>

<span data-ttu-id="89b28-444">**Opciones de CORS**</span><span class="sxs-lookup"><span data-stu-id="89b28-444">**CORS Options**</span></span>

<span data-ttu-id="89b28-445">Javascript del lado cliente no puede llamar a las API de forma predeterminada debido a que el explorador evitará todas las solicitudes entre orígenes.</span><span class="sxs-lookup"><span data-stu-id="89b28-445">Client-side Javascript cannot call any APIs by default since the browser will prevent all cross-origin requests.</span></span> <span data-ttu-id="89b28-446">Habilite CORS (uso compartido recursos entre orígenes) estableciendo el atributo `corsOptions` para que permita consultas de origen cruzado en su índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-446">Enable CORS (Cross-Origin Resource Sharing) by setting the `corsOptions` attribute to allow cross-origin queries to your index.</span></span> <span data-ttu-id="89b28-447">Tenga en cuenta que solamente las API de consulta admiten CORS por motivos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="89b28-447">Note that only query APIs support CORS for security reasons.</span></span> <span data-ttu-id="89b28-448">Se pueden establecer las opciones siguientes para CORS:</span><span class="sxs-lookup"><span data-stu-id="89b28-448">The following options can be set for CORS:</span></span>

* <span data-ttu-id="89b28-449">`allowedOrigins` (obligatorio): se trata de una lista de orígenes a los que se le concederá acceso a su índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-449">`allowedOrigins` (required): This is a list of origins that will be granted access to your index.</span></span> <span data-ttu-id="89b28-450">Esto significa que cualquier código Javascript que se suministre desde esos orígenes podrá consultar el índice (suponiendo que proporcione la clave de API correcta).</span><span class="sxs-lookup"><span data-stu-id="89b28-450">This means that any Javascript code served from those origins will be allowed to query your index (assuming it provides the correct API key).</span></span> <span data-ttu-id="89b28-451">Cada origen suele ser de formato `protocol://fully-qualified-domain-name:port` , aunque a menudo se omite el puerto.</span><span class="sxs-lookup"><span data-stu-id="89b28-451">Each origin is typically of the form `protocol://fully-qualified-domain-name:port` although the port is often omitted.</span></span> <span data-ttu-id="89b28-452">Consulte [este artículo](http://go.microsoft.com/fwlink/?LinkId=330822) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="89b28-452">See [this article](http://go.microsoft.com/fwlink/?LinkId=330822) for more details.</span></span>
  * <span data-ttu-id="89b28-453">Si desea permitir el acceso a todos los orígenes, incluya `*` como elemento único en la matriz `allowedOrigins`.</span><span class="sxs-lookup"><span data-stu-id="89b28-453">If you want to allow access to all origins, include `*` as a single item in the `allowedOrigins` array.</span></span> <span data-ttu-id="89b28-454">Tenga en cuenta que **esta no es una práctica recomendada para los servicios de búsqueda de producción.**</span><span class="sxs-lookup"><span data-stu-id="89b28-454">Note that **this is not recommended practice for production search services.**</span></span> <span data-ttu-id="89b28-455">Sin embargo, puede ser útil para el desarrollo o con fines de depuración.</span><span class="sxs-lookup"><span data-stu-id="89b28-455">However, it may be useful for development or debugging purposes.</span></span>
* <span data-ttu-id="89b28-456">`maxAgeInSeconds` (opcional): los exploradores usan este valor para determinar la duración (en segundos) para almacenar en la memoria caché las respuestas preparatorias de CORS.</span><span class="sxs-lookup"><span data-stu-id="89b28-456">`maxAgeInSeconds` (optional): Browsers use this value to determine the duration (in seconds) to cache CORS preflight responses.</span></span> <span data-ttu-id="89b28-457">Esto debe ser un entero no negativo.</span><span class="sxs-lookup"><span data-stu-id="89b28-457">This must be a non-negative integer.</span></span> <span data-ttu-id="89b28-458">Cuanto mayor sea este valor es, mejor será el rendimiento, pero más tiempo tardarán en surtir efecto los cambios en la directiva CORS.</span><span class="sxs-lookup"><span data-stu-id="89b28-458">The larger this value is, the better performance will be, but the longer it will take for CORS policy changes to take effect.</span></span> <span data-ttu-id="89b28-459">Si no se establece, se usará una duración predeterminada de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="89b28-459">If it is not set, a default duration of 5 minutes will be used.</span></span>

<span data-ttu-id="89b28-460"><a name="CreateUpdateIndexExample"></a>
**Ejemplo de cuerpo de solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-460"><a name="CreateUpdateIndexExample"></a>
**Request Body Example**</span></span>

    {
      "name": "hotels",  
      "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String"},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean"},
        {"name": "smokingAllowed", "type": "Edm.Boolean"},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["hotelName"]
        }
      ]
    }

<span data-ttu-id="89b28-461">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="89b28-461">**Response**</span></span>

<span data-ttu-id="89b28-462">Para obtener una solicitud correcta: "201 Creado".</span><span class="sxs-lookup"><span data-stu-id="89b28-462">For a successful request: "201 Created".</span></span>

<span data-ttu-id="89b28-463">De forma predeterminada, el cuerpo de la respuesta contendrá el JSON de la definición del índice que se creó.</span><span class="sxs-lookup"><span data-stu-id="89b28-463">By default the response body will contain the JSON for the index definition that was created.</span></span> <span data-ttu-id="89b28-464">Si se establece el encabezado de la solicitud `Prefer` en `return=minimal`, el cuerpo de respuesta quedará vacío y el código de estado correcto será "204 Sin contenido" en lugar de "201 creado".</span><span class="sxs-lookup"><span data-stu-id="89b28-464">If the `Prefer` request header is set to `return=minimal`, the response body will be empty and the success status code will be "204 No Content" instead of "201 Created".</span></span> <span data-ttu-id="89b28-465">Esto es cierto independientemente de si se utiliza PUT o POST para crear el índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-465">This is true regardless of whether PUT or POST was used to create the index.</span></span>

<span data-ttu-id="89b28-466">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="89b28-466">**Remarks**</span></span>

<span data-ttu-id="89b28-467">Actualmente, hay compatibilidad limitada para las actualizaciones del esquema de índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-467">Currently, there is limited support for index schema updates.</span></span> <span data-ttu-id="89b28-468">Actualmente no se admiten las actualizaciones del esquema que requieran volver a indexar, como el cambio de tipos de campo.</span><span class="sxs-lookup"><span data-stu-id="89b28-468">Any schema updates that would require re-indexing such as changing field types are not currently supported.</span></span> <span data-ttu-id="89b28-469">Aunque los campos existentes no se pueden modificar ni eliminar, los campos nuevos pueden agregarse a un índice existente en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="89b28-469">Although existing fields cannot be changed or deleted, new fields can be added to an existing index at any time.</span></span> <span data-ttu-id="89b28-470">Al agregar un nuevo campo, todos los documentos existentes del índice tendrán un valor null para ese campo automáticamente.</span><span class="sxs-lookup"><span data-stu-id="89b28-470">When a new field is added, all existing documents in the index will automatically have a null value for that field.</span></span> <span data-ttu-id="89b28-471">No se consumirá espacio de almacenamiento adicional hasta que se agreguen nuevos documentos al índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-471">No additional storage space will be consumed until new documents are added to the index.</span></span>

<a name="Suggesters"></a>

## <a name="suggesters"></a><span data-ttu-id="89b28-472">Proveedores de sugerencias</span><span class="sxs-lookup"><span data-stu-id="89b28-472">Suggesters</span></span>
<span data-ttu-id="89b28-473">La característica de sugerencias de Búsqueda de Azure es una capacidad de consulta de escritura anticipada o autocompletar, que proporciona una lista de posibles términos de búsqueda en respuesta a las entradas de cadenas parciales especificadas en un cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-473">The suggestions feature in Azure Search is a type-ahead or auto-complete query capability, providing a list of potential search terms in response to partial string inputs entered into a search box.</span></span> <span data-ttu-id="89b28-474">Probablemente haya observado sugerencias de consulta al utilizar los motores de búsqueda web comerciales: si se escribe ".NET" en Bing, se genera una lista de términos para ".NET 4.5", ".NET Framework 3.5", y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="89b28-474">You've probably noticed query suggestions when using commercial web search engines: typing ".NET" in Bing produces a list of terms for ".NET 4.5", ".NET Framework 3.5", and so forth.</span></span> <span data-ttu-id="89b28-475">Cuando se utiliza la API de REST del servicio Búsqueda, la implementación de sugerencias en una aplicación de Búsqueda de Azure personalizada requiere lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="89b28-475">When using the Search service REST API, implementing suggestions in a custom Azure Search application requires the following:</span></span>

* <span data-ttu-id="89b28-476">Habilite las sugerencias agregando una construcción de **proveedor de sugerencias** en el índice, lo que proporciona el nombre, el modo de búsqueda y una lista de campos para los que se requiere la escritura anticipada.</span><span class="sxs-lookup"><span data-stu-id="89b28-476">Enable suggestions by adding a **suggester** construction in your index, giving the name, search mode, and a list of fields for which type-ahead is invoked.</span></span> <span data-ttu-id="89b28-477">Por ejemplo, si especifica "nombreCiudad" como un campo de origen, al escribir la cadena de búsqueda parcial de "Sea", dará como resultado "Seattle", "Seaside" y "Seatac" (las tres son nombres de ciudades reales) ofrecidos como sugerencias de consulta para el usuario.</span><span class="sxs-lookup"><span data-stu-id="89b28-477">For example, if you specify "cityName" as a source field, typing a partial search string of "Sea" will result in "Seattle", "Seaside", and "Seatac" (all three are actual city names) offered up as query suggestions to the user.</span></span>
* <span data-ttu-id="89b28-478">Invoque sugerencias llamando a la [API de sugerencias](#Suggestions) en el código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="89b28-478">Invoke suggestions by calling the [Suggestions API](#Suggestions) in your application code.</span></span> <span data-ttu-id="89b28-479">Normalmente las cadenas de búsqueda parcial se envían al servicio mientras el usuario está escribiendo una consulta de búsqueda y la API devuelve un conjunto de frases sugeridas.</span><span class="sxs-lookup"><span data-stu-id="89b28-479">Typically partial search strings are sent to the service while the user is typing a search query, and this API returns a set of suggested phrases.</span></span>

<span data-ttu-id="89b28-480">Este artículo explica cómo configurar un **proveedor de sugerencias**.</span><span class="sxs-lookup"><span data-stu-id="89b28-480">This article explains how to configure a **suggester**.</span></span> <span data-ttu-id="89b28-481">También debe revisar la [API de sugerencias](#Suggestions) para obtener más información sobre cómo se utiliza un proveedor de sugerencias.</span><span class="sxs-lookup"><span data-stu-id="89b28-481">You should also review the [Suggestions API](#Suggestions) for details on how a suggester is used.</span></span>

<span data-ttu-id="89b28-482">**Uso**</span><span class="sxs-lookup"><span data-stu-id="89b28-482">**Usage**</span></span>

<span data-ttu-id="89b28-483">`Suggesters` se crean en el índice y funcionan mejor cuando se usan para sugerir documentos específicos en lugar de términos o frases flexibles.</span><span class="sxs-lookup"><span data-stu-id="89b28-483">`Suggesters` are created in the index and work best when used to suggest specific documents rather than loose terms or phrases.</span></span> <span data-ttu-id="89b28-484">Los campos de mejores candidatos son títulos, nombres y demás frases relativamente cortas que pueden identificar un elemento.</span><span class="sxs-lookup"><span data-stu-id="89b28-484">The best candidate fields are titles, names, and other relatively short phrases that can identify an item.</span></span> <span data-ttu-id="89b28-485">Los campos repetitivos son menos efectivos, por ejemplo, las categorías y etiquetas, o campos muy largos como campos de descripciones o comentarios.</span><span class="sxs-lookup"><span data-stu-id="89b28-485">Less effective are repetitive fields, such as categories and tags, or very long fields such as descriptions or comments fields.</span></span>

<span data-ttu-id="89b28-486">Como parte de la definición del índice puede agregar un único proveedor de sugerencias a la colección `suggesters` .</span><span class="sxs-lookup"><span data-stu-id="89b28-486">As part of the index definition, you can add a single suggester to the `suggesters` collection.</span></span> <span data-ttu-id="89b28-487">Las propiedades que definen a un proveedor de sugerencias se incluyen las siguientes:</span><span class="sxs-lookup"><span data-stu-id="89b28-487">Properties that define a suggester include the following:</span></span>

* <span data-ttu-id="89b28-488">`name`: el nombre del proveedor de sugerencias.</span><span class="sxs-lookup"><span data-stu-id="89b28-488">`name`: The name of the suggester.</span></span> <span data-ttu-id="89b28-489">Use el nombre del proveedor de sugerencias para llamar a la API de `suggest` .</span><span class="sxs-lookup"><span data-stu-id="89b28-489">You use the name of the suggester when calling the `suggest` API.</span></span>
* <span data-ttu-id="89b28-490">`searchMode`: la estrategia que se usa para buscar las frases candidatas.</span><span class="sxs-lookup"><span data-stu-id="89b28-490">`searchMode`: The strategy used to search for candidate phrases.</span></span> <span data-ttu-id="89b28-491">El único modo que se admite actualmente es `analyzingInfixMatching`, que establece una correspondencia flexible de frases al principio o en medio de las oraciones.</span><span class="sxs-lookup"><span data-stu-id="89b28-491">The only mode currently supported is `analyzingInfixMatching`, which performs flexible matching of phrases at the beginning or in the middle of sentences.</span></span>
* <span data-ttu-id="89b28-492">`sourceFields`: lista de uno o más campos que son el origen del contenido para obtener sugerencias.</span><span class="sxs-lookup"><span data-stu-id="89b28-492">`sourceFields`: A list of one or more fields that are the source of the content for suggestions.</span></span> <span data-ttu-id="89b28-493">Solo los campos de tipo `Edm.String` y `Collection(Edm.String)` pueden ser orígenes para obtener sugerencias.</span><span class="sxs-lookup"><span data-stu-id="89b28-493">Only fields of type `Edm.String` and `Collection(Edm.String)` may be sources for suggestions.</span></span> <span data-ttu-id="89b28-494">Solo se pueden usar los campos que no tienen un analizador de lenguaje personalizado establecido.</span><span class="sxs-lookup"><span data-stu-id="89b28-494">Only fields that don't have a custom language analyzer set can be used.</span></span>

<span data-ttu-id="89b28-495">**Ejemplo de proveedor de sugerencias**</span><span class="sxs-lookup"><span data-stu-id="89b28-495">**Suggester Example**</span></span>

<span data-ttu-id="89b28-496">Un proveedor de sugerencias forma parte del índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-496">A suggester is part of the index.</span></span> <span data-ttu-id="89b28-497">Solo un proveedor de sugerencias puede existir en la colección `suggesters` en la versión actual, junto con la colección de campos y `scoringProfiles`.</span><span class="sxs-lookup"><span data-stu-id="89b28-497">Only one suggester can exist in the `suggesters` collection in the current version, alongside the fields collection and `scoringProfiles`.</span></span>

        {
          "name": "hotels",
          "fields": [
             . . .
           ],
          "suggesters": [
            {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields: ["hotelName", "category"]
            }
          ],
          "scoringProfiles": [
             . . .
          ]
        }

> [!NOTE]
> <span data-ttu-id="89b28-498">Si ha usado la versión de vista previa pública de Búsqueda de Azure, `suggesters` sustituirá a una propiedad booleana anterior (`"suggestions": false`) que solo admitía sugerencias de prefijos para cadenas cortas (3-25 caracteres).</span><span class="sxs-lookup"><span data-stu-id="89b28-498">If you used the public preview version of Azure Search, `suggesters` replaces an older boolean property (`"suggestions": false`) that only supported prefix suggestions for short strings (3-25 characters).</span></span> <span data-ttu-id="89b28-499">Su reemplazo, `suggesters`, admite la detección de coincidencias de infijos que encuentra términos coincidentes al principio o en medio del contenido del campo, con una mejor tolerancia a errores en las cadenas de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-499">Its replacement, `suggesters`, supports infix matching that finds matching terms at the beginning or in the middle of field content, with better tolerance for mistakes in search strings.</span></span> <span data-ttu-id="89b28-500">A partir de la versión disponible con carácter general, esta es ahora la única implementación de la API de sugerencias.</span><span class="sxs-lookup"><span data-stu-id="89b28-500">Starting with the generally available release, this is now the only implementation of the suggestions API.</span></span> <span data-ttu-id="89b28-501">La propiedad `suggestions` anterior que se introdujo en `api-version=2014-07-31-Preview` continúa funcionando en esa versión, pero no está operativa en la versión `2015-02-28` o posteriores de Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="89b28-501">The older `suggestions` property that was introduced in `api-version=2014-07-31-Preview` continues to work in that version, but is not operational in the `2015-02-28` or later versions of Azure Search.</span></span>
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a><span data-ttu-id="89b28-502">Actualizar índice</span><span class="sxs-lookup"><span data-stu-id="89b28-502">Update Index</span></span>
<span data-ttu-id="89b28-503">Puede actualizar un índice existente en Búsqueda de Azure mediante una solicitud HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="89b28-503">You can update an existing index within Azure Search using an HTTP PUT request.</span></span> <span data-ttu-id="89b28-504">Las actualizaciones pueden incluir agregar nuevos campos al esquema existente, modificar las opciones de CORS y modificar perfiles de puntuación.</span><span class="sxs-lookup"><span data-stu-id="89b28-504">Updates can include adding new fields to the existing schema, modifying CORS options, and modifying scoring profiles.</span></span> <span data-ttu-id="89b28-505">Consulte [Agregar perfiles de puntuación](https://msdn.microsoft.com/library/azure/dn798928.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="89b28-505">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> <span data-ttu-id="89b28-506">Especifique el nombre del índice que se va a actualizar en el URI de solicitud:</span><span class="sxs-lookup"><span data-stu-id="89b28-506">You specify the name of the index to update on the request URI:</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="89b28-507">**Importante:** la compatibilidad con las actualizaciones del esquema de índice se limita a las operaciones que no requieren volver a generar el índice de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-507">**Important:** Support for index schema updates is limited to operations that don't require rebuilding the search index.</span></span> <span data-ttu-id="89b28-508">Actualmente no se admiten las actualizaciones del esquema que requieran volver a indexar, como el cambio de tipos de campo.</span><span class="sxs-lookup"><span data-stu-id="89b28-508">Any schema updates that would require re-indexing, such as changing field types, are not currently supported.</span></span> <span data-ttu-id="89b28-509">Pueden agregarse nuevos campos en cualquier momento, aunque no se pueden modificar ni eliminar los campos existentes.</span><span class="sxs-lookup"><span data-stu-id="89b28-509">New fields can be added at any time, although existing fields cannot be changed or deleted.</span></span> <span data-ttu-id="89b28-510">Lo mismo se aplica a `suggesters`.</span><span class="sxs-lookup"><span data-stu-id="89b28-510">The same applies to `suggesters`.</span></span> <span data-ttu-id="89b28-511">Es posible agregar nuevos campos a un proveedor de sugerencias en el momento en que se agregan los campos, pero no se puede quitar campos de `suggesters` y no se pueden agregar campos existentes a `suggesters`.</span><span class="sxs-lookup"><span data-stu-id="89b28-511">New fields may be added to a suggester at the time the fields are added, but fields cannot be removed from `suggesters` and existing fields cannot be added to `suggesters`.</span></span>

<span data-ttu-id="89b28-512">Al agregar un nuevo campo a un índice, todos los documentos existentes en el índice tendrá un valor null para ese campo automáticamente.</span><span class="sxs-lookup"><span data-stu-id="89b28-512">When adding a new field to an index, all existing documents in the index will automatically have a null value for that field.</span></span> <span data-ttu-id="89b28-513">No se consumirá espacio de almacenamiento adicional hasta que se agreguen nuevos documentos al índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-513">No additional storage space will be consumed until new documents are added to the index.</span></span>

<span data-ttu-id="89b28-514">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-514">**Request**</span></span>

<span data-ttu-id="89b28-515">HTTPS es necesario para todas las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-515">HTTPS is required for all service requests.</span></span> <span data-ttu-id="89b28-516">La solicitud **Actualizar índice** se construye utilizando HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="89b28-516">The **Update Index** request is constructed using HTTP PUT.</span></span> <span data-ttu-id="89b28-517">Con PUT, el nombre del índice es parte de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="89b28-517">With PUT, the index name is part of the URL.</span></span> <span data-ttu-id="89b28-518">Si el índice no existe, se crea.</span><span class="sxs-lookup"><span data-stu-id="89b28-518">If the index doesn't exist, it is created.</span></span> <span data-ttu-id="89b28-519">Si ya existe el índice, se actualiza a la nueva definición.</span><span class="sxs-lookup"><span data-stu-id="89b28-519">If the index already exists, it is updated to the new definition.</span></span>

<span data-ttu-id="89b28-520">El nombre del índice debe estar en minúsculas, comenzar por una letra o un número, no tener ninguna barra o punto y tener menos de 128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="89b28-520">The index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="89b28-521">Después de iniciar el nombre del índice por una letra o un número, el resto del nombre puede incluir cualquier letra, número y guiones, siempre que los guiones no aparezcan de manera consecutiva.</span><span class="sxs-lookup"><span data-stu-id="89b28-521">After starting the index name with a letter or number, the rest of the name can include any letter, number and dashes, as long as the dashes are not consecutive.</span></span>

<span data-ttu-id="89b28-522">`api-version=[string]` (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="89b28-522">`api-version=[string]` (required).</span></span> <span data-ttu-id="89b28-523">La versión de vista previa es `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="89b28-523">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="89b28-524">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.</span><span class="sxs-lookup"><span data-stu-id="89b28-524">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="89b28-525">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-525">**Request Headers**</span></span>

<span data-ttu-id="89b28-526">En la lista siguiente se describen los encabezados de solicitud obligatorios y opcionales.</span><span class="sxs-lookup"><span data-stu-id="89b28-526">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="89b28-527">`Content-Type`: obligatorio.</span><span class="sxs-lookup"><span data-stu-id="89b28-527">`Content-Type`: Required.</span></span> <span data-ttu-id="89b28-528">Establézcalo en `application/json`</span><span class="sxs-lookup"><span data-stu-id="89b28-528">Set this to `application/json`</span></span>
* <span data-ttu-id="89b28-529">`api-key`: obligatorio.</span><span class="sxs-lookup"><span data-stu-id="89b28-529">`api-key`: Required.</span></span> <span data-ttu-id="89b28-530">`api-key` se usa para autenticar la solicitud en su servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-530">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="89b28-531">Es un valor de cadena único para el servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-531">It is a string value, unique to your service.</span></span> <span data-ttu-id="89b28-532">La solicitud **Actualizar índice** debe incluir un encabezado `api-key` establecido en su clave de administración (en lugar de una clave de consulta).</span><span class="sxs-lookup"><span data-stu-id="89b28-532">The **Update Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="89b28-533">También necesitará el nombre del servicio para construir la dirección URL de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="89b28-533">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="89b28-534">Puede obtener el nombre de servicio y `api-key` desde el panel de servicio en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="89b28-534">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="89b28-535">Consulte [Crear un servicio de Búsqueda de Azure en el portal](search-create-service-portal.md) para obtener ayuda sobre la navegación en páginas.</span><span class="sxs-lookup"><span data-stu-id="89b28-535">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="89b28-536">**Sintaxis del cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-536">**Request Body Syntax**</span></span>

<span data-ttu-id="89b28-537">Al actualizar un índice existente, el cuerpo debe incluir la definición de esquema original, además de los nuevos campos que se van a agregar, así como los perfiles de puntuación modificados, los proveedores de sugerencias y las opciones de CORS, si existen.</span><span class="sxs-lookup"><span data-stu-id="89b28-537">When updating an existing index, the body must include the original schema definition, plus the new fields you are adding, as well as the modified scoring profiles, suggesters and CORS options, if any.</span></span> <span data-ttu-id="89b28-538">Si no va a modificar los perfiles de puntuación y las opciones de CORS, deberá incluir los originales de cuando se creó el índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-538">If you are not modifying the scoring profiles and CORS options, you must include the originals from when the index was created.</span></span> <span data-ttu-id="89b28-539">En general, el mejor patrón que se puede utilizar para las actualizaciones consiste en recuperar la definición del índice con un comando GET, modificarlo y luego actualizarlo con PUT.</span><span class="sxs-lookup"><span data-stu-id="89b28-539">In general the best pattern to use for updates is to retrieve the index definition with a GET, modify it, then update it with PUT.</span></span>

<span data-ttu-id="89b28-540">A continuación se reproduce la sintaxis del esquema usada para crear un índice por motivos de comodidad.</span><span class="sxs-lookup"><span data-stu-id="89b28-540">The schema syntax used to create an index is reproduced here for convenience.</span></span> <span data-ttu-id="89b28-541">Consulte [Crear índice](#CreateIndex) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="89b28-541">See [Create Index](#CreateIndex) for more details.</span></span>

    {
      "name": (optional) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false, 
          "analyzer": "name of the analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of the search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of the indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in the future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies to searchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading to now over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter to be passed in queries to use as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (the distance in kilometers from the reference location where the boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter to be passed in queries to specify list of tags to compare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }


<span data-ttu-id="89b28-542">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="89b28-542">**Response**</span></span>

<span data-ttu-id="89b28-543">Para obtener una solicitud correcta: "204 Sin contenido".</span><span class="sxs-lookup"><span data-stu-id="89b28-543">For a successful request: "204 No Content".</span></span>

<span data-ttu-id="89b28-544">De forma predeterminada, el cuerpo de respuesta estará vacío.</span><span class="sxs-lookup"><span data-stu-id="89b28-544">By default the response body will be empty.</span></span> <span data-ttu-id="89b28-545">No obstante, si el encabezado de la solicitud `Prefer` está establecido en `return=representation`, el cuerpo de la respuesta contendrá el JSON de la definición del índice que se actualizó.</span><span class="sxs-lookup"><span data-stu-id="89b28-545">However, if the `Prefer` request header is set to `return=representation`, the response body will contain the JSON for the index definition that was updated.</span></span> <span data-ttu-id="89b28-546">En este caso, el código de estado correcto será "200 Correcto".</span><span class="sxs-lookup"><span data-stu-id="89b28-546">In this case, the success status code will be "200 OK".</span></span>

<span data-ttu-id="89b28-547">**Actualización de definiciones de índices con analizadores personalizados**</span><span class="sxs-lookup"><span data-stu-id="89b28-547">**Updating index definition with custom analyzers**</span></span>

<span data-ttu-id="89b28-548">Una vez definido un analizador, un tokenizador o un filtro de caracteres, no se puede modificar.</span><span class="sxs-lookup"><span data-stu-id="89b28-548">Once an analyzer, a tokenizer, a token filter or a char filter is defined, it cannot be modified.</span></span> <span data-ttu-id="89b28-549">Se pueden agregar unos nuevos a un índice existente solo si la marca de `allowIndexDowntime` está establecida en true en la solicitud de actualización del índice:</span><span class="sxs-lookup"><span data-stu-id="89b28-549">New ones can be added to an existing index only if the `allowIndexDowntime` flag is set to true in the index update request:</span></span> 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

<span data-ttu-id="89b28-550">Tenga en cuenta que esta operación hará que el índice pase a estar sin conexión durante al menos unos segundos, de modo que las solicitudes de indexación y consulta darán error.</span><span class="sxs-lookup"><span data-stu-id="89b28-550">Note that this operation will put your index offline for at least a few seconds, causing your indexing and query requests to fail.</span></span> <span data-ttu-id="89b28-551">El rendimiento y la disponibilidad de escritura del índice pueden ser desiguales durante varios minutos después de que se actualice el índice, o durante más tiempo en el caso de índices muy grandes.</span><span class="sxs-lookup"><span data-stu-id="89b28-551">Performance and write availability of the index can be impaired for several minutes after the index is updated, or longer for very large indexes.</span></span>

<a name="ListIndexes"></a>

## <a name="list-indexes"></a><span data-ttu-id="89b28-552">Índices de la lista</span><span class="sxs-lookup"><span data-stu-id="89b28-552">List Indexes</span></span>
<span data-ttu-id="89b28-553">La operación **Índices de la lista** devuelve una lista de los índices que se encuentran actualmente en el servicio de Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="89b28-553">The **List Indexes** operation returns a list of the indexes currently in your Azure Search service.</span></span>

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="89b28-554">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-554">**Request**</span></span>

<span data-ttu-id="89b28-555">HTTPS es necesario para todas las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-555">HTTPS is required for all service requests.</span></span> <span data-ttu-id="89b28-556">La solicitud **Índices de la lista** puede crearse mediante el método GET.</span><span class="sxs-lookup"><span data-stu-id="89b28-556">The **List Indexes** request can be constructed using the GET method.</span></span>

<span data-ttu-id="89b28-557">`api-version=[string]` (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="89b28-557">`api-version=[string]` (required).</span></span> <span data-ttu-id="89b28-558">La versión de vista previa es `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="89b28-558">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="89b28-559">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.</span><span class="sxs-lookup"><span data-stu-id="89b28-559">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="89b28-560">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-560">**Request Headers**</span></span>

<span data-ttu-id="89b28-561">En la lista siguiente se describen los encabezados de solicitud obligatorios y opcionales.</span><span class="sxs-lookup"><span data-stu-id="89b28-561">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="89b28-562">`api-key`: obligatorio.</span><span class="sxs-lookup"><span data-stu-id="89b28-562">`api-key`: Required.</span></span> <span data-ttu-id="89b28-563">`api-key` se usa para autenticar la solicitud en su servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-563">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="89b28-564">Es un valor de cadena único para el servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-564">It is a string value, unique to your service.</span></span> <span data-ttu-id="89b28-565">La solicitud **Índices de la lista** debe incluir un `api-key` establecido en una clave de administración (en lugar de una clave de consulta).</span><span class="sxs-lookup"><span data-stu-id="89b28-565">The **List Indexes** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="89b28-566">También necesitará el nombre del servicio para construir la dirección URL de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="89b28-566">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="89b28-567">Puede obtener el nombre de servicio y `api-key` desde el panel de servicio en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="89b28-567">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="89b28-568">Consulte [Crear un servicio de Búsqueda de Azure en el portal](search-create-service-portal.md) para obtener ayuda sobre la navegación en páginas.</span><span class="sxs-lookup"><span data-stu-id="89b28-568">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="89b28-569">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-569">**Request Body**</span></span>

<span data-ttu-id="89b28-570">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="89b28-570">None.</span></span>

<span data-ttu-id="89b28-571">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="89b28-571">**Response**</span></span>

<span data-ttu-id="89b28-572">Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.</span><span class="sxs-lookup"><span data-stu-id="89b28-572">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="89b28-573">A continuación se proporciona un cuerpo de respuesta de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="89b28-573">Here is an example response body:</span></span>

    {
      "value": [
        {
          "name": "Books",
          "fields": [
            {"name": "ISBN", ...},
            ...
          ]
        },
        {
          "name": "Games",
          ...
        },
        ...
      ]
    }

<span data-ttu-id="89b28-574">Tenga en cuenta que puede filtrar la respuesta a solo las propiedades que le interesan.</span><span class="sxs-lookup"><span data-stu-id="89b28-574">Note that you can filter the response down to just the properties you're interested in.</span></span> <span data-ttu-id="89b28-575">Por ejemplo, si solamente desea una lista de los nombres de índices, use la opción de consulta OData `$select` :</span><span class="sxs-lookup"><span data-stu-id="89b28-575">For example, if you want only a list of index names, use the OData `$select` query option:</span></span>

    GET /indexes?api-version=2015-02-28-Preview&$select=name

<span data-ttu-id="89b28-576">En este caso, la respuesta del ejemplo anterior podría aparecer como sigue:</span><span class="sxs-lookup"><span data-stu-id="89b28-576">In this case, the response from the above example would appear as follows:</span></span>

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

<span data-ttu-id="89b28-577">Se trata de una técnica útil para ahorrar ancho de banda, si tiene una gran cantidad de índices en el servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-577">This is a useful technique to save bandwidth if you have a lot of indexes in your Search service.</span></span>

<a name="GetIndex"></a>

## <a name="get-index"></a><span data-ttu-id="89b28-578">Obtener índice</span><span class="sxs-lookup"><span data-stu-id="89b28-578">Get Index</span></span>
<span data-ttu-id="89b28-579">La operación **Obtener índice** obtiene la definición del índice de Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="89b28-579">The **Get Index** operation gets the index definition from Azure Search.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="89b28-580">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-580">**Request**</span></span>

<span data-ttu-id="89b28-581">HTTPS es necesario para las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-581">HTTPS is required for service requests.</span></span> <span data-ttu-id="89b28-582">La solicitud **Obtener índices** puede crearse mediante el método GET.</span><span class="sxs-lookup"><span data-stu-id="89b28-582">The **Get Index** request can be constructed using the GET method.</span></span>

<span data-ttu-id="89b28-583">El [nombre de índice] del URI de la solicitud especifica qué índice se va a obtener de la colección de índices.</span><span class="sxs-lookup"><span data-stu-id="89b28-583">The [index name] in the request URI specifies which index to return from the indexes collection.</span></span>

<span data-ttu-id="89b28-584">`api-version=[string]` (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="89b28-584">`api-version=[string]` (required).</span></span> <span data-ttu-id="89b28-585">La versión de vista previa es `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="89b28-585">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="89b28-586">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.</span><span class="sxs-lookup"><span data-stu-id="89b28-586">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="89b28-587">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-587">**Request Headers**</span></span>

<span data-ttu-id="89b28-588">En la lista siguiente se describen los encabezados de solicitud obligatorios y opcionales.</span><span class="sxs-lookup"><span data-stu-id="89b28-588">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="89b28-589">`api-key`: `api-key` se usa para autenticar la solicitud en su servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-589">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="89b28-590">Es un valor de cadena único para el servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-590">It is a string value, unique to your service.</span></span> <span data-ttu-id="89b28-591">La solicitud **Obtener índice** debe incluir un `api-key` establecido en una clave de administración (en lugar de una clave de consulta).</span><span class="sxs-lookup"><span data-stu-id="89b28-591">The **Get Index** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="89b28-592">También necesitará el nombre del servicio para construir la dirección URL de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="89b28-592">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="89b28-593">Puede obtener el nombre de servicio y `api-key` desde el panel de servicio en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="89b28-593">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="89b28-594">Consulte [Crear un servicio de Búsqueda de Azure en el portal](search-create-service-portal.md) para obtener ayuda sobre la navegación en páginas.</span><span class="sxs-lookup"><span data-stu-id="89b28-594">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="89b28-595">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-595">**Request Body**</span></span>

<span data-ttu-id="89b28-596">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="89b28-596">None.</span></span>

<span data-ttu-id="89b28-597">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="89b28-597">**Response**</span></span>

<span data-ttu-id="89b28-598">Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.</span><span class="sxs-lookup"><span data-stu-id="89b28-598">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="89b28-599">Consulte el JSON de ejemplo en [creación y actualización de un índice](#CreateUpdateIndexExample) para obtener un ejemplo de la carga de respuesta.</span><span class="sxs-lookup"><span data-stu-id="89b28-599">See the example JSON in [Creating and Updating an Index](#CreateUpdateIndexExample) for an example of the response payload.</span></span>

<a name="DeleteIndex"></a>

## <a name="delete-index"></a><span data-ttu-id="89b28-600">Eliminar índice</span><span class="sxs-lookup"><span data-stu-id="89b28-600">Delete Index</span></span>
<span data-ttu-id="89b28-601">La operación **Eliminar índice** quita un índice y los documentos asociados del servicio de Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="89b28-601">The **Delete Index** operation removes an index and associated documents from your Azure Search service.</span></span> <span data-ttu-id="89b28-602">Puede obtener el nombre del índice del panel de servicio en el Portal de Azure o de la API.</span><span class="sxs-lookup"><span data-stu-id="89b28-602">You can get the index name from the service dashboard in the Azure portal, or from the API.</span></span> <span data-ttu-id="89b28-603">Consulte [Índices de la lista](#ListIndexes) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="89b28-603">See [List Indexes](#ListIndexes) for details.</span></span>

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="89b28-604">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-604">**Request**</span></span>

<span data-ttu-id="89b28-605">HTTPS es necesario para las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-605">HTTPS is required for service requests.</span></span> <span data-ttu-id="89b28-606">La solicitud **Eliminar índice** puede crearse mediante el método DELETE.</span><span class="sxs-lookup"><span data-stu-id="89b28-606">The **Delete Index** request can be constructed using the DELETE method.</span></span>

<span data-ttu-id="89b28-607">El [nombre de índice] del URI de la solicitud especifica qué índice se va a eliminar de la colección de índices.</span><span class="sxs-lookup"><span data-stu-id="89b28-607">The [index name] in the request URI specifies which index to delete from the indexes collection.</span></span>

<span data-ttu-id="89b28-608">`api-version=[string]` (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="89b28-608">`api-version=[string]` (required).</span></span> <span data-ttu-id="89b28-609">La versión de vista previa es `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="89b28-609">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="89b28-610">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.</span><span class="sxs-lookup"><span data-stu-id="89b28-610">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="89b28-611">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-611">**Request Headers**</span></span>

<span data-ttu-id="89b28-612">En la lista siguiente se describen los encabezados de solicitud obligatorios y opcionales.</span><span class="sxs-lookup"><span data-stu-id="89b28-612">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="89b28-613">`api-key`: obligatorio.</span><span class="sxs-lookup"><span data-stu-id="89b28-613">`api-key`: Required.</span></span> <span data-ttu-id="89b28-614">`api-key` se usa para autenticar la solicitud en su servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-614">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="89b28-615">Es un valor de cadena, único en su URL de servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-615">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="89b28-616">La solicitud **Eliminar índice** debe incluir un encabezado `api-key` establecido en su clave de administración (en lugar de una clave de consulta).</span><span class="sxs-lookup"><span data-stu-id="89b28-616">The **Delete Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="89b28-617">También necesitará el nombre del servicio para construir la dirección URL de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="89b28-617">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="89b28-618">Puede obtener el nombre de servicio y `api-key` desde el panel de servicio en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="89b28-618">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="89b28-619">Consulte [Crear un servicio de Búsqueda de Azure en el portal](search-create-service-portal.md) para obtener ayuda sobre la navegación en páginas.</span><span class="sxs-lookup"><span data-stu-id="89b28-619">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="89b28-620">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-620">**Request Body**</span></span>

<span data-ttu-id="89b28-621">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="89b28-621">None.</span></span>

<span data-ttu-id="89b28-622">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="89b28-622">**Response**</span></span>

<span data-ttu-id="89b28-623">Código de estado: al obtener una respuesta correcta, se visualiza 204 Sin contenido.</span><span class="sxs-lookup"><span data-stu-id="89b28-623">Status Code: 204 No Content is returned for a successful response.</span></span>

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a><span data-ttu-id="89b28-624">Obtención de estadísticas de índice</span><span class="sxs-lookup"><span data-stu-id="89b28-624">Get Index Statistics</span></span>
<span data-ttu-id="89b28-625">La operación **Obtener estadísticas de índice** obtiene de Búsqueda de Azure un recuento de documentos para el índice actual, más el uso del almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="89b28-625">The **Get Index Statistics** operation returns from Azure Search a document count for the current index, plus storage usage.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> <span data-ttu-id="89b28-626">Se recopilan estadísticas del tamaño de almacenamiento y el número de documento cada pocos minutos; es decir, no se hace en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="89b28-626">Statistics on document count and storage size are collected every few minutes, not in real time.</span></span> <span data-ttu-id="89b28-627">Por lo tanto, es posible que las estadísticas que devuelve esta API no reflejen los cambios causados por operaciones de indexación recientes.</span><span class="sxs-lookup"><span data-stu-id="89b28-627">Therefore, the statistics returned by this API may not reflect changes caused by recent indexing operations.</span></span>
> 
> 

<span data-ttu-id="89b28-628">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-628">**Request**</span></span>

<span data-ttu-id="89b28-629">HTTPS es necesario para todas las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-629">HTTPS is required for all services requests.</span></span> <span data-ttu-id="89b28-630">La solicitud **Obtener estadísticas de índices** puede crearse mediante el método GET.</span><span class="sxs-lookup"><span data-stu-id="89b28-630">The **Get Index Statistics** request can be constructed using the GET method.</span></span>

<span data-ttu-id="89b28-631">El [nombre de índice] del URI de la solicitud indica al servicio que devuelva estadísticas de índice para el índice especificado.</span><span class="sxs-lookup"><span data-stu-id="89b28-631">The [index name] in the request URI tells the service to return index statistics for the specified index.</span></span>

<span data-ttu-id="89b28-632">`api-version=[string]` (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="89b28-632">`api-version=[string]` (required).</span></span> <span data-ttu-id="89b28-633">La versión de vista previa es `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="89b28-633">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="89b28-634">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.</span><span class="sxs-lookup"><span data-stu-id="89b28-634">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="89b28-635">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-635">**Request Headers**</span></span>

<span data-ttu-id="89b28-636">En la lista siguiente se describen los encabezados de solicitud obligatorios y opcionales.</span><span class="sxs-lookup"><span data-stu-id="89b28-636">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="89b28-637">`api-key`: `api-key` se usa para autenticar la solicitud en su servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-637">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="89b28-638">Es un valor de cadena único para el servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-638">It is a string value, unique to your service.</span></span> <span data-ttu-id="89b28-639">La solicitud **Obtener estadísticas de índice** debe incluir un encabezado `api-key` establecido en una clave de administración (en lugar de una clave de consulta).</span><span class="sxs-lookup"><span data-stu-id="89b28-639">The **Get Index Statistics** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="89b28-640">También necesitará el nombre del servicio para construir la dirección URL de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="89b28-640">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="89b28-641">Puede obtener el nombre de servicio y `api-key` desde el panel de servicio en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="89b28-641">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="89b28-642">Consulte [Crear un servicio de Búsqueda de Azure en el portal](search-create-service-portal.md) para obtener ayuda sobre la navegación en páginas.</span><span class="sxs-lookup"><span data-stu-id="89b28-642">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="89b28-643">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-643">**Request Body**</span></span>

<span data-ttu-id="89b28-644">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="89b28-644">None.</span></span>

<span data-ttu-id="89b28-645">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="89b28-645">**Response**</span></span>

<span data-ttu-id="89b28-646">Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.</span><span class="sxs-lookup"><span data-stu-id="89b28-646">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="89b28-647">El cuerpo de la respuesta está en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="89b28-647">The response body is in the following format:</span></span>

    {
      "documentCount": number,
      "storageSize": number (size of the index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a><span data-ttu-id="89b28-648">Analizador de prueba</span><span class="sxs-lookup"><span data-stu-id="89b28-648">Test Analyzer</span></span>
<span data-ttu-id="89b28-649">La **API de análisis** muestra cómo un analizador descompone el texto en tokens.</span><span class="sxs-lookup"><span data-stu-id="89b28-649">The **Analyze API** shows how an analyzer breaks text into tokens.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="89b28-650">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-650">**Request**</span></span>

<span data-ttu-id="89b28-651">HTTPS es necesario para todas las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-651">HTTPS is required for all services requests.</span></span> <span data-ttu-id="89b28-652">La solicitud de la **API de análisis** se puede crear mediante el método POST.</span><span class="sxs-lookup"><span data-stu-id="89b28-652">The **Analyze API** request can be constructed using the POST method.</span></span>

<span data-ttu-id="89b28-653">`api-version=[string]` (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="89b28-653">`api-version=[string]` (required).</span></span> <span data-ttu-id="89b28-654">La versión de vista previa es `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="89b28-654">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="89b28-655">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.</span><span class="sxs-lookup"><span data-stu-id="89b28-655">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="89b28-656">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-656">**Request Headers**</span></span>

<span data-ttu-id="89b28-657">En la lista siguiente se describen los encabezados de solicitud obligatorios y opcionales.</span><span class="sxs-lookup"><span data-stu-id="89b28-657">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="89b28-658">`api-key`: `api-key` se usa para autenticar la solicitud en su servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-658">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="89b28-659">Es un valor de cadena único para el servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-659">It is a string value, unique to your service.</span></span> <span data-ttu-id="89b28-660">La solicitud de **API de análisis** debe incluir un valor de `api-key` establecido en una clave de administración (en lugar de una clave de consulta).</span><span class="sxs-lookup"><span data-stu-id="89b28-660">The **Analyze API** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="89b28-661">También necesitará el nombre del índice y el nombre del servicio para construir la dirección URL de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="89b28-661">You will also need the index name and the service name to construct the request URL.</span></span> <span data-ttu-id="89b28-662">Puede obtener el nombre de servicio y `api-key` desde el panel de servicio en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="89b28-662">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="89b28-663">Consulte [Crear un servicio de Búsqueda de Azure en el portal](search-create-service-portal.md) para obtener ayuda sobre la navegación en páginas.</span><span class="sxs-lookup"><span data-stu-id="89b28-663">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="89b28-664">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-664">**Request Body**</span></span>

    {
      "text": "Text to analyze",
      "analyzer": "analyzer_name"
    }

<span data-ttu-id="89b28-665">o</span><span class="sxs-lookup"><span data-stu-id="89b28-665">or</span></span>

    {
      "text": "Text to analyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

<span data-ttu-id="89b28-666">`analyzer_name`, `tokenizer_name`, `token_filter_name` y `char_filter_name` deben ser nombres válidos de analizadores, tokenizadores, filtros de token y filtros de caracteres predefinidos o personalizados para el índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-666">The `analyzer_name`, `tokenizer_name`, `token_filter_name` and `char_filter_name` need to be valid names of predefined or custom analyzers, tokenizers, token filters and char filters for the index.</span></span> <span data-ttu-id="89b28-667">Para obtener más información sobre el proceso de análisis léxico, consulte [Análisis en Búsqueda de Azure](https://aka.ms/azsanalysis).</span><span class="sxs-lookup"><span data-stu-id="89b28-667">To learn more about the process of lexical analysis see [Analysis in Azure Search](https://aka.ms/azsanalysis).</span></span>

<span data-ttu-id="89b28-668">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="89b28-668">**Response**</span></span>

<span data-ttu-id="89b28-669">Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.</span><span class="sxs-lookup"><span data-stu-id="89b28-669">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="89b28-670">El cuerpo de la respuesta está en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="89b28-670">The response body is in the following format:</span></span>

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of the first character of the token),
          "endOffset": number (index of the last character of the token),
          "position": number (position of the token in the input text)
        },
        ...
      ]
    }

<span data-ttu-id="89b28-671">**Ejemplo de la API de análisis**</span><span class="sxs-lookup"><span data-stu-id="89b28-671">**Analyze API example**</span></span>

<span data-ttu-id="89b28-672">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-672">**Request**</span></span>

    {
      "text": "Text to analyze",
      "analyzer": "standard"
    }

<span data-ttu-id="89b28-673">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="89b28-673">**Response**</span></span>

    {
      "tokens": [
        {
          "token": "text",
          "startOffset": 0,
          "endOffset": 4,
          "position": 0
        },
        {
          "token": "to",
          "startOffset": 5,
          "endOffset": 7,
          "position": 1
        },
        {
          "token": "analyze",
          "startOffset": 8,
          "endOffset": 15,
          "position": 2
        }
      ]
    }

- - -
<a name="DocOps"></a>

## <a name="document-operations"></a><span data-ttu-id="89b28-674">Operaciones del documento</span><span class="sxs-lookup"><span data-stu-id="89b28-674">Document Operations</span></span>
<span data-ttu-id="89b28-675">En Búsqueda de Azure, se almacena un índice en la nube y se rellena con documentos JSON que se cargan en el servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-675">In Azure Search, an index is stored in the cloud and populated using JSON documents that you upload to the service.</span></span> <span data-ttu-id="89b28-676">Todos los documentos que se cargan comprenden el corpus de los datos de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-676">All the documents that you upload comprise the corpus of your search data.</span></span> <span data-ttu-id="89b28-677">Los documentos contienen campos, algunos de los cuales se acortan en términos de búsqueda cuando se cargan.</span><span class="sxs-lookup"><span data-stu-id="89b28-677">Documents contain fields, some of which are tokenized into search terms as they are uploaded.</span></span> <span data-ttu-id="89b28-678">El segmento de URL `/docs` de la API de Búsqueda de Azure representa la colección de documentos en un índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-678">The `/docs` URL segment in the Azure Search API represents the collection of documents in an index.</span></span> <span data-ttu-id="89b28-679">Todas las operaciones realizadas en la colección, como cargar, combinar, eliminar o consultar documentos se producen en el contexto de un índice único, por lo que las direcciones URL de estas operaciones siempre se iniciarán mediante `/indexes/[index name]/docs` para un nombre de índice especificado.</span><span class="sxs-lookup"><span data-stu-id="89b28-679">All operations performed on the collection such as uploading, merging, deleting, or querying documents take place in the context of a single index, so the URLs for these operations will always start with `/indexes/[index name]/docs` for a given index name.</span></span>

<span data-ttu-id="89b28-680">El código de aplicación debe generar documentos JSON para cargarlos en Azure Search o se puede usar un [indexador](https://msdn.microsoft.com/library/dn946891.aspx) para cargar documentos si el origen de datos es Azure SQL Database o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="89b28-680">Your application code must either generate JSON documents to upload to Azure Search or you can use an [indexer](https://msdn.microsoft.com/library/dn946891.aspx) to load documents if the data source is either Azure SQL Database or Azure Cosmos DB.</span></span> <span data-ttu-id="89b28-681">Normalmente, los índices se rellenan desde un único conjunto de datos que suministre.</span><span class="sxs-lookup"><span data-stu-id="89b28-681">Typically, indexes are populated from a single dataset that you provide.</span></span>

<span data-ttu-id="89b28-682">Debe planear disponer de un documento para cada elemento que desee buscar.</span><span class="sxs-lookup"><span data-stu-id="89b28-682">You should plan on having one document for each item that you want to search.</span></span> <span data-ttu-id="89b28-683">Una aplicación de alquiler de películas puede disponer de un documento por película, una aplicación de escaparate podría tener un documento por SKU, una aplicación de software con fines pedagógicos en línea podría tener un documento por curso, una empresa de investigación podría tener un documento para cada documento académico de su repositorio, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="89b28-683">A movie rental application might have one document per movie, a storefront application might have one document per SKU, an online courseware application might have one document per course, a research firm might have one document for each academic paper in their repository, and so on.</span></span>

<span data-ttu-id="89b28-684">Los documentos constan de uno o varios campos.</span><span class="sxs-lookup"><span data-stu-id="89b28-684">Documents consist of one or more fields.</span></span> <span data-ttu-id="89b28-685">Los campos pueden contener texto acortado por Búsqueda de Azure a términos de búsqueda, así como los valores no acortados o que no sean de texto que pueden utilizarse en filtros o perfiles de puntuación.</span><span class="sxs-lookup"><span data-stu-id="89b28-685">Fields can contain text that is tokenized by Azure Search into search terms, as well as non-tokenized or non-text values that can be used in filters or scoring profiles.</span></span> <span data-ttu-id="89b28-686">Los nombres, tipos de datos y funciones de búsqueda admitidos para cada campo están determinados por el esquema de índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-686">The names, data types, and search features supported for each field are determined by the index schema.</span></span> <span data-ttu-id="89b28-687">Uno de los campos de cada esquema de índice debe designarse como identificador, y cada documento debe tener un valor para el campo de identificador que identifica ese documento de manera única en el índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-687">One of the fields in each index schema must be designated as an ID, and each document must have a value for the ID field that uniquely identifies that document in the index.</span></span> <span data-ttu-id="89b28-688">Todos los demás campos de documento son opcionales y se establecerán de manera predeterminada en un valor null si no se especifican.</span><span class="sxs-lookup"><span data-stu-id="89b28-688">All other document fields are optional and will default to a null value if left unspecified.</span></span> <span data-ttu-id="89b28-689">Tenga en cuenta que los valores null no ocupan espacio en el índice de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-689">Note that null values do not take up space in the search index.</span></span>

<span data-ttu-id="89b28-690">Para poder cargar documentos, debe haber creado el índice en el servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-690">Before you can upload documents, you must have already created the index on the service.</span></span> <span data-ttu-id="89b28-691">Consulte [Crear índice](#CreateIndex) para obtener más información acerca de este primer paso.</span><span class="sxs-lookup"><span data-stu-id="89b28-691">See [Create Index](#CreateIndex) for details about this first step.</span></span>

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a><span data-ttu-id="89b28-692">Agregar, actualizar o eliminar documentos</span><span class="sxs-lookup"><span data-stu-id="89b28-692">Add, Update, or Delete Documents</span></span>
<span data-ttu-id="89b28-693">Puede cargar, combinar, combinar o cargar o eliminar documentos en un índice especificado mediante HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="89b28-693">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span> <span data-ttu-id="89b28-694">Para números elevados de actualizaciones, se recomienda efectuar el procesamiento por lotes de documentos (hasta 1.000 documentos por lote o aproximadamente 16 MB por lote).</span><span class="sxs-lookup"><span data-stu-id="89b28-694">For large numbers of updates, batching of documents (up to 1000 documents per batch or about 16 MB per batch) is recommended.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="89b28-695">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-695">**Request**</span></span>

<span data-ttu-id="89b28-696">HTTPS es necesario para todas las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-696">HTTPS is required for all service requests.</span></span> <span data-ttu-id="89b28-697">Puede cargar, combinar, combinar o cargar o eliminar documentos en un índice especificado mediante HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="89b28-697">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span>

<span data-ttu-id="89b28-698">El URI de solicitud incluye eI [nombre de índice], y especifica en qué índice publicar los documentos.</span><span class="sxs-lookup"><span data-stu-id="89b28-698">The request URI includes [index name], specifying which index to post documents.</span></span> <span data-ttu-id="89b28-699">Solo se pueden publicar documentos en un índice de cada vez.</span><span class="sxs-lookup"><span data-stu-id="89b28-699">You can only post documents to one index at a time.</span></span>

<span data-ttu-id="89b28-700">`api-version=[string]` (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="89b28-700">`api-version=[string]` (required).</span></span> <span data-ttu-id="89b28-701">La versión de vista previa es `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="89b28-701">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="89b28-702">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.</span><span class="sxs-lookup"><span data-stu-id="89b28-702">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="89b28-703">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-703">**Request Headers**</span></span>

<span data-ttu-id="89b28-704">En la lista siguiente se describen los encabezados de solicitud obligatorios y opcionales.</span><span class="sxs-lookup"><span data-stu-id="89b28-704">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="89b28-705">`Content-Type`: obligatorio.</span><span class="sxs-lookup"><span data-stu-id="89b28-705">`Content-Type`: Required.</span></span> <span data-ttu-id="89b28-706">Establézcalo en `application/json`</span><span class="sxs-lookup"><span data-stu-id="89b28-706">Set this to `application/json`</span></span>
* <span data-ttu-id="89b28-707">`api-key`: obligatorio.</span><span class="sxs-lookup"><span data-stu-id="89b28-707">`api-key`: Required.</span></span> <span data-ttu-id="89b28-708">`api-key` se usa para autenticar la solicitud en su servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-708">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="89b28-709">Es un valor de cadena único para el servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-709">It is a string value, unique to your service.</span></span> <span data-ttu-id="89b28-710">La solicitud **Agregar documentos** debe incluir un encabezado `api-key` establecido en su clave de administración (en lugar de una clave de consulta).</span><span class="sxs-lookup"><span data-stu-id="89b28-710">The **Add Documents** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="89b28-711">También necesitará el nombre del servicio para construir la dirección URL de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="89b28-711">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="89b28-712">Puede obtener el nombre de servicio y `api-key` desde el panel de servicio en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="89b28-712">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="89b28-713">Consulte [Crear un servicio de Búsqueda de Azure en el portal](search-create-service-portal.md) para obtener ayuda sobre la navegación en páginas.</span><span class="sxs-lookup"><span data-stu-id="89b28-713">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="89b28-714">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-714">**Request Body**</span></span>

<span data-ttu-id="89b28-715">El cuerpo de la solicitud contiene uno o más documentos para indexar.</span><span class="sxs-lookup"><span data-stu-id="89b28-715">The body of the request contains one or more documents to be indexed.</span></span> <span data-ttu-id="89b28-716">Los documentos se identifican mediante una clave única.</span><span class="sxs-lookup"><span data-stu-id="89b28-716">Documents are identified by a unique key.</span></span> <span data-ttu-id="89b28-717">Cada documento está asociado a una acción: carga, combinación, combinación o carga o eliminación.</span><span class="sxs-lookup"><span data-stu-id="89b28-717">Each document is associated with an action: upload, merge, mergeOrUpload or delete.</span></span> <span data-ttu-id="89b28-718">Las solicitudes de carga deben incluir los datos del documento como un conjunto de pares de clave/valor.</span><span class="sxs-lookup"><span data-stu-id="89b28-718">Upload requests must include the document data as a set of key/value pairs.</span></span>

    {
      "value": [
        {
          "@search.action": "upload (default) | merge | mergeOrUpload | delete",
          "key_field_name": "unique_key_of_document", (key/value pair for key field from index schema)
          "field_name": field_value (key/value pairs matching index schema)
            ...
        },
        ...
      ]
    }

> [!NOTE]
> <span data-ttu-id="89b28-719">Las claves de documento solo pueden contener letras, números, guiones ("-"), caracteres de subrayado ("_") y signos igual ("=").</span><span class="sxs-lookup"><span data-stu-id="89b28-719">Document keys can only contain letters, numbers, dashes ("-"), underscores ("_"), and equal signs ("=").</span></span> <span data-ttu-id="89b28-720">Para obtener más información, consulte [Reglas de nomenclatura](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span><span class="sxs-lookup"><span data-stu-id="89b28-720">For more details, see [Naming rules](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span></span>
> 
> 

<span data-ttu-id="89b28-721">**Acciones de documentos**</span><span class="sxs-lookup"><span data-stu-id="89b28-721">**Document Actions**</span></span>

* <span data-ttu-id="89b28-722">`upload`: una acción de carga es similar a un "upsert" donde se insertará el documento si es nuevo y se actualizará/reemplazará si existe.</span><span class="sxs-lookup"><span data-stu-id="89b28-722">`upload`: An upload action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span></span> <span data-ttu-id="89b28-723">Tenga en cuenta que se reemplazarán todos los campos en el caso de la actualización.</span><span class="sxs-lookup"><span data-stu-id="89b28-723">Note that all fields are replaced in the update case.</span></span>
* <span data-ttu-id="89b28-724">`merge`: la combinación actualiza un documento existente con los campos especificados.</span><span class="sxs-lookup"><span data-stu-id="89b28-724">`merge`: Merge updates an existing document with the specified fields.</span></span> <span data-ttu-id="89b28-725">Si el documento no existe, se producirá un error en la combinación.</span><span class="sxs-lookup"><span data-stu-id="89b28-725">If the document doesn't exist, the merge will fail.</span></span> <span data-ttu-id="89b28-726">Cualquier campo que se especifica en una combinación reemplazará al campo existente en el documento.</span><span class="sxs-lookup"><span data-stu-id="89b28-726">Any field you specify in a merge will replace the existing field in the document.</span></span> <span data-ttu-id="89b28-727">Aquí se incluyen los campos de tipo `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="89b28-727">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="89b28-728">Por ejemplo, si el documento contiene un campo "etiquetas" con el valor `["budget"]` y ejecuta una combinación con el valor `["economy", "pool"]` para "etiquetas", el valor final del campo "etiquetas" será `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="89b28-728">For example, if the document contains a field "tags" with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for "tags", the final value of the "tags" field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="89b28-729">**No** será `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="89b28-729">It will **not** be `["budget", "economy", "pool"]`.</span></span>
* <span data-ttu-id="89b28-730">`mergeOrUpload`: se comporta como `merge` si ya existe un documento con la clave especificada en el índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-730">`mergeOrUpload`: behaves like `merge` if a document with the given key already exists in the index.</span></span> <span data-ttu-id="89b28-731">Si el documento no existe, se comporta como `upload` con un nuevo documento.</span><span class="sxs-lookup"><span data-stu-id="89b28-731">If the document does not exist it behaves like `upload` with a new document.</span></span>
* <span data-ttu-id="89b28-732">`delete`: la eliminación quita el documento especificado del índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-732">`delete`: Delete removes the specified document from the index.</span></span> <span data-ttu-id="89b28-733">Tenga en cuenta que los campos que especifique en una operación `delete` , que no sean el campo de clave, se omitirán.</span><span class="sxs-lookup"><span data-stu-id="89b28-733">Note that any fields you specify in a `delete` operation other than the key field will be ignored.</span></span> <span data-ttu-id="89b28-734">Si desea quitar un campo individual de un documento, use `merge` en su lugar y simplemente establezca el campo explícitamente en `null`.</span><span class="sxs-lookup"><span data-stu-id="89b28-734">If you want to remove an individual field from a document, use `merge` instead and simply set the field explicitly to `null`.</span></span>

<span data-ttu-id="89b28-735">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="89b28-735">**Response**</span></span>

<span data-ttu-id="89b28-736">Código de estado: se obtendrá 200 Correcto con una respuesta correcta, lo que significa que todos los elementos se han indexado correctamente.</span><span class="sxs-lookup"><span data-stu-id="89b28-736">Status code 200 (OK) is returned for a successful response, meaning that all items have been successfully indexed.</span></span> <span data-ttu-id="89b28-737">Esto se indica mediante el `status` establecimiento de la propiedad en true para todos los elementos, así como el establecimiento de la propiedad `statusCode` en 201 (para documentos recién cargados) o en 200 (para documentos combinados o eliminados):</span><span class="sxs-lookup"><span data-stu-id="89b28-737">This is indicated by the `status` property being set to true for all items, as well as the `statusCode` property being set to either 201 (for newly uploaded documents) or 200 (for merged or deleted documents):</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_new_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 201
        },
        {
          "key": "unique_key_of_merged_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        },
        {
          "key": "unique_key_of_deleted_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        }
      ]
    }  

<span data-ttu-id="89b28-738">Se devolverá un código de estado 207 (varios estados) solo con que un elemento no se indexe correctamente.</span><span class="sxs-lookup"><span data-stu-id="89b28-738">Status code 207 (Multi-Status) is returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="89b28-739">Los elementos que no se indexaron tienen el campo `status` establecido en false.</span><span class="sxs-lookup"><span data-stu-id="89b28-739">Items that have not been indexed have the `status` field set to false.</span></span> <span data-ttu-id="89b28-740">Las propiedades `errorMessage` y `statusCode` indicarán el motivo del error de indexación:</span><span class="sxs-lookup"><span data-stu-id="89b28-740">The `errorMessage` and `statusCode` properties will indicate the reason for the indexing error:</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "The search service is too busy to process this document. Please try again later.",
          "statusCode": 503
        },
        {
          "key": "unique_key_of_document_2",
          "status": false,
          "errorMessage": "Document not found.",
          "statusCode": 404
        },
        {
          "key": "unique_key_of_document_3",
          "status": false,
          "errorMessage": "Index is temporarily unavailable because it was updated with the 'allowIndexDowntime' flag set to 'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

<span data-ttu-id="89b28-741">La tabla siguiente explica los distintos códigos de estado por documento que se pueden devolver en la respuesta.</span><span class="sxs-lookup"><span data-stu-id="89b28-741">The following table explains the various per-document status codes that can be returned in the response.</span></span> <span data-ttu-id="89b28-742">Tenga en cuenta que algunos indican problemas con la solicitud, mientras que otros indican condiciones de error temporales.</span><span class="sxs-lookup"><span data-stu-id="89b28-742">Note that some indicate problems with the request itself, while others indicate temporary error conditions.</span></span> <span data-ttu-id="89b28-743">En este último caso debe volver a intentarlo después de un tiempo.</span><span class="sxs-lookup"><span data-stu-id="89b28-743">The latter you should retry after a delay.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="89b28-744">Código de estado</span><span class="sxs-lookup"><span data-stu-id="89b28-744">Status code</span></span></th>
        <th><span data-ttu-id="89b28-745">Significado</span><span class="sxs-lookup"><span data-stu-id="89b28-745">Meaning</span></span></th>
        <th><span data-ttu-id="89b28-746">Se puede volver a intentar</span><span class="sxs-lookup"><span data-stu-id="89b28-746">Retryable</span></span></th>
        <th><span data-ttu-id="89b28-747">Notas</span><span class="sxs-lookup"><span data-stu-id="89b28-747">Notes</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-748">200</span><span class="sxs-lookup"><span data-stu-id="89b28-748">200</span></span></td>
        <td><span data-ttu-id="89b28-749">Documento correctamente modificado o eliminado.</span><span class="sxs-lookup"><span data-stu-id="89b28-749">Document was successfully modified or deleted.</span></span></td>
        <td><span data-ttu-id="89b28-750">N/D</span><span class="sxs-lookup"><span data-stu-id="89b28-750">n/a</span></span></td>
        <td><span data-ttu-id="89b28-751">Las operaciones de eliminación son <a href="https://en.wikipedia.org/wiki/Idempotence">idempotentes</a>.</span><span class="sxs-lookup"><span data-stu-id="89b28-751">Delete operations are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span> <span data-ttu-id="89b28-752">Es decir, incluso si no existe una clave de documento en el índice, intentar una operación de eliminación con esa clave producirá un código de estado 200.</span><span class="sxs-lookup"><span data-stu-id="89b28-752">That is, even if a document key does not exist in the index, attempting a delete operation with that key will result in a 200 status code.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-753">201</span><span class="sxs-lookup"><span data-stu-id="89b28-753">201</span></span></td>
        <td><span data-ttu-id="89b28-754">El documento se creó correctamente.</span><span class="sxs-lookup"><span data-stu-id="89b28-754">Document was successfully created.</span></span></td>
        <td><span data-ttu-id="89b28-755">N/D</span><span class="sxs-lookup"><span data-stu-id="89b28-755">n/a</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-756">400</span><span class="sxs-lookup"><span data-stu-id="89b28-756">400</span></span></td>
        <td><span data-ttu-id="89b28-757">Se produjo un error en el documento que ha impedido que se indexe.</span><span class="sxs-lookup"><span data-stu-id="89b28-757">There was an error in the document that prevented it from being indexed.</span></span></td>
        <td><span data-ttu-id="89b28-758">No</span><span class="sxs-lookup"><span data-stu-id="89b28-758">No</span></span></td>
        <td><span data-ttu-id="89b28-759">El mensaje de error en la respuesta indica cuál es el problema con el documento.</span><span class="sxs-lookup"><span data-stu-id="89b28-759">The error message in the response will indicate what is wrong with the document.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-760">404</span><span class="sxs-lookup"><span data-stu-id="89b28-760">404</span></span></td>
        <td><span data-ttu-id="89b28-761">No se pudo combinar el documento porque no existe la clave especificada en el índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-761">The document could not be merged because the given key doesn't exist in the index.</span></span></td>
        <td><span data-ttu-id="89b28-762">No</span><span class="sxs-lookup"><span data-stu-id="89b28-762">No</span></span></td>
        <td><span data-ttu-id="89b28-763">Este error no se produce durante las cargas ya que estas crean nuevos documentos y no se producen durante las eliminaciones porque son <a href="https://en.wikipedia.org/wiki/Idempotence">idempotentes</a>.</span><span class="sxs-lookup"><span data-stu-id="89b28-763">This error does not occur for uploads since they create new documents, and it does not occur for deletes because they are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-764">409</span><span class="sxs-lookup"><span data-stu-id="89b28-764">409</span></span></td>
        <td><span data-ttu-id="89b28-765">Se detectó un conflicto de versión al intentar indexar un documento.</span><span class="sxs-lookup"><span data-stu-id="89b28-765">A version conflict was detected when attempting to index a document.</span></span></td>
        <td><span data-ttu-id="89b28-766">Sí</span><span class="sxs-lookup"><span data-stu-id="89b28-766">Yes</span></span></td>
        <td><span data-ttu-id="89b28-767">Esto puede ocurrir si intenta indexar el mismo documento más de una vez al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="89b28-767">This can happen when you're trying to index the same document more than once concurrently.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-768">422</span><span class="sxs-lookup"><span data-stu-id="89b28-768">422</span></span></td>
        <td><span data-ttu-id="89b28-769">El índice no está disponible temporalmente porque se ha actualizado con el indicador 'allowIndexDowntime' establecido en 'true'.</span><span class="sxs-lookup"><span data-stu-id="89b28-769">The index is temporarily unavailable because it was updated with the 'allowIndexDowntime' flag set to 'true'.</span></span></td>
        <td><span data-ttu-id="89b28-770">Sí</span><span class="sxs-lookup"><span data-stu-id="89b28-770">Yes</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="89b28-771">503</span><span class="sxs-lookup"><span data-stu-id="89b28-771">503</span></span></td>
        <td><span data-ttu-id="89b28-772">El servicio de búsqueda no está disponible temporalmente, posiblemente debido a una carga elevada.</span><span class="sxs-lookup"><span data-stu-id="89b28-772">Your search service is temporarily unavailable, possibly due to heavy load.</span></span></td>
        <td><span data-ttu-id="89b28-773">Sí</span><span class="sxs-lookup"><span data-stu-id="89b28-773">Yes</span></span></td>
        <td><span data-ttu-id="89b28-774">En este caso, el código debe esperar antes de reintentar ya que, de lo contrario, se arriesga a prolongar la no disponibilidad del servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-774">Your code should wait before retrying in this case or you risk prolonging the service unavailability.</span></span></td>
    </tr>
</table> 

<span data-ttu-id="89b28-775">**Nota**: Si el código de cliente encuentra con frecuencia una respuesta 207, una razón posible es que el sistema está bajo carga.</span><span class="sxs-lookup"><span data-stu-id="89b28-775">**Note**: If your client code frequently encounters a 207 response, one possible reason is that the system is under load.</span></span> <span data-ttu-id="89b28-776">Puede confirmar esto comprobando la propiedad `statusCode` para 503.</span><span class="sxs-lookup"><span data-stu-id="89b28-776">You can confirm this by checking the `statusCode` property for 503.</span></span> <span data-ttu-id="89b28-777">En tal caso, es recomendable ***limitar las solicitudes de indexación***.</span><span class="sxs-lookup"><span data-stu-id="89b28-777">If this is the case, we recommend ***throttling indexing requests***.</span></span> <span data-ttu-id="89b28-778">De lo contrario, si el tráfico de indexación de tráfico no se reduce, es posible que el sistema comience a rechazar todas las solicitudes mediante errores 503.</span><span class="sxs-lookup"><span data-stu-id="89b28-778">Otherwise, if indexing traffic doesn't subside, the system could start rejecting all requests with 503 errors.</span></span>

<span data-ttu-id="89b28-779">El código de estado 429 indica que se ha superado la cuota del número de documentos por índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-779">Status code 429 indicates that you have exceeded your quota on the number of documents per index.</span></span> <span data-ttu-id="89b28-780">Debe crear un nuevo índice o actualizar para obtener límites de capacidad superiores.</span><span class="sxs-lookup"><span data-stu-id="89b28-780">You must either create a new index or upgrade for higher capacity limits.</span></span>

<span data-ttu-id="89b28-781">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="89b28-781">**Example:**</span></span>

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
          "@search.action": "merge",
          "hotelId": "3",
          "baseRate": 279.99,
          "description": "Surprisingly expensive",
          "lastRenovationDate": null
        },
        {
          "@search.action": "delete",
          "hotelId": "4"
        }
      ]
    }
- - -
<a name="SearchDocs"></a>

## <a name="search-documents"></a><span data-ttu-id="89b28-782">Buscar documentos</span><span class="sxs-lookup"><span data-stu-id="89b28-782">Search Documents</span></span>
<span data-ttu-id="89b28-783">La operación de **búsqueda** se emite como una solicitud GET o POST y especifica parámetros que ofrecen los criterios necesarios para seleccionar los documentos coincidentes.</span><span class="sxs-lookup"><span data-stu-id="89b28-783">A **Search** operation is issued as a GET or POST request and specifies parameters that give the criteria for selecting matching documents.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="89b28-784">**Cuándo usar POST en lugar de GET**</span><span class="sxs-lookup"><span data-stu-id="89b28-784">**When to use POST instead of GET**</span></span>

<span data-ttu-id="89b28-785">Cuando use HTTP GET para llamar a la API de **búsqueda** , deberá tener en cuenta que la longitud de la URL de la solicitud no puede superar los 8 KB.</span><span class="sxs-lookup"><span data-stu-id="89b28-785">When you use HTTP GET to call the **Search** API, you need to be aware that the length of the request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="89b28-786">Esto suele ser suficiente para la mayoría de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="89b28-786">This is usually enough for most applications.</span></span> <span data-ttu-id="89b28-787">Sin embargo, algunas aplicaciones generan consultas muy extensas o expresiones de filtro OData.</span><span class="sxs-lookup"><span data-stu-id="89b28-787">However, some applications produce very large queries or OData filter expressions.</span></span> <span data-ttu-id="89b28-788">Para estas aplicaciones, el uso de HTTP POST es una opción mejor porque permite filtros y consultas mayores que GET.</span><span class="sxs-lookup"><span data-stu-id="89b28-788">For these applications, using HTTP POST is a better choice because it allows larger filters and queries than GET.</span></span> <span data-ttu-id="89b28-789">Con POST, el número de términos o cláusulas en una consulta es el factor limitador, no el tamaño de la consulta básica, ya que el límite de tamaño de la solicitud POST es de 16 MB aproximadamente.</span><span class="sxs-lookup"><span data-stu-id="89b28-789">With POST, the number of terms or clauses in a query is the limiting factor, not the size of the raw query since the request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="89b28-790">Aunque el límite de tamaño de la solicitud POST es muy grande, las consultas y las expresiones de filtro de búsqueda no pueden ser arbitrariamente complejas.</span><span class="sxs-lookup"><span data-stu-id="89b28-790">Even though the POST request size limit is very large, search queries and filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="89b28-791">Consulte la [sintaxis de consulta de Lucene](https://msdn.microsoft.com/library/mt589323.aspx) y la [sintaxis de expresiones de OData](https://msdn.microsoft.com/library/dn798921.aspx) para más información sobre las limitaciones de complejidad de consultas y filtros de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-791">See [Lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx) and [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about search query and filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="89b28-792">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-792">**Request**</span></span>

<span data-ttu-id="89b28-793">HTTPS es necesario para las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-793">HTTPS is required for service requests.</span></span> <span data-ttu-id="89b28-794">La solicitud **Búsqueda** puede crearse mediante los método GET o POST.</span><span class="sxs-lookup"><span data-stu-id="89b28-794">The **Search** request can be constructed using the GET or POST methods.</span></span>

<span data-ttu-id="89b28-795">El URI de solicitud especifica qué índice se va a consultar para todos los documentos que coinciden con los parámetros de consulta.</span><span class="sxs-lookup"><span data-stu-id="89b28-795">The request URI specifies which index to query, for all documents that match the parameters.</span></span> <span data-ttu-id="89b28-796">Los parámetros se especifican en la cadena de consulta en el caso de solicitudes GET y en el cuerpo de la solicitud en el caso de las solicitudes POST.</span><span class="sxs-lookup"><span data-stu-id="89b28-796">Parameters are specified on the query string in the case of GET requests, and in the request body in the case of POST requests.</span></span>

<span data-ttu-id="89b28-797">Como práctica recomendada al crear solicitudes GET, recuerde [codificar con URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) los parámetros de consulta específicos al llamar a la API de REST directamente.</span><span class="sxs-lookup"><span data-stu-id="89b28-797">As a best practice when creating GET requests, remember to [URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling the REST API directly.</span></span> <span data-ttu-id="89b28-798">Para las operaciones de **Búsqueda** , esto incluye:</span><span class="sxs-lookup"><span data-stu-id="89b28-798">For **Search** operations, this includes:</span></span>

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

<span data-ttu-id="89b28-799">Solo se recomienda la codificación de direcciones URL en los parámetros de consulta anterior.</span><span class="sxs-lookup"><span data-stu-id="89b28-799">URL encoding is only recommended on the above query parameters.</span></span> <span data-ttu-id="89b28-800">Si codifica con URL involuntariamente la cadena de consulta completa (todo lo situado después de la?), las solicitudes se dividirán.</span><span class="sxs-lookup"><span data-stu-id="89b28-800">If you inadvertently URL-encode the entire query string (everything after the ?), requests will break.</span></span>

<span data-ttu-id="89b28-801">Además, la codificación con URL solo es necesaria cuando se llama directamente a la API de REST directamente con GET.</span><span class="sxs-lookup"><span data-stu-id="89b28-801">Also, URL encoding is only necessary when calling the REST API directly using GET.</span></span> <span data-ttu-id="89b28-802">No se requiere ninguna codificación de URL cuando se llama a la **Búsqueda** mediante POST o cuando se usa la [biblioteca de cliente .NET](https://msdn.microsoft.com/library/dn951165.aspx)que controla la codificación de direcciones URL en su lugar.</span><span class="sxs-lookup"><span data-stu-id="89b28-802">No URL encoding is necessary when calling **Search** using POST, or when using the [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="89b28-803"><a name="SearchQueryParameters"></a>
**Parámetros de consulta**</span><span class="sxs-lookup"><span data-stu-id="89b28-803"><a name="SearchQueryParameters"></a>
**Query Parameters**</span></span>

<span data-ttu-id="89b28-804">**búsqueda** acepta varios parámetros que ofrecen criterios de consulta y que también especifican el comportamiento de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-804">**Search** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="89b28-805">Ofrece estos parámetros en la cadena de consulta URL al llamar a la **búsqueda** mediante GET y como propiedades JSON en el cuerpo de solicitud al llamar a la **búsqueda** mediante POST.</span><span class="sxs-lookup"><span data-stu-id="89b28-805">You provide these parameters in the URL query string when calling **Search** via GET, and as JSON properties in the request body when calling **Search** via POST.</span></span> <span data-ttu-id="89b28-806">La sintaxis de algunos parámetros es algo diferente entre GET y POST.</span><span class="sxs-lookup"><span data-stu-id="89b28-806">The syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="89b28-807">Estas diferencias se indican como aplicables a continuación:</span><span class="sxs-lookup"><span data-stu-id="89b28-807">These differences are noted as applicable below:</span></span>

<span data-ttu-id="89b28-808">`search=[string]` (opcional): el texto que se debe buscar.</span><span class="sxs-lookup"><span data-stu-id="89b28-808">`search=[string]` (optional) - The text to search for.</span></span> <span data-ttu-id="89b28-809">Se busca en los campos `searchable` de forma predeterminada a menos que se especifique `searchFields`.</span><span class="sxs-lookup"><span data-stu-id="89b28-809">All `searchable` fields are searched by default unless `searchFields` is specified.</span></span> <span data-ttu-id="89b28-810">Al realizar búsquedas en campos `searchable`, se limita el propio texto de la búsqueda, por lo que los distintos términos pueden separarse mediante un espacio en blanco (por ejemplo: `search=hello world`).</span><span class="sxs-lookup"><span data-stu-id="89b28-810">When searching `searchable` fields, the search text itself is tokenized, so multiple terms can be separated by white space (for example: `search=hello world`).</span></span> <span data-ttu-id="89b28-811">Para encontrar un término, use `*` (esto puede ser útil para las consultas de filtro booleano).</span><span class="sxs-lookup"><span data-stu-id="89b28-811">To match any term, use `*` (this can be useful for boolean filter queries).</span></span> <span data-ttu-id="89b28-812">Omitir este parámetro tiene el mismo efecto que establecerlo en `*`.</span><span class="sxs-lookup"><span data-stu-id="89b28-812">Omitting this parameter has the same effect as setting it to `*`.</span></span> <span data-ttu-id="89b28-813">Para obtener información específica sobre la sintaxis de búsqueda, consulte [Sintaxis de consulta simple](https://msdn.microsoft.com/library/dn798920.aspx) .</span><span class="sxs-lookup"><span data-stu-id="89b28-813">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) for specifics on the search syntax.</span></span>

* <span data-ttu-id="89b28-814">**Nota**: los resultados a veces pueden ser sorprendentes al consultar sobre campos `searchable`.</span><span class="sxs-lookup"><span data-stu-id="89b28-814">**Note**: The results can sometimes be surprising when querying over `searchable` fields.</span></span> <span data-ttu-id="89b28-815">El tokenizer incluye una lógica para controlar los casos comunes en texto en inglés como apóstrofos, comas en números, etc. Por ejemplo, `search=123,456` hallará el único término 123,456 en lugar de los términos individuales 123 y 456, ya que en los números grandes en inglés se usan comas como separadores de miles.</span><span class="sxs-lookup"><span data-stu-id="89b28-815">The tokenizer includes logic to handle cases common to English text like apostrophes, commas in numbers, etc. For example, `search=123,456` will match a single term 123,456 rather than the individual terms 123 and 456, since commas are used as thousand-separators for large numbers in English.</span></span> <span data-ttu-id="89b28-816">Por este motivo, se recomienda usar espacios en blanco en lugar de signos de puntuación para separar los términos en el parámetro `search`.</span><span class="sxs-lookup"><span data-stu-id="89b28-816">For this reason, we recommend using white space rather than punctuation to separate terms in the `search` parameter.</span></span>

<span data-ttu-id="89b28-817">`searchMode=any|all` (opcional, tiene como valor predeterminado `any`): si alguno o todos los términos de búsqueda deben coincidir con el fin de contar el documento como una coincidencia.</span><span class="sxs-lookup"><span data-stu-id="89b28-817">`searchMode=any|all` (optional, defaults to `any`) - whether any or all of the search terms must be matched in order to count the document as a match.</span></span>

<span data-ttu-id="89b28-818">`searchFields=[string]` (opcional): la lista separada por comas de nombres de campo para buscar el texto especificado.</span><span class="sxs-lookup"><span data-stu-id="89b28-818">`searchFields=[string]` (optional) - The list of comma-separated field names to search for the specified text.</span></span> <span data-ttu-id="89b28-819">Los campos de destino deben estar marcados como `searchable`.</span><span class="sxs-lookup"><span data-stu-id="89b28-819">Target fields must be marked as `searchable`.</span></span>

<span data-ttu-id="89b28-820">`queryType=simple|full` (opcional, tiene como valor predeterminado `simple`): cuando se establece en "simple", el texto de búsqueda se interpreta mediante un lenguaje de consulta simple que permite símbolos como +, * y "".</span><span class="sxs-lookup"><span data-stu-id="89b28-820">`queryType=simple|full` (optional, defaults to `simple`) - when set to "simple" search text is interpreted using a simple query language that allows for symbols such as +, * and "".</span></span> <span data-ttu-id="89b28-821">Las consultas se evalúan en todos los campos de búsqueda (o campos indicados en `searchFields`) en cada documento de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="89b28-821">Queries are evaluated across all searchable fields (or fields indicated in `searchFields`) in each document by default.</span></span> <span data-ttu-id="89b28-822">Cuando se establece el tipo de consulta en `full` , el texto de búsqueda se interpreta mediante el lenguaje de consulta de Lucene que permite realizar búsquedas específicas de campos y ponderadas.</span><span class="sxs-lookup"><span data-stu-id="89b28-822">When the query type is set to `full` search text is interpreted using the Lucene query language which allows field-specific and weighted searches.</span></span> <span data-ttu-id="89b28-823">Para obtener información específica sobre las sintaxis de búsqueda, consulte [Sintaxis de consulta simple](https://msdn.microsoft.com/library/dn798920.aspx) y [Sintaxis de consulta de Lucene](https://msdn.microsoft.com/library/mt589323.aspx).</span><span class="sxs-lookup"><span data-stu-id="89b28-823">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) and [Lucene Query Syntax](https://msdn.microsoft.com/library/mt589323.aspx) for specifics on the search syntaxes.</span></span> 

> [!NOTE]
> <span data-ttu-id="89b28-824">No está admitido el intervalo de búsqueda en el lenguaje de consulta de Lucene, es preferible usar $filter que ofrece una funcionalidad similar.</span><span class="sxs-lookup"><span data-stu-id="89b28-824">Range search in the Lucene query language is not supported in favor of $filter which offers similar functionality.</span></span>
> 
> 

<span data-ttu-id="89b28-825">`moreLikeThis=[key]` (opcional) **Importante:** esta característica solo está disponible en `2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="89b28-825">`moreLikeThis=[key]` (optional) **Important:** This feature is only available in `2015-02-28-Preview`.</span></span> <span data-ttu-id="89b28-826">Esta opción no se puede usar en una consulta que contiene el parámetro de búsqueda de texto, `search=[string]`.</span><span class="sxs-lookup"><span data-stu-id="89b28-826">This option cannot be used in a query that contains the text search parameter, `search=[string]`.</span></span> <span data-ttu-id="89b28-827">El parámetro `moreLikeThis` busca documentos que son similares al documento especificado por la clave del documento.</span><span class="sxs-lookup"><span data-stu-id="89b28-827">The `moreLikeThis` parameter finds documents that are similar to the document specified by the document key.</span></span> <span data-ttu-id="89b28-828">Cuando se realiza una solicitud de búsqueda con `moreLikeThis`, se genera una lista de términos de búsqueda en función de la frecuencia y la rareza de los términos en el documento de origen.</span><span class="sxs-lookup"><span data-stu-id="89b28-828">When a search request is made with `moreLikeThis`, a list of search terms is generated based on the frequency and rarity of terms in the source document.</span></span> <span data-ttu-id="89b28-829">Estos términos se usan a continuación para realizar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="89b28-829">Those terms are then used to make the request.</span></span> <span data-ttu-id="89b28-830">De forma predeterminada, se considera el contenido de todos los campos `searchable` a menos que se use `searchFields` para restringir los campos que se buscan.</span><span class="sxs-lookup"><span data-stu-id="89b28-830">By default, the contents of all `searchable` fields are considered unless `searchFields` is used to restrict which fields are searched.</span></span>  

<span data-ttu-id="89b28-831">`$skip=#` (opcional): el número de resultados de búsqueda que se omiten; no puede ser superior a 100.000.</span><span class="sxs-lookup"><span data-stu-id="89b28-831">`$skip=#` (optional) - the number of search results to skip; Cannot be greater than 100,000.</span></span> <span data-ttu-id="89b28-832">Si necesita examinar documentos en secuencia pero no puede usar `$skip` debido a esta limitación, utilice `$orderby` en una clave totalmente ordenada y `$filter` con una consulta por rango en su lugar.</span><span class="sxs-lookup"><span data-stu-id="89b28-832">If you need to scan documents in sequence but cannot use `$skip` due to this limitation, consider using `$orderby` on a totally-ordered key and `$filter` with a range query instead.</span></span>

> [!NOTE]
> <span data-ttu-id="89b28-833">Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `skip` en lugar de `$skip`.</span><span class="sxs-lookup"><span data-stu-id="89b28-833">When calling **Search** using POST, this parameter is named `skip` instead of `$skip`.</span></span>
> 
> 

<span data-ttu-id="89b28-834">`$top=#` (opcional): número de resultados de búsqueda para recuperar.</span><span class="sxs-lookup"><span data-stu-id="89b28-834">`$top=#` (optional) - the number of search results to retrieve.</span></span> <span data-ttu-id="89b28-835">Se puede usar junto con `$skip` para implementar la paginación del lado del cliente de los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-835">This can be used in conjunction with `$skip` to implement client-side paging of search results.</span></span>

> [!NOTE]
> <span data-ttu-id="89b28-836">Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `top` en lugar de `$top`.</span><span class="sxs-lookup"><span data-stu-id="89b28-836">When calling **Search** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="89b28-837">`$count=true|false` (opcional, tiene como valor predeterminado `false`): especifica si se va a obtener el número total de resultados.</span><span class="sxs-lookup"><span data-stu-id="89b28-837">`$count=true|false` (optional, defaults to `false`) - Specifies whether to fetch the total count of results.</span></span> <span data-ttu-id="89b28-838">Este es el recuento de todos los documentos que coinciden con los parámetros `search` y `$filter`, omitiendo `$top` y `$skip`.</span><span class="sxs-lookup"><span data-stu-id="89b28-838">This is the count of all documents that match the `search` and `$filter` parameters, ignoring `$top` and `$skip`.</span></span> <span data-ttu-id="89b28-839">Establecer este valor en `true` puede afectar al rendimiento.</span><span class="sxs-lookup"><span data-stu-id="89b28-839">Setting this value to `true` may have a performance impact.</span></span> <span data-ttu-id="89b28-840">Tenga en cuenta que el número devuelto será una aproximación.</span><span class="sxs-lookup"><span data-stu-id="89b28-840">Note that the count returned is an approximation.</span></span>

> [!NOTE]
> <span data-ttu-id="89b28-841">Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `count` en lugar de `$count`.</span><span class="sxs-lookup"><span data-stu-id="89b28-841">When calling **Search** using POST, this parameter is named `count` instead of `$count`.</span></span>
> 
> 

<span data-ttu-id="89b28-842">`$orderby=[string]` (opcional): lista de expresiones separadas por comas por la que ordenar los resultados.</span><span class="sxs-lookup"><span data-stu-id="89b28-842">`$orderby=[string]` (optional) - A list of comma-separated expressions to sort the results by.</span></span> <span data-ttu-id="89b28-843">Cada expresión puede ser un nombre de campo o una llamada a la función `geo.distance()` .</span><span class="sxs-lookup"><span data-stu-id="89b28-843">Each expression can be either a field name or a call to the `geo.distance()` function.</span></span> <span data-ttu-id="89b28-844">Cada expresión puede ir seguida de `asc` para indicar el orden ascendente y de `desc` para indicar el orden descendente.</span><span class="sxs-lookup"><span data-stu-id="89b28-844">Each expression can be followed by `asc` to indicated ascending, and `desc` to indicate descending.</span></span> <span data-ttu-id="89b28-845">El valor predeterminado es ascendente.</span><span class="sxs-lookup"><span data-stu-id="89b28-845">The default is ascending order.</span></span> <span data-ttu-id="89b28-846">Los empates se resolverán por la puntuación de coincidencia de los documentos.</span><span class="sxs-lookup"><span data-stu-id="89b28-846">Ties will be broken by the match scores of documents.</span></span> <span data-ttu-id="89b28-847">Si no se especifica ningún `$orderby` , el orden predeterminado será descendente por puntuación de coincidencia del documento.</span><span class="sxs-lookup"><span data-stu-id="89b28-847">If no `$orderby` is specified, the default sort order is descending by document match score.</span></span> <span data-ttu-id="89b28-848">Hay un límite de 32 cláusulas para `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="89b28-848">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="89b28-849">Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `orderby` en lugar de `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="89b28-849">When calling **Search** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="89b28-850">`$select=[string]` (opcional): lista de campos separados por comas para recuperar.</span><span class="sxs-lookup"><span data-stu-id="89b28-850">`$select=[string]` (optional) - A list of comma-separated fields to retrieve.</span></span> <span data-ttu-id="89b28-851">Si no se especifica nada, se incluirán todos los campos marcados como recuperables en el esquema.</span><span class="sxs-lookup"><span data-stu-id="89b28-851">If unspecified, all fields marked as retrievable in the schema are included.</span></span> <span data-ttu-id="89b28-852">También se pueden solicitar explícitamente todos los campos estableciendo este parámetro en `*`.</span><span class="sxs-lookup"><span data-stu-id="89b28-852">You can also explicitly request all fields by setting this parameter to `*`.</span></span>

> [!NOTE]
> <span data-ttu-id="89b28-853">Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `select` en lugar de `$select`.</span><span class="sxs-lookup"><span data-stu-id="89b28-853">When calling **Search** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="89b28-854">`facet=[string]` (cero o más): un campo por el que establecer facetas.</span><span class="sxs-lookup"><span data-stu-id="89b28-854">`facet=[string]` (zero or more) - A field to facet by.</span></span> <span data-ttu-id="89b28-855">Es posible que la cadena contenga parámetros para personalizar la faceta expresada como pares `name:value` separados por comas.</span><span class="sxs-lookup"><span data-stu-id="89b28-855">Optionally the string may contain parameters to customize the faceting expressed as comma-separated `name:value` pairs.</span></span> <span data-ttu-id="89b28-856">Los parámetros válidos son:</span><span class="sxs-lookup"><span data-stu-id="89b28-856">Valid parameters are:</span></span>

* <span data-ttu-id="89b28-857">`count` (número máximo de términos de faceta; el valor predeterminado es 10).</span><span class="sxs-lookup"><span data-stu-id="89b28-857">`count` (max number of facet terms; default is 10).</span></span> <span data-ttu-id="89b28-858">No hay ningún máximo, pero los valores más altos incurren en una penalización de rendimiento correspondiente, especialmente si el campo con facetas contiene un gran número de términos únicos.</span><span class="sxs-lookup"><span data-stu-id="89b28-858">There is no maximum, but higher values incur a corresponding performance penalty, especially if the faceted field contains a large number of unique terms.</span></span>
  * <span data-ttu-id="89b28-859">Por ejemplo: `facet=category,count:5` obtiene las cinco categorías principales en los resultados de la faceta.</span><span class="sxs-lookup"><span data-stu-id="89b28-859">For example: `facet=category,count:5` gets the top five categories in facet results.</span></span>  
  * <span data-ttu-id="89b28-860">**Nota:** Si el parámetro `count` es menor que el número de términos únicos, es posible que los resultados no sean precisos.</span><span class="sxs-lookup"><span data-stu-id="89b28-860">**Note**: If the `count` parameter is less than the number of unique terms, the results may not be accurate.</span></span> <span data-ttu-id="89b28-861">Esto es debido a la manera en que se distribuyen las consultas de facetas entre las particiones.</span><span class="sxs-lookup"><span data-stu-id="89b28-861">This is due to the way faceting queries are distributed across shards.</span></span> <span data-ttu-id="89b28-862">Aumentar `count` generalmente aumenta la precisión de los recuentos de términos, pero ello afecta al rendimiento.</span><span class="sxs-lookup"><span data-stu-id="89b28-862">Increasing `count` generally increases the accuracy of the term counts, but at a performance cost.</span></span>
* <span data-ttu-id="89b28-863">`sort` (uno de `count` para ordenar de manera *descendente* por número, `-count` para ordenar de manera *ascendente* por número, `value` para ordenar de manera *ascendente* por valor o `-value` para ordenar de manera *descendente* por valor)</span><span class="sxs-lookup"><span data-stu-id="89b28-863">`sort` (one of `count` to sort *descending* by count, `-count` to sort *ascending* by count, `value` to sort *ascending* by value, or `-value` to sort *descending* by value)</span></span>
  * <span data-ttu-id="89b28-864">Por ejemplo: `facet=category,count:3,sort:count` obtiene las tres categorías principales en los resultados de la faceta en orden descendente por el número de documentos con el nombre de cada ciudad.</span><span class="sxs-lookup"><span data-stu-id="89b28-864">For example: `facet=category,count:3,sort:count` gets the top three categories in facet results in descending order by the number of documents with each city name.</span></span> <span data-ttu-id="89b28-865">Por ejemplo, si las tres categorías principales son Presupuesto, Motel y Lujo, y Presupuesto tiene 5 resultados, Motel tiene 6 y Lujo tiene 4, a continuación, los depósitos se colocarán en el orden siguiente: Motel, Presupuesto, Lujo.</span><span class="sxs-lookup"><span data-stu-id="89b28-865">For example, if the top three categories are Budget, Motel, and Luxury, and Budget has 5 hits, Motel has 6, and Luxury has 4, then the buckets will be in the order Motel, Budget, Luxury.</span></span>
  * <span data-ttu-id="89b28-866">Por ejemplo: `facet=rating,sort:-value` genera depósitos para todas las clasificaciones posibles en orden descendente por valor.</span><span class="sxs-lookup"><span data-stu-id="89b28-866">For example: `facet=rating,sort:-value` produces buckets for all possible ratings, in descending order by value.</span></span> <span data-ttu-id="89b28-867">Por ejemplo, si las clasificaciones son de 1 a 5, los depósitos se ordenarán como 5, 4, 3, 2, 1 independientemente de cuántos documentos coincidan con cada clasificación.</span><span class="sxs-lookup"><span data-stu-id="89b28-867">For example, if the ratings are from 1 to 5, the buckets will be ordered 5, 4, 3, 2, 1, irrespective of how many documents match each rating.</span></span>
* <span data-ttu-id="89b28-868">`values` (valores numéricos delimitados por canalización o `Edm.DateTimeOffset` que especifican un conjunto dinámico de valores de entrada de faceta)</span><span class="sxs-lookup"><span data-stu-id="89b28-868">`values` (pipe-delimited numeric or `Edm.DateTimeOffset` values specifying a dynamic set of facet entry values)</span></span>
  * <span data-ttu-id="89b28-869">Por ejemplo: `facet=baseRate,values:10|20` genera tres depósitos: uno para la tarifa base 0 hasta, pero sin incluir la tarifa 10, uno para 10 hasta pero sin incluir 20 y uno para 20 o superiores.</span><span class="sxs-lookup"><span data-stu-id="89b28-869">For example: `facet=baseRate,values:10|20` produces three buckets: One for base rate 0 up to but not including 10, one for 10 up to but not including 20, and one for 20 or higher.</span></span>
  * <span data-ttu-id="89b28-870">Por ejemplo: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` genera dos depósitos: uno para hoteles reformados antes de febrero de 2010 y otro para hoteles reformados desde el 1 de febrero de 2010 en adelante.</span><span class="sxs-lookup"><span data-stu-id="89b28-870">For example: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produces two buckets: One for hotels renovated before February 2010, and one for hotels renovated February 1st, 2010 or later.</span></span>
* <span data-ttu-id="89b28-871">`interval` (intervalo de número entero mayor que 0 para números, o `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` para los valores de fecha y hora)</span><span class="sxs-lookup"><span data-stu-id="89b28-871">`interval` (integer interval greater than 0 for numbers, or `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` for date time values)</span></span>
  * <span data-ttu-id="89b28-872">Por ejemplo: `facet=baseRate,interval:100` genera depósitos basados en intervalos de tarifas base de tamaño de 100.</span><span class="sxs-lookup"><span data-stu-id="89b28-872">For example: `facet=baseRate,interval:100` produces buckets based on base rate ranges of size 100.</span></span> <span data-ttu-id="89b28-873">Por ejemplo, si las tarifas base se encuentran entre 60 y 600 dólares, habrá depósitos para 0-100, 100-200, 300 200, 300-400, 400-500 y 500-600.</span><span class="sxs-lookup"><span data-stu-id="89b28-873">For example, if base rates are all between $60 and $600, there will be buckets for 0-100, 100-200, 200-300, 300-400, 400-500, and 500-600.</span></span>
  * <span data-ttu-id="89b28-874">Por ejemplo: `facet=lastRenovationDate,interval:year` genera un depósito para cada año en que se han reformado los hoteles.</span><span class="sxs-lookup"><span data-stu-id="89b28-874">For example: `facet=lastRenovationDate,interval:year` produces one bucket for each year when hotels were renovated.</span></span>
* <span data-ttu-id="89b28-875">`timeoffset` ([+-] hh: mm, [+-] hhmm, o [+-] hh) `timeoffset` es opcional.</span><span class="sxs-lookup"><span data-stu-id="89b28-875">`timeoffset` ([+-]hh:mm, [+-]hhmm, or [+-]hh) `timeoffset` is optional.</span></span> <span data-ttu-id="89b28-876">Solo se puede combinar con la opción `interval` y solo cuando se aplica a un campo de tipo `Edm.DateTimeOffset`.</span><span class="sxs-lookup"><span data-stu-id="89b28-876">It can only be combined with the `interval` option, and only when applied to a field of type `Edm.DateTimeOffset`.</span></span> <span data-ttu-id="89b28-877">El valor especifica la diferencia horaria UTC para explicar la configuración de los límites de tiempo.</span><span class="sxs-lookup"><span data-stu-id="89b28-877">The value specifies the UTC time offset to account for in setting time boundaries.</span></span>
  * <span data-ttu-id="89b28-878">Por ejemplo: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` usa el límite de día que comienza a la 01:00:00 UTC (medianoche en la zona horaria de destino)</span><span class="sxs-lookup"><span data-stu-id="89b28-878">For example: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` uses the day boundary that starts at 01:00:00 UTC (midnight in the target time zone)</span></span>
* <span data-ttu-id="89b28-879">**Nota**:`count` y `sort` se pueden combinar en la misma especificación de faceta, pero no se pueden combinar con `interval` o `values`, y `interval` y `values` no se pueden combinar entre sí.</span><span class="sxs-lookup"><span data-stu-id="89b28-879">**Note**: `count` and `sort` can be combined in the same facet specification, but they cannot be combined with `interval` or `values`, and `interval` and `values` cannot be combined together.</span></span>
* <span data-ttu-id="89b28-880">**Nota**: Las facetas de intervalo de fecha y hora se calculan en función de la hora UTC si `timeoffset` no se ha especificado.</span><span class="sxs-lookup"><span data-stu-id="89b28-880">**Note**: Interval facets on date time are computed based on UTC time if `timeoffset` is not specified.</span></span> <span data-ttu-id="89b28-881">Por ejemplo, para `facet=lastRenovationDate,interval:day`, el límite de día comienza a las 00:00:00 UTC.</span><span class="sxs-lookup"><span data-stu-id="89b28-881">For example: for `facet=lastRenovationDate,interval:day`, the day boundary starts at 00:00:00 UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="89b28-882">Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `facets` en lugar de `facet`.</span><span class="sxs-lookup"><span data-stu-id="89b28-882">When calling **Search** using POST, this parameter is named `facets` instead of `facet`.</span></span> <span data-ttu-id="89b28-883">Además, lo especifica como una matriz JSON de cadenas, donde cada cadena es una expresión de faceta independiente.</span><span class="sxs-lookup"><span data-stu-id="89b28-883">Also, you specify it as a JSON array of strings where each string is a separate facet expression.</span></span>
> 
> 

<span data-ttu-id="89b28-884">`$filter=[string]` (opcional): expresión de búsqueda estructurada en la sintaxis estándar de OData.</span><span class="sxs-lookup"><span data-stu-id="89b28-884">`$filter=[string]` (optional) - A structured search expression in standard OData syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="89b28-885">Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `filter` en lugar de `$filter`.</span><span class="sxs-lookup"><span data-stu-id="89b28-885">When calling **Search** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="89b28-886">`highlight=[string]` (opcional): conjunto de nombres de campos delimitado por comas usado para los resaltados de referencias.</span><span class="sxs-lookup"><span data-stu-id="89b28-886">`highlight=[string]` (optional) - A set of comma-separated field names used for hit highlights.</span></span> <span data-ttu-id="89b28-887">Solo se pueden usar `searchable` campos para resaltar las referencias.</span><span class="sxs-lookup"><span data-stu-id="89b28-887">Only `searchable` fields can be used for hit highlighting.</span></span>

<span data-ttu-id="89b28-888">`highlightPreTag=[string]` (opcional, se establece de forma predeterminada en `<em>`): una etiqueta de cadena que se antepone al resaltado de referencias.</span><span class="sxs-lookup"><span data-stu-id="89b28-888">`highlightPreTag=[string]` (optional, defaults to `<em>`) - A string tag that prepends to hit highlights.</span></span> <span data-ttu-id="89b28-889">Debe establecerse con `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="89b28-889">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="89b28-890">Al llamar a la **búsqueda** mediante GET, los caracteres reservados en la dirección URL deben estar codificados con porcentaje (por ejemplo, %23 en vez de #).</span><span class="sxs-lookup"><span data-stu-id="89b28-890">When calling **Search** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="89b28-891">`highlightPostTag=[string]` (opcional, se establece de forma predeterminada en `</em>`): una etiqueta de cadena que se antepone al resaltado de referencias.</span><span class="sxs-lookup"><span data-stu-id="89b28-891">`highlightPostTag=[string]` (optional, defaults to `</em>`) - a string tag that appends to hit highlights.</span></span> <span data-ttu-id="89b28-892">Debe establecerse con `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="89b28-892">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="89b28-893">Al llamar a la **búsqueda** mediante GET, los caracteres reservados en la dirección URL deben estar codificados con porcentaje (por ejemplo, %23 en vez de #).</span><span class="sxs-lookup"><span data-stu-id="89b28-893">When calling **Search** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="89b28-894">`scoringProfile=[string]` (opcional): nombre de un perfil de puntuación para evaluar puntuaciones de coincidencias de documentos coincidentes con el fin de ordenar los resultados.</span><span class="sxs-lookup"><span data-stu-id="89b28-894">`scoringProfile=[string]` (optional) - The name of a scoring profile to evaluate match scores for matching documents in order to sort the results.</span></span>

<span data-ttu-id="89b28-895">`scoringParameter=[string]` (cero o más): indica los valores para cada parámetro definido en una función de puntuación (por ejemplo, `referencePointParameter`) con el formato `name-value1,value2,...`.</span><span class="sxs-lookup"><span data-stu-id="89b28-895">`scoringParameter=[string]` (zero or more) - Indicates the values for each parameter defined in a scoring function (for example, `referencePointParameter`) using the format `name-value1,value2,...`.</span></span>

* <span data-ttu-id="89b28-896">Por ejemplo, si el perfil de puntuación define una función con un parámetro denominado "mylocation", la opción de cadena de consulta sería `&scoringParameter=mylocation--122.2,44.8`.</span><span class="sxs-lookup"><span data-stu-id="89b28-896">For example, if the scoring profile defines a function with a parameter called "mylocation" the query string option would be `&scoringParameter=mylocation--122.2,44.8`.</span></span> <span data-ttu-id="89b28-897">El primer guión separa el nombre de la lista de valores, mientras que el segundo guión es parte del primer valor (longitud en este ejemplo).</span><span class="sxs-lookup"><span data-stu-id="89b28-897">The first dash separates the name from the value list, while the second dash is part of the first value (longitude in this example).</span></span>
* <span data-ttu-id="89b28-898">Para los parámetros de puntuación así como para el aprovechamiento de etiquetas que contienen comas, es posible separar tales valores de la lista mediante el uso de comillas simples.</span><span class="sxs-lookup"><span data-stu-id="89b28-898">For scoring parameters such as for tag boosting that can contain commas, you can escape any such values in the list using single quotes.</span></span> <span data-ttu-id="89b28-899">Si los propios valores contienen comillas simples, puede separarlos duplicando la comilla simple.</span><span class="sxs-lookup"><span data-stu-id="89b28-899">If the values themselves contain single quotes, you can escape them by doubling.</span></span>
  * <span data-ttu-id="89b28-900">Por ejemplo, si tiene un parámetro de aprovechamiento de etiqueta llamado mytag y desea aprovechar los valores de la etiqueta Hello, O' Brien y Smith, la opción de la cadena de consulta sería `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span><span class="sxs-lookup"><span data-stu-id="89b28-900">For example, if you have a tag boosting parameter called "mytag" and you want to boost on the tag values "Hello, O'Brien" and "Smith", the query string option would be `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span></span> <span data-ttu-id="89b28-901">Tenga en cuenta que las comillas solo son necesarias para los valores que contienen comas.</span><span class="sxs-lookup"><span data-stu-id="89b28-901">Note that quotes are only required for values that contain commas.</span></span>

> [!NOTE]
> <span data-ttu-id="89b28-902">Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `scoringParameters` en lugar de `scoringParameter`.</span><span class="sxs-lookup"><span data-stu-id="89b28-902">When calling **Search** using POST, this parameter is named `scoringParameters` instead of `scoringParameter`.</span></span> <span data-ttu-id="89b28-903">Además, lo especifica como una matriz JSON de cadenas, donde cada cadena es un par `name-values` independiente.</span><span class="sxs-lookup"><span data-stu-id="89b28-903">Also, you specify it as a JSON array of strings where each string is a separate `name-values` pair.</span></span>
> 
> 

<span data-ttu-id="89b28-904">`minimumCoverage` (opcional, el valor predeterminado es 100): un número entre 0 y 100 que indica el porcentaje del índice que debe estar cubierto por una consulta de búsqueda para que la consulta se realice correctamente.</span><span class="sxs-lookup"><span data-stu-id="89b28-904">`minimumCoverage` (optional, defaults to 100) - a number between 0 and 100 indicating the percentage of the index that must be covered by a search query in order for the query to be reported as a success.</span></span> <span data-ttu-id="89b28-905">De forma predeterminada, todo el índice debe estar disponible o `Search` se devolverá el código de estado HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="89b28-905">By default, the entire index must be available or `Search` will return HTTP status code 503.</span></span> <span data-ttu-id="89b28-906">Si establece `minimumCoverage` y `Search` se realiza correctamente, devolverá HTTP 200 e incluye un valor `@search.coverage` en la respuesta que indica el porcentaje del índice que se incluyó en la consulta.</span><span class="sxs-lookup"><span data-stu-id="89b28-906">If you set `minimumCoverage` and `Search` succeeds, it will return HTTP 200 and include a `@search.coverage` value in the response indicating the percentage of the index that was included in the query.</span></span>

> [!NOTE]
> <span data-ttu-id="89b28-907">Establecer este parámetro en un valor inferior a 100 puede ser útil para garantizar la disponibilidad de la búsqueda incluso para servicios con una única réplica.</span><span class="sxs-lookup"><span data-stu-id="89b28-907">Setting this parameter to a value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="89b28-908">Sin embargo, no se garantiza que todos los documentos coincidentes existan en los resultados de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-908">However, not all matching documents are guaranteed to be present in the search results.</span></span> <span data-ttu-id="89b28-909">Si la recuperación de búsqueda es más importante para la aplicación que la disponibilidad, es mejor dejar `minimumCoverage` en su valor predeterminado de 100.</span><span class="sxs-lookup"><span data-stu-id="89b28-909">If search recall is more important to your application than availability, then it's best to leave `minimumCoverage` at its default value of 100.</span></span>
> 
> 

<span data-ttu-id="89b28-910">`api-version=[string]` (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="89b28-910">`api-version=[string]` (required).</span></span> <span data-ttu-id="89b28-911">La versión de vista previa es `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="89b28-911">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="89b28-912">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.</span><span class="sxs-lookup"><span data-stu-id="89b28-912">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="89b28-913">Nota: Para esta operación, `api-version` se especifica como un parámetro de consulta en la dirección URL sin tener en cuenta si se llama a la **Búsqueda** con GET o POST.</span><span class="sxs-lookup"><span data-stu-id="89b28-913">Note: For this operation, the `api-version` is specified as a query parameter in the URL regardless of whether you call **Search** with GET or POST.</span></span>

<span data-ttu-id="89b28-914">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-914">**Request Headers**</span></span>

<span data-ttu-id="89b28-915">En la lista siguiente se describen los encabezados de solicitud obligatorios y opcionales.</span><span class="sxs-lookup"><span data-stu-id="89b28-915">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="89b28-916">`api-key`: `api-key` se usa para autenticar la solicitud en su servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-916">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="89b28-917">Es un valor de cadena, único en su URL de servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-917">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="89b28-918">La solicitud de **búsqueda** puede especificar una clave de administración o una clave de consulta para `api-key`.</span><span class="sxs-lookup"><span data-stu-id="89b28-918">The **Search** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="89b28-919">También necesitará el nombre del servicio para construir la dirección URL de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="89b28-919">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="89b28-920">Puede obtener el nombre de servicio y `api-key` desde el panel de servicio en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="89b28-920">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="89b28-921">Consulte [Crear un servicio de Búsqueda de Azure en el portal](search-create-service-portal.md) para obtener ayuda sobre la navegación en páginas.</span><span class="sxs-lookup"><span data-stu-id="89b28-921">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="89b28-922">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-922">**Request Body**</span></span>

<span data-ttu-id="89b28-923">Para GET: ninguno.</span><span class="sxs-lookup"><span data-stu-id="89b28-923">For GET: None.</span></span>

<span data-ttu-id="89b28-924">Para POST:</span><span class="sxs-lookup"><span data-stu-id="89b28-924">For POST:</span></span>

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered to declare query successful; default 100),
      "moreLikeThis": "document_key" (mutually exclusive with "search" parameter),
      "orderby": "orderby_expression",
      "scoringParameters": [ "scoring_parameter_1", "scoring_parameter_2", ... ],
      "scoringProfile": "scoring_profile_name",
      "search": "simple_query_expression",
      "searchFields": "field_name_1, field_name_2, ...",
      "searchMode": "any" (default) | "all",
      "select": "field_name_1, field_name_2, ...",
      "skip": # (default 0),
      "top": #
    }

<span data-ttu-id="89b28-925">**Continuación de las respuestas de búsqueda parciales**</span><span class="sxs-lookup"><span data-stu-id="89b28-925">**Continuation of Partial Search Responses**</span></span>

<span data-ttu-id="89b28-926">A veces, Búsqueda de Azure no puede devolver todos los resultados solicitados en una sola respuesta de Búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-926">Sometimes Azure Search can't return all the requested results in a single Search response.</span></span> <span data-ttu-id="89b28-927">Esto puede ocurrir por diferentes motivos; por ejemplo, cuando la consulta solicita demasiados documentos al no especificar `$top` o especificar un valor para `$top` que es demasiado grande.</span><span class="sxs-lookup"><span data-stu-id="89b28-927">This can happen for different reasons, such as when the query requests too many documents by not specifying `$top` or specifying a value for `$top` that is too large.</span></span> <span data-ttu-id="89b28-928">En tales casos, Búsqueda de Azure incluirá la anotación `@odata.nextLink` en el cuerpo de respuesta, y también `@search.nextPageParameters` si era una solicitud POST.</span><span class="sxs-lookup"><span data-stu-id="89b28-928">In such cases, Azure Search will include the `@odata.nextLink` annotation in the response body, and also `@search.nextPageParameters` if it was a POST request.</span></span> <span data-ttu-id="89b28-929">Puede usar los valores de estas anotaciones para formular otra solicitud de Búsqueda a fin de obtener la siguiente parte de la respuesta de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-929">You can use the values of these annotations to formulate another Search request to get the next part of the search response.</span></span> <span data-ttu-id="89b28-930">Esto se denomina ***continuación*** de la solicitud de búsqueda original, y las anotaciones se suelen llamar ***tokens de continuación***.</span><span class="sxs-lookup"><span data-stu-id="89b28-930">This is called a ***continuation*** of the original Search request, and the annotations are generally called ***continuation tokens***.</span></span> <span data-ttu-id="89b28-931">Consulte [el ejemplo siguiente](#SearchResponse) para obtener más información sobre la sintaxis de estas anotaciones y el lugar en que aparecen en el cuerpo de respuesta.</span><span class="sxs-lookup"><span data-stu-id="89b28-931">See [the example below](#SearchResponse) for details on the syntax of these annotations and where they appear in the response body.</span></span> 

<span data-ttu-id="89b28-932">Los motivos por los que Búsqueda de Azure podría devolver tokens de continuación son específicos de la implementación y están sujetos a cambio.</span><span class="sxs-lookup"><span data-stu-id="89b28-932">The reasons why Azure Search might return continuation tokens are implementation-specific and subject to change.</span></span> <span data-ttu-id="89b28-933">Los clientes sólidos deben estar siempre preparados para controlar los casos en que se devuelven menos documentos de lo esperado y se incluye un token de continuación para seguir recuperando documentos.</span><span class="sxs-lookup"><span data-stu-id="89b28-933">Robust clients should always be ready to handle cases where fewer documents than expected are returned and a continuation token is included to continue retrieving documents.</span></span> <span data-ttu-id="89b28-934">Tenga en cuenta también que debe usar el mismo método HTTP como solicitud original para poder continuar.</span><span class="sxs-lookup"><span data-stu-id="89b28-934">Also note that you must use the same HTTP method as the original request in order to continue.</span></span> <span data-ttu-id="89b28-935">Por ejemplo, si envía una solicitud GET, las solicitudes de continuación que envíe también deben utilizar GET (y lo mismo para POST).</span><span class="sxs-lookup"><span data-stu-id="89b28-935">For example, if you sent a GET request, any continuation requests you send must also use GET (and likewise for POST).</span></span>

<span data-ttu-id="89b28-936"><a name="SearchResponse"></a>
**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="89b28-936"><a name="SearchResponse"></a>
**Response**</span></span>

<span data-ttu-id="89b28-937">Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.</span><span class="sxs-lookup"><span data-stu-id="89b28-937">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@odata.count": # (if $count=true was provided in the query),
      "@search.coverage": # (if minimumCoverage was provided in the query),
      "@search.facets": { (if faceting was specified in the query)
        "facet_field": [
          {
            "value": facet_entry_value (for non-range facets),
            "from": facet_entry_value (for range facets),
            "to": facet_entry_value (for range facets),
            "count": number_of_documents
          }
        ],
        ...
      },
      "@search.nextPageParameters": { (request body to fetch the next page of results if not all results could be returned in this response and Search was called with POST)
        "count": ... (value from request body if present),
        "facets": ... (value from request body if present),
        "filter": ... (value from request body if present),
        "highlight": ... (value from request body if present),
        "highlightPreTag": ... (value from request body if present),
        "highlightPostTag": ... (value from request body if present),
        "minimumCoverage": ... (value from request body if present),
        "moreLikeThis": ... (value from request body if present),
        "orderby": ... (value from request body if present),
        "scoringParameters": ... (value from request body if present),
        "scoringProfile": ... (value from request body if present),
        "search": ... (value from request body if present),
        "searchFields": ... (value from request body if present),
        "searchMode": ... (value from request body if present),
        "select": ... (value from request body if present),
        "skip": ... (page size plus value from request body if present),
        "top": ... (value from request body if present minus page size),
      },
      "value": [
        {
          "@search.score": document_score (if a text query was provided),
          "@search.highlights": {
            field_name: [ subset of text, ... ],
            ...
          },
          key_field_name: document_key,
          field_name: field_value (retrievable fields or specified projection),
          ...
        },
        ...
      ],
      "@odata.nextLink": (URL to fetch the next page of results if not all results could be returned in this response; Applies to both GET and POST)
    }

<span data-ttu-id="89b28-938">**Ejemplos:**</span><span class="sxs-lookup"><span data-stu-id="89b28-938">**Examples:**</span></span>

<span data-ttu-id="89b28-939">Puede encontrar ejemplos adicionales en la página [Sintaxis de expresiones de OData para la Búsqueda de Azure](https://msdn.microsoft.com/library/azure/dn798921.aspx) .</span><span class="sxs-lookup"><span data-stu-id="89b28-939">You can find additional examples on the [OData Expression Syntax for Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) page.</span></span>

1)    <span data-ttu-id="89b28-940">Busque en el índice por fecha en orden descendente.</span><span class="sxs-lookup"><span data-stu-id="89b28-940">Search the Index sorted descending by date.</span></span>

    <span data-ttu-id="89b28-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="89b28-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="89b28-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span><span class="sxs-lookup"><span data-stu-id="89b28-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span></span>

2)    <span data-ttu-id="89b28-943">En una búsqueda con facetas, busque en el índice y recupere las facetas de categorías, clasificación, etiquetas, así como elementos con baseRate en intervalos específicos:</span><span class="sxs-lookup"><span data-stu-id="89b28-943">In a faceted search, search the index and retrieve facets for categories, rating, tags, as well as items with baseRate in specific ranges:</span></span>

    <span data-ttu-id="89b28-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="89b28-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="89b28-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span><span class="sxs-lookup"><span data-stu-id="89b28-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span></span>

3)    <span data-ttu-id="89b28-946">Mediante un filtro, restrinja los resultados de la consulta con facetas anterior después de que el usuario haga clic en la tarifa 3 y en la categoría "Motel":</span><span class="sxs-lookup"><span data-stu-id="89b28-946">Using a filter, narrow down the previous faceted query results after the user clicks on rating 3 and category "Motel":</span></span>

    <span data-ttu-id="89b28-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="89b28-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="89b28-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span><span class="sxs-lookup"><span data-stu-id="89b28-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span></span>

4) <span data-ttu-id="89b28-949">En una búsqueda con facetas, establezca un límite superior en términos únicos devueltos en una consulta.</span><span class="sxs-lookup"><span data-stu-id="89b28-949">In a faceted search, set an upper limit on unique terms returned in a query.</span></span> <span data-ttu-id="89b28-950">El valor predeterminado es 10, pero se puede aumentar o disminuir este valor utilizando el parámetro `count` en el atributo `facet`:</span><span class="sxs-lookup"><span data-stu-id="89b28-950">The default is 10, but you can increase or decrease this value using the `count` parameter on the `facet` attribute:</span></span>

    <span data-ttu-id="89b28-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="89b28-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="89b28-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span><span class="sxs-lookup"><span data-stu-id="89b28-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span></span>

5)    <span data-ttu-id="89b28-953">Busque en el índice en campos específicos; por ejemplo, un campo específico del idioma:</span><span class="sxs-lookup"><span data-stu-id="89b28-953">Search the Index within specific fields; For example, a language-specific field:</span></span>

    <span data-ttu-id="89b28-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="89b28-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="89b28-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span><span class="sxs-lookup"><span data-stu-id="89b28-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span></span>

6) <span data-ttu-id="89b28-956">Busque en el índice en varios campos.</span><span class="sxs-lookup"><span data-stu-id="89b28-956">Search the Index across multiple fields.</span></span> <span data-ttu-id="89b28-957">Por ejemplo, puede almacenar y consultar los campos de búsqueda en varios idiomas, todo ello en el mismo índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-957">For example, you can store and query searchable fields in multiple languages, all within the same index.</span></span>  <span data-ttu-id="89b28-958">Si las descripciones de inglés y francés coexisten en el mismo documento, puede devolver cualquiera en los resultados de la consulta:</span><span class="sxs-lookup"><span data-stu-id="89b28-958">If English and French descriptions co-exist in the same document, you can return any or all in the query results:</span></span>

    <span data-ttu-id="89b28-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="89b28-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="89b28-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span><span class="sxs-lookup"><span data-stu-id="89b28-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span></span>

<span data-ttu-id="89b28-961">Tenga en cuenta que solo puede consultar un índice de cada vez.</span><span class="sxs-lookup"><span data-stu-id="89b28-961">Note that you can only query one index at a time.</span></span> <span data-ttu-id="89b28-962">No cree varios índices para cada idioma a menos que planee consultar una de cada vez.</span><span class="sxs-lookup"><span data-stu-id="89b28-962">Do not create multiple indexes for each language unless you plan to query one at a time.</span></span>

7)    <span data-ttu-id="89b28-963">Paginación: obtenga la primera página de los elementos (el tamaño de la página es 10):</span><span class="sxs-lookup"><span data-stu-id="89b28-963">Paging - Get the 1st page of items (page size is 10):</span></span>

    <span data-ttu-id="89b28-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="89b28-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="89b28-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="89b28-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span></span>

8)    <span data-ttu-id="89b28-966">Paginación: obtenga la segunda página de los elementos (el tamaño de la página es 10):</span><span class="sxs-lookup"><span data-stu-id="89b28-966">Paging - Get the 2nd page of items (page size is 10):</span></span>

    <span data-ttu-id="89b28-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="89b28-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="89b28-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="89b28-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span></span>

9)    <span data-ttu-id="89b28-969">Recupere un conjunto específico de campos:</span><span class="sxs-lookup"><span data-stu-id="89b28-969">Retrieve a specific set of fields:</span></span>

    <span data-ttu-id="89b28-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="89b28-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="89b28-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span><span class="sxs-lookup"><span data-stu-id="89b28-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span></span>

10)  <span data-ttu-id="89b28-972">Recupere documentos que coincidan con una expresión de filtro específica:</span><span class="sxs-lookup"><span data-stu-id="89b28-972">Retrieve documents matching a specific filter expression:</span></span>

    <span data-ttu-id="89b28-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="89b28-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="89b28-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span><span class="sxs-lookup"><span data-stu-id="89b28-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span></span>

11) <span data-ttu-id="89b28-975">Busque en el índice y obtenga fragmentos con resaltado de referencias.</span><span class="sxs-lookup"><span data-stu-id="89b28-975">Search the index and return fragments with hit highlights</span></span>

    <span data-ttu-id="89b28-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="89b28-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="89b28-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span><span class="sxs-lookup"><span data-stu-id="89b28-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span></span>

12) <span data-ttu-id="89b28-978">Busque en el índice y obtenga documentos ordenados de más próximos a más alejados de una ubicación de referencia.</span><span class="sxs-lookup"><span data-stu-id="89b28-978">Search the index and return documents sorted from closer to farther away from a reference location</span></span>

    <span data-ttu-id="89b28-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="89b28-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="89b28-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span><span class="sxs-lookup"><span data-stu-id="89b28-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span></span>

13) <span data-ttu-id="89b28-981">Busque en el índice suponiendo que haya un perfil de puntuaciones denominado "geográfico" con dos funciones de puntuación de distancia, una para definir un parámetro llamado "currentLocation" y otra para definir un parámetro llamado "lastLocation".</span><span class="sxs-lookup"><span data-stu-id="89b28-981">Search the index assuming there's a scoring profile called "geo" with two distance scoring functions, one defining a parameter called "currentLocation" and one defining a parameter called "lastLocation"</span></span>

    <span data-ttu-id="89b28-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="89b28-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="89b28-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span><span class="sxs-lookup"><span data-stu-id="89b28-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span></span>

14) <span data-ttu-id="89b28-984">Busque documentos en el índice utilizando la [sintaxis de consulta simple](https://msdn.microsoft.com/library/dn798920.aspx).</span><span class="sxs-lookup"><span data-stu-id="89b28-984">Find documents in the index using [simple query syntax](https://msdn.microsoft.com/library/dn798920.aspx).</span></span> <span data-ttu-id="89b28-985">Esta consulta devuelve los hoteles, en los que los campos de búsqueda contienen los términos "comodidad" y "ubicación", pero no "motel":</span><span class="sxs-lookup"><span data-stu-id="89b28-985">This query returns hotels where searchable fields contain the terms "comfort" and "location" but not "motel":</span></span>

    <span data-ttu-id="89b28-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="89b28-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="89b28-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="89b28-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span></span>

<span data-ttu-id="89b28-988">Tenga en cuenta el uso de `searchMode=all` anteriormente.</span><span class="sxs-lookup"><span data-stu-id="89b28-988">Note the use of `searchMode=all` above.</span></span> <span data-ttu-id="89b28-989">Incluyendo este parámetro se invalida el valor predeterminado de `searchMode=any`, lo que asegura que `-motel` significa "Y NO" en lugar de "O NO".</span><span class="sxs-lookup"><span data-stu-id="89b28-989">Including this parameter overrides the default of `searchMode=any`, ensuring that `-motel` means "AND NOT" instead of "OR NOT".</span></span> <span data-ttu-id="89b28-990">Sin `searchMode=all`, obtendrá "O NO", que expandirá en lugar de restringir los resultados de la búsqueda, lo cual puede resultar contradictorio para algunos usuarios.</span><span class="sxs-lookup"><span data-stu-id="89b28-990">Without `searchMode=all`, you get "OR NOT" which expands rather than restricts search results, and this can be counter-intuitive to some users.</span></span>

15) <span data-ttu-id="89b28-991">Busque documentos en el índice usando la [sintaxis de consulta de Lucene](https://msdn.microsoft.com/library/mt589323.aspx).</span><span class="sxs-lookup"><span data-stu-id="89b28-991">Find documents in the index using [lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx).</span></span> <span data-ttu-id="89b28-992">Esta consulta devuelve los hoteles en los que el campo de categoría contiene el término "budget" y todos los campos de búsqueda que incluyen la expresión "recently renovated".</span><span class="sxs-lookup"><span data-stu-id="89b28-992">This query returns hotels where the category field contains the term "budget" and all searchable fields containing the phrase "recently renovated".</span></span> <span data-ttu-id="89b28-993">Los documentos que contienen la expresión "recently renovated" tienen una clasificación más alta como resultado del valor de aumento del término (3)</span><span class="sxs-lookup"><span data-stu-id="89b28-993">Documents containing the phrase "recently renovated" are ranked higher as a result of the term boost value (3)</span></span>

    <span data-ttu-id="89b28-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span><span class="sxs-lookup"><span data-stu-id="89b28-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span></span>

    <span data-ttu-id="89b28-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="89b28-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span></span>

<a name="LookupAPI"></a>

## <a name="lookup-document"></a><span data-ttu-id="89b28-996">Buscar documento</span><span class="sxs-lookup"><span data-stu-id="89b28-996">Lookup Document</span></span>
<span data-ttu-id="89b28-997">La operación **Buscar documento** permite recuperar un documento de Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="89b28-997">The **Lookup Document** operation retrieves a document from Azure Search.</span></span> <span data-ttu-id="89b28-998">Esto resulta útil cuando un usuario hace clic en un resultado de búsqueda específico y desea buscar detalles específicos acerca de ese documento.</span><span class="sxs-lookup"><span data-stu-id="89b28-998">This is useful when a user clicks on a specific search result, and you want to look up specific details about that document.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

<span data-ttu-id="89b28-999">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-999">**Request**</span></span>

<span data-ttu-id="89b28-1000">HTTPS es necesario para las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-1000">HTTPS is required for service requests.</span></span> <span data-ttu-id="89b28-1001">La solicitud **Buscar documento** se puede generar del modo indicado a continuación.</span><span class="sxs-lookup"><span data-stu-id="89b28-1001">The **Lookup Document** request can be constructed as follows.</span></span>

    GET /indexes/[index name]/docs/key?[query parameters]

<span data-ttu-id="89b28-1002">También puede usar la sintaxis de OData tradicional para la búsqueda de claves:</span><span class="sxs-lookup"><span data-stu-id="89b28-1002">Alternatively, you can use the traditional OData syntax for key lookup:</span></span>

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

<span data-ttu-id="89b28-1003">El URI de solicitud incluye un [nombre de índice] y una [clave], que especifica qué documento para recuperar del índice correspondiente.</span><span class="sxs-lookup"><span data-stu-id="89b28-1003">The request URI includes an [index name] and [key], specifying which document to retrieve from which index.</span></span> <span data-ttu-id="89b28-1004">Solamente se puede obtener un documento de cada vez.</span><span class="sxs-lookup"><span data-stu-id="89b28-1004">You can only get one document at a time.</span></span> <span data-ttu-id="89b28-1005">Utilice **Búsqueda** para obtener varios documentos en una única solicitud.</span><span class="sxs-lookup"><span data-stu-id="89b28-1005">Use **Search** to get multiple documents in a single request.</span></span>

<span data-ttu-id="89b28-1006">**Parámetros de consulta**</span><span class="sxs-lookup"><span data-stu-id="89b28-1006">**Query Parameters**</span></span>

<span data-ttu-id="89b28-1007">`$select=[string]` (opcional): lista de campos separados por comas para recuperar.</span><span class="sxs-lookup"><span data-stu-id="89b28-1007">`$select=[string]` (optional) - a list of comma-separated fields to retrieve.</span></span> <span data-ttu-id="89b28-1008">Si no se especifica nada o se establece en `*`, se incluirán en la proyección todos los campos marcados como recuperables en el esquema.</span><span class="sxs-lookup"><span data-stu-id="89b28-1008">If unspecified or set to `*`, all fields marked as retrievable in the schema are included in the projection.</span></span>

<span data-ttu-id="89b28-1009">`api-version=[string]` (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="89b28-1009">`api-version=[string]` (required).</span></span> <span data-ttu-id="89b28-1010">La versión de vista previa es `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="89b28-1010">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="89b28-1011">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.</span><span class="sxs-lookup"><span data-stu-id="89b28-1011">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="89b28-1012">Nota: Para esta operación, `api-version` se especifica como parámetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="89b28-1012">Note: For this operation, the `api-version` is specified as a query parameter.</span></span>

<span data-ttu-id="89b28-1013">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-1013">**Request Headers**</span></span>

<span data-ttu-id="89b28-1014">En la lista siguiente se describen los encabezados de solicitud obligatorios y opcionales.</span><span class="sxs-lookup"><span data-stu-id="89b28-1014">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="89b28-1015">`api-key`: `api-key` se usa para autenticar la solicitud en su servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-1015">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="89b28-1016">Es un valor de cadena, único en su URL de servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-1016">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="89b28-1017">La solicitud **Buscar documento** puede especificar una clave de administración o una clave de consulta para `api-key`.</span><span class="sxs-lookup"><span data-stu-id="89b28-1017">The **Lookup Document** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="89b28-1018">También necesitará el nombre del servicio para construir la dirección URL de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="89b28-1018">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="89b28-1019">Puede obtener el nombre de servicio y `api-key` desde el panel de servicio en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="89b28-1019">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="89b28-1020">Consulte [Crear un servicio de Búsqueda de Azure en el portal](search-create-service-portal.md) para obtener ayuda sobre la navegación en páginas.</span><span class="sxs-lookup"><span data-stu-id="89b28-1020">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="89b28-1021">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-1021">**Request Body**</span></span>

<span data-ttu-id="89b28-1022">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="89b28-1022">None.</span></span>

<span data-ttu-id="89b28-1023">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="89b28-1023">**Response**</span></span>

<span data-ttu-id="89b28-1024">Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.</span><span class="sxs-lookup"><span data-stu-id="89b28-1024">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      field_name: field_value (fields matching the default or specified projection)
    }

<span data-ttu-id="89b28-1025">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="89b28-1025">**Example**</span></span>

<span data-ttu-id="89b28-1026">Busque el documento que tiene la clave "2"</span><span class="sxs-lookup"><span data-stu-id="89b28-1026">Lookup the document that has key '2'</span></span>

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

<span data-ttu-id="89b28-1027">Busque el documento que tiene la clave "3" con la sintaxis de OData:</span><span class="sxs-lookup"><span data-stu-id="89b28-1027">Lookup the document that has key '3' using OData syntax:</span></span>

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a><span data-ttu-id="89b28-1028">Documentos de recuento</span><span class="sxs-lookup"><span data-stu-id="89b28-1028">Count Documents</span></span>
<span data-ttu-id="89b28-1029">La operación **Documentos de recuento** recupera un recuento del número de documentos en un índice de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-1029">The **Count Documents** operation retrieves a count of the number of documents in a search index.</span></span> <span data-ttu-id="89b28-1030">La sintaxis `$count` forma parte del protocolo OData.</span><span class="sxs-lookup"><span data-stu-id="89b28-1030">The `$count` syntax is part of the OData protocol.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

<span data-ttu-id="89b28-1031">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-1031">**Request**</span></span>

<span data-ttu-id="89b28-1032">HTTPS es necesario para las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-1032">HTTPS is required for service requests.</span></span> <span data-ttu-id="89b28-1033">La solicitud **Documentos de recuento** puede crearse mediante el método GET.</span><span class="sxs-lookup"><span data-stu-id="89b28-1033">The **Count Documents** request can be constructed using the GET method.</span></span>

<span data-ttu-id="89b28-1034">El [nombre de índice] del URI de la solicitud indica al servicio que devuelva un recuento de todos los elementos de la colección de documentos del índice especificado.</span><span class="sxs-lookup"><span data-stu-id="89b28-1034">The [index name] in the request URI tells the service to return a count of all items in the docs collection of the specified index.</span></span>

<span data-ttu-id="89b28-1035">`api-version=[string]` (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="89b28-1035">`api-version=[string]` (required).</span></span> <span data-ttu-id="89b28-1036">La versión de vista previa es `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="89b28-1036">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="89b28-1037">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.</span><span class="sxs-lookup"><span data-stu-id="89b28-1037">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="89b28-1038">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-1038">**Request Headers**</span></span>

<span data-ttu-id="89b28-1039">En la lista siguiente se describen los encabezados de solicitud obligatorios y opcionales.</span><span class="sxs-lookup"><span data-stu-id="89b28-1039">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="89b28-1040">`Accept`: este valor debe establecerse en `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="89b28-1040">`Accept`: This value must be set to `text/plain`.</span></span>
* <span data-ttu-id="89b28-1041">`api-key`: `api-key` se usa para autenticar la solicitud en su servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-1041">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="89b28-1042">Es un valor de cadena, único en su URL de servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-1042">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="89b28-1043">La solicitud **Documentos de recuento** puede especificar una clave de administración o una clave de consulta para `api-key`.</span><span class="sxs-lookup"><span data-stu-id="89b28-1043">The **Count Documents** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="89b28-1044">También necesitará el nombre del servicio para construir la dirección URL de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="89b28-1044">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="89b28-1045">Puede obtener el nombre de servicio y `api-key` desde el panel de servicio en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="89b28-1045">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="89b28-1046">Consulte [Crear un servicio de Búsqueda de Azure en el portal](search-create-service-portal.md) para obtener ayuda sobre la navegación en páginas.</span><span class="sxs-lookup"><span data-stu-id="89b28-1046">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="89b28-1047">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-1047">**Request Body**</span></span>

<span data-ttu-id="89b28-1048">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="89b28-1048">None.</span></span>

<span data-ttu-id="89b28-1049">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="89b28-1049">**Response**</span></span>

<span data-ttu-id="89b28-1050">Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.</span><span class="sxs-lookup"><span data-stu-id="89b28-1050">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="89b28-1051">El cuerpo de la respuesta contiene el valor de recuento como un entero con formato de texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="89b28-1051">The response body contains the count value as an integer formatted in plain text.</span></span>

<a name="Suggestions"></a>

## <a name="suggestions"></a><span data-ttu-id="89b28-1052">Sugerencias</span><span class="sxs-lookup"><span data-stu-id="89b28-1052">Suggestions</span></span>
<span data-ttu-id="89b28-1053">La operación **Sugerencias** recupera sugerencias basadas en la entrada de búsqueda parcial.</span><span class="sxs-lookup"><span data-stu-id="89b28-1053">The **Suggestions** operation retrieves suggestions based on partial search input.</span></span> <span data-ttu-id="89b28-1054">Se suele usar en los cuadros de búsqueda para proporcionar sugerencias anticipadas cuando los usuarios están introduciendo términos de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-1054">It's typically used in search boxes to provide type-ahead suggestions as users are entering search terms.</span></span>

<span data-ttu-id="89b28-1055">Las solicitudes de sugerencias están destinadas a sugerir documentos de destino, por lo que el texto sugerido puede repetirse si varios documentos candidatos coinciden con la misma entrada de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-1055">Suggestion requests aim at suggesting target documents, so the suggested text may be repeated if multiple candidate documents match the same search input.</span></span> <span data-ttu-id="89b28-1056">Puede usar `$select` para recuperar otros campos del documento (incluida la clave del documento) para que pueda indicar qué documento es el origen para cada sugerencia.</span><span class="sxs-lookup"><span data-stu-id="89b28-1056">You can use `$select` to retrieve other document fields (including the document key) so that you can tell which document is the source for each suggestion.</span></span>

<span data-ttu-id="89b28-1057">Una operación **Sugerencias** se emite como una solicitud GET o POST.</span><span class="sxs-lookup"><span data-stu-id="89b28-1057">A **Suggestions** operation is issued as a GET or POST request.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="89b28-1058">**Cuándo usar POST en lugar de GET**</span><span class="sxs-lookup"><span data-stu-id="89b28-1058">**When to use POST instead of GET**</span></span>

<span data-ttu-id="89b28-1059">Cuando use HTTP GET para llamar a la API de **Sugerencias** , deberá tener en cuenta que la longitud de la URL de la solicitud no puede superar los 8 KB.</span><span class="sxs-lookup"><span data-stu-id="89b28-1059">When you use HTTP GET to call the **Suggestions** API, you need to be aware that the length of the request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="89b28-1060">Esto suele ser suficiente para la mayoría de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="89b28-1060">This is usually enough for most applications.</span></span> <span data-ttu-id="89b28-1061">Sin embargo, algunas aplicaciones generan consultas muy extensas, en concreto, expresiones de filtro de OData.</span><span class="sxs-lookup"><span data-stu-id="89b28-1061">However, some applications produce very large queries, specifically OData filter expressions.</span></span> <span data-ttu-id="89b28-1062">Para estas aplicaciones, el uso de HTTP POST es una opción mejor porque permite filtros mayores que GET.</span><span class="sxs-lookup"><span data-stu-id="89b28-1062">For these applications, using HTTP POST is a better choice because it allows larger filters than GET.</span></span> <span data-ttu-id="89b28-1063">Con POST, el número de cláusulas en un filtro es el factor limitador, no el tamaño de la cadena del filtro, ya que el límite de tamaño de la solicitud POST es de 16 MB aproximadamente.</span><span class="sxs-lookup"><span data-stu-id="89b28-1063">With POST, the number of clauses in a filter is the limiting factor, not the size of the raw filter string since the request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="89b28-1064">Aunque el límite de tamaño de la solicitud POST es muy grande, las expresiones de filtro no pueden ser arbitrariamente complejas.</span><span class="sxs-lookup"><span data-stu-id="89b28-1064">Even though the POST request size limit is very large, filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="89b28-1065">Consulte [Sintaxis de expresiones de OData para Búsqueda de Azure](https://msdn.microsoft.com/library/dn798921.aspx) para obtener más información sobre las limitaciones de complejidad de filtros.</span><span class="sxs-lookup"><span data-stu-id="89b28-1065">See [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="89b28-1066">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-1066">**Request**</span></span>

<span data-ttu-id="89b28-1067">HTTPS es necesario para las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-1067">HTTPS is required for service requests.</span></span> <span data-ttu-id="89b28-1068">La solicitud de **Sugerencias** puede crearse mediante los métodos GET o POST.</span><span class="sxs-lookup"><span data-stu-id="89b28-1068">The **Suggestions** request can be constructed using the GET or POST methods.</span></span>

<span data-ttu-id="89b28-1069">El URI de la solicitud especifica el nombre del índice que se consulta.</span><span class="sxs-lookup"><span data-stu-id="89b28-1069">The request URI specifies the name of the index to query.</span></span> <span data-ttu-id="89b28-1070">Los parámetros, como el término de búsqueda de entrada parcial, se especifican en la cadena de consulta en el caso de solicitudes GET y en el cuerpo de la solicitud en el caso de las solicitudes POST.</span><span class="sxs-lookup"><span data-stu-id="89b28-1070">Parameters, such as the partially input search term, are specified on the query string in the case of GET requests, and in the request body in the case of POST requests.</span></span>

<span data-ttu-id="89b28-1071">Como práctica recomendada al crear solicitudes GET, recuerde [codificar con URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) los parámetros de consulta específicos al llamar a la API de REST directamente.</span><span class="sxs-lookup"><span data-stu-id="89b28-1071">As a best practice when creating GET requests, remember to [URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling the REST API directly.</span></span> <span data-ttu-id="89b28-1072">Para las operaciones **Sugerencias** , se incluye lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="89b28-1072">For **Suggestions** operations, this includes:</span></span>

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

<span data-ttu-id="89b28-1073">Solo se recomienda la codificación de direcciones URL en los parámetros de consulta anterior.</span><span class="sxs-lookup"><span data-stu-id="89b28-1073">URL encoding is only recommended on the above query parameters.</span></span> <span data-ttu-id="89b28-1074">Si codifica con URL involuntariamente la cadena de consulta completa (todo lo situado después de la?), las solicitudes se dividirán.</span><span class="sxs-lookup"><span data-stu-id="89b28-1074">If you inadvertently URL-encode the entire query string (everything after the ?), requests will break.</span></span>

<span data-ttu-id="89b28-1075">Además, la codificación con URL solo es necesaria cuando se llama directamente a la API de REST directamente con GET.</span><span class="sxs-lookup"><span data-stu-id="89b28-1075">Also, URL encoding is only necessary when calling the REST API directly using GET.</span></span> <span data-ttu-id="89b28-1076">No se necesita ninguna codificación de URL para llamar a las **Sugerencias** mediante POST o cuando se usa la [biblioteca de cliente .NET](https://msdn.microsoft.com/library/dn951165.aspx), que controla la codificación de direcciones URL en su lugar.</span><span class="sxs-lookup"><span data-stu-id="89b28-1076">No URL encoding is necessary when calling **Suggestions** using POST, or when using the [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="89b28-1077">**Parámetros de consulta**</span><span class="sxs-lookup"><span data-stu-id="89b28-1077">**Query Parameters**</span></span>

<span data-ttu-id="89b28-1078">**Sugerencias** acepta varios parámetros que ofrecen criterios de consulta y que también especifican el comportamiento de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-1078">**Suggestions** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="89b28-1079">Estos parámetros se especifican en la cadena de consulta URL al llamar a las **Sugerencias** mediante GET y como propiedades JSON en el cuerpo de solicitud al llamar a las **Sugerencias** mediante POST.</span><span class="sxs-lookup"><span data-stu-id="89b28-1079">You provide these parameters in the URL query string when calling **Suggestions** via GET, and as JSON properties in the request body when calling **Suggestions** via POST.</span></span> <span data-ttu-id="89b28-1080">La sintaxis de algunos parámetros es algo diferente entre GET y POST.</span><span class="sxs-lookup"><span data-stu-id="89b28-1080">The syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="89b28-1081">Estas diferencias se indican como aplicables a continuación:</span><span class="sxs-lookup"><span data-stu-id="89b28-1081">These differences are noted as applicable below:</span></span>

<span data-ttu-id="89b28-1082">`search=[string]` : texto de búsqueda que se utiliza para sugerir las consultas.</span><span class="sxs-lookup"><span data-stu-id="89b28-1082">`search=[string]` - the search text to use to suggest queries.</span></span> <span data-ttu-id="89b28-1083">Debe tener 1 carácter como mínimo y no más de 100 caracteres.</span><span class="sxs-lookup"><span data-stu-id="89b28-1083">Must be at least 1 character, and no more than 100 characters.</span></span>

<span data-ttu-id="89b28-1084">`highlightPreTag=[string]` (opcional): una etiqueta de cadena que se antepone a resultados de búsquedas.</span><span class="sxs-lookup"><span data-stu-id="89b28-1084">`highlightPreTag=[string]` (optional) - a string tag that prepends to search hits.</span></span> <span data-ttu-id="89b28-1085">Debe establecerse con `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="89b28-1085">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="89b28-1086">Al llamar a las **Sugerencias** mediante GET, los caracteres reservados en la dirección URL deben estar codificados con porcentaje (por ejemplo, %23 en vez de #).</span><span class="sxs-lookup"><span data-stu-id="89b28-1086">When calling **Suggestions** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="89b28-1087">`highlightPostTag=[string]` (opcional): una etiqueta de cadena que se adjunta a resultados de búsquedas.</span><span class="sxs-lookup"><span data-stu-id="89b28-1087">`highlightPostTag=[string]` (optional) - a string tag that appends to search hits.</span></span> <span data-ttu-id="89b28-1088">Debe establecerse con `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="89b28-1088">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="89b28-1089">Al llamar a las **Sugerencias** mediante GET, los caracteres reservados en la dirección URL deben estar codificados con porcentaje (por ejemplo, %23 en vez de #).</span><span class="sxs-lookup"><span data-stu-id="89b28-1089">When calling **Suggestions** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="89b28-1090">`suggesterName=[string]`: el nombre del proveedor de sugerencias tal y como se especifica en la colección `suggesters` que forma parte de la definición del índice.</span><span class="sxs-lookup"><span data-stu-id="89b28-1090">`suggesterName=[string]` - the name of the suggester as specified in the `suggesters` collection that's part of the index definition.</span></span> <span data-ttu-id="89b28-1091">Un `suggester` determina qué campos se analizan para encontrar términos de consulta sugeridos.</span><span class="sxs-lookup"><span data-stu-id="89b28-1091">A `suggester` determines which fields are scanned for suggested query terms.</span></span> <span data-ttu-id="89b28-1092">Consulte [Proveedores de sugerencias](#Suggesters) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="89b28-1092">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="89b28-1093">`fuzzy=[boolean]` (opcional, valor predeterminado = false): si se establece en true esta API encontrará sugerencias incluso si hay un carácter sustituido o no encontrado en el texto de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-1093">`fuzzy=[boolean]` (optional, default = false) - when set to true this API will find suggestions even if there's a substituted or missing character in the search text.</span></span> <span data-ttu-id="89b28-1094">Si bien esto proporciona una mejor experiencia en algunos escenarios, ello afecta al rendimiento, ya que las búsquedas de sugerencias aproximadas son más lentas y consumen más recursos.</span><span class="sxs-lookup"><span data-stu-id="89b28-1094">While this provides a better experience in some scenarios it comes at a performance cost as fuzzy suggestion searches are slower and consume more resources.</span></span>

<span data-ttu-id="89b28-1095">`searchFields=[string]` (opcional): lista separada por comas de nombres de campo para buscar el texto de búsqueda especificado.</span><span class="sxs-lookup"><span data-stu-id="89b28-1095">`searchFields=[string]` (optional) - the list of comma-separated field names to search for the specified search text.</span></span> <span data-ttu-id="89b28-1096">Los campos de destino deben estar habilitados para obtener sugerencias.</span><span class="sxs-lookup"><span data-stu-id="89b28-1096">Target fields must be enabled for suggestions.</span></span>

<span data-ttu-id="89b28-1097">`$top=#` (opcional, valor predeterminado = 5): número de sugerencias para recuperar.</span><span class="sxs-lookup"><span data-stu-id="89b28-1097">`$top=#` (optional, default = 5) - the number of suggestions to retrieve.</span></span> <span data-ttu-id="89b28-1098">Debe ser un número entre 1 y 100.</span><span class="sxs-lookup"><span data-stu-id="89b28-1098">Must be a number between 1 and 100.</span></span>

> [!NOTE]
> <span data-ttu-id="89b28-1099">Al llamar a las **sugerencias** mediante POST, este parámetro se denomina `top` en lugar de `$top`.</span><span class="sxs-lookup"><span data-stu-id="89b28-1099">When calling **Suggestions** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="89b28-1100">`$filter=[string]` (opcional): expresión que filtra los documentos que se consideran para obtener sugerencias.</span><span class="sxs-lookup"><span data-stu-id="89b28-1100">`$filter=[string]` (optional) - an expression that filters the documents considered for suggestions.</span></span>

> [!NOTE]
> <span data-ttu-id="89b28-1101">Al llamar a las **sugerencias** mediante POST, este parámetro se denomina `filter` en lugar de `$filter`.</span><span class="sxs-lookup"><span data-stu-id="89b28-1101">When calling **Suggestions** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="89b28-1102">`$orderby=[string]` (opcional): lista de expresiones separadas por comas por la que ordenar los resultados.</span><span class="sxs-lookup"><span data-stu-id="89b28-1102">`$orderby=[string]` (optional) - a list of comma-separated expressions to sort the results by.</span></span> <span data-ttu-id="89b28-1103">Cada expresión puede ser un nombre de campo o una llamada a la función `geo.distance()` .</span><span class="sxs-lookup"><span data-stu-id="89b28-1103">Each expression can be either a field name or a call to the `geo.distance()` function.</span></span> <span data-ttu-id="89b28-1104">Cada expresión puede ir seguida de `asc` para indicar el orden ascendente y de `desc` para indicar el orden descendente.</span><span class="sxs-lookup"><span data-stu-id="89b28-1104">Each expression can be followed by `asc` to indicated ascending, and `desc` to indicate descending.</span></span> <span data-ttu-id="89b28-1105">El valor predeterminado es ascendente.</span><span class="sxs-lookup"><span data-stu-id="89b28-1105">The default is ascending order.</span></span> <span data-ttu-id="89b28-1106">Hay un límite de 32 cláusulas para `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="89b28-1106">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="89b28-1107">Al llamar a las **sugerencias** mediante POST, este parámetro se denomina `orderby` en lugar de `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="89b28-1107">When calling **Suggestions** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="89b28-1108">`$select=[string]` (opcional): lista de campos separados por comas para recuperar.</span><span class="sxs-lookup"><span data-stu-id="89b28-1108">`$select=[string]` (optional) - a list of comma-separated fields to retrieve.</span></span> <span data-ttu-id="89b28-1109">Si no se especifica, solo se devolverá la clave del documento y el texto de la sugerencia.</span><span class="sxs-lookup"><span data-stu-id="89b28-1109">If unspecified, only the document key and suggestion text is returned.</span></span> <span data-ttu-id="89b28-1110">Se pueden solicitar explícitamente todos los campos estableciendo este parámetro en `*`.</span><span class="sxs-lookup"><span data-stu-id="89b28-1110">You can explicitly request all fields by setting this parameter to `*`.</span></span>

> [!NOTE]
> <span data-ttu-id="89b28-1111">Al llamar a las **sugerencias** mediante POST, este parámetro se denomina `select` en lugar de `$select`.</span><span class="sxs-lookup"><span data-stu-id="89b28-1111">When calling **Suggestions** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="89b28-1112">`minimumCoverage` (opcional, el valor predeterminado es 80): un número entre 0 y 100 que indica el porcentaje del índice que debe estar cubierto por una consulta de búsqueda para que la consulta se realice correctamente.</span><span class="sxs-lookup"><span data-stu-id="89b28-1112">`minimumCoverage` (optional, defaults to 80) - a number between 0 and 100 indicating the percentage of the index that must be covered by a suggestions query in order for the query to be reported as a success.</span></span> <span data-ttu-id="89b28-1113">De forma predeterminada, al menos el 80% del índice debe estar disponible o `Suggest` devolverá el código de estado HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="89b28-1113">By default, at least 80% of the index must be available or `Suggest` will return HTTP status code 503.</span></span> <span data-ttu-id="89b28-1114">Si establece `minimumCoverage` y `Suggest` se realiza correctamente, devolverá HTTP 200 e incluye un valor `@search.coverage` en la respuesta que indica el porcentaje del índice que se incluyó en la consulta.</span><span class="sxs-lookup"><span data-stu-id="89b28-1114">If you set `minimumCoverage` and `Suggest` succeeds, it will return HTTP 200 and include a `@search.coverage` value in the response indicating the percentage of the index that was included in the query.</span></span>

> [!NOTE]
> <span data-ttu-id="89b28-1115">Establecer este parámetro en un valor inferior a 100 puede ser útil para garantizar la disponibilidad de la búsqueda incluso para servicios con una única réplica.</span><span class="sxs-lookup"><span data-stu-id="89b28-1115">Setting this parameter to a value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="89b28-1116">Sin embargo, no se garantiza que todos los documentos coincidentes existan en los resultados.</span><span class="sxs-lookup"><span data-stu-id="89b28-1116">However, not all matching suggestions are guaranteed to be present in the results.</span></span> <span data-ttu-id="89b28-1117">Si la recuperación es más importante para la aplicación que la disponibilidad, es mejor dejar `minimumCoverage` por debajo de su valor predeterminado de 80.</span><span class="sxs-lookup"><span data-stu-id="89b28-1117">If recall is more important to your application than availability, then it's best not to lower `minimumCoverage` below its default value of 80.</span></span>
> 
> 

<span data-ttu-id="89b28-1118">`api-version=[string]` (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="89b28-1118">`api-version=[string]` (required).</span></span> <span data-ttu-id="89b28-1119">La versión de vista previa es `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="89b28-1119">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="89b28-1120">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.</span><span class="sxs-lookup"><span data-stu-id="89b28-1120">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="89b28-1121">Nota: Para esta operación, `api-version` se especifica como un parámetro de consulta en la dirección URL sin tener en cuenta si se llama a las **Sugerencias** con GET o POST.</span><span class="sxs-lookup"><span data-stu-id="89b28-1121">Note: For this operation, the `api-version` is specified as a query parameter in the URL regardless of whether you call **Suggestions** with GET or POST.</span></span>

<span data-ttu-id="89b28-1122">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-1122">**Request Headers**</span></span>

<span data-ttu-id="89b28-1123">En la lista siguiente se describen los encabezados de solicitud obligatorios y opcionales.</span><span class="sxs-lookup"><span data-stu-id="89b28-1123">The following list describes the required and optional request headers</span></span>

* <span data-ttu-id="89b28-1124">`api-key`: `api-key` se usa para autenticar la solicitud en su servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89b28-1124">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="89b28-1125">Es un valor de cadena, único en su URL de servicio.</span><span class="sxs-lookup"><span data-stu-id="89b28-1125">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="89b28-1126">La solicitud **Sugerencias** puede especificar una clave de administración o una clave de consulta como `api-key`.</span><span class="sxs-lookup"><span data-stu-id="89b28-1126">The **Suggestions** request can specify either an admin key or query key as the `api-key`.</span></span>

<span data-ttu-id="89b28-1127">También necesitará el nombre del servicio para construir la dirección URL de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="89b28-1127">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="89b28-1128">Puede obtener el nombre de servicio y `api-key` desde el panel de servicio en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="89b28-1128">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="89b28-1129">Consulte [Crear un servicio de Búsqueda de Azure en el portal](search-create-service-portal.md) para obtener ayuda sobre la navegación en páginas.</span><span class="sxs-lookup"><span data-stu-id="89b28-1129">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="89b28-1130">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="89b28-1130">**Request Body**</span></span>

<span data-ttu-id="89b28-1131">Para GET: ninguno.</span><span class="sxs-lookup"><span data-stu-id="89b28-1131">For GET: None.</span></span>

<span data-ttu-id="89b28-1132">Para POST:</span><span class="sxs-lookup"><span data-stu-id="89b28-1132">For POST:</span></span>

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered to declare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

<span data-ttu-id="89b28-1133">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="89b28-1133">**Response**</span></span>

<span data-ttu-id="89b28-1134">Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.</span><span class="sxs-lookup"><span data-stu-id="89b28-1134">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in the query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

<span data-ttu-id="89b28-1135">Si se utiliza la opción de proyección para recuperar campos que están incluidos en cada elemento de la matriz:</span><span class="sxs-lookup"><span data-stu-id="89b28-1135">If the projection option is used to retrieve fields they are included in each element of the array:</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in the query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

<span data-ttu-id="89b28-1136">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="89b28-1136">**Example**</span></span>

<span data-ttu-id="89b28-1137">Recupere 5 sugerencias en las que la entrada de búsqueda parcial sea "lux"</span><span class="sxs-lookup"><span data-stu-id="89b28-1137">Retrieve 5 suggestions where the partial search input is 'lux'</span></span>

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
