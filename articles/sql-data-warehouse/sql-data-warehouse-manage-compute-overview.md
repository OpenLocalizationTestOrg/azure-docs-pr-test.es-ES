---
title: "Administración de la potencia de proceso en Azure SQL Data Warehouse (introducción) | Microsoft Docs"
description: Funcionalidades de escalado horizontal del rendimiento en Almacenamiento de datos SQL de Azure. Realice el escalado horizontal ajustando las DWU o pause y reanude los recursos de proceso para ahorrar costos.
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: e13a82b0-abfe-429f-ac3c-f2b6789a70c6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/22/2017
ms.author: elbutter
ms.openlocfilehash: abe22f542a79714f6e894870872ee6b76ffe7633
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a><span data-ttu-id="fcdaf-104">Administración de la potencia de proceso en Almacenamiento de datos SQL de Azure (información general)</span><span class="sxs-lookup"><span data-stu-id="fcdaf-104">Manage compute power in Azure SQL Data Warehouse (Overview)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fcdaf-105">Información general</span><span class="sxs-lookup"><span data-stu-id="fcdaf-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="fcdaf-106">Portal</span><span class="sxs-lookup"><span data-stu-id="fcdaf-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="fcdaf-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fcdaf-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="fcdaf-108">REST</span><span class="sxs-lookup"><span data-stu-id="fcdaf-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="fcdaf-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="fcdaf-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<span data-ttu-id="fcdaf-110">La arquitectura del Almacenamiento de datos SQL separa el proceso y el almacenamiento, lo que permite a cada uno escalar de manera independiente.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-110">The architecture of SQL Data Warehouse separates storage and compute, allowing each to scale independently.</span></span> <span data-ttu-id="fcdaf-111">Por consiguiente, el proceso se puede escalar para satisfacer las demandas de rendimiento independientemente de la cantidad de datos.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-111">As a result, compute can be scaled to meet performance demands independent of the amount of data.</span></span> <span data-ttu-id="fcdaf-112">Una consecuencia natural de esta arquitectura es que la [facturación][billed] para el proceso y almacenamiento es independiente.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-112">A natural consequence of this architecture is that [billing][billed] for compute and storage is separate.</span></span> 

<span data-ttu-id="fcdaf-113">En esta introducción se describe cómo funciona el escalado horizontal con SQL Data Warehouse y cómo utilizar las funcionalidades de pausa, reanudación y escala de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-113">This overview describes how scale out works with SQL Data Warehouse and how to utilize the pause, resume, and scale capabilities of SQL Data Warehouse.</span></span> <span data-ttu-id="fcdaf-114">Consulte la página de [unidades de almacenamiento de datos (DWU)][data warehouse units (DWUs)] para obtener información sobre la relación existente entre DWU y el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-114">Consult the [data warehouse units (DWUs)][data warehouse units (DWUs)] page to learn how DWUs and performance are related.</span></span> 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a><span data-ttu-id="fcdaf-115">Funcionamiento de las operaciones de administración de proceso en SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="fcdaf-115">How compute management operations work in SQL Data Warehouse</span></span>
<span data-ttu-id="fcdaf-116">La arquitectura de SQL Data Warehouse está formada por un nodo del control, nodos de proceso y la capa de almacenamiento que se reparten a lo largo de 60 distribuciones.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-116">The architecture for SQL Data Warehouse consists of a control node, compute nodes, and the storage layer spread across 60 distributions.</span></span> 

<span data-ttu-id="fcdaf-117">Durante una sesión activa normal en SQL Data Warehouse, el nodo principal del sistema administra los metadatos y contiene el optimizador de consultas distribuidas.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-117">During a normal active session in SQL Data Warehouse, your system's head node manages the metadata and contains the distributed query optimizer.</span></span> <span data-ttu-id="fcdaf-118">Debajo de este nodo principal se encuentran los nodos de proceso y el nivel de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-118">Beneath this head node are your compute nodes and your storage layer.</span></span> <span data-ttu-id="fcdaf-119">Para un 400 DWU, el sistema tiene un nodo principal, cuatro nodos de proceso y la capa de almacenamiento, que consta de 60 distribuciones.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-119">For a DWU 400, your system has one head node, four compute nodes, and the storage layer, consisting of 60 distributions.</span></span> 

