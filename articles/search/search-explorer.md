---
title: "Consulta de un índice (portal - Azure Search) | Microsoft Docs"
description: "Emita una consulta de búsqueda en el Explorador de búsqueda del Portal de Azure."
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
ms.openlocfilehash: dd68d8ed073bf7b8666ddef35a2f1f84df690b4b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-the-azure-portal"></a><span data-ttu-id="e5514-103">Consulta de un índice de Azure Search mediante el Explorador de búsqueda de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e5514-103">Query an Azure Search index using Search Explorer in the Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e5514-104">Información general</span><span class="sxs-lookup"><span data-stu-id="e5514-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="e5514-105">Portal</span><span class="sxs-lookup"><span data-stu-id="e5514-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="e5514-106">.NET</span><span class="sxs-lookup"><span data-stu-id="e5514-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="e5514-107">REST</span><span class="sxs-lookup"><span data-stu-id="e5514-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="e5514-108">En este artículo se muestra cómo consultar un índice de Azure Search mediante el **Explorador de búsqueda** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e5514-108">This article shows you how to query an Azure Search index using **Search Explorer** in the Azure portal.</span></span> <span data-ttu-id="e5514-109">El Explorador de búsqueda se puede usar para enviar cadenas de consulta de Lucene simples o completas para cualquier índice existente en el servicio.</span><span class="sxs-lookup"><span data-stu-id="e5514-109">You can use Search Explorer to submit simple or full Lucene query strings to any existing index in your service.</span></span>

## <a name="open-the-service-dashboard"></a><span data-ttu-id="e5514-110">Abrir el panel del servicio</span><span class="sxs-lookup"><span data-stu-id="e5514-110">Open the service dashboard</span></span>
1. <span data-ttu-id="e5514-111">Haga clic en **Todos los recursos** en la barra de acceso rápido del menú izquierdo de [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span><span class="sxs-lookup"><span data-stu-id="e5514-111">Click **All resources** in the jump bar on the left side of the [Azure portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span></span>
2. <span data-ttu-id="e5514-112">Seleccione el servicio Azure Search.</span><span class="sxs-lookup"><span data-stu-id="e5514-112">Select your Azure Search service.</span></span>

## <a name="select-an-index"></a><span data-ttu-id="e5514-113">Seleccionar un índice</span><span class="sxs-lookup"><span data-stu-id="e5514-113">Select an index</span></span>

<span data-ttu-id="e5514-114">Seleccione el índice en el que desea buscar con el icono **Índices**.</span><span class="sxs-lookup"><span data-stu-id="e5514-114">Select the index you would like to search from the **Indexes** tile.</span></span>

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a><span data-ttu-id="e5514-115">Abrir el Explorador de búsqueda</span><span class="sxs-lookup"><span data-stu-id="e5514-115">Open Search Explorer</span></span>

<span data-ttu-id="e5514-116">Haga clic en el icono del Explorador de búsqueda para abrir la barra de búsqueda y el panel de resultados.</span><span class="sxs-lookup"><span data-stu-id="e5514-116">Click on the Search Explorer tile to slide open the search bar and results pane.</span></span>

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a><span data-ttu-id="e5514-117">Inicio de la búsqueda</span><span class="sxs-lookup"><span data-stu-id="e5514-117">Start searching</span></span>

<span data-ttu-id="e5514-118">Cuando utilice el Explorador de búsqueda, puede especificar los [parámetros de consulta](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) para formular la consulta.</span><span class="sxs-lookup"><span data-stu-id="e5514-118">When using the Search Explorer, you can specify [query parameters](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) to formulate the query.</span></span>

1. <span data-ttu-id="e5514-119">En **Cadena de consulta**, escriba una consulta y pulse **Buscar**.</span><span class="sxs-lookup"><span data-stu-id="e5514-119">In **Query string**, type a query and then press **Search**.</span></span> 

   <span data-ttu-id="e5514-120">La cadena de consulta se analiza automáticamente en la dirección URL de solicitud adecuada para enviar una solicitud HTTP con la API de REST de Azure Search.</span><span class="sxs-lookup"><span data-stu-id="e5514-120">The query string is automatically parsed into the proper request URL to submit a HTTP request against the Azure Search REST API.</span></span>   
   
   <span data-ttu-id="e5514-121">Puede usar cualquier sintaxis de consulta de Lucene simple o completa válida para crear la solicitud.</span><span class="sxs-lookup"><span data-stu-id="e5514-121">You can use any valid simple or full Lucene query syntax to create the request.</span></span> <span data-ttu-id="e5514-122">El carácter `*` equivale a una búsqueda vacía o sin especificar que devuelve todos los documentos sin ningún orden determinado.</span><span class="sxs-lookup"><span data-stu-id="e5514-122">The `*` character is equivalent to an empty or unspecified search that returns all documents in no particular order.</span></span>

2. <span data-ttu-id="e5514-123">En **Resultados**, los resultados de las consultas se presentan en formato JSON sin formato, que son idénticos a la carga útil que se devuelve en un cuerpo de respuesta HTTP al emitir solicitudes mediante programación.</span><span class="sxs-lookup"><span data-stu-id="e5514-123">In  **Results**, query results are presented in raw JSON, identical to the payload returned in an HTTP Response Body when issuing requests programmatically.</span></span>

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a><span data-ttu-id="e5514-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e5514-124">Next steps</span></span>

<span data-ttu-id="e5514-125">Los siguientes recursos proporcionan ejemplos y la información de la sintaxis de consulta adicionales.</span><span class="sxs-lookup"><span data-stu-id="e5514-125">The following resources provide additional query syntax information and examples.</span></span>

 + [<span data-ttu-id="e5514-126">Sintaxis de consulta simplificada</span><span class="sxs-lookup"><span data-stu-id="e5514-126">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [<span data-ttu-id="e5514-127">Sintaxis de consulta de Lucene</span><span class="sxs-lookup"><span data-stu-id="e5514-127">Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [<span data-ttu-id="e5514-128">Ejemplos de sintaxis de consulta de Lucene para la creación de consultas en Azure Search</span><span class="sxs-lookup"><span data-stu-id="e5514-128">Lucene query syntax examples</span></span>](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + <span data-ttu-id="e5514-129">[OData Expression Syntax for Azure Search](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) (Sintaxis de expresiones de OData en Azure Search)</span><span class="sxs-lookup"><span data-stu-id="e5514-129">[OData Filter expression syntax](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search)</span></span> 