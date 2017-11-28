---
title: 'Supervisar y mejorar el rendimiento: Azure SQL Database | Microsoft Docs'
description: "Azure SQL Database ofrece herramientas de rendimiento para ayudarle a identificar áreas que pueden mejorar el rendimiento actual de las consultas."
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
ms.openlocfilehash: 522b932ab055978c52f085dbaa36095bb6b77962
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-improve-performance"></a><span data-ttu-id="586b2-103">Supervisión y mejora del rendimiento</span><span class="sxs-lookup"><span data-stu-id="586b2-103">Monitor and improve performance</span></span>
<span data-ttu-id="586b2-104">Azure SQL Database identifica posibles problemas en la base de datos y recomienda las acciones que pueden mejorar el rendimiento de la carga de trabajo mediante recomendaciones y acciones de optimización inteligentes.</span><span class="sxs-lookup"><span data-stu-id="586b2-104">Azure SQL Database identifies potential problems in your database and recommends actions that can improve performance of your workload by providing intelligent tuning actions and recommendations.</span></span>

<span data-ttu-id="586b2-105">Para revisar el rendimiento de la base de datos, use el icono **Rendimiento** de la página Información general o desplácese hacia abajo hasta la sección "Soporte técnico y solución de problemas":</span><span class="sxs-lookup"><span data-stu-id="586b2-105">To review your database performance, use the **Performance** tile on the Overview page, or navigate down to "Support + troubleshooting" section:</span></span>

   ![Vista Rendimiento](./media/sql-database-performance/entries.png)

<span data-ttu-id="586b2-107">En la sección "Soporte técnico y solución de problemas", puede usar las páginas siguientes:</span><span class="sxs-lookup"><span data-stu-id="586b2-107">In the "Support + troubleshooting" section, you can use the following pages:</span></span>


