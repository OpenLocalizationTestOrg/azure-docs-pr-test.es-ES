---
title: rendimiento de aaaTroubleshoot problemas y optimizar la base de datos | Documentos de Microsoft
description: "Aplicar recomendaciones de rendimiento tooyour base de datos SQL así como borrar cómo toogain información acerca de Hola rendimiento de las consultas de Hola que se ejecuta en la base de datos"
metakeywords: azure sql database performance monitoring recommendation
services: sql-database
documentationcenter: 
manager: jhubbard
author: jan-eng
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,monitor & tune
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: janeng
ms.openlocfilehash: e948d30ac74eecf45420d5d77ef55e3c0b6f3f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a><span data-ttu-id="ed06b-103">Solución de problemas de rendimiento y optimización de bases de datos</span><span class="sxs-lookup"><span data-stu-id="ed06b-103">Troubleshoot performance issues and optimize your database</span></span>

<span data-ttu-id="ed06b-104">Entre los motivos comunes para un rendimiento deficiente de la base de datos se encuentran índices que faltan y consultas mal optimizadas.</span><span class="sxs-lookup"><span data-stu-id="ed06b-104">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="ed06b-105">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="ed06b-105">In this tutorial you learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="ed06b-106">Revisar, aplicar y revertir las recomendaciones para la mejora de rendimiento</span><span class="sxs-lookup"><span data-stu-id="ed06b-106">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="ed06b-107">Buscar consultas con un uso intensivo de los recursos</span><span class="sxs-lookup"><span data-stu-id="ed06b-107">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="ed06b-108">Buscar consultas de ejecución prolongada</span><span class="sxs-lookup"><span data-stu-id="ed06b-108">Find long running queries</span></span>

> <span data-ttu-id="ed06b-109">Necesita una carga de trabajo continua en una base de datos con problemas de rendimiento: falta un índice, por ejemplo tooreceive una recomendación.</span><span class="sxs-lookup"><span data-stu-id="ed06b-109">You need a continuous workload on a database with performance issues – missing an index for example tooreceive a recommendation.</span></span>
>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="ed06b-110">Inicie sesión en toohello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ed06b-110">Log in toohello Azure portal</span></span>

<span data-ttu-id="ed06b-111">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ed06b-111">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="review-and-apply-a-recommendation"></a><span data-ttu-id="ed06b-112">Revisión y aplicación de una recomendación</span><span class="sxs-lookup"><span data-stu-id="ed06b-112">Review and apply a recommendation</span></span>

<span data-ttu-id="ed06b-113">Siga estos tooapply pasos una recomendación de sistema de hello para la base de datos:</span><span class="sxs-lookup"><span data-stu-id="ed06b-113">Follow these steps tooapply a recommendation from hello system for your database:</span></span>

