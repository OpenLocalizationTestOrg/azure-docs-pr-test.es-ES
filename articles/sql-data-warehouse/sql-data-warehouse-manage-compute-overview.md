---
title: "capacidad de almacenamiento de datos de SQL Azure (Introducción) de cálculo aaaManage | Documentos de Microsoft"
description: Funcionalidades de escalado horizontal del rendimiento en Almacenamiento de datos SQL de Azure. Escalar horizontalmente mediante el ajuste a Dwu o pausar y reanudar los costos de toosave de recursos de proceso.
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
ms.openlocfilehash: 1ffbe8d694ac181eaeb6f585a2cee87a570ed7d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a><span data-ttu-id="c4c73-104">Administración de la potencia de proceso en Almacenamiento de datos SQL de Azure (información general)</span><span class="sxs-lookup"><span data-stu-id="c4c73-104">Manage compute power in Azure SQL Data Warehouse (Overview)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c4c73-105">Información general</span><span class="sxs-lookup"><span data-stu-id="c4c73-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="c4c73-106">Portal</span><span class="sxs-lookup"><span data-stu-id="c4c73-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="c4c73-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4c73-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="c4c73-108">REST</span><span class="sxs-lookup"><span data-stu-id="c4c73-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="c4c73-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="c4c73-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<span data-ttu-id="c4c73-110">arquitectura de Hola de almacenamiento de datos SQL separa almacenamiento y proceso, lo que permite cada tooscale de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="c4c73-110">hello architecture of SQL Data Warehouse separates storage and compute, allowing each tooscale independently.</span></span> <span data-ttu-id="c4c73-111">Como resultado, compute puede ser demandas de rendimiento escalado toomeet independiente de la cantidad de Hola de datos.</span><span class="sxs-lookup"><span data-stu-id="c4c73-111">As a result, compute can be scaled toomeet performance demands independent of hello amount of data.</span></span> <span data-ttu-id="c4c73-112">Una consecuencia natural de esta arquitectura es que la [facturación][billed] para el proceso y almacenamiento es independiente.</span><span class="sxs-lookup"><span data-stu-id="c4c73-112">A natural consequence of this architecture is that [billing][billed] for compute and storage is separate.</span></span> 

<span data-ttu-id="c4c73-113">Esta introducción se describe cómo escalar horizontalmente funciona con almacenamiento de datos SQL y cómo tooutilize Hola pausar, reanudar y capacidades de escala de almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="c4c73-113">This overview describes how scale out works with SQL Data Warehouse and how tooutilize hello pause, resume, and scale capabilities of SQL Data Warehouse.</span></span> <span data-ttu-id="c4c73-114">Consulte hello [unidades (a Dwu) del almacenamiento de datos] [ data warehouse units (DWUs)] toolearn página cómo se relacionan a Dwu y rendimiento.</span><span class="sxs-lookup"><span data-stu-id="c4c73-114">Consult hello [data warehouse units (DWUs)][data warehouse units (DWUs)] page toolearn how DWUs and performance are related.</span></span> 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a><span data-ttu-id="c4c73-115">Funcionamiento de las operaciones de administración de proceso en SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c4c73-115">How compute management operations work in SQL Data Warehouse</span></span>
<span data-ttu-id="c4c73-116">arquitectura de Hola para almacenamiento de datos de SQL está formada por un nodo del control, nodos de proceso y Hola repartidos 60 distribuciones de capa de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c4c73-116">hello architecture for SQL Data Warehouse consists of a control node, compute nodes, and hello storage layer spread across 60 distributions.</span></span> 

<span data-ttu-id="c4c73-117">Durante una sesión activa normal en el almacén de datos de SQL, nodo principal del sistema administra los metadatos de Hola y contiene el optimizador de consultas distribuida de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4c73-117">During a normal active session in SQL Data Warehouse, your system's head node manages hello metadata and contains hello distributed query optimizer.</span></span> <span data-ttu-id="c4c73-118">Debajo de este nodo principal se encuentran los nodos de proceso y el nivel de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c4c73-118">Beneath this head node are your compute nodes and your storage layer.</span></span> <span data-ttu-id="c4c73-119">Para un 400 DWU, el sistema tiene un nodo principal, cuatro nodos de proceso y capa de almacenamiento de hello, que consta de 60 distribuciones.</span><span class="sxs-lookup"><span data-stu-id="c4c73-119">For a DWU 400, your system has one head node, four compute nodes, and hello storage layer, consisting of 60 distributions.</span></span> 

