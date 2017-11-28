---
title: "tamaños de aaaWindows VM en Azure | Documentos de Microsoft"
description: "Muestra los tamaños diferentes de hello disponibles para máquinas virtuales de Windows en Azure."
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: aabf0d30-04eb-4d34-b44a-69f8bfb84f22
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 80bd8241b134031c41b56224e841c7557c4845cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-windows-virtual-machines-in-azure"></a><span data-ttu-id="92b7a-103">Tamaños de las máquinas virtuales Windows en Azure</span><span class="sxs-lookup"><span data-stu-id="92b7a-103">Sizes for Windows virtual machines in Azure</span></span>

<span data-ttu-id="92b7a-104">Este artículo describe los tamaños disponibles de Hola y opciones para hello máquinas virtuales de Azure puede usar toorun sus aplicaciones de Windows y las cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="92b7a-104">This article describes hello available sizes and options for hello Azure virtual machines you can use toorun your Windows apps and workloads.</span></span> <span data-ttu-id="92b7a-105">También proporciona toobe de consideraciones de implementación en cuenta cuando planee toouse estos recursos.</span><span class="sxs-lookup"><span data-stu-id="92b7a-105">It also provides deployment considerations toobe aware of when you're planning toouse these resources.</span></span>  <span data-ttu-id="92b7a-106">Este artículo también está disponible para [máquinas virtuales Linux](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="92b7a-106">This article is also available for [Linux virtual machines](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


