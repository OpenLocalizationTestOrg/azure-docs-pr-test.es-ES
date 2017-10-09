---
title: "administración de aaaConcurrency y carga de trabajo en el almacén de datos de SQL | Documentos de Microsoft"
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
ms.openlocfilehash: 7f7e77aa687760252aed16573b609817ed9111c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a><span data-ttu-id="d3e25-103">Simultaneidad y administración de cargas de trabajo en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="d3e25-103">Concurrency and workload management in SQL Data Warehouse</span></span>
<span data-ttu-id="d3e25-104">toodeliver un rendimiento predecible a escala, almacenamiento de datos de SQL de Microsoft Azure le ayuda a controlar los niveles de simultaneidad y las asignaciones de recursos como memoria y asignación de prioridades de CPU.</span><span class="sxs-lookup"><span data-stu-id="d3e25-104">toodeliver predictable performance at scale, Microsoft Azure SQL Data Warehouse helps you control concurrency levels and resource allocations like memory and CPU prioritization.</span></span> <span data-ttu-id="d3e25-105">Este artículo detallan toohello conceptos de administración de simultaneidad y la carga de trabajo, que explica cómo ambas características se han implementado y cómo se puede controlar en el almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="d3e25-105">This article introduces you toohello concepts of concurrency and workload management, explaining how both features have been implemented and how you can control them in your data warehouse.</span></span> <span data-ttu-id="d3e25-106">Administración de cargas de trabajo de almacenamiento de datos SQL es toohelp previsto admitir entornos de varios usuarios.</span><span class="sxs-lookup"><span data-stu-id="d3e25-106">SQL Data Warehouse workload management is intended toohelp you support multi-user environments.</span></span> <span data-ttu-id="d3e25-107">No está diseñada para cargas de trabajo de multiinquilino.</span><span class="sxs-lookup"><span data-stu-id="d3e25-107">It is not intended for multi-tenant workloads.</span></span>

## <a name="concurrency-limits"></a><span data-ttu-id="d3e25-108">Límites de simultaneidad</span><span class="sxs-lookup"><span data-stu-id="d3e25-108">Concurrency limits</span></span>
<span data-ttu-id="d3e25-109">Almacenamiento de datos SQL permite que un too1, 024 conexiones simultáneas.</span><span class="sxs-lookup"><span data-stu-id="d3e25-109">SQL Data Warehouse allows up too1,024 concurrent connections.</span></span> <span data-ttu-id="d3e25-110">Todas las 1.024 conexiones pueden enviar consultas al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="d3e25-110">All 1,024 connections can submit queries concurrently.</span></span> <span data-ttu-id="d3e25-111">Sin embargo, toooptimize rendimiento, almacenamiento de datos SQL puede poner en cola algunos tooensure de las consultas que cada consulta recibe una concesión de memoria mínima.</span><span class="sxs-lookup"><span data-stu-id="d3e25-111">However, toooptimize throughput, SQL Data Warehouse may queue some queries tooensure that each query receives a minimal memory grant.</span></span> <span data-ttu-id="d3e25-112">Durante el tiempo de ejecución de las consultas, estas se empiezan a poner en cola.</span><span class="sxs-lookup"><span data-stu-id="d3e25-112">Queuing occurs at query execution time.</span></span> <span data-ttu-id="d3e25-113">Las consultas de puesta en cola cuando puede aumentar la simultaneidad se alcanzan los límites, almacenamiento de datos SQL total rendimiento asegurándose de que las consultas activas obtienen acceso toocritically necesita recursos de memoria.</span><span class="sxs-lookup"><span data-stu-id="d3e25-113">By queuing queries when concurrency limits are reached, SQL Data Warehouse can increase total throughput by ensuring that active queries get access toocritically needed memory resources.</span></span>  

<span data-ttu-id="d3e25-114">Los límites de simultaneidad se rigen por dos conceptos: *consultas simultáneas* y *espacios de simultaneidad*.</span><span class="sxs-lookup"><span data-stu-id="d3e25-114">Concurrency limits are governed by two concepts: *concurrent queries* and *concurrency slots*.</span></span> <span data-ttu-id="d3e25-115">Para una consulta tooexecute, debe ejecutar dentro de límite de simultaneidad de consultas de Hola y asignación de ranura de simultaneidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3e25-115">For a query tooexecute, it must execute within both hello query concurrency limit and hello concurrency slot allocation.</span></span>

