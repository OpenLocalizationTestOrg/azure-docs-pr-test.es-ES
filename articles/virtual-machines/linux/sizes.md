---
title: "Tamaños de las máquinas virtuales Linux en Azure | Microsoft Docs"
description: "Enumera los tamaños diferentes disponibles para las máquinas virtuales Linux en Azure."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: da681171-f045-4c80-a5a9-d8bd47964673
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: fe7a92901ae25aa99ef71f09c416e6c6ad30d39b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="sizes-for-linux-virtual-machines-in-azure"></a><span data-ttu-id="056d6-103">Tamaños de las máquinas virtuales Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="056d6-103">Sizes for Linux virtual machines in Azure</span></span>
<span data-ttu-id="056d6-104">En este artículo se describen los tamaños y las opciones disponibles para las máquinas virtuales de Azure que puede usar para ejecutar las aplicaciones y cargas de trabajo de Linux.</span><span class="sxs-lookup"><span data-stu-id="056d6-104">This article describes the available sizes and options for the Azure virtual machines you can use to run your Linux apps and workloads.</span></span> <span data-ttu-id="056d6-105">También ofrece consideraciones de implementación que hay que tener en cuenta siempre que planee usar estos recursos.</span><span class="sxs-lookup"><span data-stu-id="056d6-105">It also provides deployment considerations to be aware of when you're planning to use these resources.</span></span> <span data-ttu-id="056d6-106">Este artículo también está disponible para [máquinas virtuales Windows](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="056d6-106">This article is also available for [Windows virtual machines](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