| <span data-ttu-id="92b7a-107">Tipo</span><span class="sxs-lookup"><span data-stu-id="92b7a-107">Type</span></span>                     | <span data-ttu-id="92b7a-108">Tamaños</span><span class="sxs-lookup"><span data-stu-id="92b7a-108">Sizes</span></span>           |    <span data-ttu-id="92b7a-109">Descripción</span><span class="sxs-lookup"><span data-stu-id="92b7a-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="92b7a-110">Uso general</span><span class="sxs-lookup"><span data-stu-id="92b7a-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="92b7a-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="92b7a-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span> | <span data-ttu-id="92b7a-112">Uso equilibrado de la CPU en proporción de memoria.</span><span class="sxs-lookup"><span data-stu-id="92b7a-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="92b7a-113">Ideal para pruebas y desarrollo, las bases de datos pequeñas toomedium y servidores web de tráfico de toomedium baja.</span><span class="sxs-lookup"><span data-stu-id="92b7a-113">Ideal for testing and development, small toomedium databases, and low toomedium traffic web servers.</span></span> |
| [<span data-ttu-id="92b7a-114">Proceso optimizado</span><span class="sxs-lookup"><span data-stu-id="92b7a-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="92b7a-115">Fs, F</span><span class="sxs-lookup"><span data-stu-id="92b7a-115">Fs, F</span></span>             | <span data-ttu-id="92b7a-116">Uso elevado de la CPU en proporción de memoria.</span><span class="sxs-lookup"><span data-stu-id="92b7a-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="92b7a-117">Bueno para servidores web de tráfico medio, aplicaciones de red, procesos por lotes y servidores de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="92b7a-117">Good for medium traffic web servers, network appliances, batch processes, and application servers.</span></span>        |
| [<span data-ttu-id="92b7a-118">Memoria optimizada</span><span class="sxs-lookup"><span data-stu-id="92b7a-118">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)         | <span data-ttu-id="92b7a-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="92b7a-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="92b7a-120">Memoria alta en proporción de CPU.</span><span class="sxs-lookup"><span data-stu-id="92b7a-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="92b7a-121">Excelente para servidores de base de datos relacional, las cachés de toolarge intermedio y análisis en memoria.</span><span class="sxs-lookup"><span data-stu-id="92b7a-121">Great for relational database servers, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="92b7a-122">Almacenamiento optimizado</span><span class="sxs-lookup"><span data-stu-id="92b7a-122">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)        | <span data-ttu-id="92b7a-123">LS</span><span class="sxs-lookup"><span data-stu-id="92b7a-123">Ls</span></span>                | <span data-ttu-id="92b7a-124">Alto rendimiento de disco y E/S.</span><span class="sxs-lookup"><span data-stu-id="92b7a-124">High disk throughput and IO.</span></span> <span data-ttu-id="92b7a-125">Perfecto para bases de datos SQL y NoSQL y macrodatos.</span><span class="sxs-lookup"><span data-stu-id="92b7a-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="92b7a-126">GPU</span><span class="sxs-lookup"><span data-stu-id="92b7a-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="92b7a-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="92b7a-127">NV, NC</span></span>            | <span data-ttu-id="92b7a-128">Máquinas virtuales especializadas específicas para la representación de gráficos pesados y la edición de vídeo.</span><span class="sxs-lookup"><span data-stu-id="92b7a-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="92b7a-129">Están disponibles con uno o varios GPU.</span><span class="sxs-lookup"><span data-stu-id="92b7a-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="92b7a-130">Proceso de alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="92b7a-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="92b7a-131">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="92b7a-131">H, A8-11</span></span>          | <span data-ttu-id="92b7a-132">Nuestras máquinas virtuales de CPU más rápidas y eficaces con interfaces de red de alto rendimiento opcionales (RDMA).</span><span class="sxs-lookup"><span data-stu-id="92b7a-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br> 

- <span data-ttu-id="92b7a-133">Para obtener información sobre los precios de saludo diversos tamaños, vea [precios de máquinas virtuales](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span><span class="sxs-lookup"><span data-stu-id="92b7a-133">For information about pricing of hello various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span></span> 
- <span data-ttu-id="92b7a-134">límites generales de toosee en máquinas virtuales de Azure, consulte [suscripción de Azure y límites de servicio, cuotas y restricciones](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="92b7a-134">toosee general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="92b7a-135">Los costos de almacenamiento se calculan por separado según las páginas usadas en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="92b7a-135">Storage costs are calculated separately based on used pages in hello storage account.</span></span> <span data-ttu-id="92b7a-136">Para obtener más información, consulte [Precios de Azure Storage](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="92b7a-136">For details, [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>
- <span data-ttu-id="92b7a-137">Obtenga más información sobre cómo las [unidades de proceso de Azure (ACU)](acu.md) pueden ayudarlo a comparar el rendimiento en los distintos SKU de Azure.</span><span class="sxs-lookup"><span data-stu-id="92b7a-137">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>



## <a name="rest-api"></a><span data-ttu-id="92b7a-138">API de REST</span><span class="sxs-lookup"><span data-stu-id="92b7a-138">Rest API</span></span>

<span data-ttu-id="92b7a-139">Para obtener información sobre el uso de tooquery de API de REST de Hola para tamaños de máquinas virtuales, vea Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="92b7a-139">For information on using hello REST API tooquery for VM sizes, see hello following:</span></span>

- [<span data-ttu-id="92b7a-140">Lista de tamaños de máquina virtual disponibles para cambio de tamaño</span><span class="sxs-lookup"><span data-stu-id="92b7a-140">List available virtual machine sizes for resizing</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [<span data-ttu-id="92b7a-141">Lista de tamaños de máquina virtual disponibles para una suscripción</span><span class="sxs-lookup"><span data-stu-id="92b7a-141">List available virtual machine sizes for a subscription</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [<span data-ttu-id="92b7a-142">Lista de tamaños de máquina virtual disponibles en un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="92b7a-142">List available virtual machine sizes in an availability set</span></span>](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a><span data-ttu-id="92b7a-143">ACU</span><span class="sxs-lookup"><span data-stu-id="92b7a-143">ACU</span></span>

<span data-ttu-id="92b7a-144">Obtenga más información sobre cómo las [unidades de proceso de Azure (ACU)](acu.md) pueden ayudarlo a comparar el rendimiento en los distintos SKU de Azure.</span><span class="sxs-lookup"><span data-stu-id="92b7a-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92b7a-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="92b7a-145">Next steps</span></span>

<span data-ttu-id="92b7a-146">Más información acerca de los diferentes tamaños VM de Hola que están disponibles:</span><span class="sxs-lookup"><span data-stu-id="92b7a-146">Learn more about hello different VM sizes that are available:</span></span>
- [<span data-ttu-id="92b7a-147">Uso general</span><span class="sxs-lookup"><span data-stu-id="92b7a-147">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="92b7a-148">Proceso optimizado</span><span class="sxs-lookup"><span data-stu-id="92b7a-148">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="92b7a-149">Memoria optimizada</span><span class="sxs-lookup"><span data-stu-id="92b7a-149">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="92b7a-150">Almacenamiento optimizado</span><span class="sxs-lookup"><span data-stu-id="92b7a-150">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="92b7a-151">GPU optimizada</span><span class="sxs-lookup"><span data-stu-id="92b7a-151">GPU optimized</span></span>](sizes-gpu.md)
- [<span data-ttu-id="92b7a-152">Proceso de alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="92b7a-152">High performance compute</span></span>](sizes-hpc.md)



