---
title: "Simultaneidad y administración de cargas de trabajo en SQL Data Warehouse | Microsoft Docs"
description: "Obtenga información sobre la simultaneidad y la administración de cargas de trabajo en Almacenamiento de datos SQL de Azure para el desarrollo de soluciones."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 08/23/2017
ms.author: joeyong;barbkess;kavithaj
ms.openlocfilehash: eaf2d43286dbaa52ada1430fbb7ce1e37f41c0d4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a><span data-ttu-id="cd3a9-103">Simultaneidad y administración de cargas de trabajo en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="cd3a9-103">Concurrency and workload management in SQL Data Warehouse</span></span>
<span data-ttu-id="cd3a9-104">Para proporcionar un rendimiento predecible a escala, Almacenamiento de datos SQL de Microsoft Azure le permite controlar los niveles de simultaneidad y las asignaciones de recursos, como la asignación de prioridades de CPU y memoria.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-104">To deliver predictable performance at scale, Microsoft Azure SQL Data Warehouse helps you control concurrency levels and resource allocations like memory and CPU prioritization.</span></span> <span data-ttu-id="cd3a9-105">En este artículo se presentan los conceptos de simultaneidad y administración de cargas de trabajo, y se explica cómo se han implementado ambas características y cómo puede controlarlas en su almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-105">This article introduces you to the concepts of concurrency and workload management, explaining how both features have been implemented and how you can control them in your data warehouse.</span></span> <span data-ttu-id="cd3a9-106">La administración de cargas de trabajo de Almacenamiento de datos SQL está diseñada para admitir entornos de varios usuarios.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-106">SQL Data Warehouse workload management is intended to help you support multi-user environments.</span></span> <span data-ttu-id="cd3a9-107">No está diseñada para cargas de trabajo de multiinquilino.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-107">It is not intended for multi-tenant workloads.</span></span>

## <a name="concurrency-limits"></a><span data-ttu-id="cd3a9-108">Límites de simultaneidad</span><span class="sxs-lookup"><span data-stu-id="cd3a9-108">Concurrency limits</span></span>
<span data-ttu-id="cd3a9-109">Almacenamiento de datos SQL permite hasta 1.024 conexiones simultáneas.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-109">SQL Data Warehouse allows up to 1,024 concurrent connections.</span></span> <span data-ttu-id="cd3a9-110">Todas las 1.024 conexiones pueden enviar consultas al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-110">All 1,024 connections can submit queries concurrently.</span></span> <span data-ttu-id="cd3a9-111">Sin embargo, para optimizar el rendimiento, Almacenamiento de datos SQL puede poner en cola algunas consultas para asegurarse de que cada una de ellas tiene garantizado un mínimo de memoria.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-111">However, to optimize throughput, SQL Data Warehouse may queue some queries to ensure that each query receives a minimal memory grant.</span></span> <span data-ttu-id="cd3a9-112">Durante el tiempo de ejecución de las consultas, estas se empiezan a poner en cola.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-112">Queuing occurs at query execution time.</span></span> <span data-ttu-id="cd3a9-113">Al iniciar una cola con las consultas cuando se alcanzan los límites de simultaneidad, Almacenamiento de datos SQL puede aumentar el rendimiento total, asegurándose de que las consultas activas obtienen el acceso a los recursos de la memoria que tanto necesitan.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-113">By queuing queries when concurrency limits are reached, SQL Data Warehouse can increase total throughput by ensuring that active queries get access to critically needed memory resources.</span></span>  

<span data-ttu-id="cd3a9-114">Los límites de simultaneidad se rigen por dos conceptos: *consultas simultáneas* y *espacios de simultaneidad*.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-114">Concurrency limits are governed by two concepts: *concurrent queries* and *concurrency slots*.</span></span> <span data-ttu-id="cd3a9-115">Para que una consulta se ejecute, lo ha de hacer tanto dentro de su límite de simultaneidad como dentro de la asignación de espacio de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-115">For a query to execute, it must execute within both the query concurrency limit and the concurrency slot allocation.</span></span>