<span data-ttu-id="c4c73-120">Cuando se someten a una escala o pausa la operación, el sistema de hello primero elimina todas las consultas entrantes y, a continuación, revierte las transacciones tooensure un estado coherente.</span><span class="sxs-lookup"><span data-stu-id="c4c73-120">When you undergo a scale or pause operation, hello system first kills all incoming queries and then rolls back transactions tooensure a consistent state.</span></span> <span data-ttu-id="c4c73-121">Para las operaciones de escala, el escalado solo se producirá una vez completada esta reversión transaccional.</span><span class="sxs-lookup"><span data-stu-id="c4c73-121">For scale operations, scaling will only occur once this transactional rollback has completed.</span></span> <span data-ttu-id="c4c73-122">Para una operación de escalado vertical, disposiciones de sistema de Hola Hola extra deseado número de nodos de proceso y comienza a continuación, volver a adjuntar la capa de almacenamiento de toohello de nodos de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4c73-122">For a scale-up operation, hello system provisions hello extra desired number of compute nodes, and then begins reattaching hello compute nodes toohello storage layer.</span></span> <span data-ttu-id="c4c73-123">Para una operación de reducción, hello nodos innecesarios se liberan y nodos de proceso restantes Hola volver a adjuntar por sí mismos toohello número adecuado de las distribuciones.</span><span class="sxs-lookup"><span data-stu-id="c4c73-123">For a scale-down operation, hello unneeded nodes are released and hello remaining compute nodes reattach themselves toohello appropriate number of distributions.</span></span> <span data-ttu-id="c4c73-124">Para una operación de pausa, todos los de proceso se liberan los nodos y el sistema sufrirá una variedad de metadatos operaciones tooleave el sistema final en un estado estable.</span><span class="sxs-lookup"><span data-stu-id="c4c73-124">For a pause operation, all compute nodes are released and your system will undergo a variety of metadata operations tooleave your final system in a stable state.</span></span>

