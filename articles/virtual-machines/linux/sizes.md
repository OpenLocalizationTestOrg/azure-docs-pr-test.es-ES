---
title: "tamaños de aaaLinux VM en Azure | Documentos de Microsoft"
description: "Muestra los tamaños diferentes de hello disponibles para máquinas virtuales de Linux en Azure."
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
ms.openlocfilehash: 56cbe0a0d7d34def07636edba74c4c699e336012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-linux-virtual-machines-in-azure"></a><span data-ttu-id="a2d48-103">Tamaños de las máquinas virtuales Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="a2d48-103">Sizes for Linux virtual machines in Azure</span></span>
<span data-ttu-id="a2d48-104">Este artículo describe los tamaños disponibles de Hola y opciones para hello máquinas virtuales de Azure puede usar toorun sus cargas de trabajo y aplicaciones de Linux.</span><span class="sxs-lookup"><span data-stu-id="a2d48-104">This article describes hello available sizes and options for hello Azure virtual machines you can use toorun your Linux apps and workloads.</span></span> <span data-ttu-id="a2d48-105">También proporciona toobe de consideraciones de implementación en cuenta cuando planee toouse estos recursos.</span><span class="sxs-lookup"><span data-stu-id="a2d48-105">It also provides deployment considerations toobe aware of when you're planning toouse these resources.</span></span> <span data-ttu-id="a2d48-106">Este artículo también está disponible para [máquinas virtuales Windows](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a2d48-106">This article is also available for [Windows virtual machines](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


