---
title: "Paginación de los resultados de Azure Search | Microsoft Docs"
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
ms.openlocfilehash: 1054e15a2751c53aad5dbc8054c4cec41102dee9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-page-search-results-in-azure-search"></a><span data-ttu-id="f03af-103">Cómo paginar los resultados de la búsqueda en Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="f03af-103">How to page search results in Azure Search</span></span>
<span data-ttu-id="f03af-104">Este artículo proporciona orientación sobre la forma de usar la API de REST del servicio Búsqueda de Azure para implementar los elementos habituales de una página de resultados de búsqueda, como recuentos totales, recuperación de documentos, criterios de ordenación y navegación.</span><span class="sxs-lookup"><span data-stu-id="f03af-104">This article provides guidance on how to use the Azure Search Service REST API to implement standard elements of a search results page, such as total counts, document retrieval, sort orders, and navigation.</span></span>

<span data-ttu-id="f03af-105">En todos los casos que se mencionan a continuación, las opciones relacionadas con la página que aportan datos o información a la página de resultados de búsqueda se especifican a través de solicitudes [Buscar documento](http://msdn.microsoft.com/library/azure/dn798927.aspx) que se envían a su servicio Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="f03af-105">In every case mentioned below, page-related options that contribute data or information to your search results page are specified through the [Search Document](http://msdn.microsoft.com/library/azure/dn798927.aspx) requests sent to your Azure Search Service.</span></span> <span data-ttu-id="f03af-106">Las solicitudes incluyen un comando GET, ruta de acceso y parámetros de consulta que informan el servicio de lo que se solicita y de cómo formular la respuesta.</span><span class="sxs-lookup"><span data-stu-id="f03af-106">Requests include a GET command, path, and query parameters that inform the service what is being requested, and how to formulate the response.</span></span>

> [!NOTE]
> <span data-ttu-id="f03af-107">Una solicitud válida incluye una serie de elementos, como una dirección URL del servicio y la ruta de acceso, el verbo HTTP, `api-version`, etc.</span><span class="sxs-lookup"><span data-stu-id="f03af-107">A valid request includes a number of elements, such as a service URL and path, HTTP verb, `api-version`, and so on.</span></span> <span data-ttu-id="f03af-108">Para mayor brevedad, hemos acortado los ejemplos para resaltar solo la sintaxis que resulta relevante para la paginación.</span><span class="sxs-lookup"><span data-stu-id="f03af-108">For brevity, we trimmed the examples to highlight just the syntax that is relevant to pagination.</span></span> <span data-ttu-id="f03af-109">Consulte la documentación de [API de REST del Servicio de Búsqueda de Azure](http://msdn.microsoft.com/library/azure/dn798935.aspx) para obtener más información acerca de la sintaxis de solicitud.</span><span class="sxs-lookup"><span data-stu-id="f03af-109">Please see the [Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentation for details about request syntax.</span></span>
> 
> 

## <a name="total-hits-and-page-counts"></a><span data-ttu-id="f03af-110">Total de resultados y recuentos de página</span><span class="sxs-lookup"><span data-stu-id="f03af-110">Total hits and Page Counts</span></span>
<span data-ttu-id="f03af-111">Muestra el número total de resultados devueltos por una consulta y, a continuación, devolver los resultados en bloques más pequeños, es fundamental para casi todas las páginas de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="f03af-111">Showing the total number of results returned from a query, and then returning those results in smaller chunks, is fundamental to virtually all search pages.</span></span>

![][1]

<span data-ttu-id="f03af-112">En Búsqueda de Azure se utilizan los parámetros `$count`, `$top` y `$skip` para devolver esos valores.</span><span class="sxs-lookup"><span data-stu-id="f03af-112">In Azure Search, you use the `$count`, `$top`, and `$skip` parameters to return these values.</span></span> <span data-ttu-id="f03af-113">En el ejemplo siguiente se muestra un ejemplo de solicitud del total de resultados, que se devuelve como `@OData.count`:</span><span class="sxs-lookup"><span data-stu-id="f03af-113">The following example shows a sample request for total hits, returned as `@OData.count`:</span></span>

        GET /indexes/onlineCatalog/docs?$count=true

<span data-ttu-id="f03af-114">Recuperar documentos en grupos de 15 y mostrar también el total de resultados, comenzando por la primera página:</span><span class="sxs-lookup"><span data-stu-id="f03af-114">Retrieve documents in groups of 15, and also show the total hits, starting at the first page:</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

<span data-ttu-id="f03af-115">Paginar resultados requiere `$top` y `$skip`, donde `$top` especifica cuántos elementos se devuelven en un lote y `$skip` especifica cuántos elementos se omiten.</span><span class="sxs-lookup"><span data-stu-id="f03af-115">Paginating results requires both `$top` and `$skip`, where `$top` specifies how many items to return in a batch, and `$skip` specifies how many items to skip.</span></span> <span data-ttu-id="f03af-116">En el ejemplo siguiente, cada página muestra los siguientes 15 elementos, indicado por los saltos incrementales en el parámetro `$skip` .</span><span class="sxs-lookup"><span data-stu-id="f03af-116">In the following example, each page shows the next 15 items, indicated by the incremental jumps in the `$skip` parameter.</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a><span data-ttu-id="f03af-117">Diseño</span><span class="sxs-lookup"><span data-stu-id="f03af-117">Layout</span></span>
<span data-ttu-id="f03af-118">En una página de resultados de búsqueda, puede ser deseable mostrar una imagen en miniatura, un subconjunto de campos y un vínculo a una página de producto completa.</span><span class="sxs-lookup"><span data-stu-id="f03af-118">On a search results page, you might want to show a thumbnail image, a subset of fields, and a link to a full product page.</span></span>

 ![][2]

<span data-ttu-id="f03af-119">En Búsqueda de Azure se utiliza `$select` y un comando de búsqueda para implementar esta experiencia.</span><span class="sxs-lookup"><span data-stu-id="f03af-119">In Azure Search, you would use `$select` and a lookup command to implement this experience.</span></span>

<span data-ttu-id="f03af-120">Para devolver un subconjunto de campos con un diseño en mosaico:</span><span class="sxs-lookup"><span data-stu-id="f03af-120">To return a subset of fields for a tiled layout:</span></span>

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

<span data-ttu-id="f03af-121">Las imágenes y los archivos multimedia no se pueden buscar directamente y se deben almacenar en otra plataforma de almacenamiento, como Almacenamiento de blobs de Azure, para reducir los costes.</span><span class="sxs-lookup"><span data-stu-id="f03af-121">Images and media files are not directly searchable and should be stored in another storage platform, such as Azure Blob storage, to reduce costs.</span></span> <span data-ttu-id="f03af-122">En el índice y los documentos, defina un campo que almacene la dirección URL del contenido externo.</span><span class="sxs-lookup"><span data-stu-id="f03af-122">In the index and documents, define a field that stores the URL address of the external content.</span></span> <span data-ttu-id="f03af-123">Después puede utilizar el campo como referencia de imagen.</span><span class="sxs-lookup"><span data-stu-id="f03af-123">You can then use the field as an image reference.</span></span> <span data-ttu-id="f03af-124">La dirección URL de la imagen debe estar en el documento.</span><span class="sxs-lookup"><span data-stu-id="f03af-124">The URL to the image should be in the document.</span></span>

<span data-ttu-id="f03af-125">Para recuperar una página de descripción de producto para un evento **onClick** , use [Buscar documento](http://msdn.microsoft.com/library/azure/dn798929.aspx) para pasar la clave del documento que se va a recuperar.</span><span class="sxs-lookup"><span data-stu-id="f03af-125">To retrieve a product description page for an **onClick** event, use [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) to pass in the key of the document to retrieve.</span></span> <span data-ttu-id="f03af-126">El tipo de datos de la clave es `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="f03af-126">The data type of the key is `Edm.String`.</span></span> <span data-ttu-id="f03af-127">En este ejemplo, es *246810*.</span><span class="sxs-lookup"><span data-stu-id="f03af-127">In this example, it is *246810*.</span></span> 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a><span data-ttu-id="f03af-128">Ordenar por relevancia, clasificación o precio</span><span class="sxs-lookup"><span data-stu-id="f03af-128">Sort by relevance, rating, or price</span></span>
<span data-ttu-id="f03af-129">A menudo, el orden predeterminado se basa en la relevancia, pero es habitual poner a disposición de los clientes otros criterios de ordenación para que puedan reorganizar rápidamente los resultados existentes en un orden diferente.</span><span class="sxs-lookup"><span data-stu-id="f03af-129">Sort orders often default to relevance, but it's common to make alternative sort orders readily available so that customers can quickly reshuffle existing results into a different rank order.</span></span>

 ![][3]

<span data-ttu-id="f03af-130">En Búsqueda de Azure, la ordenación se basa en la expresión `$orderby` para todos los campos que se indizan como `"Sortable": true.`</span><span class="sxs-lookup"><span data-stu-id="f03af-130">In Azure Search, sorting is based on the `$orderby` expression, for all fields that are indexed as `"Sortable": true.`</span></span>

<span data-ttu-id="f03af-131">La relevancia está estrechamente asociada con perfiles de puntuación.</span><span class="sxs-lookup"><span data-stu-id="f03af-131">Relevance is strongly associated with scoring profiles.</span></span> <span data-ttu-id="f03af-132">Puede utilizar la puntuación predeterminada, que se basa en el análisis de texto y las estadísticas para ordenar todos los resultados, con las puntuaciones más altas destinadas a documentos con más coincidencias de un término de búsqueda o con coincidencias más importantes.</span><span class="sxs-lookup"><span data-stu-id="f03af-132">You can use the default scoring, which relies on text analysis and statistics to rank order all results, with higher scores going to documents with more or stronger matches on a search term.</span></span>

<span data-ttu-id="f03af-133">Los criterios de ordenación alternativos se suelen asociar a eventos **onClick** que llaman a un método que compila el criterio de ordenación.</span><span class="sxs-lookup"><span data-stu-id="f03af-133">Alternative sort orders are typically associated with **onClick** events that call back to a method that builds the sort order.</span></span> <span data-ttu-id="f03af-134">Por ejemplo, con este elemento de página:</span><span class="sxs-lookup"><span data-stu-id="f03af-134">For example, given this page element:</span></span>

 ![][4]

<span data-ttu-id="f03af-135">Deberá crear un método que acepte la opción de ordenación seleccionada como entrada y devuelva una lista ordenada de los criterios asociados a esa opción.</span><span class="sxs-lookup"><span data-stu-id="f03af-135">You would create a method that accepts the selected sort option as input, and returns an ordered list for the criteria associated with that option.</span></span>

 ![][5]

> [!NOTE]
> <span data-ttu-id="f03af-136">Aunque la puntuación predeterminada es suficiente para muchos escenarios, se recomienda basar la relevancia en un perfil de puntuación personalizado.</span><span class="sxs-lookup"><span data-stu-id="f03af-136">While the default scoring is sufficient for many scenarios, we recommend basing relevance on a custom scoring profile instead.</span></span> <span data-ttu-id="f03af-137">Un perfil personalizado de puntuación le ofrece una forma de aumentar los elementos que son más útiles para su negocio.</span><span class="sxs-lookup"><span data-stu-id="f03af-137">A custom scoring profile gives you a way to boost items that are more beneficial to your business.</span></span> <span data-ttu-id="f03af-138">Consulte [Incorporación de un perfil de puntuación](http://msdn.microsoft.com/library/azure/dn798928.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="f03af-138">See [Add a scoring profile](http://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> 
> 
> 

## <a name="faceted-navigation"></a><span data-ttu-id="f03af-139">Navegación por facetas</span><span class="sxs-lookup"><span data-stu-id="f03af-139">Faceted navigation</span></span>
<span data-ttu-id="f03af-140">La navegación de búsqueda es habitual en una página de resultados; a menudo se encuentra en un lado o en la parte superior de una página.</span><span class="sxs-lookup"><span data-stu-id="f03af-140">Search navigation is common on a results page, often located at the side or top of a page.</span></span> <span data-ttu-id="f03af-141">En Búsqueda de Azure, la navegación por facetas proporciona una búsqueda autodirigida basándose en filtros predefinidos.</span><span class="sxs-lookup"><span data-stu-id="f03af-141">In Azure Search, faceted navigation provides self-directed search based on predefined filters.</span></span> <span data-ttu-id="f03af-142">Consulte [Navegación por facetas en Búsqueda de Azure](search-faceted-navigation.md) para obtener más detalles</span><span class="sxs-lookup"><span data-stu-id="f03af-142">See [Faceted navigation in Azure Search](search-faceted-navigation.md) for details.</span></span>

## <a name="filters-at-the-page-level"></a><span data-ttu-id="f03af-143">Filtros en el nivel de página</span><span class="sxs-lookup"><span data-stu-id="f03af-143">Filters at the page level</span></span>
<span data-ttu-id="f03af-144">Si el diseño de la solución incluye páginas de búsqueda dedicadas para determinados tipos de contenido (por ejemplo, una aplicación comercial en línea que enumera los departamentos en la parte superior de la página), puede insertar una expresión de filtro junto con un evento **onClick** para abrir una página en un estado prefiltrado.</span><span class="sxs-lookup"><span data-stu-id="f03af-144">If your solution design included dedicated search pages for specific types of content (for example, an online retail application that has departments listed at the top of the page), you can insert a filter expression alongside an **onClick** event to open a page in a prefiltered state.</span></span> 

<span data-ttu-id="f03af-145">Puede enviar un filtro con o sin expresión de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="f03af-145">You can send a filter with or without a search expression.</span></span> <span data-ttu-id="f03af-146">Por ejemplo, la siguiente solicitud filtrará por el nombre de la marca y devolverá solamente los documentos que coincidan con él.</span><span class="sxs-lookup"><span data-stu-id="f03af-146">For example, the following request will filter on brand name, returning only those documents that match it.</span></span>

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

<span data-ttu-id="f03af-147">Consulte [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) (Búsqueda de documentos [API de Azure Search]) para más información sobre las expresiones `$filter`.</span><span class="sxs-lookup"><span data-stu-id="f03af-147">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for more information about `$filter` expressions.</span></span>

## <a name="see-also"></a><span data-ttu-id="f03af-148">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="f03af-148">See Also</span></span>
* [<span data-ttu-id="f03af-149">API de REST del Servicio Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="f03af-149">Azure Search Service REST API</span></span>](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [<span data-ttu-id="f03af-150">Operaciones de índice</span><span class="sxs-lookup"><span data-stu-id="f03af-150">Index Operations</span></span>](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [<span data-ttu-id="f03af-151">Operaciones del documento</span><span class="sxs-lookup"><span data-stu-id="f03af-151">Document Operations</span></span>](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [<span data-ttu-id="f03af-152">Vídeo y tutoriales acerca de Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="f03af-152">Video and tutorials about Azure Search</span></span>](search-video-demo-tutorial-list.md)
* [<span data-ttu-id="f03af-153">Navegación por facetas en Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="f03af-153">Faceted Navigation in Azure Search</span></span>](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