| <span data-ttu-id="c4c73-125">DWU</span><span class="sxs-lookup"><span data-stu-id="c4c73-125">DWU</span></span>  | <span data-ttu-id="c4c73-126">\# de nodos de ejecución</span><span class="sxs-lookup"><span data-stu-id="c4c73-126">\#of compute nodes</span></span> | <span data-ttu-id="c4c73-127">\# de distribuciones por nodo</span><span class="sxs-lookup"><span data-stu-id="c4c73-127">\# of distributions per node</span></span> |
| ---- | ------------------ | ---------------------------- |
| <span data-ttu-id="c4c73-128">100</span><span class="sxs-lookup"><span data-stu-id="c4c73-128">100</span></span>  | <span data-ttu-id="c4c73-129">1</span><span class="sxs-lookup"><span data-stu-id="c4c73-129">1</span></span>                  | <span data-ttu-id="c4c73-130">60</span><span class="sxs-lookup"><span data-stu-id="c4c73-130">60</span></span>                           |
| <span data-ttu-id="c4c73-131">200</span><span class="sxs-lookup"><span data-stu-id="c4c73-131">200</span></span>  | <span data-ttu-id="c4c73-132">2</span><span class="sxs-lookup"><span data-stu-id="c4c73-132">2</span></span>                  | <span data-ttu-id="c4c73-133">30</span><span class="sxs-lookup"><span data-stu-id="c4c73-133">30</span></span>                           |
| <span data-ttu-id="c4c73-134">300</span><span class="sxs-lookup"><span data-stu-id="c4c73-134">300</span></span>  | <span data-ttu-id="c4c73-135">3</span><span class="sxs-lookup"><span data-stu-id="c4c73-135">3</span></span>                  | <span data-ttu-id="c4c73-136">20 |</span><span class="sxs-lookup"><span data-stu-id="c4c73-136">20</span></span>                           |
| <span data-ttu-id="c4c73-137">400</span><span class="sxs-lookup"><span data-stu-id="c4c73-137">400</span></span>  | <span data-ttu-id="c4c73-138">4</span><span class="sxs-lookup"><span data-stu-id="c4c73-138">4</span></span>                  | <span data-ttu-id="c4c73-139">15</span><span class="sxs-lookup"><span data-stu-id="c4c73-139">15</span></span>                           |
| <span data-ttu-id="c4c73-140">500</span><span class="sxs-lookup"><span data-stu-id="c4c73-140">500</span></span>  | <span data-ttu-id="c4c73-141">5</span><span class="sxs-lookup"><span data-stu-id="c4c73-141">5</span></span>                  | <span data-ttu-id="c4c73-142">12</span><span class="sxs-lookup"><span data-stu-id="c4c73-142">12</span></span>                           |
| <span data-ttu-id="c4c73-143">600</span><span class="sxs-lookup"><span data-stu-id="c4c73-143">600</span></span>  | <span data-ttu-id="c4c73-144">6</span><span class="sxs-lookup"><span data-stu-id="c4c73-144">6</span></span>                  | <span data-ttu-id="c4c73-145">10</span><span class="sxs-lookup"><span data-stu-id="c4c73-145">10</span></span>                           |
| <span data-ttu-id="c4c73-146">1000</span><span class="sxs-lookup"><span data-stu-id="c4c73-146">1000</span></span> | <span data-ttu-id="c4c73-147">10</span><span class="sxs-lookup"><span data-stu-id="c4c73-147">10</span></span>                 | <span data-ttu-id="c4c73-148">6</span><span class="sxs-lookup"><span data-stu-id="c4c73-148">6</span></span>                            |
| <span data-ttu-id="c4c73-149">1200</span><span class="sxs-lookup"><span data-stu-id="c4c73-149">1200</span></span> | <span data-ttu-id="c4c73-150">12</span><span class="sxs-lookup"><span data-stu-id="c4c73-150">12</span></span>                 | <span data-ttu-id="c4c73-151">5</span><span class="sxs-lookup"><span data-stu-id="c4c73-151">5</span></span>                            |
| <span data-ttu-id="c4c73-152">1.500</span><span class="sxs-lookup"><span data-stu-id="c4c73-152">1500</span></span> | <span data-ttu-id="c4c73-153">15</span><span class="sxs-lookup"><span data-stu-id="c4c73-153">15</span></span>                 | <span data-ttu-id="c4c73-154">4</span><span class="sxs-lookup"><span data-stu-id="c4c73-154">4</span></span>                            |
| <span data-ttu-id="c4c73-155">2000</span><span class="sxs-lookup"><span data-stu-id="c4c73-155">2000</span></span> | <span data-ttu-id="c4c73-156">20 |</span><span class="sxs-lookup"><span data-stu-id="c4c73-156">20</span></span>                 | <span data-ttu-id="c4c73-157">3</span><span class="sxs-lookup"><span data-stu-id="c4c73-157">3</span></span>                            |
| <span data-ttu-id="c4c73-158">3000</span><span class="sxs-lookup"><span data-stu-id="c4c73-158">3000</span></span> | <span data-ttu-id="c4c73-159">30</span><span class="sxs-lookup"><span data-stu-id="c4c73-159">30</span></span>                 | <span data-ttu-id="c4c73-160">2</span><span class="sxs-lookup"><span data-stu-id="c4c73-160">2</span></span>                            |
| <span data-ttu-id="c4c73-161">6000</span><span class="sxs-lookup"><span data-stu-id="c4c73-161">6000</span></span> | <span data-ttu-id="c4c73-162">60</span><span class="sxs-lookup"><span data-stu-id="c4c73-162">60</span></span>                 | <span data-ttu-id="c4c73-163">1</span><span class="sxs-lookup"><span data-stu-id="c4c73-163">1</span></span>                            |

<span data-ttu-id="c4c73-164">Hola tres funciones principales para administrar el proceso son:</span><span class="sxs-lookup"><span data-stu-id="c4c73-164">hello three primary functions for managing compute are:</span></span>