<span data-ttu-id="fcdaf-120">Cuando se lleva a cabo una operación de escala o pausa, el sistema primero elimina todas las consultas entrantes y luego revierte las transacciones para garantizar un estado coherente.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-120">When you undergo a scale or pause operation, the system first kills all incoming queries and then rolls back transactions to ensure a consistent state.</span></span> <span data-ttu-id="fcdaf-121">Para las operaciones de escala, el escalado solo se producirá una vez completada esta reversión transaccional.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-121">For scale operations, scaling will only occur once this transactional rollback has completed.</span></span> <span data-ttu-id="fcdaf-122">Para una operación de escalado vertical, el sistema aprovisiona el número deseado adicional de nodos de proceso y luego comienza a asociar de nuevo los nodos de proceso con el nivel de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-122">For a scale-up operation, the system provisions the extra desired number of compute nodes, and then begins reattaching the compute nodes to the storage layer.</span></span> <span data-ttu-id="fcdaf-123">Para una operación de escalado horizontal, se liberan los nodos que no necesita y el resto de nodos de proceso se vuelven a asociar ellos mismos con el número apropiado de distribuciones.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-123">For a scale-down operation, the unneeded nodes are released and the remaining compute nodes reattach themselves to the appropriate number of distributions.</span></span> <span data-ttu-id="fcdaf-124">Para una operación de pausa, se liberan todos los nodos de proceso y el sistema se somete a una serie de operaciones de metadatos para dejar el sistema final en un estado estable.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-124">For a pause operation, all compute nodes are released and your system will undergo a variety of metadata operations to leave your final system in a stable state.</span></span>