* <span data-ttu-id="cd3a9-116">Las consultas simultáneas son consultas que se ejecutan al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-116">Concurrent queries are the queries executing at the same time.</span></span> <span data-ttu-id="cd3a9-117">Almacenamiento de datos SQL admite hasta 32 consultas simultáneas en los tamaños de DWU más grandes.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-117">SQL Data Warehouse supports up to 32 concurrent queries on the larger DWU sizes.</span></span>
* <span data-ttu-id="cd3a9-118">Los espacios de simultaneidad se asignan según DWU.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-118">Concurrency slots are allocated based on DWU.</span></span> <span data-ttu-id="cd3a9-119">Cada 100 DWU proporciona 4 espacios de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-119">Each 100 DWU provides 4 concurrency slots.</span></span> <span data-ttu-id="cd3a9-120">Por ejemplo, un DW100 asigna 4 espacios de simultaneidad y DW1000 asigna 40.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-120">For example, a DW100 allocates 4 concurrency slots and DW1000 allocates 40.</span></span> <span data-ttu-id="cd3a9-121">Cada consulta consume uno o más espacios de simultaneidad, en función de la [clase de recursos](#resource-classes) de la consulta.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-121">Each query consumes one or more concurrency slots, dependent on the [resource class](#resource-classes) of the query.</span></span> <span data-ttu-id="cd3a9-122">Las consultas que se ejecutan en la clase de recurso smallrc consumen una ranura de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-122">Queries running in the smallrc resource class consume one concurrency slot.</span></span> <span data-ttu-id="cd3a9-123">Las consultas que se ejecutan en una clase de recurso superior consumen más intervalos de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-123">Queries running in a higher resource class consume more concurrency slots.</span></span>

<span data-ttu-id="cd3a9-124">La tabla siguiente describe los límites de consultas simultáneas y espacios de simultaneidad en los distintos tamaños de DWU.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-124">The following table describes the limits for both concurrent queries and concurrency slots at the various DWU sizes.</span></span>

### <a name="concurrency-limits"></a><span data-ttu-id="cd3a9-125">Límites de simultaneidad</span><span class="sxs-lookup"><span data-stu-id="cd3a9-125">Concurrency limits</span></span>
| <span data-ttu-id="cd3a9-126">DWU</span><span class="sxs-lookup"><span data-stu-id="cd3a9-126">DWU</span></span> | <span data-ttu-id="cd3a9-127">N.º máximo de consultas simultáneas</span><span class="sxs-lookup"><span data-stu-id="cd3a9-127">Max concurrent queries</span></span> | <span data-ttu-id="cd3a9-128">Espacios de simultaneidad asignados</span><span class="sxs-lookup"><span data-stu-id="cd3a9-128">Concurrency slots allocated</span></span> |
|:--- |:---:|:---:|
| <span data-ttu-id="cd3a9-129">DW100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-129">DW100</span></span> |<span data-ttu-id="cd3a9-130">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-130">4</span></span> |<span data-ttu-id="cd3a9-131">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-131">4</span></span> |
| <span data-ttu-id="cd3a9-132">DW200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-132">DW200</span></span> |<span data-ttu-id="cd3a9-133">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-133">8</span></span> |<span data-ttu-id="cd3a9-134">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-134">8</span></span> |
| <span data-ttu-id="cd3a9-135">DW300</span><span class="sxs-lookup"><span data-stu-id="cd3a9-135">DW300</span></span> |<span data-ttu-id="cd3a9-136">12</span><span class="sxs-lookup"><span data-stu-id="cd3a9-136">12</span></span> |<span data-ttu-id="cd3a9-137">12</span><span class="sxs-lookup"><span data-stu-id="cd3a9-137">12</span></span> |
| <span data-ttu-id="cd3a9-138">DW400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-138">DW400</span></span> |<span data-ttu-id="cd3a9-139">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-139">16</span></span> |<span data-ttu-id="cd3a9-140">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-140">16</span></span> |
| <span data-ttu-id="cd3a9-141">DW500</span><span class="sxs-lookup"><span data-stu-id="cd3a9-141">DW500</span></span> |<span data-ttu-id="cd3a9-142">20 |</span><span class="sxs-lookup"><span data-stu-id="cd3a9-142">20</span></span> |<span data-ttu-id="cd3a9-143">20 |</span><span class="sxs-lookup"><span data-stu-id="cd3a9-143">20</span></span> |
| <span data-ttu-id="cd3a9-144">DW600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-144">DW600</span></span> |<span data-ttu-id="cd3a9-145">24</span><span class="sxs-lookup"><span data-stu-id="cd3a9-145">24</span></span> |<span data-ttu-id="cd3a9-146">24</span><span class="sxs-lookup"><span data-stu-id="cd3a9-146">24</span></span> |
| <span data-ttu-id="cd3a9-147">DW1000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-147">DW1000</span></span> |<span data-ttu-id="cd3a9-148">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-148">32</span></span> |<span data-ttu-id="cd3a9-149">40</span><span class="sxs-lookup"><span data-stu-id="cd3a9-149">40</span></span> |
| <span data-ttu-id="cd3a9-150">DW1200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-150">DW1200</span></span> |<span data-ttu-id="cd3a9-151">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-151">32</span></span> |<span data-ttu-id="cd3a9-152">48</span><span class="sxs-lookup"><span data-stu-id="cd3a9-152">48</span></span> |
| <span data-ttu-id="cd3a9-153">DW1500</span><span class="sxs-lookup"><span data-stu-id="cd3a9-153">DW1500</span></span> |<span data-ttu-id="cd3a9-154">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-154">32</span></span> |<span data-ttu-id="cd3a9-155">60</span><span class="sxs-lookup"><span data-stu-id="cd3a9-155">60</span></span> |
| <span data-ttu-id="cd3a9-156">DW2000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-156">DW2000</span></span> |<span data-ttu-id="cd3a9-157">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-157">32</span></span> |<span data-ttu-id="cd3a9-158">80</span><span class="sxs-lookup"><span data-stu-id="cd3a9-158">80</span></span> |
| <span data-ttu-id="cd3a9-159">DW3000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-159">DW3000</span></span> |<span data-ttu-id="cd3a9-160">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-160">32</span></span> |<span data-ttu-id="cd3a9-161">120</span><span class="sxs-lookup"><span data-stu-id="cd3a9-161">120</span></span> |
| <span data-ttu-id="cd3a9-162">DW6000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-162">DW6000</span></span> |<span data-ttu-id="cd3a9-163">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-163">32</span></span> |<span data-ttu-id="cd3a9-164">240</span><span class="sxs-lookup"><span data-stu-id="cd3a9-164">240</span></span> |

<span data-ttu-id="cd3a9-165">Cuando se alcanza alguno de estos umbrales, se ponen a la cola nuevas consultas y se ejecutan según la regla "primero en entrar, primero en salir".</span><span class="sxs-lookup"><span data-stu-id="cd3a9-165">When one of these thresholds is met, new queries are queued and executed on a first-in, first-out basis.</span></span>  <span data-ttu-id="cd3a9-166">A medida que las consultas finalizan y el número de consultas y ranuras desciende por debajo de los límites, las consultas en cola se liberan.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-166">As a queries finishes and the number of queries and slots falls below the limits, queued queries are released.</span></span> 

> [!NOTE]  
> <span data-ttu-id="cd3a9-167">*Select* que se ejecutan exclusivamente en vistas de administración dinámica (DMV) o vistas de catálogo no están reguladas por ninguno de los límites de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-167">*Select* queries executing exclusively on dynamic management views (DMVs) or catalog views are not governed by any of the concurrency limits.</span></span> <span data-ttu-id="cd3a9-168">Puede supervisar el sistema independientemente del número de consultas que se ejecutan en él.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-168">You can monitor the system regardless of the number of queries executing on it.</span></span>
> 
> 

## <a name="resource-classes"></a><span data-ttu-id="cd3a9-169">Clases de recursos</span><span class="sxs-lookup"><span data-stu-id="cd3a9-169">Resource classes</span></span>
<span data-ttu-id="cd3a9-170">Las clases de recursos le permiten controlar la asignación de memoria y los ciclos de CPI que se asignan a una consulta.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-170">Resource classes help you control memory allocation and CPU cycles given to a query.</span></span> <span data-ttu-id="cd3a9-171">Puede asignar dos tipos de recursos a un usuario en forma de roles de base de datos.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-171">You can assign two types of resource classes to a user in the form of database roles.</span></span> <span data-ttu-id="cd3a9-172">Los dos tipos de clases de recursos son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="cd3a9-172">The two types of resource classes are as follows:</span></span>
1. <span data-ttu-id="cd3a9-173">Clases de recursos dinámicos (**smallrc, mediumrc, largerc, xlargerc**) asignan una cantidad variable de memoria en función de la unidad de almacenamiento de datos actual.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-173">Dynamic Resource Classes (**smallrc, mediumrc, largerc, xlargerc**) allocate a variable amount of memory depending on the current DWU.</span></span> <span data-ttu-id="cd3a9-174">Esto significa que, al escalar a una unidad mayor, las consultas obtienen más memoria automáticamente.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-174">This means that when you scale up to a larger DWU, your queries automatically get more memory.</span></span> 
2. <span data-ttu-id="cd3a9-175">Las clases de recursos estáticos (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) asignan la misma cantidad de memoria, independientemente de la unidad de almacenamiento de datos actual (siempre que la propia unidad tenga memoria suficiente).</span><span class="sxs-lookup"><span data-stu-id="cd3a9-175">Static Resource Classes (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) allocate the same amount of memory regardless of the current DWU (provided that the DWU itself has enough memory).</span></span> <span data-ttu-id="cd3a9-176">Esto significa que, con unidades mayores, puede ejecutar más consultas en cada clase de recursos al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-176">This means that on larger DWUs, you can run more queries in each resource class concurrently.</span></span>

<span data-ttu-id="cd3a9-177">A los usuarios con **smallrc** y **staticrc10** se les concede una cantidad de memoria menor y pueden aprovechar una mayor simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-177">Users in **smallrc** and **staticrc10** are given a smaller amount of memory and can take advantage of higher concurrency.</span></span> <span data-ttu-id="cd3a9-178">Por el contrario, los usuarios asignados a **xlargerc** o **staticrc80** reciben grandes cantidades de memoria y, por tanto, son menos las consultas que pueden ejecutar de manera simultánea.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-178">In contrast, users assigned to **xlargerc** or **staticrc80** are given large amounts of memory, and therefore fewer of their queries can run concurrently.</span></span>

<span data-ttu-id="cd3a9-179">De forma predeterminada, cada usuario es miembro de la clase de recursos pequeña: **smallrc**.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-179">By default, each user is a member of the small resource class, **smallrc**.</span></span> <span data-ttu-id="cd3a9-180">El procedimiento `sp_addrolemember` se usa para aumentar la clase de recursos, mientras que `sp_droprolemember` se usa para disminuirla.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-180">The procedure `sp_addrolemember` is used to increase the resource class, and `sp_droprolemember` is used to decrease the resource class.</span></span> <span data-ttu-id="cd3a9-181">Por ejemplo, este comando aumentaría la clase de recursos de loaduser a **largerc**:</span><span class="sxs-lookup"><span data-stu-id="cd3a9-181">For example, this command would increase the resource class of loaduser to **largerc**:</span></span>

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a><span data-ttu-id="cd3a9-182">Consultas que no respetan las clases de recursos</span><span class="sxs-lookup"><span data-stu-id="cd3a9-182">Queries that do not honor resource classes</span></span>

<span data-ttu-id="cd3a9-183">Existen algunos tipos de consultas que no se benefician de una mayor asignación de memoria.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-183">There are a few types of queries that do not benefit from a larger memory allocation.</span></span> <span data-ttu-id="cd3a9-184">El sistema omite su asignación de clase de recursos y siempre ejecuta estas consultas en la clase de recursos pequeña.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-184">The system ignores their resource class allocation and always run these queries in the small resource class instead.</span></span> <span data-ttu-id="cd3a9-185">Si estas consultas se ejecutan siempre en la clase de recursos small, se pueden ejecutar cuando los espacios de simultaneidad estén bajo presión y no consumirán más espacios que los necesarios.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-185">If these queries always run in the small resource class, they can run when concurrency slots are under pressure and they won't consume more slots than needed.</span></span> <span data-ttu-id="cd3a9-186">Consulte [Excepciones de clase de recursos](#query-exceptions-to-concurrency-limits) para más información.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-186">See [Resource class exceptions](#query-exceptions-to-concurrency-limits) for more information.</span></span>

## <a name="details-on-resource-class-assignment"></a><span data-ttu-id="cd3a9-187">Detalles sobre la asignación de la clase de recursos</span><span class="sxs-lookup"><span data-stu-id="cd3a9-187">Details on resource class assignment</span></span>


<span data-ttu-id="cd3a9-188">Más detalles en la clase de recursos:</span><span class="sxs-lookup"><span data-stu-id="cd3a9-188">A few more details on resource class:</span></span>

* <span data-ttu-id="cd3a9-189">*Alter role* es necesario para cambiar la clase de recursos de un usuario.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-189">*Alter role* permission is required to change the resource class of a user.</span></span>
* <span data-ttu-id="cd3a9-190">Aunque puede agregar un usuario a una o varias de las clases de recursos más altas, los dinámicos tienen prioridad sobre los estáticos.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-190">Although you can add a user to one or more of the higher resource classes, dynamic resource classes take precedence over static resource classes.</span></span> <span data-ttu-id="cd3a9-191">Es decir, si un usuario está asignado tanto a **mediumrc**(dinámico) como a **staticrc80**(estático), **mediumrc** es la clase de recursos que se respeta.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-191">That is, if a user is assigned to both **mediumrc**(dynamic) and **staticrc80**(static), **mediumrc** is the resource class that is honored.</span></span>
 * <span data-ttu-id="cd3a9-192">Cuando a un usuario se le asigna más de una clase de recurso en un tipo de clase de recursos específico (más de uno dinámico o más de uno estático), se respeta la más alta.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-192">When a user is assigned to more than one resource class in a specific resource class type (more than one dynamic resource class or more than one static resource class), the highest resource class is honored.</span></span> <span data-ttu-id="cd3a9-193">Es decir, si a un usuario se le asigna mediumrc y largerc, se aplica la clase de recursos más alta, largerc.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-193">That is, if a user is assigned to both mediumrc and largerc, the higher resource class (largerc) is honored.</span></span> <span data-ttu-id="cd3a9-194">Y, si a un usuario se le asignan ambas, **staticrc20** y **statirc80**, se usa **staticrc80**.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-194">And if a user is assigned to both **staticrc20** and **statirc80**, **staticrc80** is honored.</span></span>
* <span data-ttu-id="cd3a9-195">No se puede cambiar la clase de recursos del usuario administrativo.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-195">The resource class of the system administrative user cannot be changed.</span></span>

<span data-ttu-id="cd3a9-196">Para un ejemplo detallado, consulte [Cambio de ejemplo de clase de recursos de usuario](#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="cd3a9-196">For a detailed example, see [Changing user resource class example](#changing-user-resource-class-example).</span></span>

## <a name="memory-allocation"></a><span data-ttu-id="cd3a9-197">Asignación de memoria</span><span class="sxs-lookup"><span data-stu-id="cd3a9-197">Memory allocation</span></span>
<span data-ttu-id="cd3a9-198">Aumentar clase de recursos de un usuario tiene ventajas y desventajas.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-198">There are pros and cons to increasing a user's resource class.</span></span> <span data-ttu-id="cd3a9-199">Al aumentar una clase de recursos para un usuario, a sus consultas se les concede acceso a más memoria, lo que puede implicar que las consultas se ejecuten más rápido.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-199">Increasing a resource class for a user, gives their queries access to more memory, which may mean queries execute faster.</span></span>  <span data-ttu-id="cd3a9-200">Sin embargo, las clases de recursos más altas también reducen el número de consultas simultáneas que se pueden ejecutar.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-200">However, higher resource classes also reduce the number of concurrent queries that can run.</span></span> <span data-ttu-id="cd3a9-201">Esto es consecuencia del principio de mantener el equilibrio entre asignar grandes cantidades de memoria a una sola consulta o permitir que otras consultas, que también necesitan asignaciones de memoria, se ejecuten al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-201">This is the trade-off between allocating large amounts of memory to a single query or allowing other queries, which also need memory allocations, to run concurrently.</span></span> <span data-ttu-id="cd3a9-202">Si un usuario recibe asignaciones altas de memoria para una consulta, otros usuarios no tendrán acceso a esa misma memoria a fin de ejecutar una consulta.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-202">If one user is given high allocations of memory for a query, other users will not have access to that same memory to run a query.</span></span>

<span data-ttu-id="cd3a9-203">La tabla siguiente presenta un esquema de la memoria asignada a cada distribución por DWU y clases de recursos.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-203">The following table maps the memory allocated to each distribution by DWU and resource class.</span></span>

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a><span data-ttu-id="cd3a9-204">Asignaciones de memoria por distribución para las clases de recursos dinámicos (MB)</span><span class="sxs-lookup"><span data-stu-id="cd3a9-204">Memory allocations per distribution for dynamic resource classes (MB)</span></span>
| <span data-ttu-id="cd3a9-205">DWU</span><span class="sxs-lookup"><span data-stu-id="cd3a9-205">DWU</span></span> | <span data-ttu-id="cd3a9-206">smallrc</span><span class="sxs-lookup"><span data-stu-id="cd3a9-206">smallrc</span></span> | <span data-ttu-id="cd3a9-207">mediumrc</span><span class="sxs-lookup"><span data-stu-id="cd3a9-207">mediumrc</span></span> | <span data-ttu-id="cd3a9-208">largerc</span><span class="sxs-lookup"><span data-stu-id="cd3a9-208">largerc</span></span> | <span data-ttu-id="cd3a9-209">xlargerc</span><span class="sxs-lookup"><span data-stu-id="cd3a9-209">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="cd3a9-210">DW100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-210">DW100</span></span> |<span data-ttu-id="cd3a9-211">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-211">100</span></span> |<span data-ttu-id="cd3a9-212">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-212">100</span></span> |<span data-ttu-id="cd3a9-213">200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-213">200</span></span> |<span data-ttu-id="cd3a9-214">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-214">400</span></span> |
| <span data-ttu-id="cd3a9-215">DW200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-215">DW200</span></span> |<span data-ttu-id="cd3a9-216">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-216">100</span></span> |<span data-ttu-id="cd3a9-217">200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-217">200</span></span> |<span data-ttu-id="cd3a9-218">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-218">400</span></span> |<span data-ttu-id="cd3a9-219">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-219">800</span></span> |
| <span data-ttu-id="cd3a9-220">DW300</span><span class="sxs-lookup"><span data-stu-id="cd3a9-220">DW300</span></span> |<span data-ttu-id="cd3a9-221">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-221">100</span></span> |<span data-ttu-id="cd3a9-222">200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-222">200</span></span> |<span data-ttu-id="cd3a9-223">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-223">400</span></span> |<span data-ttu-id="cd3a9-224">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-224">800</span></span> |
| <span data-ttu-id="cd3a9-225">DW400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-225">DW400</span></span> |<span data-ttu-id="cd3a9-226">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-226">100</span></span> |<span data-ttu-id="cd3a9-227">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-227">400</span></span> |<span data-ttu-id="cd3a9-228">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-228">800</span></span> |<span data-ttu-id="cd3a9-229">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-229">1,600</span></span> |
| <span data-ttu-id="cd3a9-230">DW500</span><span class="sxs-lookup"><span data-stu-id="cd3a9-230">DW500</span></span> |<span data-ttu-id="cd3a9-231">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-231">100</span></span> |<span data-ttu-id="cd3a9-232">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-232">400</span></span> |<span data-ttu-id="cd3a9-233">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-233">800</span></span> |<span data-ttu-id="cd3a9-234">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-234">1,600</span></span> |
| <span data-ttu-id="cd3a9-235">DW600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-235">DW600</span></span> |<span data-ttu-id="cd3a9-236">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-236">100</span></span> |<span data-ttu-id="cd3a9-237">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-237">400</span></span> |<span data-ttu-id="cd3a9-238">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-238">800</span></span> |<span data-ttu-id="cd3a9-239">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-239">1,600</span></span> |
| <span data-ttu-id="cd3a9-240">DW1000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-240">DW1000</span></span> |<span data-ttu-id="cd3a9-241">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-241">100</span></span> |<span data-ttu-id="cd3a9-242">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-242">800</span></span> |<span data-ttu-id="cd3a9-243">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-243">1,600</span></span> |<span data-ttu-id="cd3a9-244">3.200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-244">3,200</span></span> |
| <span data-ttu-id="cd3a9-245">DW1200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-245">DW1200</span></span> |<span data-ttu-id="cd3a9-246">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-246">100</span></span> |<span data-ttu-id="cd3a9-247">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-247">800</span></span> |<span data-ttu-id="cd3a9-248">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-248">1,600</span></span> |<span data-ttu-id="cd3a9-249">3.200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-249">3,200</span></span> |
| <span data-ttu-id="cd3a9-250">DW1500</span><span class="sxs-lookup"><span data-stu-id="cd3a9-250">DW1500</span></span> |<span data-ttu-id="cd3a9-251">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-251">100</span></span> |<span data-ttu-id="cd3a9-252">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-252">800</span></span> |<span data-ttu-id="cd3a9-253">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-253">1,600</span></span> |<span data-ttu-id="cd3a9-254">3.200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-254">3,200</span></span> |
| <span data-ttu-id="cd3a9-255">DW2000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-255">DW2000</span></span> |<span data-ttu-id="cd3a9-256">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-256">100</span></span> |<span data-ttu-id="cd3a9-257">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-257">1,600</span></span> |<span data-ttu-id="cd3a9-258">3.200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-258">3,200</span></span> |<span data-ttu-id="cd3a9-259">6.400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-259">6,400</span></span> |
| <span data-ttu-id="cd3a9-260">DW3000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-260">DW3000</span></span> |<span data-ttu-id="cd3a9-261">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-261">100</span></span> |<span data-ttu-id="cd3a9-262">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-262">1,600</span></span> |<span data-ttu-id="cd3a9-263">3.200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-263">3,200</span></span> |<span data-ttu-id="cd3a9-264">6.400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-264">6,400</span></span> |
| <span data-ttu-id="cd3a9-265">DW6000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-265">DW6000</span></span> |<span data-ttu-id="cd3a9-266">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-266">100</span></span> |<span data-ttu-id="cd3a9-267">3.200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-267">3,200</span></span> |<span data-ttu-id="cd3a9-268">6.400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-268">6,400</span></span> |<span data-ttu-id="cd3a9-269">12.800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-269">12,800</span></span> |

<span data-ttu-id="cd3a9-270">La tabla siguiente presenta un esquema de la memoria asignada a cada distribución por unidad de almacenamiento de datos y clase de recursos estáticos.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-270">The following table maps the memory allocated to each distribution by DWU and static resource class.</span></span> <span data-ttu-id="cd3a9-271">Tenga en cuenta que las clases de recursos más altas tienen una memoria reducida para respetar los límites de unidad globales.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-271">Note that the higher resource classes have their memory reduced to honor the global DWU limits.</span></span>

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a><span data-ttu-id="cd3a9-272">Asignaciones de memoria por distribución para las clases de recursos estáticos (MB)</span><span class="sxs-lookup"><span data-stu-id="cd3a9-272">Memory allocations per distribution for static resource classes (MB)</span></span>
| <span data-ttu-id="cd3a9-273">DWU</span><span class="sxs-lookup"><span data-stu-id="cd3a9-273">DWU</span></span> | <span data-ttu-id="cd3a9-274">staticrc10</span><span class="sxs-lookup"><span data-stu-id="cd3a9-274">staticrc10</span></span> | <span data-ttu-id="cd3a9-275">staticrc20</span><span class="sxs-lookup"><span data-stu-id="cd3a9-275">staticrc20</span></span> | <span data-ttu-id="cd3a9-276">staticrc30</span><span class="sxs-lookup"><span data-stu-id="cd3a9-276">staticrc30</span></span> | <span data-ttu-id="cd3a9-277">staticrc40</span><span class="sxs-lookup"><span data-stu-id="cd3a9-277">staticrc40</span></span> | <span data-ttu-id="cd3a9-278">staticrc50</span><span class="sxs-lookup"><span data-stu-id="cd3a9-278">staticrc50</span></span> | <span data-ttu-id="cd3a9-279">staticrc60</span><span class="sxs-lookup"><span data-stu-id="cd3a9-279">staticrc60</span></span> | <span data-ttu-id="cd3a9-280">staticrc70</span><span class="sxs-lookup"><span data-stu-id="cd3a9-280">staticrc70</span></span> | <span data-ttu-id="cd3a9-281">staticrc80</span><span class="sxs-lookup"><span data-stu-id="cd3a9-281">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="cd3a9-282">DW100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-282">DW100</span></span> |<span data-ttu-id="cd3a9-283">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-283">100</span></span> |<span data-ttu-id="cd3a9-284">200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-284">200</span></span> |<span data-ttu-id="cd3a9-285">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-285">400</span></span> |<span data-ttu-id="cd3a9-286">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-286">400</span></span> |<span data-ttu-id="cd3a9-287">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-287">400</span></span> |<span data-ttu-id="cd3a9-288">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-288">400</span></span> |<span data-ttu-id="cd3a9-289">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-289">400</span></span> |<span data-ttu-id="cd3a9-290">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-290">400</span></span> |
| <span data-ttu-id="cd3a9-291">DW200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-291">DW200</span></span> |<span data-ttu-id="cd3a9-292">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-292">100</span></span> |<span data-ttu-id="cd3a9-293">200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-293">200</span></span> |<span data-ttu-id="cd3a9-294">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-294">400</span></span> |<span data-ttu-id="cd3a9-295">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-295">800</span></span> |<span data-ttu-id="cd3a9-296">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-296">800</span></span> |<span data-ttu-id="cd3a9-297">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-297">800</span></span> |<span data-ttu-id="cd3a9-298">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-298">800</span></span> |<span data-ttu-id="cd3a9-299">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-299">800</span></span> |
| <span data-ttu-id="cd3a9-300">DW300</span><span class="sxs-lookup"><span data-stu-id="cd3a9-300">DW300</span></span> |<span data-ttu-id="cd3a9-301">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-301">100</span></span> |<span data-ttu-id="cd3a9-302">200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-302">200</span></span> |<span data-ttu-id="cd3a9-303">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-303">400</span></span> |<span data-ttu-id="cd3a9-304">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-304">800</span></span> |<span data-ttu-id="cd3a9-305">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-305">800</span></span> |<span data-ttu-id="cd3a9-306">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-306">800</span></span> |<span data-ttu-id="cd3a9-307">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-307">800</span></span> |<span data-ttu-id="cd3a9-308">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-308">800</span></span> |
| <span data-ttu-id="cd3a9-309">DW400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-309">DW400</span></span> |<span data-ttu-id="cd3a9-310">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-310">100</span></span> |<span data-ttu-id="cd3a9-311">200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-311">200</span></span> |<span data-ttu-id="cd3a9-312">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-312">400</span></span> |<span data-ttu-id="cd3a9-313">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-313">800</span></span> |<span data-ttu-id="cd3a9-314">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-314">1,600</span></span> |<span data-ttu-id="cd3a9-315">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-315">1,600</span></span> |<span data-ttu-id="cd3a9-316">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-316">1,600</span></span> |<span data-ttu-id="cd3a9-317">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-317">1,600</span></span> |
| <span data-ttu-id="cd3a9-318">DW500</span><span class="sxs-lookup"><span data-stu-id="cd3a9-318">DW500</span></span> |<span data-ttu-id="cd3a9-319">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-319">100</span></span> |<span data-ttu-id="cd3a9-320">200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-320">200</span></span> |<span data-ttu-id="cd3a9-321">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-321">400</span></span> |<span data-ttu-id="cd3a9-322">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-322">800</span></span> |<span data-ttu-id="cd3a9-323">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-323">1,600</span></span> |<span data-ttu-id="cd3a9-324">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-324">1,600</span></span> |<span data-ttu-id="cd3a9-325">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-325">1,600</span></span> |<span data-ttu-id="cd3a9-326">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-326">1,600</span></span> |
| <span data-ttu-id="cd3a9-327">DW600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-327">DW600</span></span> |<span data-ttu-id="cd3a9-328">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-328">100</span></span> |<span data-ttu-id="cd3a9-329">200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-329">200</span></span> |<span data-ttu-id="cd3a9-330">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-330">400</span></span> |<span data-ttu-id="cd3a9-331">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-331">800</span></span> |<span data-ttu-id="cd3a9-332">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-332">1,600</span></span> |<span data-ttu-id="cd3a9-333">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-333">1,600</span></span> |<span data-ttu-id="cd3a9-334">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-334">1,600</span></span> |<span data-ttu-id="cd3a9-335">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-335">1,600</span></span> |
| <span data-ttu-id="cd3a9-336">DW1000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-336">DW1000</span></span> |<span data-ttu-id="cd3a9-337">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-337">100</span></span> |<span data-ttu-id="cd3a9-338">200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-338">200</span></span> |<span data-ttu-id="cd3a9-339">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-339">400</span></span> |<span data-ttu-id="cd3a9-340">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-340">800</span></span> |<span data-ttu-id="cd3a9-341">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-341">1,600</span></span> |<span data-ttu-id="cd3a9-342">3.200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-342">3,200</span></span> |<span data-ttu-id="cd3a9-343">3.200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-343">3,200</span></span> |<span data-ttu-id="cd3a9-344">3.200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-344">3,200</span></span> |
| <span data-ttu-id="cd3a9-345">DW1200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-345">DW1200</span></span> |<span data-ttu-id="cd3a9-346">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-346">100</span></span> |<span data-ttu-id="cd3a9-347">200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-347">200</span></span> |<span data-ttu-id="cd3a9-348">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-348">400</span></span> |<span data-ttu-id="cd3a9-349">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-349">800</span></span> |<span data-ttu-id="cd3a9-350">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-350">1,600</span></span> |<span data-ttu-id="cd3a9-351">3.200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-351">3,200</span></span> |<span data-ttu-id="cd3a9-352">3.200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-352">3,200</span></span> |<span data-ttu-id="cd3a9-353">3.200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-353">3,200</span></span> |
| <span data-ttu-id="cd3a9-354">DW1500</span><span class="sxs-lookup"><span data-stu-id="cd3a9-354">DW1500</span></span> |<span data-ttu-id="cd3a9-355">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-355">100</span></span> |<span data-ttu-id="cd3a9-356">200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-356">200</span></span> |<span data-ttu-id="cd3a9-357">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-357">400</span></span> |<span data-ttu-id="cd3a9-358">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-358">800</span></span> |<span data-ttu-id="cd3a9-359">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-359">1,600</span></span> |<span data-ttu-id="cd3a9-360">3.200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-360">3,200</span></span> |<span data-ttu-id="cd3a9-361">3.200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-361">3,200</span></span> |<span data-ttu-id="cd3a9-362">3.200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-362">3,200</span></span> |
| <span data-ttu-id="cd3a9-363">DW2000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-363">DW2000</span></span> |<span data-ttu-id="cd3a9-364">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-364">100</span></span> |<span data-ttu-id="cd3a9-365">200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-365">200</span></span> |<span data-ttu-id="cd3a9-366">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-366">400</span></span> |<span data-ttu-id="cd3a9-367">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-367">800</span></span> |<span data-ttu-id="cd3a9-368">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-368">1,600</span></span> |<span data-ttu-id="cd3a9-369">3.200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-369">3,200</span></span> |<span data-ttu-id="cd3a9-370">6.400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-370">6,400</span></span> |<span data-ttu-id="cd3a9-371">6.400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-371">6,400</span></span> |
| <span data-ttu-id="cd3a9-372">DW3000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-372">DW3000</span></span> |<span data-ttu-id="cd3a9-373">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-373">100</span></span> |<span data-ttu-id="cd3a9-374">200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-374">200</span></span> |<span data-ttu-id="cd3a9-375">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-375">400</span></span> |<span data-ttu-id="cd3a9-376">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-376">800</span></span> |<span data-ttu-id="cd3a9-377">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-377">1,600</span></span> |<span data-ttu-id="cd3a9-378">3.200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-378">3,200</span></span> |<span data-ttu-id="cd3a9-379">6.400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-379">6,400</span></span> |<span data-ttu-id="cd3a9-380">6.400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-380">6,400</span></span> |
| <span data-ttu-id="cd3a9-381">DW6000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-381">DW6000</span></span> |<span data-ttu-id="cd3a9-382">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-382">100</span></span> |<span data-ttu-id="cd3a9-383">200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-383">200</span></span> |<span data-ttu-id="cd3a9-384">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-384">400</span></span> |<span data-ttu-id="cd3a9-385">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-385">800</span></span> |<span data-ttu-id="cd3a9-386">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-386">1,600</span></span> |<span data-ttu-id="cd3a9-387">3.200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-387">3,200</span></span> |<span data-ttu-id="cd3a9-388">6.400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-388">6,400</span></span> |<span data-ttu-id="cd3a9-389">12.800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-389">12,800</span></span> |

<span data-ttu-id="cd3a9-390">A partir de la tabla anterior, puede ver que una consulta que se ejecuta en DW2000 en la clase de recurso **xlargerc**, tendría acceso a 6 400 MB de memoria en cada una de las 60 bases de datos distribuidas.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-390">From the preceding table, you can see that a query running on a DW2000 in the **xlargerc** resource class would have access to 6,400 MB of memory within each of the 60 distributed databases.</span></span>  <span data-ttu-id="cd3a9-391">En Almacenamiento de datos SQL, existe 60 distribuciones.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-391">In SQL Data Warehouse, there are 60 distributions.</span></span> <span data-ttu-id="cd3a9-392">Por lo tanto, para calcular la asignación de memoria total para una consulta en una clase de recurso dada, los valores anteriores se deben multiplicar por 60.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-392">Therefore, to calculate the total memory allocation for a query in a given resource class, the above values should be multiplied by 60.</span></span>

### <a name="memory-allocations-system-wide-gb"></a><span data-ttu-id="cd3a9-393">Asignaciones de memoria en todo el sistema (GB)</span><span class="sxs-lookup"><span data-stu-id="cd3a9-393">Memory allocations system-wide (GB)</span></span>
| <span data-ttu-id="cd3a9-394">DWU</span><span class="sxs-lookup"><span data-stu-id="cd3a9-394">DWU</span></span> | <span data-ttu-id="cd3a9-395">smallrc</span><span class="sxs-lookup"><span data-stu-id="cd3a9-395">smallrc</span></span> | <span data-ttu-id="cd3a9-396">mediumrc</span><span class="sxs-lookup"><span data-stu-id="cd3a9-396">mediumrc</span></span> | <span data-ttu-id="cd3a9-397">largerc</span><span class="sxs-lookup"><span data-stu-id="cd3a9-397">largerc</span></span> | <span data-ttu-id="cd3a9-398">xlargerc</span><span class="sxs-lookup"><span data-stu-id="cd3a9-398">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="cd3a9-399">DW100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-399">DW100</span></span> |<span data-ttu-id="cd3a9-400">6</span><span class="sxs-lookup"><span data-stu-id="cd3a9-400">6</span></span> |<span data-ttu-id="cd3a9-401">6</span><span class="sxs-lookup"><span data-stu-id="cd3a9-401">6</span></span> |<span data-ttu-id="cd3a9-402">12</span><span class="sxs-lookup"><span data-stu-id="cd3a9-402">12</span></span> |<span data-ttu-id="cd3a9-403">23</span><span class="sxs-lookup"><span data-stu-id="cd3a9-403">23</span></span> |
| <span data-ttu-id="cd3a9-404">DW200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-404">DW200</span></span> |<span data-ttu-id="cd3a9-405">6</span><span class="sxs-lookup"><span data-stu-id="cd3a9-405">6</span></span> |<span data-ttu-id="cd3a9-406">12</span><span class="sxs-lookup"><span data-stu-id="cd3a9-406">12</span></span> |<span data-ttu-id="cd3a9-407">23</span><span class="sxs-lookup"><span data-stu-id="cd3a9-407">23</span></span> |<span data-ttu-id="cd3a9-408">47</span><span class="sxs-lookup"><span data-stu-id="cd3a9-408">47</span></span> |
| <span data-ttu-id="cd3a9-409">DW300</span><span class="sxs-lookup"><span data-stu-id="cd3a9-409">DW300</span></span> |<span data-ttu-id="cd3a9-410">6</span><span class="sxs-lookup"><span data-stu-id="cd3a9-410">6</span></span> |<span data-ttu-id="cd3a9-411">12</span><span class="sxs-lookup"><span data-stu-id="cd3a9-411">12</span></span> |<span data-ttu-id="cd3a9-412">23</span><span class="sxs-lookup"><span data-stu-id="cd3a9-412">23</span></span> |<span data-ttu-id="cd3a9-413">47</span><span class="sxs-lookup"><span data-stu-id="cd3a9-413">47</span></span> |
| <span data-ttu-id="cd3a9-414">DW400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-414">DW400</span></span> |<span data-ttu-id="cd3a9-415">6</span><span class="sxs-lookup"><span data-stu-id="cd3a9-415">6</span></span> |<span data-ttu-id="cd3a9-416">23</span><span class="sxs-lookup"><span data-stu-id="cd3a9-416">23</span></span> |<span data-ttu-id="cd3a9-417">47</span><span class="sxs-lookup"><span data-stu-id="cd3a9-417">47</span></span> |<span data-ttu-id="cd3a9-418">94</span><span class="sxs-lookup"><span data-stu-id="cd3a9-418">94</span></span> |
| <span data-ttu-id="cd3a9-419">DW500</span><span class="sxs-lookup"><span data-stu-id="cd3a9-419">DW500</span></span> |<span data-ttu-id="cd3a9-420">6</span><span class="sxs-lookup"><span data-stu-id="cd3a9-420">6</span></span> |<span data-ttu-id="cd3a9-421">23</span><span class="sxs-lookup"><span data-stu-id="cd3a9-421">23</span></span> |<span data-ttu-id="cd3a9-422">47</span><span class="sxs-lookup"><span data-stu-id="cd3a9-422">47</span></span> |<span data-ttu-id="cd3a9-423">94</span><span class="sxs-lookup"><span data-stu-id="cd3a9-423">94</span></span> |
| <span data-ttu-id="cd3a9-424">DW600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-424">DW600</span></span> |<span data-ttu-id="cd3a9-425">6</span><span class="sxs-lookup"><span data-stu-id="cd3a9-425">6</span></span> |<span data-ttu-id="cd3a9-426">23</span><span class="sxs-lookup"><span data-stu-id="cd3a9-426">23</span></span> |<span data-ttu-id="cd3a9-427">47</span><span class="sxs-lookup"><span data-stu-id="cd3a9-427">47</span></span> |<span data-ttu-id="cd3a9-428">94</span><span class="sxs-lookup"><span data-stu-id="cd3a9-428">94</span></span> |
| <span data-ttu-id="cd3a9-429">DW1000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-429">DW1000</span></span> |<span data-ttu-id="cd3a9-430">6</span><span class="sxs-lookup"><span data-stu-id="cd3a9-430">6</span></span> |<span data-ttu-id="cd3a9-431">47</span><span class="sxs-lookup"><span data-stu-id="cd3a9-431">47</span></span> |<span data-ttu-id="cd3a9-432">94</span><span class="sxs-lookup"><span data-stu-id="cd3a9-432">94</span></span> |<span data-ttu-id="cd3a9-433">188</span><span class="sxs-lookup"><span data-stu-id="cd3a9-433">188</span></span> |
| <span data-ttu-id="cd3a9-434">DW1200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-434">DW1200</span></span> |<span data-ttu-id="cd3a9-435">6</span><span class="sxs-lookup"><span data-stu-id="cd3a9-435">6</span></span> |<span data-ttu-id="cd3a9-436">47</span><span class="sxs-lookup"><span data-stu-id="cd3a9-436">47</span></span> |<span data-ttu-id="cd3a9-437">94</span><span class="sxs-lookup"><span data-stu-id="cd3a9-437">94</span></span> |<span data-ttu-id="cd3a9-438">188</span><span class="sxs-lookup"><span data-stu-id="cd3a9-438">188</span></span> |
| <span data-ttu-id="cd3a9-439">DW1500</span><span class="sxs-lookup"><span data-stu-id="cd3a9-439">DW1500</span></span> |<span data-ttu-id="cd3a9-440">6</span><span class="sxs-lookup"><span data-stu-id="cd3a9-440">6</span></span> |<span data-ttu-id="cd3a9-441">47</span><span class="sxs-lookup"><span data-stu-id="cd3a9-441">47</span></span> |<span data-ttu-id="cd3a9-442">94</span><span class="sxs-lookup"><span data-stu-id="cd3a9-442">94</span></span> |<span data-ttu-id="cd3a9-443">188</span><span class="sxs-lookup"><span data-stu-id="cd3a9-443">188</span></span> |
| <span data-ttu-id="cd3a9-444">DW2000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-444">DW2000</span></span> |<span data-ttu-id="cd3a9-445">6</span><span class="sxs-lookup"><span data-stu-id="cd3a9-445">6</span></span> |<span data-ttu-id="cd3a9-446">94</span><span class="sxs-lookup"><span data-stu-id="cd3a9-446">94</span></span> |<span data-ttu-id="cd3a9-447">188</span><span class="sxs-lookup"><span data-stu-id="cd3a9-447">188</span></span> |<span data-ttu-id="cd3a9-448">375</span><span class="sxs-lookup"><span data-stu-id="cd3a9-448">375</span></span> |
| <span data-ttu-id="cd3a9-449">DW3000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-449">DW3000</span></span> |<span data-ttu-id="cd3a9-450">6</span><span class="sxs-lookup"><span data-stu-id="cd3a9-450">6</span></span> |<span data-ttu-id="cd3a9-451">94</span><span class="sxs-lookup"><span data-stu-id="cd3a9-451">94</span></span> |<span data-ttu-id="cd3a9-452">188</span><span class="sxs-lookup"><span data-stu-id="cd3a9-452">188</span></span> |<span data-ttu-id="cd3a9-453">375</span><span class="sxs-lookup"><span data-stu-id="cd3a9-453">375</span></span> |
| <span data-ttu-id="cd3a9-454">DW6000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-454">DW6000</span></span> |<span data-ttu-id="cd3a9-455">6</span><span class="sxs-lookup"><span data-stu-id="cd3a9-455">6</span></span> |<span data-ttu-id="cd3a9-456">188</span><span class="sxs-lookup"><span data-stu-id="cd3a9-456">188</span></span> |<span data-ttu-id="cd3a9-457">375</span><span class="sxs-lookup"><span data-stu-id="cd3a9-457">375</span></span> |<span data-ttu-id="cd3a9-458">750</span><span class="sxs-lookup"><span data-stu-id="cd3a9-458">750</span></span> |

<span data-ttu-id="cd3a9-459">Por esta tabla de asignaciones de memoria de todo el sistema, puede ver que a una consulta que se ejecuta en DW2000 en la clase de recurso xlargercs se le asigna un total de 375 GB de memoria (6400 MB * 60 distribuciones / 1024 para pasar a GB) sobre la totalidad del almacenamiento de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-459">From this table of system-wide memory allocations, you can see that a query running on a DW2000 in the xlargerc resource class is allocated a total of 375 GB of memory (6,400 MB * 60 distributions / 1,024 to convert to GB) over the entirety of your SQL Data Warehouse.</span></span>

<span data-ttu-id="cd3a9-460">El mismo cálculo se aplica a las clases de recursos estáticos.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-460">The same calculation applies to static resource classes.</span></span>
 
## <a name="concurrency-slot-consumption"></a><span data-ttu-id="cd3a9-461">Consumo de ranuras de simultaneidad</span><span class="sxs-lookup"><span data-stu-id="cd3a9-461">Concurrency slot consumption</span></span>  
<span data-ttu-id="cd3a9-462">Almacenamiento de datos SQL concederá más memoria a las consultas que se ejecutan en clases de recursos superiores.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-462">SQL Data Warehouse grants more memory to queries running in higher resource classes.</span></span> <span data-ttu-id="cd3a9-463">La memoria es un recurso fijo.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-463">Memory is a fixed resource.</span></span>  <span data-ttu-id="cd3a9-464">Por lo tanto, cuanta más memoria asignada por consulta, menos consultas simultáneas se pueden ejecutar.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-464">Therefore, the more memory allocated per query, the fewer concurrent queries can execute.</span></span> <span data-ttu-id="cd3a9-465">En la tabla siguiente se reiteran todos los conceptos anteriores en una vista única donde se muestra el número de intervalos de simultaneidad disponibles por DWU, así como los espacios que consume cada clase de recurso.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-465">The following table reiterates all of the previous concepts in a single view that shows the number of concurrency slots available by DWU and the slots consumed by each resource class.</span></span>  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a><span data-ttu-id="cd3a9-466">Asignación y consumo de espacios de simultaneidad para las clases de recursos dinámicos</span><span class="sxs-lookup"><span data-stu-id="cd3a9-466">Allocation and consumption of concurrency slots for dynamic resource classes</span></span>  
| <span data-ttu-id="cd3a9-467">DWU</span><span class="sxs-lookup"><span data-stu-id="cd3a9-467">DWU</span></span> | <span data-ttu-id="cd3a9-468">N.º máximo de consultas simultáneas</span><span class="sxs-lookup"><span data-stu-id="cd3a9-468">Maximum concurrent queries</span></span> | <span data-ttu-id="cd3a9-469">Espacios de simultaneidad asignados</span><span class="sxs-lookup"><span data-stu-id="cd3a9-469">Concurrency slots allocated</span></span> | <span data-ttu-id="cd3a9-470">Ranuras utilizadas por smallrc</span><span class="sxs-lookup"><span data-stu-id="cd3a9-470">Slots used by smallrc</span></span> | <span data-ttu-id="cd3a9-471">Ranuras utilizadas por mediumrc</span><span class="sxs-lookup"><span data-stu-id="cd3a9-471">Slots used by mediumrc</span></span> | <span data-ttu-id="cd3a9-472">Ranuras utilizadas por largerc</span><span class="sxs-lookup"><span data-stu-id="cd3a9-472">Slots used by largerc</span></span> | <span data-ttu-id="cd3a9-473">Ranuras utilizadas por xlargerc</span><span class="sxs-lookup"><span data-stu-id="cd3a9-473">Slots used by xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="cd3a9-474">DW100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-474">DW100</span></span> |<span data-ttu-id="cd3a9-475">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-475">4</span></span> |<span data-ttu-id="cd3a9-476">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-476">4</span></span> |<span data-ttu-id="cd3a9-477">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-477">1</span></span> |<span data-ttu-id="cd3a9-478">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-478">1</span></span> |<span data-ttu-id="cd3a9-479">2</span><span class="sxs-lookup"><span data-stu-id="cd3a9-479">2</span></span> |<span data-ttu-id="cd3a9-480">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-480">4</span></span> |
| <span data-ttu-id="cd3a9-481">DW200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-481">DW200</span></span> |<span data-ttu-id="cd3a9-482">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-482">8</span></span> |<span data-ttu-id="cd3a9-483">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-483">8</span></span> |<span data-ttu-id="cd3a9-484">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-484">1</span></span> |<span data-ttu-id="cd3a9-485">2</span><span class="sxs-lookup"><span data-stu-id="cd3a9-485">2</span></span> |<span data-ttu-id="cd3a9-486">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-486">4</span></span> |<span data-ttu-id="cd3a9-487">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-487">8</span></span> |
| <span data-ttu-id="cd3a9-488">DW300</span><span class="sxs-lookup"><span data-stu-id="cd3a9-488">DW300</span></span> |<span data-ttu-id="cd3a9-489">12</span><span class="sxs-lookup"><span data-stu-id="cd3a9-489">12</span></span> |<span data-ttu-id="cd3a9-490">12</span><span class="sxs-lookup"><span data-stu-id="cd3a9-490">12</span></span> |<span data-ttu-id="cd3a9-491">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-491">1</span></span> |<span data-ttu-id="cd3a9-492">2</span><span class="sxs-lookup"><span data-stu-id="cd3a9-492">2</span></span> |<span data-ttu-id="cd3a9-493">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-493">4</span></span> |<span data-ttu-id="cd3a9-494">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-494">8</span></span> |
| <span data-ttu-id="cd3a9-495">DW400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-495">DW400</span></span> |<span data-ttu-id="cd3a9-496">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-496">16</span></span> |<span data-ttu-id="cd3a9-497">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-497">16</span></span> |<span data-ttu-id="cd3a9-498">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-498">1</span></span> |<span data-ttu-id="cd3a9-499">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-499">4</span></span> |<span data-ttu-id="cd3a9-500">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-500">8</span></span> |<span data-ttu-id="cd3a9-501">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-501">16</span></span> |
| <span data-ttu-id="cd3a9-502">DW500</span><span class="sxs-lookup"><span data-stu-id="cd3a9-502">DW500</span></span> |<span data-ttu-id="cd3a9-503">20 |</span><span class="sxs-lookup"><span data-stu-id="cd3a9-503">20</span></span> |<span data-ttu-id="cd3a9-504">20 |</span><span class="sxs-lookup"><span data-stu-id="cd3a9-504">20</span></span> |<span data-ttu-id="cd3a9-505">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-505">1</span></span> |<span data-ttu-id="cd3a9-506">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-506">4</span></span> |<span data-ttu-id="cd3a9-507">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-507">8</span></span> |<span data-ttu-id="cd3a9-508">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-508">16</span></span> |
| <span data-ttu-id="cd3a9-509">DW600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-509">DW600</span></span> |<span data-ttu-id="cd3a9-510">24</span><span class="sxs-lookup"><span data-stu-id="cd3a9-510">24</span></span> |<span data-ttu-id="cd3a9-511">24</span><span class="sxs-lookup"><span data-stu-id="cd3a9-511">24</span></span> |<span data-ttu-id="cd3a9-512">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-512">1</span></span> |<span data-ttu-id="cd3a9-513">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-513">4</span></span> |<span data-ttu-id="cd3a9-514">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-514">8</span></span> |<span data-ttu-id="cd3a9-515">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-515">16</span></span> |
| <span data-ttu-id="cd3a9-516">DW1000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-516">DW1000</span></span> |<span data-ttu-id="cd3a9-517">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-517">32</span></span> |<span data-ttu-id="cd3a9-518">40</span><span class="sxs-lookup"><span data-stu-id="cd3a9-518">40</span></span> |<span data-ttu-id="cd3a9-519">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-519">1</span></span> |<span data-ttu-id="cd3a9-520">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-520">8</span></span> |<span data-ttu-id="cd3a9-521">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-521">16</span></span> |<span data-ttu-id="cd3a9-522">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-522">32</span></span> |
| <span data-ttu-id="cd3a9-523">DW1200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-523">DW1200</span></span> |<span data-ttu-id="cd3a9-524">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-524">32</span></span> |<span data-ttu-id="cd3a9-525">48</span><span class="sxs-lookup"><span data-stu-id="cd3a9-525">48</span></span> |<span data-ttu-id="cd3a9-526">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-526">1</span></span> |<span data-ttu-id="cd3a9-527">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-527">8</span></span> |<span data-ttu-id="cd3a9-528">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-528">16</span></span> |<span data-ttu-id="cd3a9-529">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-529">32</span></span> |
| <span data-ttu-id="cd3a9-530">DW1500</span><span class="sxs-lookup"><span data-stu-id="cd3a9-530">DW1500</span></span> |<span data-ttu-id="cd3a9-531">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-531">32</span></span> |<span data-ttu-id="cd3a9-532">60</span><span class="sxs-lookup"><span data-stu-id="cd3a9-532">60</span></span> |<span data-ttu-id="cd3a9-533">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-533">1</span></span> |<span data-ttu-id="cd3a9-534">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-534">8</span></span> |<span data-ttu-id="cd3a9-535">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-535">16</span></span> |<span data-ttu-id="cd3a9-536">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-536">32</span></span> |
| <span data-ttu-id="cd3a9-537">DW2000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-537">DW2000</span></span> |<span data-ttu-id="cd3a9-538">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-538">32</span></span> |<span data-ttu-id="cd3a9-539">80</span><span class="sxs-lookup"><span data-stu-id="cd3a9-539">80</span></span> |<span data-ttu-id="cd3a9-540">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-540">1</span></span> |<span data-ttu-id="cd3a9-541">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-541">16</span></span> |<span data-ttu-id="cd3a9-542">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-542">32</span></span> |<span data-ttu-id="cd3a9-543">64</span><span class="sxs-lookup"><span data-stu-id="cd3a9-543">64</span></span> |
| <span data-ttu-id="cd3a9-544">DW3000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-544">DW3000</span></span> |<span data-ttu-id="cd3a9-545">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-545">32</span></span> |<span data-ttu-id="cd3a9-546">120</span><span class="sxs-lookup"><span data-stu-id="cd3a9-546">120</span></span> |<span data-ttu-id="cd3a9-547">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-547">1</span></span> |<span data-ttu-id="cd3a9-548">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-548">16</span></span> |<span data-ttu-id="cd3a9-549">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-549">32</span></span> |<span data-ttu-id="cd3a9-550">64</span><span class="sxs-lookup"><span data-stu-id="cd3a9-550">64</span></span> |
| <span data-ttu-id="cd3a9-551">DW6000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-551">DW6000</span></span> |<span data-ttu-id="cd3a9-552">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-552">32</span></span> |<span data-ttu-id="cd3a9-553">240</span><span class="sxs-lookup"><span data-stu-id="cd3a9-553">240</span></span> |<span data-ttu-id="cd3a9-554">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-554">1</span></span> |<span data-ttu-id="cd3a9-555">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-555">32</span></span> |<span data-ttu-id="cd3a9-556">64</span><span class="sxs-lookup"><span data-stu-id="cd3a9-556">64</span></span> |<span data-ttu-id="cd3a9-557">128</span><span class="sxs-lookup"><span data-stu-id="cd3a9-557">128</span></span> |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a><span data-ttu-id="cd3a9-558">Asignación y consumo de espacios de simultaneidad para las clases de recursos estáticos</span><span class="sxs-lookup"><span data-stu-id="cd3a9-558">Allocation and consumption of concurrency slots for static resource classes</span></span>  
| <span data-ttu-id="cd3a9-559">DWU</span><span class="sxs-lookup"><span data-stu-id="cd3a9-559">DWU</span></span> | <span data-ttu-id="cd3a9-560">N.º máximo de consultas simultáneas</span><span class="sxs-lookup"><span data-stu-id="cd3a9-560">Maximum concurrent queries</span></span> | <span data-ttu-id="cd3a9-561">Espacios de simultaneidad asignados</span><span class="sxs-lookup"><span data-stu-id="cd3a9-561">Concurrency slots allocated</span></span> |<span data-ttu-id="cd3a9-562">staticrc10</span><span class="sxs-lookup"><span data-stu-id="cd3a9-562">staticrc10</span></span> | <span data-ttu-id="cd3a9-563">staticrc20</span><span class="sxs-lookup"><span data-stu-id="cd3a9-563">staticrc20</span></span> | <span data-ttu-id="cd3a9-564">staticrc30</span><span class="sxs-lookup"><span data-stu-id="cd3a9-564">staticrc30</span></span> | <span data-ttu-id="cd3a9-565">staticrc40</span><span class="sxs-lookup"><span data-stu-id="cd3a9-565">staticrc40</span></span> | <span data-ttu-id="cd3a9-566">staticrc50</span><span class="sxs-lookup"><span data-stu-id="cd3a9-566">staticrc50</span></span> | <span data-ttu-id="cd3a9-567">staticrc60</span><span class="sxs-lookup"><span data-stu-id="cd3a9-567">staticrc60</span></span> | <span data-ttu-id="cd3a9-568">staticrc70</span><span class="sxs-lookup"><span data-stu-id="cd3a9-568">staticrc70</span></span> | <span data-ttu-id="cd3a9-569">staticrc80</span><span class="sxs-lookup"><span data-stu-id="cd3a9-569">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="cd3a9-570">DW100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-570">DW100</span></span> |<span data-ttu-id="cd3a9-571">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-571">4</span></span> |<span data-ttu-id="cd3a9-572">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-572">4</span></span> |<span data-ttu-id="cd3a9-573">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-573">1</span></span> |<span data-ttu-id="cd3a9-574">2</span><span class="sxs-lookup"><span data-stu-id="cd3a9-574">2</span></span> |<span data-ttu-id="cd3a9-575">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-575">4</span></span> |<span data-ttu-id="cd3a9-576">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-576">4</span></span> |<span data-ttu-id="cd3a9-577">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-577">4</span></span> |<span data-ttu-id="cd3a9-578">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-578">4</span></span> |<span data-ttu-id="cd3a9-579">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-579">4</span></span> |<span data-ttu-id="cd3a9-580">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-580">4</span></span> |
| <span data-ttu-id="cd3a9-581">DW200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-581">DW200</span></span> |<span data-ttu-id="cd3a9-582">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-582">8</span></span> |<span data-ttu-id="cd3a9-583">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-583">8</span></span> |<span data-ttu-id="cd3a9-584">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-584">1</span></span> |<span data-ttu-id="cd3a9-585">2</span><span class="sxs-lookup"><span data-stu-id="cd3a9-585">2</span></span> |<span data-ttu-id="cd3a9-586">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-586">4</span></span> |<span data-ttu-id="cd3a9-587">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-587">8</span></span> |<span data-ttu-id="cd3a9-588">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-588">8</span></span> |<span data-ttu-id="cd3a9-589">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-589">8</span></span> |<span data-ttu-id="cd3a9-590">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-590">8</span></span> |<span data-ttu-id="cd3a9-591">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-591">8</span></span> |
| <span data-ttu-id="cd3a9-592">DW300</span><span class="sxs-lookup"><span data-stu-id="cd3a9-592">DW300</span></span> |<span data-ttu-id="cd3a9-593">12</span><span class="sxs-lookup"><span data-stu-id="cd3a9-593">12</span></span> |<span data-ttu-id="cd3a9-594">12</span><span class="sxs-lookup"><span data-stu-id="cd3a9-594">12</span></span> |<span data-ttu-id="cd3a9-595">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-595">1</span></span> |<span data-ttu-id="cd3a9-596">2</span><span class="sxs-lookup"><span data-stu-id="cd3a9-596">2</span></span> |<span data-ttu-id="cd3a9-597">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-597">4</span></span> |<span data-ttu-id="cd3a9-598">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-598">8</span></span> |<span data-ttu-id="cd3a9-599">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-599">8</span></span> |<span data-ttu-id="cd3a9-600">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-600">8</span></span> |<span data-ttu-id="cd3a9-601">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-601">8</span></span> |<span data-ttu-id="cd3a9-602">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-602">8</span></span> |
| <span data-ttu-id="cd3a9-603">DW400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-603">DW400</span></span> |<span data-ttu-id="cd3a9-604">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-604">16</span></span> |<span data-ttu-id="cd3a9-605">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-605">16</span></span> |<span data-ttu-id="cd3a9-606">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-606">1</span></span> |<span data-ttu-id="cd3a9-607">2</span><span class="sxs-lookup"><span data-stu-id="cd3a9-607">2</span></span> |<span data-ttu-id="cd3a9-608">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-608">4</span></span> |<span data-ttu-id="cd3a9-609">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-609">8</span></span> |<span data-ttu-id="cd3a9-610">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-610">16</span></span> |<span data-ttu-id="cd3a9-611">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-611">16</span></span> |<span data-ttu-id="cd3a9-612">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-612">16</span></span> |<span data-ttu-id="cd3a9-613">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-613">16</span></span> |
| <span data-ttu-id="cd3a9-614">DW500</span><span class="sxs-lookup"><span data-stu-id="cd3a9-614">DW500</span></span> | <span data-ttu-id="cd3a9-615">20 |</span><span class="sxs-lookup"><span data-stu-id="cd3a9-615">20</span></span>| <span data-ttu-id="cd3a9-616">20 |</span><span class="sxs-lookup"><span data-stu-id="cd3a9-616">20</span></span>| <span data-ttu-id="cd3a9-617">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-617">1</span></span>| <span data-ttu-id="cd3a9-618">2</span><span class="sxs-lookup"><span data-stu-id="cd3a9-618">2</span></span>| <span data-ttu-id="cd3a9-619">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-619">4</span></span>| <span data-ttu-id="cd3a9-620">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-620">8</span></span>| <span data-ttu-id="cd3a9-621">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-621">16</span></span>| <span data-ttu-id="cd3a9-622">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-622">16</span></span>| <span data-ttu-id="cd3a9-623">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-623">16</span></span>| <span data-ttu-id="cd3a9-624">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-624">16</span></span>|
| <span data-ttu-id="cd3a9-625">DW600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-625">DW600</span></span> | <span data-ttu-id="cd3a9-626">24</span><span class="sxs-lookup"><span data-stu-id="cd3a9-626">24</span></span>| <span data-ttu-id="cd3a9-627">24</span><span class="sxs-lookup"><span data-stu-id="cd3a9-627">24</span></span>| <span data-ttu-id="cd3a9-628">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-628">1</span></span>| <span data-ttu-id="cd3a9-629">2</span><span class="sxs-lookup"><span data-stu-id="cd3a9-629">2</span></span>| <span data-ttu-id="cd3a9-630">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-630">4</span></span>| <span data-ttu-id="cd3a9-631">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-631">8</span></span>| <span data-ttu-id="cd3a9-632">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-632">16</span></span>| <span data-ttu-id="cd3a9-633">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-633">16</span></span>| <span data-ttu-id="cd3a9-634">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-634">16</span></span>| <span data-ttu-id="cd3a9-635">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-635">16</span></span>|
| <span data-ttu-id="cd3a9-636">DW1000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-636">DW1000</span></span> | <span data-ttu-id="cd3a9-637">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-637">32</span></span>| <span data-ttu-id="cd3a9-638">40</span><span class="sxs-lookup"><span data-stu-id="cd3a9-638">40</span></span>| <span data-ttu-id="cd3a9-639">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-639">1</span></span>| <span data-ttu-id="cd3a9-640">2</span><span class="sxs-lookup"><span data-stu-id="cd3a9-640">2</span></span>| <span data-ttu-id="cd3a9-641">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-641">4</span></span>| <span data-ttu-id="cd3a9-642">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-642">8</span></span>| <span data-ttu-id="cd3a9-643">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-643">16</span></span>| <span data-ttu-id="cd3a9-644">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-644">32</span></span>| <span data-ttu-id="cd3a9-645">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-645">32</span></span>| <span data-ttu-id="cd3a9-646">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-646">32</span></span>|
| <span data-ttu-id="cd3a9-647">DW1200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-647">DW1200</span></span> | <span data-ttu-id="cd3a9-648">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-648">32</span></span>| <span data-ttu-id="cd3a9-649">48</span><span class="sxs-lookup"><span data-stu-id="cd3a9-649">48</span></span>| <span data-ttu-id="cd3a9-650">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-650">1</span></span>| <span data-ttu-id="cd3a9-651">2</span><span class="sxs-lookup"><span data-stu-id="cd3a9-651">2</span></span>| <span data-ttu-id="cd3a9-652">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-652">4</span></span>| <span data-ttu-id="cd3a9-653">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-653">8</span></span>| <span data-ttu-id="cd3a9-654">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-654">16</span></span>| <span data-ttu-id="cd3a9-655">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-655">32</span></span>| <span data-ttu-id="cd3a9-656">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-656">32</span></span>| <span data-ttu-id="cd3a9-657">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-657">32</span></span>|
| <span data-ttu-id="cd3a9-658">DW1500</span><span class="sxs-lookup"><span data-stu-id="cd3a9-658">DW1500</span></span> | <span data-ttu-id="cd3a9-659">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-659">32</span></span>| <span data-ttu-id="cd3a9-660">60</span><span class="sxs-lookup"><span data-stu-id="cd3a9-660">60</span></span>| <span data-ttu-id="cd3a9-661">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-661">1</span></span>| <span data-ttu-id="cd3a9-662">2</span><span class="sxs-lookup"><span data-stu-id="cd3a9-662">2</span></span>| <span data-ttu-id="cd3a9-663">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-663">4</span></span>| <span data-ttu-id="cd3a9-664">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-664">8</span></span>| <span data-ttu-id="cd3a9-665">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-665">16</span></span>| <span data-ttu-id="cd3a9-666">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-666">32</span></span>| <span data-ttu-id="cd3a9-667">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-667">32</span></span>| <span data-ttu-id="cd3a9-668">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-668">32</span></span>|
| <span data-ttu-id="cd3a9-669">DW2000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-669">DW2000</span></span> | <span data-ttu-id="cd3a9-670">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-670">32</span></span>| <span data-ttu-id="cd3a9-671">80</span><span class="sxs-lookup"><span data-stu-id="cd3a9-671">80</span></span>| <span data-ttu-id="cd3a9-672">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-672">1</span></span>| <span data-ttu-id="cd3a9-673">2</span><span class="sxs-lookup"><span data-stu-id="cd3a9-673">2</span></span>| <span data-ttu-id="cd3a9-674">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-674">4</span></span>| <span data-ttu-id="cd3a9-675">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-675">8</span></span>| <span data-ttu-id="cd3a9-676">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-676">16</span></span>| <span data-ttu-id="cd3a9-677">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-677">32</span></span>| <span data-ttu-id="cd3a9-678">64</span><span class="sxs-lookup"><span data-stu-id="cd3a9-678">64</span></span>| <span data-ttu-id="cd3a9-679">64</span><span class="sxs-lookup"><span data-stu-id="cd3a9-679">64</span></span>|
| <span data-ttu-id="cd3a9-680">DW3000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-680">DW3000</span></span> | <span data-ttu-id="cd3a9-681">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-681">32</span></span>| <span data-ttu-id="cd3a9-682">120</span><span class="sxs-lookup"><span data-stu-id="cd3a9-682">120</span></span>| <span data-ttu-id="cd3a9-683">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-683">1</span></span>| <span data-ttu-id="cd3a9-684">2</span><span class="sxs-lookup"><span data-stu-id="cd3a9-684">2</span></span>| <span data-ttu-id="cd3a9-685">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-685">4</span></span>| <span data-ttu-id="cd3a9-686">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-686">8</span></span>| <span data-ttu-id="cd3a9-687">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-687">16</span></span>| <span data-ttu-id="cd3a9-688">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-688">32</span></span>| <span data-ttu-id="cd3a9-689">64</span><span class="sxs-lookup"><span data-stu-id="cd3a9-689">64</span></span>| <span data-ttu-id="cd3a9-690">64</span><span class="sxs-lookup"><span data-stu-id="cd3a9-690">64</span></span>|
| <span data-ttu-id="cd3a9-691">DW6000</span><span class="sxs-lookup"><span data-stu-id="cd3a9-691">DW6000</span></span> | <span data-ttu-id="cd3a9-692">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-692">32</span></span>| <span data-ttu-id="cd3a9-693">240</span><span class="sxs-lookup"><span data-stu-id="cd3a9-693">240</span></span>| <span data-ttu-id="cd3a9-694">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-694">1</span></span>| <span data-ttu-id="cd3a9-695">2</span><span class="sxs-lookup"><span data-stu-id="cd3a9-695">2</span></span>| <span data-ttu-id="cd3a9-696">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-696">4</span></span>| <span data-ttu-id="cd3a9-697">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-697">8</span></span>| <span data-ttu-id="cd3a9-698">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-698">16</span></span>| <span data-ttu-id="cd3a9-699">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-699">32</span></span>| <span data-ttu-id="cd3a9-700">64</span><span class="sxs-lookup"><span data-stu-id="cd3a9-700">64</span></span>| <span data-ttu-id="cd3a9-701">128</span><span class="sxs-lookup"><span data-stu-id="cd3a9-701">128</span></span>|

<span data-ttu-id="cd3a9-702">En esta tabla, puede ver que SQL Data Warehouse, que se ejecuta como DW1000, ofrece 32 consultas simultáneas como máximo y 40 ranuras de simultaneidad en total.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-702">From these tables, you can see that SQL Data Warehouse running as DW1000 allocates a maximum of 32 concurrent queries and a total of 40 concurrency slots.</span></span> <span data-ttu-id="cd3a9-703">Si todos los usuarios se ejecutan en la clase smallrc, se permitirían 32 consultas simultáneas, ya que cada una consumiría 1 espacio de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-703">If all users are running in smallrc, 32 concurrent queries would be allowed because each query would consume 1 concurrency slot.</span></span> <span data-ttu-id="cd3a9-704">Si todos los usuarios de DW1000 se ejecutaran en la clase mediumrc, se asignaría a cada consulta 800 MB por distribuciones para una asignación de memoria total de 47 GB por consulta y la simultaneidad se limitaría a 5 usuarios (40 espacios de simultaneidad/8 espacios por usuario mediumrc).</span><span class="sxs-lookup"><span data-stu-id="cd3a9-704">If all users on a DW1000 were running in mediumrc, each query would be allocated 800 MB per distribution for a total memory allocation of 47 GB per query, and concurrency would be limited to 5 users (40 concurrency slots / 8 slots per mediumrc user).</span></span>

## <a name="selecting-proper-resource-class"></a><span data-ttu-id="cd3a9-705">Selección de la clase de recurso correcta</span><span class="sxs-lookup"><span data-stu-id="cd3a9-705">Selecting proper resource class</span></span>  
<span data-ttu-id="cd3a9-706">Es una práctica recomendada asignar usuarios permanentemente a una clase de recursos en lugar de cambiar sus clases de recursos.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-706">A good practice is to permanently assign users to a resource class rather than changing their resource classes.</span></span> <span data-ttu-id="cd3a9-707">Por ejemplo, las cargas a tablas de almacén de columnas en clúster crean índices de mayor calidad cuando se les asigna más memoria.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-707">For example, loads to clustered columnstore tables create higher-quality indexes when allocated more memory.</span></span> <span data-ttu-id="cd3a9-708">Para asegurarse de que las cargas tienen acceso a una memoria superior, cree un usuario específico para cargar datos y asigne este usuario de forma permanente a una clase de recursos más alta.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-708">To ensure that loads have access to higher memory, create a user specifically for loading data and permanently assign this user to a higher resource class.</span></span>
<span data-ttu-id="cd3a9-709">Aquí puede consultar varios procedimientos recomendados.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-709">There are a couple of best practices to follow here.</span></span> <span data-ttu-id="cd3a9-710">Como se mencionó anteriormente, SQL DW admite dos tipos de clase de recurso: estáticos y dinámicos.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-710">As mentioned above, SQL DW supports two kinds of resource class types: static resource classes and dynamic resource classes.</span></span>
### <a name="loading-best-practices"></a><span data-ttu-id="cd3a9-711">Carga de procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="cd3a9-711">Loading best practices</span></span>
1.  <span data-ttu-id="cd3a9-712">Si se espera tener cargas con una cantidad regular de datos, una clase de recurso estático es una buena elección.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-712">If the expectations are loads with regular amount of data, a static resource class is a good choice.</span></span> <span data-ttu-id="cd3a9-713">Más adelante, al escalar para obtener una mayor capacidad de proceso, el almacenamiento de datos será capaz de ejecutar más consultas simultáneas sin hacer cambios, ya que el usuario que realiza la carga no consume más memoria.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-713">Later, when scaling up to get more computational power, the data warehouse will be able to run more concurrent queries out-of-the-box, as the load user does not consume more memory.</span></span>
2.  <span data-ttu-id="cd3a9-714">Si se espera tener mayores cargas en algunas ocasiones, una clase de recurso dinámico es una buena elección.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-714">If the expectations are bigger loads in some occasions, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="cd3a9-715">Más adelante, al escalar para obtener una mayor capacidad de proceso, el usuario que realiza la carga obtendrá más memoria directamente, con lo que la carga se podrá realizar más rápido.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-715">Later, when scaling up to get more computational power, the load user will get more memory out-of-the-box, hence allowing the load to perform faster.</span></span>

<span data-ttu-id="cd3a9-716">La memoria necesaria para procesar las cargas eficazmente depende de la naturaleza de la tabla cargada y de la cantidad de datos procesados.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-716">The memory needed to process loads efficiently depends on the nature of the table loaded and the amount of data processed.</span></span> <span data-ttu-id="cd3a9-717">Por ejemplo, cargar datos en tablas CCI requiere memoria para permitir que se llegue a los grupos de filas CCI de forma óptima.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-717">For instance, loading data into CCI tables requires some memory to let CCI rowgroups reach optimality.</span></span> <span data-ttu-id="cd3a9-718">Para más información, consulte la guía sobre los índices de almacén de columnas y la carga de datos.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-718">For more details, see the Columnstore indexes - data loading guidance.</span></span>

<span data-ttu-id="cd3a9-719">Como procedimiento recomendado, le aconsejamos que utilice al menos 200 MB de memoria para las cargas.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-719">As a best practice, we advise you to use at least 200MB of memory for loads.</span></span>

### <a name="querying-best-practices"></a><span data-ttu-id="cd3a9-720">Procedimientos recomendados sobre las consultas</span><span class="sxs-lookup"><span data-stu-id="cd3a9-720">Querying best practices</span></span>
<span data-ttu-id="cd3a9-721">Las consultas tienen requisitos diferentes en función de su complejidad.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-721">Queries have different requirements depending on their complexity.</span></span> <span data-ttu-id="cd3a9-722">Tanto el aumento de la memoria por cada consulta como la simultaneidad constituyen mecanismos válidos para aumentar el rendimiento general según las necesidades de la consulta.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-722">Increasing memory per query or increasing the concurrency are both valid ways to augment overall throughput depending on the query needs.</span></span>
1.  <span data-ttu-id="cd3a9-723">Si se espera tener consultas normales y complejas (por ejemplo, para generar informes diarios y semanales) y no es necesario aprovechar las ventajas de la simultaneidad, una clase de recurso dinámico es una buena elección.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-723">If the expectations are regular, complex queries (for instance, to generate daily and weekly reports) and do not need to take advantage of concurrency, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="cd3a9-724">Si el sistema tiene más datos que se van a procesar, al escalar el almacenamiento de datos se proporcionará, por tanto, automáticamente más memoria para el usuario que ejecuta la consulta.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-724">If the system has more data to process, scaling up the data warehouse will therefore automatically provide more memory to the user running the query.</span></span>
2.  <span data-ttu-id="cd3a9-725">Si se espera tener modelos de simultaneidad variables o diurnos (por ejemplo, si se consulta la base de datos a través de la interfaz de usuario de un sitio web ampliamente accesible), una clase de recurso estático es una buena elección.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-725">If the expectations are variable or diurnal concurrency patterns (for instance if the database is queried through a web UI broadly accessible), a static resource class is a good choice.</span></span> <span data-ttu-id="cd3a9-726">Más adelante, cuando se escale a un almacenamiento de datos, el usuario asociado a la clase de recurso estático será capaz automáticamente de ejecutar más consultas simultáneas.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-726">Later, when scaling up to data warehouse, the user associated with the static resource class will automatically be able to run more concurrent queries.</span></span>

<span data-ttu-id="cd3a9-727">La selección de la concesión de memoria adecuada según las necesidades de las consultas no resulta trivial, ya que depende de muchos factores, como la cantidad de datos consultados, la naturaleza de los esquemas de tabla y los diversos predicados de grupo, selección y combinación.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-727">Selecting proper memory grant depending on the need of your query is non-trivial, as it depends on many factors, such as the amount of data queried, the nature of the table schemas, and various join, selection, and group predicates.</span></span> <span data-ttu-id="cd3a9-728">Desde un punto de vista general, la asignación de más memoria permitirá que las consultas se completen más rápidamente, pero podría reducir la simultaneidad global.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-728">From a general standpoint, allocating more memory will allow queries to complete faster, but would reduce the overall concurrency.</span></span> <span data-ttu-id="cd3a9-729">Si la simultaneidad no es un problema, asignar una cantidad de memoria mayor de la necesaria no resulta perjudicial.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-729">If concurrency is not an issue, over-allocating memory does not harm.</span></span> <span data-ttu-id="cd3a9-730">Para ajustar el rendimiento, puede ser preciso probar con distintas combinaciones de clases de recursos.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-730">To fine-tune throughput, trying various flavors of resource classes may be required.</span></span>

<span data-ttu-id="cd3a9-731">Puede usar el siguiente procedimiento almacenado para averiguar la concesión de memoria y simultaneidad por clase de recurso en un SLO determinado y la clase de recurso recomendada más apropiada para operaciones de CCI que usen mucho la memoria en la tabla CCI sin particiones en una clase de recurso determinado:</span><span class="sxs-lookup"><span data-stu-id="cd3a9-731">You can use the following stored procedure to figure out concurrency and memory grant per resource class at a given SLO and the closest best resource class for memory intensive CCI operations on non-partitioned CCI table at a given resource class:</span></span>

#### <a name="description"></a><span data-ttu-id="cd3a9-732">Description:</span><span class="sxs-lookup"><span data-stu-id="cd3a9-732">Description:</span></span>  
<span data-ttu-id="cd3a9-733">Este es el propósito de este procedimiento almacenado:</span><span class="sxs-lookup"><span data-stu-id="cd3a9-733">Here's the purpose of this stored procedure:</span></span>  
1. <span data-ttu-id="cd3a9-734">Ayudar a los usuarios a averiguar la concesión de memoria y simultaneidad por clase de recurso en un SLO determinado.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-734">To help user figure out concurrency and memory grant per resource class at a given SLO.</span></span> <span data-ttu-id="cd3a9-735">El usuario tiene que proporcionar un valor NULL tanto para el esquema como para el nombre de tabla, tal como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-735">User needs to provide NULL for both schema and tablename for this as shown in the example below.</span></span>  
2. <span data-ttu-id="cd3a9-736">Ayudar al usuario a averiguar la clase de recurso recomendada más adecuada para las operaciones CCI que usan mucha memoria (carga, tabla de copia, regeneración de índices, etc.) en la tabla CCI sin particiones con una clase de recurso determinado.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-736">To help user figure out the closest best resource class for the memory intensed CCI operations (load, copy table, rebuild index, etc.) on non partitioned CCI table at a given resource class.</span></span> <span data-ttu-id="cd3a9-737">El procedimiento almacenado usa el esquema de tabla para averiguar la concesión de memoria necesaria en este caso.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-737">The stored proc uses table schema to find out the required memory grant for this.</span></span>

#### <a name="dependencies--restrictions"></a><span data-ttu-id="cd3a9-738">Dependencias y restricciones:</span><span class="sxs-lookup"><span data-stu-id="cd3a9-738">Dependencies & Restrictions:</span></span>
- <span data-ttu-id="cd3a9-739">Este procedimiento almacenado no está diseñado para calcular los requisitos de memoria de la tabla CCI con particiones.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-739">This stored proc is not designed to calculate memory requirement for partitioned-cci table.</span></span>    
- <span data-ttu-id="cd3a9-740">Este procedimiento almacenado no tiene en cuenta los requisitos de memoria de la parte SELECT de CTAS/INSERT-SELECT y se da por supuesto que es una instrucción SELECT simple.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-740">This stored proc doesn't take memory requirement into account for the SELECT part of CTAS/INSERT-SELECT and assumes it to be a simple SELECT.</span></span>
- <span data-ttu-id="cd3a9-741">Este procedimiento almacenado utiliza una tabla temporal, por lo que se puede utilizar en la sesión en la que se creó.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-741">This stored proc uses a temp table so this can be used in the session where this stored proc was created.</span></span>    
- <span data-ttu-id="cd3a9-742">Este procedimiento almacenado depende de las ofertas actuales (por ejemplo, configuración de hardware, configuración DMS) y, si algo cambiara, no funcionaría correctamente.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-742">This stored proc depends on the current offerings (e.g. hardware configuration, DMS config) and if any of that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="cd3a9-743">Este procedimiento almacenado depende del límite de simultaneidad ofrecido actualmente y, si este cambiara, no funcionaría correctamente.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-743">This stored proc depends on existing offered concurrency limit and if that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="cd3a9-744">Este procedimiento almacenado depende de las ofertas de clase de recursos actuales y, si estas cambiaran, no funcionaría correctamente.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-744">This stored proc depends on existing resource class offerings and if that changes then this stored proc wuold not work correctly.</span></span>  

>  [!NOTE]  
>  <span data-ttu-id="cd3a9-745">Si no se obtienen resultados después de ejecutar el procedimiento almacenado con los parámetros proporcionados, podrían darse dos circunstancias.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-745">If you are not getting output after executing stored procedure with parameters provided then there could be two cases.</span></span> <br /><span data-ttu-id="cd3a9-746">1. Algún parámetro del almacenamiento de datos contiene un valor de SLO no válido</span><span class="sxs-lookup"><span data-stu-id="cd3a9-746">1. Either DW Parameter contains invalid SLO value</span></span> <br /><span data-ttu-id="cd3a9-747">2. O bien, no hay ninguna clase de recursos coincidente para la operación CCI, si se proporcionó el nombre de la tabla.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-747">2. OR there are no matching resource class for CCI operation if table name was provided.</span></span> <br /><span data-ttu-id="cd3a9-748">Por ejemplo, en DW100, la concesión de memoria máxima disponible es de 400 MB y el esquema de tabla es lo suficientemente ancho como para superar el requisito de 400 MB.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-748">For example, at DW100, highest memory grant available is 400MB and if table schema is wide enough to cross the requirement of 400MB.</span></span>
      
#### <a name="usage-example"></a><span data-ttu-id="cd3a9-749">Ejemplo de uso:</span><span class="sxs-lookup"><span data-stu-id="cd3a9-749">Usage example:</span></span>
<span data-ttu-id="cd3a9-750">Sintaxis:</span><span class="sxs-lookup"><span data-stu-id="cd3a9-750">Syntax:</span></span>  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. <span data-ttu-id="cd3a9-751">@DWU: proporcione un parámetro NULL para extraer la unidad de almacenamiento de datos actual de la base de datos de almacenamiento de datos o proporcione una unidad admitida con el formato 'DW100'</span><span class="sxs-lookup"><span data-stu-id="cd3a9-751">@DWU: Either provide a NULL parameter to extract the current DWU from the DW DB or provide any supported DWU in the form of 'DW100'</span></span>
2. <span data-ttu-id="cd3a9-752">@SCHEMA_NAME: proporcione un nombre de esquema de la tabla</span><span class="sxs-lookup"><span data-stu-id="cd3a9-752">@SCHEMA_NAME: Provide a schema name of the table</span></span>
3. <span data-ttu-id="cd3a9-753">@TABLE_NAME: proporcione un nombre de tabla del interés</span><span class="sxs-lookup"><span data-stu-id="cd3a9-753">@TABLE_NAME: Provide a table name of the interest</span></span>

<span data-ttu-id="cd3a9-754">Ejemplos de ejecución de este procedimiento almacenado:</span><span class="sxs-lookup"><span data-stu-id="cd3a9-754">Examples executing this stored proc:</span></span>  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

<span data-ttu-id="cd3a9-755">La instancia de Table1 utilizada en los ejemplos anteriores se pudo crear como sigue:</span><span class="sxs-lookup"><span data-stu-id="cd3a9-755">Table1 used in the above examples could be created as below:</span></span>  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-the-stored-procedure-definition"></a><span data-ttu-id="cd3a9-756">Aquí puede ver la definición del procedimiento almacenado:</span><span class="sxs-lookup"><span data-stu-id="cd3a9-756">Here's the stored procedure definition:</span></span>
```sql  
-------------------------------------------------------------------------------
-- Dropping prc_workload_management_by_DWU procedure if it exists.
-------------------------------------------------------------------------------
IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'prc_workload_management_by_DWU')
DROP PROCEDURE dbo.prc_workload_management_by_DWU
GO

-------------------------------------------------------------------------------
-- Creating prc_workload_management_by_DWU.
-------------------------------------------------------------------------------
CREATE PROCEDURE dbo.prc_workload_management_by_DWU
(   @DWU VARCHAR(7),
      @SCHEMA_NAME VARCHAR(128),
       @TABLE_NAME VARCHAR(128)
)
AS
IF @DWU IS NULL
BEGIN
-- Selecting proper DWU for the current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need to supply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) to hold mapping info.
-- CREATE TABLE #ref
CREATE TABLE #ref
WITH (DISTRIBUTION = ROUND_ROBIN)
AS 
WITH
-- Creating concurrency slots mapping for various DWUs.
alloc
AS
(
  SELECT 'DW100' AS DWU, 4 AS max_queries, 4 AS max_slots, 1 AS slots_used_smallrc, 1 AS slots_used_mediumrc,
        2 AS slots_used_largerc, 4 AS slots_used_xlargerc, 1 AS slots_used_staticrc10, 2 AS slots_used_staticrc20,
        4 AS slots_used_staticrc30, 4 AS slots_used_staticrc40, 4 AS slots_used_staticrc50,
        4 AS slots_used_staticrc60, 4 AS slots_used_staticrc70, 4 AS slots_used_staticrc80
  UNION ALL
    SELECT 'DW200', 8, 8, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW300', 12, 12, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW400', 16, 16, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
     SELECT 'DW500', 20, 20, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW600', 24, 24, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW1000', 32, 40, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1200', 32, 48, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1500', 32, 60, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW2000', 32, 80, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
   SELECT 'DW3000', 32, 120, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
    SELECT 'DW6000', 32, 240, 1, 32, 64, 128, 1, 2, 4, 8, 16, 32, 64, 128
)
-- Creating workload mapping to their corresponding slot consumption and default memory grant.
,map
AS
(
  SELECT 'SloDWGroupC00' AS wg_name,1 AS slots_used,100 AS tgt_mem_grant_MB
  UNION ALL
    SELECT 'SloDWGroupC01',2,200
  UNION ALL
    SELECT 'SloDWGroupC02',4,400
  UNION ALL
    SELECT 'SloDWGroupC03',8,800
  UNION ALL
    SELECT 'SloDWGroupC04',16,1600
  UNION ALL
    SELECT 'SloDWGroupC05',32,3200
  UNION ALL
    SELECT 'SloDWGroupC06',64,6400
  UNION ALL
    SELECT 'SloDWGroupC07',128,12800
)
-- Creating ref based on current / asked DWU.
, ref
AS
(
  SELECT  a1.*
  ,       m1.wg_name          AS wg_name_smallrc
  ,       m1.tgt_mem_grant_MB AS tgt_mem_grant_MB_smallrc
  ,       m2.wg_name          AS wg_name_mediumrc
  ,       m2.tgt_mem_grant_MB AS tgt_mem_grant_MB_mediumrc
  ,       m3.wg_name          AS wg_name_largerc
  ,       m3.tgt_mem_grant_MB AS tgt_mem_grant_MB_largerc
  ,       m4.wg_name          AS wg_name_xlargerc
  ,       m4.tgt_mem_grant_MB AS tgt_mem_grant_MB_xlargerc
  ,       m5.wg_name          AS wg_name_staticrc10
  ,       m5.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc10
  ,       m6.wg_name          AS wg_name_staticrc20
  ,       m6.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc20
  ,       m7.wg_name          AS wg_name_staticrc30
  ,       m7.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc30
  ,       m8.wg_name          AS wg_name_staticrc40
  ,       m8.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc40
  ,       m9.wg_name          AS wg_name_staticrc50
  ,       m9.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc50
  ,       m10.wg_name          AS wg_name_staticrc60
  ,       m10.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc60
  ,       m11.wg_name          AS wg_name_staticrc70
  ,       m11.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc70
  ,       m12.wg_name          AS wg_name_staticrc80
  ,       m12.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc80
  FROM alloc a1
  JOIN map   m1  ON a1.slots_used_smallrc     = m1.slots_used
  JOIN map   m2  ON a1.slots_used_mediumrc    = m2.slots_used
  JOIN map   m3  ON a1.slots_used_largerc     = m3.slots_used
  JOIN map   m4  ON a1.slots_used_xlargerc    = m4.slots_used
  JOIN map   m5  ON a1.slots_used_staticrc10    = m5.slots_used
  JOIN map   m6  ON a1.slots_used_staticrc20    = m6.slots_used
  JOIN map   m7  ON a1.slots_used_staticrc30    = m7.slots_used
  JOIN map   m8  ON a1.slots_used_staticrc40    = m8.slots_used
  JOIN map   m9  ON a1.slots_used_staticrc50    = m9.slots_used
  JOIN map   m10  ON a1.slots_used_staticrc60    = m10.slots_used
  JOIN map   m11  ON a1.slots_used_staticrc70    = m11.slots_used
  JOIN map   m12  ON a1.slots_used_staticrc80    = m12.slots_used
-- WHERE   a1.DWU = @DWU
  WHERE   a1.DWU = UPPER(@DWU)
)
SELECT  DWU
,       max_queries
,       max_slots
,       slots_used
,       wg_name
,       tgt_mem_grant_MB
,       up1 as rc
,       (ROW_NUMBER() OVER(PARTITION BY DWU ORDER BY DWU)) as rc_id
FROM
(
    SELECT  DWU
    ,       max_queries
    ,       max_slots
    ,       slots_used
    ,       wg_name
    ,       tgt_mem_grant_MB
    ,       REVERSE(SUBSTRING(REVERSE(wg_names),1,CHARINDEX('_',REVERSE(wg_names),1)-1)) as up1
    ,       REVERSE(SUBSTRING(REVERSE(tgt_mem_grant_MBs),1,CHARINDEX('_',REVERSE(tgt_mem_grant_MBs),1)-1)) as up2
    ,       REVERSE(SUBSTRING(REVERSE(slots_used_all),1,CHARINDEX('_',REVERSE(slots_used_all),1)-1)) as up3
    FROM    ref AS r1
    UNPIVOT
    (
        wg_name FOR wg_names IN (wg_name_smallrc,wg_name_mediumrc,wg_name_largerc,wg_name_xlargerc,
        wg_name_staticrc10, wg_name_staticrc20, wg_name_staticrc30, wg_name_staticrc40, wg_name_staticrc50,
        wg_name_staticrc60, wg_name_staticrc70, wg_name_staticrc80)
    ) AS r2
    UNPIVOT
    (
        tgt_mem_grant_MB FOR tgt_mem_grant_MBs IN (tgt_mem_grant_MB_smallrc,tgt_mem_grant_MB_mediumrc,
        tgt_mem_grant_MB_largerc,tgt_mem_grant_MB_xlargerc, tgt_mem_grant_MB_staticrc10, tgt_mem_grant_MB_staticrc20,
        tgt_mem_grant_MB_staticrc30, tgt_mem_grant_MB_staticrc40, tgt_mem_grant_MB_staticrc50,
        tgt_mem_grant_MB_staticrc60, tgt_mem_grant_MB_staticrc70, tgt_mem_grant_MB_staticrc80)
    ) AS r3
    UNPIVOT
    (
        slots_used FOR slots_used_all IN (slots_used_smallrc,slots_used_mediumrc,slots_used_largerc,
        slots_used_xlargerc, slots_used_staticrc10, slots_used_staticrc20, slots_used_staticrc30,
        slots_used_staticrc40, slots_used_staticrc50, slots_used_staticrc60, slots_used_staticrc70,
        slots_used_staticrc80)
    ) AS r4
) a
WHERE   up1 = up2
AND     up1 = up3
;
-- Getting current info about workload groups.
WITH  
dmv  
AS  
(
  SELECT
          rp.name                                           AS rp_name
  ,       rp.max_memory_kb*1.0/1048576                      AS rp_max_mem_GB
  ,       (rp.max_memory_kb*1.0/1024)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_MB
  ,       (rp.max_memory_kb*1.0/1048576)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_GB
  ,       wg.name                                           AS wg_name
  ,       wg.importance                                     AS importance
  ,       wg.request_max_memory_grant_percent               AS request_max_memory_grant_percent
  FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
  JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    ON  wg.pdw_node_id  = rp.pdw_node_id
                                                                  AND wg.pool_id      = rp.pool_id
  WHERE   rp.name = 'SloDWPool'
  GROUP BY
          rp.name
  ,       rp.max_memory_kb
  ,       wg.name
  ,       wg.importance
  ,       wg.request_max_memory_grant_percent
)
-- Creating resource class name mapping.
,names
AS
(
  SELECT 'smallrc' as resource_class, 1 as rc_id
  UNION ALL
    SELECT 'mediumrc', 2
  UNION ALL
    SELECT 'largerc', 3
  UNION ALL
    SELECT 'xlargerc', 4
  UNION ALL
    SELECT 'staticrc10', 5
  UNION ALL
    SELECT 'staticrc20', 6
  UNION ALL
    SELECT 'staticrc30', 7
  UNION ALL
    SELECT 'staticrc40', 8
  UNION ALL
    SELECT 'staticrc50', 9
  UNION ALL
    SELECT 'staticrc60', 10
  UNION ALL
    SELECT 'staticrc70', 11
  UNION ALL
    SELECT 'staticrc80', 12
)
,base AS
(   SELECT  schema_name
    ,       table_name
    ,       SUM(column_count)                   AS column_count
    ,       ISNULL(SUM(short_string_column_count),0)   AS short_string_column_count
    ,       ISNULL(SUM(long_string_column_count),0)    AS long_string_column_count
    FROM    (   SELECT  sm.name                                             AS schema_name
                ,       tb.name                                             AS table_name
                ,       COUNT(co.column_id)                                 AS column_count
                           ,       CASE    WHEN co.system_type_id IN (36,43,106,108,165,167,173,175,231,239) 
                                AND  co.max_length <= 32 
                                THEN COUNT(co.column_id) 
                        END                                                 AS short_string_column_count
                ,       CASE    WHEN co.system_type_id IN (165,167,173,175,231,239) 
                                AND  co.max_length > 32 and co.max_length <=8000
                                THEN COUNT(co.column_id) 
                        END                                                 AS long_string_column_count
                FROM    sys.schemas AS sm
                JOIN    sys.tables  AS tb   on sm.[schema_id] = tb.[schema_id]
                JOIN    sys.columns AS co   ON tb.[object_id] = co.[object_id]
                           WHERE tb.name = @TABLE_NAME AND sm.name = @SCHEMA_NAME
                GROUP BY sm.name
                ,        tb.name
                ,        co.system_type_id
                ,        co.max_length            ) a
GROUP BY schema_name
,        table_name
)
, size AS
(
SELECT  schema_name
,       table_name
,       75497472                                            AS table_overhead

,       column_count*1048576*8                              AS column_size
,       short_string_column_count*1048576*32                       AS short_string_size,       (long_string_column_count*16777216) AS long_string_size
FROM    base
UNION
SELECT CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as schema_name
         ,CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as table_name
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as table_overhead
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as column_size
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as short_string_size

,CASE WHEN COUNT(*) = 0 THEN 0 END as long_string_size
FROM   base
)
, load_multiplier as 
(
SELECT  CASE 
                     WHEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) > 0 THEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) 
                     ELSE 1 
              END AS multipliplication_factor
) 
       SELECT  r1.DWU
       , schema_name
       , table_name
       , rc.resource_class as closest_rc_in_increasing_order
       , max_queries_at_this_rc = CASE
             WHEN (r1.max_slots / r1.slots_used > r1.max_queries)
                  THEN r1.max_queries
             ELSE r1.max_slots / r1.slots_used
                  END
       , r1.max_slots as max_concurrency_slots
       , r1.slots_used as required_slots_for_the_rc
       , r1.tgt_mem_grant_MB  as rc_mem_grant_MB
       , CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) AS est_mem_grant_required_for_cci_operation_MB       
       FROM    size, load_multiplier, #ref r1, names  rc
       WHERE r1.rc_id=rc.rc_id
                     AND CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) < r1.tgt_mem_grant_MB
       ORDER BY ABS(CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) - r1.tgt_mem_grant_MB)
GO
```

## <a name="query-importance"></a><span data-ttu-id="cd3a9-757">Importancia de las consultas</span><span class="sxs-lookup"><span data-stu-id="cd3a9-757">Query importance</span></span>
<span data-ttu-id="cd3a9-758">Almacenamiento de datos SQL implementa las clases de recursos mediante el uso de grupos de cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-758">SQL Data Warehouse implements resource classes by using workload groups.</span></span> <span data-ttu-id="cd3a9-759">Hay un total de ocho grupos de cargas de trabajo que controlan el comportamiento de las clases de recursos en los distintos tamaños de DWU.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-759">There are a total of eight workload groups that control the behavior of the resource classes across the various DWU sizes.</span></span> <span data-ttu-id="cd3a9-760">Para cualquier DWU, Almacenamiento de datos SQL solo usa cuatro de los ocho grupos de cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-760">For any DWU, SQL Data Warehouse uses only four of the eight workload groups.</span></span> <span data-ttu-id="cd3a9-761">Esto tiene sentido porque cada grupo de cargas de trabajo está asignado a una de las cuatro clases de recursos: smallrc, mediumrc, largerc o xlargerc.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-761">This makes sense because each workload group is assigned to one of four resource classes: smallrc, mediumrc, largerc, or xlargerc.</span></span> <span data-ttu-id="cd3a9-762">La importancia de comprender los grupos de cargas de trabajo es que algunos de estos grupos se establecen con un nivel de *importancia*más alto.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-762">The importance of understanding the workload groups is that some of these workload groups are set to higher *importance*.</span></span> <span data-ttu-id="cd3a9-763">El nivel de importancia se usa para la programación de la CPU.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-763">Importance is used for CPU scheduling.</span></span> <span data-ttu-id="cd3a9-764">Las consultas que se ejecutan con importancia alta obtendrán tres veces más ciclos de CPU que aquellas con importancia media.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-764">Queries run with high importance will get three times more CPU cycles than those with medium importance.</span></span> <span data-ttu-id="cd3a9-765">Por lo tanto, las asignaciones de espacio de simultaneidad también determinan la prioridad en la CPU.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-765">Therefore, concurrency slot mappings also determine CPU priority.</span></span> <span data-ttu-id="cd3a9-766">Si una consulta utiliza 16 o más espacios, se ejecuta con importancia alta.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-766">When a query consumes 16 or more slots, it runs as high importance.</span></span>

<span data-ttu-id="cd3a9-767">La tabla siguiente muestra las asignaciones de importancia para cada grupo de cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-767">The following table shows the importance mappings for each workload group.</span></span>

### <a name="workload-group-mappings-to-concurrency-slots-and-importance"></a><span data-ttu-id="cd3a9-768">Asignaciones de grupos de cargas de trabajo a los espacios de simultaneidad e importancia</span><span class="sxs-lookup"><span data-stu-id="cd3a9-768">Workload group mappings to concurrency slots and importance</span></span>
| <span data-ttu-id="cd3a9-769">Grupos de carga de trabajo</span><span class="sxs-lookup"><span data-stu-id="cd3a9-769">Workload groups</span></span> | <span data-ttu-id="cd3a9-770">Asignación de espacio de simultaneidad</span><span class="sxs-lookup"><span data-stu-id="cd3a9-770">Concurrency slot mapping</span></span> | <span data-ttu-id="cd3a9-771">MB/Distribución</span><span class="sxs-lookup"><span data-stu-id="cd3a9-771">MB / Distribution</span></span> | <span data-ttu-id="cd3a9-772">Asignación de importancia</span><span class="sxs-lookup"><span data-stu-id="cd3a9-772">Importance mapping</span></span> |
|:--- |:---:|:---:|:--- |
| <span data-ttu-id="cd3a9-773">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="cd3a9-773">SloDWGroupC00</span></span> |<span data-ttu-id="cd3a9-774">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-774">1</span></span> |<span data-ttu-id="cd3a9-775">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-775">100</span></span> |<span data-ttu-id="cd3a9-776">Mediano</span><span class="sxs-lookup"><span data-stu-id="cd3a9-776">Medium</span></span> |
| <span data-ttu-id="cd3a9-777">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="cd3a9-777">SloDWGroupC01</span></span> |<span data-ttu-id="cd3a9-778">2</span><span class="sxs-lookup"><span data-stu-id="cd3a9-778">2</span></span> |<span data-ttu-id="cd3a9-779">200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-779">200</span></span> |<span data-ttu-id="cd3a9-780">Mediano</span><span class="sxs-lookup"><span data-stu-id="cd3a9-780">Medium</span></span> |
| <span data-ttu-id="cd3a9-781">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="cd3a9-781">SloDWGroupC02</span></span> |<span data-ttu-id="cd3a9-782">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-782">4</span></span> |<span data-ttu-id="cd3a9-783">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-783">400</span></span> |<span data-ttu-id="cd3a9-784">Mediano</span><span class="sxs-lookup"><span data-stu-id="cd3a9-784">Medium</span></span> |
| <span data-ttu-id="cd3a9-785">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="cd3a9-785">SloDWGroupC03</span></span> |<span data-ttu-id="cd3a9-786">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-786">8</span></span> |<span data-ttu-id="cd3a9-787">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-787">800</span></span> |<span data-ttu-id="cd3a9-788">Mediano</span><span class="sxs-lookup"><span data-stu-id="cd3a9-788">Medium</span></span> |
| <span data-ttu-id="cd3a9-789">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="cd3a9-789">SloDWGroupC04</span></span> |<span data-ttu-id="cd3a9-790">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-790">16</span></span> |<span data-ttu-id="cd3a9-791">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-791">1,600</span></span> |<span data-ttu-id="cd3a9-792">Alto</span><span class="sxs-lookup"><span data-stu-id="cd3a9-792">High</span></span> |
| <span data-ttu-id="cd3a9-793">SloDWGroupC05</span><span class="sxs-lookup"><span data-stu-id="cd3a9-793">SloDWGroupC05</span></span> |<span data-ttu-id="cd3a9-794">32</span><span class="sxs-lookup"><span data-stu-id="cd3a9-794">32</span></span> |<span data-ttu-id="cd3a9-795">3.200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-795">3,200</span></span> |<span data-ttu-id="cd3a9-796">Alto</span><span class="sxs-lookup"><span data-stu-id="cd3a9-796">High</span></span> |
| <span data-ttu-id="cd3a9-797">SloDWGroupC06</span><span class="sxs-lookup"><span data-stu-id="cd3a9-797">SloDWGroupC06</span></span> |<span data-ttu-id="cd3a9-798">64</span><span class="sxs-lookup"><span data-stu-id="cd3a9-798">64</span></span> |<span data-ttu-id="cd3a9-799">6.400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-799">6,400</span></span> |<span data-ttu-id="cd3a9-800">Alto</span><span class="sxs-lookup"><span data-stu-id="cd3a9-800">High</span></span> |
| <span data-ttu-id="cd3a9-801">SloDWGroupC07</span><span class="sxs-lookup"><span data-stu-id="cd3a9-801">SloDWGroupC07</span></span> |<span data-ttu-id="cd3a9-802">128</span><span class="sxs-lookup"><span data-stu-id="cd3a9-802">128</span></span> |<span data-ttu-id="cd3a9-803">12.800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-803">12,800</span></span> |<span data-ttu-id="cd3a9-804">Alto</span><span class="sxs-lookup"><span data-stu-id="cd3a9-804">High</span></span> |

<span data-ttu-id="cd3a9-805">Desde el gráfico **Asignación y consumo de espacios de simultaneidad** , es posible ver que un DW500 usa 1, 4, 8 o 16 espacios de simultaneidad para smallrc, mediumrc, largerc y xlargerc, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-805">From the **Allocation and consumption of concurrency slots** chart, you can see that a DW500 uses 1, 4, 8 or 16 concurrency slots for smallrc, mediumrc, largerc, and xlargerc, respectively.</span></span> <span data-ttu-id="cd3a9-806">Puede buscar estos valores en el gráfico anterior para encontrar la importancia de cada clase de recursos.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-806">You can look those values up in the preceding chart to find the importance for each resource class.</span></span>

### <a name="dw500-mapping-of-resource-classes-to-importance"></a><span data-ttu-id="cd3a9-807">Asignación de DW500 de las clases de recursos a importancia</span><span class="sxs-lookup"><span data-stu-id="cd3a9-807">DW500 mapping of resource classes to importance</span></span>
| <span data-ttu-id="cd3a9-808">clase de recursos</span><span class="sxs-lookup"><span data-stu-id="cd3a9-808">Resource class</span></span> | <span data-ttu-id="cd3a9-809">Grupo de cargas de trabajo</span><span class="sxs-lookup"><span data-stu-id="cd3a9-809">Workload group</span></span> | <span data-ttu-id="cd3a9-810">Espacios de simultaneidad usados</span><span class="sxs-lookup"><span data-stu-id="cd3a9-810">Concurrency slots used</span></span> | <span data-ttu-id="cd3a9-811">MB/Distribución</span><span class="sxs-lookup"><span data-stu-id="cd3a9-811">MB / Distribution</span></span> | <span data-ttu-id="cd3a9-812">importancia</span><span class="sxs-lookup"><span data-stu-id="cd3a9-812">Importance</span></span> |
|:--- |:--- |:---:|:---:|:--- |
| <span data-ttu-id="cd3a9-813">smallrc</span><span class="sxs-lookup"><span data-stu-id="cd3a9-813">smallrc</span></span> |<span data-ttu-id="cd3a9-814">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="cd3a9-814">SloDWGroupC00</span></span> |<span data-ttu-id="cd3a9-815">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-815">1</span></span> |<span data-ttu-id="cd3a9-816">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-816">100</span></span> |<span data-ttu-id="cd3a9-817">Mediano</span><span class="sxs-lookup"><span data-stu-id="cd3a9-817">Medium</span></span> |
| <span data-ttu-id="cd3a9-818">mediumrc</span><span class="sxs-lookup"><span data-stu-id="cd3a9-818">mediumrc</span></span> |<span data-ttu-id="cd3a9-819">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="cd3a9-819">SloDWGroupC02</span></span> |<span data-ttu-id="cd3a9-820">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-820">4</span></span> |<span data-ttu-id="cd3a9-821">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-821">400</span></span> |<span data-ttu-id="cd3a9-822">Mediano</span><span class="sxs-lookup"><span data-stu-id="cd3a9-822">Medium</span></span> |
| <span data-ttu-id="cd3a9-823">largerc</span><span class="sxs-lookup"><span data-stu-id="cd3a9-823">largerc</span></span> |<span data-ttu-id="cd3a9-824">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="cd3a9-824">SloDWGroupC03</span></span> |<span data-ttu-id="cd3a9-825">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-825">8</span></span> |<span data-ttu-id="cd3a9-826">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-826">800</span></span> |<span data-ttu-id="cd3a9-827">Mediano</span><span class="sxs-lookup"><span data-stu-id="cd3a9-827">Medium</span></span> |
| <span data-ttu-id="cd3a9-828">xlargerc</span><span class="sxs-lookup"><span data-stu-id="cd3a9-828">xlargerc</span></span> |<span data-ttu-id="cd3a9-829">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="cd3a9-829">SloDWGroupC04</span></span> |<span data-ttu-id="cd3a9-830">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-830">16</span></span> |<span data-ttu-id="cd3a9-831">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-831">1,600</span></span> |<span data-ttu-id="cd3a9-832">Alto</span><span class="sxs-lookup"><span data-stu-id="cd3a9-832">High</span></span> |
| <span data-ttu-id="cd3a9-833">staticrc10</span><span class="sxs-lookup"><span data-stu-id="cd3a9-833">staticrc10</span></span> |<span data-ttu-id="cd3a9-834">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="cd3a9-834">SloDWGroupC00</span></span> |<span data-ttu-id="cd3a9-835">1</span><span class="sxs-lookup"><span data-stu-id="cd3a9-835">1</span></span> |<span data-ttu-id="cd3a9-836">100</span><span class="sxs-lookup"><span data-stu-id="cd3a9-836">100</span></span> |<span data-ttu-id="cd3a9-837">Mediano</span><span class="sxs-lookup"><span data-stu-id="cd3a9-837">Medium</span></span> |
| <span data-ttu-id="cd3a9-838">staticrc20</span><span class="sxs-lookup"><span data-stu-id="cd3a9-838">staticrc20</span></span> |<span data-ttu-id="cd3a9-839">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="cd3a9-839">SloDWGroupC01</span></span> |<span data-ttu-id="cd3a9-840">2</span><span class="sxs-lookup"><span data-stu-id="cd3a9-840">2</span></span> |<span data-ttu-id="cd3a9-841">200</span><span class="sxs-lookup"><span data-stu-id="cd3a9-841">200</span></span> |<span data-ttu-id="cd3a9-842">Mediano</span><span class="sxs-lookup"><span data-stu-id="cd3a9-842">Medium</span></span> |
| <span data-ttu-id="cd3a9-843">staticrc30</span><span class="sxs-lookup"><span data-stu-id="cd3a9-843">staticrc30</span></span> |<span data-ttu-id="cd3a9-844">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="cd3a9-844">SloDWGroupC02</span></span> |<span data-ttu-id="cd3a9-845">4</span><span class="sxs-lookup"><span data-stu-id="cd3a9-845">4</span></span> |<span data-ttu-id="cd3a9-846">400</span><span class="sxs-lookup"><span data-stu-id="cd3a9-846">400</span></span> |<span data-ttu-id="cd3a9-847">Mediano</span><span class="sxs-lookup"><span data-stu-id="cd3a9-847">Medium</span></span> |
| <span data-ttu-id="cd3a9-848">staticrc40</span><span class="sxs-lookup"><span data-stu-id="cd3a9-848">staticrc40</span></span> |<span data-ttu-id="cd3a9-849">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="cd3a9-849">SloDWGroupC03</span></span> |<span data-ttu-id="cd3a9-850">8</span><span class="sxs-lookup"><span data-stu-id="cd3a9-850">8</span></span> |<span data-ttu-id="cd3a9-851">800</span><span class="sxs-lookup"><span data-stu-id="cd3a9-851">800</span></span> |<span data-ttu-id="cd3a9-852">Mediano</span><span class="sxs-lookup"><span data-stu-id="cd3a9-852">Medium</span></span> |
| <span data-ttu-id="cd3a9-853">staticrc50</span><span class="sxs-lookup"><span data-stu-id="cd3a9-853">staticrc50</span></span> |<span data-ttu-id="cd3a9-854">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="cd3a9-854">SloDWGroupC03</span></span> |<span data-ttu-id="cd3a9-855">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-855">16</span></span> |<span data-ttu-id="cd3a9-856">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-856">1,600</span></span> |<span data-ttu-id="cd3a9-857">Alto</span><span class="sxs-lookup"><span data-stu-id="cd3a9-857">High</span></span> |
| <span data-ttu-id="cd3a9-858">staticrc60</span><span class="sxs-lookup"><span data-stu-id="cd3a9-858">staticrc60</span></span> |<span data-ttu-id="cd3a9-859">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="cd3a9-859">SloDWGroupC03</span></span> |<span data-ttu-id="cd3a9-860">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-860">16</span></span> |<span data-ttu-id="cd3a9-861">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-861">1,600</span></span> |<span data-ttu-id="cd3a9-862">Alto</span><span class="sxs-lookup"><span data-stu-id="cd3a9-862">High</span></span> |
| <span data-ttu-id="cd3a9-863">staticrc70</span><span class="sxs-lookup"><span data-stu-id="cd3a9-863">staticrc70</span></span> |<span data-ttu-id="cd3a9-864">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="cd3a9-864">SloDWGroupC03</span></span> |<span data-ttu-id="cd3a9-865">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-865">16</span></span> |<span data-ttu-id="cd3a9-866">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-866">1,600</span></span> |<span data-ttu-id="cd3a9-867">Alto</span><span class="sxs-lookup"><span data-stu-id="cd3a9-867">High</span></span> |
| <span data-ttu-id="cd3a9-868">staticrc80</span><span class="sxs-lookup"><span data-stu-id="cd3a9-868">staticrc80</span></span> |<span data-ttu-id="cd3a9-869">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="cd3a9-869">SloDWGroupC03</span></span> |<span data-ttu-id="cd3a9-870">16</span><span class="sxs-lookup"><span data-stu-id="cd3a9-870">16</span></span> |<span data-ttu-id="cd3a9-871">1600</span><span class="sxs-lookup"><span data-stu-id="cd3a9-871">1,600</span></span> |<span data-ttu-id="cd3a9-872">Alto</span><span class="sxs-lookup"><span data-stu-id="cd3a9-872">High</span></span> |

<span data-ttu-id="cd3a9-873">Puede usar la siguiente consulta DMV para ver las diferencias en la asignación de recursos de memoria en detalle desde la perspectiva del regulador de recursos, o bien para analizar el uso activo e histórico de los grupos de cargas de trabajo en el momento de solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-873">You can use the following DMV query to look at the differences in memory resource allocation in detail from the perspective of the resource governor, or to analyze active and historic usage of the workload groups when troubleshooting.</span></span>

```sql
WITH rg
AS
(   SELECT  
     pn.name                        AS node_name
    ,pn.[type]                        AS node_type
    ,pn.pdw_node_id                    AS node_id
    ,rp.name                        AS pool_name
    ,rp.max_memory_kb*1.0/1024                AS pool_max_mem_MB
    ,wg.name                        AS group_name
    ,wg.importance                    AS group_importance
    ,wg.request_max_memory_grant_percent        AS group_request_max_memory_grant_pcnt
    ,wg.max_dop                        AS group_max_dop
    ,wg.effective_max_dop                AS group_effective_max_dop
    ,wg.total_request_count                AS group_total_request_count
    ,wg.total_queued_request_count            AS group_total_queued_request_count
    ,wg.active_request_count                AS group_active_request_count
    ,wg.queued_request_count                AS group_queued_request_count
    FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
    JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    
            ON  wg.pdw_node_id  = rp.pdw_node_id
            AND wg.pool_id      = rp.pool_id
    JOIN    sys.dm_pdw_nodes pn
            ON    wg.pdw_node_id    = pn.pdw_node_id
    WHERE   wg.name like 'SloDWGroup%'
        AND     rp.name = 'SloDWPool'
)
SELECT    pool_name
,        pool_max_mem_MB
,        group_name
,        group_importance
,        (pool_max_mem_MB/100)*group_request_max_memory_grant_pcnt AS max_memory_grant_MB
,        node_name
,        node_type
,       group_total_request_count
,       group_total_queued_request_count
,       group_active_request_count
,       group_queued_request_count
FROM    rg
ORDER BY
    node_name
,    group_request_max_memory_grant_pcnt
,    group_importance
;
```

## <a name="queries-that-honor-concurrency-limits"></a><span data-ttu-id="cd3a9-874">Consultas que respetan los límites de simultaneidad</span><span class="sxs-lookup"><span data-stu-id="cd3a9-874">Queries that honor concurrency limits</span></span>
<span data-ttu-id="cd3a9-875">La mayoría de las consultas se rigen por las clases de recursos.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-875">Most queries are governed by resource classes.</span></span> <span data-ttu-id="cd3a9-876">Estas consultas deben encontrarse dentro de los umbrales de ranuras de simultaneidad y consultas simultáneas.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-876">These queries must fit inside both the concurrent query and concurrency slot thresholds.</span></span> <span data-ttu-id="cd3a9-877">Un usuario no puede elegir excluir una consulta del modelo de espacio de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-877">A user cannot choose to exclude a query from the concurrency slot model.</span></span>

<span data-ttu-id="cd3a9-878">Nuevamente, las siguientes instrucciones respetan las clases de recursos:</span><span class="sxs-lookup"><span data-stu-id="cd3a9-878">To reiterate, the following statements honor resource classes:</span></span>

* <span data-ttu-id="cd3a9-879">INSERT-SELECT</span><span class="sxs-lookup"><span data-stu-id="cd3a9-879">INSERT-SELECT</span></span>
* <span data-ttu-id="cd3a9-880">UPDATE</span><span class="sxs-lookup"><span data-stu-id="cd3a9-880">UPDATE</span></span>
* <span data-ttu-id="cd3a9-881">DELETE</span><span class="sxs-lookup"><span data-stu-id="cd3a9-881">DELETE</span></span>
* <span data-ttu-id="cd3a9-882">SELECT (al consultar las tablas de usuario)</span><span class="sxs-lookup"><span data-stu-id="cd3a9-882">SELECT (when querying user tables)</span></span>
* <span data-ttu-id="cd3a9-883">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="cd3a9-883">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="cd3a9-884">ALTER INDEX REORGANIZE</span><span class="sxs-lookup"><span data-stu-id="cd3a9-884">ALTER INDEX REORGANIZE</span></span>
* <span data-ttu-id="cd3a9-885">ALTER TABLE REBUILD</span><span class="sxs-lookup"><span data-stu-id="cd3a9-885">ALTER TABLE REBUILD</span></span>
* <span data-ttu-id="cd3a9-886">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="cd3a9-886">CREATE INDEX</span></span>
* <span data-ttu-id="cd3a9-887">CREATE CLUSTERED COLUMNSTORE INDEX</span><span class="sxs-lookup"><span data-stu-id="cd3a9-887">CREATE CLUSTERED COLUMNSTORE INDEX</span></span>
* <span data-ttu-id="cd3a9-888">CREATE TABLE AS SELECT (CTAS)</span><span class="sxs-lookup"><span data-stu-id="cd3a9-888">CREATE TABLE AS SELECT (CTAS)</span></span>
* <span data-ttu-id="cd3a9-889">Carga de datos</span><span class="sxs-lookup"><span data-stu-id="cd3a9-889">Data loading</span></span>
* <span data-ttu-id="cd3a9-890">Operaciones de movimiento de datos llevadas a cabo por el servicio de movimiento de datos (DMS)</span><span class="sxs-lookup"><span data-stu-id="cd3a9-890">Data movement operations conducted by the Data Movement Service (DMS)</span></span>

## <a name="query-exceptions-to-concurrency-limits"></a><span data-ttu-id="cd3a9-891">Excepciones de la consulta a los límites de simultaneidad</span><span class="sxs-lookup"><span data-stu-id="cd3a9-891">Query exceptions to concurrency limits</span></span>
<span data-ttu-id="cd3a9-892">Algunas consultas no respetan la clase de recursos a la que está asignado el usuario.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-892">Some queries do not honor the resource class to which the user is assigned.</span></span> <span data-ttu-id="cd3a9-893">Estas excepciones a los límites de simultaneidad se realizan cuando los recursos de memoria necesarios para un determinado comando son bajos, a menudo porque el comando es una operación de metadatos.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-893">These exceptions to the concurrency limits are made when the memory resources needed for a particular command are low, often because the command is a metadata operation.</span></span> <span data-ttu-id="cd3a9-894">El objetivo de estas excepciones es evitar asignaciones mayores de memoria a las consultas que nunca las necesitarán.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-894">The goal of these exceptions is to avoid larger memory allocations for queries that will never need them.</span></span> <span data-ttu-id="cd3a9-895">En estos casos, siempre se usa la clase de recursos predeterminada pequeña (smallrc) con independencia de la clase de recursos real asignada al usuario.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-895">In these cases, the default small resource class (smallrc) is always used regardless of the actual resource class assigned to the user.</span></span> <span data-ttu-id="cd3a9-896">Por ejemplo, `CREATE LOGIN` se ejecutará siempre en la clase smallrc.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-896">For example, `CREATE LOGIN` will always run in smallrc.</span></span> <span data-ttu-id="cd3a9-897">Los recursos necesarios para llevar a cabo esta operación son muy bajos, por lo que no tiene sentido incluir la consulta en el modelo de espacio de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-897">The resources required to fulfill this operation are very low, so it does not make sense to include the query in the concurrency slot model.</span></span>  <span data-ttu-id="cd3a9-898">Estas consultas tampoco están limitadas por el límite de simultaneidad de 32 usuarios; sino que puede ejecutar un número ilimitado de estas consultas hasta llegar al límite de 1024 sesiones.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-898">These queries are also not limited by the 32 user concurrency limit, an unlimited number of these queries can run up to the session limit of 1,024 sessions.</span></span>

<span data-ttu-id="cd3a9-899">Las instrucciones siguientes no respetan las clases de recursos:</span><span class="sxs-lookup"><span data-stu-id="cd3a9-899">The following statements do not honor resource classes:</span></span>

* <span data-ttu-id="cd3a9-900">CREATE o DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="cd3a9-900">CREATE or DROP TABLE</span></span>
* <span data-ttu-id="cd3a9-901">ALTER TABLE ... SWITCH, SPLIT o MERGE PARTITION</span><span class="sxs-lookup"><span data-stu-id="cd3a9-901">ALTER TABLE ... SWITCH, SPLIT, or MERGE PARTITION</span></span>
* <span data-ttu-id="cd3a9-902">ALTER INDEX DISABLE</span><span class="sxs-lookup"><span data-stu-id="cd3a9-902">ALTER INDEX DISABLE</span></span>
* <span data-ttu-id="cd3a9-903">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="cd3a9-903">DROP INDEX</span></span>
* <span data-ttu-id="cd3a9-904">CREATE, UPDATE o DROP STATISTICS</span><span class="sxs-lookup"><span data-stu-id="cd3a9-904">CREATE, UPDATE, or DROP STATISTICS</span></span>
* <span data-ttu-id="cd3a9-905">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="cd3a9-905">TRUNCATE TABLE</span></span>
* <span data-ttu-id="cd3a9-906">ALTER AUTHORIZATION</span><span class="sxs-lookup"><span data-stu-id="cd3a9-906">ALTER AUTHORIZATION</span></span>
* <span data-ttu-id="cd3a9-907">CREATE LOGIN</span><span class="sxs-lookup"><span data-stu-id="cd3a9-907">CREATE LOGIN</span></span>
* <span data-ttu-id="cd3a9-908">CREATE, ALTER o DROP USER</span><span class="sxs-lookup"><span data-stu-id="cd3a9-908">CREATE, ALTER or DROP USER</span></span>
* <span data-ttu-id="cd3a9-909">CREATE, ALTER o DROP PROCEDURE</span><span class="sxs-lookup"><span data-stu-id="cd3a9-909">CREATE, ALTER or DROP PROCEDURE</span></span>
* <span data-ttu-id="cd3a9-910">CREATE o DROP VIEW</span><span class="sxs-lookup"><span data-stu-id="cd3a9-910">CREATE or DROP VIEW</span></span>
* <span data-ttu-id="cd3a9-911">INSERT VALUES</span><span class="sxs-lookup"><span data-stu-id="cd3a9-911">INSERT VALUES</span></span>
* <span data-ttu-id="cd3a9-912">SELECT (desde vistas del sistema y DMV)</span><span class="sxs-lookup"><span data-stu-id="cd3a9-912">SELECT from system views and DMVs</span></span>
* <span data-ttu-id="cd3a9-913">EXPLAIN</span><span class="sxs-lookup"><span data-stu-id="cd3a9-913">EXPLAIN</span></span>
* <span data-ttu-id="cd3a9-914">DBCC</span><span class="sxs-lookup"><span data-stu-id="cd3a9-914">DBCC</span></span>

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <span data-ttu-id="cd3a9-915"><a name="changing-user-resource-class-example"></a> Ejemplo de cambio de una clase de recursos de usuario</span><span class="sxs-lookup"><span data-stu-id="cd3a9-915"><a name="changing-user-resource-class-example"></a> Change a user resource class example</span></span>
1. <span data-ttu-id="cd3a9-916">**Cree un inicio de sesión:** abra una conexión con la base de datos **maestra** en el servidor SQL Server que hospeda la base de datos de SQL Data Warehouse y ejecute los comandos siguientes.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-916">**Create login:** Open a connection to your **master** database on the SQL server hosting your SQL Data Warehouse database and execute the following commands.</span></span>
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > <span data-ttu-id="cd3a9-917">Es una buena idea crear un usuario en la base de datos maestra para los usuarios de Almacenamiento de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-917">It is a good idea to create a user in the master database for Azure SQL Data Warehouse users.</span></span> <span data-ttu-id="cd3a9-918">La creación de un usuario en la base de datos maestra posibilita el inicio de sesión mediante herramientas como SSMS sin especificar un nombre de base de datos.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-918">Creating a user in master allows a user to login using tools like SSMS without specifying a database name.</span></span>  <span data-ttu-id="cd3a9-919">También permite el uso del Explorador de objetos para ver todas las bases de datos en un servidor SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-919">It also allows them to use the object explorer to view all databases on a SQL server.</span></span>  <span data-ttu-id="cd3a9-920">Para obtener más información sobre cómo crear y administrar usuarios, consulte [Proteger una base de datos en SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="cd3a9-920">For more details about creating and managing users, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>
   > 
   > 
2. <span data-ttu-id="cd3a9-921">**Cree un usuario de SQL Data Warehouse**: abra una conexión con la base de datos de **SQL Data Warehouse** y ejecute el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-921">**Create SQL Data Warehouse user:** Open a connection to the **SQL Data Warehouse** database and execute the following command.</span></span>
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. <span data-ttu-id="cd3a9-922">**Conceder permisos:** el siguiente ejemplo se concede `CONTROL` en la base de datos de **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-922">**Grant permissions:** The following example grants `CONTROL` on the **SQL Data Warehouse** database.</span></span> <span data-ttu-id="cd3a9-923">`CONTROL` en la base de datos de nivel es el equivalente de db_owner en SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-923">`CONTROL` at the database level is the equivalent of db_owner in SQL Server.</span></span>
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW to newperson;
    ```
4. <span data-ttu-id="cd3a9-924">**Aumente la clase de recursos:** use la consulta siguiente para agregar un usuario a un rol de administración de cargas de trabajo con privilegios más altos.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-924">**Increase resource class:** Use the following query to add a user to a higher workload management role.</span></span>
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. <span data-ttu-id="cd3a9-925">**Disminuya la clase de recursos:** use la consulta siguiente para eliminar un usuario de un rol de administración de cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-925">**Decrease resource class:** Use the following query to remove a user from a workload management role.</span></span>
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="cd3a9-926">No se puede quitar un usuario de smallrc.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-926">It is not possible to remove a user from smallrc.</span></span>
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a><span data-ttu-id="cd3a9-927">Detección de consulta en cola y otras DMV</span><span class="sxs-lookup"><span data-stu-id="cd3a9-927">Queued query detection and other DMVs</span></span>
<span data-ttu-id="cd3a9-928">Puede usar la DMV `sys.dm_pdw_exec_requests` para identificar las consultas que están a la espera en una cola de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-928">You can use the `sys.dm_pdw_exec_requests` DMV to identify queries that are waiting in a concurrency queue.</span></span> <span data-ttu-id="cd3a9-929">Las consultas que esperan un espacio de simultaneidad tendrán el estado de **suspendido**.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-929">Queries waiting for a concurrency slot will have a status of **suspended**.</span></span>

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

<span data-ttu-id="cd3a9-930">Los roles de administración de cargas de trabajo se pueden ver con `sys.database_principals`.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-930">Workload management roles can be viewed with `sys.database_principals`.</span></span>

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

<span data-ttu-id="cd3a9-931">La consulta siguiente muestra qué rol tiene asignado cada usuario.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-931">The following query shows which role each user is assigned to.</span></span>

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

<span data-ttu-id="cd3a9-932">Almacenamiento de datos SQL tiene los siguientes tipos de espera:</span><span class="sxs-lookup"><span data-stu-id="cd3a9-932">SQL Data Warehouse has the following wait types:</span></span>

* <span data-ttu-id="cd3a9-933">**LocalQueriesConcurrencyResourceType**: se refiere a las consultas que residen fuera del marco del espacio de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-933">**LocalQueriesConcurrencyResourceType**: Queries that sit outside of the concurrency slot framework.</span></span> <span data-ttu-id="cd3a9-934">Las funciones del sistema y las consultas DMV como `SELECT @@VERSION` son ejemplos de consultas locales.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-934">DMV queries and system functions such as `SELECT @@VERSION` are examples of local queries.</span></span>
* <span data-ttu-id="cd3a9-935">**UserConcurrencyResourceType**: se refiere a las consultas que residen dentro del marco del espacio de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-935">**UserConcurrencyResourceType**: Queries that sit inside the concurrency slot framework.</span></span> <span data-ttu-id="cd3a9-936">Las consultas en tablas de usuario final representan ejemplos que usarían este tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-936">Queries against end-user tables represent examples that would use this resource type.</span></span>
* <span data-ttu-id="cd3a9-937">**DmsConcurrencyResourceType**: se refiere a las esperas que son el resultado de operaciones de movimiento de datos.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-937">**DmsConcurrencyResourceType**: Waits resulting from data movement operations.</span></span>
* <span data-ttu-id="cd3a9-938">**BackupConcurrencyResourceType**: se refiere a una espera que indica que se está creando la copia de seguridad de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-938">**BackupConcurrencyResourceType**: This wait indicates that a database is being backed up.</span></span> <span data-ttu-id="cd3a9-939">El valor máximo para este tipo de recurso es 1.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-939">The maximum value for this resource type is 1.</span></span> <span data-ttu-id="cd3a9-940">Si varias copias de seguridad se solicitaron al mismo tiempo, las demás se pondrán en la cola.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-940">If multiple backups have been requested at the same time, the others will queue.</span></span>

<span data-ttu-id="cd3a9-941">La DMV `sys.dm_pdw_waits` puede utilizarse para ver por qué recursos está esperando una solicitud.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-941">The `sys.dm_pdw_waits` DMV can be used to see which resources a request is waiting for.</span></span>

```sql
SELECT  w.[wait_id]
,       w.[session_id]
,       w.[type]            AS Wait_type
,       w.[object_type]
,       w.[object_name]
,       w.[request_id]
,       w.[request_time]
,       w.[acquire_time]
,       w.[state]
,       w.[priority]
,    SESSION_ID()            AS Current_session
,    s.[status]            AS Session_status
,    s.[login_name]
,    s.[query_count]
,    s.[client_id]
,    s.[sql_spid]
,    r.[command]            AS Request_command
,    r.[label]
,    r.[status]            AS Request_status
,    r.[submit_time]
,    r.[start_time]
,    r.[end_compile_time]
,    r.[end_time]
,    DATEDIFF(ms,r.[submit_time],r.[start_time])        AS Request_queue_time_ms
,    DATEDIFF(ms,r.[start_time],r.[end_compile_time])    AS Request_compile_time_ms
,    DATEDIFF(ms,r.[end_compile_time],r.[end_time])        AS Request_execution_time_ms
,    r.[total_elapsed_time]
FROM    sys.dm_pdw_waits w
JOIN    sys.dm_pdw_exec_sessions s  ON w.[session_id] = s.[session_id]
JOIN    sys.dm_pdw_exec_requests r  ON w.[request_id] = r.[request_id]
WHERE    w.[session_id] <> SESSION_ID();
```

<span data-ttu-id="cd3a9-942">La DMV `sys.dm_pdw_resource_waits` muestra solo las esperas de recursos consumidas por una consulta determinada.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-942">The `sys.dm_pdw_resource_waits` DMV shows only the resource waits consumed by a given query.</span></span> <span data-ttu-id="cd3a9-943">El tiempo de espera del recurso solo mide el tiempo que se espera a que se proporcionen los recursos, por oposición al tiempo de espera de la señal, que es el tiempo que tardan los servidores SQL Server subyacentes en programar la consulta en la CPU.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-943">Resource wait time only measures the time waiting for resources to be provided, as opposed to signal wait time, which is the time it takes for the underlying SQL servers to schedule the query onto the CPU.</span></span>

```sql
SELECT  [session_id]
,       [type]
,       [object_type]
,       [object_name]
,       [request_id]
,       [request_time]
,       [acquire_time]
,       DATEDIFF(ms,[request_time],[acquire_time])  AS acquire_duration_ms
,       [concurrency_slots_used]                    AS concurrency_slots_reserved
,       [resource_class]
,       [wait_id]                                   AS queue_position
FROM    sys.dm_pdw_resource_waits
WHERE    [session_id] <> SESSION_ID();
```

<span data-ttu-id="cd3a9-944">La DMV `sys.dm_pdw_wait_stats` se puede utilizar para analizar las tendencias históricas de las esperas.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-944">The `sys.dm_pdw_wait_stats` DMV can be used for historic trend analysis of waits.</span></span>

```sql
SELECT    w.[pdw_node_id]
,        w.[wait_name]
,        w.[max_wait_time]
,        w.[request_count]
,        w.[signal_time]
,        w.[completed_count]
,        w.[wait_time]
FROM    sys.dm_pdw_wait_stats w;
```

## <a name="next-steps"></a><span data-ttu-id="cd3a9-945">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cd3a9-945">Next steps</span></span>
<span data-ttu-id="cd3a9-946">Para obtener más información sobre cómo administrar los usuarios y la seguridad de la base de datos, consulte [Proteger una base de datos en SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="cd3a9-946">For more information about managing database users and security, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span> <span data-ttu-id="cd3a9-947">Para más información sobre cómo las clases de recursos mayores pueden mejorar la calidad de los índices de almacén de columnas agrupado, consulte [Regeneración de índices para mejorar la calidad de los segmentos].</span><span class="sxs-lookup"><span data-stu-id="cd3a9-947">For more information about how larger resource classes can improve clustered columnstore index quality, see [Rebuilding indexes to improve segment quality].</span></span>

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Regeneración de índices para mejorar la calidad de los segmentos]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