1. <span data-ttu-id="586b2-108">[Información general de rendimiento](#performance-overview) para supervisar el rendimiento de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="586b2-108">[Performance overview](#performance-overview) to monitor performance of your database.</span></span> 
2. <span data-ttu-id="586b2-109">[Recomendaciones de rendimiento](#performance-recommendations) para buscar las recomendaciones de rendimiento que pueden mejorar el rendimiento de la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="586b2-109">[Performance recommendations](#performance-recommendations) to find performance recommendations that can improve performance of your workload.</span></span>
3. <span data-ttu-id="586b2-110">[Información de rendimiento de consultas](#query-performance-insight) para buscar las consultas que consumen más recursos.</span><span class="sxs-lookup"><span data-stu-id="586b2-110">[Query Performance Insight](#query-performance-insight) to find top resource consuming queries.</span></span>
4. <span data-ttu-id="586b2-111">[Ajuste automático](#automatic-tuning) para permitir que Azure SQL Database optimice automáticamente la base de datos.</span><span class="sxs-lookup"><span data-stu-id="586b2-111">[Automatic tuning](#automatic-tuning) to let Azure SQL Database automatically optimize your database.</span></span>

## <a name="performance-overview"></a><span data-ttu-id="586b2-112">Información general de rendimiento</span><span class="sxs-lookup"><span data-stu-id="586b2-112">Performance Overview</span></span>
<span data-ttu-id="586b2-113">Esta vista ofrece un resumen del rendimiento de la base de datos y le ayuda con la optimización y solución de problemas de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="586b2-113">This view provides a summary of your database performance, and helps you with performance tuning and troubleshooting.</span></span> 

![Rendimiento](./media/sql-database-performance/performance.png)

* <span data-ttu-id="586b2-115">El icono de **Recomendaciones** proporciona un desglose de recomendaciones de ajuste para la base de datos (se muestran las tres primeras recomendaciones si hay más).</span><span class="sxs-lookup"><span data-stu-id="586b2-115">The **Recommendations** tile provides a breakdown of tuning recommendations for your database (top three recommendations are shown if there are more).</span></span> <span data-ttu-id="586b2-116">Haga clic en este icono para acceder a **[Recomendaciones de rendimiento](#performance-recommendations)**.</span><span class="sxs-lookup"><span data-stu-id="586b2-116">Clicking this tile takes you to **[Performance recommendations](#performance-recommendations)**.</span></span> 
* <span data-ttu-id="586b2-117">El icono de **Tuning activity** (Actividad de optimización) proporciona un resumen de las acciones de optimización en curso y finalizadas para la base de datos, lo que le brinda una vista rápida del historial de la actividad de optimización.</span><span class="sxs-lookup"><span data-stu-id="586b2-117">The **Tuning activity** tile provides a summary of the ongoing and completed tuning actions for your database, giving you a quick view into the history of tuning activity.</span></span> <span data-ttu-id="586b2-118">Si hace clic en este icono irá a la vista completa del historial de optimización de la basa de datos.</span><span class="sxs-lookup"><span data-stu-id="586b2-118">Clicking this tile takes you to the full tuning history view for your database.</span></span>
* <span data-ttu-id="586b2-119">El icono **Ajuste automático** muestra la [configuración de ajuste automático](sql-database-automatic-tuning-enable.md) de la base de datos (las opciones de ajuste que se aplican automáticamente a la base de datos).</span><span class="sxs-lookup"><span data-stu-id="586b2-119">The **Auto-tuning** tile shows the [auto-tuning configuration](sql-database-automatic-tuning-enable.md) for your database (tuning options that are automatically applied to your database).</span></span> <span data-ttu-id="586b2-120">Al hacer clic en este icono se abre el cuadro de diálogo de configuración de automatización.</span><span class="sxs-lookup"><span data-stu-id="586b2-120">Clicking this tile opens the automation configuration dialog.</span></span>
* <span data-ttu-id="586b2-121">El icono de **Consultas de bases de datos** muestra el resumen del rendimiento de consultas de la base de datos (uso general de DTU y consultas que consumen más recursos).</span><span class="sxs-lookup"><span data-stu-id="586b2-121">The **Database queries** tile shows the summary of the query performance for your database (overall DTU usage and top resource consuming queries).</span></span> <span data-ttu-id="586b2-122">Haga clic en este icono para acceder a **[Información de rendimiento de consultas](#query-performance-insight)**.</span><span class="sxs-lookup"><span data-stu-id="586b2-122">Clicking this tile takes you to **[Query Performance Insight](#query-performance-insight)**.</span></span>

## <a name="performance-recommendations"></a><span data-ttu-id="586b2-123">Recomendaciones de rendimiento</span><span class="sxs-lookup"><span data-stu-id="586b2-123">Performance recommendations</span></span>
<span data-ttu-id="586b2-124">En esta página se proporcionan [recomendaciones de ajuste](sql-database-advisor.md) inteligentes que pueden mejorar el rendimiento de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="586b2-124">This page provides intelligent [tuning recommendations](sql-database-advisor.md) that can improve your database's performance.</span></span> <span data-ttu-id="586b2-125">Los siguientes tipos de recomendaciones se muestran en esta página:</span><span class="sxs-lookup"><span data-stu-id="586b2-125">The following types of recommendations are shown on this page:</span></span>

* <span data-ttu-id="586b2-126">Recomendaciones sobre qué índices se deben crear o quitar.</span><span class="sxs-lookup"><span data-stu-id="586b2-126">Recommendations on which indexes to create or drop.</span></span>
* <span data-ttu-id="586b2-127">Recomendaciones cuando se identifican problemas del esquema en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="586b2-127">Recommendations when schema issues are identified in the database.</span></span>
* <span data-ttu-id="586b2-128">Recomendaciones en caso de consultas que puedan beneficiarse de consultas parametrizadas.</span><span class="sxs-lookup"><span data-stu-id="586b2-128">Recommendations when queries can benefit from parameterized queries.</span></span>

![Rendimiento](./media/sql-database-performance/recommendations.png)

<span data-ttu-id="586b2-130">También puede encontrar el historial completo de las acciones de ajuste que se aplicaron en el pasado.</span><span class="sxs-lookup"><span data-stu-id="586b2-130">You can also find complete history of tuning actions that were applied in the past.</span></span>

<span data-ttu-id="586b2-131">Obtenga información sobre cómo buscar y aplicar recomendaciones de rendimiento en el artículo [Búsqueda y aplicación de recomendaciones de rendimiento](sql-database-advisor-portal.md).</span><span class="sxs-lookup"><span data-stu-id="586b2-131">Learn how to find an apply performance recommendations in [Find and apply performance recommendations](sql-database-advisor-portal.md) article.</span></span>

## <a name="automatic-tuning"></a><span data-ttu-id="586b2-132">Ajuste automático</span><span class="sxs-lookup"><span data-stu-id="586b2-132">Automatic tuning</span></span>
<span data-ttu-id="586b2-133">Las bases de datos de Azure SQL Database puede optimizar automáticamente el rendimiento de base de datos mediante la aplicación de [recomendaciones de rendimiento](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="586b2-133">Azure SQL Databases can automatically tune database performance by applying [performance recommendations](sql-database-advisor.md).</span></span> <span data-ttu-id="586b2-134">Para obtener más información, lea el [artículo Ajuste automático](sql-database-automatic-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="586b2-134">To learn more, read [Automatic tuning article](sql-database-automatic-tuning.md).</span></span> <span data-ttu-id="586b2-135">Para habilitarlo, lea [cómo habilitar el ajuste automático](sql-database-automatic-tuning-enable.md).</span><span class="sxs-lookup"><span data-stu-id="586b2-135">To enable it, read [how to enable automatic tuning](sql-database-automatic-tuning-enable.md).</span></span>

## <a name="query-performance-insight"></a><span data-ttu-id="586b2-136">Información de rendimiento de consultas</span><span class="sxs-lookup"><span data-stu-id="586b2-136">Query Performance Insight</span></span>
<span data-ttu-id="586b2-137">[Información de rendimiento de consultas](sql-database-query-performance.md) permite dedicar menos tiempo a la solución de problemas de rendimiento de bases de datos, ya que proporciona:</span><span class="sxs-lookup"><span data-stu-id="586b2-137">[Query Performance Insight](sql-database-query-performance.md) allows you to spend less time troubleshooting database performance by providing:</span></span>

* <span data-ttu-id="586b2-138">Información más detallada sobre el consumo de recursos (DTU) de las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="586b2-138">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="586b2-139">Las consultas que más CPU consumen, que potencialmente pueden ajustarse para mejorar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="586b2-139">The top CPU consuming queries, which can potentially be tuned for improved performance.</span></span> 
* <span data-ttu-id="586b2-140">La posibilidad de profundizar en los detalles de una consulta.</span><span class="sxs-lookup"><span data-stu-id="586b2-140">The ability to drill down into the details of a query.</span></span> 

  ![panel de rendimiento](./media/sql-database-query-performance/performance.png)

<span data-ttu-id="586b2-142">Obtenga más información sobre esta página en el artículo **[Cómo usar información de rendimiento de consultas](sql-database-query-performance.md)**.</span><span class="sxs-lookup"><span data-stu-id="586b2-142">Find more information about this page in the article **[How to use Query Performance Insight](sql-database-query-performance.md)**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="586b2-143">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="586b2-143">Additional resources</span></span>
* [<span data-ttu-id="586b2-144">Guía de rendimiento de Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="586b2-144">Azure SQL Database performance guidance for single databases</span></span>](sql-database-performance-guidance.md)
* [<span data-ttu-id="586b2-145">¿Cuándo se debe utilizar un grupo elástico?</span><span class="sxs-lookup"><span data-stu-id="586b2-145">When should an elastic pool be used?</span></span>](sql-database-elastic-pool-guidance.md)