1. <span data-ttu-id="c4c73-165">Pausar</span><span class="sxs-lookup"><span data-stu-id="c4c73-165">Pause</span></span>
2. <span data-ttu-id="c4c73-166">Reanudación</span><span class="sxs-lookup"><span data-stu-id="c4c73-166">Resume</span></span>
3. <span data-ttu-id="c4c73-167">Escala</span><span class="sxs-lookup"><span data-stu-id="c4c73-167">Scale</span></span>

<span data-ttu-id="c4c73-168">Cada una de estas operaciones puede tardar varios toocomplete minutos.</span><span class="sxs-lookup"><span data-stu-id="c4c73-168">Each of these operations may take several minutes toocomplete.</span></span> <span data-ttu-id="c4c73-169">Si estás escalado, pausar o reanudar automáticamente, puede que desee tooimplement de lógica tooensure que algunas de las operaciones se hayan completado antes de realizar otra acción.</span><span class="sxs-lookup"><span data-stu-id="c4c73-169">If you are scaling/pausing/resuming automatically, you may want tooimplement logic tooensure that certain operations have been completed before proceeding with another action.</span></span> 

<span data-ttu-id="c4c73-170">Comprobando el estado de la base de datos de Hola a través de varios extremos le permitirá toocorrectly implementar automatización de tales operaciones.</span><span class="sxs-lookup"><span data-stu-id="c4c73-170">Checking hello database state through various endpoints will allow you toocorrectly implement automation of such operations.</span></span> <span data-ttu-id="c4c73-171">portal de Hola proporcionará la notificación tras la finalización de un estado actual de las bases de datos hello y operación pero no permite la programación de comprobación del estado.</span><span class="sxs-lookup"><span data-stu-id="c4c73-171">hello portal will provide notification upon completion of an operation and hello databases current state but does not allow for programmatic checking of state.</span></span> 

>  [!NOTE]
>
>  <span data-ttu-id="c4c73-172">La funcionalidad de administración del proceso no existe en todos los puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="c4c73-172">Compute management functionality does not exist across all endpoints.</span></span>
>
>  

|              | <span data-ttu-id="c4c73-173">Pausar y reanudar</span><span class="sxs-lookup"><span data-stu-id="c4c73-173">Pause/Resume</span></span> | <span data-ttu-id="c4c73-174">Escala</span><span class="sxs-lookup"><span data-stu-id="c4c73-174">Scale</span></span> | <span data-ttu-id="c4c73-175">Comprobar el estado de la base de datos</span><span class="sxs-lookup"><span data-stu-id="c4c73-175">Check database state</span></span> |
| ------------ | ------------ | ----- | -------------------- |
| <span data-ttu-id="c4c73-176">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c4c73-176">Azure portal</span></span> | <span data-ttu-id="c4c73-177">Sí</span><span class="sxs-lookup"><span data-stu-id="c4c73-177">Yes</span></span>          | <span data-ttu-id="c4c73-178">Sí</span><span class="sxs-lookup"><span data-stu-id="c4c73-178">Yes</span></span>   | <span data-ttu-id="c4c73-179">**No**</span><span class="sxs-lookup"><span data-stu-id="c4c73-179">**No**</span></span>               |
| <span data-ttu-id="c4c73-180">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4c73-180">PowerShell</span></span>   | <span data-ttu-id="c4c73-181">Sí</span><span class="sxs-lookup"><span data-stu-id="c4c73-181">Yes</span></span>          | <span data-ttu-id="c4c73-182">Sí</span><span class="sxs-lookup"><span data-stu-id="c4c73-182">Yes</span></span>   | <span data-ttu-id="c4c73-183">Sí</span><span class="sxs-lookup"><span data-stu-id="c4c73-183">Yes</span></span>                  |
| <span data-ttu-id="c4c73-184">API de REST</span><span class="sxs-lookup"><span data-stu-id="c4c73-184">REST API</span></span>     | <span data-ttu-id="c4c73-185">Sí</span><span class="sxs-lookup"><span data-stu-id="c4c73-185">Yes</span></span>          | <span data-ttu-id="c4c73-186">Sí</span><span class="sxs-lookup"><span data-stu-id="c4c73-186">Yes</span></span>   | <span data-ttu-id="c4c73-187">Sí</span><span class="sxs-lookup"><span data-stu-id="c4c73-187">Yes</span></span>                  |
| <span data-ttu-id="c4c73-188">T-SQL</span><span class="sxs-lookup"><span data-stu-id="c4c73-188">T-SQL</span></span>        | <span data-ttu-id="c4c73-189">**No**</span><span class="sxs-lookup"><span data-stu-id="c4c73-189">**No**</span></span>       | <span data-ttu-id="c4c73-190">Sí</span><span class="sxs-lookup"><span data-stu-id="c4c73-190">Yes</span></span>   | <span data-ttu-id="c4c73-191">Sí</span><span class="sxs-lookup"><span data-stu-id="c4c73-191">Yes</span></span>                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="c4c73-192">Escalado de proceso</span><span class="sxs-lookup"><span data-stu-id="c4c73-192">Scale compute</span></span>

