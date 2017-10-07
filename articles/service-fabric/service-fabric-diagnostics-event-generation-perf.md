---
title: "aaaAzure supervisión del rendimiento de servicio de Fabric | Documentos de Microsoft"
description: "Obtenga información sobre los contadores de rendimiento para la supervisión y el diagnóstico de clústeres de Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 54d4c62b7250a1f70b0898ba07ae5a37716f4cf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="performance-metrics"></a><span data-ttu-id="39365-103">Métricas de rendimiento</span><span class="sxs-lookup"><span data-stu-id="39365-103">Performance metrics</span></span>

<span data-ttu-id="39365-104">Las métricas deben ser recopilados toounderstand Hola rendimiento del clúster, así como aplicaciones de Hola que se ejecutan en él.</span><span class="sxs-lookup"><span data-stu-id="39365-104">Metrics should be collected toounderstand hello performance of your cluster as well as hello applications running in it.</span></span> <span data-ttu-id="39365-105">Para los clústeres de Service Fabric, se recomienda recopilar Hola siguiendo los contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="39365-105">For Service Fabric clusters, we recommend collecting hello following performance counters.</span></span>

## <a name="nodes"></a><span data-ttu-id="39365-106">Nodos</span><span class="sxs-lookup"><span data-stu-id="39365-106">Nodes</span></span>

<span data-ttu-id="39365-107">Para las máquinas de hello en el clúster, considere la posibilidad de recopilar Hola siguiendo los contadores de rendimiento toobetter comprender Hola carga de cada equipo y asegúrese de ajuste de escala en las decisiones de clúster correspondientes.</span><span class="sxs-lookup"><span data-stu-id="39365-107">For hello machines in your cluster, consider collecting hello following performance counters toobetter understand hello load on each machine and make appropriate cluster scaling decisions.</span></span>

