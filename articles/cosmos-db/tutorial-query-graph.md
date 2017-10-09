---
title: "¿aaaHow tooquery datos del gráfico en la base de datos de Azure Cosmos? | Microsoft Docs"
description: "Obtenga información acerca de los datos del gráfico tooquery en la base de datos de Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 8bde5c80-581c-4f70-acb4-9578873c92fa
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: fdde881edd6c488e2fea51e5c9665e1d736009fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-hello-graph-api-preview"></a><span data-ttu-id="e0266-104">Azure Cosmos DB: Cómo Hola tooquery con API Graph (versión preliminar)?</span><span class="sxs-lookup"><span data-stu-id="e0266-104">Azure Cosmos DB: How tooquery with hello Graph API (preview)?</span></span>

<span data-ttu-id="e0266-105">base de datos de Azure Cosmos Hello [API Graph](graph-introduction.md) (vista previa) es compatible con [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) consultas.</span><span class="sxs-lookup"><span data-stu-id="e0266-105">hello Azure Cosmos DB [Graph API](graph-introduction.md) (preview) supports [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) queries.</span></span> <span data-ttu-id="e0266-106">Este artículo proporciona ejemplos de documentos y consultas tooget que se inició.</span><span class="sxs-lookup"><span data-stu-id="e0266-106">This article provides sample documents and queries tooget you started.</span></span> <span data-ttu-id="e0266-107">Se proporciona una referencia detallada de Gremlin en hello [compatibilidad Gremlin](gremlin-support.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="e0266-107">A detailed Gremlin reference is provided in hello [Gremlin support](gremlin-support.md) article.</span></span>

<span data-ttu-id="e0266-108">En este artículo se trata Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="e0266-108">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="e0266-109">Consulta de datos con Gremlin</span><span class="sxs-lookup"><span data-stu-id="e0266-109">Querying data with Gremlin</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0266-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e0266-110">Prerequisites</span></span>

<span data-ttu-id="e0266-111">Para estos toowork consultas, debe tener una cuenta de base de datos de Azure Cosmos y tener datos de gráfico en el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0266-111">For these queries toowork, you must have an Azure Cosmos DB account and have graph data in hello container.</span></span> <span data-ttu-id="e0266-112">¿No tiene nada de lo anterior?</span><span class="sxs-lookup"><span data-stu-id="e0266-112">Don't have any of those?</span></span> <span data-ttu-id="e0266-113">Hola completa [inicio rápido de 5 minutos](create-graph-dotnet.md) o hello [tutorial de programadores](tutorial-query-graph.md) toocreate una cuenta y rellenar la base de datos.</span><span class="sxs-lookup"><span data-stu-id="e0266-113">Complete hello [5-minute quickstart](create-graph-dotnet.md) or hello [developer tutorial](tutorial-query-graph.md) toocreate an account and populate your database.</span></span> <span data-ttu-id="e0266-114">Puede ejecutar hello las siguientes consultas con hello [biblioteca de .NET de base de datos de Azure Cosmos graph](graph-sdk-dotnet.md), [consola Gremlin](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), o el controlador Gremlin favoritos.</span><span class="sxs-lookup"><span data-stu-id="e0266-114">You can run hello following queries using hello [Azure Cosmos DB .NET graph library](graph-sdk-dotnet.md), [Gremlin console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), or your favorite Gremlin driver.</span></span>

## <a name="count-vertices-in-hello-graph"></a><span data-ttu-id="e0266-115">Recuento de vértices en el gráfico de Hola</span><span class="sxs-lookup"><span data-stu-id="e0266-115">Count vertices in hello graph</span></span>

<span data-ttu-id="e0266-116">Hola siguiente fragmento de código muestra cómo toocount Hola número de vértices en el gráfico de hello:</span><span class="sxs-lookup"><span data-stu-id="e0266-116">hello following snippet shows how toocount hello number of vertices in hello graph:</span></span>

```
g.V().count()
```

## <a name="filters"></a><span data-ttu-id="e0266-117">Filtros</span><span class="sxs-lookup"><span data-stu-id="e0266-117">Filters</span></span>

<span data-ttu-id="e0266-118">Puede realizar filtros utilizando del Gremlin `has` y `hasLabel` los pasos y combinarlos con `and`, `or`, y `not` toobuild los filtros más complejos.</span><span class="sxs-lookup"><span data-stu-id="e0266-118">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` toobuild more complex filters.</span></span> <span data-ttu-id="e0266-119">Azure Cosmos DB proporciona indexación independiente del esquema de todas las propiedades de los vértices y grados para consultas rápidas:</span><span class="sxs-lookup"><span data-stu-id="e0266-119">Azure Cosmos DB provides schema-agnostic indexing of all properties within your vertices and degrees for fast queries:</span></span>

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a><span data-ttu-id="e0266-120">Proyección</span><span class="sxs-lookup"><span data-stu-id="e0266-120">Projection</span></span>

<span data-ttu-id="e0266-121">Puede proyectar ciertas propiedades de resultados de la consulta de hello mediante hello `values` paso:</span><span class="sxs-lookup"><span data-stu-id="e0266-121">You can project certain properties in hello query results using hello `values` step:</span></span>

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a><span data-ttu-id="e0266-122">Búsqueda de bordes y vértices relacionados</span><span class="sxs-lookup"><span data-stu-id="e0266-122">Find related edges and vertices</span></span>

<span data-ttu-id="e0266-123">Hasta ahora, solo hemos visto operadores de consulta que funcionan en cualquier base de datos.</span><span class="sxs-lookup"><span data-stu-id="e0266-123">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="e0266-124">Gráficos son rápidos y eficaces para las operaciones de recorrido cuando necesite toonavigate toorelated bordes y vértices.</span><span class="sxs-lookup"><span data-stu-id="e0266-124">Graphs are fast and efficient for traversal operations when you need toonavigate toorelated edges and vertices.</span></span> <span data-ttu-id="e0266-125">Encontremos a todos los amigos de Thomas.</span><span class="sxs-lookup"><span data-stu-id="e0266-125">Let's find all friends of Thomas.</span></span> <span data-ttu-id="e0266-126">Hacer esto mediante el uso del Gremlin `outE` paso toofind Hola todos los out-bordes de Thomas, a continuación, recorrer toohello vértices respecto a los bordes del Gremlin `inV` paso:</span><span class="sxs-lookup"><span data-stu-id="e0266-126">We do this by using Gremlin's `outE` step toofind all hello out-edges from Thomas, then traversing toohello in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="e0266-127">realiza la siguiente consulta de Hello toofind de dos saltos todos "Amigos de amigos" de Thomas, mediante una llamada a `outE` y `inV` dos veces.</span><span class="sxs-lookup"><span data-stu-id="e0266-127">hello next query performs two hops toofind all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="e0266-128">Puede crear consultas más complejas e implementar lógica de cruce seguro de gráfico eficaz mediante Gremlin, filtro de combinación incluido Hola de expresiones, realizar el bucle con `loop` paso y la implementación de navegación condicional mediante hello `choose` paso.</span><span class="sxs-lookup"><span data-stu-id="e0266-128">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using hello `loop` step, and implementing conditional navigation using hello `choose` step.</span></span> <span data-ttu-id="e0266-129">Obtenga más información sobre lo que puede hacer con [Compatibilidad con Gremlin](gremlin-support.md).</span><span class="sxs-lookup"><span data-stu-id="e0266-129">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0266-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e0266-130">Next steps</span></span>

<span data-ttu-id="e0266-131">En este tutorial, ha hecho siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="e0266-131">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e0266-132">Ha aprendido cómo tooquery mediante Graph</span><span class="sxs-lookup"><span data-stu-id="e0266-132">Learned how tooquery using Graph</span></span> 

<span data-ttu-id="e0266-133">Ahora puede continuar toohello siguiente tutorial toolearn cómo toodistribute los datos globales.</span><span class="sxs-lookup"><span data-stu-id="e0266-133">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e0266-134">Distribución de datos global</span><span class="sxs-lookup"><span data-stu-id="e0266-134">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)