| <span data-ttu-id="a2d48-107">Tipo</span><span class="sxs-lookup"><span data-stu-id="a2d48-107">Type</span></span>                     | <span data-ttu-id="a2d48-108">Tamaños</span><span class="sxs-lookup"><span data-stu-id="a2d48-108">Sizes</span></span>           |    <span data-ttu-id="a2d48-109">Descripción</span><span class="sxs-lookup"><span data-stu-id="a2d48-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="a2d48-110">Uso general</span><span class="sxs-lookup"><span data-stu-id="a2d48-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="a2d48-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7,</span><span class="sxs-lookup"><span data-stu-id="a2d48-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7,</span></span>  | <span data-ttu-id="a2d48-112">Uso equilibrado de la CPU en proporción de memoria.</span><span class="sxs-lookup"><span data-stu-id="a2d48-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="a2d48-113">Ideal para pruebas y desarrollo, las bases de datos pequeñas toomedium y servidores web de tráfico de toomedium baja.</span><span class="sxs-lookup"><span data-stu-id="a2d48-113">Ideal for testing and development, small toomedium databases, and low toomedium traffic web servers.</span></span> |
| [<span data-ttu-id="a2d48-114">Proceso optimizado</span><span class="sxs-lookup"><span data-stu-id="a2d48-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="a2d48-115">Fs, F</span><span class="sxs-lookup"><span data-stu-id="a2d48-115">Fs, F</span></span>             | <span data-ttu-id="a2d48-116">Uso elevado de la CPU en proporción de memoria.</span><span class="sxs-lookup"><span data-stu-id="a2d48-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="a2d48-117">Bueno para servidores web de tráfico medio, aplicaciones de red, procesos por lotes y servidores de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a2d48-117">Good for medium traffic web servers, network appliances, bath processes, and application servers.</span></span>        |
| [<span data-ttu-id="a2d48-118">Memoria optimizada</span><span class="sxs-lookup"><span data-stu-id="a2d48-118">Memory optimized</span></span>](sizes-memory.md)         | <span data-ttu-id="a2d48-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="a2d48-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="a2d48-120">Memoria alta en proporción de CPU.</span><span class="sxs-lookup"><span data-stu-id="a2d48-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="a2d48-121">Excelente para servidores de base de datos relacional, las cachés de toolarge intermedio y análisis en memoria.</span><span class="sxs-lookup"><span data-stu-id="a2d48-121">Great for relational database servers, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="a2d48-122">Almacenamiento optimizado</span><span class="sxs-lookup"><span data-stu-id="a2d48-122">Storage optimized</span></span>](sizes-storage.md)        | <span data-ttu-id="a2d48-123">LS</span><span class="sxs-lookup"><span data-stu-id="a2d48-123">Ls</span></span>                | <span data-ttu-id="a2d48-124">Alto rendimiento de disco y E/S.</span><span class="sxs-lookup"><span data-stu-id="a2d48-124">High disk throughput and IO.</span></span> <span data-ttu-id="a2d48-125">Perfecto para bases de datos SQL y NoSQL y macrodatos.</span><span class="sxs-lookup"><span data-stu-id="a2d48-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="a2d48-126">GPU</span><span class="sxs-lookup"><span data-stu-id="a2d48-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="a2d48-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="a2d48-127">NV, NC</span></span>            | <span data-ttu-id="a2d48-128">Máquinas virtuales especializadas específicas para la representación de gráficos pesados y la edición de vídeo.</span><span class="sxs-lookup"><span data-stu-id="a2d48-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="a2d48-129">Están disponibles con uno o varios GPU.</span><span class="sxs-lookup"><span data-stu-id="a2d48-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="a2d48-130">Proceso de alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="a2d48-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="a2d48-131">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="a2d48-131">H, A8-11</span></span>          | <span data-ttu-id="a2d48-132">Nuestras máquinas virtuales de CPU más rápidas y eficaces con interfaces de red de alto rendimiento opcionales (RDMA).</span><span class="sxs-lookup"><span data-stu-id="a2d48-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br>

- <span data-ttu-id="a2d48-133">Para obtener información sobre los precios de saludo diversos tamaños, vea [precios de máquinas virtuales](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="a2d48-133">For information about pricing of hello various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span> 
- <span data-ttu-id="a2d48-134">Para ver la disponibilidad de los tamaños de máquina virtual en las regiones de Azure, consulte [Productos disponibles por región](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="a2d48-134">For availability of VM sizes in Azure regions, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
- <span data-ttu-id="a2d48-135">límites generales de toosee en máquinas virtuales de Azure, consulte [suscripción de Azure y límites de servicio, cuotas y restricciones](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="a2d48-135">toosee general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="a2d48-136">Obtenga más información sobre cómo las [unidades de proceso de Azure (ACU)](../windows/acu.md) pueden ayudarlo a comparar el rendimiento en los distintos SKU de Azure.</span><span class="sxs-lookup"><span data-stu-id="a2d48-136">Learn more about how [Azure compute units (ACU)](../windows/acu.md) can help you compare compute performance across Azure SKUs.</span></span>


## <a name="rest-api"></a><span data-ttu-id="a2d48-137">API de REST</span><span class="sxs-lookup"><span data-stu-id="a2d48-137">Rest API</span></span>

<span data-ttu-id="a2d48-138">Para obtener información sobre el uso de tooquery de API de REST de Hola para tamaños de máquinas virtuales, vea Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="a2d48-138">For information on using hello REST API tooquery for VM sizes, see hello following:</span></span>

- [<span data-ttu-id="a2d48-139">Lista de tamaños de máquina virtual disponibles para cambio de tamaño</span><span class="sxs-lookup"><span data-stu-id="a2d48-139">List available virtual machine sizes for resizing</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [<span data-ttu-id="a2d48-140">Lista de tamaños de máquina virtual disponibles para una suscripción</span><span class="sxs-lookup"><span data-stu-id="a2d48-140">List available virtual machine sizes for a subscription</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [<span data-ttu-id="a2d48-141">Lista de tamaños de máquina virtual disponibles en un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="a2d48-141">List available virtual machine sizes in an availability set</span></span>](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a><span data-ttu-id="a2d48-142">ACU</span><span class="sxs-lookup"><span data-stu-id="a2d48-142">ACU</span></span>

<span data-ttu-id="a2d48-143">Obtenga más información sobre cómo las [unidades de proceso de Azure (ACU)](acu.md) pueden ayudarlo a comparar el rendimiento en los distintos SKU de Azure.</span><span class="sxs-lookup"><span data-stu-id="a2d48-143">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2d48-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a2d48-144">Next steps</span></span>

<span data-ttu-id="a2d48-145">Más información acerca de los diferentes tamaños VM de Hola que están disponibles:</span><span class="sxs-lookup"><span data-stu-id="a2d48-145">Learn more about hello different VM sizes that are available:</span></span>
- [<span data-ttu-id="a2d48-146">Uso general</span><span class="sxs-lookup"><span data-stu-id="a2d48-146">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="a2d48-147">Proceso optimizado</span><span class="sxs-lookup"><span data-stu-id="a2d48-147">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="a2d48-148">Memoria optimizada</span><span class="sxs-lookup"><span data-stu-id="a2d48-148">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="a2d48-149">Almacenamiento optimizado</span><span class="sxs-lookup"><span data-stu-id="a2d48-149">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="a2d48-150">GPU</span><span class="sxs-lookup"><span data-stu-id="a2d48-150">GPU</span></span>](sizes-gpu.md)
- [<span data-ttu-id="a2d48-151">Proceso de alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="a2d48-151">High performance compute</span></span>](sizes-hpc.md)