| <span data-ttu-id="39365-108">Categoría de contador</span><span class="sxs-lookup"><span data-stu-id="39365-108">Counter Category</span></span> | <span data-ttu-id="39365-109">Nombre del contador</span><span class="sxs-lookup"><span data-stu-id="39365-109">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="39365-110">Disco físico (por disco)</span><span class="sxs-lookup"><span data-stu-id="39365-110">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="39365-111">Prom. Longitud de la cola de lectura de disco</span><span class="sxs-lookup"><span data-stu-id="39365-111">Avg. Disk Read Queue Length</span></span> |
| <span data-ttu-id="39365-112">Disco físico (por disco)</span><span class="sxs-lookup"><span data-stu-id="39365-112">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="39365-113">Prom. Longitud de la cola de escritura de disco</span><span class="sxs-lookup"><span data-stu-id="39365-113">Avg. Disk Write Queue Length</span></span> |
| <span data-ttu-id="39365-114">Disco físico (por disco)</span><span class="sxs-lookup"><span data-stu-id="39365-114">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="39365-115">Prom. Segundos de disco/lecturas</span><span class="sxs-lookup"><span data-stu-id="39365-115">Avg. Disk sec/Read</span></span> |
| <span data-ttu-id="39365-116">Disco físico (por disco)</span><span class="sxs-lookup"><span data-stu-id="39365-116">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="39365-117">Prom. Segundos de disco/escrituras</span><span class="sxs-lookup"><span data-stu-id="39365-117">Avg. Disk sec/Write</span></span> |
| <span data-ttu-id="39365-118">Disco físico (por disco)</span><span class="sxs-lookup"><span data-stu-id="39365-118">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="39365-119">Lecturas de disco/s </span><span class="sxs-lookup"><span data-stu-id="39365-119">Disk Reads/sec</span></span> |
| <span data-ttu-id="39365-120">Disco físico (por disco)</span><span class="sxs-lookup"><span data-stu-id="39365-120">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="39365-121">Bytes de lectura de disco/s </span><span class="sxs-lookup"><span data-stu-id="39365-121">Disk Read Bytes/sec</span></span> |
| <span data-ttu-id="39365-122">Disco físico (por disco)</span><span class="sxs-lookup"><span data-stu-id="39365-122">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="39365-123">Escrituras en disco/s</span><span class="sxs-lookup"><span data-stu-id="39365-123">Disk Writes/sec</span></span> |
| <span data-ttu-id="39365-124">Disco físico (por disco)</span><span class="sxs-lookup"><span data-stu-id="39365-124">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="39365-125"> Bytes de escritura en disco/s</span><span class="sxs-lookup"><span data-stu-id="39365-125">Disk Write Bytes/sec</span></span> |
| <span data-ttu-id="39365-126">Memoria</span><span class="sxs-lookup"><span data-stu-id="39365-126">Memory</span></span> | <span data-ttu-id="39365-127">MB disponibles</span><span class="sxs-lookup"><span data-stu-id="39365-127">Available MBytes</span></span> |
| <span data-ttu-id="39365-128">Archivo de paginación</span><span class="sxs-lookup"><span data-stu-id="39365-128">PagingFile</span></span> | <span data-ttu-id="39365-129">% de uso</span><span class="sxs-lookup"><span data-stu-id="39365-129">% Usage</span></span> |
| <span data-ttu-id="39365-130">Proceso (total)</span><span class="sxs-lookup"><span data-stu-id="39365-130">Process(Total)</span></span> | <span data-ttu-id="39365-131">% de tiempo de procesador</span><span class="sxs-lookup"><span data-stu-id="39365-131">% Processor Time</span></span> |
| <span data-ttu-id="39365-132">Proceso (por servicio)</span><span class="sxs-lookup"><span data-stu-id="39365-132">Process (per service)</span></span> | <span data-ttu-id="39365-133">% de tiempo de procesador</span><span class="sxs-lookup"><span data-stu-id="39365-133">% Processor Time</span></span> |
| <span data-ttu-id="39365-134">Proceso (por servicio)</span><span class="sxs-lookup"><span data-stu-id="39365-134">Process (per service)</span></span> | <span data-ttu-id="39365-135">Id. de proceso</span><span class="sxs-lookup"><span data-stu-id="39365-135">ID Process</span></span> |
| <span data-ttu-id="39365-136">Proceso (por servicio)</span><span class="sxs-lookup"><span data-stu-id="39365-136">Process (per service)</span></span> | <span data-ttu-id="39365-137">Bytes privados</span><span class="sxs-lookup"><span data-stu-id="39365-137">Private Bytes</span></span> |
| <span data-ttu-id="39365-138">Proceso (por servicio)</span><span class="sxs-lookup"><span data-stu-id="39365-138">Process (per service)</span></span> | <span data-ttu-id="39365-139">Número de subprocesos</span><span class="sxs-lookup"><span data-stu-id="39365-139">Thread Count</span></span> |
| <span data-ttu-id="39365-140">Proceso (por servicio)</span><span class="sxs-lookup"><span data-stu-id="39365-140">Process (per service)</span></span> | <span data-ttu-id="39365-141">Bytes virtuales</span><span class="sxs-lookup"><span data-stu-id="39365-141">Virtual Bytes</span></span> |
| <span data-ttu-id="39365-142">Proceso (por servicio)</span><span class="sxs-lookup"><span data-stu-id="39365-142">Process (per service)</span></span> | <span data-ttu-id="39365-143">Espacio de trabajo</span><span class="sxs-lookup"><span data-stu-id="39365-143">Working Set</span></span> |
| <span data-ttu-id="39365-144">Proceso (por servicio)</span><span class="sxs-lookup"><span data-stu-id="39365-144">Process (per service)</span></span> | <span data-ttu-id="39365-145">Espacio de trabajo privado</span><span class="sxs-lookup"><span data-stu-id="39365-145">Working Set - Private</span></span> |

## <a name="net-applications-and-services"></a><span data-ttu-id="39365-146">Aplicaciones y servicios .NET</span><span class="sxs-lookup"><span data-stu-id="39365-146">.NET applications and services</span></span>

<span data-ttu-id="39365-147">Recopilar Hola después de contadores si va a implementar el clúster de .NET services tooyour.</span><span class="sxs-lookup"><span data-stu-id="39365-147">Collect hello following counters if you are deploying .NET services tooyour cluster.</span></span> 