| <span data-ttu-id="fcdaf-125">DWU</span><span class="sxs-lookup"><span data-stu-id="fcdaf-125">DWU</span></span>  | <span data-ttu-id="fcdaf-126">\# de nodos de ejecución</span><span class="sxs-lookup"><span data-stu-id="fcdaf-126">\#of compute nodes</span></span> | <span data-ttu-id="fcdaf-127">\# de distribuciones por nodo</span><span class="sxs-lookup"><span data-stu-id="fcdaf-127">\# of distributions per node</span></span> |
| ---- | ------------------ | ---------------------------- |
| <span data-ttu-id="fcdaf-128">100</span><span class="sxs-lookup"><span data-stu-id="fcdaf-128">100</span></span>  | <span data-ttu-id="fcdaf-129">1</span><span class="sxs-lookup"><span data-stu-id="fcdaf-129">1</span></span>                  | <span data-ttu-id="fcdaf-130">60</span><span class="sxs-lookup"><span data-stu-id="fcdaf-130">60</span></span>                           |
| <span data-ttu-id="fcdaf-131">200</span><span class="sxs-lookup"><span data-stu-id="fcdaf-131">200</span></span>  | <span data-ttu-id="fcdaf-132">2</span><span class="sxs-lookup"><span data-stu-id="fcdaf-132">2</span></span>                  | <span data-ttu-id="fcdaf-133">30</span><span class="sxs-lookup"><span data-stu-id="fcdaf-133">30</span></span>                           |
| <span data-ttu-id="fcdaf-134">300</span><span class="sxs-lookup"><span data-stu-id="fcdaf-134">300</span></span>  | <span data-ttu-id="fcdaf-135">3</span><span class="sxs-lookup"><span data-stu-id="fcdaf-135">3</span></span>                  | <span data-ttu-id="fcdaf-136">20 |</span><span class="sxs-lookup"><span data-stu-id="fcdaf-136">20</span></span>                           |
| <span data-ttu-id="fcdaf-137">400</span><span class="sxs-lookup"><span data-stu-id="fcdaf-137">400</span></span>  | <span data-ttu-id="fcdaf-138">4</span><span class="sxs-lookup"><span data-stu-id="fcdaf-138">4</span></span>                  | <span data-ttu-id="fcdaf-139">15</span><span class="sxs-lookup"><span data-stu-id="fcdaf-139">15</span></span>                           |
| <span data-ttu-id="fcdaf-140">500</span><span class="sxs-lookup"><span data-stu-id="fcdaf-140">500</span></span>  | <span data-ttu-id="fcdaf-141">5</span><span class="sxs-lookup"><span data-stu-id="fcdaf-141">5</span></span>                  | <span data-ttu-id="fcdaf-142">12</span><span class="sxs-lookup"><span data-stu-id="fcdaf-142">12</span></span>                           |
| <span data-ttu-id="fcdaf-143">600</span><span class="sxs-lookup"><span data-stu-id="fcdaf-143">600</span></span>  | <span data-ttu-id="fcdaf-144">6</span><span class="sxs-lookup"><span data-stu-id="fcdaf-144">6</span></span>                  | <span data-ttu-id="fcdaf-145">10</span><span class="sxs-lookup"><span data-stu-id="fcdaf-145">10</span></span>                           |
| <span data-ttu-id="fcdaf-146">1000</span><span class="sxs-lookup"><span data-stu-id="fcdaf-146">1000</span></span> | <span data-ttu-id="fcdaf-147">10</span><span class="sxs-lookup"><span data-stu-id="fcdaf-147">10</span></span>                 | <span data-ttu-id="fcdaf-148">6</span><span class="sxs-lookup"><span data-stu-id="fcdaf-148">6</span></span>                            |
| <span data-ttu-id="fcdaf-149">1200</span><span class="sxs-lookup"><span data-stu-id="fcdaf-149">1200</span></span> | <span data-ttu-id="fcdaf-150">12</span><span class="sxs-lookup"><span data-stu-id="fcdaf-150">12</span></span>                 | <span data-ttu-id="fcdaf-151">5</span><span class="sxs-lookup"><span data-stu-id="fcdaf-151">5</span></span>                            |
| <span data-ttu-id="fcdaf-152">1.500</span><span class="sxs-lookup"><span data-stu-id="fcdaf-152">1500</span></span> | <span data-ttu-id="fcdaf-153">15</span><span class="sxs-lookup"><span data-stu-id="fcdaf-153">15</span></span>                 | <span data-ttu-id="fcdaf-154">4</span><span class="sxs-lookup"><span data-stu-id="fcdaf-154">4</span></span>                            |
| <span data-ttu-id="fcdaf-155">2000</span><span class="sxs-lookup"><span data-stu-id="fcdaf-155">2000</span></span> | <span data-ttu-id="fcdaf-156">20 |</span><span class="sxs-lookup"><span data-stu-id="fcdaf-156">20</span></span>                 | <span data-ttu-id="fcdaf-157">3</span><span class="sxs-lookup"><span data-stu-id="fcdaf-157">3</span></span>                            |
| <span data-ttu-id="fcdaf-158">3000</span><span class="sxs-lookup"><span data-stu-id="fcdaf-158">3000</span></span> | <span data-ttu-id="fcdaf-159">30</span><span class="sxs-lookup"><span data-stu-id="fcdaf-159">30</span></span>                 | <span data-ttu-id="fcdaf-160">2</span><span class="sxs-lookup"><span data-stu-id="fcdaf-160">2</span></span>                            |
| <span data-ttu-id="fcdaf-161">6000</span><span class="sxs-lookup"><span data-stu-id="fcdaf-161">6000</span></span> | <span data-ttu-id="fcdaf-162">60</span><span class="sxs-lookup"><span data-stu-id="fcdaf-162">60</span></span>                 | <span data-ttu-id="fcdaf-163">1</span><span class="sxs-lookup"><span data-stu-id="fcdaf-163">1</span></span>                            |

<span data-ttu-id="fcdaf-164">Las tres funciones principales para administrar el proceso son:</span><span class="sxs-lookup"><span data-stu-id="fcdaf-164">The three primary functions for managing compute are:</span></span>

1. <span data-ttu-id="fcdaf-165">Pausar</span><span class="sxs-lookup"><span data-stu-id="fcdaf-165">Pause</span></span>
2. <span data-ttu-id="fcdaf-166">Reanudación</span><span class="sxs-lookup"><span data-stu-id="fcdaf-166">Resume</span></span>
3. <span data-ttu-id="fcdaf-167">Escala</span><span class="sxs-lookup"><span data-stu-id="fcdaf-167">Scale</span></span>

