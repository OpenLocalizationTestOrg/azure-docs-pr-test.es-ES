---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "La documentación preliminar de la característica Sinónimos (versión preliminar), expuesta en la API de REST de Azure Search."
services: search
documentationCenter: 
authors: mhko
manager: pablocas
editor: 
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/07/2016
ms.author: nateko
ms.openlocfilehash: 739a0ad77c68ea74ec25bc80c7539ac8b3f18201
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="synonyms-in-azure-search-preview"></a><span data-ttu-id="89840-102">Sinónimos en Azure Search (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="89840-102">Synonyms in Azure Search (preview)</span></span>

<span data-ttu-id="89840-103">Los sinónimos de los motores de búsqueda asocian términos equivalentes que expanden implícitamente el ámbito de una consulta, sin que el usuario tenga que proporcionar realmente el término.</span><span class="sxs-lookup"><span data-stu-id="89840-103">Synonyms in search engines associate equivalent terms that implicitly expand the scope of a query, without the user having to actually provide the term.</span></span> <span data-ttu-id="89840-104">Por ejemplo, con el término "perro" y las asociaciones de sinónimos de "canino" y "cachorro", los documentos que contengan los términos "perro", "canino" o "cachorro" estarán dentro del ámbito de la consulta.</span><span class="sxs-lookup"><span data-stu-id="89840-104">For example, given the term "dog" and synonym associations of "canine" and "puppy", any documents containing "dog", "canine" or "puppy" will fall within the scope of the query.</span></span>

<span data-ttu-id="89840-105">En Azure Search, la expansión de sinónimos se realiza en el momento de la consulta.</span><span class="sxs-lookup"><span data-stu-id="89840-105">In Azure Search, synonym expansion is done at query time.</span></span> <span data-ttu-id="89840-106">Puede agregar asignaciones de sinónimos a un servicio sin que se interrumpan las operaciones existentes.</span><span class="sxs-lookup"><span data-stu-id="89840-106">You can add synonym maps to a service with no disruption to existing operations.</span></span> <span data-ttu-id="89840-107">Puede agregar una propiedad **synonymMaps** a una definición de campo sin tener que volver a crear un índice.</span><span class="sxs-lookup"><span data-stu-id="89840-107">You can add a  **synonymMaps** property to a field definition without having to rebuild the index.</span></span> <span data-ttu-id="89840-108">Para más información, vea [Actualización de índice](https://docs.microsoft.com/rest/api/searchservice/update-index).</span><span class="sxs-lookup"><span data-stu-id="89840-108">For more information, see [Update Index](https://docs.microsoft.com/rest/api/searchservice/update-index).</span></span>

## <a name="feature-availability"></a><span data-ttu-id="89840-109">Disponibilidad de características</span><span class="sxs-lookup"><span data-stu-id="89840-109">Feature availability</span></span>

<span data-ttu-id="89840-110">La característica Sinónimos está actualmente en la versión preliminar y solo es compatible con la versión de la API de versión preliminar más reciente (api-version=2016-09-01-Preview).</span><span class="sxs-lookup"><span data-stu-id="89840-110">The synonyms feature is currently in preview and only supported in the latest preview api-version (api-version=2016-09-01-Preview).</span></span> <span data-ttu-id="89840-111">En este momento no es compatible con Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="89840-111">There is no Azure portal support at this time.</span></span> <span data-ttu-id="89840-112">Puesto que la versión de la API se especifica en la solicitud, es posible combinar API de versión preliminar y disponibles en general en la misma aplicación.</span><span class="sxs-lookup"><span data-stu-id="89840-112">Because the API version is specified on the request, it's possible to combine generally available (GA) and preview APIs in the same app.</span></span> <span data-ttu-id="89840-113">Sin embargo, la versión preliminar de las API no se someten a las condiciones del Acuerdo de Nivel de Servicio y sus características pueden cambiar, por lo que no se recomienda su uso en aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="89840-113">However, preview APIs are not under SLA and features may change, so we do not recommend using them in production applications.</span></span>

## <a name="how-to-use-synonyms-in-azure-search"></a><span data-ttu-id="89840-114">Cómo utilizar sinónimos en Azure Search</span><span class="sxs-lookup"><span data-stu-id="89840-114">How to use synonyms in Azure search</span></span>

<span data-ttu-id="89840-115">En Azure Search, la compatibilidad de los sinónimos se basa en las asignaciones de sinónimos que defina y cargue en el servicio.</span><span class="sxs-lookup"><span data-stu-id="89840-115">In Azure Search, synonym support is based on synonym maps that you define and upload to your service.</span></span> <span data-ttu-id="89840-116">Estas asignaciones constituyen un recurso independiente (como índices u orígenes de datos), y cualquier campo buscable puede usarlas en cualquier índice en el servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="89840-116">These maps constitute an independent resource (like indexes or data sources), and can be used by any searchable field in any index in your search service.</span></span>

<span data-ttu-id="89840-117">Los índices y asignaciones de sinónimos se mantienen de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="89840-117">Synonym maps and indexes are maintained independently.</span></span> <span data-ttu-id="89840-118">Una vez que defina una asignación de sinónimos y la cargue en el servicio, podrá habilitar la característica Sinónimos en un campo agregando una nueva propiedad denominada **synonymMaps** en la definición del campo.</span><span class="sxs-lookup"><span data-stu-id="89840-118">Once you define a synonym map and upload it to your service, you can enable the synonym feature on a field by adding a new property called **synonymMaps** in the field definition.</span></span> <span data-ttu-id="89840-119">La creación, carga y eliminación de una asignación de sinónimos es siempre una operación de documento completo, lo que significa que no puede crear, actualizar o eliminar partes de la asignación de sinónimos de forma incremental.</span><span class="sxs-lookup"><span data-stu-id="89840-119">Creating, updating, and deleting a synonym map is always a whole-document operation, meaning that you cannot create, update or delete parts of the synonym map incrementally.</span></span> <span data-ttu-id="89840-120">La actualización de incluso una entrada única requiere que se vuelva a cargar.</span><span class="sxs-lookup"><span data-stu-id="89840-120">Updating even a single entry requires a reload.</span></span>

<span data-ttu-id="89840-121">La incorporación de sinónimos en la aplicación de búsqueda es un proceso de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="89840-121">Incorporating synonyms into your search application is a two-step process:</span></span>

1.  <span data-ttu-id="89840-122">Agregar una asignación de sinónimos al servicio de búsqueda a través de las API siguientes.</span><span class="sxs-lookup"><span data-stu-id="89840-122">Add a synonym map to your search service through the APIs below.</span></span>  

2.  <span data-ttu-id="89840-123">Configurar un campo buscable para usar la asignación de sinónimos en la definición del índice.</span><span class="sxs-lookup"><span data-stu-id="89840-123">Configure a searchable field to use the synonym map in the index definition.</span></span>

### <a name="synonymmaps-resource-apis"></a><span data-ttu-id="89840-124">API de recursos de SynonymMaps</span><span class="sxs-lookup"><span data-stu-id="89840-124">SynonymMaps Resource APIs</span></span>

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a><span data-ttu-id="89840-125">Adición o actualización de una asignación de sinónimos en su servicio, con POST o PUT</span><span class="sxs-lookup"><span data-stu-id="89840-125">Add or update a synonym map under your service, using POST or PUT.</span></span>

<span data-ttu-id="89840-126">Las asignaciones de sinónimos se cargan en el servicio a través de POST o PUT.</span><span class="sxs-lookup"><span data-stu-id="89840-126">Synonym maps are uploaded to the service via POST or PUT.</span></span> <span data-ttu-id="89840-127">Cada regla debe estar delimitada por el nuevo carácter de línea ('\n').</span><span class="sxs-lookup"><span data-stu-id="89840-127">Each rule must be delimited by the new line character ('\n').</span></span> <span data-ttu-id="89840-128">Puede definir hasta 5000 reglas por asignación de sinónimos en un servicio gratuito y 10 000 reglas en las demás SKU.</span><span class="sxs-lookup"><span data-stu-id="89840-128">You can define up to 5,000 rules per synonym map in a free service and 10,000 rules in all other SKUs.</span></span> <span data-ttu-id="89840-129">Cada regla puede tener hasta 20 expansiones.</span><span class="sxs-lookup"><span data-stu-id="89840-129">Each rule can have up to 20 expansions.</span></span>

<span data-ttu-id="89840-130">En esta versión preliminar, las asignaciones de sinónimos deben estar en formato Apache Solr, que se explica a continuación.</span><span class="sxs-lookup"><span data-stu-id="89840-130">In this preview, synonym maps must be in the Apache Solr format which is explained below.</span></span> <span data-ttu-id="89840-131">Si dispone de un diccionario de sinónimos existente en un formato distinto y desea usarlo directamente, háganoslo saber en [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="89840-131">If you have an existing synonym dictionary in a different format and want to use it directly, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

<span data-ttu-id="89840-132">Puede crear una nueva asignación de sinónimos con HTTP POST, como en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="89840-132">You can create a new synonym map using HTTP POST, as in the following example:</span></span>

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

<span data-ttu-id="89840-133">De forma alternativa, puede usar PUT y especificar el nombre de asignación del sinónimo en el identificador URI.</span><span class="sxs-lookup"><span data-stu-id="89840-133">Alternatively, you can use PUT and specify the synonym map name on the URI.</span></span> <span data-ttu-id="89840-134">Si la asignación de sinónimos no existe, se creará.</span><span class="sxs-lookup"><span data-stu-id="89840-134">If the synonym map does not exist, it will be created.</span></span>

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a><span data-ttu-id="89840-135">Formato de sinónimos de Apache</span><span class="sxs-lookup"><span data-stu-id="89840-135">Apache Solr synonym format</span></span>

<span data-ttu-id="89840-136">El formato Solr es compatible con asignaciones de sinónimos equivalentes y explícitos.</span><span class="sxs-lookup"><span data-stu-id="89840-136">The Solr format supports equivalent and explicit synonym mappings.</span></span> <span data-ttu-id="89840-137">Las reglas de asignación se adhieren a la especificación del filtro de sinónimos de código abierto de Apache Solr descrita en este documento: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span><span class="sxs-lookup"><span data-stu-id="89840-137">Mapping rules adhere to the open source synonym filter specification of Apache Solr, described in this document: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span></span> <span data-ttu-id="89840-138">A continuación se muestra una regla de ejemplo para los sinónimos equivalentes.</span><span class="sxs-lookup"><span data-stu-id="89840-138">Below is a sample rule for equivalent synonyms.</span></span>
```
              USA, United States, United States of America
```

<span data-ttu-id="89840-139">Con la regla anterior, la consulta de búsqueda "EE. UU." se ampliará a "EE. UU." O "Estados Unidos" O "Estados Unidos de América".</span><span class="sxs-lookup"><span data-stu-id="89840-139">With the rule above, a search query "USA" will expand to "USA" OR "United States" OR "United States of America".</span></span>

<span data-ttu-id="89840-140">La asignación explícita se denota mediante una flecha "=>".</span><span class="sxs-lookup"><span data-stu-id="89840-140">Explicit mapping is denoted by an arrow "=>".</span></span> <span data-ttu-id="89840-141">Cuando se especifica, una secuencia de términos de una consulta de búsqueda que coincide con el lateral izquierdo de "=>" se sustituirá por las alternativas de la derecha.</span><span class="sxs-lookup"><span data-stu-id="89840-141">When specified, a term sequence of a search query that matches the left hand side of "=>" will be replaced with the alternatives on the right hand side.</span></span> <span data-ttu-id="89840-142">Según la regla siguiente, las consultas de búsqueda "Washington", "Wash."</span><span class="sxs-lookup"><span data-stu-id="89840-142">Given the rule below, search queries "Washington", "Wash."</span></span> <span data-ttu-id="89840-143">o "WA" se reescribirán a "WA".</span><span class="sxs-lookup"><span data-stu-id="89840-143">or "WA" will all be rewritten to "WA".</span></span> <span data-ttu-id="89840-144">La asignación explícita solo se aplica en la dirección especificada y no reescribe la consulta "WA" a "Washington" en este caso.</span><span class="sxs-lookup"><span data-stu-id="89840-144">Explicit mapping only applies in the direction specified and does not rewrite the query "WA" to "Washington" in this case.</span></span>
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a><span data-ttu-id="89840-145">Enumeración de asignaciones de sinónimos en su servicio</span><span class="sxs-lookup"><span data-stu-id="89840-145">List synonym maps under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a><span data-ttu-id="89840-146">Obtención de la asignación de sinónimos en su servicio</span><span class="sxs-lookup"><span data-stu-id="89840-146">Get a synonym map under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a><span data-ttu-id="89840-147">Eliminación de la asignación de sinónimos en su servicio</span><span class="sxs-lookup"><span data-stu-id="89840-147">Delete a synonyms map under your service.</span></span>

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-to-use-the-synonym-map-in-the-index-definition"></a><span data-ttu-id="89840-148">Configuración de un campo buscable para usar la asignación de sinónimos en la definición del índice</span><span class="sxs-lookup"><span data-stu-id="89840-148">Configure a searchable field to use the synonym map in the index definition.</span></span>

<span data-ttu-id="89840-149">Puede usarse una nueva propiedad de campo **synonymMaps** para especificar una asignación de sinónimos que usar para un campo buscable.</span><span class="sxs-lookup"><span data-stu-id="89840-149">A new field property **synonymMaps** can be used to specify a synonym map to use for a searchable field.</span></span> <span data-ttu-id="89840-150">Las asignaciones de sinónimos son recursos de nivel de servicio y puede hacerse referencia a ellas mediante cualquier campo del índice en el servicio.</span><span class="sxs-lookup"><span data-stu-id="89840-150">Synonym maps are service level resources and can be referenced by any field of an index under the service.</span></span>

    POST https://[servicename].search.windows.net/indexes?api-version=2016-09-01-Preview
    api-key: [admin key]

    {
       "name":"myindex",
       "fields":[
          {
             "name":"id",
             "type":"Edm.String",
             "key":true
          },
          {
             "name":"name",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"en.lucene",
             "synonymMaps":[
                "mysynonymmap"
             ]
          },
          {
             "name":"name_jp",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"ja.microsoft",
             "synonymMaps":[
                "japanesesynonymmap"
             ]
          }
       ]
    }

<span data-ttu-id="89840-151">**synonymMaps** puede especificarse para los campos buscables del tipo 'Edm.String' o 'Collection(Edm.String)'.</span><span class="sxs-lookup"><span data-stu-id="89840-151">**synonymMaps** can be specified for searchable fields of the type 'Edm.String' or 'Collection(Edm.String)'.</span></span>

> [!NOTE]
> <span data-ttu-id="89840-152">En esta versión preliminar, solo puede tener una asignación de sinónimos por campo.</span><span class="sxs-lookup"><span data-stu-id="89840-152">In this preview, you can only have one synonym map per field.</span></span> <span data-ttu-id="89840-153">Si desea usar varias asignaciones de sinónimos, indíquenoslo en [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="89840-153">If you want to use multiple synonym maps, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

## <a name="impact-of-synonyms-on-other-search-features"></a><span data-ttu-id="89840-154">Repercusión de Sinónimos en otras características de búsqueda</span><span class="sxs-lookup"><span data-stu-id="89840-154">Impact of synonyms on other search features</span></span>

<span data-ttu-id="89840-155">La característica Sinónimos reescribe la consulta original con sinónimos con el operador OR.</span><span class="sxs-lookup"><span data-stu-id="89840-155">The synonyms feature rewrites the original query with synonyms with the OR operator.</span></span> <span data-ttu-id="89840-156">Por este motivo, el resaltado de referencias y los perfiles de puntuación tratan el término original y los sinónimos como equivalentes.</span><span class="sxs-lookup"><span data-stu-id="89840-156">For this reason, hit highlighting and scoring profiles treat the original term and synonyms as equivalent.</span></span>

<span data-ttu-id="89840-157">La característica Sinónimos se aplica a consultas de búsquedas y no se aplica a filtros o facetas.</span><span class="sxs-lookup"><span data-stu-id="89840-157">Synonym feature applies to search queries and does not apply to filters or facets.</span></span> <span data-ttu-id="89840-158">De forma similar, las sugerencias se basan solo en el término original; las coincidencias de sinónimos no aparecen en la respuesta.</span><span class="sxs-lookup"><span data-stu-id="89840-158">Similarly, suggestions are based only on the original term; synonym matches do not appear in the response.</span></span>

<span data-ttu-id="89840-159">Las expansiones de sinónimos no se aplican a los términos de búsqueda de carácter comodín; los prefijos, las coincidencias parciales y las regex no se expanden.</span><span class="sxs-lookup"><span data-stu-id="89840-159">Synonym expansions do not apply to wildcard search terms; prefix, fuzzy, and regex terms aren't expanded.</span></span>

## <a name="tips-for-building-a-synonym-map"></a><span data-ttu-id="89840-160">Consejos para crear un asignación de sinónimos</span><span class="sxs-lookup"><span data-stu-id="89840-160">Tips for building a synonym map</span></span>

- <span data-ttu-id="89840-161">Una asignación de sinónimos concisa y bien diseñada es más eficiente que una lista exhaustiva de posibles coincidencias.</span><span class="sxs-lookup"><span data-stu-id="89840-161">A concise, well-designed synonym map is more efficient than an exhaustive list of possible matches.</span></span> <span data-ttu-id="89840-162">Unos diccionarios excesivamente grandes o complejos tardan más en analizarse y afectan a la latencia de la consulta si esta se expande a muchos sinónimos.</span><span class="sxs-lookup"><span data-stu-id="89840-162">Excessively large or complex dictionaries take longer to parse and affect the query latency if the query expands to many synonyms.</span></span> <span data-ttu-id="89840-163">En lugar de adivinar qué términos pueden usarse, puede obtener los verdaderos términos a través de un [informe de análisis de tráfico de búsqueda](search-traffic-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="89840-163">Rather than guess at which terms might be used, you can get the actual terms via a [search traffic analysis report](search-traffic-analytics.md).</span></span>

- <span data-ttu-id="89840-164">Como ejercicio preliminar y de validación, habilite y luego use este informe para determinar de forma precisa qué términos se beneficiarán de una coincidencia de sinónimo y, a continuación, siga usándolo como validación de que la asignación de sinónimos está generando un mejor resultado.</span><span class="sxs-lookup"><span data-stu-id="89840-164">As both a preliminary and validation exercise, enable and then use this report to precisely determine which terms will benefit from a synonym match, and then continue to use it as validation that your synonym map is producing a better outcome.</span></span> <span data-ttu-id="89840-165">En el informe predefinido, los iconos "Consultas de búsquedas más comunes" y "Consultas de búsqueda con resultado cero" le proporcionarán la información necesaria.</span><span class="sxs-lookup"><span data-stu-id="89840-165">In the predefined report, the tiles "Most common search queries" and "Zero-result search queries" will give you the necessary information.</span></span>

- <span data-ttu-id="89840-166">Puede crear varias asignaciones para la aplicación de búsqueda (por ejemplo, mediante el idioma si la aplicación es compatible con una base de cliente de varios idiomas).</span><span class="sxs-lookup"><span data-stu-id="89840-166">You can create multiple synonym maps for your search application (for example, by language if your application supports a multi-lingual customer base).</span></span> <span data-ttu-id="89840-167">Actualmente, un campo solo puede usar una de ellas.</span><span class="sxs-lookup"><span data-stu-id="89840-167">Currently, a field can only use one of them.</span></span> <span data-ttu-id="89840-168">Puede actualizar una propiedad synonymMaps del campo en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="89840-168">You can update a field's synonymMaps property at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89840-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="89840-169">Next Steps</span></span>

- <span data-ttu-id="89840-170">Si dispone de un índice existente en un entorno de desarrollo (no producción), experimente con un diccionario pequeño para ver cómo la adición de sinónimos cambia la experiencia de búsqueda, incluida la repercusión en los perfiles de puntuación, el resaltado de referencias y las sugerencias.</span><span class="sxs-lookup"><span data-stu-id="89840-170">If you have an existing index in a development (non-production) environment, experiment with a small dictionary to see how the addition of synonyms changes the search experience, including impact on scoring profiles, hit highlighting, and suggestions.</span></span>

- <span data-ttu-id="89840-171">[Habilite el análisis de tráfico de búsqueda](search-traffic-analytics.md) y use el informe de Power BI predefinido para conocer qué términos se usan con mayor frecuencia y cuáles devuelven cero documentos.</span><span class="sxs-lookup"><span data-stu-id="89840-171">[Enable search traffic analytics](search-traffic-analytics.md) and use the predefined Power BI report to learn which terms are used the most, and which ones return zero documents.</span></span> <span data-ttu-id="89840-172">Con estos datos, revise el diccionario para incluir sinónimos para consultas que no sean productivas que deban resolverse en documentos en su índice.</span><span class="sxs-lookup"><span data-stu-id="89840-172">Armed with these insights, revise the dictionary to include synonyms for unproductive queries that should be resolving to documents in your index.</span></span>
