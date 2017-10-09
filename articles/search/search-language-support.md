---
title: "aaaAzure multilingüe de búsqueda | Documentos de Microsoft"
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
ms.openlocfilehash: 9a2e567a82ee563521c12ea320f6c484a8e73f04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a><span data-ttu-id="f972a-103">Creación de un índice para documentos en varios idiomas en Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="f972a-103">Create an index for documents in multiple languages in Azure Search</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="f972a-104">Portal</span><span class="sxs-lookup"><span data-stu-id="f972a-104">Portal</span></span>](search-language-support.md)
> * [<span data-ttu-id="f972a-105">REST</span><span class="sxs-lookup"><span data-stu-id="f972a-105">REST</span></span>](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [<span data-ttu-id="f972a-106">.NET</span><span class="sxs-lookup"><span data-stu-id="f972a-106">.NET</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

<span data-ttu-id="f972a-107">Unleashing power Hola de analizadores de lenguaje es tan fácil como una propiedad de configuración en un campo de búsqueda en la definición del índice Hola.</span><span class="sxs-lookup"><span data-stu-id="f972a-107">Unleashing hello power of language analyzers is as easy as setting one property on a searchable field in hello index definition.</span></span> <span data-ttu-id="f972a-108">Ahora puede realizar este paso en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="f972a-108">Now you can do this step in hello portal.</span></span>

<span data-ttu-id="f972a-109">A continuación se muestran capturas de pantalla de hello hojas de Portal de Azure para la búsqueda de Azure que permiten a los usuarios toodefine un esquema de índice.</span><span class="sxs-lookup"><span data-stu-id="f972a-109">Below are screenshots of hello Azure Portal blades for Azure Search that allow users toodefine an index schema.</span></span> <span data-ttu-id="f972a-110">Desde esta hoja, los usuarios pueden crear todos los campos de Hola y establecer la propiedad de analizador de Hola para cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="f972a-110">From this blade, users can create all of hello fields and set hello analyzer property for each of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f972a-111">Solo puede establecer un analizador de lenguaje durante la definición del campo, como en cuando cree un nuevo índice de hello descárguese de corriente, o cuando se agrega un nuevo índice existente de tooan de campo.</span><span class="sxs-lookup"><span data-stu-id="f972a-111">You can only set a language analyzer during field definition, as in when creating a new index from hello ground up, or when adding a new field tooan existing index.</span></span> <span data-ttu-id="f972a-112">Asegúrese de que especificar completamente todos los atributos, como analizador de hello, al crear el campo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f972a-112">Make sure you fully specify all attributes, including hello analyzer, while creating hello field.</span></span> <span data-ttu-id="f972a-113">No ser capaz de tooedit atributos de Hola o cambiar el tipo de analizador de hello una vez que guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="f972a-113">You won't be able tooedit hello attributes or change hello analyzer type once you save your changes.</span></span>
>
>

## <a name="define-a-new-field-definition"></a><span data-ttu-id="f972a-114">Definición de una nueva definición de campo</span><span class="sxs-lookup"><span data-stu-id="f972a-114">Define a new field definition</span></span>
1. <span data-ttu-id="f972a-115">Inicie sesión en toohello [portal de Azure](https://portal.azure.com) y hoja de servicio de hello abierto de su servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="f972a-115">Sign in toohello [Azure portal](https://portal.azure.com) and open hello service blade of your search service.</span></span>
2. <span data-ttu-id="f972a-116">Haga clic en **agregar índice** de comando de hello barra princip Hola de hello servicio panel toostart un nuevo índice, o abrir un tooset índice existente en nuevos campos que se va a agregar un analizador de índice existente tooan.</span><span class="sxs-lookup"><span data-stu-id="f972a-116">Click **Add index** in hello command bar at hello top of hello service dashboard toostart a new index, or open an existing index tooset an analyzer on new fields you're adding tooan existing index.</span></span>
3. <span data-ttu-id="f972a-117">aparece la hoja de campos de Hello, lo que le ofrece opciones para definir el esquema de Hola de índice de hello, incluido tab del analizador de Hola utiliza para elegir un analizador de lenguaje.</span><span class="sxs-lookup"><span data-stu-id="f972a-117">hello Fields blade appears, giving you options for defining hello schema of hello index, including hello Analyzer tab used for choosing a language analyzer.</span></span>
4. <span data-ttu-id="f972a-118">En los campos, inicie una definición de campo proporcionar un nombre, Elegir tipo de datos de Hola y establecer campo de atributos toomark Hola como texto completo permite realizar búsquedas, puede recuperar en resultados de búsqueda, puede usar en las estructuras de navegación de faceta, que se puede ordenar y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="f972a-118">In Fields, start a field definition by providing a name, choosing hello data type, and setting attributes toomark hello field as full text searchable, retrievable in search results, usable in facet navigation structures, sortable, and so forth.</span></span>
5. <span data-ttu-id="f972a-119">Antes de continuar toohello siguiente campo, abra hello **analizador** ficha.</span><span class="sxs-lookup"><span data-stu-id="f972a-119">Before moving on toohello next field, open hello **Analyzer** tab.</span></span>

<span data-ttu-id="f972a-120">![][1]
*tooselect un analizador, haga clic en la ficha de analizador de hello en la hoja de campos de Hola*</span><span class="sxs-lookup"><span data-stu-id="f972a-120">![][1]
*tooselect an analyzer, click hello Analyzer tab on hello Fields blade*</span></span>

## <a name="choose-an-analyzer"></a><span data-ttu-id="f972a-121">Selección de un analizador</span><span class="sxs-lookup"><span data-stu-id="f972a-121">Choose an analyzer</span></span>
1. <span data-ttu-id="f972a-122">Campo de desplazamiento toofind Hola que se está definiendo.</span><span class="sxs-lookup"><span data-stu-id="f972a-122">Scroll toofind hello field you are defining.</span></span>
2. <span data-ttu-id="f972a-123">Si no ha marcado el campo hello como búsqueda, haga clic en hello casilla ahora toomark como **Searchable**.</span><span class="sxs-lookup"><span data-stu-id="f972a-123">If you haven't marked hello field as searchable, click hello checkbox now toomark it as **Searchable**.</span></span>
3. <span data-ttu-id="f972a-124">Haga clic en lista Hola analizador área toodisplay Hola de analizadores disponibles.</span><span class="sxs-lookup"><span data-stu-id="f972a-124">Click hello Analyzer area toodisplay hello list of available analyzers.</span></span>
4. <span data-ttu-id="f972a-125">Elija el analizador de hello desea toouse.</span><span class="sxs-lookup"><span data-stu-id="f972a-125">Choose hello analyzer you want toouse.</span></span>

<span data-ttu-id="f972a-126">![][2]
*Seleccione uno de los analizadores de hello admitido para cada campo*</span><span class="sxs-lookup"><span data-stu-id="f972a-126">![][2]
*Select one of hello supported analyzers for each field*</span></span>

<span data-ttu-id="f972a-127">De forma predeterminada, todos los campos que permiten búsqueda usan hello [analizador estándar Lucene](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) que es independiente del idioma.</span><span class="sxs-lookup"><span data-stu-id="f972a-127">By default, all searchable fields use hello [Standard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) which is language agnostic.</span></span> <span data-ttu-id="f972a-128">admite la lista completa de hello tooview de analizadores, consulte [compatibilidad con idiomas en búsqueda de Azure](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span><span class="sxs-lookup"><span data-stu-id="f972a-128">tooview hello full list of supported analyzers, see [Language Support in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span></span>

<span data-ttu-id="f972a-129">Una vez seleccionado el analizador de lenguaje de Hola para un campo, se utilizará con cada solicitud de búsqueda e indización para ese campo.</span><span class="sxs-lookup"><span data-stu-id="f972a-129">Once hello language analyzer is selected for a field, it will be used with each indexing and search request for that field.</span></span> <span data-ttu-id="f972a-130">Cuando se emite una consulta en varios campos mediante analizadores de diferentes, se procesarán independientemente consulta Hola analizadores de derecho de Hola para cada campo.</span><span class="sxs-lookup"><span data-stu-id="f972a-130">When a query is issued against multiple fields using different analyzers, hello query will be processed independently by hello right analyzers for each field.</span></span>

<span data-ttu-id="f972a-131">Muchas aplicaciones web y móviles atienden a usuarios mundo Hola con distintos idiomas.</span><span class="sxs-lookup"><span data-stu-id="f972a-131">Many web and mobile applications serve users around hello globe using different languages.</span></span> <span data-ttu-id="f972a-132">Es posible toodefine un índice para un escenario similar a éste mediante la creación de un campo para cada idioma admitido.</span><span class="sxs-lookup"><span data-stu-id="f972a-132">It’s possible toodefine an index for a scenario like this by creating a field for each language supported.</span></span>

<span data-ttu-id="f972a-133">![][3]
*Definición de índice con un campo de descripción para cada idioma admitido*</span><span class="sxs-lookup"><span data-stu-id="f972a-133">![][3]
*Index definition with a description field for each language supported*</span></span>

<span data-ttu-id="f972a-134">Si se conoce el idioma de Hola del agente de hello emitir una consulta, una solicitud de búsqueda puede ser tooa ámbito campo específico mediante hello **searchFields** parámetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="f972a-134">If hello language of hello agent issuing a query is known, a search request can be scoped tooa specific field using hello **searchFields** query parameter.</span></span> <span data-ttu-id="f972a-135">Hello siguiente consulta se emitirá solo para descripción de hello en polaco:</span><span class="sxs-lookup"><span data-stu-id="f972a-135">hello following query will be issued only against hello description in Polish:</span></span>

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

<span data-ttu-id="f972a-136">Puede consultar el índice desde el portal de hello, con **buscar en el explorador** toopaste en un toohello similar de consulta se muestra anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f972a-136">You can query your index from hello portal, using **Search explorer** toopaste in a query similar toohello one shown above.</span></span> <span data-ttu-id="f972a-137">Buscar en el explorador está disponible en la barra de comandos de hello en el módulo de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="f972a-137">Search explorer is available from hello command bar in hello service blade.</span></span> <span data-ttu-id="f972a-138">Vea [consultar el índice de búsqueda de Azure en el portal de hello](search-explorer.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="f972a-138">See [Query your Azure Search index in hello portal](search-explorer.md) for details.</span></span>

<span data-ttu-id="f972a-139">A veces hello idioma del agente de hello emitir una consulta no se conoce en qué caso Hola consulta se puede emitir en todos los campos al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="f972a-139">Sometimes hello language of hello agent issuing a query is not known, in which case hello query can be issued against all fields simultaneously.</span></span> <span data-ttu-id="f972a-140">Si es necesario, se pueden definir una preferencia de resultados en un determinado idioma mediante [perfiles de puntuación](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="f972a-140">If needed, preference for results in a certain language can be defined using [scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span> <span data-ttu-id="f972a-141">En el ejemplo de Hola siguiente, las coincidencias encontradas en la descripción de saludo en inglés será mayor toomatches relativa en polaco y francés:</span><span class="sxs-lookup"><span data-stu-id="f972a-141">In hello example below, matches found in hello description in English will be scored higher relative toomatches in Polish and French:</span></span>

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

<span data-ttu-id="f972a-142">Si es un desarrollador de .NET, tenga en cuenta que puede configurar los analizadores de lenguaje con hello [SDK de .NET de búsqueda de Azure](http://www.nuget.org/packages/Microsoft.Azure.Search).</span><span class="sxs-lookup"><span data-stu-id="f972a-142">If you're a .NET developer, note that you can configure language analyzers using hello [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span></span> <span data-ttu-id="f972a-143">versión más reciente de Hello incluye compatibilidad para analizadores de lenguaje de Microsoft de hello así.</span><span class="sxs-lookup"><span data-stu-id="f972a-143">hello latest release includes support for hello Microsoft language analyzers as well.</span></span>

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