<span data-ttu-id="fcdaf-168">Cada una de estas operaciones puede tardar varios minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-168">Each of these operations may take several minutes to complete.</span></span> <span data-ttu-id="fcdaf-169">Si está realizando una operación de escalado, pausa o reanudación automáticamente, puede que desee implementar la lógica para asegurarse de que ciertas operaciones se completaron antes de pasar a realizar otra acción.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-169">If you are scaling/pausing/resuming automatically, you may want to implement logic to ensure that certain operations have been completed before proceeding with another action.</span></span> 

<span data-ttu-id="fcdaf-170">La comprobación del estado de la base de datos a través de varios puntos de conexión le permitirá implementar correctamente la automatización de tales operaciones.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-170">Checking the database state through various endpoints will allow you to correctly implement automation of such operations.</span></span> <span data-ttu-id="fcdaf-171">El portal le proporcionará una notificación tras la finalización de una operación y el estado actual de las bases de datos, pero no permitirá la comprobación programática del estado.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-171">The portal will provide notification upon completion of an operation and the databases current state but does not allow for programmatic checking of state.</span></span> 

>  [!NOTE]
>
>  <span data-ttu-id="fcdaf-172">La funcionalidad de administración del proceso no existe en todos los puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-172">Compute management functionality does not exist across all endpoints.</span></span>
>
>  

|              | <span data-ttu-id="fcdaf-173">Pausar y reanudar</span><span class="sxs-lookup"><span data-stu-id="fcdaf-173">Pause/Resume</span></span> | <span data-ttu-id="fcdaf-174">Escala</span><span class="sxs-lookup"><span data-stu-id="fcdaf-174">Scale</span></span> | <span data-ttu-id="fcdaf-175">Comprobar el estado de la base de datos</span><span class="sxs-lookup"><span data-stu-id="fcdaf-175">Check database state</span></span> |
| ------------ | ------------ | ----- | -------------------- |
| <span data-ttu-id="fcdaf-176">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="fcdaf-176">Azure portal</span></span> | <span data-ttu-id="fcdaf-177">Sí</span><span class="sxs-lookup"><span data-stu-id="fcdaf-177">Yes</span></span>          | <span data-ttu-id="fcdaf-178">Sí</span><span class="sxs-lookup"><span data-stu-id="fcdaf-178">Yes</span></span>   | <span data-ttu-id="fcdaf-179">**No**</span><span class="sxs-lookup"><span data-stu-id="fcdaf-179">**No**</span></span>               |
| <span data-ttu-id="fcdaf-180">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fcdaf-180">PowerShell</span></span>   | <span data-ttu-id="fcdaf-181">Sí</span><span class="sxs-lookup"><span data-stu-id="fcdaf-181">Yes</span></span>          | <span data-ttu-id="fcdaf-182">Sí</span><span class="sxs-lookup"><span data-stu-id="fcdaf-182">Yes</span></span>   | <span data-ttu-id="fcdaf-183">Sí</span><span class="sxs-lookup"><span data-stu-id="fcdaf-183">Yes</span></span>                  |
| <span data-ttu-id="fcdaf-184">API de REST</span><span class="sxs-lookup"><span data-stu-id="fcdaf-184">REST API</span></span>     | <span data-ttu-id="fcdaf-185">Sí</span><span class="sxs-lookup"><span data-stu-id="fcdaf-185">Yes</span></span>          | <span data-ttu-id="fcdaf-186">Sí</span><span class="sxs-lookup"><span data-stu-id="fcdaf-186">Yes</span></span>   | <span data-ttu-id="fcdaf-187">Sí</span><span class="sxs-lookup"><span data-stu-id="fcdaf-187">Yes</span></span>                  |
| <span data-ttu-id="fcdaf-188">T-SQL</span><span class="sxs-lookup"><span data-stu-id="fcdaf-188">T-SQL</span></span>        | <span data-ttu-id="fcdaf-189">**No**</span><span class="sxs-lookup"><span data-stu-id="fcdaf-189">**No**</span></span>       | <span data-ttu-id="fcdaf-190">Sí</span><span class="sxs-lookup"><span data-stu-id="fcdaf-190">Yes</span></span>   | <span data-ttu-id="fcdaf-191">Sí</span><span class="sxs-lookup"><span data-stu-id="fcdaf-191">Yes</span></span>                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="fcdaf-192">Escalado de proceso</span><span class="sxs-lookup"><span data-stu-id="fcdaf-192">Scale compute</span></span>

