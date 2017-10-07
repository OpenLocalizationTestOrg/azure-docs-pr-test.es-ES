---
title: "aaa \"consultar un índice (portal - búsqueda de Azure) | Documentos de Microsoft\""
description: "Emitir una consulta de búsqueda en el Explorador de búsqueda del Portal de Azure Hola."
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 8e524188-73a7-44db-9e64-ae8bf66b05d3
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 07/10/2017
ms.author: ashmaka
ms.openlocfilehash: 56bab3ef8a66eeb053fbbeb6d322acb6824fb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-hello-azure-portal"></a><span data-ttu-id="c8b44-103">Consultar un índice de búsqueda de Azure mediante el Explorador de búsqueda en hello Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c8b44-103">Query an Azure Search index using Search Explorer in hello Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c8b44-104">Información general</span><span class="sxs-lookup"><span data-stu-id="c8b44-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="c8b44-105">Portal</span><span class="sxs-lookup"><span data-stu-id="c8b44-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="c8b44-106">.NET</span><span class="sxs-lookup"><span data-stu-id="c8b44-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="c8b44-107">REST</span><span class="sxs-lookup"><span data-stu-id="c8b44-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="c8b44-108">Este artículo muestra cómo tooquery una búsqueda de Azure INDICE mediante **buscar en el explorador** Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c8b44-108">This article shows you how tooquery an Azure Search index using **Search Explorer** in hello Azure portal.</span></span> <span data-ttu-id="c8b44-109">Puede usar Buscar en el explorador toosubmit simple o completo Lucene consulta cadenas tooany índice existente en el servicio.</span><span class="sxs-lookup"><span data-stu-id="c8b44-109">You can use Search Explorer toosubmit simple or full Lucene query strings tooany existing index in your service.</span></span>

## <a name="open-hello-service-dashboard"></a><span data-ttu-id="c8b44-110">Panel de servicio de hello abierto</span><span class="sxs-lookup"><span data-stu-id="c8b44-110">Open hello service dashboard</span></span>
1. <span data-ttu-id="c8b44-111">Haga clic en **todos los recursos** en la barra de salto de hello en la parte izquierda de Hola de hello [portal de Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span><span class="sxs-lookup"><span data-stu-id="c8b44-111">Click **All resources** in hello jump bar on hello left side of hello [Azure portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span></span>
2. <span data-ttu-id="c8b44-112">Seleccione el servicio Azure Search.</span><span class="sxs-lookup"><span data-stu-id="c8b44-112">Select your Azure Search service.</span></span>

## <a name="select-an-index"></a><span data-ttu-id="c8b44-113">Seleccionar un índice</span><span class="sxs-lookup"><span data-stu-id="c8b44-113">Select an index</span></span>

<span data-ttu-id="c8b44-114">Índice de hello seleccione le gustaría toosearch de hello **índices** icono.</span><span class="sxs-lookup"><span data-stu-id="c8b44-114">Select hello index you would like toosearch from hello **Indexes** tile.</span></span>

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a><span data-ttu-id="c8b44-115">Abrir el Explorador de búsqueda</span><span class="sxs-lookup"><span data-stu-id="c8b44-115">Open Search Explorer</span></span>

<span data-ttu-id="c8b44-116">Haga clic en hello barra de búsqueda de búsqueda del explorador mosaico tooslide Hola abierto y panel de resultados.</span><span class="sxs-lookup"><span data-stu-id="c8b44-116">Click on hello Search Explorer tile tooslide open hello search bar and results pane.</span></span>

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a><span data-ttu-id="c8b44-117">Inicio de la búsqueda</span><span class="sxs-lookup"><span data-stu-id="c8b44-117">Start searching</span></span>

<span data-ttu-id="c8b44-118">Al utilizar Hola buscar en el explorador, se puede especificar [parámetros de consulta](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) consulta de hello tooformulate.</span><span class="sxs-lookup"><span data-stu-id="c8b44-118">When using hello Search Explorer, you can specify [query parameters](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) tooformulate hello query.</span></span>

1. <span data-ttu-id="c8b44-119">En **Cadena de consulta**, escriba una consulta y pulse **Buscar**.</span><span class="sxs-lookup"><span data-stu-id="c8b44-119">In **Query string**, type a query and then press **Search**.</span></span> 

   <span data-ttu-id="c8b44-120">cadena de consulta de Hola se analiza automáticamente en la solicitud correcta de hello URL toosubmit una solicitud HTTP en hello API de REST de búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="c8b44-120">hello query string is automatically parsed into hello proper request URL toosubmit a HTTP request against hello Azure Search REST API.</span></span>   
   
   <span data-ttu-id="c8b44-121">Puede usar cualquier válido simple o completo Lucene sintaxis toocreate Hola solicitud de consulta.</span><span class="sxs-lookup"><span data-stu-id="c8b44-121">You can use any valid simple or full Lucene query syntax toocreate hello request.</span></span> <span data-ttu-id="c8b44-122">Hola `*` carácter es búsqueda vacía o sin especificar tooan equivalente que devuelve todos los documentos sin ningún orden determinado.</span><span class="sxs-lookup"><span data-stu-id="c8b44-122">hello `*` character is equivalent tooan empty or unspecified search that returns all documents in no particular order.</span></span>

2. <span data-ttu-id="c8b44-123">En **resultados**, resultados de la consulta se presentan en JSON sin formato, carga toohello idénticos que se devuelve en un cuerpo de respuesta HTTP al emitir solicitudes mediante programación.</span><span class="sxs-lookup"><span data-stu-id="c8b44-123">In  **Results**, query results are presented in raw JSON, identical toohello payload returned in an HTTP Response Body when issuing requests programmatically.</span></span>

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a><span data-ttu-id="c8b44-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c8b44-124">Next steps</span></span>

<span data-ttu-id="c8b44-125">Hola recursos siguientes proporciona ejemplos y la información de la sintaxis de consulta adicionales.</span><span class="sxs-lookup"><span data-stu-id="c8b44-125">hello following resources provide additional query syntax information and examples.</span></span>

 + [<span data-ttu-id="c8b44-126">Sintaxis de consulta simplificada</span><span class="sxs-lookup"><span data-stu-id="c8b44-126">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [<span data-ttu-id="c8b44-127">Sintaxis de consulta de Lucene</span><span class="sxs-lookup"><span data-stu-id="c8b44-127">Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [<span data-ttu-id="c8b44-128">Ejemplos de sintaxis de consulta de Lucene para la creación de consultas en Azure Search</span><span class="sxs-lookup"><span data-stu-id="c8b44-128">Lucene query syntax examples</span></span>](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + <span data-ttu-id="c8b44-129">[OData Expression Syntax for Azure Search](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) (Sintaxis de expresiones de OData en Azure Search)</span><span class="sxs-lookup"><span data-stu-id="c8b44-129">[OData Filter expression syntax](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search)</span></span> 