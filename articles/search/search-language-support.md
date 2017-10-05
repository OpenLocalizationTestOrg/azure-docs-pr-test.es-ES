---
title: Varios lenguajes para Azure Search | Microsoft Docs
description: "Búsqueda de Azure admite 56 idiomas y aprovecha los analizadores de idiomas Lucene y la tecnología de procesamiento de lenguaje natural de Microsoft."
services: search
documentationcenter: 
author: yahnoosh
manager: pablocas
editor: 
ms.assetid: 55a00b44-804d-41bb-9c96-e6ea498616f5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: jlembicz
ms.openlocfilehash: dbbab31bac66ce73dbf9883992713a2c16581e19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a><span data-ttu-id="f5524-103">Creación de un índice para documentos en varios idiomas en Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="f5524-103">Create an index for documents in multiple languages in Azure Search</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="f5524-104">Portal</span><span class="sxs-lookup"><span data-stu-id="f5524-104">Portal</span></span>](search-language-support.md)
> * [<span data-ttu-id="f5524-105">REST</span><span class="sxs-lookup"><span data-stu-id="f5524-105">REST</span></span>](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [<span data-ttu-id="f5524-106">.NET</span><span class="sxs-lookup"><span data-stu-id="f5524-106">.NET</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

<span data-ttu-id="f5524-107">Desatar la potencia de los analizadores de lenguajes es tan fácil como establecer una propiedad en un campo de búsqueda en la definición del índice.</span><span class="sxs-lookup"><span data-stu-id="f5524-107">Unleashing the power of language analyzers is as easy as setting one property on a searchable field in the index definition.</span></span> <span data-ttu-id="f5524-108">Ahora puede realizar este paso en el portal.</span><span class="sxs-lookup"><span data-stu-id="f5524-108">Now you can do this step in the portal.</span></span>

<span data-ttu-id="f5524-109">A continuación, se muestran capturas de pantalla de las hojas del Portal de Azure para Búsqueda de Azure que permiten a los usuarios definir un esquema de índice.</span><span class="sxs-lookup"><span data-stu-id="f5524-109">Below are screenshots of the Azure Portal blades for Azure Search that allow users to define an index schema.</span></span> <span data-ttu-id="f5524-110">En esta hoja, los usuarios pueden crear todos los campos y establecer la propiedad de analizador para cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="f5524-110">From this blade, users can create all of the fields and set the analyzer property for each of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f5524-111">Solo puede establecer un analizador de lenguaje durante la definición de campo, como en al crear un nuevo índice desde el principio de o al agregar un nuevo campo a un índice existente.</span><span class="sxs-lookup"><span data-stu-id="f5524-111">You can only set a language analyzer during field definition, as in when creating a new index from the ground up, or when adding a new field to an existing index.</span></span> <span data-ttu-id="f5524-112">Asegúrese de especificar completamente todos los atributos, incluido el analizador, al crear el campo.</span><span class="sxs-lookup"><span data-stu-id="f5524-112">Make sure you fully specify all attributes, including the analyzer, while creating the field.</span></span> <span data-ttu-id="f5524-113">No podrá editar los atributos ni cambiar el tipo de analizador una vez guardado los cambios.</span><span class="sxs-lookup"><span data-stu-id="f5524-113">You won't be able to edit the attributes or change the analyzer type once you save your changes.</span></span>
>
>

## <a name="define-a-new-field-definition"></a><span data-ttu-id="f5524-114">Definición de una nueva definición de campo</span><span class="sxs-lookup"><span data-stu-id="f5524-114">Define a new field definition</span></span>
1. <span data-ttu-id="f5524-115">Inicie sesión en [Azure Portal](https://portal.azure.com) y abra la hoja de servicio del servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="f5524-115">Sign in to the [Azure portal](https://portal.azure.com) and open the service blade of your search service.</span></span>
2. <span data-ttu-id="f5524-116">Haga clic en **Agregar un índice** en la barra de comandos de la parte superior del panel de servicio para iniciar un nuevo índice, o abra un índice existente para establecer un analizador de nuevos campos que se va a agregar a un índice existente.</span><span class="sxs-lookup"><span data-stu-id="f5524-116">Click **Add index** in the command bar at the top of the service dashboard to start a new index, or open an existing index to set an analyzer on new fields you're adding to an existing index.</span></span>
3. <span data-ttu-id="f5524-117">Aparece la hoja Campos, que proporciona opciones para definir el esquema del índice, incluida la pestaña Analizador usada para elegir un analizador de lenguaje.</span><span class="sxs-lookup"><span data-stu-id="f5524-117">The Fields blade appears, giving you options for defining the schema of the index, including the Analyzer tab used for choosing a language analyzer.</span></span>
4. <span data-ttu-id="f5524-118">En Campos, inicie una definición de campo y proporcione un nombre, seleccione el tipo de datos y establezca los atributos para marcar el campo como texto completo que se puede buscar, recuperar resultados de búsqueda, que se pueden usar en estructuras de navegación de facetas, se pueden ordenar, etc.</span><span class="sxs-lookup"><span data-stu-id="f5524-118">In Fields, start a field definition by providing a name, choosing the data type, and setting attributes to mark the field as full text searchable, retrievable in search results, usable in facet navigation structures, sortable, and so forth.</span></span>
5. <span data-ttu-id="f5524-119">Antes de pasar al siguiente campo, abra la pestaña **Analizador** .</span><span class="sxs-lookup"><span data-stu-id="f5524-119">Before moving on to the next field, open the **Analyzer** tab.</span></span>

<span data-ttu-id="f5524-120">![][1]
*Para seleccionar un analizador, haga clic en la pestaña Analizador en la hoja Campos*.</span><span class="sxs-lookup"><span data-stu-id="f5524-120">![][1]
*To select an analyzer, click the Analyzer tab on the Fields blade*</span></span>

## <a name="choose-an-analyzer"></a><span data-ttu-id="f5524-121">Selección de un analizador</span><span class="sxs-lookup"><span data-stu-id="f5524-121">Choose an analyzer</span></span>
1. <span data-ttu-id="f5524-122">Desplácese hasta encontrar el campo que va a definir.</span><span class="sxs-lookup"><span data-stu-id="f5524-122">Scroll to find the field you are defining.</span></span>
2. <span data-ttu-id="f5524-123">Si no ha marcado el campo como de búsqueda, haga clic en la casilla para marcarla como **Permite búsqueda**.</span><span class="sxs-lookup"><span data-stu-id="f5524-123">If you haven't marked the field as searchable, click the checkbox now to mark it as **Searchable**.</span></span>
3. <span data-ttu-id="f5524-124">Haga clic en el área Analizador para mostrar la lista de analizadores disponibles.</span><span class="sxs-lookup"><span data-stu-id="f5524-124">Click the Analyzer area to display the list of available analyzers.</span></span>
4. <span data-ttu-id="f5524-125">Elija el analizador que desea usar.</span><span class="sxs-lookup"><span data-stu-id="f5524-125">Choose the analyzer you want to use.</span></span>

<span data-ttu-id="f5524-126">![][2]
*Seleccione uno de los analizadores compatibles para cada campo*.</span><span class="sxs-lookup"><span data-stu-id="f5524-126">![][2]
*Select one of the supported analyzers for each field*</span></span>

<span data-ttu-id="f5524-127">De forma predeterminada, todos los campos en los que se puede buscar usan el [analizador Standard Lucene](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) , que no depende del idioma.</span><span class="sxs-lookup"><span data-stu-id="f5524-127">By default, all searchable fields use the [Standard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) which is language agnostic.</span></span> <span data-ttu-id="f5524-128">Para ver la lista completa de los analizadores compatibles, consulte [Compatibilidad de idioma (API de REST de servicio de Búsqueda de Azure)](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span><span class="sxs-lookup"><span data-stu-id="f5524-128">To view the full list of supported analyzers, see [Language Support in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span></span>

<span data-ttu-id="f5524-129">Una vez que el analizador de idioma está activado para un campo, se usará con cada solicitud de búsqueda e indexación para ese campo.</span><span class="sxs-lookup"><span data-stu-id="f5524-129">Once the language analyzer is selected for a field, it will be used with each indexing and search request for that field.</span></span> <span data-ttu-id="f5524-130">Cuando se emite una consulta en varios campos con diferentes analizadores, la consulta se procesará de manera independiente por los analizadores correctos para cada campo.</span><span class="sxs-lookup"><span data-stu-id="f5524-130">When a query is issued against multiple fields using different analyzers, the query will be processed independently by the right analyzers for each field.</span></span>

<span data-ttu-id="f5524-131">Muchas aplicaciones web y móviles dan servicio a usuarios de todo el mundo que usan diferentes idiomas.</span><span class="sxs-lookup"><span data-stu-id="f5524-131">Many web and mobile applications serve users around the globe using different languages.</span></span> <span data-ttu-id="f5524-132">Es posible definir un índice para un escenario similar al siguiente al crear un campo para cada idioma admitido.</span><span class="sxs-lookup"><span data-stu-id="f5524-132">It’s possible to define an index for a scenario like this by creating a field for each language supported.</span></span>

<span data-ttu-id="f5524-133">![][3]
*Definición de índice con un campo de descripción para cada idioma admitido*</span><span class="sxs-lookup"><span data-stu-id="f5524-133">![][3]
*Index definition with a description field for each language supported*</span></span>

<span data-ttu-id="f5524-134">Si se conoce el idioma del agente que emite una consulta, una solicitud de búsqueda se puede aplicar a un campo específico con el parámetro de consulta **searchFields** .</span><span class="sxs-lookup"><span data-stu-id="f5524-134">If the language of the agent issuing a query is known, a search request can be scoped to a specific field using the **searchFields** query parameter.</span></span> <span data-ttu-id="f5524-135">La siguiente consulta solo se emitirá en relación a la descripción en polaco:</span><span class="sxs-lookup"><span data-stu-id="f5524-135">The following query will be issued only against the description in Polish:</span></span>

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

<span data-ttu-id="f5524-136">Puede consultar el índice desde el portal con el **Explorador de búsqueda** para pegar una consulta similar a la mostrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f5524-136">You can query your index from the portal, using **Search explorer** to paste in a query similar to the one shown above.</span></span> <span data-ttu-id="f5524-137">El Explorador de búsqueda está disponible en la barra de comandos de la hoja del servicio.</span><span class="sxs-lookup"><span data-stu-id="f5524-137">Search explorer is available from the command bar in the service blade.</span></span> <span data-ttu-id="f5524-138">Para obtener más información, consulte [Consultas en Búsqueda de Azure.](search-explorer.md)</span><span class="sxs-lookup"><span data-stu-id="f5524-138">See [Query your Azure Search index in the portal](search-explorer.md) for details.</span></span>

<span data-ttu-id="f5524-139">A veces se desconoce el idioma del agente que emite una consulta, en cuyo caso la consulta puede emitir en todos los campos al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="f5524-139">Sometimes the language of the agent issuing a query is not known, in which case the query can be issued against all fields simultaneously.</span></span> <span data-ttu-id="f5524-140">Si es necesario, se pueden definir una preferencia de resultados en un determinado idioma mediante [perfiles de puntuación](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="f5524-140">If needed, preference for results in a certain language can be defined using [scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span> <span data-ttu-id="f5524-141">En el ejemplo siguiente, las coincidencias encontradas en la descripción en inglés tendrán una puntuación mayor que las coincidencias en polaco y francés:</span><span class="sxs-lookup"><span data-stu-id="f5524-141">In the example below, matches found in the description in English will be scored higher relative to matches in Polish and French:</span></span>

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

<span data-ttu-id="f5524-142">Si es desarrollador de. NET, tenga en cuenta que puede configurar los analizadores de idioma mediante el [SDK de Azure Search para .NET](http://www.nuget.org/packages/Microsoft.Azure.Search).</span><span class="sxs-lookup"><span data-stu-id="f5524-142">If you're a .NET developer, note that you can configure language analyzers using the [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span></span> <span data-ttu-id="f5524-143">La última versión incluye compatibilidad con los analizadores de idioma de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f5524-143">The latest release includes support for the Microsoft language analyzers as well.</span></span>

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
