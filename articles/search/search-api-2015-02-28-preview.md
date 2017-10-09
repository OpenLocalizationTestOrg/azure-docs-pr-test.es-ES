---
title: "aaaAzure búsqueda servicio REST API versión 2015-02-28-vista previa | Documentos de Microsoft"
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
ms.openlocfilehash: 63cb30b7f43a42552c6744ea087afea947857224
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a><span data-ttu-id="9e15b-103">API de REST del Servicio Búsqueda de Azure versión 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9e15b-103">Azure Search Service REST API: Version 2015-02-28-Preview</span></span>
<span data-ttu-id="9e15b-104">Este artículo es la documentación de referencia de Hola para `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-104">This article is hello reference documentation for `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9e15b-105">Esta vista previa extiende versión disponible con carácter general actual hello, [api-version = 2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), proporcionando Hola siguiendo las características experimentales:</span><span class="sxs-lookup"><span data-stu-id="9e15b-105">This preview extends hello current generally available version, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), by providing hello following experimental features:</span></span>

* <span data-ttu-id="9e15b-106">`moreLikeThis`parámetro Hola consulta [buscar documentos](#SearchDocs) API.</span><span class="sxs-lookup"><span data-stu-id="9e15b-106">`moreLikeThis` query parameter in hello [Search Documents](#SearchDocs) API.</span></span> <span data-ttu-id="9e15b-107">Busca otros documentos que son relevantes tooanother documento específico.</span><span class="sxs-lookup"><span data-stu-id="9e15b-107">It finds other documents that are relevant tooanother specific document.</span></span>

<span data-ttu-id="9e15b-108">Algunas partes adicionales de hello `2015-02-28-Preview` API de REST se documentan por separado.</span><span class="sxs-lookup"><span data-stu-id="9e15b-108">A few additional parts of hello `2015-02-28-Preview` REST API are documented separately.</span></span> <span data-ttu-id="9e15b-109">Entre ellos se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="9e15b-109">These include:</span></span>

* [<span data-ttu-id="9e15b-110">Perfiles de puntuación</span><span class="sxs-lookup"><span data-stu-id="9e15b-110">Scoring Profiles</span></span>](search-api-scoring-profiles-2015-02-28-preview.md)
* [<span data-ttu-id="9e15b-111">Indexadores</span><span class="sxs-lookup"><span data-stu-id="9e15b-111">Indexers</span></span>](search-api-indexers-2015-02-28-preview.md)

<span data-ttu-id="9e15b-112">El servicio de Búsqueda de Azure está disponible en varias versiones.</span><span class="sxs-lookup"><span data-stu-id="9e15b-112">Azure Search service is available in multiple versions.</span></span> <span data-ttu-id="9e15b-113">Consulte demasiado[versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="9e15b-113">Please refer too[Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details.</span></span>

## <a name="apis-in-this-document"></a><span data-ttu-id="9e15b-114">API incluidas en este documento</span><span class="sxs-lookup"><span data-stu-id="9e15b-114">APIs in this document</span></span>
<span data-ttu-id="9e15b-115">La API del servicio Búsqueda de Azure admite dos sintaxis de URL para operaciones de API: simple y OData (consulte [Compatibilidad con OData (API de Búsqueda de Azure)](http://msdn.microsoft.com/library/azure/dn798932.aspx) para obtener más información).</span><span class="sxs-lookup"><span data-stu-id="9e15b-115">Azure Search service API supports two URL syntaxes for API operations: simple and OData (see [Support for OData (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) for details).</span></span> <span data-ttu-id="9e15b-116">Hello lista siguiente muestra una sintaxis sencilla Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-116">hello following list shows hello simple syntax.</span></span>

[<span data-ttu-id="9e15b-117">Crear índice</span><span class="sxs-lookup"><span data-stu-id="9e15b-117">Create Index</span></span>](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="9e15b-118">Actualizar índice</span><span class="sxs-lookup"><span data-stu-id="9e15b-118">Update Index</span></span>](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="9e15b-119">Obtener índice</span><span class="sxs-lookup"><span data-stu-id="9e15b-119">Get Index</span></span>](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="9e15b-120">Enumerar índices</span><span class="sxs-lookup"><span data-stu-id="9e15b-120">Listing Indexes</span></span>](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="9e15b-121">Obtención de estadísticas de índice</span><span class="sxs-lookup"><span data-stu-id="9e15b-121">Get Index Statistics</span></span>](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[<span data-ttu-id="9e15b-122">Analizador de prueba</span><span class="sxs-lookup"><span data-stu-id="9e15b-122">Test Analyzer</span></span>](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[<span data-ttu-id="9e15b-123">Eliminar un índice</span><span class="sxs-lookup"><span data-stu-id="9e15b-123">Delete an Index</span></span>](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="9e15b-124">Agregar, eliminar y actualizar datos en un índice</span><span class="sxs-lookup"><span data-stu-id="9e15b-124">Add, Delete, and Update Data within an Index</span></span>](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[<span data-ttu-id="9e15b-125">Buscar en documentos</span><span class="sxs-lookup"><span data-stu-id="9e15b-125">Search Documents</span></span>](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[<span data-ttu-id="9e15b-126">Buscar documento</span><span class="sxs-lookup"><span data-stu-id="9e15b-126">Lookup Document</span></span>](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[<span data-ttu-id="9e15b-127">Documentos de recuento</span><span class="sxs-lookup"><span data-stu-id="9e15b-127">Count Documents</span></span>](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[<span data-ttu-id="9e15b-128">Sugerencias</span><span class="sxs-lookup"><span data-stu-id="9e15b-128">Suggestions</span></span>](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a><span data-ttu-id="9e15b-129">Operaciones de índice</span><span class="sxs-lookup"><span data-stu-id="9e15b-129">Index Operations</span></span>
<span data-ttu-id="9e15b-130">Puede crear y administrar índices en el servicio de Búsqueda de Azure a través de solicitudes HTTP sencillas (POST, GET, PUT, DELETE) en un recurso de índice determinado.</span><span class="sxs-lookup"><span data-stu-id="9e15b-130">You can create and manage indexes in Azure Search service via simple HTTP requests (POST, GET, PUT, DELETE) against a given index resource.</span></span> <span data-ttu-id="9e15b-131">toocreate un índice, REGISTRE primero un documento JSON que describe el esquema de índice Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-131">toocreate an index, you first POST a JSON document that describes hello index schema.</span></span> <span data-ttu-id="9e15b-132">esquema de Hello define los campos de Hola de índice de hello, sus tipos de datos y cómo se puede usar (por ejemplo, en las búsquedas de texto completo, filtros, ordenación o facetas).</span><span class="sxs-lookup"><span data-stu-id="9e15b-132">hello schema defines hello fields of hello index, their data types, and how they can be used (for example, in full-text searches, filters, sorting, or faceting).</span></span> <span data-ttu-id="9e15b-133">También define los perfiles de puntuación, proveedores de sugerencias y otros comportamientos de hello tooconfigure de atributos de índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-133">It also defines scoring profiles, suggesters and other attributes tooconfigure hello behavior of hello index.</span></span>

<span data-ttu-id="9e15b-134">Hello en el ejemplo siguiente se proporciona una ilustración de un esquema utilizado para buscar información sobre hoteles con campo de descripción de hello definido en dos idiomas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-134">hello following example provides an illustration of a schema used for searching on hotel information with hello Description field defined in two languages.</span></span> <span data-ttu-id="9e15b-135">Observe cómo los atributos controlan cómo se utiliza el campo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-135">Notice how attributes control how hello field is used.</span></span> <span data-ttu-id="9e15b-136">Por ejemplo Hola `hotelId` se utiliza como clave de documento de hello (`"key": true`) y se excluye de búsquedas de texto completo (`"searchable": false`).</span><span class="sxs-lookup"><span data-stu-id="9e15b-136">For example hello `hotelId` is used as hello document key (`"key": true`) and is excluded from full-text searches (`"searchable": false`).</span></span>

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

<span data-ttu-id="9e15b-137">Después de crea el índice de hello, podrá cargar documentos que rellenan índice Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-137">After hello index is created, you'll upload documents that populate hello index.</span></span> <span data-ttu-id="9e15b-138">Consulte [Agregar o actualizar documentos](#AddOrUpdateDocuments) para este siguiente paso.</span><span class="sxs-lookup"><span data-stu-id="9e15b-138">See [Add or Update Documents](#AddOrUpdateDocuments) for this next step.</span></span>

<span data-ttu-id="9e15b-139">Para tooindexing de vídeo de introducción en búsqueda de Azure, vea hello [episodio de Cloud Cover de Channel 9 sobre búsqueda de Azure](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span><span class="sxs-lookup"><span data-stu-id="9e15b-139">For a video introduction tooindexing in Azure Search, see hello [Channel 9 Cloud Cover episode on Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span></span>

<a name="CreateIndex"></a>

## <a name="create-index"></a><span data-ttu-id="9e15b-140">Crear índice</span><span class="sxs-lookup"><span data-stu-id="9e15b-140">Create Index</span></span>
<span data-ttu-id="9e15b-141">Un índice es el medio principal de Hola de organizar y buscar documentos en búsqueda de Azure, toohow similar una tabla organiza los registros en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="9e15b-141">An index is hello primary means of organizing and searching documents in Azure Search, similar toohow a table organizes records in a database.</span></span> <span data-ttu-id="9e15b-142">Cada índice tiene una colección de documentos que conformes toohello esquema de índice (nombres de campo, tipos de datos y propiedades), pero los índices también especifican construcciones adicionales (proveedores de sugerencias, perfiles de puntuación y opciones de CORS) que definen otros comportamientos de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-142">Each index has a collection of documents that all conform toohello index schema (field names, data types, and properties), but indexes also specify additional constructs (suggesters, scoring profiles, and CORS options) that define other search behaviors.</span></span>

<span data-ttu-id="9e15b-143">Puede crear un índice nuevo dentro de un servicio de Búsqueda de Azure mediante una solicitud HTTP POST o PUT.</span><span class="sxs-lookup"><span data-stu-id="9e15b-143">You can create a new index within an Azure Search service using an HTTP POST or PUT request.</span></span> <span data-ttu-id="9e15b-144">cuerpo de saludo de solicitud de hello es un esquema JSON que especifica la información de índice y la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-144">hello body of hello request is a JSON schema that specifies hello index and configuration information.</span></span>

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="9e15b-145">Como alternativa, puede usar PUT y especificar el nombre del índice de hello en hello URI.</span><span class="sxs-lookup"><span data-stu-id="9e15b-145">Alternatively, you can use PUT and specify hello index name on hello URI.</span></span> <span data-ttu-id="9e15b-146">Si el índice de hello no existe, se creará.</span><span class="sxs-lookup"><span data-stu-id="9e15b-146">If hello index does not exist, it will be created.</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

<span data-ttu-id="9e15b-147">Crear un índice determina la estructura de Hola de hello documentos almacenados y utilizados en operaciones de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-147">Creating an index determines hello structure of hello documents stored and used in search operations.</span></span> <span data-ttu-id="9e15b-148">Rellenar índice hello es una operación independiente.</span><span class="sxs-lookup"><span data-stu-id="9e15b-148">Populating hello index is a separate operation.</span></span> <span data-ttu-id="9e15b-149">En este paso, puede usar un [indexador](https://msdn.microsoft.com/library/azure/mt183328.aspx) (disponible para orígenes de datos admitidos) o una operación [Agregar, actualizar o eliminar documentos](https://msdn.microsoft.com/library/azure/dn798930.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e15b-149">For this step, you can use an [indexer](https://msdn.microsoft.com/library/azure/mt183328.aspx) (available for supported data sources) or an [Add, Update, or Delete Documents](https://msdn.microsoft.com/library/azure/dn798930.aspx) operation.</span></span> <span data-ttu-id="9e15b-150">índice Hola invertido se genera cuando se publican los documentos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-150">hello inverted index is generated when hello documents are posted.</span></span>

<span data-ttu-id="9e15b-151">**Tenga en cuenta**: Hola número máximo de índices permitidos varía según el nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="9e15b-151">**Note**: hello maximum number of indexes allowed varies by pricing tier.</span></span> <span data-ttu-id="9e15b-152">servicio gratuito de Hello permite que los índices de too3.</span><span class="sxs-lookup"><span data-stu-id="9e15b-152">hello free service allows up too3 indexes.</span></span> <span data-ttu-id="9e15b-153">El servicio estándar permite 50 índices por servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-153">Standard service allows 50 indexes per Search service.</span></span> <span data-ttu-id="9e15b-154">Consulte [Límites y restricciones](http://msdn.microsoft.com/library/azure/dn798934.aspx) para obtener detalles.</span><span class="sxs-lookup"><span data-stu-id="9e15b-154">See [Limits and constraints](http://msdn.microsoft.com/library/azure/dn798934.aspx) for details.</span></span>

<span data-ttu-id="9e15b-155">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-155">**Request**</span></span>

<span data-ttu-id="9e15b-156">HTTPS es necesario para todas las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-156">HTTPS is required for all service requests.</span></span> <span data-ttu-id="9e15b-157">Hola **Create Index** solicitud puede crearse mediante un método POST o PUT.</span><span class="sxs-lookup"><span data-stu-id="9e15b-157">hello **Create Index** request can be constructed using either a POST or PUT method.</span></span> <span data-ttu-id="9e15b-158">Al usar POST, debe proporcionar un nombre de índice en el cuerpo de la solicitud junto con la definición de esquema de índice de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-158">When using POST, you must provide an index name in hello request body along with hello index schema definition.</span></span> <span data-ttu-id="9e15b-159">Con PUT, el nombre del índice de hello es parte de la dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-159">With PUT, hello index name is part of hello URL.</span></span> <span data-ttu-id="9e15b-160">Si el índice de hello no existe, se crea.</span><span class="sxs-lookup"><span data-stu-id="9e15b-160">If hello index doesn't exist, it is created.</span></span> <span data-ttu-id="9e15b-161">Si ya existe, está actualizada toohello nueva definición.</span><span class="sxs-lookup"><span data-stu-id="9e15b-161">If it already exists, it is updated toohello new definition.</span></span>

<span data-ttu-id="9e15b-162">nombre del índice Hola debe estar en minúsculas, empezar por una letra o un número, no tener barras o puntos y tener menos de 128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9e15b-162">hello index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="9e15b-163">Después de iniciar el nombre del índice de hello con una letra o un número, rest Hola de nombre de hello puede incluir cualquier letra, número y guiones, como Hola guiones no sean consecutivos.</span><span class="sxs-lookup"><span data-stu-id="9e15b-163">After starting hello index name with a letter or number, hello rest of hello name can include any letter, number and dashes, as long as hello dashes are not consecutive.</span></span>

<span data-ttu-id="9e15b-164">Hola `api-version` es necesario.</span><span class="sxs-lookup"><span data-stu-id="9e15b-164">hello `api-version` is required.</span></span> <span data-ttu-id="9e15b-165">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener una lista de las versiones disponibles.</span><span class="sxs-lookup"><span data-stu-id="9e15b-165">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for a list of available versions.</span></span>

<span data-ttu-id="9e15b-166">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-166">**Request Headers**</span></span>

<span data-ttu-id="9e15b-167">Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales.</span><span class="sxs-lookup"><span data-stu-id="9e15b-167">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="9e15b-168">`Content-Type`: obligatorio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-168">`Content-Type`: Required.</span></span> <span data-ttu-id="9e15b-169">Establezca esta propiedad demasiado`application/json`</span><span class="sxs-lookup"><span data-stu-id="9e15b-169">Set this too`application/json`</span></span>
* <span data-ttu-id="9e15b-170">`api-key`: obligatorio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-170">`api-key`: Required.</span></span> <span data-ttu-id="9e15b-171">Hola `api-key` se usa para</span><span class="sxs-lookup"><span data-stu-id="9e15b-171">hello `api-key` is used to</span></span>
* <span data-ttu-id="9e15b-172">autenticar el servicio de búsqueda de hello solicitud tooyour.</span><span class="sxs-lookup"><span data-stu-id="9e15b-172">authenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9e15b-173">Es un valor de cadena, el servicio de tooyour único.</span><span class="sxs-lookup"><span data-stu-id="9e15b-173">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="9e15b-174">Hola **Create Index** solicitud debe incluir un `api-key` encabezado establece clave de administrador de tooyour (como clave de consulta tooa lugar).</span><span class="sxs-lookup"><span data-stu-id="9e15b-174">hello **Create Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="9e15b-175">También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-175">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9e15b-176">Se puede obtener el nombre de servicio hello y `api-key` desde el panel de servicio en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e15b-176">You can get both hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9e15b-177">Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.</span><span class="sxs-lookup"><span data-stu-id="9e15b-177">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9e15b-178"><a name="RequestData"></a>
**Sintaxis del cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-178"><a name="RequestData"></a>
**Request Body Syntax**</span></span>

<span data-ttu-id="9e15b-179">Hola el cuerpo de solicitud de hello contiene una definición de esquema, que incluye Hola lista de campos de datos dentro de los documentos que se introducirán en este índice, tipos de datos, atributos, así como una lista opcional de los perfiles de puntuación es utilizado tooscore coincidencia de documentos en tiempo de consulta.</span><span class="sxs-lookup"><span data-stu-id="9e15b-179">hello body of hello request contains a schema definition, which includes hello list of data fields within documents that will be fed into this index, data types, attributes, as well as an optional list of scoring profiles that are used tooscore matching documents at query time.</span></span>

<span data-ttu-id="9e15b-180">Tenga en cuenta que para una solicitud POST, debe especificar el nombre del índice de Hola Hola del cuerpo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="9e15b-180">Note that for a POST request, you must specify hello index name in hello request body.</span></span>

<span data-ttu-id="9e15b-181">Solo puede haber un campo de clave de índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-181">There can only be one key field in hello index.</span></span> <span data-ttu-id="9e15b-182">Tiene un campo de cadena toobe.</span><span class="sxs-lookup"><span data-stu-id="9e15b-182">It has toobe a string field.</span></span> <span data-ttu-id="9e15b-183">Este campo representa el identificador único de Hola para cada documento almacenado en el índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-183">This field represents hello unique identifier for each document stored within hello index.</span></span>

<span data-ttu-id="9e15b-184">partes principales de Hola de un índice Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="9e15b-184">hello main parts of an index include hello following:</span></span>

* `name`
* <span data-ttu-id="9e15b-185">`fields` que se introducirán en este índice, incluido el nombre, tipo de datos y propiedades que definen las acciones permitidas en ese campo.</span><span class="sxs-lookup"><span data-stu-id="9e15b-185">`fields` that will be fed into this index, including name, data type, and properties that define allowable actions on that field.</span></span>
* <span data-ttu-id="9e15b-186">`suggesters` se usa para autocompletar o anticipar la escritura de las consultas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-186">`suggesters` used for auto-complete or type-ahead queries.</span></span>
* <span data-ttu-id="9e15b-187">`scoringProfiles` se usa para la clasificación de la puntuación de la búsqueda personalizada.</span><span class="sxs-lookup"><span data-stu-id="9e15b-187">`scoringProfiles` used for custom search score ranking.</span></span> <span data-ttu-id="9e15b-188">Consulte [Agregar perfiles de puntuación](https://msdn.microsoft.com/library/azure/dn798928.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="9e15b-188">See [Add scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for details.</span></span>
* <span data-ttu-id="9e15b-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` utiliza toodefine cómo las documentos y consultas se dividen en tokens indizable/permite realizar búsquedas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` used toodefine how your documents/queries are broken into indexable/searchable tokens.</span></span> <span data-ttu-id="9e15b-190">Consulte [Análisis en Búsqueda de Azure](https://aka.ms//azsanalysis) para más detalles.</span><span class="sxs-lookup"><span data-stu-id="9e15b-190">See [Analysis in Azure Search](https://aka.ms//azsanalysis) for details.</span></span>
* <span data-ttu-id="9e15b-191">`defaultScoringProfile`Usar valor predeterminado de hello toooverwrite comportamientos de puntuación.</span><span class="sxs-lookup"><span data-stu-id="9e15b-191">`defaultScoringProfile` used toooverwrite hello default scoring behaviors.</span></span>
* <span data-ttu-id="9e15b-192">`corsOptions`consultas entre orígenes de tooallow sobre el índice.</span><span class="sxs-lookup"><span data-stu-id="9e15b-192">`corsOptions` tooallow cross-origin queries against your index.</span></span>

<span data-ttu-id="9e15b-193">sintaxis de Hola para estructurar la carga de la solicitud de hello es como sigue.</span><span class="sxs-lookup"><span data-stu-id="9e15b-193">hello syntax for structuring hello request payload is as follows.</span></span> <span data-ttu-id="9e15b-194">En este tema se proporciona una solicitud de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9e15b-194">A sample request is provided further on in this topic.</span></span>

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
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
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
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
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

<span data-ttu-id="9e15b-195">**Atributos de índice**</span><span class="sxs-lookup"><span data-stu-id="9e15b-195">**Index Attributes**</span></span>

<span data-ttu-id="9e15b-196">Hello atributos siguientes pueden establecerse al crear un índice.</span><span class="sxs-lookup"><span data-stu-id="9e15b-196">hello following attributes can be set when creating an index.</span></span> <span data-ttu-id="9e15b-197">Para obtener más información sobre la puntuación y los perfiles de puntuación, consulte [Agregar perfiles de puntuación](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e15b-197">For details about scoring and scoring profiles, see [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span>

<span data-ttu-id="9e15b-198">`name`-Conjuntos Hola nombre del campo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-198">`name` - Sets hello name of hello field.</span></span>

<span data-ttu-id="9e15b-199">`type`-Conjuntos Hola tipo de datos de campo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-199">`type` - Sets hello data type for hello field.</span></span>

<span data-ttu-id="9e15b-200">`searchable`-Marca Hola campo como texto completo capacitado para búsquedas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-200">`searchable` - Marks hello field as full-text search-able.</span></span> <span data-ttu-id="9e15b-201">Esto significa que se someterá a análisis como la separación de palabras durante la indexación.</span><span class="sxs-lookup"><span data-stu-id="9e15b-201">This means it will undergo analysis such as word-breaking during indexing.</span></span> <span data-ttu-id="9e15b-202">Si establece un `searchable` valor del campo tooa como "sunny day", internamente será dividir en tokens individuales Hola "sunny" y "día".</span><span class="sxs-lookup"><span data-stu-id="9e15b-202">If you set a `searchable` field tooa value like "sunny day", internally it will be split into hello individual tokens "sunny" and "day".</span></span> <span data-ttu-id="9e15b-203">Esto permite realizar búsquedas de texto completo de estos términos.</span><span class="sxs-lookup"><span data-stu-id="9e15b-203">This enables full-text searches for these terms.</span></span> <span data-ttu-id="9e15b-204">Los campos de tipo `Edm.String` o `Collection(Edm.String)` son `searchable` de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9e15b-204">Fields of type `Edm.String` or `Collection(Edm.String)` are `searchable` by default.</span></span> <span data-ttu-id="9e15b-205">Los campos de otros tipos no pueden ser `searchable`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-205">Fields of other types cannot be `searchable`.</span></span>

* <span data-ttu-id="9e15b-206">**Tenga en cuenta**: `searchable` campos consumen espacio adicional en el índice, ya que la búsqueda de Azure almacenará una versión con tokens adicional del valor de campo de Hola para búsquedas de texto completo.</span><span class="sxs-lookup"><span data-stu-id="9e15b-206">**Note**: `searchable` fields consume extra space in your index since Azure Search will store an additional tokenized version of hello field value for full-text searches.</span></span> <span data-ttu-id="9e15b-207">Si desea toosave espacio en el índice y no es necesario un toobe de campo que se incluyen en las búsquedas, establezca `searchable` demasiado`false`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-207">If you want toosave space in your index and you don't need a field toobe included in searches, set `searchable` too`false`.</span></span>

<span data-ttu-id="9e15b-208">`filterable`: Permite hello toobe de campo al que hace referencia en `$filter` las consultas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-208">`filterable` - Allows hello field toobe referenced in `$filter` queries.</span></span> <span data-ttu-id="9e15b-209">`filterable` difiere de `searchable` en el modo en que se gestionan las cadenas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-209">`filterable` differs from `searchable` in how strings are handled.</span></span> <span data-ttu-id="9e15b-210">Los campos de tipo `Edm.String` o `Collection(Edm.String)` que son `filterable` no sufren separación de palabras, por lo que las comparaciones son solo para las coincidencias exactas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-210">Fields of type `Edm.String` or `Collection(Edm.String)` that are `filterable` do not undergo word-breaking, so comparisons are for exact matches only.</span></span> <span data-ttu-id="9e15b-211">Por ejemplo, si establece este tipo de campo `f` demasiado "sunny day", `$filter=f eq 'sunny'` encontrará ninguna coincidencia, pero `$filter=f eq 'sunny day'` le.</span><span class="sxs-lookup"><span data-stu-id="9e15b-211">For example, if you set such a field `f` too"sunny day", `$filter=f eq 'sunny'` will find no matches, but `$filter=f eq 'sunny day'` will.</span></span> <span data-ttu-id="9e15b-212">Todos los campos son `filterable` de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9e15b-212">All fields are `filterable` by default.</span></span>

<span data-ttu-id="9e15b-213">`sortable`-Predeterminada Hola sistema ordena los resultados por puntuación, pero en muchas ocasiones los usuarios desearán toosort por campos de documentos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-213">`sortable` - By default hello system sorts results by score, but in many experiences users will want toosort by fields in hello documents.</span></span> <span data-ttu-id="9e15b-214">Los campos de tipo `Collection(Edm.String)` no pueden ser `sortable`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-214">Fields of type `Collection(Edm.String)` cannot be `sortable`.</span></span> <span data-ttu-id="9e15b-215">El resto de campos son `sortable` de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9e15b-215">All other fields are `sortable` by default.</span></span>

<span data-ttu-id="9e15b-216">`facetable`: suele utilizarse en una presentación de resultados de búsqueda que incluya el número de resultados por categoría (por ejemplo, busque cámaras digitales y consulte los resultados divididos por marca, por megapíxeles, por precio, etc.).</span><span class="sxs-lookup"><span data-stu-id="9e15b-216">`facetable`- Typically used in a presentation of search results that includes hit count by category (for example, search for digital cameras and see hits by brand, by megapixels, by price, etc.).</span></span> <span data-ttu-id="9e15b-217">Esta opción no puede utilizarse con campos de tipo `Edm.GeographyPoint`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-217">This option cannot be used with fields of type `Edm.GeographyPoint`.</span></span> <span data-ttu-id="9e15b-218">El resto de campos son `facetable` de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9e15b-218">All other fields are `facetable` by default.</span></span>

* <span data-ttu-id="9e15b-219">**Nota**: los campos de tipo `Edm.String` que son `filterable`, `sortable` o `facetable` solo pueden ocupar una longitud de 32 KB como máximo.</span><span class="sxs-lookup"><span data-stu-id="9e15b-219">**Note**: Fields of type `Edm.String` that are `filterable`, `sortable`, or `facetable` can be at most 32KB in length.</span></span> <span data-ttu-id="9e15b-220">Esto es porque esos campos se tratan como un término de búsqueda sencillo, y la longitud máxima de Hola de un término de búsqueda de Azure es 32KB.</span><span class="sxs-lookup"><span data-stu-id="9e15b-220">This is because such fields are treated as a single search term, and hello maximum length of a term in Azure Search is 32KB.</span></span> <span data-ttu-id="9e15b-221">Si necesita toostore texto más que la especificada en un campo de cadena único, deberá tooexplicitly establecer `filterable`, `sortable`, y `facetable` demasiado`false` en la definición del índice.</span><span class="sxs-lookup"><span data-stu-id="9e15b-221">If you need toostore more text than this in a single string field, you will need tooexplicitly set `filterable`, `sortable`, and `facetable` too`false` in your index definition.</span></span>
* <span data-ttu-id="9e15b-222">**Tenga en cuenta**: si un campo no tiene ninguno de hello anterior atributos se establecen demasiado`true` (`searchable`, `filterable`, `sortable`, o`facetable`) campo Hola se excluye eficazmente del índice de hello invertido.</span><span class="sxs-lookup"><span data-stu-id="9e15b-222">**Note**: If a field has none of hello above attributes set too`true` (`searchable`, `filterable`, `sortable`,  or`facetable`) hello field is effectively excluded from hello inverted index.</span></span> <span data-ttu-id="9e15b-223">Esta opción es útil para los campos que no se utilizan en las consultas, pero que son necesarios en los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-223">This option is useful for fields that are not used in queries, but are needed in search results.</span></span> <span data-ttu-id="9e15b-224">Exclusión de esos campos del índice de hello mejora el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="9e15b-224">Excluding such fields from hello index improves performance.</span></span>

<span data-ttu-id="9e15b-225">`key`-Marcas Hola campo como que contiene identificadores únicos para los documentos en el índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-225">`key` - Marks hello field as containing unique identifiers for documents within hello index.</span></span> <span data-ttu-id="9e15b-226">Se debe elegir exactamente un campo como hello `key` campo y debe ser de tipo `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-226">Exactly one field must be chosen as hello `key` field and it must be of type `Edm.String`.</span></span> <span data-ttu-id="9e15b-227">Campos clave pueden ser utilizado toolook documentos directamente a través de hello [API de búsqueda](#LookupAPI).</span><span class="sxs-lookup"><span data-stu-id="9e15b-227">Key fields can be used toolook up documents directly via hello [Lookup API](#LookupAPI).</span></span>

<span data-ttu-id="9e15b-228">`retrievable`-Establece si el campo de Hola se puede devolver resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-228">`retrievable` - Sets whether hello field can be returned in a search result.</span></span>  <span data-ttu-id="9e15b-229">Esto es útil cuando se desea toouse un campo (por ejemplo, margen) como un filtro, ordenación o puntuación mecanismo pero no desea que el usuario final toohello visible de hello campo toobe.</span><span class="sxs-lookup"><span data-stu-id="9e15b-229">This is useful when you want toouse a field (for example, margin) as a filter, sorting, or scoring mechanism but do not want hello field toobe visible toohello end user.</span></span> <span data-ttu-id="9e15b-230">Este atributo debe ser `true` for `key` .</span><span class="sxs-lookup"><span data-stu-id="9e15b-230">This attribute must be `true` for `key` fields.</span></span>

<span data-ttu-id="9e15b-231">`analyzer`-Conjuntos Hola nombre de hello analizador toouse campo hello en tiempo de búsqueda y el momento de la indización.</span><span class="sxs-lookup"><span data-stu-id="9e15b-231">`analyzer` - Sets hello name of hello analyzer toouse for hello field at search time and indexing time.</span></span> <span data-ttu-id="9e15b-232">Encontrará Hola conjunto de valores permitido [analizadores](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e15b-232">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="9e15b-233">Esta opción puede utilizarse solo con campos `searchable` y no se puede establecer junto con `searchAnalyzer` o `indexAnalyzer`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-233">This option can be used only with `searchable` fields and it can't be set together with either `searchAnalyzer` or `indexAnalyzer`.</span></span>  <span data-ttu-id="9e15b-234">Una vez que se elige el analizador de hello, no se puede cambiar para el campo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-234">Once hello analyzer is chosen, it cannot be changed for hello field.</span></span>

<span data-ttu-id="9e15b-235">`searchAnalyzer`-Conjuntos Hola nombre del analizador de Hola que se usa en tiempo de búsqueda para el campo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-235">`searchAnalyzer` - Sets hello name of hello analyzer used at search time for hello field.</span></span> <span data-ttu-id="9e15b-236">Encontrará Hola conjunto de valores permitido [analizadores](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e15b-236">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="9e15b-237">Esta opción solo puede utilizarse con campos `searchable` .</span><span class="sxs-lookup"><span data-stu-id="9e15b-237">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="9e15b-238">Debe establecerse junto con `indexAnalyzer` y no se puede establecer junto con hello `analyzer` opción.</span><span class="sxs-lookup"><span data-stu-id="9e15b-238">It must be set together with `indexAnalyzer` and it cannot be set together with hello `analyzer` option.</span></span> <span data-ttu-id="9e15b-239">Este analizador se puede actualizar en un campo existente.</span><span class="sxs-lookup"><span data-stu-id="9e15b-239">This analyzer can be updated on an existing field.</span></span>

<span data-ttu-id="9e15b-240">`indexAnalyzer`-Conjuntos Hola nombre del analizador de hello usada en tiempo de indización para el campo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-240">`indexAnalyzer` - Sets hello name of hello analyzer used at indexing time for hello field.</span></span> <span data-ttu-id="9e15b-241">Encontrará Hola conjunto de valores permitido [analizadores](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e15b-241">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="9e15b-242">Esta opción solo puede utilizarse con campos `searchable` .</span><span class="sxs-lookup"><span data-stu-id="9e15b-242">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="9e15b-243">Debe establecerse junto con `searchAnalyzer` y no se puede establecer junto con hello `analyzer` opción.</span><span class="sxs-lookup"><span data-stu-id="9e15b-243">It must be set together with `searchAnalyzer` and it cannot be set together with hello `analyzer` option.</span></span> <span data-ttu-id="9e15b-244">Una vez que se elige el analizador de hello, no se puede cambiar para el campo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-244">Once hello analyzer is chosen, it cannot be changed for hello field.</span></span>

<span data-ttu-id="9e15b-245">`suggesters`-Conjuntos Hola a modo de búsqueda y campos que son origen de Hola de contenido de Hola para obtener sugerencias.</span><span class="sxs-lookup"><span data-stu-id="9e15b-245">`suggesters` - Sets hello search mode and fields that are hello source of hello content for suggestions.</span></span> <span data-ttu-id="9e15b-246">Consulte [Proveedores de sugerencias](#Suggesters) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="9e15b-246">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="9e15b-247">`scoringProfiles` : define comportamientos de puntuación personalizados que permiten influir en los elementos que aparecen más arriba en los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-247">`scoringProfiles` - Defines custom scoring behaviors that let you influence which items appear higher in search results.</span></span> <span data-ttu-id="9e15b-248">Los perfiles de puntuación se componen de ponderaciones de campos y de funciones.</span><span class="sxs-lookup"><span data-stu-id="9e15b-248">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="9e15b-249">Vea [agregar perfiles de puntuación](https://msdn.microsoft.com/library/azure/dn798928.aspx) para obtener más información sobre atributos de hello usados en un perfil de puntuación.</span><span class="sxs-lookup"><span data-stu-id="9e15b-249">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information about hello attributes used in a scoring profile.</span></span>

<span data-ttu-id="9e15b-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Compatibilidad con idioma**</span><span class="sxs-lookup"><span data-stu-id="9e15b-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Language support**</span></span>

<span data-ttu-id="9e15b-251">Los campos localizables se someten a análisis que con frecuencia implican la separación de palabras, la normalización de texto y el filtrado de términos.</span><span class="sxs-lookup"><span data-stu-id="9e15b-251">Searchable fields undergo analysis that most frequently involves word-breaking, text normalization, and filtering out terms.</span></span> <span data-ttu-id="9e15b-252">De forma predeterminada, los campos de búsqueda en búsqueda de Azure se analizan con hello [analizador estándar Lucene de Apache](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) que divide el texto en los elementos que siguen la["Segmentación de texto Unicode"](http://unicode.org/reports/tr29/) reglas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-252">By default, searchable fields in Azure Search are analyzed with hello [Apache Lucene Standard analyzer](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) which breaks text into elements following the["Unicode Text Segmentation"](http://unicode.org/reports/tr29/) rules.</span></span> <span data-ttu-id="9e15b-253">Además, analizador estándar Hola convierte formato en todos los caracteres tootheir minúsculas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-253">Additionally, hello standard analyzer converts all characters tootheir lower case form.</span></span> <span data-ttu-id="9e15b-254">Los documentos indizados y términos de búsqueda van a través del análisis de Hola durante la indización y procesamiento de consultas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-254">Both indexed documents and search terms go through hello analysis during indexing and query processing.</span></span>

<span data-ttu-id="9e15b-255">Búsqueda de Azure admite una variedad de lenguajes.</span><span class="sxs-lookup"><span data-stu-id="9e15b-255">Azure Search supports a variety of languages.</span></span> <span data-ttu-id="9e15b-256">Cada uno de esos idiomas requiere un analizador de texto no estándar que representa las características de un idioma determinado.</span><span class="sxs-lookup"><span data-stu-id="9e15b-256">Each language requires a non-standard text analyzer which accounts for characteristics of a given language.</span></span> <span data-ttu-id="9e15b-257">Búsqueda de Azure ofrece dos tipos de analizadores:</span><span class="sxs-lookup"><span data-stu-id="9e15b-257">Azure Search offers two types of analyzers:</span></span>

* <span data-ttu-id="9e15b-258">35 analizadores respaldados por Lucene.</span><span class="sxs-lookup"><span data-stu-id="9e15b-258">35 analyzers backed by Lucene.</span></span>
* <span data-ttu-id="9e15b-259">50 analizadores respaldados por la tecnología de procesamiento de lenguaje natural de Microsoft usada en Office y Bing.</span><span class="sxs-lookup"><span data-stu-id="9e15b-259">50 analyzers backed by proprietary Microsoft natural language processing technology used in Office and Bing.</span></span>

<span data-ttu-id="9e15b-260">Algunos desarrolladores de software podría ser preferible Hola solución mucho más familiar, simple, código abierto de Lucene.</span><span class="sxs-lookup"><span data-stu-id="9e15b-260">Some developers might prefer hello more familiar, simple, open-source solution of Lucene.</span></span> <span data-ttu-id="9e15b-261">Analizadores de Lucene son más rápidos, pero analizadores de Microsoft hello tienen capacidades, como la lematización avanzadas, decompounding (en idiomas como el alemán, danés, neerlandés, sueco, noruego, estonio, finalizar, húngaro, eslovaco) y reconocimiento de entidades (las direcciones URL de word mensajes de correo electrónico, fechas, números).</span><span class="sxs-lookup"><span data-stu-id="9e15b-261">Lucene analyzers are faster, but hello Microsoft analyzers have advanced capabilities, such as lemmatization, word decompounding (in languages like German, Danish, Dutch, Swedish, Norwegian, Estonian, Finish, Hungarian, Slovak) and entity recognition (URLs, emails, dates, numbers).</span></span> <span data-ttu-id="9e15b-262">Si es posible, debe ejecutar las comparaciones de ambos toodecide Hola Microsoft y Lucene analizadores cuál es mejor.</span><span class="sxs-lookup"><span data-stu-id="9e15b-262">If possible, you should run comparisons of both hello Microsoft and Lucene analyzers toodecide which one is a better fit.</span></span>

<span data-ttu-id="9e15b-263">***Cómo se comparan***</span><span class="sxs-lookup"><span data-stu-id="9e15b-263">***How they compare***</span></span>

<span data-ttu-id="9e15b-264">Analizador de Lucene de Hola para inglés amplía el analizador estándar Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-264">hello Lucene analyzer for English extends hello standard analyzer.</span></span> <span data-ttu-id="9e15b-265">Elimina los posesivos (los ’s finales) de las palabras, aplica la lematización conforme al [Algoritmo de lematización Porter](http://tartarus.org/~martin/PorterStemmer/) y elimina las [palabras no significativas](http://en.wikipedia.org/wiki/Stop_words) del inglés.</span><span class="sxs-lookup"><span data-stu-id="9e15b-265">It removes possessives (trailing 's) from words, applies stemming as per [Porter Stemming algorithm](http://tartarus.org/~martin/PorterStemmer/), and removes English [stop words](http://en.wikipedia.org/wiki/Stop_words).</span></span>

<span data-ttu-id="9e15b-266">En comparación, analizador de Microsoft hello realiza lematización en lugar de lematización.</span><span class="sxs-lookup"><span data-stu-id="9e15b-266">In comparison, hello Microsoft analyzer performs lemmatization instead of stemming.</span></span> <span data-ttu-id="9e15b-267">Significa que puede controlar mucho mejor formas de palabras derivadas e irregulares, lo que da como resultado unos resultados de búsqueda más pertinentes (consulte el módulo 7 de [presentación MVA de Búsqueda de Azure](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) para obtener más detalles).</span><span class="sxs-lookup"><span data-stu-id="9e15b-267">It means it can handle inflected and irregular word forms much better what results in more relevant search results (watch module 7 of [Azure Search MVA presentation](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) for more details).</span></span>

<span data-ttu-id="9e15b-268">La indización con analizadores de Microsoft por término medio es dos veces toothree más lentos que sus equivalentes de Lucene, según el lenguaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-268">Indexing with Microsoft analyzers is on average two toothree times slower than their Lucene equivalents, depending on hello language.</span></span> <span data-ttu-id="9e15b-269">El rendimiento de la búsqueda no debería verse afectado significativamente en las consultas de tamaño medio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-269">Search performance should not be significantly affected for average size queries.</span></span>

<span data-ttu-id="9e15b-270">***Configuración***</span><span class="sxs-lookup"><span data-stu-id="9e15b-270">***Configuration***</span></span>

<span data-ttu-id="9e15b-271">Para cada campo en la definición del índice hello, puede establecer hello `analyzer` nombre del analizador de tooan propiedad que especifica qué idioma y el proveedor.</span><span class="sxs-lookup"><span data-stu-id="9e15b-271">For each field in hello index definition, you can set hello `analyzer` property tooan analyzer name that specifies which language and vendor.</span></span> <span data-ttu-id="9e15b-272">Hola mismo analizador se aplicarán cuando la indización y búsqueda para ese campo.</span><span class="sxs-lookup"><span data-stu-id="9e15b-272">hello same analyzer will be applied when indexing and searching for that field.</span></span>
<span data-ttu-id="9e15b-273">Por ejemplo, puede tener campos separados para descripciones de hoteles inglés, francés y español que existen en paralelo en hello mismo índice.</span><span class="sxs-lookup"><span data-stu-id="9e15b-273">For example, you can have separate fields for English, French, and Spanish hotel descriptions that exist side-by-side in hello same index.</span></span> <span data-ttu-id="9e15b-274">Hola de uso ['searchFields' parámetro de consulta](#SearchQueryParameters) toospecify qué toosearch de campo específico del idioma en las consultas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-274">Use hello ['searchFields' query parameter](#SearchQueryParameters) toospecify which language-specific field toosearch against in your queries.</span></span> <span data-ttu-id="9e15b-275">Puede revisar los ejemplos de consultas que incluyen hello `analyzer` propiedad en [buscar documentos](#SearchDocs).</span><span class="sxs-lookup"><span data-stu-id="9e15b-275">You can review query examples that include hello `analyzer` property in [Search Documents](#SearchDocs).</span></span> 

<span data-ttu-id="9e15b-276">***Lista de analizadores***</span><span class="sxs-lookup"><span data-stu-id="9e15b-276">***Analyzer list***</span></span>

<span data-ttu-id="9e15b-277">A continuación se muestra la lista de Hola de idiomas admitidos junto con los nombres de analizador de Lucene y Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9e15b-277">Below is hello list of supported languages together with Lucene and Microsoft analyzer names.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="9e15b-278">language</span><span class="sxs-lookup"><span data-stu-id="9e15b-278">Language</span></span></th>
        <th><span data-ttu-id="9e15b-279">Nombre del analizador de Microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-279">Microsoft analyzer name</span></span></th>
        <th><span data-ttu-id="9e15b-280">Nombre del analizador de Lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-280">Lucene analyzer name</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-281">Árabe</span><span class="sxs-lookup"><span data-stu-id="9e15b-281">Arabic</span></span></td>
        <td><span data-ttu-id="9e15b-282">ar.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-282">ar.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-283">ar.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-283">ar.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-284">Armenio</span><span class="sxs-lookup"><span data-stu-id="9e15b-284">Armenian</span></span></td>
        <td></td>
        <td><span data-ttu-id="9e15b-285">hy.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-285">hy.lucene</span></span></td>
      </tr>
    <tr>
        <td><span data-ttu-id="9e15b-286">Bangla</span><span class="sxs-lookup"><span data-stu-id="9e15b-286">Bangla</span></span></td>
        <td><span data-ttu-id="9e15b-287">bn.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-287">bn.microsoft</span></span></td>
        <td></td>
    </tr>
      <tr>
        <td><span data-ttu-id="9e15b-288">Vasco</span><span class="sxs-lookup"><span data-stu-id="9e15b-288">Basque</span></span></td>
        <td></td>
        <td><span data-ttu-id="9e15b-289">eu.Lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-289">eu.lucene</span></span></td>
    </tr>
      <tr>
         <td><span data-ttu-id="9e15b-290">Búlgaro</span><span class="sxs-lookup"><span data-stu-id="9e15b-290">Bulgarian</span></span></td>
        <td><span data-ttu-id="9e15b-291">bg.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-291">bg.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-292">bg.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-292">bg.lucene</span></span></td>
      </tr>
      <tr>
        <td><span data-ttu-id="9e15b-293">Catalán</span><span class="sxs-lookup"><span data-stu-id="9e15b-293">Catalan</span></span></td>
        <td><span data-ttu-id="9e15b-294">ca.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-294">ca.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-295">ca.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-295">ca.lucene</span></span></td>          
      </tr>
    <tr>
        <td><span data-ttu-id="9e15b-296">Chino simplificado</span><span class="sxs-lookup"><span data-stu-id="9e15b-296">Chinese Simplified</span></span></td>
        <td><span data-ttu-id="9e15b-297">zh-Hans.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-297">zh-Hans.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-298">zh-Hans.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-298">zh-Hans.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-299">Chino tradicional</span><span class="sxs-lookup"><span data-stu-id="9e15b-299">Chinese Traditional</span></span></td>
        <td><span data-ttu-id="9e15b-300">zh-Hant.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-300">zh-Hant.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-301">zh-Hant.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-301">zh-Hant.lucene</span></span></td>        
    <tr>
    <tr>
        <td><span data-ttu-id="9e15b-302">Croata</span><span class="sxs-lookup"><span data-stu-id="9e15b-302">Croatian</span></span></td>
        <td><span data-ttu-id="9e15b-303">hr.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-303">hr.microsoft</span></span></td>
        <td/></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-304">Checo</span><span class="sxs-lookup"><span data-stu-id="9e15b-304">Czech</span></span></td>
        <td><span data-ttu-id="9e15b-305">cs.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-305">cs.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-306">cs.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-306">cs.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="9e15b-307">Danés</span><span class="sxs-lookup"><span data-stu-id="9e15b-307">Danish</span></span></td>
        <td><span data-ttu-id="9e15b-308">da.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-308">da.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-309">da.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-309">da.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="9e15b-310">Neerlandés</span><span class="sxs-lookup"><span data-stu-id="9e15b-310">Dutch</span></span></td>
        <td><span data-ttu-id="9e15b-311">nl.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-311">nl.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-312">nl.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-312">nl.lucene</span></span></td>    
    </tr>    
    <tr>
        <td><span data-ttu-id="9e15b-313">English</span><span class="sxs-lookup"><span data-stu-id="9e15b-313">English</span></span></td>        
        <td><span data-ttu-id="9e15b-314">en.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-314">en.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-315">en.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-315">en.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-316">Estonio</span><span class="sxs-lookup"><span data-stu-id="9e15b-316">Estonian</span></span></td>
        <td><span data-ttu-id="9e15b-317">et.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-317">et.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-318">Finés</span><span class="sxs-lookup"><span data-stu-id="9e15b-318">Finnish</span></span></td>
        <td><span data-ttu-id="9e15b-319">fi.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-319">fi.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-320">fi.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-320">fi.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="9e15b-321">Francés</span><span class="sxs-lookup"><span data-stu-id="9e15b-321">French</span></span></td>
        <td><span data-ttu-id="9e15b-322">fr.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-322">fr.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-323">fr.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-323">fr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-324">Gallego</span><span class="sxs-lookup"><span data-stu-id="9e15b-324">Galician</span></span></td>
        <td></td>
        <td><span data-ttu-id="9e15b-325">gl.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-325">gl.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="9e15b-326">Alemán</span><span class="sxs-lookup"><span data-stu-id="9e15b-326">German</span></span></td>
        <td><span data-ttu-id="9e15b-327">de.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-327">de.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-328">de.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-328">de.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-329">Griego</span><span class="sxs-lookup"><span data-stu-id="9e15b-329">Greek</span></span></td>
        <td><span data-ttu-id="9e15b-330">el.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-330">el.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-331">el.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-331">el.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-332">Gujarati</span><span class="sxs-lookup"><span data-stu-id="9e15b-332">Gujarati</span></span></td>
        <td><span data-ttu-id="9e15b-333">gu.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-333">gu.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-334">Hebreo</span><span class="sxs-lookup"><span data-stu-id="9e15b-334">Hebrew</span></span></td>
        <td><span data-ttu-id="9e15b-335">he.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-335">he.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-336">Hindi</span><span class="sxs-lookup"><span data-stu-id="9e15b-336">Hindi</span></span></td>
        <td><span data-ttu-id="9e15b-337">hi.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-337">hi.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-338">hi.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-338">hi.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-339">Húngaro</span><span class="sxs-lookup"><span data-stu-id="9e15b-339">Hungarian</span></span></td>        
        <td><span data-ttu-id="9e15b-340">hu.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-340">hu.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-341">hu.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-341">hu.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-342">Islandés</span><span class="sxs-lookup"><span data-stu-id="9e15b-342">Icelandic</span></span></td>
        <td><span data-ttu-id="9e15b-343">is.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-343">is.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-344">Indonesio (Bahasa)</span><span class="sxs-lookup"><span data-stu-id="9e15b-344">Indonesian (Bahasa)</span></span></td>
        <td><span data-ttu-id="9e15b-345">id.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-345">id.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-346">id.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-346">id.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-347">Irlandés</span><span class="sxs-lookup"><span data-stu-id="9e15b-347">Irish</span></span></td>
        <td></td>
          <td><span data-ttu-id="9e15b-348">ga.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-348">ga.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-349">Italiano</span><span class="sxs-lookup"><span data-stu-id="9e15b-349">Italian</span></span></td>
        <td><span data-ttu-id="9e15b-350">it.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-350">it.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-351">it.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-351">it.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-352">Japonés</span><span class="sxs-lookup"><span data-stu-id="9e15b-352">Japanese</span></span></td>
        <td><span data-ttu-id="9e15b-353">ja.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-353">ja.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-354">ja.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-354">ja.lucene</span></span></td>

    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-355">Kannada</span><span class="sxs-lookup"><span data-stu-id="9e15b-355">Kannada</span></span></td>
        <td><span data-ttu-id="9e15b-356">ka.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-356">ka.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-357">Coreano</span><span class="sxs-lookup"><span data-stu-id="9e15b-357">Korean</span></span></td>
        <td><span data-ttu-id="9e15b-358">ko.Microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-358">ko.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-359">ko.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-359">ko.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-360">Letón</span><span class="sxs-lookup"><span data-stu-id="9e15b-360">Latvian</span></span></td>        
        <td><span data-ttu-id="9e15b-361">lv.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-361">lv.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-362">lv.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-362">lv.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-363">Lituano</span><span class="sxs-lookup"><span data-stu-id="9e15b-363">Lithuanian</span></span></td>
        <td><span data-ttu-id="9e15b-364">lt.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-364">lt.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-365">Malayalam</span><span class="sxs-lookup"><span data-stu-id="9e15b-365">Malayalam</span></span></td>
        <td><span data-ttu-id="9e15b-366">ml.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-366">ml.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-367">Malayo (latino)</span><span class="sxs-lookup"><span data-stu-id="9e15b-367">Malay (Latin)</span></span></td>
        <td><span data-ttu-id="9e15b-368">ms.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-368">ms.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-369">Marathi</span><span class="sxs-lookup"><span data-stu-id="9e15b-369">Marathi</span></span></td>
        <td><span data-ttu-id="9e15b-370">mr.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-370">mr.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-371">Noruego</span><span class="sxs-lookup"><span data-stu-id="9e15b-371">Norwegian</span></span></td>
        <td><span data-ttu-id="9e15b-372">nb.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-372">nb.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-373">no.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-373">no.lucene</span></span></td>        
    </tr>
      <tr>
        <td><span data-ttu-id="9e15b-374">Persa</span><span class="sxs-lookup"><span data-stu-id="9e15b-374">Persian</span></span></td>
        <td></td>
        <td><span data-ttu-id="9e15b-375">fa.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-375">fa.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="9e15b-376">Polaco</span><span class="sxs-lookup"><span data-stu-id="9e15b-376">Polish</span></span></td>
        <td><span data-ttu-id="9e15b-377">pl.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-377">pl.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-378">pl.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-378">pl.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-379">Portugués (Brasil)</span><span class="sxs-lookup"><span data-stu-id="9e15b-379">Portuguese (Brazil)</span></span></td>
        <td><span data-ttu-id="9e15b-380">pt-Br.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-380">pt-Br.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-381">pt-Br.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-381">pt-Br.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-382">Portugués (Portugal)</span><span class="sxs-lookup"><span data-stu-id="9e15b-382">Portuguese (Portugal)</span></span></td>
        <td><span data-ttu-id="9e15b-383">pt-Pt.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-383">pt-Pt.microsoft</span></span></td>        
        <td><span data-ttu-id="9e15b-384">pt-Pt.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-384">pt-Pt.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-385">Punjabi</span><span class="sxs-lookup"><span data-stu-id="9e15b-385">Punjabi</span></span></td>
        <td><span data-ttu-id="9e15b-386">pa.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-386">pa.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-387">Rumano</span><span class="sxs-lookup"><span data-stu-id="9e15b-387">Romanian</span></span></td>
        <td><span data-ttu-id="9e15b-388">ro.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-388">ro.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-389">ro.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-389">ro.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-390">Ruso</span><span class="sxs-lookup"><span data-stu-id="9e15b-390">Russian</span></span></td>
        <td><span data-ttu-id="9e15b-391">ru.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-391">ru.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-392">ru.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-392">ru.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-393">Serbio (cirílico)</span><span class="sxs-lookup"><span data-stu-id="9e15b-393">Serbian (Cyrillic)</span></span></td>
        <td><span data-ttu-id="9e15b-394">sr-cyrillic.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-394">sr-cyrillic.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-395">Serbio (latino)</span><span class="sxs-lookup"><span data-stu-id="9e15b-395">Serbian (Latin)</span></span></td>
        <td><span data-ttu-id="9e15b-396">sr-latin.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-396">sr-latin.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-397">Eslovaco</span><span class="sxs-lookup"><span data-stu-id="9e15b-397">Slovak</span></span></td>
        <td><span data-ttu-id="9e15b-398">sk.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-398">sk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-399">Esloveno</span><span class="sxs-lookup"><span data-stu-id="9e15b-399">Slovenian</span></span></td>
        <td><span data-ttu-id="9e15b-400">sl.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-400">sl.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-401">Español</span><span class="sxs-lookup"><span data-stu-id="9e15b-401">Spanish</span></span></td>
        <td><span data-ttu-id="9e15b-402">es.Microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-402">es.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-403">es.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-403">es.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-404">Sueco</span><span class="sxs-lookup"><span data-stu-id="9e15b-404">Swedish</span></span></td>
        <td><span data-ttu-id="9e15b-405">sv.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-405">sv.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-406">sv.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-406">sv.lucene</span></span></td>
    </tr>

    <tr>
        <td><span data-ttu-id="9e15b-407">Tamil</span><span class="sxs-lookup"><span data-stu-id="9e15b-407">Tamil</span></span></td>
        <td><span data-ttu-id="9e15b-408">ta.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-408">ta.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-409">Telugu</span><span class="sxs-lookup"><span data-stu-id="9e15b-409">Telugu</span></span></td>
        <td><span data-ttu-id="9e15b-410">te.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-410">te.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-411">Tailandés</span><span class="sxs-lookup"><span data-stu-id="9e15b-411">Thai</span></span></td>
        <td><span data-ttu-id="9e15b-412">th.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-412">th.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-413">th.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-413">th.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-414">Turco</span><span class="sxs-lookup"><span data-stu-id="9e15b-414">Turkish</span></span></td>
        <td><span data-ttu-id="9e15b-415">tr.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-415">tr.microsoft</span></span></td>
        <td><span data-ttu-id="9e15b-416">tr.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-416">tr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-417">Ucraniano</span><span class="sxs-lookup"><span data-stu-id="9e15b-417">Ukrainian</span></span></td>
        <td><span data-ttu-id="9e15b-418">uk.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-418">uk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-419">Urdu</span><span class="sxs-lookup"><span data-stu-id="9e15b-419">Urdu</span></span></td>
        <td><span data-ttu-id="9e15b-420">ur.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-420">ur.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-421">Vietnamita</span><span class="sxs-lookup"><span data-stu-id="9e15b-421">Vietnamese</span></span></td>
        <td><span data-ttu-id="9e15b-422">vi.microsoft</span><span class="sxs-lookup"><span data-stu-id="9e15b-422">vi.microsoft</span></span></td>
        <td></td>
    </tr>
    <td colspan="3"><span data-ttu-id="9e15b-423">Además, Búsqueda de Azure proporciona las configuraciones del analizador de lenguaje válido</span><span class="sxs-lookup"><span data-stu-id="9e15b-423">Additionally Azure Search provides language-agnostic analyzer configurations</span></span></td>
    <tr>
        <td><span data-ttu-id="9e15b-424">Plegamiento de ASCII estándar</span><span class="sxs-lookup"><span data-stu-id="9e15b-424">Standard ASCII Folding</span></span></td>
        <td><span data-ttu-id="9e15b-425">standardasciifolding.lucene</span><span class="sxs-lookup"><span data-stu-id="9e15b-425">standardasciifolding.lucene</span></span></td>
        <td>
        <ul>
            <li><span data-ttu-id="9e15b-426">Segmentación de texto Unicode (Tokenizer estándar)</span><span class="sxs-lookup"><span data-stu-id="9e15b-426">Unicode text segmentation (Standard Tokenizer)</span></span></li>
            <li><span data-ttu-id="9e15b-427">Filtro de conversión de ASCII - convierte los caracteres Unicode que no pertenecen toohello conjunto de los primeros 127 caracteres ASCII en sus valores ASCII equivalentes.</span><span class="sxs-lookup"><span data-stu-id="9e15b-427">ASCII folding filter - converts Unicode characters that don't belong toohello set of first 127 ASCII characters into their ASCII equivalents.</span></span> <span data-ttu-id="9e15b-428">Esto es útil para quitar los signos diacríticos.</span><span class="sxs-lookup"><span data-stu-id="9e15b-428">This is useful for removing diacritics.</span></span></li>
        </ul>
        </td>
    </tr>
</table>

<span data-ttu-id="9e15b-429">Todos los analizadores con nombres anotados con <i>lucene</i> disponen de tecnología de [analizadores de idioma de Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span><span class="sxs-lookup"><span data-stu-id="9e15b-429">All analyzers with names annotated with <i>lucene</i> are powered by [Apache Lucene's language analyzers](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span></span> <span data-ttu-id="9e15b-430">Puede encontrar más información sobre el filtro de conversión de ASCII de hello [aquí](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span><span class="sxs-lookup"><span data-stu-id="9e15b-430">More information about hello ASCII folding filter can be found [here](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span></span>

<span data-ttu-id="9e15b-431">**Proveedores de sugerencias**</span><span class="sxs-lookup"><span data-stu-id="9e15b-431">**Suggesters**</span></span>

<span data-ttu-id="9e15b-432">Un `suggester` define qué campos en un índice son utilizado toosupport Autocompletar en las búsquedas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-432">A `suggester` defines which fields in an index are used toosupport auto-complete in searches.</span></span> <span data-ttu-id="9e15b-433">Normalmente, las cadenas de búsqueda parcial se envían toohello [API sugerencias](#Suggestions) mientras el usuario de hello está escribiendo una consulta de búsqueda y Hola API devuelve un conjunto de frases sugeridas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-433">Typically partial search strings are sent toohello [Suggestions API](#Suggestions) while hello user is typing a search query, and hello API returns a set of suggested phrases.</span></span> <span data-ttu-id="9e15b-434">Un proveedor de sugerencias que defina en el índice de hello determina qué campos son los términos de búsqueda anticipada de hello toobuild usado.</span><span class="sxs-lookup"><span data-stu-id="9e15b-434">A suggester that you define in hello index determines which fields are used toobuild hello type-ahead search terms.</span></span> <span data-ttu-id="9e15b-435">Consulte [Proveedores de sugerencias](#Suggesters) para obtener más detalles sobre la configuración.</span><span class="sxs-lookup"><span data-stu-id="9e15b-435">See [Suggesters](#Suggesters) for configuration details.</span></span>

<span data-ttu-id="9e15b-436">**Perfiles de puntuación**</span><span class="sxs-lookup"><span data-stu-id="9e15b-436">**Scoring profiles**</span></span>

<span data-ttu-id="9e15b-437">Un `scoringProfile` define los comportamientos de puntuación personalizados que pueden influir en los elementos que aparecen más arriba en resultados de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-437">A `scoringProfile` defines custom scoring behaviors that let you influence which items appear higher in hello search results.</span></span> <span data-ttu-id="9e15b-438">Los perfiles de puntuación se componen de ponderaciones de campos y de funciones.</span><span class="sxs-lookup"><span data-stu-id="9e15b-438">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="9e15b-439">toouse usarlas, se especifica un perfil por nombre en la cadena de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-439">toouse them, you specify a profile by name on hello query string.</span></span>

<span data-ttu-id="9e15b-440">Un perfil de puntuación predeterminado funciona en segundo Hola plano toocompute una puntuación de búsqueda para todos los elementos de un conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="9e15b-440">A default scoring profile operates behind hello scenes toocompute a search score for every item in a result set.</span></span> <span data-ttu-id="9e15b-441">Puede usar Hola interno, sin nombre perfil de puntuación.</span><span class="sxs-lookup"><span data-stu-id="9e15b-441">You can use hello internal, unnamed scoring profile.</span></span> <span data-ttu-id="9e15b-442">Por otra parte, defina `defaultScoringProfile` toouse un perfil personalizado como Hola de forma predeterminada, se invoca cuando un perfil personalizado no se especifica en la cadena de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-442">Alternatively, set `defaultScoringProfile` toouse a custom profile as hello default, invoked whenever a custom profile is not specified on hello query string.</span></span>

<span data-ttu-id="9e15b-443">Vea [puntuación agregar perfiles de índice de búsqueda tooa (API de REST de servicio de búsqueda de Azure)](search-api-scoring-profiles-2015-02-28-preview.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="9e15b-443">See [Add scoring profiles tooa search index (Azure Search Service REST API)](search-api-scoring-profiles-2015-02-28-preview.md) for details.</span></span>

<span data-ttu-id="9e15b-444">**Opciones de CORS**</span><span class="sxs-lookup"><span data-stu-id="9e15b-444">**CORS Options**</span></span>

<span data-ttu-id="9e15b-445">Javascript del lado cliente no puede llamar a las API de forma predeterminada, ya que el Explorador de hello impedirá todas las solicitudes entre orígenes.</span><span class="sxs-lookup"><span data-stu-id="9e15b-445">Client-side Javascript cannot call any APIs by default since hello browser will prevent all cross-origin requests.</span></span> <span data-ttu-id="9e15b-446">Habilitar CORS (uso compartido recursos entre orígenes) por establecer hello `corsOptions` índice tooyour de atributo tooallow consultas entre orígenes.</span><span class="sxs-lookup"><span data-stu-id="9e15b-446">Enable CORS (Cross-Origin Resource Sharing) by setting hello `corsOptions` attribute tooallow cross-origin queries tooyour index.</span></span> <span data-ttu-id="9e15b-447">Tenga en cuenta que solamente las API de consulta admiten CORS por motivos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9e15b-447">Note that only query APIs support CORS for security reasons.</span></span> <span data-ttu-id="9e15b-448">Hola siguientes opciones se pueden establecer para CORS:</span><span class="sxs-lookup"><span data-stu-id="9e15b-448">hello following options can be set for CORS:</span></span>

* <span data-ttu-id="9e15b-449">`allowedOrigins`(obligatorio): se trata de una lista de orígenes que se le concederá el índice de tooyour de acceso.</span><span class="sxs-lookup"><span data-stu-id="9e15b-449">`allowedOrigins` (required): This is a list of origins that will be granted access tooyour index.</span></span> <span data-ttu-id="9e15b-450">Esto significa que cualquier código de Javascript que se sirva desde esos orígenes permite tooquery su índice (suponiendo proporciona la clave de API correcta de hello).</span><span class="sxs-lookup"><span data-stu-id="9e15b-450">This means that any Javascript code served from those origins will be allowed tooquery your index (assuming it provides hello correct API key).</span></span> <span data-ttu-id="9e15b-451">Cada origen suele del formulario de hello `protocol://fully-qualified-domain-name:port` aunque a menudo se omite el puerto de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-451">Each origin is typically of hello form `protocol://fully-qualified-domain-name:port` although hello port is often omitted.</span></span> <span data-ttu-id="9e15b-452">Consulte [este artículo](http://go.microsoft.com/fwlink/?LinkId=330822) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="9e15b-452">See [this article](http://go.microsoft.com/fwlink/?LinkId=330822) for more details.</span></span>
  * <span data-ttu-id="9e15b-453">Si desea que los orígenes de tooall de acceso tooallow, incluya `*` como un único elemento de hello `allowedOrigins` matriz.</span><span class="sxs-lookup"><span data-stu-id="9e15b-453">If you want tooallow access tooall origins, include `*` as a single item in hello `allowedOrigins` array.</span></span> <span data-ttu-id="9e15b-454">Tenga en cuenta que **esta no es una práctica recomendada para los servicios de búsqueda de producción.**</span><span class="sxs-lookup"><span data-stu-id="9e15b-454">Note that **this is not recommended practice for production search services.**</span></span> <span data-ttu-id="9e15b-455">Sin embargo, puede ser útil para el desarrollo o con fines de depuración.</span><span class="sxs-lookup"><span data-stu-id="9e15b-455">However, it may be useful for development or debugging purposes.</span></span>
* <span data-ttu-id="9e15b-456">`maxAgeInSeconds`(opcional): los exploradores utilizan este las respuestas preparatorias de CORS toocache de valor toodetermine Hola duración (en segundos).</span><span class="sxs-lookup"><span data-stu-id="9e15b-456">`maxAgeInSeconds` (optional): Browsers use this value toodetermine hello duration (in seconds) toocache CORS preflight responses.</span></span> <span data-ttu-id="9e15b-457">Esto debe ser un entero no negativo.</span><span class="sxs-lookup"><span data-stu-id="9e15b-457">This must be a non-negative integer.</span></span> <span data-ttu-id="9e15b-458">Hola mayor que es este valor, será un mejor rendimiento de hello, pero hello más tiempo que tardará CORS directiva cambios tootake efecto.</span><span class="sxs-lookup"><span data-stu-id="9e15b-458">hello larger this value is, hello better performance will be, but hello longer it will take for CORS policy changes tootake effect.</span></span> <span data-ttu-id="9e15b-459">Si no se establece, se usará una duración predeterminada de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="9e15b-459">If it is not set, a default duration of 5 minutes will be used.</span></span>

<span data-ttu-id="9e15b-460"><a name="CreateUpdateIndexExample"></a>
**Ejemplo de cuerpo de solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-460"><a name="CreateUpdateIndexExample"></a>
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

<span data-ttu-id="9e15b-461">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="9e15b-461">**Response**</span></span>

<span data-ttu-id="9e15b-462">Para obtener una solicitud correcta: "201 Creado".</span><span class="sxs-lookup"><span data-stu-id="9e15b-462">For a successful request: "201 Created".</span></span>

<span data-ttu-id="9e15b-463">De forma predeterminada cuerpo de respuesta de hello contendrá hello JSON para la definición de índice de Hola que se creó.</span><span class="sxs-lookup"><span data-stu-id="9e15b-463">By default hello response body will contain hello JSON for hello index definition that was created.</span></span> <span data-ttu-id="9e15b-464">Si hello `Prefer` encabezado de solicitud se establece demasiado`return=minimal`, cuerpo de respuesta de hello estará vacío y código de estado de hello correcto será "204 Sin contenido" en lugar de "201 Created".</span><span class="sxs-lookup"><span data-stu-id="9e15b-464">If hello `Prefer` request header is set too`return=minimal`, hello response body will be empty and hello success status code will be "204 No Content" instead of "201 Created".</span></span> <span data-ttu-id="9e15b-465">Esto es cierto independientemente de si PUT o POST estaba índice de hello toocreate usado.</span><span class="sxs-lookup"><span data-stu-id="9e15b-465">This is true regardless of whether PUT or POST was used toocreate hello index.</span></span>

<span data-ttu-id="9e15b-466">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="9e15b-466">**Remarks**</span></span>

<span data-ttu-id="9e15b-467">Actualmente, hay compatibilidad limitada para las actualizaciones del esquema de índice.</span><span class="sxs-lookup"><span data-stu-id="9e15b-467">Currently, there is limited support for index schema updates.</span></span> <span data-ttu-id="9e15b-468">Actualmente no se admiten las actualizaciones del esquema que requieran volver a indexar, como el cambio de tipos de campo.</span><span class="sxs-lookup"><span data-stu-id="9e15b-468">Any schema updates that would require re-indexing such as changing field types are not currently supported.</span></span> <span data-ttu-id="9e15b-469">Aunque no se puede cambiar los campos existentes o eliminado los campos nuevos se pueden agregar índice existente tooan en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="9e15b-469">Although existing fields cannot be changed or deleted, new fields can be added tooan existing index at any time.</span></span> <span data-ttu-id="9e15b-470">Cuando se agrega un nuevo campo, todos los documentos existentes en el índice de hello automáticamente tendrá un valor null para ese campo.</span><span class="sxs-lookup"><span data-stu-id="9e15b-470">When a new field is added, all existing documents in hello index will automatically have a null value for that field.</span></span> <span data-ttu-id="9e15b-471">No hay espacio de almacenamiento adicional se consumirán hasta que se agreguen nuevos documentos toohello índice.</span><span class="sxs-lookup"><span data-stu-id="9e15b-471">No additional storage space will be consumed until new documents are added toohello index.</span></span>

<a name="Suggesters"></a>

## <a name="suggesters"></a><span data-ttu-id="9e15b-472">Proveedores de sugerencias</span><span class="sxs-lookup"><span data-stu-id="9e15b-472">Suggesters</span></span>
<span data-ttu-id="9e15b-473">característica de sugerencias de Hello en búsqueda de Azure es una capacidad de consulta anticipada o Autocompletar, que proporciona una lista de posibles términos de búsqueda en respuesta toopartial las entradas de cadena especificadas en un cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-473">hello suggestions feature in Azure Search is a type-ahead or auto-complete query capability, providing a list of potential search terms in response toopartial string inputs entered into a search box.</span></span> <span data-ttu-id="9e15b-474">Probablemente haya observado sugerencias de consulta al utilizar los motores de búsqueda web comerciales: si se escribe ".NET" en Bing, se genera una lista de términos para ".NET 4.5", ".NET Framework 3.5", y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="9e15b-474">You've probably noticed query suggestions when using commercial web search engines: typing ".NET" in Bing produces a list of terms for ".NET 4.5", ".NET Framework 3.5", and so forth.</span></span> <span data-ttu-id="9e15b-475">Cuando se usa el servicio de búsqueda de hello API de REST, implementación de sugerencias en una aplicación de búsqueda de Azure personalizada requiere siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="9e15b-475">When using hello Search service REST API, implementing suggestions in a custom Azure Search application requires hello following:</span></span>

* <span data-ttu-id="9e15b-476">Habilite sugerencias agregando una **proveedor de sugerencias** construcción en el índice, se ha dado nombre hello, modo de búsqueda y una lista de campos para que anticipada se invoca.</span><span class="sxs-lookup"><span data-stu-id="9e15b-476">Enable suggestions by adding a **suggester** construction in your index, giving hello name, search mode, and a list of fields for which type-ahead is invoked.</span></span> <span data-ttu-id="9e15b-477">Por ejemplo, si especifica "cityName" como un campo de origen, escriba una cadena de búsqueda parcial del "Mar" dará como resultado "Seattle", "Seaside" y "Seatac" (las tres son nombres de ciudades reales) presenten como usuario de toohello de sugerencias de consulta.</span><span class="sxs-lookup"><span data-stu-id="9e15b-477">For example, if you specify "cityName" as a source field, typing a partial search string of "Sea" will result in "Seattle", "Seaside", and "Seatac" (all three are actual city names) offered up as query suggestions toohello user.</span></span>
* <span data-ttu-id="9e15b-478">Invocar sugerencias que realiza la llamada hello [API sugerencias](#Suggestions) en el código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="9e15b-478">Invoke suggestions by calling hello [Suggestions API](#Suggestions) in your application code.</span></span> <span data-ttu-id="9e15b-479">Normalmente las cadenas de búsqueda parcial se envían toohello servicio mientras Hola usuario escribe una consulta de búsqueda, y esta API devuelve un conjunto de frases sugeridas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-479">Typically partial search strings are sent toohello service while hello user is typing a search query, and this API returns a set of suggested phrases.</span></span>

<span data-ttu-id="9e15b-480">Este artículo se explica cómo tooconfigure una **proveedor de sugerencias**.</span><span class="sxs-lookup"><span data-stu-id="9e15b-480">This article explains how tooconfigure a **suggester**.</span></span> <span data-ttu-id="9e15b-481">También debe revisar hello [API sugerencias](#Suggestions) para obtener más información sobre cómo se utiliza un proveedor de sugerencias.</span><span class="sxs-lookup"><span data-stu-id="9e15b-481">You should also review hello [Suggestions API](#Suggestions) for details on how a suggester is used.</span></span>

<span data-ttu-id="9e15b-482">**Uso**</span><span class="sxs-lookup"><span data-stu-id="9e15b-482">**Usage**</span></span>

<span data-ttu-id="9e15b-483">`Suggesters`se crean en el índice de Hola y funcionan mejor cuando se usa toosuggest específicos se documentan en lugar de términos o frases sueltos.</span><span class="sxs-lookup"><span data-stu-id="9e15b-483">`Suggesters` are created in hello index and work best when used toosuggest specific documents rather than loose terms or phrases.</span></span> <span data-ttu-id="9e15b-484">campos de Hello más recomendados son títulos, nombres y demás frases relativamente cortas que puedan identificar un elemento.</span><span class="sxs-lookup"><span data-stu-id="9e15b-484">hello best candidate fields are titles, names, and other relatively short phrases that can identify an item.</span></span> <span data-ttu-id="9e15b-485">Los campos repetitivos son menos efectivos, por ejemplo, las categorías y etiquetas, o campos muy largos como campos de descripciones o comentarios.</span><span class="sxs-lookup"><span data-stu-id="9e15b-485">Less effective are repetitive fields, such as categories and tags, or very long fields such as descriptions or comments fields.</span></span>

<span data-ttu-id="9e15b-486">Como parte de la definición del índice hello, puede agregar un único proveedor de sugerencias toohello `suggesters` colección.</span><span class="sxs-lookup"><span data-stu-id="9e15b-486">As part of hello index definition, you can add a single suggester toohello `suggesters` collection.</span></span> <span data-ttu-id="9e15b-487">Propiedades que definen un proveedor de sugerencias Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="9e15b-487">Properties that define a suggester include hello following:</span></span>

* <span data-ttu-id="9e15b-488">`name`: nombre de hello del proveedor de sugerencias de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-488">`name`: hello name of hello suggester.</span></span> <span data-ttu-id="9e15b-489">Usar nombre de hello del proveedor de sugerencias de hello al llamar a hello `suggest` API.</span><span class="sxs-lookup"><span data-stu-id="9e15b-489">You use hello name of hello suggester when calling hello `suggest` API.</span></span>
* <span data-ttu-id="9e15b-490">`searchMode`: Hola toosearch estrategia que se usa para frases candidatas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-490">`searchMode`: hello strategy used toosearch for candidate phrases.</span></span> <span data-ttu-id="9e15b-491">Hola único modo que admite actualmente es `analyzingInfixMatching`, que realiza una coincidencia flexible de frases al principio de Hola o en medio de Hola de oraciones.</span><span class="sxs-lookup"><span data-stu-id="9e15b-491">hello only mode currently supported is `analyzingInfixMatching`, which performs flexible matching of phrases at hello beginning or in hello middle of sentences.</span></span>
* <span data-ttu-id="9e15b-492">`sourceFields`: Una lista de uno o más campos que son origen de hello del contenido de Hola para obtener sugerencias.</span><span class="sxs-lookup"><span data-stu-id="9e15b-492">`sourceFields`: A list of one or more fields that are hello source of hello content for suggestions.</span></span> <span data-ttu-id="9e15b-493">Solo los campos de tipo `Edm.String` y `Collection(Edm.String)` pueden ser orígenes para obtener sugerencias.</span><span class="sxs-lookup"><span data-stu-id="9e15b-493">Only fields of type `Edm.String` and `Collection(Edm.String)` may be sources for suggestions.</span></span> <span data-ttu-id="9e15b-494">Solo se pueden usar los campos que no tienen un analizador de lenguaje personalizado establecido.</span><span class="sxs-lookup"><span data-stu-id="9e15b-494">Only fields that don't have a custom language analyzer set can be used.</span></span>

<span data-ttu-id="9e15b-495">**Ejemplo de proveedor de sugerencias**</span><span class="sxs-lookup"><span data-stu-id="9e15b-495">**Suggester Example**</span></span>

<span data-ttu-id="9e15b-496">Un proveedor de sugerencias es parte del índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-496">A suggester is part of hello index.</span></span> <span data-ttu-id="9e15b-497">Puede haber solo un proveedor de sugerencias en hello `suggesters` colección de campos de la colección en la versión actual de hello, junto con hello y `scoringProfiles`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-497">Only one suggester can exist in hello `suggesters` collection in hello current version, alongside hello fields collection and `scoringProfiles`.</span></span>

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
> <span data-ttu-id="9e15b-498">Si ha usado la versión de vista previa pública de Hola de búsqueda de Azure, `suggesters` reemplaza una propiedad booleana más antigua (`"suggestions": false`) que solo admitía sugerencias de prefijo para cadenas cortas (3-25 caracteres).</span><span class="sxs-lookup"><span data-stu-id="9e15b-498">If you used hello public preview version of Azure Search, `suggesters` replaces an older boolean property (`"suggestions": false`) that only supported prefix suggestions for short strings (3-25 characters).</span></span> <span data-ttu-id="9e15b-499">Su reemplazo, `suggesters`, admite coincidencias de infijo que encuentra términos coincidentes al principio de Hola o en medio de Hola de contenido de este campo, con una mejor tolerancia a errores en las cadenas de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-499">Its replacement, `suggesters`, supports infix matching that finds matching terms at hello beginning or in hello middle of field content, with better tolerance for mistakes in search strings.</span></span> <span data-ttu-id="9e15b-500">A partir de la versión de disponibilidad general de hello, ahora es única implementación de sugerencias de hello API de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-500">Starting with hello generally available release, this is now hello only implementation of hello suggestions API.</span></span> <span data-ttu-id="9e15b-501">Hola anterior `suggestions` propiedad que se introdujo en `api-version=2014-07-31-Preview` continúa toowork en esa versión, pero no está operativa en hello `2015-02-28` o versiones posteriores de búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e15b-501">hello older `suggestions` property that was introduced in `api-version=2014-07-31-Preview` continues toowork in that version, but is not operational in hello `2015-02-28` or later versions of Azure Search.</span></span>
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a><span data-ttu-id="9e15b-502">Actualizar índice</span><span class="sxs-lookup"><span data-stu-id="9e15b-502">Update Index</span></span>
<span data-ttu-id="9e15b-503">Puede actualizar un índice existente en Búsqueda de Azure mediante una solicitud HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="9e15b-503">You can update an existing index within Azure Search using an HTTP PUT request.</span></span> <span data-ttu-id="9e15b-504">Las actualizaciones pueden incluir agregar nuevos campos toohello esquema existente, modificar las opciones de CORS y modificar perfiles de puntuación.</span><span class="sxs-lookup"><span data-stu-id="9e15b-504">Updates can include adding new fields toohello existing schema, modifying CORS options, and modifying scoring profiles.</span></span> <span data-ttu-id="9e15b-505">Consulte [Agregar perfiles de puntuación](https://msdn.microsoft.com/library/azure/dn798928.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="9e15b-505">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> <span data-ttu-id="9e15b-506">Especificar nombre de Hola de hello índice tooupdate en URI de solicitud de hello:</span><span class="sxs-lookup"><span data-stu-id="9e15b-506">You specify hello name of hello index tooupdate on hello request URI:</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="9e15b-507">**Importante:** compatibilidad con las actualizaciones de esquema de índice es toooperations limitada que no requieren volver a generar índice de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-507">**Important:** Support for index schema updates is limited toooperations that don't require rebuilding hello search index.</span></span> <span data-ttu-id="9e15b-508">Actualmente no se admiten las actualizaciones del esquema que requieran volver a indexar, como el cambio de tipos de campo.</span><span class="sxs-lookup"><span data-stu-id="9e15b-508">Any schema updates that would require re-indexing, such as changing field types, are not currently supported.</span></span> <span data-ttu-id="9e15b-509">Pueden agregarse nuevos campos en cualquier momento, aunque no se pueden modificar ni eliminar los campos existentes.</span><span class="sxs-lookup"><span data-stu-id="9e15b-509">New fields can be added at any time, although existing fields cannot be changed or deleted.</span></span> <span data-ttu-id="9e15b-510">Hello Esto mismo se aplica demasiado`suggesters`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-510">hello same applies too`suggesters`.</span></span> <span data-ttu-id="9e15b-511">Pueden agregarse nuevos campos se agregan tooa proveedor de sugerencias en campos de Hola Hola hora, pero no se puede quitar campos `suggesters` y no se puede agregar campos existentes demasiado`suggesters`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-511">New fields may be added tooa suggester at hello time hello fields are added, but fields cannot be removed from `suggesters` and existing fields cannot be added too`suggesters`.</span></span>

<span data-ttu-id="9e15b-512">Al agregar un nuevo índice tooan de campo, todos los documentos existentes en el índice de hello automáticamente tendrá un valor null para ese campo.</span><span class="sxs-lookup"><span data-stu-id="9e15b-512">When adding a new field tooan index, all existing documents in hello index will automatically have a null value for that field.</span></span> <span data-ttu-id="9e15b-513">No hay espacio de almacenamiento adicional se consumirán hasta que se agreguen nuevos documentos toohello índice.</span><span class="sxs-lookup"><span data-stu-id="9e15b-513">No additional storage space will be consumed until new documents are added toohello index.</span></span>

<span data-ttu-id="9e15b-514">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-514">**Request**</span></span>

<span data-ttu-id="9e15b-515">HTTPS es necesario para todas las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-515">HTTPS is required for all service requests.</span></span> <span data-ttu-id="9e15b-516">Hola **Actualizar índice** solicitud se construye utilizando PUT de HTTP.</span><span class="sxs-lookup"><span data-stu-id="9e15b-516">hello **Update Index** request is constructed using HTTP PUT.</span></span> <span data-ttu-id="9e15b-517">Con PUT, el nombre del índice de hello es parte de la dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-517">With PUT, hello index name is part of hello URL.</span></span> <span data-ttu-id="9e15b-518">Si el índice de hello no existe, se crea.</span><span class="sxs-lookup"><span data-stu-id="9e15b-518">If hello index doesn't exist, it is created.</span></span> <span data-ttu-id="9e15b-519">Si ya existe un índice de hello, es toohello actualizada nueva definición.</span><span class="sxs-lookup"><span data-stu-id="9e15b-519">If hello index already exists, it is updated toohello new definition.</span></span>

<span data-ttu-id="9e15b-520">nombre del índice Hola debe estar en minúsculas, empezar por una letra o un número, no tener barras o puntos y tener menos de 128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9e15b-520">hello index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="9e15b-521">Después de iniciar el nombre del índice de hello con una letra o un número, rest Hola de nombre de hello puede incluir cualquier letra, número y guiones, como Hola guiones no sean consecutivos.</span><span class="sxs-lookup"><span data-stu-id="9e15b-521">After starting hello index name with a letter or number, hello rest of hello name can include any letter, number and dashes, as long as hello dashes are not consecutive.</span></span>

<span data-ttu-id="9e15b-522">`api-version=[string]` (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="9e15b-522">`api-version=[string]` (required).</span></span> <span data-ttu-id="9e15b-523">versión de vista previa de Hello es `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-523">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9e15b-524">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-524">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="9e15b-525">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-525">**Request Headers**</span></span>

<span data-ttu-id="9e15b-526">Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales.</span><span class="sxs-lookup"><span data-stu-id="9e15b-526">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="9e15b-527">`Content-Type`: obligatorio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-527">`Content-Type`: Required.</span></span> <span data-ttu-id="9e15b-528">Establezca esta propiedad demasiado`application/json`</span><span class="sxs-lookup"><span data-stu-id="9e15b-528">Set this too`application/json`</span></span>
* <span data-ttu-id="9e15b-529">`api-key`: obligatorio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-529">`api-key`: Required.</span></span> <span data-ttu-id="9e15b-530">Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-530">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9e15b-531">Es un valor de cadena, el servicio de tooyour único.</span><span class="sxs-lookup"><span data-stu-id="9e15b-531">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="9e15b-532">Hola **Actualizar índice** solicitud debe incluir un `api-key` encabezado establece clave de administrador de tooyour (como clave de consulta tooa lugar).</span><span class="sxs-lookup"><span data-stu-id="9e15b-532">hello **Update Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="9e15b-533">También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-533">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9e15b-534">Puede obtener el nombre del servicio de Hola y `api-key` desde el panel de servicio en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e15b-534">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9e15b-535">Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.</span><span class="sxs-lookup"><span data-stu-id="9e15b-535">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9e15b-536">**Sintaxis del cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-536">**Request Body Syntax**</span></span>

<span data-ttu-id="9e15b-537">Al actualizar un índice existente, el cuerpo de hello debe incluir la definición de esquema original de hello, además de nuevos campos de Hola que va a agregar, así como Hola modifica perfiles de puntuación, proveedores de sugerencias y las opciones de CORS, si existe.</span><span class="sxs-lookup"><span data-stu-id="9e15b-537">When updating an existing index, hello body must include hello original schema definition, plus hello new fields you are adding, as well as hello modified scoring profiles, suggesters and CORS options, if any.</span></span> <span data-ttu-id="9e15b-538">Si no va a modificar perfiles de puntuación de Hola y opciones de CORS, debe incluir los originales Hola de cuándo se creó el índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-538">If you are not modifying hello scoring profiles and CORS options, you must include hello originals from when hello index was created.</span></span> <span data-ttu-id="9e15b-539">Por lo general Hola mejor patrón toouse actualizaciones es definición del índice de hello tooretrieve con una operación GET, modificarlo, actualizarlo con PUT.</span><span class="sxs-lookup"><span data-stu-id="9e15b-539">In general hello best pattern toouse for updates is tooretrieve hello index definition with a GET, modify it, then update it with PUT.</span></span>

<span data-ttu-id="9e15b-540">sintaxis de esquema de Hello utilizan toocreate que un índice se reproduce aquí por comodidad.</span><span class="sxs-lookup"><span data-stu-id="9e15b-540">hello schema syntax used toocreate an index is reproduced here for convenience.</span></span> <span data-ttu-id="9e15b-541">Consulte [Crear índice](#CreateIndex) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="9e15b-541">See [Create Index](#CreateIndex) for more details.</span></span>

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
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
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
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
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


<span data-ttu-id="9e15b-542">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="9e15b-542">**Response**</span></span>

<span data-ttu-id="9e15b-543">Para obtener una solicitud correcta: "204 Sin contenido".</span><span class="sxs-lookup"><span data-stu-id="9e15b-543">For a successful request: "204 No Content".</span></span>

<span data-ttu-id="9e15b-544">De forma predeterminada el cuerpo de la respuesta de hello estará vacío.</span><span class="sxs-lookup"><span data-stu-id="9e15b-544">By default hello response body will be empty.</span></span> <span data-ttu-id="9e15b-545">Sin embargo, si hello `Prefer` encabezado de solicitud se establece demasiado`return=representation`, cuerpo de respuesta de hello contendrá hello JSON para la definición del índice Hola que se ha actualizado.</span><span class="sxs-lookup"><span data-stu-id="9e15b-545">However, if hello `Prefer` request header is set too`return=representation`, hello response body will contain hello JSON for hello index definition that was updated.</span></span> <span data-ttu-id="9e15b-546">En este caso, código de estado de hello correcto será "200 Aceptar".</span><span class="sxs-lookup"><span data-stu-id="9e15b-546">In this case, hello success status code will be "200 OK".</span></span>

<span data-ttu-id="9e15b-547">**Actualización de definiciones de índices con analizadores personalizados**</span><span class="sxs-lookup"><span data-stu-id="9e15b-547">**Updating index definition with custom analyzers**</span></span>

<span data-ttu-id="9e15b-548">Una vez definido un analizador, un tokenizador o un filtro de caracteres, no se puede modificar.</span><span class="sxs-lookup"><span data-stu-id="9e15b-548">Once an analyzer, a tokenizer, a token filter or a char filter is defined, it cannot be modified.</span></span> <span data-ttu-id="9e15b-549">Nuevos pueden agregarse índice existente tooan solo si hello `allowIndexDowntime` tootrue se establece una marca en la solicitud de actualización de índice de hello:</span><span class="sxs-lookup"><span data-stu-id="9e15b-549">New ones can be added tooan existing index only if hello `allowIndexDowntime` flag is set tootrue in hello index update request:</span></span> 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

<span data-ttu-id="9e15b-550">Tenga en cuenta que esta operación, se colocará el índice sin conexión al menos unos segundos, haciendo que la indización y consulta solicita toofail.</span><span class="sxs-lookup"><span data-stu-id="9e15b-550">Note that this operation will put your index offline for at least a few seconds, causing your indexing and query requests toofail.</span></span> <span data-ttu-id="9e15b-551">Disponibilidad de rendimiento y la escritura del índice de hello puede ser afectado durante varios minutos después de haber actualizado el índice de Hola o más índices muy grandes.</span><span class="sxs-lookup"><span data-stu-id="9e15b-551">Performance and write availability of hello index can be impaired for several minutes after hello index is updated, or longer for very large indexes.</span></span>

<a name="ListIndexes"></a>

## <a name="list-indexes"></a><span data-ttu-id="9e15b-552">Índices de la lista</span><span class="sxs-lookup"><span data-stu-id="9e15b-552">List Indexes</span></span>
<span data-ttu-id="9e15b-553">Hola **índices de la lista** operación devuelve una lista de índices de hello actualmente en el servicio de búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e15b-553">hello **List Indexes** operation returns a list of hello indexes currently in your Azure Search service.</span></span>

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="9e15b-554">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-554">**Request**</span></span>

<span data-ttu-id="9e15b-555">HTTPS es necesario para todas las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-555">HTTPS is required for all service requests.</span></span> <span data-ttu-id="9e15b-556">Hola **índices de la lista** solicitud puede crearse mediante el método GET de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-556">hello **List Indexes** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="9e15b-557">`api-version=[string]` (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="9e15b-557">`api-version=[string]` (required).</span></span> <span data-ttu-id="9e15b-558">versión de vista previa de Hello es `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-558">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9e15b-559">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-559">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="9e15b-560">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-560">**Request Headers**</span></span>

<span data-ttu-id="9e15b-561">Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales.</span><span class="sxs-lookup"><span data-stu-id="9e15b-561">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="9e15b-562">`api-key`: obligatorio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-562">`api-key`: Required.</span></span> <span data-ttu-id="9e15b-563">Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-563">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9e15b-564">Es un valor de cadena, el servicio de tooyour único.</span><span class="sxs-lookup"><span data-stu-id="9e15b-564">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="9e15b-565">Hola **índices de la lista** solicitud debe incluir un `api-key` conjunto tooan clave de administración (como clave de consulta tooa lugar).</span><span class="sxs-lookup"><span data-stu-id="9e15b-565">hello **List Indexes** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="9e15b-566">También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-566">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9e15b-567">Puede obtener el nombre del servicio de Hola y `api-key` desde el panel de servicio en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e15b-567">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9e15b-568">Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.</span><span class="sxs-lookup"><span data-stu-id="9e15b-568">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9e15b-569">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-569">**Request Body**</span></span>

<span data-ttu-id="9e15b-570">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="9e15b-570">None.</span></span>

<span data-ttu-id="9e15b-571">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="9e15b-571">**Response**</span></span>

<span data-ttu-id="9e15b-572">Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.</span><span class="sxs-lookup"><span data-stu-id="9e15b-572">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="9e15b-573">A continuación se proporciona un cuerpo de respuesta de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9e15b-573">Here is an example response body:</span></span>

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

<span data-ttu-id="9e15b-574">Tenga en cuenta que puede filtrar Hola respuesta hacia abajo de propiedades de hello toojust que le interesa.</span><span class="sxs-lookup"><span data-stu-id="9e15b-574">Note that you can filter hello response down toojust hello properties you're interested in.</span></span> <span data-ttu-id="9e15b-575">Por ejemplo, si desea que solo una lista de nombres de índice, use Hola OData `$select` opción de consulta:</span><span class="sxs-lookup"><span data-stu-id="9e15b-575">For example, if you want only a list of index names, use hello OData `$select` query option:</span></span>

    GET /indexes?api-version=2015-02-28-Preview&$select=name

<span data-ttu-id="9e15b-576">En este caso, respuesta Hola Hola ejemplo anterior podría aparecer como sigue:</span><span class="sxs-lookup"><span data-stu-id="9e15b-576">In this case, hello response from hello above example would appear as follows:</span></span>

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

<span data-ttu-id="9e15b-577">Se trata de un ancho de banda de toosave técnica útil si tiene una gran cantidad de índices en el servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-577">This is a useful technique toosave bandwidth if you have a lot of indexes in your Search service.</span></span>

<a name="GetIndex"></a>

## <a name="get-index"></a><span data-ttu-id="9e15b-578">Obtener índice</span><span class="sxs-lookup"><span data-stu-id="9e15b-578">Get Index</span></span>
<span data-ttu-id="9e15b-579">Hola **obtener índice** operación obtiene la definición del índice Hola de búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e15b-579">hello **Get Index** operation gets hello index definition from Azure Search.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="9e15b-580">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-580">**Request**</span></span>

<span data-ttu-id="9e15b-581">HTTPS es necesario para las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-581">HTTPS is required for service requests.</span></span> <span data-ttu-id="9e15b-582">Hola **obtener índice** solicitud puede crearse mediante el método GET de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-582">hello **Get Index** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="9e15b-583">Hola [nombre del índice] Hola URI de la solicitud especifica qué tooreturn de índice de la colección de índices de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-583">hello [index name] in hello request URI specifies which index tooreturn from hello indexes collection.</span></span>

<span data-ttu-id="9e15b-584">`api-version=[string]` (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="9e15b-584">`api-version=[string]` (required).</span></span> <span data-ttu-id="9e15b-585">versión de vista previa de Hello es `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-585">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9e15b-586">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-586">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="9e15b-587">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-587">**Request Headers**</span></span>

<span data-ttu-id="9e15b-588">Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales.</span><span class="sxs-lookup"><span data-stu-id="9e15b-588">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="9e15b-589">`api-key`: Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-589">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9e15b-590">Es un valor de cadena, el servicio de tooyour único.</span><span class="sxs-lookup"><span data-stu-id="9e15b-590">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="9e15b-591">Hola **obtener índice** solicitud debe incluir un `api-key` conjunto tooan clave de administración (como clave de consulta tooa lugar).</span><span class="sxs-lookup"><span data-stu-id="9e15b-591">hello **Get Index** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="9e15b-592">También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-592">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9e15b-593">Puede obtener el nombre del servicio de Hola y `api-key` desde el panel de servicio en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e15b-593">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9e15b-594">Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.</span><span class="sxs-lookup"><span data-stu-id="9e15b-594">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9e15b-595">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-595">**Request Body**</span></span>

<span data-ttu-id="9e15b-596">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="9e15b-596">None.</span></span>

<span data-ttu-id="9e15b-597">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="9e15b-597">**Response**</span></span>

<span data-ttu-id="9e15b-598">Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.</span><span class="sxs-lookup"><span data-stu-id="9e15b-598">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="9e15b-599">Vea el ejemplo de Hola JSON en [creación y actualización de un índice](#CreateUpdateIndexExample) para obtener un ejemplo de carga de respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-599">See hello example JSON in [Creating and Updating an Index](#CreateUpdateIndexExample) for an example of hello response payload.</span></span>

<a name="DeleteIndex"></a>

## <a name="delete-index"></a><span data-ttu-id="9e15b-600">Eliminar índice</span><span class="sxs-lookup"><span data-stu-id="9e15b-600">Delete Index</span></span>
<span data-ttu-id="9e15b-601">Hola **Eliminar índice** operación quita un índice y los documentos asociados desde el servicio de búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e15b-601">hello **Delete Index** operation removes an index and associated documents from your Azure Search service.</span></span> <span data-ttu-id="9e15b-602">Puede obtener el nombre del índice de Hola desde el panel de servicio de hello en hello portal de Azure o desde Hola API.</span><span class="sxs-lookup"><span data-stu-id="9e15b-602">You can get hello index name from hello service dashboard in hello Azure portal, or from hello API.</span></span> <span data-ttu-id="9e15b-603">Consulte [Índices de la lista](#ListIndexes) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="9e15b-603">See [List Indexes](#ListIndexes) for details.</span></span>

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="9e15b-604">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-604">**Request**</span></span>

<span data-ttu-id="9e15b-605">HTTPS es necesario para las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-605">HTTPS is required for service requests.</span></span> <span data-ttu-id="9e15b-606">Hola **Eliminar índice** solicitud puede crearse mediante el método de eliminación de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-606">hello **Delete Index** request can be constructed using hello DELETE method.</span></span>

<span data-ttu-id="9e15b-607">Hola [nombre del índice] Hola URI de la solicitud especifica qué toodelete de índice de la colección de índices de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-607">hello [index name] in hello request URI specifies which index toodelete from hello indexes collection.</span></span>

<span data-ttu-id="9e15b-608">`api-version=[string]` (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="9e15b-608">`api-version=[string]` (required).</span></span> <span data-ttu-id="9e15b-609">versión de vista previa de Hello es `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-609">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9e15b-610">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-610">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="9e15b-611">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-611">**Request Headers**</span></span>

<span data-ttu-id="9e15b-612">Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales.</span><span class="sxs-lookup"><span data-stu-id="9e15b-612">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="9e15b-613">`api-key`: obligatorio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-613">`api-key`: Required.</span></span> <span data-ttu-id="9e15b-614">Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-614">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9e15b-615">Es un valor de cadena único tooyour dirección URL del servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-615">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="9e15b-616">Hola **Eliminar índice** solicitud debe incluir un `api-key` encabezado establece clave de administrador de tooyour (como clave de consulta tooa lugar).</span><span class="sxs-lookup"><span data-stu-id="9e15b-616">hello **Delete Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="9e15b-617">También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-617">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9e15b-618">Puede obtener el nombre del servicio de Hola y `api-key` desde el panel de servicio en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e15b-618">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9e15b-619">Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.</span><span class="sxs-lookup"><span data-stu-id="9e15b-619">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9e15b-620">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-620">**Request Body**</span></span>

<span data-ttu-id="9e15b-621">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="9e15b-621">None.</span></span>

<span data-ttu-id="9e15b-622">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="9e15b-622">**Response**</span></span>

<span data-ttu-id="9e15b-623">Código de estado: al obtener una respuesta correcta, se visualiza 204 Sin contenido.</span><span class="sxs-lookup"><span data-stu-id="9e15b-623">Status Code: 204 No Content is returned for a successful response.</span></span>

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a><span data-ttu-id="9e15b-624">Obtención de estadísticas de índice</span><span class="sxs-lookup"><span data-stu-id="9e15b-624">Get Index Statistics</span></span>
<span data-ttu-id="9e15b-625">Hola **obtener estadísticas de índice** operación devuelve de búsqueda de Azure, un número de documento para el índice actual de hello, además de uso de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9e15b-625">hello **Get Index Statistics** operation returns from Azure Search a document count for hello current index, plus storage usage.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> <span data-ttu-id="9e15b-626">Se recopilan estadísticas del tamaño de almacenamiento y el número de documento cada pocos minutos; es decir, no se hace en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="9e15b-626">Statistics on document count and storage size are collected every few minutes, not in real time.</span></span> <span data-ttu-id="9e15b-627">Por lo tanto, las estadísticas de hello devueltas por esta API pueden no reflejar cambios causado por operaciones de indización recientes.</span><span class="sxs-lookup"><span data-stu-id="9e15b-627">Therefore, hello statistics returned by this API may not reflect changes caused by recent indexing operations.</span></span>
> 
> 

<span data-ttu-id="9e15b-628">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-628">**Request**</span></span>

<span data-ttu-id="9e15b-629">HTTPS es necesario para todas las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-629">HTTPS is required for all services requests.</span></span> <span data-ttu-id="9e15b-630">Hola **obtener estadísticas de índice** solicitud puede crearse mediante el método GET de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-630">hello **Get Index Statistics** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="9e15b-631">Hola [nombre del índice] en el URI de solicitud de hello indica estadísticas de índice tooreturn Hola de servicio para el índice especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-631">hello [index name] in hello request URI tells hello service tooreturn index statistics for hello specified index.</span></span>

<span data-ttu-id="9e15b-632">`api-version=[string]` (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="9e15b-632">`api-version=[string]` (required).</span></span> <span data-ttu-id="9e15b-633">versión de vista previa de Hello es `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-633">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9e15b-634">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-634">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="9e15b-635">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-635">**Request Headers**</span></span>

<span data-ttu-id="9e15b-636">Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales.</span><span class="sxs-lookup"><span data-stu-id="9e15b-636">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="9e15b-637">`api-key`: Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-637">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9e15b-638">Es un valor de cadena, el servicio de tooyour único.</span><span class="sxs-lookup"><span data-stu-id="9e15b-638">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="9e15b-639">Hola **obtener estadísticas de índice** solicitud debe incluir un `api-key` conjunto tooan clave de administración (como clave de consulta tooa lugar).</span><span class="sxs-lookup"><span data-stu-id="9e15b-639">hello **Get Index Statistics** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="9e15b-640">También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-640">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9e15b-641">Puede obtener el nombre del servicio de Hola y `api-key` desde el panel de servicio en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e15b-641">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9e15b-642">Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.</span><span class="sxs-lookup"><span data-stu-id="9e15b-642">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9e15b-643">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-643">**Request Body**</span></span>

<span data-ttu-id="9e15b-644">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="9e15b-644">None.</span></span>

<span data-ttu-id="9e15b-645">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="9e15b-645">**Response**</span></span>

<span data-ttu-id="9e15b-646">Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.</span><span class="sxs-lookup"><span data-stu-id="9e15b-646">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="9e15b-647">cuerpo de respuesta de Hello es Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="9e15b-647">hello response body is in hello following format:</span></span>

    {
      "documentCount": number,
      "storageSize": number (size of hello index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a><span data-ttu-id="9e15b-648">Analizador de prueba</span><span class="sxs-lookup"><span data-stu-id="9e15b-648">Test Analyzer</span></span>
<span data-ttu-id="9e15b-649">Hola **API analizar** muestra cómo un analizador divide el texto en tokens.</span><span class="sxs-lookup"><span data-stu-id="9e15b-649">hello **Analyze API** shows how an analyzer breaks text into tokens.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="9e15b-650">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-650">**Request**</span></span>

<span data-ttu-id="9e15b-651">HTTPS es necesario para todas las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-651">HTTPS is required for all services requests.</span></span> <span data-ttu-id="9e15b-652">Hola **API analizar** solicitud puede crearse mediante el método POST de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-652">hello **Analyze API** request can be constructed using hello POST method.</span></span>

<span data-ttu-id="9e15b-653">`api-version=[string]` (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="9e15b-653">`api-version=[string]` (required).</span></span> <span data-ttu-id="9e15b-654">versión de vista previa de Hello es `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-654">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9e15b-655">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-655">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="9e15b-656">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-656">**Request Headers**</span></span>

<span data-ttu-id="9e15b-657">Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales.</span><span class="sxs-lookup"><span data-stu-id="9e15b-657">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="9e15b-658">`api-key`: Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-658">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9e15b-659">Es un valor de cadena, el servicio de tooyour único.</span><span class="sxs-lookup"><span data-stu-id="9e15b-659">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="9e15b-660">Hola **API analizar** solicitud debe incluir un `api-key` conjunto tooan clave de administración (como clave de consulta tooa lugar).</span><span class="sxs-lookup"><span data-stu-id="9e15b-660">hello **Analyze API** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="9e15b-661">También necesitará el nombre del índice de Hola y Hola nombre tooconstruct Hola solicitud dirección URL del servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-661">You will also need hello index name and hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9e15b-662">Puede obtener el nombre del servicio de Hola y `api-key` desde el panel de servicio en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e15b-662">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9e15b-663">Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.</span><span class="sxs-lookup"><span data-stu-id="9e15b-663">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9e15b-664">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-664">**Request Body**</span></span>

    {
      "text": "Text tooanalyze",
      "analyzer": "analyzer_name"
    }

<span data-ttu-id="9e15b-665">o</span><span class="sxs-lookup"><span data-stu-id="9e15b-665">or</span></span>

    {
      "text": "Text tooanalyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

<span data-ttu-id="9e15b-666">Hola `analyzer_name`, `tokenizer_name`, `token_filter_name` y `char_filter_name` necesita toobe nombres válidos de analizadores predefinidos o personalizados, Tokenizer, token filtros y filtros de char para índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-666">hello `analyzer_name`, `tokenizer_name`, `token_filter_name` and `char_filter_name` need toobe valid names of predefined or custom analyzers, tokenizers, token filters and char filters for hello index.</span></span> <span data-ttu-id="9e15b-667">toolearn más información sobre el proceso de Hola de análisis léxico vea [análisis en búsqueda de Azure](https://aka.ms/azsanalysis).</span><span class="sxs-lookup"><span data-stu-id="9e15b-667">toolearn more about hello process of lexical analysis see [Analysis in Azure Search](https://aka.ms/azsanalysis).</span></span>

<span data-ttu-id="9e15b-668">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="9e15b-668">**Response**</span></span>

<span data-ttu-id="9e15b-669">Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.</span><span class="sxs-lookup"><span data-stu-id="9e15b-669">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="9e15b-670">cuerpo de respuesta de Hello es Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="9e15b-670">hello response body is in hello following format:</span></span>

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of hello first character of hello token),
          "endOffset": number (index of hello last character of hello token),
          "position": number (position of hello token in hello input text)
        },
        ...
      ]
    }

<span data-ttu-id="9e15b-671">**Ejemplo de la API de análisis**</span><span class="sxs-lookup"><span data-stu-id="9e15b-671">**Analyze API example**</span></span>

<span data-ttu-id="9e15b-672">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-672">**Request**</span></span>

    {
      "text": "Text tooanalyze",
      "analyzer": "standard"
    }

<span data-ttu-id="9e15b-673">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="9e15b-673">**Response**</span></span>

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

## <a name="document-operations"></a><span data-ttu-id="9e15b-674">Operaciones del documento</span><span class="sxs-lookup"><span data-stu-id="9e15b-674">Document Operations</span></span>
<span data-ttu-id="9e15b-675">En búsqueda de Azure, un índice se almacena en la nube de Hola y rellena con los documentos JSON que cargar toohello servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-675">In Azure Search, an index is stored in hello cloud and populated using JSON documents that you upload toohello service.</span></span> <span data-ttu-id="9e15b-676">Todos los documentos de Hola que se cargan comprenden corpus de Hola de los datos de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-676">All hello documents that you upload comprise hello corpus of your search data.</span></span> <span data-ttu-id="9e15b-677">Los documentos contienen campos, algunos de los cuales se acortan en términos de búsqueda cuando se cargan.</span><span class="sxs-lookup"><span data-stu-id="9e15b-677">Documents contain fields, some of which are tokenized into search terms as they are uploaded.</span></span> <span data-ttu-id="9e15b-678">Hola `/docs` segmento de dirección URL en hello API de búsqueda de Azure representa la colección de Hola de documentos en un índice.</span><span class="sxs-lookup"><span data-stu-id="9e15b-678">hello `/docs` URL segment in hello Azure Search API represents hello collection of documents in an index.</span></span> <span data-ttu-id="9e15b-679">Todas las operaciones realizadas en la colección de hello como cargar, combinar, eliminar o consultar documentos que tienen lugar en el contexto de Hola de un índice único, por lo que las direcciones de URL de Hola para estas operaciones siempre empezarán por `/indexes/[index name]/docs` para un nombre de índice especificado.</span><span class="sxs-lookup"><span data-stu-id="9e15b-679">All operations performed on hello collection such as uploading, merging, deleting, or querying documents take place in hello context of a single index, so hello URLs for these operations will always start with `/indexes/[index name]/docs` for a given index name.</span></span>

<span data-ttu-id="9e15b-680">El código de aplicación debe generar JSON documentos tooupload tooAzure búsqueda o puede usar un [indizador](https://msdn.microsoft.com/library/dn946891.aspx) tooload documentos si el origen de datos de hello es la base de datos de SQL Azure o base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="9e15b-680">Your application code must either generate JSON documents tooupload tooAzure Search or you can use an [indexer](https://msdn.microsoft.com/library/dn946891.aspx) tooload documents if hello data source is either Azure SQL Database or Azure Cosmos DB.</span></span> <span data-ttu-id="9e15b-681">Normalmente, los índices se rellenan desde un único conjunto de datos que suministre.</span><span class="sxs-lookup"><span data-stu-id="9e15b-681">Typically, indexes are populated from a single dataset that you provide.</span></span>

<span data-ttu-id="9e15b-682">Debe contar con un documento para cada elemento que desee toosearch.</span><span class="sxs-lookup"><span data-stu-id="9e15b-682">You should plan on having one document for each item that you want toosearch.</span></span> <span data-ttu-id="9e15b-683">Una aplicación de alquiler de películas puede disponer de un documento por película, una aplicación de escaparate podría tener un documento por SKU, una aplicación de software con fines pedagógicos en línea podría tener un documento por curso, una empresa de investigación podría tener un documento para cada documento académico de su repositorio, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="9e15b-683">A movie rental application might have one document per movie, a storefront application might have one document per SKU, an online courseware application might have one document per course, a research firm might have one document for each academic paper in their repository, and so on.</span></span>

<span data-ttu-id="9e15b-684">Los documentos constan de uno o varios campos.</span><span class="sxs-lookup"><span data-stu-id="9e15b-684">Documents consist of one or more fields.</span></span> <span data-ttu-id="9e15b-685">Los campos pueden contener texto acortado por Búsqueda de Azure a términos de búsqueda, así como los valores no acortados o que no sean de texto que pueden utilizarse en filtros o perfiles de puntuación.</span><span class="sxs-lookup"><span data-stu-id="9e15b-685">Fields can contain text that is tokenized by Azure Search into search terms, as well as non-tokenized or non-text values that can be used in filters or scoring profiles.</span></span> <span data-ttu-id="9e15b-686">Hello nombres, tipos de datos y características de búsqueda admitidas para cada campo se determinan por el esquema de índice Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-686">hello names, data types, and search features supported for each field are determined by hello index schema.</span></span> <span data-ttu-id="9e15b-687">Uno de los campos de hello en cada esquema de índice debe designarse como identificador, y cada documento debe tener un valor para el campo de Id. de Hola que identifica ese documento en el índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-687">One of hello fields in each index schema must be designated as an ID, and each document must have a value for hello ID field that uniquely identifies that document in hello index.</span></span> <span data-ttu-id="9e15b-688">Todos los demás campos de documento son opcionales y serán tooa de valor null si no se especifican.</span><span class="sxs-lookup"><span data-stu-id="9e15b-688">All other document fields are optional and will default tooa null value if left unspecified.</span></span> <span data-ttu-id="9e15b-689">Tenga en cuenta que los valores null no ocupan espacio en el índice de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-689">Note that null values do not take up space in hello search index.</span></span>

<span data-ttu-id="9e15b-690">Antes de poder cargar documentos, debe ya ha creado el índice de hello en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-690">Before you can upload documents, you must have already created hello index on hello service.</span></span> <span data-ttu-id="9e15b-691">Consulte [Crear índice](#CreateIndex) para obtener más información acerca de este primer paso.</span><span class="sxs-lookup"><span data-stu-id="9e15b-691">See [Create Index](#CreateIndex) for details about this first step.</span></span>

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a><span data-ttu-id="9e15b-692">Agregar, actualizar o eliminar documentos</span><span class="sxs-lookup"><span data-stu-id="9e15b-692">Add, Update, or Delete Documents</span></span>
<span data-ttu-id="9e15b-693">Puede cargar, combinar, combinar o cargar o eliminar documentos en un índice especificado mediante HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="9e15b-693">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span> <span data-ttu-id="9e15b-694">Para un gran número de actualizaciones, se recomienda el procesamiento por lotes de documentos (too1000 documentos por lote) o aproximadamente 16 MB por lote.</span><span class="sxs-lookup"><span data-stu-id="9e15b-694">For large numbers of updates, batching of documents (up too1000 documents per batch or about 16 MB per batch) is recommended.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="9e15b-695">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-695">**Request**</span></span>

<span data-ttu-id="9e15b-696">HTTPS es necesario para todas las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-696">HTTPS is required for all service requests.</span></span> <span data-ttu-id="9e15b-697">Puede cargar, combinar, combinar o cargar o eliminar documentos en un índice especificado mediante HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="9e15b-697">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span>

<span data-ttu-id="9e15b-698">Hola URI de solicitud incluye [nombre del índice], especificar qué documentos de toopost de índice.</span><span class="sxs-lookup"><span data-stu-id="9e15b-698">hello request URI includes [index name], specifying which index toopost documents.</span></span> <span data-ttu-id="9e15b-699">Índice de tooone documentos sólo se puede registrar a la vez.</span><span class="sxs-lookup"><span data-stu-id="9e15b-699">You can only post documents tooone index at a time.</span></span>

<span data-ttu-id="9e15b-700">`api-version=[string]` (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="9e15b-700">`api-version=[string]` (required).</span></span> <span data-ttu-id="9e15b-701">versión de vista previa de Hello es `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-701">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9e15b-702">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-702">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="9e15b-703">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-703">**Request Headers**</span></span>

<span data-ttu-id="9e15b-704">Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales.</span><span class="sxs-lookup"><span data-stu-id="9e15b-704">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="9e15b-705">`Content-Type`: obligatorio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-705">`Content-Type`: Required.</span></span> <span data-ttu-id="9e15b-706">Establezca esta propiedad demasiado`application/json`</span><span class="sxs-lookup"><span data-stu-id="9e15b-706">Set this too`application/json`</span></span>
* <span data-ttu-id="9e15b-707">`api-key`: obligatorio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-707">`api-key`: Required.</span></span> <span data-ttu-id="9e15b-708">Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-708">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9e15b-709">Es un valor de cadena, el servicio de tooyour único.</span><span class="sxs-lookup"><span data-stu-id="9e15b-709">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="9e15b-710">Hola **agregar documentos** solicitud debe incluir un `api-key` encabezado establece clave de administrador de tooyour (como clave de consulta tooa lugar).</span><span class="sxs-lookup"><span data-stu-id="9e15b-710">hello **Add Documents** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="9e15b-711">También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-711">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9e15b-712">Puede obtener el nombre del servicio de Hola y `api-key` desde el panel de servicio en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e15b-712">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9e15b-713">Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.</span><span class="sxs-lookup"><span data-stu-id="9e15b-713">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9e15b-714">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-714">**Request Body**</span></span>

<span data-ttu-id="9e15b-715">cuerpo de saludo de solicitud de hello contiene uno o más toobe documentos indizados.</span><span class="sxs-lookup"><span data-stu-id="9e15b-715">hello body of hello request contains one or more documents toobe indexed.</span></span> <span data-ttu-id="9e15b-716">Los documentos se identifican mediante una clave única.</span><span class="sxs-lookup"><span data-stu-id="9e15b-716">Documents are identified by a unique key.</span></span> <span data-ttu-id="9e15b-717">Cada documento está asociado a una acción: carga, combinación, combinación o carga o eliminación.</span><span class="sxs-lookup"><span data-stu-id="9e15b-717">Each document is associated with an action: upload, merge, mergeOrUpload or delete.</span></span> <span data-ttu-id="9e15b-718">Carga las solicitudes deben incluir los datos del documento Hola como un conjunto de pares clave/valor.</span><span class="sxs-lookup"><span data-stu-id="9e15b-718">Upload requests must include hello document data as a set of key/value pairs.</span></span>

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
> <span data-ttu-id="9e15b-719">Las claves de documento solo pueden contener letras, números, guiones ("-"), caracteres de subrayado ("_") y signos igual ("=").</span><span class="sxs-lookup"><span data-stu-id="9e15b-719">Document keys can only contain letters, numbers, dashes ("-"), underscores ("_"), and equal signs ("=").</span></span> <span data-ttu-id="9e15b-720">Para obtener más información, consulte [Reglas de nomenclatura](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e15b-720">For more details, see [Naming rules](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span></span>
> 
> 

<span data-ttu-id="9e15b-721">**Acciones de documentos**</span><span class="sxs-lookup"><span data-stu-id="9e15b-721">**Document Actions**</span></span>

* <span data-ttu-id="9e15b-722">`upload`: Una acción de carga es similar tooan "upsert" donde se insertan si es nuevo y actualiza/reemplaza si existe el documento de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-722">`upload`: An upload action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> <span data-ttu-id="9e15b-723">Tenga en cuenta que todos los campos se reemplazan en caso de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-723">Note that all fields are replaced in hello update case.</span></span>
* <span data-ttu-id="9e15b-724">`merge`: Merge actualiza una existente de documentos con hello especifica campos.</span><span class="sxs-lookup"><span data-stu-id="9e15b-724">`merge`: Merge updates an existing document with hello specified fields.</span></span> <span data-ttu-id="9e15b-725">Si no existe el documento de hello, se producirá un error en la combinación de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-725">If hello document doesn't exist, hello merge will fail.</span></span> <span data-ttu-id="9e15b-726">Cualquier campo que se especifica en una combinación reemplazará el campo existente de hello en el documento de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-726">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="9e15b-727">Aquí se incluyen los campos de tipo `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-727">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="9e15b-728">Por ejemplo, si hello documento contiene un campo "tags" con el valor `["budget"]` y ejecutar una combinación con el valor `["economy", "pool"]` para "etiquetas", valor final de Hola de campo Hola "tags" será `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-728">For example, if hello document contains a field "tags" with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for "tags", hello final value of hello "tags" field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="9e15b-729">**No** será `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-729">It will **not** be `["budget", "economy", "pool"]`.</span></span>
* <span data-ttu-id="9e15b-730">`mergeOrUpload`: se comporta como `merge` si un documento con hello clave dada ya existe en el índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-730">`mergeOrUpload`: behaves like `merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="9e15b-731">Si el documento de hello no existe, ésta se comporta como `upload` con un nuevo documento.</span><span class="sxs-lookup"><span data-stu-id="9e15b-731">If hello document does not exist it behaves like `upload` with a new document.</span></span>
* <span data-ttu-id="9e15b-732">`delete`: La eliminación quita documento especificado Hola Hola índice.</span><span class="sxs-lookup"><span data-stu-id="9e15b-732">`delete`: Delete removes hello specified document from hello index.</span></span> <span data-ttu-id="9e15b-733">Tenga en cuenta que los campos especifique en una `delete` operación distinta de campo de clave de Hola se pasará por alto.</span><span class="sxs-lookup"><span data-stu-id="9e15b-733">Note that any fields you specify in a `delete` operation other than hello key field will be ignored.</span></span> <span data-ttu-id="9e15b-734">Si desea tooremove un campo individual de un documento, use `merge` en su lugar y simplemente defina el campo de hello explícitamente demasiado`null`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-734">If you want tooremove an individual field from a document, use `merge` instead and simply set hello field explicitly too`null`.</span></span>

<span data-ttu-id="9e15b-735">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="9e15b-735">**Response**</span></span>

<span data-ttu-id="9e15b-736">Código de estado: se obtendrá 200 Correcto con una respuesta correcta, lo que significa que todos los elementos se han indexado correctamente.</span><span class="sxs-lookup"><span data-stu-id="9e15b-736">Status code 200 (OK) is returned for a successful response, meaning that all items have been successfully indexed.</span></span> <span data-ttu-id="9e15b-737">Esto se indica mediante hello `status` propiedad se ha establecido tootrue para todos los elementos, así como hello `statusCode` propiedad se ha establecido tooeither 201 (para los documentos recién cargados) o 200 (para los documentos combinados o eliminados):</span><span class="sxs-lookup"><span data-stu-id="9e15b-737">This is indicated by hello `status` property being set tootrue for all items, as well as hello `statusCode` property being set tooeither 201 (for newly uploaded documents) or 200 (for merged or deleted documents):</span></span>

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

<span data-ttu-id="9e15b-738">Se devolverá un código de estado 207 (varios estados) solo con que un elemento no se indexe correctamente.</span><span class="sxs-lookup"><span data-stu-id="9e15b-738">Status code 207 (Multi-Status) is returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="9e15b-739">Elementos que no se han indizado tienen hello `status` toofalse de conjunto de campos.</span><span class="sxs-lookup"><span data-stu-id="9e15b-739">Items that have not been indexed have hello `status` field set toofalse.</span></span> <span data-ttu-id="9e15b-740">Hola `errorMessage` y `statusCode` propiedades indicará el motivo Hola Hola indización de error:</span><span class="sxs-lookup"><span data-stu-id="9e15b-740">hello `errorMessage` and `statusCode` properties will indicate hello reason for hello indexing error:</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "hello search service is too busy tooprocess this document. Please try again later.",
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
          "errorMessage": "Index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

<span data-ttu-id="9e15b-741">Hello en la tabla siguiente explica Hola distintos cada documento códigos de estado que se pueden devolver en la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-741">hello following table explains hello various per-document status codes that can be returned in hello response.</span></span> <span data-ttu-id="9e15b-742">Tenga en cuenta que algunos indican problemas con la solicitud de hello, mientras que otros usuarios indican condiciones de error temporal.</span><span class="sxs-lookup"><span data-stu-id="9e15b-742">Note that some indicate problems with hello request itself, while others indicate temporary error conditions.</span></span> <span data-ttu-id="9e15b-743">Hola este último que debe reintentar después de un retraso.</span><span class="sxs-lookup"><span data-stu-id="9e15b-743">hello latter you should retry after a delay.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="9e15b-744">Código de estado</span><span class="sxs-lookup"><span data-stu-id="9e15b-744">Status code</span></span></th>
        <th><span data-ttu-id="9e15b-745">Significado</span><span class="sxs-lookup"><span data-stu-id="9e15b-745">Meaning</span></span></th>
        <th><span data-ttu-id="9e15b-746">Se puede volver a intentar</span><span class="sxs-lookup"><span data-stu-id="9e15b-746">Retryable</span></span></th>
        <th><span data-ttu-id="9e15b-747">Notas</span><span class="sxs-lookup"><span data-stu-id="9e15b-747">Notes</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-748">200</span><span class="sxs-lookup"><span data-stu-id="9e15b-748">200</span></span></td>
        <td><span data-ttu-id="9e15b-749">Documento correctamente modificado o eliminado.</span><span class="sxs-lookup"><span data-stu-id="9e15b-749">Document was successfully modified or deleted.</span></span></td>
        <td><span data-ttu-id="9e15b-750">N/D</span><span class="sxs-lookup"><span data-stu-id="9e15b-750">n/a</span></span></td>
        <td><span data-ttu-id="9e15b-751">Las operaciones de eliminación son <a href="https://en.wikipedia.org/wiki/Idempotence">idempotentes</a>.</span><span class="sxs-lookup"><span data-stu-id="9e15b-751">Delete operations are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span> <span data-ttu-id="9e15b-752">Es decir, incluso si una clave de documento no existe en el índice de hello, intentar una operación de eliminación con esa clave se producirá en un código de 200 estado.</span><span class="sxs-lookup"><span data-stu-id="9e15b-752">That is, even if a document key does not exist in hello index, attempting a delete operation with that key will result in a 200 status code.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-753">201</span><span class="sxs-lookup"><span data-stu-id="9e15b-753">201</span></span></td>
        <td><span data-ttu-id="9e15b-754">El documento se creó correctamente.</span><span class="sxs-lookup"><span data-stu-id="9e15b-754">Document was successfully created.</span></span></td>
        <td><span data-ttu-id="9e15b-755">N/D</span><span class="sxs-lookup"><span data-stu-id="9e15b-755">n/a</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-756">400</span><span class="sxs-lookup"><span data-stu-id="9e15b-756">400</span></span></td>
        <td><span data-ttu-id="9e15b-757">Se produjo un error en el documento de Hola que impidió que se está indizando.</span><span class="sxs-lookup"><span data-stu-id="9e15b-757">There was an error in hello document that prevented it from being indexed.</span></span></td>
        <td><span data-ttu-id="9e15b-758">No</span><span class="sxs-lookup"><span data-stu-id="9e15b-758">No</span></span></td>
        <td><span data-ttu-id="9e15b-759">mensaje de error de Hola en respuesta Hola indicará cuál es el problema con el documento de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-759">hello error message in hello response will indicate what is wrong with hello document.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-760">404</span><span class="sxs-lookup"><span data-stu-id="9e15b-760">404</span></span></td>
        <td><span data-ttu-id="9e15b-761">no se pudieron combinar documento Hola porque Hola clave dada no existe en el índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-761">hello document could not be merged because hello given key doesn't exist in hello index.</span></span></td>
        <td><span data-ttu-id="9e15b-762">No</span><span class="sxs-lookup"><span data-stu-id="9e15b-762">No</span></span></td>
        <td><span data-ttu-id="9e15b-763">Este error no se produce durante las cargas ya que estas crean nuevos documentos y no se producen durante las eliminaciones porque son <a href="https://en.wikipedia.org/wiki/Idempotence">idempotentes</a>.</span><span class="sxs-lookup"><span data-stu-id="9e15b-763">This error does not occur for uploads since they create new documents, and it does not occur for deletes because they are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-764">409</span><span class="sxs-lookup"><span data-stu-id="9e15b-764">409</span></span></td>
        <td><span data-ttu-id="9e15b-765">Se detectó un conflicto de versión al tratar de tooindex un documento.</span><span class="sxs-lookup"><span data-stu-id="9e15b-765">A version conflict was detected when attempting tooindex a document.</span></span></td>
        <td><span data-ttu-id="9e15b-766">Sí</span><span class="sxs-lookup"><span data-stu-id="9e15b-766">Yes</span></span></td>
        <td><span data-ttu-id="9e15b-767">Esto puede ocurrir al que está tratando de hello tooindex mismo documento más de una vez al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="9e15b-767">This can happen when you're trying tooindex hello same document more than once concurrently.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-768">422</span><span class="sxs-lookup"><span data-stu-id="9e15b-768">422</span></span></td>
        <td><span data-ttu-id="9e15b-769">índice de Hello no está disponible temporalmente porque se actualizó con allowIndexDowntime' hello' marca conjunto too'true'.</span><span class="sxs-lookup"><span data-stu-id="9e15b-769">hello index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'.</span></span></td>
        <td><span data-ttu-id="9e15b-770">Sí</span><span class="sxs-lookup"><span data-stu-id="9e15b-770">Yes</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9e15b-771">503</span><span class="sxs-lookup"><span data-stu-id="9e15b-771">503</span></span></td>
        <td><span data-ttu-id="9e15b-772">El servicio de búsqueda no está disponible temporalmente, posiblemente debido a carga tooheavy.</span><span class="sxs-lookup"><span data-stu-id="9e15b-772">Your search service is temporarily unavailable, possibly due tooheavy load.</span></span></td>
        <td><span data-ttu-id="9e15b-773">Sí</span><span class="sxs-lookup"><span data-stu-id="9e15b-773">Yes</span></span></td>
        <td><span data-ttu-id="9e15b-774">El código debe esperar antes de reintentar en este caso, o se arriesga a prolongar la no disponibilidad del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-774">Your code should wait before retrying in this case or you risk prolonging hello service unavailability.</span></span></td>
    </tr>
</table> 

<span data-ttu-id="9e15b-775">**Tenga en cuenta**: si el código de cliente encuentra con frecuencia una respuesta 207, una razón posible es que sistema Hola está bajo carga.</span><span class="sxs-lookup"><span data-stu-id="9e15b-775">**Note**: If your client code frequently encounters a 207 response, one possible reason is that hello system is under load.</span></span> <span data-ttu-id="9e15b-776">Puede confirmarlo comprobando hello `statusCode` propiedad 503.</span><span class="sxs-lookup"><span data-stu-id="9e15b-776">You can confirm this by checking hello `statusCode` property for 503.</span></span> <span data-ttu-id="9e15b-777">Si éste es el caso de hello, se recomienda ***la limitación de peticiones de indización***.</span><span class="sxs-lookup"><span data-stu-id="9e15b-777">If this is hello case, we recommend ***throttling indexing requests***.</span></span> <span data-ttu-id="9e15b-778">En caso contrario, si el tráfico de indización no remite, el sistema de hello podría empezar a rechazar todas las solicitudes con 503 errores.</span><span class="sxs-lookup"><span data-stu-id="9e15b-778">Otherwise, if indexing traffic doesn't subside, hello system could start rejecting all requests with 503 errors.</span></span>

<span data-ttu-id="9e15b-779">Código de estado 429 indica que se ha superado la cuota Hola número de documentos por índice.</span><span class="sxs-lookup"><span data-stu-id="9e15b-779">Status code 429 indicates that you have exceeded your quota on hello number of documents per index.</span></span> <span data-ttu-id="9e15b-780">Debe crear un nuevo índice o actualizar para obtener límites de capacidad superiores.</span><span class="sxs-lookup"><span data-stu-id="9e15b-780">You must either create a new index or upgrade for higher capacity limits.</span></span>

<span data-ttu-id="9e15b-781">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="9e15b-781">**Example:**</span></span>

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

## <a name="search-documents"></a><span data-ttu-id="9e15b-782">Buscar documentos</span><span class="sxs-lookup"><span data-stu-id="9e15b-782">Search Documents</span></span>
<span data-ttu-id="9e15b-783">A **búsqueda** operación se emite como una solicitud GET o POST y especifica los parámetros que proporcionen a los criterios de Hola para seleccionar documentos asociados.</span><span class="sxs-lookup"><span data-stu-id="9e15b-783">A **Search** operation is issued as a GET or POST request and specifies parameters that give hello criteria for selecting matching documents.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="9e15b-784">**Cuando este tipo de toouse en lugar de obtener**</span><span class="sxs-lookup"><span data-stu-id="9e15b-784">**When toouse POST instead of GET**</span></span>

<span data-ttu-id="9e15b-785">Cuando se utiliza HTTP GET toocall hello **búsqueda** API, deberá toobe tenga en cuenta que longitud Hola de dirección URL de solicitud de hello no puede superar los 8 KB.</span><span class="sxs-lookup"><span data-stu-id="9e15b-785">When you use HTTP GET toocall hello **Search** API, you need toobe aware that hello length of hello request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="9e15b-786">Esto suele ser suficiente para la mayoría de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9e15b-786">This is usually enough for most applications.</span></span> <span data-ttu-id="9e15b-787">Sin embargo, algunas aplicaciones generan consultas muy extensas o expresiones de filtro OData.</span><span class="sxs-lookup"><span data-stu-id="9e15b-787">However, some applications produce very large queries or OData filter expressions.</span></span> <span data-ttu-id="9e15b-788">Para estas aplicaciones, el uso de HTTP POST es una opción mejor porque permite filtros y consultas mayores que GET.</span><span class="sxs-lookup"><span data-stu-id="9e15b-788">For these applications, using HTTP POST is a better choice because it allows larger filters and queries than GET.</span></span> <span data-ttu-id="9e15b-789">Con POST, número de Hola de términos o cláusulas en una consulta está limitando Hola factor, no el tamaño de Hola de consulta sin procesar de hello como límite de tamaño de hello solicitud de POST es aproximadamente 16 MB.</span><span class="sxs-lookup"><span data-stu-id="9e15b-789">With POST, hello number of terms or clauses in a query is hello limiting factor, not hello size of hello raw query since hello request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="9e15b-790">Aunque el límite de tamaño de solicitud POST hello es muy grande, las consultas de búsqueda y las expresiones de filtro no pueden ser arbitrariamente complejas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-790">Even though hello POST request size limit is very large, search queries and filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="9e15b-791">Consulte la [sintaxis de consulta de Lucene](https://msdn.microsoft.com/library/mt589323.aspx) y la [sintaxis de expresiones de OData](https://msdn.microsoft.com/library/dn798921.aspx) para más información sobre las limitaciones de complejidad de consultas y filtros de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-791">See [Lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx) and [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about search query and filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="9e15b-792">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-792">**Request**</span></span>

<span data-ttu-id="9e15b-793">HTTPS es necesario para las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-793">HTTPS is required for service requests.</span></span> <span data-ttu-id="9e15b-794">Hola **búsqueda** solicitud puede crearse mediante Hola GET o métodos POST.</span><span class="sxs-lookup"><span data-stu-id="9e15b-794">hello **Search** request can be constructed using hello GET or POST methods.</span></span>

<span data-ttu-id="9e15b-795">URI de solicitud de Hello especifica qué tooquery de índice, para todos los documentos que coinciden con los parámetros de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-795">hello request URI specifies which index tooquery, for all documents that match hello parameters.</span></span> <span data-ttu-id="9e15b-796">Se especifican en la cadena de consulta de hello en caso de hello de solicitudes GET, y en la solicitud de Hola solicita cuerpo en caso de hello de publicación.</span><span class="sxs-lookup"><span data-stu-id="9e15b-796">Parameters are specified on hello query string in hello case of GET requests, and in hello request body in hello case of POST requests.</span></span>

<span data-ttu-id="9e15b-797">Como práctica recomendada al crear las solicitudes GET, recuerde demasiado[codifica como URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) consulta específica parámetros cuando se llama a Hola API de REST directamente.</span><span class="sxs-lookup"><span data-stu-id="9e15b-797">As a best practice when creating GET requests, remember too[URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling hello REST API directly.</span></span> <span data-ttu-id="9e15b-798">Para las operaciones de **Búsqueda** , esto incluye:</span><span class="sxs-lookup"><span data-stu-id="9e15b-798">For **Search** operations, this includes:</span></span>

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

<span data-ttu-id="9e15b-799">Solo se recomienda la codificación de direcciones URL en hello por encima de los parámetros de consulta.</span><span class="sxs-lookup"><span data-stu-id="9e15b-799">URL encoding is only recommended on hello above query parameters.</span></span> <span data-ttu-id="9e15b-800">Si se codifica como URL accidentalmente hello cadena de consulta completa (todos los elementos después de hello?), se interrumpirán las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="9e15b-800">If you inadvertently URL-encode hello entire query string (everything after hello ?), requests will break.</span></span>

<span data-ttu-id="9e15b-801">Además, la codificación de direcciones URL solo es necesaria cuando se llama a Hola obtener API de REST directamente mediante.</span><span class="sxs-lookup"><span data-stu-id="9e15b-801">Also, URL encoding is only necessary when calling hello REST API directly using GET.</span></span> <span data-ttu-id="9e15b-802">Codificación de dirección URL no es necesaria cuando se llama a **búsqueda** mediante POST, o al usar hello [biblioteca de cliente .NET](https://msdn.microsoft.com/library/dn951165.aspx), que controla la codificación de direcciones URL para usted.</span><span class="sxs-lookup"><span data-stu-id="9e15b-802">No URL encoding is necessary when calling **Search** using POST, or when using hello [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="9e15b-803"><a name="SearchQueryParameters"></a>
**Parámetros de consulta**</span><span class="sxs-lookup"><span data-stu-id="9e15b-803"><a name="SearchQueryParameters"></a>
**Query Parameters**</span></span>

<span data-ttu-id="9e15b-804">**búsqueda** acepta varios parámetros que ofrecen criterios de consulta y que también especifican el comportamiento de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-804">**Search** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="9e15b-805">Proporcionar la cadena de consulta de estos parámetros en la dirección URL de hello al llamar a **búsqueda** a través de GET y como propiedades JSON en el cuerpo de la solicitud de hello al llamar a **búsqueda** a través de POST.</span><span class="sxs-lookup"><span data-stu-id="9e15b-805">You provide these parameters in hello URL query string when calling **Search** via GET, and as JSON properties in hello request body when calling **Search** via POST.</span></span> <span data-ttu-id="9e15b-806">sintaxis de Hola para algunos parámetros difiere ligeramente entre GET y POST.</span><span class="sxs-lookup"><span data-stu-id="9e15b-806">hello syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="9e15b-807">Estas diferencias se indican como aplicables a continuación:</span><span class="sxs-lookup"><span data-stu-id="9e15b-807">These differences are noted as applicable below:</span></span>

<span data-ttu-id="9e15b-808">`search=[string]`(opcional): Hola toosearch de texto para.</span><span class="sxs-lookup"><span data-stu-id="9e15b-808">`search=[string]` (optional) - hello text toosearch for.</span></span> <span data-ttu-id="9e15b-809">Se busca en los campos `searchable` de forma predeterminada a menos que se especifique `searchFields`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-809">All `searchable` fields are searched by default unless `searchFields` is specified.</span></span> <span data-ttu-id="9e15b-810">Al buscar `searchable` se acorta campos, Hola texto de búsqueda, por lo que se pueden separar varios términos con espacios en blanco (por ejemplo: `search=hello world`).</span><span class="sxs-lookup"><span data-stu-id="9e15b-810">When searching `searchable` fields, hello search text itself is tokenized, so multiple terms can be separated by white space (for example: `search=hello world`).</span></span> <span data-ttu-id="9e15b-811">usar de cualquier término, toomatch `*` (puede ser útil para las consultas de filtro booleano).</span><span class="sxs-lookup"><span data-stu-id="9e15b-811">toomatch any term, use `*` (this can be useful for boolean filter queries).</span></span> <span data-ttu-id="9e15b-812">Si se omite este parámetro tiene el mismo efecto que si se establece demasiado de hello`*`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-812">Omitting this parameter has hello same effect as setting it too`*`.</span></span> <span data-ttu-id="9e15b-813">Vea [sintaxis de consulta Simple](https://msdn.microsoft.com/library/dn798920.aspx) para obtener información específica acerca de la sintaxis de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-813">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) for specifics on hello search syntax.</span></span>

* <span data-ttu-id="9e15b-814">**Tenga en cuenta**: resultados de Hola a veces pueden ser sorprendentes cuando se consulta sobre `searchable` campos.</span><span class="sxs-lookup"><span data-stu-id="9e15b-814">**Note**: hello results can sometimes be surprising when querying over `searchable` fields.</span></span> <span data-ttu-id="9e15b-815">tokenizer Hola incluye lógica toohandle casos comunes tooEnglish texto como apóstrofo, comas en números, etcetera. Por ejemplo, `search=123,456` coincidirá con un término 123,456 en lugar de términos individuales de hello 123 y 456, dado que se utilizan comas como separadores de miles para números grandes en inglés.</span><span class="sxs-lookup"><span data-stu-id="9e15b-815">hello tokenizer includes logic toohandle cases common tooEnglish text like apostrophes, commas in numbers, etc. For example, `search=123,456` will match a single term 123,456 rather than hello individual terms 123 and 456, since commas are used as thousand-separators for large numbers in English.</span></span> <span data-ttu-id="9e15b-816">Por este motivo, se recomienda utilizar el espacio en blanco en lugar de términos de puntuación tooseparate Hola `search` parámetro.</span><span class="sxs-lookup"><span data-stu-id="9e15b-816">For this reason, we recommend using white space rather than punctuation tooseparate terms in hello `search` parameter.</span></span>

<span data-ttu-id="9e15b-817">`searchMode=any|all`(opcional, valor predeterminado es demasiado`any`): indica si alguno o todos los términos de búsqueda de hello deben coincidir en el documento de pedido toocount hello como una coincidencia.</span><span class="sxs-lookup"><span data-stu-id="9e15b-817">`searchMode=any|all` (optional, defaults too`any`) - whether any or all of hello search terms must be matched in order toocount hello document as a match.</span></span>

<span data-ttu-id="9e15b-818">`searchFields=[string]`(opcional): lista de Hola de toosearch de nombres de campo separados por comas para hello el texto especificado.</span><span class="sxs-lookup"><span data-stu-id="9e15b-818">`searchFields=[string]` (optional) - hello list of comma-separated field names toosearch for hello specified text.</span></span> <span data-ttu-id="9e15b-819">Los campos de destino deben estar marcados como `searchable`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-819">Target fields must be marked as `searchable`.</span></span>

<span data-ttu-id="9e15b-820">`queryType=simple|full`(opcional, valor predeterminado es demasiado`simple`): cuando set demasiado "simple" Buscar texto se interpreta usando un lenguaje de consulta simple que permite símbolos como +, * y "".</span><span class="sxs-lookup"><span data-stu-id="9e15b-820">`queryType=simple|full` (optional, defaults too`simple`) - when set too"simple" search text is interpreted using a simple query language that allows for symbols such as +, * and "".</span></span> <span data-ttu-id="9e15b-821">Las consultas se evalúan en todos los campos de búsqueda (o campos indicados en `searchFields`) en cada documento de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9e15b-821">Queries are evaluated across all searchable fields (or fields indicated in `searchFields`) in each document by default.</span></span> <span data-ttu-id="9e15b-822">Cuando se establece demasiado el tipo de consulta de hello`full` texto de búsqueda se interpreta con lenguaje de consulta de Lucene de Hola que permite realizar búsquedas específicas de los campos y ponderadas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-822">When hello query type is set too`full` search text is interpreted using hello Lucene query language which allows field-specific and weighted searches.</span></span> <span data-ttu-id="9e15b-823">Vea [sintaxis de consulta Simple](https://msdn.microsoft.com/library/dn798920.aspx) y [sintaxis de consulta de Lucene](https://msdn.microsoft.com/library/mt589323.aspx) para obtener información específica sobre la sintaxis de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-823">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) and [Lucene Query Syntax](https://msdn.microsoft.com/library/mt589323.aspx) for specifics on hello search syntaxes.</span></span> 

> [!NOTE]
> <span data-ttu-id="9e15b-824">Intervalo de búsqueda en hello Lucene no se admite el lenguaje de consulta en favor de $filter que ofrece una funcionalidad similar.</span><span class="sxs-lookup"><span data-stu-id="9e15b-824">Range search in hello Lucene query language is not supported in favor of $filter which offers similar functionality.</span></span>
> 
> 

<span data-ttu-id="9e15b-825">`moreLikeThis=[key]` (opcional) **Importante:**  esta característica solo está disponible en `2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-825">`moreLikeThis=[key]` (optional) **Important:** This feature is only available in `2015-02-28-Preview`.</span></span> <span data-ttu-id="9e15b-826">Esta opción no se puede usar en una consulta que contiene el parámetro de búsqueda de texto hello, `search=[string]`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-826">This option cannot be used in a query that contains hello text search parameter, `search=[string]`.</span></span> <span data-ttu-id="9e15b-827">Hola `moreLikeThis` parámetro busca documentos que son similares documento toohello especificado por clave de documento de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-827">hello `moreLikeThis` parameter finds documents that are similar toohello document specified by hello document key.</span></span> <span data-ttu-id="9e15b-828">Cuando se realiza una solicitud de búsqueda con `moreLikeThis`, se genera una lista de términos de búsqueda en función de la frecuencia de Hola y escasez de términos en el documento de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-828">When a search request is made with `moreLikeThis`, a list of search terms is generated based on hello frequency and rarity of terms in hello source document.</span></span> <span data-ttu-id="9e15b-829">Estos términos son utilizado toomake Hola solicitud.</span><span class="sxs-lookup"><span data-stu-id="9e15b-829">Those terms are then used toomake hello request.</span></span> <span data-ttu-id="9e15b-830">De forma predeterminada, Hola contenido de todos los `searchable` campos se consideran a menos que `searchFields` es toorestrict usa los campos que se buscan.</span><span class="sxs-lookup"><span data-stu-id="9e15b-830">By default, hello contents of all `searchable` fields are considered unless `searchFields` is used toorestrict which fields are searched.</span></span>  

<span data-ttu-id="9e15b-831">`$skip=#`(opcional): número de Hola de búsqueda de resultados tooskip; No puede ser superior a 100 000.</span><span class="sxs-lookup"><span data-stu-id="9e15b-831">`$skip=#` (optional) - hello number of search results tooskip; Cannot be greater than 100,000.</span></span> <span data-ttu-id="9e15b-832">Si necesita tooscan documentos en secuencia pero no se puede usar `$skip` debido a la limitación toothis, considere el uso de `$orderby` en una clave totalmente ordenada y `$filter` con un intervalo de consulta en su lugar.</span><span class="sxs-lookup"><span data-stu-id="9e15b-832">If you need tooscan documents in sequence but cannot use `$skip` due toothis limitation, consider using `$orderby` on a totally-ordered key and `$filter` with a range query instead.</span></span>

> [!NOTE]
> <span data-ttu-id="9e15b-833">Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `skip` en lugar de `$skip`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-833">When calling **Search** using POST, this parameter is named `skip` instead of `$skip`.</span></span>
> 
> 

<span data-ttu-id="9e15b-834">`$top=#`(opcional): número de Hola de búsqueda resultados tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="9e15b-834">`$top=#` (optional) - hello number of search results tooretrieve.</span></span> <span data-ttu-id="9e15b-835">Esto puede utilizarse junto con `$skip` tooimplement paginación por parte del cliente de resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-835">This can be used in conjunction with `$skip` tooimplement client-side paging of search results.</span></span>

> [!NOTE]
> <span data-ttu-id="9e15b-836">Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `top` en lugar de `$top`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-836">When calling **Search** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="9e15b-837">`$count=true|false`(opcional, valor predeterminado es demasiado`false`)-especifica si toofetch Hola número total de resultados.</span><span class="sxs-lookup"><span data-stu-id="9e15b-837">`$count=true|false` (optional, defaults too`false`) - Specifies whether toofetch hello total count of results.</span></span> <span data-ttu-id="9e15b-838">Es Hola recuento de todos los documentos que coinciden con hello `search` y `$filter` parámetros, se omitirá `$top` y `$skip`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-838">This is hello count of all documents that match hello `search` and `$filter` parameters, ignoring `$top` and `$skip`.</span></span> <span data-ttu-id="9e15b-839">Este valor demasiado`true` puede afectar al rendimiento.</span><span class="sxs-lookup"><span data-stu-id="9e15b-839">Setting this value too`true` may have a performance impact.</span></span> <span data-ttu-id="9e15b-840">Tenga en cuenta que devuelve el recuento de hello es una aproximación.</span><span class="sxs-lookup"><span data-stu-id="9e15b-840">Note that hello count returned is an approximation.</span></span>

> [!NOTE]
> <span data-ttu-id="9e15b-841">Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `count` en lugar de `$count`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-841">When calling **Search** using POST, this parameter is named `count` instead of `$count`.</span></span>
> 
> 

<span data-ttu-id="9e15b-842">`$orderby=[string]`(opcional): una lista de expresiones separadas por comas toosort Hola resultados por.</span><span class="sxs-lookup"><span data-stu-id="9e15b-842">`$orderby=[string]` (optional) - A list of comma-separated expressions toosort hello results by.</span></span> <span data-ttu-id="9e15b-843">Cada expresión puede ser un nombre de campo o una llamada toohello `geo.distance()` función.</span><span class="sxs-lookup"><span data-stu-id="9e15b-843">Each expression can be either a field name or a call toohello `geo.distance()` function.</span></span> <span data-ttu-id="9e15b-844">Cada expresión puede ir seguida de `asc` tooindicated ascendente, y `desc` tooindicate descendente.</span><span class="sxs-lookup"><span data-stu-id="9e15b-844">Each expression can be followed by `asc` tooindicated ascending, and `desc` tooindicate descending.</span></span> <span data-ttu-id="9e15b-845">valor predeterminado de Hello es ascendente.</span><span class="sxs-lookup"><span data-stu-id="9e15b-845">hello default is ascending order.</span></span> <span data-ttu-id="9e15b-846">El empate se rompe por las puntuaciones de coincidencia de Hola de documentos.</span><span class="sxs-lookup"><span data-stu-id="9e15b-846">Ties will be broken by hello match scores of documents.</span></span> <span data-ttu-id="9e15b-847">Si no hay ningún `$orderby` se especifica, criterio de ordenación predeterminado de hello es descendente según la puntuación de coincidencia de documento.</span><span class="sxs-lookup"><span data-stu-id="9e15b-847">If no `$orderby` is specified, hello default sort order is descending by document match score.</span></span> <span data-ttu-id="9e15b-848">Hay un límite de 32 cláusulas para `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-848">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="9e15b-849">Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `orderby` en lugar de `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-849">When calling **Search** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="9e15b-850">`$select=[string]`(opcional): una lista de campos separados por comas tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="9e15b-850">`$select=[string]` (optional) - A list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="9e15b-851">Si no se especifica, se incluyen todos los campos marcados como recuperables en el esquema de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-851">If unspecified, all fields marked as retrievable in hello schema are included.</span></span> <span data-ttu-id="9e15b-852">Puede solicitar explícitamente todos los campos, establezca este parámetro demasiado`*`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-852">You can also explicitly request all fields by setting this parameter too`*`.</span></span>

> [!NOTE]
> <span data-ttu-id="9e15b-853">Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `select` en lugar de `$select`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-853">When calling **Search** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="9e15b-854">`facet=[string]`(cero o más) - un toofacet campo por.</span><span class="sxs-lookup"><span data-stu-id="9e15b-854">`facet=[string]` (zero or more) - A field toofacet by.</span></span> <span data-ttu-id="9e15b-855">Opcionalmente, Hola de cadena puede contener facetas de parámetros toocustomize Hola expresado como separada por comas `name:value` pares.</span><span class="sxs-lookup"><span data-stu-id="9e15b-855">Optionally hello string may contain parameters toocustomize hello faceting expressed as comma-separated `name:value` pairs.</span></span> <span data-ttu-id="9e15b-856">Los parámetros válidos son:</span><span class="sxs-lookup"><span data-stu-id="9e15b-856">Valid parameters are:</span></span>

* <span data-ttu-id="9e15b-857">`count` (número máximo de términos de faceta; el valor predeterminado es 10).</span><span class="sxs-lookup"><span data-stu-id="9e15b-857">`count` (max number of facet terms; default is 10).</span></span> <span data-ttu-id="9e15b-858">No hay ningún máximo, pero los valores más altos incurren en una disminución correspondiente del rendimiento, especialmente si el campo por facetas hello contiene un gran número de términos únicos.</span><span class="sxs-lookup"><span data-stu-id="9e15b-858">There is no maximum, but higher values incur a corresponding performance penalty, especially if hello faceted field contains a large number of unique terms.</span></span>
  * <span data-ttu-id="9e15b-859">Por ejemplo: `facet=category,count:5` obtiene Hola cinco categorías principales en los resultados de la faceta.</span><span class="sxs-lookup"><span data-stu-id="9e15b-859">For example: `facet=category,count:5` gets hello top five categories in facet results.</span></span>  
  * <span data-ttu-id="9e15b-860">**Tenga en cuenta**: si hello `count` parámetro es menor que el número de Hola de términos únicos, resultados de hello pueden no ser exacto.</span><span class="sxs-lookup"><span data-stu-id="9e15b-860">**Note**: If hello `count` parameter is less than hello number of unique terms, hello results may not be accurate.</span></span> <span data-ttu-id="9e15b-861">Esto es debido a las consultas de facetas se distribuyen entre las particiones de forma de toohello.</span><span class="sxs-lookup"><span data-stu-id="9e15b-861">This is due toohello way faceting queries are distributed across shards.</span></span> <span data-ttu-id="9e15b-862">Aumentar `count` generalmente aumenta Hola precisión de recuentos de término de hello, pero con un costo de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="9e15b-862">Increasing `count` generally increases hello accuracy of hello term counts, but at a performance cost.</span></span>
* <span data-ttu-id="9e15b-863">`sort`(una de `count` toosort *descendente* por número, `-count` toosort *ascendente* por número, `value` toosort *ascendente* por valor, o `-value` toosort *descendente* por valor)</span><span class="sxs-lookup"><span data-stu-id="9e15b-863">`sort` (one of `count` toosort *descending* by count, `-count` toosort *ascending* by count, `value` toosort *ascending* by value, or `-value` toosort *descending* by value)</span></span>
  * <span data-ttu-id="9e15b-864">Por ejemplo: `facet=category,count:3,sort:count` obtiene Hola tres categorías principales en los resultados de la faceta en orden descendente por número de Hola de documentos con cada nombre de ciudad.</span><span class="sxs-lookup"><span data-stu-id="9e15b-864">For example: `facet=category,count:3,sort:count` gets hello top three categories in facet results in descending order by hello number of documents with each city name.</span></span> <span data-ttu-id="9e15b-865">Por ejemplo, si tres categorías principales Hola son presupuesto, Motel y lujo y presupuesto tiene 5 resultados, Motel tiene 6 y lujo tiene 4, a continuación, hello depósitos será en orden de hello Motel, presupuesto, lujo.</span><span class="sxs-lookup"><span data-stu-id="9e15b-865">For example, if hello top three categories are Budget, Motel, and Luxury, and Budget has 5 hits, Motel has 6, and Luxury has 4, then hello buckets will be in hello order Motel, Budget, Luxury.</span></span>
  * <span data-ttu-id="9e15b-866">Por ejemplo: `facet=rating,sort:-value` genera depósitos para todas las clasificaciones posibles en orden descendente por valor.</span><span class="sxs-lookup"><span data-stu-id="9e15b-866">For example: `facet=rating,sort:-value` produces buckets for all possible ratings, in descending order by value.</span></span> <span data-ttu-id="9e15b-867">Por ejemplo, si las clasificaciones de hello son de 1 too5, Hola cubos se ordenarán 5, 4, 3, 2, 1, independientemente de cuántos documentos coinciden con cada clasificación.</span><span class="sxs-lookup"><span data-stu-id="9e15b-867">For example, if hello ratings are from 1 too5, hello buckets will be ordered 5, 4, 3, 2, 1, irrespective of how many documents match each rating.</span></span>
* <span data-ttu-id="9e15b-868">`values` (valores numéricos delimitados por canalización o `Edm.DateTimeOffset` que especifican un conjunto dinámico de valores de entrada de faceta)</span><span class="sxs-lookup"><span data-stu-id="9e15b-868">`values` (pipe-delimited numeric or `Edm.DateTimeOffset` values specifying a dynamic set of facet entry values)</span></span>
  * <span data-ttu-id="9e15b-869">Por ejemplo: `facet=baseRate,values:10|20` genera tres cubos: uno para la tarifa base 0 seguridad toobut sin incluir 10, uno para 10 arriba toobut sin incluir 20 y uno para 20 o superior.</span><span class="sxs-lookup"><span data-stu-id="9e15b-869">For example: `facet=baseRate,values:10|20` produces three buckets: One for base rate 0 up toobut not including 10, one for 10 up toobut not including 20, and one for 20 or higher.</span></span>
  * <span data-ttu-id="9e15b-870">Por ejemplo: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` genera dos depósitos: uno para hoteles reformados antes de febrero de 2010 y otro para hoteles reformados desde el 1 de febrero de 2010 en adelante.</span><span class="sxs-lookup"><span data-stu-id="9e15b-870">For example: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produces two buckets: One for hotels renovated before February 2010, and one for hotels renovated February 1st, 2010 or later.</span></span>
* <span data-ttu-id="9e15b-871">`interval` (intervalo de número entero mayor que 0 para números, o `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` para los valores de fecha y hora)</span><span class="sxs-lookup"><span data-stu-id="9e15b-871">`interval` (integer interval greater than 0 for numbers, or `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` for date time values)</span></span>
  * <span data-ttu-id="9e15b-872">Por ejemplo: `facet=baseRate,interval:100` genera depósitos basados en intervalos de tarifas base de tamaño de 100.</span><span class="sxs-lookup"><span data-stu-id="9e15b-872">For example: `facet=baseRate,interval:100` produces buckets based on base rate ranges of size 100.</span></span> <span data-ttu-id="9e15b-873">Por ejemplo, si las tarifas base se encuentran entre 60 y 600 dólares, habrá depósitos para 0-100, 100-200, 300 200, 300-400, 400-500 y 500-600.</span><span class="sxs-lookup"><span data-stu-id="9e15b-873">For example, if base rates are all between $60 and $600, there will be buckets for 0-100, 100-200, 200-300, 300-400, 400-500, and 500-600.</span></span>
  * <span data-ttu-id="9e15b-874">Por ejemplo: `facet=lastRenovationDate,interval:year` genera un depósito para cada año en que se han reformado los hoteles.</span><span class="sxs-lookup"><span data-stu-id="9e15b-874">For example: `facet=lastRenovationDate,interval:year` produces one bucket for each year when hotels were renovated.</span></span>
* <span data-ttu-id="9e15b-875">`timeoffset` ([+-] hh: mm, [+-] hhmm, o [+-] hh) `timeoffset` es opcional.</span><span class="sxs-lookup"><span data-stu-id="9e15b-875">`timeoffset` ([+-]hh:mm, [+-]hhmm, or [+-]hh) `timeoffset` is optional.</span></span> <span data-ttu-id="9e15b-876">Solo puede combinarse con hello `interval` opción y sólo cuando aplica tooa campo de tipo `Edm.DateTimeOffset`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-876">It can only be combined with hello `interval` option, and only when applied tooa field of type `Edm.DateTimeOffset`.</span></span> <span data-ttu-id="9e15b-877">valor de Hello especifica tooaccount desplazamiento de hora UTC hello para establecer los límites de tiempo.</span><span class="sxs-lookup"><span data-stu-id="9e15b-877">hello value specifies hello UTC time offset tooaccount for in setting time boundaries.</span></span>
  * <span data-ttu-id="9e15b-878">Por ejemplo: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` usa Hola límites de día que empieza en 01:00:00 UTC (medianoche en la zona horaria de destino de hello)</span><span class="sxs-lookup"><span data-stu-id="9e15b-878">For example: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` uses hello day boundary that starts at 01:00:00 UTC (midnight in hello target time zone)</span></span>
* <span data-ttu-id="9e15b-879">**Tenga en cuenta**: `count` y `sort` se pueden combinar en hello misma especificación de faceta, pero no se puede combinar con `interval` o `values`, y `interval` y `values` no se pueden combinar entre sí.</span><span class="sxs-lookup"><span data-stu-id="9e15b-879">**Note**: `count` and `sort` can be combined in hello same facet specification, but they cannot be combined with `interval` or `values`, and `interval` and `values` cannot be combined together.</span></span>
* <span data-ttu-id="9e15b-880">**Nota**: Las facetas de intervalo de fecha y hora se calculan en función de la hora UTC si `timeoffset` no se ha especificado.</span><span class="sxs-lookup"><span data-stu-id="9e15b-880">**Note**: Interval facets on date time are computed based on UTC time if `timeoffset` is not specified.</span></span> <span data-ttu-id="9e15b-881">Por ejemplo: para `facet=lastRenovationDate,interval:day`, límites de día de hello comienza en 00:00:00 UTC.</span><span class="sxs-lookup"><span data-stu-id="9e15b-881">For example: for `facet=lastRenovationDate,interval:day`, hello day boundary starts at 00:00:00 UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="9e15b-882">Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `facets` en lugar de `facet`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-882">When calling **Search** using POST, this parameter is named `facets` instead of `facet`.</span></span> <span data-ttu-id="9e15b-883">Además, lo especifica como una matriz JSON de cadenas, donde cada cadena es una expresión de faceta independiente.</span><span class="sxs-lookup"><span data-stu-id="9e15b-883">Also, you specify it as a JSON array of strings where each string is a separate facet expression.</span></span>
> 
> 

<span data-ttu-id="9e15b-884">`$filter=[string]` (opcional): expresión de búsqueda estructurada en la sintaxis estándar de OData.</span><span class="sxs-lookup"><span data-stu-id="9e15b-884">`$filter=[string]` (optional) - A structured search expression in standard OData syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="9e15b-885">Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `filter` en lugar de `$filter`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-885">When calling **Search** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="9e15b-886">`highlight=[string]` (opcional): conjunto de nombres de campos delimitado por comas usado para los resaltados de referencias.</span><span class="sxs-lookup"><span data-stu-id="9e15b-886">`highlight=[string]` (optional) - A set of comma-separated field names used for hit highlights.</span></span> <span data-ttu-id="9e15b-887">Solo se pueden usar `searchable` campos para resaltar las referencias.</span><span class="sxs-lookup"><span data-stu-id="9e15b-887">Only `searchable` fields can be used for hit highlighting.</span></span>

<span data-ttu-id="9e15b-888">`highlightPreTag=[string]`(opcional, valor predeterminado es demasiado`<em>`): una cadena de etiqueta que se antepone toohit resaltados.</span><span class="sxs-lookup"><span data-stu-id="9e15b-888">`highlightPreTag=[string]` (optional, defaults too`<em>`) - A string tag that prepends toohit highlights.</span></span> <span data-ttu-id="9e15b-889">Debe establecerse con `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-889">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="9e15b-890">Al llamar a **búsqueda** con GET, caracteres reservados en la dirección URL de hello deben estar codificados en porcentaje (por ejemplo, % 23 en lugar de #).</span><span class="sxs-lookup"><span data-stu-id="9e15b-890">When calling **Search** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="9e15b-891">`highlightPostTag=[string]`(opcional, valor predeterminado es demasiado`</em>`)-una etiqueta de cadena que se anexa información destacada de toohit.</span><span class="sxs-lookup"><span data-stu-id="9e15b-891">`highlightPostTag=[string]` (optional, defaults too`</em>`) - a string tag that appends toohit highlights.</span></span> <span data-ttu-id="9e15b-892">Debe establecerse con `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-892">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="9e15b-893">Al llamar a **búsqueda** con GET, caracteres reservados en la dirección URL de hello deben estar codificados en porcentaje (por ejemplo, % 23 en lugar de #).</span><span class="sxs-lookup"><span data-stu-id="9e15b-893">When calling **Search** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="9e15b-894">`scoringProfile=[string]`(opcional): nombre Hola de una puntuación tooevaluate perfil puntuaciones de coincidencia para documentos coincidentes en los resultados de orden toosort Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-894">`scoringProfile=[string]` (optional) - hello name of a scoring profile tooevaluate match scores for matching documents in order toosort hello results.</span></span>

<span data-ttu-id="9e15b-895">`scoringParameter=[string]`(cero o más): indican los valores de hello para cada parámetro definido en una función de puntuación (por ejemplo, `referencePointParameter`) con formato de hello `name-value1,value2,...`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-895">`scoringParameter=[string]` (zero or more) - Indicates hello values for each parameter defined in a scoring function (for example, `referencePointParameter`) using hello format `name-value1,value2,...`.</span></span>

* <span data-ttu-id="9e15b-896">Por ejemplo, si Hola perfil de puntuación define una función con un parámetro llamado "mylocation" opción de la cadena de consulta de hello sería `&scoringParameter=mylocation--122.2,44.8`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-896">For example, if hello scoring profile defines a function with a parameter called "mylocation" hello query string option would be `&scoringParameter=mylocation--122.2,44.8`.</span></span> <span data-ttu-id="9e15b-897">guión primera Hola separa el nombre de Hola de lista de valores de hello, mientras guión segundo Hola forma parte del primer valor de hello (longitud en este ejemplo).</span><span class="sxs-lookup"><span data-stu-id="9e15b-897">hello first dash separates hello name from hello value list, while hello second dash is part of hello first value (longitude in this example).</span></span>
* <span data-ttu-id="9e15b-898">Para los parámetros de puntuación como etiqueta de impulso puede contener comas, puede omitir cualquier tales valores de lista de hello con comillas simples.</span><span class="sxs-lookup"><span data-stu-id="9e15b-898">For scoring parameters such as for tag boosting that can contain commas, you can escape any such values in hello list using single quotes.</span></span> <span data-ttu-id="9e15b-899">Si los propios valores de hello contengan comillas simples, se puede omitir duplicando.</span><span class="sxs-lookup"><span data-stu-id="9e15b-899">If hello values themselves contain single quotes, you can escape them by doubling.</span></span>
  * <span data-ttu-id="9e15b-900">Por ejemplo, si tiene una etiqueta impulso parámetro denominado "mytag" y desea tooboost en etiqueta Hola valores "¡Hello, o ' Brien" y "Smith", consulta Hola cadena opción sería `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-900">For example, if you have a tag boosting parameter called "mytag" and you want tooboost on hello tag values "Hello, O'Brien" and "Smith", hello query string option would be `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span></span> <span data-ttu-id="9e15b-901">Tenga en cuenta que las comillas solo son necesarias para los valores que contienen comas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-901">Note that quotes are only required for values that contain commas.</span></span>

> [!NOTE]
> <span data-ttu-id="9e15b-902">Al llamar a la **búsqueda** mediante POST, este parámetro se denomina `scoringParameters` en lugar de `scoringParameter`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-902">When calling **Search** using POST, this parameter is named `scoringParameters` instead of `scoringParameter`.</span></span> <span data-ttu-id="9e15b-903">Además, lo especifica como una matriz JSON de cadenas, donde cada cadena es un par `name-values` independiente.</span><span class="sxs-lookup"><span data-stu-id="9e15b-903">Also, you specify it as a JSON array of strings where each string is a separate `name-values` pair.</span></span>
> 
> 

<span data-ttu-id="9e15b-904">`minimumCoverage`(opcional, tiene como valor predeterminado too100) - un número entre 0 y 100 que indica el porcentaje de Hola de índice de Hola que debe ser abarcado por una consulta de búsqueda en orden para hello consulta toobe notificarse como tales.</span><span class="sxs-lookup"><span data-stu-id="9e15b-904">`minimumCoverage` (optional, defaults too100) - a number between 0 and 100 indicating hello percentage of hello index that must be covered by a search query in order for hello query toobe reported as a success.</span></span> <span data-ttu-id="9e15b-905">De forma predeterminada, todo índice de hello debe estar disponible o `Search` se devolverá el código de estado HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="9e15b-905">By default, hello entire index must be available or `Search` will return HTTP status code 503.</span></span> <span data-ttu-id="9e15b-906">Si establece `minimumCoverage` y `Search` se realiza correctamente, devolverá HTTP 200 e incluyen una `@search.coverage` valor de respuesta de Hola que indica el porcentaje de Hola de índice de Hola que se incluyó en la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-906">If you set `minimumCoverage` and `Search` succeeds, it will return HTTP 200 and include a `@search.coverage` value in hello response indicating hello percentage of hello index that was included in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="9e15b-907">Establecer este valor de parámetro tooa menor que 100 puede ser útil para garantizar la disponibilidad de búsqueda incluso para servicios con una única réplica.</span><span class="sxs-lookup"><span data-stu-id="9e15b-907">Setting this parameter tooa value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="9e15b-908">Sin embargo, no todos los documentos coincidentes se garantiza que toobe presente en los resultados de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-908">However, not all matching documents are guaranteed toobe present in hello search results.</span></span> <span data-ttu-id="9e15b-909">Si la recuperación de búsqueda es más importante aplicación tooyour de disponibilidad, es mejor tooleave `minimumCoverage` en su valor predeterminado de 100.</span><span class="sxs-lookup"><span data-stu-id="9e15b-909">If search recall is more important tooyour application than availability, then it's best tooleave `minimumCoverage` at its default value of 100.</span></span>
> 
> 

<span data-ttu-id="9e15b-910">`api-version=[string]` (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="9e15b-910">`api-version=[string]` (required).</span></span> <span data-ttu-id="9e15b-911">versión de vista previa de Hello es `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-911">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9e15b-912">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-912">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="9e15b-913">Nota: Para realizar esta operación, Hola `api-version` se especifica como un parámetro de consulta de dirección URL de hello independientemente de si se llama a **búsqueda** con GET o POST.</span><span class="sxs-lookup"><span data-stu-id="9e15b-913">Note: For this operation, hello `api-version` is specified as a query parameter in hello URL regardless of whether you call **Search** with GET or POST.</span></span>

<span data-ttu-id="9e15b-914">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-914">**Request Headers**</span></span>

<span data-ttu-id="9e15b-915">Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales.</span><span class="sxs-lookup"><span data-stu-id="9e15b-915">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="9e15b-916">`api-key`: Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-916">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9e15b-917">Es un valor de cadena único tooyour dirección URL del servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-917">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="9e15b-918">Hola **búsqueda** solicitud puede especificar una clave de administración o la clave de consulta para `api-key`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-918">hello **Search** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="9e15b-919">También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-919">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9e15b-920">Puede obtener el nombre del servicio de Hola y `api-key` desde el panel de servicio en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e15b-920">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9e15b-921">Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.</span><span class="sxs-lookup"><span data-stu-id="9e15b-921">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9e15b-922">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-922">**Request Body**</span></span>

<span data-ttu-id="9e15b-923">Para GET: ninguno.</span><span class="sxs-lookup"><span data-stu-id="9e15b-923">For GET: None.</span></span>

<span data-ttu-id="9e15b-924">Para POST:</span><span class="sxs-lookup"><span data-stu-id="9e15b-924">For POST:</span></span>

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 100),
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

<span data-ttu-id="9e15b-925">**Continuación de las respuestas de búsqueda parciales**</span><span class="sxs-lookup"><span data-stu-id="9e15b-925">**Continuation of Partial Search Responses**</span></span>

<span data-ttu-id="9e15b-926">A veces, búsqueda de Azure no puede devolver que todos los Hola resultados solicitados en una única respuesta de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-926">Sometimes Azure Search can't return all hello requested results in a single Search response.</span></span> <span data-ttu-id="9e15b-927">Esto puede ocurrir por diferentes motivos, como consultas de hello las solicitudes de demasiados documentos especificando no `$top` o especificar un valor para `$top` que es demasiado grande.</span><span class="sxs-lookup"><span data-stu-id="9e15b-927">This can happen for different reasons, such as when hello query requests too many documents by not specifying `$top` or specifying a value for `$top` that is too large.</span></span> <span data-ttu-id="9e15b-928">En tales casos, búsqueda de Azure incluirá hello `@odata.nextLink` anotación en el cuerpo de la respuesta de hello y también `@search.nextPageParameters` si era una solicitud POST.</span><span class="sxs-lookup"><span data-stu-id="9e15b-928">In such cases, Azure Search will include hello `@odata.nextLink` annotation in hello response body, and also `@search.nextPageParameters` if it was a POST request.</span></span> <span data-ttu-id="9e15b-929">Puede usar valores de hello de estas anotaciones tooformulate otra búsqueda solicitud tooget Hola siguiente parte de la respuesta de la búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-929">You can use hello values of these annotations tooformulate another Search request tooget hello next part of hello search response.</span></span> <span data-ttu-id="9e15b-930">Esto se denomina una ***continuación*** de solicitud de búsqueda original de Hola y Hola generalmente se denominan anotaciones ***tokens de continuación***.</span><span class="sxs-lookup"><span data-stu-id="9e15b-930">This is called a ***continuation*** of hello original Search request, and hello annotations are generally called ***continuation tokens***.</span></span> <span data-ttu-id="9e15b-931">Vea [ejemplo Hola siguiente](#SearchResponse) para obtener más información acerca de la sintaxis de Hola de estas anotaciones y que aparecen en el cuerpo de la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-931">See [hello example below](#SearchResponse) for details on hello syntax of these annotations and where they appear in hello response body.</span></span> 

<span data-ttu-id="9e15b-932">¿Por qué la búsqueda de Azure podría devolver tokens de continuación de razones de Hello son toochange específico de la implementación y está sujeto.</span><span class="sxs-lookup"><span data-stu-id="9e15b-932">hello reasons why Azure Search might return continuation tokens are implementation-specific and subject toochange.</span></span> <span data-ttu-id="9e15b-933">Los clientes sólidos siempre deben ser toohandle listo casos donde se devuelven documentos menos de lo esperado y un token de continuación es toocontinue incluye la recuperación de documentos.</span><span class="sxs-lookup"><span data-stu-id="9e15b-933">Robust clients should always be ready toohandle cases where fewer documents than expected are returned and a continuation token is included toocontinue retrieving documents.</span></span> <span data-ttu-id="9e15b-934">También tenga en cuenta que debe usar Hola mismo método HTTP como solicitud original de hello en orden toocontinue.</span><span class="sxs-lookup"><span data-stu-id="9e15b-934">Also note that you must use hello same HTTP method as hello original request in order toocontinue.</span></span> <span data-ttu-id="9e15b-935">Por ejemplo, si envía una solicitud GET, las solicitudes de continuación que envíe también deben utilizar GET (y lo mismo para POST).</span><span class="sxs-lookup"><span data-stu-id="9e15b-935">For example, if you sent a GET request, any continuation requests you send must also use GET (and likewise for POST).</span></span>

<span data-ttu-id="9e15b-936"><a name="SearchResponse"></a>
**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="9e15b-936"><a name="SearchResponse"></a>
**Response**</span></span>

<span data-ttu-id="9e15b-937">Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.</span><span class="sxs-lookup"><span data-stu-id="9e15b-937">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@odata.count": # (if $count=true was provided in hello query),
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "@search.facets": { (if faceting was specified in hello query)
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
      "@search.nextPageParameters": { (request body toofetch hello next page of results if not all results could be returned in this response and Search was called with POST)
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
      "@odata.nextLink": (URL toofetch hello next page of results if not all results could be returned in this response; Applies tooboth GET and POST)
    }

<span data-ttu-id="9e15b-938">**Ejemplos:**</span><span class="sxs-lookup"><span data-stu-id="9e15b-938">**Examples:**</span></span>

<span data-ttu-id="9e15b-939">Puede encontrar ejemplos adicionales en hello [sintaxis de expresiones de OData para búsqueda de Azure](https://msdn.microsoft.com/library/azure/dn798921.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="9e15b-939">You can find additional examples on hello [OData Expression Syntax for Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) page.</span></span>

1)    <span data-ttu-id="9e15b-940">Hola de búsqueda índice descendente por fecha.</span><span class="sxs-lookup"><span data-stu-id="9e15b-940">Search hello Index sorted descending by date.</span></span>

    <span data-ttu-id="9e15b-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9e15b-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9e15b-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span><span class="sxs-lookup"><span data-stu-id="9e15b-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span></span>

2)    <span data-ttu-id="9e15b-943">En una búsqueda por facetas, busque en el índice de Hola y recupere facetas para categorías, clasificación, etiquetas, así como elementos con baseRate en intervalos específicos:</span><span class="sxs-lookup"><span data-stu-id="9e15b-943">In a faceted search, search hello index and retrieve facets for categories, rating, tags, as well as items with baseRate in specific ranges:</span></span>

    <span data-ttu-id="9e15b-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9e15b-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9e15b-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span><span class="sxs-lookup"><span data-stu-id="9e15b-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span></span>

3)    <span data-ttu-id="9e15b-946">Mediante un filtro, restringir los resultados de consulta por facetas anterior Hola después Hola usuario hace clic en clasificación 3 y la categoría "Motel":</span><span class="sxs-lookup"><span data-stu-id="9e15b-946">Using a filter, narrow down hello previous faceted query results after hello user clicks on rating 3 and category "Motel":</span></span>

    <span data-ttu-id="9e15b-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9e15b-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9e15b-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span><span class="sxs-lookup"><span data-stu-id="9e15b-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span></span>

4) <span data-ttu-id="9e15b-949">En una búsqueda con facetas, establezca un límite superior en términos únicos devueltos en una consulta.</span><span class="sxs-lookup"><span data-stu-id="9e15b-949">In a faceted search, set an upper limit on unique terms returned in a query.</span></span> <span data-ttu-id="9e15b-950">valor predeterminado de Hello es 10, pero puede aumentar o disminuir este valor mediante hello `count` parámetro en hello `facet` atributo:</span><span class="sxs-lookup"><span data-stu-id="9e15b-950">hello default is 10, but you can increase or decrease this value using hello `count` parameter on hello `facet` attribute:</span></span>

    <span data-ttu-id="9e15b-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9e15b-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9e15b-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span><span class="sxs-lookup"><span data-stu-id="9e15b-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span></span>

5)    <span data-ttu-id="9e15b-953">Hola índice de búsqueda en campos específicos; Por ejemplo, un campo específico del idioma:</span><span class="sxs-lookup"><span data-stu-id="9e15b-953">Search hello Index within specific fields; For example, a language-specific field:</span></span>

    <span data-ttu-id="9e15b-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9e15b-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9e15b-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span><span class="sxs-lookup"><span data-stu-id="9e15b-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span></span>

6) <span data-ttu-id="9e15b-956">Buscar Hola índice en varios campos.</span><span class="sxs-lookup"><span data-stu-id="9e15b-956">Search hello Index across multiple fields.</span></span> <span data-ttu-id="9e15b-957">Por ejemplo, puede almacenar y campos de consulta de búsqueda en varios idiomas, todo dentro de Hola mismo índice.</span><span class="sxs-lookup"><span data-stu-id="9e15b-957">For example, you can store and query searchable fields in multiple languages, all within hello same index.</span></span>  <span data-ttu-id="9e15b-958">Si las descripciones de inglés y francés coexisten en hello mismo documento, puede devolver hello en uno o todos los resultados de la consulta:</span><span class="sxs-lookup"><span data-stu-id="9e15b-958">If English and French descriptions co-exist in hello same document, you can return any or all in hello query results:</span></span>

    <span data-ttu-id="9e15b-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9e15b-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9e15b-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span><span class="sxs-lookup"><span data-stu-id="9e15b-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span></span>

<span data-ttu-id="9e15b-961">Tenga en cuenta que solo puede consultar un índice de cada vez.</span><span class="sxs-lookup"><span data-stu-id="9e15b-961">Note that you can only query one index at a time.</span></span> <span data-ttu-id="9e15b-962">No cree varios índices para cada idioma a menos que piense tooquery uno a la vez.</span><span class="sxs-lookup"><span data-stu-id="9e15b-962">Do not create multiple indexes for each language unless you plan tooquery one at a time.</span></span>

7)    <span data-ttu-id="9e15b-963">Paginación: página 1 de Get hello de elementos (el tamaño de página es 10):</span><span class="sxs-lookup"><span data-stu-id="9e15b-963">Paging - Get hello 1st page of items (page size is 10):</span></span>

    <span data-ttu-id="9e15b-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9e15b-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9e15b-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="9e15b-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span></span>

8)    <span data-ttu-id="9e15b-966">Paginación: página 2 º de Get hello de elementos (el tamaño de página es 10):</span><span class="sxs-lookup"><span data-stu-id="9e15b-966">Paging - Get hello 2nd page of items (page size is 10):</span></span>

    <span data-ttu-id="9e15b-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9e15b-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9e15b-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="9e15b-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span></span>

9)    <span data-ttu-id="9e15b-969">Recupere un conjunto específico de campos:</span><span class="sxs-lookup"><span data-stu-id="9e15b-969">Retrieve a specific set of fields:</span></span>

    <span data-ttu-id="9e15b-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9e15b-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9e15b-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span><span class="sxs-lookup"><span data-stu-id="9e15b-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span></span>

10)  <span data-ttu-id="9e15b-972">Recupere documentos que coincidan con una expresión de filtro específica:</span><span class="sxs-lookup"><span data-stu-id="9e15b-972">Retrieve documents matching a specific filter expression:</span></span>

    <span data-ttu-id="9e15b-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9e15b-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9e15b-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span><span class="sxs-lookup"><span data-stu-id="9e15b-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span></span>

11) <span data-ttu-id="9e15b-975">Busque en el índice de Hola y devolver fragmentos con resultados destacados</span><span class="sxs-lookup"><span data-stu-id="9e15b-975">Search hello index and return fragments with hit highlights</span></span>

    <span data-ttu-id="9e15b-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9e15b-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9e15b-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span><span class="sxs-lookup"><span data-stu-id="9e15b-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span></span>

12) <span data-ttu-id="9e15b-978">Busque en el índice de Hola y devuelva documentos ordenados desde más de cerca toofarther fuera de una ubicación de referencia</span><span class="sxs-lookup"><span data-stu-id="9e15b-978">Search hello index and return documents sorted from closer toofarther away from a reference location</span></span>

    <span data-ttu-id="9e15b-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9e15b-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9e15b-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span><span class="sxs-lookup"><span data-stu-id="9e15b-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span></span>

13) <span data-ttu-id="9e15b-981">Búsqueda Hola índice suponiendo que existe es un perfil de puntuación llamado "geo" con dos funciones de puntuación de distancia, uno define un parámetro llamado "currentLocation" y otro que define un parámetro llamado "lastLocation"</span><span class="sxs-lookup"><span data-stu-id="9e15b-981">Search hello index assuming there's a scoring profile called "geo" with two distance scoring functions, one defining a parameter called "currentLocation" and one defining a parameter called "lastLocation"</span></span>

    <span data-ttu-id="9e15b-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9e15b-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9e15b-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span><span class="sxs-lookup"><span data-stu-id="9e15b-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span></span>

14) <span data-ttu-id="9e15b-984">Buscar documentos en hello índice utilizando [sintaxis de consulta simple](https://msdn.microsoft.com/library/dn798920.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e15b-984">Find documents in hello index using [simple query syntax](https://msdn.microsoft.com/library/dn798920.aspx).</span></span> <span data-ttu-id="9e15b-985">Esta consulta devuelve hoteles donde los campos que permiten búsqueda contienen Hola términos "comodidad" y "ubicación" pero no "motel":</span><span class="sxs-lookup"><span data-stu-id="9e15b-985">This query returns hotels where searchable fields contain hello terms "comfort" and "location" but not "motel":</span></span>

    <span data-ttu-id="9e15b-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9e15b-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9e15b-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="9e15b-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span></span>

<span data-ttu-id="9e15b-988">Tenga en cuenta uso Hola de `searchMode=all` anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9e15b-988">Note hello use of `searchMode=all` above.</span></span> <span data-ttu-id="9e15b-989">Incluir este parámetro invalida el valor predeterminado de Hola de `searchMode=any`, lo que asegura que `-motel` significa "AND NOT" en lugar de "OR NOT".</span><span class="sxs-lookup"><span data-stu-id="9e15b-989">Including this parameter overrides hello default of `searchMode=any`, ensuring that `-motel` means "AND NOT" instead of "OR NOT".</span></span> <span data-ttu-id="9e15b-990">Sin `searchMode=all`, obtendrá "OR NOT" que se expande en lugar de restringe los resultados de búsqueda, y puede ser contraproducente toosome a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="9e15b-990">Without `searchMode=all`, you get "OR NOT" which expands rather than restricts search results, and this can be counter-intuitive toosome users.</span></span>

15) <span data-ttu-id="9e15b-991">Buscar documentos en hello índice utilizando [sintaxis de consulta de lucene](https://msdn.microsoft.com/library/mt589323.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e15b-991">Find documents in hello index using [lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx).</span></span> <span data-ttu-id="9e15b-992">Esta consulta devuelve hoteles donde el campo de categoría hello contiene Hola término "budget" y puede buscar todos los campos que contengan la frase Hola "renovada recientemente".</span><span class="sxs-lookup"><span data-stu-id="9e15b-992">This query returns hotels where hello category field contains hello term "budget" and all searchable fields containing hello phrase "recently renovated".</span></span> <span data-ttu-id="9e15b-993">Documentos que contengan la frase Hola "recientemente reformada" con un rango superior como resultado del valor de aumento de término de hello (3)</span><span class="sxs-lookup"><span data-stu-id="9e15b-993">Documents containing hello phrase "recently renovated" are ranked higher as a result of hello term boost value (3)</span></span>

    <span data-ttu-id="9e15b-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span><span class="sxs-lookup"><span data-stu-id="9e15b-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span></span>

    <span data-ttu-id="9e15b-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="9e15b-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span></span>

<a name="LookupAPI"></a>

## <a name="lookup-document"></a><span data-ttu-id="9e15b-996">Buscar documento</span><span class="sxs-lookup"><span data-stu-id="9e15b-996">Lookup Document</span></span>
<span data-ttu-id="9e15b-997">Hola **búsqueda de documento** operación recupera un documento de búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e15b-997">hello **Lookup Document** operation retrieves a document from Azure Search.</span></span> <span data-ttu-id="9e15b-998">Esto es útil cuando un usuario hace clic en un resultado de búsqueda específico y desea toolook detalles concretos de ese documento.</span><span class="sxs-lookup"><span data-stu-id="9e15b-998">This is useful when a user clicks on a specific search result, and you want toolook up specific details about that document.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

<span data-ttu-id="9e15b-999">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-999">**Request**</span></span>

<span data-ttu-id="9e15b-1000">HTTPS es necesario para las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1000">HTTPS is required for service requests.</span></span> <span data-ttu-id="9e15b-1001">Hola **búsqueda de documento** solicitud se puede generar como sigue.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1001">hello **Lookup Document** request can be constructed as follows.</span></span>

    GET /indexes/[index name]/docs/key?[query parameters]

<span data-ttu-id="9e15b-1002">Como alternativa, puede usar la sintaxis de OData tradicional de Hola para búsqueda de claves:</span><span class="sxs-lookup"><span data-stu-id="9e15b-1002">Alternatively, you can use hello traditional OData syntax for key lookup:</span></span>

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

<span data-ttu-id="9e15b-1003">Hola URI de solicitud incluye un [nombre de índice] y [key], especificar qué tooretrieve documento desde qué índice.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1003">hello request URI includes an [index name] and [key], specifying which document tooretrieve from which index.</span></span> <span data-ttu-id="9e15b-1004">Solamente se puede obtener un documento de cada vez.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1004">You can only get one document at a time.</span></span> <span data-ttu-id="9e15b-1005">Use **búsqueda** tooget varios documentos en una sola solicitud.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1005">Use **Search** tooget multiple documents in a single request.</span></span>

<span data-ttu-id="9e15b-1006">**Parámetros de consulta**</span><span class="sxs-lookup"><span data-stu-id="9e15b-1006">**Query Parameters**</span></span>

<span data-ttu-id="9e15b-1007">`$select=[string]`(opcional): una lista de campos separados por comas tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1007">`$select=[string]` (optional) - a list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="9e15b-1008">Si no se especifica o se establece demasiado`*`, se incluyen todos los campos marcados como recuperables en el esquema de hello en proyección Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1008">If unspecified or set too`*`, all fields marked as retrievable in hello schema are included in hello projection.</span></span>

<span data-ttu-id="9e15b-1009">`api-version=[string]` (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="9e15b-1009">`api-version=[string]` (required).</span></span> <span data-ttu-id="9e15b-1010">versión de vista previa de Hello es `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1010">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9e15b-1011">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1011">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="9e15b-1012">Nota: Para realizar esta operación, Hola `api-version` se especifica como un parámetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1012">Note: For this operation, hello `api-version` is specified as a query parameter.</span></span>

<span data-ttu-id="9e15b-1013">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-1013">**Request Headers**</span></span>

<span data-ttu-id="9e15b-1014">Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1014">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="9e15b-1015">`api-key`: Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1015">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9e15b-1016">Es un valor de cadena único tooyour dirección URL del servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1016">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="9e15b-1017">Hola **búsqueda de documento** solicitud puede especificar una clave de administración o la clave de consulta para `api-key`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1017">hello **Lookup Document** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="9e15b-1018">También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1018">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9e15b-1019">Puede obtener el nombre del servicio de Hola y `api-key` desde el panel de servicio en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1019">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9e15b-1020">Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1020">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9e15b-1021">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-1021">**Request Body**</span></span>

<span data-ttu-id="9e15b-1022">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1022">None.</span></span>

<span data-ttu-id="9e15b-1023">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="9e15b-1023">**Response**</span></span>

<span data-ttu-id="9e15b-1024">Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1024">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      field_name: field_value (fields matching hello default or specified projection)
    }

<span data-ttu-id="9e15b-1025">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="9e15b-1025">**Example**</span></span>

<span data-ttu-id="9e15b-1026">Documento de Hola de búsqueda que tiene la clave '2'</span><span class="sxs-lookup"><span data-stu-id="9e15b-1026">Lookup hello document that has key '2'</span></span>

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

<span data-ttu-id="9e15b-1027">Documento de Hola de búsqueda que tiene la clave "3" utilizando la sintaxis de OData:</span><span class="sxs-lookup"><span data-stu-id="9e15b-1027">Lookup hello document that has key '3' using OData syntax:</span></span>

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a><span data-ttu-id="9e15b-1028">Documentos de recuento</span><span class="sxs-lookup"><span data-stu-id="9e15b-1028">Count Documents</span></span>
<span data-ttu-id="9e15b-1029">Hola **número de documentos** operación recupera un recuento del número de Hola de documentos en un índice de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1029">hello **Count Documents** operation retrieves a count of hello number of documents in a search index.</span></span> <span data-ttu-id="9e15b-1030">Hola `$count` sintaxis forma parte del programa Hola Protocolo OData.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1030">hello `$count` syntax is part of hello OData protocol.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

<span data-ttu-id="9e15b-1031">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-1031">**Request**</span></span>

<span data-ttu-id="9e15b-1032">HTTPS es necesario para las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1032">HTTPS is required for service requests.</span></span> <span data-ttu-id="9e15b-1033">Hola **número de documentos** solicitud puede crearse mediante el método GET de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1033">hello **Count Documents** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="9e15b-1034">Hola [nombre del índice] en el URI de solicitud de hello indica Hola servicio tooreturn un recuento de todos los elementos de colección de documentos de Hola de índice especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1034">hello [index name] in hello request URI tells hello service tooreturn a count of all items in hello docs collection of hello specified index.</span></span>

<span data-ttu-id="9e15b-1035">`api-version=[string]` (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="9e15b-1035">`api-version=[string]` (required).</span></span> <span data-ttu-id="9e15b-1036">versión de vista previa de Hello es `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1036">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9e15b-1037">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1037">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="9e15b-1038">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-1038">**Request Headers**</span></span>

<span data-ttu-id="9e15b-1039">Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1039">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="9e15b-1040">`Accept`: Este valor debe estar establecido demasiado`text/plain`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1040">`Accept`: This value must be set too`text/plain`.</span></span>
* <span data-ttu-id="9e15b-1041">`api-key`: Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1041">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9e15b-1042">Es un valor de cadena único tooyour dirección URL del servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1042">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="9e15b-1043">Hola **número de documentos** solicitud puede especificar una clave de administración o la clave de consulta para `api-key`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1043">hello **Count Documents** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="9e15b-1044">También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1044">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9e15b-1045">Puede obtener el nombre del servicio de Hola y `api-key` desde el panel de servicio en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1045">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9e15b-1046">Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1046">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9e15b-1047">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-1047">**Request Body**</span></span>

<span data-ttu-id="9e15b-1048">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1048">None.</span></span>

<span data-ttu-id="9e15b-1049">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="9e15b-1049">**Response**</span></span>

<span data-ttu-id="9e15b-1050">Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1050">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="9e15b-1051">cuerpo de respuesta de Hello contiene el valor del recuento de Hola como un entero con formato de texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1051">hello response body contains hello count value as an integer formatted in plain text.</span></span>

<a name="Suggestions"></a>

## <a name="suggestions"></a><span data-ttu-id="9e15b-1052">Sugerencias</span><span class="sxs-lookup"><span data-stu-id="9e15b-1052">Suggestions</span></span>
<span data-ttu-id="9e15b-1053">Hola **sugerencias** operación recupera sugerencias basadas en la entrada de búsqueda parcial.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1053">hello **Suggestions** operation retrieves suggestions based on partial search input.</span></span> <span data-ttu-id="9e15b-1054">Normalmente se utiliza en cuadros tooprovide anticipada sugerencias como los usuarios están escribiendo términos de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1054">It's typically used in search boxes tooprovide type-ahead suggestions as users are entering search terms.</span></span>

<span data-ttu-id="9e15b-1055">Solicitudes de sugerencias tienen como fin sugerir documentos de destino, para que hello sugiere texto puede repetirse si varios documentos candidatos coinciden Hola mismo Buscar entrada.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1055">Suggestion requests aim at suggesting target documents, so hello suggested text may be repeated if multiple candidate documents match hello same search input.</span></span> <span data-ttu-id="9e15b-1056">Puede usar `$select` tooretrieve otro documento campos (incluida la clave de documento de hello) por lo que puede indicarle qué documento es el origen de Hola para cada sugerencia.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1056">You can use `$select` tooretrieve other document fields (including hello document key) so that you can tell which document is hello source for each suggestion.</span></span>

<span data-ttu-id="9e15b-1057">Una operación **Sugerencias** se emite como una solicitud GET o POST.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1057">A **Suggestions** operation is issued as a GET or POST request.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="9e15b-1058">**Cuando este tipo de toouse en lugar de obtener**</span><span class="sxs-lookup"><span data-stu-id="9e15b-1058">**When toouse POST instead of GET**</span></span>

<span data-ttu-id="9e15b-1059">Cuando se utiliza HTTP GET toocall hello **sugerencias** API, deberá toobe tenga en cuenta que longitud Hola de dirección URL de solicitud de hello no puede superar los 8 KB.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1059">When you use HTTP GET toocall hello **Suggestions** API, you need toobe aware that hello length of hello request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="9e15b-1060">Esto suele ser suficiente para la mayoría de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1060">This is usually enough for most applications.</span></span> <span data-ttu-id="9e15b-1061">Sin embargo, algunas aplicaciones generan consultas muy extensas, en concreto, expresiones de filtro de OData.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1061">However, some applications produce very large queries, specifically OData filter expressions.</span></span> <span data-ttu-id="9e15b-1062">Para estas aplicaciones, el uso de HTTP POST es una opción mejor porque permite filtros mayores que GET.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1062">For these applications, using HTTP POST is a better choice because it allows larger filters than GET.</span></span> <span data-ttu-id="9e15b-1063">Utiliza el método POST, número Hola de cláusulas de un filtro es el factor de limitación de hello, no Hola tamaño de la cadena de filtro sin procesar de hello como límite de tamaño de hello solicitud de POST es aproximadamente 16 MB.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1063">With POST, hello number of clauses in a filter is hello limiting factor, not hello size of hello raw filter string since hello request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="9e15b-1064">Aunque el límite de tamaño de solicitud POST hello es muy grande, las expresiones de filtro no pueden ser arbitrariamente complejas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1064">Even though hello POST request size limit is very large, filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="9e15b-1065">Consulte [Sintaxis de expresiones de OData para Búsqueda de Azure](https://msdn.microsoft.com/library/dn798921.aspx) para obtener más información sobre las limitaciones de complejidad de filtros.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1065">See [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="9e15b-1066">**Solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-1066">**Request**</span></span>

<span data-ttu-id="9e15b-1067">HTTPS es necesario para las solicitudes de servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1067">HTTPS is required for service requests.</span></span> <span data-ttu-id="9e15b-1068">Hola **sugerencias** solicitud puede crearse mediante Hola GET o métodos POST.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1068">hello **Suggestions** request can be constructed using hello GET or POST methods.</span></span>

<span data-ttu-id="9e15b-1069">URI de solicitud de Hello especifica nombre de Hola de hello tooquery de índice.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1069">hello request URI specifies hello name of hello index tooquery.</span></span> <span data-ttu-id="9e15b-1070">Se especifican parámetros, como término de búsqueda escrito parcialmente de hello, en la cadena de consulta de hello en caso de hello de solicitudes GET y, en la solicitud de hello solicita cuerpo en caso de hello de publicación.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1070">Parameters, such as hello partially input search term, are specified on hello query string in hello case of GET requests, and in hello request body in hello case of POST requests.</span></span>

<span data-ttu-id="9e15b-1071">Como práctica recomendada al crear las solicitudes GET, recuerde demasiado[codifica como URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) consulta específica parámetros cuando se llama a Hola API de REST directamente.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1071">As a best practice when creating GET requests, remember too[URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling hello REST API directly.</span></span> <span data-ttu-id="9e15b-1072">Para las operaciones **Sugerencias** , se incluye lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9e15b-1072">For **Suggestions** operations, this includes:</span></span>

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

<span data-ttu-id="9e15b-1073">Solo se recomienda la codificación de direcciones URL en hello por encima de los parámetros de consulta.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1073">URL encoding is only recommended on hello above query parameters.</span></span> <span data-ttu-id="9e15b-1074">Si se codifica como URL accidentalmente hello cadena de consulta completa (todos los elementos después de hello?), se interrumpirán las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1074">If you inadvertently URL-encode hello entire query string (everything after hello ?), requests will break.</span></span>

<span data-ttu-id="9e15b-1075">Además, la codificación de direcciones URL solo es necesaria cuando se llama a Hola obtener API de REST directamente mediante.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1075">Also, URL encoding is only necessary when calling hello REST API directly using GET.</span></span> <span data-ttu-id="9e15b-1076">Codificación de dirección URL no es necesaria cuando se llama a **sugerencias** mediante POST, o al usar hello [biblioteca de cliente .NET](https://msdn.microsoft.com/library/dn951165.aspx), que controla la codificación de direcciones URL para usted.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1076">No URL encoding is necessary when calling **Suggestions** using POST, or when using hello [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="9e15b-1077">**Parámetros de consulta**</span><span class="sxs-lookup"><span data-stu-id="9e15b-1077">**Query Parameters**</span></span>

<span data-ttu-id="9e15b-1078">**Sugerencias** acepta varios parámetros que ofrecen criterios de consulta y que también especifican el comportamiento de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1078">**Suggestions** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="9e15b-1079">Proporcionar la cadena de consulta de estos parámetros en la dirección URL de hello al llamar a **sugerencias** a través de GET y como propiedades JSON en el cuerpo de la solicitud de hello al llamar a **sugerencias** a través de POST.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1079">You provide these parameters in hello URL query string when calling **Suggestions** via GET, and as JSON properties in hello request body when calling **Suggestions** via POST.</span></span> <span data-ttu-id="9e15b-1080">sintaxis de Hola para algunos parámetros difiere ligeramente entre GET y POST.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1080">hello syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="9e15b-1081">Estas diferencias se indican como aplicables a continuación:</span><span class="sxs-lookup"><span data-stu-id="9e15b-1081">These differences are noted as applicable below:</span></span>

<span data-ttu-id="9e15b-1082">`search=[string]`-Hola toouse toosuggest consultas de búsqueda de texto.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1082">`search=[string]` - hello search text toouse toosuggest queries.</span></span> <span data-ttu-id="9e15b-1083">Debe tener 1 carácter como mínimo y no más de 100 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1083">Must be at least 1 character, and no more than 100 characters.</span></span>

<span data-ttu-id="9e15b-1084">`highlightPreTag=[string]`(opcional): una etiqueta de cadena que se antepone toosearch aciertos.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1084">`highlightPreTag=[string]` (optional) - a string tag that prepends toosearch hits.</span></span> <span data-ttu-id="9e15b-1085">Debe establecerse con `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1085">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="9e15b-1086">Al llamar a **sugerencias** con GET, caracteres reservados en la dirección URL de hello deben estar codificados en porcentaje (por ejemplo, % 23 en lugar de #).</span><span class="sxs-lookup"><span data-stu-id="9e15b-1086">When calling **Suggestions** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="9e15b-1087">`highlightPostTag=[string]`(opcional): una etiqueta de cadena que se anexa toosearch aciertos.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1087">`highlightPostTag=[string]` (optional) - a string tag that appends toosearch hits.</span></span> <span data-ttu-id="9e15b-1088">Debe establecerse con `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1088">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="9e15b-1089">Al llamar a **sugerencias** con GET, caracteres reservados en la dirección URL de hello deben estar codificados en porcentaje (por ejemplo, % 23 en lugar de #).</span><span class="sxs-lookup"><span data-stu-id="9e15b-1089">When calling **Suggestions** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="9e15b-1090">`suggesterName=[string]`-nombre de hello del proveedor de sugerencias de hello como Hola especificado en `suggesters` colección que forma parte de la definición del índice Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1090">`suggesterName=[string]` - hello name of hello suggester as specified in hello `suggesters` collection that's part of hello index definition.</span></span> <span data-ttu-id="9e15b-1091">Un `suggester` determina qué campos se analizan para encontrar términos de consulta sugeridos.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1091">A `suggester` determines which fields are scanned for suggested query terms.</span></span> <span data-ttu-id="9e15b-1092">Consulte [Proveedores de sugerencias](#Suggesters) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1092">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="9e15b-1093">`fuzzy=[boolean]`(opcional, el valor predeterminado = false)-tootrue cuando se establece esta API encontrará sugerencias incluso si hay un carácter sustituye o falta en el texto de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1093">`fuzzy=[boolean]` (optional, default = false) - when set tootrue this API will find suggestions even if there's a substituted or missing character in hello search text.</span></span> <span data-ttu-id="9e15b-1094">Si bien esto proporciona una mejor experiencia en algunos escenarios, ello afecta al rendimiento, ya que las búsquedas de sugerencias aproximadas son más lentas y consumen más recursos.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1094">While this provides a better experience in some scenarios it comes at a performance cost as fuzzy suggestion searches are slower and consume more resources.</span></span>

<span data-ttu-id="9e15b-1095">`searchFields=[string]`(opcional): lista de Hola de toosearch de nombres de campo separados por comas para hello especifica el texto de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1095">`searchFields=[string]` (optional) - hello list of comma-separated field names toosearch for hello specified search text.</span></span> <span data-ttu-id="9e15b-1096">Los campos de destino deben estar habilitados para obtener sugerencias.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1096">Target fields must be enabled for suggestions.</span></span>

<span data-ttu-id="9e15b-1097">`$top=#`(opcional, el valor predeterminado = 5)-número de sugerencias tooretrieve de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1097">`$top=#` (optional, default = 5) - hello number of suggestions tooretrieve.</span></span> <span data-ttu-id="9e15b-1098">Debe ser un número entre 1 y 100.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1098">Must be a number between 1 and 100.</span></span>

> [!NOTE]
> <span data-ttu-id="9e15b-1099">Al llamar a las **sugerencias** mediante POST, este parámetro se denomina `top` en lugar de `$top`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1099">When calling **Suggestions** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="9e15b-1100">`$filter=[string]`(opcional): una expresión que filtra los documentos de hello considerados para obtener sugerencias.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1100">`$filter=[string]` (optional) - an expression that filters hello documents considered for suggestions.</span></span>

> [!NOTE]
> <span data-ttu-id="9e15b-1101">Al llamar a las **sugerencias** mediante POST, este parámetro se denomina `filter` en lugar de `$filter`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1101">When calling **Suggestions** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="9e15b-1102">`$orderby=[string]`(opcional): una lista de expresiones separadas por comas toosort Hola resultados por.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1102">`$orderby=[string]` (optional) - a list of comma-separated expressions toosort hello results by.</span></span> <span data-ttu-id="9e15b-1103">Cada expresión puede ser un nombre de campo o una llamada toohello `geo.distance()` función.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1103">Each expression can be either a field name or a call toohello `geo.distance()` function.</span></span> <span data-ttu-id="9e15b-1104">Cada expresión puede ir seguida de `asc` tooindicated ascendente, y `desc` tooindicate descendente.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1104">Each expression can be followed by `asc` tooindicated ascending, and `desc` tooindicate descending.</span></span> <span data-ttu-id="9e15b-1105">valor predeterminado de Hello es ascendente.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1105">hello default is ascending order.</span></span> <span data-ttu-id="9e15b-1106">Hay un límite de 32 cláusulas para `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1106">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="9e15b-1107">Al llamar a las **sugerencias** mediante POST, este parámetro se denomina `orderby` en lugar de `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1107">When calling **Suggestions** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="9e15b-1108">`$select=[string]`(opcional): una lista de campos separados por comas tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1108">`$select=[string]` (optional) - a list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="9e15b-1109">Si no se especifica, solo Hola clave de documento y se devuelve el texto de sugerencia.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1109">If unspecified, only hello document key and suggestion text is returned.</span></span> <span data-ttu-id="9e15b-1110">Puede solicitar explícitamente todos los campos, establezca este parámetro demasiado`*`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1110">You can explicitly request all fields by setting this parameter too`*`.</span></span>

> [!NOTE]
> <span data-ttu-id="9e15b-1111">Al llamar a las **sugerencias** mediante POST, este parámetro se denomina `select` en lugar de `$select`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1111">When calling **Suggestions** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="9e15b-1112">`minimumCoverage`(opcional, tiene como valor predeterminado too80) - un número entre 0 y 100 que indica el porcentaje Hola de índice de Hola que debe ser abarcado por una consulta de sugerencias en orden para hello consulta toobe notificarse como tales.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1112">`minimumCoverage` (optional, defaults too80) - a number between 0 and 100 indicating hello percentage of hello index that must be covered by a suggestions query in order for hello query toobe reported as a success.</span></span> <span data-ttu-id="9e15b-1113">De forma predeterminada, debe estar disponible al menos el 80% del índice de Hola o `Suggest` se devolverá el código de estado HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1113">By default, at least 80% of hello index must be available or `Suggest` will return HTTP status code 503.</span></span> <span data-ttu-id="9e15b-1114">Si establece `minimumCoverage` y `Suggest` se realiza correctamente, devolverá HTTP 200 e incluyen una `@search.coverage` valor de respuesta de Hola que indica el porcentaje de Hola de índice de Hola que se incluyó en la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1114">If you set `minimumCoverage` and `Suggest` succeeds, it will return HTTP 200 and include a `@search.coverage` value in hello response indicating hello percentage of hello index that was included in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="9e15b-1115">Establecer este valor de parámetro tooa menor que 100 puede ser útil para garantizar la disponibilidad de búsqueda incluso para servicios con una única réplica.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1115">Setting this parameter tooa value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="9e15b-1116">Sin embargo, no todas las sugerencias de búsqueda de coincidencias se garantiza que toobe presente en los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1116">However, not all matching suggestions are guaranteed toobe present in hello results.</span></span> <span data-ttu-id="9e15b-1117">Si la recuperación es más importante aplicación de tooyour de disponibilidad, entonces es mejor no toolower `minimumCoverage` por debajo de su valor predeterminado de 80.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1117">If recall is more important tooyour application than availability, then it's best not toolower `minimumCoverage` below its default value of 80.</span></span>
> 
> 

<span data-ttu-id="9e15b-1118">`api-version=[string]` (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="9e15b-1118">`api-version=[string]` (required).</span></span> <span data-ttu-id="9e15b-1119">versión de vista previa de Hello es `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1119">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9e15b-1120">Consulte [Versiones del servicio de búsqueda](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obtener más información y versiones alternativas.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1120">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="9e15b-1121">Nota: Para realizar esta operación, Hola `api-version` se especifica como un parámetro de consulta de dirección URL de hello independientemente de si se llama a **sugerencias** con GET o POST.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1121">Note: For this operation, hello `api-version` is specified as a query parameter in hello URL regardless of whether you call **Suggestions** with GET or POST.</span></span>

<span data-ttu-id="9e15b-1122">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-1122">**Request Headers**</span></span>

<span data-ttu-id="9e15b-1123">Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales</span><span class="sxs-lookup"><span data-stu-id="9e15b-1123">hello following list describes hello required and optional request headers</span></span>

* <span data-ttu-id="9e15b-1124">`api-key`: Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1124">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9e15b-1125">Es un valor de cadena único tooyour dirección URL del servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1125">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="9e15b-1126">Hola **sugerencias** solicitud puede especificar una clave de administración o la clave de consulta como hello `api-key`.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1126">hello **Suggestions** request can specify either an admin key or query key as hello `api-key`.</span></span>

<span data-ttu-id="9e15b-1127">También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1127">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9e15b-1128">Puede obtener el nombre del servicio de Hola y `api-key` desde el panel de servicio en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1128">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9e15b-1129">Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1129">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9e15b-1130">**Cuerpo de la solicitud**</span><span class="sxs-lookup"><span data-stu-id="9e15b-1130">**Request Body**</span></span>

<span data-ttu-id="9e15b-1131">Para GET: ninguno.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1131">For GET: None.</span></span>

<span data-ttu-id="9e15b-1132">Para POST:</span><span class="sxs-lookup"><span data-stu-id="9e15b-1132">For POST:</span></span>

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

<span data-ttu-id="9e15b-1133">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="9e15b-1133">**Response**</span></span>

<span data-ttu-id="9e15b-1134">Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.</span><span class="sxs-lookup"><span data-stu-id="9e15b-1134">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

<span data-ttu-id="9e15b-1135">Si es de opción de proyección de hello tooretrieve usado campos se incluyen en cada elemento de matriz de hello:</span><span class="sxs-lookup"><span data-stu-id="9e15b-1135">If hello projection option is used tooretrieve fields they are included in each element of hello array:</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

<span data-ttu-id="9e15b-1136">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="9e15b-1136">**Example**</span></span>

<span data-ttu-id="9e15b-1137">Recuperar 5 sugerencias donde hello entrada de búsqueda parcial es 'lux'</span><span class="sxs-lookup"><span data-stu-id="9e15b-1137">Retrieve 5 suggestions where hello partial search input is 'lux'</span></span>

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