<span data-ttu-id="fcdaf-193">El rendimiento en SQL Data Warehouse se mide en [unidades de almacenamiento de datos (DWU)][data warehouse units (DWUs)], que es una medida de recursos de proceso abstracta, como la CPU, la memoria y el ancho de banda de E/S.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-193">Performance in SQL Data Warehouse is measured in [data warehouse units (DWUs)][data warehouse units (DWUs)] which is an abstracted measure of compute resources such as CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="fcdaf-194">Un usuario que desea escalar el rendimiento del sistema puede hacerlo a través de varios medios, como pueden ser el portal, T-SQL y API de REST.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-194">A user who wishes to scale their system's performance can do so through various means, such as through the portal, T-SQL, and REST APIs.</span></span> 

### <a name="how-do-i-scale-compute"></a><span data-ttu-id="fcdaf-195">¿Cómo se puede escalar el proceso?</span><span class="sxs-lookup"><span data-stu-id="fcdaf-195">How do I scale compute?</span></span>
<span data-ttu-id="fcdaf-196">La energía de proceso se administra para SQL Data Warehouse cambiando el ajuste de DWU.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-196">Compute power is managed for you SQL Data Warehouse by changing the DWU setting.</span></span> <span data-ttu-id="fcdaf-197">El rendimiento aumenta [linealmente][linearly] a medida que agrega más DWU para determinadas operaciones.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-197">Performance increases [linearly][linearly] as you add more DWU for certain operations.</span></span>  <span data-ttu-id="fcdaf-198">Proporcionamos ofertas de DWU que garantizan que el rendimiento cambiará considerablemente al escalar o reducir el sistema verticalmente.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-198">We offer DWU offerings that ensure that your performance will change noticeably when you scale your system up or down.</span></span> 

<span data-ttu-id="fcdaf-199">Para ajustar las DWU, puede utilizar cualquiera de estos métodos individuales.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-199">To adjust DWUs, you can use any of these individual methods.</span></span>

