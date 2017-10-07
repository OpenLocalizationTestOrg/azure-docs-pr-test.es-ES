---
title: "resultados de búsqueda de toopage de aaaHow en búsqueda de Azure | Documentos de Microsoft"
description: "Paginación de Búsqueda de Azure, un servicio de búsqueda hospedado en la nube en Microsoft Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: a0a1d315-8624-4cdf-b38e-ba12569c6fcc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/29/2016
ms.author: heidist
ms.openlocfilehash: e3abc1ca4d5994b0a77955379081a4fcfa5a7fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopage-search-results-in-azure-search"></a><span data-ttu-id="a80f6-103">Cómo resultados de búsqueda de toopage en búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="a80f6-103">How toopage search results in Azure Search</span></span>
<span data-ttu-id="a80f6-104">Este artículo proporciona instrucciones sobre cómo toouse Hola API de REST de servicio de búsqueda de Azure tooimplement elementos estándar de una búsqueda de página de resultados, como los recuentos totales, la recuperación de documentos, criterios de ordenación y la navegación.</span><span class="sxs-lookup"><span data-stu-id="a80f6-104">This article provides guidance on how toouse hello Azure Search Service REST API tooimplement standard elements of a search results page, such as total counts, document retrieval, sort orders, and navigation.</span></span>

