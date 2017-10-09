---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Documentación preliminar de característica de sinónimos (vista previa) de hello, expuesta en hello API de REST de búsqueda de Azure."
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
ms.openlocfilehash: 2695139d2b298fa2e7c1814715fdf96729f594ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="synonyms-in-azure-search-preview"></a><span data-ttu-id="b3160-102">Sinónimos en Azure Search (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="b3160-102">Synonyms in Azure Search (preview)</span></span>

<span data-ttu-id="b3160-103">Sinónimos en los motores de búsqueda asocian términos equivalentes que se expanden implícitamente ámbito Hola de una consulta, sin que el usuario de hello tener tooactually proporcionar término Hola.</span><span class="sxs-lookup"><span data-stu-id="b3160-103">Synonyms in search engines associate equivalent terms that implicitly expand hello scope of a query, without hello user having tooactually provide hello term.</span></span> <span data-ttu-id="b3160-104">Por ejemplo, hello determinado término "dog" y las asociaciones de sinónimos de "perro" y "cachorro", todos los documentos que contengan "dog", "perro" o "cachorro" entrarán en ámbito de Hola de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3160-104">For example, given hello term "dog" and synonym associations of "canine" and "puppy", any documents containing "dog", "canine" or "puppy" will fall within hello scope of hello query.</span></span>

<span data-ttu-id="b3160-105">En Azure Search, la expansión de sinónimos se realiza en el momento de la consulta.</span><span class="sxs-lookup"><span data-stu-id="b3160-105">In Azure Search, synonym expansion is done at query time.</span></span> <span data-ttu-id="b3160-106">Puede agregar sinónimo mapas tooa servicio con ninguna operación de tooexisting de interrupción.</span><span class="sxs-lookup"><span data-stu-id="b3160-106">You can add synonym maps tooa service with no disruption tooexisting operations.</span></span> <span data-ttu-id="b3160-107">Puede agregar un **synonymMaps** definición de campo de propiedad tooa sin necesidad de índice de hello toorebuild.</span><span class="sxs-lookup"><span data-stu-id="b3160-107">You can add a  **synonymMaps** property tooa field definition without having toorebuild hello index.</span></span> <span data-ttu-id="b3160-108">Para más información, vea [Actualización de índice](https://docs.microsoft.com/rest/api/searchservice/update-index).</span><span class="sxs-lookup"><span data-stu-id="b3160-108">For more information, see [Update Index](https://docs.microsoft.com/rest/api/searchservice/update-index).</span></span>

## <a name="feature-availability"></a><span data-ttu-id="b3160-109">Disponibilidad de características</span><span class="sxs-lookup"><span data-stu-id="b3160-109">Feature availability</span></span>

<span data-ttu-id="b3160-110">sinónimos de Hello característica está actualmente en vista previa y solo es compatible en Hola versión de api de vista previa más reciente (api-version = 2016-09-01-versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="b3160-110">hello synonyms feature is currently in preview and only supported in hello latest preview api-version (api-version=2016-09-01-Preview).</span></span> <span data-ttu-id="b3160-111">En este momento no es compatible con Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b3160-111">There is no Azure portal support at this time.</span></span> <span data-ttu-id="b3160-112">Porque se especifica la versión de API de hello en solicitud de hello, es posible toocombine disponible con carácter general (GA) y API de vista previa en hello misma aplicación.</span><span class="sxs-lookup"><span data-stu-id="b3160-112">Because hello API version is specified on hello request, it's possible toocombine generally available (GA) and preview APIs in hello same app.</span></span> <span data-ttu-id="b3160-113">Sin embargo, la versión preliminar de las API no se someten a las condiciones del Acuerdo de Nivel de Servicio y sus características pueden cambiar, por lo que no se recomienda su uso en aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="b3160-113">However, preview APIs are not under SLA and features may change, so we do not recommend using them in production applications.</span></span>

## <a name="how-toouse-synonyms-in-azure-search"></a><span data-ttu-id="b3160-114">Cómo buscar sinónimos toouse en Azure</span><span class="sxs-lookup"><span data-stu-id="b3160-114">How toouse synonyms in Azure search</span></span>

<span data-ttu-id="b3160-115">En búsqueda de Azure, compatibilidad con sinónimos se basa en los mapas de sinónimo que define y cargar el servicio tooyour.</span><span class="sxs-lookup"><span data-stu-id="b3160-115">In Azure Search, synonym support is based on synonym maps that you define and upload tooyour service.</span></span> <span data-ttu-id="b3160-116">Estas asignaciones constituyen un recurso independiente (como índices u orígenes de datos), y cualquier campo buscable puede usarlas en cualquier índice en el servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="b3160-116">These maps constitute an independent resource (like indexes or data sources), and can be used by any searchable field in any index in your search service.</span></span>

<span data-ttu-id="b3160-117">Los índices y asignaciones de sinónimos se mantienen de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="b3160-117">Synonym maps and indexes are maintained independently.</span></span> <span data-ttu-id="b3160-118">Una vez que se define un mapa de sinónimo y cargarlo tooyour servicio, puede habilitar característica de sinónimo de hello en un campo mediante la adición de una nueva propiedad llamada **synonymMaps** en la definición de campo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3160-118">Once you define a synonym map and upload it tooyour service, you can enable hello synonym feature on a field by adding a new property called **synonymMaps** in hello field definition.</span></span> <span data-ttu-id="b3160-119">Crear, actualizar y eliminar que una asignación de sinónimo siempre es una operación de documento de enteros, lo que significa que no se puede crear, actualización o eliminen elementos de mapa de sinónimo Hola incrementalmente.</span><span class="sxs-lookup"><span data-stu-id="b3160-119">Creating, updating, and deleting a synonym map is always a whole-document operation, meaning that you cannot create, update or delete parts of hello synonym map incrementally.</span></span> <span data-ttu-id="b3160-120">La actualización de incluso una entrada única requiere que se vuelva a cargar.</span><span class="sxs-lookup"><span data-stu-id="b3160-120">Updating even a single entry requires a reload.</span></span>

<span data-ttu-id="b3160-121">La incorporación de sinónimos en la aplicación de búsqueda es un proceso de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="b3160-121">Incorporating synonyms into your search application is a two-step process:</span></span>

1.  <span data-ttu-id="b3160-122">Agregar un servicio de búsqueda de sinónimo mapa tooyour a través de las API debajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3160-122">Add a synonym map tooyour search service through hello APIs below.</span></span>  

2.  <span data-ttu-id="b3160-123">Configurar una asignación de campo de búsqueda toouse Hola sinónimo en la definición del índice Hola.</span><span class="sxs-lookup"><span data-stu-id="b3160-123">Configure a searchable field toouse hello synonym map in hello index definition.</span></span>

### <a name="synonymmaps-resource-apis"></a><span data-ttu-id="b3160-124">API de recursos de SynonymMaps</span><span class="sxs-lookup"><span data-stu-id="b3160-124">SynonymMaps Resource APIs</span></span>

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a><span data-ttu-id="b3160-125">Adición o actualización de una asignación de sinónimos en su servicio, con POST o PUT</span><span class="sxs-lookup"><span data-stu-id="b3160-125">Add or update a synonym map under your service, using POST or PUT.</span></span>

<span data-ttu-id="b3160-126">Mapas de sinónimo se cargan toohello servicio a través de POST o PUT.</span><span class="sxs-lookup"><span data-stu-id="b3160-126">Synonym maps are uploaded toohello service via POST or PUT.</span></span> <span data-ttu-id="b3160-127">Cada regla debe estar delimitado por el carácter de nueva línea ('\n') de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3160-127">Each rule must be delimited by hello new line character ('\n').</span></span> <span data-ttu-id="b3160-128">Puede definir too5, 000 reglas por asignación sinónimo en un servicio gratuito y 10 000 reglas en todas las SKU que otros.</span><span class="sxs-lookup"><span data-stu-id="b3160-128">You can define up too5,000 rules per synonym map in a free service and 10,000 rules in all other SKUs.</span></span> <span data-ttu-id="b3160-129">Cada regla puede tener hasta too20 expansiones.</span><span class="sxs-lookup"><span data-stu-id="b3160-129">Each rule can have up too20 expansions.</span></span>

<span data-ttu-id="b3160-130">En esta versión preliminar, mapas de sinónimo deben tener formato de Apache Solr Hola que se explica a continuación.</span><span class="sxs-lookup"><span data-stu-id="b3160-130">In this preview, synonym maps must be in hello Apache Solr format which is explained below.</span></span> <span data-ttu-id="b3160-131">Si tiene un diccionario de sinónimos existentes en un formato diferente y desea toouse lo directamente, háganoslo saber en [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="b3160-131">If you have an existing synonym dictionary in a different format and want toouse it directly, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

<span data-ttu-id="b3160-132">Puede crear un nuevo mapa de sinónimo utilizando HTTP POST, como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="b3160-132">You can create a new synonym map using HTTP POST, as in hello following example:</span></span>

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

<span data-ttu-id="b3160-133">Como alternativa, puede usar PUT y especifique el nombre de asignación de sinónimo de hello en hello URI.</span><span class="sxs-lookup"><span data-stu-id="b3160-133">Alternatively, you can use PUT and specify hello synonym map name on hello URI.</span></span> <span data-ttu-id="b3160-134">Si el mapa de sinónimo hello no existe, se creará.</span><span class="sxs-lookup"><span data-stu-id="b3160-134">If hello synonym map does not exist, it will be created.</span></span>

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a><span data-ttu-id="b3160-135">Formato de sinónimos de Apache</span><span class="sxs-lookup"><span data-stu-id="b3160-135">Apache Solr synonym format</span></span>

<span data-ttu-id="b3160-136">formato de Hello Solr admite asignaciones de sinónimo equivalente y explícita.</span><span class="sxs-lookup"><span data-stu-id="b3160-136">hello Solr format supports equivalent and explicit synonym mappings.</span></span> <span data-ttu-id="b3160-137">Las reglas de asignación cumplen la especificación del filtro sinónimo toohello de código abierto de Apache Solr, se describe en este documento: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span><span class="sxs-lookup"><span data-stu-id="b3160-137">Mapping rules adhere toohello open source synonym filter specification of Apache Solr, described in this document: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span></span> <span data-ttu-id="b3160-138">A continuación se muestra una regla de ejemplo para los sinónimos equivalentes.</span><span class="sxs-lookup"><span data-stu-id="b3160-138">Below is a sample rule for equivalent synonyms.</span></span>
```
              USA, United States, United States of America
```

<span data-ttu-id="b3160-139">Con la regla de hello anterior, una consulta de búsqueda "EE" expandirá demasiado "EE" o "United States" o "Estados Unidos".</span><span class="sxs-lookup"><span data-stu-id="b3160-139">With hello rule above, a search query "USA" will expand too"USA" OR "United States" OR "United States of America".</span></span>

<span data-ttu-id="b3160-140">La asignación explícita se denota mediante una flecha "=>".</span><span class="sxs-lookup"><span data-stu-id="b3160-140">Explicit mapping is denoted by an arrow "=>".</span></span> <span data-ttu-id="b3160-141">Cuando especifica una secuencia de términos de una consulta de búsqueda que coincide con hello del lado izquierdo de "= >" se reemplazará con alternativas de hello en hello del lado derecho.</span><span class="sxs-lookup"><span data-stu-id="b3160-141">When specified, a term sequence of a search query that matches hello left hand side of "=>" will be replaced with hello alternatives on hello right hand side.</span></span> <span data-ttu-id="b3160-142">Dada la regla de Hola a continuación, las consultas de búsqueda "Washington", "Washington"</span><span class="sxs-lookup"><span data-stu-id="b3160-142">Given hello rule below, search queries "Washington", "Wash."</span></span> <span data-ttu-id="b3160-143">o "WA" todos se reescribirán demasiado "WA".</span><span class="sxs-lookup"><span data-stu-id="b3160-143">or "WA" will all be rewritten too"WA".</span></span> <span data-ttu-id="b3160-144">Asignación explícita solo se aplica en la dirección de hello especificada y no vuelva a escribir consultas de Hola "WA" demasiado "Washington" en este caso.</span><span class="sxs-lookup"><span data-stu-id="b3160-144">Explicit mapping only applies in hello direction specified and does not rewrite hello query "WA" too"Washington" in this case.</span></span>
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a><span data-ttu-id="b3160-145">Enumeración de asignaciones de sinónimos en su servicio</span><span class="sxs-lookup"><span data-stu-id="b3160-145">List synonym maps under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a><span data-ttu-id="b3160-146">Obtención de la asignación de sinónimos en su servicio</span><span class="sxs-lookup"><span data-stu-id="b3160-146">Get a synonym map under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a><span data-ttu-id="b3160-147">Eliminación de la asignación de sinónimos en su servicio</span><span class="sxs-lookup"><span data-stu-id="b3160-147">Delete a synonyms map under your service.</span></span>

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-toouse-hello-synonym-map-in-hello-index-definition"></a><span data-ttu-id="b3160-148">Configurar una asignación de campo de búsqueda toouse Hola sinónimo en la definición del índice Hola.</span><span class="sxs-lookup"><span data-stu-id="b3160-148">Configure a searchable field toouse hello synonym map in hello index definition.</span></span>

<span data-ttu-id="b3160-149">Una nueva propiedad de campo **synonymMaps** puede ser usado toospecify un toouse de mapa de sinónimo para un campo de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="b3160-149">A new field property **synonymMaps** can be used toospecify a synonym map toouse for a searchable field.</span></span> <span data-ttu-id="b3160-150">Las asignaciones de sinónimo son recursos de nivel de servicio y pueden hacer referencia a cualquier campo de un índice mediante el servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="b3160-150">Synonym maps are service level resources and can be referenced by any field of an index under hello service.</span></span>

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

<span data-ttu-id="b3160-151">**synonymMaps** se puede especificar para campos de búsqueda de tipo hello 'Edm.String' o 'Collection (EDM.String)'.</span><span class="sxs-lookup"><span data-stu-id="b3160-151">**synonymMaps** can be specified for searchable fields of hello type 'Edm.String' or 'Collection(Edm.String)'.</span></span>

> [!NOTE]
> <span data-ttu-id="b3160-152">En esta versión preliminar, solo puede tener una asignación de sinónimos por campo.</span><span class="sxs-lookup"><span data-stu-id="b3160-152">In this preview, you can only have one synonym map per field.</span></span> <span data-ttu-id="b3160-153">Si desea toouse varias asignaciones de sinónimo, háganoslo saber en [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="b3160-153">If you want toouse multiple synonym maps, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

## <a name="impact-of-synonyms-on-other-search-features"></a><span data-ttu-id="b3160-154">Repercusión de Sinónimos en otras características de búsqueda</span><span class="sxs-lookup"><span data-stu-id="b3160-154">Impact of synonyms on other search features</span></span>

<span data-ttu-id="b3160-155">característica de sinónimos de Hello reescribe la consulta original de hello con sinónimos con hello operador OR.</span><span class="sxs-lookup"><span data-stu-id="b3160-155">hello synonyms feature rewrites hello original query with synonyms with hello OR operator.</span></span> <span data-ttu-id="b3160-156">Por esta razón, resaltado de llamadas y los perfiles de puntuación tratan término original de Hola y sinónimos como equivalentes.</span><span class="sxs-lookup"><span data-stu-id="b3160-156">For this reason, hit highlighting and scoring profiles treat hello original term and synonyms as equivalent.</span></span>

<span data-ttu-id="b3160-157">Característica de sinónimo aplica a las consultas de toosearch y no hay ningún toofilters o facetas.</span><span class="sxs-lookup"><span data-stu-id="b3160-157">Synonym feature applies toosearch queries and does not apply toofilters or facets.</span></span> <span data-ttu-id="b3160-158">De forma similar, las sugerencias se basan únicamente en términos de hello original; coincidencias de sinónimos no aparecen en la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3160-158">Similarly, suggestions are based only on hello original term; synonym matches do not appear in hello response.</span></span>

<span data-ttu-id="b3160-159">Expansiones de sinónimo no aplican los términos de búsqueda toowildcard; no se expanden prefijo, de forma aproximada y los términos de regex.</span><span class="sxs-lookup"><span data-stu-id="b3160-159">Synonym expansions do not apply toowildcard search terms; prefix, fuzzy, and regex terms aren't expanded.</span></span>

## <a name="tips-for-building-a-synonym-map"></a><span data-ttu-id="b3160-160">Consejos para crear un asignación de sinónimos</span><span class="sxs-lookup"><span data-stu-id="b3160-160">Tips for building a synonym map</span></span>

- <span data-ttu-id="b3160-161">Una asignación de sinónimos concisa y bien diseñada es más eficiente que una lista exhaustiva de posibles coincidencias.</span><span class="sxs-lookup"><span data-stu-id="b3160-161">A concise, well-designed synonym map is more efficient than an exhaustive list of possible matches.</span></span> <span data-ttu-id="b3160-162">Diccionarios excesivamente grandes o complejos tardar más tiempo tooparse y afecta a la latencia de consulta Hola si consulta Hola expande toomany sinónimos.</span><span class="sxs-lookup"><span data-stu-id="b3160-162">Excessively large or complex dictionaries take longer tooparse and affect hello query latency if hello query expands toomany synonyms.</span></span> <span data-ttu-id="b3160-163">En lugar de estimación en el que podrían utilizarse términos, puede obtener términos real de Hola a través de un [buscar informes de análisis de tráfico](search-traffic-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="b3160-163">Rather than guess at which terms might be used, you can get hello actual terms via a [search traffic analysis report](search-traffic-analytics.md).</span></span>

- <span data-ttu-id="b3160-164">Como ejercicio un preliminar y la validación, habilitar y, a continuación, use este informe tooprecisely determinar cuáles son los términos beneficiarse de una coincidencia de sinónimo y, a continuación, continuar toouse como que la asignación de sinónimo produce mejores resultados de validación.</span><span class="sxs-lookup"><span data-stu-id="b3160-164">As both a preliminary and validation exercise, enable and then use this report tooprecisely determine which terms will benefit from a synonym match, and then continue toouse it as validation that your synonym map is producing a better outcome.</span></span> <span data-ttu-id="b3160-165">En el informe de hello predefinido, Hola iconos "consultas de búsqueda más comunes" e "consultas de búsqueda de resultado de cero" le proporcionará la información necesaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3160-165">In hello predefined report, hello tiles "Most common search queries" and "Zero-result search queries" will give you hello necessary information.</span></span>

- <span data-ttu-id="b3160-166">Puede crear varias asignaciones para la aplicación de búsqueda (por ejemplo, mediante el idioma si la aplicación es compatible con una base de cliente de varios idiomas).</span><span class="sxs-lookup"><span data-stu-id="b3160-166">You can create multiple synonym maps for your search application (for example, by language if your application supports a multi-lingual customer base).</span></span> <span data-ttu-id="b3160-167">Actualmente, un campo solo puede usar una de ellas.</span><span class="sxs-lookup"><span data-stu-id="b3160-167">Currently, a field can only use one of them.</span></span> <span data-ttu-id="b3160-168">Puede actualizar una propiedad synonymMaps del campo en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="b3160-168">You can update a field's synonymMaps property at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3160-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b3160-169">Next Steps</span></span>

- <span data-ttu-id="b3160-170">Si tiene un índice existente en un entorno de desarrollo (no es de producción), experimentar con un pequeño diccionario toosee cómo cambia la experiencia de búsqueda de hello, incluido el impacto en los perfiles de puntuación, posicionamiento resaltado y sugerencias suma Hola de sinónimos.</span><span class="sxs-lookup"><span data-stu-id="b3160-170">If you have an existing index in a development (non-production) environment, experiment with a small dictionary toosee how hello addition of synonyms changes hello search experience, including impact on scoring profiles, hit highlighting, and suggestions.</span></span>

- <span data-ttu-id="b3160-171">[Habilitar el análisis de tráfico de búsqueda](search-traffic-analytics.md) y use Hola predefinidos toolearn qué términos se usan Hola mayoría y los que los devuelto cero documentos de informe de Power BI.</span><span class="sxs-lookup"><span data-stu-id="b3160-171">[Enable search traffic analytics](search-traffic-analytics.md) and use hello predefined Power BI report toolearn which terms are used hello most, and which ones return zero documents.</span></span> <span data-ttu-id="b3160-172">Gracias a estas informaciones, revise los sinónimos de tooinclude de diccionario de Hola para consultas improductivos que deberían estar resolviendo toodocuments en el índice.</span><span class="sxs-lookup"><span data-stu-id="b3160-172">Armed with these insights, revise hello dictionary tooinclude synonyms for unproductive queries that should be resolving toodocuments in your index.</span></span>