* <span data-ttu-id="d3e25-116">Consultas simultáneas son consultas de hello ejecutar en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="d3e25-116">Concurrent queries are hello queries executing at hello same time.</span></span> <span data-ttu-id="d3e25-117">Almacenamiento de datos SQL admite hasta too32 consultas simultáneas en hello DWU más grandes.</span><span class="sxs-lookup"><span data-stu-id="d3e25-117">SQL Data Warehouse supports up too32 concurrent queries on hello larger DWU sizes.</span></span>
* <span data-ttu-id="d3e25-118">Los espacios de simultaneidad se asignan según DWU.</span><span class="sxs-lookup"><span data-stu-id="d3e25-118">Concurrency slots are allocated based on DWU.</span></span> <span data-ttu-id="d3e25-119">Cada 100 DWU proporciona 4 espacios de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="d3e25-119">Each 100 DWU provides 4 concurrency slots.</span></span> <span data-ttu-id="d3e25-120">Por ejemplo, un DW100 asigna 4 espacios de simultaneidad y DW1000 asigna 40.</span><span class="sxs-lookup"><span data-stu-id="d3e25-120">For example, a DW100 allocates 4 concurrency slots and DW1000 allocates 40.</span></span> <span data-ttu-id="d3e25-121">Cada consulta consume uno o más simultaneidad ranuras, depende de hello [clase de recursos](#resource-classes) de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3e25-121">Each query consumes one or more concurrency slots, dependent on hello [resource class](#resource-classes) of hello query.</span></span> <span data-ttu-id="d3e25-122">Las consultas se ejecutan en la clase de recurso de hello smallrc consuman una ranura de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="d3e25-122">Queries running in hello smallrc resource class consume one concurrency slot.</span></span> <span data-ttu-id="d3e25-123">Las consultas que se ejecutan en una clase de recurso superior consumen más intervalos de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="d3e25-123">Queries running in a higher resource class consume more concurrency slots.</span></span>

<span data-ttu-id="d3e25-124">Hello tabla siguiente describen los límites de Hola para consultas simultáneas y ranuras de simultaneidad en hello diversos tamaños de unidad.</span><span class="sxs-lookup"><span data-stu-id="d3e25-124">hello following table describes hello limits for both concurrent queries and concurrency slots at hello various DWU sizes.</span></span>

### <a name="concurrency-limits"></a><span data-ttu-id="d3e25-125">Límites de simultaneidad</span><span class="sxs-lookup"><span data-stu-id="d3e25-125">Concurrency limits</span></span>
| <span data-ttu-id="d3e25-126">DWU</span><span class="sxs-lookup"><span data-stu-id="d3e25-126">DWU</span></span> | <span data-ttu-id="d3e25-127">N.º máximo de consultas simultáneas</span><span class="sxs-lookup"><span data-stu-id="d3e25-127">Max concurrent queries</span></span> | <span data-ttu-id="d3e25-128">Espacios de simultaneidad asignados</span><span class="sxs-lookup"><span data-stu-id="d3e25-128">Concurrency slots allocated</span></span> |
|:--- |:---:|:---:|
| <span data-ttu-id="d3e25-129">DW100</span><span class="sxs-lookup"><span data-stu-id="d3e25-129">DW100</span></span> |<span data-ttu-id="d3e25-130">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-130">4</span></span> |<span data-ttu-id="d3e25-131">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-131">4</span></span> |
| <span data-ttu-id="d3e25-132">DW200</span><span class="sxs-lookup"><span data-stu-id="d3e25-132">DW200</span></span> |<span data-ttu-id="d3e25-133">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-133">8</span></span> |<span data-ttu-id="d3e25-134">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-134">8</span></span> |
| <span data-ttu-id="d3e25-135">DW300</span><span class="sxs-lookup"><span data-stu-id="d3e25-135">DW300</span></span> |<span data-ttu-id="d3e25-136">12</span><span class="sxs-lookup"><span data-stu-id="d3e25-136">12</span></span> |<span data-ttu-id="d3e25-137">12</span><span class="sxs-lookup"><span data-stu-id="d3e25-137">12</span></span> |
| <span data-ttu-id="d3e25-138">DW400</span><span class="sxs-lookup"><span data-stu-id="d3e25-138">DW400</span></span> |<span data-ttu-id="d3e25-139">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-139">16</span></span> |<span data-ttu-id="d3e25-140">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-140">16</span></span> |
| <span data-ttu-id="d3e25-141">DW500</span><span class="sxs-lookup"><span data-stu-id="d3e25-141">DW500</span></span> |<span data-ttu-id="d3e25-142">20 |</span><span class="sxs-lookup"><span data-stu-id="d3e25-142">20</span></span> |<span data-ttu-id="d3e25-143">20 |</span><span class="sxs-lookup"><span data-stu-id="d3e25-143">20</span></span> |
| <span data-ttu-id="d3e25-144">DW600</span><span class="sxs-lookup"><span data-stu-id="d3e25-144">DW600</span></span> |<span data-ttu-id="d3e25-145">24</span><span class="sxs-lookup"><span data-stu-id="d3e25-145">24</span></span> |<span data-ttu-id="d3e25-146">24</span><span class="sxs-lookup"><span data-stu-id="d3e25-146">24</span></span> |
| <span data-ttu-id="d3e25-147">DW1000</span><span class="sxs-lookup"><span data-stu-id="d3e25-147">DW1000</span></span> |<span data-ttu-id="d3e25-148">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-148">32</span></span> |<span data-ttu-id="d3e25-149">40</span><span class="sxs-lookup"><span data-stu-id="d3e25-149">40</span></span> |
| <span data-ttu-id="d3e25-150">DW1200</span><span class="sxs-lookup"><span data-stu-id="d3e25-150">DW1200</span></span> |<span data-ttu-id="d3e25-151">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-151">32</span></span> |<span data-ttu-id="d3e25-152">48</span><span class="sxs-lookup"><span data-stu-id="d3e25-152">48</span></span> |
| <span data-ttu-id="d3e25-153">DW1500</span><span class="sxs-lookup"><span data-stu-id="d3e25-153">DW1500</span></span> |<span data-ttu-id="d3e25-154">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-154">32</span></span> |<span data-ttu-id="d3e25-155">60</span><span class="sxs-lookup"><span data-stu-id="d3e25-155">60</span></span> |
| <span data-ttu-id="d3e25-156">DW2000</span><span class="sxs-lookup"><span data-stu-id="d3e25-156">DW2000</span></span> |<span data-ttu-id="d3e25-157">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-157">32</span></span> |<span data-ttu-id="d3e25-158">80</span><span class="sxs-lookup"><span data-stu-id="d3e25-158">80</span></span> |
| <span data-ttu-id="d3e25-159">DW3000</span><span class="sxs-lookup"><span data-stu-id="d3e25-159">DW3000</span></span> |<span data-ttu-id="d3e25-160">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-160">32</span></span> |<span data-ttu-id="d3e25-161">120</span><span class="sxs-lookup"><span data-stu-id="d3e25-161">120</span></span> |
| <span data-ttu-id="d3e25-162">DW6000</span><span class="sxs-lookup"><span data-stu-id="d3e25-162">DW6000</span></span> |<span data-ttu-id="d3e25-163">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-163">32</span></span> |<span data-ttu-id="d3e25-164">240</span><span class="sxs-lookup"><span data-stu-id="d3e25-164">240</span></span> |

<span data-ttu-id="d3e25-165">Cuando se alcanza alguno de estos umbrales, se ponen a la cola nuevas consultas y se ejecutan según la regla "primero en entrar, primero en salir".</span><span class="sxs-lookup"><span data-stu-id="d3e25-165">When one of these thresholds is met, new queries are queued and executed on a first-in, first-out basis.</span></span>  <span data-ttu-id="d3e25-166">Cuando finaliza un consulta y número de Hola de consultas y ranuras cae por debajo de los límites de hello, se liberan las consultas en cola.</span><span class="sxs-lookup"><span data-stu-id="d3e25-166">As a queries finishes and hello number of queries and slots falls below hello limits, queued queries are released.</span></span> 

> [!NOTE]  
> <span data-ttu-id="d3e25-167">*Seleccione* las consultas que se ejecuta exclusivamente en vistas de administración dinámica (DMV) o vistas de catálogo no se rigen por cualquiera de los límites de simultaneidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3e25-167">*Select* queries executing exclusively on dynamic management views (DMVs) or catalog views are not governed by any of hello concurrency limits.</span></span> <span data-ttu-id="d3e25-168">Puede supervisar el sistema de hello independientemente del número de Hola de las consultas que se ejecuta en él.</span><span class="sxs-lookup"><span data-stu-id="d3e25-168">You can monitor hello system regardless of hello number of queries executing on it.</span></span>
> 
> 

## <a name="resource-classes"></a><span data-ttu-id="d3e25-169">Clases de recursos</span><span class="sxs-lookup"><span data-stu-id="d3e25-169">Resource classes</span></span>
<span data-ttu-id="d3e25-170">Clases de recursos ayudan a controlar la asignación de memoria y ciclos de CPU proporcionados tooa consulta.</span><span class="sxs-lookup"><span data-stu-id="d3e25-170">Resource classes help you control memory allocation and CPU cycles given tooa query.</span></span> <span data-ttu-id="d3e25-171">Puede asignar a dos tipos de usuario de tooa de clases de recursos con formato de Hola de roles de base de datos.</span><span class="sxs-lookup"><span data-stu-id="d3e25-171">You can assign two types of resource classes tooa user in hello form of database roles.</span></span> <span data-ttu-id="d3e25-172">Hola dos tipos de clases de recursos son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="d3e25-172">hello two types of resource classes are as follows:</span></span>
1. <span data-ttu-id="d3e25-173">Clases de recursos dinámicos (**smallrc, mediumrc, largerc, xlargerc**) asigne una cantidad de memoria en función hello variable DWU actual.</span><span class="sxs-lookup"><span data-stu-id="d3e25-173">Dynamic Resource Classes (**smallrc, mediumrc, largerc, xlargerc**) allocate a variable amount of memory depending on hello current DWU.</span></span> <span data-ttu-id="d3e25-174">Esto significa que al escalar una tooa DWU más grande, las consultas automáticamente obtengan más memoria.</span><span class="sxs-lookup"><span data-stu-id="d3e25-174">This means that when you scale up tooa larger DWU, your queries automatically get more memory.</span></span> 
2. <span data-ttu-id="d3e25-175">Las clases estáticas de recursos (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) asignar Hola misma cantidad de memoria con independencia de Hola DWU actual (siempre que Hola DWU propio no tiene suficiente memoria).</span><span class="sxs-lookup"><span data-stu-id="d3e25-175">Static Resource Classes (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) allocate hello same amount of memory regardless of hello current DWU (provided that hello DWU itself has enough memory).</span></span> <span data-ttu-id="d3e25-176">Esto significa que, con unidades mayores, puede ejecutar más consultas en cada clase de recursos al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="d3e25-176">This means that on larger DWUs, you can run more queries in each resource class concurrently.</span></span>

<span data-ttu-id="d3e25-177">A los usuarios con **smallrc** y **staticrc10** se les concede una cantidad de memoria menor y pueden aprovechar una mayor simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="d3e25-177">Users in **smallrc** and **staticrc10** are given a smaller amount of memory and can take advantage of higher concurrency.</span></span> <span data-ttu-id="d3e25-178">En cambio, los usuarios asignados demasiado**xlargerc** o **staticrc80** reciben grandes cantidades de memoria, y por lo tanto, menos las consultas pueden ejecutarse simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="d3e25-178">In contrast, users assigned too**xlargerc** or **staticrc80** are given large amounts of memory, and therefore fewer of their queries can run concurrently.</span></span>

<span data-ttu-id="d3e25-179">De manera predeterminada, cada usuario es un miembro de clase de recursos pequeño hello, **smallrc**.</span><span class="sxs-lookup"><span data-stu-id="d3e25-179">By default, each user is a member of hello small resource class, **smallrc**.</span></span> <span data-ttu-id="d3e25-180">Hola procedimiento `sp_addrolemember` es usa la clase de recurso tooincrease hello y `sp_droprolemember` es usa la clase de recurso de hello toodecrease.</span><span class="sxs-lookup"><span data-stu-id="d3e25-180">hello procedure `sp_addrolemember` is used tooincrease hello resource class, and `sp_droprolemember` is used toodecrease hello resource class.</span></span> <span data-ttu-id="d3e25-181">Por ejemplo, este comando podría aumentar la clase de recurso de hello de loaduser demasiado**largerc**:</span><span class="sxs-lookup"><span data-stu-id="d3e25-181">For example, this command would increase hello resource class of loaduser too**largerc**:</span></span>

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a><span data-ttu-id="d3e25-182">Consultas que no respetan las clases de recursos</span><span class="sxs-lookup"><span data-stu-id="d3e25-182">Queries that do not honor resource classes</span></span>

<span data-ttu-id="d3e25-183">Existen algunos tipos de consultas que no se benefician de una mayor asignación de memoria.</span><span class="sxs-lookup"><span data-stu-id="d3e25-183">There are a few types of queries that do not benefit from a larger memory allocation.</span></span> <span data-ttu-id="d3e25-184">sistema de Hello omite su asignación de recursos de clase y siempre ejecuta estas consultas en la clase de recursos pequeño hello en su lugar.</span><span class="sxs-lookup"><span data-stu-id="d3e25-184">hello system ignores their resource class allocation and always run these queries in hello small resource class instead.</span></span> <span data-ttu-id="d3e25-185">Si estas consultas se ejecutan siempre en la clase de recursos pequeño de hello, pueden ejecutarse cuando las ranuras de simultaneidad que están bajo presión y no consumen más ranuras de los necesarios.</span><span class="sxs-lookup"><span data-stu-id="d3e25-185">If these queries always run in hello small resource class, they can run when concurrency slots are under pressure and they won't consume more slots than needed.</span></span> <span data-ttu-id="d3e25-186">Consulte [Excepciones de clase de recursos](#query-exceptions-to-concurrency-limits) para más información.</span><span class="sxs-lookup"><span data-stu-id="d3e25-186">See [Resource class exceptions](#query-exceptions-to-concurrency-limits) for more information.</span></span>

## <a name="details-on-resource-class-assignment"></a><span data-ttu-id="d3e25-187">Detalles sobre la asignación de la clase de recursos</span><span class="sxs-lookup"><span data-stu-id="d3e25-187">Details on resource class assignment</span></span>


<span data-ttu-id="d3e25-188">Más detalles en la clase de recursos:</span><span class="sxs-lookup"><span data-stu-id="d3e25-188">A few more details on resource class:</span></span>

* <span data-ttu-id="d3e25-189">*Modificar rol* se requiere permiso de clase de recurso de hello toochange de un usuario.</span><span class="sxs-lookup"><span data-stu-id="d3e25-189">*Alter role* permission is required toochange hello resource class of a user.</span></span>
* <span data-ttu-id="d3e25-190">Aunque puede agregar un usuario tooone o más de las clases de recursos elevadas Hola, clases de recursos dinámicos tienen prioridad sobre las clases de recurso estático.</span><span class="sxs-lookup"><span data-stu-id="d3e25-190">Although you can add a user tooone or more of hello higher resource classes, dynamic resource classes take precedence over static resource classes.</span></span> <span data-ttu-id="d3e25-191">Es decir, si se asigna a un usuario tooboth **mediumrc**(dinámico) y **staticrc80**(estático), **mediumrc** es la clase de recurso de Hola que se respeta.</span><span class="sxs-lookup"><span data-stu-id="d3e25-191">That is, if a user is assigned tooboth **mediumrc**(dynamic) and **staticrc80**(static), **mediumrc** is hello resource class that is honored.</span></span>
 * <span data-ttu-id="d3e25-192">Cuando se asigna a un usuario toomore que la clase de un recurso en un tipo de clase de recurso específico (más de una clase de recurso dinámico o más de una clase de recurso estático), está asignada la clase de recurso más alto de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3e25-192">When a user is assigned toomore than one resource class in a specific resource class type (more than one dynamic resource class or more than one static resource class), hello highest resource class is honored.</span></span> <span data-ttu-id="d3e25-193">Es decir, si un usuario se le asigna largerc y tooboth mediumrc, se respeta la clase de recurso superior hello (largerc).</span><span class="sxs-lookup"><span data-stu-id="d3e25-193">That is, if a user is assigned tooboth mediumrc and largerc, hello higher resource class (largerc) is honored.</span></span> <span data-ttu-id="d3e25-194">Y si se asigna a un usuario tooboth **staticrc20** y **statirc80**, **staticrc80** se cumplirá.</span><span class="sxs-lookup"><span data-stu-id="d3e25-194">And if a user is assigned tooboth **staticrc20** and **statirc80**, **staticrc80** is honored.</span></span>
* <span data-ttu-id="d3e25-195">no se puede cambiar la clase de recurso de Hola Hola administrativos de usuario del sistema.</span><span class="sxs-lookup"><span data-stu-id="d3e25-195">hello resource class of hello system administrative user cannot be changed.</span></span>

<span data-ttu-id="d3e25-196">Para un ejemplo detallado, consulte [Cambio de ejemplo de clase de recursos de usuario](#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="d3e25-196">For a detailed example, see [Changing user resource class example](#changing-user-resource-class-example).</span></span>

## <a name="memory-allocation"></a><span data-ttu-id="d3e25-197">Asignación de memoria</span><span class="sxs-lookup"><span data-stu-id="d3e25-197">Memory allocation</span></span>
<span data-ttu-id="d3e25-198">Hay ventajas y desventajas tooincreasing clase de recursos de un usuario.</span><span class="sxs-lookup"><span data-stu-id="d3e25-198">There are pros and cons tooincreasing a user's resource class.</span></span> <span data-ttu-id="d3e25-199">Al aumentar una clase de recursos para un usuario, ofrece a sus consultas memoria toomore de acceso, lo que puede conllevar las consultas se ejecutan con mayor rapidez.</span><span class="sxs-lookup"><span data-stu-id="d3e25-199">Increasing a resource class for a user, gives their queries access toomore memory, which may mean queries execute faster.</span></span>  <span data-ttu-id="d3e25-200">Sin embargo, las clases de recursos elevadas también reducen el número de Hola de consultas simultáneas que se pueden ejecutar.</span><span class="sxs-lookup"><span data-stu-id="d3e25-200">However, higher resource classes also reduce hello number of concurrent queries that can run.</span></span> <span data-ttu-id="d3e25-201">Se trata de equilibrio de hello entre asignar grandes cantidades de consulta única de tooa de memoria o si permite que otras consultas, que también necesitan las asignaciones de memoria, toorun simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="d3e25-201">This is hello trade-off between allocating large amounts of memory tooa single query or allowing other queries, which also need memory allocations, toorun concurrently.</span></span> <span data-ttu-id="d3e25-202">Si un usuario se le concede alta asignaciones de memoria para una consulta, otros usuarios no tendrán acceso toothat mismo memoria toorun una consulta.</span><span class="sxs-lookup"><span data-stu-id="d3e25-202">If one user is given high allocations of memory for a query, other users will not have access toothat same memory toorun a query.</span></span>

<span data-ttu-id="d3e25-203">Hello en la tabla siguiente asigna memoria de Hola asignada tooeach distribución por unidad y recursos de clase.</span><span class="sxs-lookup"><span data-stu-id="d3e25-203">hello following table maps hello memory allocated tooeach distribution by DWU and resource class.</span></span>

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a><span data-ttu-id="d3e25-204">Asignaciones de memoria por distribución para las clases de recursos dinámicos (MB)</span><span class="sxs-lookup"><span data-stu-id="d3e25-204">Memory allocations per distribution for dynamic resource classes (MB)</span></span>
| <span data-ttu-id="d3e25-205">DWU</span><span class="sxs-lookup"><span data-stu-id="d3e25-205">DWU</span></span> | <span data-ttu-id="d3e25-206">smallrc</span><span class="sxs-lookup"><span data-stu-id="d3e25-206">smallrc</span></span> | <span data-ttu-id="d3e25-207">mediumrc</span><span class="sxs-lookup"><span data-stu-id="d3e25-207">mediumrc</span></span> | <span data-ttu-id="d3e25-208">largerc</span><span class="sxs-lookup"><span data-stu-id="d3e25-208">largerc</span></span> | <span data-ttu-id="d3e25-209">xlargerc</span><span class="sxs-lookup"><span data-stu-id="d3e25-209">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="d3e25-210">DW100</span><span class="sxs-lookup"><span data-stu-id="d3e25-210">DW100</span></span> |<span data-ttu-id="d3e25-211">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-211">100</span></span> |<span data-ttu-id="d3e25-212">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-212">100</span></span> |<span data-ttu-id="d3e25-213">200</span><span class="sxs-lookup"><span data-stu-id="d3e25-213">200</span></span> |<span data-ttu-id="d3e25-214">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-214">400</span></span> |
| <span data-ttu-id="d3e25-215">DW200</span><span class="sxs-lookup"><span data-stu-id="d3e25-215">DW200</span></span> |<span data-ttu-id="d3e25-216">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-216">100</span></span> |<span data-ttu-id="d3e25-217">200</span><span class="sxs-lookup"><span data-stu-id="d3e25-217">200</span></span> |<span data-ttu-id="d3e25-218">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-218">400</span></span> |<span data-ttu-id="d3e25-219">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-219">800</span></span> |
| <span data-ttu-id="d3e25-220">DW300</span><span class="sxs-lookup"><span data-stu-id="d3e25-220">DW300</span></span> |<span data-ttu-id="d3e25-221">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-221">100</span></span> |<span data-ttu-id="d3e25-222">200</span><span class="sxs-lookup"><span data-stu-id="d3e25-222">200</span></span> |<span data-ttu-id="d3e25-223">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-223">400</span></span> |<span data-ttu-id="d3e25-224">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-224">800</span></span> |
| <span data-ttu-id="d3e25-225">DW400</span><span class="sxs-lookup"><span data-stu-id="d3e25-225">DW400</span></span> |<span data-ttu-id="d3e25-226">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-226">100</span></span> |<span data-ttu-id="d3e25-227">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-227">400</span></span> |<span data-ttu-id="d3e25-228">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-228">800</span></span> |<span data-ttu-id="d3e25-229">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-229">1,600</span></span> |
| <span data-ttu-id="d3e25-230">DW500</span><span class="sxs-lookup"><span data-stu-id="d3e25-230">DW500</span></span> |<span data-ttu-id="d3e25-231">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-231">100</span></span> |<span data-ttu-id="d3e25-232">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-232">400</span></span> |<span data-ttu-id="d3e25-233">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-233">800</span></span> |<span data-ttu-id="d3e25-234">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-234">1,600</span></span> |
| <span data-ttu-id="d3e25-235">DW600</span><span class="sxs-lookup"><span data-stu-id="d3e25-235">DW600</span></span> |<span data-ttu-id="d3e25-236">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-236">100</span></span> |<span data-ttu-id="d3e25-237">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-237">400</span></span> |<span data-ttu-id="d3e25-238">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-238">800</span></span> |<span data-ttu-id="d3e25-239">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-239">1,600</span></span> |
| <span data-ttu-id="d3e25-240">DW1000</span><span class="sxs-lookup"><span data-stu-id="d3e25-240">DW1000</span></span> |<span data-ttu-id="d3e25-241">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-241">100</span></span> |<span data-ttu-id="d3e25-242">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-242">800</span></span> |<span data-ttu-id="d3e25-243">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-243">1,600</span></span> |<span data-ttu-id="d3e25-244">3.200</span><span class="sxs-lookup"><span data-stu-id="d3e25-244">3,200</span></span> |
| <span data-ttu-id="d3e25-245">DW1200</span><span class="sxs-lookup"><span data-stu-id="d3e25-245">DW1200</span></span> |<span data-ttu-id="d3e25-246">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-246">100</span></span> |<span data-ttu-id="d3e25-247">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-247">800</span></span> |<span data-ttu-id="d3e25-248">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-248">1,600</span></span> |<span data-ttu-id="d3e25-249">3.200</span><span class="sxs-lookup"><span data-stu-id="d3e25-249">3,200</span></span> |
| <span data-ttu-id="d3e25-250">DW1500</span><span class="sxs-lookup"><span data-stu-id="d3e25-250">DW1500</span></span> |<span data-ttu-id="d3e25-251">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-251">100</span></span> |<span data-ttu-id="d3e25-252">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-252">800</span></span> |<span data-ttu-id="d3e25-253">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-253">1,600</span></span> |<span data-ttu-id="d3e25-254">3.200</span><span class="sxs-lookup"><span data-stu-id="d3e25-254">3,200</span></span> |
| <span data-ttu-id="d3e25-255">DW2000</span><span class="sxs-lookup"><span data-stu-id="d3e25-255">DW2000</span></span> |<span data-ttu-id="d3e25-256">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-256">100</span></span> |<span data-ttu-id="d3e25-257">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-257">1,600</span></span> |<span data-ttu-id="d3e25-258">3.200</span><span class="sxs-lookup"><span data-stu-id="d3e25-258">3,200</span></span> |<span data-ttu-id="d3e25-259">6.400</span><span class="sxs-lookup"><span data-stu-id="d3e25-259">6,400</span></span> |
| <span data-ttu-id="d3e25-260">DW3000</span><span class="sxs-lookup"><span data-stu-id="d3e25-260">DW3000</span></span> |<span data-ttu-id="d3e25-261">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-261">100</span></span> |<span data-ttu-id="d3e25-262">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-262">1,600</span></span> |<span data-ttu-id="d3e25-263">3.200</span><span class="sxs-lookup"><span data-stu-id="d3e25-263">3,200</span></span> |<span data-ttu-id="d3e25-264">6.400</span><span class="sxs-lookup"><span data-stu-id="d3e25-264">6,400</span></span> |
| <span data-ttu-id="d3e25-265">DW6000</span><span class="sxs-lookup"><span data-stu-id="d3e25-265">DW6000</span></span> |<span data-ttu-id="d3e25-266">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-266">100</span></span> |<span data-ttu-id="d3e25-267">3.200</span><span class="sxs-lookup"><span data-stu-id="d3e25-267">3,200</span></span> |<span data-ttu-id="d3e25-268">6.400</span><span class="sxs-lookup"><span data-stu-id="d3e25-268">6,400</span></span> |<span data-ttu-id="d3e25-269">12.800</span><span class="sxs-lookup"><span data-stu-id="d3e25-269">12,800</span></span> |

<span data-ttu-id="d3e25-270">Hello en la tabla siguiente asigna memoria de hello asignada tooeach distribución por unidad y la clase de recurso estático.</span><span class="sxs-lookup"><span data-stu-id="d3e25-270">hello following table maps hello memory allocated tooeach distribution by DWU and static resource class.</span></span> <span data-ttu-id="d3e25-271">Tenga en cuenta que las clases de recursos elevadas hello tienen su memoria reduce los límites de DWU globales toohonor Hola.</span><span class="sxs-lookup"><span data-stu-id="d3e25-271">Note that hello higher resource classes have their memory reduced toohonor hello global DWU limits.</span></span>

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a><span data-ttu-id="d3e25-272">Asignaciones de memoria por distribución para las clases de recursos estáticos (MB)</span><span class="sxs-lookup"><span data-stu-id="d3e25-272">Memory allocations per distribution for static resource classes (MB)</span></span>
| <span data-ttu-id="d3e25-273">DWU</span><span class="sxs-lookup"><span data-stu-id="d3e25-273">DWU</span></span> | <span data-ttu-id="d3e25-274">staticrc10</span><span class="sxs-lookup"><span data-stu-id="d3e25-274">staticrc10</span></span> | <span data-ttu-id="d3e25-275">staticrc20</span><span class="sxs-lookup"><span data-stu-id="d3e25-275">staticrc20</span></span> | <span data-ttu-id="d3e25-276">staticrc30</span><span class="sxs-lookup"><span data-stu-id="d3e25-276">staticrc30</span></span> | <span data-ttu-id="d3e25-277">staticrc40</span><span class="sxs-lookup"><span data-stu-id="d3e25-277">staticrc40</span></span> | <span data-ttu-id="d3e25-278">staticrc50</span><span class="sxs-lookup"><span data-stu-id="d3e25-278">staticrc50</span></span> | <span data-ttu-id="d3e25-279">staticrc60</span><span class="sxs-lookup"><span data-stu-id="d3e25-279">staticrc60</span></span> | <span data-ttu-id="d3e25-280">staticrc70</span><span class="sxs-lookup"><span data-stu-id="d3e25-280">staticrc70</span></span> | <span data-ttu-id="d3e25-281">staticrc80</span><span class="sxs-lookup"><span data-stu-id="d3e25-281">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="d3e25-282">DW100</span><span class="sxs-lookup"><span data-stu-id="d3e25-282">DW100</span></span> |<span data-ttu-id="d3e25-283">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-283">100</span></span> |<span data-ttu-id="d3e25-284">200</span><span class="sxs-lookup"><span data-stu-id="d3e25-284">200</span></span> |<span data-ttu-id="d3e25-285">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-285">400</span></span> |<span data-ttu-id="d3e25-286">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-286">400</span></span> |<span data-ttu-id="d3e25-287">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-287">400</span></span> |<span data-ttu-id="d3e25-288">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-288">400</span></span> |<span data-ttu-id="d3e25-289">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-289">400</span></span> |<span data-ttu-id="d3e25-290">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-290">400</span></span> |
| <span data-ttu-id="d3e25-291">DW200</span><span class="sxs-lookup"><span data-stu-id="d3e25-291">DW200</span></span> |<span data-ttu-id="d3e25-292">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-292">100</span></span> |<span data-ttu-id="d3e25-293">200</span><span class="sxs-lookup"><span data-stu-id="d3e25-293">200</span></span> |<span data-ttu-id="d3e25-294">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-294">400</span></span> |<span data-ttu-id="d3e25-295">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-295">800</span></span> |<span data-ttu-id="d3e25-296">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-296">800</span></span> |<span data-ttu-id="d3e25-297">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-297">800</span></span> |<span data-ttu-id="d3e25-298">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-298">800</span></span> |<span data-ttu-id="d3e25-299">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-299">800</span></span> |
| <span data-ttu-id="d3e25-300">DW300</span><span class="sxs-lookup"><span data-stu-id="d3e25-300">DW300</span></span> |<span data-ttu-id="d3e25-301">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-301">100</span></span> |<span data-ttu-id="d3e25-302">200</span><span class="sxs-lookup"><span data-stu-id="d3e25-302">200</span></span> |<span data-ttu-id="d3e25-303">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-303">400</span></span> |<span data-ttu-id="d3e25-304">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-304">800</span></span> |<span data-ttu-id="d3e25-305">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-305">800</span></span> |<span data-ttu-id="d3e25-306">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-306">800</span></span> |<span data-ttu-id="d3e25-307">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-307">800</span></span> |<span data-ttu-id="d3e25-308">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-308">800</span></span> |
| <span data-ttu-id="d3e25-309">DW400</span><span class="sxs-lookup"><span data-stu-id="d3e25-309">DW400</span></span> |<span data-ttu-id="d3e25-310">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-310">100</span></span> |<span data-ttu-id="d3e25-311">200</span><span class="sxs-lookup"><span data-stu-id="d3e25-311">200</span></span> |<span data-ttu-id="d3e25-312">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-312">400</span></span> |<span data-ttu-id="d3e25-313">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-313">800</span></span> |<span data-ttu-id="d3e25-314">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-314">1,600</span></span> |<span data-ttu-id="d3e25-315">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-315">1,600</span></span> |<span data-ttu-id="d3e25-316">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-316">1,600</span></span> |<span data-ttu-id="d3e25-317">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-317">1,600</span></span> |
| <span data-ttu-id="d3e25-318">DW500</span><span class="sxs-lookup"><span data-stu-id="d3e25-318">DW500</span></span> |<span data-ttu-id="d3e25-319">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-319">100</span></span> |<span data-ttu-id="d3e25-320">200</span><span class="sxs-lookup"><span data-stu-id="d3e25-320">200</span></span> |<span data-ttu-id="d3e25-321">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-321">400</span></span> |<span data-ttu-id="d3e25-322">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-322">800</span></span> |<span data-ttu-id="d3e25-323">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-323">1,600</span></span> |<span data-ttu-id="d3e25-324">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-324">1,600</span></span> |<span data-ttu-id="d3e25-325">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-325">1,600</span></span> |<span data-ttu-id="d3e25-326">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-326">1,600</span></span> |
| <span data-ttu-id="d3e25-327">DW600</span><span class="sxs-lookup"><span data-stu-id="d3e25-327">DW600</span></span> |<span data-ttu-id="d3e25-328">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-328">100</span></span> |<span data-ttu-id="d3e25-329">200</span><span class="sxs-lookup"><span data-stu-id="d3e25-329">200</span></span> |<span data-ttu-id="d3e25-330">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-330">400</span></span> |<span data-ttu-id="d3e25-331">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-331">800</span></span> |<span data-ttu-id="d3e25-332">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-332">1,600</span></span> |<span data-ttu-id="d3e25-333">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-333">1,600</span></span> |<span data-ttu-id="d3e25-334">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-334">1,600</span></span> |<span data-ttu-id="d3e25-335">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-335">1,600</span></span> |
| <span data-ttu-id="d3e25-336">DW1000</span><span class="sxs-lookup"><span data-stu-id="d3e25-336">DW1000</span></span> |<span data-ttu-id="d3e25-337">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-337">100</span></span> |<span data-ttu-id="d3e25-338">200</span><span class="sxs-lookup"><span data-stu-id="d3e25-338">200</span></span> |<span data-ttu-id="d3e25-339">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-339">400</span></span> |<span data-ttu-id="d3e25-340">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-340">800</span></span> |<span data-ttu-id="d3e25-341">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-341">1,600</span></span> |<span data-ttu-id="d3e25-342">3.200</span><span class="sxs-lookup"><span data-stu-id="d3e25-342">3,200</span></span> |<span data-ttu-id="d3e25-343">3.200</span><span class="sxs-lookup"><span data-stu-id="d3e25-343">3,200</span></span> |<span data-ttu-id="d3e25-344">3.200</span><span class="sxs-lookup"><span data-stu-id="d3e25-344">3,200</span></span> |
| <span data-ttu-id="d3e25-345">DW1200</span><span class="sxs-lookup"><span data-stu-id="d3e25-345">DW1200</span></span> |<span data-ttu-id="d3e25-346">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-346">100</span></span> |<span data-ttu-id="d3e25-347">200</span><span class="sxs-lookup"><span data-stu-id="d3e25-347">200</span></span> |<span data-ttu-id="d3e25-348">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-348">400</span></span> |<span data-ttu-id="d3e25-349">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-349">800</span></span> |<span data-ttu-id="d3e25-350">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-350">1,600</span></span> |<span data-ttu-id="d3e25-351">3.200</span><span class="sxs-lookup"><span data-stu-id="d3e25-351">3,200</span></span> |<span data-ttu-id="d3e25-352">3.200</span><span class="sxs-lookup"><span data-stu-id="d3e25-352">3,200</span></span> |<span data-ttu-id="d3e25-353">3.200</span><span class="sxs-lookup"><span data-stu-id="d3e25-353">3,200</span></span> |
| <span data-ttu-id="d3e25-354">DW1500</span><span class="sxs-lookup"><span data-stu-id="d3e25-354">DW1500</span></span> |<span data-ttu-id="d3e25-355">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-355">100</span></span> |<span data-ttu-id="d3e25-356">200</span><span class="sxs-lookup"><span data-stu-id="d3e25-356">200</span></span> |<span data-ttu-id="d3e25-357">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-357">400</span></span> |<span data-ttu-id="d3e25-358">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-358">800</span></span> |<span data-ttu-id="d3e25-359">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-359">1,600</span></span> |<span data-ttu-id="d3e25-360">3.200</span><span class="sxs-lookup"><span data-stu-id="d3e25-360">3,200</span></span> |<span data-ttu-id="d3e25-361">3.200</span><span class="sxs-lookup"><span data-stu-id="d3e25-361">3,200</span></span> |<span data-ttu-id="d3e25-362">3.200</span><span class="sxs-lookup"><span data-stu-id="d3e25-362">3,200</span></span> |
| <span data-ttu-id="d3e25-363">DW2000</span><span class="sxs-lookup"><span data-stu-id="d3e25-363">DW2000</span></span> |<span data-ttu-id="d3e25-364">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-364">100</span></span> |<span data-ttu-id="d3e25-365">200</span><span class="sxs-lookup"><span data-stu-id="d3e25-365">200</span></span> |<span data-ttu-id="d3e25-366">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-366">400</span></span> |<span data-ttu-id="d3e25-367">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-367">800</span></span> |<span data-ttu-id="d3e25-368">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-368">1,600</span></span> |<span data-ttu-id="d3e25-369">3.200</span><span class="sxs-lookup"><span data-stu-id="d3e25-369">3,200</span></span> |<span data-ttu-id="d3e25-370">6.400</span><span class="sxs-lookup"><span data-stu-id="d3e25-370">6,400</span></span> |<span data-ttu-id="d3e25-371">6.400</span><span class="sxs-lookup"><span data-stu-id="d3e25-371">6,400</span></span> |
| <span data-ttu-id="d3e25-372">DW3000</span><span class="sxs-lookup"><span data-stu-id="d3e25-372">DW3000</span></span> |<span data-ttu-id="d3e25-373">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-373">100</span></span> |<span data-ttu-id="d3e25-374">200</span><span class="sxs-lookup"><span data-stu-id="d3e25-374">200</span></span> |<span data-ttu-id="d3e25-375">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-375">400</span></span> |<span data-ttu-id="d3e25-376">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-376">800</span></span> |<span data-ttu-id="d3e25-377">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-377">1,600</span></span> |<span data-ttu-id="d3e25-378">3.200</span><span class="sxs-lookup"><span data-stu-id="d3e25-378">3,200</span></span> |<span data-ttu-id="d3e25-379">6.400</span><span class="sxs-lookup"><span data-stu-id="d3e25-379">6,400</span></span> |<span data-ttu-id="d3e25-380">6.400</span><span class="sxs-lookup"><span data-stu-id="d3e25-380">6,400</span></span> |
| <span data-ttu-id="d3e25-381">DW6000</span><span class="sxs-lookup"><span data-stu-id="d3e25-381">DW6000</span></span> |<span data-ttu-id="d3e25-382">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-382">100</span></span> |<span data-ttu-id="d3e25-383">200</span><span class="sxs-lookup"><span data-stu-id="d3e25-383">200</span></span> |<span data-ttu-id="d3e25-384">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-384">400</span></span> |<span data-ttu-id="d3e25-385">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-385">800</span></span> |<span data-ttu-id="d3e25-386">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-386">1,600</span></span> |<span data-ttu-id="d3e25-387">3.200</span><span class="sxs-lookup"><span data-stu-id="d3e25-387">3,200</span></span> |<span data-ttu-id="d3e25-388">6.400</span><span class="sxs-lookup"><span data-stu-id="d3e25-388">6,400</span></span> |<span data-ttu-id="d3e25-389">12.800</span><span class="sxs-lookup"><span data-stu-id="d3e25-389">12,800</span></span> |

<span data-ttu-id="d3e25-390">De hello tabla anterior, puede ver que una consulta que se ejecuta en un DW2000 Hola **xlargerc** clase de recurso tendría acceso too6, 400 MB de memoria en cada una de las bases de datos distribuidas Hola 60.</span><span class="sxs-lookup"><span data-stu-id="d3e25-390">From hello preceding table, you can see that a query running on a DW2000 in hello **xlargerc** resource class would have access too6,400 MB of memory within each of hello 60 distributed databases.</span></span>  <span data-ttu-id="d3e25-391">En Almacenamiento de datos SQL, existe 60 distribuciones.</span><span class="sxs-lookup"><span data-stu-id="d3e25-391">In SQL Data Warehouse, there are 60 distributions.</span></span> <span data-ttu-id="d3e25-392">Por lo tanto, asignación de memoria total de hello toocalculate para una consulta en una clase de recurso determinado, Hola por encima de valores debe se multiplica por 60.</span><span class="sxs-lookup"><span data-stu-id="d3e25-392">Therefore, toocalculate hello total memory allocation for a query in a given resource class, hello above values should be multiplied by 60.</span></span>

### <a name="memory-allocations-system-wide-gb"></a><span data-ttu-id="d3e25-393">Asignaciones de memoria en todo el sistema (GB)</span><span class="sxs-lookup"><span data-stu-id="d3e25-393">Memory allocations system-wide (GB)</span></span>
| <span data-ttu-id="d3e25-394">DWU</span><span class="sxs-lookup"><span data-stu-id="d3e25-394">DWU</span></span> | <span data-ttu-id="d3e25-395">smallrc</span><span class="sxs-lookup"><span data-stu-id="d3e25-395">smallrc</span></span> | <span data-ttu-id="d3e25-396">mediumrc</span><span class="sxs-lookup"><span data-stu-id="d3e25-396">mediumrc</span></span> | <span data-ttu-id="d3e25-397">largerc</span><span class="sxs-lookup"><span data-stu-id="d3e25-397">largerc</span></span> | <span data-ttu-id="d3e25-398">xlargerc</span><span class="sxs-lookup"><span data-stu-id="d3e25-398">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="d3e25-399">DW100</span><span class="sxs-lookup"><span data-stu-id="d3e25-399">DW100</span></span> |<span data-ttu-id="d3e25-400">6</span><span class="sxs-lookup"><span data-stu-id="d3e25-400">6</span></span> |<span data-ttu-id="d3e25-401">6</span><span class="sxs-lookup"><span data-stu-id="d3e25-401">6</span></span> |<span data-ttu-id="d3e25-402">12</span><span class="sxs-lookup"><span data-stu-id="d3e25-402">12</span></span> |<span data-ttu-id="d3e25-403">23</span><span class="sxs-lookup"><span data-stu-id="d3e25-403">23</span></span> |
| <span data-ttu-id="d3e25-404">DW200</span><span class="sxs-lookup"><span data-stu-id="d3e25-404">DW200</span></span> |<span data-ttu-id="d3e25-405">6</span><span class="sxs-lookup"><span data-stu-id="d3e25-405">6</span></span> |<span data-ttu-id="d3e25-406">12</span><span class="sxs-lookup"><span data-stu-id="d3e25-406">12</span></span> |<span data-ttu-id="d3e25-407">23</span><span class="sxs-lookup"><span data-stu-id="d3e25-407">23</span></span> |<span data-ttu-id="d3e25-408">47</span><span class="sxs-lookup"><span data-stu-id="d3e25-408">47</span></span> |
| <span data-ttu-id="d3e25-409">DW300</span><span class="sxs-lookup"><span data-stu-id="d3e25-409">DW300</span></span> |<span data-ttu-id="d3e25-410">6</span><span class="sxs-lookup"><span data-stu-id="d3e25-410">6</span></span> |<span data-ttu-id="d3e25-411">12</span><span class="sxs-lookup"><span data-stu-id="d3e25-411">12</span></span> |<span data-ttu-id="d3e25-412">23</span><span class="sxs-lookup"><span data-stu-id="d3e25-412">23</span></span> |<span data-ttu-id="d3e25-413">47</span><span class="sxs-lookup"><span data-stu-id="d3e25-413">47</span></span> |
| <span data-ttu-id="d3e25-414">DW400</span><span class="sxs-lookup"><span data-stu-id="d3e25-414">DW400</span></span> |<span data-ttu-id="d3e25-415">6</span><span class="sxs-lookup"><span data-stu-id="d3e25-415">6</span></span> |<span data-ttu-id="d3e25-416">23</span><span class="sxs-lookup"><span data-stu-id="d3e25-416">23</span></span> |<span data-ttu-id="d3e25-417">47</span><span class="sxs-lookup"><span data-stu-id="d3e25-417">47</span></span> |<span data-ttu-id="d3e25-418">94</span><span class="sxs-lookup"><span data-stu-id="d3e25-418">94</span></span> |
| <span data-ttu-id="d3e25-419">DW500</span><span class="sxs-lookup"><span data-stu-id="d3e25-419">DW500</span></span> |<span data-ttu-id="d3e25-420">6</span><span class="sxs-lookup"><span data-stu-id="d3e25-420">6</span></span> |<span data-ttu-id="d3e25-421">23</span><span class="sxs-lookup"><span data-stu-id="d3e25-421">23</span></span> |<span data-ttu-id="d3e25-422">47</span><span class="sxs-lookup"><span data-stu-id="d3e25-422">47</span></span> |<span data-ttu-id="d3e25-423">94</span><span class="sxs-lookup"><span data-stu-id="d3e25-423">94</span></span> |
| <span data-ttu-id="d3e25-424">DW600</span><span class="sxs-lookup"><span data-stu-id="d3e25-424">DW600</span></span> |<span data-ttu-id="d3e25-425">6</span><span class="sxs-lookup"><span data-stu-id="d3e25-425">6</span></span> |<span data-ttu-id="d3e25-426">23</span><span class="sxs-lookup"><span data-stu-id="d3e25-426">23</span></span> |<span data-ttu-id="d3e25-427">47</span><span class="sxs-lookup"><span data-stu-id="d3e25-427">47</span></span> |<span data-ttu-id="d3e25-428">94</span><span class="sxs-lookup"><span data-stu-id="d3e25-428">94</span></span> |
| <span data-ttu-id="d3e25-429">DW1000</span><span class="sxs-lookup"><span data-stu-id="d3e25-429">DW1000</span></span> |<span data-ttu-id="d3e25-430">6</span><span class="sxs-lookup"><span data-stu-id="d3e25-430">6</span></span> |<span data-ttu-id="d3e25-431">47</span><span class="sxs-lookup"><span data-stu-id="d3e25-431">47</span></span> |<span data-ttu-id="d3e25-432">94</span><span class="sxs-lookup"><span data-stu-id="d3e25-432">94</span></span> |<span data-ttu-id="d3e25-433">188</span><span class="sxs-lookup"><span data-stu-id="d3e25-433">188</span></span> |
| <span data-ttu-id="d3e25-434">DW1200</span><span class="sxs-lookup"><span data-stu-id="d3e25-434">DW1200</span></span> |<span data-ttu-id="d3e25-435">6</span><span class="sxs-lookup"><span data-stu-id="d3e25-435">6</span></span> |<span data-ttu-id="d3e25-436">47</span><span class="sxs-lookup"><span data-stu-id="d3e25-436">47</span></span> |<span data-ttu-id="d3e25-437">94</span><span class="sxs-lookup"><span data-stu-id="d3e25-437">94</span></span> |<span data-ttu-id="d3e25-438">188</span><span class="sxs-lookup"><span data-stu-id="d3e25-438">188</span></span> |
| <span data-ttu-id="d3e25-439">DW1500</span><span class="sxs-lookup"><span data-stu-id="d3e25-439">DW1500</span></span> |<span data-ttu-id="d3e25-440">6</span><span class="sxs-lookup"><span data-stu-id="d3e25-440">6</span></span> |<span data-ttu-id="d3e25-441">47</span><span class="sxs-lookup"><span data-stu-id="d3e25-441">47</span></span> |<span data-ttu-id="d3e25-442">94</span><span class="sxs-lookup"><span data-stu-id="d3e25-442">94</span></span> |<span data-ttu-id="d3e25-443">188</span><span class="sxs-lookup"><span data-stu-id="d3e25-443">188</span></span> |
| <span data-ttu-id="d3e25-444">DW2000</span><span class="sxs-lookup"><span data-stu-id="d3e25-444">DW2000</span></span> |<span data-ttu-id="d3e25-445">6</span><span class="sxs-lookup"><span data-stu-id="d3e25-445">6</span></span> |<span data-ttu-id="d3e25-446">94</span><span class="sxs-lookup"><span data-stu-id="d3e25-446">94</span></span> |<span data-ttu-id="d3e25-447">188</span><span class="sxs-lookup"><span data-stu-id="d3e25-447">188</span></span> |<span data-ttu-id="d3e25-448">375</span><span class="sxs-lookup"><span data-stu-id="d3e25-448">375</span></span> |
| <span data-ttu-id="d3e25-449">DW3000</span><span class="sxs-lookup"><span data-stu-id="d3e25-449">DW3000</span></span> |<span data-ttu-id="d3e25-450">6</span><span class="sxs-lookup"><span data-stu-id="d3e25-450">6</span></span> |<span data-ttu-id="d3e25-451">94</span><span class="sxs-lookup"><span data-stu-id="d3e25-451">94</span></span> |<span data-ttu-id="d3e25-452">188</span><span class="sxs-lookup"><span data-stu-id="d3e25-452">188</span></span> |<span data-ttu-id="d3e25-453">375</span><span class="sxs-lookup"><span data-stu-id="d3e25-453">375</span></span> |
| <span data-ttu-id="d3e25-454">DW6000</span><span class="sxs-lookup"><span data-stu-id="d3e25-454">DW6000</span></span> |<span data-ttu-id="d3e25-455">6</span><span class="sxs-lookup"><span data-stu-id="d3e25-455">6</span></span> |<span data-ttu-id="d3e25-456">188</span><span class="sxs-lookup"><span data-stu-id="d3e25-456">188</span></span> |<span data-ttu-id="d3e25-457">375</span><span class="sxs-lookup"><span data-stu-id="d3e25-457">375</span></span> |<span data-ttu-id="d3e25-458">750</span><span class="sxs-lookup"><span data-stu-id="d3e25-458">750</span></span> |

<span data-ttu-id="d3e25-459">En esta tabla de asignaciones de memoria de todo el sistema, puede ver que una consulta que se ejecuta en un DW2000 en la clase de recurso de hello xlargerc se asigna un total de 375 GB de memoria (MB * 60 6.400 distribuciones / 1.024 tooconvert tooGB) en toda Hola el almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="d3e25-459">From this table of system-wide memory allocations, you can see that a query running on a DW2000 in hello xlargerc resource class is allocated a total of 375 GB of memory (6,400 MB * 60 distributions / 1,024 tooconvert tooGB) over hello entirety of your SQL Data Warehouse.</span></span>

<span data-ttu-id="d3e25-460">Hello mismo cálculo aplica toostatic clases de recursos.</span><span class="sxs-lookup"><span data-stu-id="d3e25-460">hello same calculation applies toostatic resource classes.</span></span>
 
## <a name="concurrency-slot-consumption"></a><span data-ttu-id="d3e25-461">Consumo de ranuras de simultaneidad</span><span class="sxs-lookup"><span data-stu-id="d3e25-461">Concurrency slot consumption</span></span>  
<span data-ttu-id="d3e25-462">Almacenamiento de datos SQL concede más tooqueries memoria ejecuta en las clases de recursos elevadas.</span><span class="sxs-lookup"><span data-stu-id="d3e25-462">SQL Data Warehouse grants more memory tooqueries running in higher resource classes.</span></span> <span data-ttu-id="d3e25-463">La memoria es un recurso fijo.</span><span class="sxs-lookup"><span data-stu-id="d3e25-463">Memory is a fixed resource.</span></span>  <span data-ttu-id="d3e25-464">Por lo tanto, hello más memoria asignada por cada consulta, Hola pueden ejecutar menos consultas simultáneas.</span><span class="sxs-lookup"><span data-stu-id="d3e25-464">Therefore, hello more memory allocated per query, hello fewer concurrent queries can execute.</span></span> <span data-ttu-id="d3e25-465">Hello siguiente tabla Reitere todos Hola conceptos anterior en una sola vista que muestra el número de Hola de ranuras de simultaneidad disponibles por unidad y ranuras de hello consumidas por cada clase de recursos.</span><span class="sxs-lookup"><span data-stu-id="d3e25-465">hello following table reiterates all of hello previous concepts in a single view that shows hello number of concurrency slots available by DWU and hello slots consumed by each resource class.</span></span>  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a><span data-ttu-id="d3e25-466">Asignación y consumo de espacios de simultaneidad para las clases de recursos dinámicos</span><span class="sxs-lookup"><span data-stu-id="d3e25-466">Allocation and consumption of concurrency slots for dynamic resource classes</span></span>  
| <span data-ttu-id="d3e25-467">DWU</span><span class="sxs-lookup"><span data-stu-id="d3e25-467">DWU</span></span> | <span data-ttu-id="d3e25-468">N.º máximo de consultas simultáneas</span><span class="sxs-lookup"><span data-stu-id="d3e25-468">Maximum concurrent queries</span></span> | <span data-ttu-id="d3e25-469">Espacios de simultaneidad asignados</span><span class="sxs-lookup"><span data-stu-id="d3e25-469">Concurrency slots allocated</span></span> | <span data-ttu-id="d3e25-470">Ranuras utilizadas por smallrc</span><span class="sxs-lookup"><span data-stu-id="d3e25-470">Slots used by smallrc</span></span> | <span data-ttu-id="d3e25-471">Ranuras utilizadas por mediumrc</span><span class="sxs-lookup"><span data-stu-id="d3e25-471">Slots used by mediumrc</span></span> | <span data-ttu-id="d3e25-472">Ranuras utilizadas por largerc</span><span class="sxs-lookup"><span data-stu-id="d3e25-472">Slots used by largerc</span></span> | <span data-ttu-id="d3e25-473">Ranuras utilizadas por xlargerc</span><span class="sxs-lookup"><span data-stu-id="d3e25-473">Slots used by xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="d3e25-474">DW100</span><span class="sxs-lookup"><span data-stu-id="d3e25-474">DW100</span></span> |<span data-ttu-id="d3e25-475">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-475">4</span></span> |<span data-ttu-id="d3e25-476">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-476">4</span></span> |<span data-ttu-id="d3e25-477">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-477">1</span></span> |<span data-ttu-id="d3e25-478">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-478">1</span></span> |<span data-ttu-id="d3e25-479">2</span><span class="sxs-lookup"><span data-stu-id="d3e25-479">2</span></span> |<span data-ttu-id="d3e25-480">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-480">4</span></span> |
| <span data-ttu-id="d3e25-481">DW200</span><span class="sxs-lookup"><span data-stu-id="d3e25-481">DW200</span></span> |<span data-ttu-id="d3e25-482">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-482">8</span></span> |<span data-ttu-id="d3e25-483">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-483">8</span></span> |<span data-ttu-id="d3e25-484">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-484">1</span></span> |<span data-ttu-id="d3e25-485">2</span><span class="sxs-lookup"><span data-stu-id="d3e25-485">2</span></span> |<span data-ttu-id="d3e25-486">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-486">4</span></span> |<span data-ttu-id="d3e25-487">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-487">8</span></span> |
| <span data-ttu-id="d3e25-488">DW300</span><span class="sxs-lookup"><span data-stu-id="d3e25-488">DW300</span></span> |<span data-ttu-id="d3e25-489">12</span><span class="sxs-lookup"><span data-stu-id="d3e25-489">12</span></span> |<span data-ttu-id="d3e25-490">12</span><span class="sxs-lookup"><span data-stu-id="d3e25-490">12</span></span> |<span data-ttu-id="d3e25-491">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-491">1</span></span> |<span data-ttu-id="d3e25-492">2</span><span class="sxs-lookup"><span data-stu-id="d3e25-492">2</span></span> |<span data-ttu-id="d3e25-493">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-493">4</span></span> |<span data-ttu-id="d3e25-494">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-494">8</span></span> |
| <span data-ttu-id="d3e25-495">DW400</span><span class="sxs-lookup"><span data-stu-id="d3e25-495">DW400</span></span> |<span data-ttu-id="d3e25-496">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-496">16</span></span> |<span data-ttu-id="d3e25-497">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-497">16</span></span> |<span data-ttu-id="d3e25-498">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-498">1</span></span> |<span data-ttu-id="d3e25-499">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-499">4</span></span> |<span data-ttu-id="d3e25-500">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-500">8</span></span> |<span data-ttu-id="d3e25-501">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-501">16</span></span> |
| <span data-ttu-id="d3e25-502">DW500</span><span class="sxs-lookup"><span data-stu-id="d3e25-502">DW500</span></span> |<span data-ttu-id="d3e25-503">20 |</span><span class="sxs-lookup"><span data-stu-id="d3e25-503">20</span></span> |<span data-ttu-id="d3e25-504">20 |</span><span class="sxs-lookup"><span data-stu-id="d3e25-504">20</span></span> |<span data-ttu-id="d3e25-505">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-505">1</span></span> |<span data-ttu-id="d3e25-506">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-506">4</span></span> |<span data-ttu-id="d3e25-507">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-507">8</span></span> |<span data-ttu-id="d3e25-508">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-508">16</span></span> |
| <span data-ttu-id="d3e25-509">DW600</span><span class="sxs-lookup"><span data-stu-id="d3e25-509">DW600</span></span> |<span data-ttu-id="d3e25-510">24</span><span class="sxs-lookup"><span data-stu-id="d3e25-510">24</span></span> |<span data-ttu-id="d3e25-511">24</span><span class="sxs-lookup"><span data-stu-id="d3e25-511">24</span></span> |<span data-ttu-id="d3e25-512">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-512">1</span></span> |<span data-ttu-id="d3e25-513">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-513">4</span></span> |<span data-ttu-id="d3e25-514">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-514">8</span></span> |<span data-ttu-id="d3e25-515">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-515">16</span></span> |
| <span data-ttu-id="d3e25-516">DW1000</span><span class="sxs-lookup"><span data-stu-id="d3e25-516">DW1000</span></span> |<span data-ttu-id="d3e25-517">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-517">32</span></span> |<span data-ttu-id="d3e25-518">40</span><span class="sxs-lookup"><span data-stu-id="d3e25-518">40</span></span> |<span data-ttu-id="d3e25-519">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-519">1</span></span> |<span data-ttu-id="d3e25-520">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-520">8</span></span> |<span data-ttu-id="d3e25-521">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-521">16</span></span> |<span data-ttu-id="d3e25-522">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-522">32</span></span> |
| <span data-ttu-id="d3e25-523">DW1200</span><span class="sxs-lookup"><span data-stu-id="d3e25-523">DW1200</span></span> |<span data-ttu-id="d3e25-524">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-524">32</span></span> |<span data-ttu-id="d3e25-525">48</span><span class="sxs-lookup"><span data-stu-id="d3e25-525">48</span></span> |<span data-ttu-id="d3e25-526">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-526">1</span></span> |<span data-ttu-id="d3e25-527">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-527">8</span></span> |<span data-ttu-id="d3e25-528">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-528">16</span></span> |<span data-ttu-id="d3e25-529">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-529">32</span></span> |
| <span data-ttu-id="d3e25-530">DW1500</span><span class="sxs-lookup"><span data-stu-id="d3e25-530">DW1500</span></span> |<span data-ttu-id="d3e25-531">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-531">32</span></span> |<span data-ttu-id="d3e25-532">60</span><span class="sxs-lookup"><span data-stu-id="d3e25-532">60</span></span> |<span data-ttu-id="d3e25-533">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-533">1</span></span> |<span data-ttu-id="d3e25-534">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-534">8</span></span> |<span data-ttu-id="d3e25-535">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-535">16</span></span> |<span data-ttu-id="d3e25-536">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-536">32</span></span> |
| <span data-ttu-id="d3e25-537">DW2000</span><span class="sxs-lookup"><span data-stu-id="d3e25-537">DW2000</span></span> |<span data-ttu-id="d3e25-538">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-538">32</span></span> |<span data-ttu-id="d3e25-539">80</span><span class="sxs-lookup"><span data-stu-id="d3e25-539">80</span></span> |<span data-ttu-id="d3e25-540">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-540">1</span></span> |<span data-ttu-id="d3e25-541">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-541">16</span></span> |<span data-ttu-id="d3e25-542">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-542">32</span></span> |<span data-ttu-id="d3e25-543">64</span><span class="sxs-lookup"><span data-stu-id="d3e25-543">64</span></span> |
| <span data-ttu-id="d3e25-544">DW3000</span><span class="sxs-lookup"><span data-stu-id="d3e25-544">DW3000</span></span> |<span data-ttu-id="d3e25-545">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-545">32</span></span> |<span data-ttu-id="d3e25-546">120</span><span class="sxs-lookup"><span data-stu-id="d3e25-546">120</span></span> |<span data-ttu-id="d3e25-547">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-547">1</span></span> |<span data-ttu-id="d3e25-548">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-548">16</span></span> |<span data-ttu-id="d3e25-549">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-549">32</span></span> |<span data-ttu-id="d3e25-550">64</span><span class="sxs-lookup"><span data-stu-id="d3e25-550">64</span></span> |
| <span data-ttu-id="d3e25-551">DW6000</span><span class="sxs-lookup"><span data-stu-id="d3e25-551">DW6000</span></span> |<span data-ttu-id="d3e25-552">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-552">32</span></span> |<span data-ttu-id="d3e25-553">240</span><span class="sxs-lookup"><span data-stu-id="d3e25-553">240</span></span> |<span data-ttu-id="d3e25-554">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-554">1</span></span> |<span data-ttu-id="d3e25-555">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-555">32</span></span> |<span data-ttu-id="d3e25-556">64</span><span class="sxs-lookup"><span data-stu-id="d3e25-556">64</span></span> |<span data-ttu-id="d3e25-557">128</span><span class="sxs-lookup"><span data-stu-id="d3e25-557">128</span></span> |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a><span data-ttu-id="d3e25-558">Asignación y consumo de espacios de simultaneidad para las clases de recursos estáticos</span><span class="sxs-lookup"><span data-stu-id="d3e25-558">Allocation and consumption of concurrency slots for static resource classes</span></span>  
| <span data-ttu-id="d3e25-559">DWU</span><span class="sxs-lookup"><span data-stu-id="d3e25-559">DWU</span></span> | <span data-ttu-id="d3e25-560">N.º máximo de consultas simultáneas</span><span class="sxs-lookup"><span data-stu-id="d3e25-560">Maximum concurrent queries</span></span> | <span data-ttu-id="d3e25-561">Espacios de simultaneidad asignados</span><span class="sxs-lookup"><span data-stu-id="d3e25-561">Concurrency slots allocated</span></span> |<span data-ttu-id="d3e25-562">staticrc10</span><span class="sxs-lookup"><span data-stu-id="d3e25-562">staticrc10</span></span> | <span data-ttu-id="d3e25-563">staticrc20</span><span class="sxs-lookup"><span data-stu-id="d3e25-563">staticrc20</span></span> | <span data-ttu-id="d3e25-564">staticrc30</span><span class="sxs-lookup"><span data-stu-id="d3e25-564">staticrc30</span></span> | <span data-ttu-id="d3e25-565">staticrc40</span><span class="sxs-lookup"><span data-stu-id="d3e25-565">staticrc40</span></span> | <span data-ttu-id="d3e25-566">staticrc50</span><span class="sxs-lookup"><span data-stu-id="d3e25-566">staticrc50</span></span> | <span data-ttu-id="d3e25-567">staticrc60</span><span class="sxs-lookup"><span data-stu-id="d3e25-567">staticrc60</span></span> | <span data-ttu-id="d3e25-568">staticrc70</span><span class="sxs-lookup"><span data-stu-id="d3e25-568">staticrc70</span></span> | <span data-ttu-id="d3e25-569">staticrc80</span><span class="sxs-lookup"><span data-stu-id="d3e25-569">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="d3e25-570">DW100</span><span class="sxs-lookup"><span data-stu-id="d3e25-570">DW100</span></span> |<span data-ttu-id="d3e25-571">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-571">4</span></span> |<span data-ttu-id="d3e25-572">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-572">4</span></span> |<span data-ttu-id="d3e25-573">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-573">1</span></span> |<span data-ttu-id="d3e25-574">2</span><span class="sxs-lookup"><span data-stu-id="d3e25-574">2</span></span> |<span data-ttu-id="d3e25-575">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-575">4</span></span> |<span data-ttu-id="d3e25-576">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-576">4</span></span> |<span data-ttu-id="d3e25-577">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-577">4</span></span> |<span data-ttu-id="d3e25-578">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-578">4</span></span> |<span data-ttu-id="d3e25-579">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-579">4</span></span> |<span data-ttu-id="d3e25-580">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-580">4</span></span> |
| <span data-ttu-id="d3e25-581">DW200</span><span class="sxs-lookup"><span data-stu-id="d3e25-581">DW200</span></span> |<span data-ttu-id="d3e25-582">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-582">8</span></span> |<span data-ttu-id="d3e25-583">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-583">8</span></span> |<span data-ttu-id="d3e25-584">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-584">1</span></span> |<span data-ttu-id="d3e25-585">2</span><span class="sxs-lookup"><span data-stu-id="d3e25-585">2</span></span> |<span data-ttu-id="d3e25-586">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-586">4</span></span> |<span data-ttu-id="d3e25-587">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-587">8</span></span> |<span data-ttu-id="d3e25-588">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-588">8</span></span> |<span data-ttu-id="d3e25-589">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-589">8</span></span> |<span data-ttu-id="d3e25-590">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-590">8</span></span> |<span data-ttu-id="d3e25-591">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-591">8</span></span> |
| <span data-ttu-id="d3e25-592">DW300</span><span class="sxs-lookup"><span data-stu-id="d3e25-592">DW300</span></span> |<span data-ttu-id="d3e25-593">12</span><span class="sxs-lookup"><span data-stu-id="d3e25-593">12</span></span> |<span data-ttu-id="d3e25-594">12</span><span class="sxs-lookup"><span data-stu-id="d3e25-594">12</span></span> |<span data-ttu-id="d3e25-595">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-595">1</span></span> |<span data-ttu-id="d3e25-596">2</span><span class="sxs-lookup"><span data-stu-id="d3e25-596">2</span></span> |<span data-ttu-id="d3e25-597">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-597">4</span></span> |<span data-ttu-id="d3e25-598">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-598">8</span></span> |<span data-ttu-id="d3e25-599">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-599">8</span></span> |<span data-ttu-id="d3e25-600">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-600">8</span></span> |<span data-ttu-id="d3e25-601">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-601">8</span></span> |<span data-ttu-id="d3e25-602">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-602">8</span></span> |
| <span data-ttu-id="d3e25-603">DW400</span><span class="sxs-lookup"><span data-stu-id="d3e25-603">DW400</span></span> |<span data-ttu-id="d3e25-604">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-604">16</span></span> |<span data-ttu-id="d3e25-605">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-605">16</span></span> |<span data-ttu-id="d3e25-606">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-606">1</span></span> |<span data-ttu-id="d3e25-607">2</span><span class="sxs-lookup"><span data-stu-id="d3e25-607">2</span></span> |<span data-ttu-id="d3e25-608">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-608">4</span></span> |<span data-ttu-id="d3e25-609">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-609">8</span></span> |<span data-ttu-id="d3e25-610">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-610">16</span></span> |<span data-ttu-id="d3e25-611">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-611">16</span></span> |<span data-ttu-id="d3e25-612">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-612">16</span></span> |<span data-ttu-id="d3e25-613">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-613">16</span></span> |
| <span data-ttu-id="d3e25-614">DW500</span><span class="sxs-lookup"><span data-stu-id="d3e25-614">DW500</span></span> | <span data-ttu-id="d3e25-615">20 |</span><span class="sxs-lookup"><span data-stu-id="d3e25-615">20</span></span>| <span data-ttu-id="d3e25-616">20 |</span><span class="sxs-lookup"><span data-stu-id="d3e25-616">20</span></span>| <span data-ttu-id="d3e25-617">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-617">1</span></span>| <span data-ttu-id="d3e25-618">2</span><span class="sxs-lookup"><span data-stu-id="d3e25-618">2</span></span>| <span data-ttu-id="d3e25-619">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-619">4</span></span>| <span data-ttu-id="d3e25-620">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-620">8</span></span>| <span data-ttu-id="d3e25-621">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-621">16</span></span>| <span data-ttu-id="d3e25-622">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-622">16</span></span>| <span data-ttu-id="d3e25-623">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-623">16</span></span>| <span data-ttu-id="d3e25-624">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-624">16</span></span>|
| <span data-ttu-id="d3e25-625">DW600</span><span class="sxs-lookup"><span data-stu-id="d3e25-625">DW600</span></span> | <span data-ttu-id="d3e25-626">24</span><span class="sxs-lookup"><span data-stu-id="d3e25-626">24</span></span>| <span data-ttu-id="d3e25-627">24</span><span class="sxs-lookup"><span data-stu-id="d3e25-627">24</span></span>| <span data-ttu-id="d3e25-628">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-628">1</span></span>| <span data-ttu-id="d3e25-629">2</span><span class="sxs-lookup"><span data-stu-id="d3e25-629">2</span></span>| <span data-ttu-id="d3e25-630">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-630">4</span></span>| <span data-ttu-id="d3e25-631">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-631">8</span></span>| <span data-ttu-id="d3e25-632">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-632">16</span></span>| <span data-ttu-id="d3e25-633">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-633">16</span></span>| <span data-ttu-id="d3e25-634">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-634">16</span></span>| <span data-ttu-id="d3e25-635">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-635">16</span></span>|
| <span data-ttu-id="d3e25-636">DW1000</span><span class="sxs-lookup"><span data-stu-id="d3e25-636">DW1000</span></span> | <span data-ttu-id="d3e25-637">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-637">32</span></span>| <span data-ttu-id="d3e25-638">40</span><span class="sxs-lookup"><span data-stu-id="d3e25-638">40</span></span>| <span data-ttu-id="d3e25-639">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-639">1</span></span>| <span data-ttu-id="d3e25-640">2</span><span class="sxs-lookup"><span data-stu-id="d3e25-640">2</span></span>| <span data-ttu-id="d3e25-641">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-641">4</span></span>| <span data-ttu-id="d3e25-642">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-642">8</span></span>| <span data-ttu-id="d3e25-643">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-643">16</span></span>| <span data-ttu-id="d3e25-644">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-644">32</span></span>| <span data-ttu-id="d3e25-645">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-645">32</span></span>| <span data-ttu-id="d3e25-646">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-646">32</span></span>|
| <span data-ttu-id="d3e25-647">DW1200</span><span class="sxs-lookup"><span data-stu-id="d3e25-647">DW1200</span></span> | <span data-ttu-id="d3e25-648">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-648">32</span></span>| <span data-ttu-id="d3e25-649">48</span><span class="sxs-lookup"><span data-stu-id="d3e25-649">48</span></span>| <span data-ttu-id="d3e25-650">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-650">1</span></span>| <span data-ttu-id="d3e25-651">2</span><span class="sxs-lookup"><span data-stu-id="d3e25-651">2</span></span>| <span data-ttu-id="d3e25-652">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-652">4</span></span>| <span data-ttu-id="d3e25-653">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-653">8</span></span>| <span data-ttu-id="d3e25-654">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-654">16</span></span>| <span data-ttu-id="d3e25-655">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-655">32</span></span>| <span data-ttu-id="d3e25-656">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-656">32</span></span>| <span data-ttu-id="d3e25-657">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-657">32</span></span>|
| <span data-ttu-id="d3e25-658">DW1500</span><span class="sxs-lookup"><span data-stu-id="d3e25-658">DW1500</span></span> | <span data-ttu-id="d3e25-659">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-659">32</span></span>| <span data-ttu-id="d3e25-660">60</span><span class="sxs-lookup"><span data-stu-id="d3e25-660">60</span></span>| <span data-ttu-id="d3e25-661">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-661">1</span></span>| <span data-ttu-id="d3e25-662">2</span><span class="sxs-lookup"><span data-stu-id="d3e25-662">2</span></span>| <span data-ttu-id="d3e25-663">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-663">4</span></span>| <span data-ttu-id="d3e25-664">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-664">8</span></span>| <span data-ttu-id="d3e25-665">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-665">16</span></span>| <span data-ttu-id="d3e25-666">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-666">32</span></span>| <span data-ttu-id="d3e25-667">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-667">32</span></span>| <span data-ttu-id="d3e25-668">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-668">32</span></span>|
| <span data-ttu-id="d3e25-669">DW2000</span><span class="sxs-lookup"><span data-stu-id="d3e25-669">DW2000</span></span> | <span data-ttu-id="d3e25-670">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-670">32</span></span>| <span data-ttu-id="d3e25-671">80</span><span class="sxs-lookup"><span data-stu-id="d3e25-671">80</span></span>| <span data-ttu-id="d3e25-672">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-672">1</span></span>| <span data-ttu-id="d3e25-673">2</span><span class="sxs-lookup"><span data-stu-id="d3e25-673">2</span></span>| <span data-ttu-id="d3e25-674">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-674">4</span></span>| <span data-ttu-id="d3e25-675">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-675">8</span></span>| <span data-ttu-id="d3e25-676">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-676">16</span></span>| <span data-ttu-id="d3e25-677">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-677">32</span></span>| <span data-ttu-id="d3e25-678">64</span><span class="sxs-lookup"><span data-stu-id="d3e25-678">64</span></span>| <span data-ttu-id="d3e25-679">64</span><span class="sxs-lookup"><span data-stu-id="d3e25-679">64</span></span>|
| <span data-ttu-id="d3e25-680">DW3000</span><span class="sxs-lookup"><span data-stu-id="d3e25-680">DW3000</span></span> | <span data-ttu-id="d3e25-681">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-681">32</span></span>| <span data-ttu-id="d3e25-682">120</span><span class="sxs-lookup"><span data-stu-id="d3e25-682">120</span></span>| <span data-ttu-id="d3e25-683">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-683">1</span></span>| <span data-ttu-id="d3e25-684">2</span><span class="sxs-lookup"><span data-stu-id="d3e25-684">2</span></span>| <span data-ttu-id="d3e25-685">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-685">4</span></span>| <span data-ttu-id="d3e25-686">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-686">8</span></span>| <span data-ttu-id="d3e25-687">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-687">16</span></span>| <span data-ttu-id="d3e25-688">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-688">32</span></span>| <span data-ttu-id="d3e25-689">64</span><span class="sxs-lookup"><span data-stu-id="d3e25-689">64</span></span>| <span data-ttu-id="d3e25-690">64</span><span class="sxs-lookup"><span data-stu-id="d3e25-690">64</span></span>|
| <span data-ttu-id="d3e25-691">DW6000</span><span class="sxs-lookup"><span data-stu-id="d3e25-691">DW6000</span></span> | <span data-ttu-id="d3e25-692">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-692">32</span></span>| <span data-ttu-id="d3e25-693">240</span><span class="sxs-lookup"><span data-stu-id="d3e25-693">240</span></span>| <span data-ttu-id="d3e25-694">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-694">1</span></span>| <span data-ttu-id="d3e25-695">2</span><span class="sxs-lookup"><span data-stu-id="d3e25-695">2</span></span>| <span data-ttu-id="d3e25-696">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-696">4</span></span>| <span data-ttu-id="d3e25-697">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-697">8</span></span>| <span data-ttu-id="d3e25-698">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-698">16</span></span>| <span data-ttu-id="d3e25-699">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-699">32</span></span>| <span data-ttu-id="d3e25-700">64</span><span class="sxs-lookup"><span data-stu-id="d3e25-700">64</span></span>| <span data-ttu-id="d3e25-701">128</span><span class="sxs-lookup"><span data-stu-id="d3e25-701">128</span></span>|

<span data-ttu-id="d3e25-702">En esta tabla, puede ver que SQL Data Warehouse, que se ejecuta como DW1000, ofrece 32 consultas simultáneas como máximo y 40 ranuras de simultaneidad en total.</span><span class="sxs-lookup"><span data-stu-id="d3e25-702">From these tables, you can see that SQL Data Warehouse running as DW1000 allocates a maximum of 32 concurrent queries and a total of 40 concurrency slots.</span></span> <span data-ttu-id="d3e25-703">Si todos los usuarios se ejecutan en la clase smallrc, se permitirían 32 consultas simultáneas, ya que cada una consumiría 1 espacio de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="d3e25-703">If all users are running in smallrc, 32 concurrent queries would be allowed because each query would consume 1 concurrency slot.</span></span> <span data-ttu-id="d3e25-704">Si todos los usuarios en un DW1000 se estaban ejecutando en mediumrc, cada consulta se asignaría 800 MB por la distribución para una asignación de memoria total de 47 GB por cada consulta y simultaneidad sería too5 limitado a los usuarios (40 ranuras de simultaneidad 8 ranuras disponibles por usuario mediumrc).</span><span class="sxs-lookup"><span data-stu-id="d3e25-704">If all users on a DW1000 were running in mediumrc, each query would be allocated 800 MB per distribution for a total memory allocation of 47 GB per query, and concurrency would be limited too5 users (40 concurrency slots / 8 slots per mediumrc user).</span></span>

## <a name="selecting-proper-resource-class"></a><span data-ttu-id="d3e25-705">Selección de la clase de recurso correcta</span><span class="sxs-lookup"><span data-stu-id="d3e25-705">Selecting proper resource class</span></span>  
<span data-ttu-id="d3e25-706">Clase de recursos de tooa de toopermanently asignar los usuarios, en lugar de cambiar sus clases de recursos, es una práctica recomendada.</span><span class="sxs-lookup"><span data-stu-id="d3e25-706">A good practice is toopermanently assign users tooa resource class rather than changing their resource classes.</span></span> <span data-ttu-id="d3e25-707">Por ejemplo, tablas de almacén de columnas de carga tooclustered crear índices de mayor calidad al asignar más memoria.</span><span class="sxs-lookup"><span data-stu-id="d3e25-707">For example, loads tooclustered columnstore tables create higher-quality indexes when allocated more memory.</span></span> <span data-ttu-id="d3e25-708">tooensure que carga tiene acceso toohigher memoria, cree un usuario específico para cargar datos y asigna de forma permanente esta clase de recurso de usuario tooa superior.</span><span class="sxs-lookup"><span data-stu-id="d3e25-708">tooensure that loads have access toohigher memory, create a user specifically for loading data and permanently assign this user tooa higher resource class.</span></span>
<span data-ttu-id="d3e25-709">Hay un par de toofollow de prácticas recomendada aquí.</span><span class="sxs-lookup"><span data-stu-id="d3e25-709">There are a couple of best practices toofollow here.</span></span> <span data-ttu-id="d3e25-710">Como se mencionó anteriormente, SQL DW admite dos tipos de clase de recurso: estáticos y dinámicos.</span><span class="sxs-lookup"><span data-stu-id="d3e25-710">As mentioned above, SQL DW supports two kinds of resource class types: static resource classes and dynamic resource classes.</span></span>
### <a name="loading-best-practices"></a><span data-ttu-id="d3e25-711">Carga de procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="d3e25-711">Loading best practices</span></span>
1.  <span data-ttu-id="d3e25-712">Si las expectativas de hello son cargas regulares cantidad de datos, una clase de recurso estático es una buena elección.</span><span class="sxs-lookup"><span data-stu-id="d3e25-712">If hello expectations are loads with regular amount of data, a static resource class is a good choice.</span></span> <span data-ttu-id="d3e25-713">Más adelante, cuando tooget el escalado más potencia de cálculo, almacenamiento de datos de hello podrán toorun más simultánea consulta out-of-the-box, como usuario de la carga de hello no consume más memoria.</span><span class="sxs-lookup"><span data-stu-id="d3e25-713">Later, when scaling up tooget more computational power, hello data warehouse will be able toorun more concurrent queries out-of-the-box, as hello load user does not consume more memory.</span></span>
2.  <span data-ttu-id="d3e25-714">Si las expectativas de hello son mayores cargas en algunas ocasiones, una clase de recurso dinámico es una buena elección.</span><span class="sxs-lookup"><span data-stu-id="d3e25-714">If hello expectations are bigger loads in some occasions, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="d3e25-715">Más adelante, cuando se escala ascendentemente tooget más potencia de cálculo, Hola carga usuario obtendrá más memoria out-of-the-box, por lo tanto, lo que permite Hola carga tooperform con mayor rapidez.</span><span class="sxs-lookup"><span data-stu-id="d3e25-715">Later, when scaling up tooget more computational power, hello load user will get more memory out-of-the-box, hence allowing hello load tooperform faster.</span></span>

<span data-ttu-id="d3e25-716">Hello memoria necesaria tooprocess cargas eficazmente depende Hola naturaleza de tabla Hola cargado y cantidad de Hola de procesamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="d3e25-716">hello memory needed tooprocess loads efficiently depends on hello nature of hello table loaded and hello amount of data processed.</span></span> <span data-ttu-id="d3e25-717">Por ejemplo, cargar datos en tablas CCI requiere que algunos grupos de filas de memoria toolet CCI alcanzar estado óptimo.</span><span class="sxs-lookup"><span data-stu-id="d3e25-717">For instance, loading data into CCI tables requires some memory toolet CCI rowgroups reach optimality.</span></span> <span data-ttu-id="d3e25-718">Para obtener más información, vea índices de almacén de columnas de hello - Guía de la carga de datos.</span><span class="sxs-lookup"><span data-stu-id="d3e25-718">For more details, see hello Columnstore indexes - data loading guidance.</span></span>

<span data-ttu-id="d3e25-719">Como práctica recomendada, se aconseja toouse como mínimo 200MB de memoria para las cargas.</span><span class="sxs-lookup"><span data-stu-id="d3e25-719">As a best practice, we advise you toouse at least 200MB of memory for loads.</span></span>

### <a name="querying-best-practices"></a><span data-ttu-id="d3e25-720">Procedimientos recomendados sobre las consultas</span><span class="sxs-lookup"><span data-stu-id="d3e25-720">Querying best practices</span></span>
<span data-ttu-id="d3e25-721">Las consultas tienen requisitos diferentes en función de su complejidad.</span><span class="sxs-lookup"><span data-stu-id="d3e25-721">Queries have different requirements depending on their complexity.</span></span> <span data-ttu-id="d3e25-722">El aumento de memoria por consulta o aumentar la simultaneidad de hello son ambos métodos válidos tooaugment rendimiento global en función de las necesidades de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3e25-722">Increasing memory per query or increasing hello concurrency are both valid ways tooaugment overall throughput depending on hello query needs.</span></span>
1.  <span data-ttu-id="d3e25-723">Si las expectativas de hello son consultas normales y complejas (por ejemplo, toogenerate informes diarios y semanales) y no es necesario tootake ventajas de simultaneidad, una clase de recurso dinámico es una buena elección.</span><span class="sxs-lookup"><span data-stu-id="d3e25-723">If hello expectations are regular, complex queries (for instance, toogenerate daily and weekly reports) and do not need tootake advantage of concurrency, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="d3e25-724">Si el sistema de hello tiene más tooprocess de datos, escalar verticalmente el almacenamiento de datos de hello, por tanto, proporcionará automáticamente más ejecutando Hola consulta de usuario de toohello de la memoria.</span><span class="sxs-lookup"><span data-stu-id="d3e25-724">If hello system has more data tooprocess, scaling up hello data warehouse will therefore automatically provide more memory toohello user running hello query.</span></span>
2.  <span data-ttu-id="d3e25-725">Si las expectativas de Hola son modelos de simultaneidad de variable o diurna (por ejemplo si se consulta la base de datos de Hola a través de un sitio web ampliamente accesible de la interfaz de usuario), una clase de recurso estático es una buena elección.</span><span class="sxs-lookup"><span data-stu-id="d3e25-725">If hello expectations are variable or diurnal concurrency patterns (for instance if hello database is queried through a web UI broadly accessible), a static resource class is a good choice.</span></span> <span data-ttu-id="d3e25-726">Más adelante, cuando se escala ascendentemente toodata almacenamiento, usuario Hola asociado con la clase de recurso estático Hola configurará automáticamente y ser capaz de toorun consultas más simultáneas.</span><span class="sxs-lookup"><span data-stu-id="d3e25-726">Later, when scaling up toodata warehouse, hello user associated with hello static resource class will automatically be able toorun more concurrent queries.</span></span>

<span data-ttu-id="d3e25-727">Selección de concesión de memoria adecuada según la necesidad de saludo de la consulta no es trivial, ya que depende de muchos factores, como la cantidad de Hola de datos consultados, naturaleza Hola de esquemas de tabla de hello y combinación de varios, selección y predicados de grupo.</span><span class="sxs-lookup"><span data-stu-id="d3e25-727">Selecting proper memory grant depending on hello need of your query is non-trivial, as it depends on many factors, such as hello amount of data queried, hello nature of hello table schemas, and various join, selection, and group predicates.</span></span> <span data-ttu-id="d3e25-728">Desde la perspectiva general, asignar más memoria le permitirá toocomplete de consultas más rápido, pero se reduciría Hola simultaneidad general.</span><span class="sxs-lookup"><span data-stu-id="d3e25-728">From a general standpoint, allocating more memory will allow queries toocomplete faster, but would reduce hello overall concurrency.</span></span> <span data-ttu-id="d3e25-729">Si la simultaneidad no es un problema, asignar una cantidad de memoria mayor de la necesaria no resulta perjudicial.</span><span class="sxs-lookup"><span data-stu-id="d3e25-729">If concurrency is not an issue, over-allocating memory does not harm.</span></span> <span data-ttu-id="d3e25-730">toofine optimizar el rendimiento, tratando de distintas versiones de las clases de recursos puede ser necesario.</span><span class="sxs-lookup"><span data-stu-id="d3e25-730">toofine-tune throughput, trying various flavors of resource classes may be required.</span></span>

<span data-ttu-id="d3e25-731">Puede usar los siguientes Hola almacenados toofigure procedimiento espera de concesión de memoria y simultaneidad por clase de recurso en un determinado hello y SLO clase más cercana mejor recurso para operaciones de CCI intensivo de memoria en la tabla CCI sin particiones en una clase de recurso determinado:</span><span class="sxs-lookup"><span data-stu-id="d3e25-731">You can use hello following stored procedure toofigure out concurrency and memory grant per resource class at a given SLO and hello closest best resource class for memory intensive CCI operations on non-partitioned CCI table at a given resource class:</span></span>

#### <a name="description"></a><span data-ttu-id="d3e25-732">Description:</span><span class="sxs-lookup"><span data-stu-id="d3e25-732">Description:</span></span>  
<span data-ttu-id="d3e25-733">Este es el propósito de Hola de este procedimiento almacenado:</span><span class="sxs-lookup"><span data-stu-id="d3e25-733">Here's hello purpose of this stored procedure:</span></span>  
1. <span data-ttu-id="d3e25-734">toohelp usuario averiguar grant de simultaneidad y la memoria por clase de recurso en un objetivo determinado.</span><span class="sxs-lookup"><span data-stu-id="d3e25-734">toohelp user figure out concurrency and memory grant per resource class at a given SLO.</span></span> <span data-ttu-id="d3e25-735">Usuario necesita tooprovide NULL para el esquema y nombre de tabla para este tal y como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3e25-735">User needs tooprovide NULL for both schema and tablename for this as shown in hello example below.</span></span>  
2. <span data-ttu-id="d3e25-736">toohelp usuario averiguar más cercano clase de recurso Hola recomendada para hello memoria intensed operaciones de CCI (carga, tabla de copia, volver a generar índice, etc.) en una tabla con particiones no de CCI a una clase de recurso determinado.</span><span class="sxs-lookup"><span data-stu-id="d3e25-736">toohelp user figure out hello closest best resource class for hello memory intensed CCI operations (load, copy table, rebuild index, etc.) on non partitioned CCI table at a given resource class.</span></span> <span data-ttu-id="d3e25-737">Hola almacenado proc utiliza toofind del esquema de tabla out Hola concesión de memoria necesaria para este.</span><span class="sxs-lookup"><span data-stu-id="d3e25-737">hello stored proc uses table schema toofind out hello required memory grant for this.</span></span>

#### <a name="dependencies--restrictions"></a><span data-ttu-id="d3e25-738">Dependencias y restricciones:</span><span class="sxs-lookup"><span data-stu-id="d3e25-738">Dependencies & Restrictions:</span></span>
- <span data-ttu-id="d3e25-739">Este procedimiento almacenado no es requisito de memoria de toocalculate diseñada para la tabla de particiones de cci.</span><span class="sxs-lookup"><span data-stu-id="d3e25-739">This stored proc is not designed toocalculate memory requirement for partitioned-cci table.</span></span>    
- <span data-ttu-id="d3e25-740">Este procedimiento almacenado no tiene requisitos de memoria en la cuenta de la parte SELECT de Hola de CTAS/INSERT-SELECT y se da por supuesto toobe una instrucción SELECT simple.</span><span class="sxs-lookup"><span data-stu-id="d3e25-740">This stored proc doesn't take memory requirement into account for hello SELECT part of CTAS/INSERT-SELECT and assumes it toobe a simple SELECT.</span></span>
- <span data-ttu-id="d3e25-741">Este procedimiento almacenado utiliza una tabla temporal, por lo que se puede utilizar en la sesión de Hola donde se creó este procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="d3e25-741">This stored proc uses a temp table so this can be used in hello session where this stored proc was created.</span></span>    
- <span data-ttu-id="d3e25-742">Este procedimiento almacenado depende de ofertas actuales de hello (por ejemplo, configuración de hardware, configuración DMS) y si alguno de los cambia, a continuación, este procedimiento almacenado no funcionará correctamente.</span><span class="sxs-lookup"><span data-stu-id="d3e25-742">This stored proc depends on hello current offerings (e.g. hardware configuration, DMS config) and if any of that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="d3e25-743">Este procedimiento almacenado depende del límite de simultaneidad ofrecido actualmente y, si este cambiara, no funcionaría correctamente.</span><span class="sxs-lookup"><span data-stu-id="d3e25-743">This stored proc depends on existing offered concurrency limit and if that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="d3e25-744">Este procedimiento almacenado depende de las ofertas de clase de recursos actuales y, si estas cambiaran, no funcionaría correctamente.</span><span class="sxs-lookup"><span data-stu-id="d3e25-744">This stored proc depends on existing resource class offerings and if that changes then this stored proc wuold not work correctly.</span></span>  

>  [!NOTE]  
>  <span data-ttu-id="d3e25-745">Si no se obtienen resultados después de ejecutar el procedimiento almacenado con los parámetros proporcionados, podrían darse dos circunstancias.</span><span class="sxs-lookup"><span data-stu-id="d3e25-745">If you are not getting output after executing stored procedure with parameters provided then there could be two cases.</span></span> <br /><span data-ttu-id="d3e25-746">1. Algún parámetro del almacenamiento de datos contiene un valor de SLO no válido</span><span class="sxs-lookup"><span data-stu-id="d3e25-746">1. Either DW Parameter contains invalid SLO value</span></span> <br /><span data-ttu-id="d3e25-747">2. O bien, no hay ninguna clase de recursos coincidente para la operación CCI, si se proporcionó el nombre de la tabla.</span><span class="sxs-lookup"><span data-stu-id="d3e25-747">2. OR there are no matching resource class for CCI operation if table name was provided.</span></span> <br /><span data-ttu-id="d3e25-748">Por ejemplo, en DW100, concesión de memoria máxima disponible es 400MB y si el esquema de tabla es extensa suficiente toocross Hola requisito de 400MB.</span><span class="sxs-lookup"><span data-stu-id="d3e25-748">For example, at DW100, highest memory grant available is 400MB and if table schema is wide enough toocross hello requirement of 400MB.</span></span>
      
#### <a name="usage-example"></a><span data-ttu-id="d3e25-749">Ejemplo de uso:</span><span class="sxs-lookup"><span data-stu-id="d3e25-749">Usage example:</span></span>
<span data-ttu-id="d3e25-750">Sintaxis:</span><span class="sxs-lookup"><span data-stu-id="d3e25-750">Syntax:</span></span>  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. <span data-ttu-id="d3e25-751">@DWU:Escriba un tooextract de parámetro NULL Hola DWU actual de hello DW DB o proporcionar cualquier admitido DWU en forma de Hola de 'DW100'</span><span class="sxs-lookup"><span data-stu-id="d3e25-751">@DWU: Either provide a NULL parameter tooextract hello current DWU from hello DW DB or provide any supported DWU in hello form of 'DW100'</span></span>
2. <span data-ttu-id="d3e25-752">@SCHEMA_NAME:Proporcione un nombre de esquema de tabla de Hola</span><span class="sxs-lookup"><span data-stu-id="d3e25-752">@SCHEMA_NAME: Provide a schema name of hello table</span></span>
3. <span data-ttu-id="d3e25-753">@TABLE_NAME:Proporcione un nombre de tabla de interés de Hola</span><span class="sxs-lookup"><span data-stu-id="d3e25-753">@TABLE_NAME: Provide a table name of hello interest</span></span>

<span data-ttu-id="d3e25-754">Ejemplos de ejecución de este procedimiento almacenado:</span><span class="sxs-lookup"><span data-stu-id="d3e25-754">Examples executing this stored proc:</span></span>  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

<span data-ttu-id="d3e25-755">Table1 usa Hola por encima de los ejemplos se pudo crear como sigue:</span><span class="sxs-lookup"><span data-stu-id="d3e25-755">Table1 used in hello above examples could be created as below:</span></span>  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-hello-stored-procedure-definition"></a><span data-ttu-id="d3e25-756">Esta es la definición del procedimiento almacenado de hello:</span><span class="sxs-lookup"><span data-stu-id="d3e25-756">Here's hello stored procedure definition:</span></span>
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
-- Selecting proper DWU for hello current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need toosupply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) toohold mapping info.
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
-- Creating workload mapping tootheir corresponding slot consumption and default memory grant.
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

## <a name="query-importance"></a><span data-ttu-id="d3e25-757">Importancia de las consultas</span><span class="sxs-lookup"><span data-stu-id="d3e25-757">Query importance</span></span>
<span data-ttu-id="d3e25-758">Almacenamiento de datos SQL implementa las clases de recursos mediante el uso de grupos de cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="d3e25-758">SQL Data Warehouse implements resource classes by using workload groups.</span></span> <span data-ttu-id="d3e25-759">Hay un total de ocho grupos de cargas de trabajo que controlan el comportamiento de Hola de clases de recursos de hello en hello diversos tamaños de unidad.</span><span class="sxs-lookup"><span data-stu-id="d3e25-759">There are a total of eight workload groups that control hello behavior of hello resource classes across hello various DWU sizes.</span></span> <span data-ttu-id="d3e25-760">Para cualquier unidad, almacenamiento de datos SQL usa solo cuatro de ocho grupos de cargas de trabajo Hola.</span><span class="sxs-lookup"><span data-stu-id="d3e25-760">For any DWU, SQL Data Warehouse uses only four of hello eight workload groups.</span></span> <span data-ttu-id="d3e25-761">Esto tiene sentido porque se asigna cada grupo de cargas de trabajo tooone de cuatro clases de recursos: smallrc, mediumrc, largerc, o xlargerc.</span><span class="sxs-lookup"><span data-stu-id="d3e25-761">This makes sense because each workload group is assigned tooone of four resource classes: smallrc, mediumrc, largerc, or xlargerc.</span></span> <span data-ttu-id="d3e25-762">Hello importancia de la descripción de los grupos de cargas de trabajo de hello es que algunos de estos grupos de cargas de trabajo se establecen toohigher *importancia*.</span><span class="sxs-lookup"><span data-stu-id="d3e25-762">hello importance of understanding hello workload groups is that some of these workload groups are set toohigher *importance*.</span></span> <span data-ttu-id="d3e25-763">El nivel de importancia se usa para la programación de la CPU.</span><span class="sxs-lookup"><span data-stu-id="d3e25-763">Importance is used for CPU scheduling.</span></span> <span data-ttu-id="d3e25-764">Las consultas que se ejecutan con importancia alta obtendrán tres veces más ciclos de CPU que aquellas con importancia media.</span><span class="sxs-lookup"><span data-stu-id="d3e25-764">Queries run with high importance will get three times more CPU cycles than those with medium importance.</span></span> <span data-ttu-id="d3e25-765">Por lo tanto, las asignaciones de espacio de simultaneidad también determinan la prioridad en la CPU.</span><span class="sxs-lookup"><span data-stu-id="d3e25-765">Therefore, concurrency slot mappings also determine CPU priority.</span></span> <span data-ttu-id="d3e25-766">Si una consulta utiliza 16 o más espacios, se ejecuta con importancia alta.</span><span class="sxs-lookup"><span data-stu-id="d3e25-766">When a query consumes 16 or more slots, it runs as high importance.</span></span>

<span data-ttu-id="d3e25-767">Hello tabla siguiente muestran las asignaciones de importancia de Hola para cada grupo de cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="d3e25-767">hello following table shows hello importance mappings for each workload group.</span></span>

### <a name="workload-group-mappings-tooconcurrency-slots-and-importance"></a><span data-ttu-id="d3e25-768">Importancia y ranuras de tooconcurrency de asignaciones de grupo de cargas de trabajo</span><span class="sxs-lookup"><span data-stu-id="d3e25-768">Workload group mappings tooconcurrency slots and importance</span></span>
| <span data-ttu-id="d3e25-769">Grupos de carga de trabajo</span><span class="sxs-lookup"><span data-stu-id="d3e25-769">Workload groups</span></span> | <span data-ttu-id="d3e25-770">Asignación de espacio de simultaneidad</span><span class="sxs-lookup"><span data-stu-id="d3e25-770">Concurrency slot mapping</span></span> | <span data-ttu-id="d3e25-771">MB/Distribución</span><span class="sxs-lookup"><span data-stu-id="d3e25-771">MB / Distribution</span></span> | <span data-ttu-id="d3e25-772">Asignación de importancia</span><span class="sxs-lookup"><span data-stu-id="d3e25-772">Importance mapping</span></span> |
|:--- |:---:|:---:|:--- |
| <span data-ttu-id="d3e25-773">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="d3e25-773">SloDWGroupC00</span></span> |<span data-ttu-id="d3e25-774">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-774">1</span></span> |<span data-ttu-id="d3e25-775">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-775">100</span></span> |<span data-ttu-id="d3e25-776">Mediano</span><span class="sxs-lookup"><span data-stu-id="d3e25-776">Medium</span></span> |
| <span data-ttu-id="d3e25-777">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="d3e25-777">SloDWGroupC01</span></span> |<span data-ttu-id="d3e25-778">2</span><span class="sxs-lookup"><span data-stu-id="d3e25-778">2</span></span> |<span data-ttu-id="d3e25-779">200</span><span class="sxs-lookup"><span data-stu-id="d3e25-779">200</span></span> |<span data-ttu-id="d3e25-780">Mediano</span><span class="sxs-lookup"><span data-stu-id="d3e25-780">Medium</span></span> |
| <span data-ttu-id="d3e25-781">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="d3e25-781">SloDWGroupC02</span></span> |<span data-ttu-id="d3e25-782">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-782">4</span></span> |<span data-ttu-id="d3e25-783">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-783">400</span></span> |<span data-ttu-id="d3e25-784">Mediano</span><span class="sxs-lookup"><span data-stu-id="d3e25-784">Medium</span></span> |
| <span data-ttu-id="d3e25-785">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="d3e25-785">SloDWGroupC03</span></span> |<span data-ttu-id="d3e25-786">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-786">8</span></span> |<span data-ttu-id="d3e25-787">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-787">800</span></span> |<span data-ttu-id="d3e25-788">Mediano</span><span class="sxs-lookup"><span data-stu-id="d3e25-788">Medium</span></span> |
| <span data-ttu-id="d3e25-789">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="d3e25-789">SloDWGroupC04</span></span> |<span data-ttu-id="d3e25-790">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-790">16</span></span> |<span data-ttu-id="d3e25-791">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-791">1,600</span></span> |<span data-ttu-id="d3e25-792">Alto</span><span class="sxs-lookup"><span data-stu-id="d3e25-792">High</span></span> |
| <span data-ttu-id="d3e25-793">SloDWGroupC05</span><span class="sxs-lookup"><span data-stu-id="d3e25-793">SloDWGroupC05</span></span> |<span data-ttu-id="d3e25-794">32</span><span class="sxs-lookup"><span data-stu-id="d3e25-794">32</span></span> |<span data-ttu-id="d3e25-795">3.200</span><span class="sxs-lookup"><span data-stu-id="d3e25-795">3,200</span></span> |<span data-ttu-id="d3e25-796">Alto</span><span class="sxs-lookup"><span data-stu-id="d3e25-796">High</span></span> |
| <span data-ttu-id="d3e25-797">SloDWGroupC06</span><span class="sxs-lookup"><span data-stu-id="d3e25-797">SloDWGroupC06</span></span> |<span data-ttu-id="d3e25-798">64</span><span class="sxs-lookup"><span data-stu-id="d3e25-798">64</span></span> |<span data-ttu-id="d3e25-799">6.400</span><span class="sxs-lookup"><span data-stu-id="d3e25-799">6,400</span></span> |<span data-ttu-id="d3e25-800">Alto</span><span class="sxs-lookup"><span data-stu-id="d3e25-800">High</span></span> |
| <span data-ttu-id="d3e25-801">SloDWGroupC07</span><span class="sxs-lookup"><span data-stu-id="d3e25-801">SloDWGroupC07</span></span> |<span data-ttu-id="d3e25-802">128</span><span class="sxs-lookup"><span data-stu-id="d3e25-802">128</span></span> |<span data-ttu-id="d3e25-803">12.800</span><span class="sxs-lookup"><span data-stu-id="d3e25-803">12,800</span></span> |<span data-ttu-id="d3e25-804">Alto</span><span class="sxs-lookup"><span data-stu-id="d3e25-804">High</span></span> |

<span data-ttu-id="d3e25-805">De hello **asignación y el consumo de ranuras de simultaneidad** gráfico, puede ver que una DW500 usa 1, 4, 8 o ranuras de simultaneidad 16 para smallrc, mediumrc, largerc y xlargerc, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="d3e25-805">From hello **Allocation and consumption of concurrency slots** chart, you can see that a DW500 uses 1, 4, 8 or 16 concurrency slots for smallrc, mediumrc, largerc, and xlargerc, respectively.</span></span> <span data-ttu-id="d3e25-806">Puede buscar esos valores en hello anterior importancia de hello toofind de gráfico para cada clase de recursos.</span><span class="sxs-lookup"><span data-stu-id="d3e25-806">You can look those values up in hello preceding chart toofind hello importance for each resource class.</span></span>

### <a name="dw500-mapping-of-resource-classes-tooimportance"></a><span data-ttu-id="d3e25-807">Asignación de DW500 de tooimportance de clases de recursos</span><span class="sxs-lookup"><span data-stu-id="d3e25-807">DW500 mapping of resource classes tooimportance</span></span>
| <span data-ttu-id="d3e25-808">clase de recursos</span><span class="sxs-lookup"><span data-stu-id="d3e25-808">Resource class</span></span> | <span data-ttu-id="d3e25-809">Grupo de cargas de trabajo</span><span class="sxs-lookup"><span data-stu-id="d3e25-809">Workload group</span></span> | <span data-ttu-id="d3e25-810">Espacios de simultaneidad usados</span><span class="sxs-lookup"><span data-stu-id="d3e25-810">Concurrency slots used</span></span> | <span data-ttu-id="d3e25-811">MB/Distribución</span><span class="sxs-lookup"><span data-stu-id="d3e25-811">MB / Distribution</span></span> | <span data-ttu-id="d3e25-812">importancia</span><span class="sxs-lookup"><span data-stu-id="d3e25-812">Importance</span></span> |
|:--- |:--- |:---:|:---:|:--- |
| <span data-ttu-id="d3e25-813">smallrc</span><span class="sxs-lookup"><span data-stu-id="d3e25-813">smallrc</span></span> |<span data-ttu-id="d3e25-814">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="d3e25-814">SloDWGroupC00</span></span> |<span data-ttu-id="d3e25-815">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-815">1</span></span> |<span data-ttu-id="d3e25-816">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-816">100</span></span> |<span data-ttu-id="d3e25-817">Mediano</span><span class="sxs-lookup"><span data-stu-id="d3e25-817">Medium</span></span> |
| <span data-ttu-id="d3e25-818">mediumrc</span><span class="sxs-lookup"><span data-stu-id="d3e25-818">mediumrc</span></span> |<span data-ttu-id="d3e25-819">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="d3e25-819">SloDWGroupC02</span></span> |<span data-ttu-id="d3e25-820">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-820">4</span></span> |<span data-ttu-id="d3e25-821">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-821">400</span></span> |<span data-ttu-id="d3e25-822">Mediano</span><span class="sxs-lookup"><span data-stu-id="d3e25-822">Medium</span></span> |
| <span data-ttu-id="d3e25-823">largerc</span><span class="sxs-lookup"><span data-stu-id="d3e25-823">largerc</span></span> |<span data-ttu-id="d3e25-824">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="d3e25-824">SloDWGroupC03</span></span> |<span data-ttu-id="d3e25-825">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-825">8</span></span> |<span data-ttu-id="d3e25-826">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-826">800</span></span> |<span data-ttu-id="d3e25-827">Mediano</span><span class="sxs-lookup"><span data-stu-id="d3e25-827">Medium</span></span> |
| <span data-ttu-id="d3e25-828">xlargerc</span><span class="sxs-lookup"><span data-stu-id="d3e25-828">xlargerc</span></span> |<span data-ttu-id="d3e25-829">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="d3e25-829">SloDWGroupC04</span></span> |<span data-ttu-id="d3e25-830">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-830">16</span></span> |<span data-ttu-id="d3e25-831">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-831">1,600</span></span> |<span data-ttu-id="d3e25-832">Alto</span><span class="sxs-lookup"><span data-stu-id="d3e25-832">High</span></span> |
| <span data-ttu-id="d3e25-833">staticrc10</span><span class="sxs-lookup"><span data-stu-id="d3e25-833">staticrc10</span></span> |<span data-ttu-id="d3e25-834">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="d3e25-834">SloDWGroupC00</span></span> |<span data-ttu-id="d3e25-835">1</span><span class="sxs-lookup"><span data-stu-id="d3e25-835">1</span></span> |<span data-ttu-id="d3e25-836">100</span><span class="sxs-lookup"><span data-stu-id="d3e25-836">100</span></span> |<span data-ttu-id="d3e25-837">Mediano</span><span class="sxs-lookup"><span data-stu-id="d3e25-837">Medium</span></span> |
| <span data-ttu-id="d3e25-838">staticrc20</span><span class="sxs-lookup"><span data-stu-id="d3e25-838">staticrc20</span></span> |<span data-ttu-id="d3e25-839">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="d3e25-839">SloDWGroupC01</span></span> |<span data-ttu-id="d3e25-840">2</span><span class="sxs-lookup"><span data-stu-id="d3e25-840">2</span></span> |<span data-ttu-id="d3e25-841">200</span><span class="sxs-lookup"><span data-stu-id="d3e25-841">200</span></span> |<span data-ttu-id="d3e25-842">Mediano</span><span class="sxs-lookup"><span data-stu-id="d3e25-842">Medium</span></span> |
| <span data-ttu-id="d3e25-843">staticrc30</span><span class="sxs-lookup"><span data-stu-id="d3e25-843">staticrc30</span></span> |<span data-ttu-id="d3e25-844">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="d3e25-844">SloDWGroupC02</span></span> |<span data-ttu-id="d3e25-845">4</span><span class="sxs-lookup"><span data-stu-id="d3e25-845">4</span></span> |<span data-ttu-id="d3e25-846">400</span><span class="sxs-lookup"><span data-stu-id="d3e25-846">400</span></span> |<span data-ttu-id="d3e25-847">Mediano</span><span class="sxs-lookup"><span data-stu-id="d3e25-847">Medium</span></span> |
| <span data-ttu-id="d3e25-848">staticrc40</span><span class="sxs-lookup"><span data-stu-id="d3e25-848">staticrc40</span></span> |<span data-ttu-id="d3e25-849">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="d3e25-849">SloDWGroupC03</span></span> |<span data-ttu-id="d3e25-850">8</span><span class="sxs-lookup"><span data-stu-id="d3e25-850">8</span></span> |<span data-ttu-id="d3e25-851">800</span><span class="sxs-lookup"><span data-stu-id="d3e25-851">800</span></span> |<span data-ttu-id="d3e25-852">Mediano</span><span class="sxs-lookup"><span data-stu-id="d3e25-852">Medium</span></span> |
| <span data-ttu-id="d3e25-853">staticrc50</span><span class="sxs-lookup"><span data-stu-id="d3e25-853">staticrc50</span></span> |<span data-ttu-id="d3e25-854">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="d3e25-854">SloDWGroupC03</span></span> |<span data-ttu-id="d3e25-855">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-855">16</span></span> |<span data-ttu-id="d3e25-856">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-856">1,600</span></span> |<span data-ttu-id="d3e25-857">Alto</span><span class="sxs-lookup"><span data-stu-id="d3e25-857">High</span></span> |
| <span data-ttu-id="d3e25-858">staticrc60</span><span class="sxs-lookup"><span data-stu-id="d3e25-858">staticrc60</span></span> |<span data-ttu-id="d3e25-859">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="d3e25-859">SloDWGroupC03</span></span> |<span data-ttu-id="d3e25-860">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-860">16</span></span> |<span data-ttu-id="d3e25-861">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-861">1,600</span></span> |<span data-ttu-id="d3e25-862">Alto</span><span class="sxs-lookup"><span data-stu-id="d3e25-862">High</span></span> |
| <span data-ttu-id="d3e25-863">staticrc70</span><span class="sxs-lookup"><span data-stu-id="d3e25-863">staticrc70</span></span> |<span data-ttu-id="d3e25-864">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="d3e25-864">SloDWGroupC03</span></span> |<span data-ttu-id="d3e25-865">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-865">16</span></span> |<span data-ttu-id="d3e25-866">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-866">1,600</span></span> |<span data-ttu-id="d3e25-867">Alto</span><span class="sxs-lookup"><span data-stu-id="d3e25-867">High</span></span> |
| <span data-ttu-id="d3e25-868">staticrc80</span><span class="sxs-lookup"><span data-stu-id="d3e25-868">staticrc80</span></span> |<span data-ttu-id="d3e25-869">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="d3e25-869">SloDWGroupC03</span></span> |<span data-ttu-id="d3e25-870">16</span><span class="sxs-lookup"><span data-stu-id="d3e25-870">16</span></span> |<span data-ttu-id="d3e25-871">1600</span><span class="sxs-lookup"><span data-stu-id="d3e25-871">1,600</span></span> |<span data-ttu-id="d3e25-872">Alto</span><span class="sxs-lookup"><span data-stu-id="d3e25-872">High</span></span> |

<span data-ttu-id="d3e25-873">Puede usar Hola después toolook de consulta DMV en diferencias de Hola de asignación de recursos de memoria en detalle de perspectiva de hello del regulador de recursos de Hola o el uso activos e históricos tooanalyze de grupos de cargas de trabajo de Hola para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="d3e25-873">You can use hello following DMV query toolook at hello differences in memory resource allocation in detail from hello perspective of hello resource governor, or tooanalyze active and historic usage of hello workload groups when troubleshooting.</span></span>

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

## <a name="queries-that-honor-concurrency-limits"></a><span data-ttu-id="d3e25-874">Consultas que respetan los límites de simultaneidad</span><span class="sxs-lookup"><span data-stu-id="d3e25-874">Queries that honor concurrency limits</span></span>
<span data-ttu-id="d3e25-875">La mayoría de las consultas se rigen por las clases de recursos.</span><span class="sxs-lookup"><span data-stu-id="d3e25-875">Most queries are governed by resource classes.</span></span> <span data-ttu-id="d3e25-876">Estas consultas deben caber dentro de consultas simultáneas de Hola y umbrales de espacio de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="d3e25-876">These queries must fit inside both hello concurrent query and concurrency slot thresholds.</span></span> <span data-ttu-id="d3e25-877">Un usuario no puede elegir tooexclude una consulta de modelo de ranura de simultaneidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3e25-877">A user cannot choose tooexclude a query from hello concurrency slot model.</span></span>

<span data-ttu-id="d3e25-878">tooreiterate, hello instrucciones siguientes respetan las clases de recursos:</span><span class="sxs-lookup"><span data-stu-id="d3e25-878">tooreiterate, hello following statements honor resource classes:</span></span>

* <span data-ttu-id="d3e25-879">INSERT-SELECT</span><span class="sxs-lookup"><span data-stu-id="d3e25-879">INSERT-SELECT</span></span>
* <span data-ttu-id="d3e25-880">UPDATE</span><span class="sxs-lookup"><span data-stu-id="d3e25-880">UPDATE</span></span>
* <span data-ttu-id="d3e25-881">DELETE</span><span class="sxs-lookup"><span data-stu-id="d3e25-881">DELETE</span></span>
* <span data-ttu-id="d3e25-882">SELECT (al consultar las tablas de usuario)</span><span class="sxs-lookup"><span data-stu-id="d3e25-882">SELECT (when querying user tables)</span></span>
* <span data-ttu-id="d3e25-883">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="d3e25-883">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="d3e25-884">ALTER INDEX REORGANIZE</span><span class="sxs-lookup"><span data-stu-id="d3e25-884">ALTER INDEX REORGANIZE</span></span>
* <span data-ttu-id="d3e25-885">ALTER TABLE REBUILD</span><span class="sxs-lookup"><span data-stu-id="d3e25-885">ALTER TABLE REBUILD</span></span>
* <span data-ttu-id="d3e25-886">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="d3e25-886">CREATE INDEX</span></span>
* <span data-ttu-id="d3e25-887">CREATE CLUSTERED COLUMNSTORE INDEX</span><span class="sxs-lookup"><span data-stu-id="d3e25-887">CREATE CLUSTERED COLUMNSTORE INDEX</span></span>
* <span data-ttu-id="d3e25-888">CREATE TABLE AS SELECT (CTAS)</span><span class="sxs-lookup"><span data-stu-id="d3e25-888">CREATE TABLE AS SELECT (CTAS)</span></span>
* <span data-ttu-id="d3e25-889">Carga de datos</span><span class="sxs-lookup"><span data-stu-id="d3e25-889">Data loading</span></span>
* <span data-ttu-id="d3e25-890">Operaciones de movimiento de datos realizadas por hello servicio de movimiento de datos (DMS)</span><span class="sxs-lookup"><span data-stu-id="d3e25-890">Data movement operations conducted by hello Data Movement Service (DMS)</span></span>

## <a name="query-exceptions-tooconcurrency-limits"></a><span data-ttu-id="d3e25-891">Límites de tooconcurrency de excepciones de consulta</span><span class="sxs-lookup"><span data-stu-id="d3e25-891">Query exceptions tooconcurrency limits</span></span>
<span data-ttu-id="d3e25-892">Algunas consultas no respetan los recursos de hello clase toowhich Hola usuario está asignado.</span><span class="sxs-lookup"><span data-stu-id="d3e25-892">Some queries do not honor hello resource class toowhich hello user is assigned.</span></span> <span data-ttu-id="d3e25-893">Estos límites de simultaneidad de las excepciones toohello se realizan cuando Hola memoria necesarios para un determinado comando hay pocos recursos, a menudo como comando hello es una operación de metadatos.</span><span class="sxs-lookup"><span data-stu-id="d3e25-893">These exceptions toohello concurrency limits are made when hello memory resources needed for a particular command are low, often because hello command is a metadata operation.</span></span> <span data-ttu-id="d3e25-894">objetivo de Hola de estas excepciones es tooavoid asignaciones de memoria mayor para las consultas que nunca será necesario.</span><span class="sxs-lookup"><span data-stu-id="d3e25-894">hello goal of these exceptions is tooavoid larger memory allocations for queries that will never need them.</span></span> <span data-ttu-id="d3e25-895">En estos casos, predeterminado Hola siempre se utiliza la clase de recursos pequeño (smallrc), independientemente de la clase de recurso real de hello asignado toohello usuario.</span><span class="sxs-lookup"><span data-stu-id="d3e25-895">In these cases, hello default small resource class (smallrc) is always used regardless of hello actual resource class assigned toohello user.</span></span> <span data-ttu-id="d3e25-896">Por ejemplo, `CREATE LOGIN` se ejecutará siempre en la clase smallrc.</span><span class="sxs-lookup"><span data-stu-id="d3e25-896">For example, `CREATE LOGIN` will always run in smallrc.</span></span> <span data-ttu-id="d3e25-897">Hola recursos necesarios toofulfill esta operación son muy bajo, por lo que no consulta de sentido tooinclude hello en el modelo de ranura de simultaneidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3e25-897">hello resources required toofulfill this operation are very low, so it does not make sense tooinclude hello query in hello concurrency slot model.</span></span>  <span data-ttu-id="d3e25-898">Estas consultas no están también limitadas por límite de simultaneidad de usuarios de hello 32, límite de 1.024 sesiones de toohello sesión puede ejecutar un número ilimitado de estas consultas.</span><span class="sxs-lookup"><span data-stu-id="d3e25-898">These queries are also not limited by hello 32 user concurrency limit, an unlimited number of these queries can run up toohello session limit of 1,024 sessions.</span></span>

<span data-ttu-id="d3e25-899">Hola siguiendo las instrucciones no respeta las clases de recursos:</span><span class="sxs-lookup"><span data-stu-id="d3e25-899">hello following statements do not honor resource classes:</span></span>

* <span data-ttu-id="d3e25-900">CREATE o DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="d3e25-900">CREATE or DROP TABLE</span></span>
* <span data-ttu-id="d3e25-901">ALTER TABLE ... SWITCH, SPLIT o MERGE PARTITION</span><span class="sxs-lookup"><span data-stu-id="d3e25-901">ALTER TABLE ... SWITCH, SPLIT, or MERGE PARTITION</span></span>
* <span data-ttu-id="d3e25-902">ALTER INDEX DISABLE</span><span class="sxs-lookup"><span data-stu-id="d3e25-902">ALTER INDEX DISABLE</span></span>
* <span data-ttu-id="d3e25-903">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="d3e25-903">DROP INDEX</span></span>
* <span data-ttu-id="d3e25-904">CREATE, UPDATE o DROP STATISTICS</span><span class="sxs-lookup"><span data-stu-id="d3e25-904">CREATE, UPDATE, or DROP STATISTICS</span></span>
* <span data-ttu-id="d3e25-905">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="d3e25-905">TRUNCATE TABLE</span></span>
* <span data-ttu-id="d3e25-906">ALTER AUTHORIZATION</span><span class="sxs-lookup"><span data-stu-id="d3e25-906">ALTER AUTHORIZATION</span></span>
* <span data-ttu-id="d3e25-907">CREATE LOGIN</span><span class="sxs-lookup"><span data-stu-id="d3e25-907">CREATE LOGIN</span></span>
* <span data-ttu-id="d3e25-908">CREATE, ALTER o DROP USER</span><span class="sxs-lookup"><span data-stu-id="d3e25-908">CREATE, ALTER or DROP USER</span></span>
* <span data-ttu-id="d3e25-909">CREATE, ALTER o DROP PROCEDURE</span><span class="sxs-lookup"><span data-stu-id="d3e25-909">CREATE, ALTER or DROP PROCEDURE</span></span>
* <span data-ttu-id="d3e25-910">CREATE o DROP VIEW</span><span class="sxs-lookup"><span data-stu-id="d3e25-910">CREATE or DROP VIEW</span></span>
* <span data-ttu-id="d3e25-911">INSERT VALUES</span><span class="sxs-lookup"><span data-stu-id="d3e25-911">INSERT VALUES</span></span>
* <span data-ttu-id="d3e25-912">SELECT (desde vistas del sistema y DMV)</span><span class="sxs-lookup"><span data-stu-id="d3e25-912">SELECT from system views and DMVs</span></span>
* <span data-ttu-id="d3e25-913">EXPLAIN</span><span class="sxs-lookup"><span data-stu-id="d3e25-913">EXPLAIN</span></span>
* <span data-ttu-id="d3e25-914">DBCC</span><span class="sxs-lookup"><span data-stu-id="d3e25-914">DBCC</span></span>

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <span data-ttu-id="d3e25-915"><a name="changing-user-resource-class-example"></a> Ejemplo de cambio de una clase de recursos de usuario</span><span class="sxs-lookup"><span data-stu-id="d3e25-915"><a name="changing-user-resource-class-example"></a> Change a user resource class example</span></span>
1. <span data-ttu-id="d3e25-916">**Crear el inicio de sesión:** abrir una conexión tooyour **maestro** en hello SQL server que hospeda la base de datos de almacenamiento de datos SQL de base de datos y ejecutar Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="d3e25-916">**Create login:** Open a connection tooyour **master** database on hello SQL server hosting your SQL Data Warehouse database and execute hello following commands.</span></span>
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > <span data-ttu-id="d3e25-917">Es un toocreate buena idea un usuario en la base de datos maestra de Hola para los usuarios de almacenamiento de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d3e25-917">It is a good idea toocreate a user in hello master database for Azure SQL Data Warehouse users.</span></span> <span data-ttu-id="d3e25-918">La creación de un usuario en master permite un toologin de usuario con herramientas como SSMS sin especificar un nombre de base de datos.</span><span class="sxs-lookup"><span data-stu-id="d3e25-918">Creating a user in master allows a user toologin using tools like SSMS without specifying a database name.</span></span>  <span data-ttu-id="d3e25-919">También les permite toouse Hola objeto explorer tooview todas las bases de datos en un servidor SQL server.</span><span class="sxs-lookup"><span data-stu-id="d3e25-919">It also allows them toouse hello object explorer tooview all databases on a SQL server.</span></span>  <span data-ttu-id="d3e25-920">Para obtener más información sobre cómo crear y administrar usuarios, consulte [Proteger una base de datos en SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="d3e25-920">For more details about creating and managing users, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>
   > 
   > 
2. <span data-ttu-id="d3e25-921">**Crear usuario del almacén de datos SQL:** abrir una conexión toohello **almacenamiento de datos SQL** la base de datos y ejecute el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3e25-921">**Create SQL Data Warehouse user:** Open a connection toohello **SQL Data Warehouse** database and execute hello following command.</span></span>
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. <span data-ttu-id="d3e25-922">**Conceder permisos:** Hola siguientes en el ejemplo se concede `CONTROL` en hello **almacenamiento de datos SQL** base de datos.</span><span class="sxs-lookup"><span data-stu-id="d3e25-922">**Grant permissions:** hello following example grants `CONTROL` on hello **SQL Data Warehouse** database.</span></span> <span data-ttu-id="d3e25-923">`CONTROL`en hello el nivel de base de datos es Hola equivalente de db_owner en SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d3e25-923">`CONTROL` at hello database level is hello equivalent of db_owner in SQL Server.</span></span>
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW toonewperson;
    ```
4. <span data-ttu-id="d3e25-924">**Aumentar la clase de recurso:** consulta de uso Hola siguiente tooadd un rol usuario tooa mayor carga de trabajo administración.</span><span class="sxs-lookup"><span data-stu-id="d3e25-924">**Increase resource class:** Use hello following query tooadd a user tooa higher workload management role.</span></span>
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. <span data-ttu-id="d3e25-925">**Reducir la clase de recurso:** consulta de uso Hola siguiente tooremove un usuario de un rol de administración de cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="d3e25-925">**Decrease resource class:** Use hello following query tooremove a user from a workload management role.</span></span>
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="d3e25-926">No es posible tooremove un usuario de smallrc.</span><span class="sxs-lookup"><span data-stu-id="d3e25-926">It is not possible tooremove a user from smallrc.</span></span>
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a><span data-ttu-id="d3e25-927">Detección de consulta en cola y otras DMV</span><span class="sxs-lookup"><span data-stu-id="d3e25-927">Queued query detection and other DMVs</span></span>
<span data-ttu-id="d3e25-928">Puede usar hello `sys.dm_pdw_exec_requests` consultas tooidentify DMV que esperan en una cola de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="d3e25-928">You can use hello `sys.dm_pdw_exec_requests` DMV tooidentify queries that are waiting in a concurrency queue.</span></span> <span data-ttu-id="d3e25-929">Las consultas que esperan un espacio de simultaneidad tendrán el estado de **suspendido**.</span><span class="sxs-lookup"><span data-stu-id="d3e25-929">Queries waiting for a concurrency slot will have a status of **suspended**.</span></span>

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

<span data-ttu-id="d3e25-930">Los roles de administración de cargas de trabajo se pueden ver con `sys.database_principals`.</span><span class="sxs-lookup"><span data-stu-id="d3e25-930">Workload management roles can be viewed with `sys.database_principals`.</span></span>

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

<span data-ttu-id="d3e25-931">Hola después de consulta muestra el rol que está asignado cada usuario.</span><span class="sxs-lookup"><span data-stu-id="d3e25-931">hello following query shows which role each user is assigned to.</span></span>

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

<span data-ttu-id="d3e25-932">Almacenamiento de datos de SQL tiene Hola siguientes tipos de espera:</span><span class="sxs-lookup"><span data-stu-id="d3e25-932">SQL Data Warehouse has hello following wait types:</span></span>

* <span data-ttu-id="d3e25-933">**LocalQueriesConcurrencyResourceType**: las consultas que residen fuera del marco de ranura de simultaneidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3e25-933">**LocalQueriesConcurrencyResourceType**: Queries that sit outside of hello concurrency slot framework.</span></span> <span data-ttu-id="d3e25-934">Las funciones del sistema y las consultas DMV como `SELECT @@VERSION` son ejemplos de consultas locales.</span><span class="sxs-lookup"><span data-stu-id="d3e25-934">DMV queries and system functions such as `SELECT @@VERSION` are examples of local queries.</span></span>
* <span data-ttu-id="d3e25-935">**UserConcurrencyResourceType**: las consultas que se encuentran dentro de hello simultaneidad ranura framework.</span><span class="sxs-lookup"><span data-stu-id="d3e25-935">**UserConcurrencyResourceType**: Queries that sit inside hello concurrency slot framework.</span></span> <span data-ttu-id="d3e25-936">Las consultas en tablas de usuario final representan ejemplos que usarían este tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="d3e25-936">Queries against end-user tables represent examples that would use this resource type.</span></span>
* <span data-ttu-id="d3e25-937">**DmsConcurrencyResourceType**: se refiere a las esperas que son el resultado de operaciones de movimiento de datos.</span><span class="sxs-lookup"><span data-stu-id="d3e25-937">**DmsConcurrencyResourceType**: Waits resulting from data movement operations.</span></span>
* <span data-ttu-id="d3e25-938">**BackupConcurrencyResourceType**: se refiere a una espera que indica que se está creando la copia de seguridad de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="d3e25-938">**BackupConcurrencyResourceType**: This wait indicates that a database is being backed up.</span></span> <span data-ttu-id="d3e25-939">valor máximo de Hola para este tipo de recurso es 1.</span><span class="sxs-lookup"><span data-stu-id="d3e25-939">hello maximum value for this resource type is 1.</span></span> <span data-ttu-id="d3e25-940">Si varias copias de seguridad se han solicitado en hello mismo tiempo, Hola otros se pondrán en cola.</span><span class="sxs-lookup"><span data-stu-id="d3e25-940">If multiple backups have been requested at hello same time, hello others will queue.</span></span>

<span data-ttu-id="d3e25-941">Hola `sys.dm_pdw_waits` DMV puede ser toosee usa los recursos que una solicitud está esperando.</span><span class="sxs-lookup"><span data-stu-id="d3e25-941">hello `sys.dm_pdw_waits` DMV can be used toosee which resources a request is waiting for.</span></span>

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

<span data-ttu-id="d3e25-942">Hola `sys.dm_pdw_resource_waits` DMV muestra solo hello las esperas de recursos utilizadas por una consulta determinada.</span><span class="sxs-lookup"><span data-stu-id="d3e25-942">hello `sys.dm_pdw_resource_waits` DMV shows only hello resource waits consumed by a given query.</span></span> <span data-ttu-id="d3e25-943">Tiempo de espera de recursos sólo mide el tiempo de hello esperando toobe de recursos proporcionado, como los opuestos toosignal espera tiempo, lo que es el momento de hello tarda Hola subyacente de la consulta SQL servidores tooschedule hello en hello CPU.</span><span class="sxs-lookup"><span data-stu-id="d3e25-943">Resource wait time only measures hello time waiting for resources toobe provided, as opposed toosignal wait time, which is hello time it takes for hello underlying SQL servers tooschedule hello query onto hello CPU.</span></span>

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

<span data-ttu-id="d3e25-944">Hola `sys.dm_pdw_wait_stats` DMV se puede utilizar para el análisis de tendencias históricas de esperas.</span><span class="sxs-lookup"><span data-stu-id="d3e25-944">hello `sys.dm_pdw_wait_stats` DMV can be used for historic trend analysis of waits.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d3e25-945">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d3e25-945">Next steps</span></span>
<span data-ttu-id="d3e25-946">Para obtener más información sobre cómo administrar los usuarios y la seguridad de la base de datos, consulte [Proteger una base de datos en SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="d3e25-946">For more information about managing database users and security, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span> <span data-ttu-id="d3e25-947">Para obtener más información acerca de cómo mayores clases de recursos puede mejorar la calidad del índice de almacén de columnas agrupado, vea [volver a generar la calidad de segmento de índices tooimprove].</span><span class="sxs-lookup"><span data-stu-id="d3e25-947">For more information about how larger resource classes can improve clustered columnstore index quality, see [Rebuilding indexes tooimprove segment quality].</span></span>

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[volver a generar la calidad de segmento de índices tooimprove]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
