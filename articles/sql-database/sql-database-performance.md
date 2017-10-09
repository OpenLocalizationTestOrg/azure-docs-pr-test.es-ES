---
title: aaaMonitor y mejorar el rendimiento - base de datos de SQL de Azure | Documentos de Microsoft
description: "Hola que la base de datos SQL Azure proporciona un rendimiento de las herramientas toohelp identificar áreas que pueden mejorar el rendimiento de la consulta actual."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: a60b75ac-cf27-4d73-8322-ee4d4c448aa2
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2016
ms.author: sstein
ms.openlocfilehash: 84b8a1bc62698a29deb49e765f208bd7e14d0870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-improve-performance"></a><span data-ttu-id="f47ea-103">Supervisión y mejora del rendimiento</span><span class="sxs-lookup"><span data-stu-id="f47ea-103">Monitor and improve performance</span></span>
<span data-ttu-id="f47ea-104">Azure SQL Database identifica posibles problemas en la base de datos y recomienda las acciones que pueden mejorar el rendimiento de la carga de trabajo mediante recomendaciones y acciones de optimización inteligentes.</span><span class="sxs-lookup"><span data-stu-id="f47ea-104">Azure SQL Database identifies potential problems in your database and recommends actions that can improve performance of your workload by providing intelligent tuning actions and recommendations.</span></span>

<span data-ttu-id="f47ea-105">tooreview el rendimiento de la base de datos, use hello **rendimiento** de mosaico en la página de información general de Hola o navegar hacia abajo demasiado "Compatibilidad con + solución de problemas" sección:</span><span class="sxs-lookup"><span data-stu-id="f47ea-105">tooreview your database performance, use hello **Performance** tile on hello Overview page, or navigate down too"Support + troubleshooting" section:</span></span>

   ![Vista Rendimiento](./media/sql-database-performance/entries.png)

<span data-ttu-id="f47ea-107">En la sección "Compatibilidad con + solución de problemas" de Hola, puede usar Hola siguientes páginas:</span><span class="sxs-lookup"><span data-stu-id="f47ea-107">In hello "Support + troubleshooting" section, you can use hello following pages:</span></span>