| <span data-ttu-id="39365-148">Categoría de contador</span><span class="sxs-lookup"><span data-stu-id="39365-148">Counter Category</span></span> | <span data-ttu-id="39365-149">Nombre del contador</span><span class="sxs-lookup"><span data-stu-id="39365-149">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="39365-150">Memoria CLR de .NET (por servicio)</span><span class="sxs-lookup"><span data-stu-id="39365-150">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="39365-151">Identificador del proceso</span><span class="sxs-lookup"><span data-stu-id="39365-151">Process ID</span></span> |
| <span data-ttu-id="39365-152">Memoria CLR de .NET (por servicio)</span><span class="sxs-lookup"><span data-stu-id="39365-152">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="39365-153">Número total de bytes confirmados</span><span class="sxs-lookup"><span data-stu-id="39365-153"># Total committed Bytes</span></span> |
| <span data-ttu-id="39365-154">Memoria CLR de .NET (por servicio)</span><span class="sxs-lookup"><span data-stu-id="39365-154">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="39365-155">Número total de bytes reservados</span><span class="sxs-lookup"><span data-stu-id="39365-155"># Total reserved Bytes</span></span> |
| <span data-ttu-id="39365-156">Memoria CLR de .NET (por servicio)</span><span class="sxs-lookup"><span data-stu-id="39365-156">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="39365-157">Número de bytes en todos los montones</span><span class="sxs-lookup"><span data-stu-id="39365-157"># Bytes in all Heaps</span></span> |
| <span data-ttu-id="39365-158">Memoria CLR de .NET (por servicio)</span><span class="sxs-lookup"><span data-stu-id="39365-158">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="39365-159">Número de colecciones de gen. 0</span><span class="sxs-lookup"><span data-stu-id="39365-159"># Gen 0 Collections</span></span> |
| <span data-ttu-id="39365-160">Memoria CLR de .NET (por servicio)</span><span class="sxs-lookup"><span data-stu-id="39365-160">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="39365-161">Número de colecciones de gen. 1</span><span class="sxs-lookup"><span data-stu-id="39365-161"># Gen 1 Collections</span></span> |
| <span data-ttu-id="39365-162">Memoria CLR de .NET (por servicio)</span><span class="sxs-lookup"><span data-stu-id="39365-162">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="39365-163">Número de colecciones de gen. 2</span><span class="sxs-lookup"><span data-stu-id="39365-163"># Gen 2 Collections</span></span> |
| <span data-ttu-id="39365-164">Memoria CLR de .NET (por servicio)</span><span class="sxs-lookup"><span data-stu-id="39365-164">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="39365-165">% de tiempo del GC</span><span class="sxs-lookup"><span data-stu-id="39365-165">% Time in GC</span></span> |

### <a name="service-fabrics-custom-performance-counters"></a><span data-ttu-id="39365-166">Contadores de rendimiento personalizados de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="39365-166">Service Fabric's custom performance counters</span></span>

<span data-ttu-id="39365-167">Service Fabric genera una cantidad considerable de contadores de rendimiento personalizados.</span><span class="sxs-lookup"><span data-stu-id="39365-167">Service Fabric generates a substantial amount of custom performance counters.</span></span> <span data-ttu-id="39365-168">Si tienes Hola SDK instalado, puede ver lista completa de hello en el equipo de Windows en la aplicación de Monitor de rendimiento (Inicio > Monitor de rendimiento).</span><span class="sxs-lookup"><span data-stu-id="39365-168">If you have hello SDK installed, you can see hello comprehensive list on your Windows machine in your Performance Monitor application (Start > Performance Monitor).</span></span> 

<span data-ttu-id="39365-169">En las aplicaciones de hello están implementando tooyour clúster, si usas Reliable Actors, agregue countes de `Service Fabric Actor` y `Service Fabric Actor Method` categorías (vea [confiable actores diagnósticos del tejido servicio](service-fabric-reliable-actors-diagnostics.md)).</span><span class="sxs-lookup"><span data-stu-id="39365-169">In hello applications you are deploying tooyour cluster, if you are using Reliable Actors, add countes from `Service Fabric Actor` and `Service Fabric Actor Method` categories (see [Service Fabric Reliable Actors Diagnostics](service-fabric-reliable-actors-diagnostics.md)).</span></span>

<span data-ttu-id="39365-170">Si usa Reliable Services, del mismo modo tenemos las categorías de contadores `Service Fabric Service` y `Service Fabric Service Method` desde las cuales se deben recopilar los contadores.</span><span class="sxs-lookup"><span data-stu-id="39365-170">If you use Reliable Services, we similarly have `Service Fabric Service` and `Service Fabric Service Method` counter categories that you should collect counters from.</span></span> 

<span data-ttu-id="39365-171">Si se usan colecciones confiables, se recomienda agregar hello `Avg. Transaction ms/Commit` de hello `Service Fabric Transactional Replicator` latencia de promedio de confirmación de hello toocollect por métrica de transacción.</span><span class="sxs-lookup"><span data-stu-id="39365-171">If you use Reliable Collections, we recommend adding hello `Avg. Transaction ms/Commit` from hello `Service Fabric Transactional Replicator` toocollect hello average commit latency per transaction metric.</span></span>


## <a name="next-steps"></a><span data-ttu-id="39365-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="39365-172">Next steps</span></span>

* <span data-ttu-id="39365-173">Obtenga más información sobre [generación de eventos en el nivel de la plataforma de hello](service-fabric-diagnostics-event-generation-infra.md) en Service Fabric</span><span class="sxs-lookup"><span data-stu-id="39365-173">Learn more about [event generation at hello platform level](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric</span></span>
* <span data-ttu-id="39365-174">Recopile las métricas de rendimiento mediante [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span><span class="sxs-lookup"><span data-stu-id="39365-174">Collect performance metrics through [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span></span>