| <span data-ttu-id="056d6-107">Tipo</span><span class="sxs-lookup"><span data-stu-id="056d6-107">Type</span></span>                     | <span data-ttu-id="056d6-108">Tamaños</span><span class="sxs-lookup"><span data-stu-id="056d6-108">Sizes</span></span>           |    <span data-ttu-id="056d6-109">Descripción</span><span class="sxs-lookup"><span data-stu-id="056d6-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="056d6-110">Uso general</span><span class="sxs-lookup"><span data-stu-id="056d6-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="056d6-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7,</span><span class="sxs-lookup"><span data-stu-id="056d6-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7,</span></span>  | <span data-ttu-id="056d6-112">Uso equilibrado de la CPU en proporción de memoria.</span><span class="sxs-lookup"><span data-stu-id="056d6-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="056d6-113">Ideal para desarrollo y pruebas, bases de datos pequeñas o medianas, y servidores web de tráfico bajo o medio.</span><span class="sxs-lookup"><span data-stu-id="056d6-113">Ideal for testing and development, small to medium databases, and low to medium traffic web servers.</span></span> |
| [<span data-ttu-id="056d6-114">Proceso optimizado</span><span class="sxs-lookup"><span data-stu-id="056d6-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="056d6-115">Fs, F</span><span class="sxs-lookup"><span data-stu-id="056d6-115">Fs, F</span></span>             | <span data-ttu-id="056d6-116">Uso elevado de la CPU en proporción de memoria.</span><span class="sxs-lookup"><span data-stu-id="056d6-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="056d6-117">Bueno para servidores web de tráfico medio, aplicaciones de red, procesos por lotes y servidores de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="056d6-117">Good for medium traffic web servers, network appliances, bath processes, and application servers.</span></span>        |
| [<span data-ttu-id="056d6-118">Memoria optimizada</span><span class="sxs-lookup"><span data-stu-id="056d6-118">Memory optimized</span></span>](sizes-memory.md)         | <span data-ttu-id="056d6-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="056d6-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="056d6-120">Memoria alta en proporción de CPU.</span><span class="sxs-lookup"><span data-stu-id="056d6-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="056d6-121">Excelente para servidores de bases de datos relacionales, memorias caché de capacidad media o grande y análisis en memoria.</span><span class="sxs-lookup"><span data-stu-id="056d6-121">Great for relational database servers, medium to large caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="056d6-122">Almacenamiento optimizado</span><span class="sxs-lookup"><span data-stu-id="056d6-122">Storage optimized</span></span>](sizes-storage.md)        | <span data-ttu-id="056d6-123">LS</span><span class="sxs-lookup"><span data-stu-id="056d6-123">Ls</span></span>                | <span data-ttu-id="056d6-124">Alto rendimiento de disco y E/S.</span><span class="sxs-lookup"><span data-stu-id="056d6-124">High disk throughput and IO.</span></span> <span data-ttu-id="056d6-125">Perfecto para bases de datos SQL y NoSQL y macrodatos.</span><span class="sxs-lookup"><span data-stu-id="056d6-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="056d6-126">GPU</span><span class="sxs-lookup"><span data-stu-id="056d6-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="056d6-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="056d6-127">NV, NC</span></span>            | <span data-ttu-id="056d6-128">Máquinas virtuales especializadas específicas para la representación de gráficos pesados y la edición de vídeo.</span><span class="sxs-lookup"><span data-stu-id="056d6-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="056d6-129">Están disponibles con uno o varios GPU.</span><span class="sxs-lookup"><span data-stu-id="056d6-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="056d6-130">Proceso de alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="056d6-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="056d6-131">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="056d6-131">H, A8-11</span></span>          | <span data-ttu-id="056d6-132">Nuestras máquinas virtuales de CPU más rápidas y eficaces con interfaces de red de alto rendimiento opcionales (RDMA).</span><span class="sxs-lookup"><span data-stu-id="056d6-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br>

- <span data-ttu-id="056d6-133">Para obtener información sobre los precios de los diferentes tamaños, consulte [Precios de máquinas virtuales](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="056d6-133">For information about pricing of the various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span> 
- <span data-ttu-id="056d6-134">Para ver la disponibilidad de los tamaños de máquina virtual en las regiones de Azure, consulte [Productos disponibles por región](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="056d6-134">For availability of VM sizes in Azure regions, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
- <span data-ttu-id="056d6-135">Para ver los límites generales de las máquinas virtuales de Azure, consulte [Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="056d6-135">To see general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="056d6-136">Obtenga más información sobre cómo las [unidades de proceso de Azure (ACU)](../windows/acu.md) pueden ayudarlo a comparar el rendimiento en los distintos SKU de Azure.</span><span class="sxs-lookup"><span data-stu-id="056d6-136">Learn more about how [Azure compute units (ACU)](../windows/acu.md) can help you compare compute performance across Azure SKUs.</span></span>


## <a name="rest-api"></a><span data-ttu-id="056d6-137">API de REST</span><span class="sxs-lookup"><span data-stu-id="056d6-137">Rest API</span></span>

<span data-ttu-id="056d6-138">Para obtener información sobre el uso de la API de REST para consultar los tamaños de máquina virtual, consulte lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="056d6-138">For information on using the REST API to query for VM sizes, see the following:</span></span>

- [<span data-ttu-id="056d6-139">Lista de tamaños de máquina virtual disponibles para cambio de tamaño</span><span class="sxs-lookup"><span data-stu-id="056d6-139">List available virtual machine sizes for resizing</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [<span data-ttu-id="056d6-140">Lista de tamaños de máquina virtual disponibles para una suscripción</span><span class="sxs-lookup"><span data-stu-id="056d6-140">List available virtual machine sizes for a subscription</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [<span data-ttu-id="056d6-141">Lista de tamaños de máquina virtual disponibles en un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="056d6-141">List available virtual machine sizes in an availability set</span></span>](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a><span data-ttu-id="056d6-142">ACU</span><span class="sxs-lookup"><span data-stu-id="056d6-142">ACU</span></span>

<span data-ttu-id="056d6-143">Obtenga más información sobre cómo las [unidades de proceso de Azure (ACU)](acu.md) pueden ayudarlo a comparar el rendimiento en los distintos SKU de Azure.</span><span class="sxs-lookup"><span data-stu-id="056d6-143">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="056d6-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="056d6-144">Next steps</span></span>

<span data-ttu-id="056d6-145">Obtenga más información sobre los diferentes tamaños de máquina virtual que están disponibles:</span><span class="sxs-lookup"><span data-stu-id="056d6-145">Learn more about the different VM sizes that are available:</span></span>
- [<span data-ttu-id="056d6-146">Uso general</span><span class="sxs-lookup"><span data-stu-id="056d6-146">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="056d6-147">Proceso optimizado</span><span class="sxs-lookup"><span data-stu-id="056d6-147">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="056d6-148">Memoria optimizada</span><span class="sxs-lookup"><span data-stu-id="056d6-148">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="056d6-149">Almacenamiento optimizado</span><span class="sxs-lookup"><span data-stu-id="056d6-149">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="056d6-150">GPU</span><span class="sxs-lookup"><span data-stu-id="056d6-150">GPU</span></span>](sizes-gpu.md)
- [<span data-ttu-id="056d6-151">Proceso de alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="056d6-151">High performance compute</span></span>](sizes-hpc.md)