1. <span data-ttu-id="f47ea-108">[Información general sobre rendimiento](#performance-overview) toomonitor rendimiento de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f47ea-108">[Performance overview](#performance-overview) toomonitor performance of your database.</span></span> 
2. <span data-ttu-id="f47ea-109">[Recomendaciones de rendimiento](#performance-recommendations) toofind recomendaciones de rendimiento que pueden mejorar el rendimiento de la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f47ea-109">[Performance recommendations](#performance-recommendations) toofind performance recommendations that can improve performance of your workload.</span></span>
3. <span data-ttu-id="f47ea-110">[Consultar información de rendimiento de](#query-performance-insight) toofind las consultas que consumen más de los recursos.</span><span class="sxs-lookup"><span data-stu-id="f47ea-110">[Query Performance Insight](#query-performance-insight) toofind top resource consuming queries.</span></span>
4. <span data-ttu-id="f47ea-111">[El ajuste automático](#automatic-tuning) toolet base de datos de SQL Azure optimice automáticamente la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f47ea-111">[Automatic tuning](#automatic-tuning) toolet Azure SQL Database automatically optimize your database.</span></span>

## <a name="performance-overview"></a><span data-ttu-id="f47ea-112">Información general de rendimiento</span><span class="sxs-lookup"><span data-stu-id="f47ea-112">Performance Overview</span></span>
<span data-ttu-id="f47ea-113">Esta vista ofrece un resumen del rendimiento de la base de datos y le ayuda con la optimización y solución de problemas de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="f47ea-113">This view provides a summary of your database performance, and helps you with performance tuning and troubleshooting.</span></span> 

![Rendimiento](./media/sql-database-performance/performance.png)

* <span data-ttu-id="f47ea-115">Hola **recomendaciones** mosaico proporciona un desglose de recomendaciones para la base de datos de optimización (tres primeras se muestran recomendaciones si hay más).</span><span class="sxs-lookup"><span data-stu-id="f47ea-115">hello **Recommendations** tile provides a breakdown of tuning recommendations for your database (top three recommendations are shown if there are more).</span></span> <span data-ttu-id="f47ea-116">Al hacer clic en este icono le lleva demasiado**[recomendaciones de rendimiento](#performance-recommendations)**.</span><span class="sxs-lookup"><span data-stu-id="f47ea-116">Clicking this tile takes you too**[Performance recommendations](#performance-recommendations)**.</span></span> 
* <span data-ttu-id="f47ea-117">Hola **para la optimización actividad** mosaico proporciona un resumen de hello en curso y completada las acciones para la base de datos para la optimización, lo que le ofrece una vista rápida de historial de Hola de actividad para la optimización.</span><span class="sxs-lookup"><span data-stu-id="f47ea-117">hello **Tuning activity** tile provides a summary of hello ongoing and completed tuning actions for your database, giving you a quick view into hello history of tuning activity.</span></span> <span data-ttu-id="f47ea-118">Al hacer clic en este icono, se le toohello completa para la optimización vista Historial para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f47ea-118">Clicking this tile takes you toohello full tuning history view for your database.</span></span>
* <span data-ttu-id="f47ea-119">Hola **ajuste automático** icono muestra hello [ajuste automático de la configuración](sql-database-automatic-tuning-enable.md) para la base de datos (optimización de opciones de base de datos de tooyour automáticamente aplicado).</span><span class="sxs-lookup"><span data-stu-id="f47ea-119">hello **Auto-tuning** tile shows hello [auto-tuning configuration](sql-database-automatic-tuning-enable.md) for your database (tuning options that are automatically applied tooyour database).</span></span> <span data-ttu-id="f47ea-120">Al hacer clic en este icono abre el cuadro de diálogo de configuración de automatización de Hola.</span><span class="sxs-lookup"><span data-stu-id="f47ea-120">Clicking this tile opens hello automation configuration dialog.</span></span>
* <span data-ttu-id="f47ea-121">Hola **consultas de base de datos** mosaico muestra Hola resumen del rendimiento de las consultas de hello para la base de datos (general DTU uso y los principales consultas que consumen recursos).</span><span class="sxs-lookup"><span data-stu-id="f47ea-121">hello **Database queries** tile shows hello summary of hello query performance for your database (overall DTU usage and top resource consuming queries).</span></span> <span data-ttu-id="f47ea-122">Al hacer clic en este icono le lleva demasiado**[Query Performance Insight](#query-performance-insight)**.</span><span class="sxs-lookup"><span data-stu-id="f47ea-122">Clicking this tile takes you too**[Query Performance Insight](#query-performance-insight)**.</span></span>

## <a name="performance-recommendations"></a><span data-ttu-id="f47ea-123">Recomendaciones de rendimiento</span><span class="sxs-lookup"><span data-stu-id="f47ea-123">Performance recommendations</span></span>
<span data-ttu-id="f47ea-124">En esta página se proporcionan [recomendaciones de ajuste](sql-database-advisor.md) inteligentes que pueden mejorar el rendimiento de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f47ea-124">This page provides intelligent [tuning recommendations](sql-database-advisor.md) that can improve your database's performance.</span></span> <span data-ttu-id="f47ea-125">Hola siguientes tipos de recomendaciones se muestra en esta página:</span><span class="sxs-lookup"><span data-stu-id="f47ea-125">hello following types of recommendations are shown on this page:</span></span>

* <span data-ttu-id="f47ea-126">Obtener recomendaciones sobre qué índices toocreate o drop.</span><span class="sxs-lookup"><span data-stu-id="f47ea-126">Recommendations on which indexes toocreate or drop.</span></span>
* <span data-ttu-id="f47ea-127">Recomendaciones cuando se identifiquen problemas del esquema de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f47ea-127">Recommendations when schema issues are identified in hello database.</span></span>
* <span data-ttu-id="f47ea-128">Recomendaciones en caso de consultas que puedan beneficiarse de consultas parametrizadas.</span><span class="sxs-lookup"><span data-stu-id="f47ea-128">Recommendations when queries can benefit from parameterized queries.</span></span>

![Rendimiento](./media/sql-database-performance/recommendations.png)

<span data-ttu-id="f47ea-130">También puede encontrar el historial completo de las acciones que se aplicaron en hello pasado para la optimización.</span><span class="sxs-lookup"><span data-stu-id="f47ea-130">You can also find complete history of tuning actions that were applied in hello past.</span></span>

<span data-ttu-id="f47ea-131">Obtenga información acerca de cómo toofind apply recomendaciones de rendimiento en [buscar y aplicar las recomendaciones de rendimiento](sql-database-advisor-portal.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="f47ea-131">Learn how toofind an apply performance recommendations in [Find and apply performance recommendations](sql-database-advisor-portal.md) article.</span></span>

## <a name="automatic-tuning"></a><span data-ttu-id="f47ea-132">Ajuste automático</span><span class="sxs-lookup"><span data-stu-id="f47ea-132">Automatic tuning</span></span>
<span data-ttu-id="f47ea-133">Las bases de datos de Azure SQL Database puede optimizar automáticamente el rendimiento de base de datos mediante la aplicación de [recomendaciones de rendimiento](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="f47ea-133">Azure SQL Databases can automatically tune database performance by applying [performance recommendations](sql-database-advisor.md).</span></span> <span data-ttu-id="f47ea-134">más información, lea toolearn [artículo optimización automática](sql-database-automatic-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="f47ea-134">toolearn more, read [Automatic tuning article](sql-database-automatic-tuning.md).</span></span> <span data-ttu-id="f47ea-135">tooenable, leer [cómo el ajuste automático de tooenable](sql-database-automatic-tuning-enable.md).</span><span class="sxs-lookup"><span data-stu-id="f47ea-135">tooenable it, read [how tooenable automatic tuning](sql-database-automatic-tuning-enable.md).</span></span>

## <a name="query-performance-insight"></a><span data-ttu-id="f47ea-136">Información de rendimiento de consultas</span><span class="sxs-lookup"><span data-stu-id="f47ea-136">Query Performance Insight</span></span>
<span data-ttu-id="f47ea-137">[Consultar información de rendimiento de](sql-database-query-performance.md) permite toospend menos tiempo a la solución de problemas de rendimiento de la base de datos al proporcionar:</span><span class="sxs-lookup"><span data-stu-id="f47ea-137">[Query Performance Insight](sql-database-query-performance.md) allows you toospend less time troubleshooting database performance by providing:</span></span>

* <span data-ttu-id="f47ea-138">Información más detallada sobre el consumo de recursos (DTU) de las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="f47ea-138">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="f47ea-139">Hola que consuman más CPU consultas, que pueden optimizarse para mejorar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="f47ea-139">hello top CPU consuming queries, which can potentially be tuned for improved performance.</span></span> 
* <span data-ttu-id="f47ea-140">Hola capacidad toodrill hacia abajo en los detalles de Hola de una consulta.</span><span class="sxs-lookup"><span data-stu-id="f47ea-140">hello ability toodrill down into hello details of a query.</span></span> 

  ![panel de rendimiento](./media/sql-database-query-performance/performance.png)

<span data-ttu-id="f47ea-142">Obtener más información acerca de esta página en el artículo de hello  **[cómo toouse Query Performance Insight](sql-database-query-performance.md)**.</span><span class="sxs-lookup"><span data-stu-id="f47ea-142">Find more information about this page in hello article **[How toouse Query Performance Insight](sql-database-query-performance.md)**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f47ea-143">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="f47ea-143">Additional resources</span></span>
* [<span data-ttu-id="f47ea-144">Guía de rendimiento de Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="f47ea-144">Azure SQL Database performance guidance for single databases</span></span>](sql-database-performance-guidance.md)
* [<span data-ttu-id="f47ea-145">¿Cuándo se debe utilizar un grupo elástico?</span><span class="sxs-lookup"><span data-stu-id="f47ea-145">When should an elastic pool be used?</span></span>](sql-database-elastic-pool-guidance.md)

