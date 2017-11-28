---
title: "Solución de problemas de rendimiento y optimización de bases de datos | Microsoft Docs"
description: "Aplique las recomendaciones de rendimiento a SQL Database y aprenda a obtener información acerca del rendimiento de las consultas que se ejecutan en la base de datos"
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
ms.openlocfilehash: f9ae96cdc80c347593f229cb2fce3f2d4d8e7caf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a><span data-ttu-id="7596b-103">Solución de problemas de rendimiento y optimización de bases de datos</span><span class="sxs-lookup"><span data-stu-id="7596b-103">Troubleshoot performance issues and optimize your database</span></span>

<span data-ttu-id="7596b-104">Entre los motivos comunes para un rendimiento deficiente de la base de datos se encuentran índices que faltan y consultas mal optimizadas.</span><span class="sxs-lookup"><span data-stu-id="7596b-104">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="7596b-105">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="7596b-105">In this tutorial you learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="7596b-106">Revisar, aplicar y revertir las recomendaciones para la mejora de rendimiento</span><span class="sxs-lookup"><span data-stu-id="7596b-106">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="7596b-107">Buscar consultas con un uso intensivo de los recursos</span><span class="sxs-lookup"><span data-stu-id="7596b-107">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="7596b-108">Buscar consultas de ejecución prolongada</span><span class="sxs-lookup"><span data-stu-id="7596b-108">Find long running queries</span></span>

> <span data-ttu-id="7596b-109">Necesita una carga de trabajo continua en una base de datos con problemas de rendimiento (por ejemplo, falta un índice para obtener una recomendación).</span><span class="sxs-lookup"><span data-stu-id="7596b-109">You need a continuous workload on a database with performance issues – missing an index for example to receive a recommendation.</span></span>
>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="7596b-110">Inicio de sesión en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7596b-110">Log in to the Azure portal</span></span>

<span data-ttu-id="7596b-111">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7596b-111">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="review-and-apply-a-recommendation"></a><span data-ttu-id="7596b-112">Revisión y aplicación de una recomendación</span><span class="sxs-lookup"><span data-stu-id="7596b-112">Review and apply a recommendation</span></span>

<span data-ttu-id="7596b-113">Siga estos pasos para aplicar una recomendación del sistema a la base de datos:</span><span class="sxs-lookup"><span data-stu-id="7596b-113">Follow these steps to apply a recommendation from the system for your database:</span></span>