<span data-ttu-id="c4c73-193">El rendimiento en SQL Data Warehouse se mide en [unidades de almacenamiento de datos (DWU)][data warehouse units (DWUs)], que es una medida de recursos de proceso abstracta, como la CPU, la memoria y el ancho de banda de E/S.</span><span class="sxs-lookup"><span data-stu-id="c4c73-193">Performance in SQL Data Warehouse is measured in [data warehouse units (DWUs)][data warehouse units (DWUs)] which is an abstracted measure of compute resources such as CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="c4c73-194">Un usuario que desea tooscale el rendimiento de su sistema puede hacerlo a través de varios medios, como a través del portal de hello, T-SQL y API de REST.</span><span class="sxs-lookup"><span data-stu-id="c4c73-194">A user who wishes tooscale their system's performance can do so through various means, such as through hello portal, T-SQL, and REST APIs.</span></span> 

### <a name="how-do-i-scale-compute"></a><span data-ttu-id="c4c73-195">¿Cómo se puede escalar el proceso?</span><span class="sxs-lookup"><span data-stu-id="c4c73-195">How do I scale compute?</span></span>
<span data-ttu-id="c4c73-196">Cambiar la configuración de la unidad de hello administra capacidad de proceso para su almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="c4c73-196">Compute power is managed for you SQL Data Warehouse by changing hello DWU setting.</span></span> <span data-ttu-id="c4c73-197">El rendimiento aumenta [linealmente][linearly] a medida que agrega más DWU para determinadas operaciones.</span><span class="sxs-lookup"><span data-stu-id="c4c73-197">Performance increases [linearly][linearly] as you add more DWU for certain operations.</span></span>  <span data-ttu-id="c4c73-198">Proporcionamos ofertas de DWU que garantizan que el rendimiento cambiará considerablemente al escalar o reducir el sistema verticalmente.</span><span class="sxs-lookup"><span data-stu-id="c4c73-198">We offer DWU offerings that ensure that your performance will change noticeably when you scale your system up or down.</span></span> 

<span data-ttu-id="c4c73-199">tooadjust a Dwu, puede usar cualquiera de estos métodos individuales.</span><span class="sxs-lookup"><span data-stu-id="c4c73-199">tooadjust DWUs, you can use any of these individual methods.</span></span>