* <span data-ttu-id="fcdaf-200">[Escalado de la potencia de proceso con Azure Portal][Scale compute power with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="fcdaf-200">[Scale compute power with Azure portal][Scale compute power with Azure portal]</span></span>
* <span data-ttu-id="fcdaf-201">[Escalado de la potencia de proceso con PowerShell][Scale compute power with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="fcdaf-201">[Scale compute power with PowerShell][Scale compute power with PowerShell]</span></span>
* <span data-ttu-id="fcdaf-202">[Escalado de la potencia de proceso con API de REST][Scale compute power with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="fcdaf-202">[Scale compute power with REST APIs][Scale compute power with REST APIs]</span></span>
* <span data-ttu-id="fcdaf-203">[Escalado de la potencia de proceso con TSQL][Scale compute power with TSQL]</span><span class="sxs-lookup"><span data-stu-id="fcdaf-203">[Scale compute power with TSQL][Scale compute power with TSQL]</span></span>

### <a name="how-many-dwus-should-i-use"></a><span data-ttu-id="fcdaf-204">¿Cuántas DWU debería usar?</span><span class="sxs-lookup"><span data-stu-id="fcdaf-204">How many DWUs should I use?</span></span>

<span data-ttu-id="fcdaf-205">Para entender el valor ideal de su DWU, pruebe a escalar y reducir verticalmente y a ejecutar algunas consultas después de cargar los datos.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-205">To understand what your ideal DWU value is, try scaling up and down, and running a few queries after loading your data.</span></span> <span data-ttu-id="fcdaf-206">Dado que el escalado se realiza rápidamente, puede probar varios niveles de rendimiento en una hora o menos.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-206">Since scaling is quick, you can try various performance levels in an hour or less.</span></span> 

> [!Note] 
> <span data-ttu-id="fcdaf-207">SQL Data Warehouse está diseñado para procesar grandes cantidades de datos.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-207">SQL Data Warehouse is designed to process large amounts of data.</span></span> <span data-ttu-id="fcdaf-208">Para ver sus funcionalidades verdaderas para escalado, especialmente en DWU mayores, desea utilizar un conjunto de datos grande cuyo tamaño se aproxima o supera 1 TB.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-208">To see its true capabilities for scaling, especially at larger DWUs, you want to use a large data set which approaches or exceeds 1 TB.</span></span>

<span data-ttu-id="fcdaf-209">Recomendaciones para encontrar la mejor DWU para la carga de trabajo:</span><span class="sxs-lookup"><span data-stu-id="fcdaf-209">Recommendations for finding the best DWU for your workload:</span></span>

1. <span data-ttu-id="fcdaf-210">Para un almacenamiento de datos en desarrollo, comience seleccionando un número pequeño de DWU.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-210">For a data warehouse in development, begin by selecting a smaller DWU performance level.</span></span>  <span data-ttu-id="fcdaf-211">Un buen punto de partida es DW400 o DW200.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-211">A good starting point is DW400 or DW200.</span></span>
2. <span data-ttu-id="fcdaf-212">Supervise el rendimiento de su aplicación, observando el número de DWU seleccionados en comparación con el rendimiento que observe.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-212">Monitor your application performance, observing the number of DWUs selected compared to the performance you observe.</span></span>
3. <span data-ttu-id="fcdaf-213">Determine en qué grado debería ser el rendimiento más rápido o más lento para poder alcanzar el nivel óptimo de rendimiento para sus requerimientos suponiendo una escala lineal.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-213">Determine how much faster or slower performance should be for you to reach the optimum performance level for your requirements by assuming linear scale.</span></span>
4. <span data-ttu-id="fcdaf-214">Aumente o disminuya el número de DWU en proporción a la rapidez con la que quiere que funcione la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-214">Increase or decrease the number of DWUs in proportion to how much faster or slower you want your workload to perform.</span></span> 
5. <span data-ttu-id="fcdaf-215">Continúe realizando ajustes hasta llegar a un nivel de rendimiento adecuado para sus requerimientos empresariales.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-215">Continue making adjustments until you reach an optimum performance level for your business requirements.</span></span>

> [!NOTE]
>
> <span data-ttu-id="fcdaf-216">El rendimiento de las consultas solo aumenta con más paralelización si el trabajo se puede dividir entre nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-216">Query performance only increases with more parallelization if the work can be split between compute nodes.</span></span> <span data-ttu-id="fcdaf-217">Si observa que el escalado no cambia el rendimiento, consulte nuestros artículos de ajuste de rendimiento para comprobar si los datos no se distribuyen uniformemente o si introduce una gran cantidad de movimiento de datos.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-217">If you find that scaling is not changing your performance, please check out our performance tuning articles to check whether your data is unevenly distributed or if you are introducing a large amount of data movement.</span></span> 

### <a name="when-should-i-scale-dwus"></a><span data-ttu-id="fcdaf-218">¿Cuándo debo realizar un escalado de DWU?</span><span class="sxs-lookup"><span data-stu-id="fcdaf-218">When should I scale DWUs?</span></span>
<span data-ttu-id="fcdaf-219">El escalado de DWU modifica los siguientes escenarios importantes:</span><span class="sxs-lookup"><span data-stu-id="fcdaf-219">Scaling DWUs alters the following important scenarios:</span></span>

1. <span data-ttu-id="fcdaf-220">El cambio lineal del rendimiento del sistema para exámenes, agregaciones e instrucciones CTAS</span><span class="sxs-lookup"><span data-stu-id="fcdaf-220">Linearly changing performance of the system for scans, aggregations, and CTAS statements</span></span>
2. <span data-ttu-id="fcdaf-221">Aumento del número de lectores y escritores cuando se carga con PolyBase</span><span class="sxs-lookup"><span data-stu-id="fcdaf-221">Increasing the number of readers and writers when loading with PolyBase</span></span>
3. <span data-ttu-id="fcdaf-222">Número máximo de consultas simultáneas y ranuras de simultaneidad</span><span class="sxs-lookup"><span data-stu-id="fcdaf-222">Maximum number of concurrent queries and concurrency slots</span></span>

<span data-ttu-id="fcdaf-223">Recomendaciones de cuándo realizar el escalado de DWU:</span><span class="sxs-lookup"><span data-stu-id="fcdaf-223">Recommendations for when to scale DWUs:</span></span>

1. <span data-ttu-id="fcdaf-224">Para realizar una operación de transformación o carga de una gran cantidad de datos, realice el escalado vertical de DWU para que los datos estén disponibles con mayor rapidez.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-224">Before you perform a heavy data loading or transformation operation, scale up DWUs so that your data is available more quickly.</span></span>
2. <span data-ttu-id="fcdaf-225">Durante las horas punta comerciales, escale para dar cabida a un mayor número de consultas simultáneas.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-225">During peak business hours, scale to accommodate larger numbers of concurrent queries.</span></span> 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="fcdaf-226">Pausa del proceso</span><span class="sxs-lookup"><span data-stu-id="fcdaf-226">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="fcdaf-227">Para pausar una base de datos, use cualquiera de estos métodos individuales.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-227">To pause a database, use any of these individual methods.</span></span>

* <span data-ttu-id="fcdaf-228">[Pausa del proceso con Azure Portal][Pause compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="fcdaf-228">[Pause compute with Azure portal][Pause compute with Azure portal]</span></span>
* <span data-ttu-id="fcdaf-229">[Pausa del proceso con PowerShell][Pause compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="fcdaf-229">[Pause compute with PowerShell][Pause compute with PowerShell]</span></span>
* <span data-ttu-id="fcdaf-230">[Pausa del proceso con las API de REST][Pause compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="fcdaf-230">[Pause compute with REST APIs][Pause compute with REST APIs]</span></span>

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="fcdaf-231">Reanudación del proceso</span><span class="sxs-lookup"><span data-stu-id="fcdaf-231">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="fcdaf-232">Para reanudar una base de datos, use cualquiera de estos métodos individuales.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-232">To resume a database, use any of these individual methods.</span></span>

* <span data-ttu-id="fcdaf-233">[Reanudación del proceso con Azure Portal][Resume compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="fcdaf-233">[Resume compute with Azure portal][Resume compute with Azure portal]</span></span>
* <span data-ttu-id="fcdaf-234">[Reanudación del proceso con PowerShell][Resume compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="fcdaf-234">[Resume compute with PowerShell][Resume compute with PowerShell]</span></span>
* <span data-ttu-id="fcdaf-235">[Reanudación del proceso con las API de REST][Resume compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="fcdaf-235">[Resume compute with REST APIs][Resume compute with REST APIs]</span></span>

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="fcdaf-236">Comprobar el estado de la base de datos</span><span class="sxs-lookup"><span data-stu-id="fcdaf-236">Check database state</span></span> 

<span data-ttu-id="fcdaf-237">Para reanudar una base de datos, use cualquiera de estos métodos individuales.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-237">To resume a database, use any of these individual methods.</span></span>

- <span data-ttu-id="fcdaf-238">[Comprobar el estado de la base de datos con T-SQL][Check database state with T-SQL]</span><span class="sxs-lookup"><span data-stu-id="fcdaf-238">[Check database state with T-SQL][Check database state with T-SQL]</span></span>
- <span data-ttu-id="fcdaf-239">[Comprobar el estado de la base de datos con PowerShell][Check database state with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="fcdaf-239">[Check database state with PowerShell][Check database state with PowerShell]</span></span>
- <span data-ttu-id="fcdaf-240">[Comprobar el estado de la base de datos con API de REST][Check database state with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="fcdaf-240">[Check database state with REST APIs][Check database state with REST APIs]</span></span>

## <a name="permissions"></a><span data-ttu-id="fcdaf-241">Permisos</span><span class="sxs-lookup"><span data-stu-id="fcdaf-241">Permissions</span></span>

<span data-ttu-id="fcdaf-242">Para escalar la base de datos, se requieren los permisos descritos en [ALTER DATABASE][ALTER DATABASE].</span><span class="sxs-lookup"><span data-stu-id="fcdaf-242">Scaling the database requires the permissions described in [ALTER DATABASE][ALTER DATABASE].</span></span>  <span data-ttu-id="fcdaf-243">Para pausar y reanudar, se requiere el permiso [Colaborador de base de datos SQL][SQL DB Contributor], específicamente Microsoft.Sql/servers/databases/action.</span><span class="sxs-lookup"><span data-stu-id="fcdaf-243">Pause and Resume require the [SQL DB Contributor][SQL DB Contributor] permission, specifically Microsoft.Sql/servers/databases/action.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="fcdaf-244">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fcdaf-244">Next steps</span></span>
<span data-ttu-id="fcdaf-245">Consulte los artículos siguientes para comprender mejor algunos conceptos fundamentales adicionales sobre rendimiento:</span><span class="sxs-lookup"><span data-stu-id="fcdaf-245">Refer to the following articles to help you understand some additional key performance concepts:</span></span>

* <span data-ttu-id="fcdaf-246">[Administración de cargas de trabajo y simultaneidad][Workload and concurrency management]</span><span class="sxs-lookup"><span data-stu-id="fcdaf-246">[Workload and concurrency management][Workload and concurrency management]</span></span>
* <span data-ttu-id="fcdaf-247">[Introducción al diseño de tablas][Table design overview]</span><span class="sxs-lookup"><span data-stu-id="fcdaf-247">[Table design overview][Table design overview]</span></span>
* <span data-ttu-id="fcdaf-248">[Distribución de tablas][Table distribution]</span><span class="sxs-lookup"><span data-stu-id="fcdaf-248">[Table distribution][Table distribution]</span></span>
* <span data-ttu-id="fcdaf-249">[Indexación de tablas][Table indexing]</span><span class="sxs-lookup"><span data-stu-id="fcdaf-249">[Table indexing][Table indexing]</span></span>
* <span data-ttu-id="fcdaf-250">[Partición de tabla][Table partitioning]</span><span class="sxs-lookup"><span data-stu-id="fcdaf-250">[Table partitioning][Table partitioning]</span></span>
* <span data-ttu-id="fcdaf-251">[Estadísticas de tabla][Table statistics]</span><span class="sxs-lookup"><span data-stu-id="fcdaf-251">[Table statistics][Table statistics]</span></span>
* <span data-ttu-id="fcdaf-252">[Prácticas recomendadas][Best practices]</span><span class="sxs-lookup"><span data-stu-id="fcdaf-252">[Best practices][Best practices]</span></span>

<!--Image reference-->

<!--Article references-->
[data warehouse units (DWUs)]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[billed]: https://azure.microsoft.com/en-us/pricing/details/sql-data-warehouse/
[linearly]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[Scale compute power with Azure portal]: ./sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[Scale compute power with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#scale-compute-bk
[Scale compute power with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#scale-compute-bk
[Scale compute power with TSQL]: ./sql-data-warehouse-manage-compute-tsql.md#scale-compute-bk

[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md

[Pause compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#pause-compute-bk
[Pause compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#pause-compute-bk
[Pause compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#pause-compute-bk

[Resume compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#resume-compute-bk
[Resume compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#resume-compute-bk
[Resume compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#resume-compute-bk

[Check database state with T-SQL]: ./sql-data-warehouse-manage-compute-tsql.md#check-database-state-and-operation-progress
[Check database state with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#check-database-state
[Check database state with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#check-database-state

[Workload and concurrency management]: ./sql-data-warehouse-develop-concurrency.md
[Table design overview]: ./sql-data-warehouse-tables-overview.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexing]: ./sql-data-warehouse-tables-index.md
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Table statistics]: ./sql-data-warehouse-tables-statistics.md
[Best practices]: ./sql-data-warehouse-best-practices.md
[development overview]: ./sql-data-warehouse-overview-develop.md

[SQL DB Contributor]: ../active-directory/role-based-access-built-in-roles.md#sql-db-contributor

<!--MSDN references-->
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx

<!--Other Web references-->
[Azure portal]: http://portal.azure.com/