1. <span data-ttu-id="ed06b-114">Haga clic en hello **recomendaciones de rendimiento** menú en la hoja de la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed06b-114">Click hello **Performance recommendations** menu in hello database blade.</span></span>

    ![recomendación de rendimiento](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. <span data-ttu-id="ed06b-116">Seleccionar una recomendación de active en hello lista de recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="ed06b-116">From hello list of recommendations, select an active recommendation.</span></span> <span data-ttu-id="ed06b-117">En este ejemplo, Create Index.</span><span class="sxs-lookup"><span data-stu-id="ed06b-117">In this example, Create Index.</span></span>

    ![seleccionar recomendación](./media/sql-database-performance-tutorial/create_index.png)

3. <span data-ttu-id="ed06b-119">Aplique la recomendación de hello haciendo clic en hello **aplicar** botón.</span><span class="sxs-lookup"><span data-stu-id="ed06b-119">Apply hello recommendation by clicking hello **Apply** button.</span></span> <span data-ttu-id="ed06b-120">Si lo desea, revise los detalles de la recomendación de Hola y ver script de Hola T-SQL ejecutará demasiado haciendo clic en **ver Script** botón.</span><span class="sxs-lookup"><span data-stu-id="ed06b-120">Optionally, review hello recommendation details and see hello T-SQL script too be executed by clicking on **View Script** button.</span></span>

    ![aplicar recomendación](./media/sql-database-performance-tutorial/apply.png)

4. <span data-ttu-id="ed06b-122">[Opcional] Habilitar el ajuste automático para toobe de recomendaciones que se aplican automáticamente.</span><span class="sxs-lookup"><span data-stu-id="ed06b-122">[Optional] Enable automatic tuning for recommendations toobe applied automatically.</span></span>

    ![ajuste automático](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a><span data-ttu-id="ed06b-124">Reversión de una recomendación</span><span class="sxs-lookup"><span data-stu-id="ed06b-124">Revert a recommendation</span></span>

<span data-ttu-id="ed06b-125">Hola Asesor de la base de datos supervisa cada recomendación implementado.</span><span class="sxs-lookup"><span data-stu-id="ed06b-125">hello Database Advisor monitors every recommendation implemented.</span></span> <span data-ttu-id="ed06b-126">Si una recomendación no mejora la carga de trabajo de Hola se revertirán automáticamente.</span><span class="sxs-lookup"><span data-stu-id="ed06b-126">If a recommendation doesn't improve hello workload it will be automatically reverted.</span></span> <span data-ttu-id="ed06b-127">Cualquier recomendación se puede revertir, pero en la mayoría de los casos no es necesario.</span><span class="sxs-lookup"><span data-stu-id="ed06b-127">Manually reverting a recommendation is possible, but not necessary in most cases.</span></span> <span data-ttu-id="ed06b-128">toorevert una recomendación:</span><span class="sxs-lookup"><span data-stu-id="ed06b-128">toorevert a recommendation:</span></span>

1. <span data-ttu-id="ed06b-129">Vaya el menú de las recomendaciones de rendimiento de toohello y seleccione una de las recomendaciones de hello aplica.</span><span class="sxs-lookup"><span data-stu-id="ed06b-129">Go toohello performance recommendations menu and select one of hello applied recommendations.</span></span>

    ![seleccionar recomendación](./media/sql-database-performance-tutorial/select.png)

2. <span data-ttu-id="ed06b-131">En la vista de detalles de hello, haga clic en **Revert**.</span><span class="sxs-lookup"><span data-stu-id="ed06b-131">In hello details view, click **Revert**.</span></span>

    ![revertir recomendación](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-hello-query-that-consumes-hello-most-resources"></a><span data-ttu-id="ed06b-133">Encontrar más recursos de consulta de Hola que consume Hola</span><span class="sxs-lookup"><span data-stu-id="ed06b-133">Find hello query that consumes hello most resources</span></span>

<span data-ttu-id="ed06b-134">Siga estas consultas de hello pasos toofind consumiendo Hola mayoría de los recursos:</span><span class="sxs-lookup"><span data-stu-id="ed06b-134">Follow these steps toofind hello query consuming hello most resources:</span></span>

1. <span data-ttu-id="ed06b-135">Haga clic en hello **Query Performance Insight** menú en la hoja de la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed06b-135">Click on hello **Query Performance Insight** menu in hello database blade.</span></span>

    ![información de consultas](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. <span data-ttu-id="ed06b-137">Seleccione de un tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="ed06b-137">Select a resource type.</span></span>

    ![información de consultas](./media/sql-database-performance-tutorial/select_resource_type.png)

3. <span data-ttu-id="ed06b-139">Hola seleccione primera consulta de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed06b-139">Select hello first query in hello table.</span></span>

    ![información de consultas](./media/sql-database-performance-tutorial/select_query.png)

4. <span data-ttu-id="ed06b-141">Revise los detalles de la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed06b-141">Review hello query details.</span></span>

    ![información de consultas](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-hello-longest-running-query"></a><span data-ttu-id="ed06b-143">Buscar consultas de ejecución más larga de Hola</span><span class="sxs-lookup"><span data-stu-id="ed06b-143">Find hello longest running query</span></span>

1. <span data-ttu-id="ed06b-144">Vaya tooQuery Performance Insight y seleccione hello **consultas de larga ejecución** ficha.</span><span class="sxs-lookup"><span data-stu-id="ed06b-144">Go tooQuery Performance Insight and select hello **Long running queries** tab.</span></span>

    ![información de consultas](./media/sql-database-performance-tutorial/long_running.png)

3. <span data-ttu-id="ed06b-146">Hola seleccione primera consulta de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed06b-146">Select hello first query in hello table.</span></span>

    ![información de consultas](./media/sql-database-performance-tutorial/select_first_query.png)

4. <span data-ttu-id="ed06b-148">Revise los detalles de la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed06b-148">Review hello query details.</span></span>

    ![información de consultas](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a><span data-ttu-id="ed06b-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ed06b-150">Next steps</span></span> 
<span data-ttu-id="ed06b-151">Entre los motivos comunes para un rendimiento deficiente de la base de datos se encuentran índices que faltan y consultas mal optimizadas.</span><span class="sxs-lookup"><span data-stu-id="ed06b-151">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="ed06b-152">En este tutorial aprendió lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ed06b-152">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="ed06b-153">Revisar, aplicar y revertir las recomendaciones para la mejora de rendimiento</span><span class="sxs-lookup"><span data-stu-id="ed06b-153">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="ed06b-154">Buscar consultas con un uso intensivo de los recursos</span><span class="sxs-lookup"><span data-stu-id="ed06b-154">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="ed06b-155">Buscar consultas de ejecución prolongada</span><span class="sxs-lookup"><span data-stu-id="ed06b-155">Find long running queries</span></span>

[<span data-ttu-id="ed06b-156">Sugerencias para la optimización del rendimiento de Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="ed06b-156">SQL Database performance tuning tips</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