* <span data-ttu-id="c4c73-200">[Escalado de la potencia de proceso con Azure Portal][Scale compute power with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="c4c73-200">[Scale compute power with Azure portal][Scale compute power with Azure portal]</span></span>
* <span data-ttu-id="c4c73-201">[Escalado de la potencia de proceso con PowerShell][Scale compute power with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="c4c73-201">[Scale compute power with PowerShell][Scale compute power with PowerShell]</span></span>
* <span data-ttu-id="c4c73-202">[Escalado de la potencia de proceso con API de REST][Scale compute power with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="c4c73-202">[Scale compute power with REST APIs][Scale compute power with REST APIs]</span></span>
* <span data-ttu-id="c4c73-203">[Escalado de la potencia de proceso con TSQL][Scale compute power with TSQL]</span><span class="sxs-lookup"><span data-stu-id="c4c73-203">[Scale compute power with TSQL][Scale compute power with TSQL]</span></span>

### <a name="how-many-dwus-should-i-use"></a><span data-ttu-id="c4c73-204">¿Cuántas DWU debería usar?</span><span class="sxs-lookup"><span data-stu-id="c4c73-204">How many DWUs should I use?</span></span>

<span data-ttu-id="c4c73-205">toounderstand qué el valor DWU ideal es, intente escalado vertical y horizontalmente y ejecute algunas consultas después de cargar los datos.</span><span class="sxs-lookup"><span data-stu-id="c4c73-205">toounderstand what your ideal DWU value is, try scaling up and down, and running a few queries after loading your data.</span></span> <span data-ttu-id="c4c73-206">Dado que el escalado se realiza rápidamente, puede probar varios niveles de rendimiento en una hora o menos.</span><span class="sxs-lookup"><span data-stu-id="c4c73-206">Since scaling is quick, you can try various performance levels in an hour or less.</span></span> 

> [!Note] 
> <span data-ttu-id="c4c73-207">Almacenamiento de datos de SQL está diseñado tooprocess grandes cantidades de datos.</span><span class="sxs-lookup"><span data-stu-id="c4c73-207">SQL Data Warehouse is designed tooprocess large amounts of data.</span></span> <span data-ttu-id="c4c73-208">toosee sus capacidades true para ajustar la escala, especialmente en a mayor Dwu, desea toouse un gran conjunto de datos que se aproxima o supera 1 TB.</span><span class="sxs-lookup"><span data-stu-id="c4c73-208">toosee its true capabilities for scaling, especially at larger DWUs, you want toouse a large data set which approaches or exceeds 1 TB.</span></span>

<span data-ttu-id="c4c73-209">Recomendaciones para buscar Hola DWU recomendada para la carga de trabajo:</span><span class="sxs-lookup"><span data-stu-id="c4c73-209">Recommendations for finding hello best DWU for your workload:</span></span>

1. <span data-ttu-id="c4c73-210">Para un almacenamiento de datos en desarrollo, comience seleccionando un número pequeño de DWU.</span><span class="sxs-lookup"><span data-stu-id="c4c73-210">For a data warehouse in development, begin by selecting a smaller DWU performance level.</span></span>  <span data-ttu-id="c4c73-211">Un buen punto de partida es DW400 o DW200.</span><span class="sxs-lookup"><span data-stu-id="c4c73-211">A good starting point is DW400 or DW200.</span></span>
2. <span data-ttu-id="c4c73-212">Supervisar el rendimiento de la aplicación, observar el número de Hola de a Dwu seleccionado compara el rendimiento toohello que observa.</span><span class="sxs-lookup"><span data-stu-id="c4c73-212">Monitor your application performance, observing hello number of DWUs selected compared toohello performance you observe.</span></span>
3. <span data-ttu-id="c4c73-213">Determinar cuánto rendimiento más rápido o más lento que debería ser para tooreach Hola nivel de rendimiento adecuado para sus requisitos, suponiendo la escala lineal.</span><span class="sxs-lookup"><span data-stu-id="c4c73-213">Determine how much faster or slower performance should be for you tooreach hello optimum performance level for your requirements by assuming linear scale.</span></span>
4. <span data-ttu-id="c4c73-214">Aumentar o reducir el número de Hola de a Dwu en proporción toohow mucho más rápida o más lentamente que desea que su tooperform de carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="c4c73-214">Increase or decrease hello number of DWUs in proportion toohow much faster or slower you want your workload tooperform.</span></span> 
5. <span data-ttu-id="c4c73-215">Continúe realizando ajustes hasta llegar a un nivel de rendimiento adecuado para sus requerimientos empresariales.</span><span class="sxs-lookup"><span data-stu-id="c4c73-215">Continue making adjustments until you reach an optimum performance level for your business requirements.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c4c73-216">Rendimiento de las consultas solo aumenta con la ejecución en paralelo más si se puede dividir el trabajo de hello entre nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="c4c73-216">Query performance only increases with more parallelization if hello work can be split between compute nodes.</span></span> <span data-ttu-id="c4c73-217">Si encuentra que el ajuste de escala no cambia su rendimiento, desproteja nuestro artículos toocheck si los datos no se distribuyen o si va a presentar una gran cantidad de movimiento de datos de optimización del rendimiento.</span><span class="sxs-lookup"><span data-stu-id="c4c73-217">If you find that scaling is not changing your performance, please check out our performance tuning articles toocheck whether your data is unevenly distributed or if you are introducing a large amount of data movement.</span></span> 

### <a name="when-should-i-scale-dwus"></a><span data-ttu-id="c4c73-218">¿Cuándo debo realizar un escalado de DWU?</span><span class="sxs-lookup"><span data-stu-id="c4c73-218">When should I scale DWUs?</span></span>
<span data-ttu-id="c4c73-219">Ajuste de escala a Dwu modifica Hola escenarios importantes siguientes:</span><span class="sxs-lookup"><span data-stu-id="c4c73-219">Scaling DWUs alters hello following important scenarios:</span></span>

1. <span data-ttu-id="c4c73-220">Cambiar linealmente el rendimiento del sistema de Hola para exámenes, agregaciones y las instrucciones de CTAS</span><span class="sxs-lookup"><span data-stu-id="c4c73-220">Linearly changing performance of hello system for scans, aggregations, and CTAS statements</span></span>
2. <span data-ttu-id="c4c73-221">Aumentar el número de Hola de lectores y escritores cuando se carga con PolyBase</span><span class="sxs-lookup"><span data-stu-id="c4c73-221">Increasing hello number of readers and writers when loading with PolyBase</span></span>
3. <span data-ttu-id="c4c73-222">Número máximo de consultas simultáneas y ranuras de simultaneidad</span><span class="sxs-lookup"><span data-stu-id="c4c73-222">Maximum number of concurrent queries and concurrency slots</span></span>

<span data-ttu-id="c4c73-223">Recomendaciones para saber cuándo tooscale a Dwu:</span><span class="sxs-lookup"><span data-stu-id="c4c73-223">Recommendations for when tooscale DWUs:</span></span>

1. <span data-ttu-id="c4c73-224">Para realizar una operación de transformación o carga de una gran cantidad de datos, realice el escalado vertical de DWU para que los datos estén disponibles con mayor rapidez.</span><span class="sxs-lookup"><span data-stu-id="c4c73-224">Before you perform a heavy data loading or transformation operation, scale up DWUs so that your data is available more quickly.</span></span>
2. <span data-ttu-id="c4c73-225">Durante las horas punta, escalar tooaccommodate un mayor número de consultas simultáneas.</span><span class="sxs-lookup"><span data-stu-id="c4c73-225">During peak business hours, scale tooaccommodate larger numbers of concurrent queries.</span></span> 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="c4c73-226">Pausa del proceso</span><span class="sxs-lookup"><span data-stu-id="c4c73-226">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="c4c73-227">toopause una base de datos, use cualquiera de estos métodos individuales.</span><span class="sxs-lookup"><span data-stu-id="c4c73-227">toopause a database, use any of these individual methods.</span></span>

* <span data-ttu-id="c4c73-228">[Pausa del proceso con Azure Portal][Pause compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="c4c73-228">[Pause compute with Azure portal][Pause compute with Azure portal]</span></span>
* <span data-ttu-id="c4c73-229">[Pausa del proceso con PowerShell][Pause compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="c4c73-229">[Pause compute with PowerShell][Pause compute with PowerShell]</span></span>
* <span data-ttu-id="c4c73-230">[Pausa del proceso con las API de REST][Pause compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="c4c73-230">[Pause compute with REST APIs][Pause compute with REST APIs]</span></span>

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="c4c73-231">Reanudación del proceso</span><span class="sxs-lookup"><span data-stu-id="c4c73-231">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="c4c73-232">tooresume una base de datos, use cualquiera de estos métodos individuales.</span><span class="sxs-lookup"><span data-stu-id="c4c73-232">tooresume a database, use any of these individual methods.</span></span>

* <span data-ttu-id="c4c73-233">[Reanudación del proceso con Azure Portal][Resume compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="c4c73-233">[Resume compute with Azure portal][Resume compute with Azure portal]</span></span>
* <span data-ttu-id="c4c73-234">[Reanudación del proceso con PowerShell][Resume compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="c4c73-234">[Resume compute with PowerShell][Resume compute with PowerShell]</span></span>
* <span data-ttu-id="c4c73-235">[Reanudación del proceso con las API de REST][Resume compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="c4c73-235">[Resume compute with REST APIs][Resume compute with REST APIs]</span></span>

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="c4c73-236">Comprobar el estado de la base de datos</span><span class="sxs-lookup"><span data-stu-id="c4c73-236">Check database state</span></span> 

<span data-ttu-id="c4c73-237">tooresume una base de datos, use cualquiera de estos métodos individuales.</span><span class="sxs-lookup"><span data-stu-id="c4c73-237">tooresume a database, use any of these individual methods.</span></span>

- <span data-ttu-id="c4c73-238">[Comprobar el estado de la base de datos con T-SQL][Check database state with T-SQL]</span><span class="sxs-lookup"><span data-stu-id="c4c73-238">[Check database state with T-SQL][Check database state with T-SQL]</span></span>
- <span data-ttu-id="c4c73-239">[Comprobar el estado de la base de datos con PowerShell][Check database state with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="c4c73-239">[Check database state with PowerShell][Check database state with PowerShell]</span></span>
- <span data-ttu-id="c4c73-240">[Comprobar el estado de la base de datos con API de REST][Check database state with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="c4c73-240">[Check database state with REST APIs][Check database state with REST APIs]</span></span>

## <a name="permissions"></a><span data-ttu-id="c4c73-241">Permisos</span><span class="sxs-lookup"><span data-stu-id="c4c73-241">Permissions</span></span>

<span data-ttu-id="c4c73-242">Base de datos de hello escala requiere permisos de hello descritos en [ALTER DATABASE][ALTER DATABASE].</span><span class="sxs-lookup"><span data-stu-id="c4c73-242">Scaling hello database requires hello permissions described in [ALTER DATABASE][ALTER DATABASE].</span></span>  <span data-ttu-id="c4c73-243">Pausar y reanudar requieren hello [colaborador de la base de datos de SQL] [ SQL DB Contributor] permiso, Microsoft.Sql/servers/databases/action específicamente.</span><span class="sxs-lookup"><span data-stu-id="c4c73-243">Pause and Resume require hello [SQL DB Contributor][SQL DB Contributor] permission, specifically Microsoft.Sql/servers/databases/action.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="c4c73-244">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c4c73-244">Next steps</span></span>
<span data-ttu-id="c4c73-245">Consulte toohello después toohelp artículos entender algunos conceptos clave de rendimiento adicionales:</span><span class="sxs-lookup"><span data-stu-id="c4c73-245">Refer toohello following articles toohelp you understand some additional key performance concepts:</span></span>

* <span data-ttu-id="c4c73-246">[Administración de cargas de trabajo y simultaneidad][Workload and concurrency management]</span><span class="sxs-lookup"><span data-stu-id="c4c73-246">[Workload and concurrency management][Workload and concurrency management]</span></span>
* <span data-ttu-id="c4c73-247">[Introducción al diseño de tablas][Table design overview]</span><span class="sxs-lookup"><span data-stu-id="c4c73-247">[Table design overview][Table design overview]</span></span>
* <span data-ttu-id="c4c73-248">[Distribución de tablas][Table distribution]</span><span class="sxs-lookup"><span data-stu-id="c4c73-248">[Table distribution][Table distribution]</span></span>
* <span data-ttu-id="c4c73-249">[Indexación de tablas][Table indexing]</span><span class="sxs-lookup"><span data-stu-id="c4c73-249">[Table indexing][Table indexing]</span></span>
* <span data-ttu-id="c4c73-250">[Partición de tabla][Table partitioning]</span><span class="sxs-lookup"><span data-stu-id="c4c73-250">[Table partitioning][Table partitioning]</span></span>
* <span data-ttu-id="c4c73-251">[Estadísticas de tabla][Table statistics]</span><span class="sxs-lookup"><span data-stu-id="c4c73-251">[Table statistics][Table statistics]</span></span>
* <span data-ttu-id="c4c73-252">[Prácticas recomendadas][Best practices]</span><span class="sxs-lookup"><span data-stu-id="c4c73-252">[Best practices][Best practices]</span></span>

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