1. <span data-ttu-id="7596b-114">Haga clic en el menú **Recomendaciones de rendimiento** de la hoja de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="7596b-114">Click the **Performance recommendations** menu in the database blade.</span></span>

    ![recomendación de rendimiento](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. <span data-ttu-id="7596b-116">En la lista de recomendaciones, seleccione una recomendación activa.</span><span class="sxs-lookup"><span data-stu-id="7596b-116">From the list of recommendations, select an active recommendation.</span></span> <span data-ttu-id="7596b-117">En este ejemplo, Create Index.</span><span class="sxs-lookup"><span data-stu-id="7596b-117">In this example, Create Index.</span></span>

    ![seleccionar recomendación](./media/sql-database-performance-tutorial/create_index.png)

3. <span data-ttu-id="7596b-119">Aplique la recomendación, para lo que debe hacer clic en el botón **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="7596b-119">Apply the recommendation by clicking the **Apply** button.</span></span> <span data-ttu-id="7596b-120">Opcionalmente, revise los detalles de la recomendación y vea el script de T-SQL que se ejecuta, para lo que debe hacer clic en el botón **Ver script**.</span><span class="sxs-lookup"><span data-stu-id="7596b-120">Optionally, review the recommendation details and see the T-SQL script to  be executed by clicking on **View Script** button.</span></span>

    ![aplicar recomendación](./media/sql-database-performance-tutorial/apply.png)

4. <span data-ttu-id="7596b-122">[Opcional] Habilite el ajuste automático para que las recomendaciones se apliquen automáticamente.</span><span class="sxs-lookup"><span data-stu-id="7596b-122">[Optional] Enable automatic tuning for recommendations to be applied automatically.</span></span>

    ![ajuste automático](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a><span data-ttu-id="7596b-124">Reversión de una recomendación</span><span class="sxs-lookup"><span data-stu-id="7596b-124">Revert a recommendation</span></span>

<span data-ttu-id="7596b-125">Database Advisor supervisa todas las recomendaciones implementadas.</span><span class="sxs-lookup"><span data-stu-id="7596b-125">The Database Advisor monitors every recommendation implemented.</span></span> <span data-ttu-id="7596b-126">Si una recomendación no mejora la carga de trabajo, se revertirá automáticamente.</span><span class="sxs-lookup"><span data-stu-id="7596b-126">If a recommendation doesn't improve the workload it will be automatically reverted.</span></span> <span data-ttu-id="7596b-127">Cualquier recomendación se puede revertir, pero en la mayoría de los casos no es necesario.</span><span class="sxs-lookup"><span data-stu-id="7596b-127">Manually reverting a recommendation is possible, but not necessary in most cases.</span></span> <span data-ttu-id="7596b-128">Para revertir una recomendación:</span><span class="sxs-lookup"><span data-stu-id="7596b-128">To revert a recommendation:</span></span>

1. <span data-ttu-id="7596b-129">Vaya al menú de recomendaciones de rendimiento y seleccione una de las recomendaciones aplicadas.</span><span class="sxs-lookup"><span data-stu-id="7596b-129">Go to the performance recommendations menu and select one of the applied recommendations.</span></span>

    ![seleccionar recomendación](./media/sql-database-performance-tutorial/select.png)

2. <span data-ttu-id="7596b-131">En la vista de detalles, haga clic en **Revertir**.</span><span class="sxs-lookup"><span data-stu-id="7596b-131">In the details view, click **Revert**.</span></span>

    ![revertir recomendación](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-the-query-that-consumes-the-most-resources"></a><span data-ttu-id="7596b-133">Busque la consulta que consume más recursos</span><span class="sxs-lookup"><span data-stu-id="7596b-133">Find the query that consumes the most resources</span></span>

<span data-ttu-id="7596b-134">Siga estos pasos para buscar la consulta que consume más recursos:</span><span class="sxs-lookup"><span data-stu-id="7596b-134">Follow these steps to find the query consuming the most resources:</span></span>

1. <span data-ttu-id="7596b-135">Haga clic en el menú **Información de rendimiento de consultas** de la hoja de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="7596b-135">Click on the **Query Performance Insight** menu in the database blade.</span></span>

    ![información de consultas](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. <span data-ttu-id="7596b-137">Seleccione de un tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="7596b-137">Select a resource type.</span></span>

    ![información de consultas](./media/sql-database-performance-tutorial/select_resource_type.png)

3. <span data-ttu-id="7596b-139">Seleccione la primera consulta de la tabla.</span><span class="sxs-lookup"><span data-stu-id="7596b-139">Select the first query in the table.</span></span>

    ![información de consultas](./media/sql-database-performance-tutorial/select_query.png)

4. <span data-ttu-id="7596b-141">Revise los detalles de la consulta.</span><span class="sxs-lookup"><span data-stu-id="7596b-141">Review the query details.</span></span>

    ![información de consultas](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-the-longest-running-query"></a><span data-ttu-id="7596b-143">Busque la consulta que más tarda en ejecutarse</span><span class="sxs-lookup"><span data-stu-id="7596b-143">Find the longest running query</span></span>

1. <span data-ttu-id="7596b-144">Vaya a Información de rendimiento de consultas y seleccione la pestaña **Consultas de larga ejecución**.</span><span class="sxs-lookup"><span data-stu-id="7596b-144">Go to Query Performance Insight and select the **Long running queries** tab.</span></span>

    ![información de consultas](./media/sql-database-performance-tutorial/long_running.png)

3. <span data-ttu-id="7596b-146">Seleccione la primera consulta de la tabla.</span><span class="sxs-lookup"><span data-stu-id="7596b-146">Select the first query in the table.</span></span>

    ![información de consultas](./media/sql-database-performance-tutorial/select_first_query.png)

4. <span data-ttu-id="7596b-148">Revise los detalles de la consulta.</span><span class="sxs-lookup"><span data-stu-id="7596b-148">Review the query details.</span></span>

    ![información de consultas](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a><span data-ttu-id="7596b-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7596b-150">Next steps</span></span> 
<span data-ttu-id="7596b-151">Entre los motivos comunes para un rendimiento deficiente de la base de datos se encuentran índices que faltan y consultas mal optimizadas.</span><span class="sxs-lookup"><span data-stu-id="7596b-151">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="7596b-152">En este tutorial aprendió lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7596b-152">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="7596b-153">Revisar, aplicar y revertir las recomendaciones para la mejora de rendimiento</span><span class="sxs-lookup"><span data-stu-id="7596b-153">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="7596b-154">Buscar consultas con un uso intensivo de los recursos</span><span class="sxs-lookup"><span data-stu-id="7596b-154">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="7596b-155">Buscar consultas de ejecución prolongada</span><span class="sxs-lookup"><span data-stu-id="7596b-155">Find long running queries</span></span>

[<span data-ttu-id="7596b-156">Sugerencias para la optimización del rendimiento de Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="7596b-156">SQL Database performance tuning tips</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