<span data-ttu-id="a80f6-105">En cada caso mencionado a continuación, se especifican opciones relacionadas con la página que contribuyen a datos o información de la página de resultados de búsqueda tooyour a través de hello [Buscar documento](http://msdn.microsoft.com/library/azure/dn798927.aspx) las solicitudes enviadas tooyour servicio de búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="a80f6-105">In every case mentioned below, page-related options that contribute data or information tooyour search results page are specified through hello [Search Document](http://msdn.microsoft.com/library/azure/dn798927.aspx) requests sent tooyour Azure Search Service.</span></span> <span data-ttu-id="a80f6-106">Las solicitudes incluyen un comando GET, ruta de acceso y parámetros de consulta que informan sobre lo que se solicita el servicio de Hola y cómo tooformulate Hola respuesta.</span><span class="sxs-lookup"><span data-stu-id="a80f6-106">Requests include a GET command, path, and query parameters that inform hello service what is being requested, and how tooformulate hello response.</span></span>

> [!NOTE]
> <span data-ttu-id="a80f6-107">Una solicitud válida incluye una serie de elementos, como una dirección URL del servicio y la ruta de acceso, el verbo HTTP, `api-version`, etc.</span><span class="sxs-lookup"><span data-stu-id="a80f6-107">A valid request includes a number of elements, such as a service URL and path, HTTP verb, `api-version`, and so on.</span></span> <span data-ttu-id="a80f6-108">Para mayor brevedad, se recortan Hola ejemplos toohighlight Hola simplemente sintaxis toopagination relevante.</span><span class="sxs-lookup"><span data-stu-id="a80f6-108">For brevity, we trimmed hello examples toohighlight just hello syntax that is relevant toopagination.</span></span> <span data-ttu-id="a80f6-109">Vea hello [API de REST de servicio de búsqueda de Azure](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentación para obtener más información acerca de la sintaxis de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="a80f6-109">Please see hello [Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentation for details about request syntax.</span></span>
> 
> 

## <a name="total-hits-and-page-counts"></a><span data-ttu-id="a80f6-110">Total de resultados y recuentos de página</span><span class="sxs-lookup"><span data-stu-id="a80f6-110">Total hits and Page Counts</span></span>
<span data-ttu-id="a80f6-111">Mostrar hello total número de resultados devueltos por una consulta y, a continuación, devolverlos resultados en fragmentos más pequeños, es fundamental toovirtually todas las páginas de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="a80f6-111">Showing hello total number of results returned from a query, and then returning those results in smaller chunks, is fundamental toovirtually all search pages.</span></span>

![][1]

<span data-ttu-id="a80f6-112">En la búsqueda de Azure, use hello `$count`, `$top`, y `$skip` parámetros tooreturn estos valores.</span><span class="sxs-lookup"><span data-stu-id="a80f6-112">In Azure Search, you use hello `$count`, `$top`, and `$skip` parameters tooreturn these values.</span></span> <span data-ttu-id="a80f6-113">Hello en el ejemplo siguiente se muestra una solicitud de ejemplo para el total de aciertos, formando `@OData.count`:</span><span class="sxs-lookup"><span data-stu-id="a80f6-113">hello following example shows a sample request for total hits, returned as `@OData.count`:</span></span>

        GET /indexes/onlineCatalog/docs?$count=true

<span data-ttu-id="a80f6-114">Recuperar los documentos en los grupos de 15 y también muestran Hola total de aciertos, empezando por la primera página de hello:</span><span class="sxs-lookup"><span data-stu-id="a80f6-114">Retrieve documents in groups of 15, and also show hello total hits, starting at hello first page:</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

<span data-ttu-id="a80f6-115">Paginar resultados requiere `$top` y `$skip`, donde `$top` especifica el número de elementos de tooreturn en un lote, y `$skip` especifica el número de elementos de tooskip.</span><span class="sxs-lookup"><span data-stu-id="a80f6-115">Paginating results requires both `$top` and `$skip`, where `$top` specifies how many items tooreturn in a batch, and `$skip` specifies how many items tooskip.</span></span> <span data-ttu-id="a80f6-116">Hola siguiente ejemplo, cada página muestra hello 15 a continuación de los elementos, indicado por saltos incremental de Hola Hola `$skip` parámetro.</span><span class="sxs-lookup"><span data-stu-id="a80f6-116">In hello following example, each page shows hello next 15 items, indicated by hello incremental jumps in hello `$skip` parameter.</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a><span data-ttu-id="a80f6-117">Diseño</span><span class="sxs-lookup"><span data-stu-id="a80f6-117">Layout</span></span>
<span data-ttu-id="a80f6-118">En una página de resultados de búsqueda, puede que desee tooshow una imagen en miniatura, un subconjunto de campos y una página de vínculo tooa producto completo.</span><span class="sxs-lookup"><span data-stu-id="a80f6-118">On a search results page, you might want tooshow a thumbnail image, a subset of fields, and a link tooa full product page.</span></span>

 ![][2]

<span data-ttu-id="a80f6-119">En búsqueda de Azure, usaría `$select` y una búsqueda de comandos tooimplement esta experiencia.</span><span class="sxs-lookup"><span data-stu-id="a80f6-119">In Azure Search, you would use `$select` and a lookup command tooimplement this experience.</span></span>

<span data-ttu-id="a80f6-120">tooreturn un subconjunto de campos para un diseño en mosaico:</span><span class="sxs-lookup"><span data-stu-id="a80f6-120">tooreturn a subset of fields for a tiled layout:</span></span>

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

<span data-ttu-id="a80f6-121">Imágenes y archivos multimedia no se puede buscar directamente y deberían almacenarse en otra plataforma de almacenamiento, como almacenamiento de blobs de Azure, los costos de tooreduce.</span><span class="sxs-lookup"><span data-stu-id="a80f6-121">Images and media files are not directly searchable and should be stored in another storage platform, such as Azure Blob storage, tooreduce costs.</span></span> <span data-ttu-id="a80f6-122">En el índice de Hola y documentos, defina un campo que almacena la dirección URL de Hola de contenido externo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a80f6-122">In hello index and documents, define a field that stores hello URL address of hello external content.</span></span> <span data-ttu-id="a80f6-123">A continuación, puede usar el campo de hello como referencia de una imagen.</span><span class="sxs-lookup"><span data-stu-id="a80f6-123">You can then use hello field as an image reference.</span></span> <span data-ttu-id="a80f6-124">imagen de toohello de Hello dirección URL debe estar en el documento de Hola.</span><span class="sxs-lookup"><span data-stu-id="a80f6-124">hello URL toohello image should be in hello document.</span></span>

<span data-ttu-id="a80f6-125">tooretrieve página de descripción de un producto para un **onClick** evento, use [búsqueda de documento](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass en clave de Hola de hello documento tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="a80f6-125">tooretrieve a product description page for an **onClick** event, use [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass in hello key of hello document tooretrieve.</span></span> <span data-ttu-id="a80f6-126">Hola de tipo de datos de clave de hello es `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="a80f6-126">hello data type of hello key is `Edm.String`.</span></span> <span data-ttu-id="a80f6-127">En este ejemplo, es *246810*.</span><span class="sxs-lookup"><span data-stu-id="a80f6-127">In this example, it is *246810*.</span></span> 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a><span data-ttu-id="a80f6-128">Ordenar por relevancia, clasificación o precio</span><span class="sxs-lookup"><span data-stu-id="a80f6-128">Sort by relevance, rating, or price</span></span>
<span data-ttu-id="a80f6-129">Criterios de ordenación a menudo predeterminado toorelevance, pero es común toomake alternativos de ordenación estén disponibles para que los clientes pueden reorganizar rápidamente los resultados existentes en un orden diferente del rango.</span><span class="sxs-lookup"><span data-stu-id="a80f6-129">Sort orders often default toorelevance, but it's common toomake alternative sort orders readily available so that customers can quickly reshuffle existing results into a different rank order.</span></span>

 ![][3]

<span data-ttu-id="a80f6-130">En búsqueda de Azure, la ordenación se basa en hello `$orderby` expresión para todos los campos que se indizan como`"Sortable": true.`</span><span class="sxs-lookup"><span data-stu-id="a80f6-130">In Azure Search, sorting is based on hello `$orderby` expression, for all fields that are indexed as `"Sortable": true.`</span></span>

<span data-ttu-id="a80f6-131">La relevancia está estrechamente asociada con perfiles de puntuación.</span><span class="sxs-lookup"><span data-stu-id="a80f6-131">Relevance is strongly associated with scoring profiles.</span></span> <span data-ttu-id="a80f6-132">Puede usar Hola de puntuación predeterminado, que basa en el orden de toorank de análisis y las estadísticas de texto todos los resultados, con las puntuaciones más altas sucediendo toodocuments más fuertes o más coincidencias con un término de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="a80f6-132">You can use hello default scoring, which relies on text analysis and statistics toorank order all results, with higher scores going toodocuments with more or stronger matches on a search term.</span></span>

<span data-ttu-id="a80f6-133">Criterios de ordenación alternativos se suelen estar asociados a **onClick** eventos que devuelva la llamada tooa método que genera el criterio de ordenación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a80f6-133">Alternative sort orders are typically associated with **onClick** events that call back tooa method that builds hello sort order.</span></span> <span data-ttu-id="a80f6-134">Por ejemplo, con este elemento de página:</span><span class="sxs-lookup"><span data-stu-id="a80f6-134">For example, given this page element:</span></span>

 ![][4]

<span data-ttu-id="a80f6-135">Deberá crear un método que acepta la opción de ordenación de hello seleccionado como entrada y devuelve una lista ordenada de los criterios de hello asociados a esa opción.</span><span class="sxs-lookup"><span data-stu-id="a80f6-135">You would create a method that accepts hello selected sort option as input, and returns an ordered list for hello criteria associated with that option.</span></span>

 ![][5]

> [!NOTE]
> <span data-ttu-id="a80f6-136">Mientras la puntuación de hello predeterminada es suficiente para muchos escenarios, se recomienda basar relevancia en un perfil de puntuación personalizado en su lugar.</span><span class="sxs-lookup"><span data-stu-id="a80f6-136">While hello default scoring is sufficient for many scenarios, we recommend basing relevance on a custom scoring profile instead.</span></span> <span data-ttu-id="a80f6-137">Un perfil de puntuación personalizado ofrece un elementos de tooboost de manera que son más beneficioso para el negocio tooyour.</span><span class="sxs-lookup"><span data-stu-id="a80f6-137">A custom scoring profile gives you a way tooboost items that are more beneficial tooyour business.</span></span> <span data-ttu-id="a80f6-138">Consulte [Incorporación de un perfil de puntuación](http://msdn.microsoft.com/library/azure/dn798928.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="a80f6-138">See [Add a scoring profile](http://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> 
> 
> 

## <a name="faceted-navigation"></a><span data-ttu-id="a80f6-139">Navegación por facetas</span><span class="sxs-lookup"><span data-stu-id="a80f6-139">Faceted navigation</span></span>
<span data-ttu-id="a80f6-140">Navegación de búsqueda es común en una página de resultados, normalmente situada al lado de Hola o la parte superior de una página.</span><span class="sxs-lookup"><span data-stu-id="a80f6-140">Search navigation is common on a results page, often located at hello side or top of a page.</span></span> <span data-ttu-id="a80f6-141">En Búsqueda de Azure, la navegación por facetas proporciona una búsqueda autodirigida basándose en filtros predefinidos.</span><span class="sxs-lookup"><span data-stu-id="a80f6-141">In Azure Search, faceted navigation provides self-directed search based on predefined filters.</span></span> <span data-ttu-id="a80f6-142">Consulte [Navegación por facetas en Búsqueda de Azure](search-faceted-navigation.md) para obtener más detalles</span><span class="sxs-lookup"><span data-stu-id="a80f6-142">See [Faceted navigation in Azure Search](search-faceted-navigation.md) for details.</span></span>

## <a name="filters-at-hello-page-level"></a><span data-ttu-id="a80f6-143">Filtros de nivel de página Hola</span><span class="sxs-lookup"><span data-stu-id="a80f6-143">Filters at hello page level</span></span>
<span data-ttu-id="a80f6-144">Si el diseño de la solución incluye páginas de búsqueda dedicado para determinados tipos de contenido (por ejemplo, una aplicación comercial en línea que tiene departamentos aparece al principio de Hola de página de hello), puede insertar una expresión de filtro junto con un **onClick** tooopen una página en un estado prefiltrada de eventos.</span><span class="sxs-lookup"><span data-stu-id="a80f6-144">If your solution design included dedicated search pages for specific types of content (for example, an online retail application that has departments listed at hello top of hello page), you can insert a filter expression alongside an **onClick** event tooopen a page in a prefiltered state.</span></span> 

<span data-ttu-id="a80f6-145">Puede enviar un filtro con o sin expresión de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="a80f6-145">You can send a filter with or without a search expression.</span></span> <span data-ttu-id="a80f6-146">Por ejemplo, hello solicitud siguiente se filtrará en nombre de la marca, devolver únicamente los documentos que coinciden con él.</span><span class="sxs-lookup"><span data-stu-id="a80f6-146">For example, hello following request will filter on brand name, returning only those documents that match it.</span></span>

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

<span data-ttu-id="a80f6-147">Consulte [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) (Búsqueda de documentos [API de Azure Search]) para más información sobre las expresiones `$filter`.</span><span class="sxs-lookup"><span data-stu-id="a80f6-147">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for more information about `$filter` expressions.</span></span>

## <a name="see-also"></a><span data-ttu-id="a80f6-148">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="a80f6-148">See Also</span></span>
* [<span data-ttu-id="a80f6-149">API de REST del Servicio Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="a80f6-149">Azure Search Service REST API</span></span>](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [<span data-ttu-id="a80f6-150">Operaciones de índice</span><span class="sxs-lookup"><span data-stu-id="a80f6-150">Index Operations</span></span>](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [<span data-ttu-id="a80f6-151">Operaciones del documento</span><span class="sxs-lookup"><span data-stu-id="a80f6-151">Document Operations</span></span>](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [<span data-ttu-id="a80f6-152">Vídeo y tutoriales acerca de Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="a80f6-152">Video and tutorials about Azure Search</span></span>](search-video-demo-tutorial-list.md)
* [<span data-ttu-id="a80f6-153">Navegación por facetas en Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="a80f6-153">Faceted Navigation in Azure Search</span></span>](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
